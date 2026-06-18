# OpenSearch

**Since Camel 4.0**

**Only producer is supported**

The OpenSearch component allows you to interface with an [OpenSearch](https://opensearch.org/) 3.x API using the Java API Client library.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-opensearch</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

opensearch://clusterName\[?options\]

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

The OpenSearch component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | The time in ms to wait before connection will time out. | 30000 | int |
| **hostAddresses** (producer) | Comma separated list with ip:port formatted remote transport addresses to use. The ip and port options must be left blank for hostAddresses to be considered instead. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxRetryTimeout** (producer) | The time in ms before retry. | 30000 | int |
| **socketTimeout** (producer) | The timeout in ms to wait before the socket will time out. | 30000 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | **Autowired** To use an existing configured OpenSearch client, instead of creating a client per endpoint. This allows customizing the client with specific settings. |  | RestClient |
| **enableSniffer** (advanced) | Enable automatically discover nodes from a running OpenSearch cluster. If this option is used in conjunction with Spring Boot, then it’s managed by the Spring Boot configuration (see: Disable Sniffer in Spring Boot). | false | boolean |
| **sniffAfterFailureDelay** (advanced) | The delay of a sniff execution scheduled after a failure (in milliseconds). | 60000 | int |
| **snifferInterval** (advanced) | The interval between consecutive ordinary sniff executions in milliseconds. Will be honoured when sniffOnFailure is disabled or when there are no failures between consecutive sniff executions. | 300000 | int |
| **enableSSL** (security) | Enable SSL. | false | boolean |
| **password** (security) | Password for authenticating. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. When configured, this takes precedence over the certificatePath option. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **user** (security) | Basic authenticate user. |  | String |

## Endpoint Options

The OpenSearch endpoint is configured using URI syntax:

opensearch:clusterName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterName** (producer) | **Required** Name of the cluster. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | The time in ms to wait before connection will time out. | 30000 | int |
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
    
-   GetById
    
-   MultiGet
    
-   MultiSearch
    
-   Delete
    
-   DeleteIndex
    
-   Search
    
-   Exists
    
-   Ping
    





 |  | OpensearchOperation |
| **scrollKeepAliveMs** (producer) | Time in ms during which OpenSearch will keep search context alive. | 60000 | int |
| **size** (producer) | Size of the response. |  | Integer |
| **socketTimeout** (producer) | The timeout in ms to wait before the socket will time out. | 30000 | int |
| **useScroll** (producer) | Enable scroll usage. | false | boolean |
| **waitForActiveShards** (producer) | Index creation waits for the write consistency number of shards to be available. | 1 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **documentClass** (advanced) | The class to use when deserializing the documents. | ObjectNode | Class |
| **enableSniffer** (advanced) | Enable automatically discover nodes from a running OpenSearch cluster. If this option is used in conjunction with Spring Boot, then it’s managed by the Spring Boot configuration (see: Disable Sniffer in Spring Boot). | false | boolean |
| **hostnameVerifier** (advanced) | The class to use as HostnameVerifier. By default there is no HostnameVerifier. |  | HostnameVerifier |
| **sniffAfterFailureDelay** (advanced) | The delay of a sniff execution scheduled after a failure (in milliseconds). | 60000 | int |
| **snifferInterval** (advanced) | The interval between consecutive ordinary sniff executions in milliseconds. Will be honoured when sniffOnFailure is disabled or when there are no failures between consecutive sniff executions. | 300000 | int |
| **certificatePath** (security) | The certificate that can be used to access the ES Cluster. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **enableSSL** (security) | Enable SSL. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. When configured, this takes precedence over the certificatePath option. This allows configuring named groups, signature schemes, cipher suites, and protocols for the TLS connection. |  | SSLContextParameters |

## Message Headers

The OpenSearch component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpensearchOperation** (producer) Constant: [`PARAM_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_OPERATION) | 
The operation to perform.

Enum values:

-   Index
    
-   Update
    
-   Bulk
    
-   GetById
    
-   MultiGet
    
-   MultiSearch
    
-   Delete
    
-   DeleteIndex
    
-   Search
    
-   Exists
    
-   Ping
    





 |  | OpensearchOperation |
| **CamelOpensearchIndexId** (producer) Constant: [`PARAM_INDEX_ID`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_INDEX_ID) | The id of the indexed document. |  | String |
| **CamelOpensearchIndexName** (producer) Constant: [`PARAM_INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_INDEX_NAME) | The name of the index to act against. |  | String |
| **CamelOpensearchDocumentClass** (producer) Constant: [`PARAM_DOCUMENT_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_DOCUMENT_CLASS) | The full qualified name of the class of the document to unmarshall. | ObjectNode | Class |
| **CamelOpensearchWaitForActiveShards** (producer) Constant: [`PARAM_WAIT_FOR_ACTIVE_SHARDS`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_WAIT_FOR_ACTIVE_SHARDS) | The index creation waits for the write consistency number of shards to be available. |  | Integer |
| **CamelOpensearchScrollKeepAliveMs** (producer) Constant: [`PARAM_SCROLL_KEEP_ALIVE_MS`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_SCROLL_KEEP_ALIVE_MS) | The starting index of the response. |  | Integer |
| **CamelOpensearchUseScroll** (producer) Constant: [`PARAM_SCROLL`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_SCROLL) | Set to true to enable scroll usage. When enabled, the body is returned as a OpensearchScrollRequestIterator. Make sure to use the stream and close it accordingly to avoid potential resource leaks. |  | Boolean |
| **CamelOpensearchSize** (producer) Constant: [`PARAM_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_SIZE) | The size of the response. |  | Integer |
| **CamelOpensearchFrom** (producer) Constant: [`PARAM_FROM`](https://javadoc.io/doc/org.apache.camel/camel-opensearch/latest/org/apache/camel/component/opensearch/OpensearchConstants.html#PARAM_FROM) | The starting index of the response. |  | Integer |

## Usage

### Message Operations

The following [OpenSearch](https://opensearch.org/) operations are currently supported. Set an endpoint URI option or exchange header with a key of "operation" and a value set to one of the following. Some operations also require other parameters or the message body to be set.

  
| operation | message body | description |
| --- | --- | --- |
| `Index` | `Map`, `String`, `byte[]`, `Reader`, `InputStream` or `IndexRequest.Builder` content to index | Adds content to an index and returns the content’s indexId in the body. You can set the name of the target index by setting the message header with the key "indexName". You can set the indexId by setting the message header with the key "indexId". |
| `GetById` | `String` or `GetRequest.Builder` index id of content to retrieve | Retrieves the document corresponding to the given index id and returns a GetResponse object in the body. You can set the name of the target index by setting the message header with the key "indexName". You can set the type of document by setting the message header with the key "documentClass". |
| `Delete` | `String` or `DeleteRequest.Builder` index id of content to delete | Deletes the specified indexName and returns a Result object in the body. You can set the name of the target index by setting the message header with the key "indexName". |
| `DeleteIndex` | `String` or `DeleteIndexRequest.Builder` index name of the index to delete | Deletes the specified indexName and returns a status code in the body. You can set the name of the target index by setting the message header with the key "indexName". |
| `Bulk` `Iterable` or `BulkRequest.Builder` of any type that is already accepted (DeleteOperation.Builder for delete operation, UpdateOperation.Builder for update operation, CreateOperation.Builder for create operation, byte\[\], InputStream, String, Reader, Map or any document type for index operation) | Adds/Updates/Deletes content from/to an index and returns a List<BulkResponseItem> object in the body You can set the name of the target index by setting the message header with the key "indexName". | `Search` |
| `Map`, `String` or `SearchRequest.Builder` | Search the content with the map of query string. You can set the name of the target index by setting the message header with the key "indexName". You can set the number of hits to return by setting the message header with the key "size". You can set the starting document offset by setting the message header with the key "from". | `MultiSearch` |
| `MsearchRequest.Builder` | Multiple search in one | `MultiGet` |
| `Iterable<String>` or `MgetRequest.Builder` the id of the document to retrieve | Multiple get in one You can set the name of the target index by setting the message header with the key "indexName". | `Exists` |
| None | Checks whether the index exists or not and returns a Boolean flag in the body. You must set the name of the target index by setting the message header with the key "indexName". | `Update` |
| `byte[]`, `InputStream`, `String`, `Reader`, `Map` or any document type content to update | Updates content to an index and returns the content’s indexId in the body. You can set the name of the target index by setting the message header with the key "indexName". You can set the indexId by setting the message header with the key "indexId". | Ping |

### Configure the component and enable basic authentication

To use the OpenSearch component, it has to be configured with a minimum configuration.

_Java-only: programmatic CamelContext configuration_

```java
OpensearchComponent opensearchComponent = new OpensearchComponent();
opensearchComponent.setHostAddresses("opensearch-host:9200");
camelContext.addComponent("opensearch", opensearchComponent);
```

For basic authentication with OpenSearch or using reverse http proxy in front of the OpenSearch cluster, simply setup basic authentication and SSL on the component like the example below

_Java-only: programmatic CamelContext configuration_

```java
OpenSearchComponent opensearchComponent = new OpenSearchComponent();
opensearchComponent.setHostAddresses("opensearch-host:9200");
opensearchComponent.setUser("opensearchuser");
opensearchComponent.setPassword("secure!!");

camelContext.addComponent("opensearch", opensearchComponent);
```

### Document type

For all the search operations, it is possible to indicate the type of document to retrieve to get the result already unmarshalled with the expected type.

The document type can be set using the header "documentClass" or via the uri parameter of the same name.

## Examples

### Index Example

Below is a simple INDEX example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:index")
    .to("opensearch://opensearch?operation=Index&indexName=twitter");
```

```xml
<route>
    <from uri="direct:index"/>
    <to uri="opensearch://opensearch?operation=Index&amp;indexName=twitter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:index
      steps:
        - to:
            uri: opensearch://opensearch
            parameters:
              operation: Index
              indexName: twitter
```

> **Note**
> For this operation, you’ll need to specify an indexId header.

A client would simply need to pass a body message containing a Map to the route. The result body contains the indexId created.

_Java-only: Java test API (ProducerTemplate)_

```java
Map<String, String> map = new HashMap<String, String>();
map.put("content", "test");
String indexId = template.requestBody("direct:index", map, String.class);
```

### Search Example

Searching on specific field(s) and value use the Operation ´Search´. Pass in the query JSON String or the Map

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:search")
    .to("opensearch://opensearch?operation=Search&indexName=twitter");
```

```xml
<route>
    <from uri="direct:search"/>
    <to uri="opensearch://opensearch?operation=Search&amp;indexName=twitter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:search
      steps:
        - to:
            uri: opensearch://opensearch
            parameters:
              operation: Search
              indexName: twitter
```

_Java-only: Java test API (ProducerTemplate)_

```java
String query = "{\"query\":{\"match\":{\"doc.content\":\"new release of ApacheCamel\"}}}";
HitsMetadata<?> response = template.requestBody("direct:search", query, HitsMetadata.class);
```

Search on specific field(s) using Map.

_Java-only: Java test API (ProducerTemplate)_

```java
Map<String, Object> actualQuery = new HashMap<>();
actualQuery.put("doc.content", "new release of ApacheCamel");

Map<String, Object> match = new HashMap<>();
match.put("match", actualQuery);

Map<String, Object> query = new HashMap<>();
query.put("query", match);
HitsMetadata<?> response = template.requestBody("direct:search", query, HitsMetadata.class);
```

Search using OpenSearch scroll api to fetch all results.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:search")
    .to("opensearch://opensearch?operation=Search&indexName=twitter&useScroll=true&scrollKeepAliveMs=30000");
```

```xml
<route>
    <from uri="direct:search"/>
    <to uri="opensearch://opensearch?operation=Search&amp;indexName=twitter&amp;useScroll=true&amp;scrollKeepAliveMs=30000"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:search
      steps:
        - to:
            uri: opensearch://opensearch
            parameters:
              operation: Search
              indexName: twitter
              useScroll: true
              scrollKeepAliveMs: 30000
```

_Java-only: Java test API (ProducerTemplate)_

```java
String query = "{\"query\":{\"match\":{\"doc.content\":\"new release of ApacheCamel\"}}}";
try (OpenSearchScrollRequestIterator response = template.requestBody("direct:search", query, OpenSearchScrollRequestIterator.class)) {
    // do something smart with results
}
```

[Split EIP](eips/split-eip.md) can also be used.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:search")
  .to("opensearch://opensearch?operation=Search&indexName=twitter&useScroll=true&scrollKeepAliveMs=30000")
  .split()
  .body()
  .streaming()
  .to("mock:output")
  .end();
```

```xml
<route>
  <from uri="direct:search"/>
  <to uri="opensearch://opensearch?operation=Search&amp;indexName=twitter&amp;useScroll=true&amp;scrollKeepAliveMs=30000"/>
  <split streaming="true">
    <simple>${body}</simple>
    <to uri="mock:output"/>
  </split>
</route>
```

```yaml
- route:
    from:
      uri: direct:search
      steps:
        - to:
            uri: opensearch://opensearch
            parameters:
              operation: Search
              indexName: twitter
              useScroll: true
              scrollKeepAliveMs: 30000
        - split:
            simple: "${body}"
            streaming: true
            steps:
              - to:
                  uri: mock:output
```

### MultiSearch Example

MultiSearching on specific field(s) and value uses the Operation `MultiSearch`. Pass in the MultiSearchRequest instance

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:multiSearch")
    .to("opensearch://opensearch?operation=MultiSearch");
```

```xml
<route>
    <from uri="direct:multiSearch"/>
    <to uri="opensearch://opensearch?operation=MultiSearch"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:multiSearch
      steps:
        - to:
            uri: opensearch://opensearch
            parameters:
              operation: MultiSearch
```

MultiSearch on specific field(s)

_Java-only: Java SDK builder API (ProducerTemplate)_

```java
MsearchRequest.Builder builder = new MsearchRequest.Builder().index("twitter").searches(
        new RequestItem.Builder().header(new MultisearchHeader.Builder().build())
                .body(new MultisearchBody.Builder().query(b -> b.matchAll(x -> x)).build()).build(),
        new RequestItem.Builder().header(new MultisearchHeader.Builder().build())
                .body(new MultisearchBody.Builder().query(b -> b.matchAll(x -> x)).build()).build());
List<MultiSearchResponseItem<?>> response = template.requestBody("direct:multiSearch", builder, List.class);
```