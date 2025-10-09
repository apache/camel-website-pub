# Sort

How you can sort the content of the message?

![image](_images/eip/MessageTranslator.gif)

Use a special filter, a [Message Translator](message-translator.md), between other filters to sort the content of the message.

## Options

The Sort eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **expression** | **Required** Optional expression to sort by something else than the message body. |  | ExpressionDefinition |
| **comparator** | Sets the comparator to use for sorting. |  | Comparator |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## How sorting works

Sort will by default sort the message body using a default `Comparator` that handles numeric values or uses the `String` representation.

You can also configure a custom `Comparator` to control the sorting.

An [Expression](../../../manual/expression.md) can also be used, which performs the sorting, and return the sorted message body. The value returned from the `Expression` must be convertible to `java.util.List` as this is required by the JDK sort operation.

### Using Sort EIP

Imagine you consume text files and before processing each file you want to be sure the content is sorted.

In the route below it will read the file content and tokenize by line breaks so each line can be sorted.

```java
from("file:inbox")
    .sort(body().tokenize("\n"))
    .to("bean:MyServiceBean.processLine");
```

You can pass in your own comparator as a 2nd argument:

```java
from("file:inbox")
    .sort(body().tokenize("\n"), new MyReverseComparator())
    .to("bean:MyServiceBean.processLine");
```

In the route below it will read the file content and tokenize by line breaks so each line can be sorted. In XML you use the [Tokenize](../../4.18.x/languages/tokenize-language.md) language as shown:

```xml
<route>
  <from uri="file:inbox"/>
  <sort>
    <tokenize>\n</tokenize>
  </sort>
  <to uri="bean:myServiceBean.processLine"/>
</route>
```

And to use our own `Comparator` we do as follows:

```xml
<route>
  <from uri="file:inbox"/>
  <sort comparator="#class:com.mycompany.MyReverseComparator">
    <simple>${body}</simple>
  </sort>
  <beanRef ref="MyServiceBean" method="processLine"/>
</route>
```

Notice how we use `<simple>${body}</simple>` in the example above to tell Sort EIP that it should use the message body for sorting. This is needed when you use a custom `Comparator`.