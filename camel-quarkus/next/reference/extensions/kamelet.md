# Kamelet

JVM since1.7.0 Native since1.7.0

To call Kamelets

## What’s inside

-   [Kamelet component](../../../../components/next/kamelet-component.md), URI syntax: `kamelet:templateId/routeId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-kamelet)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-kamelet</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Using the Kamelet Catalog

A set of pre-made Kamelets can be found in the Kamelet Catalog. To use a Kamelet from the catalog, you need to copy its YAML definition (that you can find [in the camel-kamelets repository](https://github.com/apache/camel-kamelets/)) to your project.

Alternatively, you can add the `camel-kamelets` dependency to your application.

```xml
<dependency>
    <groupId>org.apache.camel.kamelets</groupId>
    <artifactId>camel-kamelets</artifactId>
</dependency>
```

### Custom Kamelets

It’s advised to name files containing your custom Kamelet definitions with the extension `.kamelet.yaml`.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.kamelet.identifiers](#quarkus-camel-kamelet-identifiers)`
Optional comma separated list of kamelet identifiers to configure for native mode support. A kamelet identifier is the Kamelet file name without the `.kamelet.yaml` suffix.

The default value `*` will result in all discovered Kamelet definition files being included into the native image. Note that this configuration option is only relevant when producing a native application.

 | List of `string` | `*` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.