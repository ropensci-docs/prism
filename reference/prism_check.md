# Check if prism files exist

Helper function to check if files already exist in the prism download
directory. Determines if files have **not** been downloaded yet, i.e.,
returns `TRUE` if they do not exist.

## Usage

``` r
prism_check(prismfiles, lgl = FALSE, pre81_months = NULL)
```

## Arguments

- prismfiles:

  a list of full prism file names ending in ".zip".

- lgl:

  `TRUE` returns a logical vector indicating those not yet downloaded;
  `FALSE` returns the file names that are not yet downloaded.

- pre81_months:

  Numeric vector of months that will be downloaded, if downloading data
  before 1981. This is so that the existence of the data can be
  correctly checked, as the file includes all monthly data for a given
  year.

## Value

a character vector of file names that are not yet downloaded or a
logical vector indication those not yet downloaded.
