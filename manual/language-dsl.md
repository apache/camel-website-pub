# Language DSL

The Language DSL is a builder API that allows using type safe construction of Camel [Languages](languages.md).

The Language DSL is exclusively available as part of the Java DSL.

The DSL can be accessed directly from the `RouteBuilder` with the `expression()` method.

## Using Language DSL

In the following example, a `TokenizerExpression` is created using the legacy approach where the expression is instantiated explicitly and configured using setters:

_Java-only: creating a tokenizer expression using the legacy approach_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        TokenizerExpression expression = new TokenizerExpression("(\\W+)\\s*"); (1)
        expression.setRegex(true); (2)
        from("file:data")
            .split(expression) (3)
            .process("processEntry");
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Instantiate the expected expression</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Configure the expression according to the needs</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Affect the expression with the expected configuration</td></tr></tbody></table>

The previous code could be simplified using the utility methods available directly from the `ExpressionClause` corresponding to the type returned by several existing methods such as `split()`, `setBody()`, `setHeader(String)`, `aggregate()`, etc.:

_Java-only: simplified tokenizer using ExpressionClause utility method_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("file:data")
            .split()
            .tokenize("(\\W+)\\s*", true) (1)
            .process("processEntry");
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Select the <code>tokenize</code> language with a specific regular expression</td></tr></tbody></table>

This approach is suitable for very basic configuration, but as there are only limited utility methods for each supported language, for more complex configuration, we can quickly face situations where the utility method for our expected configuration doesn’t exist. In this situation, you can either use the legacy approach or the language DSL like in the next code snippet:

_Java-only: configuring a tokenizer using the Language DSL builder_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("file:data")
            .split(
                expression() (1)
                    .tokenize() (2)
                        .token("(\\W+)\\s*") (3)
                        .regex(true) (3)
                    .end()) (4)
                .process("processEntry");
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Give access to all the supported languages</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Select the <code>tokenize</code> language</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Configure the expression according to the needs</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>Build the expression with the expected configuration</td></tr></tbody></table>

Sometimes creating an expression can be a bit verbose with a number of fluent builder methods. What you can do is to pre create the expression before the route as shown below:

_Java-only: pre-creating an expression before the route_

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        var token = expression().tokenize().token("(\\W+)\\s*").regex(true).end(); (1)

        from("file:data")
            .split(token) (2)
                .process("processEntry");
    }
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Pre create the expression</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Use the expression in the route</td></tr></tbody></table>