# Download, read and format STATS19 data in one function.

Download, read and format STATS19 data in one function.

## Usage

``` r
get_stats19(
  year = NULL,
  type = "collision",
  data_dir = get_data_directory(),
  file_name = NULL,
  format = TRUE,
  ask = FALSE,
  silent = FALSE,
  output_format = "tibble",
  ...
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

- format:

  Switch to return raw read from file, default is `TRUE`.

- ask:

  Should you be asked whether or not to download the files? `TRUE` by
  default.

- silent:

  Boolean. If `FALSE` (default value), display useful progress messages
  on the screen.

- output_format:

  A string that specifies the desired output format. The default value
  is `"tibble"`. Other possible values are `"data.frame"`, `"sf"` and
  `"ppp"`, that, respectively, returns objects of class
  [`data.frame`](https://rdrr.io/r/base/data.frame.html),
  [`sf::sf`](https://r-spatial.github.io/sf/reference/sf.html) and
  [`spatstat.geom::ppp`](https://rdrr.io/pkg/spatstat.geom/man/ppp.html).
  Any other string is ignored and a tibble output is returned. See
  details and examples.

- ...:

  Other arguments be passed to
  [`format_sf()`](https://docs.ropensci.org/stats19/reference/format_sf.md)
  or
  [`format_ppp()`](https://docs.ropensci.org/stats19/reference/format_ppp.md)
  functions. Read and run the examples.

## Details

This function gets STATS19 data. Behind the scenes it uses
[`dl_stats19()`](https://docs.ropensci.org/stats19/reference/dl_stats19.md)
and `read_*` functions, returning a `tibble` (default), `data.frame`,
`sf` or `ppp` object, depending on the `output_format` parameter.

By default, stats19 downloads files to a temporary directory. You can
change this behavior to save the files in a permanent directory. This is
done by setting the `STATS19_DOWNLOAD_DIRECTORY` environment variable. A
convenient way to do this is by adding
`STATS19_DOWNLOAD_DIRECTORY=/path/to/a/dir` to your `.Renviron` file,
which can be opened with
[`usethis::edit_r_environ()`](https://usethis.r-lib.org/reference/edit.html).

The function returns data for a specific year (e.g. `year = 2022`)

Note: for years before 2016 the function may return data from more years
than are requested due to the nature of the files hosted at
[data.gov.uk](https://www.data.gov.uk/dataset/cb7ae6f0-4be6-4935-9277-47e5ce24a11f/road-accidents-safety-data).

As this function uses `dl_stats19` function, it can download many MB of
data, so ensure you have a sufficient disk space.

If `output_format = "data.frame"` or `output_format = "sf"` or
`output_format = "ppp"` then the output data is transformed into a
data.frame, sf or ppp object using the
[`as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html) or
[`format_sf()`](https://docs.ropensci.org/stats19/reference/format_sf.md)
or
[`format_ppp()`](https://docs.ropensci.org/stats19/reference/format_ppp.md)
functions, as shown in the examples.

## See also

[`dl_stats19()`](https://docs.ropensci.org/stats19/reference/dl_stats19.md)

[`read_collisions()`](https://docs.ropensci.org/stats19/reference/read_collisions.md)

## Examples

``` r
# \donttest{
if(curl::has_internet()) {
col = get_stats19(year = 2022, type = "collision")
cas = get_stats19(year = 2022, type = "casualty")
veh = get_stats19(year = 2022, type = "vehicle")
class(col)
# data.frame output
x = get_stats19(2022, silent = TRUE, output_format = "data.frame")
class(x)

# # Get 5-years worth of data (commented-out due to large response size):
# col_5 = get_stats19(year = 5, type = "collision")
# cas_5 = get_stats19(year = 5, type = "casualty")
# veh_5 = get_stats19(year = 5, type = "vehicle")


# Run tests only if endpoint is alive:
if(nrow(x) > 0) {

# sf output
x_sf = get_stats19(2022, silent = TRUE, output_format = "sf")

# sf output with lonlat coordinates
x_sf = get_stats19(2022, silent = TRUE, output_format = "sf", lonlat = TRUE)
sf::st_crs(x_sf)

if (requireNamespace("spatstat.geom", quietly = TRUE)) {
# ppp output
x_ppp = get_stats19(2022, silent = TRUE, output_format = "ppp")

# We can use the window parameter of format_ppp function to filter only the
# events occurred in a specific area. For example we can create a new bbox
# of 5km around the city center of Leeds

leeds_window = spatstat.geom::owin(
xrange = c(425046.1, 435046.1),
yrange = c(428577.2, 438577.2)
)

leeds_ppp = get_stats19(2022, silent = TRUE, output_format = "ppp", window = leeds_window)
spatstat.geom::plot.ppp(leeds_ppp, use.marks = FALSE, clipwin = leeds_window)

# or even more fancy examples where we subset all the events occurred in a
# pre-defined polygon area

# The following example requires osmdata package
# greater_london_sf_polygon = osmdata::getbb(
# "Greater London, UK",
# format_out = "sf_polygon"
# )
# spatstat works only with planar coordinates
# greater_london_sf_polygon = sf::st_transform(greater_london_sf_polygon, 27700)
# then we extract the coordinates and create the window object.
# greater_london_polygon = sf::st_coordinates(greater_london_sf_polygon)[, c(1, 2)]
# greater_london_window = spatstat.geom::owin(poly = greater_london_polygon)

# greater_london_ppp = get_stats19(2022, output_format = "ppp", window = greater_london_window)
# spatstat.geom::plot.ppp(greater_london_ppp, use.marks = FALSE, clipwin = greater_london_window)
}
}
}
#> Files identified: dft-road-casualty-statistics-collision-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-collision-2022.csv
#> Data already exists in data_dir, not downloading
#> Reading in: 
#> /tmp/RtmpYK4NLW/dft-road-casualty-statistics-collision-2022.csv
#> date and time columns present, creating formatted datetime column
#> Files identified: dft-road-casualty-statistics-casualty-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-casualty-2022.csv
#> Data already exists in data_dir, not downloading
#> Warning: The following named parsers don't match the column names: casualty_adjusted_serious, casualty_adjusted_slight, carriageway_hazards, carriageway_hazards_historic, collision_adjusted_serious, collision_adjusted_slight, collision_injury_based, collision_severity, date, day_of_week, did_police_officer_attend_scene_of_accident, did_police_officer_attend_scene_of_collision, enhanced_collision_severity, first_road_class, first_road_number, junction_control, junction_detail, junction_detail_historic, latitude, light_conditions, local_authority_district, local_authority_highway, local_authority_highway_current, local_authority_ons_district, location_easting_osgr, location_northing_osgr, longitude, lsoa_of_accident_location, lsoa_of_collision_location, number_of_casualties, number_of_vehicles, pedestrian_crossing, pedestrian_crossing_human_control_historic, pedestrian_crossing_physical_facilities_historic, police_force, road_surface_conditions, road_type, second_road_class, second_road_number, special_conditions_at_site, speed_limit, time, trunk_road_flag, urban_or_rural_area, weather_conditions, accident_index, accident_ref_no, accident_year, effective_date_of_change, previously_published_value, replacement_value, variable, age_band_of_driver, age_of_driver, age_of_vehicle, driver_distance_banding, driver_imd_decile, engine_capacity_cc, escooter_flag, first_point_of_impact, generic_make_model, hit_object_in_carriageway, hit_object_off_carriageway, journey_purpose_of_driver, journey_purpose_of_driver_historic, junction_location, lsoa_of_driver, propulsion_code, sex_of_driver, skidding_and_overturning, towing_and_articulation, vehicle_direction_from, vehicle_direction_to, vehicle_leaving_carriageway, vehicle_left_hand_drive, vehicle_location_restricted_lane, vehicle_location_restricted_lane_historic, vehicle_manoeuvre, vehicle_manoeuvre_historic, vehicle_type
#> Warning: NAs introduced by coercion
#> Files identified: dft-road-casualty-statistics-vehicle-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-vehicle-2022.csv
#> Data already exists in data_dir, not downloading
#> Warning: The following named parsers don't match the column names: age_band_of_casualty, age_of_casualty, bus_or_coach_passenger, car_passenger, casualty_adjusted_serious, casualty_adjusted_slight, casualty_class, casualty_distance_banding, casualty_imd_decile, casualty_injury_based, casualty_reference, casualty_severity, casualty_type, enhanced_casualty_severity, lsoa_of_casualty, pedestrian_location, pedestrian_movement, pedestrian_road_maintenance_worker, sex_of_casualty, carriageway_hazards, carriageway_hazards_historic, collision_adjusted_serious, collision_adjusted_slight, collision_injury_based, collision_severity, date, day_of_week, did_police_officer_attend_scene_of_accident, did_police_officer_attend_scene_of_collision, enhanced_collision_severity, first_road_class, first_road_number, junction_control, junction_detail, junction_detail_historic, latitude, light_conditions, local_authority_district, local_authority_highway, local_authority_highway_current, local_authority_ons_district, location_easting_osgr, location_northing_osgr, longitude, lsoa_of_accident_location, lsoa_of_collision_location, number_of_casualties, number_of_vehicles, pedestrian_crossing, pedestrian_crossing_human_control_historic, pedestrian_crossing_physical_facilities_historic, police_force, road_surface_conditions, road_type, second_road_class, second_road_number, special_conditions_at_site, speed_limit, time, trunk_road_flag, urban_or_rural_area, weather_conditions, accident_index, accident_ref_no, accident_year, effective_date_of_change, previously_published_value, replacement_value, variable
#> Warning: NAs introduced by coercion
#> Warning: NAs introduced by coercion
#> date and time columns present, creating formatted datetime column
#> date and time columns present, creating formatted datetime column
#> 22 rows removed with no coordinates
#> date and time columns present, creating formatted datetime column
#> 22 rows removed with no coordinates
#> date and time columns present, creating formatted datetime column
#> 22 rows removed with no coordinates
#> Warning: some mark values are NA in the point pattern x
#> date and time columns present, creating formatted datetime column
#> 22 rows removed with no coordinates
#> Warning: 105096 points were rejected as lying outside the specified window
#> Warning: some mark values are NA in the point pattern x

# }
```
