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

## Wave

Can be used to auto-generate containers for workflow runs (if conda is not available).

- from conda environment to containerized version
- use `wave` profile from nf-core template config (will deactivate any pre-built docker 
  or singularity containers)

## Define the report path

> Did not yet succeed in getting the report to show up in Seqera Cloud

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
