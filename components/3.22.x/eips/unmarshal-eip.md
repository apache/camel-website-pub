# Unmarshal EIP

The [Marshal](marshal-eip.md) and [Unmarshal](#) EIPs are used for [Message Transformation](message-translator.md).

![image](_images/eip/MessageTranslator.gif)

Camel has support for message transformation using several techniques. One such technique is [Data Formats](../dataformats/index.md), where marshal and unmarshal comes from.

So in other words the [Marshal](marshal-eip.md) and [Unmarshal](#) EIPs are used with [Data Formats](../dataformats/index.md).

-   _Marshal_ - Transforms the message body (such as Java object) into a binary or textual format, ready to be wired over the network.
    
-   _Unmarshal_ - Transforms data in some binary or textual format (such as received over the network) into a Java object; or some other representation according to the data format being used.
    

## Example

The following example reads XML files from the inbox/xml directory. Each file is then transformed into Java Objects using [JAXB](../dataformats/jaxb-dataformat.md). Then a [Bean](../bean-component.md) is invoked that takes in the Java object.

Then the reverse operation happens to transform the Java objects back into XML also via JAXB, but using the `marshal` operation. And finally the message is routed to a [JMS](../jms-component.md) queue.

```java
from("file:inbox/xml")
  .unmarshal().jaxb()
  .to("bean:validateOrder")
  .marshal().jaxb()
  .to("jms:queue:order");
```

And in XML:

```xml
<route>
  <from uri="file:inbox/xml"/>
  <unmarshal><jaxb/></unmarshal>
  <to uri="bean:validateOrder"/>
  <marshal><jaxb/></marshal>
  <to uri="jms:queue:order"/>
</route>
```

## Allow Null Body

Sometimes, there are situations where `null` can be a normal value for the body of a message but `null` by default is not an accepted value to unmarshal. To workaround that, it is possible to allow `null` as value to a body to unmarshall using the option `allowNullBody` as shown in the next code snippets:

```java
// Beginning of the route
  .unmarshal().allowNullBody().jaxb()
// End of the route
```

And in XML:

```xml
<!-- Beginning of the route -->
  <unmarshal allowNullBody="true"><jaxb/></unmarshal>
<!-- End of the route -->
```