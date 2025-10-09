# Nitrite

**Since Camel 3.0**

**Both producer and consumer are supported**

Nitrite component is used to access [Nitrite NoSQL database](https://github.com/dizitart/nitrite-database)

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-nitrite</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The Nitrite component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Nitrite endpoint is configured using URI syntax:

nitrite:database

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **database** (common) | **Required** Path to database file. Will be created if not exists. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (common) | Name of Nitrite collection. Cannot be used in combination with repositoryClass option. |  | String |
| **repositoryClass** (common) | Class of Nitrite ObjectRepository. Cannot be used in combination with collection option. |  | Class |
| **repositoryName** (common) | Optional name of ObjectRepository. Can be only used in combination with repositoryClass, otherwise have no effect. |  | String |
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
| **password** (security) | Password for Nitrite database. Required, if option username specified. |  | String |
| **username** (security) | Username for Nitrite database. Database is not secured if option not specified. |  | String |

## Message Headers

The Nitrite component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNitriteChangeTimestamp** (consumer) Constant: [`CHANGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-nitrite/latest/org/apache/camel/component/nitrite/NitriteConstants.html#CHANGE_TIMESTAMP) | Event timestamp in Epoch millis. |  | long |
| **CamelNitriteChangeType** (consumer) Constant: [`CHANGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-nitrite/latest/org/apache/camel/component/nitrite/NitriteConstants.html#CHANGE_TYPE) | 
Type of event.

Enum values:

-   INSERT
    
-   UPDATE
    
-   REMOVE
    
-   DROP
    
-   CLOSE
    





 |  | ChangeType |
| **CamelNitriteOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-nitrite/latest/org/apache/camel/component/nitrite/NitriteConstants.html#OPERATION) | Operation to invoke on Collection or Repository. Defaults to UpsertOperation if not specified. |  | AbstractNitriteOperation |
| **CamelNitriteWriteResult** (common) Constant: [`WRITE_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-nitrite/latest/org/apache/camel/component/nitrite/NitriteConstants.html#WRITE_RESULT) | Result of data modifying operation. |  | WriteResult |

## Producer operations

The following Operations are available to specify as NitriteConstants.OPERATION when producing to Nitrite.

   
| Class | Type | Parameters | Description |
| --- | --- | --- | --- |
| `FindCollectionOperation` | `collection` | `Filter(optional), FindOptions(optional)` | Find Documents in collection by Filter. If not specified, returns all documents |
| `RemoveCollectionOperation` | `collection` | `Filter(required), RemoveOptions(optional)` | Remove documents matching Filter |
| `UpdateCollectionOperation` | `collection` | `Filter(required), UpdateOptions(optional), Document(optional)` | Update documents matching Filter. If Document not specified, the message body is used |
| `CreateIndexOperation` | `common` | `field:String(required), IndexOptions(required)` | Create index with IndexOptions on field |
| `DropIndexOperation` | `common` | `field:String(required)` | Drop index on field |
| `ExportDatabaseOperation` | `common` | `ExportOptions(optional)` | Export full database to JSON and stores result in body - see Nitrite docs for details about format |
| `GetAttributesOperation` | `common` |  | Get attributes of collection |
| `GetByIdOperation` | `common` | `NitriteId` | Get Document by \_id |
| `ImportDatabaseOperation` | `common` |  | Import full database from JSON in body |
| `InsertOperation` | `common` | `payload(optional)` | Insert document to collection or object to ObjectRepository. If parameter not specified, inserts message body |
| `ListIndicesOperation` | `common` |  | List indexes in collection and stores `List<Index>` in message body |
| `RebuildIndexOperation` | `common` | `field (required), async (optional)` | Rebuild existing index on field |
| `UpdateOperation` | `common` | `payload(optional)` | Update document in collection or object in ObjectRepository. If parameter not specified, updates document from message body |
| `UpsertOperation` | `common` | `payload(optional)` | Upsert (Insert or Update) document in collection or object in ObjectRepository. If parameter not specified, updates document from message body |
| `FindRepositoryOperation` | `repository` | `ObjectFilter(optional), FindOptions(optional)` | Find objects in ObjectRepository by ObjectFilter. If not specified, returns all objects in repository |
| `RemoveRepositoryOperation` | `repository` | `ObjectFilter(required), RepoveOptions(optional)` | Remove objects in ObjectRepository matched by ObjectFilter |
| `UpdateRepositoryOperation` | `repository` | `ObjectFilter(required), UpdateOptions(optional), payload(optional)` | Update objects matching ObjectFilter. If payload not specified, the message body is used |

## Examples

### Consume changes in collection.

```java
from("nitrite:/path/to/database.db?collection=myCollection")
    .to("log:change")
```

### Consume changes in object repository.

```java
from("nitrite:/path/to/database.db?repositoryClass=my.project.MyPersistentObject")
    .to("log:change")
```

```java
package my.project;

@Indices({
        @Index(value = "key1", type = IndexType.NonUnique)
})
public class MyPersistentObject {
    @Id
    private long id;
    private String key1;
    // Getters, setters
}
```

### Insert or update document

```java
from("direct:upsert")
    .setBody(constant(Document.createDocument("key1", "val1")))
    .to("nitrite:/path/to/database.db?collection=myCollection")
```

### Get Document by id

```java
from("direct:getByID")
    .setHeader(NitriteConstants.OPERATION, () -> new GetByIdOperation(NitriteId.createId(123L)))
    .to("nitrite:/path/to/database.db?collection=myCollection")
    .to("log:result")
```

### Find Document in collection

```java
from("direct:getByID")
    .setHeader(NitriteConstants.OPERATION, () -> new FindCollectionOperation(Filters.eq("myKey", "withValue")))
    .to("nitrite:/path/to/database.db?collection=myCollection")
    .to("log:result");
```

## Spring Boot Auto-Configuration

When using nitrite with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-nitrite-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.nitrite.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.nitrite.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.nitrite.enabled** | Whether to enable auto configuration of the nitrite component. This is enabled by default. |  | Boolean |
| **camel.component.nitrite.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |