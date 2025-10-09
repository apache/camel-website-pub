# Solr

> **Warning**
> **Deprecated:** This solr is deprecated and may be removed in a future release.

**Since Camel 2.9**

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

solr://host\[:port\]/solr?\[options\]
solrs://host\[:port\]/solr?\[options\]
solrCloud://host\[:port\]/solr?\[options\]

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

The Solr component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Solr endpoint is configured using URI syntax:

solr:url

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **url** (producer) | **Required** Hostname and port for the Solr server(s). Multiple hosts can be specified, separated with a comma. See the solrClient parameter for more information on the SolrClient used to connect to Solr. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCommit** (producer) | If true, each producer operation will be automatically followed by a commit. | false | boolean |
| **connectionTimeout** (producer) | Sets the connection timeout on the SolrClient. |  | Integer |
| **defaultMaxConnectionsPerHost** (producer) | **Deprecated** maxConnectionsPerHost on the underlying HttpConnectionManager. |  | Integer |
| **httpClient** (producer) | Sets the http client to be used by the solrClient. This is only applicable when solrClient is not set. |  | HttpClient |
| **maxRetries** (producer) | **Deprecated** Maximum number of retries to attempt in the event of transient errors. |  | Integer |
| **maxTotalConnections** (producer) | **Deprecated** maxTotalConnection on the underlying HttpConnectionManager. |  | Integer |
| **requestHandler** (producer) | Set the request handler to be used. |  | String |
| **solrClient** (producer) | Uses the provided solr client to connect to solr. When this parameter is not specified, camel applies the following rules to determine the SolrClient: 1) when zkHost or zkChroot (=zookeeper root) parameter is set, then the CloudSolrClient is used. 2) when multiple hosts are specified in the uri (separated with a comma), then the CloudSolrClient (uri scheme is 'solrCloud') or the LBHttpSolrClient (uri scheme is not 'solrCloud') is used. 3) when the solr operation is INSERT\_STREAMING, then the ConcurrentUpdateSolrClient is used. 4) otherwise, the HttpSolrClient is used. Note: A CloudSolrClient should point to zookeeper endpoint(s); other clients point to Solr endpoint(s). The SolrClient can also be set via the exchange header 'CamelSolrClient'. |  | SolrClient |
| **soTimeout** (producer) | Sets the socket timeout on the SolrClient. |  | Integer |
| **streamingQueueSize** (producer) | Sets the queue size for the ConcurrentUpdateSolrClient. | 10 | int |
| **streamingThreadCount** (producer) | Sets the number of threads for the ConcurrentUpdateSolrClient. | 2 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **collection** (CloudSolrClient) | Set the default collection for SolrCloud. |  | String |
| **zkChroot** (CloudSolrClient) | Set the chroot of the zookeeper connection (include the leading slash; e.g. '/mychroot'). |  | String |
| **zkHost** (CloudSolrClient) | Set the ZooKeeper host(s) urls which the CloudSolrClient uses, e.g. zkHost=localhost:2181,localhost:2182. Optionally add the chroot, e.g. zkHost=localhost:2181,localhost:2182/rootformysolr. In case the first part of the url path (='contextroot') is set to 'solr' (e.g. 'localhost:2181/solr' or 'localhost:2181/solr/..'), then that path is not considered as zookeeper chroot for backward compatibility reasons (this behaviour can be overridden via zkChroot parameter). |  | String |
| **allowCompression** (HttpSolrClient) | Server side must support gzip or deflate for this to have any effect. |  | Boolean |
| **followRedirects** (HttpSolrClient) | Indicates whether redirects are used to get to the Solr server. |  | Boolean |
| **password** (security) | Sets password for basic auth plugin enabled servers. |  | String |
| **username** (security) | Sets username for basic auth plugin enabled servers. |  | String |

## Message Headers

The Solr component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSolrClient** (producer) Constant: [`CLIENT`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#CLIENT) | The client. |  | SolrClient |
| **CamelSolrCollection** (producer) Constant: [`COLLECTION`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#COLLECTION) | The collection to execute the request again. |  | String |
| **SolrOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelSolrQueryString** (producer) Constant: [`QUERY_STRING`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#QUERY_STRING) | The query to execute. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-solr/latest/org/apache/camel/component/solr/SolrConstants.html#CONTENT_TYPE) | The content type. |  | String |

## Message Operations

The following Solr operations are currently supported. Simply set an exchange header with a key of "SolrOperation" and a value set to one of the following. Some operations also require the message body to be set.

-   INSERT
    
-   INSERT\_STREAMING
    

  
| Operation | Message body | Description |
| --- | --- | --- |
| INSERT/INSERT\_STREAMING | n/a | adds an index using message headers (must be prefixed with "SolrField.") |
| INSERT/INSERT\_STREAMING | File | adds an index using the given File (using ContentStreamUpdateRequest) |
| INSERT/INSERT\_STREAMING | SolrInputDocument | updates index based on the given SolrInputDocument |
| INSERT/INSERT\_STREAMING | String XML | updates index based on the given XML (must follow SolrInputDocument format) |
| ADD\_BEAN | bean instance | adds an index based on values in an [annotated bean](http://wiki.apache.org/solr/Solrj#Directly_adding_POJOs_to_Solr) |
| ADD\_BEANS | collection<bean> | adds index based on a collection of [annotated bean](http://wiki.apache.org/solr/Solrj#Directly_adding_POJOs_to_Solr) |
| DELETE\_BY\_ID | index id to delete | delete a record by ID |
| DELETE\_BY\_QUERY | query string | delete a record by a query |
| COMMIT | n/a | performs a commit on any pending index changes |
| SOFT\_COMMIT | n/a | performs a `soft commit` (without guarantee that Lucene index files are written to stable storage; useful for Near Real Time operations) on any pending index changes |
| ROLLBACK | n/a | performs a rollback on any pending index changes |
| OPTIMIZE | n/a | performs a commit on any pending index changes and then runs the optimize command (This command reorganizes the Solr index and might be a heavy task) |

## Example

Below is a simple INSERT, DELETE and COMMIT example

```java
from("direct:insert")
    .setHeader(SolrConstants.OPERATION, constant(SolrConstants.OPERATION_INSERT))
    .setHeader(SolrConstants.FIELD + "id", body())
    .to("solr://localhost:8983/solr");

from("direct:delete")
    .setHeader(SolrConstants.OPERATION, constant(SolrConstants.OPERATION_DELETE_BY_ID))
    .to("solr://localhost:8983/solr");

from("direct:commit")
    .setHeader(SolrConstants.OPERATION, constant(SolrConstants.OPERATION_COMMIT))
    .to("solr://localhost:8983/solr");
```

```xml
<route>
    <from uri="direct:insert"/>
    <setHeader name="SolrOperation">
        <constant>INSERT</constant>
    </setHeader>
    <setHeader name="SolrField.id">
        <simple>${body}</simple>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
<route>
    <from uri="direct:delete"/>
    <setHeader name="SolrOperation">
        <constant>DELETE_BY_ID</constant>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
<route>
    <from uri="direct:commit"/>
    <setHeader name="SolrOperation">
        <constant>COMMIT</constant>
    </setHeader>
    <to uri="solr://localhost:8983/solr"/>
</route>
```

A client would simply need to pass a body message to the insert or delete routes and then call the commit route.

```java
template.sendBody("direct:insert", "1234");
template.sendBody("direct:commit", null);
template.sendBody("direct:delete", "1234");
template.sendBody("direct:commit", null);
```

## Querying Solr

The components provide a producer operation to query Solr.

For more information:

[Solr Query Syntax](https://solr.apache.org/guide/8_8/the-standard-query-parser.md)

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

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.solr.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.solr.enabled** | Whether to enable auto configuration of the solr component. This is enabled by default. |  | Boolean |
| **camel.component.solr.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |