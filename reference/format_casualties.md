# Format STATS19 casualties

Format STATS19 casualties

## Usage

``` r
format_casualties(x)
```

## Arguments

- x:

  Data frame created with
  [`read_casualties()`](https://docs.ropensci.org/stats19/reference/read_casualties.md)

## Details

This function formats raw STATS19 data

## Examples

``` r
# \donttest{
if(curl::has_internet()) {
dl_stats19(year = 2022, type = "casualty")
x = read_casualties(year = 2022)
casualties = format_casualties(x)
}
#> Files identified: dft-road-casualty-statistics-casualty-2022.csv
#>    https://data.dft.gov.uk/road-accidents-safety-data/dft-road-casualty-statistics-casualty-2022.csv
#> Data already exists in data_dir, not downloading
#> Warning: The following named parsers don't match the column names: casualty_adjusted_serious, casualty_adjusted_slight, carriageway_hazards, carriageway_hazards_historic, collision_adjusted_serious, collision_adjusted_slight, collision_injury_based, collision_severity, date, day_of_week, did_police_officer_attend_scene_of_accident, did_police_officer_attend_scene_of_collision, enhanced_collision_severity, first_road_class, first_road_number, junction_control, junction_detail, junction_detail_historic, latitude, light_conditions, local_authority_district, local_authority_highway, local_authority_highway_current, local_authority_ons_district, location_easting_osgr, location_northing_osgr, longitude, lsoa_of_accident_location, lsoa_of_collision_location, number_of_casualties, number_of_vehicles, pedestrian_crossing, pedestrian_crossing_human_control_historic, pedestrian_crossing_physical_facilities_historic, police_force, road_surface_conditions, road_type, second_road_class, second_road_number, special_conditions_at_site, speed_limit, time, trunk_road_flag, urban_or_rural_area, weather_conditions, accident_index, accident_ref_no, accident_year, effective_date_of_change, previously_published_value, replacement_value, variable, age_band_of_driver, age_of_driver, age_of_vehicle, driver_distance_banding, driver_imd_decile, engine_capacity_cc, escooter_flag, first_point_of_impact, generic_make_model, hit_object_in_carriageway, hit_object_off_carriageway, journey_purpose_of_driver, journey_purpose_of_driver_historic, junction_location, lsoa_of_driver, propulsion_code, sex_of_driver, skidding_and_overturning, towing_and_articulation, vehicle_direction_from, vehicle_direction_to, vehicle_leaving_carriageway, vehicle_left_hand_drive, vehicle_location_restricted_lane, vehicle_location_restricted_lane_historic, vehicle_manoeuvre, vehicle_manoeuvre_historic, vehicle_type
#> Warning: NAs introduced by coercion
# }
```
