---
sidebar_position: 2
---

# Region Setup

In order for a region to be managed by a regional partner, two prerequisite steps must be completed. Firstly, the stations within the region need to be added. This includes one or more train stations that are interconnected with cities, as well as a variety of regional bus stations. Secondly, the connections between the train stations and the cities need to be established. 

## 1. Adding Stations

Following connection types are supported:
  - [TRAIN](#TRAIN) 
  - [BUS](#BUS) 

### POST /connections/stations
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/connections/connectionsStationsPOST](https://api.sublin.cloud/docs/#/connections/connectionsStationsPOST)** The number of items allowed in a POST call is limited to 500.


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

### GET /connections/stations
Swagger documentation: **[https://api.sublin.cloud/docs/#/connections/connectionsStationsGET](https://api.sublin.cloud/docs/#/connections/connectionsStationsGET)**

```jsx title="Query example for all stations of a region"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE
```

## 2. Connect the region to cities
Before initiating the onboarding process for Points of Interest (POIs) within a region, it is essential to establish connections between the train stations in the region and the cities located outside of the region. These connections serve as the starting point for further connections within the region, such as shuttle services from the POIs.

For information on connection management, including establishing and managing these train connections, please consult the "[Manage Connections](/docs/tutorial-connections/manage-connections)" section. 