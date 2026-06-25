# Sort

How can you sort the content of the message?

![image](_images/eip/MessageTranslator.gif)

Use a special filter, a [Message Translator](message-translator.md), between other filters to sort the content of the message.

## Options

The Sort eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The expression to use for sorting. The message body is split into a list, sorted using this expression as the comparator key, and then reassembled. |  | ExpressionDefinition |
| **comparator** | Sets a reference to lookup for the comparator to use for sorting. |  | Comparator |

## Exchange properties

The Sort eip has no exchange properties.

## How sorting works

Sort will by default sort the message body using a default `Comparator` that handles numeric values or uses the `String` representation.

You can also configure a custom `Comparator` to control the sorting.

An [Expression](../../../manual/expression.md) can also be used, which performs the sorting, and returns the sorted message body. The value returned from the `Expression` must be convertible to `java.util.List` as this is required by the JDK sort operation.

### Using Sort EIP

Imagine you consume text files and before processing each file, you want to be sure the content is sorted.

In the route below, it will read the file content and tokenize by line breaks so each line can be sorted.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
    .sort(body().tokenize("\n"))
    .to("bean:MyServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <sort>
    <tokenize token="\n"/>
  </sort>
  <to uri="bean:myServiceBean.processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - sort:
            expression:
              tokenize:
                token: "\n"
        - to:
            uri: bean:myServiceBean.processLine
```

You can control how to sort using a custom `java.util.Comparator`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
    .sort().tokenize("\n").comparator("myComparator")
    .to("bean:MyServiceBean.processLine");
```

```xml
<route>
    <from uri="file:inbox"/>
    <sort comparator="myComparator">
        <tokenize token="\n"/>
    </sort>
    <to uri="bean:MyServiceBean.processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - sort:
            comparator: myComparator
            expression:
              tokenize:
                token: "\n"
        - to:
            uri: bean:MyServiceBean.processLine
```

> **Tip**
> You can also refer to the custom comparator using `#class:` syntax as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
    .sort().tokenize("\n").comparator("#class:com.mycompany.MyReverseComparator")
    .to("bean:MyServiceBean.processLine");
```

In Java DSL you can also provide the custom `Comparator` directly as the object as follows:

```java
from("file:inbox")
    .sort().body().comparator(new MyReverseComparator())
    .to("bean:MyServiceBean.processLine");
```

```xml
<route>
  <from uri="file:inbox"/>
  <sort comparator="#class:com.mycompany.MyReverseComparator">
    <tokenize token="\n"/>
  </sort>
  <bean ref="MyServiceBean" method="processLine"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - sort:
            comparator: "#class:com.mycompany.MyReverseComparator"
            expression:
              tokenize:
                token: "\n"
        - bean:
            ref: MyServiceBean
            method: processLine
```