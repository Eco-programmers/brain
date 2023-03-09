---
title: Install and setup R, RStudio, Rcpp
date created: 2021-11-06T00:00:00.000Z
date updated: '2021-11-24'
---

# Install and setup R, RStudio, Rcpp

## Ubuntu

The `R` version in the Ubuntu repositories is usually outdated. I therefore recommend to use CRAN's Ubuntu repository:

```bash
sudo apt install --no-install-recommends software-properties-common dirmngr

wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc

sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
```

Then install R, Rcpp and RInside:

```
sudo apt-get update
sudo apt-get install r-base r-base-dev r-cran-rinside r-cran-rcpp
```

To install RStudio download the *.deb file from <https://rstudio.com/products/rstudio/download/#download> and install it.

## Windows

### 1. Install R

- Download R from <https://cran.r-project.org/bin/windows/base/>
- Install R in a directory with no fancy characters in its path, e.g. `C:\R\R-4.1.2` is safe
  - Accept all defaults

### 2. Install RTools

Rtools provides a compiler and some helpers to compile code for R in Windows. Download Rtools from here: <https://cran.r-project.org/bin/windows/Rtools/> and select the appropriate Rtools version (4.0 with R 4.x.x)

Install Rtools in a directory with no fancy characters in its path, e.g. `C:\R\Rtools` is safe. To install, right click on the `Rtools40.exe` and select “Run as administrator”. During the installation make sure to select "Add Rtools to PATH". Otherwise, accept all defaults for everything else.

### 3. Install RStudio

- Download RStudio from https://rstudio.com/products/rstudio/download/#download
- Install R in a directory with no fancy characters in its path, e.g. `C:\R\RStudio` is safe

### 4. Install Rcpp & RInside

- in RStudio: `install.packages(c("RInside", "Rcpp"))`

---

References: https://cran.r-project.org/bin/linux/ubuntu/
Related: 
