# gh-dl
Download an R package as a tarball from Github.

## Requirements
Makes use of `httr` and `docopt`.

```R
install.packages("httr")
devtools::install_github("docopt/docopt.R")
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
gh-dl --user=curtisalexander --pkg=CRAmisc --path=/Volumes/Data Science/Code/R/pkgs"
```

## Caveats
I have need to use a [custom certificate](https://github.com/curtisalexander/til/blob/master/R/custom-cert.md) in order to download packages using `httr`.  I have hard coded my certificate location in the script.  Either remove or update as needed.

The line to be removed or updated is

```R
httr::set_config(httr::config(cainfo = "/Users/calexander/.cert/ca-bundle.crt"))
```
