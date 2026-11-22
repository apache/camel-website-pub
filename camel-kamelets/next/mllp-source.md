# ![mllp source](_images/kamelets/mllp-source.svg) MLLP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives HL7 v2 messages, such as admissions (ADT) or lab results (ORU), that hospital systems send over MLLP, a plain TCP connection, and acknowledges each one.

Use it to receive the HL7 v2 feed of a hospital information system, a lab system or an interface engine, for example to store the messages, or to turn them into FHIR resources for `fhir-sink`. To send HL7 v2 messages, use `mllp-sink`.

Output: the body is the HL7 message, as text, with its segments separated by a carriage return (`\r`). The text is read in the charset that the MSH-18 field of the message names, such as `UNICODE UTF-8`, or in `charset` when MSH-18 is empty. Headers give the fields of the MSH segment: `CamelMllpMessageType` (MSH-9, such as `ADT^A01`), split into `CamelMllpEventType` (`ADT`) and `CamelMllpTriggerEvent` (`A01`), `CamelMllpMessageControlId` (MSH-10), `CamelMllpSendingApplication` and `CamelMllpSendingFacility` (MSH-3 and MSH-4), `CamelMllpReceivingApplication` and `CamelMllpReceivingFacility` (MSH-5 and MSH-6), `CamelMllpTimestamp` (MSH-7), `CamelMllpProcessingId` (MSH-11), `CamelMllpVersionId` (MSH-12) and `CamelMllpCharset` (MSH-18, such as `UNICODE UTF-8`). A header is not set when its field is empty. `CamelMllpRemoteAddress` is the address and port of the sender.

Good to know: it answers each message with an HL7 acknowledgement (ACK) once the rest of the flow has processed it, and the sender waits for it: `AA` (accepted), or `AE` (error) when a step of the flow fails, with the name of the error in the MSA-3 field. A message without a complete MSH segment still reaches the flow, but gets no acknowledgement. It listens on all the network interfaces of the machine unless `host` says otherwise, with no login and no TLS, so anyone who can reach the port can send messages: protect the port with network rules, and treat the content as untrusted. HL7 messages hold patient data. For TLS, set the application properties `camel.ssl.enabled=true`, `camel.ssl.keyStore`, `camel.ssl.keystorePassword` and `camel.component.mllp.useGlobalSslContextParameters=true`: every MLLP source and sink of the application then uses TLS.

## Configuration Options

The following table summarizes the configuration options available for the `mllp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **port** | Port | **Required** The TCP port to listen on for the connections of the sending systems. 2575 is the port registered for HL7 over MLLP. A port below 1024 needs administrator rights on most systems. | integer |  | 2575 |
| **charset** | Charset | The charset to read the text of a message in when its MSH-18 field is empty, such as `UTF-8`. When it is not set, it is ISO-8859-1. A message whose MSH-18 names a charset, such as `UNICODE UTF-8` or `8859/1`, is read in that charset. | string |  | UTF-8 |
| **host** | Host | The local address to listen on. The default, `0.0.0.0`, accepts connections on all the network interfaces of the machine; `127.0.0.1` accepts only connections from the same machine. | string | 0.0.0.0 | 127.0.0.1 |

## Dependencies

At runtime, the `mllp-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mllp-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mllp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mllp-source.kamelet.yaml)