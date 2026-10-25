# Ignite Queues

**Since Camel 2.17**

**Only producer is supported**

The Ignite Queue endpoint is one of camel-ignite endpoints that allow you to interact with [Ignite Queue data structures](https://apacheignite.readme.io/docs/queue-and-set).

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

The Ignite Queues component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationResource** (producer) | The resource from where to load the configuration. It can be a: URL, String or InputStream type. |  | Object |
| **ignite** (producer) | To use an existing Ignite instance. |  | Ignite |
| **igniteConfiguration** (producer) | Allows the user to set a programmatic ignite configuration. |  | IgniteConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Ignite Queues endpoint is configured using URI syntax:

ignite-queue:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** The queue name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **capacity** (producer) | The queue capacity. Default: non-bounded. |  | int |
| **configuration** (producer) | The collection configuration. Default: empty configuration. You can also conveniently set inner properties by using configuration.xyz=123 options. |  | CollectionConfiguration |
| **operation** (producer) | 
The operation to invoke on the Ignite Queue. Superseded by the IgniteConstants.IGNITE\_QUEUE\_OPERATION header in the IN message. Possible values: CONTAINS, ADD, SIZE, REMOVE, ITERATOR, CLEAR, RETAIN\_ALL, ARRAY, DRAIN, ELEMENT, PEEK, OFFER, POLL, TAKE, PUT.

Enum values:

-   CONTAINS
    
-   ADD
    
-   SIZE
    
-   REMOVE
    
-   ITERATOR
    
-   CLEAR
    
-   RETAIN\_ALL
    
-   ARRAY
    
-   DRAIN
    
-   ELEMENT
    
-   PEEK
    
-   OFFER
    
-   POLL
    
-   TAKE
    
-   PUT
    





 |  | IgniteQueueOperation |
| **propagateIncomingBodyIfNoReturnValue** (producer) | Sets whether to propagate the incoming body if the return type of the underlying Ignite operation is void. | true | boolean |
| **timeoutMillis** (producer) | The queue timeout in milliseconds. Default: no timeout. |  | Long |
| **treatCollectionsAsCacheObjects** (producer) | Sets whether to treat Collections as cache objects or as Collections of items to insert/update/compute, etc. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Ignite Queues component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIgniteQueueOperation** (producer) Constant: [`IGNITE_QUEUE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_QUEUE_OPERATION) | 
Allows you to dynamically change the queue operation.

Enum values:

-   CONTAINS
    
-   ADD
    
-   SIZE
    
-   REMOVE
    
-   ITERATOR
    
-   CLEAR
    
-   RETAIN\_ALL
    
-   ARRAY
    
-   DRAIN
    
-   ELEMENT
    
-   PEEK
    
-   OFFER
    
-   POLL
    
-   TAKE
    
-   PUT
    





 |  | IgniteQueueOperation |
| **CamelIgniteQueueMaxElements** (producer) Constant: [`IGNITE_QUEUE_MAX_ELEMENTS`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_QUEUE_MAX_ELEMENTS) | When invoking the DRAIN operation, the amount of items to drain. |  | Integer |
| **CamelIgniteQueueTransferredCount** (producer) Constant: [`IGNITE_QUEUE_TRANSFERRED_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_QUEUE_TRANSFERRED_COUNT) | The amount of items transferred as the result of the DRAIN operation. |  | Integer |
| **CamelIgniteQueueTimeoutMillis** (producer) Constant: [`IGNITE_QUEUE_TIMEOUT_MILLIS`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_QUEUE_TIMEOUT_MILLIS) | Dynamically sets the timeout in milliseconds to use when invoking the OFFER or POLL operations. |  | Long |

## Message Body

The message body at each side of the Ignite Queues component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | ADD, OFFER, PUT, CONTAINS, REMOVE and RETAIN\_ALL use the body as the element, and a Collection as several elements unless treatCollectionsAsCacheObjects=true; no body fails ADD, CONTAINS, REMOVE and RETAIN\_ALL. DRAIN drains into a Collection body, or a new List. The other operations do not use the body. The operation is the operation option or the CamelIgniteQueueOperation header; with neither the producer fails. |
| **Producer output** | `unknown` | true or false for ADD, OFFER, CONTAINS, REMOVE and RETAIN\_ALL, the number of elements for SIZE, an Iterator for ITERATOR, an Object array for ARRAY, and the Collection of the drained elements for DRAIN, with their count in the CamelIgniteQueueTransferredCount header. ELEMENT, TAKE, PEEK and POLL give the head element; PEEK and POLL give null for an empty queue. CLEAR and PUT leave the body.
-   With `operation=ADD`: `value` (`java.lang.Boolean`)
    
-   With `operation=OFFER`: `value` (`java.lang.Boolean`)
    
-   With `operation=CONTAINS`: `value` (`java.lang.Boolean`)
    
-   With `operation=REMOVE`: `value` (`java.lang.Boolean`)
    
-   With `operation=RETAIN_ALL`: `value` (`java.lang.Boolean`)
    
-   With `operation=SIZE`: `value` (`java.lang.Integer`)
    
-   With `operation=ITERATOR`: `iterator`
    
-   With `operation=ARRAY`: `list`
    
-   With `operation=DRAIN`: `list`
    
-   With `operation=CLEAR`: `unchanged`
    
-   With `operation=PUT`: `unchanged`
    

Not known when `propagateIncomingBodyIfNoReturnValue` is set.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

The component needs an Ignite node: [Ignite](ignite-summary.md) describes the ways to give it one. A node of its own with the default configuration takes one line in `application.properties`. On Java 17 and later, Ignite also needs the `--add-opens` JVM options that its documentation lists.

```properties
camel.component.ignite-queue.ignite-configuration = #class:org.apache.ignite.configuration.IgniteConfiguration
```

The first route adds the body to the `tasks` queue. The second polls the queue every second, and `POLL` returns null when the queue is empty:

```yaml
- route:
    from:
      uri: direct:addTask
      steps:
        - to:
            uri: ignite-queue:tasks
            parameters:
              operation: ADD
- route:
    from:
      uri: timer:pollTasks
      parameters:
        period: 1000
      steps:
        - to:
            uri: ignite-queue:tasks
            parameters:
              operation: POLL
        - filter:
            expression:
              simple:
                expression: "${body} != null"
            steps:
              - log:
                  message: "Task: ${body}"
```