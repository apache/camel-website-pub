# XSLT

JVM since0.4.0 Native since0.4.0

Transforms XML payload using an XSLT template.

## What’s inside

-   [XSLT component](../../../../components/4.18.x/xslt-component.md), URI syntax: `xslt:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-xslt)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-xslt</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

To optimize XSLT processing, the extension needs to know the locations of the XSLT templates at build time. The XSLT source URIs have to be passed via the `quarkus.camel.xslt.sources` property. Multiple URIs can be separated by comma.

```properties
quarkus.camel.xslt.sources = transform.xsl, classpath:path/to/my/file.xsl
```

Scheme-less URIs are interpreted as `classpath:` URIs.

Only `classpath:` URIs are supported on Quarkus native mode. `file:`, `http:` and other kinds of URIs can be used on JVM mode only.

`<xsl:include>` and `<xsl:messaging>` XSLT elements are also supported in JVM mode only right now.

If `aggregate` DSL is used, `XsltSaxonAggregationStrategy` has to be used such as

```java
from("file:src/test/resources?noop=true&sortBy=file:name&antInclude=*.xml")
   .routeId("aggregate").noAutoStartup()
   .aggregate(new XsltSaxonAggregationStrategy("xslt/aggregate.xsl"))
   .constant(true)
   .completionFromBatchConsumer()
   .log("after aggregate body: ${body}")
   .to("mock:transformed");
```

Also, it’s only supported on JVM mode.

### Configuration

TransformerFactory features can be configured using following property:

```properties
quarkus.camel.xslt.features."http\://javax.xml.XMLConstants/feature/secure-processing"=false
```

Features are applied to every template the component transforms with, whether it was compiled to a translet at build time or loaded at runtime. A feature the `TransformerFactory` does not support fails endpoint creation.

> **Warning**
> Disabling secure-processing permits templates to call Xalan extension functions, and is logged as a warning on startup. Only do this where every template the application transforms with is trusted.

### External access

The extension transforms with Xalan-J rather than the XSLT implementation built into the JDK, because translets have to be compiled ahead of time to work in native mode. Xalan-J 2.7.x predates JAXP 1.5 and cannot honour `javax.xml.XMLConstants.ACCESS_EXTERNAL_DTD` or `ACCESS_EXTERNAL_STYLESHEET`, so `setAttribute` throws for both, and its secure-processing feature restricts extension functions without implying the external access restrictions the JDK applies under the same feature. The extension applies those restrictions itself:

-   Documents being transformed are parsed with an `XMLReader` that does not resolve external general entities, so a `SYSTEM` entity in a `DOCTYPE` declaration does not expand into the result. A `SAXSource` carrying an `XMLReader` the caller configured is used as it is.
    
-   Resources fetched at transform time by the `document()` function are denied unless a `javax.xml.transform.URIResolver` resolves them. This applies to every entry point that hands out something to transform with, so a `TransformerHandler` or an `XMLFilter` is restricted just as a `Transformer` is. The component installs a resolver on every transformer it uses, so routes resolve `document()` as they do on plain Camel.
    

`<xsl:import>` and `<xsl:include>` are not restricted. Xalan dereferences those hrefs itself while compiling a stylesheet, ignoring the resolver it consulted first. Stylesheets are deployment owned rather than attacker controlled, and the component resolves includes through its own unrestricted resolver in any case.

> **Note**
> This factory is registered as the JAXP default, so the restrictions above also apply to code in the application that obtains a `TransformerFactory` through `TransformerFactory.newInstance()`.

### Extension functions support

[Xalan’s extension functions](https://xml.apache.org/xalan-j/extensions.md) do work properly only when:

1.  Secure-processing is disabled
    
2.  Functions are defined in a separate jar
    
3.  Functions are augmented during native build phase. For example, they can be registered for reflection:
    

@RegisterForReflection(targets = { my.Functions.class })
public class FunctionsConfiguration {
}

> **Note**
> The content of the XSLT source URIs is parsed and compiled into Java classes at build time. These Java classes are the only source of XSLT information at runtime. The XSLT source files may not be included in the application archive at all.

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.xslt.sources](#quarkus-camel-xslt-sources)`
A comma separated list of templates to compile.

 | List of `string` |  |
| `[quarkus.camel.xslt.package-name](#quarkus-camel-xslt-package-name)`

The package name for the generated classes.

 | `string` | `org.apache.camel.quarkus.component.xslt.generated` |
| `[quarkus.camel.xslt.features."features"](#quarkus-camel-xslt-features-features)`

TransformerFactory features.

 | `Map<String,Boolean>` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.