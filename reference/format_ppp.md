# Convert STATS19 data into ppp (spatstat) format.

This function is a wrapper around the
[`spatstat.geom::ppp()`](https://rdrr.io/pkg/spatstat.geom/man/ppp.html)
function and it is used to transform STATS19 data into a ppp format.

## Usage

``` r
format_ppp(data, window = NULL, ...)
```

## Arguments

- data:

  A STATS19 dataframe to be converted into ppp format.

- window:

  A windows of observation, an object of class `owin()`. If
  `window = NULL` (i.e. the default) then the function creates an
  approximate bounding box covering the whole UK. It can also be used to
  filter only the events occurring in a specific region of UK (see the
  examples of
  [`get_stats19`](https://docs.ropensci.org/stats19/reference/get_stats19.md)).

- ...:

  Additional parameters that should be passed to
  [`spatstat.geom::ppp()`](https://rdrr.io/pkg/spatstat.geom/man/ppp.html)
  function. Read the help page of that function for a detailed
  description of the available parameters.

## Value

A ppp object.

## See also

[`format_sf`](https://docs.ropensci.org/stats19/reference/format_sf.md)
for an analogous function used to convert data into sf format and
[`spatstat.geom::ppp()`](https://rdrr.io/pkg/spatstat.geom/man/ppp.html)
for the original function.

## Examples

``` r
if (requireNamespace("spatstat.geom", quietly = TRUE)) {
  x_ppp = format_ppp(accidents_sample)
  x_ppp
}
#> Warning: some mark values are NA in the point pattern x
#> Marked planar point pattern: 3 points
#> Mark variables: 
#>    accident_index accident_year accident_reference longitude latitude 
#> police_force accident_severity number_of_vehicles number_of_casualties date 
#> day_of_week time local_authority_district local_authority_ons_district 
#> local_authority_highway first_road_class first_road_number road_type 
#> speed_limit junction_detail junction_control second_road_class 
#> second_road_number pedestrian_crossing_human_control 
#> pedestrian_crossing_physical_facilities light_conditions weather_conditions 
#> road_surface_conditions special_conditions_at_site carriageway_hazards 
#> urban_or_rural_area did_police_officer_attend_scene_of_accident trunk_road_flag 
#> lsoa_of_accident_location enhanced_severity_collision
#> window: rectangle = [64950, 655391] x [10235, 1209512] units
```
