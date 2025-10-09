# Gora

> **Warning**
> **Deprecated:** This gora is deprecated and may be removed in a future release.

**Since Camel 2.14**

**Both producer and consumer are supported**

**Camel-Gora** is an [Apache Camel](http://camel.apache.org/) component that allows you to work with NoSQL databases using the [Apache Gora](http://gora.apache.org/) framework.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
 <groupId>org.apache.camel</groupId>
 <artifactId>camel-gora</artifactId>
 <!-- use the same version as your Camel core version -->
 <version>x.x.x</version>
</dependency>
```

## Apache Gora Overview

The [Apache Gora](http://gora.apache.org/) open source framework provides an in-memory data model and persistence for big data. Gora supports persisting to column stores, key value stores, document stores and RDBMSs, and analyzing the data with extensive [Apache Hadoop™ MapReduce](http://hadoop.apache.org/) support. Gora uses the [Apache Software License v2.0](http://www.apache.org/licenses/LICENSE-2.0.md) and graduated from the Apache Incubator in Janauary 2012 to become a top-level Apache project.

Apache Gora currently supports the following datastores: [Apache HBase](http://hbase.apache.org/), [Apache Cassandra](http://cassandra.apache.org/), [Apache Accumulo](http://accumulo.apache.org/), [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) and SQL databases such as [hsqldb](http://hsqldb.org/), [MySQL](http://www.mysql.com/) and more.

## URI format

gora:instanceName\[?options\]

Hbase examples with mandatory options :

_XML_

```xml
<to uri="gora:foobar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

_Java DSL_

```java
to("gora:foobar?keyClass=java.lang.Long&valueClass=org.apache.camel.component.gora.generated.Pageview&dataStoreClass=org.apache.gora.hbase.store.HBaseStore")
```

## Configuration

Using camel-gora needs some configuration. This mainly involve to configure the _AvroStore_ through the _gora.properties_ file and to define the relevant mappings as part of the _[gora-core](http://gora.apache.org/current/gora-core.md)_ module.

Extensive information for this configuration can be found in the apache [gora documentation](http://gora.apache.org/current/index.md) and the [gora-conf](http://gora.apache.org/current/gora-conf.md) page.

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

The Gora component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Gora endpoint is configured using URI syntax:

gora:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Instance name. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataStoreClass** (common) | The type of the dataStore. |  | String |
| **keyClass** (common) | The type class of the key. |  | String |
| **valueClass** (common) | The type of the value. |  | String |
| **concurrentConsumers** (consumer) | Number of concurrent consumers. | 1 | int |
| **endKey** (consumer) | The End Key. |  | Object |
| **endTime** (consumer) | The End Time. |  | long |
| **fields** (consumer) | The Fields. |  | Strings |
| **keyRangeFrom** (consumer) | The Key Range From. |  | Object |
| **keyRangeTo** (consumer) | The Key Range To. |  | Object |
| **limit** (consumer) | The Limit. |  | long |
| **startKey** (consumer) | The Start Key. |  | Object |
| **startTime** (consumer) | The Start Time. |  | long |
| **timeRangeFrom** (consumer) | The Time Range From. |  | long |
| **timeRangeTo** (consumer) | The Time Range To. |  | long |
| **timestamp** (consumer) | The Timestamp. |  | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **flushOnEveryOperation** (producer) | Flush on every operation. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **hadoopConfiguration** (advanced) | Hadoop Configuration. |  | Configuration |

## Message Headers

The Gora component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **goraKey** (producer) Constant: [`GORA_KEY.value`](https://javadoc.io/doc/org.apache.camel/camel-gora/latest/org/apache/camel/component/gora/GoraAttribute.html#GORA_KEY) | Used in order to define the datum key for the operations need it. |  | Object |
| **goraOperation** (producer) Constant: [`GORA_OPERATION.value`](https://javadoc.io/doc/org.apache.camel/camel-gora/latest/org/apache/camel/component/gora/GoraAttribute.html#GORA_OPERATION) | Used in order to define the operation to execute. |  | String |

## Supported Gora Operations

Supported operations include : **put**, **get**, **delete**, **getSchemaName**, **deleteSchema**, **createSchema**, **query**, **deleteByQuery**, **schemaExists**.

Some operations require arguments while some others no. The arguments to operations could be either the _body_ of the _in_ message or defined in a header property. Below there is a list with some additional info for each operation.

 
| Property | Description |
| --- | --- |
| put | _Inserts the persistent object with the given key._ |
| get | _Returns the object corresponding to the given key fetching all the fields._ |
| delete | _Deletes the object with the given key._ |
| getSchemaName | _Returns the schema name given to this DataStore._ |
| deleteSchema | _Deletes the underlying schema or table (or similar) in the datastore that holds the objects._ |
| createSchema | _Creates the optional schema or table (or similar) in the datastore to hold the objects._ |
| query | _Executes the given query and returns the results._ |
| deleteByQuery | _Deletes all the objects matching the query._ |
| schemaExists | _Returns whether the schema that holds the data exists in the datastore._ |

## Usage examples

**Create Schema** _(XML DSL)_:

```xml
<setHeader name="GoraOperation">
 <constant>CreateSchema</constant>
</setHeader>
<to uri="gora:foobar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

**SchemaExists** _(XML DSL)_:

```xml
<setHeader name="GoraOperation">
 <constant>SchemaExists</constant>
</setHeader>
 <to uri="gora:foobar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

**Put** _(XML DSL)_:

```xml
<setHeader name="GoraOperation">
 <constant>put</constant>
</setHeader>
<setHeader name="GoraKey">
 <constant>22222</constant>
</setHeader>
<to uri="gora:foo?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

**Get** _(XML DSL)_:

```xml
<setHeader name="GoraOperation">
 <constant>GET</constant>
</setHeader>
<setHeader name="GoraKey">
 <constant>10101</constant>
</setHeader>
<to uri="gora:bar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

**Delete** _(XML DSL)_:

```xml
<setHeader name="GoraOperation">
 <constant>DELETE</constant>
</setHeader>
<setHeader name="GoraKey">
 <constant>22222</constant>
</setHeader>
<to uri="gora:bar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

**Query** _(XML DSL)_:

```xml
<to uri="gora:foobar?keyClass=java.lang.Long&amp;valueClass=org.apache.camel.component.gora.generated.Pageview&amp;dataStoreClass=org.apache.gora.hbase.store.HBaseStore"/>
```

The full usage examples in the form of integration tests can be found at [camel-gora-examples](https://github.com/ipolyzos/camel-gora-examples/) repository.

## More resources

For more please information and in depth configuration refer to the [Apache Gora Documentation](http://gora.apache.org/current/overview.md) and the [Apache Gora Tutorial](http://gora.apache.org/current/tutorial.md).

## Spring Boot Auto-Configuration

When using gora with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-gora-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.gora.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.gora.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.gora.enabled** | Whether to enable auto configuration of the gora component. This is enabled by default. |  | Boolean |
| **camel.component.gora.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |