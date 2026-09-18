# Salesforce - Streaming and Pub/Sub

[Back to Salesforce Component](../salesforce-component.md)

## Pub/Sub API

The Pub/Sub API allows you to publish and subscribe to platform events, including real-time event monitoring events, and change data capture events. This API is based on gRPC and HTTP/2, and event payloads are delivered in Apache Avro format.

## Publishing Events

The URI format for publishing events is:

salesforce:pubSubPublish:<topic\_name>

For example:

.to("salesforce:pubsubPublish:/event/MyCustomPlatformEvent\_\_e")

## Publish an Event

`pubSubPublish`

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| Body | `List`. List can contained mixed types (see description below). | Event payloads to be published |  |  |

Because The Pub/Sub API requires that event payloads be serialized in Apache Avro format, Camel will attempt to serialize event payloads from the following input types:

-   Avro `GenericRecord`. Camel fetches the Avro schema in order to serialize `GenericRecord` instances. This option doesn’t require ahead-of-time generation of Event classes.
    
-   Avro `SpecificRecord`. Subclasses of `SpecificRecord` contain properties that are specific to an event type. The [maven plugin](../salesforce-component.html#MavenPlugin) can generate the subclasses automatically.
    
-   POJO. Camel fetches the Avro schema in order to serialize POJO instances. The POJO’s field names must match event field names exactly, including case.
    
-   `String`. Camel will treat the `String` value as JSON and serialize to Avro. Note that the JSON value does not have to be Avro-encoded JSON. It can be arbitrary JSON, but it must be serializable to Avro based on the Schema associated with the topic you’re publishing to. The JSON object’s field names must match event field names exactly, including case.
    
-   `byte[]`. Camel will not perform any serialization. Value must be the Avro-encoded event payload.
    
-   `com.salesforce.eventbus.protobuf.ProducerEvent`. Providing a `ProducerEvent` allows full control, e.g., setting the `id` property, which can be tied back to the `PublishResult.CorrelationKey`.
    

**Output**

Type: `List<org.apache.camel.component.salesforce.api.dto.pubsub.PublishResult>`

The order of the items in the returned `List` correlates to the order of the items in the input `List`.

## Subscribing

The URI format for subscribing to a Pub/Sub topic is:

salesforce:pubSubSubscribe:<topic\_name>

For example:

from("salesforce:pubSubSubscribe:/event/BatchApexErrorEvent")

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `replayPreset` | `ReplayPreset` | Values: `LATEST`, `EARLIEST`, `CUSTOM`. | `LATEST` |  |
| `pubSubReplayId` | `String` | When `replayPreset` is set to `CUSTOM`, the replayId to use when subscribing to a topic. |  |  |
| `pubSubBatchSize` | int | Max number of events to receive at a time. Values >100 will be normalized to 100 by salesforce. | 100 | X |
| `pubSubDeserializeType` | `PubSubDeserializeType` | Values: `AVRO`, `SPECIFIC_RECORD`, `GENERIC_RECORD`, `POJO`, `JSON`. `AVRO` will try a `SpecificRecord` subclass if found, otherwise `GenericRecord` | `AVRO` | X |
| `pubSubPojoClass` | Fully qualified class name to deserialize Pub/Sub API event to. |  |  | If `pubSubDeserializeType` is `POJO` |

**Output**

Type: Determined by the `pubSubDeserializeType` option.

Headers: `CamelSalesforcePubSubReplayId`

## Streaming API

The Streaming API enables streaming of events using push technology and provides a subscription mechanism for receiving events in near real time. The Streaming API subscription mechanism supports multiple types of events, including PushTopic events, generic events, platform events, and Change Data Capture events.

## Push Topics

The URI format for consuming Push Topics is:

salesforce:subscribe:<topic\_name>\[?options\]

To create and subscribe to a topic

-   Java
    
-   XML
    
-   YAML
    

```java
from("salesforce:subscribe:CamelTestTopic?notifyForFields=ALL&notifyForOperations=ALL&sObjectName=Merchandise__c&updateTopic=true&sObjectQuery=SELECT Id, Name FROM Merchandise__c")
    .to("...");
```

```xml
<route>
  <from uri="salesforce:subscribe:CamelTestTopic?notifyForFields=ALL&amp;notifyForOperations=ALL&amp;sObjectName=Merchandise__c&amp;updateTopic=true&amp;sObjectQuery=SELECT Id, Name FROM Merchandise__c"/>
  <to uri="..."/>
</route>
```

```yaml
- route:
    from:
      uri: salesforce:subscribe:CamelTestTopic
      parameters:
        notifyForFields: ALL
        notifyForOperations: ALL
        sObjectName: Merchandise__c
        updateTopic: true
        sObjectQuery: "SELECT Id, Name FROM Merchandise__c"
      steps:
        - to:
            uri: "..."
```

To subscribe to an existing topic

-   Java
    
-   XML
    
-   YAML
    

```java
from("salesforce:subscribe:CamelTestTopic?sObjectName=Merchandise__c")
    .to("...");
```

```xml
<route>
  <from uri="salesforce:subscribe:CamelTestTopic?sObjectName=Merchandise__c"/>
  <to uri="..."/>
</route>
```

```yaml
- route:
    from:
      uri: salesforce:subscribe:CamelTestTopic
      parameters:
        sObjectName: Merchandise__c
      steps:
        - to:
            uri: "..."
```

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `sObjectName` | `String` | SObject to monitor |  | x |
| `sObjectQuery` | `String` | SOQL query used to create Push Topic |  | Required for creating new topics |
| `updateTopic` | `Boolean` | Whether to update an existing Push Topic if exists | false |  |
| `notifyForFields` | `NotifyForFieldsEnum` | Specifies how the record is evaluated against the PushTopic query. | Referenced |  |
| `notifyForOperationCreate` | `Boolean` | Whether a create operation should generate a notification. | false |  |
| `notifyForOperationDelete` | `Boolean` | Whether a delete operation should generate a notification. | false |  |
| `notifyForOperationUndelete` | `Boolean` | Whether an undelete operation should generate a notification. | false |  |
| `notifyForOperationUpdate` | `Boolean` | Whether an update operation should generate a notification. | false |  |
| `notifyForOperations` | `NotifyForOperationsEnum` | Whether an update operation should generate a notification. Only for use in API version < 29.0 | All |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

## Parallel processing received events

You can turn on `consumerWorkerPoolEnabled=true` on the salesforce endpoint to let Camel use a thread-pool to process the received events, which allows to process these events in parallel.

> **Note**
> It has been reported that when receiving from PUSH\_TOPIC events and then later sending a message to salesforce (via producer) via the same thread could cause Salesforce to block. Enabling the worker pool can help with this. See more in [CAMEL-22332](https://issues.apache.org/jira/browse/CAMEL-22332).

**Output**

Type: Class passed via `sObjectName` parameter

## Platform Events

To emit a platform event use the [createSObject](salesforce-rest-api.html#createSObject) operation, passing an instance of a platform event, e.g. `Order_Event__e`.

The URI format for consuming platform events is:

salesforce:subscribe:event/<event\_name>

For example, to receive platform events use for the event type `Order_Event__e`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("salesforce:subscribe:event/Order_Event__e")
    .to("...");
```

```xml
<route>
  <from uri="salesforce:subscribe:event/Order_Event__e"/>
  <to uri="..."/>
</route>
```

```yaml
- route:
    from:
      uri: salesforce:subscribe:event/Order_Event__e
      steps:
        - to:
            uri: "..."
```

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `rawPayload` | `Boolean` | If false, operation returns a `PlatformEvent`, otherwise returns the raw Bayeux Message | false |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

**Output**

Type: `PlatformEvent` or `org.cometd.bayeux.Message`

## Change Data Capture Events

Change Data Capture (CDC) allows you to receive near-real-time changes of Salesforce records, and synchronize corresponding records in an external data store. Change Data Capture publishes change events, which represent changes to Salesforce records. Changes include the creation of a new record, updates to an existing record, deletion of a record, and undeletion of a record.

The URI format to consume CDC events is as follows:

All Selected Entities

salesforce:subscribe:data/ChangeEvents

Standard Objects

salesforce:subscribe:data/<Standard\_Object\_Name>ChangeEvent

Custom Objects

salesforce:subscribe:data/<Custom\_Object\_Name>\_\_ChangeEvent

Here are a few examples

-   Java
    
-   XML
    
-   YAML
    

```java
from("salesforce:subscribe:data/ChangeEvents?replayId=-1")
    .log("being notified of all change events");

from("salesforce:subscribe:data/AccountChangeEvent?replayId=-1")
    .log("being notified of change events for Account records");

from("salesforce:subscribe:data/Employee__ChangeEvent?replayId=-1")
    .log("being notified of change events for Employee__c custom object");
```

```xml
<route>
  <from uri="salesforce:subscribe:data/ChangeEvents?replayId=-1"/>
  <log message="being notified of all change events"/>
</route>
<route>
  <from uri="salesforce:subscribe:data/AccountChangeEvent?replayId=-1"/>
  <log message="being notified of change events for Account records"/>
</route>
<route>
  <from uri="salesforce:subscribe:data/Employee__ChangeEvent?replayId=-1"/>
  <log message="being notified of change events for Employee__c custom object"/>
</route>
```

```yaml
- route:
    from:
      uri: salesforce:subscribe:data/ChangeEvents
      parameters:
        replayId: -1
      steps:
        - log: "being notified of all change events"
- route:
    from:
      uri: salesforce:subscribe:data/AccountChangeEvent
      parameters:
        replayId: -1
      steps:
        - log: "being notified of change events for Account records"
- route:
    from:
      uri: salesforce:subscribe:data/Employee__ChangeEvent
      parameters:
        replayId: -1
      steps:
        - log: "being notified of change events for Employee__c custom object"
```

More details about how to use the Camel Salesforce component change data capture capabilities could be found in the [ChangeEventsConsumerIntegrationTest](https://github.com/apache/camel/tree/main/components/camel-salesforce/camel-salesforce-component/src/test/java/org/apache/camel/component/salesforce/ChangeEventsConsumerIntegrationTest.java).

The [Salesforce developer guide](https://developer.salesforce.com/docs/atlas.en-us.change_data_capture.meta/change_data_capture/cdc_intro.htm) is a good fit to better know the subtleties of implementing a change data capture integration application. The dynamic nature of change event body fields, high level replication steps as well as security considerations could be of interest.

    
| Parameter | Type | Description | Default | Required |
| --- | --- | --- | --- | --- |
| `rawPayload` | `Boolean` | If false, operation returns a `Map<String, Object>`, otherwise returns the raw Bayeux `Message` | false |  |
| `replayId` | `int` | The replayId value to use when subscribing. |  |  |
| `defaultReplayId` | `int` | Default replayId setting if no value is found in initialReplayIdMap. | \-1 |  |
| `fallBackReplayId` | `int` | ReplayId to fall back to after an Invalid Replay Id response. | \-1 |  |

**Output**

Type: `Map<String, Object>` or `org.cometd.bayeux.Message`

Headers

 
| Name | Description |
| --- | --- |
| `CamelSalesforceChangeType` | `CREATE`, `UPDATE`, `DELETE` or `UNDELETE` |