# Solr

**Since Camel 4.8**

**Only producer is supported**

The Solr component allows you to interface with an [Apache Solr](https://solr.apache.org/) server.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-solr</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

solr://host\[:port\]?\[options\]

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

The Solr component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionTimeout** (producer) | The time in ms to wait before connection will time out. | 60000 | long |
| **defaultCollection** (producer) | Solr default collection name. |  | String |
| **host** (producer) | The solr instance host name. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **port** (producer) | The solr instance port number. |  | int |
| **requestTimeout** (producer) | The timeout in ms to wait before the socket will time out. | 600000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **solrClient** (advanced) | **Autowired** To use an existing configured solr client, instead of creating a client per endpoint. This allows customizing the client with specific advanced settings. |  | SolrClient |
| **enableSSL** (security) | Enable SSL. | false | boolean |
| **password** (security) | Password for authenticating. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. When configured, this takes precedence over the certificatePath option. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **username** (security) | Basic authenticate user. |  | String |

## Endpoint Options

The Solr endpoint is configured using URI syntax:

solr:host:port/basePath

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** The solr instance host name (set to 'default' to use the host name defined on component level). |  | String |
| **port** (producer) | The solr instance port number. | 8983 | int |
| **basePath** (producer) | The solr instance base path (usually /solr). | /solr | String |

### Query Parameters (17 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **async** (producer) | Use async request processing (when supported by the solr client). | true | boolean |
| **autoCommit** (producer) | If true, each producer insert/delete operation will be automatically performing a commit. | false | boolean |
| **collection** (producer) | The name of the collection to act against. |  | String |
| **connectionTimeout** (producer) | The time in ms to wait before connection will time out. |  | Long |
| **deleteByQuery** (producer) | For the delete instruction, interprete body as query/queries instead of id/ids. | true | boolean |
| **from** (producer) | Starting index of the response. |  | Integer |
| **operation** (producer) | 
What operation to perform.

Enum values:

-   DELETE
    
-   INSERT
    
-   PING
    
-   SEARCH
    





 |  | SolrOperation |
| **requestHandler** (producer) | The path of the update request handler (use for update requests / set solr parameter qt for search requests). |  | String |
| **requestTimeout** (producer) | The time in ms to wait before the request will time out (former soTimeout). |  | Long |
| **size** (producer) | Size of the response. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **solrClient** (advanced) | The solr client to connect to solr. When solrClient bean is provided, all connection properties will be used from that solrClient (host, port, username, password, connectionTimeout, requestTimeout, enableSSL, …​). When not explicitly configured, camel uses the HttpJdkSolrClient. |  | SolrClient |
| **certificatePath** (security) | The certificate that can be used to access the solr host. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **enableSSL** (security) | Enable SSL. | false | boolean |
| **password** (security) | Password for authenticating. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. When configured, this takes precedence over the certificatePath option. This allows configuring named groups, signature schemes, cipher suites, and protocols for the TLS connection. |  | SSLContextParameters |
| **username** (security) | Basic authenticate user. |  | String |

## Message Headers

The Solr component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSolrOperation** (producer) Constant: [`PARAM_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_OPERATION) | The operation to perform. |  | String |
| **CamelSolrCollection** (producer) Constant: [`PARAM_COLLECTION`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_COLLECTION) | The collection to execute the request against. |  | String |
| **CamelSolrRequestHandler** (producer) Constant: [`PARAM_REQUEST_HANDLER`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_REQUEST_HANDLER) | The request handler to execute the solr request against. |  | String |
| **CamelSolrQueryString** (producer) Constant: [`PARAM_QUERY_STRING`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_QUERY_STRING) | The query to execute. |  | String |
| **CamelSolrSize** (producer) Constant: [`PARAM_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_SIZE) | The size of the response. |  | Integer |
| **CamelSolrFrom** (producer) Constant: [`PARAM_FROM`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_FROM) | The starting index of the response. |  | Integer |
| **CamelSolrParams** (producer) Constant: [`PARAM_SOLR_PARAMS`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_SOLR_PARAMS) | The solr parameters to use for the request. |  | SolrParams |
| **CamelSolrDeleteByQuery** (producer) Constant: [`PARAM_DELETE_BY_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_DELETE_BY_QUERY) | For the delete instruction, interpret body as query/queries instead of id/ids. | false | boolean |
| **Content-Type** (producer) Constant: [`PARAM_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#PARAM_CONTENT_TYPE) | The content type is used to identify the type when inserting files. |  | String |

## Usage

### Message Operations

The following Solr operations are currently supported. Set an exchange header with a key of "operation" and a value set to one of the following. Some operations also require the message body to be set.

-   `INSERT`
    
-   `DELETE`
    
-   `SEARCH`
    
-   `PING`
    

  
| Operation | Message body | Description |
| --- | --- | --- |
| `INSERT` | n/a | inserts/updates a document using message headers (solr fields must be prefixed with "CamelSolrField.") |
| `INSERT` | File | inserts/updates a document or documents using the given File (using ContentStreamUpdateRequest) |
| `INSERT` | SolrInputDocument or Collection<SolrInputDocument> | inserts/updates a document or documents based on the given (collection of) SolrInputDocument |
| `INSERT` | bean or Collection<bean> | inserts/updates a document or documents based on values in an [annotated bean](http://wiki.apache.org/solr/Solrj#Directly_adding_POJOs_to_Solr) |
| `INSERT` | String | inserts/updates a document or documents index based on the given XML or json as string (must follow SolrInputDocument format) |
| `DELETE` | String or Collection<String> | delete a record by ID (or collection of ids) or by a query (or a collection of queries) when header "deleteByQuery=true" |
| `PING` | SolrPing | Pings the solr instance |
| `SEARCH` | SolrQuery | Performs a search request to the solr instance |
| `SEARCH` | QueryRequest | Performs a search request to the solr instance |

## Example

Below is a simple `INSERT`, `DELETE` and `SEARCH` example

```java
from("direct:insert")
    .setHeader(SolrConstants.PARAM_OPERATION, constant(SolrOperation.INSERT))
    .setHeader(SolrConstants.FIELD + "id", body())
    .to("solr://localhost:8983/solr");

from("direct:delete")
    .setHeader(SolrConstants.PARAM_OPERATION, constant(SolrOperation.DELETE))
    .to("solr://localhost:8983/solr");

from("direct:search")
    .setHeader(SolrConstants.PARAM_OPERATION, constant(SolrOperation.SEARCH))
    .to("solr://localhost:8983/solr");
```

```xml
<route>
    <from uri="direct:insert"/>
    <setHeader name="CamelSolrOperation">
        <constant>INSERT</constant>
    </setHeader>
    <setHeader name="CamelSolrField.id">
        <simple>${body}</simple>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
<route>
    <from uri="direct:delete"/>
    <setHeader name="CamelSolrOperation">
        <constant>DELETE</constant>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
<route>
    <from uri="direct:search"/>
    <setHeader name="CamelSolrOperation">
        <constant>SEARCH</constant>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
```

A client would simply need to pass a body message to the insert or delete routes and then call the commit route.

```java
template.sendBodyAndHeader("direct:insert", "1234", "CamelSolrParam.commit", true);
template.sendBodyAndHeader("direct:delete", "1234", "CamelSolrParam.commit", true);
template.sendBody("direct:search", "id:1234");
```

For more information:

[Apache Solr Reference Guide](https://solr.apache.org/guide/solr/latest/)

## Spring Boot Auto-Configuration

When using solr with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-solr-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.solr.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.solr.connection-timeout** | The time in ms to wait before connection will time out. | 60000 | Long |
| **camel.component.solr.default-collection** | Solr default collection name. |  | String |
| **camel.component.solr.enable-s-s-l** | Enable SSL. | false | Boolean |
| **camel.component.solr.enabled** | Whether to enable auto configuration of the solr component. This is enabled by default. |  | Boolean |
| **camel.component.solr.host** | The solr instance host name. |  | String |
| **camel.component.solr.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.solr.password** | Password for authenticating. |  | String |
| **camel.component.solr.port** | The solr instance port number. |  | Integer |
| **camel.component.solr.request-timeout** | The timeout in ms to wait before the socket will time out. | 600000 | Long |
| **camel.component.solr.solr-client** | To use an existing configured solr client, instead of creating a client per endpoint. This allows customizing the client with specific advanced settings. The option is a org.apache.solr.client.solrj.SolrClient type. |  | SolrClient |
| **camel.component.solr.username** | Basic authenticate user. |  | String |