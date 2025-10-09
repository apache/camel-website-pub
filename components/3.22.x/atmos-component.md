# Atmos

**Since Camel 2.15**

**Both producer and consumer are supported**

Camel-Atmos is an [Apache Camel](http://camel.apache.org/) component that allows you to work with ViPR object data services using the [Atmos Client](https://github.com/EMCECS/atmos-client-java).

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

The Atmos component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **uri** (advanced) | The URI of the server for the Atmos client to connect to. |  | String |
| **fullTokenId** (security) | The token id to pass to the Atmos client. |  | String |
| **secretKey** (security) | The secret key to pass to the Atmos client (should be base64 encoded). |  | String |
| **sslValidation** (security) | Whether the Atmos client should perform SSL validation. | false | boolean |

## Endpoint Options

The Atmos endpoint is configured using URI syntax:

atmos:name/operation

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | Atmos name. |  | String |
| **operation** (common) | 
**Required** Operation to perform.

Enum values:

-   put
    
-   del
    
-   search
    
-   get
    
-   move
    





 |  | AtmosOperation |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **localPath** (common) | Local path to put files. |  | String |
| **newRemotePath** (common) | New path on Atmos when moving files. |  | String |
| **query** (common) | Search query on Atmos. |  | String |
| **remotePath** (common) | Where to put files on Atmos. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **uri** (advanced) | Atomos server uri. |  | String |
| **fullTokenId** (security) | Atmos client fullTokenId. |  | String |
| **secretKey** (security) | The secret key to pass to the Atmos client (should be base64 encoded). |  | String |
| **sslValidation** (security) | Atmos SSL validation. | false | boolean |

## Message Headers

The Atmos component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **DOWNLOADED\_FILE** (common) Constant: [`DOWNLOADED_FILE`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#DOWNLOADED_FILE) | The name of the remote path downloaded in case of a single file. |  | String |
| **DOWNLOADED\_FILES** (common) Constant: [`DOWNLOADED_FILES`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#DOWNLOADED_FILES) | The name of the remote paths downloaded in case of multiple files (one per line). |  | String |
| **UPLOADED\_FILE** (producer) Constant: [`UPLOADED_FILE`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#UPLOADED_FILE) | The name of the remote path uploaded in case of a single file. |  | String |
| **UPLOADED\_FILES** (producer) Constant: [`UPLOADED_FILES`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#UPLOADED_FILES) | The name of the remote paths uploaded in case of multiple files (one per line). |  | String |
| **DELETED\_PATH** (producer) Constant: [`DELETED_PATH`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#DELETED_PATH) | The remote path deleted on Atmos. |  | String |
| **MOVED\_PATH** (producer) Constant: [`MOVED_PATH`](https://javadoc.io/doc/org.apache.camel/camel-atmos/latest/org/apache/camel/component/atmos/util/AtmosConstants.html#MOVED_PATH) | The moved path. |  | String |

## Dependencies

To use Atmos in your camel routes you need to add the dependency on **camel-atmos** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-atmos</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Integrations

When you look at atmos integrations, there is one type of consumer, GetConsumer, which is a type of ScheduledPollConsumer.

-   `Get`
    

Whereas there are 4 types of producers which are

-   `Get`
    
-   `Del`
    
-   `Move`
    
-   `Put`
    

## Operations

Regarding the operations, the following headers are set on camel exchange

```text
DOWNLOADED_FILE, DOWNLOADED_FILES, UPLOADED_FILE, UPLOADED_FILES, DELETED_PATH, MOVED_PATH
```

## Examples

### Consumer Example

```java
from("atmos:foo/get?remotePath=/path")
  .to("mock:test");
```

`remotePath` represents the path from where the data will be read and passes the camel exchange to regarding producer Underneath, this component uses Atmos client API for this and every other operations.

### Producer Example

```java
from("direct:start")
  .to("atmos://get?remotePath=/dummy/dummy.txt")
```

`remotePath` represents the path where the operations occur on ViPR object data service. In producers, operations(`Get`,`Del`, `Move`,`Put`) run on ViPR object data services and results are set on headers of camel exchange.

## Spring Boot Auto-Configuration

When using atmos with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-atmos-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.atmos.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.atmos.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.atmos.enabled** | Whether to enable auto configuration of the atmos component. This is enabled by default. |  | Boolean |
| **camel.component.atmos.full-token-id** | The token id to pass to the Atmos client. |  | String |
| **camel.component.atmos.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.atmos.secret-key** | The secret key to pass to the Atmos client (should be base64 encoded). |  | String |
| **camel.component.atmos.ssl-validation** | Whether the Atmos client should perform SSL validation. | false | Boolean |
| **camel.component.atmos.uri** | The URI of the server for the Atmos client to connect to. |  | String |