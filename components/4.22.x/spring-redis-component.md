# Spring Redis

**Since Camel 2.11**

**Both producer and consumer are supported**

This component allows sending and receiving messages from [Redis](https://redis.io/). Redis is an advanced key-value store where keys can contain strings, hashes, lists, sets and sorted sets. In addition, it provides pub/sub functionality for inter-app communications. Camel provides a producer for executing commands, consumer for subscribing to pub/sub messages an idempotent repository for filtering out duplicate messages.

> **Note**
> **Prerequisites**
>
> To use this component, you must have a Redis server running.

## URI Format

spring-redis://host:port\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Spring Redis component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **redisTemplate** (common) | **Autowired** Reference to a pre-configured RedisTemplate instance to use. |  | RedisTemplate |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring Redis endpoint is configured using URI syntax:

spring-redis:host:port

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** The host where Redis server is running. |  | String |
| **port** (common) | **Required** Redis server port number. |  | Integer |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channels** (common) | List of topic names or name patterns to subscribe to. Multiple names can be separated by comma. |  | String |
| **command** (common) | 
Default command, which can be overridden by message header. Notice the consumer only supports the following commands: PSUBSCRIBE and SUBSCRIBE.

Enum values:

-   PING
    
-   SET
    
-   GET
    
-   QUIT
    
-   EXISTS
    
-   DEL
    
-   TYPE
    
-   FLUSHDB
    
-   KEYS
    
-   RANDOMKEY
    
-   RENAME
    
-   RENAMENX
    
-   RENAMEX
    
-   DBSIZE
    
-   EXPIRE
    
-   EXPIREAT
    
-   TTL
    
-   SELECT
    
-   MOVE
    
-   FLUSHALL
    
-   GETSET
    
-   MGET
    
-   SETNX
    
-   SETEX
    
-   MSET
    
-   MSETNX
    
-   DECRBY
    
-   DECR
    
-   INCRBY
    
-   INCR
    
-   APPEND
    
-   SUBSTR
    
-   HSET
    
-   HGET
    
-   HSETNX
    
-   HMSET
    
-   HMGET
    
-   HINCRBY
    
-   HEXISTS
    
-   HDEL
    
-   HLEN
    
-   HKEYS
    
-   HVALS
    
-   HGETALL
    
-   RPUSH
    
-   LPUSH
    
-   LLEN
    
-   LRANGE
    
-   LTRIM
    
-   LINDEX
    
-   LSET
    
-   LREM
    
-   LPOP
    
-   RPOP
    
-   RPOPLPUSH
    
-   SADD
    
-   SMEMBERS
    
-   SREM
    
-   SPOP
    
-   SMOVE
    
-   SCARD
    
-   SISMEMBER
    
-   SINTER
    
-   SINTERSTORE
    
-   SUNION
    
-   SUNIONSTORE
    
-   SDIFF
    
-   SDIFFSTORE
    
-   SRANDMEMBER
    
-   ZADD
    
-   ZRANGE
    
-   ZREM
    
-   ZINCRBY
    
-   ZRANK
    
-   ZREVRANK
    
-   ZREVRANGE
    
-   ZCARD
    
-   ZSCORE
    
-   MULTI
    
-   DISCARD
    
-   EXEC
    
-   WATCH
    
-   UNWATCH
    
-   SORT
    
-   BLPOP
    
-   BRPOP
    
-   AUTH
    
-   SUBSCRIBE
    
-   PUBLISH
    
-   UNSUBSCRIBE
    
-   PSUBSCRIBE
    
-   PUNSUBSCRIBE
    
-   ZCOUNT
    
-   ZRANGEBYSCORE
    
-   ZREVRANGEBYSCORE
    
-   ZREMRANGEBYRANK
    
-   ZREMRANGEBYSCORE
    
-   ZUNIONSTORE
    
-   ZINTERSTORE
    
-   SAVE
    
-   BGSAVE
    
-   BGREWRITEAOF
    
-   LASTSAVE
    
-   SHUTDOWN
    
-   INFO
    
-   MONITOR
    
-   SLAVEOF
    
-   CONFIG
    
-   STRLEN
    
-   SYNC
    
-   LPUSHX
    
-   PERSIST
    
-   RPUSHX
    
-   ECHO
    
-   LINSERT
    
-   DEBUG
    
-   BRPOPLPUSH
    
-   SETBIT
    
-   GETBIT
    
-   SETRANGE
    
-   GETRANGE
    
-   PEXPIRE
    
-   PEXPIREAT
    
-   GEOADD
    
-   GEODIST
    
-   GEOHASH
    
-   GEOPOS
    
-   GEORADIUS
    
-   GEORADIUSBYMEMBER
    





 | SET | Command |
| **connectionFactory** (common) | Reference to a pre-configured RedisConnectionFactory instance to use. |  | RedisConnectionFactory |
| **redisTemplate** (common) | Reference to a pre-configured RedisTemplate instance to use. |  | RedisTemplate |
| **serializer** (common) | Reference to a pre-configured RedisSerializer instance to use. |  | RedisSerializer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **listenerContainer** (consumer (advanced)) | Reference to a pre-configured RedisMessageListenerContainer instance to use. |  | RedisMessageListenerContainer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied when the default JDK serializer deserializes Redis payloads, both on the consumer and on producer read commands. When not set, the JVM-wide jdk.serialFilter is used if present; otherwise a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. packages is applied. Ignored when a custom serializer is set. |  | String |

## Message Headers

The Spring Redis component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelRedis.Command** (producer) Constant: [`COMMAND`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#COMMAND) | The command to perform. |  | String |
| **CamelRedis.Key** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#KEY) | The key. |  | String |
| **CamelRedis.Keys** (common) Constant: [`KEYS`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#KEYS) | The keys. |  | Collection |
| **CamelRedis.Field** (common) Constant: [`FIELD`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#FIELD) | The field. |  | String |
| **CamelRedis.Fields** (common) Constant: [`FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#FIELDS) | The fields. |  | Collection |
| **CamelRedis.Value** (common) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#VALUE) | The value. |  | Object |
| **CamelRedis.Values** (common) Constant: [`VALUES`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#VALUES) | The values. |  | Map |
| **CamelRedis.Start** (common) Constant: [`START`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#START) | Start. |  | Long |
| **CamelRedis.End** (common) Constant: [`END`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#END) | End. |  | Long |
| **CamelRedis.Timeout** (common) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#TIMEOUT) | The timeout. |  | Long |
| **CamelRedis.Offset** (common) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#OFFSET) | The offset. |  | Long |
| **CamelRedis.Destination** (common) Constant: [`DESTINATION`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#DESTINATION) | The destination. |  | String |
| **CamelRedis.Channel** (common) Constant: [`CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#CHANNEL) | The channel. |  | byte\[\] or String |
| **CamelRedis.Message** (common) Constant: [`MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#MESSAGE) | The message. |  | Object |
| **CamelRedis.Index** (common) Constant: [`INDEX`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#INDEX) | The index. |  | Long |
| **CamelRedis.Position** (common) Constant: [`POSITION`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#POSITION) | The position. |  | String |
| **CamelRedis.Pivot** (common) Constant: [`PIVOT`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#PIVOT) | The pivot. |  | String |
| **CamelRedis.Count** (common) Constant: [`COUNT`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#COUNT) | Count. |  | Long |
| **CamelRedis.Timestamp** (common) Constant: [`TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#TIMESTAMP) | The timestamp. |  | Long |
| **CamelRedis.Pattern** (common) Constant: [`PATTERN`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#PATTERN) | The pattern. |  | byte\[\] or String |
| **CamelRedis.Db** (common) Constant: [`DB`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#DB) | The db. |  | Integer |
| **CamelRedis.Score** (common) Constant: [`SCORE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#SCORE) | The score. |  | Double |
| **CamelRedis.Min** (common) Constant: [`MIN`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#MIN) | The min. |  | Double |
| **CamelRedis.Max** (common) Constant: [`MAX`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#MAX) | The max. |  | Double |
| **CamelRedis.Increment** (common) Constant: [`INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#INCREMENT) | Increment. |  | Double |
| **CamelRedis.WithScore** (common) Constant: [`WITHSCORE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#WITHSCORE) | WithScore. |  | Boolean |
| **CamelRedis.Latitude** (common) Constant: [`LATITUDE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#LATITUDE) | Latitude. |  | Double |
| **CamelRedis.Longitude** (common) Constant: [`LONGITUDE`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#LONGITUDE) | Longitude. |  | Double |
| **CamelRedis.Radius** (common) Constant: [`RADIUS`](https://javadoc.io/doc/org.apache.camel/camel-spring-redis/latest/org/apache/camel/component/redis/RedisConstants.html#RADIUS) | Radius. |  | Double |

## Usage

See also the unit tests available at [https://github.com/apache/camel/tree/main/components/camel-spring-redis/src/test/java/org/apache/camel/component/redis](https://github.com/apache/camel/tree/main/components/camel-spring-redis/src/test/java/org/apache/camel/component/redis).

### Message headers evaluated by the Redis producer

The producer issues commands to the server, and each command has a different set of parameters with specific types. The result from the command execution is returned in the message body.

   
| Hash Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `HSET` | Set the string value of a hash field | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | void |
| `HGET` | Get the value of a hash field | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String) | String |
| `HSETNX` | Set the value of a hash field only if the field does not exist | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | void |
| `HMSET` | Set multiple hash fields to multiple values | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUES`/"CamelRedis.Values" (Map<String, Object>) | void |
| `HMGET` | Get the values of all the given hash fields | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELDS`/"CamelRedis.Fields" (Collection<String>) | Collection<Object> |
| `HINCRBY` | Increment the integer value of a hash field by the given number | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Long) | Long |
| `HEXISTS` | Determine if a hash field exists | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String) | Boolean |
| `HDEL` | Delete one or more hash fields | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.FIELD`/"CamelRedis.Field" (String) | void |
| `HLEN` | Get the number of fields in a hash | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `HKEYS` | Get all the fields in a hash | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Set<String> |
| `HVALS` | Get all the values in a hash | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Collection<Object> |
| `HGETALL` | Get all the fields and values in a hash | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Map<String, Object> |   
| List Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `RPUSH` | Append one or multiple values to a list | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `RPUSHX` | Append a value to a list only if the list exists | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `LPUSH` | Prepend one or multiple values to a list | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `LLEN` | Get the length of a list | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `LRANGE` | Get a range of elements from a list | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long) | List<Object> |
| `LTRIM` | Trim a list to the specified range | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long) | void |
| `LINDEX` | Get an element from a list by its index | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.INDEX`/"CamelRedis.Index" (Long) | String |
| `LINSERT` | Insert an element before or after another element in a list | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.PIVOT`/"CamelRedis.Pivot" (String), `RedisConstants.POSITION`/"CamelRedis.Position" (String) | Long |
| `LSET` | Set the value of an element in a list by its index | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.INDEX`/"CamelRedis.Index" (Long) | void |
| `LREM` | Remove elements from a list | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.COUNT`/"CamelRedis.Count" (Long) | Long |
| `LPOP` | Remove and get the first element in a list | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Object |
| `RPOP` | Remove and get the last element in a list | `RedisConstants.KEY`/"CamelRedis.Key" (String) | String |
| `RPOPLPUSH` | Remove the last element in a list, append it to another list and return it | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | Object |
| `BRPOPLPUSH` | Pop a value from a list, push it to another list and return it; or block until one is available | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long) | Object |
| `BLPOP` | Remove and get the first element in a list, or block until one is available | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long) | Object |
| `BRPOP` | Remove and get the last element in a list, or block until one is available | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long) | String |   
| Set Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `SADD` | Add one or more members to a set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Boolean |
| `SMEMBERS` | Get all the members in a set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Set<Object> |
| `SREM` | Remove one or more members from a set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Boolean |
| `SPOP` | Remove and return a random member from a set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | String |
| `SMOVE` | Move a member from one set to another | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | Boolean |
| `SCARD` | Get the number of members in a set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `SISMEMBER` | Determine if a given value is a member of a set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Boolean |
| `SINTER` | Intersect multiple sets | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String) | Set<Object> |
| `SINTERSTORE` | Intersect multiple sets and store the resulting set in a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | void |
| `SUNION` | Add multiple sets | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String) | Set<Object> |
| `SUNIONSTORE` | Add multiple sets and store the resulting set in a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | void |
| `SDIFF` | Subtract multiple sets | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String) | Set<Object> |
| `SDIFFSTORE` | Subtract multiple sets and store the resulting set in a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | void |
| `SRANDMEMBER` | Get one or multiple random members from a set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | String |   
| Ordered set Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `ZADD` | Add one or more members to a sorted set, or update its score if it already exists | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.SCORE`/"CamelRedis.Score" (Double) | Boolean |
| `ZRANGE` | Return a range of members in a sorted set, by index | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long), `RedisConstants.WITHSCORE`/"CamelRedis.WithScore" (Boolean) | Object |
| `ZREM` | Remove one or more members from a sorted set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Boolean |
| `ZINCRBY` | Increment the score of a member in a sorted set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.INCREMENT`/"CamelRedis.Increment" (Double) | Double |
| `ZRANK` | Determine the index of a member in a sorted set | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `ZREVRANK` | Determine the index of a member in a sorted set, with scores ordered from high to low | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `ZREVRANGE` | Return a range of members in a sorted set, by index, with scores ordered from high to low | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long), `RedisConstants.WITHSCORE`/"CamelRedis.WithScore" (Boolean) | Object |
| `ZCARD` | Get the number of members in a sorted set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `ZCOUNT` | Count the members in a sorted set with scores within the given values | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.MIN`/"CamelRedis.Min" (Double), `RedisConstants.MAX`/"CamelRedis.Max" (Double) | Long |
| `ZRANGEBYSCORE` | Return a range of members in a sorted set, by score | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.MIN`/"CamelRedis.Min" (Double), `RedisConstants.MAX`/"CamelRedis.Max" (Double) | Set<Object> |
| `ZREVRANGEBYSCORE` | Return a range of members in a sorted set, by score, with scores ordered from high to low | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.MIN`/"CamelRedis.Min" (Double), `RedisConstants.MAX`/"CamelRedis.Max" (Double) | Set<Object> |
| `ZREMRANGEBYRANK` | Remove all members in a sorted set within the given indexes | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long) | void |
| `ZREMRANGEBYSCORE` | Remove all members in a sorted set within the given scores | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long) | void |
| `ZUNIONSTORE` | Add multiple sorted sets and store the resulting-sorted set in a new key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | void |
| `ZINTERSTORE` | Intersect multiple sorted sets and store the resulting sorted set in a new key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.KEYS`/"CamelRedis.Keys" (String), `RedisConstants.DESTINATION`/"CamelRedis.Destination" (String) | void |   
| String Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `SET` | Set the string value of a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | void |
| `GET` | Get the value of a key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Object |
| `STRLEN` | Get the length of the value stored in a key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `APPEND` | Append a value to a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (String) | Integer |
| `SETBIT` | Sets or clears the bit at offset in the string value stored at key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.OFFSET`/"CamelRedis.Offset" (Long), `RedisConstants.VALUE`/"CamelRedis.Value" (Boolean) | void |
| `GETBIT` | Returns the bit value at offset in the string value stored at key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.OFFSET`/"CamelRedis.Offset" (Long) | Boolean |
| `SETRANGE` | Overwrite part of a string at key starting at the specified offset | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.OFFSET`/"CamelRedis.Offset" (Long) | void |
| `GETRANGE` | Get a substring of the string stored at a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.START`/"CamelRedis.Start"Long), `RedisConstants.END`/"CamelRedis.End" (Long) | String |
| `SETNX` | Set the value of a key only if the key does not exist | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Boolean |
| `SETEX` | Set the value and expiration of a key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long), SECONDS | void |
| `DECRBY` | Decrement the integer value of a key by the given number | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Long) | Long |
| `DECR` | Decrement the integer value of a key by one | `RedisConstants.KEY`/"CamelRedis.Key" (String), | Long |
| `INCRBY` | Increment the integer value of a key by the given amount | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Long) | Long |
| `INCR` | Increment the integer value of a key by one | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `MGET` | Get the values of all the given keys | `RedisConstants.FIELDS`/"CamelRedis.Fields" (Collection<String>) | List<Object> |
| `MSET` | Set multiple keys to multiple values | `RedisConstants.VALUES`/"CamelRedis.Values" (Map<String, Object>) | void |
| `MSETNX` | Set multiple keys to multiple values only if none of the keys exist | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | void |
| `GETSET` | Set the string value of a key and return its old value | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Object |   
| Key Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `EXISTS` | Determine if a key exists | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Boolean |
| `DEL` | Delete a key | `RedisConstants.KEYS`/"CamelRedis.Keys" (String) | void |
| `TYPE` | Determine the type stored at key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | DataType |
| `KEYS` | Find all keys matching the given pattern | `RedisConstants.PATERN`/"CamelRedis.Pattern" (String) | Collection<String> |
| `RANDOMKEY` | Return a random key from the keyspace | `RedisConstants.PATERN`/"CamelRedis.Pattern" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (String) | String |
| `RENAME` | Rename a key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | void |
| `RENAMENX` | Rename a key, only if the new key does not exist | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (String) | Boolean |
| `EXPIRE` | Set a key’s time to live in seconds | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long) | Boolean |
| `SORT` | Sort the elements in a list, set or sorted set | `RedisConstants.KEY`/"CamelRedis.Key" (String) | List<Object> |
| `PERSIST` | Remove the expiration from a key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Boolean |
| `EXPIREAT` | Set the expiration for a key as a UNIX timestamp | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMESTAMP`/"CamelRedis.Timestamp" (Long) | Boolean |
| `PEXPIRE` | Set a key’s time to live in milliseconds | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMEOUT`/"CamelRedis.Timeout" (Long) | Boolean |
| `PEXPIREAT` | Set the expiration for a key as a UNIX timestamp specified in milliseconds | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.TIMESTAMP`/"CamelRedis.Timestamp" (Long) | Boolean |
| `TTL` | Get the time to live for a key | `RedisConstants.KEY`/"CamelRedis.Key" (String) | Long |
| `MOVE` | Move a key to another database | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.DB`/"CamelRedis.Db" (Integer) | Boolean |   
| Geo Commands | Description | Parameters | Result |
| --- | --- | --- | --- |
| `GEOADD` | Adds the specified geospatial items (latitude, longitude, name) to the specified key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.LATITUDE`/"CamelRedis.Latitude" (Double), `RedisConstants.LONGITUDE`/"CamelRedis.Longitude" (Double), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | Long |
| `GEODIST` | Return the distance between two members in the geospatial index for the specified key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUES`/"CamelRedis.Values" (Object\[\]) | Distance |
| `GEOHASH` | Return valid Geohash strings representing the position of an element in the geospatial index for the specified key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | List<String> |
| `GEOPOS` | Return the positions (longitude, latitude) of an element in the geospatial index for the specified key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object) | List<Point> |
| `GEORADIUS` | Return the element in the geospatial index for the specified key which is within the borders of the area specified with the center location and the maximum distance from the center (the radius) | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.LATITUDE`/"CamelRedis.Latitude" (Double), `RedisConstants.LONGITUDE`/"CamelRedis.Longitude" (Double), `RedisConstants.RADIUS`/"CamelRedis.Radius" (Double), `RedisConstants.COUNT`/"CamelRedis.Count" (Integer) | GeoResults |
| `GEORADIUSBYMEMBER` | This command is exactly like GEORADIUS with the sole difference that instead of taking, as the center of the area to query, a longitude and latitude value, it takes the name of a member already existing inside the geospatial index for the specified key | `RedisConstants.KEY`/"CamelRedis.Key" (String), `RedisConstants.VALUE`/"CamelRedis.Value" (Object), `RedisConstants.RADIUS`/"CamelRedis.Radius" (Double), `RedisConstants.COUNT`/"CamelRedis.Count" (Integer) | GeoResults |   
| Other Command | Description | Parameters | Result |
| --- | --- | --- | --- |
| `MULTI` | Mark the start of a transaction block | none | void |
| `DISCARD` | Discard all commands issued after MULTI | none | void |
| `EXEC` | Execute all commands issued after MULTI | none | void |
| `WATCH` | Watch the given keys to determine execution of the MULTI/EXEC block | `RedisConstants.KEYS`/"CamelRedis.Keys" (String) | void |
| `UNWATCH` | Forget about all watched keys | none | void |
| `ECHO` | Echo the given string | `RedisConstants.VALUE`/"CamelRedis.Value" (String) | String |
| `PING` | Ping the server | none | String |
| `QUIT` | Close the connection | none | void |
| `PUBLISH` | Post a message to a channel | `RedisConstants.CHANNEL`/"CamelRedis.Channel" (String), `RedisConstants.MESSAGE`/"CamelRedis.Message" (Object) | void |

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-redis</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.