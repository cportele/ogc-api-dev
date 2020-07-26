# Retrieve a time series for selected variables at a position and apply functions on the values for each variable

This DAPA endpoint returns observation values at the selected location (parameter `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`).

All values in the time interval for each requested variable (parameter `variables`) are aggregated and each of the requested statistical functions (parameter `functions`) is applied to the aggregated values.

## Sample request

Percipitation and maximum/minimum temperatures on 5 days in August 2019, in Lieser, Germany. The functions min(), max(), mean(), count() and std-dev() are applied to the time series.

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/position:aggregate-time?
coord=POINT(7.0218 49.9174)&
datetime=2019-08-07/2019-08-11&
variables=TMAX,TMIN,PRCP&
functions=min,max,mean,count,std-dev
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/position:aggregate-time?coord=POINT(7.0218%2049.9174)&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/position:aggregate-time?coord=POINT(7.0218%2049.9174)&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=csv)

## Sample responses

### CSV

```csv
PRCP_count,PRCP_max,PRCP_mean,PRCP_min,PRCP_std-dev,TMAX_count,TMAX_max,TMAX_mean,TMAX_min,TMAX_std-dev,TMIN_count,TMIN_max,TMIN_mean,TMIN_min,TMIN_std-dev
5,175.7282,49.449417,0.1784924,74.594795,5,261.97256,230.02454,206.25876,23.499502,5,148.28212,132.24287,107.17521,17.294535
```

### GeoJSON

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.0218, 49.9174 ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-07/2019-08-11",
      "TMAX_mean" : 230.02454,
      "TMIN_std-dev" : 17.294535,
      "TMIN_max" : 148.28212,
      "TMIN_count" : 5,
      "TMAX_count" : 5,
      "PRCP_mean" : 49.449417,
      "TMAX_max" : 261.97256,
      "PRCP_min" : 0.1784924,
      "TMAX_min" : 206.25876,
      "PRCP_count" : 5,
      "TMAX_std-dev" : 23.499502,
      "TMIN_min" : 107.17521,
      "PRCP_std-dev" : 74.594795,
      "TMIN_mean" : 132.24287
    }
  } ]
}
```

---
[BACK](README.md)
