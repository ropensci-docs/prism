# Set, check, and get prism download directory

`prism_set_dl_dir()` sets the directory that downloaded prism data will
be saved to. The prism download directory is saved in the "prism.path"
option.

`prism_get_dl_dir()` gets the folder that prism data will be saved to.
It is a wrapper around `getOption("prism.path")` so the user does not
have to remember the option name.

`prism_check_dl_dir()` checks that prism download folder has been set.
If it has not been set, and in interactive mode, then prompt user to
specify the download location. If not in interactive mode and it has not
been set then it will stop and post an error.

`path_check()` is a deprecated version of `prism_check_dl_dir()`.

## Usage

``` r
prism_set_dl_dir(path, create = TRUE)

prism_get_dl_dir()

prism_check_dl_dir()

path_check()
```

## Arguments

- path:

  The path that prism data will be unzipped into.

- create:

  Boolean that determines if the `path` will be created if it does not
  already exist.

## Value

Invisibly returns `path`

## Examples

``` r
if (FALSE) { # \dontrun{
prism_set_dl_dir('.')
prism_set_dl_dir('~/prism_data')
} # }
  
prism_get_dl_dir()
#> NULL


if (FALSE) { # \dontrun{
prism_check_dl_dir()
} # }
```
