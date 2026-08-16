# Alibaba EventBridge

**Since Camel 4.23**

**Only producer is supported**

The Alibaba Cloud EventBridge component allows you to publish CloudEvents to an EventBridge event bus.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-eventbridge</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
alibaba-eventbridge:operation[?options]
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

The Alibaba EventBridge component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba EventBridge endpoint is configured using URI syntax:

alibaba-eventbridge:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** Operation to perform.

Enum values:

-   putEvents
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | EventBridge endpoint URL. Carries higher precedence than region based client initialization. |  | String |
| **eventBusName** (producer) | Default event bus name. |  | String |
| **eventSource** (producer) | Default event source. |  | String |
| **eventSubject** (producer) | Default event subject. |  | String |
| **eventType** (producer) | Default event type. |  | String |
| **region** (producer) | **Required** Alibaba Cloud region. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **eventBridgeClient** (advanced) | **Autowired** Autowire an existing EventBridge client instance. |  | EventBridgeClient |
| **accessKey** (security) | Access key for the cloud user. |  | String |
| **secretKey** (security) | Secret key for the cloud user. |  | String |
| **serviceKeys** (security) | Configuration object for cloud service authentication. |  | ServiceKeys |

## Message Headers

The Alibaba EventBridge component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaEventBridgeEventBusName** (producer) Constant: [`EVENT_BUS_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#EVENT_BUS_NAME) | Event bus name override. |  | String |
| **CamelAlibabaEventBridgeEventSource** (producer) Constant: [`EVENT_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#EVENT_SOURCE) | Event source override. |  | String |
| **CamelAlibabaEventBridgeEventType** (producer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#EVENT_TYPE) | Event type override. |  | String |
| **CamelAlibabaEventBridgeEventSubject** (producer) Constant: [`EVENT_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#EVENT_SUBJECT) | Event subject override. |  | String |
| **CamelAlibabaEventBridgeRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#REQUEST_ID) | Alibaba Cloud request id. |  | String |

## Usage

### Operations

The component supports the following operations:

-   `putEvents` - publish one or more CloudEvents (producer)
    

### Producer example

```java
from("direct:start")
    .setBody(constant("{\"orderId\":\"123\"}"))
    .to("alibaba-eventbridge:putEvents?eventBusName=my-bus&eventSource=camel.test&eventType=OrderCreated&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-eventbridge` module.