# IRC

**Since Camel 1.1**

**Both producer and consumer are supported**

The IRC component implements an [IRC](http://en.wikipedia.org/wiki/Internet_Relay_Chat) (Internet Relay Chat) transport.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-irc</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The IRC component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The IRC endpoint is configured using URI syntax:

irc:hostname:port

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (common) | **Required** Hostname for the IRC chat server. |  | String |
| **port** (common) | Port number for the IRC chat server. If no port is configured then a default port of either 6667, 6668 or 6669 is used. |  | int |

### Query Parameters (27 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoRejoin** (common) | Whether to auto re-join when being kicked. | true | boolean |
| **channels** (common) | Comma separated list of IRC channels. |  | String |
| **commandTimeout** (common) | Delay in milliseconds before sending commands after the connection is established. | 5000 | long |
| **keys** (common) | Comma separated list of keys for channels. |  | String |
| **namesOnJoin** (common) | Sends NAMES command to channel after joining it. onReply has to be true in order to process the result which will have the header value irc.num = '353'. | false | boolean |
| **nickname** (common) | The nickname used in chat. |  | String |
| **persistent** (common) | **Deprecated** Use persistent messages. | true | boolean |
| **realname** (common) | The IRC user’s actual name. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **colors** (advanced) | Whether or not the server supports color codes. | true | boolean |
| **onJoin** (filter) | Handle user join events. | true | boolean |
| **onKick** (filter) | Handle kick events. | true | boolean |
| **onMode** (filter) | Handle mode change events. | true | boolean |
| **onNick** (filter) | Handle nickname change events. | true | boolean |
| **onPart** (filter) | Handle user part events. | true | boolean |
| **onPrivmsg** (filter) | Handle private message events. | true | boolean |
| **onQuit** (filter) | Handle user quit events. | true | boolean |
| **onReply** (filter) | Whether or not to handle general responses to commands or informational messages. | false | boolean |
| **onTopic** (filter) | Handle topic change events. | true | boolean |
| **nickPassword** (security) | Your IRC server nickname password. |  | String |
| **password** (security) | The IRC server password. |  | String |
| **sslContextParameters** (security) | Used for configuring security using SSL. Reference to a org.apache.camel.support.jsse.SSLContextParameters in the Registry. This reference overrides any configured SSLContextParameters at the component level. Note that this setting overrides the trustManager option. |  | SSLContextParameters |
| **trustManager** (security) | The trust manager used to verify the SSL server’s certificate. |  | SSLTrustManager |
| **username** (security) | The IRC server user name. |  | String |

## Message Headers

The IRC component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **irc.messageType** (common) Constant: [`IRC_MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_MESSAGE_TYPE) | The type of message. |  | String |
| **irc.target** (common) Constant: [`IRC_TARGET`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_TARGET) | The target. |  | String |
| **irc.sendTo** (common) Constant: [`IRC_SEND_TO`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_SEND_TO) | The nickname or channel the message should be sent to. |  | String |
| **irc.user.kicked** (common) Constant: [`IRC_USER_KICKED`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_USER_KICKED) | The nickname of the user who is kicked from a channel (passive). |  | String |
| **irc.user.host** (common) Constant: [`IRC_USER_HOST`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_USER_HOST) | The host of the person who sent the line. |  | String |
| **irc.user.nick** (common) Constant: [`IRC_USER_NICK`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_USER_NICK) | The nickname of the person who sent the line or the server name of the server which sent the line. |  | String |
| **irc.user.servername** (common) Constant: [`IRC_USER_SERVERNAME`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_USER_SERVERNAME) | The server name of the server which sent the line or the nickname of the person who sent the line. |  | String |
| **irc.user.username** (common) Constant: [`IRC_USER_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_USER_USERNAME) | The username of the person who sent the line. |  | String |
| **irc.num** (common) Constant: [`IRC_NUM`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_NUM) | The numeric reply. |  | int |
| **irc.value** (common) Constant: [`IRC_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-irc/latest/org/apache/camel/component/irc/IrcConstants.html#IRC_VALUE) | The first part of the message. |  | String |

## Usage

### SSL Support

#### Using the JSSE Configuration Utility

The IRC component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component-specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the IRC component.

Programmatic configuration of the endpoint

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/users/home/server/truststore.jks");
ksp.setPassword("keystorePassword");

TrustManagersParameters tmp = new TrustManagersParameters();
tmp.setKeyStore(ksp);

SSLContextParameters scp = new SSLContextParameters();
scp.setTrustManagers(tmp);

Registry registry = ...
registry.bind("sslContextParameters", scp);

...

from(...)
    .to("ircs://camel-prd-user@server:6669/#camel-test?nickname=camel-prd&password=password&sslContextParameters=#sslContextParameters");
```

Spring DSL based configuration of endpoint

```xml
...
  <camel:sslContextParameters
      id="sslContextParameters">
    <camel:trustManagers>
      <camel:keyStore
          resource="/users/home/server/truststore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
  </camel:sslContextParameters>...
...
  <to uri="ircs://camel-prd-user@server:6669/#camel-test?nickname=camel-prd&password=password&sslContextParameters=#sslContextParameters"/>...
```

### Using the legacy basic configuration options

You can also connect to an SSL enabled IRC server, as follows:

```java
ircs:host[:port]/#room?username=user&password=pass
```

By default, the IRC transport uses [SSLDefaultTrustManager](http://moepii.sourceforge.net/irclib/javadoc/org/schwering/irc/lib/ssl/SSLDefaultTrustManager.md). If you need to provide your own custom trust manager, use the `trustManager` parameter as follows:

```java
ircs:host[:port]/#room?username=user&password=pass&trustManager=#referenceToMyTrustManagerBean
```

## Examples

### Using keys

Some IRC rooms require you to provide a key to be able to join that channel. The key is just a secret word.

For example, we join three channels whereas only channel 1 and 3 use a key.

```java
irc:nick@irc.server.org?channels=#chan1,#chan2,#chan3&keys=chan1Key,,chan3key
```

### Getting a list of channel users

Using the `namesOnJoin` option one can invoke the IRC-`NAMES` command after the component has joined a channel. The server will reply with `irc.num = 353`. So to process the result the property `onReply` has to be `true`. Furthermore, one has to filter the `onReply` exchanges to get the names.

For example, we want to get all exchanges that contain the usernames of the channel:

```java
from("ircs:nick@myserver:1234/#mychannelname?namesOnJoin=true&onReply=true")
	.choice()
		.when(header("irc.messageType").isEqualToIgnoreCase("REPLY"))
			.filter(header("irc.num").isEqualTo("353"))
			.to("mock:result").stop();
```

### Sending to a different channel or a person

If you need to send messages to a different channel (or a person) which is not defined on IRC endpoint, you can specify a different destination in a message header.

You can specify the destination in the following header:

  
| Header | Type | Description |
| --- | --- | --- |
| `irc.sendTo` | `String` | The channel (or the person) name. |

## Spring Boot Auto-Configuration

When using irc with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-irc-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.irc.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.irc.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.irc.enabled** | Whether to enable auto configuration of the irc component. This is enabled by default. |  | Boolean |
| **camel.component.irc.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.irc.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |