# ![jms pooled apache artemis source](_images/kamelets/jms-pooled-apache-artemis-source.svg) JMS Pooled - Apache Artemis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an Apache Artemis message broker by using JMS Pooled Connection.

## Configuration Options

The following table summarizes the configuration options available for the `jms-pooled-apache-artemis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The JMS URL. | string |  | tcp://my-host:61616 |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **connectionIdleTimeout** | Connection Idle Timeout | The maximum time a pooled Connection can sit unused before it is eligible for removal (in milliseconds). | integer | 30000 |  |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | The number of idle sessions allowed per connection before they are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Session Per Connection | The maximum number of pooled sessions per connection in the pool. | integer | 500 |  |
| **password** | Broker Password | The JMS Broker Password. | string |  |  |
| **username** | Broker Username | The JMS Broker Username. | string |  |  |

## Dependencies

At runtime, the `jms-pooled-apache-artemis-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.54.0
    
-   mvn:org.messaginghub:pooled-jms:3.2.2
    

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
      uri: "kamelet:jms-pooled-apache-artemis-source"
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

## JMS Pooled Apache Artemis Source Kamelet Description

### Authentication methods

This Kamelet connects to Apache Artemis JMS broker using:

-   Broker URL and connection credentials
    
-   Pooled connection factory for better performance
    
-   Username and password authentication
    

### Output format

The Kamelet consumes messages from Apache Artemis JMS queues and produces the message data in the configured format.

### Configuration

The Kamelet requires Apache Artemis connection parameters:

-   `brokerURL`: The Apache Artemis broker URL
    
-   `destinationName`: The destination queue or topic name
    
-   `username`: Username for authentication
    
-   `password`: Password for authentication
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: jms-pooled-apache-artemis-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: jms-pooled-apache-artemis-source
    properties:
      brokerURL: "tcp://artemis-broker:61616"
      destinationName: "my-queue"
      username: "{{username}}"
      password: "{{password}}"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-source.kamelet.yaml)