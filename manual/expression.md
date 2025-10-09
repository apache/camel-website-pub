# Expressions

Expressions and [Predicates](predicate.md) can then be used to create the various [Enterprise Integration Patterns](../components/4.18.x/eips/enterprise-integration-patterns.md) in the [DSL](dsl.md) like with the [Content Based Router](../components/4.18.x/eips/choice-eip.md) EIP, or [Recipient List](../components/4.18.x/eips/recipientList-eip.md) EIP.

To support dynamic rules Camel supports pluggable [Expression](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Expression.md) strategies using a variety of different [Languages](../components/4.18.x/languages/index.md).

> **Note**
> The [Simple](../components/4.18.x/languages/simple-language.md) is often used as predicates and expressions with the Camel EIPs.

If you are outside the DSL and want to create your own expressions you can either implement the [Expression interface](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Expression.md), reuse one of the other builders or try the [ExpressionBuilder class](https://www.javadoc.io/doc/org.apache.camel/camel-support/current/org/apache/camel/support/builder/ExpressionBuilder.md).

## Expression API

The API for a Camel Expression is defined in the `org.apache.camel.Expression` interface as shown:

```java
public interface Expression {

    /**
     * Returns the value of the expression on the given exchange
     *
     * @param exchange the message exchange on which to evaluate the expression
     * @param type the expected type of the evaluation result
     * @return the value of the expression
     */
    <T> T evaluate(Exchange exchange, Class<T> type);
}
```

A `Expression` is being evaluated to an Object value. This makes expressions so powerful as this can be used for functions, data mapping, templating, and for low-code users.