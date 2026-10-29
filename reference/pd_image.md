# Quick spatial image of prism data

`pd_image()` makes a spatial image plot of the specified prism data
(single variable and time step.). It is meant for rapid visualization,
but more detailed plots will require other methods.

`prism_image()` is the deprecated version of `pd_image()`.

## Usage

``` r
pd_image(pd, col = "heat")

prism_image(prismfile, col = "heat")
```

## Arguments

- pd, prismfile:

  the name of a single file to be plotted, this is most easily found
  through
  [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
  or
  [`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).

- col:

  the color pattern to use. The default is heat, the other valid option
  is "redblue".

## Value

Invisibly returns `gg` object of the image.

## See also

[`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md),
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md),
[`ggplot2::geom_raster()`](https://ggplot2.tidyverse.org/reference/geom_tile.html)

## Examples

``` r
if (FALSE) { # \dontrun{
get_prism_dailys(
  type = "tmean",
  minDate = "2013-06-01",
  maxDate = "2013-06-14",
  keepZip = FALSE
)

# get June 5th
pd <- prism_archive_subset("tmean", "daily", dates = "2013-06-05")

# and plot it
pd_image(pd)
} # }
```
