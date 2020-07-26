# DAPA endpoint of interactive instruments

## The data

[Global Historical Climatology Network Daily (GHCN-D)](https://www.ncdc.noaa.gov/ghcnd-data-access) is a dataset from NOAA that contains daily observations over global land areas. It contains station-based measurements from land-based stations worldwide, about two thirds of which are for precipitation measurement only. Other meteorological elements include, but are not limited to, daily maximum and minimum temperature, snowfall and snow depth. It is a composite of climate records from numerous sources that were merged together and subjected to a common suite of quality assurance reviews.

Currently, the 2019 data from the GHCN-D dataset is available via the API. It consists of 115,082 weather stations and 34,093,913 observations.

## The API

The API is a Web API consistent with the [emerging OGC API family of standards](https://ogcapi.org/). It provides access to the weather observations in two ways:

* The API provides access to the raw data, that is each weather station and observation, via the [OGC API Features standard](https://www.ogc.org/standards/ogcapi-features).
* In addition, the concept of a [Data Access and Processing API (DAPA)](https://portal.ogc.org/files/91644#PartDAPA) that is currently explored in OGC Testbed-16 provides additional options to retrieve the data with the goal to simplfy the use of the data for end-users, for example, for use in Jupyter Notebooks. Data retrieval in DAPA is based on the selection of the observations by the spatial sampling geometry (point, area, or grid), the temporal sampling geometry (instant or interval), and the observed properties followed by optional post-processing to aggregate observations by space and/or time. 

The landing page of the Web API is at [http://t16.ldproxy.net/ghcnd](http://t16.ldproxy.net/ghcnd).

The API is a work-in-progress and subject to change. The DAPA implementation and deployment have not yet been optimized for performance and the current server has a low end configuration, so DAPA responses take a while.

Please contact us with feedback how to improve the data retrieval requests and the encoding of the responses.

Note that all readable URIs in this repository are not percent-encoded for better readability.

## The API definition

The API is formally specified in [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/README.md). The API definition is available in [JSON](http://t16.ldproxy.net/ghcnd/api?f=json) or [YAML](http://t16.ldproxy.net/ghcnd/api?f=yaml) and can be used by clients directly. In addition, code-generators are available to generate client code for many programming environments for this API.

The API definition is also used to generate an [API documentation in HTML](http://t16.ldproxy.net/ghcnd/api?f=html), which has detailed information about all paths, operations, parameters, responses and schemas supported by the API. The documentation is an interactive client, too, and can be used to play with the API - look for the "Try it out" button.

The API definition is also available on [SwaggerHub](https://app.swaggerhub.com/apis/cportele/t16-dapa-api).

## General OGC API resources in the API

APIs implementing OGC API standards typically support JSON and HTML for most endpoints and this API is no different.

Software clients including scripts in a Jupyter Notebook will typically request responses in JSON - either by including `application/json` or `application/geo+json` in the `Accept` header of the HTTP request or by adding a query parameter `f=json` to the request.

The HTML responses enable to explore the API directly in the web browser without the need for a specific client.

APIs that implement OGC API standards and share spatial data all implement the following resources:

* The [landing page of the API](http://t16.ldproxy.net/ghcnd) has basic information about the API and links to other resources in the API.
* The [conformance declaration](http://t16.ldproxy.net/ghcnd/conformance) lists all the OGC API conformance classes that the API implements. This information is mainly of interest to clients familiar with the OGC API standards.
* The [spatial data resources](http://t16.ldproxy.net/ghcnd/collections) available in the API, also known as "collections". In this case there are two such resources, the weather stations and the observations. Both are collections of features.
* Each of the collections has its own landing page, too: [observations](http://t16.ldproxy.net/ghcnd/collections/observation) and [weather stations](http://t16.ldproxy.net/ghcnd/collections/station). These resources links to the feature data itself and to other information like schema information or the queryables (properties that can be used in queries).

## More information

* [Access the raw observation data](01-access-features.md)
* [Data retrieval patterns - DAPA overview and concepts](02-dapa-overview.md)
* DAPA information
  * [`/dapa` - Access information about the available data retrieval patterns / the DAPA landing page](03-dapa.md)
  * [`/dapa/variables` - Access information about the available variables](04-variables.md)
* Data retrieval
  * [`/dapa/position` - Retrieve a time series for selected variables at a position](05-position.md)
  * [`/dapa/area` - Retrieve a time series for selected variables for each station in an area](06-area.md)
  * [`/dapa/resample-to-grid` - Retrieve a time series for selected variables for each station in an area and resample the observations to a time series for each cell in a 2D grid](07-grid.md)
* Data retrieval and processing (apply simple data processing functions on the data retrieval results)
  * [`/dapa/position:aggregate-time` - Retrieve a time series for selected variables at a position and apply functions on the values for each variable](08-position-agg-time.md)
  * [`/dapa/area:aggregate-time` - Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time series](09-area-agg-time.md)
  * [`/dapa/area:aggregate-space` - Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time step](10-area-agg-space.md)
  * [`/dapa/area:aggregate-space-time` - Retrieve a time series for selected variables for each station in an area and apply functions on all values](11-area-agg-space-time.md)
  * [`/dapa/resample-to-grid:aggregate-time` - Retrieve a time series for selected variables for each station in an area, resample the observations to a time series in a 2D grid and apply functions on the values of each time series](12-grid-agg-time.md)
