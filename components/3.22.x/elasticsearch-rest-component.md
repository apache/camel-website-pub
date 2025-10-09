# Elasticsearch Rest

> **Warning**
> **Deprecated:** This elasticsearch-rest is deprecated and may be removed in a future release.

**Since Camel 2.21**

**Only producer is supported**

The ElasticSearch component allows you to interface with an [ElasticSearch](https://www.elastic.co/products/elasticsearch) 6.x API using the REST Client library.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-elasticsearch-rest</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

elasticsearch-rest://clusterName\[?options\]

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

The Elasticsearch Rest component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | The time in ms to wait before connection will timeout. | 30000 | int |
| **hostAddresses** (producer) | Comma separated list with ip:port formatted remote transport addresses to use. The ip and port options must be left blank for hostAddresses to be considered instead. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxRetryTimeout** (producer) | The time in ms before retry. | 30000 | int |
| **socketTimeout** (producer) | The timeout in ms to wait before the socket will timeout. | 30000 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | **Autowired** To use an existing configured Elasticsearch client, instead of creating a client per endpoint. This allows to customize the client with specific settings. |  | RestClient |
| **enableSniffer** (advanced) | Enable automatically discover nodes from a running Elasticsearch cluster. If this option is used in conjunction with Spring Boot then it’s managed by the Spring Boot configuration (see: Disable Sniffer in Spring Boot). | false | boolean |
| **sniffAfterFailureDelay** (advanced) | The delay of a sniff execution scheduled after a failure (in milliseconds). | 60000 | int |
| **snifferInterval** (advanced) | The interval between consecutive ordinary sniff executions in milliseconds. Will be honoured when sniffOnFailure is disabled or when there are no failures between consecutive sniff executions. | 300000 | int |
| **enableSSL** (security) | Enable SSL. | false | boolean |
| **password** (security) | Password for authenticate. |  | String |
| **user** (security) | Basic authenticate user. |  | String |

## Endpoint Options

The Elasticsearch Rest endpoint is configured using URI syntax:

elasticsearch-rest:clusterName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterName** (producer) | **Required** Name of the cluster. |  | String |

### Query Parameters (17 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | The time in ms to wait before connection will timeout. | 30000 | int |
| **disconnect** (producer) | Disconnect after it finish calling the producer. | false | boolean |
| **from** (producer) | Starting index of the response. |  | Integer |
| **hostAddresses** (producer) | Comma separated list with ip:port formatted remote transport addresses to use. |  | String |
| **indexName** (producer) | The name of the index to act against. |  | String |
| **maxRetryTimeout** (producer) | The time in ms before retry. | 30000 | int |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   Index
    
-   Update
    
-   Bulk
    
-   BulkIndex
    
-   GetById
    
-   MultiGet
    
-   MultiSearch
    
-   Delete
    
-   DeleteIndex
    
-   Search
    
-   Exists
    
-   Ping
    





 |  | ElasticsearchOperation |
| **scrollKeepAliveMs** (producer) | Time in ms during which elasticsearch will keep search context alive. | 60000 | int |
| **size** (producer) | Size of the response. |  | Integer |
| **socketTimeout** (producer) | The timeout in ms to wait before the socket will timeout. | 30000 | int |
| **useScroll** (producer) | Enable scroll usage. | false | boolean |
| **waitForActiveShards** (producer) | Index creation waits for the write consistency number of shards to be available. | 1 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **enableSniffer** (advanced) | Enable automatically discover nodes from a running Elasticsearch cluster. If this option is used in conjunction with Spring Boot then it’s managed by the Spring Boot configuration (see: Disable Sniffer in Spring Boot). | false | boolean |
| **sniffAfterFailureDelay** (advanced) | The delay of a sniff execution scheduled after a failure (in milliseconds). | 60000 | int |
| **snifferInterval** (advanced) | The interval between consecutive ordinary sniff executions in milliseconds. Will be honoured when sniffOnFailure is disabled or when there are no failures between consecutive sniff executions. | 300000 | int |
| **enableSSL** (security) | Enable SSL. | false | boolean |

## Message Headers

The Elasticsearch Rest component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) Constant: [`PARAM_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_OPERATION) | 
The operation to perform.

Enum values:

-   Index
    
-   Update
    
-   Bulk
    
-   BulkIndex
    
-   GetById
    
-   MultiGet
    
-   MultiSearch
    
-   Delete
    
-   DeleteIndex
    
-   Search
    
-   Exists
    
-   Ping
    





 |  | ElasticsearchOperation |
| **indexId** (producer) Constant: [`PARAM_INDEX_ID`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_INDEX_ID) | The id of the indexed document. |  | String |
| **indexName** (producer) Constant: [`PARAM_INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_INDEX_NAME) | The name of the index to act against. |  | String |
| **waitForActiveShards** (producer) Constant: [`PARAM_WAIT_FOR_ACTIVE_SHARDS`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_WAIT_FOR_ACTIVE_SHARDS) | The index creation waits for the write consistency number of shards to be available. |  | Integer |
| **scrollKeepAliveMs** (producer) Constant: [`PARAM_SCROLL_KEEP_ALIVE_MS`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_SCROLL_KEEP_ALIVE_MS) | The starting index of the response. |  | Integer |
| **useScroll** (producer) Constant: [`PARAM_SCROLL`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_SCROLL) | Set to true to enable scroll usage. |  | Boolean |
| **size** (producer) Constant: [`PARAM_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_SIZE) | The size of the response. |  | Integer |
| **from** (producer) Constant: [`PARAM_FROM`](https://javadoc.io/doc/org.apache.camel/camel-elasticsearch-rest/latest/org/apache/camel/component/elasticsearch/ElasticsearchConstants.html#PARAM_FROM) | The starting index of the response. |  | Integer |

## Message Operations

The following ElasticSearch operations are currently supported. Simply set an endpoint URI option or exchange header with a key of "operation" and a value set to one of the following. Some operations also require other parameters or the message body to be set.

  
| operation | message body | description |
| --- | --- | --- |
| Index | **Map**, **String**, **byte\[\]**, **XContentBuilder** or **IndexRequest** content to index | Adds content to an index and returns the content’s indexId in the body. You can set the indexId by setting the message header with the key "indexId". |
| GetById | **String** or **GetRequest** index id of content to retrieve | Retrieves the specified index and returns a GetResult object in the body |
| Delete | **String** or **DeleteRequest** index name and type of content to delete | Deletes the specified indexName and returns a DeleteResponse object in the body |
| DeleteIndex | **String** or **DeleteRequest** index name of the index to delete | Deletes the specified indexName and returns a status code the body |
| BulkIndex | a **List**, **BulkRequest**, or **Collection** of any type that is already accepted (XContentBuilder, Map, byte\[\], String) | Adds content to an index and return a List of the id of the successfully indexed documents in the body |
| Bulk | a **List**, **BulkRequest**, or **Collection** of any type that is already accepted (XContentBuilder, Map, byte\[\], String) | Adds content to an index and returns the BulkItemResponse\[\] object in the body |
| Search | **Map**, **String** or **SearchRequest** | Search the content with the map of query string |
| MultiSearch | **MultiSearchRequest** | Multiple search in one |
| Exists | Index name(indexName) as header | Checks the index exists or not and returns a Boolean flag in the body |
| Update | **Map**, **UpdateRequest**, **String**, **byte\[\]** or **XContentBuilder** content to update | Updates content to an index and returns the content’s indexId in the body. |
| Ping | None | Pings the remote Elasticsearch cluster and returns true if the ping succeeded, false otherwise |

## Configure the component and enable basic authentication

To use the Elasticsearch component it has to be configured with a minimum configuration.

```java
ElasticsearchComponent elasticsearchComponent = new ElasticsearchComponent();
elasticsearchComponent.setHostAddresses("myelkhost:9200");
camelContext.addComponent("elasticsearch-rest", elasticsearchComponent);
```

For basic authentication with elasticsearch or using reverse http proxy in front of the elasticsearch cluster, simply setup basic authentication and SSL on the component like the example below

```java
ElasticsearchComponent elasticsearchComponent = new ElasticsearchComponent();
elasticsearchComponent.setHostAddresses("myelkhost:9200");
elasticsearchComponent.setUser("elkuser");
elasticsearchComponent.setPassword("secure!!");
elasticsearchComponent.setEnableSSL(true);

camelContext.addComponent("elasticsearch-rest", elasticsearchComponent);
```

## Index Example

Below is a simple INDEX example

```java
from("direct:index")
  .to("elasticsearch-rest://elasticsearch?operation=Index&indexName=twitter");
```

```xml
<route>
    <from uri="direct:index"/>
    <to uri="elasticsearch-rest://elasticsearch?operation=Index&amp;indexName=twitter"/>
</route>
```

**For this operation you’ll need to specify a indexId header.**

A client would simply need to pass a body message containing a Map to the route. The result body contains the indexId created.

```java
Map<String, String> map = new HashMap<String, String>();
map.put("content", "test");
String indexId = template.requestBody("direct:index", map, String.class);
```

## Search Example

Searching on specific field(s) and value use the Operation ´Search´. Pass in the query JSON String or the Map

```java
from("direct:search")
  .to("elasticsearch-rest://elasticsearch?operation=Search&indexName=twitter");
```

```xml
<route>
    <from uri="direct:search"/>
    <to uri="elasticsearch-rest://elasticsearch?operation=Search&amp;indexName=twitter"/>
</route>
```

```java
String query = "{\"query\":{\"match\":{\"content\":\"new release of ApacheCamel\"}}}";
SearchHits response = template.requestBody("direct:search", query, SearchHits.class);
```

Search on specific field(s) using Map.

```java
Map<String, Object> actualQuery = new HashMap<>();
actualQuery.put("content", "new release of ApacheCamel");

Map<String, Object> match = new HashMap<>();
match.put("match", actualQuery);

Map<String, Object> query = new HashMap<>();
query.put("query", match);
SearchHits response = template.requestBody("direct:search", query, SearchHits.class);
```

Search using Elasticsearch scroll api in order to fetch all results.

```java
from("direct:search")
  .to("elasticsearch-rest://elasticsearch?operation=Search&indexName=twitter&useScroll=true&scrollKeepAliveMs=30000");
```

```xml
<route>
    <from uri="direct:search"/>
    <to uri="elasticsearch-rest://elasticsearch?operation=Search&amp;indexName=twitter&amp;useScroll=true&amp;scrollKeepAliveMs=30000"/>
</route>
```

```java
String query = "{\"query\":{\"match\":{\"content\":\"new release of ApacheCamel\"}}}";
try (ElasticsearchScrollRequestIterator response = template.requestBody("direct:search", query, ElasticsearchScrollRequestIterator.class)) {
    // do something smart with results
}
```

[Split EIP](eips/split-eip.md) can also be used.

```java
from("direct:search")
  .to("elasticsearch-rest://elasticsearch?operation=Search&indexName=twitter&useScroll=true&scrollKeepAliveMs=30000")
  .split()
  .body()
  .streaming()
  .to("mock:output")
  .end();
```

## MultiSearch Example

MultiSearching on specific field(s) and value use the Operation ´MultiSearch´. Pass in the MultiSearchRequest instance

```java
from("direct:multiSearch")
  .to("elasticsearch-rest://elasticsearch?operation=MultiSearch");
```

```xml
<route>
    <from uri="direct:multiSearch"/>
    <to uri="elasticsearch-rest://elasticsearch?operation=MultiSearch"/>
</route>
```

MultiSearch on specific field(s)

```java
SearchRequest req = new SearchRequest();
req.indices("twitter");
SearchRequest req1 = new SearchRequest();
req.indices("twitter");
MultiSearchRequest request = new MultiSearchRequest().add(req1).add(req);
Item[] response = template.requestBody("direct:search", request, Item[].class);
```

## Disable Sniffer when using Spring Boot

When Spring Boot is on the classpath the Sniffer client for Elasticsearch is enabled by default. This option can be disabled in the Spring Boot Configuration:

```yaml
spring:
  autoconfigure:
    exclude: org.springframework.boot.autoconfigure.elasticsearch.ElasticsearchRestClientAutoConfiguration
```

## Spring Boot Auto-Configuration

When using elasticsearch-rest with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-elasticsearch-rest-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.elasticsearch-rest.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.elasticsearch-rest.client** | To use an existing configured Elasticsearch client, instead of creating a client per endpoint. This allows to customize the client with specific settings. The option is a org.elasticsearch.client.RestClient type. |  | RestClient |
| **camel.component.elasticsearch-rest.connection-timeout** | The time in ms to wait before connection will timeout. | 30000 | Integer |
| **camel.component.elasticsearch-rest.enable-s-s-l** | Enable SSL. | false | Boolean |
| **camel.component.elasticsearch-rest.enable-sniffer** | Enable automatically discover nodes from a running Elasticsearch cluster. If this option is used in conjunction with Spring Boot then it’s managed by the Spring Boot configuration (see: Disable Sniffer in Spring Boot). | false | Boolean |
| **camel.component.elasticsearch-rest.enabled** | Whether to enable auto configuration of the elasticsearch-rest component. This is enabled by default. |  | Boolean |
| **camel.component.elasticsearch-rest.host-addresses** | Comma separated list with ip:port formatted remote transport addresses to use. The ip and port options must be left blank for hostAddresses to be considered instead. |  | String |
| **camel.component.elasticsearch-rest.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.elasticsearch-rest.max-retry-timeout** | The time in ms before retry. | 30000 | Integer |
| **camel.component.elasticsearch-rest.password** | Password for authenticate. |  | String |
| **camel.component.elasticsearch-rest.sniff-after-failure-delay** | The delay of a sniff execution scheduled after a failure (in milliseconds). | 60000 | Integer |
| **camel.component.elasticsearch-rest.sniffer-interval** | The interval between consecutive ordinary sniff executions in milliseconds. Will be honoured when sniffOnFailure is disabled or when there are no failures between consecutive sniff executions. | 300000 | Integer |
| **camel.component.elasticsearch-rest.socket-timeout** | The timeout in ms to wait before the socket will timeout. | 30000 | Integer |
| **camel.component.elasticsearch-rest.user** | Basic authenticate user. |  | String |