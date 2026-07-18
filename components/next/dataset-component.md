# Dataset

**Since Camel 1.3**

**Both producer and consumer are supported**

Testing of distributed and asynchronous processing is notoriously challenging. The [Mock](mock-component.md), [DataSet](#), and [DataSet Test](dataset-test-component.md) endpoints work with the Camel Testing Framework to simplify your unit and integration testing using [Enterprise Integration Patterns](eips/enterprise-integration-patterns.md) and Camel’s large range of Components together with the powerful Bean Integration.

The DataSet component provides a mechanism to easily perform load & soak testing of your system. It works by allowing you to create [DataSet instances](https://www.javadoc.io/doc/org.apache.camel/camel-dataset/current/org/apache/camel/component/dataset/DataSet.md) both as a source of messages and as a way to assert that the data set is received.

Camel will use the [throughput logger](log-component.md) when sending the dataset.

## URI format

dataset:name\[?options\]

Where **name** is used to find the [DataSet instance](https://www.javadoc.io/doc/org.apache.camel/camel-dataset/current/org/apache/camel/component/dataset/DataSet.md) in the Registry

Camel ships with a support implementation of `org.apache.camel.component.dataset.DataSet`, the `org.apache.camel.component.dataset.DataSetSupport` class, that can be used as a base for implementing your own data set. Camel also ships with some implementations that can be used for testing: `org.apache.camel.component.dataset.SimpleDataSet`, `org.apache.camel.component.dataset.ListDataSet` and `org.apache.camel.component.dataset.FileDataSet`, all of which extend `DataSetSupport`.

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

The Dataset component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging, then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **exchangeFormatter** (advanced) | **Autowired** To use a custom ExchangeFormatter to format the Exchange into a String suitable for logging. |  | ExchangeFormatter |

## Endpoint Options

The Dataset endpoint is configured using URI syntax:

dataset:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of DataSet to lookup in the registry. |  | DataSet |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSetIndex** (common) | 
Controls the behaviour of the CamelDataSetIndex header. off (consumer) the header will not be set. strict (consumer) the header will be set. lenient (consumer) the header will be set. off (producer) the header value will not be verified, and will not be set if it is not present. strict (producer) the header value must be present and will be verified. lenient (producer) the header value will be verified if it is present, and will be set if it is not present.

Enum values:

-   strict
    
-   lenient
    
-   off
    





 | lenient | String |
| **initialDelay** (consumer) | Time period in millis to wait before starting sending messages. | 1000 | long |
| **minRate** (consumer) | Wait until the DataSet contains at least this number of messages. | 0 | int |
| **preloadSize** (consumer) | Sets how many messages should be preloaded (sent) before the route completes its initialization. | 0 | long |
| **produceDelay** (consumer) | Allows a delay to be specified which causes a delay when a message is sent by the consumer (to simulate slow processing). | 3 | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **assertPeriod** (producer) | Sets a grace period after which the mock will re-assert to ensure the preliminary assertion is still valid. This is used, for example, to assert that exactly a number of messages arrive. For example, if the expected count was set to 5, then the assertion is satisfied when five or more messages arrive. To ensure that exactly 5 messages arrive, then you would need to wait a little period to ensure no further message arrives. This is what you can use this method for. By default, this period is disabled. |  | long |
| **consumeDelay** (producer) | Allows a delay to be specified which causes a delay when a message is consumed by the producer (to simulate slow processing). | 0 | long |
| **expectedCount** (producer) | Specifies the expected number of message exchanges that should be received by this mock. Beware: If you want to expect that 0 messages, then take extra care, as 0 matches when the tests starts, so you need to set a assert period time to let the test run for a while to make sure there are still no messages arrived; for that use the assertPeriod option. If you want to assert that exactly nth message arrives to this mock, then see also the assertPeriod option for further details. | \-1 | int |
| **copyOnExchange** (producer (advanced)) | Sets whether to make a deep copy of the incoming Exchange when received at this mock endpoint. | true | boolean |
| **failFast** (producer (advanced)) | Sets whether assertIsSatisfied() should fail fast at the first detected failed expectation while it may otherwise wait for all expected messages to arrive before performing expectations verifications. Is by default true. Set to false to use behavior as in Camel 2.x. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer (advanced)) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging, then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **reportGroup** (producer (advanced)) | A number that is used to turn on throughput logging based on groups of the size. |  | int |
| **resultMinimumWaitTime** (producer (advanced)) | Sets the minimum expected amount of time the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **resultWaitTime** (producer (advanced)) | Sets the maximum amount of time the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **retainFirst** (producer (advanced)) | Specifies to only retain the first nth number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received message. For example if we have received 5000 messages and have configured to only retain the first 10 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the first 10 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both retainFirst and retainLast options, to limit both the first and last received. | \-1 | int |
| **retainLast** (producer (advanced)) | Specifies to only retain the last nth number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received message. For example if we have received 5000 messages and have configured to only retain the last 20 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the last 20 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both retainFirst and retainLast options, to limit both the first and last received. | \-1 | int |
| **sleepForEmptyTest** (producer (advanced)) | Allows a sleep to be specified to wait to check that this mock really is empty when expectedMessageCount(int) is called with zero value. |  | long |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |

## Message Headers

The Dataset component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDataSetIndex** (common) Constant: [`DATASET_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-dataset/latest/org/apache/camel/component/dataset/DataSetConstants.html#DATASET_INDEX) | The dataset index. |  | Long |

## Usage

### Configuring DataSet

Camel will look up in the Registry for a bean implementing the `DataSet` interface. So you can register your own data set as:

```xml
<bean id="myDataSet" class="com.mycompany.MyDataSet">
  <property name="size" value="100"/>
</bean>
```

### DataSetSupport (abstract class)

The `DataSetSupport` abstract class is a nice starting point for new data set, and provides some useful features to derived classes.

#### Additional Properties on DataSetSupport

   
| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `defaultHeaders` | `Map<String,Object>` | `null` | Specify the default message body. For `SimpleDataSet` it is a constant payload; though if you want to create custom payloads per message, create your own derivation of `DataSetSupport`. |
| `outputTransformer` | `org.apache.camel.Processor` | null |  |
| `size` | `long` | `10` | Specify how many messages to send/consume. |
| `reportCount` | `long` | `-1` | Specify the number of messages to be received before reporting progress. Useful for showing the progress of a large load test. If smaller than zero (\` < 0\`), then `size` / 5, if is 0 then `size`, else set to `reportCount` value. |

### SimpleDataSet

The `SimpleDataSet` extends `DataSetSupport`, and adds a default body.

#### Additional Properties on SimpleDataSet

   
| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `defaultBody` | `Object` | `<hello>world!</hello>` | Specify the default message body. By default, the `SimpleDataSet` produces the same constant payload for each exchange. If you want to customize the payload for each exchange, create a Camel `Processor` and configure the `SimpleDataSet` to use it by setting the `outputTransformer` property. |

### ListDataSet

The List\`DataSet\` extends `DataSetSupport`, and adds a list of default bodies.

#### Additional Properties on ListDataSet

   
| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `defaultBodies` | `List<Object>` | `empty LinkedList<Object>` | Specify the default message body. By default, the `ListDataSet` selects a constant payload from the list of `defaultBodies` using the `CamelDataSetIndex`. If you want to customize the payload, create a Camel `Processor` and configure the `ListDataSet` to use it by setting the `outputTransformer` property. |
| `size` | `long` | the size of the defaultBodies list | Specify how many messages to send/consume. This value can be different from the size of the `defaultBodies` list. If the value is less than the size of the `defaultBodies` list, some of the list elements will not be used. If the value is greater than the size of the `defaultBodies` list, the payload for the exchange will be selected using the modulus of the `CamelDataSetIndex` and the size of the `defaultBodies` list (i.e., `CamelDataSetIndex % defaultBodies.size()` ) |

### FileDataSet

The `FileDataSet` extends `ListDataSet`, and adds support for loading the bodies from a file.

#### Additional Properties on FileDataSet

   
| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `sourceFile` | `File` | null | Specify the source file for payloads |
| `delimiter` | `String` | \\z | Specify the delimiter pattern used by a `java.util.Scanner` to split the file into multiple payloads. |

## Example

For example, to test that a set of messages are sent to a queue and then consumed from the queue without losing any messages:

-   Java
    
-   XML
    
-   YAML
    

```java
// send the dataset to a queue
from("dataset:foo").to("activemq:SomeQueue");

// now lets test that the messages are consumed correctly
from("activemq:SomeQueue").to("dataset:foo");
```

```xml
<!-- send the dataset to a queue -->
<route>
  <from uri="dataset:foo"/>
  <to uri="activemq:SomeQueue"/>
</route>
<!-- now lets test that the messages are consumed correctly -->
<route>
  <from uri="activemq:SomeQueue"/>
  <to uri="dataset:foo"/>
</route>
```

```yaml
# send the dataset to a queue
- route:
    from:
      uri: dataset:foo
      steps:
        - to:
            uri: activemq:SomeQueue
# now lets test that the messages are consumed correctly
- route:
    from:
      uri: activemq:SomeQueue
      steps:
        - to:
            uri: dataset:foo
```

The above would look in the Registry to find the `foo` `DataSet` instance which is used to create the messages.

Then you create a `DataSet` implementation, such as using the `SimpleDataSet` as described below, configuring things like how big the data set is and what the messages look like etc.