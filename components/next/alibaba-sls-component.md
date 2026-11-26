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
**Required** The operation that the producer performs. The CamelAlibabaSlsOperation header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option.

Enum values:

-   putLogs
    
-   getLogs
    
-   listLogStores
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | The endpoint of Simple Log Service, which is a host name without http:// or https://, for example cn-hangzhou.log.aliyuncs.com. The producer sends requests over HTTPS to the endpoint, with the name of the project in front of it. If not set, the region option determines the endpoint, and one of the two is required. Not used when the slsClient option is set or autowired. |  | String |
| **logStoreName** (producer) | The name of the Logstore for putLogs and getLogs. The producer writes the logs to this Logstore for putLogs, and queries its logs for getLogs. The CamelAlibabaSlsLogStoreName header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required for putLogs and getLogs. |  | String |
| **project** (producer) | The name of the project. The CamelAlibabaSlsProject header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **region** (producer) | The region ID of Simple Log Service, for example cn-hangzhou. Only used when the endpoint option is not set, to build the endpoint of Simple Log Service. Not used when the slsClient option is set or autowired. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **slsClient** (advanced) | **Autowired** To use a custom com.aliyun.sls20201230.Client. The producer sends its requests with this client, and the region, endpoint, accessKey, secretKey and serviceKeys options are not used. If no client is set or autowired, the Camel endpoint creates a client from these options. It creates this client when the producer processes its first message. |  | Client |
| **from** (getLogs) | The start time for getLogs, as a Unix timestamp in seconds. Simple Log Service requires a start time. The CamelAlibabaSlsFrom header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no start time to the request. |  | Integer |
| **line** (getLogs) | The maximum number of logs to return for getLogs. Simple Log Service accepts a value of at most 100. Simple Log Service does not use it when query contains an analytic statement. The CamelAlibabaSlsLine header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no maximum number of logs to the request. |  | Long |
| **offset** (getLogs) | The offset of the first log to return for getLogs. Simple Log Service does not use it when query contains an analytic statement. The CamelAlibabaSlsOffset header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no offset to the request. |  | Long |
| **query** (getLogs) | The search statement or analytic statement for getLogs. The CamelAlibabaSlsQuery header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no search statement or analytic statement to the request. |  | String |
| **reverse** (getLogs) | Whether to return logs in descending order of log timestamps for getLogs. Simple Log Service does not use it when query contains an analytic statement. The CamelAlibabaSlsReverse header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no sort order to the request. |  | Boolean |
| **to** (getLogs) | The end time for getLogs, as a Unix timestamp in seconds. Simple Log Service requires an end time. The CamelAlibabaSlsTo header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no end time to the request. |  | Integer |
| **topic** (getLogs) | The log topic for getLogs. The CamelAlibabaSlsTopic header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no log topic to the request. |  | String |
| **accessKey** (security) | The AccessKey ID of the AccessKey pair for the requests that the producer sends to Simple Log Service. If not set, the accessKey of the serviceKeys option is used, and one of the two is required. Not used when the slsClient option is set or autowired. |  | String |
| **secretKey** (security) | The AccessKey secret of the AccessKey pair for the requests that the producer sends to Simple Log Service. If not set, the secretKey of the serviceKeys option is used, and one of the two is required. Not used when the slsClient option is set or autowired. |  | String |
| **serviceKeys** (security) | The AccessKey pair as an org.apache.camel.component.alibaba.common.models.ServiceKeys. Its accessKey is the AccessKey ID and its secretKey is the AccessKey secret. Each of the two is used when the option of the same name is not set. Not used when the slsClient option is set or autowired. |  | ServiceKeys |

## Message Headers

The Alibaba Simple Log Service (SLS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaSlsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#OPERATION) | 
The operation that the producer performs. This header replaces the operation option. If this header is not set, an exchange property of the same name replaces the operation option.

Enum values:

-   putLogs
    
-   getLogs
    
-   listLogStores
    





 |  | String |
| **CamelAlibabaSlsProject** (producer) Constant: [`PROJECT`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#PROJECT) | The name of the project. This header replaces the project option. If this header is not set, an exchange property of the same name replaces the project option. |  | String |
| **CamelAlibabaSlsLogStoreName** (producer) Constant: [`LOG_STORE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LOG_STORE_NAME) | The name of the Logstore for putLogs and getLogs. The producer writes the logs to this Logstore for putLogs, and queries its logs for getLogs. This header replaces the logStoreName option. If this header is not set, an exchange property of the same name replaces the logStoreName option. |  | String |
| **CamelAlibabaSlsQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#QUERY) | The search statement or analytic statement for getLogs. This header replaces the query option. If this header is not set, an exchange property of the same name replaces the query option. |  | String |
| **CamelAlibabaSlsFrom** (producer) Constant: [`FROM`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#FROM) | The start time for getLogs, as a Unix timestamp in seconds. Simple Log Service requires a start time. This header replaces the from option. If this header is not set, an exchange property of the same name replaces the from option. |  | Integer |
| **CamelAlibabaSlsTo** (producer) Constant: [`TO`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TO) | The end time for getLogs, as a Unix timestamp in seconds. Simple Log Service requires an end time. This header replaces the to option. If this header is not set, an exchange property of the same name replaces the to option. |  | Integer |
| **CamelAlibabaSlsLine** (producer) Constant: [`LINE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LINE) | The maximum number of logs to return for getLogs. Simple Log Service accepts a value of at most 100. Simple Log Service does not use it when query contains an analytic statement. This header replaces the line option. If this header is not set, an exchange property of the same name replaces the line option. |  | Long |
| **CamelAlibabaSlsOffset** (producer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#OFFSET) | The offset of the first log to return for getLogs. Simple Log Service does not use it when query contains an analytic statement. This header replaces the offset option. If this header is not set, an exchange property of the same name replaces the offset option. |  | Long |
| **CamelAlibabaSlsTopic** (producer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TOPIC) | The log topic for getLogs. This header replaces the topic option. If this header is not set, an exchange property of the same name replaces the topic option. |  | String |
| **CamelAlibabaSlsReverse** (producer) Constant: [`REVERSE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#REVERSE) | Whether to return logs in descending order of log timestamps for getLogs. Simple Log Service does not use it when query contains an analytic statement. This header replaces the reverse option. If this header is not set, an exchange property of the same name replaces the reverse option. |  | Boolean |
| **CamelAlibabaSlsListLogStoreName** (producer) Constant: [`LOGSTORE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LOGSTORE_NAME) | The name of the Logstore for listLogStores. Simple Log Service returns the Logstores whose name contains the value. If this header is not set, the producer uses an exchange property of the same name. If neither of the two is set, the producer adds no Logstore name to the request. |  | String |
| **CamelAlibabaSlsMode** (producer) Constant: [`MODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#MODE) | The type of the Logstore for listLogStores. The value must be standard or query. If this header is not set, the producer uses an exchange property of the same name. If neither of the two is set, the producer adds no Logstore type to the request. |  | String |
| **CamelAlibabaSlsSize** (producer) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#SIZE) | The number of entries per page for listLogStores. Simple Log Service accepts a value of at most 500. If this header is not set, the producer uses an exchange property of the same name. If neither of the two is set, the producer adds no number of entries per page to the request. |  | Integer |
| **CamelAlibabaSlsListOffset** (producer) Constant: [`LIST_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#LIST_OFFSET) | The offset of the first Logstore to return for listLogStores. If this header is not set, the producer uses an exchange property of the same name. If neither of the two is set, the producer adds no offset to the request. |  | Integer |
| **CamelAlibabaSlsTelemetryType** (producer) Constant: [`TELEMETRY_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#TELEMETRY_TYPE) | The telemetry type for listLogStores. The value must be None for logs or Metrics for metrics. If this header is not set, the producer uses an exchange property of the same name. If neither of the two is set, the producer adds no telemetry type to the request. |  | String |
| **CamelAlibabaSlsRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#REQUEST_ID) | The request ID that Simple Log Service returns in the response to the operation. The producer sets it when the response has one. |  | String |
| **CamelAlibabaSlsStatusCode** (producer) Constant: [`STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sls/latest/org/apache/camel/component/alibaba/sls/constants/AlibabaSlsHeaders.html#STATUS_CODE) | The HTTP status code of the response to the operation. The producer sets it, unless the exchange fails. |  | Integer |

## Message Body

The message body at each side of the Alibaba Simple Log Service (SLS) component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
The logs to write for putLogs: a LogGroup or a PutLogsRequest of the SLS SDK, any other body fails. getLogs and listLogStores do not read the body, they take their input from options and headers.

-   With `operation=putLogs`: `pojo`
    





 |
| **Producer output** | `map` | A Map of the response with its statusCode and headers. For getLogs the GetLogsResponseBody of the SLS SDK is under body, for listLogStores the names under logstores with count and total. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Operations

The component supports the following operations:

-   `putLogs` - write a log group to a log store (producer)
    
-   `getLogs` - query logs from a log store (producer)
    
-   `listLogStores` - list log stores in a project (producer)
    

### Producer examples

Put logs, where the message body must be a `LogGroup` or a `PutLogsRequest` of the SLS SDK: any other body, such as text, fails. Each log of a log group has a time, in seconds since the epoch, and its fields as `LogContent` keys and values. A bean can build the log group, such as this one, which writes the text of the message as one log, under the key `message`:

```java
package com.example;

import java.time.Instant;
import java.util.List;

import com.aliyun.sls20201230.models.LogContent;
import com.aliyun.sls20201230.models.LogGroup;
import com.aliyun.sls20201230.models.LogItem;

public class SlsLogs {

    public LogGroup toLogGroup(String message) {
        LogItem log = new LogItem()
                .setTime((int) Instant.now().getEpochSecond())
                .setContents(List.of(new LogContent().setKey("message").setValue(message)));
        return new LogGroup().setTopic("camel").setLogItems(List.of(log));
    }
}
```

The route calls the bean before `putLogs`:

-   Java
    
-   YAML
    

```java
from("direct:start")
    .bean(SlsLogs.class, "toLogGroup")
    .to("alibaba-sls:putLogs?project=my-project&logStoreName=my-logstore&region=cn-hangzhou&endpoint=cn-hangzhou.log.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - bean:
            beanType: com.example.SlsLogs
            method: toLogGroup
        - to:
            uri: alibaba-sls:putLogs
            parameters:
              project: my-project
              logStoreName: my-logstore
              endpoint: cn-hangzhou.log.aliyuncs.com
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

Query logs:

-   Java
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAlibabaSlsQuery", constant("*"))
    .setHeader("CamelAlibabaSlsFrom", constant(1700000000))
    .setHeader("CamelAlibabaSlsTo", constant(1700003600))
    .to("alibaba-sls:getLogs?project=my-project&logStoreName=my-logstore&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAlibabaSlsQuery
            expression:
              constant:
                expression: "*"
        - setHeader:
            name: CamelAlibabaSlsFrom
            expression:
              constant:
                expression: "1700000000"
        - setHeader:
            name: CamelAlibabaSlsTo
            expression:
              constant:
                expression: "1700003600"
        - to:
            uri: alibaba-sls:getLogs
            parameters:
              project: my-project
              logStoreName: my-logstore
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

List log stores:

-   Java
    
-   YAML
    

```java
from("direct:start")
    .to("alibaba-sls:listLogStores?project=my-project&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: alibaba-sls:listLogStores
            parameters:
              project: my-project
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-sls` module.