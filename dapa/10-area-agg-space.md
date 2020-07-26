# Retrieve a time series for selected variables for each station in an area and apply functions on the values of each time step

This DAPA endpoint returns a time series for an area (parameter `bbox`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). 

All values in the area for each requested variable (parameter `variables`) are aggregated for each time step and each of the requested statistical functions (parameter `functions`) is applied to the aggregated values.

## Sample request

Percipitation and maximum/minimum temperatures on 5 days in August 2019 over Germany. The functions min(), max(), mean(), count() and std-dev() are applied to the values for each day.

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space?
coord=POLYGON((5.8 47.2,15.1 47.2,15.1 55.1,5.8 55.1,5.8 47.2))&
datetime=2019-08-07/2019-08-11&
variables=TMAX,TMIN,PRCP&
functions=min,max,mean,count,std-dev
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area:aggregate-space?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&functions=min,max,mean,count,std-dev&f=csv)

## Sample responses

### CSV

```csv
phenomenonTime,PRCP_count,PRCP_max,PRCP_mean,PRCP_min,PRCP_std-dev,TMAX_count,TMAX_max,TMAX_mean,TMAX_min,TMAX_std-dev,TMIN_count,TMIN_max,TMIN_mean,TMIN_min,TMIN_std-dev
2019-08-11,709,281.0,26.931225,0.0,45.49806,485,306.0,258.65854,115.0,27.334553,486,187.0,137.17947,58.0,20.78836
2019-08-10,709,229.0,12.449949,0.0,26.586481,485,305.0,245.46971,99.0,24.421343,486,206.0,157.32607,61.0,20.63871
2019-08-09,709,431.0,55.968887,0.0,56.121117,485,351.0,277.59433,134.0,34.76338,486,188.0,128.55798,52.0,21.31758
2019-08-08,709,439.0,5.9656353,0.0,25.032032,485,294.5,248.36009,67.0,23.795979,486,178.0,131.79442,20.0,16.903353
2019-08-07,709,490.0,63.96998,0.0,84.83652,485,285.0,225.75258,73.0,26.090208,486,177.53384399414062,144.37961,27.0,16.778051
```

### GeoJSON

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 5.8, 47.2 ], [ 15.1, 47.2 ], [ 15.1, 55.1 ], [ 5.8, 55.1 ], [ 5.8, 47.2 ] ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-11",
      "TMAX_mean" : 258.65854,
      "TMIN_std-dev" : 20.78836,
      "TMIN_max" : 187.0,
      "TMAX_max" : 306.0,
      "PRCP_min" : 0.0,
      "TMIN_count" : 486,
      "TMAX_count" : 485,
      "PRCP_mean" : 26.931225,
      "TMAX_min" : 115.0,
      "PRCP_max" : 281.0,
      "PRCP_count" : 709,
      "TMIN_min" : 58.0,
      "PRCP_std-dev" : 45.49806,
      "TMAX_std-dev" : 27.334553,
      "TMIN_mean" : 137.17947
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 5.8, 47.2 ], [ 15.1, 47.2 ], [ 15.1, 55.1 ], [ 5.8, 55.1 ], [ 5.8, 47.2 ] ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-10",
      "TMAX_mean" : 245.46971,
      "TMIN_std-dev" : 20.63871,
      "TMIN_max" : 206.0,
      "TMIN_count" : 486,
      "TMAX_count" : 485,
      "PRCP_mean" : 12.449949,
      "TMAX_max" : 305.0,
      "PRCP_min" : 0.0,
      "TMAX_min" : 99.0,
      "PRCP_max" : 229.0,
      "TMIN_min" : 61.0,
      "PRCP_std-dev" : 26.586481,
      "TMAX_std-dev" : 24.421343,
      "TMIN_mean" : 157.32607
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 5.8, 47.2 ], [ 15.1, 47.2 ], [ 15.1, 55.1 ], [ 5.8, 55.1 ], [ 5.8, 47.2 ] ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-09",
      "TMAX_mean" : 277.59433,
      "TMIN_std-dev" : 21.31758,
      "TMIN_max" : 188.0,
      "TMIN_count" : 486,
      "TMAX_count" : 485,
      "PRCP_mean" : 55.968887,
      "TMAX_max" : 351.0,
      "PRCP_min" : 0.0,
      "PRCP_count" : 709,
      "TMIN_min" : 52.0,
      "PRCP_std-dev" : 56.121117,
      "TMAX_min" : 134.0,
      "PRCP_max" : 431.0,
      "TMAX_std-dev" : 34.76338,
      "TMIN_mean" : 128.55798
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 5.8, 47.2 ], [ 15.1, 47.2 ], [ 15.1, 55.1 ], [ 5.8, 55.1 ], [ 5.8, 47.2 ] ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-08",
      "TMAX_mean" : 248.36009,
      "TMIN_std-dev" : 16.903353,
      "TMIN_max" : 178.0,
      "TMIN_count" : 486,
      "TMAX_count" : 485,
      "PRCP_mean" : 5.9656353,
      "TMAX_max" : 294.5,
      "PRCP_min" : 0.0,
      "TMAX_std-dev" : 23.795979,
      "TMIN_mean" : 131.79442,
      "TMAX_min" : 67.0,
      "PRCP_max" : 439.0,
      "PRCP_count" : 709,
      "TMIN_min" : 20.0,
      "PRCP_std-dev" : 25.032032
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Polygon",
      "coordinates" : [ [ [ 5.8, 47.2 ], [ 15.1, 47.2 ], [ 15.1, 55.1 ], [ 5.8, 55.1 ], [ 5.8, 47.2 ] ] ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-07",
      "TMAX_mean" : 225.75258,
      "TMIN_std-dev" : 16.778051,
      "TMIN_max" : 177.53384,
      "TMIN_count" : 486,
      "TMAX_count" : 485,
      "PRCP_mean" : 63.96998,
      "TMAX_max" : 285.0,
      "PRCP_min" : 0.0,
      "PRCP_count" : 709,
      "TMIN_min" : 27.0,
      "PRCP_std-dev" : 84.83652,
      "TMAX_min" : 73.0,
      "PRCP_max" : 490.0,
      "TMAX_std-dev" : 26.090208,
      "TMIN_mean" : 144.37961
    }
  } ]
}
```

---
[BACK](README.md)
