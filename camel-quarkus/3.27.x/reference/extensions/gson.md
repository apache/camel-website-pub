# Gson

JVM since1.0.0 Native since1.0.0

Marshal POJOs to JSON and back using Gson

## What’s inside

-   [JSON Gson data format](../../../../components/4.14.x/dataformats/gson-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-gson)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-gson</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Marshaling / Unmarshalling objects in native mode

When marshaling / unmarshalling objects in native mode, their target types must be [registered for reflection](https://quarkus.io/guides/writing-native-applications-tips#registering-for-reflection).

For example when using any of the following:

-   `GsonDataFormat.setUnmarshalType(MyPojo.class)`
    
-   `GsonDataFormat.setUnmarshalTypeName("org.acme.MyPojo")`
    
-   `GsonDataFormat.setUnmarshalGenericType(MyPojo.class)`
    

`MyPojo.class` can be registered for reflection as follows.

```java
package org.acme.MyPojo;

@RegisterForReflection
public class MyPojo {
}
```