# QuickJS

**Since Camel 4.23**

The QuickJS language evaluates JavaScript as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

`camel-javascript` provides GraalVM JavaScript with Java interoperability, while `camel-quickjs` provides a lightweight pure-Java JavaScript runtime using QuickJS4J and JSON-based data exchange.

QuickJS4J compiles QuickJS to WebAssembly and runs it as Java bytecode through Endive (the successor to Chicory). There is no JNI and no native library. Native-image compatibility and architecture-specific support have not been validated as part of this module.

Do not treat this language as a drop-in replacement for [JavaScript](js-language.md). The scripting APIs and Exchange bindings are different.

For example, you can use QuickJS in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

## QuickJS Options

The QuickJS language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Variables

The following variables are bound for each evaluation. Values are JSON snapshots, not live Java objects. This data-only binding is the intended Preview design: there is no host-object bridge to live `Exchange`, `Message`, or `CamelContext` instances.

  
| Variable | Type | Description |
| --- | --- | --- |
| body | JSON value | the message body after JSON conversion |
| headers | Object | the message headers after JSON conversion |
| properties | Object | the exchange properties after JSON conversion |
| exchangeId | String | the exchange id |

`message`, `exchange`, and `context` are not bound. Scripts that refer to them raise a JavaScript `ReferenceError`.

The following is **not** supported:

```javascript
exchange.getMessage().setHeader('foo', 'bar')
```

Assigning to `headers` or `body` inside a script changes only the JavaScript snapshot. It does not mutate the Camel `Exchange`. Use the expression result (for example `.transform().quickjs(…​)`) when you need to change the message body.

The generic `ScriptingLanguage.evaluate(script, bindings, resultType)` API uses caller-supplied map keys as JavaScript function parameters. Those keys must be valid JavaScript identifiers (for example `body` or `foo_bar`). Names such as `foo-bar`, `123foo`, or reserved words such as `for` are rejected with a Camel evaluation exception rather than a raw JavaScript `SyntaxError`. Route expressions do not use this map.

## Data types

Values cross the Java/JavaScript boundary as JSON:

-   `null`, string, boolean, and number pass through.
    
-   `Map` becomes a JavaScript object. Header and property names are strings, so `headers.MyHeader` and `headers['MyHeader']` both work.
    
-   `List` and arrays become JavaScript arrays.
    
-   `byte[]` becomes a Base64 JSON string. `char[]` becomes a JSON string.
    
-   Other Java types are serialized with Jackson into a JSON object or array snapshot. Java methods such as `getAge()` are not callable from JavaScript; use JSON fields such as `body.age`.
    
-   `Exchange`, `Message`, `CamelContext`, `Class`, and `ClassLoader` values are rejected when they appear as the message body, with an evaluation error. They are never passed into the script.
    
-   Streaming bodies (`InputStream`, `Reader`, and Camel `StreamCache`) are rejected with an evaluation error. The stream is not read, closed, or otherwise consumed.
    
-   Header and property values that cannot be JSON-serialized (including Camel internals and streaming values) are omitted from the JavaScript snapshot so evaluation can still use the remaining data.
    

Serialization failures of the message body raise a Camel evaluation exception that names the unsupported type.

## Expression and predicate

As an expression, the JavaScript value of the script becomes the Camel result (then converted with Camel type converters when a result type is requested).

As a predicate (`.when().quickjs(…​)` or `.filter().quickjs(…​)`), the result is converted to boolean with Camel’s standard `ObjectHelper.evaluateValuePredicate` rules: a `Boolean` is used directly; the strings `true`/`false` are parsed; any other non-empty, non-null value is true.

## Security

JavaScript runs in the QuickJS4J sandbox. The runtime does not expose Java classes, reflection, class loaders, or live Camel objects. WASI has no filesystem or network preopens. Stdout from scripts is discarded so a reused engine does not accumulate output. Per-evaluation stderr is captured into Camel exceptions (for example `ReferenceError`) and then cleared so later evaluations do not include stale error output.

QuickJS4J host plumbing is not available to user scripts: `java_invoke` throws a `TypeError` and `quickjs4j_engine` is undefined, including when accessed through `globalThis`.

This is not the same as GraalVM `HostAccess.ALL`. There is no opt-in to call methods on `Exchange` or `Message`.

## Usage

```java
import static org.apache.camel.language.quickjs.QuickjsLanguage.quickjs;

public class MyRouteBuilder extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
            .choice()
                .when().quickjs("headers.MyHeader == 'foo'").to("mock:foo")
                .otherwise().to("mock:other");
    }
}
```

Transform the body with the expression result:

```java
from("direct:start")
    .transform().quickjs("body.toUpperCase()")
    .to("mock:result");
```

You can load the script from an external resource with the `resource:scheme:location` syntax, for example `resource:classpath:myscript.js` or `resource:file:/path/to/script.js`.

> **Warning**
> Do not derive `resource:classpath:` or `resource:file:` paths from untrusted input such as message headers or query parameters. A path taken from untrusted data can cause Camel to load and evaluate an unexpected JavaScript file.

## Dependencies

To use QuickJS in your Camel routes, you need to add the dependency on **camel-quickjs**.

QuickJS4J is licensed under Apache License 2.0 (ASF Category A).

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-quickjs</artifactId>
  <version>x.x.x</version>
</dependency>
```