# ![redis sink](_images/kamelets/redis-sink.svg) Redis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a Redis command for each message, such as storing the body under a key with `SET`, adding it to a list with `RPUSH`, or publishing it on a channel with `PUBLISH`.

Use it to put values in a Redis cache for other applications to read, to push work items onto a Redis list, or to publish events on a Redis channel that `redis-source` or other subscribers listen to.

Input: the body is the value, as text. The `key` header (or `ce-key`) gives the key, for commands that work on a key such as `SET`, `GET` or `RPUSH`. The `channel` header (or `ce-channel`) gives the channel for `PUBLISH`; without it, the channel in `channels` is used.

Output: when it is used inside a route, the body afterwards is what Redis answered, such as the value for `GET` or the new length of the list for `RPUSH`; for `SET` the body is unchanged.

Good to know: the default `command` is `GET`, which reads and stores nothing, so set it to the command you need. A body that is not text, such as a Map, fails the message; turn it into JSON text first, for example with `json-serialize-action`. It connects with no password and no TLS.

## Configuration Options

The following table summarizes the configuration options available for the `redis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **command** | Command | **Required** The Redis command to run for each message, such as `SET` to store the body under the key, `RPUSH` or `LPUSH` to add it to a list, `SADD` to add it to a set, or `PUBLISH` to send it on a channel. | string | GET | SET |
| **redisHost** | Redis Host | **Required** The host name or IP address of the Redis server. | string |  | redis.example.com |
| **redisPort** | Redis Port | **Required** The port of the Redis server, usually 6379. | integer |  | 6379 |
| **channels** | Channels | The channel that `PUBLISH` sends to when the message has no `channel` or `ce-channel` header. | string | one |  |
| **serializer** | Serializer | The full Java class name of the Spring Data Redis serializer that turns the values and keys into the bytes Redis stores. The default stores them as text. | string | org.springframework.data.redis.serializer.StringRedisSerializer |  |

## Dependencies

At runtime, the `redis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:spring-redis
    

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
            uri: "kamelet:redis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Redis Sink Kamelet Description

### In-Memory Data Store

This Kamelet integrates with Redis, an open-source, in-memory data structure store used as a database, cache, and message broker. Redis provides high performance and low latency data operations.

### Data Structures

Redis supports various data structures including:

-   Strings and binary-safe strings
    
-   Lists, sets, and sorted sets
    
-   Hashes and bitmaps
    
-   HyperLogLogs and streams
    

### Caching and Session Storage

Commonly used for caching frequently accessed data and session storage in web applications, providing fast data retrieval and improved application performance.

### Persistence Options

Redis offers configurable persistence options including:

-   RDB snapshots for point-in-time backups
    
-   AOF (Append Only File) for durability
    
-   Hybrid persistence combining both approaches
    

### High Availability

Supports Redis Sentinel for high availability and Redis Cluster for horizontal scaling and automatic failover capabilities.

### Use Cases

Ideal for scenarios requiring:

-   Fast data access and caching
    
-   Real-time analytics and counters
    
-   Session management
    
-   Pub/sub messaging patterns
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-sink.kamelet.yaml)