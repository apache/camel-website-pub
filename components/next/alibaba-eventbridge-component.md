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
| **allowedEventSources** (producer) | Allowed event sources and source-scoped event types per event bus. Supports multi-bus DSL (bussrc - type1,type2), single-bus shorthand (src - type1,type2), JSON string, or Map/List objects. |  | String |
| **endpoint** (producer) | EventBridge endpoint URL. Carries higher precedence than region based client initialization. |  | String |
| **eventBusName** (producer) | Default event bus name. |  | String |
| **eventSource** (producer) | Default event source. |  | String |
| **eventSubject** (producer) | Default event subject. |  | String |
| **eventType** (producer) | Default event type. |  | String |
| **region** (producer) | **Required** Alibaba Cloud region. |  | String |
| **validateEventSource** (producer) | When true, verifies that the target event bus exists in Alibaba Cloud EventBridge using listEventBuses before publishing. Also validates the CloudEvent source URI against the allowedEventSources whitelist when that option is set. | false | boolean |
| **validateEventSpec** (producer) | Validate CloudEvents 1.0 specification constraints on map fields. | true | boolean |
| **validateEventType** (producer) | When true, verifies that the CloudEvent event type is valid for the event source on the target event bus against Alibaba Cloud rule filter patterns before publishing. | false | boolean |
| **eventSourceCacheTtl** (producer (advanced)) | TTL in milliseconds for caching event bus existence lookups per bus name. Applies only when validateEventSource is true. | 300000 | long |
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
| **CamelAlibabaEventBridgeValidateEventSource** (producer) Constant: [`VALIDATE_EVENT_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#VALIDATE_EVENT_SOURCE) | Validate event source against Alibaba Cloud EventBridge. |  | Boolean |
| **CamelAlibabaEventBridgeValidateEventType** (producer) Constant: [`VALIDATE_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#VALIDATE_EVENT_TYPE) | Validate event type against Alibaba Cloud EventBridge rule filter patterns. |  | Boolean |
| **CamelAlibabaEventBridgeValidateEventSpec** (producer) Constant: [`VALIDATE_EVENT_SPEC`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#VALIDATE_EVENT_SPEC) | Validate CloudEvents 1.0 specification constraints on map fields. |  | Boolean |
| **CamelAlibabaEventBridgeAllowedEventSources** (producer) Constant: [`ALLOWED_EVENT_SOURCES`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#ALLOWED_EVENT_SOURCES) | Allowed event sources and source-scoped event types per event bus (DSL string, JSON, Map, or List). |  | Object |
| **CamelAlibabaEventBridgeEventSourceCacheTtl** (producer) Constant: [`EVENT_SOURCE_CACHE_TTL`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#EVENT_SOURCE_CACHE_TTL) | TTL in milliseconds for cached bus event sources and types. |  | Long |
| **CamelAlibabaEventBridgeRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-eventbridge/latest/org/apache/camel/component/alibaba/eventbridge/constants/AlibabaEventBridgeHeaders.html#REQUEST_ID) | Alibaba Cloud request id. |  | String |

## Usage

### Message Headers and Properties

The component defines constants in package `org.apache.camel.component.alibaba.eventbridge.constants`:

-   `AlibabaEventBridgeHeaders` defines all message header constants evaluated or set by the EventBridge producer.
    
-   `AlibabaEventBridgeProperties` extends `AlibabaEventBridgeHeaders` and provides constants for Exchange properties (such as `OPERATION`), while inheriting all header constants.
    

#### Message headers evaluated by the EventBridge producer

   
| Constant (`AlibabaEventBridgeHeaders`) | Header String | Type | Description |
| --- | --- | --- | --- |
| `EVENT_BUS_NAME` | `CamelAlibabaEventBridgeEventBusName` | `String` | Event bus name to publish events to (overrides the endpoint option). |
| `EVENT_SOURCE` | `CamelAlibabaEventBridgeEventSource` | `String` | Event source URI (overrides the endpoint option). |
| `EVENT_TYPE` | `CamelAlibabaEventBridgeEventType` | `String` | Event type (overrides the endpoint option). |
| `EVENT_SUBJECT` | `CamelAlibabaEventBridgeEventSubject` | `String` | Event subject (overrides the endpoint option). |
| `VALIDATE_EVENT_SOURCE` | `CamelAlibabaEventBridgeValidateEventSource` | `boolean` | Whether to validate the event bus and event source against Alibaba Cloud. |
| `VALIDATE_EVENT_TYPE` | `CamelAlibabaEventBridgeValidateEventType` | `boolean` | Whether to validate the event type against Alibaba Cloud rule filter patterns for that source. |
| `VALIDATE_EVENT_SPEC` | `CamelAlibabaEventBridgeValidateEventSpec` | `boolean` | Whether to enforce CloudEvents 1.0 specification compliance checks (defaults to `true`). |
| `ALLOWED_EVENT_SOURCES` | `CamelAlibabaEventBridgeAllowedEventSources` | `Object` | Allowed event sources and source-scoped event types per bus (DSL string, JSON string, Map, or List). |
| `EVENT_SOURCE_CACHE_TTL` | `CamelAlibabaEventBridgeEventSourceCacheTtl` | `long` | Cache time-to-live in milliseconds for verified Alibaba Cloud event bus and type metadata (defaults to `300000` / 5 minutes). |

If any of the above headers are set, they will override their corresponding exchange property or query parameter value.

#### Message headers set by the EventBridge producer

   
| Constant (`AlibabaEventBridgeHeaders`) | Header String | Type | Description |
| --- | --- | --- | --- |
| `REQUEST_ID` | `CamelAlibabaEventBridgeRequestId` | `String` | Alibaba Cloud request ID returned by EventBridge. |

#### Exchange properties

   
| Constant (`AlibabaEventBridgeProperties`) | Property String | Type | Description |
| --- | --- | --- | --- |
| `OPERATION` | `CamelAlibabaEventBridgeOperation` | `String` | Name of operation to invoke (e.g. `putEvents`). Inherits all constants from `AlibabaEventBridgeHeaders`. |

### Event payload Map keys evaluated by the producer

When the message body is a `Map` (or `List<Map>` for publishing batch events), the producer validates and converts the Map into CloudEvents. Both Alibaba EventBridge dictionary keys and standard CloudEvents 1.0 specification keys are supported:

   
| Alibaba Key | CloudEvents Key | Type | Description |
| --- | --- | --- | --- |
| `eventBusName` | \- | `String` | Target event bus name (overrides header or endpoint option). |
| `eventSource` | `source` | `String` / `URI` | Event source identifier (e.g., `acs:oss:cn-hangzhou:12345:my-bucket` or `my.custom.service`). |
| `eventType` | `type` | `String` | Event type identifier (e.g., `oss:ObjectCreated:PutObject` or `OrderCreated`). |
| `eventSubject` | `subject` | `String` | Event subject / topic identifier. |
| `eventData` | `data` | `Object` | Event payload data (serialized to JSON string if passed as a Map, POJO, or primitive). |
| \- | `id` | `String` | Unique event identifier (optional; auto-generated UUID if omitted). Cannot be blank if provided. |
| \- | `time` | `String` / `Date` / `Instant` | Event timestamp in RFC 3339 / ISO-8601 format (e.g., `2026-08-23T10:15:30Z`), `Date`, or `Instant`. |
| \- | `specversion` | `String` | CloudEvents specification version. Must be `1.0` if specified. |
| \- | `datacontenttype` | `String` | Media type of event data (e.g. `application/json`). |
| \- | `dataschema` | `String` / `URI` | URI identifying the schema that data adheres to. |

### Event Validation and Caching

The component supports a 3-level hierarchical validation model: `EventBus (N) → EventSources (N specific to that EventBus) → EventTypes (N specific to that EventSource)`

**Cloud Validation with Cache (`validateEventSource` and `validateEventType`):**

-   **Validated Cache Update Workflow**: When validation is enabled, the component queries `listEventBuses` and `listRules` on Alibaba Cloud EventBridge.
    
-   **Fail-Closed Semantics**: If Alibaba Cloud API calls fail (network errors, permission errors, rate limits) or if target buses/rules are missing, validation fails closed immediately and throws an `IllegalArgumentException` to prevent unvalidated events from being published during outages.
    
-   **Prefix and Exact Match Rules**: Rule ``filterPattern`s are inspected for both exact match strings and prefix patterns (``{"prefix": "…​"}\`) for both event sources and event types.
    
-   **Verified Cache Population**: Only after cloud verification succeeds is the verified metadata stored in `EventSourceCache` for the configured TTL (defaults to `eventSourceCacheTtl=300000`, or per-message via `CamelAlibabaEventBridgeEventSourceCacheTtl`).
    

**Whitelist Validation (`allowedEventSources`):**

-   Statically validates that the event bus, source URI, and event type in outgoing CloudEvents conform to a configured whitelist.
    
-   Restricts publishing to only authorized event sources and event types per event bus.
    
-   Supports single-bus shorthand, multi-bus DSL, JSON string format, and Java objects (`Map` / `List`).
    

### Security Considerations and Untrusted Ingress

> **Important**
> In Apache Camel’s security model, Camel message headers take precedence over endpoint URI options.
>
> When building routes that accept untrusted external ingress (such as HTTP endpoints, webhooks, or public messaging queues), external messages may carry `CamelAlibabaEventBridge*` headers that could override endpoint-level security policies (such as `allowedEventSources` or validation toggles).
>
> To prevent untrusted callers from manipulating security policies, always sanitize or remove Camel headers before forwarding to the Alibaba EventBridge producer:
>
> ```java
> from("platform-http:/ingress")
>     .removeHeaders("CamelAlibabaEventBridge*")
>     .to("alibaba-eventbridge:putEvents?eventBusName=orders-bus&allowedEventSources=RAW(app.orders -> order:created:v1)&region=cn-hangzhou");
> ```

### Allowed Event Sources Configuration

The `allowedEventSources` option (and the `CamelAlibabaEventBridgeAllowedEventSources` header) allows you to define fine-grained whitelists for event buses, event sources, and source-scoped event types.

 
| Format | Description and Syntax |
| --- | --- |
| **Single-Bus Shorthand DSL** | 
Configures allowed sources and types for the default event bus (or wildcard `*`):

```text
source1 -> type1, type2; source2 -> type3
```

-   Uses `→` or `=` as the mapping operator between source and comma-separated event types.
    
-   Multiple sources are separated with semicolons (`;`).
    
-   If event types are omitted (e.g. `source1; source2 → type3`), any event type is allowed for `source1`.
    
-   Sources containing scheme colons or port numbers (e.g. `[http://example.com:8080/events](http://example.com:8080/events)` or `urn:custom:source`) are supported without conflict because type mapping is performed exclusively via `→` and `=`.
    





 |
| **Multi-Bus DSL** | 

Scopes allowed event sources and event types per specific event bus:

```text
bus1[source1 -> type1, type2; source2 -> type3] | bus2[source3 -> type4]
```

-   Each bus block is designated by `busName[…​]`.
    
-   Multiple bus blocks are separated by pipe (`|`).
    
-   Multiple sources within a bus block are separated with semicolons (`;`).
    
-   The producer dynamically matches each outgoing event’s bus against its corresponding bus block.
    





 |
| **JSON String Configuration** | Defines hierarchical multi-bus or single-bus whitelists via JSON: \* **Multi-bus JSON structure**: Top-level keys are event bus names, mapping to child objects of `source → [types]`. \* **Single-bus JSON structure**: Flat object of `source → [types]` applied to the default bus. \* Types can be specified as a JSON array (`["type1", "type2"]`) or a comma-separated string (`"type1, type2"`). |
| **Java Objects / Registry** | Programmatically configure using: \* `Map<String, Map<String, Collection<String>>>` (Bus → Source → Types) \* `Map<String, Collection<String>>` (Source → Types under default bus) \* `List<AllowedEventBus>` or `List<AllowedEventSource>` models. |

#### Single-Bus Configuration

When your route publishes to a single event bus (specified via `eventBusName` or endpoint URI), you can use the single-bus shorthand DSL or flat JSON format:

**Shorthand DSL syntax:**

```text
acs:oss:cn-hangzhou:12345:my-bucket -> oss:ObjectCreated:PutObject, oss:ObjectCreated:PostObject; app.orders -> order:created:v1
```

In the endpoint URI (using `RAW(…​)` to preserve special characters):

```text
alibaba-eventbridge:putEvents?eventBusName=my-bus&allowedEventSources=RAW(acs:oss:cn-hangzhou:12345:my-bucket -> oss:ObjectCreated:PutObject, oss:ObjectCreated:PostObject; app.orders -> order:created:v1)&region=cn-hangzhou&accessKey=RAW(ak)&secretKey=RAW(sk)
```

#### Multi-Bus Configuration

When your route publishes events or batches spanning multiple distinct event buses, use the multi-bus DSL syntax to isolate permissions per bus:

**Multi-Bus DSL syntax:**

```text
orders-bus[acs:oss:cn-hangzhou:12345:orders -> oss:ObjectCreated:PutObject; app.orders -> order:created:v1] | payments-bus[app.payments -> payment:authorized:v1, payment:captured:v1]
```

**Multi-Bus DSL Grammar and Components:**

-   **Bus Scopes**: Each bus definition is enclosed in square brackets: `busName[…​]`.
    
-   **Bus Separator**: Pipe (`|`) separates multiple bus scope definitions.
    
-   **Source Separator**: Semicolon (`;`) separates multiple sources within a bus scope.
    
-   **Event Type Mapping**: Arrow (`→`) or equals (`=`) maps a source to its allowed comma-separated event types. Sources containing colons (such as URI ports or URNs) are supported without conflict.
    
-   **Wildcard Fallback**: Use `*[…​]` to match any event bus not explicitly named.
    
-   **Omitted Types**: If event types are omitted for a source (e.g. `orders-bus[app.orders]`), any event type is permitted for that source.
    

**In the endpoint URI:**

```text
alibaba-eventbridge:putEvents?allowedEventSources=RAW(orders-bus[acs:oss:cn-hangzhou:12345:orders -> oss:ObjectCreated:PutObject] | payments-bus[app.payments -> payment:captured:v1])&region=cn-hangzhou&accessKey=RAW(ak)&secretKey=RAW(sk)
```

If a message targeted for `orders-bus` attempts to use an event source configured only under `payments-bus`, validation fails with an `IllegalArgumentException`.

#### JSON Configuration

JSON configuration provides a clean, structured representation that is particularly well-suited for Spring Boot `application.yml`, Kubernetes ConfigMaps, or Camel JBang properties.

**Multi-Bus JSON structure:**

```json
{
  "orders-bus": {
    "acs:oss:cn-hangzhou:12345:orders": [
      "oss:ObjectCreated:PutObject",
      "oss:ObjectCreated:PostObject"
    ],
    "app.orders": [
      "order:created:v1",
      "order:cancelled:v1"
    ]
  },
  "payments-bus": {
    "app.payments": [
      "payment:authorized:v1",
      "payment:captured:v1"
    ]
  }
}
```

**Single-Bus flat JSON structure:**

```json
{
  "acs:oss:cn-hangzhou:12345:my-bucket": [
    "oss:ObjectCreated:PutObject",
    "oss:ObjectCreated:PostObject"
  ],
  "app.orders": [
    "order:created:v1"
  ]
}
```

In addition to JSON arrays, comma-separated strings are also supported for event types:

```json
{
  "app.orders": "order:created:v1, order:cancelled:v1"
}
```

### Response metadata in message body

The `putEvents` producer operation returns structured response metadata in the message body (`Map<String, Object>`):

  
| Key | Type | Description |
| --- | --- | --- |
| `requestId` | `String` | Request identifier returned by EventBridge. |
| `resourceOwnerAccountId` | `String` | Resource owner account identifier. |
| `failedEntryCount` | `Integer` | Number of failed entries in the batch. |
| `entryList` | `List<Map>` | List of entry results, where each entry map contains `eventId`, `errorCode`, and `errorMessage`. |

### Operations

The component supports the following operations:

-   `putEvents` - publish one or more CloudEvents (producer).
    

## Examples

### Publish event with String / JSON body

```java
from("direct:start")
    .setBody(constant("{\"orderId\":\"123\"}"))
    .to("alibaba-eventbridge:putEvents?eventBusName=my-bus&eventSource=camel.test&eventType=OrderCreated&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

### Publish event with Map body (Alibaba Key Dictionary)

```java
Map<String, Object> event = new HashMap<>();
event.put("eventBusName", "my-bus");
event.put("eventSource", "camel.test");
event.put("eventType", "OrderCreated");
event.put("eventSubject", "order/123");
event.put("eventData", Map.of("orderId", "123"));

from("direct:start")
    .setBody(constant(event))
    .to("alibaba-eventbridge:putEvents?region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

### Single-Bus Allowed Event Sources Validation

```java
from("direct:start")
    .setBody(constant(Map.of(
        "eventBusName", "orders-bus",
        "source", "acs:oss:cn-hangzhou:12345:my-bucket",
        "type", "oss:ObjectCreated:PutObject",
        "data", Map.of("file", "invoice.pdf")
    )))
    .to("alibaba-eventbridge:putEvents"
        + "?eventBusName=orders-bus"
        + "&allowedEventSources=RAW(acs:oss:cn-hangzhou:12345:my-bucket -> oss:ObjectCreated:PutObject, oss:ObjectCreated:PostObject; app.orders -> order:created:v1)"
        + "&validateEventSource=true&validateEventType=true"
        + "&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

### Multi-Bus Allowed Event Sources Validation (Batch Publishing)

```java
from("direct:start")
    .setBody(constant(List.of(
        Map.of("eventBusName", "orders-bus", "source", "acs:oss:cn-hangzhou:12345:orders", "type", "oss:ObjectCreated:PutObject", "data", Map.of("file", "image.jpg")),
        Map.of("eventBusName", "payments-bus", "source", "app.payments", "type", "payment:captured:v1", "data", Map.of("amount", 100))
    )))
    .to("alibaba-eventbridge:putEvents"
        + "?allowedEventSources=RAW(orders-bus[acs:oss:cn-hangzhou:12345:orders -> oss:ObjectCreated:PutObject] | payments-bus[app.payments -> payment:captured:v1])"
        + "&validateEventSource=true&validateEventType=true"
        + "&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

### JSON Configuration for Allowed Event Sources

```java
String jsonConfig = """
    {
      "orders-bus": {
        "acs:oss:cn-hangzhou:12345:orders": ["oss:ObjectCreated:PutObject", "oss:ObjectCreated:PostObject"],
        "app.orders": ["order:created:v1"]
      },
      "payments-bus": {
        "app.payments": ["payment:authorized:v1", "payment:captured:v1"]
      }
    }
    """;

from("direct:start")
    .setHeader(AlibabaEventBridgeHeaders.ALLOWED_EVENT_SOURCES, constant(jsonConfig))
    .setBody(constant(Map.of(
        "eventBusName", "orders-bus",
        "source", "app.orders",
        "type", "order:created:v1",
        "data", Map.of("orderId", "ORD-12345")
    )))
    .to("alibaba-eventbridge:putEvents?region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

### Dynamic Header and Property Overrides

```java
from("direct:start")
    .setHeader(AlibabaEventBridgeHeaders.EVENT_BUS_NAME, constant("orders-bus"))
    .setHeader(AlibabaEventBridgeHeaders.VALIDATE_EVENT_SOURCE, constant(true))
    .setHeader(AlibabaEventBridgeHeaders.VALIDATE_EVENT_TYPE, constant(true))
    .setHeader(AlibabaEventBridgeHeaders.ALLOWED_EVENT_SOURCES, constant("acs:oss:cn-hangzhou:12345:bucket -> oss:ObjectCreated:PutObject; app.orders -> order:created:v1"))
    .setBody(constant("{\"orderId\":\"123\"}"))
    .to("alibaba-eventbridge:putEvents?eventSource=app.orders&eventType=order:created:v1&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

For more examples, see the unit tests in the `camel-alibaba-eventbridge` module.