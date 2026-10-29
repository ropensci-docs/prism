# Extract prism station metadata

`pd_get_station_md()` extracts prism metadata on the stations used to
generate the prism data. **The data must already be downloaded and
available in the prism download folder.** "prism data", i.e., `pd` are
the folder names returned by
[`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
or
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).

`get_prism_station_md()` is a deprecated version of
`pd_get_station_md()` that only works with daily prism data.

## Usage

``` r
pd_get_station_md(pd)

get_prism_station_md(type, minDate = NULL, maxDate = NULL, dates = NULL)
```

## Arguments

- pd:

  prism data character vector.

- type:

  The type of data you want to subset. Must be "ppt", "tmean", "tmin",
  "tmax", "tdmean", "vpdmin", "vpdmax", "solclear", "solslope",
  "soltotal", or "soltrans".

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

## Value

A `tbl_df` containing metadata on the stations used for the specified
day and variable. The data frame contains the following columns: "date",
"prism_data", "type", "station", "name", "longitude", "latitude",
"elevation", "network", "stnid"

The "date" column is a character representation of the data. Monthly and
annual data are given first day of month, and first month of year for
reporting here. Monthly and annual normals are empty strings.

## Details

Note that station metadata does not exist for "tmean" type, any "annual"
temporal periods, nor for daily normals.

See
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)
for further details on specifying ranges of dates for different temporal
periods.

## See also

[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)

## Examples

``` r
if (FALSE) { # \dontrun{
# download and then get meta data for January 1, 2010 precipitation
get_prism_dailys("ppt", dates = "2010-01-01")
pd <- prism_archive_subset("ppt", "daily", dates = "2010-01-01")

# will warn that 2010-01-02 is not found:
pd_get_station_md(pd)
} # }
  
```
