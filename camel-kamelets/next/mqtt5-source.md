# ![mqtt5 source](_images/kamelets/mqtt5-source.svg) MQTT 5 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows receiving messages from any endpoint that supports the MQTT v5 protocol, such as a message broker.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt5-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The URL of the broker where to establish the connection. | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to subscribe to. | string |  | mytopic |
| **clientId** | Client ID | The client ID to use when connecting to the resource. | string | mqtt-source |  |
| **password** | Password | Password to use when connecting to the MQTT v5 compliant broker. | string |  |  |
| **username** | Username | Username to use when connecting to the MQTT v5 compliant broker. | string |  |  |

## Dependencies

At runtime, the `mqtt5-source` Kamelet relies upon the presence of the following dependencies:

-   camel:paho-mqtt5
    
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
      uri: "kamelet:mqtt5-source"
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

## Mqtt5 Source Kamelet Description

### Authentication methods

This Kamelet connects to Mqtt5 using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Mqtt5 and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Mqtt5:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: mqtt5-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: mqtt5-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-source.kamelet.yaml)