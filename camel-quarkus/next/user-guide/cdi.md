# Contexts and Dependency Injection (CDI) in Camel Quarkus

CDI plays a central role in Quarkus and Camel Quarkus offers a first class support for it too.

You may use `@Inject`, `@ConfigProperty` and similar annotations e.g. to inject beans and configuration values to your Camel `RouteBuilder`. Here is the `RouteBuilder` from our `timer-log-cdi` [example](examples.md):

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Inject;
import org.apache.camel.builder.RouteBuilder;
import org.eclipse.microprofile.config.inject.ConfigProperty;

@ApplicationScoped (1)
public class TimerRoute extends RouteBuilder {

    @ConfigProperty(name = "timer.period", defaultValue = "1000") (2)
    String period;

    @Inject
    Counter counter;

    @Override
    public void configure() throws Exception {
        fromF("timer:foo?period=%s", period)
                .setBody(exchange -> "Incremented the counter: " + counter.increment())
                .to("log:cdi-example?showExchangePattern=false&showBodyType=false");
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>The <code>@ApplicationScoped</code> annotation is required for <code>@Inject</code> and <code>@ConfigProperty</code> to work in a <code>RouteBuilder</code>. Note that the <code>@ApplicationScoped</code> beans are managed by the CDI container and their life cycle is thus a bit more complex than the one of the plain <code>RouteBuilder</code>. In other words, using <code>@ApplicationScoped</code> in <code>RouteBuilder</code> comes with some boot time penalty, and you should therefore only annotate your <code>RouteBuilder</code> with <code>@ApplicationScoped</code> when you really need it.</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>The value for the <code>timer.period</code> property is defined in <code>src/main/resources/application.properties</code> of the example project.</td></tr></tbody></table>

> **Tip**
> Please refer to the [Quarkus Dependency Injection guide](https://quarkus.io/blog/quarkus-dependency-injection) for more details.

## Accessing `CamelContext`

To access `CamelContext` just inject it into your bean:

```java
import jakarta.inject.Inject;
import jakarta.enterprise.context.ApplicationScoped;
import java.util.stream.Collectors;
import java.util.List;
import org.apache.camel.CamelContext;

@ApplicationScoped
public class MyBean {

    @Inject
    CamelContext context;

    public List<String> listRouteIds() {
        return context.getRoutes().stream().map(Route::getId).sorted().collect(Collectors.toList());
    }
}
```

## `ProducerTemplate` and `ConsumerTemplate`

If you want to use `ProducerTemplate` or `ConsumerTemplate`, then they can be injected into beans.

```java
import jakarta.inject.Inject;
import jakarta.enterprise.context.ApplicationScoped;
import org.apache.camel.ConsumerTemplate;
import org.apache.camel.FluentProducerTemplate;
import org.apache.camel.ProducerTemplate;

@ApplicationScoped
public class MyBean {
    @Inject
    ProducerTemplate producerTemplate;

    @Inject
    FluentProducerTemplate fluentProducerTemplate;

    @Inject
    ConsumerTemplate consumerTemplate;

    public String produceToDirectEndpoint() {
        return producerTemplate.requestBody("direct:start", "Hello World", String.class);
    }

    public String produceToDirectEndpointFluently() {
        return fluentProducerTemplate.to("direct:start").withBody("Hello World").request(String.class);
    }

    public String consumeFromJMSEndpoint() {
        return consumerTemplate.receiveBody("jms:queue:camel", String.class);
    }
}
```

## Accessing the Camel Registry

The Camel registry can be injected into beans.

```java
import jakarta.inject.Inject;
import jakarta.enterprise.context.ApplicationScoped;
import org.apache.camel.spi.Registry;

@ApplicationScoped
public class MyBean {
    @Inject
    Registry registry;

    public CoolBean lookupBean() {
        return registry.lookupByNameAndType("coolBean", CoolBean.class);
    }
}
```

## `@EndpointInject` and `@Produce`

If you are used to `@org.apache.camel.EndpointInject` and `@org.apache.camel.Produce` from [plain Camel](../../../manual/pojo-producing.md) or from Camel on SpringBoot, you can continue using them on Quarkus too.

The following use cases are supported by `org.apache.camel.quarkus:camel-quarkus-core`:

```java
import jakarta.enterprise.context.ApplicationScoped;
import org.apache.camel.EndpointInject;
import org.apache.camel.FluentProducerTemplate;
import org.apache.camel.Produce;
import org.apache.camel.ProducerTemplate;

@ApplicationScoped
class MyBean {

    @EndpointInject("direct:myDirect1")
    ProducerTemplate producerTemplate;

    @EndpointInject("direct:myDirect2")
    FluentProducerTemplate fluentProducerTemplate;

    @EndpointInject("direct:myDirect3")
    DirectEndpoint directEndpoint;

    @Produce("direct:myDirect4")
    ProducerTemplate produceProducer;

    @Produce("direct:myDirect5")
    FluentProducerTemplate produceProducerFluent;

}
```

You can use any other Camel producer endpoint URI instead of `direct:myDirect*`.

> **Warning**
> `@EndpointInject` and `@Produce` are not supported on setter methods - see [#2579](https://github.com/apache/camel-quarkus/issues/2579)

The following use case is supported by `org.apache.camel.quarkus:camel-quarkus-bean`:

```java
import jakarta.enterprise.context.ApplicationScoped;
import org.apache.camel.Produce;

@ApplicationScoped
class MyProduceBean {

    public interface ProduceInterface {
        String sayHello(String name);
    }

    @Produce("direct:myDirect6")
    ProduceInterface produceInterface;

    void doSomething() {
        produceInterface.sayHello("Kermit")
    }

}
```

## CDI and the Camel Bean component

`org.apache.camel.quarkus:camel-quarkus-bean` artifact brings support for the following features:

### Refer to a bean by name

To refer to a bean in a route definition by name, just annotate the bean with `@Named("myNamedBean")` and `@ApplicationScoped` (or some other [supported](https://quarkus.io/guides/cdi-reference#supported_features) scope). The `@RegisterForReflection` annotation is important for the native mode.

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Named;
import io.quarkus.runtime.annotations.RegisterForReflection;

@ApplicationScoped
@Named("myNamedBean")
@RegisterForReflection
public class NamedBean {
    public String hello(String name) {
        return "Hello " + name + " from the NamedBean";
    }
}
```

Then you can use the `myNamedBean` name in a route definition:

```java
import org.apache.camel.builder.RouteBuilder;
public class CamelRoute extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:named")
                .bean("myNamedBean", "hello");
        /* ... which is an equivalent of the following: */
        from("direct:named")
                .to("bean:myNamedBean?method=hello");
    }
}
```

As an alternative to `@Named`, you may also use `io.smallrye.common.annotation.Identifier` to name and identify a bean.

```java
import jakarta.enterprise.context.ApplicationScoped;
import io.quarkus.runtime.annotations.RegisterForReflection;
import io.smallrye.common.annotation.Identifier;

@ApplicationScoped
@Identifier("myBeanIdentifier")
@RegisterForReflection
public class MyBean {
    public String hello(String name) {
        return "Hello " + name + " from MyBean";
    }
}
```

Then refer to the identifier value within the Camel route:

```java
import org.apache.camel.builder.RouteBuilder;
public class CamelRoute extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
                .bean("myBeanIdentifier", "Camel");
    }
}
```

> **Note**
> We aim at supporting all use cases listed in [Bean binding](../../../manual/bean-binding.md) section of Camel documentation. Do not hesitate to [file an issue](https://github.com/apache/camel-quarkus/issues) if some bean binding scenario does not work for you.

### `@Consume`

The `camel-quarkus-bean` artifact brings support for `@org.apache.camel.Consume` - see the [Pojo consuming](../../../manual/pojo-consuming.md) section of Camel documentation.

Declaring a class like the following

```java
import org.apache.camel.Consume;
public class Foo {

  @Consume("activemq:cheese")
  public void onCheese(String name) {
    ...
  }
}
```

will automatically create the following Camel route

```java
from("activemq:cheese").bean("foo1234", "onCheese")
```

for you. Note that Camel Quarkus will implicitly add `@jakarta.inject.Singleton` and `jakarta.inject.Named("foo1234")` to the bean class, where `1234` is a hash code obtained from the fully qualified class name. If your bean has some CDI scope (such as `@ApplicationScoped`) or `@Named("someName")` set already, those will be honored in the auto-created route.

## CDI Contexts & `ContextNotActiveException`

When using CDI beans in `bean` endpoints, in the `.bean` or `.process` EIPs, there is the potential for bean method invocations to throw `ContextNotActiveException`.

Typically, this can happen when invoking `list` & `query` operations on a Hibernate Panache entity within your bean or processor methods. To ensure such beans have access to the request scope, you can annotate methods with `@ActivateRequestContext`.

For example in a bean.

```java
@Singleton
public class GreetingsBean {
    @ActivateRequestContext
    public String greet() {
        Greeting greeting = Greeting.findById(1);
        return greeting.getMessage();
    }
}
```

In `Processor` bean, annotate the `process` method with `@ActivateRequestContext`.

```java
@Singleton
public class GreetingsProcessor implements Processor {
    @Override
    @ActivateRequestContext
    public void process(Exchange exchange) {
        Greeting greeting = Greeting.findById(1);
        exchange.getMessage().setBody(greeting.getMessage());
    }
}
```