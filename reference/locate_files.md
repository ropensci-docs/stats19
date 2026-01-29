# Locate a file on disk

Helper function to locate files. Given below params, the function
returns 0 or more files found at location/names given.

## Usage

``` r
locate_files(
  data_dir = get_data_directory(),
  type = NULL,
  years = NULL,
  quiet = FALSE
)
```

## Arguments

- data_dir:

  Super directory where dataset(s) were first downloaded to.

- type:

  One of 'Collision', 'Casualties', 'Vehicles'; defaults to 'Collision',
  ignores case.

- years:

  Years for which data are to be found

- quiet:

  Print out messages (files found)

## Value

Character string representing the full path of a single file found, list
of directories where data from the Department for Transport
(stats19::filenames) have been downloaded, or NULL if no files were
found.
