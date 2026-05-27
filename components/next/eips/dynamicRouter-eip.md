# Dynamic Router

The [Dynamic Router](http://www.enterpriseintegrationpatterns.com/DynamicRouter.md) from the [EIP patterns](enterprise-integration-patterns.md) allows you to route messages while avoiding the dependency of the router on all possible destinations while maintaining its efficiency.

![image](_images/eip/DynamicRouter.gif)

## Options

The Dynamic Router eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression to call that returns the endpoint(s) to route to in the dynamic routing. Important: The expression will be called in a while loop fashion, until the expression returns null which means the dynamic router is finished. |  | ExpressionDefinition |
| **uriDelimiter** | Sets the uri delimiter to use. | , | String |
| **ignoreInvalidEndpoints** | Ignore the invalidate endpoint exception when try to create a producer with that endpoint. | false | Boolean |
| **cacheSize** | Sets the maximum size used by the org.apache.camel.spi.ProducerCache which is used to cache and reuse producers when using this dynamic router, when uris are reused. Beware that when using dynamic endpoints then it affects how well the cache can be utilized. If each dynamic endpoint is unique then its best to turn off caching by setting this to -1, which allows Camel to not cache both the producers and endpoints; they are regarded as prototype scoped and will be stopped and discarded after use. This reduces memory usage as otherwise producers/endpoints are stored in memory in the caches. However if there are a high degree of dynamic endpoints that have been used before, then it can benefit to use the cache to reuse both producers and endpoints and therefore the cache size can be set accordingly or rely on the default size (1000). If there is a mix of unique and used before dynamic endpoints, then setting a reasonable cache size can help reduce memory usage to avoid storing too many non frequent used producers. |  | Integer |

## Exchange properties

The Dynamic Router eip has no exchange properties.

## Dynamic Router

The Dynamic Router is similar to the [Routing Slip](routingSlip-eip.md) EIP, but with the slip evaluated dynamically _on-the-fly_. The [Routing Slip](routingSlip-eip.md) on the other hand evaluates the slip only once in the beginning.

The Dynamic Router sets the exchange property (`Exchange.SLIP_ENDPOINT`) with the current slip. This allows you to know how far we have processed in the overall slip.

## Example

You can use the `dynamicRouter` as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    // use a bean as the dynamic router
    .dynamicRouter(method(MySlipBean.class, "slip"));
```

```xml
<route>
    <from uri="direct:start"/>
    <dynamicRouter>
        <!-- use a method call on a bean as dynamic router -->
        <method beanType="com.foo.MySlipBean" method="slip"/>
    </dynamicRouter>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - dynamicRouter:
            expression:
              method:
                beanType: com.foo.MySlipBean
                method: slip
```

Which will call a [Bean Method](../languages/bean-language.md) to compute the slip _on-the-fly_. The bean could be implemented as follows:

```java
/**
 * Use this method to compute dynamic where we should route next.
 *
 * @param body the message body
 * @return endpoints to go, or <tt>null</tt> to indicate the end
 */
public String slip(String body) {
    bodies.add(body);
    invoked++;

    if (invoked == 1) {
        return "mock:a";
    } else if (invoked == 2) {
        return "mock:b,mock:c";
    } else if (invoked == 3) {
        return "direct:foo";
    } else if (invoked == 4) {
        return "mock:result";
    }

    // no more so return null
    return null;
}
```

> **Warning**
> **Beware** You must ensure the expression used for the `dynamicRouter` such as a bean, will return `null` to indicate the end. Otherwise, the `dynamicRouter` will keep repeating endlessly.

### Thread safety beans

Mind that this example is only for show and tell. The current implementation is not thread safe. You would have to store the state on the `Exchange`, to ensure thread safety, as shown below:

```java
/**
 * Use this method to compute dynamic where we should route next.
 *
 * @param body the message body
 * @param properties the exchange properties where we can store state between invocations
 * @return endpoints to go, or <tt>null</tt> to indicate the end
 */
public String slip(String body, @ExchangeProperties Map<String, Object> properties) {
    bodies.add(body);

    // get the state from the exchange properties and keep track how many times
    // we have been invoked
    int invoked = 0;
    Object current = properties.get("invoked");
    if (current != null) {
        invoked = Integer.parseInt(current.toString());
    }
    invoked++;
    // and store the state back on the properties
    properties.put("invoked", invoked);

    if (invoked == 1) {
        return "mock:a";
    } else if (invoked == 2) {
        return "mock:b,mock:c";
    } else if (invoked == 3) {
        return "direct:foo";
    } else if (invoked == 4) {
        return "mock:result";
    }

    // no more so return null
    return null;
}
```

You could also store state as message headers, but they are not guaranteed to be preserved during routing, whereas properties on the Exchange are.

## @DynamicRouter annotation

You can also use [Bean Integration](../../../manual/bean-integration.md) with the `@DynamicRouter` annotation, on a Java bean method.

In the example below the `route` method would then be invoked repeatedly as the message is processed dynamically. The idea is to return the next endpoint uri where to go, and to return `null` to end. You can return multiple endpoints if you like, just as the [Routing Slip](routingSlip-eip.md), where each endpoint is separated by a comma.

```java
public class MyDynamicRouter {

    @Consume(uri = "activemq:foo")
    @DynamicRouter
    public String route(@XPath("/customer/id") String customerId, @Header("Location") String location, Document body) {
        // Query a database to find the best match of the endpoint based on the input parameters
        // return the next endpoint uri, where to go. Return null to indicate the end.
    }
}
```

The parameters on the `route` method is bound to information from the Exchange using [Bean Parameter Binding](../../../manual/bean-binding.md).