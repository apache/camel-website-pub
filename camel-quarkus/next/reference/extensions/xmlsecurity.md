# XML Security Sign

JVM since1.1.0 Native since1.7.0

Sign XML payloads using the XML signature specification.

## What’s inside

-   [XML Security data format](../../../../components/4.22.x/dataformats/xmlSecurity-dataformat.md)
    
-   [XML Security Sign component](../../../../components/4.22.x/xmlsecurity-sign-component.md), URI syntax: `xmlsecurity-sign:name`
    
-   [XML Security Verify component](../../../../components/4.22.x/xmlsecurity-verify-component.md), URI syntax: `xmlsecurity-verify:name`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-xmlsecurity)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-xmlsecurity</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

There is currently no native mode support for XSLT based transform methods on the `xmlsecurity` producer via the `transformMethods` URI option.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).