# ![earthquake source](_images/kamelets/earthquake-source.svg) Earthquake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Get data about current earthquake events happening in the world using the USGS API

## Configuration Options

The following table summarizes the configuration options available for the `earthquake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **lookAhead** | Look-ahead Minutes | The amount of minutes to look ahead when starting the integration afresh. | integer | 120 |  |
| **period** | Period between Polls | The interval between fetches to the earthquake API in milliseconds. | integer | 60000 |  |

## Dependencies

At runtime, the `earthquake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:caffeine
    
-   camel:http
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jackson
    
-   camel:jsonpath
    
-   camel:timer
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:earthquake-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Earthquake Source Kamelet Description

This Kamelet provides real-time earthquake data from the United States Geological Survey (USGS) API. It periodically fetches information about current earthquake events happening worldwide and outputs each earthquake as a separate JSON message.

### Output format

The Kamelet outputs earthquake data in JSON format. Each message contains details about a single earthquake event, including:

-   Geographic coordinates (latitude, longitude)
    
-   Magnitude and depth
    
-   Time of occurrence
    
-   Location description
    
-   Additional metadata from USGS
    

### Data source

The Kamelet uses the official USGS Earthquake API at `[https://earthquake.usgs.gov/fdsnws/event/1/query](https://earthquake.usgs.gov/fdsnws/event/1/query)` to retrieve earthquake data in GeoJSON format.

### Configuration options

-   **period**: Polling interval in milliseconds (default: 60000 = 1 minute)
    
-   **lookAhead**: When starting fresh, how many minutes back to look for earthquakes (default: 120 minutes)
    

### Caching mechanism

The Kamelet maintains state to avoid duplicate earthquake reports by:

1.  Caching the timestamp of the last update
    
2.  Only fetching earthquakes that occurred after the last known update
    
3.  Using the USGS API’s `updatedafter` parameter for efficient filtering
    

### Usage examples

Basic earthquake monitoring with default settings:

```yaml
- route:
    from:
      uri: "kamelet:earthquake-source"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Custom polling interval and look-ahead period:

```yaml
- route:
    from:
      uri: "kamelet:earthquake-source"
      parameters:
        period: 300000
        lookAhead: 60
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Filter earthquakes by magnitude in the route:

```yaml
- route:
    from:
      uri: "kamelet:earthquake-source"
      steps:
        - filter:
            simple: "${jsonpath($.properties.mag)} >= 4.0"
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/earthquake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/earthquake-source.kamelet.yaml)