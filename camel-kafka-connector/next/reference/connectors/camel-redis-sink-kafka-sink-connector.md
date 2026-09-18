# camel-redis-sink-kafka-connector sink configuration

Connector Description: Write object to a Redis cache.

When using camel-redis-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-redis-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.redissink.CamelRedissinkSinkConnector
```

The camel-redis-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.redis-sink.redisHost** | **Required** The host where Redis server is running. |  | HIGH |
| **camel.kamelet.redis-sink.redisPort** | **Required** The port where Redis server is running. |  | HIGH |
| **camel.kamelet.redis-sink.command** | **Required** Redis Command. | "GET" | HIGH |
| **camel.kamelet.redis-sink.channels** | Redis Channels. | "one" | MEDIUM |
| **camel.kamelet.redis-sink.serializer** | RedisSerializer fully qualified name implementation. | "org.springframework.data.redis.serializer.StringRedisSerializer" | MEDIUM |

The camel-redis-sink sink connector has no converters out of the box.

The camel-redis-sink sink connector has no transforms out of the box.

The camel-redis-sink sink connector has no aggregation strategies out of the box.