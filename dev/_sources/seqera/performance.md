# Utilizing Flexible Compute Resources

The Seqera Platform allows for the allocation of different compute
resources to specific processing queues using the `process.queue`
directive within the Nextflow configuration. he following
resources offer detailed guidance on optimizing workloads on
Azure Batch.

## Optimizing Nextflow on Azure Batch

-   [RNA sequencing analysis on Azure using
    Nextflow](https://techcommunity.microsoft.com/blog/healthcareandlifesciencesblog/rna-sequencing-analysis-on-azure-using-nextflow-configuration-files-and-benchmar/3738854)

-   [Low-priority versus dedicated machines in
    Nextflow](https://techcommunity.microsoft.com/blog/healthcareandlifesciencesblog/rna-sequencing-analysis-on-azure-using-nextflow-low-priority-vs-dedicated-machin/3774742)

## Autopools Feature in Nextflow

The Nextflow workflow engine includes an autopools feature that can
dynamically create and destroy worker pools based on process-specific
requirements. Additional details can be found in the following
resources:

-   [Example Compute Environment in Seqera
    Cloud](https://cloud.seqera.io/orgs/DTU-Biosustain/workspaces/seqera_test/compute-envs/40jbXmCxtOnjF21HLn4ZiR)

-   [Nextflow Autopools
    Documentation](https://www.nextflow.io/docs/latest/azure.html#autopools)
