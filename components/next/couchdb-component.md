# CouchDB

**Since Camel 2.11**

**Both producer and consumer are supported**

The **couchdb:** component allows you to treat [CouchDB](http://couchdb.apache.org/) instances as a producer or consumer of messages. Using the lightweight LightCouch API, this camel component has the following features:

-   As a consumer, monitors couch changesets for inserts, updates and deletes and publishes these as messages into camel routes.
    
-   As a producer, can save, update, delete (by using `CamelCouchDbMethod` with `DELETE` value) documents and get documents by id (by using `CamelCouchDbMethod` with GET value) into CouchDB.
    
-   Can support as many endpoints as required, eg for multiple databases across multiple instances.
    
-   Ability to have events trigger for only deletes, only inserts/updates or all (default).
    
-   Headers set for sequenceId, document revision, document id, and HTTP method type.
    

> **Note**
> CouchDB 3.x is not supported.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-couchdb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

couchdb:http://hostname\[:port\]/database?\[options\]

Where **hostname** is the hostname of the running couchdb instance. Port is optional and if not specified, then defaults to 5984.

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

The CouchDB component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The CouchDB endpoint is configured using URI syntax:

couchdb:protocol:hostname:port/database

With the following _path_ and _query_ parameters:

### Path Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | 
**Required** The protocol to use for communicating with the database.

Enum values:

-   http
    
-   https
    





 |  | String |
| **hostname** (common) | **Required** Hostname of the running couchdb instance. |  | String |
| **port** (common) | Port number for the running couchdb instance. | 5984 | int |
| **database** (common) | **Required** Name of the database to use. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **createDatabase** (common) | Creates the database if it does not already exist. | false | boolean |
| **deletes** (consumer) | Document deletes are published as events. | true | boolean |
| **heartbeat** (consumer) | How often to send an empty message to keep socket alive in millis. | 30000 | long |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | int |
| **style** (consumer) | 
Specifies how many revisions are returned in the changes array. The default, main\_only, will only return the current winning revision; all\_docs will return all leaf revisions (including conflicts and deleted former conflicts.).

Enum values:

-   all\_docs
    
-   main\_only
    





 | main\_only | String |
| **updates** (consumer) | Document inserts/updates are published as events. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **password** (security) | Password for authenticated databases. |  | String |
| **username** (security) | Username in case of authenticated databases. |  | String |

## Message Headers

The CouchDB component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCouchDbDatabase** (consumer) Constant: [`HEADER_DATABASE`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#HEADER_DATABASE) | The database the message came from. |  | String |
| **CamelCouchDbSeq** (consumer) Constant: [`HEADER_SEQ`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#HEADER_SEQ) | The couchdb changeset sequence number of the update / delete message. |  | String |
| **CamelCouchDbId** (common) Constant: [`HEADER_DOC_ID`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#HEADER_DOC_ID) | The couchdb document id. |  | String |
| **CamelCouchDbRev** (common) Constant: [`HEADER_DOC_REV`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#HEADER_DOC_REV) | The couchdb document revision. |  | String |
| **CamelCouchDbMethod** (common) Constant: [`HEADER_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#HEADER_METHOD) | The method (delete / update). |  | String |
| **CamelCouchDbResumeAction** (consumer) Constant: [`COUCHDB_RESUME_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-couchdb/latest/org/apache/camel/component/couchdb/CouchDbConstants.html#COUCHDB_RESUME_ACTION) | The resume action to execute when resuming. |  | String |

Headers are set by the consumer once the message is received. The producer will also set the headers for downstream processors once the insert/update has taken place. Any headers set prior to the producer are ignored. That means, for example, if you set CamelCouchDbId as a header, it will not be used as the id for insertion, the id of the document will still be used.

## Message Body

The component will use the message body as the document to be inserted. If the body is an instance of String, then it will be marshaled into a GSON object before insert. This means that the string must be valid JSON or the insert / update will fail. If the body is an instance of a `com.google.gson.JsonElement` then it will be inserted as is. Otherwise, the producer will throw an unsupported body type exception.

> **Note**
> To update a CouchDB document, its `id` and `rev` field must be part of the json payload routed to CouchDB by Camel.

## Examples

For example, if you wish to consume all inserts, updates and deletes from a CouchDB instance running locally, on port 9999, then you could use the following:

-   Java
    
-   XML
    
-   YAML
    

```java
from("couchdb:http://localhost:9999").process(someProcessor);
```

```xml
<route>
    <from uri="couchdb:http://localhost:9999"/>
    <process ref="someProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: couchdb:http://localhost:9999
    steps:
      - process:
          ref: someProcessor
```

If you were only interested in deleting, then you could use the following:

-   Java
    
-   XML
    
-   YAML
    

```java
from("couchdb:http://localhost:9999?updates=false").process(someProcessor);
```

```xml
<route>
    <from uri="couchdb:http://localhost:9999?updates=false"/>
    <process ref="someProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: couchdb:http://localhost:9999
      parameters:
        updates: false
    steps:
      - process:
          ref: someProcessor
```

If you want to insert a message as a document, then the body of the exchange is used:

-   Java
    
-   XML
    
-   YAML
    

```java
from("someProducingEndpoint").process(someProcessor).to("couchdb:http://localhost:9999")
```

```xml
<route>
    <from uri="someProducingEndpoint"/>
    <process ref="someProcessor"/>
    <to uri="couchdb:http://localhost:9999"/>
</route>
```

```yaml
- route:
    from:
      uri: someProducingEndpoint
    steps:
      - process:
          ref: someProcessor
      - to:
          uri: couchdb:http://localhost:9999
```

To start tracking the changes immediately after an update sequence, implement a custom resume strategy. To do so, it is necessary to implement a CouchDbResumeStrategy and use the resumable to set the last (update) offset to start tracking the changes:

```none
public class CustomSequenceResumeStrategy implements CouchDbResumeStrategy {
    @Override
    public void resume(CouchDbResumable resumable) {
        resumable.setLastOffset("custom-last-update");
    }
}
```

## Spring Boot Auto-Configuration

When using couchdb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-couchdb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.couchdb.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.couchdb.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.couchdb.enabled** | Whether to enable auto configuration of the couchdb component. This is enabled by default. |  | Boolean |
| **camel.component.couchdb.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |