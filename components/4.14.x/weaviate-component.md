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

The weaviate component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | API Key to authenticate to weaviate with. |  | String |
| **configuration** (producer) | The configuration;. |  | WeaviateVectorDbConfiguration |
| **host** (producer) | Weaviate server host to connect to. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (producer) | Proxy host to connect to weaviate through. |  | String |
| **proxyPort** (producer) | Proxy port to connect to weaviate through. |  | Integer |
| **proxyScheme** (producer) | Proxy scheme to connect to weaviate through. |  | String |
| **scheme** (producer) | Scheme used to connect to weaviate. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The weaviate endpoint is configured using URI syntax:

weaviate:collection

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection Name. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | API Key to authenticate to weaviate with. |  | String |
| **host** (producer) | Weaviate server host to connect to. |  | String |
| **proxyHost** (producer) | Proxy host to connect to weaviate through. |  | String |
| **proxyPort** (producer) | Proxy port to connect to weaviate through. |  | Integer |
| **proxyScheme** (producer) | Proxy scheme to connect to weaviate through. |  | String |
| **scheme** (producer) | Scheme used to connect to weaviate. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The weaviate component supports 16 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWeaviateAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#ACTION) | 
The action to be performed.

Enum values:

-   CREATE\_COLLECTION
    
-   CREATE\_INDEX
    
-   UPSERT
    
-   INSERT
    
-   SEARCH
    
-   DELETE
    
-   UPDATE
    
-   QUERY
    
-   QUERY\_BY\_ID
    





 |  | String |
| **CamelWeaviateTextFieldName** (producer) Constant: [`TEXT_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#TEXT_FIELD_NAME) | Text Field Name for Insert/Upsert operation. |  | String |
| **CamelweaviateVectorFieldName** (producer) Constant: [`VECTOR_FIELD_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#VECTOR_FIELD_NAME) | Vector Field Name for Insert/Upsert operation. |  | String |
| **CamelWeaviateCollectionName** (producer) Constant: [`COLLECTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#COLLECTION_NAME) | Collection Name for Insert/Upsert operation. |  | String |
| **CamelWeaviateCollectionSimilarityMetric** (producer) Constant: [`COLLECTION_SIMILARITY_METRIC`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#COLLECTION_SIMILARITY_METRIC) | 

Collection Similarity Metric.

Enum values:

-   cosine
    
-   euclidean
    
-   dotproduct
    





 |  | String |
| **CamelWeaviateCollectionDimension** (producer) Constant: [`COLLECTION_DIMENSION`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#COLLECTION_DIMENSION) | Collection Dimension. |  | int |
| **CamelWeaviateCollectionCloud** (producer) Constant: [`COLLECTION_CLOUD`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#COLLECTION_CLOUD) | 

Collection Cloud Vendor.

Enum values:

-   aws
    
-   gcp
    
-   azure
    





 |  | String |
| **CamelWeaviateCollectionCloudRegion** (producer) Constant: [`COLLECTION_CLOUD_REGION`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#COLLECTION_CLOUD_REGION) | 

Collection Cloud Vendor Region.

Enum values:

-   aws
    
-   gcp
    
-   azure
    





 |  | String |
| **CamelWeaviateIndexName** (producer) Constant: [`INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#INDEX_NAME) | Index Name. |  | String |
| **CamelWeaviateFields** (producer) Constant: [`FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#FIELDS) | Weaviate Object fields. |  | HashMap |
| **CamelWeaviateProperties** (producer) Constant: [`PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#PROPERTIES) | Weaviate Object properties. |  | HashMap |
| **CamelWeaviateIndexId** (producer) Constant: [`INDEX_ID`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#INDEX_ID) | Index Id. |  | String |
| **CamelWeaviateQueryTopK** (producer) Constant: [`QUERY_TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#QUERY_TOP_K) | Query Top K. |  | Integer |
| **CamelWeaviateUpdateWithMerge** (producer) Constant: [`UPDATE_WITH_MERGE`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#UPDATE_WITH_MERGE) | Merges properties into the object. | true | Boolean |
| **CamelWeaviateKeyName** (producer) Constant: [`KEY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#KEY_NAME) | Key Name for Insert/Upsert operation. |  | String |
| **CamelWeaviateKeyValue** (producer) Constant: [`KEY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-weaviate/latest/org/apache/camel/component/weaviate/WeaviateVectorDb$Headers.html#KEY_VALUE) | Key Value for Insert/Upsert operation. |  | String |

## Spring Boot Auto-Configuration

When using weaviate with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-weaviate-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.weaviate.api-key** | API Key to authenticate to weaviate with. |  | String |
| **camel.component.weaviate.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.weaviate.configuration** | The configuration;. The option is a org.apache.camel.component.weaviate.WeaviateVectorDbConfiguration type. |  | WeaviateVectorDbConfiguration |
| **camel.component.weaviate.enabled** | Whether to enable auto configuration of the weaviate component. This is enabled by default. |  | Boolean |
| **camel.component.weaviate.host** | Weaviate server host to connect to. |  | String |
| **camel.component.weaviate.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.weaviate.proxy-host** | Proxy host to connect to weaviate through. |  | String |
| **camel.component.weaviate.proxy-port** | Proxy port to connect to weaviate through. |  | Integer |
| **camel.component.weaviate.proxy-scheme** | Proxy scheme to connect to weaviate through. |  | String |
| **camel.component.weaviate.scheme** | Scheme used to connect to weaviate. |  | String |