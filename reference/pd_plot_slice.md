# Plot a slice of a raster stack

`pd_plot_slice()` plots a slice of data at a single point location from
the specified prism data.

`prism_slice()` is the deprecated version of `pd_plot_slice()`.

## Usage

``` r
pd_plot_slice(pd, location)

prism_slice(location, prismfile)
```

## Arguments

- pd, prismfile:

  a vector of output from
  [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
  or
  [`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)
  giving a list of prism files to extract data from and plot. The latter
  is preferred as it will help ensure the prism data are from the same
  variable and temporal period.

- location:

  a vector of a single location in the form of long,lat

## Value

A `gg` object of the plot for the requested `location`.

## Details

The user should ensure the prism data comes from a continuous data set
and is made up of the same temporal period. Otherwise the plot will look
erratic and incorrect.

## Examples

``` r
if (FALSE) { # \dontrun{
### Assumes you have a clean prism directory
get_prism_dailys(
  type="tmean", 
  minDate = "2013-06-01", 
  maxDate = "2013-06-14",
  keepZip = FALSE
)
p <- pd_plot_slice(
  prism_archive_subset("tmean", "daily", year = 2020), 
  c(-73.2119,44.4758)
)
print(p)
} # }
```
