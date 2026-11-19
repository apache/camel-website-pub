# ![pqc kem action](_images/kamelets/pqc-kem-action.svg) PQC Key Encapsulation/Decapsulation Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates a new secret key for a symmetric cipher, such as AES, together with its encapsulation by a post-quantum algorithm such as ML-KEM, or takes the secret key back out of such an encapsulation.

Use it to try out post-quantum key establishment (a KEM, key encapsulation mechanism): one step creates a secret key and its encapsulation, the protected form of the key that may be sent to the holder of the private key, and a later step takes the same secret key out of it. To encrypt the messages themselves with a fixed key, use `crypto-encrypt-action`.

Input: for `generateSecretKeyEncapsulation`, any body; it is not used. For `extractSecretKeyEncapsulation` and `extractSecretKeyFromEncapsulation`, the body must be the result of `generateSecretKeyEncapsulation`.

Output: `generateSecretKeyEncapsulation` and `extractSecretKeyEncapsulation` give a Java object that holds the secret key and its encapsulation. `extractSecretKeyFromEncapsulation` gives the secret key, as a Java object. None of them is text or bytes, so the next step must be one that works with Java key objects.

Good to know: unless the key pair of the post-quantum algorithm comes from `keyStore` or `keyPair`, it is created when the application starts, so an encapsulation can be opened only by the same running application. Headers that start with `CamelPQC` are removed from the message first, so they cannot change what the Kamelet does. With a key pair from a key store, it can be opened after a restart, and by any application that has the key store. When the application has exactly one Java `KeyStore`, or one `KeyPair`, it is used even when `keyStore` or `keyPair` is not set; `keyPairAlias` and `keyStorePassword` are then needed for the key store, else the messages fail.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-kem-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **keyEncapsulationAlgorithm** | PQC Key Encapsulation Algorithm | **Required** The post-quantum algorithm that encapsulates the secret key. `MLKEM` (ML-KEM, the NIST standard FIPS 203) is the usual choice. Use the same algorithm in the steps that create and that open an encapsulation. Enum values: \* MLKEM \* BIKE \* HQC \* CMCE \* SABER \* FRODO \* NTRU \* NTRULPRime | string |  |  |
| **operation** | PQC KEM Operation | **Required** What to do with each message. `generateSecretKeyEncapsulation` creates a new secret key and its encapsulation; `extractSecretKeyEncapsulation` gives the encapsulation again; `extractSecretKeyFromEncapsulation` gives the secret key taken out of the encapsulation. Enum values: \* generateSecretKeyEncapsulation \* extractSecretKeyEncapsulation \* extractSecretKeyFromEncapsulation | string |  |  |
| **symmetricKeyAlgorithm** | Symmetric Key Algorithm | **Required** The symmetric cipher the secret key is for, such as `AES`, the usual choice. The cipher must accept a key of the length in `symmetricKeyLength`, 256 bits when it is not set; with one that does not, such as `SEED` or `SM4` with 256 bits, the integration fails to start. Enum values: \* AES \* RC2 \* RC5 \* ARIA \* CAMELLIA \* CAST5 \* CAST6 \* CHACHA7539 \* DSTU7624 \* GOST28147 \* GOST3412\_2015 \* GRAIN128 \* HC128 \* HC256 \* SALSA20 \* SEED \* SM4 \* DESEDE | string |  |  |
| **keyPair** | Key Pair | A Java `KeyPair` of the algorithm, defined in the application, as `#bean:` followed by its name, to use instead of `keyStore`. | string |  | #bean:pqcKeyPair |
| **keyPairAlias** | Key Pair Alias | The alias, the name in `keyStore`, of the ML-KEM key pair to use. | string |  | kem |
| **keyStore** | Key Store | A Java `KeyStore` defined in the application, as `#bean:` followed by its name, that holds the key pair to use, such as a PKCS12 file made with `keytool` (Java 24 or later makes ML-KEM keys). The key pair is then the same after a restart, and in other applications that load the same key store. Set `keyPairAlias` and `keyStorePassword` with it; without both, no key pair is taken from the key store, none is created either, and the messages fail. | string |  | #bean:pqcKeyStore |
| **keyStorePassword** | Key Store Password | The password of `keyStore`. It is also the password of the key pair in it, so both must be the same. | string |  |  |
| **symmetricKeyLength** | Symmetric Key Length | The length of the secret key, in bits, such as 128 or 256 for `AES`. Use the same length in the steps that create and that open an encapsulation. When it is not set, 256 is used; set it to 128 for a cipher that takes only 128-bit keys, such as `SEED` or `SM4`. | integer |  | 128 |

## Dependencies

At runtime, the `pqc-kem-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:pqc-kem-action"
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

## PQC Key Encapsulation/Decapsulation Action Kamelet Description

### Key Pair

Without `keyStore` or `keyPair`, the key pair of the post-quantum algorithm is created when the application starts. An encapsulation can then be opened only by the same running application.

To open an encapsulation after a restart, or in another application, keep the key pair in a key store. Java 24 and later can make an ML-KEM key pair with `keytool`. A key pair of a KEM cannot sign its own certificate, so `keytool` needs a signing key pair in the same key store, given with `-signer`, such as an ML-DSA one:

```bash
keytool -genkeypair -alias signer -keyalg ML-DSA -dname CN=signer \
  -validity 365 -keystore pqc.p12 -storetype PKCS12 -storepass changeit
keytool -genkeypair -alias kem -keyalg ML-KEM -groupname ML-KEM-768 -dname CN=kem -signer signer \
  -validity 365 -keystore pqc.p12 -storetype PKCS12 -storepass changeit
```

The key store is a Java `KeyStore` object, defined in the application, and referred to with `#bean:` followed by its name. Set `keyPairAlias` to the alias of the key pair, and `keyStorePassword` to the password of the key store, which must also be the password of the key pair.

When the application has exactly one Java `KeyStore`, or one `KeyPair`, the Camel PQC component uses it even when `keyStore` or `keyPair` is not set. With a key store, `keyPairAlias` and `keyStorePassword` must then be set too, else the messages fail.

### Key Length

`symmetricKeyLength` is the length of the secret key in bits, 256 when it is not set. Use the same length to create and to open an encapsulation. Set it to 128 for `SEED` and `SM4`, which take only 128-bit keys: with 256, the integration fails to start.

### Example

The following route creates a 128-bit AES key and its encapsulation with the key pair `kem` of the key store `pqc.p12`, and then takes the same key out of the encapsulation again. The key store is loaded by a Groovy script in the `beans` section, so that no Java class has to be written; Groovy needs the `camel-groovy` dependency, which Camel JBang adds by itself.

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
        message: "start"
      steps:
        - to:
            uri: "kamelet:pqc-kem-action"
            parameters:
              operation: generateSecretKeyEncapsulation
              keyEncapsulationAlgorithm: MLKEM
              symmetricKeyAlgorithm: AES
              symmetricKeyLength: 128
              keyStore: "#bean:pqcKeyStore"
              keyPairAlias: kem
              keyStorePassword: "{{pqc.keystore.password}}"
        - to:
            uri: "kamelet:pqc-kem-action"
            parameters:
              operation: extractSecretKeyEncapsulation
              keyEncapsulationAlgorithm: MLKEM
              symmetricKeyAlgorithm: AES
              symmetricKeyLength: 128
              keyStore: "#bean:pqcKeyStore"
              keyPairAlias: kem
              keyStorePassword: "{{pqc.keystore.password}}"
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-kem-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-kem-action.kamelet.yaml)