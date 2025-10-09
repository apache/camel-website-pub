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

The Pinecone component supports 14 options, which are listed below.

   
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
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | true | boolean |
| **token** (security) | Sets the API key to use for authentication. |  | String |

## Endpoint Options

The Pinecone endpoint is configured using URI syntax:

pinecone:collection

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. (Only used by some actions). |  | String |

### Query Parameters (12 parameters)

   
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
| **tls** (security) | Whether the client uses Transport Layer Security (TLS) to secure communications. | true | boolean |
| **token** (security) | Sets the API key to use for authentication. |  | String |

## Message Headers

The Pinecone component supports 17 message header(s), which is/are listed below:

   
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

## Spring Boot Auto-Configuration

When using pinecone with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-pinecone-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.pinecone.action** | Action to perform. |  | PineconeVectorDbAction |
| **camel.component.pinecone.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.pinecone.cloud** | Sets the cloud type to use (aws/gcp/azure). |  | String |
| **camel.component.pinecone.cloud-region** | Sets the cloud region. |  | String |
| **camel.component.pinecone.collection-dimension** | Sets the Collection Dimension to use (1-1536). | 1536 | Integer |
| **camel.component.pinecone.collection-similarity-metric** | Sets the Collection Similarity Metric to use (cosine/euclidean/dotproduct). |  | String |
| **camel.component.pinecone.configuration** | The configuration;. The option is a org.apache.camel.component.pinecone.PineconeVectorDbConfiguration type. |  | PineconeVectorDbConfiguration |
| **camel.component.pinecone.enabled** | Whether to enable auto configuration of the pinecone component. This is enabled by default. |  | Boolean |
| **camel.component.pinecone.host** | Sets a custom host URL to connect to. |  | String |
| **camel.component.pinecone.index-name** | Sets the index name to use. |  | String |
| **camel.component.pinecone.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.pinecone.proxy-host** | Set the proxy host. |  | String |
| **camel.component.pinecone.proxy-port** | Set the proxy port. |  | Integer |
| **camel.component.pinecone.tls** | Whether the client uses Transport Layer Security (TLS) to secure communications. | true | Boolean |
| **camel.component.pinecone.token** | Sets the API key to use for authentication. |  | String |