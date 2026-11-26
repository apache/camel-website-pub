# ![pgp decrypt action](_images/kamelets/pgp-decrypt-action.svg) PGP Decrypt Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Decrypts the OpenPGP message in the body of each message with your secret key, and can check its signature against the public key of the sender.

Use it to decrypt a file that a partner encrypted for you with gpg or `pgp-encrypt-action`, for example after reading it with `sftp-source`, `ftp-source` or `aws-s3-source`, and to make sure that it comes from that partner.

Input: an OpenPGP message, binary or ASCII armored (it starts with `-----BEGIN PGP MESSAGE-----`), as bytes, text, a stream or a file.

Output: the body is the decrypted data, as a stream, and the `Content-Type` header is set to `application/octet-stream`. The other headers are kept.

Good to know: a message that was not encrypted for a key in `secretKeyRing`, a wrong passphrase (the error says "checksum mismatch"), or a message that was changed on the way fails. A message without integrity protection fails too (the error says "not integrity protected"). Messages in the newer OCB format, which GnuPG 2.4 and later write for a key made with GnuPG 2.4 or later, are integrity protected and decrypt. When `verificationKeyRing` is set, a message must be signed by a key in that key ring, or it fails; set `signatureVerification` to `optional` to accept unsigned messages too. When `verificationKeyRing` is not set, a signature is not checked. The keys and the passphrase come only from the options: the headers of the message, such as `CamelPGPDataFormatKeyFileName`, are removed first, so a message cannot choose another key.

## Configuration Options

The following table summarizes the configuration options available for the `pgp-decrypt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **passphrase** | Passphrase | **Required** The passphrase of your secret key. | string |  |  |
| **secretKeyRing** | Secret Key Ring | **Required** Where to load your secret key ring from: `file:` followed by the path of a file, `classpath:` followed by a resource in the application, or `base64:` followed by the key ring itself, in Base64. A key ring exported with `gpg --export-secret-keys`, binary or armored, fits. The key to decrypt with is the one the message was encrypted for. | string |  | file:/etc/keys/my-secret.gpg |
| **signatureVerification** | Signature Verification | Only used when `verificationKeyRing` is set. `required`: a message must be signed by a key of `verificationKeyRing`. `optional`: an unsigned message is accepted too, but a signed message must still be signed by a key of `verificationKeyRing`. Enum values: \* required \* optional | string | required |  |
| **verificationKeyRing** | Verification Key Ring | Where to load the public key ring of the senders you trust from, to check the signature of each message: `file:`, `classpath:` or `base64:`, as for `secretKeyRing`. A key ring exported with `gpg --export` fits. A message signed by a key that is not in it fails. When it is not set, a signature is not checked. | string |  | file:/etc/keys/partner-public.gpg |

## Dependencies

At runtime, the `pgp-decrypt-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:pgp-decrypt-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pgp-decrypt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pgp-decrypt-action.kamelet.yaml)