---
title: How to setup a project (Research compendium)
date created: 2021-11-25
---
# !! Work in progress !! #WIP

## Motivation
- Reproducability -  for you and others
- easier to understand and navigate -> standardized structure
- standardized structure

## Contents
- code, raw data, results, analysis, metadata, (software) dependencies, documentation and workflow

## Basic structure for an R project

```bash
yourProject
├── raw_data      # folder contains all raw data (read-only) - modified data is in the outputs/ folder
│   └── README	  # text file which describes what is to be stored in that folder
├── DESCRIPTION   # file contains project metadata (author, date, dependencies, etc.)
├── figures       # folder contains all the figures created during the workflow
│   └── README
├── inst
│   └── CITATION  # text file with bibentry on how to cite this project
├── LICENSE.md	  # license file. No license implicitly means no-one is allowed to re-use your code
├── make.R        # file contains the complete workflow (i.e. sources all scripts from the rscripts folder in the correct order)
├── man           # folder contains documentation of the functions in the R folder
├── yourProject.Rproj # file with the RStudio project information
├── NAMESPACE	  # file 
├── outputs       # folder contains all results created by user (including modified raw data)
│   └── README
├── paper         # contains manuscript materials (biblio, templates, Rmd, etc.)
│   └── README
├── R             # R functions coded for the analysis
├── README.md	  # Project "homepage"
├── rscripts      # folder contains all analyses of the project (i.e. the steps of the workflow)
│   └── README
├── src			  # folder for other code (e.g. C++, Python, Fortran, ...)  
└── tests         # unit tests for the R-functions
    ├── testthat
    │   └── aUnitTest.R
    └── testthat.R
 ```

This structure is recognized by RStudio as an [R-Package](R-Package). This allows to `build` and even `install` your project! Also you don't need to setup this structure by hand. Either simply create an [R-Package](R-Package), with R Studio or `usethis::create_package()`

Note: use "raw_data" if you do not want to include the data to the project as you cannot exclude 'data' from the package 

## Recommended 

### Include your compute environment
- use the [renv R package](Packages/renv%20R%20package.md) to include all R packages with the respective versions in the compendium
- or put everything in a container (e.g. Docker)


### Include and manage your workflow
- use the [targets R package](Packages/targets%20R%20package.md)

### Hexstickers and Status badges
│   │   ├── hexsticker.png # always nice to have for R packages ;-)
│   │   └── lifecycle # is used to show the state of this project, important for others to decided wether or not to trust and use your work
│   │       ├── lifecycle-deprecated.svg
│   │       ├── lifecycle-experimental.svg
│   │       ├── lifecycle-stable.svg
│   │       └── lifecycle-superseded.svg

---
References: 
Related: 
