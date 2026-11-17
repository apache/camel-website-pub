# ![smpp sink](_images/kamelets/smpp-sink.svg) SMPP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends each message as an SMS text message to a mobile phone, through an SMS center (SMSC) that speaks the SMPP protocol.

Use it to send alerts, one-time codes or notifications by SMS, through an SMS provider or operator that offers SMPP access. Use `smpp-source` to receive SMS replies and delivery receipts.

Input: the body is the text of the SMS. The phone number to send it to comes from the `CamelSmppDestAddr` header when it is set, and from `destAddr` otherwise. A text longer than one SMS (140 bytes) is split, cut or refused, as `splittingPolicy` says.

Output: the message is unchanged, with the IDs that the SMSC gave the SMS in the `CamelSmppId` header (a List), and how many SMS were sent in `CamelSmppSentMessageCount`.

Good to know: the defaults of `sourceAddr` (1616) and `destAddr` (1717) are test numbers: set them, or set `CamelSmppDestAddr` on each message. It logs in to the SMSC when the integration starts, and the integration fails to start when the SMSC cannot be reached. It connects with no TLS unless `usingSSL` is true.

## Configuration Options

The following table summarizes the configuration options available for the `smpp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The host name or IP address of the SMSC (the SMS center of your SMS provider or operator). | string |  | smsc.example.com |
| **destAddr** | Recipient Address | The phone number to send the SMS to, used when the message has no `CamelSmppDestAddr` header. The default, 1717, is a test value. | string | 1717 | 4598765432 |
| **encoding** | Encoding | The character set of the text of the SMS, such as `ISO-8859-1` or `UTF-8`. | string | ISO-8859-1 |  |
| **password** | Password | The password to log in to the SMSC with. Your SMS provider gives it. | string |  |  |
| **port** | Port | The port of the SMSC. 2775 is the usual SMPP port. | integer | 2775 |  |
| **sourceAddr** | Sender Address | The sender of the SMS, as the recipient sees it: a phone number, a short code or, when the SMSC allows it, a name. The default, 1616, is a test value. | string | 1616 | 4512345678 |
| **splittingPolicy** | Splitting Policy | What to do with a text longer than one SMS (140 bytes): `ALLOW` splits it into several SMS, `TRUNCATE` cuts it at 140 bytes, and `REJECT` fails the message. Enum values: \* ALLOW \* TRUNCATE \* REJECT | string | ALLOW |  |
| **systemId** | System ID | The user name, called system ID in SMPP, to log in to the SMSC with. Your SMS provider gives it. | string | smppclient |  |
| **systemType** | System Type | A short label of at most 13 characters that some SMSCs ask for when logging in. Leave it empty unless your SMS provider gives one. | string |  | cp |
| **usingSSL** | Use TLS | Whether to secure the connection to the SMSC with TLS (the smpps protocol). The SMSC must support it, usually on another port. | boolean | false |  |

## Dependencies

At runtime, the `smpp-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:smpp-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SMPP Sink Kamelet Description

### Message

The message body is sent as the short message text. The recipient is the `CamelSmppDestAddr` header when it is set, and the `destAddr` option otherwise.

### Connection

The Kamelet binds to the SMSC when the integration starts, so an unreachable SMSC makes the integration fail to start, rather than failing each message.

Set `usingSSL` to secure the connection with TLS, where the SMSC supports it.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml)