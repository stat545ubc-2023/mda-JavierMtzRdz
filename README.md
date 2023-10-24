# mda-project-template

## Author

Javier Martinez-Rodriguez

## Description

This repository contains the exploratory analysis of the `vancouver_trees` dataset sourced from The City of Vancouver's Open Data Portal. The analysis delves into various aspects of the urban street trees across different neighborhoods.

### Repo Contents

The tree diagram below illustrates the structure of this repository. In brief, the `mini-project-1` folder contains the initial phase of the exploratory analysis on the `vancouver_trees` dataset, the `mini-project-2` folder holds the analysis of the main research questions and the `output` folder has the documents generated as a result of the mini EDA.

```bash
.
|____.here
|____output
| |____root_b_count.csv
| |____README.md
| |____model.rds
|____mini-project-1
| |____mini-project-1_files
| | |____figure-gfm
| | | |____unnamed-chunk-8-1.png
| | | |____unnamed-chunk-10-1.png
| | | |____unnamed-chunk-7-1.png
| |____mini-project-1.md
| |____README.md
| |____mini-project-1.Rmd
|____README.md
|____.gitignore
|____mini-project-2
| |____mini-project-2_files
| | |____figure-gfm
| | | |____unnamed-chunk-8-1.png
| | | |____unnamed-chunk-10-1.png
| | | |____unnamed-chunk-10-2.png
| | | |____unnamed-chunk-10-3.png
| | | |____unnamed-chunk-4-1.png
| | | |____unnamed-chunk-13-1.png
| | | |____unnamed-chunk-6-1.png
| |____README.md
| |____mini-project-2.md
| |____mini-project-2.Rmd

```

## How to Run Code from This Repository

### Pre-requisites
1. Ensure you have R and RStudio installed on your computer. Download R from [CRAN](https://cran.r-project.org/) and RStudio from [rstudio.com](https://www.rstudio.com/).

### Steps

#### Clone the Repository using RStudio
1. Launch RStudio.
2. Go to `File -> New Project`.
3. Choose `Version Control`.
4. Select `Git`.
5. In the "Repository URL" field, paste the URL of the GitHub repository.
6. Choose where to save the repository in the "Create project as subdirectory of" field.
7. Click `Create Project`.

#### Install Required Packages
1. Open the R console within RStudio.
2. Run the following code on the console. 
```
install.packages("tidyverse")
install.packages("ggridges")
install.packages("ggdist")
install.packages("scales")
install.packages("ggrepel")
install.packages("here")
install.packages("devtools")
devtools::install_github("UBC-MDS/datateachr")
```

#### Run the Code
1. If the code is in an R script, you can run it by clicking `Source`.
2. If the code is in an R Markdown file, you can knit the document by clicking the `Knit` button.

#### Troubleshooting
- If you encounter errors or missing packages, the error messages usually provide clues about what's missing or what needs to be fixed.
