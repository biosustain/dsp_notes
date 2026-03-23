# Building a custom nf-core analysis pipeline

These descriptions are based on the custom pipeline
[dsp_demo_nf_acore_vuegen](https://github.com/biosustain/dsp_demo_nf_acore_vuegen)
which is used to highlight how an analysis notebook
based on acore can be integrated with a report based on vuegen.

It is based on the nf-core `tools` and their template for a nextflow repository, see:
[nf-core/tools](https://github.com/nf-core/tools/tree/main/nf_core/pipeline-template).

## Using the template

The instructions are brief on their [website](https://nf-co.re/docs/guidelines/pipelines/requirements/use_the_template).
Follow the command line instructions. Per default it is based on genomics data showing
a fastqc analysis pipeline.

- can be customized to have a prefix, e.g. `dsp-` instead of `nf-core-`. See
  [customization options](https://nf-co.re/docs/nf-core-tools/pipelines/create#customization)
  of `nf-core pipelines create` command. Set `--organization dsp` to have `dsp-` prefix.
- pipeline structure explained
  [here](https://nf-co.re/docs/contributing/pipelines/pipeline_file_structure)
- an input schema (e.g. a SDRF file) can be defined using the
  [schema-tutorial](https://nextflow-io.github.io/nf-schema/latest/nextflow_schema/create_schema/).
  The default pipeline has as single input a csv sample sheet, and an output directory.

## Make adaptions to the pipeline created from the template

- edit the schema and remove the parameters which are not needed:
  `nf-core pipelines schema build`

- then try to get it to run

## Add modules and subworkflows

Using the `nf-core modules` or `nf-core subworkflows` command, you can add modules
or entire subworkflows to your pipeline, enabling you to augment pre-existing pipelines
with new functionality before or after the existing workflow.

### Deviate from existing modules (patch)

Patching allows you to create a modified version of an existing module, which can be
useful if you want to make small changes to an existing module without having to create
a new one from scratch. You can use the `nf-core modules patch` command to create a
patch for an existing module, which will allow you to modify the module's code while
still keeping track of the original version and allowing you to still update with new
changes.

- make custom adjustments
- still have the option to incorporate updates from the original module (or subworkflow)

For example for `thermorawfileparser` module in `bigbio/nf-modules`, you can 
pull install and patch and then update it with the latest changes:

```bash
nf-core modules --git-remote https://github.com/bigbio/nf-modules.git install thermorawfileparser
nf-core modules --git-remote https://github.com/bigbio/nf-modules.git patch thermorawfileparser
# a while later after updates were made to bigbio/nf-modules/thermorawfileparser, 
# you can pull the latest changes and update your patched version:
nf-core modules --git-remote https://github.com/bigbio/nf-modules.git update thermorawfileparser
```

On patching
 - [video](https://www.youtube.com/watch?v=7pu6Ikhi1eU)
 - [docs](https://nf-co.re/docs/nf-core-tools/modules/patch)

## Lint

Check for errors and warnings:

```bash
nf-core pipelines lint .
```

## Test

You will need to add basic test of the pipeline.

## Wave

Can be used to auto-generate containers for workflow runs (if conda is not available).

- from conda environment to containerized version
- use `wave` profile from nf-core template config (will deactivate any pre-built docker
  or singularity containers)
- allows also to specify a custom container registry, e.g. `ghcr.io/biosustain`
  for privatly hosted containers in Seqera Platform (which executes it then on
  Azure), see
  [here](https://docs.seqera.io/platform-cloud/credentials/container_registry_credentials).

## Define the report path

> The file has to be linked in a process output explicitly, not just the folder,
> i.e. `reports` as output path would
> not display a report in `reports/myreport.html`, but `reports/myreport*` would.

Custom report can be added, e.g. from VueGen, to the
[reports tab](https://docs.seqera.io/platform-cloud/reports/overview/#configure-reports).
in Seqera Cloud using the `tower.yml` configuration file.

```yaml
# tower.yml
reports:
  multiqc_report.html:
    display: "MultiQC HTML report"
  quarto_report.html:
    display: "VUEGen HTML report"
```

## Hints

- the example was moved from a course repository to its separate repository
  [dsp_demo_nf_acore_vuegen](https://github.com/biosustain/dsp_demo_nf_acore_vuegen)
  in order to make it executable on Seqera Cloud. The initial history can be found
  [here](https://github.com/biosustain/dsp_course_proteomics_intro/pull/18).

### Commit without formatting errors

- use the `pre-commit` hooks for formatting on all files:

  ```bash
  pip install pre-commit
  pre-commit install
  # then only this is needed after installing the hooks:
  pre-commit run --all-files
  ```
