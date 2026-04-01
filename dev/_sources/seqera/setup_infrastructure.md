# Setup Azure batch compute environments

Based on our discussion and the 
[documentation](https://docs.seqera.io/platform/24.2/enterprise/advanced-topics/manual-azure-batch-setup)
and [FAQ](https://docs.seqera.io/platform/24.2/troubleshooting_and_faqs/azure_troubleshooting#batch-compute-environments)


## Setup Permissions

Here are the key points with setting up Azure Infrastructure using 
a Managed Identity and Batch Pool.

### On Azure

- Create a service principal
- Create a managed identity
- Assign roles to the service principal and managed identity
- Increase quota for the Azure Batch Account
- Create Azure Batch pools in the Batch account
- Attach nodes to the virtual network in the right subnet
- Whitelist internet access on the subnet.

### On Seqera Platform within a workspace:

- Admin permissions to add credentials, compute environment(s) and pipelines to a workspace 

## On VMs as nodes in a pool
Nodes in a pool are described based on the VM naming convention:

![Name breakdown VM](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/media/size-series-breakdown.png)

See also [Azure Batch documentation](https://learn.microsoft.com/en-us/azure/batch/nodes-and-pools).

> Local storage of a VM is one-to-one in line with the number of CPUs. See the `Local Storage` tab
> for a machine in a series to find out more. See for example the
> [Ddsv4 sizes series](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/general-purpose/ddsv4-series?tabs=sizestoragelocal).

## Spreading vs Packing nodes in a pool

Defines how jobs are packed on nodes. Packing puts as many tasks as possible on a single
node. Spreading startes new nodes for each task per default. See the documentation for
 more details:
[azure/batch/batch-parallel-node-tasks](https://learn.microsoft.com/en-us/azure/batch/batch-parallel-node-tasks)

## Troubleshooting

### Connection issues

If you encounter connection issues when launching pipelines from Seqera using 
Azure Batch compute environment, try to increase the timeout settings in the
Compute Environment configuration on Seqera Platform to around 8-16 hours.

```
NXF_OPTS="-Dsun.net.client.defaultConnectTimeout=30000 -Dsun.net.client.defaultReadTimeout=60000"
```

Here are some example screenshots for setting it as global Environment variables

![Timeout settings in Compute Environment](assets/seqera_compute_env_0.png)
![Timeout settings in Compute Environment](assets/seqera_compute_env_1.png)

So you will need to set the `NXF_OPTS` environment variable in the Compute Environment 
configuration on Seqera Platform to

```
-Dsun.net.client.defaultConnectTimeout=30000 -Dsun.net.client.defaultReadTimeout=60000
```

<details>
<summary>Example error message:</summary>

```bash
The workflow execution failed to start. Exit status: 1

ERROR ~ Unable to access config file 'https://api.cloud.seqera.io/ephemeral/UZw1-XJW1qKNEQagE6yUuA' -- Cause: Server returned HTTP response code: 403 for URL: https://api.cloud.seqera.io/ephemeral/UZw1-XJW1qKNEQagE6yUuA

  Server returned HTTP response code: 403 for URL: https://api.cloud.seqera.io/ephemeral/UZw1-XJW1qKNEQagE6yUuA


 -- Check 'nf-2OSwVxmg7B2QQt.log' file for details
```
 </details>


### VM sizes

To handle workflows with a mix of low and high memory requirements, consider
to let Seqera create multiple Azure Batch pools with different VM sizes based
on process requirements. This can be achieved by using the `autopool` feature.

- See [nextflow documentation](https://www.nextflow.io/docs/latest/azure.html#auto-pools)
- See [Seqera documentation](https://docs.seqera.io/platform-cloud/enterprise/advanced-topics/manual-azure-batch-setup#option-4-use-the-nextflow-autopool-feature)

