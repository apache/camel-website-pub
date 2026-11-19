# ![crypto encrypt action](_images/kamelets/crypto-encrypt-action.svg) Crypto Encrypt Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Encrypts the body of each message with a secret key, such as an AES key, for `crypto-decrypt-action` to decrypt later with the same key.

Use it to protect sensitive data, such as personal or payment details, before it is stored or sent through a system you do not fully trust, and decrypt it later with `crypto-decrypt-action` and the same `algorithm` and `key`.

Input: text or bytes.

Output: the body is the encrypted data, as bytes (a stream), a little longer than the input. It is not text: to send it where only text fits, encode it, for example in Base64. The headers are kept.

Good to know: the key is a secret; anyone who has it can decrypt the data, so keep it in a vault or a secret, not in plain configuration. The encrypted data carries a check value, so `crypto-decrypt-action` fails on data that was changed or decrypted with another key. A key of the wrong length fails each message, not the start. Set `mode` to `CBC`: without it, AES encrypts in ECB mode, where equal parts of the data give equal encrypted bytes. Data encrypted without `mode` is decrypted only without `mode`, so set it on both actions at the same time.

## Configuration Options

The following table summarizes the configuration options available for the `crypto-encrypt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **algorithm** | Algorithm | **Required** The name of the encryption algorithm, such as `AES`, or `DESede` for Triple DES. Give the name alone: a full form such as `AES/CBC/PKCS5Padding` fails each message; choose the mode with `mode`. Use the same value in `crypto-decrypt-action`. | string |  | AES |
| **key** | Secret Key | **Required** The secret key, as text. Its length must fit the algorithm: for `AES`, 16, 24 or 32 characters (plain ASCII characters count as one byte each), and for `DESede`, 24. Use the same key in `crypto-decrypt-action`. | string |  |  |
| **mode** | Mode | The block cipher mode, `CBC`: each message is then encrypted with a new random initialization vector, which is put in front of the encrypted data, so the same text gives different bytes each time. When it is not set, `AES` and `DESede` use ECB mode, in which the same text with the same key always gives the same bytes, so repeats in the data can be seen. Use the same value in `crypto-decrypt-action`. | string |  | CBC |

## Dependencies

At runtime, the `crypto-encrypt-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:crypto-encrypt-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-encrypt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-encrypt-action.kamelet.yaml)