# Writing Integrations in Java

Using Java to write an integration to be deployed using Camel K is no different from defining your routing rules in Camel with the only difference that you do not need to build and package it as a jar.

Example.java

```java
import org.apache.camel.builder.RouteBuilder;

public class Example extends RouteBuilder {
    @Override
    public void configure() throws Exception {
        from("timer:tick")
            .setBody()
              .constant("Hello Camel K!")
            .to("log:info");
    }
}
```

You can run it with the standard command:

```none
kamel run Example.java
```