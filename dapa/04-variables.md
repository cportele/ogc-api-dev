# Access information about the available variables

Variables are the properties that have been observed and are included in this collection of observations.

## Request

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/variables
```

[Link](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/variables)

## Response in JSON

The response lists the available variables for which observations are available. It is also available as HTML.

```json
{
  "links" : [ {
    "rel" : "self",
    "type" : "application/json",
    "title" : "This document",
    "href" : "http://t16.ldproxy.net/ghcnd/collections/observation/dapa/variables?f=json"
  }, {
    "rel" : "alternate",
    "type" : "text/html",
    "title" : "This document as HTML",
    "href" : "http://t16.ldproxy.net/ghcnd/collections/observation/dapa/variables?f=html"
  } ],
  "variables" : [ {
    "id" : "PRCP",
    "title" : "Precipitation",
    "uom" : "0.1 mm"
  }, {
    "id" : "SNOW",
    "title" : "Snowfall",
    "uom" : "mm"
  }, {
    "id" : "SNWD",
    "title" : "Snow depth",
    "uom" : "mm"
  }, {
    "id" : "TMAX",
    "title" : "Maximum temperature",
    "uom" : "0.1 °C"
  }, {
    "id" : "TMIN",
    "title" : "Minimum temperature",
    "uom" : "0.1 °C"
  }, {
    "id" : "TAVG",
    "title" : "Average temperature",
    "uom" : "0.1 °C"
  } ]
}
```

---
[BACK](README.md)
