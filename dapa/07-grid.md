# Retrieve a time series for selected variables for each station in an area and resample the observations to a time series for each cell in a 2D grid

This DAPA endpoint retrieves a time series for each station in an area (parameter `box`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). Each time series contains daily observation values for each selected variable (parameter `variables`) for which a value has been observed at the station during the time interval.

The data is then resampled to a time series for each cell in a 2D spatial grid.

## Sample request

In the example we use a small grid (width = 20 cells, height is computed) and only request data at a time instant

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid?
bbox=5.8,47.2,15.1,55.1&
datetime=2019-08-09&
variables=TMAX,TMIN,PRCP&
width=20
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid?bbox=5.8,47.2,15.1,55.1&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&width=20&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid?bbox=5.8,47.2,15.1,55.1&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&width=20&f=csv)

[Request GeoTIFF](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid?bbox=5.8,47.2,15.1,55.1&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&width=20&f=tiff)

## Sample responses

### CSV

The response has been shortened to the first column:

```csv
longitude,latitude,phenomenonTime,TMAX,TMIN,PRCP
5.8,54.17058823529412,2019-08-09,208.3371,165.58093,
5.8,53.70588235294118,2019-08-09,212.30658,154.50684,69.43805
5.8,53.241176470588236,2019-08-09,216.48091,108.501335,44.1395
5.8,52.7764705882353,2019-08-09,221.22427,108.43177,38.235477
5.8,52.311764705882354,2019-08-09,229.13065,137.56642,114.42797
5.8,51.847058823529416,2019-08-09,246.9007,155.55235,73.69644
5.8,51.38235294117647,2019-08-09,253.04602,164.75665,24.300041
5.8,50.91764705882353,2019-08-09,255.91014,162.96167,106.63208
5.8,50.45294117647059,2019-08-09,257.63416,165.82362,81.62919
5.8,49.98823529411765,2019-08-09,265.50992,166.86095,63.125282
5.8,49.523529411764706,2019-08-09,274.08966,162.93968,45.84553
5.8,49.05882352941177,2019-08-09,280.13544,160.14008,19.011019
5.8,48.59411764705882,2019-08-09,284.58804,,12.559709
5.8,48.129411764705885,2019-08-09,286.05768,,34.865925
5.8,47.66470588235295,2019-08-09,281.6034,,62.27944
...
```

#### GeoTIFF

[A sample GeoTIFF file with percipitation over Germany, 2019-08-09](07-PRCP-Germany-2019-08-09.tiff)

#### GeoJSON

The response is shortened to two cells.

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 5.8, 50.91765 ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-09",
      "PRCP" : 26.634087
    }
  }, ... {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 14.610527, 52.77647 ]
    },
    "properties" : {
      "phenomenonTime" : "2019-08-09",
      "TMAX" : 263.56512,
      "PRCP" : 2.2810037
    }
  } ]
}
```

---
[BACK](README.md)
