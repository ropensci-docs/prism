# Clean the prism data by removing early and provisional data

`prism_archive_clean()` 'cleans' the prism download data by removing
early and/or provisional data if newer (provisional or stable) data also
exist for the same variable and temporal period. Stable data are newer
than provisional data that are newer than early data; only the newest
data are kept when the "clean" is performed.

`del_early_prov()` is a deprecated version of `prism_archive_clean()`
that only works for daily data, and does not prompt the user to confirm
which folders should be removed.

## Usage

``` r
prism_archive_clean(
  type,
  temp_period,
  years = NULL,
  mon = NULL,
  minDate = NULL,
  maxDate = NULL,
  dates = NULL,
  resolution = NULL
)

del_early_prov(type, minDate = NULL, maxDate = NULL, dates = NULL)
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

Invisibly returns vector of all deleted folders.

## Details

`prism_archive_clean()` prompts the user to verify the folders that
should be removed when R is running in interactive mode. Otherwise, all
data that are identified to be older than the newest available data are
removed.

Daily data are considered "early" for the current month. The previous
six months are provisional data. After six months data are considered
stable. Thus early data only exist for daily data, while there can be
monthly (and presumably yearly) provisional data.

## Examples

``` r
if (FALSE) { # \dontrun{
# delete any provisional annual precipitation data from 2000-2023
# del_files will containg any deleted files
del_files <- prism_archive_clean('ppt', 'annual', 2000:2023, resolution = "4km")
} # }
```
