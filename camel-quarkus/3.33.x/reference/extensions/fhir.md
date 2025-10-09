# FHIR

JVM since0.3.0 Native since0.3.0

Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. Marshall and unmarshall FHIR objects to/from JSON. Marshall and unmarshall FHIR objects to/from XML.

## What’s inside

-   [FHIR component](../../../../components/4.18.x/fhir-component.md), URI syntax: `fhir:apiName/methodName`
    
-   [FHIR JSon data format](../../../../components/4.18.x/dataformats/fhirJson-dataformat.md)
    
-   [FHIR XML data format](../../../../components/4.18.x/dataformats/fhirXml-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-fhir)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-fhir</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Configuring the `FhirContext` in native mode

To ensure `camel-quarkus-fhir` operates correctly in native mode, it is important that the FHIR component and data formats use a native mode optimized `FhirContext`. Examples of how to achieve this follow below.

> **Note**
> To use a particular FHIR version in native mode, you must ensure that it is enabled via the configuration options mentioned below.

Endpoint configuration when using the default `R4` FHIR version.

```java
public class FhirRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
            .to("fhir://create/resource?fhirContext=#R4&inBody=resourceAsString");
    }
}
```

Endpoint configuration when using a custom FHIR version (e.g `R5`).

```java
public class FhirRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
            .to("fhir://create/resource?fhirVersion=R5&fhirContext=#R5&inBody=resourceAsString");
    }
}
```

Instead of setting the `fhirContext` option on every endpoint URI, you can instead configure it directly on the FHIR component.

```properties
camel.component.fhir.fhir-context=#R4
```

FHIR data format configuration.

```java
public class FhirRoutes extends RouteBuilder {
    // Each FHIR version has a corresponding injectable named bean
    @Inject
    @Named("R4")
    FhirContext r4FhirContext;

    @Inject
    @Named("R5")
    FhirContext r5FhirContext;

    @Override
    public void configure() {
        // Configure FhirJsonDataFormat with the default R4 FhirContext
        FhirJsonDataFormat fhirJsonDataFormat = new FhirJsonDataFormat();
        fhirJsonDataFormat.setFhirContext(r4FhirContext);

        // Configure FhirXmlDataFormat with a custom version and the corresponding FhirContext
        FhirXmlDataFormat fhirXmlDataFormat = new FhirXmlDataFormat();
        fhirXmlDataFormat.setVersion("R5");
        fhirXmlDataFormat.setFhirContext(r5FhirContext);

        from("direct:marshalFhirJson")
            .marshal(fhirJsonDataFormat);

        from("direct:marshalFhirXml")
            .marshal(fhirXmlDataFormat);
    }
}
```

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

## Additional Camel Quarkus configuration

By default, only FHIR version `R4` is enabled in native mode, since that is also the default version configured on the FHIR component and data formats.

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.fhir.enable-dstu2](#quarkus-camel-fhir-enable-dstu2)`
Enable FHIR DSTU2 Specs in native mode.

 | `boolean` | `false` |
| `[quarkus.camel.fhir.enable-dstu2_hl7org](#quarkus-camel-fhir-enable-dstu2_hl7org)`

Enable FHIR DSTU2\_HL7ORG Specs in native mode.

 | `boolean` | `false` |
| `[quarkus.camel.fhir.enable-dstu2_1](#quarkus-camel-fhir-enable-dstu2_1)`

Enable FHIR DSTU2\_1 Specs in native mode.

 | `boolean` | `false` |
| `[quarkus.camel.fhir.enable-dstu3](#quarkus-camel-fhir-enable-dstu3)`

Enable FHIR DSTU3 Specs in native mode.

 | `boolean` | `false` |
| `[quarkus.camel.fhir.enable-r4](#quarkus-camel-fhir-enable-r4)`

Enable FHIR R4 Specs in native mode.

 | `boolean` | `true` |
| `[quarkus.camel.fhir.enable-r5](#quarkus-camel-fhir-enable-r5)`

Enable FHIR R5 Specs in native mode.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.