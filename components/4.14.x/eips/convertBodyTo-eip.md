# Convert Body To

The ConvertBodyTo EIP allows you to transform the message body to a different type.

The Convert Body To eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **type** | **Required** The java type to convert to. |  | String |
| **mandatory** | When mandatory then the conversion must return a value (cannot be null), if this is not possible then NoTypeConversionAvailableException is thrown. Setting this to false could mean conversion is not possible and the value is null. | true | Boolean |
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
- from:
    uri: file:inbox
    steps:
      - convertBodyTo:
          type: String
      - log:
          message: "The file content: ${body}"
```