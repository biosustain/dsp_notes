# Debugging jobs

If a job fails on seqera an intermediate files are lost as the VM state is not saved back
to the associated blob storage container. This makes debugging a bit more challenging,
although all relevant inputs are still normally found in the respective working directory
for a single job.

## Debugging on local machine (or any VM or HPC)

- download the relevant files
- install the required software using preferrably the method used on Seqera (docker, conda, etc.)
- run the command that failed and debug
