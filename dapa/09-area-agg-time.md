# Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time series

This DAPA endpoint returns observation values for an area (parameter `bbox`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). 

All values for each requested variable (parameter `variables`) are aggregated for each weather station and each of the requested statistical functions (parameter `functions`) is applied to the aggregated values.

## Sample request

Percipitation and maximum/minimum temperatures on 5 days in August 2019 over Germany. The functions min(), max(), mean(), count() and std-dev() are applied to the time series of each weather station in the area.

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-time?
coord=POLYGON((5.8 47.2,15.1 47.2,15.1 55.1,5.8 55.1,5.8 47.2))&
datetime=2019-08-07/2019-08-11&
variables=TMAX,TMIN,PRCP&
function=min,max,mean,count,std-dev
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-time?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-time?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=csv)

## Sample responses

### CSV

The response is shortened to two stations.

```csv
longitude,latitude,locationCode,locationName,PRCP_count,PRCP_max,PRCP_mean,PRCP_min,PRCP_std-dev,TMAX_count,TMAX_max,TMAX_mean,TMAX_min,TMAX_std-dev,TMIN_count,TMIN_max,TMIN_mean,TMIN_min,TMIN_std-dev
11.785599708557129,50.729400634765625,GME00126070,SCHMIERITZ-WELTWITZ,5,59.0,11.8,0.0,26.385603,5,297.0,256.2,204.0,36.16905,5,170.0,144.8,127.0,17.626684
...
6.258900165557861,52.434200286865234,NLE00152479,HEINO,5,53.0,18.8,0.0,26.090227,5,235.0,229.2,221.0,5.6302752,5,170.0,135.0,108.0,26.1247
```

### GeoJSON

The response is shortened to two stations.

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 11.785599708557129, 50.729400634765625 ]
    },
    "properties" : {
      "locationCode" : "GME00126070",
      "locationName" : "SCHMIERITZ-WELTWITZ",
      "phenomenonTime" : "2019-08-07/2019-08-11",
      "TMAX_mean" : 256.2,
      "TMIN_std-dev" : 17.626684,
      "TMIN_max" : 170.0,
      "TMIN_count" : 5,
      "TMAX_count" : 5,
      "TMAX_max" : 297.0,
      "PRCP_mean" : 11.8,
      "PRCP_min" : 0.0,
      "PRCP_count" : 5,
      "TMIN_min" : 127.0,
      "PRCP_std-dev" : 26.385603,
      "TMAX_min" : 204.0,
      "PRCP_max" : 59.0,
      "TMAX_std-dev" : 36.16905,
      "TMIN_mean" : 144.8
    }
  }, ... {
   "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 6.258900165557861, 52.434200286865234 ]
    },
    "properties" : {
      "locationCode" : "NLE00152479",
      "locationName" : "HEINO",
      "phenomenonTime" : "2019-08-07/2019-08-11",
      "TMAX_mean" : 229.2,
      "TMIN_std-dev" : 26.1247,
      "TMIN_max" : 170.0,
      "TMIN_count" : 5,
      "TMAX_count" : 5,
      "PRCP_mean" : 18.8,
      "TMAX_max" : 235.0,
      "PRCP_min" : 0.0,
      "TMAX_min" : 221.0,
      "PRCP_max" : 53.0,
      "PRCP_count" : 5,
      "TMIN_min" : 108.0,
      "PRCP_std-dev" : 26.090227,
      "TMAX_std-dev" : 5.6302752,
      "TMIN_mean" : 135.0
    }
  } ]
}
```

---
[BACK](README.md)
