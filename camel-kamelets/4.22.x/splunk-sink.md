# ![splunk sink](_images/kamelets/splunk-sink.svg) Splunk Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Splunk either by using "submit" or "stream" mode.

## Configuration Options

The following table summarizes the configuration options available for the `splunk-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **password** | Password | **Required** The password to authenticate to Splunk Server. | string |  |  |
| **serverHostname** | Splunk Server Address | **Required** The address of your Splunk server. | string |  | my\_server\_splunk.com |
| **username** | Username | **Required** The username to authenticate to Splunk Server. | string |  |  |
| **app** | Splunk App | The app name in Splunk. | string |  |  |
| **connectionTimeout** | Connection Timeout | Timeout in milliseconds when connecting to Splunk server. | integer | 5000 |  |
| **index** | Index | Splunk index to write to. | string |  |  |
| **mode** | Mode | The mode to publish events to Splunk. Enum values: \* submit \* stream | string | stream |  |
| **protocol** | Protocol | Connection Protocol to Splunk server. Enum values: \* http \* https | string | https |  |
| **serverPort** | Splunk Server Port | The address of your Splunk server. | integer | 8089 |  |
| **source** | Source | The source named field of the data. | string |  |  |
| **sourceType** | Source Type | The source named field of the data. | string |  |  |

## Dependencies

At runtime, the `splunk-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:splunk
    
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
            uri: "kamelet:splunk-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Splunk Sink Kamelet Description

### Splunk Platform Integration

This Kamelet provides integration with Splunk, a comprehensive platform for searching, monitoring, and analyzing machine-generated data in real-time.

### Data Ingestion

Sends data to Splunk for indexing and analysis, enabling comprehensive data analytics and operational intelligence across various data sources.

### Search and Analytics

Splunk provides powerful capabilities for:

-   Full-text search across all indexed data
    
-   Real-time and historical data analysis
    
-   Complex correlation and pattern detection
    
-   Custom dashboards and visualizations
    
-   Alerting and notification systems
    

### Machine Learning

Splunk includes machine learning capabilities for:

-   Anomaly detection
    
-   Predictive analytics
    
-   Automated insights
    
-   Pattern recognition
    
-   Behavioral analysis
    

### Use Cases

Common applications include:

-   IT operations monitoring and troubleshooting
    
-   Security information and event management (SIEM)
    
-   Business analytics and KPI tracking
    
-   Compliance reporting and auditing
    
-   IoT data analysis and monitoring
    

### Data Format Support

Supports various data formats and provides flexible parsing capabilities to handle structured, semi-structured, and unstructured data from multiple sources.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-sink.kamelet.yaml)