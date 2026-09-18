# ![jms amqp 10 source](_images/kamelets/jms-amqp-10-source.svg) JMS - AMQP 1.0 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume data from any AMQP 1.0 compliant message broker by using the Apache Qpid JMS client.

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **remoteURI** | Broker URL | **Required** The JMS URL. | string |  | amqp://my-host:31616 |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-amqp-10-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:amqp
    
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
      uri: "kamelet:jms-amqp-10-source"
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

## JMS AMQP 1.0 Source Kamelet Description

### Authentication methods

This Kamelet supports AMQP 1.0 authentication mechanisms including:

-   SASL authentication with username and password
    
-   Connection to AMQP 1.0 brokers
    

### Output format

The Kamelet consumes messages from JMS AMQP 1.0 queues and produces the message data in the configured format.

### Configuration

The Kamelet requires connection parameters for the AMQP 1.0 broker:

-   `remoteURI`: The AMQP broker URI
    
-   `username`: Username for authentication
    
-   `password`: Password for authentication
    
-   `destinationName`: The destination queue or topic name
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: jms-amqp-10-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: jms-amqp-10-source
    properties:
      remoteURI: "amqp://broker.example.com:5672"
      username: "{{username}}"
      password: "{{password}}"
      destinationName: "my-queue"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml)