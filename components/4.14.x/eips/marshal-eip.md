# Marshal

The [Marshal](#) and [Unmarshal](unmarshal-eip.md) EIPs are used for [Message Transformation](message-translator.md).

![image](_images/eip/MessageTranslator.gif)

Camel has support for message transformation using several techniques. One such technique is [Data Formats](../../4.18.x/dataformats/index.md), where marshal and unmarshal come from.

So in other words, the [Marshal](#) and [Unmarshal](unmarshal-eip.md) EIPs are used with [Data Formats](../dataformats/index.md).

-   `marshal`: transforms the message body (such as Java object) into a binary or textual format, ready to be wired over the network.
    
-   `unmarshal`: transforms data in some binary or textual format (such as received over the network) into a Java object; or some other representation according to the data format being used.
    

## Example

The following example reads XML files from the inbox/xml directory. Each file is then transformed into Java Objects using [JAXB](../dataformats/jaxb-dataformat.md). Then a [Bean](../bean-component.md) is invoked that takes in the Java object.

Then the reverse operation happens to transform the Java objects back into XML also via JAXB, but using the `marshal` operation. And finally, the message is routed to a [JMS](../jms-component.md) queue.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox/xml")
  .unmarshal().jaxb()
  .to("bean:validateOrder")
  .marshal().jaxb()
  .to("jms:queue:order");
```

```xml
<route>
  <from uri="file:inbox/xml"/>
  <unmarshal><jaxb/></unmarshal>
  <to uri="bean:validateOrder"/>
  <marshal><jaxb/></marshal>
  <to uri="jms:queue:order"/>
</route>
```

```yaml
- from:
    uri: file:inbox/xml
    steps:
      - unmarshal:
          jaxb: {}
      - to:
          uri: bean:validateOrder
      - marshal:
          jaxb: {}
      - to:
          uri: jms:queue:order
```