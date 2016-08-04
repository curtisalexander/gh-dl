# gh-dl
Download an R package as a tarball from Github.

## Requirements
Makes use of `docopt`, `httr`, and `purrr`.  And makes use of `devtools` in order to install `docopt`.

```R
devtools::install_github("docopt/docopt.R")
install.packages("httr")
install.packages("purrr")
```

## Usage

```bash
gh-dl --user=<user> --pkg=<pkg> --path=<path>
gh-dl -h | --help
```

## Options

```bash
--user=<user>   Github username
--pkg=<pkg>     R package name
--path=<path>   Directory path to save tar.gz file
-h, --help      Help
```

## Example

```bash
gh-dl --user=rstudio --pkg=sparklyr --path="~/code/r-pkgs"
```

## Use Case
When working on particular servers, I do not have the ability to install packages from Github.  The only way to install a package is to download the package as a `tar.gz` file from a different machine, copy it to the server, and perform a local install on the server.

I typically save the latest version of a package as a `tar.gz` file in a common directory.  This allows me to execute code similar to that below to install the package.

The code below will also allow me to install a locally developed package without needing to remember the exact version number. I simply replace the locally developed package in the directory with the latest version.

```R
# install sparklyr package
pkg_dir <- "~/code/r-pkgs"
tgz_file <- list.files(path = pkg_dir,
                       pattern = "^sparklyr",
                       recursive = FALSE)
pkg <- file.path(pkg_dir, tgz_file)
devtools::install_local(pkg)
```

## Caveats
As of *2016-07-29*, I don't believe this is necessary anymore due to the `httr` package making use of the `curl` package for HTTPS downloads.  I will verify and then remove the unneeded code and the entry below here in the `README.md`.

---

I have need to use a [custom certificate](https://github.com/curtisalexander/til/blob/master/R/custom-cert.md) in order to download packages using `httr`.  If you have a similar need, then create a variable in `.Renviron` named `HTTR_CAINFO` which points to your CA file.  For my needs, I have an entry in `.Renviron` that looks like the following.

```
HTTR_CAINFO=/Users/username/.cert/ca-bundle.crt
```
