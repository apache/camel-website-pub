# Python 3

**Since Camel 4.23**

Camel allows [Python 3](https://www.graalvm.org/python/) (GraalPy) to be used as an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) in Camel routes.

This language is distinct from [Python](python-language.md), which uses Jython and is limited to Python 2.7.

For example, you can use Python 3 in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

## Python 3 Options

The Python 3 language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |

## Variables

The following variables are bound by default:

  
| Variable | Type | Description |
| --- | --- | --- |
| body | Object | the message body |
| header | Map | the message headers (same as `headers`) |
| headers | Map | the message headers |
| exchangeProperty | Map | the exchange properties (same as `exchangeProperties`) |
| exchangeProperties | Map | the exchange properties |
| variable | Map | the exchange variables (same as `variables`) |
| variables | Map | the exchange variables |
| exchangeId | String | the exchange id |

The variables have the same names as in the [Groovy](groovy-language.md) language. In default mode only the data variables above are bound; the Camel host objects are bound only with trusted host access.

By default, Python can index Java maps and lists (for example `headers['foo']` or `variables['foo']`) but cannot invoke methods on host objects.

`variables` holds the exchange-scoped variables (for example set with the [Set Variable](../eips/setVariable-eip.md) EIP). Global and route variables, such as `global:foo`, are not in this map, so in default mode a script cannot read them; with trusted host access they can be read with `exchange.getVariable(…​)`. Like `headers`, it is the exchange’s own map rather than a copy, so an assignment such as `variables['foo'] = 'bar'` updates the exchange. Such an assignment does not go through `Exchange.setVariable`, so `variables['global:foo'] = 1` sets an exchange variable named `global:foo`, not a global one. Setting a variable to `None` fails, because the variables map does not accept null values.

`exchange`, `camelContext`, `message`, `request` and `exception` are not bound in default mode. Scripts that refer to them raise a Python `NameError`. Those variables are available only when you opt in to trusted host access, as described in [Trusted host access](#_trusted_host_access).

## Security

The default GraalPy context does **not** use `HostAccess.ALL` or `allowAllAccess(true)`. Host method calls on bound objects are denied unless you opt in.

`SandboxPolicy.CONSTRAINED` was evaluated and is **not** the default: it rejects the Java `Map` host access needed for `headers['foo']` and requires redirecting stdout/stderr on both the engine and the context. Primitive-only scripts can use it in a custom `Python3Language`.

The GraalPy context sets `python.PosixModuleBackend` to `java`, so POSIX operations are backed by Java file and system APIs. File I/O, process creation, and socket operations remain restricted because IO is not enabled (`allowIO` is false). That setting is **not** a hard security sandbox. HostAccess restrictions are the security boundary.

### Trusted host access

To allow Python to call public methods on host objects, and to expose Camel host objects as variables, bind a language created with `createWithHostAccess()` before the first usage.

This is a trusted host-access mode, **not** a sandbox. `HostAccess.ALL` lets Python call public methods and fields on bound Java objects. It does **not** enable `allowAllAccess`, Java class lookup, host IO, or process creation. Use it only when you trust the scripts.

> **Warning**
> Trusted host access lets Python call public methods on bound Camel objects such as `camelContext`, `exchange`, and `message`. That includes destructive operations, for example `camelContext.stop()`, `camelContext.getRegistry().bind(…​)`, and `exchange.getContext().getExecutorService(…​)`. Enable this mode only for fully trusted scripts. Do not use it with Python code taken from untrusted or external input.

In this mode the default variables above remain available, plus:

  
| Variable | Type | Description |
| --- | --- | --- |
| exchange | Exchange | the Exchange |
| camelContext | CamelContext | the CamelContext |
| message | Message | the message |
| request | Message | the message (same as `message`) |
| exception | Exception | the exception if the exchange failed (or the caught exception in an error handler), otherwise `None` |

```java
Python3Language python3 = Python3Language.createWithHostAccess();
camelContext.getRegistry().bind("python3", python3);
```

## Usage

-   Java
    
-   XML
    
-   YAML
    

```java
import static org.apache.camel.language.python3.Python3Language.python3;

public class MyRouteBuilder extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:start")
            .choice()
                .when().python3("body == 'Hello'").to("mock:hello")
                .otherwise().to("mock:other");
    }
}
```

```xml
<route>
  <from uri="direct:start"/>
  <choice>
    <when>
      <python3>body == 'Hello'</python3>
      <to uri="mock:hello"/>
    </when>
    <otherwise>
      <to uri="mock:other"/>
    </otherwise>
  </choice>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - choice:
            when:
              - expression:
                  python3:
                    expression: 'body == ''Hello'''
                steps:
                  - to:
                      uri: mock:hello
            otherwise:
              steps:
                - to:
                    uri: mock:other
```

Python 3 syntax is supported, including f-strings:

```python
f'Hello {body}'
```

You can load the script from an external resource with the `resource:scheme:location` syntax, for example `resource:classpath:myscript.py` or `resource:file:/path/to/script.py`.

> **Warning**
> Do not derive `resource:classpath:` or `resource:file:` paths from untrusted input such as message headers or query parameters. A path taken from untrusted data can cause Camel to load and evaluate an unexpected Python script.

## Dependencies

To use Python 3 in your Camel routes, you need to add the dependency on **camel-python3**, which implements the Python 3 language with GraalPy.

The GraalPy runtime (language + standard library + Truffle) is large, on the order of 100+ MB of JARs. That is expected for embedding CPython-compatible Python 3 on the JVM.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-python3</artifactId>
  <version>x.x.x</version>
</dependency>
```

GraalPy 25.x embeds CPython 3.12. On JDK 17 it typically runs in interpreter-only mode; on JDK 21+ and on a GraalVM JDK it can use the optimizing runtime. On JDK 24+ you may need `--enable-native-access=ALL-UNNAMED` (the unit tests already set this). GraalPy is skipped on `s390x` and `ppc64le` in the same way as camel-javascript.

GraalPy is licensed under MIT, the Python Software Foundation License, and the Universal Permissive License (UPL), which are ASF Category A licenses.