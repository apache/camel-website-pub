# ![spring rabbitmq source](_images/kamelets/spring-rabbitmq-source.svg) RabbitMQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives each message from a queue in a RabbitMQ broker, and can create that queue and bind it to an exchange with a routing key.

Use it to process work or events that other applications publish to RabbitMQ. Use `spring-rabbitmq-sink` to publish them.

Output: the body is text when the content type of the message starts with `text`, and bytes otherwise. The headers of the RabbitMQ message become headers, along with `CamelSpringRabbitmqExchangeName`, `CamelSpringRabbitmqRoutingKey` and `CamelSpringRabbitmqContentType`.

Good to know: with `autoDeclare` false, the default, the queue must exist already, bound to the exchange; until it does, the source keeps trying again. With `autoDeclare` true, it creates the exchange, as a `direct` exchange unless `exchangeType` says otherwise, the queue in `queues` and the binding with `routingKey`; when the exchange or the queue exists already with other settings, such as another type or another dead letter exchange, the source fails to start. Without `queues`, it reads from a new queue with a generated name. A message whose processing fails is tried 6 times, one second apart (see `maximumRetryAttempts` and `retryDelay`), and then dropped, or sent to the dead letter exchange of the queue when it has one, such as the one in `deadLetterExchange`. One consumer processes one message at a time; `concurrentConsumers` processes several in parallel, so not in order. It connects with no TLS unless `protocol` is `amqps`. With `amqps`, the certificate of the broker must be trusted by Java, or by the trust store in `sslTruststoreLocation`, and must name the host in `host`; otherwise it cannot connect.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange Name | **Required** The name of the exchange that the queue is bound to. | string |  | orders |
| **host** | Server Address | **Required** The host name or IP address of the RabbitMQ broker. | string |  | localhost |
| **port** | Server Port | **Required** The port of the RabbitMQ broker: usually 5672, or 5671 for `amqps`. | integer |  | 5672 |
| **acknowledgeMode** | Acknowledge Mode | When RabbitMQ removes a message from the queue: with `AUTO`, once it has been processed, or has failed after the retries; with `NONE`, as soon as it is delivered, so a message whose processing fails is lost and does not go to the dead letter exchange. When it is not set, `AUTO` is used. Enum values: \* AUTO \* NONE | string |  |  |
| **autoDeclare** | Create Exchange and Queue | If true, the source creates the exchange (as a `direct` exchange) and the queue in `queues`, and binds them with `routingKey`, when it starts. If false, they must exist already. | boolean | false |  |
| **concurrentConsumers** | Concurrent Consumers | How many consumers receive from the queue at the same time, each on its own channel, so that as many messages are processed in parallel. When it is not set, there is one consumer, and the messages are processed one at a time. | integer |  | 4 |
| **deadLetterExchange** | Dead Letter Exchange | The exchange that RabbitMQ sends a message to when its processing still fails after the retries. The source creates this exchange, and creates the queue in `queues` with it as its dead letter exchange. Needs `autoDeclare` true; with `autoDeclare` false, it is not used, and the dead letter exchange must be set on the queue in RabbitMQ, for example with a policy. | string |  | orders.dlx |
| **deadLetterExchangeType** | Dead Letter Exchange Type | The type of the exchange that the source creates in `deadLetterExchange`: `direct`, `fanout`, `headers` or `topic`. When it is not set, it is `direct`. Enum values: \* direct \* fanout \* headers \* topic | string |  |  |
| **deadLetterQueue** | Dead Letter Queue | A queue that the source creates and binds to `deadLetterExchange` with `deadLetterRoutingKey`, to keep the failed messages. Needs `deadLetterExchange`, `deadLetterRoutingKey` and `autoDeclare` true; without `deadLetterRoutingKey`, the source fails to start. | string |  | orders.dlq |
| **deadLetterRoutingKey** | Dead Letter Routing Key | The routing key that a failed message is sent to `deadLetterExchange` with, and that binds `deadLetterQueue` to it. When it is not set, a failed message keeps the routing key it was published with. Needs `deadLetterExchange` and `autoDeclare` true. | string |  | failed |
| **exchangeType** | Exchange Type | The type of the exchange that the source creates when `autoDeclare` is true: `direct`, `fanout`, `headers` or `topic`. When it is not set, it is `direct`. With `topic`, `routingKey` can be a pattern: `orders.*` matches `orders.new`, and `orders.#` also matches `orders.eu.new`. Not used when `autoDeclare` is false. Enum values: \* direct \* fanout \* headers \* topic | string |  |  |
| **maximumRetryAttempts** | Maximum Retry Attempts | How many times a message whose processing fails is tried again, after the first try. When it is not set, it is tried again 5 times, so 6 times in all. With 0, it is not tried again. | integer |  | 3 |
| **password** | Password | The password to log in to RabbitMQ with, for the user `username`. | string |  |  |
| **prefetchCount** | Prefetch Count | How many messages RabbitMQ sends ahead to each consumer, before they are acknowledged. When it is not set, it is 250. | integer |  | 10 |
| **protocol** | Protocol | `amqp` for a plain connection, or `amqps` for a connection encrypted with TLS, which checks the certificate of the broker and its host name. Enum values: \* amqp \* amqps | string | amqp |  |
| **queues** | Queue Name | The queue to receive the messages from. When it is not set, a new queue with a generated name is used, which only makes sense with `autoDeclare` true. | string |  | orders |
| **retryDelay** | Retry Delay | How long to wait before a failing message is tried again, in milliseconds. When it is not set, it waits 1000 milliseconds. | integer |  | 5000 |
| **routingKey** | Routing Key | The routing key that binds the queue to the exchange, when `autoDeclare` is true. A `direct` exchange then routes to the queue the messages sent with this key. | string |  | new-order |
| **sslTruststoreLocation** | SSL Truststore Location | The location of a trust store, in JKS or PKCS12 format, with the certificate of the authority that signed the certificate of the broker, such as `file:/etc/rabbitmq/truststore.p12`, or `classpath:truststore.p12` for one on the classpath. A path without `file:` is looked up on the classpath. Needed only with `amqps` when the broker uses a certificate that Java does not trust by default, such as one from a private or self-signed authority. Not used with `amqp`. | string |  | file:/etc/rabbitmq/truststore.p12 |
| **sslTruststorePassword** | SSL Truststore Password | The password of the trust store in `sslTruststoreLocation`. | string |  |  |
| **username** | Username | The user name to log in to RabbitMQ with. When it is not set, `guest` is used. | string |  |  |
| **vhost** | Virtual Host | The virtual host of the broker to connect to, which holds the exchanges and queues. RabbitMQ has the virtual host `/` from the start. | string | / |  |

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

## Spring RabbitMQ Source Kamelet Description

### Authentication methods

The Kamelet logs in to RabbitMQ with `username` and `password`; when they are not set, it uses `guest`. Set `protocol` to `amqps` for a connection with TLS.

### Output format

The body is text when the content type of the message starts with `text`, and bytes otherwise; it is not turned into JSON. The headers of the RabbitMQ message become headers.

### Queues, exchanges and bindings

With `autoDeclare` set to false (the default), the queue in `queues` must already exist and be bound to the exchange. With `autoDeclare` set to true, the Kamelet creates the exchange named `exchangeName`, the queue, and the binding with `routingKey` when it starts. The exchange is a `direct` exchange unless `exchangeType` is `fanout`, `headers` or `topic`. With `topic`, `routingKey` is a pattern: `orders.*` matches `orders.new` but not `orders.eu.new`, and `orders.#` matches both. When the exchange or the queue already exists with other settings, such as another type or another dead letter exchange, the Kamelet fails to start.

### Parallel processing

One consumer processes one message at a time. With `concurrentConsumers`, that many consumers receive from the queue, each on its own channel, and process messages in parallel, so not in order. `prefetchCount` is how many messages RabbitMQ sends ahead to each consumer before they are acknowledged (250 when it is not set). Both show in the RabbitMQ management UI, on the consumers of the queue.

With `acknowledgeMode` set to `NONE`, RabbitMQ removes each message from the queue as soon as it is delivered: a message whose processing fails is then lost, and does not go to the dead letter exchange.

### Retries and dead letters

When the processing of a message fails, the Kamelet tries it again `maximumRetryAttempts` times (5 when it is not set), `retryDelay` milliseconds apart (1000 when it is not set). When it still fails, RabbitMQ drops it, or sends it to the dead letter exchange of the queue.

With `autoDeclare` set to true, the Kamelet can set up the dead letter exchange too: it creates the exchange in `deadLetterExchange` (of type `deadLetterExchangeType`, `direct` when it is not set), creates the queue in `queues` with it as its dead letter exchange and `deadLetterRoutingKey` as its dead letter routing key, and creates the queue in `deadLetterQueue` bound to the exchange with that key. `deadLetterQueue` needs `deadLetterRoutingKey`. With `autoDeclare` false, these options are not used: set the dead letter exchange on the queue in RabbitMQ instead, for example with a policy.

The following route tries a failing message 3 times in all, 2 seconds apart, and then moves it to the queue `orders.dlq`. The message there has an `x-death` header that says which queue it failed in.

```yaml
- route:
    from:
      uri: "kamelet:spring-rabbitmq-source"
      parameters:
        host: "localhost"
        port: 5672
        exchangeName: "orders"
        queues: "orders"
        routingKey: "new-order"
        autoDeclare: true
        concurrentConsumers: 4
        prefetchCount: 10
        maximumRetryAttempts: 2
        retryDelay: 2000
        deadLetterExchange: "orders.dlx"
        deadLetterRoutingKey: "failed"
        deadLetterQueue: "orders.dlq"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:spring-rabbitmq-source"
      parameters:
        host: "localhost"
        port: 5672
        username: "guest"
        password: "guest"
        exchangeName: "orders"
        queues: "orders"
        routingKey: "new-order"
        autoDeclare: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/spring-rabbitmq-source.kamelet.yaml)