# Changelog

## prism (development version)

## prism 0.3.0

CRAN release: 2025-11-14

I am very sorry for the delay in getting a working version of prism
updated based on the API changes that were made in September 2025. In
the near future, we will be updating the entire package to take
advantage of the newly available cloud optimized GeoTiff (COG) format.
For now, most of the package still downloads the previously relied on
.bil files. The exception is described more below. Thank you to
[@ran-codes](https://github.com/ran-codes) for the heavy lifting in
switching to the new API.

The package now posts a warning if the prism archive contains folders
from the old API. Our recommendation is to start fresh, and re-download
any old data you need. The package has probably not been fully stress
tested with a combination of data from the old API with the new API.

### Breaking Changes

- [`get_prism_normals()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  no longer downloads .bil files, and instead downloads the data in COG
  format. For this reason, all of the helper functions, e.g.,
  [`pd_plot_slice()`](https://docs.ropensci.org/prism/reference/pd_plot_slice.md),
  [`pd_image()`](https://docs.ropensci.org/prism/reference/pd_image.md),
  etc., do not work with the normals.

### Major but Under-the-Hood Changes

- Switched all code to use the new API provided by Oregon State.
  ([@ran-codes](https://github.com/ran-codes),
  [\#135](https://github.com/ropensci/prism/issues/135))

### Minor Enhancements (non-API breaking changes)

- Based on the updated API, there is no longer any difference in the
  packaging of pre/post 1981 data. Therefore, `keep_pre81_months` is
  deprecated in
  [`get_prism_monthlys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  and
  [`get_prism_annual()`](https://docs.ropensci.org/prism/reference/get_prism_data.md).

## prism 0.2.3

CRAN release: 2025-03-25

**Released March 25, 2025**

- Changed
  [`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
  so that it no longer suggests ~/prismtmp as a default. The user must
  specify where the data should be downloaded to either using
  [`prism_set_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
  or via the prompts in
  [`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md).
  Additionally, if following the prompts in
  [`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md),
  if a user specifies a folder that does not exist, then it confirms
  that user wants the folder to be created.

## prism 0.2.2

CRAN release: 2025-03-18

**Released March 18, 2025** - this version was pulled down from CRAN on
March 20, 2025 for violating CRAN policies b/c
[`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
suggests a default directory (~/prismtmp) and the example files create
this folder and leave it behind. This is resolved in the next patch
version.

### Minor Enhancements (non-API breaking changes)

- Added solar radiation (clear sky), solar radiation (sloped), solar
  radiation (total), and cloud transmittance as available variables to
  download for monthly and annual normals. The variables are `solclear`,
  `solslope`, `soltotal`, and `soltrans`.
  ([\#130](https://github.com/ropensci/prism/issues/130),
  [@brownag](https://github.com/brownag))
- Added ability to download daily normals for all variables except solar
  radiation (clear sky), solar radiation (sloped), solar radiation
  (total), and cloud transmittance
  ([\#123](https://github.com/ropensci/prism/issues/123)). The `day`
  parameter was added to
  [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  to specify which days to get the normals for. It was added as the last
  parameter so previous code that does not specify arguments by name
  will still work. Made sure all `pd_get_*()` functions work with daily
  normals.
- Added a better error message when the PRISM webservice is down (not
  returning status 200).
  ([\#122](https://github.com/ropensci/prism/issues/122))

### Bug Fixes and Clean Up

- Fixed examples in the
  [`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md)
  to use correct syntax for a range of years.
  ([\#128](https://github.com/ropensci/prism/issues/128),
  [@Archaeo-Programmer](https://github.com/Archaeo-Programmer))
- Internal updates to meet ROpenSci style guide including removing uses
  of [`sapply()`](https://rdrr.io/r/base/lapply.html), removing uses of
  `1:length(...)`, and removing global assignment inside
  `prism_webservice()`
- Documented return value for
  [`pd_stack()`](https://docs.ropensci.org/prism/reference/pd_stack.md),
  [`prism_set_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
  ,[`pd_to_file()`](https://docs.ropensci.org/prism/reference/pd_get.md),
  [`pd_get_type()`](https://docs.ropensci.org/prism/reference/pd_get.md)
  & `get_prism_*()` functions.
- Added examples to documentation for
  [`pd_to_file()`](https://docs.ropensci.org/prism/reference/pd_get.md),
  [`prism_archive_clean()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md),
  [`prism_archive_verify()`](https://docs.ropensci.org/prism/reference/prism_archive_verify.md),
  [`prism_set_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md),
  & `pd_get_*()` functions.

## prism 0.2.1

CRAN release: 2023-10-18

**Released October 17, 2023**

### Minor Enhancements

- Added `service` parameter to
  [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md),
  [`get_prism_monthlys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md),
  and
  [`get_prism_annual()`](https://docs.ropensci.org/prism/reference/get_prism_data.md),
  so user can provide subscription based URLs, instead of default public
  available 4km data. ([@adamlilith](https://github.com/adamlilith))
- Changed defaults in get data functions
  ([\#104](https://github.com/ropensci/prism/issues/104))
  - [`get_prism_monthlys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
    - `mon` now defaults to `1:12`, so default now downloads all months
      for the specified years
    - `years` no longer has a default of `NULL`, so user will understand
      it has to be provided
  - [`get_prism_annual()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
    - `years` no longer has a default of `NULL`, so user will understand
      it has to be provided
  - Minor updates to documentation of `mon` and `years` parameters

### Bug Fixes and Clean Up

- Fixing CRAN notes
  - Removed LazyData and LazyLoad from Description to fix CRAN note.
  - Removed lubridate from imports to fix CRAN note.
- Removed vignette that depended on too many other libraries; did not
  want to add them all to Suggests and also relied on external shape
  file. This may be linked to from README in the future.
- Updated error message in
  [`pd_image()`](https://docs.ropensci.org/prism/reference/pd_image.md)
  when input has length of 0.
- Fixed documentation for
  [`get_prism_normals()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  to reference the new period (1991-2020).
  ([\#111](https://github.com/ropensci/prism/issues/111))
- Updated error message in
  [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  if a date before Jan. 1, 1981 is provided.
- Deprecated `check` parameter in
  [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  as it does not exist in monthly or annual functions.
  ([\#116](https://github.com/ropensci/prism/issues/116))
- Removed purrr from imports by switching one call from `purrr:map()` to
  [`lapply()`](https://rdrr.io/r/base/lapply.html).

## prism 0.2.0

CRAN release: 2020-12-05

**Published December 5, 2020**

Thanks to [@jsta](https://github.com/jsta) for updating the README and
helping with several other under the hood fixes.

### Breaking Changes

- `prism_webservice()` is no longer exported as it is wrapped by
  `get_prism_*()` functions, and requires a correctly specified url. It
  can still be called with `prism:::prism_webservice()` if users really
  need it. ([\#83](https://github.com/ropensci/prism/issues/83))
- `pr_parse()` is no longer exported. Use
  [`pd_get_name()`](https://docs.ropensci.org/prism/reference/pd_get.md)
  or
  [`pd_get_date()`](https://docs.ropensci.org/prism/reference/pd_get.md)
  instead.

### Major Updates

There are two overall major updates with this release. (1) All functions
should work with all temporal periods and all variables; previously some
functions only worked with daily data and not all variables were able to
be downloaded from the prism website. (2) A new API was implemented that
results in many functions being deprecated in favor of the updated
naming convention. This change was intended to provide consistent names
for functions that apply to different steps in the work flow implemented
in this package. The details of these changes are:

- Users can now download vpdmin, vpdmax, and tdmean variables for
  30-year normals, daily, monthly, and annual data.
  ([\#68](https://github.com/ropensci/prism/issues/68))
- There are now several functions (`prism_*_dl_dir()`) that set and
  check the prism download directory. These are hopefully easier to
  remember than using the base R
  [`options()`](https://rdrr.io/r/base/options.html) and
  [`getOption()`](https://rdrr.io/r/base/options.html) functions and the
  prism option variable name “prism.path”.
  - [`prism_check_dl_dir()`](https://docs.ropensci.org/prism/reference/prism_set_dl_dir.md)
    replaces `check_path()`, which is deprecated and will be removed in
    the next release.
- The prism data are downloaded to this directory and then referred to
  as the “prism archive”. These are the `prism_archive_*()` functions.
  - New function:
    [`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).
    This makes it much easier to get the data for a specific
    type/temporal period from the prism archive.
    ([\#69](https://github.com/ropensci/prism/issues/69))
  - [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
    replaces
    [`ls_prism_data()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md),
    which will be removed in a future release.
    - The return type and options changed from
      [`ls_prism_data()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
      to
      [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md),
      which now always returns only folder names as a vector, instead of
      a data.frame that could have between 1 and 3 columns.
    - The previous behavior can be achieved by applying new functions
      ([`pd_get_name()`](https://docs.ropensci.org/prism/reference/pd_get.md)
      and
      [`pd_to_file()`](https://docs.ropensci.org/prism/reference/pd_get.md))
      to the vector returned by
      [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md).
  - [`prism_archive_clean()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md)
    replaces
    [`del_early_prov()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md),
    which will be removed in a future release. It also now works with
    all time steps and prompts user to select which folders will be
    removed before removing them (when R is in interactive mode).
    ([\#89](https://github.com/ropensci/prism/issues/89))
  - [`prism_archive_verify()`](https://docs.ropensci.org/prism/reference/prism_archive_verify.md)
    replaces
    [`check_corrupt()`](https://docs.ropensci.org/prism/reference/prism_archive_verify.md),
    which will be removed in a future release. It also now works with
    time steps other than daily and it gains a `download_corrupt`
    argument that controls whether corrupt files are automatically
    re-downloaded.
- [`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
  and `prism_archive_pd()` both return vectors of prism data folder
  names, i.e., prism data, i.e., `pd`. There are a number of functions
  that act on the prism data. These are the `pd_*()` functions.
  - [`pd_image()`](https://docs.ropensci.org/prism/reference/pd_image.md)
    replaces
    [`prism_image()`](https://docs.ropensci.org/prism/reference/pd_image.md).
  - [`pd_plot_slice()`](https://docs.ropensci.org/prism/reference/pd_plot_slice.md)
    replaces
    [`prism_slice()`](https://docs.ropensci.org/prism/reference/pd_plot_slice.md).
  - [`pd_stack()`](https://docs.ropensci.org/prism/reference/pd_stack.md)
    replaces
    [`prism_stack()`](https://docs.ropensci.org/prism/reference/pd_stack.md).
  - [`pd_get_station_md()`](https://docs.ropensci.org/prism/reference/pd_get_station_md.md)
    replaces
    [`get_prism_station_md()`](https://docs.ropensci.org/prism/reference/pd_get_station_md.md).
    ([\#88](https://github.com/ropensci/prism/issues/88))
  - [`prism_md()`](https://docs.ropensci.org/prism/reference/pd_get.md)
    will be removed in a future release. It is replaced by:
    - [`pd_get_name()`](https://docs.ropensci.org/prism/reference/pd_get.md),
      which is equivalent to `prism_md(f, FALSE)`.
    - [`pd_get_date()`](https://docs.ropensci.org/prism/reference/pd_get.md),
      which is equivalent to `prism_md(f, TRUE)`.
  - Two new functions were added that convert the prism data to a full
    absolute path
    ([`pd_to_file()`](https://docs.ropensci.org/prism/reference/pd_get.md))
    and get the type (parameter) of the prism data
    ([`pd_get_type()`](https://docs.ropensci.org/prism/reference/pd_get.md)).

### Other Changes

- The way pre 1981 data is handled has been updated.
  - [`get_prism_annual()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
    and
    [`get_prism_monthlys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
    gain a `keep_pre81_months` parameter. This lets the user determine
    if all of the monthly and annual data are kept, since the download
    includes all 12 months + the annual data for years before 1981. If
    this is `TRUE` then all monthly data are kept, instead of only those
    that were specified in the current call to `get_prism_*()`.
    ([\#82](https://github.com/ropensci/prism/issues/82))
  - Because pre-1981 data might already have been downloaded based on
    `keep_pre81_months` parameter in previous downloads, the download
    functions now check that pre-1981 data does not exist before
    downloading it. To do this, `prism_webservice()` and
    [`prism_check()`](https://docs.ropensci.org/prism/reference/prism_check.md)
    gain a `pre81_months` parameter, which allows the functions to know
    which months were requested for downloading.
    ([\#81](https://github.com/ropensci/prism/issues/81))
- The prism web service only allows a user to download the same data
  twice in a 24-hour period. The download functions now report when the
  user has exceeded the allowable number of attempts to download the
  same file (in one day). If a user tries to download the same file more
  than two times in one day, the message is posted as a warning and the
  returned text file is saved in the prism archive. This is not posted
  as an error so that if a query of multiple files runs into this issue,
  it does not abort the full query. Another warning posts if the
  unzipped folder is empty.
  ([\#80](https://github.com/ropensci/prism/issues/80))
- [`prism_check()`](https://docs.ropensci.org/prism/reference/prism_check.md)
  is deprecated and will be no longer be exported in the next release.
- [`get_prism_normals()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  will now error if neither monthly nor annual data are specified to be
  downloaded and will download monthly and annual data simultaneously if
  asked to do so. ([\#77](https://github.com/ropensci/prism/issues/77))
- all `get_prism_*()` functions are documented in same help page.
  ([\#79](https://github.com/ropensci/prism/issues/79))
- Help pages for non-exported functions have been removed.
- More tests were added. Up to 50% coverage now. Some tests are only run
  locally to ensure prism download limits are not exceeded.
- [`pd_get_station_md()`](https://docs.ropensci.org/prism/reference/pd_get_station_md.md)
  (formerly
  [`get_prism_station_md()`](https://docs.ropensci.org/prism/reference/pd_get_station_md.md))
  now reports a warning if not all requested dates exist in the metadata
  data frame. ([\#87](https://github.com/ropensci/prism/issues/87)
  related). It also now works for monthly and normals; not solely daily
  prism data.
- [`pd_get_md()`](https://docs.ropensci.org/prism/reference/pd_get_md.md)
  was added to parse .info.txt metadata, by converting an existing
  internal function.
  ([\#88](https://github.com/ropensci/prism/issues/88))
- [`prism_archive_clean()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md)
  (formerly
  [`del_early_prov()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md))
  now invisibly returns the folders that it removes.
- [`pd_image()`](https://docs.ropensci.org/prism/reference/pd_image.md)
  (formerly
  [`prism_image()`](https://docs.ropensci.org/prism/reference/pd_image.md))
  invisibly returns the `gg` object it creates. It also shows the units
  for the prism variable in the fill legend.
  ([\#99](https://github.com/ropensci/prism/issues/99))

## prism 0.1.0

CRAN release: 2018-12-10

### Minor changes

- New functions
  - [`del_early_prov()`](https://docs.ropensci.org/prism/reference/prism_archive_clean.md)
    searches the download folder for duplicated PRISM data and keeps
    only the newest version.
  - [`get_prism_station_md()`](https://docs.ropensci.org/prism/reference/pd_get_station_md.md)
    extracts metadata from daily PRISM data.
- [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  gains a `check` parameter that allows the user to specify how prism
  files are checked.

### Bug fixes

- [`get_prism_monthlys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  can now download 1981 data. ([@sdtaylor](https://github.com/sdtaylor)
  [\#59](https://github.com/ropensci/prism/issues/59),
  [\#63](https://github.com/ropensci/prism/issues/63))
- [`get_prism_annual()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  can now download pre 1981 data by itself.
  ([@rabutler](https://github.com/rabutler)
  [\#64](https://github.com/ropensci/prism/issues/64))
- [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  now correctly sets the progress bar.
- fixed bug in `gen_dates()` so that
  [`get_prism_dailys()`](https://docs.ropensci.org/prism/reference/get_prism_data.md)
  works with only the `dates` parameter specified.
  ([@rabutler](https://github.com/rabutler)
  [\#66](https://github.com/ropensci/prism/issues/66))

### Under the hood

- added internal `gen_dates()` function for determining the specified
  dates (either from `minDate` and `maxDate`. or `dates`) used by the
  `get_prism_*()` functions.
- added tests for `gen_dates()` .

## prism 0.0.7

CRAN release: 2015-11-16

#### Changes

- Changed acquisition method to use prism webservice. Prior to this
  change the FTP acquisition method often caused the server to time out
  when download request volume became too high.

- Changed method of metadata extraction. Originally we parsed XML
  metadata to get information about raster files. However the XML for
  historical data is particularly sparse. The new method relies on
  parsing file names instead. While more universal, it may be less
  stable

#### Bug fixes

- Fixed FTP time out error by switching to webservice

- Fixed `prism_stack` by adjusting to new metadata extraction method
