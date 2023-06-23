---
sidebar_position: 3
---

# Get POIs
Before connections can be managed all POIs (active and passive) need to be retrieved for a region. 

### Active/Passive Connections

There are two primary categories of POIs: those with active connections and those without. POIs with active connections are associated with generated connections, meaning transportation options or links will be provided for these POIs. On the other hand, POIs without active connections solely rely on passive connections, which are generated from the active connections of other POIs.

In other words, active connections are directly generated for certain POIs, while other POIs benefit from indirect connections established through the active connections of neighboring POIs.

## GET /destinations
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/destinations/destinationsGET](https://api.sublin.cloud/docs/#/destinations/destinationsGET)**

```jsx title="Query example for all destinations of a region"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE
```

```jsx title="Query example for all destinations of a region, limited to the ones with active connections"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE&activeConnections
```



#### Example
A hotel with active connections provides convenient transportation options, including a bus and shuttle service, that link to the train station. Additionally, this hotel offers various bus and walking routes to nearby attractions such as a spa center, ski lift, and restaurant. On the other hand, while a nearby restaurant does not have its own active connections, it benefits from a passive connection provided by the hotel.

```jsx title="Example of hotel with active connection"
{
  ...
  "activeConnections": true, // Only if true connections need to be added
  "stationId": "id_station" // Id of the nearest station - can be train or bus station
  "types": [ 
    "lodging"
  ]
  ...
}
```

## Destination Types

There are several types of destinations, with most of them being treated equally. However, there is one exception: the "locality" destination type. Localities refer to municipalities or subregions within a region.

```jsx title="Response snippet example for all destinations of a region, limited to the ones with active connections"

  "types": [ // Destination types - see below
    "locality",  // If destination contains locality it is a town with "TRAIN" connections only
    "point_of_interest",
    "lodging",
    "ski",
    "spa",
    ...
  ]

```

### Destination Type: Locality
"locality"s only have TRAIN connections from cities to the local train station. These connections servce as starting point for other local connections like private shuttle services for a specific arrival.

## Time Frames (Coming soon)
Sublin is dedicated to promoting appropriate connections to Points of Interest (POIs). Currently, the determination of what constitutes a suitable connection is primarily based on destination types. For instance, a connection to a ski lift after closing hours would not be considered suitable. However, to further customize connections based on the unique circumstances of each individual POI, Sublin allows each POI to define specific time frames for arrivals and departures.

By incorporating these customizable time frames, Sublin ensures that the connections presented align more closely with the specific requirements and operating hours of each POI. 

```jsx title="Example of a time frame for a spa center"

  [ 
    {
      "hours": {
        "days": ["MON", "TUE", "WED", "THU", "FRI"],
        "endTime": 600, 
        "startTime": 1380 
    },
      "calender": {
          "startMonth": 1,
          "endMonth": 12,
          "startDay": 1,
          "endDay": 12
      },
    },
    {
      "hours": {
        "days": ["SAT", "SUN"],
        "endTime": 600, 
        "startTime": 1320 
    },
      "calender": {
          "startMonth": 1,
          "endMonth": 12,
          "startDay": 1,
          "endDay": 12
      },
    }
  ]

```

