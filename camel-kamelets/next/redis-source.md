# ![redis source](_images/kamelets/redis-source.svg) Redis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages published on one or more Redis channels, one message per publication, as a subscriber of Redis publish and subscribe.

Use it to react to events that other applications publish on Redis, such as notifications, cache invalidations or status changes. To publish on a channel, use `redis-sink` with the `PUBLISH` command.

Output: the body is the published message, as text. The `CamelRedis.Channel` header is the channel it was published on.

Good to know: only the messages published while the integration runs are received; Redis does not keep them for later. It connects with no password and no TLS.

## Configuration Options

The following table summarizes the configuration options available for the `redis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channels** | Channels | **Required** The channels to listen to, separated by commas, or the channel patterns with `command` set to `PSUBSCRIBE`. | string | one | orders,alerts |
| **redisHost** | Redis Host | **Required** The host name or IP address of the Redis server. | string |  | redis.example.com |
| **redisPort** | Redis Port | **Required** The port of the Redis server, usually 6379. | integer |  | 6379 |
| **command** | Command | How to subscribe. `SUBSCRIBE` listens to the channels named in `channels`; `PSUBSCRIBE` treats them as patterns, such as `orders.*`, and listens to every channel that matches. | string | SUBSCRIBE | PSUBSCRIBE |
| **serializer** | Serializer | The full Java class name of the Spring Data Redis serializer that turns the bytes of each message into the body. The default gives text. | string | org.springframework.data.redis.serializer.StringRedisSerializer |  |

## Dependencies

At runtime, the `redis-source` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet connects to Redis without a password and without TLS. It has no option for authentication, so the Redis server must accept connections without a password.

### Configuration

The Redis Source Kamelet supports the following configurations:

-   **Redis Host**: The hostname or IP address of the Redis server (required)
    
-   **Redis Port**: The port number of the Redis server, usually 6379 (required)
    
-   **Channels**: Redis channels to subscribe to, separated by commas (required)
    
-   **Command**: `SUBSCRIBE` (the default) for channel names, or `PSUBSCRIBE` for channel patterns
    

### Output Format

The Kamelet outputs the messages received from the subscribed channels. The body is the message content, as text, and the `CamelRedis.Channel` header is the name of the channel.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        channels: "notifications"
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

### Example with a Channel Pattern

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        command: "PSUBSCRIBE"
        channels: "events.*"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Pub/Sub Pattern

This kamelet implements the Redis publish/subscribe pattern, allowing real-time message consumption from Redis channels. Multiple channels can be subscribed to simultaneously by providing a comma-separated list. Only the messages published while the integration runs are received.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/redis-source.kamelet.yaml)