# Subsets PRISM folders on the disk

`prism_archive_subset()` subsets the PRISM folders stored on disk by
type, temporal period, and date. It looks through all of the PRISM data
that have been downloaded in the prism archive
([`prism_get_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md))
and returns the subset based on the specified `type`, `temp_period`, and
dates.

## Usage

``` r
prism_archive_subset(
  type,
  temp_period,
  years = NULL,
  mon = NULL,
  minDate = NULL,
  maxDate = NULL,
  dates = NULL,
  resolution = NULL
)
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

## Value

A character vector of the folders that meet the type and temporal period
specified. `character(0)` is returned if no folders are found that meet
the specifications.

## Details

`temp_period` must be specified so the function can distinguish between
wanting annual data or wanting monthly data for a specified year. For
example `prism_archive_subset("tmean", "annual", years = 2012)` would
provide only one folder: the annual average temperature for 2012.
However, `prism_archive_subset("tmean", "monthly", years = 2012)` would
provide 12 folders: each monthly tmean folder for 2012.

`temp_period`, `years`, and `mon` can be combined in various different
ways to obtain different groupings of data. `years`, `mon`, and the
daily specifiers (`minDate`/`maxDate` or `dates`) are optional. Not
specifying any of those would result in getting all annual, monthly, or
daily data.

`minDate`/`maxDate` or `dates` should only be specified for a
`temp_period` of "daily". Additionally, only `dates`, or `minDate` and
`maxDate`, should be specified, but all three should not be specified.
Nor should the daily arguments be combined with `years` and/or `mon`.
For example, if daily folders are desired, then specify `years` and/or
`mon` to get all days for those years and months **or** specify the
specific dates using `minDate`/`maxDate` or `dates`

## See also

[`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# get all annual tmin
prism_archive_subset("tmin", "annual")
# get only 2000-2015 annual tmin at 800m resolution
prism_archive_subset("tmin", "annual", years = 2000:2015, resolution = "800m")

# get monthly precipitation for 2000-2010
prism_archive_subset("ppt", "monthly", years = 2000:2010)
# get only June-August monthly precip data for 2000-2010 at 4km resolution
prism_archive_subset("ppt", "monthly", years = 2000:2010, mon = 6:8, resolution = "4km")

# get all daily tmax for July-August in 2010
prism_archive_subset("tmax", "daily", years = 2010, mon = 7:8)
# get 800m daily tmax for July-August in 2010
prism_archive_subset("tmax", "daily", years = 2010, mon = 7:8, resolution = "800m")
# same as:
prism_archive_subset(
  "tmax", 
  "daily", 
  minDate = "2010-07-01", 
  maxDate = "2010-08-31",
  resolution = "800m"
)

# get the 4km 30-year average precip for January and February
prism_archive_subset("ppt", "monthly normals", mon = 1:2, resolution = "4km")
} # }
```
