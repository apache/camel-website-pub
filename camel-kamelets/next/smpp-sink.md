# ![smpp sink](_images/kamelets/smpp-sink.svg) SMPP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send SMS messages through a SMSC (Short Message Service Center) using the SMPP protocol.

The message body is sent as the short message text.

## Configuration Options

The following table summarizes the configuration options available for the `smpp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The hostname of the SMSC server to connect to. | string |  | smsc.example.com |
| **destAddr** | Destination Address | The destination SME address. For mobile terminated messages this is the directory number of the recipient. | string | 1717 |  |
| **encoding** | Encoding | The encoding scheme of the short message user data. | string | ISO-8859-1 |  |
| **password** | Password | The password for connecting to the SMSC server. | string |  |  |
| **port** | Port | The port of the SMSC server to connect to. | integer | 2775 |  |
| **sourceAddr** | Source Address | The address of the SME (Short Message Entity) which originated the message. | string | 1616 |  |
| **splittingPolicy** | Splitting Policy | The policy for handling long messages. ALLOW splits long messages into 140 byte parts, TRUNCATE cuts them at 140 bytes, REJECT fails the exchange. Enum values: \* ALLOW \* TRUNCATE \* REJECT | string | ALLOW |  |
| **systemId** | System ID | The system id (username) for connecting to the SMSC server. | string | smppclient |  |
| **systemType** | System Type | The type of ESME (External Short Message Entity) binding to the SMSC (max. 13 characters). | string |  | cp |
| **usingSSL** | Using SSL | Whether to secure the connection to the SMSC server with TLS (the smpps protocol). | boolean | false |  |

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-sink.kamelet.yaml)