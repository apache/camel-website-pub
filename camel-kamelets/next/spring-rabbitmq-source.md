# ![spring rabbitmq source](_images/kamelets/spring-rabbitmq-source.svg) RabbitMQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives each message from a queue in a RabbitMQ broker, and can create that queue and bind it to an exchange with a routing key.

Use it to process work or events that other applications publish to RabbitMQ. Use `spring-rabbitmq-sink` to publish them.

Output: the body is text when the content type of the message starts with `text`, and bytes otherwise. The headers of the RabbitMQ message become headers, along with `CamelSpringRabbitmqExchangeName`, `CamelSpringRabbitmqRoutingKey` and `CamelSpringRabbitmqContentType`.

Good to know: with `autoDeclare` false, the default, the queue must exist already, bound to the exchange; until it does, the source keeps trying again. With `autoDeclare` true, it creates the exchange as a `direct` exchange, the queue in `queues` and the binding with `routingKey`. Without `queues`, it reads from a new queue with a generated name. A message whose processing fails is tried 5 times, one second apart, and then dropped, or sent to the dead letter exchange of the queue when RabbitMQ has one. It connects with no TLS unless `protocol` is `amqps`.

## Configuration Options

The following table summarizes the configuration options available for the `spring-rabbitmq-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **exchangeName** | Exchange Name | **Required** The name of the exchange that the queue is bound to. | string |  | orders |
| **host** | Server Address | **Required** The host name or IP address of the RabbitMQ broker. | string |  | localhost |
| **port** | Server Port | **Required** The port of the RabbitMQ broker: usually 5672, or 5671 for `amqps`. | integer |  | 5672 |
| **autoDeclare** | Create Exchange and Queue | If true, the source creates the exchange (as a `direct` exchange) and the queue in `queues`, and binds them with `routingKey`, when it starts. If false, they must exist already. | boolean | false |  |
| **password** | Password | The password to log in to RabbitMQ with, for the user `username`. | string |  |  |
| **protocol** | Protocol | `amqp` for a plain connection, or `amqps` for a connection encrypted with TLS. Enum values: \* amqp \* amqps | string | amqp |  |
| **queues** | Queue Name | The queue to receive the messages from. When it is not set, a new queue with a generated name is used, which only makes sense with `autoDeclare` true. | string |  | orders |
| **routingKey** | Routing Key | The routing key that binds the queue to the exchange, when `autoDeclare` is true. A `direct` exchange then routes to the queue the messages sent with this key. | string |  | new-order |
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

With `autoDeclare` set to false (the default), the queue in `queues` must already exist and be bound to the exchange. With `autoDeclare` set to true, the Kamelet creates a `direct` exchange named `exchangeName`, the queue, and the binding with `routingKey` when it starts.

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