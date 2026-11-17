# ![mqtt sink](_images/kamelets/mqtt-sink.svg) MQTT Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a topic on an MQTT broker, such as Eclipse Mosquitto or HiveMQ, with MQTT 3.1.1.

Use it to send commands or data to IoT devices, or to publish readings and events for MQTT clients to receive. For a broker or clients that use MQTT 5, use `mqtt5-sink`.

Input: the body is the payload, as text or bytes, and is sent as it is. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The headers of the message are not sent, as an MQTT 3 message has none.

Output: the message is unchanged.

Good to know: messages are published with quality of service 2 (exactly once) and are not retained by the broker. It connects with no TLS unless `brokerUrl` starts with `ssl://`. It connects when the integration starts, and the integration fails to start when the broker cannot be reached.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The address of the MQTT broker, as `tcp://host:port` (usually port 1883), or `ssl://host:port` for TLS (usually port 8883). | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to publish each message to, such as `sensors/temperature`. Wildcards (`+` and `#`) cannot be used here. | string |  | sensors/temperature |
| **password** | Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

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

MQTT supports different Quality of Service levels for message delivery guarantees. This Kamelet publishes every message with QoS 2 (exactly once), not retained, and has no option to change that.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml)