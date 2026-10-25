# SSH

**Since Camel 2.10**

**Both producer and consumer are supported**

The SSH component enables access to SSH servers such that you can send an SSH command and process the response.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ssh</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ssh:\[username\[:password\]@\]host\[:port\]\[?options\]

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

The SSH component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **timeout** (common) | Sets the timeout in milliseconds to wait in establishing the remote SSH server connection: connecting, authenticating and opening the channel. It does not limit how long the command runs. Defaults to 30000 milliseconds. | 30000 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **pollCommand** (consumer) | Sets the command string to send to the remote SSH server during every poll cycle. Only works with camel-ssh component being used as a consumer, i.e. from(ssh://…​) You may need to end your command with a newline, and that must be URL encoded %0A. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **authTimeout** (advanced) | Sets the authentication timeout in milliseconds. |  | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **channelOpenTimeout** (advanced) | Sets the timeout in milliseconds for opening a channel. |  | long |
| **channelType** (advanced) | Sets the channel type to pass to the Channel as part of command execution. Defaults to exec. | exec | String |
| **clientBuilder** (advanced) | **Autowired** Instance of ClientBuilder used by the producer or consumer to create a new SshClient. |  | ClientBuilder |
| **compressions** (advanced) | Whether to use compression, and if so which. |  | String |
| **configuration** (advanced) | Component configuration. |  | SshConfiguration |
| **connectTimeout** (advanced) | Sets the socket connection timeout in milliseconds. |  | long |
| **heartbeatInterval** (advanced) | Sets the heartbeat interval in milliseconds. If positive, the component will send keep-alive messages to prevent the SSH session from timing out. |  | long |
| **heartbeatReplyMaxWait** (advanced) | Sets the maximum number of keep-alive messages without reply before the session is terminated. |  | int |
| **idleTimeout** (advanced) | Sets the timeout in milliseconds to wait before the SSH session is closed due to inactivity. The default value is 0, which means no idle timeout is applied. |  | long |
| **shellPrompt** (advanced) | Sets the shellPrompt to be dropped when response is read after command execution. Required when the channelType is shell. |  | String |
| **sleepForShellPrompt** (advanced) | Sets the sleep period in milliseconds to wait reading response from shell prompt. Defaults to 100 milliseconds. | 100 | long |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **certResource** (security) | Sets the resource path of the certificate to use for Authentication. Will use ResourceHelperKeyPairProvider to resolve file based certificate, and depends on keyType setting. |  | String |
| **certResourcePassword** (security) | Sets the password to use in loading certResource, if certResource is an encrypted key. |  | String |
| **ciphers** (security) | Comma-separated list of allowed/supported ciphers in their order of preference. |  | String |
| **failOnUnknownHost** (security) | Specifies whether a connection to a server whose host has no entry without a marker in the known\_hosts resource should fail. When false, such a server is accepted. A server whose host has entries without a marker is always rejected when it presents a key that none of them lists, and a key listed in a matching revoked entry is always rejected. | false | boolean |
| **kex** (security) | Comma-separated list of allowed/supported key exchange algorithms in their order of preference. |  | String |
| **keyPairProvider** (security) | Sets the KeyPairProvider reference to use when connecting using Certificates to the remote SSH Server. |  | KeyPairProvider |
| **keyType** (security) | Sets the key type to pass to the KeyPairProvider as part of authentication. KeyPairProvider.loadKey(…​) will be passed this value. From Camel 3.0.0 / 2.25.0, by default Camel will select the first available KeyPair that is loaded. Prior to this, a KeyType of 'ssh-rsa' was enforced by default. |  | String |
| **knownHostsResource** (security) | Sets the resource path for a known\_hosts file used to verify the SSH server host key. The file uses the OpenSSH known\_hosts format, and its entries are matched against the host and port configured on the endpoint. A resource that cannot be read, or that has a line that cannot be read, makes every connection fail. When not set, the client does not verify the server host key against a known\_hosts file. |  | String |
| **macs** (security) | Comma-separated list of allowed/supported message authentication code algorithms in their order of preference. The MAC algorithm is used for data integrity protection. |  | String |
| **password** (security) | Sets the password to use in connecting to remote SSH server. Requires keyPairProvider to be set to null. |  | String |
| **signatures** (security) | Comma-separated list of allowed/supported signature algorithms in their order of preference. |  | String |
| **username** (security) | Sets the username to use in logging into the remote SSH server. |  | String |

## Endpoint Options

The SSH endpoint is configured using URI syntax:

ssh:host:port

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Sets the hostname of the remote SSH server. |  | String |
| **port** (common) | Sets the port number for the remote SSH server. | 22 | int |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **timeout** (common) | Sets the timeout in milliseconds to wait in establishing the remote SSH server connection: connecting, authenticating and opening the channel. It does not limit how long the command runs. Defaults to 30000 milliseconds. | 30000 | long |
| **pollCommand** (consumer) | Sets the command string to send to the remote SSH server during every poll cycle. Only works with camel-ssh component being used as a consumer, i.e. from(ssh://…​) You may need to end your command with a newline, and that must be URL encoded %0A. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **authTimeout** (advanced) | Sets the authentication timeout in milliseconds. |  | long |
| **channelOpenTimeout** (advanced) | Sets the timeout in milliseconds for opening a channel. |  | long |
| **channelType** (advanced) | Sets the channel type to pass to the Channel as part of command execution. Defaults to exec. | exec | String |
| **clientBuilder** (advanced) | **Autowired** Instance of ClientBuilder used by the producer or consumer to create a new SshClient. |  | ClientBuilder |
| **compressions** (advanced) | Whether to use compression, and if so which. |  | String |
| **connectTimeout** (advanced) | Sets the socket connection timeout in milliseconds. |  | long |
| **heartbeatInterval** (advanced) | Sets the heartbeat interval in milliseconds. If positive, the component will send keep-alive messages to prevent the SSH session from timing out. |  | long |
| **heartbeatReplyMaxWait** (advanced) | Sets the maximum number of keep-alive messages without reply before the session is terminated. |  | int |
| **idleTimeout** (advanced) | Sets the timeout in milliseconds to wait before the SSH session is closed due to inactivity. The default value is 0, which means no idle timeout is applied. |  | long |
| **shellPrompt** (advanced) | Sets the shellPrompt to be dropped when response is read after command execution. Required when the channelType is shell. |  | String |
| **sleepForShellPrompt** (advanced) | Sets the sleep period in milliseconds to wait reading response from shell prompt. Defaults to 100 milliseconds. | 100 | long |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **certResource** (security) | Sets the resource path of the certificate to use for Authentication. Will use ResourceHelperKeyPairProvider to resolve file based certificate, and depends on keyType setting. |  | String |
| **certResourcePassword** (security) | Sets the password to use in loading certResource, if certResource is an encrypted key. |  | String |
| **ciphers** (security) | Comma-separated list of allowed/supported ciphers in their order of preference. |  | String |
| **failOnUnknownHost** (security) | Specifies whether a connection to a server whose host has no entry without a marker in the known\_hosts resource should fail. When false, such a server is accepted. A server whose host has entries without a marker is always rejected when it presents a key that none of them lists, and a key listed in a matching revoked entry is always rejected. | false | boolean |
| **kex** (security) | Comma-separated list of allowed/supported key exchange algorithms in their order of preference. |  | String |
| **keyPairProvider** (security) | Sets the KeyPairProvider reference to use when connecting using Certificates to the remote SSH Server. |  | KeyPairProvider |
| **keyType** (security) | Sets the key type to pass to the KeyPairProvider as part of authentication. KeyPairProvider.loadKey(…​) will be passed this value. From Camel 3.0.0 / 2.25.0, by default Camel will select the first available KeyPair that is loaded. Prior to this, a KeyType of 'ssh-rsa' was enforced by default. |  | String |
| **knownHostsResource** (security) | Sets the resource path for a known\_hosts file used to verify the SSH server host key. The file uses the OpenSSH known\_hosts format, and its entries are matched against the host and port configured on the endpoint. A resource that cannot be read, or that has a line that cannot be read, makes every connection fail. When not set, the client does not verify the server host key against a known\_hosts file. |  | String |
| **macs** (security) | Comma-separated list of allowed/supported message authentication code algorithms in their order of preference. The MAC algorithm is used for data integrity protection. |  | String |
| **password** (security) | Sets the password to use in connecting to remote SSH server. Requires keyPairProvider to be set to null. |  | String |
| **signatures** (security) | Comma-separated list of allowed/supported signature algorithms in their order of preference. |  | String |
| **username** (security) | Sets the username to use in logging into the remote SSH server. |  | String |

## Message Headers

The SSH component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSshUsername** (common) Constant: [`USERNAME_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#USERNAME_HEADER) | The user name. |  | String |
| **CamelSshPassword** (common) Constant: [`PASSWORD_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#PASSWORD_HEADER) | The password. |  | String |
| **CamelSshStderr** (common) Constant: [`STDERR`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#STDERR) | The value of this header is a InputStream with the standard error stream of the executable. |  | InputStream |
| **CamelSshExitValue** (common) Constant: [`EXIT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#EXIT_VALUE) | The value of this header is the exit value that is returned, after the execution. By convention a non-zero status exit value indicates abnormal termination. Note that the exit value is OS dependent. |  | Integer |

## Message Body

The message body at each side of the SSH component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `stream` | The standard output of the pollCommand as a stream, with the exit value and the standard error in the CamelSshExitValue and CamelSshStderr headers. |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The command to run, as text: bytes, a stream or a file are read as text. A Map or a POJO is sent as its toString(): build the command as text first. No body fails. |
| **Producer output** | `stream` | The standard output of the command as a stream, with the exit value and the standard error in the CamelSshExitValue and CamelSshStderr headers; an exit value that is not 0 does not fail the exchange. Convert it to text to read it more than once. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

### Usage as a Producer endpoint

When the SSH Component is used as a Producer (`.to("ssh://…​")`), it will send the message body as the command to execute on the remote SSH server.

After the call, the message body is the standard output of the command as a stream, with the exit value in the `CamelSshExitValue` header and the standard error, as a stream as well, in the `CamelSshStderr` header. An exit value that is not 0 does not fail the exchange. The polling consumer gives the output of its `pollCommand` the same way.

Here is an example of this. Note that the command has a newline (`&#10;`).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:exampleSshProducer")
    .setBody(constant("features:list\n"))
    .to("ssh://user:pass@localhost:8101")
    .log("${body}");
```

```xml
<route id="camel-example-ssh-producer">
  <from uri="direct:exampleSshProducer"/>
  <setBody>
    <constant>features:list&#10;</constant>
  </setBody>
  <to uri="ssh://user:pass@localhost:8101"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    id: camel-example-ssh-producer
    from:
      uri: direct:exampleSshProducer
      steps:
        - setBody:
            expression:
              constant:
                expression: "features:list\n"
        - to:
            uri: ssh://user:pass@localhost:8101
        - log:
            message: "${body}"
```

The `timeout` option covers connecting to the server, authenticating and opening the channel, not the run of the command. The producer waits until the command ends, with no time limit, so a command that does not end blocks the thread that sends the message.

With `channelType=shell`, the `shellPrompt` option is required, and the endpoint fails to start without it. The producer reads the output of the shell until it ends with the `shellPrompt` text, and checks the output every `sleepForShellPrompt` milliseconds (100 by default).

### Authentication

The SSH Component can authenticate against the remote SSH server using one of two mechanisms: Public Key certificate or username/password. Configuring how the SSH Component does authentication is based on how and which options are set.

1.  First, it will look to see if the `certResource` option has been set, and if so, use it to locate the referenced Public Key certificate and use that for authentication.
    
2.  If `certResource` is not set, it will look to see if a `keyPairProvider` has been set, and if so, it will use that for certificate-based authentication.
    
3.  If neither `certResource` nor `keyPairProvider` are set, it will use the `username` and `password` options for authentication. Even though the `username` and `password` are provided in the endpoint configuration and headers set with `CamelSshUsername` and `CamelSshPassword`, the endpoint configuration is surpassed and credentials set in the headers are used.
    

The following route fragment shows an SSH polling consumer using a certificate from the classpath.

-   Java
    
-   XML
    
-   YAML
    

```java
from("ssh://scott@localhost:8101?certResource=classpath:test_rsa&useFixedDelay=true&delay=5000&pollCommand=features:list%0A")
    .log("${body}");
```

```xml
<route>
  <from uri="ssh://scott@localhost:8101?certResource=classpath:test_rsa&amp;useFixedDelay=true&amp;delay=5000&amp;pollCommand=features:list%0A"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: ssh://scott@localhost:8101
      parameters:
        certResource: "classpath:test_rsa"
        useFixedDelay: true
        delay: 5000
        pollCommand: "features:list%0A"
      steps:
        - log:
            message: "${body}"
```

An example of using Public Key authentication is provided in `examples/camel-example-ssh-security`.

### Server host key verification

The SSH Component verifies the host key of the SSH server only when the `knownHostsResource` option is set. It refers to a file in the OpenSSH `known_hosts` format, such as the output of `ssh-keyscan`. Set `failOnUnknownHost` to `true` as well, so that a server without any entry in that file is rejected. When it is `false` (the default), such a server is accepted and a warning is logged.

The entries are matched as OpenSSH matches them:

-   Each host pattern of an entry is compared, ignoring case, with the host name or address the client connects to: the host configured on the endpoint, or the `HostName` that `~/.ssh/config` gives for it. It is written `host` for port 22 and `[host]:port` for another port. **and `?` are wildcards, a pattern starting with `!` excludes the hosts it matches, and hashed entries are supported. So `db.example.com` only applies to port 22, `[db.example.com]:2222` to port 2222, and** to every host and port. The host is never resolved: an endpoint configured with an address only uses the entries for that address, and an IPv6 address such as `::1` is not expanded.
    
-   The server is accepted when an entry of its host lists the key it presents. A host can be listed with several keys, one per line.
    
-   The server is rejected when the key it presents is listed in a matching `@revoked` entry, or when its host has entries without a marker but none of them lists that key, whatever the value of `failOnUnknownHost`. That option only decides for a host without such an entry: `@revoked` and `@cert-authority` entries do not list a host.
    
-   `@cert-authority` entries (OpenSSH host certificates) are not supported and are ignored.
    
-   A `known_hosts` resource that cannot be read, or that has a line that cannot be read (for example an unknown `@` marker, a missing key, or a key that is not valid base64), makes every connection fail.
    

The following route verifies the host key of a server listening on port 2222 against a `known_hosts` file that contains the line `[db.example.com]:2222 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5…​`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:status")
    .to("ssh://scott@db.example.com:2222?certResource=classpath:test_rsa&knownHostsResource=file:/etc/camel/known_hosts&failOnUnknownHost=true");
```

```xml
<route>
  <from uri="direct:status"/>
  <to uri="ssh://scott@db.example.com:2222?certResource=classpath:test_rsa&amp;knownHostsResource=file:/etc/camel/known_hosts&amp;failOnUnknownHost=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:status
      steps:
        - to:
            uri: ssh://scott@db.example.com:2222
            parameters:
              certResource: "classpath:test_rsa"
              knownHostsResource: "file:/etc/camel/known_hosts"
              failOnUnknownHost: true
```

### Certificate Dependencies

You will need to add some additional runtime dependencies if you use certificate-based authentication. You may need to use later versions depending on what version of Camel you are using.

The component uses `sshd-core` library which is based on either `bouncycastle` or `eddsa` security providers. `camel-ssh` is picking explicitly `bouncycastle` as security provider.

```xml
<dependency>
  <groupId>org.apache.sshd</groupId>
  <artifactId>sshd-core</artifactId>
  <version>2.8.0</version>
</dependency>
<dependency>
  <groupId>org.bouncycastle</groupId>
  <artifactId>bcpg-jdk18on</artifactId>
  <version>1.71</version>
</dependency>
<dependency>
  <groupId>org.bouncycastle</groupId>
  <artifactId>bcpkix-jdk18on</artifactId>
  <version>1.71</version>
</dependency>
```