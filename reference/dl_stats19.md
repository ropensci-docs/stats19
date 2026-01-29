# Download STATS19 data for a year

Download STATS19 data for a year

## Usage

``` r
dl_stats19(
  year = NULL,
  type = NULL,
  data_dir = get_data_directory(),
  file_name = NULL,
  ask = FALSE,
  silent = FALSE,
  timeout = 600
)
```

## Arguments

- year:

  A year matching file names on the STATS19 [data release
  page](https://www.data.gov.uk/dataset/cb7ae6f0-4be6-4935-9277-47e5ce24a11f/road-accidents-safety-data)
  e.g. `2020`

- type:

  One of 'collision', 'casualty', 'Vehicle'; defaults to 'collision'.
  This text string is used to match the file names released by the DfT.

- data_dir:

  Parent directory for all downloaded files. See
  [`get_data_directory()`](https://docs.ropensci.org/stats19/reference/get_data_directory.md)
  for details.

- file_name:

  The file name (DfT named) to download.

- ask:

  Should you be asked whether or not to download the files? `TRUE` by
  default.

- silent:

  Boolean. If `FALSE` (default value), display useful progress messages
  on the screen.

- timeout:

  Timeout in seconds for the download if current option is less than
  this value. Defaults to 600 (10 minutes).

## Details

This function downloads UK road crash data. It results in .csv files
that are put in a directory that can be set with
[`get_data_directory()`](https://docs.ropensci.org/stats19/reference/get_data_directory.md).
By default, stats19 downloads files to a temporary directory. You can
change this behavior to save the files in a permanent directory. This is
done by setting the `STATS19_DOWNLOAD_DIRECTORY` environment variable. A
convenient way to do this is by adding
`STATS19_DOWNLOAD_DIRECTORY=/path/to/a/dir` to your `.Renviron` file,
which can be opened with
[`usethis::edit_r_environ()`](https://usethis.r-lib.org/reference/edit.html).

The file downloaded would be for a specific year (e.g. 2022). It could
also be a file containing data for a range of two (e.g. 2005-2014).

The `dl_*` functions can download many MB of data so ensure you have a
sufficient internet access and hard disk space.

## See also

[`get_stats19()`](https://docs.ropensci.org/stats19/reference/get_stats19.md)

## Examples

``` r
# \donttest{
if (curl::has_internet()) {
  # type by default is collisions table
  dl_stats19(year = 2022)
  # with type as casualty
  dl_stats19(year = 2022, type = "casualty")
  # try another year
  dl_stats19(year = 2023)
}
#> More than one file found, selecting the first.
#> Files identified: dft-road-casualty-statistics-casualty-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-casualty-2022.csv
#> Data saved at /tmp/RtmpYK4NLW/dft-road-casualty-statistics-casualty-2022.csv
#> Files identified: dft-road-casualty-statistics-casualty-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-casualty-2022.csv
#> Data already exists in data_dir, not downloading
#> More than one file found, selecting the first.
#> Files identified: dft-road-casualty-statistics-casualty-2023.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-casualty-2023.csv
#> Data saved at /tmp/RtmpYK4NLW/dft-road-casualty-statistics-casualty-2023.csv
#> NULL
# }
```
