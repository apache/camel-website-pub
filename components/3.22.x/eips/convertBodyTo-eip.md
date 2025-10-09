# Convert Body To

The ConvertBodyTo EIP allows you to transform the message body to a different type.

The Convert Body To eip supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** | **Required** The java type to convert to. |  | String |
| **mandatory** | When mandatory then the conversion must return a value (cannot be null), if this is not possible then NoTypeConversionAvailableException is thrown. Setting this to false could mean conversion is not possible and the value is null. | true | Boolean |
| **charset** | To use a specific charset when converting. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

The type is a FQN classname (fully qualified), so for example `java.lang.String`, `com.foo.MyBean` etc. However, Camel has shorthand for common Java types, most noticeable `String` can be used instead of `java.lang.String`. You can also use `byte[]` for a byte array.

## Example

A common use-case is for converting the message body to a `String`:

```java
from("file:inbox")
  .convertBodyTo(String.class)
  .log("The file content: ${body}");
```

And in XML DSL:

```xml
<route>
  <from uri="file:inbox"/>
  <convertBodyTo type="String"/>
  <log message="The file content: ${body}"/>
</route>
```