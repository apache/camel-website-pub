# ![mqtt sink](_images/kamelets/mqtt-sink.svg) MQTT Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a topic on an MQTT broker, such as Eclipse Mosquitto or HiveMQ, with MQTT 3.1.1.

Use it to send commands or data to IoT devices, or to publish readings and events for MQTT clients to receive. For a broker or clients that use MQTT 5, use `mqtt5-sink`.

Input: the body is the payload, as text or bytes, and is sent as it is. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The headers of the message are not sent, as an MQTT 3 message has none.

Output: the message is unchanged.

Good to know: messages are published with quality of service 2 (exactly once) unless `qos` is set, and the broker does not keep them for clients that subscribe later unless `retained` is true. It connects with no TLS unless `brokerUrl` starts with `ssl://`. With TLS it checks the certificate and the host name of the broker, and trusts the certificate authorities that Java trusts by default, or instead the ones in `sslTruststoreLocation`. It connects when the integration starts, and the integration fails to start when the broker cannot be reached or fails these checks.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The address of the MQTT broker, as `tcp://host:port` (usually port 1883), or `ssl://host:port` for TLS (usually port 8883). For a broker with a certificate from a private or self-signed authority, also set `sslTruststoreLocation`. | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to publish each message to, such as `sensors/temperature`. Wildcards (`+` and `#`) cannot be used here. | string |  | sensors/temperature |
| **password** | Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **qos** | Quality of Service | The quality of service to publish each message with: 0 (at most once, with no confirmation from the broker), 1 (at least once, a message can arrive twice) or 2 (exactly once). When it is not set, 2 is used. A subscriber receives the message with the lower of this and the quality of service it subscribed with. Enum values: \* 0 \* 1 \* 2 | integer |  | 1 |
| **retained** | Retained | Whether the broker keeps the message as the last one of the topic, and gives it to every client that subscribes to the topic later, such as the last known state of a device. Each retained message replaces the one before. When it is not set, messages are not retained. | boolean |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The path of a trust store file, in JKS or PKCS12 format, with the certificate of the authority that signed the certificate of the broker. Needed only with an `ssl://` address when the broker uses a certificate that Java does not trust by default, such as one from a private or self-signed authority. Not used with `tcp://`. | string |  | /etc/mqtt/truststore.jks |
| **sslTruststorePassword** | SSL Truststore Password | The password of the trust store file in `sslTruststoreLocation`. | string |  |  |
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

MQTT supports different Quality of Service levels for message delivery guarantees. Set them with `qos`:

-   **QoS 0**: at most once, with no confirmation from the broker
    
-   **QoS 1**: at least once; a message can arrive twice
    
-   **QoS 2**: exactly once (used when `qos` is not set)
    

A subscriber receives each message with the lower of this and the QoS it subscribed with.

### Retained Messages

With `retained: true`, the broker keeps the last message of the topic and gives it to every client that subscribes to the topic later, for example the last known state of a device. Each retained message replaces the one before. When `retained` is not set, the broker does not keep the messages.

### TLS with a Private Certificate Authority

With an `ssl://` address the Kamelet connects with TLS, checks the certificate and the host name of the broker, and trusts the certificate authorities that Java trusts by default. When the broker has a certificate from a private or self-signed authority, put the certificate of that authority in a trust store file (JKS or PKCS12) and set `sslTruststoreLocation` and `sslTruststorePassword`. The Kamelet then trusts the authorities in that file instead.

```bash
keytool -importcert -alias mqtt-ca -file ca.crt -keystore truststore.jks -storepass changeit
```

### Example with QoS 1, Retained and TLS

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "online"
        period: 60000
      steps:
        - to:
            uri: "kamelet:mqtt-sink"
            parameters:
              topic: "devices/gateway-1/status"
              brokerUrl: "ssl://mqtt.example.com:8883"
              username: "mqttuser"
              password: "mqttpass"
              qos: 1
              retained: true
              sslTruststoreLocation: "/etc/mqtt/truststore.jks"
              sslTruststorePassword: "changeit"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-sink.kamelet.yaml)