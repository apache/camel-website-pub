# ![mqtt5 source](_images/kamelets/mqtt5-source.svg) MQTT 5 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message published to a topic on an MQTT broker, such as Eclipse Mosquitto or HiveMQ, with MQTT 5.

Use it to collect readings and events from IoT devices and other MQTT clients, when the broker or the clients use MQTT 5. A topic with wildcards, such as `sensors/#`, receives from many topics at once. For a broker that only speaks MQTT 3.1.1, use `mqtt-source`.

Output: the body is the payload, as bytes. The `CamelMqttTopic` header is the topic the message was published to, `CamelMqttQoS` its quality of service, and `CamelPahoMqtt5MsgProperties` holds the MQTT 5 properties of the message, such as its user properties.

Good to know: it receives only the messages published while it is connected. Each running copy needs its own `clientId`: two clients with the same ID keep pushing each other off the broker and lose messages. When it is not set, a unique one is generated. It connects with no TLS unless `brokerUrl` starts with `ssl://`, and the integration fails to start when the broker cannot be reached.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt5-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The address of the MQTT broker, as `tcp://host:port` (usually port 1883), or `ssl://host:port` for TLS (usually port 8883). | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to subscribe to. `` ` matches one level of the topic and `#` all the levels below, as in `sensors//temperature `` or `sensors/#`. | string |  | sensors/# |
| **clientId** | Client ID | The client ID that names this connection to the broker. It must be unique on the broker: a second client with the same ID pushes the first one off. When it is not set, a unique ID is generated. | string |  | sensor-reader-1 |
| **password** | Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

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

## MQTT 5 Source Kamelet Description

### Authentication

The Kamelet logs in to the broker with `username` and `password`, or without a login when they are not set. For TLS, use an `ssl://` address in `brokerUrl`.

### Output format

The body is the MQTT payload, as bytes; it is not turned into JSON. The `CamelMqttTopic` header is the topic of the message, `CamelMqttQoS` its quality of service, and `CamelPahoMqtt5MsgProperties` its MQTT 5 properties.

### Configuration

-   `topic`: the topic to subscribe to, with the `+` and `#` wildcards
    
-   `brokerUrl`: the address of the broker, such as `tcp://mosquitto:1883`
    
-   `clientId`: the client ID; a unique one is generated when it is not set
    
-   `username` and `password`: the login, when the broker needs one
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:mqtt5-source"
      parameters:
        topic: "sensors/#"
        brokerUrl: "tcp://mosquitto:1883"
        clientId: "sensor-reader-1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt5-source.kamelet.yaml)