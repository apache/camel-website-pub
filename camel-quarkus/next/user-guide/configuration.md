# Configuration

Camel Quarkus automatically configures and deploys a Camel Context bean which by default is started/stopped according to the Quarkus Application lifecycle. The configuration step happens at build time during Quarkus' augmentation phase, and it is driven by the Camel Quarkus extensions which can be tuned using Camel Quarkus specific `quarkus.camel.*` properties.

> **Note**
> `quarkus.camel.*` configuration properties are documented on the individual extension pages - see e.g. [Camel Quarkus Core](../reference/extensions/core.md).

After the configuration is done, a minimal Camel Runtime is assembled and started in the [RUNTIME\_INIT](https://quarkus.io/guides/writing-extensions#bootstrap-three-phases) phase.

## Configuring Camel components

### `application.properties`

To configure components and other aspects of Apache Camel through properties, make sure that your application depends on `camel-quarkus-core` directly or transitively. Because most Camel Quarkus extensions depend on `camel-quarkus-core`, you typically do not need to add it explicitly.

`camel-quarkus-core` brings functionalities from [Camel Main](../../../components/next/others/main.md) to Camel Quarkus.

In the example below, we set a specific `ExchangeFormatter` configuration on the `LogComponent` via `application.properties`:

```properties
camel.component.log.exchange-formatter = #class:org.apache.camel.support.processor.DefaultExchangeFormatter
camel.component.log.exchange-formatter.show-exchange-pattern = false
camel.component.log.exchange-formatter.show-body-type = false
```

### CDI

You can also configure a component programmatically using CDI.

The recommended method is to observe the `ComponentAddEvent` and configure the component before the routes and the `CamelContext` are started:

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.enterprise.event.Observes;
import org.apache.camel.quarkus.core.events.ComponentAddEvent;
import org.apache.camel.component.log.LogComponent;
import org.apache.camel.support.processor.DefaultExchangeFormatter;

@ApplicationScoped
public static class EventHandler {
    public void onComponentAdd(@Observes ComponentAddEvent event) {
        if (event.getComponent() instanceof LogComponent) {
            /* Perform some custom configuration of the component */
            LogComponent logComponent = ((LogComponent) event.getComponent());
            DefaultExchangeFormatter formatter = new DefaultExchangeFormatter();
            formatter.setShowExchangePattern(false);
            formatter.setShowBodyType(false);
            logComponent.setExchangeFormatter(formatter);
        }
    }
}
```

#### Producing a `@Named` component instance

Alternatively, you can create and configure the component yourself in a `@Named` producer method. This works as Camel uses the component URI scheme to look-up components from its registry. For example, in the case of a `LogComponent` Camel looks for a `log` named bean.

> **Warning**
> Please note that while producing a `@Named` component bean will usually work, it may cause subtle issues with some components.
>
> Camel Quarkus extensions may do one or more of the following:
>
> -   Pass custom subtype of the default Camel component type. See the [Vert.x WebSocket extension](https://github.com/apache/camel-quarkus/blob/main/extensions/vertx-websocket/runtime/src/main/java/org/apache/camel/quarkus/component/vertx/websocket/VertxWebsocketRecorder.java#L42) example.
>     
> -   Perform some Quarkus specific customization of the component. See the [JPA extension](https://github.com/apache/camel-quarkus/blob/main/extensions/jpa/runtime/src/main/java/org/apache/camel/quarkus/component/jpa/CamelJpaRecorder.java#L35) example.
>     
>
> These actions are not performed when you produce your own component instance, therefore, configuring components in an observer method is the recommended method.

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Named;

import org.apache.camel.component.log.LogComponent;
import org.apache.camel.support.processor.DefaultExchangeFormatter;

@ApplicationScoped
public class Configurations {
    /**
     * Produces a {@link LogComponent} instance with a custom exchange formatter set-up.
     */
    @Named("log") (1)
    LogComponent log() {
        DefaultExchangeFormatter formatter = new DefaultExchangeFormatter();
        formatter.setShowExchangePattern(false);
        formatter.setShowBodyType(false);

        LogComponent component = new LogComponent();
        component.setExchangeFormatter(formatter);

        return component;
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>The <code>"log"</code> argument of the <code>@Named</code> annotation can be omitted as long as the name of the method is the same.</td></tr></tbody></table>

## Configuration by convention

In addition to support configuring Camel through properties, `camel-quarkus-core` allows you to use conventions to configure the Camel behavior. For example, if there is a single `ExchangeFormatter` instance in the CDI container, then it will automatically wire that bean to the `LogComponent`.

Component options for which this is supported are marked as _Autowired_ on their documentation pages - see e.g. the `exchangeFormatter` option on the [Log component](../../../components/next/log-component.html#_component_option_exchangeFormatter) page.

You can pass `autowiredEnabled=false` to disable it.

In case autowiring is performed for some component option, you should see a similar INFO-level message in the application log:

```shell
Autowired property: exchangeFormatter on component: log as exactly one instance of type: software.amazon.org.apache.camel.spi.ExchangeFormatter (org.apache.camel.support.processor.DefaultExchangeFormatter) found in the registry
```

### Default beans and Camel component autowiring

Quarkus has the concept of [Default beans](https://quarkus.io/guides/cdi-reference#default_beans). Many Quarkus extensions produce CDI beans for types that can be autowired into Camel components. Default beans always take priority for Camel component autowiring, when there are multiple beans for the same target type.

For example, Quarkus JDBC driver and Hibernate ORM extensions allow you to configure applications with both 'default' and 'named' configurations. Without explicitly specifying which `DataSource` or `EntityManagerFactory` you want to work with via endpoint URI options, the default bean for those types will take priority for autowiring.

## What’s next?

We recommend to continue with [CDI](cdi.md).