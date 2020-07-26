# Retrieve a time series for selected variables for each station in an area

This DAPA endpoint returns a time series for each station in an area (parameter `box`, `coord` or `coordRef`) in the selected time interval or at the selected time instant (parameter `datetime`).

Each time series contains daily observation values for each selected variable (parameter `variables`) for which a value has been observed at the station during the time interval.

## Sample requests

### Using a bounding box, requesting data for an instant

The area is a rough bounding box of Germany:

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?
bbox=5.8,47.2,15.1,55.1&
datetime=2019-08-09&
variables=TMAX,TMIN,PRCP
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?bbox=5.8,47.2,15.1,55.1&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?bbox=5.8,47.2,15.1,55.1&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=csv)

### Using a polygon, requesting data for an instant

The same bounding box as above, but as a polygon:

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?
coord=POLYGON((5.8 47.2,15.1 47.2,15.1 55.1,5.8 55.1,5.8 47.2))&
datetime=2019-08-09&
variables=TMAX,TMIN,PRCP
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coord=POLYGON((5.8%2047.2%2C15.1%2047.2%2C15.1%2055.1%2C5.8%2055.1%2C5.8%2047.2))&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=csv)

### Using a reference for the area, requesting data for an instant

The area is the polygon of the German state North-Rhine Westphalia retrieved from another API using the reference [https://www.ldproxy.nrw.de/dvg/collections/nw_dvg2_bld/items/nw_dvg2_bld.05000000](https://www.ldproxy.nrw.de/dvg/collections/nw_dvg2_bld/items/nw_dvg2_bld.05000000):

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?
coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&
datetime=2019-08-09&
variables=TMAX,TMIN,PRCP
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-09&variables=TMAX,TMIN,PRCP&f=csv)

#### Using a reference for the area, requesting data for an interval

```text
http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?
coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&
datetime=2019-08-07/2019-08-11&
variables=TMAX,TMIN,PRCP
```

[Request GeoJSON](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&f=json)

[Request CSV](http://t16.ldproxy.net/ghcnd/collections/observation/dapa/area?coordRef=https%3A%2F%2Fwww.ldproxy.nrw.de%2Fdvg%2Fcollections%2Fnw_dvg2_bld%2Fitems%2Fnw_dvg2_bld.05000000&datetime=2019-08-07/2019-08-11&variables=TMAX,TMIN,PRCP&f=csv)

## Sample responses

### CSV

A time instant (observations in North-Rhine Westphalia):

```csv
longitude,latitude,locationCode,locationName,phenomenonTime,TMAX,TMIN,PRCP
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-09,267.0,136.0,15.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-09,,,64.0
8.468099594116211,51.19029998779297,GME00111457,ALTASTENBERG,2019-08-09,208.0,146.0,88.0
6.968299865722656,51.405601501464844,GME00121978,ESSEN-BREDENEY,2019-08-09,254.0,165.0,3.0
6.88670015335083,51.87419891357422,GME00131182,BORKEN IN WESTFALEN,2019-08-09,242.0,125.0,17.0
6.246699810028076,51.495601654052734,GME00122746,GELDERN-WALBECK,2019-08-09,258.0,160.0,26.0
6.424200057983398,50.67559814453125,GME00126694,NIDEGGEN-SCHMIDT,2019-08-09,259.0,144.0,101.0
7.341700077056885,51.33420181274414,GME00122146,GEVELSBERG-OBERBROKING,2019-08-09,246.0,142.0,39.0
6.445000171661377,51.29079818725586,GME00129346,TONISVORST,2019-08-09,264.0,160.0,25.0
8.395299911499023,51.6343994140625,GME00125422,LIPPSTADT-BOKENFORDE,2019-08-09,278.0,132.0,11.0
6.7916998863220215,50.71310043334961,GME00122002,WEILERSWIST-LOMMERSUM,2019-08-09,272.0,146.0,76.0
8.839400291442871,51.78670120239258,GME00121078,BAD LIPPSPRINGE,2019-08-09,266.0,126.0,5.0
9.112799644470215,51.50529861450195,GME00129886,WARBURG,2019-08-09,263.0,128.0,34.0
8.573100090026855,52.44810104370117,GME00127558,RAHDEN-VARL,2019-08-09,276.0,105.0,12.0
6.659200191497803,50.82889938354492,GME00126766,NORVENICH (FLUGPLATZ),2019-08-09,,,96.0
7.094200134277344,51.14080047607422,GME00128902,SOLINGEN-HOHENSCHEID,2019-08-09,,,109.0
7.520299911499023,51.76810073852539,GME00131518,LUDINGHAUSEN-BROCHTRUP,2019-08-09,276.0,119.0,0.0
7.158299922943115,50.86579895019531,GME00121042,KOLN-BONN,2019-08-09,266.0,159.0,129.0
6.701900005340576,51.5099983215332,GME00122098,DUISBURG-BAERL,2019-08-09,274.0,173.0,12.0
6.095600128173828,51.76250076293945,GME00124606,KLEVE,2019-08-09,237.0,152.0,96.0
8.457799911499023,52.07279968261719,GME00131830,BIELEFELD-DEPPENDORF,2019-08-09,269.0,93.0,2.0
5.983099937438965,50.98310089111328,NLE00109280,SCHINVELD,2019-08-09,,,31.0
7.978899955749512,51.46440124511719,GME00131974,ARNSBERG-NEHEIM,2019-08-09,277.0,117.0,14.0
6.941699981689453,52.082801818847656,GMM00010309,AHAUS,2019-08-09,236.0,106.0,81.0
7.105800151824951,51.225799560546875,GME00130582,WUPPERTAL-BUCHENHOFEN,2019-08-09,242.0,137.0,40.0
8.65060043334961,51.41559982299805,GME00131374,BRILON-THULEN,2019-08-09,251.0,138.0,26.0
8.753100395202637,52.10559844970703,GME00128182,BAD SALZUFLEN,2019-08-09,264.0,120.0,4.0
6.025000095367432,50.799198150634766,GME00120958,AACHEN-ORSBACH,2019-08-09,265.0,164.0,77.0
8.156900405883789,51.25529861450195,GME00121966,ESLOHE,2019-08-09,245.0,118.0,49.0
8.035799980163574,51.1343994140625,GME00125230,LENNESTADT-THETEN,2019-08-09,252.0,124.0,58.0
7.3719000816345215,50.84560012817383,GME00126562,NEUNKIRCHEN-SEELSCHEID-KRAWINK,2019-08-09,250.0,156.0,125.0
6.104400157928467,51.04249954223633,GME00123574,HEINSBERG-SCHLEIDEN,2019-08-09,248.0,163.0,34.0
7.405600070953369,51.59809875488281,GME00122134,WALTROP-ABDINGHOF,2019-08-09,270.0,134.0,4.0
8.355299949645996,51.88890075683594,GME00123178,GUTERSLOH,2019-08-09,,,9.0
6.526700019836426,50.50279998779297,GME00124366,KALL-SISTIG,2019-08-09,239.0,139.0,135.0
8.368900299072266,50.98500061035156,GME00127258,BAD-STUNZEL BERLEBURG,2019-08-09,225.0,127.0,148.0
6.978300094604492,50.9906005859375,GME00125302,KOLN-STAMMHEIM,2019-08-09,262.0,168.0,67.0
7.643099784851074,51.246700286865234,GME00125602,LUDENSCHEID,2019-08-09,242.0,134.0,24.0
6.769999980926514,51.29690170288086,GME00102268,DUSSELDORF,2019-08-09,264.0,161.0,7.0
7.62939977645874,51.09080123901367,GME00122182,MEINERZHAGEN-REDLENDORF,2019-08-09,232.0,119.0,93.0
9.271900177001953,51.867801666259766,GME00131242,LUGDE-PAENBRUCH,2019-08-09,262.0,118.0,9.0
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-09,275.0,157.0,127.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-09,265.0,121.0,20.0
```

A time series for each station (the response has been shortened to four stations):

```csv
longitude,latitude,locationCode,locationName,phenomenonTime,TMAX,TMIN,PRCP
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-11,244.0,138.0,0.0
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-10,257.0,181.0,0.0
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-09,267.0,136.0,15.0
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-08,257.0,143.0,0.0
7.888899803161621,51.57780075073242,GMM00010424,WERL,2019-08-07,252.0,147.0,0.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-11,,,0.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-10,,,10.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-09,,,64.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-08,,,0.0
6.535799980163574,51.8307991027832,GME00130294,BOCHOLT,2019-08-07,,,0.0
...
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-11,231.0,143.0,0.0
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-10,256.0,180.0,0.0
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-09,275.0,157.0,127.0
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-08,232.0,146.0,0.0
7.193900108337402,50.73640060424805,GME00130990,BONN-ROLEBER,2019-08-07,243.0,154.0,0.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-11,240.0,166.0,0.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-10,259.0,184.0,0.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-09,265.0,121.0,20.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-08,256.0,125.0,0.0
7.699999809265137,52.13529968261719,GME00111430,MUENSTER/OSNABRUECK (AIRPORT),2019-08-07,257.0,165.0,0.0
```

### GeoJSON

The response of the first request (time instant), shortened to two of many features:

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 11.7856, 50.7294 ]
    },
    "properties" : {
      "locationCode" : "GME00126070",
      "locationName" : "SCHMIERITZ-WELTWITZ",
      "phenomenonTime" : "2019-08-09",
      "TMAX" : 297.0,
      "TMIN" : 127.0,
      "PRCP" : 0.0
    }
  }, ... {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 6.2589, 52.4342 ]
    },
    "properties" : {
      "locationCode" : "NLE00152479",
      "locationName" : "HEINO",
      "phenomenonTime" : "2019-08-09",
      "TMAX" : 221.0,
      "TMIN" : 108.0,
      "PRCP" : 53.0
    }
  } ]
}
```

Data for an interval, i.e. a time series at each station (the response is shortened to data for 2 stations):

```json
{
  "type" : "FeatureCollection",
  "features" : [ {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.888899803161621, 51.57780075073242 ]
    },
    "properties" : {
      "locationCode" : "GMM00010424",
      "locationName" : "WERL",
      "phenomenonTime" : "2019-08-11",
      "TMAX" : 244.0,
      "TMIN" : 138.0,
      "PRCP" : 0.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.888899803161621, 51.57780075073242 ]
    },
    "properties" : {
      "locationCode" : "GMM00010424",
      "locationName" : "WERL",
      "phenomenonTime" : "2019-08-10",
      "TMAX" : 257.0,
      "TMIN" : 181.0,
      "PRCP" : 0.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.888899803161621, 51.57780075073242 ]
    },
    "properties" : {
      "locationCode" : "GMM00010424",
      "locationName" : "WERL",
      "phenomenonTime" : "2019-08-09",
      "TMIN" : 136.0,
      "PRCP" : 15.0,
      "TMAX" : 267.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.888899803161621, 51.57780075073242 ]
    },
    "properties" : {
      "locationCode" : "GMM00010424",
      "locationName" : "WERL",
      "phenomenonTime" : "2019-08-08",
      "TMIN" : 143.0,
      "PRCP" : 0.0,
      "TMAX" : 257.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.888899803161621, 51.57780075073242 ]
    },
    "properties" : {
      "locationCode" : "GMM00010424",
      "locationName" : "WERL",
      "phenomenonTime" : "2019-08-07",
      "TMIN" : 147.0,
      "PRCP" : 0.0,
      "TMAX" : 252.0
    }
  }, ... {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.699999809265137, 52.13529968261719 ]
    },
    "properties" : {
      "locationCode" : "GME00111430",
      "locationName" : "MUENSTER/OSNABRUECK (AIRPORT)",
      "phenomenonTime" : "2019-08-11",
      "TMIN" : 166.0,
      "PRCP" : 0.0,
      "TMAX" : 240.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.699999809265137, 52.13529968261719 ]
    },
    "properties" : {
      "locationCode" : "GME00111430",
      "locationName" : "MUENSTER/OSNABRUECK (AIRPORT)",
      "phenomenonTime" : "2019-08-10",
      "TMIN" : 184.0,
      "PRCP" : 0.0,
      "TMAX" : 259.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.699999809265137, 52.13529968261719 ]
    },
    "properties" : {
      "locationCode" : "GME00111430",
      "locationName" : "MUENSTER/OSNABRUECK (AIRPORT)",
      "phenomenonTime" : "2019-08-09",
      "TMIN" : 121.0,
      "PRCP" : 20.0,
      "TMAX" : 265.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.699999809265137, 52.13529968261719 ]
    },
    "properties" : {
      "locationCode" : "GME00111430",
      "locationName" : "MUENSTER/OSNABRUECK (AIRPORT)",
      "phenomenonTime" : "2019-08-08",
      "TMIN" : 125.0,
      "PRCP" : 0.0,
      "TMAX" : 256.0
    }
  }, {
    "type" : "Feature",
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ 7.699999809265137, 52.13529968261719 ]
    },
    "properties" : {
      "locationCode" : "GME00111430",
      "locationName" : "MUENSTER/OSNABRUECK (AIRPORT)",
      "phenomenonTime" : "2019-08-07",
      "TMIN" : 165.0,
      "PRCP" : 0.0,
      "TMAX" : 257.0
    }
  } ]
}
```

---
[BACK](README.md)
