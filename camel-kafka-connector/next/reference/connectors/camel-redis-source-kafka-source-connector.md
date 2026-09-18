# camel-redis-source-kafka-connector source configuration

Connector Description: Get Events from a Redis cache.

When using camel-redis-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-redis-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.redissource.CamelRedissourceSourceConnector
```

The camel-redis-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.redis-source.redisHost** | **Required** The host where Redis server is running. |  | HIGH |
| **camel.kamelet.redis-source.redisPort** | **Required** The port where Redis server is running. |  | HIGH |
| **camel.kamelet.redis-source.command** | Redis Command. | "SUBSCRIBE" | MEDIUM |
| **camel.kamelet.redis-source.channels** | **Required** Redis Channels. | "one" | HIGH |
| **camel.kamelet.redis-source.serializer** | RedisSerializer fully qualified name implementation. | "org.springframework.data.redis.serializer.StringRedisSerializer" | MEDIUM |

The camel-redis-source source connector has no converters out of the box.

The camel-redis-source source connector has no transforms out of the box.

The camel-redis-source source connector has no aggregation strategies out of the box.