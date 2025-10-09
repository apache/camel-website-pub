# Custom Load Balancer

This EIP allows you to use your own [Load Balancer](loadBalance-eip.md) implementation.

The Custom Load Balancer eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ref** | **Required** Refers to the custom load balancer to lookup from the registry. |  | String |

## Example

An example using Java DSL:

```java
from("direct:start")
    // using our custom load balancer
    .loadBalance(new MyLoadBalancer())
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

And the same example using XML DSL:

```xml
<!-- this is the implementation of our custom load balancer -->
<bean id="myBalancer" class="com.foo.MyLoadBalancer"/>

<camelContext xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="direct:start"/>
    <loadBalance>
      <!-- refer to my custom load balancer -->
      <customLoadBalancer ref="myBalancer"/>
      <!-- these are the endpoints to balance -->
      <to uri="seda:x"/>
      <to uri="seda:y"/>
      <to uri="seda:z"/>
    </loadBalance>
  </route>
</camelContext>
```

To implement a custom load balancer you can extend some support classes such as `LoadBalancerSupport` and `SimpleLoadBalancerSupport`. The former supports the asynchronous routing engine, and the latter does not. Here is an example of a custom load balancer implementation:

```java
public static class MyLoadBalancer extends LoadBalancerSupport {

    public boolean process(Exchange exchange, AsyncCallback callback) {
        String body = exchange.getIn().getBody(String.class);
        try {
            if ("x".equals(body)) {
                getProcessors().get(0).process(exchange);
            } else if ("y".equals(body)) {
                getProcessors().get(1).process(exchange);
            } else {
                getProcessors().get(2).process(exchange);
            }
        } catch (Throwable e) {
            exchange.setException(e);
        }
        callback.done(true);
        return true;
    }
}
```