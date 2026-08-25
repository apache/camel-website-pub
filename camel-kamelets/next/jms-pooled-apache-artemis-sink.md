# ![jms pooled apache artemis sink](_images/kamelets/jms-pooled-apache-artemis-sink.svg) JMS Pooled - Apache Artemis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an Apache Artemis message broker by using JMS Pooled.

## Configuration Options

The following table summarizes the configuration options available for the `jms-pooled-apache-artemis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The JMS URL. | string |  | tcp://my-host:61616 |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  | person |
| **connectionIdleTimeout** | Connection Idle Timeout | The maximum time a pooled Connection can sit unused before it is eligible for removal (in milliseconds). | integer | 30000 |  |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | The number of idle sessions allowed per connection before they are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Sessions Per Connection | The maximum number of pooled sessions per connection in the pool. | integer | 500 |  |
| **password** | Broker Password | The JMS Broker Password. | string |  |  |
| **username** | Broker Username | The JMS Broker Username. | string |  |  |

## Dependencies

At runtime, the `jms-pooled-apache-artemis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.55.0
    
-   mvn:org.messaginghub:pooled-jms:3.2.4
    

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
            uri: "kamelet:jms-pooled-apache-artemis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS Pooled - Apache Artemis Sink Kamelet Description

### Connection Configuration

This Kamelet connects to an Apache Artemis message broker using JMS with connection pooling for improved performance and resource management.

### Connection Pooling

The Kamelet uses pooled connections to optimize resource usage and performance. Key pooling configuration options include:

-   Maximum sessions per connection (default: 500)
    
-   Maximum idle sessions per connection (default: 500)
    
-   Connection idle timeout in milliseconds (default: 30000)
    

### Authentication

Optional authentication can be configured using username and password properties for secure broker connections.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-sink.kamelet.yaml)