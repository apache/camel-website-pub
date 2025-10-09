# Bean Injection

We support the injection of various resources using `@EndpointInject` or `@BeanInject`. This can be used to inject

-   [Endpoint](endpoint.md) instances which can be used for testing when used with [Mock](../components/4.18.x/mock-component.md) endpoints; see the [Testing](testing.md) for an example.
    
-   [ProducerTemplate](producertemplate.md) instances for [POJO Producing](pojo-producing.md)
    
-   client side proxies for [POJO Producing](pojo-producing.md)
    

## Using @BeanInject

You can inject beans (obtained from the [Registry](registry.md)) into your beans such as `RouteBuilder` classes.

For example to inject a bean named foo, you can enlist the bean in the [Registry](registry.md) such as in a Spring XML file:

```xml
<bean id="foo" class="com.foo.MyFooBean"/>
```

Or in YAML DSL:

```yaml
- beans:
    - name: foo
      type: com.foo.MyFooBean
```

And then in a Java `RouteBuilder` class, you can inject the bean using `@BeanInject` as shown below:

```java
public class MyRouteBuilder extends RouteBuilder {

   @BeanInject("foo")
   MyFooBean foo;

   public void configure() throws Exception {
     ..
   }
}
```

If you omit the name, then Camel does a lookup by type, and injects the bean if there is exactly only one bean of that type enlisted in the [Registry](registry.md).

```java
   @BeanInject
   MyFooBean foo;
```

## Bean Injection with Quarkus

When using Camel with Spring Boot, or Quarkus, then the `@Inject`, or `@Named` annotations can be used to inject Camel resources as well.

## Bean Injection with Spring Boot

Camel has first-class support for Spring Boot, and you can use the Spring annotations such as `@Autowired` to also inject Camel resources.