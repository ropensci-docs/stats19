# Pin down a file on disk from four parameters.

Pin down a file on disk from four parameters.

## Usage

``` r
locate_one_file(
  filename = NULL,
  data_dir = get_data_directory(),
  year = NULL,
  type = NULL
)
```

## Arguments

- filename:

  Character string of the filename of the .csv to read, if this is
  given, type and years determine whether there is a target to read,
  otherwise disk scan would be needed.

- data_dir:

  Where sets of downloaded data would be found.

- year:

  Single year for which file is to be found.

- type:

  One of: 'Collision', 'Casualties', 'Vehicles'; ignores case.

## Value

One of: path for one file, a message `More than one file found` or error
if none found.

## Examples

``` r
# \donttest{
locate_one_file()
#> [1] "/tmp/RtmpYK4NLW/dft-road-casualty-statistics-casualty-2023.csv"
locate_one_file(filename = "Cas.csv")
#> character(0)
# }
```
