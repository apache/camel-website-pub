# Qdrant

**Since Camel 4.5**

**Only producer is supported**

The Qdrant Component provides support for interacting with the [Qdrant Vector Database](https://qdrant.tech).

## URI format

qdrant:collection\[?options\]

Where **collection** represents a named set of points (vectors with a payload) defined in your database.

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

The Qdrant component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | Sets the API key to use for authentication. |  | String |
| **configuration** (producer) | The configuration;. |  | QdrantConfiguration |
| **host** (producer) | The host to connect to. | localhost | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxResults** (producer) | Max results for similarity search. | 3 | int |
| **port** (producer) | The port to connect to. | 6334 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | Duration |
| **tls** (producer) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **filter** (advanced) | **Autowired** Filter of type io.qdrant.client.grpc.Points.Points.Filter for similarity search. This is for advanced usage. |  | Filter |

## Endpoint Options

The Qdrant endpoint is configured using URI syntax:

qdrant:collection

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | Sets the API key to use for authentication. |  | String |
| **host** (producer) | The host to connect to. | localhost | String |
| **maxResults** (producer) | Max results for similarity search. | 3 | int |
| **port** (producer) | The port to connect to. | 6334 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | Duration |
| **tls** (producer) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **filter** (advanced) | **Autowired** Filter of type io.qdrant.client.grpc.Points.Points.Filter for similarity search. This is for advanced usage. |  | Filter |

## Message Headers

The Qdrant component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelQdrantAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#ACTION) | 
The action to be performed.

Enum values:

-   CREATE\_COLLECTION
    
-   DELETE\_COLLECTION
    
-   UPSERT
    
-   RETRIEVE
    
-   DELETE
    
-   COLLECTION\_INFO
    
-   SIMILARITY\_SEARCH
    





 |  | String |
| **CamelQdrantPointsPayloadSelector** (producer) Constant: [`PAYLOAD_SELECTOR`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#PAYLOAD_SELECTOR) | Payload Selector. |  | Points$WithPayloadSelector |
| **CamelQdrantOperationID** (producer) Constant: [`OPERATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#OPERATION_ID) | Operation ID. |  | long |
| **CamelQdrantOperationStatus** (producer) Constant: [`OPERATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#OPERATION_STATUS) | Operation Status. |  | String |
| **CamelQdrantOperationStatusValue** (producer) Constant: [`OPERATION_STATUS_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#OPERATION_STATUS_VALUE) | Operation Status Value. |  | int |
| **CamelQdrantReadConsistency** (producer) Constant: [`READ_CONSISTENCY`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#READ_CONSISTENCY) | Read Consistency. |  | Points$ReadConsistency |
| **CamelQdrantWithPayload** (producer) Constant: [`INCLUDE_PAYLOAD`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#INCLUDE_PAYLOAD) | Include Payload. | true | boolean |
| **CamelQdrantWithVectors** (producer) Constant: [`INCLUDE_VECTORS`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#INCLUDE_VECTORS) | Include Vectors. | false | boolean |
| **CamelQdrantSize** (producer) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#SIZE) | The number of elements. |  | int |
| **CamelQdrantPointId** (producer) Constant: [`POINT_ID`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/Qdrant$Headers.html#POINT_ID) | The point id to use for operation. |  | int |

## Examples

### Collection Examples

In the route below, we use the qdrant component to create a collection named _myCollection_ with the given parameters:

#### Create Collection

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.CREATE_COLLECTION)
    .setBody()
        .constant(
            Collections.VectorParams.newBuilder()
                .setSize(2)
                .setDistance(Collections.Distance.Cosine).build())
    .to("qdrant:myCollection");
```

#### Delete Collection

In the route below, we use the qdrant component to delete a collection named _myCollection_:

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.DELETE_COLLECTION)
    .to("qdrant:myCollection");
```

#### Collection Info

In the route below, we use the qdrant component to get information about the collection named `myCollection`:

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.COLLECTION_INFO)
    .to("qdrant:myCollection")
    .process(this::process);
```

If there is a collection, you will receive a reply of type `Collections.CollectionInfo`. If there is not, the exchange will contain an exception of type `QdrantActionException` with a cause of type `StatusRuntimeException statusRuntimeException` and status `Status.NOT_FOUND`.

### Points Examples

#### Upsert

In the route below we use the qdrant component to perform insert + updates (upsert) on points in the collection named _myCollection_:

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.UPSERT)
    .setBody()
        .constant(
            Points.PointStruct.newBuilder()
                .setId(id(8))
                .setVectors(VectorsFactory.vectors(List.of(3.5f, 4.5f)))
                .putAllPayload(Map.of(
                        "foo", value("hello"),
                        "bar", value(1)))
                .build())
    .to("qdrant:myCollection");
```

#### Retrieve

In the route below, we use the qdrant component to retrieve information of a single point by id from the collection named _myCollection_:

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.RETRIEVE)
    .setBody()
        .constant(PointIdFactory.id(8))
    .to("qdrant:myCollection");
```

#### Delete

In the route below, we use the qdrant component to delete points from the collection named `myCollection` according to a criteria:

-   Java
    

```java
from("direct:in")
    .setHeader(Qdrant.Headers.ACTION)
        .constant(QdrantAction.DELETE)
    .setBody()
        .constant(ConditionFactory.matchKeyword("foo", "hello"))
    .to("qdrant:myCollection");
```

## Spring Boot Auto-Configuration

When using qdrant with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-qdrant-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.qdrant.api-key** | Sets the API key to use for authentication. |  | String |
| **camel.component.qdrant.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.qdrant.configuration** | The configuration;. The option is a org.apache.camel.component.qdrant.QdrantConfiguration type. |  | QdrantConfiguration |
| **camel.component.qdrant.enabled** | Whether to enable auto configuration of the qdrant component. This is enabled by default. |  | Boolean |
| **camel.component.qdrant.filter** | Filter of type io.qdrant.client.grpc.Points.Points.Filter for similarity search. This is for advanced usage. The option is a io.qdrant.client.grpc.Points.Filter type. |  | Points$Filter |
| **camel.component.qdrant.host** | The host to connect to. | localhost | String |
| **camel.component.qdrant.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.qdrant.max-results** | Max results for similarity search. | 3 | Integer |
| **camel.component.qdrant.port** | The port to connect to. | 6334 | Integer |
| **camel.component.qdrant.timeout** | Sets a default timeout for all requests. |  | Duration |
| **camel.component.qdrant.tls** | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | Boolean |