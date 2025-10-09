# DataSet Test

**Since Camel 1.3**

**Only producer is supported**

Testing of distributed and asynchronous processing is notoriously difficult. The [Mock](mock-component.md), [DataSet](dataset-component.md), and [DataSet Test](#) endpoints work great with the Camel Testing Framework to simplify your unit and integration testing using [Enterprise Integration Patterns](eips/enterprise-integration-patterns.md) and Camel’s large range of Components together with the powerful Bean Integration.

The **dataset-test** component extends the [Mock](mock-component.md) component to support pulling messages from another endpoint on startup to set the expected message bodies on the underlying [Mock](mock-component.md) endpoint.

That is, you use the dataset test endpoint in a route and messages arriving at it will be implicitly compared to some expected messages extracted from some other location.

So you can use, for example, an expected set of message bodies as files. This will then set up a properly configured [Mock](mock-component.md) endpoint, which is only valid if the received messages match the number of expected messages and their message payloads are equal.

## URI format

dataset-test:expectedMessagesEndpointUri

Where **expectedMessagesEndpointUri** refers to some other Component URI that the expected message bodies are pulled from before starting the test.

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

The DataSet Test component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **exchangeFormatter** (advanced) | **Autowired** Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. |  | ExchangeFormatter |

## Endpoint Options

The DataSet Test endpoint is configured using URI syntax:

dataset-test:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** Name of endpoint to lookup in the registry to use for polling messages used for testing. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **anyOrder** (producer) | Whether the expected messages should arrive in the same order or can be in any order. | false | boolean |
| **assertPeriod** (producer) | Sets a grace period after which the mock endpoint will re-assert to ensure the preliminary assertion is still valid. This is used for example to assert that exactly a number of messages arrives. For example if expected count was set to 5, then the assertion is satisfied when 5 or more message arrives. To ensure that exactly 5 messages arrives, then you would need to wait a little period to ensure no further message arrives. This is what you can use this method for. By default this period is disabled. |  | long |
| **delimiter** (producer) | The split delimiter to use when split is enabled. By default the delimiter is new line based. The delimiter can be a regular expression. |  | String |
| **expectedCount** (producer) | Specifies the expected number of message exchanges that should be received by this endpoint. Beware: If you want to expect that 0 messages, then take extra care, as 0 matches when the tests starts, so you need to set a assert period time to let the test run for a while to make sure there are still no messages arrived; for that use setAssertPeriod(long). An alternative is to use NotifyBuilder, and use the notifier to know when Camel is done routing some messages, before you call the assertIsSatisfied() method on the mocks. This allows you to not use a fixed assert period, to speedup testing times. If you want to assert that exactly n’th message arrives to this mock endpoint, then see also the setAssertPeriod(long) method for further details. | \-1 | int |
| **failFast** (producer) | Sets whether assertIsSatisfied() should fail fast at the first detected failed expectation while it may otherwise wait for all expected messages to arrive before performing expectations verifications. Is by default true. Set to false to use behavior as in Camel 2.x. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **reportGroup** (producer) | A number that is used to turn on throughput logging based on groups of the size. |  | int |
| **resultMinimumWaitTime** (producer) | Sets the minimum expected amount of time (in millis) the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **resultWaitTime** (producer) | Sets the maximum amount of time (in millis) the assertIsSatisfied() will wait on a latch until it is satisfied. |  | long |
| **retainFirst** (producer) | Specifies to only retain the first n’th number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received Exchanges. For example if we have received 5000 Exchanges, and have configured to only retain the first 10 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the first 10 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both setRetainFirst(int) and setRetainLast(int) methods, to limit both the first and last received. | \-1 | int |
| **retainLast** (producer) | Specifies to only retain the last n’th number of received Exchanges. This is used when testing with big data, to reduce memory consumption by not storing copies of every Exchange this mock endpoint receives. Important: When using this limitation, then the getReceivedCounter() will still return the actual number of received Exchanges. For example if we have received 5000 Exchanges, and have configured to only retain the last 20 Exchanges, then the getReceivedCounter() will still return 5000 but there is only the last 20 Exchanges in the getExchanges() and getReceivedExchanges() methods. When using this method, then some of the other expectation methods is not supported, for example the expectedBodiesReceived(Object…​) sets a expectation on the first number of bodies received. You can configure both setRetainFirst(int) and setRetainLast(int) methods, to limit both the first and last received. | \-1 | int |
| **sleepForEmptyTest** (producer) | Allows a sleep to be specified to wait to check that this endpoint really is empty when expectedMessageCount(int) is called with zero. |  | long |
| **split** (producer) | If enabled the messages loaded from the test endpoint will be split using new line delimiters so each line is an expected message. For example to use a file endpoint to load a file where each line is an expected message. | false | boolean |
| **timeout** (producer) | The timeout to use when polling for message bodies from the URI. | 2000 | long |
| **copyOnExchange** (producer (advanced)) | Sets whether to make a deep copy of the incoming Exchange when received at this mock endpoint. Is by default true. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Example

For example, you could write a test case as follows:

```java
from("seda:someEndpoint").
  to("dataset-test:file://data/expectedOutput?noop=true");
```

If your test then invokes the [MockEndpoint.assertIsSatisfied(camelContext) method](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#assertIsSatisfied-org.apache.camel.CamelContext-), your test case will perform the necessary assertions.

To see how you can set other expectations on the test endpoint, see the [Mock](mock-component.md) component.

## Spring Boot Auto-Configuration

When using dataset-test with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-dataset-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.dataset-test.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dataset-test.enabled** | Whether to enable auto configuration of the dataset-test component. This is enabled by default. |  | Boolean |
| **camel.component.dataset-test.exchange-formatter** | Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. The option is a org.apache.camel.spi.ExchangeFormatter type. |  | ExchangeFormatter |
| **camel.component.dataset-test.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.dataset-test.log** | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | Boolean |
| **camel.component.dataset.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dataset.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.dataset.enabled** | Whether to enable auto configuration of the dataset component. This is enabled by default. |  | Boolean |
| **camel.component.dataset.exchange-formatter** | Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. The option is a org.apache.camel.spi.ExchangeFormatter type. |  | ExchangeFormatter |
| **camel.component.dataset.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.dataset.log** | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | Boolean |