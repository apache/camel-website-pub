# Qdrant

**Since Camel 4.5**

**Only producer is supported**

The Qdrant Component provides support for interacting with the [Qdrant Vector Database](https://qdrant.tech).

## URI format

qdrant:collection\[?options\]

Where **collection** represents a named set of points (vectors with a payload) defined in your database.

The `action` option of the endpoint, or the `CamelQdrantAction` header, selects the action, such as `qdrant:myCollection?action=SIMILARITY_SEARCH`. The header, when set, wins over the option, so one endpoint can also run several actions. Without either, the producer fails.

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

The Qdrant component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The action to perform. The CamelQdrantAction header, when set, wins over this option.

Enum values:

-   CREATE\_COLLECTION
    
-   DELETE\_COLLECTION
    
-   UPSERT
    
-   RETRIEVE
    
-   DELETE
    
-   COLLECTION\_INFO
    
-   SIMILARITY\_SEARCH
    





 |  | QdrantAction |
| **configuration** (producer) | The configuration;. |  | QdrantConfiguration |
| **host** (producer) | The host to connect to. | localhost | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxResults** (producer) | Max results for similarity search. | 3 | int |
| **port** (producer) | The port to connect to. | 6334 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | Duration |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **filter** (advanced) | **Autowired** Filter for similarity search. |  | Filter |
| **apiKey** (security) | Sets the API key to use for authentication. |  | String |
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |

## Endpoint Options

The Qdrant endpoint is configured using URI syntax:

qdrant:collection

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The action to perform. The CamelQdrantAction header, when set, wins over this option.

Enum values:

-   CREATE\_COLLECTION
    
-   DELETE\_COLLECTION
    
-   UPSERT
    
-   RETRIEVE
    
-   DELETE
    
-   COLLECTION\_INFO
    
-   SIMILARITY\_SEARCH
    





 |  | QdrantAction |
| **host** (producer) | The host to connect to. | localhost | String |
| **maxResults** (producer) | Max results for similarity search. | 3 | int |
| **port** (producer) | The port to connect to. | 6334 | int |
| **timeout** (producer) | Sets a default timeout for all requests. |  | Duration |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **filter** (advanced) | **Autowired** Filter for similarity search. |  | Filter |
| **apiKey** (security) | Sets the API key to use for authentication. |  | String |
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |

## Message Headers

The Qdrant component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelQdrantAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#ACTION) | 
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
| **CamelQdrantPointsPayloadSelector** (producer) Constant: [`PAYLOAD_SELECTOR`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#PAYLOAD_SELECTOR) | Payload Selector. |  | Points$WithPayloadSelector |
| **CamelQdrantOperationID** (producer) Constant: [`OPERATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#OPERATION_ID) | Operation ID. |  | long |
| **CamelQdrantOperationStatus** (producer) Constant: [`OPERATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#OPERATION_STATUS) | Operation Status. |  | String |
| **CamelQdrantOperationStatusValue** (producer) Constant: [`OPERATION_STATUS_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#OPERATION_STATUS_VALUE) | Operation Status Value. |  | int |
| **CamelQdrantReadConsistency** (producer) Constant: [`READ_CONSISTENCY`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#READ_CONSISTENCY) | Read Consistency. |  | Points$ReadConsistency |
| **CamelQdrantWithPayload** (producer) Constant: [`INCLUDE_PAYLOAD`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#INCLUDE_PAYLOAD) | Include Payload. | true | boolean |
| **CamelQdrantWithVectors** (producer) Constant: [`INCLUDE_VECTORS`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#INCLUDE_VECTORS) | Include Vectors. | false | boolean |
| **CamelQdrantSize** (producer) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#SIZE) | The number of elements. |  | int |
| **CamelQdrantPointId** (producer) Constant: [`POINT_ID`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#POINT_ID) | The point id to use for operation. |  | int |
| **CamelQdrantMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-qdrant/latest/org/apache/camel/component/qdrant/QdrantHeaders.html#MAX_RESULTS) | The maximum number of results to return from a similarity search. |  | int |

## Message Body

The message body at each side of the Qdrant component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `pojo`, `list` or `null` | 
By the action in the action option or the CamelQdrantAction header: a VectorParams for CREATE\_COLLECTION, a PointStruct or a List of them for UPSERT, a PointId or a List of them for RETRIEVE, a PointsSelector, PointId, Filter or Condition for DELETE, and the query vector as a List of Float, a float array or a PointStruct for SIMILARITY\_SEARCH. DELETE\_COLLECTION and COLLECTION\_INFO do not read the body. Another body fails, such as a number as the id (use PointIdFactory.id) or a List of Double. The qdrant:embeddings data type transformer builds the PointStruct from the output of langchain4j-embeddings.

-   With `action=CREATE_COLLECTION`: `pojo` (`io.qdrant.client.grpc.Collections.VectorParams`)
    
-   With `action=DELETE_COLLECTION`: `any`
    
-   With `action=UPSERT`: `pojo` or `list`
    
-   With `action=RETRIEVE`: `pojo` or `list`
    
-   With `action=DELETE`: `pojo`
    
-   With `action=SIMILARITY_SEARCH`: `list` or `pojo`
    
-   With `action=COLLECTION_INFO`: `any`
    





 |
| **Producer output** | `list`, `pojo` or `unchanged` | 

By the action: a List of RetrievedPoint for RETRIEVE, a List of ScoredPoint for SIMILARITY\_SEARCH and a CollectionInfo for COLLECTION\_INFO. The other actions keep the body, UPSERT and DELETE with the operation id and status in headers.

-   With `action=CREATE_COLLECTION`: `unchanged`
    
-   With `action=DELETE_COLLECTION`: `unchanged`
    
-   With `action=UPSERT`: `unchanged`
    
-   With `action=RETRIEVE`: `list` (`java.util.List<io.qdrant.client.grpc.Points.RetrievedPoint>`)
    
-   With `action=DELETE`: `unchanged`
    
-   With `action=SIMILARITY_SEARCH`: `list` (`java.util.List<io.qdrant.client.grpc.Points.ScoredPoint>`)
    
-   With `action=COLLECTION_INFO`: `pojo` (`io.qdrant.client.grpc.Collections.CollectionInfo`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Examples

In YAML, a Groovy expression builds the request objects of the Qdrant client, such as `VectorParams` or `PointStruct`.

### Collection Examples

In the route below, we use the Qdrant component to create a collection named _myCollection_ with the given parameters:

#### Create Collection

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
        .constant(QdrantAction.CREATE_COLLECTION)
    .setBody()
        .constant(
            Collections.VectorParams.newBuilder()
                .setSize(2)
                .setDistance(Collections.Distance.Cosine).build())
    .to("qdrant:myCollection");
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: CREATE_COLLECTION
        - setBody:
            expression:
              groovy:
                expression: >-
                  io.qdrant.client.grpc.Collections.VectorParams.newBuilder()
                  .setSize(2)
                  .setDistance(io.qdrant.client.grpc.Collections.Distance.Cosine)
                  .build()
        - to:
            uri: qdrant:myCollection
```

#### Delete Collection

In the route below, we use the Qdrant component to delete a collection named _myCollection_:

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
        .constant(QdrantAction.DELETE_COLLECTION)
    .to("qdrant:myCollection");
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: DELETE_COLLECTION
        - to:
            uri: qdrant:myCollection
```

#### Collection Info

In the route below, we use the qdrant component to get information about the collection named `myCollection`:

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
        .constant(QdrantAction.COLLECTION_INFO)
    .to("qdrant:myCollection")
    .process(this::process);
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: COLLECTION_INFO
        - to:
            uri: qdrant:myCollection
        - log:
            message: "${body}"
```

If there is a collection, you will receive a reply of type `Collections.CollectionInfo`. If there is not, the exchange will contain an exception of type `QdrantActionException` with a cause of type `StatusRuntimeException statusRuntimeException` and status `Status.NOT_FOUND`.

### Points Examples

#### Upsert

In the route below we use the qdrant component to perform insert + updates (upsert) on points in the collection named _myCollection_:

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
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

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: UPSERT
        - setBody:
            expression:
              groovy:
                expression: >-
                  io.qdrant.client.grpc.Points.PointStruct.newBuilder()
                  .setId(io.qdrant.client.PointIdFactory.id(8))
                  .setVectors(io.qdrant.client.VectorsFactory.vectors([3.5f, 4.5f]))
                  .putAllPayload([foo: io.qdrant.client.ValueFactory.value('hello'),
                  bar: io.qdrant.client.ValueFactory.value(1)])
                  .build()
        - to:
            uri: qdrant:myCollection
```

#### Retrieve

In the route below, we use the Qdrant component to retrieve information of a single point by id from the collection named _myCollection_:

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
        .constant(QdrantAction.RETRIEVE)
    .setBody()
        .constant(PointIdFactory.id(8))
    .to("qdrant:myCollection");
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: RETRIEVE
        - setBody:
            expression:
              groovy:
                expression: "io.qdrant.client.PointIdFactory.id(8)"
        - to:
            uri: qdrant:myCollection
```

#### Delete

In the route below, we use the qdrant component to delete points from the collection named `myCollection` according to a criteria:

-   Java
    
-   YAML
    

```java
from("direct:in")
    .setHeader(QdrantHeaders.ACTION)
        .constant(QdrantAction.DELETE)
    .setBody()
        .constant(ConditionFactory.matchKeyword("foo", "hello"))
    .to("qdrant:myCollection");
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelQdrantAction
            expression:
              constant:
                expression: DELETE
        - setBody:
            expression:
              groovy:
                expression: "io.qdrant.client.ConditionFactory.matchKeyword('foo', 'hello')"
        - to:
            uri: qdrant:myCollection
```