# ![redis source](_images/kamelets/redis-source.svg) Redis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Get Events from a Redis cache.

## Configuration Options

The following table summarizes the configuration options available for the `redis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channels** | Channels | **Required** Redis Channels. | string | one |  |
| **redisHost** | Redis Host | **Required** The host where Redis server is running. | string |  |  |
| **redisPort** | Redis Port | **Required** The port where Redis server is running. | integer |  |  |
| **command** | Command | Redis Command. | string | SUBSCRIBE |  |
| **serializer** | Serializer | RedisSerializer fully qualified name implementation. | string | org.springframework.data.redis.serializer.StringRedisSerializer |  |

## Dependencies

At runtime, the `redis-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:redis-source"
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

## Redis Source Kamelet Description

### Authentication

This Kamelet supports Redis authentication using password-based authentication. The connection can be configured with or without authentication depending on your Redis setup.

### Configuration

The Redis Source Kamelet supports the following configurations:

-   **Redis Host**: The hostname or IP address of the Redis server (required)
    
-   **Redis Port**: The port number of the Redis server (default: 6379)
    
-   **Password**: Password for Redis authentication (optional)
    
-   **Channels**: Redis channels to subscribe to (required)
    
-   **Connection Timeout**: Connection timeout in milliseconds
    
-   **Database**: Redis database number to connect to
    

### Output Format

The Kamelet outputs Redis messages received from subscribed channels. Messages include both the channel name and message content.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        password: "redispass"
        channels: "notifications,alerts"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Multiple Channels

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        channels: "user-events,system-events,admin-events"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Database Selection

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        password: "redispass"
        database: "1"
        channels: "cache-invalidation"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Pub/Sub Pattern

This kamelet implements the Redis publish/subscribe pattern, allowing real-time message consumption from Redis channels. Multiple channels can be subscribed to simultaneously by providing a comma-separated list.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-source.kamelet.yaml)