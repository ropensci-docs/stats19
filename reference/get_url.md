# Convert file names to urls

Convert file names to urls

## Usage

``` r
get_url(
  file_name = "",
  domain = "https://data.dft.gov.uk",
  directory = "road-accidents-safety-data"
)
```

## Arguments

- file_name:

  Optional file name to add to the url returned (empty by default)

- domain:

  The domain from where the data will be downloaded

- directory:

  The subdirectory of the url

## Details

This function returns urls that allow data to be downloaded from the
pages:

https://www.gov.uk/government/collections/road-accidents-and-safety-statistics

Last updated: October 2020. Files available from the s3 url in the
default `domain` argument.

## Examples

``` r
# get_url(find_file_name(1985))
```
