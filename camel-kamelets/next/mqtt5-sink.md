# ![mqtt5 sink](_images/kamelets/mqtt5-sink.svg) MQTT v5 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows sending messages to any endpoint that supports the MQTT v5 protocol, such as a message broker.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt5-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The URL of the broker where to establish the connection. | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to send messages to. | string |  | mytopic |
| **password** | Password | Password to use when connecting to the MQTT v5 compliant broker. | string |  |  |
| **username** | Username | Username to use when connecting to the MQTT v5 compliant broker. | string |  |  |

## Dependencies

At runtime, the `mqtt5-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:mqtt5-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MQTT v5 Sink Kamelet Description

### MQTT v5 Protocol

This Kamelet implements MQTT version 5.0, the latest version of the MQTT protocol that provides enhanced features over previous versions including improved error reporting, session expiry, and user properties.

### Broker Connectivity

Connects to any MQTT v5 compliant broker using configurable broker URLs. Supports various connection protocols including TCP, SSL, and WebSocket connections.

### Authentication

Optional username and password authentication for secure broker connections. Credentials are securely managed for broker access control.

### Enhanced Features

MQTT v5 provides several enhancements over previous versions:

-   Improved error reporting and reason codes
    
-   Session expiry intervals
    
-   User properties for custom metadata
    
-   Subscription options and shared subscriptions
    

### Topic Publishing

Publishes messages to specified MQTT topics, enabling reliable message delivery in IoT and messaging scenarios.

### Lightweight Protocol

MQTT is designed for lightweight, low-bandwidth, and unreliable network scenarios, making it ideal for IoT devices and mobile applications.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-sink.kamelet.yaml)