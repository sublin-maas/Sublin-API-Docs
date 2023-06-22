---
sidebar_position: 3
---

# Manage Stations

Before connections can be added, it is necessary to include all the stations (both train and bus stations) for a given region.

## POST /connections/stations
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/connections/connectionsStationsPOST](https://api.sublin.cloud/docs/#/connections/connectionsStationsPOST)**

### Connection Types
Following connection types are supported:
  - [TRAIN](#TRAIN) 
  - [BUS](#BUS) 


#### <a name="TRAIN" />Train Station

```jsx title="Train station Bad Gastein'"
{
  "partnerId": "partner_id", // Id of region
  "providerId": "provider_id", // Id of provider of data
  "assetClass": "TRAIN"
  "departureOnly": false, // Is true if it is a city train station for departure only
  "stopName": "Bad Gastein Bahnhof",
  "stopCode": "",
  "country": "at",
  "stopUrl": "",
  "stopLon": 13.132041,
  "stopId": "8100095",
  "stopLat": 47.111306,
  "zoneId": "",
  "stopDesc": "",
}
```

#### <a name="BUS" />Bus station

```jsx title="A bus station in Bad Gastein"
{
  "partnerId": "partner_id", // Id of region
  "providerId": "provider_id", // Id of provider of data
  "assetClass": "BUS"
  "departureOnly": false, // Is true if it is a city train station for departure only
  "stopName": "Bad Gastein Kötschachdorf",
  "stopCode": "",
  "country": "at",
  "stopUrl": "",
  "stopLon": 13.15151742377142,
  "stopId": "XXX",
  "stopLat": 47.13952037809829,
  "zoneId": "",
  "stopDesc": "",
}
```

## GET /connections/stations
Swagger documentation: **[https://api.sublin.cloud/docs/#/connections/connectionsStationsGET](https://api.sublin.cloud/docs/#/connections/connectionsStationsGET)**

```jsx title="Query example for all stations of a region"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE
```