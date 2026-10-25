# Pinecone

**Since Camel 4.6**

**Only producer is supported**

The Pinecone Component provides support for interacting with the [Pinecone Vector Database](https://pinecone.io/).

## URI format

pinecone:collection\[?options\]

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

The Pinecone component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
Action to perform.

Enum values:

-   CREATE\_COLLECTION
    
-   CREATE\_SERVERLESS\_INDEX
    
-   CREATE\_POD\_INDEX
    
-   FETCH
    
-   UPSERT
    
-   DELETE\_INDEX
    
-   DELETE\_COLLECTION
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE
    
-   DELETE\_BY\_ID
    





 |  | PineconeVectorDbAction |
| **cloud** (producer) | 

Sets the cloud type to use (aws/gcp/azure).

Enum values:

-   aws
    
-   azure
    
-   gcp
    





 |  | String |
| **cloudRegion** (producer) | Sets the cloud region. |  | String |
| **collectionDimension** (producer) | Sets the Collection Dimension to use (1-1536). | 1536 | Integer |
| **collectionSimilarityMetric** (producer) | Sets the Collection Similarity Metric to use (cosine/euclidean/dotproduct). |  | String |
| **configuration** (producer) | The configuration;. |  | PineconeVectorDbConfiguration |
| **host** (producer) | Sets a custom host URL to connect to. |  | String |
| **indexName** (producer) | Sets the index name to use. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (producer) | Set the proxy host. |  | String |
| **proxyPort** (producer) | Set the proxy port. |  | Integer |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |
| **token** (security) | Sets the API key to use for authentication. |  | String |

## Endpoint Options

The Pinecone endpoint is configured using URI syntax:

pinecone:collection

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. (Only used by some actions). |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
Action to perform.

Enum values:

-   CREATE\_COLLECTION
    
-   CREATE\_SERVERLESS\_INDEX
    
-   CREATE\_POD\_INDEX
    
-   FETCH
    
-   UPSERT
    
-   DELETE\_INDEX
    
-   DELETE\_COLLECTION
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE
    
-   DELETE\_BY\_ID
    





 |  | PineconeVectorDbAction |
| **cloud** (producer) | 

Sets the cloud type to use (aws/gcp/azure).

Enum values:

-   aws
    
-   azure
    
-   gcp
    





 |  | String |
| **cloudRegion** (producer) | Sets the cloud region. |  | String |
| **collectionDimension** (producer) | Sets the Collection Dimension to use (1-1536). | 1536 | Integer |
| **collectionSimilarityMetric** (producer) | Sets the Collection Similarity Metric to use (cosine/euclidean/dotproduct). |  | String |
| **host** (producer) | Sets a custom host URL to connect to. |  | String |
| **indexName** (producer) | Sets the index name to use. |  | String |
| **proxyHost** (producer) | Set the proxy host. |  | String |
| **proxyPort** (producer) | Set the proxy port. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | false | boolean |
| **token** (security) | Sets the API key to use for authentication. |  | String |

## Message Headers

The Pinecone component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelPineconeAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#ACTION) | 
The action to be performed.

Enum values:

-   CREATE\_COLLECTION
    
-   CREATE\_SERVERLESS\_INDEX
    
-   CREATE\_POD\_INDEX
    
-   FETCH
    
-   UPSERT
    
-   DELETE\_INDEX
    
-   DELETE\_COLLECTION
    
-   QUERY
    
-   QUERY\_BY\_ID
    
-   UPDATE
    
-   DELETE\_BY\_ID
    





 |  | String |
| **CamelPineconeTextFieldName** (producer) Constant: [`TEXT_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#TEXT_FIELD_NAME) | Text Field Name for Insert/Upsert operation. |  | String |
| **CamelPineconeVectorFieldName** (producer) Constant: [`VECTOR_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#VECTOR_FIELD_NAME) | Vector Field Name for Insert/Upsert operation. |  | String |
| **CamelPineconeIndexName** (producer) Constant: [`INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#INDEX_NAME) | Index Name. |  | String |
| **CamelPineconeIndexPodType** (producer) Constant: [`INDEX_POD_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#INDEX_POD_TYPE) | Index Pod Type. |  | String |
| **CamelPineconeIndexPodEnvironment** (producer) Constant: [`INDEX_POD_ENVIRONMENT`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#INDEX_POD_ENVIRONMENT) | Index Pod Environment. |  | String |
| **CamelPineconeCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#COLLECTION_NAME) | Collection Name for Insert/Upsert operation. |  | String |
| **CamelPineconeCollectionSimilarityMetric** (producer) Constant: [`COLLECTION_SIMILARITY_METRIC`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#COLLECTION_SIMILARITY_METRIC) | 

Collection Similarity Metric.

Enum values:

-   cosine
    
-   euclidean
    
-   dotproduct
    





 |  | String |
| **CamelPineconeCollectionDimension** (producer) Constant: [`COLLECTION_DIMENSION`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#COLLECTION_DIMENSION) | Collection Dimension. |  | int |
| **CamelPineconeCollectionCloud** (producer) Constant: [`COLLECTION_CLOUD`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#COLLECTION_CLOUD) | 

Collection Cloud Vendor.

Enum values:

-   aws
    
-   gcp
    
-   azure
    





 |  | String |
| **CamelPineconeCollectionCloudRegion** (producer) Constant: [`COLLECTION_CLOUD_REGION`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#COLLECTION_CLOUD_REGION) | 

Collection Cloud Vendor Region.

Enum values:

-   aws
    
-   gcp
    
-   azure
    





 |  | String |
| **CamelPineconeIndexId** (producer) Constant: [`INDEX_ID`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#INDEX_ID) | Index Upsert Id. |  | String |
| **CamelPineconeQueryTopK** (producer) Constant: [`QUERY_TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#QUERY_TOP_K) | Query Top K. |  | Integer |
| **CamelPineconeNamespace** (producer) Constant: [`NAMESPACE`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#NAMESPACE) | Namespace for actions (query/upsert/etc). |  | String |
| **CamelPineconeQueryFilter** (producer) Constant: [`QUERY_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#QUERY_FILTER) | Query Filter. |  | String |
| **CamelPineconeQueryIncludeValues** (producer) Constant: [`QUERY_INCLUDE_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#QUERY_INCLUDE_VALUES) | Query Include Values. |  | boolean |
| **CamelPineconeQueryIncludeMetadata** (producer) Constant: [`QUERY_INCLUDE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-pinecone/latest/org/apache/camel/component/pinecone/PineconeVectorDbHeaders.html#QUERY_INCLUDE_METADATA) | Query Include Metadata. |  | Struct |

## Message Body

The message body at each side of the Pinecone component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `list` or `null` | 
By the action in the action option or the CamelPineconeAction header: the vector as a List of Float or a float array for UPSERT, UPDATE and QUERY, with the id in the CamelPineconeIndexId header, and the ids as a List of String for FETCH and DELETE\_BY\_ID. The other actions do not read the body. Another body fails, a List of Double too: the pinecone:embeddings data type transformer builds the vector from the output of langchain4j-embeddings.

-   With `action=UPSERT`: `list`
    
-   With `action=UPDATE`: `list`
    
-   With `action=QUERY`: `list`
    
-   With `action=FETCH`: `list`
    
-   With `action=DELETE_BY_ID`: `list`
    
-   With `action=QUERY_BY_ID`: `any`
    
-   With `action=CREATE_COLLECTION`: `any`
    
-   With `action=CREATE_SERVERLESS_INDEX`: `any`
    
-   With `action=CREATE_POD_INDEX`: `any`
    
-   With `action=DELETE_INDEX`: `any`
    
-   With `action=DELETE_COLLECTION`: `any`
    





 |
| **Producer output** | `pojo` or `unchanged` | 

By the action: the response of the Pinecone SDK, such as an UpsertResponse, a FetchResponse or a QueryResponseWithUnsignedIndices with the matches. DELETE\_INDEX and DELETE\_COLLECTION keep the body.

-   With `action=UPSERT`: `pojo` (`io.pinecone.proto.UpsertResponse`)
    
-   With `action=UPDATE`: `pojo` (`io.pinecone.proto.UpdateResponse`)
    
-   With `action=QUERY`: `pojo` (`io.pinecone.unsigned_indices_model.QueryResponseWithUnsignedIndices`)
    
-   With `action=QUERY_BY_ID`: `pojo` (`io.pinecone.unsigned_indices_model.QueryResponseWithUnsignedIndices`)
    
-   With `action=FETCH`: `pojo` (`io.pinecone.proto.FetchResponse`)
    
-   With `action=DELETE_BY_ID`: `pojo` (`io.pinecone.proto.DeleteResponse`)
    
-   With `action=CREATE_COLLECTION`: `pojo` (`org.openapitools.db_control.client.model.CollectionModel`)
    
-   With `action=CREATE_SERVERLESS_INDEX`: `pojo` (`org.openapitools.db_control.client.model.IndexModel`)
    
-   With `action=CREATE_POD_INDEX`: `pojo` (`org.openapitools.db_control.client.model.IndexModel`)
    
-   With `action=DELETE_INDEX`: `unchanged`
    
-   With `action=DELETE_COLLECTION`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

The `action` option, or the `CamelPineconeAction` header, selects the operation. The first route below creates a serverless index. The second route queries the index with a vector, and the `CamelPineconeQueryTopK` header sets how many matches it returns:

```yaml
- route:
    from:
      uri: direct:createIndex
      steps:
        - to:
            uri: pinecone:my-collection
            parameters:
              action: CREATE_SERVERLESS_INDEX
              token: "{{pinecone.token}}"
              indexName: my-index
              collectionSimilarityMetric: cosine
              collectionDimension: 3
              cloud: aws
              cloudRegion: us-east-1
- route:
    from:
      uri: direct:query
      steps:
        - setHeader:
            name: CamelPineconeQueryTopK
            expression:
              constant:
                expression: "3"
        - setBody:
            expression:
              groovy:
                expression: "[0.1f, 0.2f, 0.3f]"
        - to:
            uri: pinecone:my-collection
            parameters:
              action: QUERY
              token: "{{pinecone.token}}"
              indexName: my-index
        - log:
            message: "${body}"
```