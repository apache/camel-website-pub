# ![splunk hec sink](_images/kamelets/splunk-hec-sink.svg) Splunk HEC Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an event to Splunk through its HTTP Event Collector (HEC), for searching, dashboards and alerts in Splunk.

Use it to send application logs, audit records, metrics or business events from any flow into a Splunk index.

Input: the body is the event, as text or as structured data such as a Map, which is sent as a JSON object. By default the event sent to Splunk is a JSON object with the headers of the message under `headers` and the body under `body`; `bodyOnly` sends the body alone, and `headersOnly` the headers alone.

Output: the message is unchanged.

Good to know: when `index`, `source` and `sourceType` are not set, the events go to the index `camel` with the source and source type `camel`, so set them for your Splunk. The `host` field of the event is the IP address of the machine that runs the integration, unless `hostPayload` is set. It connects with HTTPS and checks the certificate of the server, unless `https` or `skipTlsVerify` say otherwise. Headers that start with `CamelSplunkHEC` are removed from the message first, so they cannot change what the Kamelet does. It sends to the event endpoint `/services/collector/event`; with `splunkEndpoint` set to `/services/collector/raw`, Splunk stores the whole JSON object as raw text instead, and `index`, `source` and `sourceType` no longer apply. A response other than 200, such as a wrong path, fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `splunk-hec-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **splunkUrl** | Splunk URL | **Required** The host and port of the HTTP Event Collector of your Splunk, as `host:port`, without `https://`. The port of HEC is 8088 unless your Splunk administrator changed it. | string |  | my\_server.splunkcloud.com:8088 |
| **token** | Token | **Required** The token of an HTTP Event Collector input, from Settings, Data Inputs, HTTP Event Collector in Splunk. It is a GUID such as `12345678-1234-1234-1234-123456789012`, not the token of a user; a value in another form makes the integration fail to start. | string |  |  |
| **bodyOnly** | Body Only | If true, the event is the body alone, without the headers of the message. | boolean | false |  |
| **headersOnly** | Headers Only | If true, the event is the headers of the message alone, as a JSON object, without the body. | boolean | false |  |
| **hostPayload** | Host of the Event | The value of the `host` field of every event, such as the name of the machine or application that the events are about. It is not the address of Splunk. When it is not set, the IP address of the machine that runs the integration is used. | string |  | web-1 |
| **https** | Secure | If true, it connects with HTTPS. Set it to false only for an HTTP Event Collector without TLS. | boolean | true |  |
| **index** | Index | The Splunk index to write the events to. The token must be allowed to write to it. When it is not set, the index `camel` is used. | string |  | main |
| **skipTlsVerify** | Skip TLS Verification | If true, the certificate of the Splunk server is not checked. Use it only for tests with a self-signed certificate. | boolean | false |  |
| **source** | Source | The value of the `source` field of every event, which tells where the events come from. When it is not set, `camel` is used. | string |  | shop-orders |
| **sourceType** | Source Type | The value of the `sourcetype` field of every event, which tells Splunk how to read the events, such as `_json`. When it is not set, `camel` is used. | string |  | \_json |
| **splunkEndpoint** | Splunk Endpoint | The path of the HTTP Event Collector endpoint to send to, starting with `/`, optionally followed by query parameters. When it is not set, it is `/services/collector/event`. With `/services/collector/raw`, Splunk stores the whole JSON object that the Kamelet sends as the text of the event, and takes the index, source and source type from the token and from query parameters, not from `index`, `source` and `sourceType`, such as `/services/collector/raw?index=main&sourcetype=_json`. | string |  | /services/collector/raw |
| **time** | Time | The time of every event, as the number of seconds since 1 January 1970 (UTC). When it is not set, Splunk uses the time the event arrives. | string |  | 1700000000 |

## Dependencies

At runtime, the `splunk-hec-sink` Kamelet relies upon the presence of the following dependencies:

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
    

### Event and Raw Endpoints

By default the Kamelet sends to the event endpoint, `/services/collector/event`, and Splunk takes the index, the source and the source type of each event from `index`, `source` and `sourceType`. With `splunkEndpoint` set to `/services/collector/raw`, Splunk stores the whole JSON object that the Kamelet sends as the raw text of the event. The index, the source and the source type then come from the token, or from query parameters on the path:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: "hello"
      steps:
        - to:
            uri: "kamelet:splunk-hec-sink"
            parameters:
              splunkUrl: "my_server.splunkcloud.com:8088"
              token: "12345678-1234-1234-1234-123456789012"
              splunkEndpoint: "/services/collector/raw?index=main&sourcetype=_json"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-hec-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-hec-sink.kamelet.yaml)