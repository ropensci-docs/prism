# Get prism metadata

Retrieves prism metadata from the specified prism data. "prism data",
i.e., `pd` are the folder names returned by
[`prism_archive_ls()`](https://docs.ropensci.org/prism/reference/prism_archive_ls.md)
or
[`prism_archive_subset()`](https://docs.ropensci.org/prism/reference/prism_archive_subset.md).
These functions get the name or date from these data, or convert these
data to a file name. A warning is provided if the specified prism data
do not exist in the archive.

## Usage

``` r
pd_get_md(pd)
```

## Arguments

- pd:

  prism data character vector.

## Value

data.frame containing metadata for all specified prism data.

## Details

The metadata includes the following variables from the .info.txt file
for daily, monthly, and annual data:

- PRISM_DATASET_FILENAME

- PRISM_DATASET_CREATE_DATE

- PRISM_DATASET_TYPE

- PRISM_DATASET_VERSION

- PRISM_CODE_VERSION

- PRISM_DATASET_REMARKS

Additionally, two local variables are added identifying where the file
is located on the local system:

- file_path

- folder_path

The annual and monthly normals data includes different keys in the
.info.txt, so they are renamed to be the same as those found in the
other temporal data. The keys/variables are renamed as follows:

- PRISM_FILENAME –\> PRISM_DATASET_FILENAME

- PRISM_CREATE_DATE –\> PRISM_DATASET_CREATE_DATE

- PRISM_DATASET –\> PRISM_DATASET_TYPE

- PRISM_VERSION –\> PRISM_CODE_VERSION

- PRISM_REMARKS –\> PRISM_DATASET_REMARKS

Additionally, the normals does not include PRISM_DATASET_VERSION, so
that variable is added with `NA` values.

## Examples

``` r
if (FALSE) { # \dontrun{
#' # Assumes 2000-2002 annual precipitation data is already downloaded
pd <- prism_archive_subset('ppt', 'annual', years = 2000:2002)
df <- pd_get_md(pd)
head(df)
} # }
```
