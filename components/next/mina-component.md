# Mina

**Since Camel 2.10**

**Both producer and consumer are supported**

The Mina component is a transport mechanism for working with [Apache MINA 2.x](http://mina.apache.org/)

> **Tip**
> Favor using [Netty](netty-component.md) as Netty is a much more active maintained and popular project than Apache Mina currently is.

> **Warning**
> Be careful with `sync=false` on consumer endpoints. In camel-mina, all consumer exchanges are `InOut`. This is different to camel-mina.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mina</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

mina:tcp://hostname\[:port\]\[?options\]
mina:udp://hostname\[:port\]\[?options\]
mina:vm://hostname\[:port\]\[?options\]

You can specify a codec in the Registry using the **codec** option. If you are using TCP and no codec is specified then the `textline` flag is used to determine if text-line-based codec or object serialization should be used instead. By default, the object serialization is used.

For UDP if no codec is specified the default uses a basic `ByteBuffer` based codec.

The VM protocol is used as a direct forwarding mechanism in the same JVM.

A Mina producer has a default timeout value of 30 seconds, while it waits for a response from the remote server.

In normal use, `camel-mina` only supports marshalling the body content—message headers and exchange properties are not sent.  
However, the option, **transferExchange**, does allow you to transfer the exchange itself over the wire. See options below.

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

The Mina component supports 28 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disconnect** (common) | Whether to disconnect(close) from Mina session right after use. Can be used for both consumer and producer. | false | boolean |
| **minaLogger** (common) | You can enable the Apache MINA logging filter. Apache MINA uses slf4j logging at INFO level to log all input and output. | false | boolean |
| **sync** (common) | Setting to set endpoint as one-way or request-response. | true | boolean |
| **timeout** (common) | You can configure the timeout that specifies how long to wait for a response from a remote server. The timeout unit is in milliseconds, so 60000 is 60 seconds. | 30000 | long |
| **writeTimeout** (common) | Maximum amount of time it should take to send data to the MINA session. Default is 10000 milliseconds. | 10000 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientMode** (consumer) | If the clientMode is true, mina consumer will connect the address as a TCP client. | false | boolean |
| **noReplyLogLevel** (consumer (advanced)) | 
If sync is enabled this option dictates MinaConsumer which logging level to use when logging a there is no reply to send back.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cachedAddress** (producer (advanced)) | Whether to create the InetAddress once and reuse. Setting this to false allows to pickup DNS changes in the network. | true | boolean |
| **lazySessionCreation** (producer (advanced)) | Sessions can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use the shared mina configuration. |  | MinaConfiguration |
| **disconnectOnNoReply** (advanced) | If sync is enabled then this option dictates MinaConsumer if it should disconnect where there is no reply to send back. | true | boolean |
| **maximumPoolSize** (advanced) | Number of worker threads in the worker pool for TCP and UDP. | 16 | int |
| **orderedThreadPoolExecutor** (advanced) | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | boolean |
| **transferExchange** (advanced) | **Deprecated** Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. Also make sure to configure objectCodecPattern to (star) to allow transferring java objects. | false | boolean |
| **allowDefaultCodec** (codec) | The mina component installs a default codec if both, codec is null and textline is false. Setting allowDefaultCodec to false prevents the mina component from installing a default codec as the first element in the filter chain. This is useful in scenarios where another filter must be the first in the filter chain, like the SSL filter. | true | boolean |
| **codec** (codec) | To use a custom minda codec implementation. |  | ProtocolCodecFactory |
| **decoderMaxLineLength** (codec) | To set the textline protocol decoder max line length. By default the default value of Mina itself is used which are 1024. | 1024 | int |
| **encoderMaxLineLength** (codec) | To set the textline protocol encoder max line length. By default the default value of Mina itself is used which are Integer.MAX\_VALUE. | \-1 | int |
| **encoding** (codec) | You can configure the encoding (a charset name) to use for the TCP textline codec and the UDP protocol. If not provided, Camel will use the JVM default Charset. |  | String |
| **filters** (codec) | You can set a list of Mina IoFilters to use. |  | List |
| **objectCodecPattern** (codec) | Accept the wildcard specified classes for Object deserialization, unless they are otherwise rejected. Multiple patterns can be separated by comma. |  | String |
| **textline** (codec) | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP. | false | boolean |
| **textlineDelimiter** (codec) | 

Only used for TCP and if textline=true. Sets the text line delimiter to use. If none provided, Camel will use DEFAULT. This delimiter is used to mark the end of text.

Enum values:

-   DEFAULT
    
-   AUTO
    
-   UNIX
    
-   WINDOWS
    
-   MAC
    





 |  | MinaTextLineDelimiter |
| **sslContextParameters** (security) | To configure SSL security. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Mina endpoint is configured using URI syntax:

mina:protocol:host:port

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | **Required** Protocol to use. |  | String |
| **host** (common) | **Required** Hostname to use. Use localhost or 0.0.0.0 for local server as consumer. For producer use the hostname or ip address of the remote server. |  | String |
| **port** (common) | **Required** Port number. |  | int |

### Query Parameters (27 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disconnect** (common) | Whether to disconnect(close) from Mina session right after use. Can be used for both consumer and producer. | false | boolean |
| **minaLogger** (common) | You can enable the Apache MINA logging filter. Apache MINA uses slf4j logging at INFO level to log all input and output. | false | boolean |
| **sync** (common) | Setting to set endpoint as one-way or request-response. | true | boolean |
| **timeout** (common) | You can configure the timeout that specifies how long to wait for a response from a remote server. The timeout unit is in milliseconds, so 60000 is 60 seconds. | 30000 | long |
| **writeTimeout** (common) | Maximum amount of time it should take to send data to the MINA session. Default is 10000 milliseconds. | 10000 | long |
| **clientMode** (consumer) | If the clientMode is true, mina consumer will connect the address as a TCP client. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **noReplyLogLevel** (consumer (advanced)) | 

If sync is enabled this option dictates MinaConsumer which logging level to use when logging a there is no reply to send back.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **cachedAddress** (producer (advanced)) | Whether to create the InetAddress once and reuse. Setting this to false allows to pickup DNS changes in the network. | true | boolean |
| **lazySessionCreation** (producer (advanced)) | Sessions can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **disconnectOnNoReply** (advanced) | If sync is enabled then this option dictates MinaConsumer if it should disconnect where there is no reply to send back. | true | boolean |
| **maximumPoolSize** (advanced) | Number of worker threads in the worker pool for TCP and UDP. | 16 | int |
| **orderedThreadPoolExecutor** (advanced) | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | boolean |
| **transferExchange** (advanced) | **Deprecated** Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. Also make sure to configure objectCodecPattern to (star) to allow transferring java objects. | false | boolean |
| **allowDefaultCodec** (codec) | The mina component installs a default codec if both, codec is null and textline is false. Setting allowDefaultCodec to false prevents the mina component from installing a default codec as the first element in the filter chain. This is useful in scenarios where another filter must be the first in the filter chain, like the SSL filter. | true | boolean |
| **codec** (codec) | To use a custom minda codec implementation. |  | ProtocolCodecFactory |
| **decoderMaxLineLength** (codec) | To set the textline protocol decoder max line length. By default the default value of Mina itself is used which are 1024. | 1024 | int |
| **encoderMaxLineLength** (codec) | To set the textline protocol encoder max line length. By default the default value of Mina itself is used which are Integer.MAX\_VALUE. | \-1 | int |
| **encoding** (codec) | You can configure the encoding (a charset name) to use for the TCP textline codec and the UDP protocol. If not provided, Camel will use the JVM default Charset. |  | String |
| **filters** (codec) | You can set a list of Mina IoFilters to use. |  | List |
| **objectCodecPattern** (codec) | Accept the wildcard specified classes for Object deserialization, unless they are otherwise rejected. Multiple patterns can be separated by comma. |  | String |
| **textline** (codec) | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP. | false | boolean |
| **textlineDelimiter** (codec) | 

Only used for TCP and if textline=true. Sets the text line delimiter to use. If none provided, Camel will use DEFAULT. This delimiter is used to mark the end of text.

Enum values:

-   DEFAULT
    
-   AUTO
    
-   UNIX
    
-   WINDOWS
    
-   MAC
    





 |  | MinaTextLineDelimiter |
| **sslContextParameters** (security) | To configure SSL security. |  | SSLContextParameters |

## Message Headers

The Mina component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMinaCloseSessionWhenComplete** (common) Constant: [`MINA_CLOSE_SESSION_WHEN_COMPLETE`](https://javadoc.io/doc/org.apache.camel/camel-mina/latest/org/apache/camel/component/mina/MinaConstants.html#MINA_CLOSE_SESSION_WHEN_COMPLETE) | Indicates whether the session should be closed after complete. |  | Boolean |
| **CamelMinaIoSession** (consumer) Constant: [`MINA_IOSESSION`](https://javadoc.io/doc/org.apache.camel/camel-mina/latest/org/apache/camel/component/mina/MinaConstants.html#MINA_IOSESSION) | The key of the IoSession which is stored in the message header. |  | IoSession |
| **CamelMinaLocalAddress** (consumer) Constant: [`MINA_LOCAL_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-mina/latest/org/apache/camel/component/mina/MinaConstants.html#MINA_LOCAL_ADDRESS) | The socket address of local machine that received the message. |  | SocketAddress |
| **CamelMinaRemoteAddress** (consumer) Constant: [`MINA_REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-mina/latest/org/apache/camel/component/mina/MinaConstants.html#MINA_REMOTE_ADDRESS) | The socket address of the remote machine that send the message. |  | SocketAddress |

## Usage

### Using a custom codec

See the Mina how to write your own codec. To use your custom codec with `camel-mina`, you should register your codec in the Registry; for example, by creating a bean in the Spring XML file. Then use the `codec` option to specify the bean ID of your codec. See [HL7](dataformats/hl7-dataformat.md) that has a custom codec.

### Get the IoSession for message

You can get the IoSession from the message header with this key `MinaConstants.MINA_IOSESSION`, and also get the local host address with the key `MinaConstants.MINA_LOCAL_ADDRESS` and remote host address with the key `MinaConstants.MINA_REMOTE_ADDRESS`.

### Configuring Mina filters

Filters permit you to use some Mina Filters, such as `SslFilter`. You can also implement some customized filters. Please note that `codec` and `logger` are also implemented as Mina filters of the type, `IoFilter`. Any filters you may define are appended to the end of the filter chain; that is, after `codec` and `logger`.

## Examples

### Example with sync=false

In this sample, Camel exposes a service that listens for TCP connections on port 6200. We use the **textline** codec. In our route, we create a Mina consumer endpoint that listens to on port 6200: ._Java-only: Java string concatenation with port variable_

```java
from("mina:tcp://localhost:" + port1 + "?textline=true&sync=false").to("mock:result");
```

As the sample is part of a unit test, we test it by sending some data to it on port 6200.

_Java-only: Java test API (MockEndpoint and ProducerTemplate)_

```java
MockEndpoint mock = getMockEndpoint("mock:result");
mock.expectedBodiesReceived("Hello World");

template.sendBody("mina:tcp://localhost:" + port1 + "?textline=true&sync=false", "Hello World");

MockEndpoint.assertIsSatisfied(context);
```

### Example with sync=true

In the next sample, we have a more common use case where we expose a TCP service on port 6201 also use the `textline` codec. However, this time we want to return a response, so we set the `sync` option to `true` on the consumer.

_Java-only: inline Processor class_

```java
fromF("mina:tcp://localhost:%d?textline=true&sync=true", port2).process(new Processor() {
    public void process(Exchange exchange) throws Exception {
        String body = exchange.getIn().getBody(String.class);
        exchange.getOut().setBody("Bye " + body);
    }
});
```

Then we test the sample by sending some data and retrieving the response using the `template.requestBody()` method. As we know the response is a `String`, we cast it to `String` and can assert that the response is, in fact, something we have dynamically set in our processor code logic.

_Java-only: Java test API (ProducerTemplate)_

```java
String response = (String)template.requestBody("mina:tcp://localhost:" + port2 + "?textline=true&sync=true", "World");
assertEquals("Bye World", response);
```

### Example with Spring DSL

Spring DSL can also be used for [MINA](#). In the sample below, we expose a TCP server on port 5555:

```xml
   <route>
     <from uri="mina:tcp://localhost:5555?textline=true"/>
     <to uri="bean:myTCPOrderHandler"/>
  </route>
```

In the route above, we expose a TCP server on port 5555 using the textline codec. We let the Spring bean with ID, `myTCPOrderHandler`, handle the request and return a reply. For instance, the handler bean could be implemented as follows:

_Java-only: Java handler class_

```java
    public String handleOrder(String payload) {
        ...
        return "Order: OK"
   }
```

## Closing Session When Complete

When acting as a server, you sometimes want to close the session when, for example, a client conversion is finished. To instruct Camel to close the session, you should add a header with the key `CamelMinaCloseSessionWhenComplete` set to a boolean `true` value.

For instance, the example below will close the session after it has written the `bye` message back to the client:

_Java-only: inline Processor class_

```java
        from("mina:tcp://localhost:8080?sync=true&textline=true").process(new Processor() {
            public void process(Exchange exchange) throws Exception {
                String body = exchange.getIn().getBody(String.class);
                exchange.getOut().setBody("Bye " + body);
                exchange.getOut().setHeader(MinaConstants.MINA_CLOSE_SESSION_WHEN_COMPLETE, true);
            }
        });
```

## Spring Boot Auto-Configuration

When using mina with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mina-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 29 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mina.allow-default-codec** | The mina component installs a default codec if both, codec is null and textline is false. Setting allowDefaultCodec to false prevents the mina component from installing a default codec as the first element in the filter chain. This is useful in scenarios where another filter must be the first in the filter chain, like the SSL filter. | true | Boolean |
| **camel.component.mina.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mina.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.mina.cached-address** | Whether to create the InetAddress once and reuse. Setting this to false allows to pickup DNS changes in the network. | true | Boolean |
| **camel.component.mina.client-mode** | If the clientMode is true, mina consumer will connect the address as a TCP client. | false | Boolean |
| **camel.component.mina.codec** | To use a custom minda codec implementation. The option is a org.apache.mina.filter.codec.ProtocolCodecFactory type. |  | ProtocolCodecFactory |
| **camel.component.mina.configuration** | To use the shared mina configuration. The option is a org.apache.camel.component.mina.MinaConfiguration type. |  | MinaConfiguration |
| **camel.component.mina.decoder-max-line-length** | To set the textline protocol decoder max line length. By default the default value of Mina itself is used which are 1024. | 1024 | Integer |
| **camel.component.mina.disconnect** | Whether to disconnect(close) from Mina session right after use. Can be used for both consumer and producer. | false | Boolean |
| **camel.component.mina.disconnect-on-no-reply** | If sync is enabled then this option dictates MinaConsumer if it should disconnect where there is no reply to send back. | true | Boolean |
| **camel.component.mina.enabled** | Whether to enable auto configuration of the mina component. This is enabled by default. |  | Boolean |
| **camel.component.mina.encoder-max-line-length** | To set the textline protocol encoder max line length. By default the default value of Mina itself is used which are Integer.MAX\_VALUE. | \-1 | Integer |
| **camel.component.mina.encoding** | You can configure the encoding (a charset name) to use for the TCP textline codec and the UDP protocol. If not provided, Camel will use the JVM default Charset. |  | String |
| **camel.component.mina.filters** | You can set a list of Mina IoFilters to use. |  | List |
| **camel.component.mina.lazy-session-creation** | Sessions can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | Boolean |
| **camel.component.mina.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.mina.maximum-pool-size** | Number of worker threads in the worker pool for TCP and UDP. | 16 | Integer |
| **camel.component.mina.mina-logger** | You can enable the Apache MINA logging filter. Apache MINA uses slf4j logging at INFO level to log all input and output. | false | Boolean |
| **camel.component.mina.no-reply-log-level** | If sync is enabled this option dictates MinaConsumer which logging level to use when logging a there is no reply to send back. | warn | LoggingLevel |
| **camel.component.mina.object-codec-pattern** | Accept the wildcard specified classes for Object deserialization, unless they are otherwise rejected. Multiple patterns can be separated by comma. |  | String |
| **camel.component.mina.ordered-thread-pool-executor** | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | Boolean |
| **camel.component.mina.ssl-context-parameters** | To configure SSL security. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.mina.sync** | Setting to set endpoint as one-way or request-response. | true | Boolean |
| **camel.component.mina.textline** | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP. | false | Boolean |
| **camel.component.mina.textline-delimiter** | Only used for TCP and if textline=true. Sets the text line delimiter to use. If none provided, Camel will use DEFAULT. This delimiter is used to mark the end of text. |  | MinaTextLineDelimiter |
| **camel.component.mina.timeout** | You can configure the timeout that specifies how long to wait for a response from a remote server. The timeout unit is in milliseconds, so 60000 is 60 seconds. | 30000 | Long |
| **camel.component.mina.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.mina.write-timeout** | Maximum amount of time it should take to send data to the MINA session. Default is 10000 milliseconds. | 10000 | Long |
| **camel.component.mina.transfer-exchange** | **Deprecated** Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. Also make sure to configure objectCodecPattern to (star) to allow transferring java objects. | false | Boolean |