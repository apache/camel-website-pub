# Bindy

JVM since1.0.0 Native since1.0.0

Marshal and unmarshal between POJOs on one side and Comma separated values (CSV), fixed field length or key-value pair (KVP) formats on the other side using Camel Bindy

## What’s inside

-   [Bindy CSV data format](../../../../components/next/dataformats/bindy-dataformat.md)
    
-   [Bindy Fixed Length data format](../../../../components/next/dataformats/bindy-dataformat.md)
    
-   [Bindy Key Value Pair data format](../../../../components/next/dataformats/bindy-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-bindy)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-bindy</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

In native mode, only the locales included in the native image are available. By default, this is only the build machine’s locale.

For instance, the code below:

```java
BindyDataFormat dataFormat = new BindyDataFormat();
dataFormat.setLocale("ar");
```

formats numbers the Arabic way in JVM mode as expected. However, in native mode it falls back to the build machine’s locale unless the `ar` locale is included in the native image.

Additional locales can be included with the `quarkus.locales` configuration property. For example:

```properties
quarkus.locales=ar-MA
```

See the [Locale](../../user-guide/native-mode.html#locale) section of the native mode guide for more details.