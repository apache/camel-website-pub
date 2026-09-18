# Contributor guide

## Prerequisites

-   `git`
    
-   GraalVM with `native-image` command installed and `GRAALVM_HOME` environment variable set, see [Building a native executable](https://quarkus.io/guides/building-native-image-guide) section of the Quarkus documentation.
    
-   If you are on Linux, `docker` or `podman` is sufficient for the native mode too. Use `-Pnative,docker` instead of `-Pnative` if you choose this option.
    
-   Java 17 or higher (Java 11 is only for Camel Quarkus < 3.0.0).
    
-   Maven 3.8.2+ (unless you use the Maven Wrapper, a.k.a. `mvnw` available in the source tree).
    

## How to build

Checkout the code

```shell
git clone https://github.com/apache/camel-quarkus.git
cd camel-quarkus
```

A fast build without tests and various checks:

```shell
mvn clean install -Dquickly
```

A build with integration tests in the JVM mode only:

```shell
mvn clean install
```

A build with integration tests in both the JVM mode and the native mode:

```shell
mvn clean install -Pnative
```

> **Tip**
> You may want to install and use [`mvnd` - the Maven Daemon](https://github.com/mvndaemon/mvnd) for faster builds. When using `mvnd` on macOS, make sure the mvnd version matches your installed Maven version (`mvn`) to avoid compilation failures due to missing dependencies.

> **Tip**
> For building native images on macOS, you usually **do not need** to use `-Dquarkus.native.container-build`. This option is primarily intended for Linux systems, where the native image build runs inside a Docker container. On macOS, GraalVM can typically generate the native image directly, so omitting this option simplifies the build and avoids unnecessary errors.

> **Tip**
> Extensions that depend on Java AWT are not yet supported for native image generation on macOS. If an integration test fails when running `mvnd clean install -Dnative` due to missing AWT support, this is expected and not necessarily a problem with your environment. Running the same test in JVM mode (`mvn clean install`) should work correctly.

> **Tip**
> To run a specific integration test, you can use the `-Dtest` property. For example: `mvn clean test -Dtest=MyTest`. To run tests in a specific module, use the `-pl` (project list) flag: `mvn clean test -pl integration-tests/my-module`.

## What’s next?

-   [Create new extension](create-new-extension.md).
    
-   [Promote a JVM extension to Native](promote-jvm-to-native.md).