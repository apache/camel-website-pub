# ![mqtt source](_images/kamelets/mqtt-source.svg) MQTT Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Allows receiving messages from any endpoint that supports the MQTT protocol, such as a message broker.

## Configuration Options

The following table summarizes the configuration options available for the `mqtt-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerUrl** | Broker URL | **Required** The URL of the broker where to establish the connection. | string |  | tcp://mosquitto:1883 |
| **topic** | Topic | **Required** The topic to subscribe to. | string |  | mytopic |
| **clientId** | Client ID | The client ID to use when connecting to the resource. | string | mqtt-source |  |
| **password** | Password | Password to use when connecting to the MQTT broker. | string |  |  |
| **username** | Username | Username to use when connecting to the MQTT broker. | string |  |  |

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

-   **Topic**: MQTT topic to subscribe to (required)
    
-   **Broker URL**: MQTT broker URL (required, e.g., tcp://broker.example.com:1883)
    
-   **Username**: Username for MQTT authentication (optional)
    
-   **Password**: Password for MQTT authentication (optional)
    
-   **Client ID**: MQTT client identifier (optional)
    
-   **Quality of Service**: QoS level (0, 1, or 2)
    
-   **Retain**: Whether to retain messages
    
-   **Clean Session**: Whether to start a clean session
    

### Output Format

The Kamelet outputs MQTT message payload along with MQTT headers including topic, QoS level, and message properties.

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

### Example with QoS Configuration

```yaml
- route:
    from:
      uri: "kamelet:mqtt-source"
      parameters:
        topic: "critical/alerts"
        brokerUrl: "tcp://mqtt.example.com:1883"
        username: "mqttuser"
        password: "mqttpass"
        qualityOfService: "2"
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
        qualityOfService: "1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Quality of Service Levels

-   **QoS 0**: At most once delivery (fire and forget)
    
-   **QoS 1**: At least once delivery (acknowledged delivery)
    
-   **QoS 2**: Exactly once delivery (assured delivery)
    

Choose the appropriate QoS level based on your reliability requirements.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mqtt-source.kamelet.yaml)