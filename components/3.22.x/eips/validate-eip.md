# Validate

The Validate EIP uses an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) to validate the contents of a message.

![image](_images/eip/MessageSelectorIcon.gif)

This is useful for ensuring that messages are valid before attempting to process them.

When a message is **not** valid then a `PredicateValidationException` is thrown.

## Options

The Validate eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **expression** | **Required** Expression to use for validation as a predicate. The expression should return either true or false. If returning false the message is invalid and an exception is thrown. |  | ExpressionDefinition |
| **predicateExceptionFactory** | The bean id of custom PredicateExceptionFactory to use for creating the exception when the validation fails. By default, Camel will throw PredicateValidationException. By using a custom factory you can control which exception to throw instead. |  | PredicateExceptionFactory |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

### Using Validate EIP

The route below will read the file contents and validate the message body against a regular expression.

```java
from("file:inbox")
  .validate(body(String.class).regex("^\\w{10}\\,\\d{2}\\,\\w{24}$"))
  .to("bean:myServiceBean.processLine");
```

Validate EIP is not limited to the message body. You can also validate the message header.

```java
from("file:inbox")
  .validate(header("bar").isGreaterThan(100))
  .to("bean:myServiceBean.processLine");
```

You can also use validate together with the [Simple](../../4.18.x/languages/simple-language.md) language.

```java
from("file:inbox")
  .validate(simple("${header.bar} > 100"))
  .to("bean:myServiceBean.processLine");
```

To use validate in the XML DSL, the easiest way is to use [Simple](../../4.18.x/languages/simple-language.md) language:

```xml
<route>
  <from uri="file:inbox"/>
  <validate>
    <simple>${body} regex ^\\w{10}\\,\\d{2}\\,\\w{24}$</simple>
  </validate>
  <to uri="bean:myServiceBean" method="processLine"/>
</route>
```

The XML DSL to validate the message header is as follows

```xml
<route>
  <from uri="file:inbox"/>
  <validate>
    <simple>${header.bar} &gt; 100</simple>
  </validate>
  <to uri="bean:myServiceBean" method="processLine"/>
</route>
```