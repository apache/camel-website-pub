# ![smpp source](_images/kamelets/smpp-source.svg) SMPP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives each SMS sent to your numbers, and the delivery receipts of the SMS you sent, from an SMS center (SMSC) that speaks the SMPP protocol.

Use it to process SMS replies from customers, such as a STOP or a YES, or to follow whether the SMS sent with `smpp-sink` reached the phone.

Output: the body is the text of the SMS. The `CamelSmppSourceAddr` header is the phone number of the sender, `CamelSmppDestAddr` the number it was sent to, and `CamelSmppMessageType` is `DeliverSm` for an SMS and `DeliveryReceipt` for a delivery receipt, whose body is the text of the receipt and whose fields are in other `CamelSmpp` headers.

Good to know: it logs in to the SMSC as a receiver when the integration starts, and the integration fails to start when the SMSC cannot be reached. The SMSC sends a delivery receipt for each SMS that `smpp-sink` sent with `registeredDelivery` `1` (its default), or `2` when the SMS failed: the `CamelSmppId` header of the receipt is the ID that `smpp-sink` got for the SMS, and `CamelSmppStatus` its final state, such as `DELIVRD`. The SMSC decides which messages it gets, from `systemId` and `addressRange`. It connects with no TLS unless `usingSSL` is true.

## Configuration Options

The following table summarizes the configuration options available for the `smpp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The host name or IP address of the SMSC (the SMS center of your SMS provider or operator). | string |  | smsc.example.com |
| **addressRange** | Address Range | The phone numbers this receiver wants the SMSC to send it messages for, as a regular expression, as defined in section 5.2.7 of the SMPP 3.4 specification. Most SMSCs decide this from `systemId` alone: leave it empty unless your SMS provider asks for it. | string |  | ^4512.\* |
| **encoding** | Encoding | The character set of the text of the SMS, such as `ISO-8859-1` or `UTF-8`. | string | ISO-8859-1 |  |
| **enquireLinkTimer** | Enquire Link Interval | How often to check that the connection to the SMSC is alive with an enquire\_link, in milliseconds. When it is not set, it is 60000, which is one minute. A lower value finds a lost connection sooner. | integer |  | 30000 |
| **password** | Password | The password to log in to the SMSC with. Your SMS provider gives it. | string |  |  |
| **port** | Port | The port of the SMSC. 2775 is the usual SMPP port. | integer | 2775 |  |
| **systemId** | System ID | The user name, called system ID in SMPP, to log in to the SMSC with. Your SMS provider gives it. | string | smppclient |  |
| **systemType** | System Type | A short label of at most 13 characters that some SMSCs ask for when logging in. Leave it empty unless your SMS provider gives one. | string |  | cp |
| **usingSSL** | Use TLS | Whether to secure the connection to the SMSC with TLS (the smpps protocol). The SMSC must support it, usually on another port. | boolean | false |  |

## Dependencies

At runtime, the `smpp-source` Kamelet relies upon the presence of the following dependencies:

-   camel:smpp
    
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
      uri: "kamelet:smpp-source"
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

## SMPP Source Kamelet Description

### Message

The short message text is emitted as the message body. Details of the received PDU stay in the `CamelSmpp*` headers the component sets, such as `CamelSmppMessageType`, `CamelSmppStatus` and `CamelSmppOptionalParameters`.

### Delivery Receipts

The SMSC sends a delivery receipt for each SMS that `smpp-sink` sent with `registeredDelivery` `1`, its default, and for each failed SMS with `registeredDelivery` `2`. A receipt has `CamelSmppMessageType` `DeliveryReceipt`. Its `CamelSmppId` header is the ID that `smpp-sink` got for the SMS in its own `CamelSmppId` header, and `CamelSmppStatus` is the final state of the SMS, such as `DELIVRD` or `UNDELIV`.

### Address Range

`addressRange` is the consumer side option that tells the SMSC which messages to route to this ESME, as defined in section 5.2.7 of the SMPP 3.4 specification.

### Connection

Every `enquireLinkTimer` milliseconds, one minute by default, the Kamelet checks that the connection is alive. A lower value finds a lost connection sooner, and the Kamelet then connects again.

### Example with Delivery Receipts

```yaml
- route:
    from:
      uri: "kamelet:smpp-source"
      parameters:
        host: "smsc.example.com"
        systemId: "myaccount"
        password: "{{smpp.password}}"
        enquireLinkTimer: 30000
      steps:
        - filter:
            simple: "$\{header.CamelSmppMessageType} == 'DeliveryReceipt'"
            steps:
              - log: "SMS $\{header.CamelSmppId} ended as $\{header.CamelSmppStatus}"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-source.kamelet.yaml)