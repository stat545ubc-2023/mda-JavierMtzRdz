# mda-project-template

## Author

Javier Martinez-Rodriguez

## Description

This repository contains the exploratory analysis of the `vancouver_trees` dataset sourced from The City of Vancouver's Open Data Portal. The analysis delves into various aspects of the urban street trees across different neighborhoods.

### Repo Contents

* The analysis can be found in `mini-project-1.Rmd`
* The knitted document is `mini-project-1.md`
* The folder `mini-project-1_files` contains the files needed to visualize `mini-project-1.md`. So far, it contains the plots of every chunk. 

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
install.packages("scales")
install.packages("ggrepel")
install.packages("devtools")
devtools::install_github("UBC-MDS/datateachr")
```

#### Run the Code
1. If the code is in an R script, you can run it by clicking `Source`.
2. If the code is in an R Markdown file, you can knit the document by clicking the `Knit` button.

#### Troubleshooting
- If you encounter errors or missing packages, the error messages usually provide clues about what's missing or what needs to be fixed.
