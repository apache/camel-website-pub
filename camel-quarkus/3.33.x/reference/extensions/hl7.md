# HL7

JVM since1.1.0 Native since1.8.0

Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec.

## What’s inside

-   [HL7 data format](../../../../components/4.18.x/dataformats/hl7-dataformat.md)
    
-   [HL7 Terser language](../../../../components/4.18.x/languages/hl7terser-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-hl7)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-hl7</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

For MLLP with TCP, Netty is the only supported means of running an Hl7 MLLP listener. Mina is not supported since it has no GraalVM native support at present.

Optional support for `HL7MLLPNettyEncoderFactory` & `HL7MLLPNettyDecoderFactory` codecs can be obtained by adding a dependency in your project `pom.xml` to `camel-quarkus-netty`.