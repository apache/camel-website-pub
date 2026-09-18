# Crypto (JCE)

JVM since1.1.0 Native since1.2.0

Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE).

## What’s inside

-   [Crypto (Java Cryptographic Extension) data format](../../../../components/4.18.x/dataformats/crypto-dataformat.md)
    
-   [Crypto (JCE) component](../../../../components/4.18.x/crypto-component.md), URI syntax: `crypto:cryptoOperation:name`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-crypto)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-crypto</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Security Provider

This extension requires a BouncyCastle security provider to be [registered](https://quarkus.io/guides/security-customization#registering-security-providers) and also utilizes the quarkus security extension.

> **Note**
> If no BouncyCastle provider is registered via the `quarkus.security.security-providers` configuration property, then a default `BC` provider is registered automatically.

### FIPS

When running the `crypto` extension on a FIPS enabled system, a FIPS-compliant Java Security Provider (such as `BCFIPS`) has to be used.

In the case of `BCFIPS`, add dependencies `bc-fips` and `quarkus-security` to your application.

```xml
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bc-fips</artifactId>
</dependency>
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-security</artifactId>
</dependency>
```

Then register the `BCFIPS` security provider by adding the following configuration to `application.properties`.

```properties
quarkus.security.security-providers=BCFIPS
```

Alternatively, you can add a different FIPS compliant provider and register it via the `quarkus.security.security-providers` configuration property.

Refer to the [Quarkus Security guide](https://quarkus.io/guides/security-customization#bouncy-castle-fips) for more information.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).