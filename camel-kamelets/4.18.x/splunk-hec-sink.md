# ![splunk hec sink](_images/kamelets/splunk-hec-sink.svg) Splunk HEC Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

The Splunk HEC sink allows to send data to Splunk using the [HTTP Event Collector](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector).

## Configuration Options

The following table summarizes the configuration options available for the `splunk-hec-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **splunkUrl** | Splunk URL | **Required** The URL of your Splunk server. No need to set the protocol prefix. | string |  | my\_server.splunkcloud.com:8088 |
| **token** | Token | **Required** The Token of the HEC. Note it is not the user’s authentication token. | string |  |  |
| **bodyOnly** | Body Only | Send to Splunk only data contained in the body. | boolean | false |  |
| **headersOnly** | Headers Only | Send to Splunk only data contained in the headers. | boolean | false |  |
| **hostPayload** | Host of the Event | The host field set in the data sent to Splunk, it is not related to the Splunk URL or the connection to Splunk server. | string |  |  |
| **https** | Secure | Use a secure HTTPS connection. | boolean | true |  |
| **index** | Index | Splunk index to write to. | string |  |  |
| **skipTlsVerify** | Skip TLS Verification | Skip TLS verification. | boolean | false |  |
| **source** | Source | The source named field of the data. | string |  |  |
| **sourceType** | Source Type | The source named field of the data. | string |  |  |
| **time** | Time | Time this event occurred. By default, the time is when this event hits the Splunk server. | string |  |  |

## Dependencies

At runtime, the `splunk-hec-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:splunk-hec
    
-   camel:kamelet
    

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:splunk-hec-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Splunk HEC Sink Kamelet Description

### Splunk HTTP Event Collector

This Kamelet integrates with Splunk’s HTTP Event Collector (HEC), which provides a fast and efficient way to send data to Splunk over HTTP/HTTPS connections.

### High-Performance Data Ingestion

HEC is designed for high-volume data ingestion, supporting:

-   High throughput data streaming
    
-   Batch and real-time data ingestion
    
-   Efficient HTTP-based protocol
    
-   Load balancing across multiple Splunk indexers
    

### Event Formatting

Supports Splunk event formatting with configurable:

-   Source and source type settings
    
-   Index targeting
    
-   Host identification
    
-   Custom field extraction
    
-   Timestamp handling
    

### Security and Authentication

Provides secure data transmission through:

-   Token-based authentication
    
-   HTTPS encryption
    
-   IP allowlisting capabilities
    
-   Role-based access controls
    

### Monitoring and Analytics

Ideal for sending various types of data to Splunk for:

-   Log aggregation and analysis
    
-   Metrics and performance monitoring
    
-   Security event correlation
    
-   Business intelligence and reporting
    
-   Machine learning and anomaly detection
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-hec-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-hec-sink.kamelet.yaml)