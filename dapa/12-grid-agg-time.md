# Retrieve a time series for selected variables for each station in an area, resample the observations to a time series in a 2D grid and on the values of each time series

This DAPA endpoint retrieves a time series for each station in an area (parameter `box`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`). Each time series contains daily observation values for each selected variable (parameter `variables`) for which a value has been observed at the station during the time interval.

The data is then resampled to a time series for each cell in a 2D spatial grid and all values in each time series are aggregated and each of the requested statistical functions (parameter `functions`) is applied to the values.

## Sample request

Generate a grid of the maxmimum temperatures in Germany during 2019. The grid has 20 columns.

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid:aggregate-time?
bbox=5.8,47.2,15.1,55.1&
datetime=2019-01-01/2019-12-31&
variables=TMAX&
width=20&
functions=max
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid:aggregate-time?bbox=5.8,47.2,15.1,55.1&datetime=2019-01-01/2019-12-31&variables=TMAX&width=20&functions=max&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid:aggregate-time?bbox=5.8,47.2,15.1,55.1&datetime=2019-01-01/2019-12-31&variables=TMAX&width=20&functions=max&f=csv)

[Request GeoTIFF](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/resample-to-grid:aggregate-time?bbox=5.8,47.2,15.1,55.1&datetime=2019-01-01/2019-12-31&variables=TMAX&width=20&functions=max&f=tiff)

## Sample responses

## CSV

The response has been shortened to the first column.

```csv
longitude,latitude,TMAX_max
5.8,54.17058823529412,302.4419
5.8,53.70588235294118,346.7035
5.8,53.241176470588236,358.9652
5.8,52.7764705882353,386.4441
5.8,52.311764705882354,396.17108
5.8,51.847058823529416,403.03824
5.8,51.38235294117647,395.76236
5.8,50.91764705882353,386.07953
5.8,50.45294117647059,390.37183
5.8,49.98823529411765,392.23697
5.8,49.523529411764706,393.08337
5.8,49.05882352941177,394.32608
5.8,48.59411764705882,396.6705
5.8,48.129411764705885,391.1083
5.8,47.66470588235295,384.11874
...
```

## GeoTIFF

[GeoTIFF file with maxmimum temperatures over Germany in 2019](12-TMAX-Germany-2019.tiff)

## GeoJSON

The response is shortened to two cells.

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 5.8, 54.17058823529412 ]
    },
    "properties" : {
      "phenomenonTime" : "2019-01-01/2019-12-31",
      "TMAX_max" : 302.4419
    }
  }, ... {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 14.635000000000002, 47.66470588235295 ]
    },
    "properties" : {
      "phenomenonTime" : "2019-01-01/2019-12-31",
      "TMAX_max" : 346.3743
    }
  } ]
}```


---
[BACK](README.md)
