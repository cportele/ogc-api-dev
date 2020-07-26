# Retrieve a time series for selected variables for each station in an area and apply functions on all values

This DAPA endpoint returns observation values for an area (parameter `bbox`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). 

All values for each requested variable (parameter `variables`) are aggregated and each of the requested statistical functions (parameter `functions`) is applied to the aggregated values.

## Sample request

Retrieve all observations in the state North-Rhine Westphalia in Germany for August 2019 and apply the functions min(), max(), mean(), count() and std-dev().

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space-time?
coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&
datetime=2019-08-01/2019-08-31&
variables=TMAX,TMIN,PRCP&
function=min,max,mean,count,std-dev
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space-time?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-01/2019-08-31&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space-time?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-01/2019-08-31&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=json)

## Sample responses

### CSV

```csv
PRCP_count,PRCP_max,PRCP_mean,PRCP_min,PRCP_std-dev,TMAX_count,TMAX_max,TMAX_mean,TMAX_min,TMAX_std-dev,TMIN_count,TMIN_max,TMIN_mean,TMIN_min,TMIN_std-dev
1333,443.0,18.745686,0.0,42.16499,1178,350.0,251.22072,139.0,39.133766,1178,218.0,128.9236,46.0,29.123257
```

#### Sample response in GeoJSON

The geometry has been shortened.

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 6.094259257869, 51.616130588555 ], [ 6.093923825039, 51.622147469348 ], ... ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-01/2019-08-31",
      "TMIN_count" : 1178,
      "TMAX_count" : 1178,
      "PRCP_mean" : 18.745686,
      "TMAX_max" : 350.0,
      "PRCP_min" : 0.0,
      "TMAX_min" : 139.0,
      "PRCP_max" : 443.0,
      "TMAX_std-dev" : 39.133766,
      "TMIN_mean" : 128.9236,
      "PRCP_count" : 1333,
      "TMIN_min" : 46.0,
      "PRCP_std-dev" : 42.16499,
      "TMAX_mean" : 251.22072,
      "TMIN_std-dev" : 29.123257,
      "TMIN_max" : 218.0
    }
  } ]
}
```

---
[BACK](README.md)
