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
