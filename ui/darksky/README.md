# Dark Sky Weather Card

![image](https://github.com/888JW/home-assistant-config/blob/master/dark-sky-weather-card-extended.gif)

The Dark Sky Weather Card provides current and forecasted weather conditions using the Dark Sky platform. You configure the card by passing in sensor entities from the Dark Sky Sensor platform.  

The card is very customizable.  You can configure many aspects of it's look and feel as well as which specific content to show by passing in customization flags and defining optional sensors.  Content can also be rearranged if desired. 

Hovering over a forecast day will display the daily weather summary in a tooltip popup if that option has been enabled.


**Installation**
------------------------------
1. Add ```dark-sky-weather-card.js``` to your ```<config-dir>/www/custom_ui/``` directory.  If you don't have this directory (this is your first custom card), you will need to create it.

2. Download the amcharts icons from https://www.amcharts.com/dl/svg-weather-icons/ and put them in ```<config-dir>/www/icons/weather_icons```.  Create the directories if necessary.

You should end up with the following folders:

```<config-dir>/www/custom_ui/dark-sky-weather-card.js```

```<config-dir>/www/icons/weather_icons/animated/```

```<config-dir>/www/icons/weather_icons/static/```

**Configuration**
------------------------------
1. Add the Dark Sky sensor platform to your configuration.yaml or sensors.yaml or wherever you keep your sensor configuration.

~~~~  
- platform: darksky
    api_key: <Your Dark Sky API Key>
    forecast:
      - 0
      - 1
      - 2
      - 3
      - 4
      - 5
    monitored_conditions:
      - icon
      - summary
      - nearest_storm_distance
      - nearest_storm_bearing
      - humidity
      - temperature
      - temperature_high
      - temperature_low
      - apparent_temperature
      - apparent_temperature_high
      - apparent_temperature_low
      - wind_speed
      - wind_bearing
      - precip_type
      - precip_probability
      - precip_accumulation
      - precip_intensity
      - precip_intensity_max
      - uv_index
      - daily_summary
      - pressure
      - visibility
    scan_interval:
      minutes: 5
      
** If you would like to use the hourly and short term forecast views then you must also add:
  
    hourly_forecast:
      - 0
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 10
      - 11
      - 12
      - 13
      - 14
      - 15
      - 16
      - 17
      - 18
      - 19
      - 20
      - 21
      - 22
      - 23
      - 24      
~~~~

The next two steps are completed differently based on the version of HA you are using:
- Pre 0.84 or if using yaml mode in 0.84 or above : Add to your ui-lovelace.yaml file.
- Using storage mode in 0.84 or above use the "Raw Config Editor" to add the reference and definition to the config.

2. Add the card reference at the top of the configuration

   **Note: Ensure type is set to module and not js**  
   **Note: /local/ points to the ```<config-dir>/www/``` dir.**

~~~~
resources:
  - url: /local/custom_ui/dark-sky-weather-card.js?v=7.1
    type: module
~~~~

3. Add the card definition:  There are required / optional and flag entries.  

Required entries must be present 
in your configuration.  The card will not work at all if any of these lines are missing. 
~~~~
type: 'custom:dark-sky-weather-card'
entity_current_conditions: sensor.dark_sky_icon
entity_temperature: sensor.dark_sky_temperature
entity_forecast_high_temp_1: sensor.dark_sky_daytime_high_temperature_1d
entity_forecast_high_temp_2: sensor.dark_sky_daytime_high_temperature_2d
entity_forecast_high_temp_3: sensor.dark_sky_daytime_high_temperature_3d
entity_forecast_high_temp_4: sensor.dark_sky_daytime_high_temperature_4d
entity_forecast_high_temp_5: sensor.dark_sky_daytime_high_temperature_5d
entity_forecast_icon_1: sensor.dark_sky_icon_1d
entity_forecast_icon_2: sensor.dark_sky_icon_2d
entity_forecast_icon_3: sensor.dark_sky_icon_3d
entity_forecast_icon_4: sensor.dark_sky_icon_4d
entity_forecast_icon_5: sensor.dark_sky_icon_5d
entity_forecast_low_temp_1: sensor.dark_sky_overnight_low_temperature_0d
entity_forecast_low_temp_2: sensor.dark_sky_overnight_low_temperature_1d
entity_forecast_low_temp_3: sensor.dark_sky_overnight_low_temperature_2d
entity_forecast_low_temp_4: sensor.dark_sky_overnight_low_temperature_3d
entity_forecast_low_temp_5: sensor.dark_sky_overnight_low_temperature_4d
entity_summary_1: sensor.dark_sky_summary_1d
entity_summary_2: sensor.dark_sky_summary_2d
entity_summary_3: sensor.dark_sky_summary_3d
entity_summary_4: sensor.dark_sky_summary_4d
entity_summary_5: sensor.dark_sky_summary_5d
~~~~

Optional entries add components to the card. 
***Please note entity_pop_1 to 5 lines must all be included for daily pop (probability of precip) to show in forecast
~~~~
entity_sun: sun.sun
entity_visibility: sensor.dark_sky_visibility
entity_daytime_high: sensor.dark_sky_daytime_high_temperature_0d
entity_wind_bearing: sensor.dark_sky_wind_bearing
entity_wind_speed: sensor.dark_sky_wind_speed
entity_humidity: sensor.dark_sky_humidity
entity_pressure: sensor.dark_sky_pressure
entity_apparent_temp: sensor.dark_sky_apparent_temperature
entity_daily_summary: sensor.dark_sky_daily_summary
entity_pop: sensor.dark_sky_precip_probability
entity_pop_intensity: sensor.dark_sky_precip_intensity
entity_pop_1: sensor.dark_sky_precip_probability_1d
entity_pop_2: sensor.dark_sky_precip_probability_2d
entity_pop_3: sensor.dark_sky_precip_probability_3d
entity_pop_4: sensor.dark_sky_precip_probability_4d
entity_pop_5: sensor.dark_sky_precip_probability_5d
~~~~

Optional entries required to use the hourly and short term forecast (sorry - makes the config bloated)
~~~~
entity_hourly_apparent_0: sensor.dark_sky_apparent_temperature_0h
entity_hourly_apparent_1: sensor.dark_sky_apparent_temperature_1h
entity_hourly_apparent_2: sensor.dark_sky_apparent_temperature_2h
entity_hourly_apparent_3: sensor.dark_sky_apparent_temperature_3h
entity_hourly_apparent_4: sensor.dark_sky_apparent_temperature_4h
entity_hourly_apparent_5: sensor.dark_sky_apparent_temperature_5h
entity_hourly_apparent_6: sensor.dark_sky_apparent_temperature_6h
entity_hourly_apparent_7: sensor.dark_sky_apparent_temperature_7h
entity_hourly_apparent_8: sensor.dark_sky_apparent_temperature_8h
entity_hourly_apparent_9: sensor.dark_sky_apparent_temperature_9h
entity_hourly_apparent_10: sensor.dark_sky_apparent_temperature_10h
entity_hourly_apparent_11: sensor.dark_sky_apparent_temperature_11h
entity_hourly_apparent_12: sensor.dark_sky_apparent_temperature_12h
entity_hourly_apparent_13: sensor.dark_sky_apparent_temperature_13h
entity_hourly_apparent_14: sensor.dark_sky_apparent_temperature_14h
entity_hourly_apparent_15: sensor.dark_sky_apparent_temperature_15h
entity_hourly_apparent_16: sensor.dark_sky_apparent_temperature_16h
entity_hourly_apparent_17: sensor.dark_sky_apparent_temperature_17h
entity_hourly_apparent_18: sensor.dark_sky_apparent_temperature_18h
entity_hourly_apparent_19: sensor.dark_sky_apparent_temperature_19h
entity_hourly_apparent_20: sensor.dark_sky_apparent_temperature_20h
entity_hourly_apparent_21: sensor.dark_sky_apparent_temperature_21h
entity_hourly_apparent_22: sensor.dark_sky_apparent_temperature_22h
entity_hourly_apparent_23: sensor.dark_sky_apparent_temperature_23h
entity_hourly_apparent_24: sensor.dark_sky_apparent_temperature_24h
entity_hourly_icon_0: sensor.dark_sky_icon_0h
entity_hourly_icon_1: sensor.dark_sky_icon_1h
entity_hourly_icon_2: sensor.dark_sky_icon_2h
entity_hourly_icon_3: sensor.dark_sky_icon_3h
entity_hourly_icon_4: sensor.dark_sky_icon_4h
entity_hourly_icon_5: sensor.dark_sky_icon_5h
entity_hourly_icon_6: sensor.dark_sky_icon_6h
entity_hourly_icon_7: sensor.dark_sky_icon_7h
entity_hourly_icon_8: sensor.dark_sky_icon_8h
entity_hourly_icon_9: sensor.dark_sky_icon_9h
entity_hourly_icon_10: sensor.dark_sky_icon_10h
entity_hourly_icon_11: sensor.dark_sky_icon_11h
entity_hourly_icon_12: sensor.dark_sky_icon_12h
entity_hourly_icon_13: sensor.dark_sky_icon_13h
entity_hourly_icon_14: sensor.dark_sky_icon_14h
entity_hourly_icon_15: sensor.dark_sky_icon_15h
entity_hourly_icon_16: sensor.dark_sky_icon_16h
entity_hourly_icon_17: sensor.dark_sky_icon_17h
entity_hourly_icon_18: sensor.dark_sky_icon_18h
entity_hourly_icon_19: sensor.dark_sky_icon_19h
entity_hourly_icon_20: sensor.dark_sky_icon_20h
entity_hourly_icon_21: sensor.dark_sky_icon_21h
entity_hourly_icon_22: sensor.dark_sky_icon_22h
entity_hourly_icon_23: sensor.dark_sky_icon_23h
entity_hourly_icon_24: sensor.dark_sky_icon_24h
entity_hourly_pop_0: sensor.dark_sky_precip_probability_0h
entity_hourly_pop_1: sensor.dark_sky_precip_probability_1h
entity_hourly_pop_2: sensor.dark_sky_precip_probability_2h
entity_hourly_pop_3: sensor.dark_sky_precip_probability_3h
entity_hourly_pop_4: sensor.dark_sky_precip_probability_4h
entity_hourly_pop_5: sensor.dark_sky_precip_probability_5h
entity_hourly_pop_6: sensor.dark_sky_precip_probability_6h
entity_hourly_pop_7: sensor.dark_sky_precip_probability_7h
entity_hourly_pop_8: sensor.dark_sky_precip_probability_8h
entity_hourly_pop_9: sensor.dark_sky_precip_probability_9h
entity_hourly_pop_10: sensor.dark_sky_precip_probability_10h
entity_hourly_pop_11: sensor.dark_sky_precip_probability_11h
entity_hourly_pop_12: sensor.dark_sky_precip_probability_12h
entity_hourly_pop_13: sensor.dark_sky_precip_probability_13h
entity_hourly_pop_14: sensor.dark_sky_precip_probability_14h
entity_hourly_pop_15: sensor.dark_sky_precip_probability_15h
entity_hourly_pop_16: sensor.dark_sky_precip_probability_16h
entity_hourly_pop_17: sensor.dark_sky_precip_probability_17h
entity_hourly_pop_18: sensor.dark_sky_precip_probability_18h
entity_hourly_pop_19: sensor.dark_sky_precip_probability_19h
entity_hourly_pop_20: sensor.dark_sky_precip_probability_20h
entity_hourly_pop_21: sensor.dark_sky_precip_probability_21h
entity_hourly_pop_22: sensor.dark_sky_precip_probability_22h
entity_hourly_pop_23: sensor.dark_sky_precip_probability_23h
entity_hourly_pop_24: sensor.dark_sky_precip_probability_24h
entity_hourly_summary_0: sensor.dark_sky_summary_0h
entity_hourly_summary_1: sensor.dark_sky_summary_1h
entity_hourly_summary_2: sensor.dark_sky_summary_2h
entity_hourly_summary_3: sensor.dark_sky_summary_3h
entity_hourly_summary_4: sensor.dark_sky_summary_4h
entity_hourly_summary_5: sensor.dark_sky_summary_5h
entity_hourly_summary_6: sensor.dark_sky_summary_6h
entity_hourly_summary_7: sensor.dark_sky_summary_7h
entity_hourly_summary_8: sensor.dark_sky_summary_8h
entity_hourly_summary_9: sensor.dark_sky_summary_9h
entity_hourly_summary_10: sensor.dark_sky_summary_10h
entity_hourly_summary_11: sensor.dark_sky_summary_11h
entity_hourly_summary_12: sensor.dark_sky_summary_12h
entity_hourly_summary_13: sensor.dark_sky_summary_13h
entity_hourly_summary_14: sensor.dark_sky_summary_14h
entity_hourly_summary_15: sensor.dark_sky_summary_15h
entity_hourly_summary_16: sensor.dark_sky_summary_16h
entity_hourly_summary_17: sensor.dark_sky_summary_17h
entity_hourly_summary_18: sensor.dark_sky_summary_18h
entity_hourly_summary_19: sensor.dark_sky_summary_19h
entity_hourly_summary_20: sensor.dark_sky_summary_20h
entity_hourly_summary_21: sensor.dark_sky_summary_21h
entity_hourly_summary_22: sensor.dark_sky_summary_22h
entity_hourly_summary_23: sensor.dark_sky_summary_23h
entity_hourly_summary_24: sensor.dark_sky_summary_24h
entity_hourly_temp_0: sensor.dark_sky_temperature_0h
entity_hourly_temp_1: sensor.dark_sky_temperature_1h
entity_hourly_temp_2: sensor.dark_sky_temperature_2h
entity_hourly_temp_3: sensor.dark_sky_temperature_3h
entity_hourly_temp_4: sensor.dark_sky_temperature_4h
entity_hourly_temp_5: sensor.dark_sky_temperature_5h
entity_hourly_temp_6: sensor.dark_sky_temperature_6h
entity_hourly_temp_7: sensor.dark_sky_temperature_7h
entity_hourly_temp_8: sensor.dark_sky_temperature_8h
entity_hourly_temp_9: sensor.dark_sky_temperature_9h
entity_hourly_temp_10: sensor.dark_sky_temperature_10h
entity_hourly_temp_11: sensor.dark_sky_temperature_11h
entity_hourly_temp_12: sensor.dark_sky_temperature_12h
entity_hourly_temp_13: sensor.dark_sky_temperature_13h
entity_hourly_temp_14: sensor.dark_sky_temperature_14h
entity_hourly_temp_15: sensor.dark_sky_temperature_15h
entity_hourly_temp_16: sensor.dark_sky_temperature_16h
entity_hourly_temp_17: sensor.dark_sky_temperature_17h
entity_hourly_temp_18: sensor.dark_sky_temperature_18h
entity_hourly_temp_19: sensor.dark_sky_temperature_19h
entity_hourly_temp_20: sensor.dark_sky_temperature_20h
entity_hourly_temp_21: sensor.dark_sky_temperature_21h
entity_hourly_temp_22: sensor.dark_sky_temperature_22h
entity_hourly_temp_23: sensor.dark_sky_temperature_23h
entity_hourly_temp_24: sensor.dark_sky_temperature_24h
~~~~

**Note:** The following entries require template sensors.  The alt_* entries are for overriding the text for the indicated slot entry. By using these you can create whatever format you like for these entries.
~~~~
entity_current_text: sensor.dark_sky_current_text
alt_daytime_high: sensor.dark_sky_alt_daytime_high 
alt_wind: sensor.dark_sky_alt_wind
alt_visibility: sensor.dark_sky_alt_visibility
alt_pop: sensor.dark_sky_alt_pop
alt_pressure: sensor.dark_sky_alt_pressure
alt_humidity: sensor.dark_sky_alt_humidity
~~~~

**Example template sensors:** You can call template sensors whatever you want so long as you use the same name in the card config.  
~~~~~
      dark_sky_current_text:
        value_template:  {% if is_state("sensor.dark_sky_icon","clear-day") %} Clear 
                         {% elif is_state("sensor.dark_sky_icon","clear-night") %} Clear 
                         {% elif is_state("sensor.dark_sky_icon","rain") %} Rain
                         {% elif is_state("sensor.dark_sky_icon","snow") %} Snowy
                         {% elif is_state("sensor.dark_sky_icon","fog") %} Foggy
                         {% elif is_state("sensor.dark_sky_icon","sleet") %} Sleet
                         {% elif is_state("sensor.dark_sky_icon","wind") %} Windy
                         {% elif is_state("sensor.dark_sky_icon","cloudy") %} Cloudy
                         {% elif is_state("sensor.dark_sky_icon","partly-cloudy-day") %} Partly Cloudy
                         {% elif is_state("sensor.dark_sky_icon","partly-cloudy-night") %} Partly Cloudy
                         {% elif is_state("sensor.dark_sky_icon","hail") %} Hailing
                         {% elif is_state("sensor.dark_sky_icon","lightning") %} Lightning
                         {% elif is_state("sensor.dark_sky_icon","thunderstorm") %} Thunderstorm
                         {% endif %}
                         
      dark_sky_alt_wind:
        value_template: >-
                        {% set winddir = ['North','North-Northeast','Northeast','East-Northeast','East','East-Southeast','Southeast','South-Southeast','South','South-Southwest','Southwest','West-Southwest','West','West-Northwest','Northwest','North-Northwest','North'] %}
                        {{ states('sensor.dark_sky_wind_speed') | round }} mi/h from the {{ winddir[((states('sensor.dark_sky_wind_bearing') | float / 360)*16) | round]}}
~~~~~

Flags are used to control the look and feel of the card (See below for details)
~~~~
locale: en
static_icons: false
tooltip_bg_color: 'rgb( 75,155,239)'
tooltip_border_color: orange
tooltip_border_width: 3
tooltip_caret_size: 10
tooltip_fg_color: '#fff'
tooltip_left_offset: -12
tooltip_width: 100
tooltips: true
old_daily_format: false
time_format: 24
show_beaufort: true

extended_info: true
cycle_duration: 60
forecast_icon_margin_right: 4px
forecast_icon_size: 60px
forecast_labels: true
forecast_labels_colour: blue
large_icon_size: 14em




~~~~

**Flags**
--------------------------
| Flag                     | Values                      | Usage                                                                       |
|--------------------------|-----------------------------|-----------------------------------------------------------------------------|
| locale                   | **en** / fr / de / etc.     | Sets locale display of day names and time formats                           |
| static_icons             | true / **false**            | Switches between static (true) and animated (false) icons                   |
| tooltips                 | true / **false**            | Enables tooltips that show daily forecast summary                           |
| tooltip_width            | **110**                     | Sets the width of the tooltip in px                                         |
| tooltip_bg_color         | **rgb( 75,155,239)**        | Sets the background color of the tooltip (rgb / # / color)                  |
| tooltip_fg_color         | **#fff**                    | Sets the foreground color of the tooltip (rgb / # / color)                  |
| tooltip_border_color     | **rgb(255,161,0)**          | Sets the color of the tooltip border including the caret (rgb / # / color)  |
| tooltip_border_width     | **1**                       | Sets the width of the tooltip border in px                                  |
| tooltip_caret_size       | **5**                       | Sets the size of the caret (the little arrow pointing down) in px           |
| tooltip_left_offset      | **-12**                     | Sets the offset of the left edge of the tooltip. In negative (-)x           |
| refresh_interval         | **30** / Integer value      | Sets the nuber of seconds between card value refreshes                      |
| old_daily_format         | true / **false**            | Sets the format of the daily high & low temps to be stacked (old format)    |
| show_beaufort            | true / **false**            | Shows Beaufort Scale wind information                                       |
| show_separator           | true / **false**            | Shows separator between current conditions columns and current temp / Icon  |
| time_format              | **locale** / 12 / 24        | Sets the format sunset and sunrise times. locale format is the default.     |
| temp_top_margin          | **-.3em** / px or em value  | Sets the top margin of the Temperature.                                     |
| temp_font_weight         | **300** / numeric value     | Sets the font weight of the Temperature.                                    |
| temp_font_size           | **4em** / em value          | Sets the font size of the Temperature.                                      |
| temp_right_pos           | **.85em** / px or em value  | Sets the right position of the Temperature.                                 |
| temp_uom_top_margin      | **-9px** / px or em value   | Sets the top margin of the Temperature Unit of Meaure.                      |
| temp_uom_right_margin    | **7px** / px or em value    | Sets the right margin of the Temperature Unit of Measure.                   |
| apparent_top_margin      | **39px** / px or em value   | Sets the top margin of the apparent (feels Like) temperature                |
| apparent_right_pos       | **1em** / px or em value    | Sets the right position of the apparent (feels Like) temperature            |
| apparent_right_margin    | **1em** / px or em value    | Sets the right margin of the apparent (feels Like) temperature              |
| current_text_top_margin  | **39px** / px or em value   | Sets the top margin of the current temperature text                         |
| current_text_left_pos    | **5em** / px or em value    | Sets the left position of the current temperature text                      |
| current_text_font_size   | **1.5em** / em value        | Sets the font size of the current temperature text                          |
| current_data_top_margin  | **6em** / px or em value    | Sets the top margin of the current data blocks                              |
| large_icon_top_margin    | **-3.5em** / px or em value | Sets the top margin of the current conditions icon                          |
| large_icon_left_position | **0em** / px or em value    | Sets the left position of the current conditions icon                       |
| separator_top_margin     | **5em** / px or em value    | Sets the top margin of the separator line                                   |
| slot_l1                  | **daytime_high**            | Sets the value used in current conditions slot l1 : See slots for more info |
| slot_l2                  | **wind**                    | Sets the value used in current conditions slot l2 : See slots for more info |
| slot_l3                  | **visibility**              | Sets the value used in current conditions slot l3 : See slots for more info |
| slot_l4                  | **sun_next**                | Sets the value used in current conditions slot l4 : See slots for more info |
| slot_r1                  | **pop**                     | Sets the value used in current conditions slot r1 : See slots for more info |
| slot_r2                  | **humidity**                | Sets the value used in current conditions slot r2 : See slots for more info |
| slot_r3                  | **pressure**                | Sets the value used in current conditions slot r3 : See slots for more info |
| slot_r4                  | **sun_following**           | Sets the value used in current conditions slot r4 : See slots for more info |
|extended_info             |  true / **false**           | If set to true then the hourly and short term forecast will be displayed    |
|cycle_duration            |  **60**                     | Sets the # of seconds to cycle through daily/short-term/hourly forecasts    |
|forecast_icon_margin_right|  **5px**  /px or em value   | Sets the right margin of the small forecast icons                           |
|forecast_icon_size        |  **50px** /px or em value   | Sets the size of the small forecast icons                                   |
|forecast_labels           |  true / **false**           | If set to true then labels will be displayed beside the rows of forecast #s |
|forecast_labels_colour    |  **#d9d9d9**                | Colour of the forecast labels (if forecast_labels = true                    |
|large_icon_size           |  **10em** /px or em value   | Sets the size of the large icon for current weather                         |


**Slots**
--------------------------
The current condition columns are specified by 'slots'.  There are 4 left column slots (designated l1 - l4) and 4 right column
slots (designated r1 - r4).  There are currently 10 possible values that can be assigned to a slot.  These are:
- daytime_high
- wind
- visibility
- sun_next (the next sun event ... sunset or sunrise)
- sun_following (The following sun event ... if sun_next is a sunset then this will be the following sunrise and vice versa)
- pop (probability of precipitation)
- humidity
- pressure
- empty (empty slot... the slot below does not rise to fill the space)
- remove (same as empty but the slot below rises to take the place of the slot)
