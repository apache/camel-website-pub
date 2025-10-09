# Apache camel-quarkus 3.15.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.15.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-src.zip.sha512) |
| [apache-camel-quarkus-3.15.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.15.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.15.0/apache-camel-quarkus-3.15.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.15.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.15.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6448](https://github.com/apache/camel-quarkus/issues/6448)

Restore kotlin-dsl xref doc link

[#6444](https://github.com/apache/camel-quarkus/issues/6444)

Deprecate kotlin extension

[#6441](https://github.com/apache/camel-quarkus/issues/6441)

FHIR Build time NPE when versions DSTU\_2\_1 & DSTU3 are enabled

[#6440](https://github.com/apache/camel-quarkus/issues/6440)

Use WireMock in kamelet-chucknorris example project tests

[#6430](https://github.com/apache/camel-quarkus/issues/6430)

Validator: extend test coverage

[#6425](https://github.com/apache/camel-quarkus/issues/6425)

Discover Datasonnet libraries at build time

[#6423](https://github.com/apache/camel-quarkus/issues/6423)

NPE in SupportSwaggerProcessor when sources do not include a package statement

[#6402](https://github.com/apache/camel-quarkus/issues/6402)

hashicorp-vault native support

[#6376](https://github.com/apache/camel-quarkus/issues/6376)

Combine knative tests into a single module

[#6368](https://github.com/apache/camel-quarkus/issues/6368)

Remove azure-eventhubs shared access configuration for AZURE\_IDENTITY credentials test

[#6367](https://github.com/apache/camel-quarkus/issues/6367)

Increase azure-eventhubs test coverage

[#6364](https://github.com/apache/camel-quarkus/issues/6364)

Use an Artemis container instead of \`quarkus-test-artemis\` in \`camel-quarkus-integration-test-jms-artemis-client\`

[#6362](https://github.com/apache/camel-quarkus/issues/6362)

Extend Spring-rabbitmq coverage

[#6350](https://github.com/apache/camel-quarkus/issues/6350)

smpp: no type converter available for byte properties

[#6348](https://github.com/apache/camel-quarkus/issues/6348)

Quarkus kubernetes-client not compatible with Camel

[#6344](https://github.com/apache/camel-quarkus/issues/6344)

Use Azure Event Hubs Emulator in azure-eventhubs extension testing

[#6341](https://github.com/apache/camel-quarkus/issues/6341)

Quarkus MongoDB client not compatible with Camel

[#6285](https://github.com/apache/camel-quarkus/issues/6285)

microprofile-fault-tolerance tests fail with CNFE for FallbackFunction

[#6254](https://github.com/apache/camel-quarkus/issues/6254)

hashicorp-vault extension does not work

[#6159](https://github.com/apache/camel-quarkus/issues/6159)

Remove bcprov-ext-jdk18on version override

[#6111](https://github.com/apache/camel-quarkus/issues/6111)

Ftp: test resource is applied even if test is disabled

[#6097](https://github.com/apache/camel-quarkus/issues/6097)

Remove workaround for kafka FIPS (upgrade of j11 to j17in the container)

[#6083](https://github.com/apache/camel-quarkus/issues/6083)

Camel 4.7 - Running Camel Quarkus in dev mode should pre-configure Camel in dev mode as well

[#5760](https://github.com/apache/camel-quarkus/issues/5760)

Disable max-disk-usage checks on ActiveMQ Artemis broker

[#3156](https://github.com/apache/camel-quarkus/issues/3156)

Simplify the dependency management of examples using QuarkusProcessExecutor

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).