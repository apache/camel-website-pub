# Data Format

Camel supports a pluggable `DataFormat` to allow messages to be marshalled to and from binary or text formats to support a kind of [Message Translator](../components/4.18.x/eips/message-translator.md).

![image](_images/images/MessageTranslator.gif)

Camel has support for message transformation using several techniques. One such technique is data formats, where marshal and unmarshal comes from.

So in other words, the [Marshal](../components/4.18.x/eips/marshal-eip.md) and [Unmarshal](../components/4.18.x/eips/unmarshal-eip.md) EIPs are used data formats.

-   _Marshal_ - Transforms the message body (such as Java object) into a binary or textual format, ready to be wired over the network.
    
-   _Unmarshal_ - Transforms data in some binary or textual format (such as received over the network) into a Java object; or some other representation according to the data format being used.
    

## Supported data formats

There are more than 40 different data formats that support formats such as XML, CSV, JSON, YAML, Avro, Protobuf, and many more.

## Example

See [Marshal](../components/4.18.x/eips/marshal-eip.md) for more information and examples.

## See Also

-   [Data Format DSL](dataformat-dsl.md)