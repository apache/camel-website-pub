# Validate

The Validate EIP uses an [Expression](../../../manual/expression.md) or a [Predicate](../../../manual/predicate.md) to validate the contents of a message.

![image](_images/eip/MessageSelectorIcon.gif)

This is useful for ensuring that messages are valid before attempting to process them.

When a message is **not** valid then a `PredicateValidationException` is thrown.

## Options

The Validate eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The predicate expression to validate against the current message. If the predicate returns false, a PredicateValidationException is thrown. |  | ExpressionDefinition |
| **predicateExceptionFactory** | Reference to a custom PredicateExceptionFactory for creating the exception when validation fails. |  | PredicateExceptionFactory |

## Exchange properties

The Validate eip has no exchange properties.

## Using Validate EIP

The route below will read the file contents and validate the message body against a regular expression.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .validate(body(String.class).regex("^\\w{10}\\,\\d{2}\\,\\w{24}$"))
  .to("bean:myServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <validate>
    <simple>${body} regex '^\\w{10}\\,\\d{2}\\,\\w{24}$'</simple>
  </validate>
  <to uri="bean:myServiceBean?method=processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - validate:
            expression:
              simple:
                expression: "${body} regex '^\\w{10}\\,\\d{2}\\,\\w{24}$'"
        - to:
            uri: bean:myServiceBean
            parameters:
              method: processLine
```

Validate EIP is not limited to the message body. You can also validate the message header.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .validate(header("bar").isGreaterThan(100))
  .to("bean:myServiceBean.processLine");
```

You can also use `validate` together with the [Simple](../../4.18.x/languages/simple-language.md) language.

```java
from("file:inbox")
  .validate(simple("${header.bar} > 100"))
  .to("bean:myServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <validate>
    <simple>${header.bar} &gt; 100</simple>
  </validate>
  <to uri="bean:myServiceBean" method="processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - validate:
            expression:
              simple:
                expression: "${header.bar} > 100"
        - to:
            uri: bean:myServiceBean.processLine
```