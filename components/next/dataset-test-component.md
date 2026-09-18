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

The DataSet Test component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **log** (producer) | To turn on logging when the mock receives an incoming message. This will log only one time at INFO level for the incoming message. For more detailed logging, then set the logger to DEBUG level for the org.apache.camel.component.mock.MockEndpoint class. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **exchangeFormatter** (advanced) | **Autowired** To use a custom ExchangeFormatter to format the Exchange into a String suitable for logging. |  | ExchangeFormatter |

## Endpoint Options

The DataSet Test endpoint is configured using URI syntax:

dataset-test:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** Name of endpoint to lookup in the registry to use for polling messages used for testing. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **anyOrder** (producer) | Whether the expected messages should arrive in the same order or can be in any order. | false | boolean |
| **assertPeriod** (producer) | Sets a grace period after which the mock will re-assert to ensure the preliminary assertion is still valid. This is used, for example, to assert that exactly a number of messages arrive. For example, if the expected count was set to 5, then the assertion is satisfied when five or more messages arrive. To ensure that exactly 5 messages arrive, then you would need to wait a little period to ensure no further message arrives. This is what you can use this method for. By default, this period is disabled. |  | long |
| **delimiter** (producer) | The split delimiter to use when split is enabled. By default the delimiter is new line based. The delimiter can be a regular expression. |  | String |
| **expectedCount** (producer) | Specifies the expected number of message exchanges that should be received by this mock. Beware: If you want to expect that 0 messages, then take extra care, as 0 matches when the tests starts, so you need to set a assert period time to let the test run for a while to make sure there are still no messages arrived; for that use the assertPeriod option. If you want to assert that exactly nth message arrives to this mock, then see also the assertPeriod option for further details. | \-1 | int |
| **split** (producer) | If enabled the messages loaded from the test endpoint will be split using new line delimiters so each line is an expected message. For example to use a file endpoint to load a file where each line is an expected message. | false | boolean |
| **timeout** (producer) | The timeout to use when polling for message bodies from the URI. | 2000 | long |
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

## Example

For example, you could write a test case as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:someEndpoint")
    .to("dataset-test:file://data/expectedOutput?noop=true");
```

```xml
<route>
  <from uri="seda:someEndpoint"/>
  <to uri="dataset-test:file://data/expectedOutput?noop=true"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:someEndpoint
      steps:
        - to:
            uri: dataset-test:file://data/expectedOutput
            parameters:
              noop: true
```

If your test then invokes the [MockEndpoint.assertIsSatisfied(camelContext) method](https://www.javadoc.io/doc/org.apache.camel/camel-mock/current/org/apache/camel/component/mock/MockEndpoint.html#assertIsSatisfied-org.apache.camel.CamelContext-), your test case will perform the necessary assertions.

To see how you can set other expectations on the test endpoint, see the [Mock](mock-component.md) component.