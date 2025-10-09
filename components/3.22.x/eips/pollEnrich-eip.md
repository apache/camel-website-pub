# Poll Enrich

Camel supports the [Content Enricher](http://www.enterpriseintegrationpatterns.com/DataEnricher.md) from the [EIP patterns](enterprise-integration-patterns.md).

![image](_images/eip/DataEnricher.gif)

In Camel the Content Enricher can be done in several ways:

-   Using [Enrich](enrich-eip.md) EIP or [Poll Enrich](#) EIP
    
-   Using a [Message Translator](message-translator.md)
    
-   Using a [Processor](../../../manual/processor.md) with the enrichment programmed in Java
    
-   Using a [Bean](bean-eip.md) EIP with the enrichment programmed in Java
    

The most natural Camel approach is using [Enrich](enrich-eip.md) EIP, which comes as two kinds:

-   [Enrich](enrich-eip.md) EIP - This is the most common content enricher that uses a `Producer` to obtain the data. It is usually used for [Request Reply](requestReply-eip.md) messaging, for instance to invoke an external web service.
    
-   [Poll Enrich](#) EIP - Uses a [Polling Consumer](polling-consumer.md) to obtain the additional data. It is usually used for [Event Message](event-message.md) messaging, for instance to read a file or download a [FTP](../ftp-component.md) file.
    

> **Note**
> This page documents the Poll Enrich EIP.

## Options

The Poll Enrich eip supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **expression** | **Required** Expression that computes the endpoint uri to use as the resource endpoint to enrich from. |  | ExpressionDefinition |
| **aggregationStrategy** | Sets the AggregationStrategy to be used to merge the reply from the external service, into a single outgoing message. By default Camel will use the reply from the external service as outgoing message. |  | AggregationStrategy |
| **aggregationStrategyMethodName** | This option can be used to explicit declare the method name to use, when using POJOs as the AggregationStrategy. |  | String |
| **aggregationStrategyMethodAllowNull** | If this option is false then the aggregate method is not used if there was no data to enrich. If this option is true then null values is used as the oldExchange (when no data to enrich), when using POJOs as the AggregationStrategy. |  | String |
| **aggregateOnException** | If this option is false then the aggregate method is not used if there was an exception thrown while trying to retrieve the data to enrich from the resource. Setting this option to true allows end users to control what to do if there was an exception in the aggregate method. For example to suppress the exception or set a custom message body etc. | false | Boolean |
| **timeout** | Timeout in millis when polling from the external service. The timeout has influence about the poll enrich behavior. It basically operations in three different modes: negative value - Waits until a message is available and then returns it. Warning that this method could block indefinitely if no messages are available. 0 - Attempts to receive a message exchange immediately without waiting and returning null if a message exchange is not available yet. positive value - Attempts to receive a message exchange, waiting up to the given timeout to expire if a message is not yet available. Returns null if timed out The default value is -1 and therefore the method could block indefinitely, and therefore its recommended to use a timeout value. | \-1 | String |
| **cacheSize** | Sets the maximum size used by the org.apache.camel.spi.ConsumerCache which is used to cache and reuse consumers when uris are reused. Beware that when using dynamic endpoints then it affects how well the cache can be utilized. If each dynamic endpoint is unique then its best to turn of caching by setting this to -1, which allows Camel to not cache both the producers and endpoints; they are regarded as prototype scoped and will be stopped and discarded after use. This reduces memory usage as otherwise producers/endpoints are stored in memory in the caches. However if there are a high degree of dynamic endpoints that have been used before, then it can benefit to use the cache to reuse both producers and endpoints and therefore the cache size can be set accordingly or rely on the default size (1000). If there is a mix of unique and used before dynamic endpoints, then setting a reasonable cache size can help reduce memory usage to avoid storing too many non frequent used producers. |  | Integer |
| **ignoreInvalidEndpoint** | Ignore the invalidate endpoint exception when try to create a producer with that endpoint. | false | Boolean |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Content enrichment using Poll Enrich EIP

`pollEnrich` uses a [Polling Consumer](polling-consumer.md) to obtain the additional data. It is usually used for [Event Message](event-message.md) messaging, for instance to read a file or download a FTP file.

The `pollEnrich` works just the same as `enrich`, however as it uses a [Polling Consumer](polling-consumer.md) we have three methods when polling:

-   `receive` - Waits until a message is available and then returns it. **Warning** that this method could block indefinitely if no messages are available.
    
-   `receiveNoWait` - Attempts to receive a message exchange immediately without waiting and returning `null` if a message exchange is not available yet.
    
-   `receive(timeout)` - Attempts to receive a message exchange, waiting up to the given timeout to expire if a message is not yet available. Returns the message or `null` if the timeout expired.
    

### Poll Enrich with timeout

It is good practice to use timeout value.

By default, Camel will use the `receive` which may block until there is a message available. It is therefore recommended to always provide a timeout value, to make this clear that we may wait for a message, until the timeout is hit.

You can pass in a timeout value that determines which method to use:

-   if timeout is `-1` or other negative number then `receive` is selected (**Important:** the `receive` method may block if there is no message)
    
-   if timeout is `0` then `receiveNoWait` is selected
    
-   otherwise, `receive(timeout)` is selected
    

The timeout values is in millis.

### Using Poll Enrich

The content enricher (`pollEnrich`) retrieves additional data from a _resource endpoint_ in order to enrich an incoming message (contained in the _original exchange_).

An `AggregationStrategy` is used to combine the original exchange and the _resource exchange_. The first parameter of the `AggregationStrategy.aggregate(Exchange, Exchange)` method corresponds to the original exchange, the second parameter the resource exchange.

Here’s an example for implementing an `AggregationStrategy`, which merges the two data together as a `String` with colon separator:

```java
public class ExampleAggregationStrategy implements AggregationStrategy {

    public Exchange aggregate(Exchange original, Exchange resource) {
        // this is just an example, for real-world use-cases the
        // aggregation strategy would be specific to the use-case

        if (resource == null) {
            return original;
        }
        Object oldBody = original.getIn().getBody();
        Object newBody = resource.getIn().getBody();
        original.getIn().setBody(oldBody + ":" + newBody);
        return original;
    }

}
```

You then use the `AggregationStrategy` with the `pollEnrich` in the Java DSL as shown:

```java
AggregationStrategy aggregationStrategy = ...

from("direct:start")
  .pollEnrich("file:inbox?fileName=data.txt", 10000, aggregationStrategy)
  .to("mock:result");
```

In the example Camel will poll a file (timeout 10 seconds). The `AggregationStrategy` is then used to merge the file with the existing `Exchange`.

In XML DSL you use `pollEnrich` as follows:

```xml
<bean id="myStrategy" class="com.foo.ExampleAggregationStrategy"/>

<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="direct:start"/>
    <pollEnrich timeout="10000" aggregationStrategy="myStrategy">
      <constant>file:inbox?fileName=data.txt</constant>
    </pollEnrich>
    <to uri="mock:result"/>
  </route>
</camelContext>
```

### Using Poll Enrich with Rest DSL

You can also use `pollEnrich` with [Rest DSL](../../../manual/rest-dsl.md) to for example download a file from [AWS S3](../aws2-s3-component.md) as the response of an API call.

```xml
<rest path="/report">
    <description>Report REST API</description>
    <get path="/{id}/payload">
        <route id="report-payload-download">
            <pollEnrich>
                <constant>aws-s3:xavier-dev?amazonS3Client=#s3client&amp;deleteAfterRead=false&amp;fileName=report-file.pdf</constant>
            </pollEnrich>
        </route>
    </get>
</rest>
```

Notice that the enriched endpoint is a constant, however Camel also supports dynamic endpoints which is covered next.

### Poll Enrich with Dynamic Endpoints

Both `enrich` and `pollEnrich` supports using dynamic uris computed based on information from the current `Exchange`.

For example to `pollEnrich` from an endpoint that uses a header to indicate a SEDA queue name:

```java
from("direct:start")
  .pollEnrich().simple("seda:${header.queueName}")
  .to("direct:result");
```

And in XML DSL:

```xml
<route>
  <from uri="direct:start"/>
  <pollEnrich>
    <simple>seda:${header.queueName}</simple>
  </pollEnrich>
  <to uri="direct:result"/>
</route>
```

> **Tip**
> See the `cacheSize` option for more details on _how much cache_ to use depending on how many or few unique endpoints are used.

## See More

See [Enrich](enrich-eip.md) EIP