# AS2

JVM since1.0.0 Native since1.0.0

Transfer data securely and reliably using the AS2 protocol (RFC4130).

## What’s inside

-   [AS2 component](../../../../components/4.18.x/as2-component.md), URI syntax: `as2:apiName/methodName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-as2)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-as2</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

Depending on its configuration, this component may require SSL encryption on its connections. In such a case, you will need to add `quarkus.ssl.native=true` to your `application.properties`. See also [Quarkus native SSL guide](https://quarkus.io/guides/native-and-ssl) and [Native mode](../../user-guide/native-mode.md) section of Camel Quarkus user guide.