# Data Format

Camel supports a pluggable `DataFormat` to allow messages to be marshalled to and from binary or text formats to support a kind of [Message Translator](../components/4.22.x/eips/message-translator.md).

![image](_images/images/MessageTranslator.gif)

Camel has support for message transformation using several techniques. One such technique is data formats, where marshal and unmarshal comes from.

So in other words, the [Marshal](../components/4.22.x/eips/marshal-eip.md) and [Unmarshal](../components/4.22.x/eips/unmarshal-eip.md) EIPs are used data formats.

-   _Marshal_ - Transforms the message body (such as Java object) into a binary or textual format, ready to be wired over the network.
    
-   _Unmarshal_ - Transforms data in some binary or textual format (such as received over the network) into a Java object; or some other representation according to the data format being used.
    

## Supported data formats

There are more than 40 different data formats that support formats such as XML, CSV, JSON, YAML, Avro, Protobuf, and many more.

## Example

See [Marshal](../components/4.22.x/eips/marshal-eip.md) for more information and examples.

## Defining a data format once

A data format with options is often used in more than one place, for example to unmarshal a message and later marshal it again. Define it once, with an id, in a top-level `dataFormats` entry, and refer to it by that id with `custom`:

```yaml
- dataFormats:
    - json:
        id: orderJson
        library: Jackson
        prettyPrint: true
- route:
    from:
      uri: timer:tick
      parameters:
        repeatCount: 1
      steps:
        - setBody:
            expression:
              constant:
                expression: '{"orderId": "ORD-1001", "qty": 2}'
        - unmarshal:
            custom:
              ref: orderJson
        - marshal:
            custom:
              ref: orderJson
        - log:
            message: "${body}"
```

Both `unmarshal` and `marshal` use the same JSON data format, so the log shows the order pretty printed.

## See Also

-   [Data Format DSL](dataformat-dsl.md)