# Elasticsearch Low level Rest Client

**Since Camel 4.3**

**Only producer is supported**

The ElasticSearch component allows you to interface with [ElasticSearch](https://www.elastic.co/products/elasticsearch) 8.x API or [OpenSearch](https://opensearch.org/) using the ElasticSearch Java Low level Rest Client.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-elasticsearch-rest-client</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

elasticsearch-rest-client://clusterName\[?options\]

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

The Elasticsearch Low level Rest Client component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | Connection timeout. | 30000 | int |
| **hostAddressesList** (producer) | List of host Addresses, multiple hosts can be separated by comma. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **socketTimeout** (producer) | Socket timeout. | 30000 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **enableSniffer** (advanced) | Enabling Sniffer. | false | boolean |
| **restClient** (advanced) | **Autowired** Rest Client of type org.elasticsearch.client.RestClient. This is only for advanced usage. |  | RestClient |
| **sniffAfterFailureDelay** (advanced) | Sniffer after failure delay (in millis). | 60000 | int |
| **snifferInterval** (advanced) | Sniffer interval (in millis). | 60000 | int |
| **certificatePath** (security) | Certificate Path. |  | String |
| **password** (security) | Password. |  | String |
| **user** (security) | Username. |  | String |

## Endpoint Options

The Elasticsearch Low level Rest Client endpoint is configured using URI syntax:

elasticsearch-rest-client:clusterName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterName** (producer) | **Required** Cluster Name. |  | String |

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | Connection timeout. | 30000 | int |
| **hostAddressesList** (producer) | List of host Addresses, multiple hosts can be separated by comma. |  | String |
| **indexName** (producer) | Index Name. |  | String |
| **operation** (producer) | 
Operation.

Enum values:

-   INDEX\_OR\_UPDATE
    
-   GET\_BY\_ID
    
-   DELETE
    
-   CREATE\_INDEX
    
-   DELETE\_INDEX
    
-   SEARCH
    





 |  | ElasticsearchRestClientOperation |
| **socketTimeout** (producer) | Socket timeout. | 30000 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **enableSniffer** (advanced) | Enabling Sniffer. | false | boolean |
| **restClient** (advanced) | **Autowired** Rest Client of type org.elasticsearch.client.RestClient. This is only for advanced usage. |  | RestClient |
| **sniffAfterFailureDelay** (advanced) | Sniffer after failure delay (in millis). | 60000 | int |
| **snifferInterval** (advanced) | Sniffer interval (in millis). | 60000 | int |
| **certificatePath** (security) | Certificate Path. |  | String |
| **password** (security) | Password. |  | String |
| **user** (security) | Username. |  | String |

## Message Headers

The Elasticsearch Low level Rest Client component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelElasticsearchId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest-client/latest/org/apache/camel/component/elasticsearch/rest/client/ElasticSearchRestClientConstant.html#ID) | ID of the object to index or retrieve or delete. |  | String |
| **CamelElasticsearchSearchQuery** (producer) Constant: [`SEARCH_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest-client/latest/org/apache/camel/component/elasticsearch/rest/client/ElasticSearchRestClientConstant.html#SEARCH_QUERY) | The JSON Query to perform for search. |  | String |
| **CamelElasticsearchIndexSettings** (producer) Constant: [`INDEX_SETTINGS`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest-client/latest/org/apache/camel/component/elasticsearch/rest/client/ElasticSearchRestClientConstant.html#INDEX_SETTINGS) | Advanced - The JSON Index Settings and/or Mappings Query to perform to create an index. |  | String |
| **CamelElasticsearchIndexName** (producer) Constant: [`INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest-client/latest/org/apache/camel/component/elasticsearch/rest/client/ElasticSearchRestClientConstant.html#INDEX_NAME) | The Index name. |  | String |
| **CamelElasticsearchOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest-client/latest/org/apache/camel/component/elasticsearch/rest/client/ElasticSearchRestClientConstant.html#OPERATION) | 
The operation to perform.

Enum values:

-   INDEX\_OR\_UPDATE
    
-   GET\_BY\_ID
    
-   DELETE
    
-   CREATE\_INDEX
    
-   DELETE\_INDEX
    
-   SEARCH
    





 |  | ElasticsearchRestClientOperation |

## Elasticsearch Low level Rest Client Operations

Set an endpoint URI option or exchange header with a name of `operation` and a value of one of the following supported options.

  
| operation | message body | description |
| --- | --- | --- |
| `INDEX_OR_UPDATE` | `String`, `byte[]`, `Reader` or `InputStream` content to index or update | Adds or updates content to an index and returns the resulting `id` in the message body. You can set the name of the target index from the `indexName` URI parameter option, or by providing a message header with the key `INDEX_NAME`. When updating indexed content, you must provide its id via a message header with the key `ID` . |
| `GET_BY_ID` | `String` id of content to retrieve | Retrieves a JSON String representation of the indexed document, corresponding to the given index id and sets it as the message exchange body. You can set the name of the target index from the `indexName` URI parameter option, or by providing a message header with the key `INDEX_NAME`. You must provide the index id of the content to retrieve either in the message body, or via a message header with the key `ID` . |
| `DELETE` | `String` id of content to delete | Deletes the specified `indexName` and returns a `boolean` value as the message exchange body, indicating whether the operation was successful. You can set the name of the target index from the `indexName` URI parameter option, or by providing a message header with the key `INDEX_NAME`. You must provide the index id of the content to delete either in the message body, or via a message header with the key `ID` . |
| `CREATE_INDEX` |  | Creates the specified `indexName` and returns a `boolean` value as the message exchange body, indicating whether the operation was successful. You can set the name of the target index to create from the `indexName` URI parameter option, or by providing a message header with the key `CamelElasticsearchIndexName`. You may also provide a header with the key `CamelElasticsearchIndexSettings` where the value is a JSON String representation of the index settings. |
| `DELETE_INDEX` |  | Deletes the specified `indexName` and returns a `boolean` value as the message exchange body, indicating whether the operation was successful. You can set the name of the target index to create from the `indexName` URI parameter option, or by providing a message header with the key `CamelElasticsearchIndexName`. |
| `SEARCH` | `Map` (optional) | Search for content with either a `Map` of `String` keys & values of query criteria. Or a JSON string representation of the query. Matching documents are returned as a JSON string set on the message exchange body. You can set the JSON query String by providing a message header with the key `CamelElasticsearchSearchQuery`. You can set the message exchange body to a `Map` of `String` keys & values for the query criteria. |

## Examples

### Index Content Example

To index some content.

```java
from("direct:index")
    .setBody().constant("{\"content\": \"ElasticSearch With Camel\"}")
    .to("elasticsearch-rest-client://myCluster?operation=INDEX_OR_UPDATE&indexName=myIndex");
```

To update existing indexed content, provide the `ID` message header and the message body with the updated content.

```java
from("direct:index")
    .setHeader("CamelElasticsearchId").constant("1")
    .setBody().constant("{\"content\": \"ElasticSearch REST Client With Camel\"}")
    .to("elasticsearch-rest-client://myCluster?operation=INDEX_OR_UPDATE&indexName=myIndex");
```

### Get By ID Example

```java
from("direct:getById")
    .setHeader("CamelElasticsearchId").constant("1")
    .to("elasticsearch-rest-client://myCluster?operation=GET_BY_ID&indexName=myIndex");
```

### Delete Example

To delete indexed content, provide the `ID` message header.

```java
from("direct:getById")
    .setHeader("CamelElasticsearchId").constant("1")
    .to("elasticsearch-rest-client://myCluster?operation=DELETE&indexName=myIndex");
```

### Create Index Example

To create a new index.

```java
from("direct:createIndex")
    .to("elasticsearch-rest-client://myCluster?operation=CREATE_INDEX&indexName=myIndex");
```

To create a new index with some custom settings.

```java
String indexSettings = "{\"settings\":{\"number_of_replicas\": 1,\"number_of_shards\": 3,\"analysis\": {},\"refresh_interval\": \"1s\"},\"mappings\":{\"dynamic\": false,\"properties\": {\"title\": {\"type\": \"text\", \"analyzer\": \"english\"}}}}";
```

```java
from("direct:createIndex")
    .setHeader("CamelElasticsearchIndexSettings").constant(indexSettings)
    .to("elasticsearch-rest-client://myCluster?operation=CREATE_INDEX&indexName=myIndex");
```

### Delete Index Example

To delete an index.

```java
from("direct:deleteIndex")
    .to("elasticsearch-rest-client://myCluster?operation=DELETE_INDEX&indexName=myIndex");
```

### Search Example

Search with a JSON query.

```java
from("direct:search")
    .setHeader("CamelElasticsearchSearchQuery").constant("{\"query\":{\"match\":{\"content\":\"ElasticSearch With Camel\"}}}")
    .to("elasticsearch-rest-client://myCluster?operation=SEARCH&indexName=myIndex");
```

Search on specific field(s) using `Map`.

```java
Map<String, String> criteria = new HashMap<>();
criteria.put("content", "Camel");
```

```java
from("direct:search")
    .setBody().constant(criteria)
    .to("elasticsearch-rest-client://myCluster?operation=SEARCH&indexName=myIndex");
```

## Spring Boot Auto-Configuration

When using elasticsearch-rest-client with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-elasticsearch-rest-client-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.elasticsearch-rest-client.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.elasticsearch-rest-client.certificate-path** | Certificate Path. |  | String |
| **camel.component.elasticsearch-rest-client.connection-timeout** | Connection timeout. | 30000 | Integer |
| **camel.component.elasticsearch-rest-client.enable-sniffer** | Enabling Sniffer. | false | Boolean |
| **camel.component.elasticsearch-rest-client.enabled** | Whether to enable auto configuration of the elasticsearch-rest-client component. This is enabled by default. |  | Boolean |
| **camel.component.elasticsearch-rest-client.host-addresses-list** | List of host Addresses, multiple hosts can be separated by comma. |  | String |
| **camel.component.elasticsearch-rest-client.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.elasticsearch-rest-client.password** | Password. |  | String |
| **camel.component.elasticsearch-rest-client.rest-client** | Rest Client of type org.elasticsearch.client.RestClient. This is only for advanced usage. The option is a org.elasticsearch.client.RestClient type. |  | RestClient |
| **camel.component.elasticsearch-rest-client.sniff-after-failure-delay** | Sniffer after failure delay (in millis). | 60000 | Integer |
| **camel.component.elasticsearch-rest-client.sniffer-interval** | Sniffer interval (in millis). | 60000 | Integer |
| **camel.component.elasticsearch-rest-client.socket-timeout** | Socket timeout. | 30000 | Integer |
| **camel.component.elasticsearch-rest-client.user** | Username. |  | String |