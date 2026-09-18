# Convert Variable To

The ConvertVariableTo EIP allows you to convert a variable to a different type.

The Convert Variable To eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of variable to convert its value The simple language can be used to define a dynamic evaluated header name to be used. Otherwise a constant name will be used. |  | String |
| **type** | **Required** The java type to convert to. |  | String |
| **toName** | To use another variable to store the result. By default, the result is stored in the same variable. This option allows to use another variable. The simple language can be used to define a dynamic evaluated variable name to be used. Otherwise a constant name will be used. |  | String |
| **mandatory** | When mandatory then the conversion must return a value (cannot be null), if this is not possible then NoTypeConversionAvailableException is thrown. Setting this to false could mean conversion is not possible and the value is null. | true | Boolean |
| **charset** | To use a specific charset when converting. |  | String |
> **Note**
> The type is a FQN class name (fully qualified), so for example `java.lang.String`, `com.foo.MyBean` etc. However, Camel has shorthand for common Java types, most noticeable `String` can be used instead of `java.lang.String`. You can also use `byte[]` for a byte array.

## Exchange properties

The Convert Variable To eip has no exchange properties.

## Example

For example, to convert the foo variable to `String`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertVariableTo("foo", String.class)
  .log("The variable content: ${variable.foo}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertVariableTo name="foo" type="String"/>
  <log message="The variable content: ${variable.foo}"/>
</route>
```

```yaml
- from:
    uri: seda:foo
    steps:
      - convertVariableTo:
          name: foo
          type: String
      - log:
          message: "The variable content: ${variable.foo}"
```

### Convert to another variable

By default, the converted value is replaced in the existing variable. However, you can tell Camel to store the result into another variable, such as shown below where the value is stored in the `bar` variable:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertVariableTo("foo", "bar", String.class)
  .log("The variable content: ${variable.bar}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertVariableTo name="foo" toName="bar" type="String"/>
  <log message="The variable content: ${variable.bar}"/>
</route>
```

```yaml
- from:
    uri: seda:foo
    steps:
      - convertVariableTo:
          name: foo
          toName: bar
          type: String
      - log:
          message: "The variable content: ${variable.bar}"
```

### Dynamic variable name

The ConvertVariableTo supports using [Simple](../../4.22.x/languages/simple-language.md) language for dynamic variable name.

Suppose you have multiple variables:

-   `region`
    
-   `emea`
    
-   `na`
    
-   `pacific`
    

And that region points to either `emea`, `na` or `pacific` which has some order details. Then you can use dynamic variable to convert the header of choice. Now suppose that the region variable has value `emea`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .convertVariableTo("${variable.region}", String.class)
  .log("Order from EMEA: ${variable.emea}");
```

```xml
<route>
  <from uri="seda:foo"/>
  <convertVariableTo name="${variable.region}" type="String"/>
  <log message="Order from EMEA: ${variable.emea}"/>
</route>
```

```yaml
- from:
    uri: seda:foo
    steps:
      - convertVariableTo:
          name: ${variable.region}
          type: String
      - log:
          message: "Order from EMEA: ${variable.emea}"
```