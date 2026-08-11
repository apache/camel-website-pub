# OpenAI

JVM since3.32.0 Native since3.32.0

OpenAI endpoint for chat completion, Responses API, embeddings, audio transcription, audio translation, and text-to-speech.

## What’s inside

-   [OpenAI component](../../../../components/next/openai-component.md), URI syntax: `openai:operation`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-openai)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-openai</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Structured output with output class in native mode

When using structured output with the `outputClass` option in native mode, you must ensure that the target class is registered for reflection.

This can be done with the `@RegisterForReflection` annotation or configuration property `quarkus.camel.native.reflection.include-patterns`. For example:

```java
@RegisterForReflection
public class MyStructuredOutputClass {
    ...
}
```

```java
public class Routes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:chat")
            .to("openai:chat-completion?outputClass=" + MyStructuredOutputClass.class.getName());
    }
}
```

### Structured output with JSON schema from classpath resource in native mode

When loading JSON schema classpath resources in native mode, you must ensure the resource is included in the native application.

For example, given a route like the following.

```java
public class Routes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:chat")
            .to("openai:chat-completion?jsonSchema=resource:classpath:schemas/mySchema.json");
    }
}
```

Add the following to `application.properties`.

```properties
quarkus.native.resources.includes=schemas/mySchema.json
```

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.