# Simple

**Since Camel 1.1**

The Simple Expression Language was a really simple language when it was created, but has since grown more powerful. It is primarily intended for being a very small and Camel specific scripting language used anywhere in Camel such as with [EIPs](../../4.18.x/eips/enterprise-integration-patterns.md) and [Route](../../../manual/routes.md).

The simple language is designed with intent to cover almost all the common use cases when little need for scripting in your Camel routes.

However, for much more complex use cases, then a more powerful language is recommended such as: [Groovy](groovy-language.md).

The simple language uses `${body}` placeholders for dynamic expressions and functions.

> **Tip**
> **Alternative syntax**
>
> You can also use the alternative syntax which uses `$simple{ }` as placeholders. This can be used in situations to avoid clashes when using, for example, Spring property placeholder together with Camel.

> **Note**
> See also the [CSimple](csimple-language.md) language which is **pre compiled**.

## A quick Simple Language example

You often use Simple together with [EIPs](../../4.18.x/eips/enterprise-integration-patterns.md) such as [Content-Based Router](../eips/choice-eip.md) EIP.

In the example below we want to route the message depending on whether a message header with key `foo` is equal to different values:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .choice()
        .when(simple("${header.foo} == 'bar'"))
            .to("direct:b")
        .when(simple("${header.foo} == 'cheese'"))
            .to("direct:c")
        .otherwise()
            .to("direct:d");
```

```xml
<route>
    <from uri="direct:a"/>
    <choice>
        <when>
            <simple>${header.foo} == 'bar'</simple>
            <to uri="direct:b"/>
        </when>
        <when>
            <simple>${header.foo} == 'cheese'</simple>
            <to uri="direct:c"/>
        </when>
        <otherwise>
            <to uri="direct:d"/>
        </otherwise>
    </choice>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - choice:
          when:
            - expression:
                simple:
                  expression: "${header.foo} == 'bar'"
              steps:
                - to:
                    uri: direct:b
            - expression:
                simple:
                  expression: "${header.foo} == 'cheese'"
              steps:
                - to:
                    uri: direct:c
          otherwise:
            steps:
              - to:
                  uri: direct:d
```

## Simple Language options

The Simple Language can be configured globally. However, its seldom needed.

The Simple language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **trimResult** (common) | `false` | `Boolean` | Whether to trim the returned values when this language is in use. |
| **pretty** (common) | `false` | `Boolean` | To pretty format the output (only JSon or XML supported). |
| **nested** (advanced) | `false` | `Boolean` | If the result is a nested simple expression should this expression be evaluated as well. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Detailed Reference

For detailed documentation on each topic, see the following sub-pages:

-   [Built-in Functions](simple-functions.md) — All function categories (Core, Array/List, Boolean, Date/Time, Math, String, XML/JSON, and more)
    
-   [Built-in Operators](simple-operators.md) — Comparison, numeric, ternary, elvis, chain, and boolean operators
    
-   [OGNL Expressions](simple-ognl.md) — OGNL dot-notation for invoking methods on POJOs
    
-   [Advanced Features](simple-advanced.md) — Init blocks, EIP examples, custom functions, and JavaScript validator
    

## Dependencies

The Simple language is part of **camel-core**.