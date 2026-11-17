# ![spring rabbitmq sink](_images/kamelets/spring-rabbitmq-sink.svg) RabbitMQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Publishes each message to an exchange in a RabbitMQ broker, which routes it to queues by its routing key.

Use it to hand work or events to applications that read from RabbitMQ queues. Use `spring-rabbitmq-source` to read from them.

Input: the body is the payload, as text or bytes. Text is sent with the content type `text/plain`, and bytes with `application/octet-stream`. A Map fails, and so does an empty body: turn structured data into JSON text first, for example with `json-serialize-action`. The headers of the message, except the Camel ones, are sent as headers of the RabbitMQ message.

Output: the message is unchanged.

Good to know: it does not create the exchange, unless `autoDeclareProducer` is true. A message sent to an exchange that does not exist is lost without an error, unless publisher confirms are on (`publisherConfirmType` and `confirm`), and RabbitMQ drops a message that no queue is bound to take. It connects with no TLS unless `protocol` is `amqps`. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange Name | **Required** The name of the exchange to publish the messages to. | string |  | orders |
| **host** | Server Address | **Required** The host name or IP address of the RabbitMQ broker. | string |  | localhost |
| **port** | Server Port | **Required** The port of the RabbitMQ broker: usually 5672, or 5671 for `amqps`. | integer |  | 5672 |
| **autoDeclareProducer** | Create Exchange and Queue | If true, the sink creates the exchange (as a `direct` exchange) and the queue in `queues`, and binds them with `routingKey`, before it sends the first message. | boolean | false |  |
| **confirm** | Confirm | Whether the sink waits for RabbitMQ to confirm each message: `enabled` always waits, `disabled` never waits, and `auto` waits when `publisherConfirmType` turns confirms on. A message that is not confirmed fails, such as one sent to an exchange that does not exist. Enum values: \* auto \* enabled \* disabled | string | auto |  |
| **confirmTimeout** | Confirm Timeout | How long to wait for RabbitMQ to confirm a message, in milliseconds. A negative value waits forever. | string | 5000 |  |
| **password** | Password | The password to log in to RabbitMQ with, for the user `username`. | string |  |  |
| **protocol** | Protocol | `amqp` for a plain connection, or `amqps` for a connection encrypted with TLS. Enum values: \* amqp \* amqps | string | amqp |  |
| **publisherConfirmType** | Publisher Confirm Type | Whether RabbitMQ confirms each message it takes: `NONE` turns confirms off, `SIMPLE` or `CORRELATED` turns them on. Use it with `confirm`. Enum values: \* NONE \* SIMPLE \* CORRELATED | string | NONE |  |
| **queues** | Queue Name | The queue to create and bind to the exchange with `routingKey` when `autoDeclareProducer` is true. Not used otherwise. | string |  | orders |
| **routingKey** | Routing Key | The routing key of each message, which the exchange uses to choose the queues that get it. With a `direct` exchange, a queue gets the message when it is bound with the same key. | string |  | new-order |
| **username** | Username | The user name to log in to RabbitMQ with. When it is not set, `guest` is used. | string |  |  |
| **vhost** | Virtual Host | The virtual host of the broker to connect to, which holds the exchanges and queues. RabbitMQ has the virtual host `/` from the start. | string | / |  |

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

Supports publish-subscribe and message queuing. It sends each message and does not wait for a reply.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml)