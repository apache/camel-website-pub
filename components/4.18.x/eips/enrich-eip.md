# Enrich

Camel supports the [Content Enricher](http://www.enterpriseintegrationpatterns.com/DataEnricher.md) from the [EIP patterns](enterprise-integration-patterns.md).

![image](_images/eip/DataEnricher.gif)

In Camel the Content Enricher can be done in several ways:

-   Using [Enrich](#) EIP or [Poll Enrich](pollEnrich-eip.md) EIP
    
-   Using a [Message Translator](message-translator.md)
    
-   Using a [Processor](../../../manual/processor.md) with the enrichment programmed in Java
    
-   Using a [Bean](bean-eip.md) EIP with the enrichment programmed in Java
    

The most natural Camel approach is using [Enrich](#) EIP, which comes as two kinds:

-   [Enrich](#) EIP: This is the most common content enricher that uses a `Producer` to obtain the data. It is usually used for [Request Reply](requestReply-eip.md) messaging, for instance, to invoke an external web service.
    
-   [Poll Enrich](pollEnrich-eip.md) EIP: Uses a [Polling Consumer](polling-consumer.md) to obtain the additional data. It is usually used for [Event Message](event-message.md) messaging, for instance, to read a file or download one using [FTP](../ftp-component.md).
    

> **Note**
> This page documents the Enrich EIP.

The Enrich eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression that computes the endpoint uri to use as the resource endpoint to enrich from. |  | ExpressionDefinition |
| **variableSend** | To use a variable to store the received message body (only body, not headers). This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. Important: When using receive variable then the received body is stored only in this variable and not on the current message. |  | String |
| **variableReceive** | To use a variable as the source for the message body to send. This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. Important: When using send variable then the message body is taken from this variable instead of the current message, however the headers from the message will still be used as well. In other words, the variable is used instead of the message body, but everything else is as usual. |  | String |
| **aggregationStrategy** | Sets the AggregationStrategy to be used to merge the reply from the external service, into a single outgoing message. By default Camel will use the reply from the external service as outgoing message. |  | AggregationStrategy |
| **aggregationStrategyMethodName** | This option can be used to explicit declare the method name to use, when using POJOs as the AggregationStrategy. |  | String |
| **aggregationStrategyMethodAllowNull** | If this option is false then the aggregate method is not used if there was no data to enrich. If this option is true then null values is used as the oldExchange (when no data to enrich), when using POJOs as the AggregationStrategy. |  | String |
| **aggregateOnException** | If this option is false then the aggregate method is not used if there was an exception thrown while trying to retrieve the data to enrich from the resource. Setting this option to true allows end users to control what to do if there was an exception in the aggregate method. For example to suppress the exception or set a custom message body etc. | false | Boolean |
| **shareUnitOfWork** | Shares the org.apache.camel.spi.UnitOfWork with the parent and the resource exchange. Enrich will by default not share unit of work between the parent exchange and the resource exchange. This means the resource exchange has its own individual unit of work. | false | Boolean |
| **cacheSize** | Sets the maximum size used by the org.apache.camel.spi.ProducerCache which is used to cache and reuse producer when uris are reused. Beware that when using dynamic endpoints then it affects how well the cache can be utilized. If each dynamic endpoint is unique then its best to turn off caching by setting this to -1, which allows Camel to not cache both the producers and endpoints; they are regarded as prototype scoped and will be stopped and discarded after use. This reduces memory usage as otherwise producers/endpoints are stored in memory in the caches. However if there are a high degree of dynamic endpoints that have been used before, then it can benefit to use the cache to reuse both producers and endpoints and therefore the cache size can be set accordingly or rely on the default size (1000). If there is a mix of unique and used before dynamic endpoints, then setting a reasonable cache size can help reduce memory usage to avoid storing too many non frequent used producers. |  | Integer |
| **ignoreInvalidEndpoint** | Ignore the invalidate endpoint exception when try to create a producer with that endpoint. | false | Boolean |
| **allowOptimisedComponents** | Whether to allow components to optimise enricher if they are org.apache.camel.spi.SendDynamicAware. | true | Boolean |
| **autoStartComponents** | Whether to auto startup components when enricher is starting up. | true | Boolean |

## Exchange properties

The Enrich eip supports 1 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelToEndpoint** | Endpoint URI where this Exchange is being sent to. |  | String |

## Content enrichment using Enrich EIP

Enrich EIP is the most common content enricher that uses a `Producer` to obtain the data.

The content enricher (`enrich`) retrieves additional data from a _resource endpoint_ to enrich an incoming message (contained in the _original exchange_).

An `AggregationStrategy` is used to combine the original exchange and the _resource exchange_. The first parameter of the `AggregationStrategy.aggregate(Exchange, Exchange)` method corresponds to the original exchange, the second parameter the resource exchange.

Here’s an example for implementing an `AggregationStrategy`, which merges the two data as a `String` with colon separator:

```java
public class ExampleAggregationStrategy implements AggregationStrategy {

    public Exchange aggregate(Exchange newExchange, Exchange oldExchange) {
        // this is just an example, for real-world use-cases the
        // aggregation strategy would be specific to the use-case

        if (newExchange == null) {
            return oldExchange;
        }
        Object oldBody = oldExchange.getIn().getBody();
        Object newBody = newExchange.getIn().getBody();
        oldExchange.getIn().setBody(oldBody + ":" + newBody);
        return oldExchange;
    }

}
```

In the example Camel will call the http endpoint to collect some data, that will then be merged with the original message using the `AggregationStrategy`:

-   Java
    
-   XML
    
-   YAML
    

```java
AggregationStrategy aggregationStrategy = ...

from("direct:start")
  .enrich("http:remoteserver/foo", aggregationStrategy)
  .to("mock:result");
```

```xml
<bean id="myStrategy" class="com.foo.ExampleAggregationStrategy"/>

<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="direct:start"/>
    <enrich aggregationStrategy="myStrategy">
      <constant>http:remoteserver/foo</constant>
    </enrich>
    <to uri="mock:result"/>
  </route>
</camelContext>
```

```yaml
- from:
    uri: direct:start
    steps:
      - enrich:
          expression:
            constant: "http:remoteserver/foo"
          aggregationStrategy: "#myStrategy"
      - to:
          uri: mock:result
- beans:
    - name: myStrategy
      type: com.foo.ExampleAggregationStrategy
```

### Aggregation Strategy is optional

The aggregation strategy is optional. If not provided, then Camel will just use the result exchange as the result.

The following example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .enrich("http:remoteserver/foo")
  .to("direct:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <enrich>
        <constant>http:remoteserver/foo</constant>
    </enrich>
    <to uri="mock:result"/>
</route>
```

```yaml
- from:
    uri: direct:start
    steps:
      - enrich:
          expression:
            constant: "http:remoteserver/foo"
      - to:
          uri: mock:result
```

Would be the same as using `to`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("http:remoteserver/foo")
  .to("direct:result");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="http:remoteserver/foo"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- from:
    uri: direct:start
    steps:
      - to:
          uri: http:remoteserver/foo
      - to:
          uri: mock:result
```

### Using dynamic uris

Both `enrich` and `pollEnrich` supports using dynamic uris computed based on information from the current Exchange. For example, to enrich from a HTTP endpoint where the header with key orderId is used as part of the content-path of the HTTP url:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .enrich().simple("http:myserver/${header.orderId}/order")
  .to("direct:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <enrich>
    <simple>http:myserver/${header.orderId}/order</simple>
  </enrich>
  <to uri="direct:result"/>
</route>
```

```yaml
- from:
    uri: direct:start
    steps:
      - enrich:
          expression:
            simple: "http:myserver/${header.orderId}/order"
      - to:
          uri: mock:result
```

> **Tip**
> See the `cacheSize` option for more details on _how much cache_ to use depending on how many or few unique endpoints are used.

### Using out-of-the-box Aggregation Strategies

The `org.apache.camel.builder.AggregationStrategies` is a builder that can be used for creating commonly used aggregation strategies without having to create a class.

For example, the `ExampleAggregationStrategy` from previously can be built as follows:

```java
AggregationStrategy agg = AggregationStrategies.string(":");
```

There are many other possibilities with the `AggregationStrategies` builder, and for more details see the [AggregationStrategies javadoc](https://www.javadoc.io/static/org.apache.camel/camel-core-model/3.12.0/org/apache/camel/builder/AggregationStrategies.md).

## See More

See [Poll Enrich](pollEnrich-eip.md) EIP