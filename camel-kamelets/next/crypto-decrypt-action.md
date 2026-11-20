# ![crypto decrypt action](_images/kamelets/crypto-decrypt-action.svg) Crypto Decrypt Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Decrypts the body of each message that `crypto-encrypt-action` encrypted, with the same algorithm and secret key.

Use it to get back the original data that was encrypted with `crypto-encrypt-action`, for example after reading it from storage or receiving it from another system.

Input: the encrypted data exactly as `crypto-encrypt-action` produced it, as bytes or a stream. If it was encoded on the way, for example in Base64, decode it first.

Output: the body is the original data, as bytes (a stream), and the `Content-Type` header is `application/octet-stream`. The other headers are kept.

Good to know: set the `Content-Type` header again to the type of the original data when the next step needs it, for example with `insert-header-action`. Data that was changed, or a different `algorithm`, `mode` or `key` than when encrypting, fails the message with "Message authentication failed". The key is a secret; keep it in a vault or a secret, not in plain configuration.

## Configuration Options

The following table summarizes the configuration options available for the `crypto-decrypt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **algorithm** | Algorithm | **Required** The name of the encryption algorithm the data was encrypted with, such as `AES`, or `DESede` for Triple DES. Give the name alone: a full form such as `AES/CBC/PKCS5Padding` fails each message; the mode is set with `mode`. | string |  | AES |
| **key** | Secret Key | **Required** The secret key the data was encrypted with, as text. Its length must fit the algorithm: for `AES`, 16, 24 or 32 characters (plain ASCII characters count as one byte each), and for `DESede`, 24. | string |  |  |
| **mode** | Mode | The block cipher mode, `CBC`: each message is then encrypted with a new random initialization vector, which is put in front of the encrypted data, so the same text gives different bytes each time. When it is not set, `AES` and `DESede` use ECB mode, in which the same text with the same key always gives the same bytes, so repeats in the data can be seen. Use the same value in `crypto-encrypt-action`. | string |  | CBC |

## Dependencies

At runtime, the `crypto-decrypt-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:crypto
    

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
            uri: "kamelet:crypto-decrypt-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-decrypt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-decrypt-action.kamelet.yaml)