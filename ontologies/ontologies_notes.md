# Ontology Development Kit (ODK) Crash Course

Aim: To kickstart your journey into using the ODK, providing the foundations on which further development can be done

Goals: 
    - You understand the what the ODK is and how to use it in ontology development
    - You are able to handle basic editing of the PREFER ontology using the ODK 
    - You know how to find documentation and help if you need it in the future

## Prerequisites

1. Download and install [GitHub Desktop](https://desktop.github.com/) if you are unfamiliar with git commands.
1. Download and install [Protege](https://protege.stanford.edu/software.php#desktop-protege). See instructions on how to set up Protege [here](../howto/set-up-protege.md)
1. Install [ELK reasoner in protege](../howto/installing-elk-in-protege.md) if your version does not already come with it
1. [Setting up ODK](../howto/odk-setup.md)

## Day 1 Agenda

### OBO Community 

- Documentation developed by the OBO community can be found in the [OBOOK](https://oboacademy.github.io/obook/)
- OBO community communicates through [slack](https://obo-communitygroup.slack.com/) (if you need an invite to join, please send an email to shawntanzk@outlook.com)

### Introduction to Ontologies

1. [Basic intro to ontologies](https://oboacademy.github.io/obook/explanation/intro-to-ontologies/)
2. Modelling: [Logical Axioms](https://oboacademy.github.io/obook/explanation/logical-axiomatization/) & [Object Properties](https://oboacademy.github.io/obook/lesson/modelling-with-object-properties/) 

Further reading for modelling:

1. Understanding existential restrictions through [this explainer](https://oboacademy.github.io/obook/explanation/subClassOf-vs-equivalentTo/) and this explainer(https://oboacademy.github.io/obook/explanation/existential-restrictions/)
2. if you want some really indepth modelling tutorial, see FHKB tutorial [here](https://oboacademy.github.io/obook/tutorial/fhkb/))



### Ontology Development Kit Basics

The Ontology Development Kit (ODK) provides a set of standardized, customizable and automatically executable workflows, and packages all required tooling in a single Docker image. 

Key Features: 

1. Standardised layout for repos to minimise time finding files. 
2. Standardised workflows which allow users to work with other ontologies without relearning processes.
3. Dynamic import to allow users to easily mantain terms imported from other ontologies.  

#### Anatomy of an ODK ontology 

All ODK repos have standard file layout. The key files you should know are

1. `src/ontology/ont.yaml` - the config file which ODK reads to build your repo 
2. `src/ontology/ont-edit.owl` - the file that you should edit on 
3. `src/ontology/ont.makefile` - custom code that the repo uses that defers from vanilla ODK 
4. `src/ontology/imports/ont.txt` - files to add ontology terms to be imported 
5. `src/ontology/profile.txt` - configuration of QC reports/checks 

Other files will be covered as needed.

#### Creating your ODK ontology 

Tutorial can be found [here](https://oboacademy.github.io/obook/tutorial/setting-up-project-odk/) - if you already have an ontology and want to migrate it, you can move the terms ot the edit file after initialising your ODK ontology. 

### How to edit in protégé

1. [Editing a term in protege](https://oboacademy.github.io/obook/howto/edit-in-protege/) - remember, let the reasoner do the work!
2. [Creating a new term in protege](https://oboacademy.github.io/obook/howto/create-new-term/)
3. [Obsoleting a term in protege](https://oboacademy.github.io/obook/howto/obsolete-term/)
4. [Merging a term in protege](https://oboacademy.github.io/obook/howto/merge-terms/)

## Day 2 Agenda

### Managing Imports with ODK 

A key function of the ODK is the handle dynamic imports. To avoid clashes in imports, I would reccomend using merged imports in the ODK. Here is an example of what you should add to your yaml config file: 

```yaml
import_group:
  use_base_merging: TRUE
  products:
    - id: ro
      use_base: TRUE
```

The ODK mantains a set of ontology shorthands where you can just use the id and add use_base, and it will automatically work. However, in certain cases, you need to define where the mirror is from (where to download the ontology file), ask the ODK to make a base file where a base file is not available, and/or define what the base IRI are. An example would look like: 

```yaml
    - id: bao
      mirror_from: http://www.bioassayontology.org/bao/bao_complete.owl
      make_base: TRUE
      base_irirs:
        - http://www.bioassayontology.org/
```
There are some ontologies (eg chebi and NCBITaxon) which are huge, please look at [this document](https://oboacademy.github.io/obook/howto/deal-with-large-ontologies/) for managing such ontologies. 

Once you have configured your imports and update your repo using `sh run.sh make update_repo`, you should see .txt files in your src/ontology/imports folder. To import terms to your ontology, add them into the .txt file, and run `sh run.sh make imports/merged_import.owl`. This will download the mirrors, extract out terms relavent to what you have added, and merge all subgraphs into merged_import.owl. 

From there you can use the imported terms in your edit file.

### Hands on Tutorial

1. Clone https://github.com/EBISPOT/ontology_editor_training/
2. Given that 'Chardonnay wine' is a generic names for wines made from Chardonnay (varietal) grapes, add a term for Chardonnay (wine) with an appropriate logical definition. 
    - What does the reasoner classify as Chardonay?
3.View the relationships (subClassOf axioms) of Chianti (wine). How might these frustrate attempts to classify wines using the pattern you just used to define Chardonay wine?
4. Add a term for [Rosé wine](https://en.wikipedia.org/wiki/Ros%C3%A9) or [orange wine](https://en.wikipedia.org/wiki/Orange_wine) and some terms for specific wines that will be auto-classified under it. 
5. Add an import for [the food ontology](https://github.com/FoodOntology/foodon) to the ODK repo, and import FOODON:00002364 and replace wine with the FOODON term for wine 

### Release Management

The newer version of ODK utilises github releases rather that uploading everything directly to github. This change was made to deal with ever larger ontologies and the limitations of how much can be hosted on a github repo. 

For release management workflow, please utilise [the workflow shown in CL documentation](https://github.com/obophenotype/cell-ontology/blob/master/docs/cl-release.md) and update it for your ontology. 
