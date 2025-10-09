# Google Pubsub

JVM since1.0.0 Native since1.5.0

Send and receive messages to/from Google Cloud Platform PubSub Service.

## What’s inside

-   [Google Pubsub component](../../../../components/4.14.x/google-pubsub-component.md), URI syntax: `google-pubsub:projectId:destinationName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-google-pubsub)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-google-pubsub</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

By default, the Camel PubSub component uses JDK object serialization via `ObjectOutputStream` whenever the message body is anything other than `String` or `byte[]`.

Since such serialization is not yet supported by GraalVM, this extension provides a custom Jackson based serializer to serialize complex message payloads as JSON.

If your payload contains binary data, then you will need to handle that by creating a custom Jackson Serializer / Deserializer. Refer to the [Quarkus Jackson guide](https://quarkus.io/guides/writing-extensions#customizing-jackson) for information on how to do this.