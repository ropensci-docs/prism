# Download prism data

Download grid cell data from the [prism
project](https://prism.nacse.org/). Temperature (min, max, and mean),
mean dewpoint temperature, precipitation, and vapor pressure deficit
(min and max) can be downloaded for annual (`get_prism_annual()`),
monthly (`get_prism_monthlys()`), daily (`get_prism_dailys()`), and
30-year averages (`get_prism_normals()`). Data are available at 4km and
800m resolution for daily, monthly, and annual data. Normals can also be
downloaded at 800m resolution.

Download data from the prism project for 30 year normals at 4km or 800m
grid cell resolution for precipitation; mean, min and max temperature;
clear sky, sloped, and total solar radiation; and cloud transmittance.

## Usage

``` r
get_prism_annual(
  type,
  years,
  keepZip = TRUE,
  keep_pre81_months = NULL,
  service = NULL,
  resolution = "4km"
)

get_prism_dailys(
  type,
  minDate = NULL,
  maxDate = NULL,
  dates = NULL,
  keepZip = TRUE,
  check = "httr",
  service = NULL,
  resolution = "4km"
)

get_prism_monthlys(
  type,
  years,
  mon = 1:12,
  keepZip = TRUE,
  keep_pre81_months = NULL,
  service = NULL,
  resolution = "4km"
)

get_prism_normals(
  type,
  resolution,
  mon = NULL,
  annual = FALSE,
  keepZip = TRUE,
  day = NULL
)
```

## Arguments

- type:

  The type of data to download. Must be "ppt", "tmean", "tmin", "tmax",
  "tdmean", "vpdmin", or "vpdmax". "solclear", "solslope", "soltotal",
  and "soltrans" are also available only for `get_prism_normals()`. Note
  that `tmean == mean(tmin, tmax)`.

- years:

  a valid numeric year, or vector of years, to download data for.

- keepZip:

  if `TRUE`, leave the downloaded zip files in your 'prism.path', if
  `FALSE`, they will be deleted.

- keep_pre81_months:

  Deprecated

- service:

  Either `NULL` (default) or a URL provided by PRISM staff for
  subscription-based service. Example:
  "http://services.nacse.org/prism/data/subscription/800m". To use the
  subscription option, you must use an IP address registered with PRISM
  staff. When `NULL`, the new PRISM web service endpoints are used based
  on the specified resolution.

- resolution:

  The spatial resolution of the data, must be either "4km" or "800m".

- minDate:

  Date to start downloading daily data. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- maxDate:

  Date to end downloading daily data. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- dates:

  A vector of dates to download daily data. Must be specified in a valid
  iso-8601 (e.g. YYYY-MM-DD) format. May be provided as either a
  character or [base::Date](https://rdrr.io/r/base/Dates.html) class.

- check:

  One of "httr" or "internal". See details.

- mon:

  a valid numeric month, or vector of months. Required for
  `get_prism_monthlys()`. Can be `NULL` for `get_prism_normals()`.

- annual:

  if `TRUE` download annual normals.

- day:

  Download daily normals. If `TRUE`, then download all daily data for
  the specified months or entire year (if `annual` is `TRUE`).
  Individual days can be specified as a `Date` object, where the year is
  ignored or specified as characters in "mm-dd" or "mmdd" form.

## Value

Nothing is returned - an error will occur if download is not successful.

## Details

A valid download directory must exist before downloading any prism data.
This can be set using
[`prism_set_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
and can be verified using
[`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md).

For the `check` parameter, "httr", the default, checks the file name
using the web service, and downloads if that file name is not in the
file system. "internal" (much faster) only attempts to download layers
that are not already in the file system as stable. "internal" should be
used with caution as it is not robust to changes in version or file
names.

## Annual and Monthly

Annual and monthly prism data are available from 1895 to present. For
1895-1980 data, monthly and annual data are grouped together in one
download file; `keep_pre81_months` determines if the other months/yearly
data are kept after the download. Data will be downloaded for all
specified months (`mon`) in all the `years` in the supplied vectors.

Data are available at two spatial resolutions: 4km (approximately 2.5
arc-minutes) and 800m. The 4km resolution covers the entire CONUS and is
suitable for most applications. The 800m resolution provides higher
spatial detail but results in larger file sizes and longer download
times.

## Daily

Daily prism data are available beginning on January 1, 1981. To download
the daily data, dates must be in the proper format or downloading will
not work properly. Dates can be specified using either a date range via
`minDate` and `maxDate`, or a vector of `dates`, but not both.

Data are available at two spatial resolutions: 4km (approximately 2.5
arc-minutes) and 800m. The 4km resolution covers the entire CONUS and is
suitable for most applications. The 800m resolution provides higher
spatial detail but results in larger file sizes and longer download
times.

## Normals

30-year normals are currently computed using 1991-2020 and are available
at 4km and 800m resolution. See <https://prism.nacse.org/normals/>. If
`mon` is specified and `annual` is `TRUE`, then monthly and annual
normal data will be downloaded. Clear sky, sloped, and total solar
radiation; and cloud transmittance are not available for daily normals.

## Examples

``` r
if (FALSE) { # \dontrun{
# Get all annual average temperature data from 1990 to 2000 at default resolution
get_prism_annual(type = "tmean", years = 1990:2000, keepZip = FALSE)

# Get annual precipitation for multiple years at 800m resolution
get_prism_annual(
  type = "ppt", 
  years = 2020:2022, 
  resolution = "800m",
  keepZip = FALSE
)

# Get single year of annual temperature data at high resolution
get_prism_annual(
  type = "tmax",
  years = 2023,
  resolution = "800m",
  keepZip = TRUE
)

# will fail - invalid resolution:
get_prism_annual(
  type = "tmean",
  years = 2023,
  resolution = "1km",
  keepZip = FALSE
)
} # }

if (FALSE) { # \dontrun{
# get daily average temperature data for June 1 - 14, 2013 at 4km resolution
get_prism_dailys(
  type = "tmean", 
  minDate = "2013-06-01", 
  maxDate = "2013-06-14", 
  keepZip = FALSE
)

# get precipitation data for June 1, 2013 at 800m resolution
get_prism_dailys(
  type = "ppt", 
  dates = "2013/06/01", 
  resolution = "800m",
  keepZip = FALSE
)

# get average temperature for three specific days at default resolution
get_prism_dailys(
  type = "tmean", 
  dates = c("2013-06-01", "2013-06-14", "2014-06-30"), 
  keepZip = FALSE
)

# get high-resolution daily maximum temperature for a date range
get_prism_dailys(
  type = "tmax",
  minDate = "2013-06-01",
  maxDate = "2013-06-07", 
  resolution = "800m",
  keepZip = FALSE
)

# will fail - both minDate and dates specified:
get_prism_dailys(
  type = "ppt", 
  minDate = "2013-06-01", 
  dates = "2013-06-14", 
  keepZip = FALSE
)

# will fail - minDate without maxDate:
get_prism_dailys(
  type = "ppt", 
  minDate = "2013-06-01", 
  keepZip = FALSE
)

# will fail - invalid resolution:
get_prism_dailys(
  type = "tmean",
  dates = "2013-06-01",
  resolution = "1km",
  keepZip = FALSE
)
} # }

if (FALSE) { # \dontrun{
# Get all the precipitation data for January from 1990 to 2000 at 4km resolution
get_prism_monthlys(type = "ppt", years = 1990:2000, mon = 1, keepZip = FALSE)

# Get January-December 2005 monthly precipitation at default resolution
get_prism_monthlys(type = "ppt", years = 2005, mon = 1:12, keepZip = FALSE)

# Get high-resolution monthly temperature data for summer months
get_prism_monthlys(
  type = "tmean", 
  years = 2023, 
  mon = 6:8, 
  resolution = "800m",
  keepZip = FALSE
)

# Get multiple years of winter precipitation at 800m resolution
get_prism_monthlys(
  type = "ppt",
  years = 2020:2022,
  mon = c(12, 1, 2),
  resolution = "800m",
  keepZip = TRUE
)

# will fail - invalid resolution:
get_prism_monthlys(
  type = "ppt",
  years = 2023,
  mon = 6,
  resolution = "1km",
  keepZip = FALSE
)
} # }

if (FALSE) { # \dontrun{
# Get 30 year normal values for January rainfall
get_prism_normals(type = "ppt", resolution = "4km", mon = 1, keepZip = FALSE)

# Get monthly (every month) and annual 30-year normals for mean temperature
get_prism_normals(
  type = "tmean", 
  resolution = "800m", 
  mon = 1:12, 
  annual = TRUE,
  keepZip = FALSE
)

# Get daily precip normals for January 1 and March 1
get_prism_normals('ppt', '4km', NULL, FALSE, TRUE, c('0101', '0301'))

# Get daily precip normals for all of February
get_prism_normals('ppt', '4km', 2, FALSE, TRUE, TRUE)

# Get July 2nd average temperature 30-year average
get_prism_normals('tmean', '800m', NULL, FALSE, TRUE, as.Date('2000-07-02'))
} # }
```
