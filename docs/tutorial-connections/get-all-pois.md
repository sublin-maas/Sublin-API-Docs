---
sidebar_position: 2
---

# Get all POIs
Before connections can be established all POIs (active and passive) need to be retrieved for a region.

## GET /destinations
Swagger documentation: 
**[https://api.sublin.cloud/docs/#/destinations/destinationsGET](https://api.sublin.cloud/docs/#/destinations/destinationsGET)**

```jsx title="Query example for all destinations of a region"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE
```

```jsx title="Query example for all destinations of a region, limited to the ones with active connections"
?country=at&partnerId=Lt2VECvJPtYim3txD6VE&activeConnections
```

### Relevant Destination Information
Destinations come with all kinds of information but only a few of them are relevant generating connections.

```jsx title="Query example for all destinations of a region, limited to the ones with active connections"
{
  "activeConnections": true, // Only if true connections need to be added
  "stationId": "id_station" // Id of the nearest station - can be train or bus station
  "types": [ // Destination types - see below
    "locality",  // If destination contains locality it is a town with "TRAIN" connections only
    "point_of_interest",
    "lodging"
  ]
}
```

### Destination Types

There are various types of destinations, most of which are treated equally. However, there is one exception: the "locality" destination types. Localities are cities within a region. 

#### Destination Type: Locality
"locality"s only have TRAIN connections from cities to the local train station. These connections servce as starting point for other local connections like private shuttle services for a specific arrival.
