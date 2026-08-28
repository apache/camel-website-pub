# ![jms apache artemis sink](_images/kamelets/jms-apache-artemis-sink.svg) JMS - Apache Artemis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an Apache Artemis message broker by using JMS.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The JMS URL. | string |  | tcp://my-host:61616 |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  | person |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-apache-artemis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.55.0
    

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
            uri: "kamelet:jms-apache-artemis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - Apache Artemis Sink Kamelet Description

### Connection Configuration

This Kamelet connects to an Apache Artemis message broker using JMS. Apache Artemis is a high-performance, scalable messaging broker that supports multiple messaging protocols.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### Apache Artemis Client

This sink uses the Apache Artemis Jakarta JMS client library to establish connections and send messages to the broker.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml)