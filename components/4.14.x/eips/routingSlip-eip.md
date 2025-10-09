# Routing Slip

Camel supports the [Routing Slip](https://www.enterpriseintegrationpatterns.com/patterns/messaging/RoutingTable.md) from the [EIP patterns](enterprise-integration-patterns.md).

How do we route a message consecutively through a series of processing steps when the sequence of steps is not known at design-time and may vary for each message?

![image](_images/eip/RoutingTableSimple.gif)

Attach a Routing Slip to each message, specifying the sequence of processing steps. Wrap each component with a special message router that reads the Routing Slip and routes the message to the next component in the list.

## Options

The Routing Slip eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression to define the routing slip, which defines which endpoints to route the message in a pipeline style. Notice the expression is evaluated once, if you want a more dynamic style, then the dynamic router eip is a better choice. |  | ExpressionDefinition |
| **uriDelimiter** | Sets the uri delimiter to use. | , | String |
| **ignoreInvalidEndpoints** | Ignore the invalidate endpoint exception when try to create a producer with that endpoint. | false | Boolean |
| **cacheSize** | Sets the maximum size used by the org.apache.camel.spi.ProducerCache which is used to cache and reuse producers when using this routing slip, when uris are reused. Beware that when using dynamic endpoints then it affects how well the cache can be utilized. If each dynamic endpoint is unique then its best to turn off caching by setting this to -1, which allows Camel to not cache both the producers and endpoints; they are regarded as prototype scoped and will be stopped and discarded after use. This reduces memory usage as otherwise producers/endpoints are stored in memory in the caches. However if there are a high degree of dynamic endpoints that have been used before, then it can benefit to use the cache to reuse both producers and endpoints and therefore the cache size can be set accordingly or rely on the default size (1000). If there is a mix of unique and used before dynamic endpoints, then setting a reasonable cache size can help reduce memory usage to avoid storing too many non frequent used producers. |  | Integer |
> **Tip**
> See the `cacheSize` option for more details on _how much cache_ to use depending on how many or few unique endpoints are used.

## Exchange properties

The Routing Slip eip supports 2 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSlipEndpoint** | The endpoint uri of this routing slip. |  | String |
| **CamelToEndpoint** | Endpoint URI where this Exchange is being sent to. |  | String |

## Using Routing Slip

The Routing Slip EIP allows to route a message through a series of [endpoints](../../../manual/endpoint.md) (the slip).

There can be 1 or more endpoint [uris](../../../manual/uris.md) in the slip.

> **Tip**
> A slip can be empty, meaning that the message will not be routed anywhere.

The following route will take any messages sent to the Apache ActiveMQ queue cheese and use the header with key "whereTo" that is used to compute the slip (endpoint [uris](../../../manual/uris.md)).

-   Java
    
-   XML
    

```java
from("activemq:cheese")
  .routingSlip(header("whereTo"));
```

```xml
<route>
  <from uri="activemq:cheese"/>
  <routingSlip>
    <header>whereTo</header>
  </routingSlip>
</route>
```

The value of the header ("whereTo") should be a comma-delimited string of endpoint URIs you wish the message to be routed to. The message will be routed in a [pipeline](pipeline-eip.md) fashion, i.e., one after the other.

The Routing Slip sets a property, `Exchange.SLIP_ENDPOINT`, on the `Exchange` which contains the current endpoint as it advanced though the slip. This allows you to _know_ how far we have processed in the slip.

The Routing Slip will compute the slip **beforehand**, which means the slip is only computed once. If you need to compute the slip _on-the-fly_, then use the [Dynamic Router](dynamicRouter-eip.md) EIP instead.

### How is the slip computed

The Routing Slip uses an [Expression](../../../manual/expression.md) to compute the value for the slip. The result of the expression can be one of:

-   `String`
    
-   `Collection`
    
-   `Iterator` or `Iterable`
    
-   Array
    

If the value is a `String` then the `uriDelimiter` is used to split the string into multiple uris. The default delimiter is comma, but can be re-configured.

### Ignore Invalid Endpoints

The Routing Slip supports `ignoreInvalidEndpoints` (like [Recipient List](recipientList-eip.md) EIP). You can use it to skip endpoints which are invalid.

-   Java
    
-   XML
    

```java
from("direct:start")
  .routingSlip("myHeader").ignoreInvalidEndpoints();
```

```xml
<route>
  <from uri="direct:start"/>
  <routingSlip ignoreInvalidEndpoints="true">
    <header>myHeader</header>
  </routingSlip>
</route>
```

Then let us say the `myHeader` contains the following two endpoints `direct:foo,xxx:bar`. The first endpoint is valid and works. However, the second one is invalid and will just be ignored. Camel logs at DEBUG level about it, so you can see why the endpoint was invalid.