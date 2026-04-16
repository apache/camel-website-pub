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

When using camel-quarkus-bindy in native mode, only the build machine’s locale is supported.

For instance, on build machines with French locale, the code below:

```java
BindyDataFormat dataFormat = new BindyDataFormat();
dataFormat.setLocale("ar");
```

formats numbers the arabic way in JVM mode as expected. However, it formats numbers the French way in native mode.

Without further tuning, the build machine’s default locale would be used. Another locale can be specified with the `quarkus.default-locale` configuration property.

For example, to make the above example work, the default locale could be set as follows.

```properties
quarkus.default-locale=ar-MA
```