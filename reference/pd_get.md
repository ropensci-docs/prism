# Perform action on "prism data"

`pd_get_name()` extracts a long, human readable name from the prism
data.

`pd_get_date()` extracts the date from the prism data. Date is returned
in yyyy-mm-dd format. For monthly data, dd is 01 and for annual data mm
is also 01. For normals, an empty character is returned.

`pd_get_type()` parses the variable from the prism data.

`prism_md()` is a deprecated function that has been replaced with
`pd_get_name()` and `pd_get_date()`

`pd_to_file()` converts prism data to a fully specified .bil file, i.e.,
the full path to the file in the prism archive. A warning is posted if
the file does not exist in the local prism archive.

## Usage

``` r
pd_get_name(pd)

pd_get_date(pd)

pd_get_type(pd)

prism_md(f, returnDate = FALSE)

pd_to_file(pd)
```

## Arguments

- pd:

  prism data character vector.

- f:

  1 or more prism directories name or .bil files.

- returnDate:

  TRUE or FALSE. If TRUE, an ISO date is returned. By default years will
  come back with YYYY-01-01 and months as YYYY-MM-01

## Value

`pd_get_name()` and `pd_get_date()` return a character vector of
names/dates.

`pd_get_type()` returns a character vector of prism variable types,
e.g., 'ppt'.

`pd_to_file()` returns a character vector with the full path to the bil
file.

## Details

"prism data", i.e., `pd` are the folder names returned by
[`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
or
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).
These functions get the name or date from these data, or convert these
data to a file name.

## Examples

``` r
if (FALSE) { # \dontrun{
# Assumes 2000-2002 annual precipitation data is already downloaded
pd <- prism_archive_subset('ppt', 'annual', years = 2000:2002)
pd_get_name(pd)
## [1] "2000 - 4km resolution - Precipitation" "2001 - 4km resolution - Precipitation"
## [3] "2002 - 4km resolution - Precipitation"

pd_get_date(pd)
## [1] "2000-01-01" "2001-01-01" "2002-01-01"

pd_get_type(pd)
## [1] "ppt" "ppt" "ppt"

pd_to_file(pd[1])
## [1] "C:/prismdir/PRISM_ppt_stable_4kmM3_2000_bil/PRISM_ppt_stable_4kmM3_2000_bil.bil"
} # }
```
