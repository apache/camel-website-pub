# Convert Body To

The ConvertBodyTo EIP allows you to transform the message body to a different type.

The Convert Body To eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **type** | The java type to convert to. |  | String |
| **mandatory** | Whether the conversion is mandatory. If mandatory and conversion is not possible, a NoTypeConversionAvailableException is thrown. Setting this to false means null may be returned if conversion is not possible. | true | Boolean |
| **charset** | To use a specific charset when converting. |  | String |
> **Note**
> The type is a FQN class name (fully qualified), so for example `java.lang.String`, `com.foo.MyBean` etc. However, Camel has shorthand for common Java types, most noticeable `String` can be used instead of `java.lang.String`. You can also use `byte[]` for a byte array.

## Exchange properties

The Convert Body To eip has no exchange properties.

## Example

A common use-case is for converting the message body to a `String`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .convertBodyTo(String.class)
  .log("The file content: ${body}");
```

```xml
<route>
  <from uri="file:inbox"/>
  <convertBodyTo type="String"/>
  <log message="The file content: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - convertBodyTo:
            type: String
        - log:
            message: "The file content: ${body}"
```