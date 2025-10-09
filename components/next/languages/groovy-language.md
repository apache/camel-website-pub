# Groovy

**Since Camel 1.3**

Camel has support for using [Groovy](http://www.groovy-lang.org/).

For example, you can use Groovy in a [Predicate](../../../manual/predicate.md) with the [Message Filter](../eips/filter-eip.md) EIP.

```java
groovy("someGroovyExpression")
```

## Groovy Options

The Groovy language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Usage

### Groovy Context

Camel will provide exchange information in the Groovy context (just a `Map`). The `Exchange` is transferred as:

 
| key | value |
| --- | --- |
| `body` | The message body. |
| `header` | The headers of the message. |
| `headers` | The headers of the message. |
| `variable` | The exchange variables |
| `variables` | The exchange variables |
| `exchangeProperty` | The exchange properties. |
| `exchangeProperties` | The exchange properties. |
| `exchange` | The `Exchange` itself. |
| `camelContext` | The Camel Context. |
| `exception` | If the exchange failed then this is the caused exception. |
| `request` | The message. |
| `response` | **Deprecated** The Out message (only for InOut message exchange pattern). |
| `attachments` | A `Map<String,jakarta.activation.DataHandler>` containing file attachments such as from HTTP file uploads, or emails containing files. |
| `log` | Can be used for logging purposes such as `log.info('Using body: {}', body)`. |

### How to get the result from multiple statements script

As the Groovy script engine evaluate method just return a `Null` if it runs a multiple statements script. Camel now looks up the value of script result by using the key of `result` from the value set. If you have multiple statements scripts, you need to make sure you set the value of result variable as the script return value.

```groovy
bar = "baz"
// some other statements ...
// camel take the result value as the script evaluation result
result = body * 2 + 1
```

### Customizing Groovy Shell

For very special use-cases you may need to use a custom `GroovyShell` instance in your Groovy expressions. To provide the custom `GroovyShell`, add an implementation of the `org.apache.camel.language.groovy.GroovyShellFactory` SPI interface to the Camel registry.

```java
public class CustomGroovyShellFactory implements GroovyShellFactory {

  public GroovyShell createGroovyShell(Exchange exchange) {
    ImportCustomizer importCustomizer = new ImportCustomizer();
    importCustomizer.addStaticStars("com.example.Utils");
    CompilerConfiguration configuration = new CompilerConfiguration();
    configuration.addCompilationCustomizers(importCustomizer);
    return new GroovyShell(configuration);
  }

}
```

Camel will then use your custom GroovyShell instance (containing your custom static imports), instead of the default one.

### Loading script from external resource

You can externalize the script and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").groovy("resource:classpath:mygroovy.groovy")
```

### Dependencies

To use scripting languages in your camel routes, you need to add a dependency on **camel-groovy**.

If you use Maven you could just add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-groovy</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Examples

In the example below, we use a groovy script as predicate in the message filter, to determine if any line items are over $100:

-   Java
    
-   XML DSL
    

```java
from("queue:foo")
    .filter(groovy("body.lineItems.any { i -> i.value > 100 }"))
        .to("queue:bar")
```

```xml
<route>
    <from uri="queue:foo"/>
    <filter>
        <groovy>body.lineItems.any { i -> i.value > 100 }</groovy>
        <to uri="queue:bar"/>
    </filter>
</route>
```

## Pre compiling shared groovy scripts

**Preview** support level.

In **Camel 4.14** we have added support for loading groovy source files and pre-compile on startup. This allows to have a common set of groovy classes and functions which can be used by Camel and Java.

By default, scripts can be placed in `src/main/resources/camel-groovy` folder, but can be fully configured via ANT path style such as:

```properties
camel.main.groovyScriptPattern = myscript/*.groovy
```

Then in the `src/main/resources/camel-groovy` folder you can have groovy source files that Camel will pre-compile on startup, and make global available via a special `GroovyScriptClassLoader`.

Because this class-loader is required to be in use for being able to load the groovy pre-compiled classes, then this feature will only work via Camel which has control of classloading when used with Camel features that would support this such as in the route DSL and elsewhere.

However, there may be some features in Camel where this may not work (yet).

> **Important**
> This feature is only intended to include smaller groovy sources as small functions, DTOs that makes it easier to use together with Camel for low-code integrations. It is not intended to support Groovy as a general purpose programming language for Camel. For this kind then you can use groovy and Java together and follow best practices for this, such as using the joint-compilation via Maven / Gradle plugins during build.

## Spring Boot Auto-Configuration

When using groovy with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-groovy-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.groovy-json.enabled** | Whether to enable auto configuration of the groovyJson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.groovy-json.pretty-print** | To pretty printing output nicely formatted. Is by default true. | true | Boolean |
| **camel.dataformat.groovy-xml.attribute-mapping** | To turn on or off attribute mapping. When enabled then keys that start with \_ or character will be mapped to an XML attribute, and vise versa. This rule is what Jackson and other XML or JSon libraries uses. | true | Boolean |
| **camel.dataformat.groovy-xml.enabled** | Whether to enable auto configuration of the groovyXml data format. This is enabled by default. |  | Boolean |
| **camel.language.groovy.enabled** | Whether to enable auto configuration of the groovy language. This is enabled by default. |  | Boolean |
| **camel.language.groovy.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |