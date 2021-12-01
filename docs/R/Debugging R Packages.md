---
title: Debugging R Packages
date created: 2021-11-30T00:00:00.000Z
date updated: '2021-12-01'
---

# Debugging R Packages

[Debugging R](https://adv-r.hadley.nz/debugging.html) code is is normally quite straight forward and RStudio offers [useful tools](https://support.rstudio.com/hc/en-us/articles/205612627-Debugging-with-the-RStudio-IDE). But when you have to debug R packages with compiled code it becomes more complicated. For C++ code, you might want to use an external debugger [like Qt Creator with gdb](Setup%20Qt%20Creator%20to%20develop%20Rcpp.md), for example.

Sometimes, especially when the bug affects the interface between R and your compiled code, R just crashes or behaves funny when using your package.  Then you need to check your package with particular R variants

The package to be tested is assumed to be in `$PWD/spectre` for this example.

## Start the Docker container

[Winston Chang](https://github.com/wch) provides a very useful [Docker image for debugging R memory problems](https://github.com/wch/r-debug) which I recommend to use:

```bash
docker run -v $PWD:/src:ro -it --rm --security-opt seccomp=unconfined wch1/r-debug
```

This container provides different variants of `R` (copied from the [image readme](https://github.com/wch/r-debug)):

- `R` The current release version of R.
- `RD` The current development version of R (R-devel). This version is compiled without optimizations (-O0), so a debugger can be used to inspect the code as written, instead of an optimized version of the code which may be significantly different.
- `RDvalgrind`: R-devel compiled with valgrind level 2 instrumentation. This should be started with RDvalgrind -d valgrind.
- `RDsan`: R-devel compiled with gcc, Address Sanitizer and Undefined Behavior Sanitizer.
- `RDcsan`: R-devel compiled with clang, Address Sanitizer and Undefined Behavior Sanitizer.
- `RDstrictbarrier`: R-devel compiled with --enable-strict-barrier. This can be used with gctorture(TRUE), or gctorture2(1, inhibit_release=TRUE).
- `RDthreadcheck`: R-devel compiled with -DTHREADCHECK, which causes it to detect if memory management functions are called from the wrong thread.

*Note that you'll have to install packages separately for each build of R.*

## Install dependencies

Once, you started the Docker container, you might need to install system dependencies like so:

```bash
add-apt-repository ppa:ubuntugis/ubuntugis-unstable
apt update && apt upgrade -y && apt install -y libgfortran-10-dev libudunits2-dev libgdal-dev libgeos-dev libproj-dev 
```

You can install the R package and its dependencies either within each R variants or via the command line for all R variants, here is an example:

```r
# !!!NO SPACES!!!
install="install.packages(c(\"testthat\",\"devtools\",\"roxygen2\",\"remotes\",\"covr\",\"Rcpp\"))"
remotes_install="remotes::install_github(\"git@github.com:ropensci/NLMR.git\",dependencies=TRUE)"
```

Repeat for each variant of `R` you are going to use, i.e. for all R variants just copy and paste the following block (not line-by-line) to the command line in the Docker container:

```bash
R -e $install && R -e $remotes_install &&
RD -e $install && RD -e $remotes_install &&
RDvalgrind -e $install && RDvalgrind -e $remotes_install &&
RDsan -e $install && RDsan -e $remotes_install &&
RDcsan -e $install && RDcsan -e $remotes_install &&
RDstrictbarrier -e $install && RDstrictbarrier -e $remotes_install &&
RDthreadcheck -e $install && RDthreadcheck -e $remotes_install
```

## Run tests

Again, you can start interactive R sessions for each R variant or run the tests from the command line. Here is an example for `NLMR`, adjust to your needs:

```bash
mkdir -p NLMR_checks && cd NLMR_checks &&
mkdir -p R && cd R &&
R -e 'tools::testInstalledPackage("NLMR")' &&
mkdir -p ../RD && cd ../RD &&
RD -e 'tools::testInstalledPackage("NLMR")' &&
mkdir -p ../RDvalgrind && cd ../RDvalgrind &&
RDvalgrind -e 'tools::testInstalledPackage("NLMR")' &&
# RDsan probably fails due to https://github.com/google/sanitizers/issues/856
# mkdir -p ../RDsan && cd ../RDsan &&
# RDsan -e 'tools::testInstalledPackage("NLMR")' &&
mkdir -p ../RDcsan && cd ../RDcsan &&
RDcsan -e 'tools::testInstalledPackage("NLMR")' &&
mkdir -p ../RDstrictbarrier && cd ../RDstrictbarrier &&
RDstrictbarrier -e 'tools::testInstalledPackage("NLMR")' &&
mkdir -p ../RDthreadcheck && cd ../RDthreadcheck &&
RDthreadcheck -e 'tools::testInstalledPackage("NLMR")' &&
cd ../..
```

To run functions without debug output, in this example `NLMR::nlm_fbm(50, 100, fract_dim = 1.2)`, you can redirect the output and errors to files:

```bash
mkdir -p NLMR_checks && cd NLMR_checks &&
mkdir -p R && cd R &&
R -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
mkdir -p ../RD && cd ../RD &&
RD -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
mkdir -p ../RDvalgrind && cd ../RDvalgrind &&
RDvalgrind -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
# RDsan probably fails due to https://github.com/google/sanitizers/issues/856
# mkdir -p ../RDsan && cd ../RDsan &&
# RDsan -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
mkdir -p ../RDcsan && cd ../RDcsan &&
RDcsan -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
mkdir -p ../RDstrictbarrier && cd ../RDstrictbarrier &&
RDstrictbarrier -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
mkdir -p ../RDthreadcheck && cd ../RDthreadcheck &&
RDthreadcheck -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> out.txt 2> err.txt &&
cd ../..
```

`1>` is the redirect for normal outputs, `2>` redirects errors.

## Valgrind

[Valgrind](https://valgrind.org/) is a powerful tool for memory debugging.

```bash
mkdir -p NLMR_checks && cd NLMR_checks &&
RDvalgrind -d valgrind -e 'devtools::test("NLMR", reporter = testthat::LocationReporter)' 1> valgrind_results.txt 2> valgrind_errors.txt &&
cd ..
```

or for a single function:

```bash
mkdir -p NLMR_checks && cd NLMR_checks &&
RDvalgrind -d valgrind -e 'NLMR::nlm_fbm(50, 100, fract_dim = 1.2)' 1> valgrind_fmb_results.txt 2> valgrind_fbm_errors.txt &&
cd ..
```

## Save results

The results are all saved in the folder `NLMR_checks` in the examples used above. So let's first zip it:

```bash
zip -r NLMR_checks.zip NLMR_checks
```

Then, open a new terminal on your computer (do leave the terminal with Docker running) and copy the zip file to your local machine with `docker cp`:

```bash
docker cp <Container ID>:<Path of file inside the container> <Path in the local machine>
```

For example:

```bash
docker ps # to get the Container ID 67bb4dabd1bd
docker cp 67bb4dabd1bd:/root/NLMR_checks.zip ./
```

The zip file will be owned by root, because you need to be root to run `docker`. To change the ownership to your current user, run:

```bash
sudo chown $USER:$USER NLMR_checks.zip 
```

---

References: <https://reside-ic.github.io/blog/debugging-and-fixing-crans-additional-checks-errors/>
Related:
