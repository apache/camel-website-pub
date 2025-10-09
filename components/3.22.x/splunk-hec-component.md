# Splunk HEC

**Since Camel 3.3**

**Only producer is supported**

The Splunk HEC component allows to send data to Splunk using the [HTTP Event Collector](https://dev.splunk.com/enterprise/docs/dataapps/httpeventcollector/).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-splunk-hec</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

splunk-hec:\[endpoint\]/\[token\]?\[options\]

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

The Splunk HEC component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Splunk HEC endpoint is configured using URI syntax:

splunk-hec:splunkURL/token

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **splunkURL** (producer) | **Required** Splunk Host and Port (example: my\_splunk\_server:8089). |  | String |
| **token** (security) | **Required** Splunk HEC token (this is the token created for HEC and not the user’s token). |  | String |

### Query Parameters (11 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bodyOnly** (producer) | Send only the message body. | false | boolean |
| **headersOnly** (producer) | Send only message headers. | false | boolean |
| **host** (producer) | Splunk host field of the event message. This is not the Splunk host to connect to. |  | String |
| **index** (producer) | Splunk index to write to. | camel | String |
| **source** (producer) | Splunk source argument. | camel | String |
| **sourceType** (producer) | Splunk sourcetype argument. | camel | String |
| **splunkEndpoint** (producer) | Splunk endpoint Defaults to /services/collector/event To write RAW data like JSON use /services/collector/raw For a list of all endpoints refer to splunk documentation (HTTP Event Collector REST API endpoints) Example for Spunk 8.2.x: [https://docs.splunk.com/Documentation/SplunkCloud/8.2.2203/Data/HECRESTendpoints](https://docs.splunk.com/Documentation/SplunkCloud/8.2.2203/Data/HECRESTendpoints) To extract timestamps in Splunk8.0 /services/collector/eventauto\_extract\_timestamp=true Remember to utilize RAW\\{} for questionmarks or slashes in parameters. | /services/collector/event | String |
| **time** (producer) | Time this even occurred. By default, the time will be when this event hits the splunk server. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **https** (security) | Contact HEC over https. | true | boolean |
| **skipTlsVerify** (security) | Splunk HEC TLS verification. | false | boolean |

## Message Headers

The Splunk HEC component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSplunkHECIndexTime** (producer) Constant: [`INDEX_TIME`](https://javadoc.io/doc/org.apache.camel/camel-splunk-hec/latest/org/apache/camel/component/splunkhec/SplunkHECConstants.html#INDEX_TIME) | Epoch-formatted time. Specify with the time query string parameter. Sets a default for all events in the request. The default time can be overridden. |  | Long |

## Message body

The body must be serializable to JSON so it may be sent to Splunk.

A `String` or a `java.util.Map` object can be serialized easily.

## Use Cases

The Splunk HEC endpoint may be used to stream data to Splunk for ingestion.

It is meant for high volume ingestion of machine data.

## Configuring the index time

By default, the index time for an event is when the event makes it to the Splunk server.

```java
from("direct:start")
        .to("splunk-hec://localhost:8080?token");
```

If you are ingesting a large enough dataset with a big enough lag then the time the event hits the server and when that event actually happened could be skewed. If you want to override the index time you can do so.

```java
from("kafka:logs")
        .setHeader(SplunkHECConstants.INDEX_TIME, simple("${headers[kafka.HEADERS].lastKey('TIME')}"))
        .to("splunk-hec://localhost:8080/token");
```

```java
from("kafka:logs")
        .toD("splunk-hec://localhost:8080/token?time=${headers[kafka.HEADERS].lastKey('TIME')}");
```

## Spring Boot Auto-Configuration

When using splunk-hec with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-splunk-hec-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.splunk-hec.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.splunk-hec.enabled** | Whether to enable auto configuration of the splunk-hec component. This is enabled by default. |  | Boolean |
| **camel.component.splunk-hec.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |