---
title: Setup an R-Package with Rcpp in RStudio
date created: 2021-11-06T00:00:00.000Z
date updated: '2021-11-24'
---

# Setup an R-Package with Rcpp in RStudio

### Prerequisites

**Windows**

- [Install and setup R, RStudio, Rcpp](Install%20and%20setup%20R,%20RStudio,%20Rcpp.md)

`install.packages(c("Rcpp", "devtools"))`

### 0.  File -> New Project -> ... -> Package using Rcpp

### 1. Create R/package.R file

- create R/package.R file
- run

`usethis::use_rcpp()`
and add the lines suggested usethis to your R/package.R file

### 2. Git Setup

`usethis::use_git()`

### 3. Open and edit DESCRIPTION file to your needs

### 4. Add a license

`usethis::use_gpl3_license(name = "Sebastian Hanss")`

### 5. add a Readme.md

`usethis::use_readme_md()`

### 6. setup unit tests in R

`usethis::use_testthat()`

### 7. setup roxygen for NAMESPCE and documentaion

- overwrite your NAMESPACE file:

`usethis::use_namespace()`

- allow Markdown in your documentation

`usethis::use_roxygen_md()`

### 8. Commit all changes to your local repository now

- in the Terminal:

`git add .`
`git commit -m "initial commit"`

### 9. Create a GitHub repo

#### 9a. if you don't have a GitHub access token, yet get one:

`usethis::browse_github_pat()`
`usethis::edit_r_environ() # Make sure '.Renviron' ends with a newline!`

#### 9b. create a GitHub repo:

`usethis::use_github(private = TRUE)`

### Enable Roxygen update on build

- Build tab -> More -> Configure Build Tools:

![](../attachments/Screenshot%20from%202020-02-05%2009-45-21.png)

- Check Generate documentation with Roxygen:

![](../attachments/Screenshot%20from%202020-02-05%2009-47-44.png)
I also check roxygenize on "Build and Restart" for convenience.

# Sources and further reading

- <http://r-pkgs.had.co.nz/>
- <https://www.r-bloggers.com/rcpp-and-roxygen2/>
- <https://laderast.github.io/2019/02/12/package-building-description-namespace/>

---

References: [YoMos Workshop 2020](https://github.com/selinaZitrone/YoMos2020)
Related: [[R]] [[Rcpp]]
