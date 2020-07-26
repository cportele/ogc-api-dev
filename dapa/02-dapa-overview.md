# Data retrieval patterns - DAPA overview

In addition to the access to the [raw observation data](01-access-features.md), additional patterns to access and process the observation data are available via Data Access and Processing API (DAPA) endpoints, that are currently explored in OGC Testbed-16. The goal is to simplfy the use of the data for end-users, for example, for use in Jupyter Notebooks. Data retrieval in DAPA is based on the selection of the observations by the spatial sampling geometry (point, area, or grid), the temporal sampling geometry (instant or interval), and the observed properties followed by optional post-processing to aggregate observations by space and/or time.

The Data Access and Processing API endpoints are fully specified in the [API documentation](http://t16.ldproxy.net/ghcnd/api/?f=html#/DAPA).

The API covers the two Use Case types mentioned in the OGC Testbed-16 Call for Proposals, [Data Retrieval](https://portal.ogc.org/files/?artifact_id=91644#UseCaseDataRetrieval) and [Data Processing](https://portal.ogc.org/files/?artifact_id=91644#UseCaseDataProcessing).

As mentioned above, DAPA endpoints process the data in two phases, which are described in the next sections.

## Phase 1: Data access

The first phase selects the observations to retrieve. This is in a way similar to the raw data access described above, but while the OGC API Features endpoints can be used with all kinds of features, the DAPA selection pattern is based on the knowledge that the set of all observations can be viewed as a spatio-temporal data cube.

The data is selected based on three aspects:

* the spatial sampling geometry (point, area, or grid),
* the temporal sampling geometry (instant or interval), and
* the observed properties / variables to retrieve.

The resulting data can be requested as CSV, GeoJSON or GeoTIFF (only for grid).

### Spatial sampling geometry

#### Point

The observations at the location are retrieved. The results are in general interpolated from other observations. The result is a time series for each variable.

The location of the point can be provided in one of two ways:

The first is a Well Known Text (WKT) point geometry in the parameter `coord`. Example: `POINT(6.9299617 50.000008)`. This is also the default point sampling geometry, if neither `coord` nor `coordRef` is specified.

The second is a URI in the parameter `coordRef` where the URI returns a GeoJSON feature, e.g. a request to an API that implements OGC API features or a request to the OpenStreetMap geocoding API. If the feature geometry is not a point, the centroid is used. Some example URIs are:

* The city of Bonn, Germany: https://www.ldproxy.nrw.de/dvg/collections/nw_dvg2_gem/items/nw_dvg2_gem.05314000?f=json
* A cadastral parcel in Bonn, Germany: https://www.ldproxy.nrw.de/kataster/collections/flurstueck/items/DENW36AL10005X65FL?f=json
* The city of Washington, DC, USA: https://nominatim.openstreetmap.org/search?q=Washington&format=geojson&limit=1

#### Area

The observations in the area are retrieved. The result is a time series for each variable and each weather station.

The polygon of the area can be provided in one of three ways:

The first is a bounding box in parameter `bbox` consisting of four numbers, separated by commas: minimum longitude, minimum latitude, maxmium longitude, maxmimum latitude. Example: `6,48.5,8,50.5`. This is also the default area sampling geometry, if neither `bbox`, `coord` nor `coordRef` is specified.

The second is a Well Known Text (WKT) polygon or multi-polygon geometry in the parameter `coord`.

The third is a URI in the parameter `coordRef` where the URI returns a GeoJSON feature, e.g. a request to an API that implements OGC API features. If the feature geometry is not a polygon or multi-polygon, a buffer is added and the bounding box of the resulting geometry is used. Some example URIs are:

* The city of Bonn, Germany: https://www.ldproxy.nrw.de/dvg/collections/nw_dvg2_gem/items/nw_dvg2_gem.05314000?f=json
* The State North-Rhine Westphalia in Germany: https://www.ldproxy.nrw.de/dvg/collections/nw_dvg2_bld/items/nw_dvg2_bld.05000000?f=json

#### Grid

The observations in the grid area are retrieved and resampled to the spatio-temporal grid. The result is a time series for each variable and each grid cell.

The area of the grid can be provided in one of two ways:

The first is a bounding box in parameter `bbox` consisting of four numbers, separated by commas: minimum longitude, minimum latitude, maxmium longitude, maxmimum latitude. Example: `6,48.5,8,50.5`. This is also the default area sampling geometry, if neither `bbox`, `coord` nor `coordRef` is specified.

The second is a URI in the parameter `coordRef` where the URI returns a GeoJSON feature, e.g. a request to an API that implements OGC API features. The bounding box of the resulting geometry is used. For example URI see above.

The number of spatial grid cells is determined by parameters `width` and `height`. The default for `width` is `10`, the default for `height` is computed from the grid area and the `width` value.

### Temporal sampling geometry

The temporal sampling geometry is always provided in the parameter `datetime`. Use dates. Intervals are expressed according to ISO 8601. Open intervals are supported, too. Examples:

* `2019-07-29`: July 29,2019
* `2019-08-07/2019-08-11`: August 7-11, 2019 (this is also the default sampling geometry, if `datetime` is not provided)
* `../2019-02-28`: Until February 28, 2019 (since the first observation is on 2019-01-01 this is the same as `2019-01-01/2019-02-28`)
* `2019-11-15/..`: November 15, 2019, and later (since the last observation is on 2019-12-31 this is the same as `2019-11-15/2019-12-31`)

### Observed properties

One or more observed properties or variables can be accessed. The values are provided as a comma-separated list in parameter `variables`.

The supported variables are:

* Precipitation in 0.1mm (`PRCP`)
* Snowfall in mm (`SNOW`)
* Snow depth in mm (`SNWD`)
* Maximum temperature in 0.1°C (`TMAX`)
* Minimum temperature in 0.1°C (`TMIN`)
* Average temperature in 0.1°C (`TAVG`)

The default are all variables, i.e. `PRCP,SNOW,SNWD,TMAX,TMIN,TAVG`.

## Phase 2: Data aggregation and processing

This step is optional. If selected, the observations that have been retrieved in phase 1 are aggregated for each variable

* over time (for point, area or grid sampling geometries),
* over the whole area (area sampling geometry only), or
* both (area sampling geometry only).

Temporal aggregation only makes sense, if the temporal sampling geometry is an interval, not an instant.

If data is aggregated, the set of values for each variable the functions to apply are specified as a comma-separated list in parameter `functions`. The following functions are available:

* Minimum value (`min`)
* Maximum value (`max`)
* Average/mean value (`mean`)
* Standard deviation (`std-dev`)
* Number of values (`count`)
* Sum (`sum`)

The default value is: `min,max,mean`.

## More information and examples

### DAPA information

| Path | Description and Link
| ---- | --------------------
|`/dapa` | [Access information about the available data retrieval patterns - the DAPA landing page](03-dapa.md)
|`/dapa/variables` | [Access information about the available variables](04-variables.md)

### Data retrieval

| Path | Description and Link
| ---- | --------------------
|`/dapa/position` | [Retrieve a time series for selected variables at a position](05-position.md)
|`/dapa/area` | [Retrieve a time series for selected variables for each station in an area](06-area.md)
|`/dapa/resample-to-grid` | [Retrieve a time series for selected variables for each station in an area and resample the observations to a time series for each cell in a 2D grid](07-grid.md)

### Data retrieval and processing (apply simple data processing functions on the data retrieval results)

| Path | Description and Link
| ---- | --------------------
|`/dapa/position:aggregate-time` | [Retrieve a time series for selected variables at a position and apply functions on the values for each variable](08-position-agg-time.md)
|`/dapa/area:aggregate-time` | [Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time series](09-area-agg-time.md)
|`/dapa/area:aggregate-space` | [Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time step](10-area-agg-space.md)
|`/dapa/area:aggregate-space-time` | [Retrieve a time series for selected variables for each station in an area and apply functions on all values](11-area-agg-space-time.md)
|`/dapa/resample-to-grid:aggregate-time` | [Retrieve a time series for selected variables for each station in an area, resample the observations to a time series in a 2D grid and apply functions on the values of each time series](12-grid-agg-time.md)

---
[BACK](README.md)
