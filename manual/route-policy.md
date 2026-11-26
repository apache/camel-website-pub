# RoutePolicy

A route policy `org.apache.camel.spi.RoutePolicy` is used to control route(s) at runtime. For example, you can use it to determine whether a route should be running or not. However, the policies can support any kind of use cases.

## How it works

You associate a route with a given `RoutePolicy` and then during runtime Camel will invoke callbacks on this policy where you can implement your custom logic. Camel provides a support class that can be used to extend `org.apache.camel.support.RoutePolicySupport` and implement your logic.

There are these callbacks invoked:

-   `onInit`
    
-   `onRemove`
    
-   `onStart`
    
-   `onStop`
    
-   `onSuspend`
    
-   `onResume`
    
-   `onExchangeBegin`
    
-   `onExchangeDone`
    

See the Javadoc of the `org.apache.camel.spi.RoutePolicy` for more details; and also the implementation of the `org.apache.camel.throttling.ThrottlingInflightRoutePolicy` for a concrete example.

Camel provides the following policies out of the box:

-   `org.apache.camel.throttling.ThrottlingInflightRoutePolicy` - a throttling based policy that automatically suspends/resumes route(s) based on metrics from the current in flight exchanges. You can use this to dynamically throttle, e.g. a [JMS](../components/4.22.x/jms-component.md) consumer, to avoid it consuming too fast.
    
-   `org.apache.camel.throttling.ThrottlingExceptionRoutePolicy` - a throttling based policy modeled after the circuit breaker. This policy will stop consuming from an endpoint based on the type of exceptions that are thrown and the threshold setting. The exception an exchange fails with and its causes are matched against the exceptions to throttle on (the same as `onException` and `doCatch`). Suppressed exceptions, such as an exception thrown in a `doFinally` block, are not matched.
    
-   `org.apache.camel.impl.cluster.ClusteredRoutePolicy` - is the foundation for `camel-cluster` which handles Camel routes to become active if a node becomes leader in a cluster.
    

Camel also provides an ability to schedule routes to be activated, deactivated, suspended and/or resumed at certain times during the day using a [ScheduledRoutePolicy](scheduledroutepolicy.md) (offered via the [Quartz](../components/4.22.x/quartz-component.md) component).

And route policy is also used as an implementation details for some of the Camel observability components.

## SuspendableService

If you want to dynamic suspend/resume routes, then it is advised to use `SuspendableService` as it allows for fine-grained suspend and resume operations.

## `ThrottlingInflightRoutePolicy`

The **`ThrottlingInflightRoutePolicy`** is triggered when an [Exchange](exchange.md) is complete, which means that it requires at least one [Exchange](exchange.md) to be complete before it _works_.

The throttling in flight route policy has the following options:

  
| Option | Default | Description |
| --- | --- | --- |
| `scope` | `Route` | A scope for either `Route` or `Context` which defines if the current number of in flight exchanges is context based or for that particular route. |
| `maxInflightExchanges` | `1000` | The maximum threshold when the throttling will start to suspend the route if the current number of in flight exchanges is higher than this value. |
| `resumePercentOfMax` | `70` | A percentage `0..100` which defines when the throttling should resume again in case it has been suspended. |
| `loggingLevel` | `INFO` | The logging level used for logging the throttling activity. |
| `logger` | `ThrottlingInflightRoutePolicy` | The logger category. |

### ThrottlingInflightRoutePolicy compared to the Throttler EIP

The `ThrottlingInflightRoutePolicy` compared to [Throttler](../components/4.22.x/eips/throttle-eip.md) EIP is that it does **not** block during throttling. Its throttling is approximate-based, meaning that its coarser grained and not explicitly precise as the [Throttler](../components/4.22.x/eips/throttle-eip.md) EIP.

The [Throttler](../components/4.22.x/eips/throttle-eip.md) EIP can be much more accurate and only allow a specific number of messages being passed per a given time unit. Also, the `ThrottlingInflightRoutePolicy` is based its metrics on number of in flight exchanges whereas [Throttler](../components/4.22.x/eips/throttle-eip.md) EIP is based on number o messages per time unit.

## `ThrottlingExceptionRoutePolicy`

The **`ThrottlingExceptionRoutePolicy`** works like a circuit breaker on the route consumer:

-   When `failureThreshold` exchanges fail within `failureWindow`, the circuit opens: the policy suspends the consumer (or stops it, if it cannot be suspended). The consumer takes no new messages; with a queue, such as JMS, they wait in the queue.
    
-   After `halfOpenAfter`, the circuit is half open: the policy resumes the consumer, and the next exchange decides. A success closes the circuit, a failure opens it again.
    
-   With a `halfOpenHandler`, the policy calls the handler instead of resuming the consumer, and closes the circuit when the handler returns `true`.
    

The circuit closes by itself, so you do not need to resume the route.

A route can have both a `ThrottlingInflightRoutePolicy` and a `ThrottlingExceptionRoutePolicy`. Then each of them resumes the consumer only when the other one no longer keeps it suspended: the inflight policy does not resume the consumer while the circuit is open, and when the circuit is half open, a consumer that the inflight policy has suspended stays suspended until the inflight policy resumes it. The exception policy keeps suspended only the consumer of the route it opened the circuit for: when it is shared by several routes, the inflight policy of another route resumes its consumer as before, and so it does for a consumer that is started again (such as when the CamelContext is restarted) while the circuit is still open.

The throttling exception route policy has the following options:

  
| Option | Default | Description |
| --- | --- | --- |
| `failureThreshold` | `50` | How many failed exchanges within the `failureWindow` open the circuit. |
| `failureWindow` | `60000` | The sliding window (in millis) in which the failures are counted. |
| `halfOpenAfter` | `30000` | How long (in millis) the circuit stays open before it is half open. Must be greater than 0. |
| `exceptions` |  | Only the exceptions of these types count as a failure (FQN class names separated by comma). By default, any exception counts. |
| `keepOpen` | `false` | Whether to always keep the circuit open (it never closes). This is only intended for development and testing. |
| `halfOpenHandler` |  | A custom `org.apache.camel.throttling.ThrottlingExceptionHalfOpenHandler` that checks whether the circuit can be closed, instead of resuming the consumer. |
| `stateLoggingLevel` | `DEBUG` | The logging level used for logging the state changes. |

For example, to stop consuming from a JMS queue when 5 exchanges fail with a `java.net.ConnectException` within a minute, and to try again after 10 seconds:

-   Java
    
-   XML
    
-   YAML
    

```java
ThrottlingExceptionRoutePolicy policy = new ThrottlingExceptionRoutePolicy();
policy.setFailureThreshold(5);
policy.setFailureWindow(60000);
policy.setHalfOpenAfter(10000);
policy.setExceptions("java.net.ConnectException");

from("jms:queue:orders")
    .routePolicy(policy)
    .to("http://orders-service/orders");
```

```xml
<bean id="ordersPolicy" class="org.apache.camel.throttling.ThrottlingExceptionRoutePolicy">
    <property name="failureThreshold" value="5"/>
    <property name="failureWindow" value="60000"/>
    <property name="halfOpenAfter" value="10000"/>
    <property name="exceptions" value="java.net.ConnectException"/>
</bean>

<route routePolicyRef="ordersPolicy">
    <from uri="jms:queue:orders"/>
    <to uri="http://orders-service/orders"/>
</route>
```

```yaml
- beans:
  - name: ordersPolicy
    type: org.apache.camel.throttling.ThrottlingExceptionRoutePolicy
    properties:
      failureThreshold: 5
      failureWindow: 60000
      halfOpenAfter: 10000
      exceptions: java.net.ConnectException
- route:
    routePolicyRef: ordersPolicy
    from:
      uri: jms:queue:orders
      steps:
        - to:
            uri: http://orders-service/orders
```

## ScheduledRoutePolicy

See [Scheduled Route Policy](scheduledroutepolicy.md) for scheduling based route policy.

## Using RoutePolicy in Camel routes

On the route(s) that should use one or more route policies, you configure this as shown below:

-   Java
    
-   XML
    
-   YAML
    

You configure the route policy as follows from Java DSL, using the `routePolicy` method:

```java
RoutePolicy myPolicy = new MyRoutePolicy();

from("seda:foo")
    .routePolicy(myPolicy)
    .to("mock:result");
```

In XML you configure using the `routePolicyRef` attribute on `<route>` as shown:

```xml
<bean id="myPolicy" class="com.mycompany.MyRoutePolicy"/>

<route routePolicyRef="myPolicy">
    <from uri="seda:foo"/>
    <to uri="mock:result"/>
</route>
```

In YAML you configure using the `routePolicyRef` attribute on `route` node as shown:

```yaml
- route:
    routePolicyRef: myPolicy
    from:
      uri: seda:foo
      steps:
        - to:
            uri: mock:result
```

You can configure one or more route policies (separated by comma), such as:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
    .routePolicy(myPolicy, myOtherPolicy)
    .to("mock:result");
```

```xml
<bean id="myPolicy" class="com.mycompany.MyRoutePolicy"/>

<route routePolicyRef="myPolicy,myOtherPolicy">
    <from uri="seda:foo"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    routePolicyRef: myPolicy,myOtherPolicy
    from:
      uri: seda:foo
      steps:
        - to:
            uri: mock:result
```

## Using RoutePolicyFactory

If you want to use a route policy for every route, you can use a `org.apache.camel.spi.RoutePolicyFactory` as a factory for creating new `RoutePolicy` instance(s) for each route. This can be used when you want to use the same kind of route policy for all.

With the factory, you only need to configure this once, and every route created will have the policy assigned.

There is API on `CamelContext` to add a factory, as shown below

-   Java
    
-   Spring Boot
    
-   Quarkus
    
-   Spring XML
    
-   XML
    
-   YAML
    

```java
CamelContext context = ...
context.addRoutePolicyFactory(new MyRoutePolicyFactory());
```

You can also mark your class with Spring Boot `@Component` for automatic dependency injection

```java
@Component
public class MyRoutePolicyFactory() {

}
```

You can also mark your class with Quarkus `@.ApplicationScoped` for automatic dependency injection

```java
@ApplicationScoped
public class MyRoutePolicyFactory() {

}
```

And from Spring XML DSL you just define a `<bean>` with the factory, and Camel will automatically detect this factory:

```xml
<bean id="myRoutePolicyFactory" class="com.foo.MyRoutePolicyFactory"/>
```

```xml
<bean name="myRoutePolicyFactory" type="com.foo.MyRoutePolicyFactory"/>
```

```yaml
- beans:
    - name: myRoutePolicyFactory
      type: com.foo.MyRoutePolicyFactory
```

> **Tip**
> You can have as many route policy factories as you want, so if you have two factories, you can just add both of them.