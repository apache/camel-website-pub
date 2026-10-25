# weaviate

**Since Camel 4.12**

**Only producer is supported**

The Weaviate Component provides support for interacting with the [weaviate Vector Database](https://weaviate.io/).

## URI format

weaviate:collection\[?options\]

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

The weaviate component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The action to perform. The CamelWeaviateAction header, when set, wins over this option.

Enum values:

-   AGGREGATE
    
-   BATCH\_CREATE
    
-   BM25\_QUERY
    
-   CREATE\_COLLECTION
    
-   CREATE
    
-   DELETE\_BY\_ID
    
-   DELETE\_COLLECTION
    
-   HYBRID\_QUERY
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE\_BY\_ID
    





 |  | WeaviateVectorDbAction |
| **apiKey** (producer) | API Key to authenticate to weaviate with. |  | String |
| **configuration** (producer) | The configuration;. |  | WeaviateVectorDbConfiguration |
| **grpcHost** (producer) | gRPC host for Weaviate server connection. |  | String |
| **grpcPort** (producer) | gRPC port for Weaviate server connection. | 50051 | Integer |
| **host** (producer) | Weaviate server host to connect to. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **scheme** (producer) | Scheme used to connect to weaviate. | http | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The weaviate endpoint is configured using URI syntax:

weaviate:collection

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The action to perform. The CamelWeaviateAction header, when set, wins over this option.

Enum values:

-   AGGREGATE
    
-   BATCH\_CREATE
    
-   BM25\_QUERY
    
-   CREATE\_COLLECTION
    
-   CREATE
    
-   DELETE\_BY\_ID
    
-   DELETE\_COLLECTION
    
-   HYBRID\_QUERY
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE\_BY\_ID
    





 |  | WeaviateVectorDbAction |
| **apiKey** (producer) | API Key to authenticate to weaviate with. |  | String |
| **grpcHost** (producer) | gRPC host for Weaviate server connection. |  | String |
| **grpcPort** (producer) | gRPC port for Weaviate server connection. | 50051 | Integer |
| **host** (producer) | Weaviate server host to connect to. |  | String |
| **scheme** (producer) | Scheme used to connect to weaviate. | http | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The weaviate component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWeaviateAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#ACTION) | 
The action to be performed.

Enum values:

-   AGGREGATE
    
-   BATCH\_CREATE
    
-   BM25\_QUERY
    
-   CREATE\_COLLECTION
    
-   CREATE
    
-   DELETE\_BY\_ID
    
-   DELETE\_COLLECTION
    
-   HYBRID\_QUERY
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE\_BY\_ID
    





 |  | String |
| **CamelWeaviateTextFieldName** (producer) Constant: [`TEXT_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#TEXT_FIELD_NAME) | Text Field Name for Create/Update/Query operation. |  | String |
| **CamelWeaviateCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#COLLECTION_NAME) | Collection Name for all operations. |  | String |
| **CamelWeaviateFields** (producer) Constant: [`FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#FIELDS) | Weaviate Object fields. |  | HashMap |
| **CamelWeaviateProperties** (producer) Constant: [`PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#PROPERTIES) | Weaviate Object properties. |  | HashMap |
| **CamelWeaviateIndexId** (producer) Constant: [`INDEX_ID`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#INDEX_ID) | Index Id. |  | String |
| **CamelWeaviateQueryTopK** (producer) Constant: [`QUERY_TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#QUERY_TOP_K) | Query Top K. |  | Integer |
| **CamelWeaviateUpdateWithMerge** (producer) Constant: [`UPDATE_WITH_MERGE`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#UPDATE_WITH_MERGE) | Merges properties into the object. | true | Boolean |
| **CamelWeaviateKeyName** (producer) Constant: [`KEY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#KEY_NAME) | Key Name for Create/Update/Query operation. |  | String |
| **CamelWeaviateKeyValue** (producer) Constant: [`KEY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#KEY_VALUE) | Key Value for Create/Update/Query operation. |  | String |
| **CamelWeaviateHybridAlpha** (producer) Constant: [`HYBRID_ALPHA`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#HYBRID_ALPHA) | Alpha value for hybrid search (0.0 = pure BM25, 1.0 = pure vector). |  | Float |
| **CamelWeaviateQueryVector** (producer) Constant: [`QUERY_VECTOR`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDbHeaders.html#QUERY_VECTOR) | Optional query vector for hybrid search (overrides server-side vectorizer). |  | List |

## Message Body

The message body at each side of the weaviate component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `list`, `text` or `null` | 
By the action in the action option or the CamelWeaviateAction header: the vector as a List of Float or a float array for CREATE, UPDATE\_BY\_ID and QUERY, with the properties in the CamelWeaviateProperties header, a List of WeaviateObject for BATCH\_CREATE, and the query text for HYBRID\_QUERY and BM25\_QUERY. CREATE\_COLLECTION, DELETE\_COLLECTION, QUERY\_BY\_ID, DELETE\_BY\_ID and AGGREGATE do not read the body, the id is in the CamelWeaviateIndexId header. Another body fails, a List of Double too: the weaviate:embeddings data type transformer builds the vector from the output of langchain4j-embeddings.

-   With `action=CREATE`: `list`
    
-   With `action=BATCH_CREATE`: `list` (`java.util.List<io.weaviate.client6.v1.api.collections.WeaviateObject<java.util.Map<java.lang.String, java.lang.Object>>>`)
    
-   With `action=UPDATE_BY_ID`: `list`
    
-   With `action=QUERY`: `list`
    
-   With `action=HYBRID_QUERY`: `text` (`java.lang.String`)
    
-   With `action=BM25_QUERY`: `text` (`java.lang.String`)
    
-   With `action=CREATE_COLLECTION`: `any`
    
-   With `action=DELETE_COLLECTION`: `any`
    
-   With `action=QUERY_BY_ID`: `any`
    
-   With `action=DELETE_BY_ID`: `any`
    
-   With `action=AGGREGATE`: `any`
    





 |
| **Producer output** | `pojo` or `value` | 

By the action: a WeaviateObject for CREATE, an InsertManyResponse for BATCH\_CREATE, a QueryResponse for QUERY, HYBRID\_QUERY and BM25\_QUERY, an Optional of WeaviateObject for QUERY\_BY\_ID, an AggregateResponse for AGGREGATE, and a Boolean for CREATE\_COLLECTION, UPDATE\_BY\_ID, DELETE\_BY\_ID and DELETE\_COLLECTION.

-   With `action=CREATE`: `pojo` (`io.weaviate.client6.v1.api.collections.WeaviateObject<java.util.Map<java.lang.String, java.lang.Object>>`)
    
-   With `action=BATCH_CREATE`: `pojo` (`io.weaviate.client6.v1.api.collections.data.InsertManyResponse`)
    
-   With `action=QUERY`: `pojo` (`io.weaviate.client6.v1.api.collections.query.QueryResponse<java.util.Map<java.lang.String, java.lang.Object>>`)
    
-   With `action=HYBRID_QUERY`: `pojo` (`io.weaviate.client6.v1.api.collections.query.QueryResponse<java.util.Map<java.lang.String, java.lang.Object>>`)
    
-   With `action=BM25_QUERY`: `pojo` (`io.weaviate.client6.v1.api.collections.query.QueryResponse<java.util.Map<java.lang.String, java.lang.Object>>`)
    
-   With `action=QUERY_BY_ID`: `pojo` (`java.util.Optional<io.weaviate.client6.v1.api.collections.WeaviateObject<java.util.Map<java.lang.String, java.lang.Object>>>`)
    
-   With `action=AGGREGATE`: `pojo` (`io.weaviate.client6.v1.api.collections.aggregate.AggregateResponse`)
    
-   With `action=CREATE_COLLECTION`: `value` (`java.lang.Boolean`)
    
-   With `action=UPDATE_BY_ID`: `value` (`java.lang.Boolean`)
    
-   With `action=DELETE_BY_ID`: `value` (`java.lang.Boolean`)
    
-   With `action=DELETE_COLLECTION`: `value` (`java.lang.Boolean`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

The `action` option of the endpoint, such as `weaviate:myCollection?action=BM25_QUERY`, or the `CamelWeaviateAction` header selects the operation; the header, when set, wins over the option. Without either, the producer fails. The weaviate:embeddings data type transformer runs before the endpoint, so it reads the header only. The routes below create a collection, add an object with its vector (the message body) and its properties (the `CamelWeaviateProperties` header), and run a keyword (BM25) search for the text in the message body:

```yaml
- route:
    from:
      uri: direct:createCollection
      steps:
        - setHeader:
            name: CamelWeaviateAction
            expression:
              constant:
                expression: CREATE_COLLECTION
        - to:
            uri: weaviate:Articles
            parameters:
              host: localhost:8080
- route:
    from:
      uri: direct:addArticle
      steps:
        - setHeader:
            name: CamelWeaviateAction
            expression:
              constant:
                expression: CREATE
        - setHeader:
            name: CamelWeaviateProperties
            expression:
              groovy:
                expression: "[title: 'Camel in Action', category: 'books']"
        - setBody:
            expression:
              groovy:
                expression: "[0.1f, 0.2f, 0.3f]"
        - to:
            uri: weaviate:Articles
            parameters:
              host: localhost:8080
- route:
    from:
      uri: direct:search
      steps:
        - setHeader:
            name: CamelWeaviateAction
            expression:
              constant:
                expression: BM25_QUERY
        - setHeader:
            name: CamelWeaviateQueryTopK
            expression:
              constant:
                expression: "5"
        - to:
            uri: weaviate:Articles
            parameters:
              host: localhost:8080
        - log:
            message: "${body}"
```