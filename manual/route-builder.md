# RouteBuilder

The `RouteBuilder` is a base class which is derived from to create routing rules using the Java DSL. Instances of `RouteBuilder` are then added to the `CamelContext`.

## RouteBuilder example

The following shows an example of a `RouteBuilder` in Java DSL:

```java
import org.apache.camel.builder.RouteBuilder;

/**
 * A Camel Java DSL Router
 */
public class MyRouteBuilder extends RouteBuilder {

    /**
     * Let's configure the Camel routing rules using Java code...
     */
    public void configure() {

        // here is a sample which processes the input files
        // (leaving them in place - see the 'noop' flag)
        // then performs content based routing on the message using XPath
        from("file:src/data?noop=true")
            .choice()
                .when(xpath("/person/city = 'London'"))
                    .to("file:target/messages/uk")
                .otherwise()
                    .to("file:target/messages/others");
    }

}
```

In the `configure` method we can define Camel [Routes](routes.md).

## More Information

See more in [DSL](dsl.md), [Java DSL](java-dsl.md) and [Routes](routes.md).