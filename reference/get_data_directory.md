# Get data download dir

Get data download dir

## Usage

``` r
get_data_directory()
```

## Details

By default, stats19 downloads files to a temporary directory. You can
change this behavior to save the files in a permanent directory. This is
done by setting the `STATS19_DOWNLOAD_DIRECTORY` environment variable. A
convenient way to do this is by adding
`STATS19_DOWNLOAD_DIRECTORY=/path/to/a/dir` to your `.Renviron` file,
which can be opened by
[`usethis::edit_r_environ()`](https://usethis.r-lib.org/reference/edit.html).

## Examples

``` r
# get_data_directory()
```
