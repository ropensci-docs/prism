# Check the integrity of downloaded PRISM data

`prism_archive_verify()` checks the data in the prism archive to ensure
it is valid, or at least can be read into R, i.e., it is not corrupt.
The prism variable type, time period, etc. is specified the same as for
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).
Any files that are not readable can automatically be re-downloaded.

`check_corrupt()` is the deprecated version of `prism_archive_verify()`

## Usage

``` r
prism_archive_verify(
  type,
  temp_period,
  years = NULL,
  mon = NULL,
  minDate = NULL,
  maxDate = NULL,
  dates = NULL,
  resolution = NULL,
  download_corrupt = TRUE,
  keepZip = TRUE
)

check_corrupt(type, minDate = NULL, maxDate = NULL, dates = NULL)
```

## Arguments

- type:

  The type of data you want to subset. Must be "ppt", "tmean", "tmin",
  "tmax", "tdmean", "vpdmin", "vpdmax", "solclear", "solslope",
  "soltotal", or "soltrans".

- temp_period:

  The temporal period to subset. Must be "annual", "monthly", "daily",
  "monthly normals", or "annual normals".

- years:

  Valid numeric year, or vector of years.

- mon:

  Valid numeric month, or vector of months.

- minDate:

  Date to start subsetting daily data. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- maxDate:

  Date to end subsetting daily data. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- dates:

  A vector of daily dates to subset. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- resolution:

  The spatial resolution of the data, must be either "4km" or "800m".
  Required for all temporal periods.

- download_corrupt:

  If `TRUE`, then any unreadable prism data are automatically
  re-downloaded.

- keepZip:

  If `TRUE`, leave the downloaded zip files in your 'prism.path', if
  `FALSE`, they will be deleted.

## Value

`prism_archive_verify()` returns `TRUE` if all data are readable. Any
prism data that are not readable are returned (folder names), whether
they are re-downloaded or not.

`check_corrupt()` returns `logical` indicating whether the process
succeeded.

## Details

Under the hood, it uses
[`raster::stack()`](https://rdrr.io/pkg/raster/man/stack.html) and then
[`raster::rasterToPoints()`](https://rdrr.io/pkg/raster/man/rasterToPoints.html)
to determine if the bil files are readable. If both those files are able
to successfully read the files, they are assumed to be valid/readable.

## Examples

``` r
if (FALSE) { # \dontrun{
# check all annual precipitation data from 2000-2023 are readable
# x will contain any corrupt files, or be TRUE if they are all readable
x <- prism_archive_verify('ppt', 'annual', 2000:2023, resolution = "4km")
} # }

  
```
