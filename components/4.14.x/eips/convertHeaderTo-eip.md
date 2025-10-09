# Convert Header To

The ConvertHeaderTo EIP allows you to transform message header to a different type.

The Convert Header To eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of message header to convert its value The simple language can be used to define a dynamic evaluated header name to be used. Otherwise a constant name will be used. |  | String |
| **type** | **Required** The java type to convert to. |  | String |
| **toName** | To use another header to store the result. By default, the result is stored in the same header. This option allows to use another header. The simple language can be used to define a dynamic evaluated header name to be used. Otherwise a constant name will be used. |  | String |
| **mandatory** | When mandatory then the conversion must return a value (cannot be null), if this is not possible then NoTypeConversionAvailableException is thrown. Setting this to false could mean conversion is not possible and the value is null. | true | Boolean |
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
- from:
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
- from:
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

The ConvertHeaderTo supports using [Simple](../../4.18.x/languages/simple-language.md) language for dynamic header name.

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
- from:
    uri: seda:foo
    steps:
      - convertHeaderTo:
          name: ${header.region}
          type: String
      - log:
          message: "Order from EMEA: ${header.emea}"
```