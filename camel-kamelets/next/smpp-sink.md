# ![smpp sink](_images/kamelets/smpp-sink.svg) SMPP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends each message as an SMS text message to a mobile phone, through an SMS center (SMSC) that speaks the SMPP protocol.

Use it to send alerts, one-time codes or notifications by SMS, through an SMS provider or operator that offers SMPP access. Use `smpp-source` to receive SMS replies and delivery receipts.

Input: the body is the text of the SMS. The phone number to send it to comes from the `CamelSmppDestAddr` header when it is set, and from `destAddr` otherwise. A text longer than one SMS (160 characters, or 70 with `alphabet` `8`) is split, cut or refused, as `splittingPolicy` says.

Output: the message is unchanged, with the IDs that the SMSC gave the SMS in the `CamelSmppId` header (a List), and how many SMS were sent in `CamelSmppSentMessageCount`.

Good to know: the defaults of `sourceAddr` (1616) and `destAddr` (1717) are test numbers: set them, or set `CamelSmppDestAddr` on each message. It asks the SMSC for a delivery receipt of each SMS, which `smpp-source` receives: set `registeredDelivery` to `0` to not ask for them. The text is encoded with `encoding`, so characters it cannot hold, such as Cyrillic or emoji in ISO-8859-1, are sent as `?`: for text in any language, set `alphabet` and `dataCoding` to `8`. It logs in to the SMSC when the integration starts, and the integration fails to start when the SMSC cannot be reached. It connects with no TLS unless `usingSSL` is true. Headers that start with `CamelSmpp`, except `CamelSmppDestAddr`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `smpp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The host name or IP address of the SMSC (the SMS center of your SMS provider or operator). | string |  | smsc.example.com |
| **alphabet** | Alphabet | How to turn the body into the bytes of the SMS: `0` encodes the text with `encoding`, `4` sends a body of bytes as it is (8-bit binary data) and encodes text with `encoding`, and `8` encodes the text as UCS-2 (UTF-16), which can hold text in any language. When it is not set, it is `0`, and characters that `encoding` cannot hold, such as Cyrillic in ISO-8859-1, are sent as `?`. It does not change the data coding the SMS is marked with: set `dataCoding` to the same value. Enum values: \* 0 \* 4 \* 8 | integer |  | 8 |
| **dataCoding** | Data Coding | The data coding the SMS is marked with, from 0 to 127, which tells the phone how to read its bytes, as in section 5.2.19 of the SMPP 3.4 specification: `0` the default alphabet of the SMSC, `3` Latin-1, `4` 8-bit binary, `8` UCS-2 (Unicode). When it is not set, it is `0`. It does not change how the text is encoded into bytes, which `alphabet` and `encoding` do: for text in any language, such as Cyrillic or emoji, set both `alphabet` and `dataCoding` to `8`. | integer |  | 8 |
| **destAddr** | Recipient Address | The phone number to send the SMS to, used when the message has no `CamelSmppDestAddr` header. The default, 1717, is a test value. | string | 1717 | 4598765432 |
| **destAddrNpi** | Recipient Numbering Plan | The numbering plan indicator (NPI) of the recipient address: `0` unknown, `1` ISDN (E.164, the plan of phone numbers), `3` data (X.121), `4` telex, `6` land mobile (E.212), `8` national, `9` private, `10` ERMES, `14` internet (IP), `18` WAP client ID. When it is not set, it is `0`. Enum values: \* 0 \* 1 \* 3 \* 4 \* 6 \* 8 \* 9 \* 10 \* 14 \* 18 | integer |  | 1 |
| **destAddrTon** | Recipient Type Of Number | The type of number (TON) of the recipient address, from `destAddr` or `CamelSmppDestAddr`: `0` unknown, `1` international, `2` national, `3` network specific, `4` subscriber number, `5` alphanumeric, `6` abbreviated. When it is not set, it is `0`. Use `1`, with `1` in `destAddrNpi`, for a phone number with its country code, such as `4598765432`. Enum values: \* 0 \* 1 \* 2 \* 3 \* 4 \* 5 \* 6 | integer |  | 1 |
| **encoding** | Encoding | The character set of the text of the SMS, such as `ISO-8859-1` or `UTF-8`. | string | ISO-8859-1 |  |
| **enquireLinkTimer** | Enquire Link Interval | How often to check that the connection to the SMSC is alive with an enquire\_link, in milliseconds. When it is not set, it is 60000, which is one minute. A lower value finds a lost connection sooner. | integer |  | 30000 |
| **password** | Password | The password to log in to the SMSC with. Your SMS provider gives it. | string |  |  |
| **port** | Port | The port of the SMSC. 2775 is the usual SMPP port. | integer | 2775 |  |
| **registeredDelivery** | Delivery Receipt | Which delivery receipts to ask the SMSC for: `1` for a receipt whether the SMS reached the phone or not, `2` only when it failed, and `0` for none. When it is not set, it is `1`. The SMSC sends the receipts to a receiver logged in to it, such as `smpp-source`: this Kamelet does not get them. Enum values: \* 0 \* 1 \* 2 | integer |  | 0 |
| **sourceAddr** | Sender Address | The sender of the SMS, as the recipient sees it: a phone number, a short code or, when the SMSC allows it, a name. The default, 1616, is a test value. | string | 1616 | 4512345678 |
| **sourceAddrNpi** | Sender Numbering Plan | The numbering plan indicator (NPI) of `sourceAddr`: `0` unknown, `1` ISDN (E.164, the plan of phone numbers), `3` data (X.121), `4` telex, `6` land mobile (E.212), `8` national, `9` private, `10` ERMES, `14` internet (IP), `18` WAP client ID. When it is not set, it is `0`. Enum values: \* 0 \* 1 \* 3 \* 4 \* 6 \* 8 \* 9 \* 10 \* 14 \* 18 | integer |  | 1 |
| **sourceAddrTon** | Sender Type Of Number | The type of number (TON) of `sourceAddr`: `0` unknown, `1` international, `2` national, `3` network specific, `4` subscriber number, `5` alphanumeric (a name instead of a number), `6` abbreviated. When it is not set, it is `0`. Use `5` to send from a name, such as `MyShop`, and `1`, with `1` in `sourceAddrNpi`, for a number with its country code. Enum values: \* 0 \* 1 \* 2 \* 3 \* 4 \* 5 \* 6 | integer |  | 5 |
| **splittingPolicy** | Splitting Policy | What to do with a text longer than one SMS (160 characters, or 70 with `alphabet` `8`): `ALLOW` splits it into several SMS, `TRUNCATE` cuts it to fit in one SMS, and `REJECT` fails the message. Enum values: \* ALLOW \* TRUNCATE \* REJECT | string | ALLOW |  |
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

### Delivery Receipts

The Kamelet asks the SMSC for a delivery receipt of each SMS. The SMSC sends the receipts to a receiver logged in to it, such as `smpp-source`, not to this Kamelet. `registeredDelivery` says which receipts to ask for:

 
| `registeredDelivery` | Receipts |
| --- | --- |
| not set, or `1` | A receipt whether the SMS reached the phone or not |
| `2` | A receipt only when the SMS failed |
| `0` | No receipt |

### Sender and Recipient Numbers

The type of number (TON) and the numbering plan (NPI) tell the SMSC how to read `sourceAddr` and the recipient address. When they are not set, both are `0` (unknown), and the SMSC guesses. Common settings:

   
| Address | TON | NPI | Example |
| --- | --- | --- | --- |
| A phone number with its country code | `1` | `1` | `4598765432` |
| A name as the sender | `5` | `0` | `MyShop` |

Set them with `sourceAddrTon` and `sourceAddrNpi` for the sender, and `destAddrTon` and `destAddrNpi` for the recipient. Ask your SMS provider which values it expects.

### Text in Any Language

The text is encoded with `encoding`, ISO-8859-1 by default, so characters it cannot hold, such as Cyrillic, Greek or emoji, are sent as `?`. To send text in any language, set both `alphabet` and `dataCoding` to `8` (UCS-2): `alphabet` encodes the text as UCS-2, and `dataCoding` marks the SMS as UCS-2 so that the phone can read it. One SMS then holds 70 characters instead of 160.

To send binary data, such as a body of bytes, set both `alphabet` and `dataCoding` to `4`: the bytes are sent as they are.

### Connection

The Kamelet binds to the SMSC when the integration starts, so an unreachable SMSC makes the integration fail to start, rather than failing each message.

Every `enquireLinkTimer` milliseconds, one minute by default, the Kamelet checks that the connection is alive. A lower value finds a lost connection sooner.

Set `usingSSL` to secure the connection with TLS, where the SMSC supports it.

### Example with Delivery Receipts and Unicode Text

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Ihr Paket ist unterwegs. Ваша посылка в пути."
        period: 3600000
      steps:
        - to:
            uri: "kamelet:smpp-sink"
            parameters:
              host: "smsc.example.com"
              systemId: "myaccount"
              password: "{{smpp.password}}"
              sourceAddr: "MyShop"
              sourceAddrTon: 5
              sourceAddrNpi: 0
              destAddr: "4598765432"
              destAddrTon: 1
              destAddrNpi: 1
              registeredDelivery: 1
              alphabet: 8
              dataCoding: 8
              enquireLinkTimer: 30000
```

The delivery receipts of these SMS arrive at an `smpp-source` logged in to the same SMSC.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml)