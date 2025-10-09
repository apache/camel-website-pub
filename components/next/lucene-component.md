# Lucene

**Since Camel 2.2**

**Only producer is supported**

The Lucene component is based on the Apache Lucene project. Apache Lucene is a powerful high-performance, full-featured text search engine library written entirely in Java. For more details about Lucene, please see the following links

-   [http://lucene.apache.org/java/docs/](http://lucene.apache.org/java/docs/)
    
-   [http://lucene.apache.org/java/docs/features.html](http://lucene.apache.org/java/docs/features.md)
    

The lucene component in camel facilitates integration and utilization of Lucene endpoints in enterprise integration patterns and scenarios. The lucene component does the following

-   builds a searchable index of documents when payloads are sent to the Lucene Endpoint
    
-   facilitates performing of indexed searches in Camel
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-lucene</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

lucene:searcherName:insert\[?options\]
lucene:searcherName:query\[?options\]

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

The Lucene component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **analyzer** (producer) | An Analyzer builds TokenStreams, which analyze text. It thus represents a policy for extracting index terms from text. The value for analyzer can be any class that extends the abstract class org.apache.lucene.analysis.Analyzer. Lucene also offers a rich set of analyzers out of the box. |  | Analyzer |
| **indexDir** (producer) | A file system directory in which index files are created upon analysis of the document by the specified analyzer. |  | File |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxHits** (producer) | An integer value that limits the result set of the search operation. |  | int |
| **srcDir** (producer) | An optional directory containing files to be used to be analyzed and added to the index at producer startup. |  | File |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **config** (advanced) | To use a shared lucene configuration. |  | LuceneConfiguration |

## Endpoint Options

The Lucene endpoint is configured using URI syntax:

lucene:host:operation

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** The URL to the lucene server. |  | String |
| **operation** (producer) | 
**Required** Operation to do such as insert or query.

Enum values:

-   insert
    
-   query
    





 |  | LuceneOperation |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **analyzer** (producer) | An Analyzer builds TokenStreams, which analyze text. It thus represents a policy for extracting index terms from text. The value for analyzer can be any class that extends the abstract class org.apache.lucene.analysis.Analyzer. Lucene also offers a rich set of analyzers out of the box. |  | Analyzer |
| **indexDir** (producer) | A file system directory in which index files are created upon analysis of the document by the specified analyzer. |  | File |
| **maxHits** (producer) | An integer value that limits the result set of the search operation. |  | int |
| **srcDir** (producer) | An optional directory containing files to be used to be analyzed and added to the index at producer startup. |  | File |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Lucene component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **QUERY** (producer) Constant: [`HEADER_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-lucene/latest/org/apache/camel/component/lucene/LuceneConstants.html#HEADER_QUERY) | The Lucene Query to performed on the index. The query may include wildcards and phrases. |  | String |
| **RETURN\_LUCENE\_DOCS** (producer) Constant: [`HEADER_RETURN_LUCENE_DOCS`](https://javadoc.io/doc/org.apache.camel/camel-lucene/latest/org/apache/camel/component/lucene/LuceneConstants.html#HEADER_RETURN_LUCENE_DOCS) | Set this header to true to include the actual Lucene documentation when returning hit information. |  | String |

## Usage

### Lucene Producers

This component supports 2 producer endpoints.

**insert**: the insert producer builds a searchable index by analyzing the body in incoming exchanges and associating it with a token ("content"). **query**: the query producer performs searches on a pre-created index. The query uses the searchable index to perform score & relevance based searches. Queries are sent via the incoming exchange contains a header property name called 'QUERY'. The value of the header property 'QUERY' is a Lucene Query. For more details on how to create Lucene Queries, check out [Query Parser Classic syntax](https://lucene.apache.org/core/8_4_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#package.description)

### Lucene Processor

There is a processor called LuceneQueryProcessor available to perform queries against lucene without the need to create a producer.

## Examples

Lucene usage samples.

### Example 1: Creating a Lucene index

```java
RouteBuilder builder = new RouteBuilder() {
    public void configure() {
       from("direct:start").
           to("lucene:whitespaceQuotesIndex:insert?
               analyzer=#whitespaceAnalyzer&indexDir=#whitespace&srcDir=#load_dir").
           to("mock:result");
    }
};
```

### Example 2: Loading properties into the JNDI registry in the Camel Context

```java
CamelContext context = new DefaultCamelContext(createRegistry());
Registry registry = context.getRegistry();
registry.bind("whitespace", new File("./whitespaceIndexDir"));
registry.bind("load_dir", new File("src/test/resources/sources"));
registry.bind("whitespaceAnalyzer", new WhitespaceAnalyzer());
```

### Example 2: Performing searches using a Query Producer

```java
RouteBuilder builder = new RouteBuilder() {
    public void configure() {
       from("direct:start").
          setHeader(LuceneConstants.HEADER_QUERY, constant("Seinfeld")).
          to("lucene:searchIndex:query?
             analyzer=#whitespaceAnalyzer&indexDir=#whitespace&maxHits=20").
          to("direct:next");

       from("direct:next").process(new Processor() {
          public void process(Exchange exchange) throws Exception {
             Hits hits = exchange.getIn().getBody(Hits.class);
             printResults(hits);
          }

          private void printResults(Hits hits) {
              LOG.debug("Number of hits: " + hits.getNumberOfHits());
              for (int i = 0; i < hits.getNumberOfHits(); i++) {
                 LOG.debug("Hit " + i + " Index Location:" + hits.getHit().get(i).getHitLocation());
                 LOG.debug("Hit " + i + " Score:" + hits.getHit().get(i).getScore());
                 LOG.debug("Hit " + i + " Data:" + hits.getHit().get(i).getData());
              }
           }
       }).to("mock:searchResult");
   }
};
```

### Example 3: Performing searches using a Query Processor

```java
RouteBuilder builder = new RouteBuilder() {
    public void configure() {
        try {
            from("direct:start").
                setHeader(LuceneConstants.HEADER_QUERY, constant("Rodney Dangerfield")).
                process(new LuceneQueryProcessor("target/stdindexDir", analyzer, null, 20)).
                to("direct:next");
        } catch (Exception e) {
            e.printStackTrace();
        }

        from("direct:next").process(new Processor() {
            public void process(Exchange exchange) throws Exception {
                Hits hits = exchange.getIn().getBody(Hits.class);
                printResults(hits);
            }

            private void printResults(Hits hits) {
                LOG.debug("Number of hits: " + hits.getNumberOfHits());
                for (int i = 0; i < hits.getNumberOfHits(); i++) {
                    LOG.debug("Hit " + i + " Index Location:" + hits.getHit().get(i).getHitLocation());
                    LOG.debug("Hit " + i + " Score:" + hits.getHit().get(i).getScore());
                    LOG.debug("Hit " + i + " Data:" + hits.getHit().get(i).getData());
                }
            }
       }).to("mock:searchResult");
   }
};
```

## Spring Boot Auto-Configuration

When using lucene with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-lucene-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.lucene.analyzer** | An Analyzer builds TokenStreams, which analyze text. It thus represents a policy for extracting index terms from text. The value for analyzer can be any class that extends the abstract class org.apache.lucene.analysis.Analyzer. Lucene also offers a rich set of analyzers out of the box. The option is a org.apache.lucene.analysis.Analyzer type. |  | Analyzer |
| **camel.component.lucene.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.lucene.config** | To use a shared lucene configuration. The option is a org.apache.camel.component.lucene.LuceneConfiguration type. |  | LuceneConfiguration |
| **camel.component.lucene.enabled** | Whether to enable auto configuration of the lucene component. This is enabled by default. |  | Boolean |
| **camel.component.lucene.index-dir** | A file system directory in which index files are created upon analysis of the document by the specified analyzer. |  | File |
| **camel.component.lucene.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.lucene.max-hits** | An integer value that limits the result set of the search operation. |  | Integer |
| **camel.component.lucene.src-dir** | An optional directory containing files to be used to be analyzed and added to the index at producer startup. |  | File |