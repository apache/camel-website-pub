# ![redis sink](_images/kamelets/redis-sink.svg) Redis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Write object to a Redis cache.

## Configuration Options

The following table summarizes the configuration options available for the `redis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **command** | Command | **Required** Redis Command. | string | GET |  |
| **redisHost** | Redis Host | **Required** The host where Redis server is running. | string |  |  |
| **redisPort** | Redis Port | **Required** The port where Redis server is running. | integer |  |  |
| **channels** | Channels | Redis Channels. | string | one |  |
| **serializer** | Serializer | RedisSerializer fully qualified name implementation. | string | org.springframework.data.redis.serializer.StringRedisSerializer |  |

## Dependencies

At runtime, the `redis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
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