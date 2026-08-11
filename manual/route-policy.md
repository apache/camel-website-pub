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
    
-   `org.apache.camel.throttling.ThrottlingExceptionRoutePolicy` - a throttling based policy modeled after the circuit breaker. This policy will stop consuming from an endpoint based on the type of exceptions that are thrown and the threshold setting.
    
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

In XML you configure using the `routePolictRef` attribute on `<route>` as shown:

```xml
<bean id="myPolicy" class="com.mycompany.MyRoutePolicy"/>

<route routePolicyRef="myPolicy">
    <from uri="seda:foo"/>
    <to uri="mock:result"/>
</route>
```

In YAML you configure using the `routePolictRef` attribute on `route` node as shown:

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