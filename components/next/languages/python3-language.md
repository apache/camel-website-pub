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

## Variables

The following variables are bound by default:

  
| Variable | Type | Description |
| --- | --- | --- |
| body | Object | the message body |
| headers | Map | the message headers |
| properties | Map | the exchange properties |
| exchangeId | String | the exchange id |

By default, Python can index Java maps and lists (for example `headers['foo']`) but cannot invoke methods on host objects.

`message`, `exchange`, and `context` are not bound in default mode. Scripts that refer to them raise a Python `NameError`. Those variables are available only when you opt in to trusted host access, as described in [Trusted host access](#_trusted_host_access).

## Security

The default GraalPy context does **not** use `HostAccess.ALL` or `allowAllAccess(true)`. Host method calls on bound objects are denied unless you opt in.

`SandboxPolicy.CONSTRAINED` was evaluated and is **not** the default: it rejects the Java `Map` host access needed for `headers['foo']` and requires redirecting stdout/stderr on both the engine and the context. Primitive-only scripts can use it in a custom `Python3Language`.

The GraalPy context sets `python.PosixModuleBackend` to `java`, so POSIX operations are backed by Java file and system APIs. File I/O, process creation, and socket operations remain restricted because IO is not enabled (`allowIO` is false). That setting is **not** a hard security sandbox. HostAccess restrictions are the security boundary.

### Trusted host access

To allow Python to call public methods on host objects, and to expose Camel host objects as variables, bind a language created with `createWithHostAccess()` before the first usage.

This is a trusted host-access mode, **not** a sandbox. `HostAccess.ALL` lets Python call public methods and fields on bound Java objects. It does **not** enable `allowAllAccess`, Java class lookup, host IO, or process creation. Use it only when you trust the scripts.

> **Warning**
> Trusted host access lets Python call public methods on bound Camel objects such as `context`, `exchange`, and `message`. That includes destructive operations, for example `context.stop()`, `context.getRegistry().bind(…​)`, and `exchange.getContext().getExecutorService(…​)`. Enable this mode only for fully trusted scripts. Do not use it with Python code taken from untrusted or external input.

In this mode the default variables above remain available, plus:

  
| Variable | Type | Description |
| --- | --- | --- |
| message | Message | the message |
| exchange | Exchange | the Exchange |
| context | CamelContext | the CamelContext |

```java
Python3Language python3 = Python3Language.createWithHostAccess();
camelContext.getRegistry().bind("python3", python3);
```

## Usage

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