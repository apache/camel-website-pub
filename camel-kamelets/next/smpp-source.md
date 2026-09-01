# ![smpp source](_images/kamelets/smpp-source.svg) SMPP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive SMS messages and delivery receipts from a SMSC (Short Message Service Center) using the SMPP protocol.

The short message text is emitted as the message body. Details of the received PDU are available in the CamelSmpp\* headers.

## Configuration Options

The following table summarizes the configuration options available for the `smpp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The hostname of the SMSC server to connect to. | string |  | smsc.example.com |
| **addressRange** | Address Range | The address range the consumer binds with, as defined in section 5.2.7 of the SMPP 3.4 specification. The SMSC uses it to route messages to this ESME. | string |  |  |
| **encoding** | Encoding | The encoding scheme of the short message user data. | string | ISO-8859-1 |  |
| **password** | Password | The password for connecting to the SMSC server. | string |  |  |
| **port** | Port | The port of the SMSC server to connect to. | integer | 2775 |  |
| **systemId** | System ID | The system id (username) for connecting to the SMSC server. | string | smppclient |  |
| **systemType** | System Type | The type of ESME (External Short Message Entity) binding to the SMSC (max. 13 characters). | string |  | cp |
| **usingSSL** | Using SSL | Whether to secure the connection to the SMSC server with TLS (the smpps protocol). | boolean | false |  |

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smpp-source.kamelet.yaml)