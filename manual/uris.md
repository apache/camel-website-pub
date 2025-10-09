# URIs

Camel makes extensive use of URIs to allow you to refer to [Endpoints](endpoint.md).

For example, consider the following URI:

```text
kafka:cheese?brokers=mykafka:1234&clientId=foo
```

This endpoint is created by the [Kafka](../components/4.18.x/kafka-component.md) component. The URI contains endpoint configurations as context-path and query parameters. In this example, the context-path is `cheese` which is the kafka topic to use.

The query parameters have two parameters:

1.  `brokers=mykafka:1234`: the remote Kafka broker to connect to.
    
2.  `clientId=foo`: the client id, which is a configuration of the Kafka component
    

## More Information

See also [Endpoints](endpoint.md)