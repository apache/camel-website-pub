# Management

JVM since1.1.0 Native since3.2.0

Camel Management

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-management)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-management</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

For information on using Managed Beans in Camel, consult the [JMX section of the Camel Manual](../../../../manual/jmx.md).

### Enabling and Disabling JMX

JMX can be enabled or disabled in Camel Quarkus by any of the following methods:

1.  Adding or removing the `camel-quarkus-management` extension.
    
2.  Setting the `camel.main.jmxEnabled` configuration property to a boolean value.
    
3.  Setting the system property `-Dorg.apache.camel.jmx.disabled` to a boolean value.
    

### Native mode

If you want the native application to be discoverable by tools such as JConsole and VisualVM, add the following configuration to `application.properties`.

```properties
quarkus.native.monitoring=jvmstat
```

For more information, refer to the [Quarkus native guide](https://quarkus.io/guides/building-native-image#using-monitoring-options).

## Camel Quarkus limitations

### Native mode

JMX in GraalVM is still **experimental**. Therefore, some features are not available in native mode.

-   Operations for MBean `java.lang:type=Threading` are not fully implemented. Therefore, it is not possible to obtain details about application threads.
    
-   Various MBean attributes do not have their values implemented. For example, the `ClassCount` attribute values for MBean `java.lang:type=ClassLoading` are fixed at `0`