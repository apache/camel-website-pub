# Bean Integration

Camel supports the integration of beans and POJOs in a number of ways.

## Annotations

If a bean is defined in Spring XML or scanned using the Spring component scanning mechanism, and a **<camelContext>** is used or a `CamelBeanPostProcessor` then we process a number of Camel annotations to do various things such as injecting resources or producing, consuming or routing messages.

The following annotations is supported and inject by Camel’s `CamelBeanPostProcessor`

 
| Annotation | Description |
| --- | --- |
| `@EndpointInject` | To inject an endpoint, see more details at [POJO Producing](pojo-producing.md). |
| `@BeanInject` | To inject a bean obtained from the [Registry](registry.md). See [Bean Injection](bean-injection.md). |
| `@BeanConfigInject` | To inject a configuration bean obtained from the [Registry](registry.md). The bean is a POJO that represents a set of configuration options, which is automatically configured with values loaded via Camel [Property Placeholders](using-propertyplaceholder.md). |
| `@PropertyInject` | To inject a value using property placeholder. |
| `@Produce` | To inject a producer to send a message to an endpoint. See [POJO Producing](pojo-producing.md). |
| `@Consume` | To inject a consumer on a method. See [POJO Consuming](pojo-consuming.md). |
| `@BindToRegistry` | Used for binding a bean to the registry. If no name is specified, then the bean will have its name auto computed based on the class name, field name, or method name where the annotation is configured. |
| `@DeferredContextBinding` | Used to indicate that if the target type is `CamelContextAware` then the `CamelContext` is deferred and injected later; after the bootstrap of Camel so the `CamelContext` is ready for use. |

See more details at:

-   [POJO Consuming](pojo-consuming.md) to consume and possibly route messages from Camel
    
-   [POJO Producing](pojo-producing.md) to make it easy to produce camel messages from your POJOs
    
-   `@DynamicRouter` Annotation for creating a [Dynamic Router](../components/4.18.x/eips/dynamicRouter-eip.md) from a POJO method
    
-   `@RecipientList` Annotation for creating a [Recipient List](../components/4.18.x/eips/recipientList-eip.md) from a POJO method
    
-   `@RoutingSlip` Annotation for creating a [Routing Slip](../components/4.18.x/eips/routingSlip-eip.md) for a POJO method
    
-   [Bean Injection](bean-injection.md) to inject Camel related resources into your POJOs
    
-   [Using Exchange Pattern Annotations](using-exchange-pattern-annotations.md) describes how the pattern annotations can be used to change the behaviour of method invocations with Spring Remoting or POJO Producing
    

**Example**

See the [POJO Messaging Example](https://github.com/apache/camel-examples/tree/main/pojo-messaging) for how to use the annotations for routing and messaging.

## Using @PropertyInject

Camel allows injecting property placeholders in POJOs using the `@PropertyInject` annotation which can be set on fields and setter methods. For example, you can use that with `RouteBuilder` classes, such as shown below:

_Java-only: injecting a property placeholder value with @PropertyInject_

```java
public class MyRouteBuilder extends RouteBuilder {

    @PropertyInject("hello")
    private String greeting;

    @Override
    public void configure() throws Exception {
        from("direct:start")
            .transform().constant(greeting)
            .to("{{result}}");
    }
}
```

Notice we have annotated the greeting field with `@PropertyInject` and define it to use the key `hello`. Camel will then lookup the property with this key and inject its value, converted to a String type.

You can also use multiple placeholders and text in the key, for example we can do:

_Java-only: using multiple placeholders and text in @PropertyInject_

```java
@PropertyInject("Hello {{name}} how are you?")
private String greeting;
```

This will lookup the placeholder with they key `name`.

You can also add a default value if the key does not exist, such as:

_Java-only: using a default value with @PropertyInject_

```java
@PropertyInject(value = "myTimeout", defaultValue = "5000")
private int timeout;
```

### Using @PropertyInject with arrays, lists, sets or maps

You can also use `@PropertyInject` to inject an array of values. For example, you may configure multiple hostnames in the configuration file, and need to inject this into an `String[]` or `List<String>` field. To do this, you need to tell Camel that the property value should be split using a separator, as follows:

_Java-only: injecting an array of values using separator_

```java
@PropertyInject(value = "myHostnames", separator = ",")
private String[] servers;
```

> **Tip**
> You can also use list/set types, such as `List<String>` or `Set<String>` instead of array.

Then in the `application.properties` file you can define the servers:

```properties
myHostnames = serverA, serverB, serverC
```

> **Tip**
> This also works for fields that are not String based, such as `int[]` for numeric values.

For `Map` types then the values are expected to be in `_key=value_` format, such as:

```properties
myServers = serverA=http://coolstore:4444,serverB=http://megastore:5555
```

You can then inject this into a `Map` as follows:

_Java-only: injecting key-value pairs into a Map_

```java
@PropertyInject(value = "myServers", separator = ",")
private Map servers;
```

You can use generic types in the Map such as the values should be `Integer` values:

_Java-only: injecting a Map with typed values_

```java
@PropertyInject(value = "ports", separator = ",")
private Map<String, Integer> ports;
```

> **Note**
> The generic type can only be a single class type, and cannot be a nested complex type such as `Map<String,Map<Kind,Priority>>`.

## See Also

-   [Bean Injection](bean-injection.md)
    
-   [Bean Binding](bean-binding.md)