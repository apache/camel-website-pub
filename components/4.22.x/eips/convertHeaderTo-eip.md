# Convert Header To

The ConvertHeaderTo EIP allows you to transform message header to a different type.

The Convert Header To eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of message header to convert its value. The simple language can be used to define a dynamic evaluated header name. |  | String |
| **type** | **Required** The java type to convert to. |  | String |
| **toName** | To use another header to store the result. By default, the result is stored in the same header. |  | String |
| **mandatory** | Whether the conversion is mandatory. If mandatory and conversion is not possible, a NoTypeConversionAvailableException is thrown. Setting this to false means null may be returned if conversion is not possible. | true | Boolean |
| **charset** | To use a specific charset when converting. |  | String |
> **Note**
> The type is a FQN class name (fully qualified), so for example `java.lang.String`, `com.foo.MyBean` etc. However, Camel has shorthand for common Java types, most noticeable `String` can be used instead of `java.lang.String`. You can also use `byte[]` for a byte array.

## Exchange properties

The Convert Header To eip has no exchange properties.

## Example

For example, to convert the foo header to `String`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertHeaderTo("foo", String.class)
  .log("The header content: ${header.foo}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertHeaderTo name="foo" type="String"/>
  <log message="The header content: ${header.foo}"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:foo
      steps:
        - convertHeaderTo:
            name: foo
            type: String
        - log:
            message: "The header content: ${header.foo}"
```

### Convert to another header

By default, the converted value is replaced in the existing header. However, you can tell Camel to store the result into another header, such as shown below where the value is stored in the `bar` header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertHeaderTo("foo", "bar", String.class)
  .log("The header content: ${header.bar}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertHeaderTo name="foo" toName="bar" type="String"/>
  <log message="The header content: ${header.bar}"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:foo
      steps:
        - convertHeaderTo:
            name: foo
            toName: bar
            type: String
        - log:
            message: "The header content: ${header.bar}"
```

### Dynamic header name

The ConvertHeaderTo supports using [Simple](../languages/simple-language.md) language for dynamic header name.

Suppose you have multiple headers:

-   `region`
    
-   `emea`
    
-   `na`
    
-   `pacific`
    

And that region points to either `emea`, `na` or `pacific`, which has some order details. Then you can use dynamic header to convert the header of choice. Now suppose that the region header has value `emea`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertHeaderTo("${header.region}", String.class)
  .log("Order from EMEA: ${header.emea}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertHeaderTo name="${header.region}" type="String"/>
  <log message="Order from EMEA: ${header.emea}"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:foo
      steps:
        - convertHeaderTo:
            name: ${header.region}
            type: String
        - log:
            message: "Order from EMEA: ${header.emea}"
```