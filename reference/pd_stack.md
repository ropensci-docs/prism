# Stack prism data

`pd_stack()` creates a raster stack from prism data. It is up to the
user to ensure that `pd` is of the expected variable and temporal
period, i.e., the function does no checking and will stack data with
different variables or temporal periods.

`prism_stack()` is the deprecated version of `pd_stack()`.

## Usage

``` r
pd_stack(pd)

prism_stack(prismfile)
```

## Arguments

- pd, prismfile:

  A vector of prism data returned by
  [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
  or
  [`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).

## Value

A `RasterStack` object. Raster layers are stacked in the order they are
provided in `pd`.

## Examples

``` r
if (FALSE) { # \dontrun{
get_prism_dailys(
  type="tmean", 
  minDate = "2013-06-01", 
  maxDate = "2013-06-14", 
  keepZip = FALSE
)
# get a raster stack of June 1-14 daily tmean
mystack <- prism_stack(prism_archive_subset(
  "tmean", 
  minDate = "2013-06-01", 
  maxDate = "2013-06-14"
))
} # }
```
