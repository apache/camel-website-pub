# ![spring rabbitmq sink](_images/kamelets/spring-rabbitmq-sink.svg) RabbitMQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Publishes each message to an exchange in a RabbitMQ broker, which routes it to queues by its routing key.

Use it to hand work or events to applications that read from RabbitMQ queues. Use `spring-rabbitmq-source` to read from them.

Input: the body is the payload, as text or bytes. Text is sent with the content type `text/plain`, and bytes with `application/octet-stream`, unless `contentType` says otherwise. A Map fails: turn structured data into JSON text first, for example with `json-serialize-action`, and set `contentType` to `application/json`. A message with no body fails, unless `allowNullBody` is true. The headers of the message, except the Camel ones, are sent as headers of the RabbitMQ message.

Output: the message is unchanged.

Good to know: it does not create the exchange, unless `autoDeclareProducer` is true. A message sent to an exchange that does not exist is lost without an error, unless publisher confirms are on (`publisherConfirmType` and `confirm`), and RabbitMQ drops a message that no queue is bound to take. It connects with no TLS unless `protocol` is `amqps`. With `amqps`, the certificate of the broker must be trusted by Java, or by the trust store in `sslTruststoreLocation`, and must name the host in `host`; otherwise it cannot connect. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does. Headers that start with `CamelSpringRabbitmq` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange Name | **Required** The name of the exchange to publish the messages to. | string |  | orders |
| **host** | Server Address | **Required** The host name or IP address of the RabbitMQ broker. | string |  | localhost |
| **port** | Server Port | **Required** The port of the RabbitMQ broker: usually 5672, or 5671 for `amqps`. | integer |  | 5672 |
| **allowNullBody** | Allow Null Body | If true, a message with no body is sent as an empty RabbitMQ message, with the content type `application/octet-stream`, or the one in `contentType`. When it is not set, a message with no body fails. | boolean |  |  |
| **autoDeclareProducer** | Create Exchange and Queue | If true, the sink creates the exchange (as a `direct` exchange) and the queue in `queues`, and binds them with `routingKey`, before it sends the first message. | boolean | false |  |
| **confirm** | Confirm | Whether the sink waits for RabbitMQ to confirm each message: `enabled` always waits, `disabled` never waits, and `auto` waits when `publisherConfirmType` turns confirms on. A message that is not confirmed fails, such as one sent to an exchange that does not exist. Enum values: \* auto \* enabled \* disabled | string | auto |  |
| **confirmTimeout** | Confirm Timeout | How long to wait for RabbitMQ to confirm a message, in milliseconds. A negative value waits forever. | string | 5000 |  |
| **contentType** | Content Type | The content type to send every message with, such as `application/json` or `application/json; charset=utf-8`, so that the applications that read it know its format. When it is not set, text is sent as `text/plain`, and bytes as `application/octet-stream`. | string |  | application/json |
| **password** | Password | The password to log in to RabbitMQ with, for the user `username`. | string |  |  |
| **protocol** | Protocol | `amqp` for a plain connection, or `amqps` for a connection encrypted with TLS, which checks the certificate of the broker and its host name. Enum values: \* amqp \* amqps | string | amqp |  |
| **publisherConfirmType** | Publisher Confirm Type | Whether RabbitMQ confirms each message it takes: `NONE` turns confirms off, `SIMPLE` or `CORRELATED` turns them on. Use it with `confirm`. Enum values: \* NONE \* SIMPLE \* CORRELATED | string | NONE |  |
| **queues** | Queue Name | The queue to create and bind to the exchange with `routingKey` when `autoDeclareProducer` is true. Not used otherwise. | string |  | orders |
| **routingKey** | Routing Key | The routing key of each message, which the exchange uses to choose the queues that get it. With a `direct` exchange, a queue gets the message when it is bound with the same key. | string |  | new-order |
| **sslTruststoreLocation** | SSL Truststore Location | The location of a trust store, in JKS or PKCS12 format, with the certificate of the authority that signed the certificate of the broker, such as `file:/etc/rabbitmq/truststore.p12`, or `classpath:truststore.p12` for one on the classpath. A path without `file:` is looked up on the classpath. Needed only with `amqps` when the broker uses a certificate that Java does not trust by default, such as one from a private or self-signed authority. Not used with `amqp`. | string |  | file:/etc/rabbitmq/truststore.p12 |
| **sslTruststorePassword** | SSL Truststore Password | The password of the trust store in `sslTruststoreLocation`. | string |  |  |
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

### Content type

Text is sent with the content type `text/plain`, and bytes with `application/octet-stream`. Set `contentType` to send every message with another content type, such as `application/json`, so that the applications that read the queue know the format. A message with no body fails, unless `allowNullBody` is true: then it is sent as an empty message.

### Usage example

The following route publishes the JSON that is posted to `/orders` to the exchange `orders`, with the routing key `new-order` and the content type `application/json`:

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      parameters:
        subpath: "orders"
      steps:
        - to:
            uri: "kamelet:spring-rabbitmq-sink"
            parameters:
              host: "localhost"
              port: 5672
              exchangeName: "orders"
              routingKey: "new-order"
              contentType: "application/json"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-sink.kamelet.yaml)