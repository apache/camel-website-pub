# Wasm

**Since Camel 4.4**

**Only producer is supported**

[WebAssembly (Wasm)](https://webassembly.org) is a portable bytecode format that languages such as Rust, Go, C and C++ compile to. [WASI](https://wasi.dev) is the system interface those programs use for their standard input, output, arguments and environment.

The Wasm component runs a WASI Preview 1 _command module_ (a program with a `_start` function) as a processor: the message body is the standard input of the program, and what the program writes to its standard output becomes the message body. Any program built for WASI Preview 1 can be used as it is, without a Camel specific API. The module runs inside the JVM on [Endive](https://github.com/bytecodealliance/endive), a WebAssembly runtime written in Java, so no native code or external process is involved.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
    <dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-wasm</artifactId>
        <version>${camel-version}</version>
    </dependency>
```

## URI format

wasm:module\[?options\]

The `module` is the location of the `.wasm` file, loaded as a resource: from the classpath by default, or with a prefix such as `classpath:`, `file:` or `http:`. For example `wasm:classpath:upper.wasm` or `wasm:file:/opt/transforms/upper.wasm`.

> **Warning**
> Use a static URI. With a dynamic one, such as `toD("wasm:${header.module}")`, data of the message chooses the program that runs, including a module downloaded from an `http:` location, and the module is loaded and parsed again for every new URI (0.2 to 0.4 seconds for a Go program). To choose between known modules, use a [Choice](eips/choice-eip.md) with one static `wasm` endpoint per module.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Wasm component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Wasm endpoint is configured using URI syntax:

wasm:module

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **module** (producer) | **Required** The WASI Preview 1 command module to run, as a resource: by default from the classpath, or with a prefix such as classpath:, file: or http:. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **args** (producer) | The command line arguments passed to the module, separated by whitespace. Use double quotes around an argument that contains whitespace. The module receives the file name of the module (for example upper.wasm, without scheme, directories or query) as argument zero, followed by these arguments. The arguments are fixed by the route: they cannot be set from message headers. |  | String |
| **compile** (producer) | Whether to compile the module to JVM bytecode, with the runtime compiler of Endive, instead of interpreting it. The module is compiled once per endpoint, when the first producer of the endpoint is initialized (with the route, or at the first message with lazyStartProducer), which takes time for a large module; every exchange then runs the compiled code, which is much faster than the interpreter. Stopping and starting the route does not compile the module again. All other options work the same way. The compiler generates classes at run time, so this option cannot be used in a GraalVM native image. | false | boolean |
| **environment** (producer) | Environment variables for the module, for example environment.LOG\_LEVEL=debug. The module sees no environment variables other than these and the headers listed in environmentHeaders; the environment of the JVM is never passed on. This is a multi-value option with prefix: environment. |  | Map |
| **environmentHeaders** (producer) | A comma separated allow-list of message headers whose values are passed to the module as environment variables of the same name. Headers usually come from whoever sent the message, so no header reaches the module unless it is listed here. A listed header that is not on the message is left unset. Camel matches header names ignoring case, so listing TENANT also passes a header named tenant, as the variable TENANT. A name may not be listed here and also be configured with environment. |  | String |
| **failOnNonZeroExit** (producer) | Whether a module that exits with a non-zero exit code fails the exchange with a WasmExitCodeException. No new body is set then, but a body that is a stream has been read by the module: it can be read again when handling the failure if stream caching is on (the default). When false, the standard output of the module replaces the message body whatever the exit code, which is available in the CamelWasmExitCode header. | true | boolean |
| **maxMemoryPages** (producer) | The maximum size of the memory of the module, in WebAssembly pages of 64 KiB. Rust and Go programs declare no maximum by default. When the limit is reached, growing the memory fails inside the module, which then usually traps or exits with an error. 0 (the default) keeps the maximum declared by the module. The value must not be lower than the initial size the module declares. |  | int |
| **maxOutputSize** (producer) | The maximum number of bytes the module may write to its standard output, and separately to its standard error, which are buffered in memory. A module that writes more is stopped and the exchange fails. 0 (the default) means no limit: a module that keeps writing then fills the heap of the JVM, so set a limit for modules whose output size is not known. |  | int |
| **timeout** (producer) | The maximum time the module may run for one exchange, in milliseconds. When it is exceeded the module is interrupted and the exchange fails with an ExchangeTimedOutException. When a timeout is set, the module runs on a separate thread while the calling thread waits, and the message body is read into memory before the module starts, instead of being streamed to it. The time to read the body does not count. 0 (the default) means no timeout. |  | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Wasm component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWasmExitCode** (producer) Constant: [`EXIT_CODE`](https://javadoc.io/doc/org.apache.camel/camel-wasm/latest/org/apache/camel/wasm/Wasm$Headers.html#EXIT_CODE) | The exit code of the module: 0 when it returned from its \_start function, otherwise the value it passed to proc\_exit. Not set when the module trapped, timed out or exceeded maxOutputSize. |  | Integer |
| **CamelWasmStderr** (producer) Constant: [`STDERR`](https://javadoc.io/doc/org.apache.camel/camel-wasm/latest/org/apache/camel/wasm/Wasm$Headers.html#STDERR) | What the module wrote to its standard error, decoded as UTF-8. Not set when the module wrote nothing or timed out. |  | String |

## Message Body

The message body at each side of the Wasm component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `null`, `text`, `bytes`, `stream` or `file` | The standard input of the module: text, bytes, a stream or a file; no body is an empty input. A Map, a List or a POJO fails: marshal it first. |
| **Producer output** | `bytes` (`byte[]`) | The standard output of the module, with the exit code in the CamelWasmExitCode header. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Writing a module

A module is an ordinary program that reads its standard input and writes its standard output. For example, in [Rust](https://www.rust-lang.org):

```rust
use std::io::{self, Read, Write};

fn main() {
    let mut input = String::new();
    io::stdin().read_to_string(&mut input).unwrap();
    io::stdout().write_all(input.to_uppercase().as_bytes()).unwrap();
}
```

Built with `rustup target add wasm32-wasip1` and `cargo build --release --target wasm32-wasip1`.

The same program in [Go](https://go.dev):

```go
package main

import (
    "bytes"
    "io"
    "os"
)

func main() {
    input, _ := io.ReadAll(os.Stdin)
    os.Stdout.Write(bytes.ToUpper(input))
}
```

Built with `GOOS=wasip1 GOARCH=wasm go build -o upper.wasm`.

### Running a module

For every exchange the component:

1.  creates a new instance of the module (the module is loaded once per endpoint, when its first producer is initialized),
    
2.  runs its `_start` function with the message body as standard input, the arguments configured with `args` and the environment variables configured with `environment` and `environmentHeaders`,
    
3.  sets the `CamelWasmExitCode` header to the exit code of the program: 0 when `_start` returns, otherwise the code the program passed to `proc_exit`,
    
4.  sets the `CamelWasmStderr` header to what the program wrote to its standard error, if anything,
    
5.  and replaces the message body with the standard output of the program, as a `byte[]`.
    

When the program exits with a non-zero code, the exchange fails with a `WasmExitCodeException` (which holds the exit code and the standard error) and the standard output is not set as the body, unless `failOnNonZeroExit` is `false`: then the standard output replaces the body as for any other exit code. The other headers of the message are kept. See [The message body after a failure](#_the_message_body_after_a_failure) for what the body holds when the exchange fails.

Every exchange runs on its own instance, so exchanges never share the memory or the globals of the module and can run in parallel without a lock. A module cannot keep state from one message to the next.

The `CamelWasmExitCode` and `CamelWasmStderr` headers always describe the current run: a value already on the message is removed before the module runs.

### What the module can access

-   **Standard input, output and error**: the message body, the new body and the `CamelWasmStderr` header. They are not terminals.
    
-   **Arguments**: the file name of the module as argument zero (`upper.wasm` for `wasm:file:/opt/modules/upper.wasm`; the directories, the host, user info and query of the location are not passed on), followed by the `args` option, for example `args=--level 2`. Use double quotes around an argument that contains spaces. Arguments are fixed by the route.
    
-   **Environment variables**: only the ones configured with `environment.NAME=value`, and the message headers listed in `environmentHeaders`, passed under the name they are listed with. Header names are matched the way Camel matches them, ignoring case: `environmentHeaders=TENANT` also passes a header named `tenant`, as the variable `TENANT`. A listed header that is not on the message is not set. Headers usually come from whoever sent the message, so no header reaches the module unless it is listed. The environment of the JVM is never passed on.
    
-   **Files and network**: none. The module gets no preopened directories, so it cannot open files, and no sockets.
    
-   **Clock**: the one of the host.
    
-   **Random numbers**: WASI `random_get` (used by Go `crypto/rand` and Rust `getrandom`) returns bytes from a `java.security.SecureRandom` of the host.
    

### Limits

The following options bound what one run of a module can use. They are off by default.

-   `maxMemoryPages`: the maximum size of the memory of the module, in pages of 64 KiB. Rust and Go programs declare no maximum by default, so the memory of one run can grow to gigabytes of JVM heap. When the limit is reached, growing the memory fails inside the module, which then usually traps or exits with an error.
    
-   `timeout`: the maximum time one run may take. The module then runs on a thread of the producer while the route thread waits. When the time is up, the module is interrupted at its next function call or loop iteration and the exchange fails with an `ExchangeTimedOutException`. Without a `timeout`, a module that never ends blocks the route thread.
    
-   `maxOutputSize`: the maximum number of bytes the module may write to its standard output, and separately to its standard error. Both are buffered in memory. A module that writes more is stopped and the exchange fails.
    

> **Warning**
> Without `maxOutputSize` the standard output and the standard error are buffered without a limit: a module that keeps writing fills the heap of the JVM, which affects the whole application and not only one exchange. Set `maxOutputSize` unless the output size of the module is known and small, for example `maxOutputSize=16777216` (16 MiB).

With a `timeout`, the message body is read into memory, on the route thread, before the module starts, and the module reads that copy. Without a `timeout` the body is streamed to the module. The copy is what makes the timeout safe: the thread of a module that timed out can run for a moment longer, and it must not read a stream that the route is using again. It also means that:

-   the whole body is on the heap for the time of the run, in addition to the buffered output,
    
-   the time to read the body is not part of the `timeout`: a body stream that delivers slowly, such as a slow network connection, holds the route thread as it does without a `timeout`,
    
-   the threads of the producer are never blocked on the body, so a module that timed out gives its thread back at its next function call or loop iteration. The pool of these threads has no maximum size and needs none: it holds one thread for each exchange that is in the endpoint at the same time.
    

These limits are robustness controls, not a sandbox. A module is trusted code chosen by the route author, like a processor or a bean, as described in the [security model](../../manual/security-model.md): the limits keep a misbehaving module from turning one message into an unbounded use of memory, time or threads, but they are not a defence against a module written to attack the host.

### Errors

 
| What happens | Result |
| --- | --- |
| The program exits with code 0 | The body is the standard output. `CamelWasmExitCode` is 0. |
| The program exits with another code | A `WasmExitCodeException`, no new body, `CamelWasmExitCode` and `CamelWasmStderr` set. With `failOnNonZeroExit=false`: the body is the standard output. |
| The program traps, for example on a Rust `panic` | A `CamelExchangeException` caused by the `TrapException` of Endive, with the start of the standard error in its message. `CamelWasmStderr` is set, `CamelWasmExitCode` is not. |
| The program writes more than `maxOutputSize` | A `CamelExchangeException`. `CamelWasmStderr` is set when the program wrote to its standard error, `CamelWasmExitCode` is not. |
| The program runs longer than `timeout` | An `ExchangeTimedOutException`. Neither header is set. |
| The module is not a WASI Preview 1 command module, or the options are invalid | The route fails to start. |

In every case, the instance the program ran on is discarded.

### The message body after a failure

When the exchange fails (a non-zero exit code, a trap, the output limit or the timeout), the component does not set a new body, but the program may already have read the old one as its standard input:

 
| Body before the call | Body when the exchange has failed |
| --- | --- |
| A `String`, a `byte[]`, a file, or another value that is converted to a stream | Unchanged. |
| A cached stream (a `StreamCache`): what [stream caching](../../manual/stream-caching.md), which is on by default, makes of a stream body | The same stream cache. The program has read from it; Camel resets it for the error handler and for a redelivery, so it can be read again. |
| A stream that is not cached, and no `timeout` | The same stream, read as far as the program read it, usually to its end. Its content cannot be read again. |
| A stream that is not cached, with a `timeout` | A `byte[]` with the content of the stream: the body was read into memory before the run, and the component puts that copy back. |

So keep stream caching on when an `onException` or a dead letter channel needs the body of a failed exchange and the body is a stream.

### Performance

Creating an instance per exchange is cheap for a small module, but the start-up code of the program itself runs for every message. Programs with a large runtime, such as standard Go programs, spend most of each run initializing that runtime; TinyGo, Rust and C programs start much faster.

By default, a module is interpreted. With `compile=true` the module is translated to JVM bytecode with the [runtime compiler](https://endive.run/docs/execution/runtime-compiler) of Endive, and every exchange runs the compiled code on its own instance. Everything else stays the same: the headers, the errors and the limits, including `timeout` (a compiled module that never ends is interrupted like an interpreted one).

```java
from("direct:in")
    .to("wasm:classpath:upper.wasm?compile=true");
```

Compiled code is much faster than the interpreter, most of all for modules that compute a lot per message. How much depends on the module, the message and the machine, so measure with your own module.

The module is compiled once per endpoint, when the first producer of the endpoint is initialized:

-   for a `to`, that is when the route is started for the first time, or at the first message when the endpoint has `lazyStartProducer=true`. Compiling takes time, which grows with the size of the module;
    
-   stopping and starting the route does not load or compile the module again: the endpoint keeps the compiled module for as long as it exists. The generated classes are only released when the endpoint itself is no longer used, that is when it is removed from the Camel context or the context is stopped, not when the route stops;
    
-   a route reload in development mode (`camel.main.routesReloadEnabled`) by default removes all routes and endpoints, so the module is read and compiled again;
    
-   with a dynamic endpoint (`toD`), every different URI is an endpoint of its own with its own compiled copy of the module, so many different URIs with `compile=true` make the JVM metaspace grow. Prefer a static URI and pass the values that change in headers (`environmentHeaders`) or in the body.
    

Keep the default when:

-   start-up time matters more than throughput: compiling is done before the first message is processed, and compiled code is slower until the JVM has optimized it;
    
-   the application runs as a GraalVM native image: the compiler generates classes while the application runs, which a native image cannot load.
    

A function of the module that is too large for a JVM method (more than 64 KB of bytecode) is not compiled: it is interpreted, the rest of the module is compiled, and the component logs this once per endpoint at `WARN`. A module that the compiler cannot translate at all fails when the first producer of the endpoint is initialized, with an exception that names the module.

The compiler is in the `run.endive:compiler` artifact, which `camel-wasm` depends on. If it was excluded from the classpath, an endpoint with `compile=true` fails as well, with an exception that names the missing artifact.

Endive also has a [build-time compiler](https://endive.run/docs/execution/build-time-compiler), the `run.endive:endive-compiler-maven-plugin` Maven plugin, which translates a module to classes when the application is built, so that nothing is compiled when it runs. The `wasm` endpoint does not use such classes: it loads the module from its location, and interprets it or compiles it as described above.

## Examples

A route that upper-cases the message body with the module `upper.wasm` from the classpath:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .to("wasm:classpath:upper.wasm?timeout=5000&maxMemoryPages=256");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="wasm:classpath:upper.wasm?timeout=5000&amp;maxMemoryPages=256"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: wasm:classpath:upper.wasm
            parameters:
              timeout: 5000
              maxMemoryPages: 256
```

A module with arguments and environment variables, which also receives the `TENANT` header of the message:

-   Java
    
-   YAML
    

```java
from("kafka:orders")
    .to("wasm:file:/opt/transforms/normalize.wasm?args=--strict&environment.LOG_LEVEL=info&environmentHeaders=TENANT")
    .to("kafka:normalized-orders");
```

```yaml
- route:
    from:
      uri: kafka:orders
      steps:
        - to:
            uri: wasm:file:/opt/transforms/normalize.wasm
            parameters:
              args: --strict
              environment.LOG_LEVEL: info
              environmentHeaders: TENANT
        - to:
            uri: kafka:normalized-orders
```