# Format STATS19 vehicles data

Format STATS19 vehicles data

## Usage

``` r
format_vehicles(x)
```

## Arguments

- x:

  Data frame created with
  [`read_vehicles()`](https://docs.ropensci.org/stats19/reference/read_vehicles.md)

## Details

This function formats raw STATS19 data

## Examples

``` r
# \donttest{
if(curl::has_internet()) {
dl_stats19(year = 2022, type = "vehicle", ask = FALSE)
x = read_vehicles(year = 2022, format = FALSE)
vehicles = format_vehicles(x)
}
#> Files identified: dft-road-casualty-statistics-vehicle-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-vehicle-2022.csv
#> Data saved at /tmp/RtmpYK4NLW/dft-road-casualty-statistics-vehicle-2022.csv
#> Warning: The following named parsers don't match the column names: age_band_of_casualty, age_of_casualty, bus_or_coach_passenger, car_passenger, casualty_adjusted_serious, casualty_adjusted_slight, casualty_class, casualty_distance_banding, casualty_imd_decile, casualty_injury_based, casualty_reference, casualty_severity, casualty_type, enhanced_casualty_severity, lsoa_of_casualty, pedestrian_location, pedestrian_movement, pedestrian_road_maintenance_worker, sex_of_casualty, carriageway_hazards, carriageway_hazards_historic, collision_adjusted_serious, collision_adjusted_slight, collision_injury_based, collision_severity, date, day_of_week, did_police_officer_attend_scene_of_accident, did_police_officer_attend_scene_of_collision, enhanced_collision_severity, first_road_class, first_road_number, junction_control, junction_detail, junction_detail_historic, latitude, light_conditions, local_authority_district, local_authority_highway, local_authority_highway_current, local_authority_ons_district, location_easting_osgr, location_northing_osgr, longitude, lsoa_of_accident_location, lsoa_of_collision_location, number_of_casualties, number_of_vehicles, pedestrian_crossing, pedestrian_crossing_human_control_historic, pedestrian_crossing_physical_facilities_historic, police_force, road_surface_conditions, road_type, second_road_class, second_road_number, special_conditions_at_site, speed_limit, time, trunk_road_flag, urban_or_rural_area, weather_conditions, accident_index, accident_ref_no, accident_year, effective_date_of_change, previously_published_value, replacement_value, variable
#> Warning: NAs introduced by coercion
#> Warning: NAs introduced by coercion
# }
```
