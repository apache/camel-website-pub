# ![pgp encrypt action](_images/kamelets/pgp-encrypt-action.svg) PGP Encrypt Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Encrypts the body of each message with OpenPGP for the public key of a recipient, and can also sign it, as GnuPG (gpg) does.

Use it to encrypt a file before you send it to a partner, for example with `sftp-sink`, `ftp-sink` or `aws-s3-sink`, when the partner gave you their public key. The partner decrypts it with gpg, or with `pgp-decrypt-action`.

Input: any body: text, bytes, a stream or a file.

Output: the body is the OpenPGP message, as a stream: binary, or ASCII text that starts with `-----BEGIN PGP MESSAGE-----` when `armored` is true. The `Content-Type` header is set to `application/pgp-encrypted`. The other headers are kept.

Good to know: the data is compressed, encrypted with AES-256 and protected against changes. When `signingKeyRing` is set, the message is also signed with your secret key, with SHA-256, so the recipient can check that it comes from you. The keys and the passphrase come only from the options: the headers of the message, such as `CamelPGPDataFormatKeyUserid`, are removed first, so a message cannot choose another key. The file name in the `CamelFileName` header, which file sources set, is stored in the message. A key ring that cannot be read, or a `keyUserId` that matches no key, fails each message. When `signingKeyRing` is set without `signingKeyUserId` or `signingPassphrase`, the Kamelet does not start.

## Configuration Options

The following table summarizes the configuration options available for the `pgp-encrypt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **keyUserId** | Key User ID | **Required** Which key of the key ring to encrypt for: its user id, such as `Partner Ltd <[files@partner.example.com](mailto:files@partner.example.com)>`, or a part of it, such as the email address. The message is encrypted for every key whose user id contains this text. | string |  | files@partner.example.com// |
| **publicKeyRing** | Public Key Ring | **Required** Where to load the public key ring of the recipient from: `file:` followed by the path of a file, `classpath:` followed by a resource in the application, or `base64:` followed by the key ring itself, in Base64. A key ring exported with `gpg --export`, binary or armored, fits. | string |  | file:/etc/keys/partner-public.gpg |
| **armored** | Armored | Whether to write the message as ASCII text (armored), which fits where only text is allowed, such as an email or a JSON field, instead of binary. Armored text is about a third larger. | boolean | false |  |
| **signingKeyRing** | Signing Key Ring | Where to load your secret key ring from, to sign the message: `file:`, `classpath:` or `base64:`, as for `publicKeyRing`. A key ring exported with `gpg --export-secret-keys` fits. When it is not set, the message is not signed. Requires `signingKeyUserId` and `signingPassphrase`. | string |  | file:/etc/keys/my-secret.gpg |
| **signingKeyUserId** | Signing Key User ID | Which key of `signingKeyRing` to sign with: its user id, or a part of it, such as the email address. Required when `signingKeyRing` is set. | string |  | exports@mycompany.example.com// |
| **signingPassphrase** | Signing Passphrase | The passphrase of the secret key to sign with. Required when `signingKeyRing` is set. | string |  |  |

## Dependencies

At runtime, the `pgp-encrypt-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:crypto-pgp
    

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
            uri: "kamelet:pgp-encrypt-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pgp-encrypt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pgp-encrypt-action.kamelet.yaml)