# Local helper to be reused.

Local helper to be reused.

## Usage

``` r
check_input_file(filename = NULL, type = NULL, data_dir = NULL, year = NULL)
```

## Arguments

- filename:

  Character string of the filename of the .csv to read, if this is
  given, type and years determine whether there is a target to read,
  otherwise disk scan would be needed.

- type:

  The type of file to be downloaded (e.g. 'collisions', 'casualty' or
  'vehicles'). Not case sensitive and searches using regular expressions
  ('acc' will work).

- data_dir:

  Where sets of downloaded data would be found.

- year:

  Single year for which data are to be read
