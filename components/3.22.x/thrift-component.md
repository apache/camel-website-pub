# Thrift

**Since Camel 2.20**

**Both producer and consumer are supported**

The Thrift component allows you to call or expose Remote Procedure Call (RPC) services using [Apache Thrift](https://thrift.apache.org/) binary communication protocol and serialization mechanism.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-thrift</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

thrift://service\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Thrift component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Determine if the thrift component is using global SSL context parameters. | false | boolean |

## Endpoint Options

The Thrift endpoint is configured using URI syntax:

thrift:host:port/service

with the following path and query parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | The Thrift server host name. This is localhost or 0.0.0.0 (if not defined) when being a consumer or remote server host name when using producer. |  | String |
| **port** (common) | **Required** The Thrift server port. |  | int |
| **service** (common) | **Required** Fully qualified service name from the thrift descriptor file (package dot service definition name). |  | String |

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **compressionType** (common) | 
Protocol compression mechanism type.

Enum values:

-   NONE
    
-   ZLIB
    





 | NONE | ThriftCompressionType |
| **exchangeProtocol** (common) | 

Exchange protocol serialization type.

Enum values:

-   BINARY
    
-   JSON
    
-   SJSON
    
-   COMPACT
    





 | BINARY | ThriftExchangeProtocol |
| **clientTimeout** (consumer) | Client timeout for consumers. |  | int |
| **maxPoolSize** (consumer) | The Thrift server consumer max thread pool size. | 10 | int |
| **poolSize** (consumer) | The Thrift server consumer initial thread pool size. | 1 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **method** (producer) | The Thrift invoked method name. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **negotiationType** (security) | 

Security negotiation type.

Enum values:

-   PLAINTEXT
    
-   SSL
    
-   SASL
    





 | PLAINTEXT | ThriftNegotiationType |
| **sslParameters** (security) | Configuration parameters for SSL/TLS security negotiation. |  | SSLContextParameters |

## Message Headers

The Thrift component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelThriftMethodName** (consumer) Constant: [`THRIFT_METHOD_NAME_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-thrift/latest/org/apache/camel/component/thrift/ThriftConstants.html#THRIFT_METHOD_NAME_HEADER) | Method name handled by the consumer service. |  | String |

## Thrift method parameters mapping

Parameters in the called procedure must be passed as a list of objects inside the message body. The primitives are converted from the objects on the fly. In order to correctly find the corresponding method, all types must be transmitted regardless of the values. Please see an exmaple below, how to pass different parameters to the method with the Camel body

```java
List requestBody = new ArrayList();

requestBody.add((boolean)true);
requestBody.add((byte)THRIFT_TEST_NUM1);
requestBody.add((short)THRIFT_TEST_NUM1);
requestBody.add((int)THRIFT_TEST_NUM1);
requestBody.add((long)THRIFT_TEST_NUM1);
requestBody.add((double)THRIFT_TEST_NUM1);
requestBody.add("empty"); // String parameter
requestBody.add(ByteBuffer.allocate(10)); // binary parameter
requestBody.add(new Work(THRIFT_TEST_NUM1, THRIFT_TEST_NUM2, Operation.MULTIPLY)); // Struct parameter
requestBody.add(new ArrayList<Integer>()); // list paramater
requestBody.add(new HashSet<String>()); // set parameter
requestBody.add(new HashMap<String, Long>()); // map parameter

Object responseBody = template.requestBody("direct:thrift-alltypes", requestBody);
```

Incoming parameters in the service consumer will also be passed to the message body as a list of objects.

## Examples

Below is a simple synchronous method invoke with host and port parameters

```java
from("direct:thrift-calculate")
.to("thrift://localhost:1101/org.apache.camel.component.thrift.generated.Calculator?method=calculate&synchronous=true");
```

Below is a simple synchronous method invoke for the XML DSL configuration

```xml
<route>
    <from uri="direct:thrift-add" />
    <to uri="thrift://localhost:1101/org.apache.camel.component.thrift.generated.Calculator?method=add&synchronous=true"/>
</route>
```

Thrift service consumer with asynchronous communication

```java
from("thrift://localhost:1101/org.apache.camel.component.thrift.generated.Calculator")
.to("direct:thrift-service");
```

It’s possible to automate Java code generation for .thrift files using **thrift-maven-plugin**, but before start the thrift compiler binary distribution for your operating system must be present on the running host.

## For more information, see these resources

[Thrift project GitHub](https://github.com/apache/thrift/) [https://thrift.apache.org/tutorial/java](https://thrift.apache.org/tutorial/java) \[Apache Thrift Java tutorial\]

## Spring Boot Auto-Configuration

When using thrift with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-thrift-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.thrift.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.thrift.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.thrift.enabled** | Whether to enable auto configuration of the thrift component. This is enabled by default. |  | Boolean |
| **camel.component.thrift.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.thrift.use-global-ssl-context-parameters** | Determine if the thrift component is using global SSL context parameters. | false | Boolean |
| **camel.dataformat.thrift.content-type-format** | Defines a content type format in which thrift message will be serialized/deserialized from(to) the Java been. The format can either be native or json for either native binary thrift, json or simple json fields representation. The default value is binary. | binary | String |
| **camel.dataformat.thrift.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.thrift.enabled** | Whether to enable auto configuration of the thrift data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.thrift.instance-class** | Name of class to use when unmarshalling. |  | String |