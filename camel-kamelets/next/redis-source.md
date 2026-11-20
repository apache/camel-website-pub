# ![redis source](_images/kamelets/redis-source.svg) Redis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages published on one or more Redis channels, one message per publication, as a subscriber of Redis publish and subscribe.

Use it to react to events that other applications publish on Redis, such as notifications, cache invalidations or status changes. To publish on a channel, use `redis-sink` with the `PUBLISH` command.

Output: the body is the published message, as text. The `CamelRedis.Channel` header is the channel it was published on, and the `CamelRedis.Pattern` header, as bytes, is the channel or pattern of `channels` that it matched.

Good to know: only the messages published while the integration runs are received; Redis does not keep them for later. By default it connects with no password and no TLS: set `password` (and `username` for an ACL user) for a Redis server that asks for a login, and `ssl` for one that needs TLS. The channels are shared by all the databases of a Redis server, so there is no database to choose.

## Configuration Options

The following table summarizes the configuration options available for the `redis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channels** | Channels | **Required** The channels to listen to, separated by commas, or the channel patterns with `command` set to `PSUBSCRIBE`. | string | one | orders,alerts |
| **redisHost** | Redis Host | **Required** The host name or IP address of the Redis server. | string |  | redis.example.com |
| **redisPort** | Redis Port | **Required** The port of the Redis server, usually 6379. | integer |  | 6379 |
| **command** | Command | How to subscribe. `SUBSCRIBE` listens to the channels named in `channels`; `PSUBSCRIBE` treats them as patterns, such as `orders.*`, and listens to every channel that matches. | string | SUBSCRIBE | PSUBSCRIBE |
| **password** | Password | The password to log in to Redis with, the one set with `requirepass` or the password of the user in `username`. Leave it empty for a Redis server that does not ask for a password. | string |  |  |
| **serializer** | Serializer | The full Java class name of the Spring Data Redis serializer that turns the bytes of each message into the body. The default gives text. | string | org.springframework.data.redis.serializer.StringRedisSerializer |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL), for a Redis server that offers TLS on `redisPort`. The certificate of the server is checked: it must be trusted by Java, as one from a public certificate authority is, and name `redisHost`. | boolean | false |  |
| **username** | Username | The Redis user to log in as, for a Redis server with access control lists (ACL, Redis 6 and later). Leave it empty to log in with `password` alone, as the `default` user. | string |  |  |

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

By default this Kamelet connects to Redis without a password and without TLS. For a Redis server that asks for a login, set `password`: the password set with `requirepass`, or, with `username`, the password of an ACL user. For a Redis server that needs TLS, set `ssl` to true; the certificate of the server must then be trusted by Java and name `redisHost`.

### Configuration

The Redis Source Kamelet supports the following configurations:

-   **Redis Host**: The hostname or IP address of the Redis server (required)
    
-   **Redis Port**: The port number of the Redis server, usually 6379 (required)
    
-   **Channels**: Redis channels to subscribe to, separated by commas (required)
    
-   **Command**: `SUBSCRIBE` (the default) for channel names, or `PSUBSCRIBE` for channel patterns
    
-   **Username** and **Password**: the login, for a Redis server that asks for one
    
-   **Use TLS**: whether to connect with TLS, false by default
    

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

### Example with a Password and TLS

```yaml
- route:
    from:
      uri: "kamelet:redis-source"
      parameters:
        redisHost: "redis.example.com"
        redisPort: "6379"
        password: "{{redis.password}}"
        ssl: true
        channels: "notifications"
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