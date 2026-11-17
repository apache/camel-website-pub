# ![mqtt5 sink](_images/kamelets/mqtt5-sink.svg) MQTT v5 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a topic on an MQTT broker, such as Eclipse Mosquitto or HiveMQ, with MQTT 5.

Use it to send commands or data to IoT devices, or to publish readings and events, when the broker or the clients use MQTT 5. For a broker that only speaks MQTT 3.1.1, use `mqtt-sink`.

Input: the body is the payload, as text or bytes, and is sent as it is. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The headers of the message are not sent, not even as MQTT 5 user properties.

Output: the message is unchanged.

Good to know: messages are published with quality of service 2 (exactly once) and are not retained by the broker. It connects with no TLS unless `brokerUrl` starts with `ssl://`. It connects when the integration starts, and the integration fails to start when the broker cannot be reached.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt5-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The address of the MQTT broker, as `tcp://host:port` (usually port 1883), or `ssl://host:port` for TLS (usually port 8883). | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to publish each message to, such as `sensors/temperature`. Wildcards (`+` and `#`) cannot be used here. | string |  | sensors/temperature |
| **password** | Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

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