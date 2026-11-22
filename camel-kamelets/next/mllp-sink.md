# ![mllp sink](_images/kamelets/mllp-sink.svg) MLLP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an HL7 v2 message to a hospital system over MLLP, a plain TCP connection, and waits for its HL7 acknowledgement (ACK).

Use it to send admissions, orders or results to a hospital information system, a lab system or an interface engine that receives HL7 v2 over MLLP, or to forward the messages that `mllp-source` receives. To write FHIR resources instead, use `fhir-sink`.

Input: the body is the HL7 message, as text with its segments separated by a carriage return (`\r`), or as bytes, which are sent as they are. Text is sent in `charset`, which is ISO-8859-1 when it is not set: set it to the charset that the MSH-18 field of the messages names, such as `UTF-8` for `UNICODE UTF-8`, because it is not read from the message.

Output: when it is used inside a route, the body is unchanged afterwards. `CamelMllpAcknowledgementType` is the code of the acknowledgement, `AA` when the receiver accepted the message, `CamelMllpAcknowledgementString` the acknowledgement as text, and `CamelMllpAcknowledgement` the same as bytes.

Good to know: an acknowledgement `AE` (error) or `AR` (rejected) fails the message, and `CamelMllpAcknowledgementType` and `CamelMllpAcknowledgementString` are still set, so that a step that handles the error can read the reason in the MSA-3 field. A receiver that cannot be reached, or that does not answer within `ackTimeout`, fails the message. It connects at the first message and keeps the connection open for the next ones. It connects with no TLS. For TLS, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.mllp.useGlobalSslContextParameters=true`: every MLLP source and sink of the application then uses TLS. Headers that start with `CamelMllpAcknowledgement`, and `CamelCharsetName`, are removed from the message first, so they cannot change what the Kamelet sends or reports.

## Configuration Options

The following table summarizes the configuration options available for the `mllp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The host name or IP address of the system to send the messages to. | string |  | hl7.hospital.example.com |
| **port** | Port | **Required** The TCP port that the system listens on for MLLP, often 2575. | integer |  | 2575 |
| **ackTimeout** | Acknowledgement Timeout | How long to wait for the acknowledgement of a message, in milliseconds. When it is not set, it is 15000 (15 seconds). | integer |  | 30000 |
| **charset** | Charset | The charset to send text in, such as `UTF-8`. Set it to the charset that MSH-18 of the messages names; it is not read from the message. It is also used to read the acknowledgement when its MSH-18 is empty. | string | ISO-8859-1 | UTF-8 |
| **connectTimeout** | Connect Timeout | How long to wait for the connection to the system, in milliseconds. When it is not set, it is 30000 (30 seconds). | integer |  | 5000 |

## Dependencies

At runtime, the `mllp-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:mllp
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:mllp-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mllp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mllp-sink.kamelet.yaml)