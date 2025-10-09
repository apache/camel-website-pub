# JavaShell DSL

**Since Camel 3.15**

> **Important**
> This DSL is experimental support level and is not recommended being used for production

The `jsh-dsl` is used for runtime compiling JavaShell routes in an existing running Camel integration. This was invented for Camel K and later ported to Apache Camel.

This means that Camel will load the `.jsh` source during startup and use the JavaShell compiler to transform this into Camel routes.

## Example

The following `example.js` source file:

example.jsh

```java
builder.from("timer:tick")
    .setBody()
        .constant("Hello Camel K!")
    .to("log:info");
```

Can then be loaded and run with Camel CLI or Camel K.

Running with Camel K

```bash
kamel run example.jsh
```

Running with Camel CLI

```bash
camel run example.jsh
```

## See Also

See [DSL](../../../manual/dsl.md)