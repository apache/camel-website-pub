# Alibaba Simple Log Service (SLS)

**Since Camel 4.23**

**Only producer is supported**

The Alibaba Cloud Simple Log Service (SLS) component allows you to write logs, query logs and list log stores.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-sls</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
alibaba-sls:operation[?options]
```

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

The Alibaba Simple Log Service (SLS) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Simple Log Service (SLS) endpoint is configured using URI syntax:

alibaba-sls:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation to perform.

Enum values:

-   putLogs
    
-   getLogs
    
-   listLogStores
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | SLS endpoint URL (e.g. cn-hangzhou.log.aliyuncs.com). Carries higher precedence than region based client initialization. |  | String |
| **logStoreName** (producer) | SLS log store name. |  | String |
| **project** (producer) | SLS project name. |  | String |
| **region** (producer) | Alibaba Cloud region. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **slsClient** (advanced) | **Autowired** Autowire an existing SLS client instance. |  | Client |
| **from** (getLogs) | Query start time for getLogs (Unix timestamp in seconds). |  | Integer |
| **line** (getLogs) | Maximum number of log lines to return for getLogs. |  | Long |
| **offset** (getLogs) | Log query offset for getLogs. |  | Long |
| **query** (getLogs) | Log query string for getLogs. |  | String |
| **reverse** (getLogs) | Whether to return logs in reverse order for getLogs. | false | Boolean |
| **to** (getLogs) | Query end time for getLogs (Unix timestamp in seconds). |  | Integer |
| **topic** (getLogs) | Log topic filter for getLogs. |  | String |
| **accessKey** (security) | Access key for the cloud user. |  | String |
| **secretKey** (security) | Secret key for the cloud user. |  | String |
| **serviceKeys** (security) | Configuration object for cloud service authentication. |  | ServiceKeys |

## Message Headers

The Alibaba Simple Log Service (SLS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaSlsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#OPERATION) | Operation override. |  | String |
| **CamelAlibabaSlsProject** (producer) Constant: [`PROJECT`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#PROJECT) | SLS project name override. |  | String |
| **CamelAlibabaSlsLogStoreName** (producer) Constant: [`LOG_STORE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LOG_STORE_NAME) | SLS log store name override. |  | String |
| **CamelAlibabaSlsQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#QUERY) | Log query string override. |  | String |
| **CamelAlibabaSlsFrom** (producer) Constant: [`FROM`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#FROM) | Query start time override (Unix timestamp in seconds). |  | Integer |
| **CamelAlibabaSlsTo** (producer) Constant: [`TO`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TO) | Query end time override (Unix timestamp in seconds). |  | Integer |
| **CamelAlibabaSlsLine** (producer) Constant: [`LINE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LINE) | Maximum number of log lines to return. |  | Long |
| **CamelAlibabaSlsOffset** (producer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#OFFSET) | Log query offset. |  | Long |
| **CamelAlibabaSlsTopic** (producer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TOPIC) | Log topic filter override. |  | String |
| **CamelAlibabaSlsReverse** (producer) Constant: [`REVERSE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#REVERSE) | Whether to return logs in reverse order. |  | Boolean |
| **CamelAlibabaSlsLogstoreName** (producer) Constant: [`LOGSTORE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LOGSTORE_NAME) | Log store name prefix filter for listLogStores. |  | String |
| **CamelAlibabaSlsMode** (producer) Constant: [`MODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#MODE) | List mode for listLogStores. |  | String |
| **CamelAlibabaSlsSize** (producer) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#SIZE) | Page size for listLogStores. |  | Integer |
| **CamelAlibabaSlsListOffset** (producer) Constant: [`LIST_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LIST_OFFSET) | Pagination offset for listLogStores. |  | Integer |
| **CamelAlibabaSlsTelemetryType** (producer) Constant: [`TELEMETRY_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TELEMETRY_TYPE) | Telemetry type filter for listLogStores. |  | String |
| **CamelAlibabaSlsRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#REQUEST_ID) | Alibaba Cloud request id. |  | String |
| **CamelAlibabaSlsStatusCode** (producer) Constant: [`STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#STATUS_CODE) | HTTP status code from SLS response. |  | Integer |

## Usage

### Operations

The component supports the following operations:

-   `putLogs` - write a log group to a log store (producer)
    
-   `getLogs` - query logs from a log store (producer)
    
-   `listLogStores` - list log stores in a project (producer)
    

### Producer examples

Put logs:

```java
from("direct:start")
    .setBody(simple("${body}"))
    .to("alibaba-sls:putLogs?project=my-project&logStoreName=my-logstore&region=cn-hangzhou&endpoint=cn-hangzhou.log.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

Query logs:

```java
from("direct:start")
    .setHeader("CamelAlibabaSlsQuery", constant("*"))
    .setHeader("CamelAlibabaSlsFrom", constant(1700000000))
    .setHeader("CamelAlibabaSlsTo", constant(1700003600))
    .to("alibaba-sls:getLogs?project=my-project&logStoreName=my-logstore&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

List log stores:

```java
from("direct:start")
    .to("alibaba-sls:listLogStores?project=my-project&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-sls` module.