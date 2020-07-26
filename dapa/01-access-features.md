# Access to the raw data

This page lists some examples how to access the raw observations directly as GeoJSON.

The API endpoint for these requests is:

```text
http://t16.ldproxy.net/ghcnd/collections/observation/items
```

[Link](http://t16.ldproxy.net/ghcnd/collections/observation/items?f=json)

This request returns 10 observation features and a link to the next "page" of features (the link with `rel` set to `next` ). This enables clients to page through the observations. The resonse is shown below, reduced to two observations.

Each observation has the point geometry of the weather station that recorded the observation and the following properties based on the Observation & Measurement standard:

* phenomenonTime: The day of the observation.
* observedProperty: The physical property that was observed, more on the available properties is described below.
* result: The observed numerical value.
* unitOfMeasurement: The unit of the value in result.
* locationCode: The code of the weather station that recorded the observation.
* locationName: The name of the weather station that recorded the observation.
* locationLink: The URI of the weather station in the API.

```json
{
   "type": "FeatureCollection",
   "@context": "http://t16.ldproxy.net/ghcnd/collections/observation/context",
   "@type": "geojson:FeatureCollection",
   "links": [
      {
         "href": "http://t16.ldproxy.net/ghcnd/collections/observation/items?f=json",
         "rel": "self",
         "type": "application/geo+json",
         "title": "This document"
      },
      {
         "href": "http://t16.ldproxy.net/ghcnd/collections/observation/items?f=html",
         "rel": "alternate",
         "type": "text/html",
         "title": "This document as HTML"
      },
      {
         "href": "http://t16.ldproxy.net/ghcnd/collections/observation/items?f=json&offset=10",
         "rel": "next",
         "type": "application/geo+json",
         "title": "Next page"
      }
   ],
   "numberReturned": 10,
   "timeStamp": "2020-07-25T11:43:19Z",
   "features": [
      {
         "type": "Feature",
         "@type": [
            "geojson:Feature",
            "sosa:Observation"
         ],
         "@id": "http://t16.ldproxy.net/ghcnd/collections/observation/items/1",
         "id": "1",
         "geometry": {
            "type": "Point",
            "coordinates": [
               -80.3111,
               27.3237
            ]
         },
         "properties": {
            "phenomenonTime": "2019-01-01",
            "observedProperty": "PRCP",
            "unitOfMeasurement": "0.1 mm",
            "result": 0,
            "locationCode": "US1FLSL0019",
            "locationLink": "http://t16.ldproxy.net/ghcnd/collections/station/items/US1FLSL0019",
            "locationName": "PORT ST. LUCIE 4.0 NE"
         }
      }, ...
      {
         "type": "Feature",
         "@type": [
            "geojson:Feature",
            "sosa:Observation"
         ],
         "@id": "http://t16.ldproxy.net/ghcnd/collections/observation/items/10",
         "id": "10",
         "geometry": {
            "type": "Point",
            "coordinates": [
               -97.6697,
               39.5592
            ]
         },
         "properties": {
            "phenomenonTime": "2019-01-01",
            "observedProperty": "SNOW",
            "unitOfMeasurement": "mm",
            "result": 0,
            "locationCode": "USC00141761",
            "locationLink": "http://t16.ldproxy.net/ghcnd/collections/station/items/USC00141761",
            "locationName": "CONCORDIA 1 W"
         }
      }
   ]
}
```

The response also includes a JSON-LD 1.1 context that relates the JSON values to definitions in the [W3C Semantic Sensor Network Ontology](https://www.w3.org/TR/vocab-ssn/) and the [GeoJSON vocabulary](https://geojson.org/geojson-ld/). JSON-LD-aware clients can process the observation data and convert it to RDF.

Query parameters can be used to adjust the request and select specific observations. The following request will select the first 1000 percipitation observations in the border area of Germany, France and Luxembourg during August 2019:

```text
http://t16.ldproxy.net/ghcnd/collections/observation/items?
bbox=6,48.5,8,50.5&
datetime=2019-08-01/2019-08-31&
observedProperty=PRCP&
limit=1000
```

[Link](http://t16.ldproxy.net/ghcnd/collections/observation/items?bbox=6,48.5,8,50.5&datetime=2019-08-01/2019-08-31&observedProperty=PRCP&limit=1000&f=json)

The next request selects the maximum temperature at Berlin-Tegel airport on July 29, 2019, with the geometry in the response in the Web Mercator projection.

```text
http://t16.ldproxy.net/ghcnd/collections/observation/items?
locationName=BERLIN-TEGEL&
datetime=2019-07-29&
observedProperty=TMAX&
crs=http://www.opengis.net/def/crs/EPSG/0/3857
```

[Link](http://t16.ldproxy.net/ghcnd/collections/observation/items?locationName=BERLIN-TEGEL&datetime=2019-07-29&observedProperty=TMAX&crs=http%3A%2F%2Fwww.opengis.net%2Fdef%2Fcrs%2FEPSG%2F0%2F3857&f=json)

The complete details of the request options are specified in the [API documentation](http://t16.ldproxy.net/ghcnd/api/?f=html#/Access%20data/get_collections_observation_items).

---
[BACK](README.md)
