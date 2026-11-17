# ![earthquake source](_images/kamelets/earthquake-source.svg) Earthquake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message for each earthquake reported by the USGS (United States Geological Survey), checking for new reports at a regular interval.

Use it to follow the earthquakes around the world, for example to alert on the strong ones, or as a stream of real, changing JSON data for a demo. No account is needed.

Output: one message per earthquake. The body is a GeoJSON feature, as JSON text: `properties` has the magnitude (`mag`), the place, the time and a link to the USGS page, and `geometry` has the longitude, the latitude and the depth. The `Content-Type` header is `application/json`.

Good to know: the first check sends the earthquakes whose report was updated in the last `lookAhead` minutes, and each later check those updated since the check before. An earthquake is sent again when USGS updates its report. The time of the last check is kept in memory only, so a restart begins again with the last `lookAhead` minutes. It calls `[https://earthquake.usgs.gov](https://earthquake.usgs.gov)` over the internet.

## Configuration Options

The following table summarizes the configuration options available for the `earthquake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **lookAhead** | Minutes to Look Back | When the integration starts, how many minutes back to look for earthquake reports. For example, 1440 first sends the reports of the last day. | integer | 120 | 1440 |
| **period** | Period | How long to wait between two checks for new reports, in milliseconds. For example, 300000 is five minutes. | integer | 60000 | 300000 |

## Dependencies

At runtime, the `earthquake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:caffeine
    
-   camel:http
    
-   camel:kamelet
    
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
    
2.  Only fetching earthquakes whose report was updated after the last known update, so an earthquake is sent again when USGS updates its report
    
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