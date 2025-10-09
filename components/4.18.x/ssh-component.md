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

The SSH component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **failOnUnknownHost** (common) | Specifies whether a connection to an unknown host should fail or not. This value is only checked when the property knownHosts is set. | false | boolean |
| **knownHostsResource** (common) | Sets the resource path for a known\_hosts file. |  | String |
| **timeout** (common) | Sets the timeout in milliseconds to wait in establishing the remote SSH server connection. Defaults to 30000 milliseconds. | 30000 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **pollCommand** (consumer) | Sets the command string to send to the remote SSH server during every poll cycle. Only works with camel-ssh component being used as a consumer, i.e. from(ssh://…​) You may need to end your command with a newline, and that must be URL encoded %0A. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **channelType** (advanced) | Sets the channel type to pass to the Channel as part of command execution. Defaults to exec. | exec | String |
| **clientBuilder** (advanced) | **Autowired** Instance of ClientBuilder used by the producer or consumer to create a new SshClient. |  | ClientBuilder |
| **compressions** (advanced) | Whether to use compression, and if so which. |  | String |
| **configuration** (advanced) | Component configuration. |  | SshConfiguration |
| **idleTimeout** (advanced) | Sets the timeout in milliseconds to wait before the SSH session is closed due to inactivity. The default value is 0, which means no idle timeout is applied. |  | long |
| **shellPrompt** (advanced) | Sets the shellPrompt to be dropped when response is read after command execution. |  | String |
| **sleepForShellPrompt** (advanced) | Sets the sleep period in milliseconds to wait reading response from shell prompt. Defaults to 100 milliseconds. | 100 | long |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **certResource** (security) | Sets the resource path of the certificate to use for Authentication. Will use ResourceHelperKeyPairProvider to resolve file based certificate, and depends on keyType setting. |  | String |
| **certResourcePassword** (security) | Sets the password to use in loading certResource, if certResource is an encrypted key. |  | String |
| **ciphers** (security) | Comma-separated list of allowed/supported ciphers in their order of preference. |  | String |
| **kex** (security) | Comma-separated list of allowed/supported key exchange algorithms in their order of preference. |  | String |
| **keyPairProvider** (security) | Sets the KeyPairProvider reference to use when connecting using Certificates to the remote SSH Server. |  | KeyPairProvider |
| **keyType** (security) | Sets the key type to pass to the KeyPairProvider as part of authentication. KeyPairProvider.loadKey(…​) will be passed this value. From Camel 3.0.0 / 2.25.0, by default Camel will select the first available KeyPair that is loaded. Prior to this, a KeyType of 'ssh-rsa' was enforced by default. |  | String |
| **macs** (security) | Comma-separated list of allowed/supported message authentication code algorithms in their order of preference. The MAC algorithm is used for data integrity protection. |  | String |
| **password** (security) | Sets the password to use in connecting to remote SSH server. Requires keyPairProvider to be set to null. |  | String |
| **signatures** (security) | Comma-separated list of allowed/supported signature algorithms in their order of preference. |  | String |
| **username** (security) | Sets the username to use in logging into the remote SSH server. |  | String |

## Endpoint Options

The SSH endpoint is configured using URI syntax:

ssh:host:port

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Sets the hostname of the remote SSH server. |  | String |
| **port** (common) | Sets the port number for the remote SSH server. | 22 | int |

### Query Parameters (40 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **failOnUnknownHost** (common) | Specifies whether a connection to an unknown host should fail or not. This value is only checked when the property knownHosts is set. | false | boolean |
| **knownHostsResource** (common) | Sets the resource path for a known\_hosts file. |  | String |
| **timeout** (common) | Sets the timeout in milliseconds to wait in establishing the remote SSH server connection. Defaults to 30000 milliseconds. | 30000 | long |
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
| **channelType** (advanced) | Sets the channel type to pass to the Channel as part of command execution. Defaults to exec. | exec | String |
| **clientBuilder** (advanced) | **Autowired** Instance of ClientBuilder used by the producer or consumer to create a new SshClient. |  | ClientBuilder |
| **compressions** (advanced) | Whether to use compression, and if so which. |  | String |
| **idleTimeout** (advanced) | Sets the timeout in milliseconds to wait before the SSH session is closed due to inactivity. The default value is 0, which means no idle timeout is applied. |  | long |
| **shellPrompt** (advanced) | Sets the shellPrompt to be dropped when response is read after command execution. |  | String |
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
| **kex** (security) | Comma-separated list of allowed/supported key exchange algorithms in their order of preference. |  | String |
| **keyPairProvider** (security) | Sets the KeyPairProvider reference to use when connecting using Certificates to the remote SSH Server. |  | KeyPairProvider |
| **keyType** (security) | Sets the key type to pass to the KeyPairProvider as part of authentication. KeyPairProvider.loadKey(…​) will be passed this value. From Camel 3.0.0 / 2.25.0, by default Camel will select the first available KeyPair that is loaded. Prior to this, a KeyType of 'ssh-rsa' was enforced by default. |  | String |
| **macs** (security) | Comma-separated list of allowed/supported message authentication code algorithms in their order of preference. The MAC algorithm is used for data integrity protection. |  | String |
| **password** (security) | Sets the password to use in connecting to remote SSH server. Requires keyPairProvider to be set to null. |  | String |
| **signatures** (security) | Comma-separated list of allowed/supported signature algorithms in their order of preference. |  | String |
| **username** (security) | Sets the username to use in logging into the remote SSH server. |  | String |

## Message Headers

The SSH component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSshUsername** (common) Constant: [`USERNAME_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#USERNAME_HEADER) | The user name. |  | String |
| **CamelSshPassword** (common) Constant: [`PASSWORD_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#PASSWORD_HEADER) | The password. |  | String |
| **CamelSshStderr** (common) Constant: [`STDERR`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#STDERR) | The value of this header is a InputStream with the standard error stream of the executable. |  | InputStream |
| **CamelSshExitValue** (common) Constant: [`EXIT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-ssh/latest/org/apache/camel/component/ssh/SshConstants.html#EXIT_VALUE) | The value of this header is the exit value that is returned, after the execution. By convention a non-zero status exit value indicates abnormal termination. Note that the exit value is OS dependent. |  | Integer |

## Usage

### Usage as a Producer endpoint

When the SSH Component is used as a Producer (`.to("ssh://…​")`), it will send the message body as the command to execute on the remote SSH server.

Here is an example of this within the XML DSL. Note that the command has an XML encoded newline (`&#10;`).

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

### Authentication

The SSH Component can authenticate against the remote SSH server using one of two mechanisms: Public Key certificate or username/password. Configuring how the SSH Component does authentication is based on how and which options are set.

1.  First, it will look to see if the `certResource` option has been set, and if so, use it to locate the referenced Public Key certificate and use that for authentication.
    
2.  If `certResource` is not set, it will look to see if a `keyPairProvider` has been set, and if so, it will use that for certificate-based authentication.
    
3.  If neither `certResource` nor `keyPairProvider` are set, it will use the `username` and `password` options for authentication. Even though the `username` and `password` are provided in the endpoint configuration and headers set with `SshConstants.USERNAME_HEADER` (`CamelSshUsername`) and `SshConstants.PASSWORD_HEADER` (`CamelSshPassword`), the endpoint configuration is surpassed and credentials set in the headers are used.
    

The following route fragment shows an SSH polling consumer using a certificate from the classpath.

In the XML DSL,

```xml
<route>
  <from uri="ssh://scott@localhost:8101?certResource=classpath:test_rsa&amp;useFixedDelay=true&amp;delay=5000&amp;pollCommand=features:list%0A"/>
  <log message="${body}"/>
</route>
```

In the Java DSL,

```java
from("ssh://scott@localhost:8101?certResource=classpath:test_rsa&useFixedDelay=true&delay=5000&pollCommand=features:list%0A")
    .log("${body}");
```

An example of using Public Key authentication is provided in `examples/camel-example-ssh-security`.

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

## Spring Boot Auto-Configuration

When using ssh with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ssh-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 27 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ssh.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ssh.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ssh.cert-resource** | Sets the resource path of the certificate to use for Authentication. Will use ResourceHelperKeyPairProvider to resolve file based certificate, and depends on keyType setting. |  | String |
| **camel.component.ssh.cert-resource-password** | Sets the password to use in loading certResource, if certResource is an encrypted key. |  | String |
| **camel.component.ssh.channel-type** | Sets the channel type to pass to the Channel as part of command execution. Defaults to exec. | exec | String |
| **camel.component.ssh.ciphers** | Comma-separated list of allowed/supported ciphers in their order of preference. |  | String |
| **camel.component.ssh.client-builder** | Instance of ClientBuilder used by the producer or consumer to create a new SshClient. The option is a org.apache.sshd.client.ClientBuilder type. |  | ClientBuilder |
| **camel.component.ssh.compressions** | Whether to use compression, and if so which. |  | String |
| **camel.component.ssh.configuration** | Component configuration. The option is a org.apache.camel.component.ssh.SshConfiguration type. |  | SshConfiguration |
| **camel.component.ssh.enabled** | Whether to enable auto configuration of the ssh component. This is enabled by default. |  | Boolean |
| **camel.component.ssh.fail-on-unknown-host** | Specifies whether a connection to an unknown host should fail or not. This value is only checked when the property knownHosts is set. | false | Boolean |
| **camel.component.ssh.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.ssh.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.ssh.idle-timeout** | Sets the timeout in milliseconds to wait before the SSH session is closed due to inactivity. The default value is 0, which means no idle timeout is applied. |  | Long |
| **camel.component.ssh.kex** | Comma-separated list of allowed/supported key exchange algorithms in their order of preference. |  | String |
| **camel.component.ssh.key-pair-provider** | Sets the KeyPairProvider reference to use when connecting using Certificates to the remote SSH Server. The option is a org.apache.sshd.common.keyprovider.KeyPairProvider type. |  | KeyPairProvider |
| **camel.component.ssh.key-type** | Sets the key type to pass to the KeyPairProvider as part of authentication. KeyPairProvider.loadKey(…​) will be passed this value. From Camel 3.0.0 / 2.25.0, by default Camel will select the first available KeyPair that is loaded. Prior to this, a KeyType of 'ssh-rsa' was enforced by default. |  | String |
| **camel.component.ssh.known-hosts-resource** | Sets the resource path for a known\_hosts file. |  | String |
| **camel.component.ssh.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ssh.macs** | Comma-separated list of allowed/supported message authentication code algorithms in their order of preference. The MAC algorithm is used for data integrity protection. |  | String |
| **camel.component.ssh.password** | Sets the password to use in connecting to remote SSH server. Requires keyPairProvider to be set to null. |  | String |
| **camel.component.ssh.poll-command** | Sets the command string to send to the remote SSH server during every poll cycle. Only works with camel-ssh component being used as a consumer, i.e. from(ssh://…​) You may need to end your command with a newline, and that must be URL encoded %0A. |  | String |
| **camel.component.ssh.shell-prompt** | Sets the shellPrompt to be dropped when response is read after command execution. |  | String |
| **camel.component.ssh.signatures** | Comma-separated list of allowed/supported signature algorithms in their order of preference. |  | String |
| **camel.component.ssh.sleep-for-shell-prompt** | Sets the sleep period in milliseconds to wait reading response from shell prompt. Defaults to 100 milliseconds. | 100 | Long |
| **camel.component.ssh.timeout** | Sets the timeout in milliseconds to wait in establishing the remote SSH server connection. Defaults to 30000 milliseconds. | 30000 | Long |
| **camel.component.ssh.username** | Sets the username to use in logging into the remote SSH server. |  | String |