# Debugging jobs

If a job fails on seqera an intermediate files are lost as the VM state is not saved back
to the associated blob storage container. This makes debugging a bit more challenging,
although all relevant inputs are still normally found in the respective working directory
for a single job.

## View detailed logs

You can download the logs from the kebab menu on "Execution log" in the tab "Execution log". 
In the web UI only the `Nextflow console output` is shown, 
but the detailed logs can be downloaded to your local laptop for inspection. 

## Debugging on local machine (or any VM or HPC)

- download the relevant files
- install the required software using preferrably the method used on Seqera (docker, conda, etc.)
- run the command that failed and debug

## Execution steps for general understanding

The steps go as follows: 

- The previous task(s) will run and create files on a local disk 
- these are uploaded to their respective Azure Blob scratch directories

- the next task will start 
- it will download files from the scratch directories of the previous tasks
- it will run the tools specified for the task (process) 
- Once complete, it will upload the files marked as outputs
  in the nextflow process definition to the Azure Blob scratch directory (to be used again
  for another task/process as input)

From this, you can see that input files do not appear in the blob storage of the task in
the working directory. They will be downloaded to local storage, but never uploaded
at the end because they are not considered outputs. This prevents duplication of 
input/output data for every task. 

## Not enough space on the VM (local storage exceeded)

Azure virtual machines come with fixed-size disks, and when a node is
assigned multiple tasks, there is a risk of overwhelming the file
system, which can lead to pipeline failures.
As detailed in [PR 5120](https://github.com/nextflow-io/nextflow/pull/5120) there is a problem 
with leaving enough space on the VM for the local storage. This is especially relevant for
jobs which get distributed on the same VM/node with high local storage requriments, but low CPU 
requirements. For example an
[`Standard_D16ds_v4`](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/general-purpose/ddsv4-series?tabs=sizestoragelocal)
has 600GB of fixed memory. Machines with locally attached storage can be identified by the
presence of a **"d" suffix** in the machine name, such as in
`Standard_e16ds_v4`. Adding four jobs with each 4cpus and 16 GB memory but a lot of
locally stored data will might fill-up the local storage.

To mitigate this risk, two
potential solutions should be considered:

1.  **Overprovisioning** a node by allocating more CPU resources than
    strictly necessary or by reducing the number of tasks assigned to a
    single node.

2.  Using **Fusion**, which may help in optimizing storage performance.

 The total available local storage for different
machine types can be found in the following resource:

[Azure Virtual Machine Storage
Overview](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/overview)

> ⚠️ Make sure that the output directory is set to a storage account and not the local 
> disk, i.e. some `az://<container-name>` path
