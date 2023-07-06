---
sidebar_position: 4
---

# Manage Connections

Connections can be added on a destination basis. 

## POST /destinations/{id}/connections
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/destinations/destinationsIdServicesPOST](https://api.sublin.cloud/docs/#/destinations/destinationsIdServicesPOST)**. The maximum limit for connections per POST call is set at 500.


### Connection Schema
Not all destination types are connected to the train stations and to each other.

|  | Departure train station | Regional train station |  lodging | point_of_interest |
| ----------- | ----------- | ----------- |  ----------- | ----------- |
| locality | [x] |
| lodging (active only) | [x] | [x] | | [x] |
| point_of_interest (active) | [x] | [x] |  | [x] |
| point_of_interest (passive) | |

### Connection Types
Depending of the connection type different information needs to be provided.

Following connection types are supported:
  - [STATIONBUS](#STATIONBUS) (from local train station to POI via bus)
  - [STATIONFOOT](#STATIONFOOT)  (from local train station to POI via foot)
  - [BUS](#BUS) (from POI to POI via bus)
  - [TRAIN](#TRAIN) (from city to local train station)

> **Note: When making a POST call, any existing connections of the same connection type will be removed before new connections are added.**

#### <a name="STATIONBUS" />STATIONBUS

```jsx title="STATIONBUS example to hotel 'Sonngastein'"
{
  "connectionId": "id_of_connection", // Typically, the identification (ID) of the primary mode of transportation is used
  "assetClass": "STATIONBUS", // Connection type - will be renamed in the coming versions
  "description": "description", // Typically, the name of the line
  "providerId": "provider_id", // Id of provider of connection
  "partnerId": "partner_id", // Id of the regional partner
  "destinationId": "id_of_hotel_Sonngastein",
  "arrivalId": "id_of_hotel_Sonngastein",
  "arrivalName": "Sonngastein",
  "arrivalStationId": "id_of_bus_station",
  "stationId": "local_train_station",
  "routes": [
    {
      "departureTime": 449,
      "numberLegs": 2,
      "stationId": "id_of_wien_hbf",
      "stationName": "Wien Hbf",
      "trainName":  "RJ111"
    }
  ],
  "hours": {
      "days": ["MON", "TUE", "WED", "THU", "FRI"],
      "endTime": 728, //Departure time (in minutes) from the local train station
      "startTime": 715 //Arrival time at the destination
  },
  "calender": {
      "startMonth": 1,
      "endMonth": 12,
      "startDay": 1,
      "endDay": 12
  },
  "deepLink": "link" // A deep link is provided, enabling access to the route through a specific app.
}
```

#### <a name="STATIONFOOT" />STATIONSFOOT

```jsx title="STATIONFOOT example to hotel 'Sonngastein'"
{
  "connectionId": "id_of_connection", // Typically, the identification (ID) of the primary mode of transportation is used
  "assetClass": "STATIONFOOT",
  "description": "description", // Typically, the name of the line
  "providerId": "provider_id", // Id of provider of connection
  "partnerId": "partner_id", // Id of the regional partner
  "destinationId": "id_of_hotel_Sonngastein",
  "arrivalId": "id_of_hotel_Sonngastein",
  "arrivalName": "Sonngastein",
  "stationId": "local_train_station",
  "routes": [
    {
      "departureTime": 449,
      "numberLegs": 2,
      "stationId": "id_of_wien_hbf",
      "stationName": "Wien Hbf",
      "trainName":  "RJ111"
    }
  ],
  "hours": {
      "days": ["MON", "TUE", "WED", "THU", "FRI"],
      "endTime": 728, //Departure time (in minutes) from the local train station
      "startTime": 715 //Arrival time at the destination
  },
  "calender": {
      "startMonth": 1,
      "endMonth": 12,
      "startDay": 1,
      "endDay": 12
  },
  "deepLink": "link" // A deep link is provided, enabling access to the route through a specific app.
}
```

#### <a name="BUS" />BUS

```jsx title="BUS example from hotel 'Sonngastein' to 'Felsentherme '"
{
  "connectionId": "id_of_connection", // Typically, the identification (ID) of the primary mode of transportation is used
  "assetClass": "BUS",
  "description": "description", // Typically, the name of the line
  "providerId": "provider_id", // Id of provider of connection
  "partnerId": "partner_id", // Id of the regional partner
  "destinationId": "id_of_hotel_Sonngastein",
  "arrivalId": "id_of_felsentherme",
  "arrivalName": "Felsentherme",
  "arrivalStationId": "id_of_bus_station",
  "departureId": "id_of_hotel_Sonngastein",
  "departureName": "Sonngastein",
  "departureStationId": "id_of_bus_station",
  "hours": {
      "days": ["MON", "TUE", "WED", "THU", "FRI"],
      "endTime": 728, //Departure time (in minutes) from the local train station
      "startTime": 715 //Arrival time at the destination
  },
  "calender": {
      "startMonth": 1,
      "endMonth": 12,
      "startDay": 1,
      "endDay": 12
  },
  "deepLink": "link" // A deep link is provided, enabling access to the route through a specific app.
}
```

#### <a name="TRAIN" />TRAIN
This type is limited to the "locality" destination type, as it serves exclusively as the starting point for other local connections.

```jsx title="TRAIN example from departure stations to local train station 'Bad Gastein'"
{
  "connectionId": "id_of_connection", // Typically, the identification (ID) of the primary mode of transportation is used
  "assetClass": "TRAIN",
  "description": "description", // Typically, the name of the line
  "providerId": "provider_id" // Id of provider of connection
  "partnerId": "partner_id" // Id of the regional partner
  "destinationId": "id_of_bad_gastein", // Id of locality
  "arrivalStationId": "id_of_arrivalStation", 
  "arrivalStationName": "name_of_arrivalStation", 
  "routes": [ // All stations on the way that are included as starting stations and use the same initial leg
    {
      "departureTime": 449,
      "numberLegs": 2,
      "stationId": "id_of_wien_hbf",
      "stationName": "Wien Hbf",
      "trainName":  "RJ111"
    },
    {
      "departureTime": 455,
      "numberLegs": 2,
      "stationId": "id_of_wien_meidling",
      "stationName": "Wien Meidling",
      "trainName":  "RJ111"
    }
  ],
  "hours": {
      "days": ["MON", "TUE", "WED", "THU", "FRI"],
      "endTime": 728, //Departure time (in minutes) from the local train station
      "startTime": 715 //Arrival time at the destination
  },
  "calender": {
      "startMonth": 1,
      "endMonth": 12,
      "startDay": 1,
      "endDay": 12
  },
  "deepLink": "link" // A deep link is provided, enabling access to the route through a specific app.
}
```

```jsx title="TRAIN example from local train station 'Bad Gastein' to departure stations"
{
  "connectionId": "id_of_connection", // Typically, the identification (ID) of the primary mode of transportation is used
  "assetClass": "TRAIN",
  "description": "description", // Typically, the name of the line
  "providerId": "provider_id" // Id of provider of connection
  "partnerId": "partner_id" // Id of the regional partner
  "destinationId": "id_of_bad_gastein", // Id of locality
  "departureStationId": "id_of_arrivalStation", 
  "departureStationName": "name_of_arrivalStation", 
  "routes": [ // All stations on the way that are included as starting stations and use the same initial leg
    {
      "arrivalTime": 728,
      "numberLegs": 2,
      "stationId": "id_of_wien_hbf",
      "stationName": "Wien Hbf",
      "trainName":  "RJ111"
    },
    {
      "arrivalTime": 723,
      "numberLegs": 2,
      "stationId": "id_of_wien_meidling",
      "stationName": "Wien Meidling",
      "trainName":  "RJ111"
    }
  ],
  "hours": {
      "days": ["MON", "TUE", "WED", "THU", "FRI"],
      "endTime": 728, //Departure time (in minutes) from the local train station
      "startTime": 715 //Arrival time at the destination
  },
  "calender": {
      "startMonth": 1,
      "endMonth": 12,
      "startDay": 1,
      "endDay": 12
  },
  "deepLink": "link" // A deep link is provided, enabling access to the route through a specific app.
}
```

## GET /connections/destinations/{id}
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/connections/connectionsDestinationsIdGET](https://api.sublin.cloud/docs/#/connections/connectionsDestinationsIdGET)**.