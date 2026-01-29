# Find file names within stats19::file_names.

Currently, there are 52 file names to download/read data from.

## Usage

``` r
find_file_name(years = NULL, type = NULL)
```

## Arguments

- years:

  Year for which data are to be found

- type:

  One of 'collisions', 'casualty' or 'vehicles' ignores case.

## Examples

``` r
find_file_name(2016)
#> [1] "dft-road-casualty-statistics-casualty-1979-latest-published-year.csv" 
#> [2] "dft-road-casualty-statistics-vehicle-1979-latest-published-year.csv"  
#> [3] "dft-road-casualty-statistics-collision-1979-latest-published-year.csv"
find_file_name(2016, type = "collision")
#> [1] "dft-road-casualty-statistics-collision-1979-latest-published-year.csv"
find_file_name(1985, type = "collision")
#> [1] "dft-road-casualty-statistics-collision-1979-latest-published-year.csv"
find_file_name(type = "cas")
#>  [1] "dft-road-casualty-statistics-casualty-provisional-mid-year-unvalidated-2025.csv"       
#>  [2] "dft-road-casualty-statistics-casualty-2024.csv"                                        
#>  [3] "dft-road-casualty-statistics-casualty-2023.csv"                                        
#>  [4] "dft-road-casualty-statistics-casualty-2022.csv"                                        
#>  [5] "dft-road-casualty-statistics-casualty-2021.csv"                                        
#>  [6] "dft-road-casualty-statistics-casualty-2020.csv"                                        
#>  [7] "dft-road-casualty-statistics-casualty-2019.csv"                                        
#>  [8] "dft-road-casualty-statistics-casualties-adjustment-last-5-years.csv"                   
#>  [9] "dft-road-casualty-statistics-casualty-adjustment-lookup_2004-latest-published-year.csv"
#> [10] "dft-road-casualty-statistics-casualty-1979-latest-published-year.csv"                  
#> [11] "dft-road-casualty-statistics-casualty-last-5-years.csv"                                
find_file_name(type = "collision")
#>  [1] "dft-road-casualty-statistics-collision-provisional-mid-year-unvalidated-2025.csv"       
#>  [2] "dft-road-casualty-statistics-collision-2024.csv"                                        
#>  [3] "dft-road-casualty-statistics-collision-2023.csv"                                        
#>  [4] "dft-road-casualty-statistics-collision-2022.csv"                                        
#>  [5] "dft-road-casualty-statistics-collision-2021.csv"                                        
#>  [6] "dft-road-casualty-statistics-collision-2020.csv"                                        
#>  [7] "dft-road-casualty-statistics-collision-2019.csv"                                        
#>  [8] "dft-road-casualty-statistics-collision-adjustment-last-5-years.csv"                     
#>  [9] "dft-road-casualty-statistics-collision-adjustment-lookup_2004-latest-published-year.csv"
#> [10] "dft-road-casualty-statistics-collision-1979-latest-published-year.csv"                  
#> [11] "dft-road-casualty-statistics-collision-last-5-years.csv"                                
```
