# ![spring rabbitmq sink](_images/kamelets/spring-rabbitmq-sink.svg) RabbitMQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to a RabbitMQ Broker.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange name | **Required** The exchange name determines the exchange the queue is bound to. | string |  |  |
| **host** | Server Address | **Required** RabbitMQ broker address. | string |  | localhost |
| **port** | Server Port | **Required** RabbitMQ broker port. | integer |  | 5672 |
| **autoDeclareProducer** | Auto Declare Producer | Specifies whether the producer should auto declare binding between exchange, queue and routing key when starting. | boolean | false |  |
| **confirm** | Confirm | Controls whether to wait for publisher confirms. auto lets Camel detect whether the connection factory is configured for confirms, enabled always waits, disabled never waits. Requires publisherConfirmType to be SIMPLE or CORRELATED. Enum values: \* auto \* enabled \* disabled | string | auto |  |
| **confirmTimeout** | Confirm Timeout | How long in milliseconds to wait for a sent message to be confirmed by RabbitMQ when doing send-only (InOnly) messaging. A negative value waits indefinitely. | string | 5000 |  |
| **password** | Password | The password to access the RabbitMQ server. | string |  |  |
| **protocol** | Protocol | The AMQP protocol to use. Enum values: \* amqp \* amqps | string | amqp |  |
| **publisherConfirmType** | Publisher Confirm Type | The publisher confirm mode of the underlying connection factory. Must be SIMPLE or CORRELATED for the confirm option below to have anything to wait on. NONE, the default, leaves publisher confirms switched off. Enum values: \* NONE \* SIMPLE \* CORRELATED | string | NONE |  |
| **queues** | Queue name | The queue to receive messages from. | string |  |  |
| **routingKey** | Routing Key | The routing key to use when binding a consumer queue to the exchange. | string |  |  |
| **username** | Username | The username to access the RabbitMQ server. | string |  |  |
| **vhost** | Virtual Host | The virtual host. | string | / |  |

## Dependencies

At runtime, the `spring-rabbitmq-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:spring-rabbitmq-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Spring RabbitMQ Sink Kamelet Description

### RabbitMQ Integration with Spring

This Kamelet integrates with RabbitMQ using Spring’s RabbitMQ support, providing advanced messaging capabilities with Spring Framework integration.

### AMQP Protocol

RabbitMQ implements the Advanced Message Queuing Protocol (AMQP), providing:

-   Reliable message delivery
    
-   Message acknowledgments and confirmations
    
-   Dead letter queues for error handling
    
-   Message persistence and durability
    

### Exchange and Routing

Supports RabbitMQ’s flexible routing mechanisms:

-   Direct, topic, fanout, and headers exchanges
    
-   Routing keys for message targeting
    
-   Queue binding and routing patterns
    
-   Message filtering and transformation
    

### Spring Integration Benefits

Leverages Spring Framework features including:

-   Dependency injection and configuration
    
-   Transaction management
    
-   Error handling and retry mechanisms
    
-   Monitoring and management capabilities
    

### High Availability

RabbitMQ provides enterprise-grade features:

-   Clustering for high availability
    
-   Mirrored queues for redundancy
    
-   Federation for distributed messaging
    
-   Load balancing and failover
    

### Message Patterns

Supports various messaging patterns including publish-subscribe, request-reply, and message queuing for different application architectures.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml)