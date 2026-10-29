# List available prism data

`prism_archive_ls()` lists all available prism data (all variables and
all temporal periods) that are available in the local archive, i.e.,
they have already been downloaded and are available in
[`prism_get_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md).
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)
can be used to subset the archive based on specified variables and
temporal periods.

`ls_prism_data()` is a deprecated version of `prism_data_ls()`.

## Usage

``` r
prism_archive_ls()

ls_prism_data(absPath = FALSE, name = FALSE)
```

## Arguments

- absPath:

  TRUE if you want to return the absolute path.

- name:

  TRUE if you want file names and titles of data products.

## Value

`prism_archive_ls()` returns a character vector.

`ls_prism_data()` returns a data frame. It can have 1-3 columns, but
always has the `files` column. `abs_path` and `product_name` columns are
added if `absPath` and `name` are `TRUE`, respectively.

## Details

`prism_archive_ls()` only returns the values found in the `files` column
as returned by `ls_prism_data()`. To replicate the behavior of
`ls_prism_data()`, use
[`pd_get_name()`](https://docs.ropensci.org/prism/reference/pd_get.md)
and
[`pd_to_file()`](https://docs.ropensci.org/prism/reference/pd_get.md)
with the output of `prism_archive_ls()`

## See also

[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# Get prism data names, used in many other prism* functions 
get_prism_dailys(
  type="tmean", 
  minDate = "2013-06-01", 
  maxDate = "2013-06-14", 
  keepZip = FALSE
)
prism_archive_ls()
} # }
```
