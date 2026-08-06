# Atmosphere Websocket

**Since Camel 2.14**

**Both producer and consumer are supported**

The Atmosphere-Websocket component provides Websocket based endpoints for a servlet communicating with external clients over Websocket (as a servlet accepting websocket connections from external clients). This component uses the [Atmosphere](https://github.com/Atmosphere/atmosphere) library to support the Websocket transport in various Servlet containers.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-atmosphere-websocket</artifactId>
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

The Atmosphere Websocket component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **servletName** (consumer) | Default name of servlet to use. The default name is CamelServlet. | CamelServlet | String |
| **attachmentMultipartBinding** (consumer (advanced)) | Whether to automatic bind multipart/form-data as attachments on the Camel Exchange. The options attachmentMultipartBinding=true and disableStreamCache=false cannot work together. Remove disableStreamCache to use AttachmentMultipartBinding. This is turn off by default as this may require servlet specific configuration to enable this when using Servlet’s. | false | boolean |
| **fileNameExtWhitelist** (consumer (advanced)) | Whitelist of accepted filename extensions for accepting uploaded files. Multiple extensions can be separated by comma, such as txt,xml. |  | String |
| **httpRegistry** (consumer (advanced)) | To use a custom org.apache.camel.component.servlet.HttpRegistry. |  | HttpRegistry |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpBinding** (advanced) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **httpConfiguration** (advanced) | To use the shared HttpConfiguration as base configuration. |  | HttpConfiguration |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied when deserializing Java objects from requests or responses with Content-Type application/x-java-serialized-object (only used when allowJavaSerializedObject or transferException is enabled). When not set, the JVM-wide jdk.serialFilter is used if present; otherwise a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. packages is applied. |  | String |

## Endpoint Options

The Atmosphere Websocket endpoint is configured using URI syntax:

atmosphere-websocket:servicePath

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **servicePath** (common) | **Required** Name of websocket endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chunked** (common) | If this option is false the Servlet will disable the HTTP streaming and set the content-length header on the response. | true | boolean |
| **disableStreamCache** (common) | Determines whether or not the raw input stream is cached or not. The Camel consumer (camel-servlet, camel-jetty etc.) will by default cache the input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The producer (camel-http) will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is (the stream can only be read once) as the message body. | false | boolean |
| **sendToAll** (common) | Whether to send to all (broadcast) or send to a single receiver. | false | boolean |
| **transferException** (common) | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **useStreaming** (common) | To enable streaming to send data as multiple text fragments. | false | boolean |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **httpBinding** (common (advanced)) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **async** (consumer) | Configure the consumer to work in async mode. | false | boolean |
| **httpMethodRestrict** (consumer) | Used to only allow consuming if the HttpMethod matches, such as GET/POST/PUT etc. Multiple methods can be specified separated by comma. |  | String |
| **logException** (consumer) | If enabled and an Exchange failed processing on the consumer side the exception’s stack trace will be logged when the exception stack trace is not sent in the response’s body. | false | boolean |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **responseBufferSize** (consumer) | To use a custom buffer size on the jakarta.servlet.ServletResponse. |  | Integer |
| **servletName** (consumer) | Name of the servlet to use. | CamelServlet | String |
| **attachmentMultipartBinding** (consumer (advanced)) | Whether to automatic bind multipart/form-data as attachments on the Camel Exchange. The options attachmentMultipartBinding=true and disableStreamCache=false cannot work together. Remove disableStreamCache to use AttachmentMultipartBinding. This is turn off by default as this may require servlet specific configuration to enable this when using Servlet’s. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eagerCheckContentAvailable** (consumer (advanced)) | Whether to eager check whether the HTTP requests has content if the content-length header is 0 or not present. This can be turned on in case HTTP clients do not send streamed data. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **fileNameExtWhitelist** (consumer (advanced)) | Whitelist of accepted filename extensions for accepting uploaded files. Multiple extensions can be separated by comma, such as txt,xml. |  | String |
| **mapHttpMessageBody** (consumer (advanced)) | If this option is true then IN exchange Body of the exchange will be mapped to HTTP body. Setting this to false will avoid the HTTP mapping. | true | boolean |
| **mapHttpMessageFormUrlEncodedBody** (consumer (advanced)) | If this option is true then IN exchange Form Encoded body of the exchange will be mapped to HTTP. Setting this to false will avoid the HTTP Form Encoded body mapping. | true | boolean |
| **mapHttpMessageHeaders** (consumer (advanced)) | If this option is true then IN exchange Headers of the exchange will be mapped to HTTP headers. Setting this to false will avoid the HTTP Headers mapping. | true | boolean |
| **optionsEnabled** (consumer (advanced)) | Specifies whether to enable HTTP OPTIONS for this Servlet consumer. By default OPTIONS is turned off. | false | boolean |
| **traceEnabled** (consumer (advanced)) | Specifies whether to enable HTTP TRACE for this Servlet consumer. By default TRACE is turned off. | false | boolean |
| **bridgeEndpoint** (producer) | If the option is true, HttpProducer will ignore the Exchange.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the option throwExceptionOnFailure to be false to let the HttpProducer send all the fault response back. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Atmosphere Websocket component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAtmosphereWebsocketConnectionKey** (common) Constant: [`CONNECTION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-atmosphere-websocket/latest/org/apache/camel/component/atmosphere/websocket/WebsocketConstants.html#CONNECTION_KEY) | The connection key. |  | String |
| **CamelAtmosphereWebsocketConnectionKeyList** (common) Constant: [`CONNECTION_KEY_LIST`](https://javadoc.io/doc/org.apache.camel/camel-atmosphere-websocket/latest/org/apache/camel/component/atmosphere/websocket/WebsocketConstants.html#CONNECTION_KEY_LIST) | The list of connection keys. |  | List |
| **CamelAtmosphereWebsocketEventType** (consumer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-atmosphere-websocket/latest/org/apache/camel/component/atmosphere/websocket/WebsocketConstants.html#EVENT_TYPE) | The type of event received. It can be ONOPEN\_EVENT\_TYPE, ONERROR\_EVENT\_TYPE or ONCLOSE\_EVENT\_TYPE. |  | int |
| **CamelAtmosphereWebsocketErrorType** (consumer) Constant: [`ERROR_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-atmosphere-websocket/latest/org/apache/camel/component/atmosphere/websocket/WebsocketConstants.html#ERROR_TYPE) | The type of error that occurred. It can be MESSAGE\_NOT\_SENT\_ERROR\_TYPE. |  | int |

## Reading and Writing Data over Websocket

An atmopshere-websocket endpoint can either write data to the socket or read from the socket, depending on whether the endpoint is configured as the producer or the consumer, respectively.

## Examples

### Consumer Example

In the route below, Camel will read from the specified websocket connection.

-   Java
    
-   XML
    
-   YAML
    

```java
from("atmosphere-websocket:///servicepath")
        .to("direct:next");
```

```xml
<route>
  <from uri="atmosphere-websocket:///servicepath"/>
  <to uri="direct:next"/>
</route>
```

```yaml
- route:
    from:
      uri: atmosphere-websocket:///servicepath
      steps:
        - to:
            uri: direct:next
```

### Producer Example

In the route below, Camel will write to the specified websocket connection.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:next")
        .to("atmosphere-websocket:///servicepath");
```

```xml
<route>
  <from uri="direct:next"/>
  <to uri="atmosphere-websocket:///servicepath"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:next
      steps:
        - to:
            uri: atmosphere-websocket:///servicepath
```