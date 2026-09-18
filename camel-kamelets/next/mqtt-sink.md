# ![mqtt sink](_images/kamelets/mqtt-sink.svg) MQTT Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows sending messages to any endpoint that supports the MQTT protocol, such as a message broker.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The URL of the broker where to establish the connection. | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to send messages to. | string |  | mytopic |
| **password** | Password | Password to use when connecting to the MQTT broker. | string |  |  |
| **username** | Username | Username to use when connecting to the MQTT broker. | string |  |  |

## Dependencies

At runtime, the `mqtt-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:paho
    
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
            uri: "kamelet:mqtt-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MQTT Sink Kamelet Description

### MQTT Protocol

This Kamelet implements the MQTT (Message Queuing Telemetry Transport) protocol, a lightweight messaging protocol designed for IoT devices and applications with limited bandwidth or unreliable network connections.

### Broker Integration

Connects to MQTT brokers using configurable broker URLs. Supports various MQTT brokers including Eclipse Mosquitto, HiveMQ, and cloud-based MQTT services.

### Publish-Subscribe Pattern

Enables publish-subscribe messaging by sending messages to MQTT topics. This pattern allows for decoupled communication between message producers and consumers.

### Authentication

Optional username and password authentication for secure broker connections. Suitable for both open and secured MQTT broker deployments.

### IoT and Mobile Applications

MQTT’s lightweight nature makes it ideal for:

-   IoT device communication
    
-   Mobile applications with limited bandwidth
    
-   Unreliable network scenarios
    
-   Battery-powered devices requiring minimal overhead
    

### Quality of Service

MQTT supports different Quality of Service levels for message delivery guarantees, though this Kamelet uses the default QoS settings provided by the underlying MQTT client.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml)