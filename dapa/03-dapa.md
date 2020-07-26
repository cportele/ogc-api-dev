# The DAPA landing page: Access information about the available data retrieval patterns

## Request

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa
```

[Link](http://t16.ldproxy.net/ghcnd/collections/observation/dapa)

## Response in JSON

The response lists the available endpoints to retrieve and process the observations in addition to the standard feature queries. The endpoints are described in the API definition and the links point to the specification of the operation in the OpenAPI definition with the available input parameters and the response schema. The URIs in the "ogc-dapa-endpoint-definition" links are JSON Pointers to the definition of the operation in the OpenAPI definition.

This page is also available as HTML.

```json
{
  "title" : "Data retrieval patterns",
  "description" : "The following endpoints are available to retrieve and process the observations in addition to the standard feature queries. The endpoints are described in the API definition and the links point to the specification of the operation in the OpenAPI definition with the available input parameters and the response schema.",
  "links" : [ {
    "rel" : "self",
    "type" : "application/json",
    "title" : "This document",
    "href" : "http://localhost:7080/rest/services/ghcnd/collections/observation/dapa?f=json"
  }, {
    "rel" : "alternate",
    "type" : "text/html",
    "title" : "This document as HTML",
    "href" : "http://localhost:7080/rest/services/ghcnd/collections/observation/dapa?f=html"
  }, {
    "rel" : "ogc-variables",
    "title" : "Observable properties included in this observation collection",
    "href" : "http://localhost:7080/rest/services/ghcnd/collections/observation/dapa/variables"
  } ],
  "endpoints" : [ {
    "title" : "retrieve a time series for selected variables for each station in an area",
    "description" : "This DAPA endpoint returns observation values at the selected location (parameter `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`).\n\nAll values in the time interval for each requested variable (parameter `variables`) are aggregated and each of the requested statistical functions (parameter `functions`) is applied to the aggregated values.",
    "links" : [ {
      "rel" : "ogc-dapa-endpoint",
      "title" : "Execute the data retrieval pattern with the default parameters",
      "href" : "http://localhost:7080/rest/services/ghcnd/collections/observation/dapa/area"
    }, {
      "rel" : "ogc-dapa-endpoint-definition",
      "title" : "Detailed description in the API definition (OpenAPI 3.0)",
      "href" : "http://localhost:7080/rest/services/ghcnd/api?f=json#/paths/~1collections~1observation~1dapa~1area"
    }, {
      "rel" : "ogc-dapa-endpoint-documentation",
      "title" : "Detailed description in the API documentation",
      "href" : "http://localhost:7080/rest/services/ghcnd/api?f=html#/DAPA/get_collections_observation_dapa_area"
    } ],
    "id" : "area",
    "inputCollectionId" : "observation",
    "mediaTypes" : [ "application/geo+json", "text/csv" ],
    "externalDocs" : {
      "description" : "Example requests and responses",
      "url" : "https://github.com/cportele/ogc-api-dev/blob/master/dapa/06-area.md"
    }
  }, ... {
    "title" : "retrieve a time series for selected variables for each station in an area, resample the observations to a time series in a 2D grid and apply functions on the values of each time series",
    "description" : "This DAPA endpoint retrieves a time series for each station in an area (parameter `box`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). Each time series contains daily observation values for each selected variable (parameter `variables`) for which a value has been observed at the station during the time interval.\n\nThe data is then resampled to a time series for each cell in a 2D spatial grid and all values in each time series are aggregated and each of the requested statistical functions (parameter `functions`) is applied to the values.",
    "links" : [ {
      "rel" : "ogc-dapa-endpoint",
      "title" : "Execute the data retrieval pattern with the default parameters",
      "href" : "http://localhost:7080/rest/services/ghcnd/collections/observation/dapa/resample-to-grid:aggregate-time"
    }, {
      "rel" : "ogc-dapa-endpoint-definition",
      "title" : "Detailed description in the API definition (OpenAPI 3.0)",
      "href" : "http://localhost:7080/rest/services/ghcnd/api?f=json#/paths/~1collections~1observation~1dapa~1resample-to-grid:aggregate-time"
    }, {
      "rel" : "ogc-dapa-endpoint-documentation",
      "title" : "Detailed description in the API documentation",
      "href" : "http://localhost:7080/rest/services/ghcnd/api?f=html#/DAPA/get_collections_observation_dapa_resample_to_grid_aggregate_time"
    } ],
    "id" : "resample-to-grid:aggregate-time",
    "inputCollectionId" : "observation",
    "mediaTypes" : [ "application/geo+json", "image/tiff", "text/csv" ],
    "externalDocs" : {
      "description" : "Example requests and responses",
      "url" : "https://github.com/cportele/ogc-api-dev/blob/master/dapa/07-grid.md"
    }
  } ]
}
```

---
[BACK](README.md)
