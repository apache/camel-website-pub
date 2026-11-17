# ![mqtt source](_images/kamelets/mqtt-source.svg) MQTT Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message published to a topic on an MQTT broker, such as Eclipse Mosquitto or HiveMQ, with MQTT 3.1.1.

Use it to collect readings and events from IoT devices and other MQTT clients. A topic with wildcards, such as `sensors/#`, receives from many topics at once. For a broker or clients that use MQTT 5, use `mqtt5-source`.

Output: the body is the payload, as bytes. The `CamelMqttTopic` header is the topic the message was published to, and `CamelMqttQoS` its quality of service.

Good to know: it receives only the messages published while it is connected. Each running copy needs its own `clientId`: two clients with the same ID keep pushing each other off the broker and lose messages. When it is not set, a unique one is generated. It connects with no TLS unless `brokerUrl` starts with `ssl://`, and the integration fails to start when the broker cannot be reached.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The address of the MQTT broker, as `tcp://host:port` (usually port 1883), or `ssl://host:port` for TLS (usually port 8883). | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to subscribe to. `` ` matches one level of the topic and `#` all the levels below, as in `sensors//temperature `` or `sensors/#`. | string |  | sensors/# |
| **clientId** | Client ID | The client ID that names this connection to the broker. It must be unique on the broker: a second client with the same ID pushes the first one off. When it is not set, a unique ID is generated. | string |  | sensor-reader-1 |
| **password** | Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `mqtt-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mqtt-source"
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

## MQTT Source Kamelet Description

### Authentication

This Kamelet supports MQTT authentication using username and password credentials. It can also connect to MQTT brokers without authentication if not required.

### Configuration

The MQTT Source Kamelet supports the following configurations:

-   **Topic**: MQTT topic to subscribe to, with the `+` and `#` wildcards (required)
    
-   **Broker URL**: MQTT broker URL (required, e.g., tcp://broker.example.com:1883, or ssl://broker.example.com:8883 for TLS)
    
-   **Username**: Username for MQTT authentication (optional)
    
-   **Password**: Password for MQTT authentication (optional)
    
-   **Client ID**: MQTT client identifier; a unique one is generated when it is not set. Two clients with the same ID push each other off the broker.
    

The Kamelet subscribes with QoS 2 and a clean session, so it receives only the messages published while it is connected. It has no options to change the QoS or the session.

### Output Format

The Kamelet outputs the MQTT message payload as bytes, with the `CamelMqttTopic` and `CamelMqttQoS` headers.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mqtt-source"
      parameters:
        topic: "sensors/temperature"
        brokerUrl: "tcp://mqtt.example.com:1883"
        username: "mqttuser"
        password: "mqttpass"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Wildcard and a Client ID

```yaml
- route:
    from:
      uri: "kamelet:mqtt-source"
      parameters:
        topic: "critical/#"
        brokerUrl: "tcp://mqtt.example.com:1883"
        username: "mqttuser"
        password: "mqttpass"
        clientId: "camel-consumer-1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with SSL/TLS

```yaml
- route:
    from:
      uri: "kamelet:mqtt-source"
      parameters:
        topic: "secure/data"
        brokerUrl: "ssl://mqtt.example.com:8883"
        username: "mqttuser"
        password: "mqttpass"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Quality of Service Levels

-   **QoS 0**: At most once delivery (fire and forget)
    
-   **QoS 1**: At least once delivery (acknowledged delivery)
    
-   **QoS 2**: Exactly once delivery (assured delivery)
    

The Kamelet subscribes with QoS 2; a message is received with the lower of that and the QoS it was published with.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-source.kamelet.yaml)