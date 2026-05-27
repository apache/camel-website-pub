# Validator

Validator performs declarative validation of the message according to the declared _Input Type_ and/or _Output Type_ on a route definition which declares the expected message type.

## Data type format

```text
scheme:name
```

where **scheme** is the type of data model like `java`, `xml` or `json`, and **name** is the individual data type name.

## Supported Validators

 
| Validator | Description |
| --- | --- |
| Predicate Validator | Validate with using Expression or Predicate |
| Endpoint Validator | Validate by forwarding to the Endpoint to be used with validation component such as Validation Component or Bean Validation Component. |
| Custom Validator | Validate with using custom validator class. Validator must be a subclass of `org.apache.camel.spi.Validator` |

## Common Options

All validators have following common options to specify which data type is supported by the validator. `type` must be specified.

 
| Name | Description |
| --- | --- |
| type | Data type to validate |

## Predicate Validator Options

 
| Name | Description |
| --- | --- |
| expression | Expression or Predicate to be used for validation |

Here is an example to specify a validation predicate:

-   Java
    
-   XML
    
-   YAML
    

```java
validator()
    .type("csv:CSVOrder")
    .withExpression(simple("${body} contains '{name:XOrder}'"));
```

```xml
<validators>
    <predicateValidator type="csv:CSVOrder">
        <simple>${body} contains '{name:XOrder}'</simple>
    </predicateValidator>
</validators>
```

```yaml
- validators:
    predicateValidator:
      type: csv:CSVOrder
      expression:
        simple:
          expression: "${body} contains '{name:XOrder}'"
```

## Endpoint Validator Options

 
| Name | Description |
| --- | --- |
| ref | Reference to the Endpoint ID |
| uri | Endpoint URI |

Here is an example to specify endpoint URI in Java DSL:

-   Java
    
-   XML
    
-   YAML
    

```java
validator()
    .type("xml")
    .withUri("validator:xsd/schema.xsd");
```

```xml
<validators>
    <endpointValidator uri="validator:xsd/schema.xsd" type="xml"/>
</validators>
```

```yaml
- validators:
    endpointValidator:
      type: xml
      uri: validator:xsd/schema.xsd
```

Note that the Endpoint Validator just forwards the message to the specified endpoint. In above example, camel forwards the message to the `validator:` endpoint, which actually is a [Validation Component](../components/4.18.x/validator-component.md). You can also use any other validation component like Bean Validation Component.

## Custom Validator Options

The validator must be an implementation of `org.apache.camel.spi.Validator`

 
| Name | Description |
| --- | --- |
| ref | Reference to the custom Validator bean ID |
| className | Fully qualified class name of the custom Validator class |

Here is an example to specify custom Validator class:

-   Java
    
-   XML
    
-   YAML
    

```java
validator()
    .type("json")
    .withJava(com.example.MyCustomValidator.class);
```

```xml
<validators>
    <customValidator className="com.example.MyCustomValidator" type="json"/>
</validators>
```

```yaml
- validators:
    customValidator:
      type: json
      className: com.example.MyCustomValidator
```

## Examples

For example to declare the Endpoint Validator which uses validator component to validate `xml:ABCOrder`, we can do as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
validator()
    .type("xml:ABCOrder")
    .withUri("validator:xsd/schema.xsd");
```

```xml
<validators>
    <endpointValidator uri="validator:xsd/schema.xsd" type="xml:ABCOrder"/>
</validators>
```

```yaml
- validators:
    endpointValidator:
      type: xml:ABCOrder
      uri: "validator:xsd/schema.xsd"
```

If you have the following route definition, above validator will be applied when `direct:abc` endpoint receives the message. Note that `inputTypeWithValidate` is used instead of `inputType` in Java DSL, and the `validate` attribute on the inputType declaration is set to `true` in XML DSL:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:abc")
    .inputTypeWithValidate("xml:ABCOrder")
    .log("${body}");
```

```xml
<route>
    <from uri="direct:abc"/>
    <inputType urn="xml:ABCOrder" validate="true"/>
    <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:abc
      steps:
        - inputType:
            urn: xml:ABCOrder
            validate: "true"
        - log:
            message: "${body}"
```

## See Also

The [Transformer](transformer.md) is a related functionality.