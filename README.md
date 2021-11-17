# Avalanche.org Public API User Guide

The public API provides access to daily backcountry avalanche danger ratings for specific geographic areas in the US. These areas generally correspond with mountainous regions which see high recreational use. 

The data is limited to the danger level on a scale of 1 - 5 as defined in the North American Avalanche Danger Scale. The full avalanche forecast(s) can be accessed through individual avalanche center websites.

Avalanche.org collects and distributes this data from 20 independent forecasting operations working under a collective initiative. As a result, it is very important that 3rd party use does not somehow inadvertently change the intent, understanding, or accuracy of the information -- doing so could jeopardize the collective. 

For example, because avalanche danger changes on a day-to-day basis, danger rating displays must be published and expired accordingly. 

## Backcountry Avalanche Forecasting in the US
More information can be found on avalanche.org:

* Avalanche Danger Scale: https://avalanche.org/avalanche-encyclopedia/danger-scale/
* Avalanche Centers in the US: https://avalanche.org/us-avalanche-centers/
* National Avalanche Danger Map: https://avalanche.org/

## Update cadence
Avalanche centers who publish a daily forecast will typically do so once a day in the morning. It is recommended to check often during the morning hours (6-10am Mountain Time). The season varies by year and avalanche center, but generally follows December - April.

Some avalanche centers publish summary information without a danger rating. These will show up as `no danger` throughout the season, but general backcountry conditions can be found by navigating to their site

## Avalanche Danger Map Guideline: 

Resolution - 1:25,000 (approximately slippy map zoom 14)

Participating organizations are represented using polygons which depict the area for which information is available and representative. These polygons display danger ratings by color, or the grey scale which indicates summary information is available.

Recommended style guidelines: 
* Polygons are drawn with a black line, with the following exception: 
* Polygons are outlined in a thick red line red during periods of EXTREME danger. 
* Polygons display the highest danger rating assigned for that zone during a 24hr period.
* Colors correspond to the NAADS, with the following exceptions: 
    * Grey shading with blue outline means  “Avalanche Information Available - No Rating” 
    * No shading (just the black outline) means “No information Available”.

Associated information for polygons:  
* Zone name, date issued and expiration, Avalanche Center name
* Avalanche danger (color, icon, nomenclature), or summary statement

Associated travel advice
* Link to Forecast or Summary Product (this opens AC forecast page)
* If no information is available, link to AC homepage


# Map Layer

A <a href='https://geojson.org/'>geojson</a> representation of the avalanche centers and the current avalanche forecast.

`GET /v2/public/products/map-layer`

## Request
```bash

curl https://api.avalanche.org/v2/public/products/map-layer
```

## Response
```json
{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "id": 213,
            "properties": {
                "name": "Chilkat Pass",
                "center": "Alaska Avalanche Center",
                "center_link": "https://alaskasnow.org/",
                "timezone": "America/Anchorage",
                "center_id": "AAIC",
                "state": "AK",
                "travel_advice": "Watch for signs of unstable snow such as recent avalanches, cracking in the snow, and audible collapsing. Avoid traveling on or under similar slopes.",
                "danger": "no rating",
                "danger_level": -1,
                "color": "#cccccc",
                "stroke": "#104efb",
                "font_color": "#ffffff",
                "link": "http://alaskasnow.org/multi-zone-haines-forecasts/chilkat-pass-forecast/",
                "start_date": null,
                "end_date": null,
                "fillOpacity": 0.5,
                "fillIncrement": 0.1,
                "warning": {
                    "product": null
                }
            },
            "geometry": {
                "type": "Polygon",
                "coordinates": [
                    [
                        [
                            -136.6056,
                            59.723
                        ],
                        [
                            -136.6693,
                            59.7346
                        ],
```

A description of the properties are:

* name: Zone name
* center: Avalanche center name
* center_link: Link to avalanche center website
* timezone: Timezone that the avalanche center uses
* center_id: The avalanche center acronym 
* state: The state which the avalanche center largely operates in
* travel_advice: The standard travel advice for the given danger rating
* danger: Textual representation of the danger rating
* danger_level: Numerical of the danger rating
* color: The danger rating color
* stroke: The danger rating outline color
* font_color: The font color which contrasts with the danger rating color
* link: Link to the forecast page for the given zone
* start_date: When the forecast was issued (ISO)
* end_date: When the forecast expires (ISO)
* warning: Populated if an avalanche warning is issued for the given zone


## Map layer by avalanche center

A <a href='https://geojson.org/'>geojson</a> representation for the given avalanche center and the current avalanche forecast.

`GET /v2/public/products/map-layer/{avalanche_center_id}`

## Request
```bash

curl https://api.avalanche.org/v2/public/products/map-layer/SNFAC
```

## Response

```json
{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "id": 301,
            "properties": {
                "name": "Galena Summit & Eastern Mtns",
                "center": "Sawtooth Avalanche Center",
                "timezone": "America/Denver",
                "state": "ID",
                "rating": 1,
                "travel_advice": "Generally safe avalanche conditions. Watch for unstable snow on isolated terrain features.",
                "danger": "low",
                "danger_level": 1,
                "color": "#55b64f",
                "stroke": "#484848",
                "font_color": "#ffffff",
                "link": "https://www.sawtoothavalanche.com/forecasts/#/galena-summit-&-eastern-mtns",
                "start_date": "2020-09-02T16:55:00",
                "end_date": "2020-09-03T12:00:00",
                "warning": {
                    "product": null,
                    "start_date": null,
                    "end_date": null,
                    "reason": null
                }
            },
            "geometry": {
                "type": "Polygon",
                "coordinates": [

```
