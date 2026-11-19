# ![pqc signature action](_images/kamelets/pqc-signature-action.svg) PQC Signature Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Signs each message with a post-quantum digital signature algorithm, such as ML-DSA, or checks the signature of a message signed before.

Use it to try out post-quantum signatures, or to check inside one running application that a message was not changed between two steps: sign it with `operation` set to `sign`, and check it later with a second copy of this Kamelet with `operation` set to `verify` and the same algorithm.

Input: the body is the data to sign or to check, as text, bytes or a stream. To check, the `CamelPQCSignature` header must hold the signature that `sign` set.

Output: the body is unchanged. `sign` sets the `CamelPQCSignature` header to the signature, as bytes. `verify` sets the `CamelPQCVerification` header to true when the signature matches the body, and to false when it does not.

Good to know: unless the key pair comes from `keyStore` or `keyPair`, it is created when the application starts, so a signature can be checked only by the same running application, and not after a restart. With a key pair from a key store, a signature can be checked after a restart, and by any application that has the public key. When the application has exactly one Java `KeyStore`, or one `KeyPair`, it is used even when `keyStore` or `keyPair` is not set; `keyPairAlias` and `keyStorePassword` are then needed for the key store, else the messages fail. A `verify` without a `CamelPQCSignature` header fails the message. Headers that start with `CamelPQC`, except `CamelPQCSignature`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-signature-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **operation** | PQC Signature Operation | **Required** What to do with each message. `sign` adds a signature of the body in the `CamelPQCSignature` header; `verify` checks the body against that header and sets `CamelPQCVerification`. Enum values: \* sign \* verify | string |  |  |
| **signatureAlgorithm** | PQC Signature Algorithm | **Required** The post-quantum signature algorithm. `MLDSA` (ML-DSA, the NIST standard FIPS 204) is the usual choice; `SLHDSA` is the hash-based NIST standard. Use the same algorithm to sign and to check. Enum values: \* MLDSA \* SLHDSA \* LMS \* XMSS \* FALCON | string |  |  |
| **keyPair** | Key Pair | A Java `KeyPair` of the algorithm, defined in the application, as `#bean:` followed by its name, to use instead of `keyStore`. | string |  | #bean:pqcKeyPair |
| **keyPairAlias** | Key Pair Alias | The alias, the name in `keyStore`, of the ML-DSA key pair to use. | string |  | signer |
| **keyStore** | Key Store | A Java `KeyStore` defined in the application, as `#bean:` followed by its name, that holds the key pair to use, such as a PKCS12 file made with `keytool` (Java 24 or later makes ML-DSA keys). The key pair is then the same after a restart, and in other applications that load the same key store. Set `keyPairAlias` and `keyStorePassword` with it; without both, no key pair is taken from the key store, none is created either, and the messages fail. | string |  | #bean:pqcKeyStore |
| **keyStorePassword** | Key Store Password | The password of `keyStore`. It is also the password of the key pair in it, so both must be the same. | string |  |  |

## Dependencies

At runtime, the `pqc-signature-action` Kamelet relies upon the presence of the following dependencies:

-   camel:pqc
    
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
            uri: "kamelet:pqc-signature-action"
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

## PQC Signature Action Kamelet Description

### Key Pair

Without `keyStore` or `keyPair`, the key pair is created when the application starts. A signature can then be checked only by the same running application, and not after a restart.

To sign with a key pair that stays the same, keep it in a key store. Java 24 and later can make an ML-DSA key pair with `keytool`:

```bash
keytool -genkeypair -alias signer -keyalg ML-DSA -groupname ML-DSA-65 -dname CN=signer \
  -validity 365 -keystore pqc.p12 -storetype PKCS12 -storepass changeit
```

The key store is a Java `KeyStore` object, defined in the application, and referred to with `#bean:` followed by its name. Set `keyPairAlias` to the alias of the key pair, and `keyStorePassword` to the password of the key store, which must also be the password of the key pair. A signature made this way can be checked after a restart, and by any application that has the public key, which `keytool -exportcert` writes out as a certificate.

When the application has exactly one Java `KeyStore`, or one `KeyPair`, the Camel PQC component uses it even when `keyStore` or `keyPair` is not set. With a key store, `keyPairAlias` and `keyStorePassword` must then be set too, else the messages fail.

### Example

The following route signs a message every 10 seconds with the key pair `signer` of the key store `pqc.p12`. The key store is loaded by a Groovy script in the `beans` section, so that no Java class has to be written; Groovy needs the `camel-groovy` dependency, which Camel JBang adds by itself.

```yaml
- beans:
    - name: pqcKeyStore
      type: java.security.KeyStore
      scriptLanguage: groovy
      script: "java.security.KeyStore.getInstance(new File('pqc.p12'), '{{pqc.keystore.password}}'.toCharArray())"
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: "Hello"
      steps:
        - to:
            uri: "kamelet:pqc-signature-action"
            parameters:
              operation: sign
              signatureAlgorithm: MLDSA
              keyStore: "#bean:pqcKeyStore"
              keyPairAlias: signer
              keyStorePassword: "{{pqc.keystore.password}}"
        - to:
            uri: "kamelet:log-sink"
            parameters:
              showHeaders: true
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-signature-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-signature-action.kamelet.yaml)