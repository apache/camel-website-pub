# PGP

JVM since3.13.0 Native since3.13.0

Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP

## What’s inside

-   [PGP (Pretty Good Privacy Cryptographic) data format](../../../../components/4.22.x/dataformats/pgp-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-crypto-pgp)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-crypto-pgp</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### FIPS

It may not be possible to run `crypto` and `crypto-pgp` extensions together on FIPS enabled system. For example if `crypto` uses `BCFIPS` provider and `crypto-pgp` uses `BC` provider, it is not possible to have both providers on one classpath.