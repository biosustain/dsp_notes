# Organizing a project

## Create python package from the template

- use the template: 
  [github.com/Rasmussenlab/python_package](https://github.com/RasmussenLab/python_package)

This allows you to 
- allows to install the package in editable mode making it availabe to your interpreter
  of you environment
- have some checks running on your code automatically in GitHub Actions
- allows to easily deploy documentation to ReadTheDocs
- opt for the `src`-layout for the reasons mentioned
  [here](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/) 


## Create a `project` folder

- could also be called `notebooks` folder
- use notebooks as scripts using [papermill](https://papermill.readthedocs.io) (note that arguments can be misstyped without 
  errors - different to argparse or click scripts)
- use nextflow or Snakemake to run the scripts in analysis workflow, potentially exploring
  different parameters for certain steps and their effect on downstream analysis

## Snakemake

If you use [Snakemake](https://snakemake.readthedocs.io), you can follow the recommended repository structure (which would
be placed in the `project` folder if you use the python template):
[link](https://snakemake.readthedocs.io/en/stable/snakefiles/deployment.html)

## Nextflow

If you use [nextflow](https://nextflow.io/), you can follow the recommended repository structure (which would
again be placed in the `project` folder if you use the python template): 
[link](https://nf-co.re/docs/contributing/pipelines/pipeline_file_structure) and 
[here](https://training.nextflow.io/advanced/structure/)

## Filepaths

- use some prefixes

prefix | meaning
--- | ---
`file_` or `fpath_` | path to a file
`dir_` or `dpath_` | path to a directory

## Configs

Try to write configs for notebooks. This way it's easier to connect an aggregated or 
otherwise transformed output to the original data source.


