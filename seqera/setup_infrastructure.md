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
