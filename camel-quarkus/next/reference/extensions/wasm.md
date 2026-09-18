# Wasm

JVM since3.10.0 Native since3.10.0 🧪Experimental

Invoke Wasm functions.

## What’s inside

-   [Wasm component](../../../../components/4.22.x/wasm-component.md), URI syntax: `wasm:functionName`
    
-   [Wasm language](../../../../components/4.22.x/languages/wasm-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-wasm)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-wasm</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

## Reading Wasm modules from the classpath in native mode

When Wasm modules are read from the classpath (the default) in native mode, you must ensure that the module(s) are added to the native image. You can do this via a configuration property in `application.properties`.

For example, assuming `.wasm` files are read from a classpath location of `was/modules`.

```properties
quarkus.native.resources.includes = wasm/modules/*.wasm
```

More information about selecting resources for inclusion in the native executable can be found in the [native mode user guide](../../user-guide/native-mode.html#embedding-resource-in-native-executable).