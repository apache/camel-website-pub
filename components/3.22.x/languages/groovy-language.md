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
| **resultType** |  | `String` | Sets the class of the result type (type from output). |
| **trim** | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Examples

In the example below we use a groovy script as predicate in the message filter, to determine if any line items is over $100:

```java
// lets route if a line item is over $100
from("queue:foo")
    .filter(groovy("request.lineItems.any { i -> i.value > 100 }"))
        .to("queue:bar")
```

And in XML DSL:

```xml
<route>
    <from uri="queue:foo"/>
    <filter>
        <groovy>request.lineItems.any { i -> i.value > 100 }</groovy>
        <to uri="queue:bar"/>
    </filter>
</route>
```

## How to get the result from multiple statements script

As the Groovy script engine evaluate method just return a `Null` if it runs a multiple statements script. Camel now look up the value of script result by using the key of "result" from the value set. If you have multiple statements script, you need to make sure you set the value of result variable as the script return value.

```text
bar = "baz";
# some other statements ...
# camel take the result value as the script evaluation result
result = body * 2 + 1
```

## Customizing Groovy Shell

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

## Loading script from external resource

You can externalize the script and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`.  
This is done using the following syntax: `"resource:scheme:location"`, eg to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").groovy("resource:classpath:mygroovy.groovy")
```

## Dependencies

To use scripting languages in your camel routes you need to add a dependency on **camel-groovy**.

If you use Maven you could just add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-groovy</artifactId>
  <version>x.x.x</version>
</dependency>
```

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

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.language.groovy.enabled** | Whether to enable auto configuration of the groovy language. This is enabled by default. |  | Boolean |
| **camel.language.groovy.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |