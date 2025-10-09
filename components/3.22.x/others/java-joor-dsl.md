# Java DSL (runtime compiled)

**Since Camel 3.9**

The `java-joor-dsl` is used for runtime compiling Java routes in an existing running Camel integration. This was invented for Camel K and later ported to Apache Camel.

This means that Camel will load the `.java` source during startup and compile this to Java byte code as `.class`, which then are loaded via class loader and behaves as regular Java compiled routes.

## Example

The following `MyRoute.java` source file:

MyRoute.java

```java
import org.apache.camel.builder.RouteBuilder;

public class MyRoute extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        from("timer:tick")
            .setBody()
                .constant("Hello Camel K!")
            .to("log:info");
    }
}
```

Can then be loaded and run with Camel CLI or Camel K.

Running with Camel K

```bash
kamel run MyRoute.java
```

Running with Camel CLI

```bash
camel run MyRoute.java
```

## See Also

See [DSL](../../../manual/dsl.md)