# ![spring rabbitmq source](_images/kamelets/spring-rabbitmq-source.svg) RabbitMQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from a RabbitMQ Broker.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange name | **Required** The exchange name determines the exchange the queue is bound to. | string |  |  |
| **host** | Server Address | **Required** RabbitMQ broker address. | string |  | localhost |
| **port** | Server Port | **Required** RabbitMQ broker port. | integer |  | 5672 |
| **autoDeclare** | Auto Declare | The routing key to use when binding a consumer queue to the exchange. | boolean | false |  |
| **password** | Password | The password to access the RabbitMQ server. | string |  |  |
| **protocol** | Protocol | The AMQP protocol to use. Enum values: \* amqp \* amqps | string | amqp |  |
| **queues** | Queue name | The queue to receive messages from. | string |  |  |
| **routingKey** | Routing Key | The routing key to use when binding a consumer queue to the exchange. | string |  |  |
| **username** | Username | The username to access the RabbitMQ server. | string |  |  |
| **vhost** | Virtual Host | The virtual host. | string | / |  |

## Dependencies

At runtime, the `spring-rabbitmq-source` Kamelet relies upon the presence of the following dependencies:

-   camel:spring-rabbitmq
    
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
      uri: "kamelet:spring-rabbitmq-source"
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

## Spring Rabbitmq Source Kamelet Description

### Authentication methods

This Kamelet connects to Spring Rabbitmq using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Spring Rabbitmq and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Spring Rabbitmq:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: spring-rabbitmq-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: spring-rabbitmq-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-source.kamelet.yaml)