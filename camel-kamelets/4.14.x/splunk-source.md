# ![splunk source](_images/kamelets/splunk-source.svg) Splunk Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Retrieve data from Splunk and outputs in json format.

## Configuration Options

The following table summarizes the configuration options available for the `splunk-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **initEarliestTime** | Init Earliest Time | **Required** Initial start offset of the first search. | string |  | 05/17/22 08:35:46:456 |
| **password** | Password | **Required** The password to authenticate to Splunk Server. | string |  |  |
| **query** | Query | **Required** The Splunk query to run. | string |  |  |
| **serverHostname** | Splunk Server Address | **Required** The address of your Splunk server. | string |  | my\_server\_splunk.com |
| **username** | Username | **Required** The username to authenticate to Splunk Server. | string |  |  |
| **app** | Splunk App | The app name in Splunk. | string |  |  |
| **connectionTimeout** | Connection Timeout | Timeout in milliseconds when connecting to Splunk server. | integer |  |  |
| **count** | Count | The maximum number of entities to return. | integer |  |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer |  |  |
| **earliestTime** | Earliest Time | Earliest time of the search time window. | string |  | 05/17/22 08:35:46:456 |
| **index** | Index | Splunk index to write to. | string |  |  |
| **latestTime** | Latest Time | Latest time of the search time window. | string |  | 05/17/22 08:35:46:456 |
| **protocol** | Protocol | Connection Protocol to Splunk server. Enum values: \* http \* https | string | https |  |
| **repeat** | Repeat | The maximum number of fires. | integer |  |  |
| **serverPort** | Splunk Server Port | The address of your Splunk server. | integer | 8089 |  |
| **source** | Source | The source named field of the data. | string |  |  |
| **sourceType** | Source Type | The source named field of the data. | string |  |  |

## Dependencies

At runtime, the `splunk-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:core
    
-   camel:splunk
    
-   camel:kamelet
    
-   mvn:com.fasterxml.jackson.datatype:jackson-datatype-joda:2.12.5
    

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
      uri: "kamelet:splunk-source"
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

## Splunk Source Kamelet Description

### Authentication methods

This Kamelet connects to Splunk using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Splunk and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Splunk:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: splunk-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: splunk-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/splunk-source.kamelet.yaml)