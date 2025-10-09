# Apache camel-quarkus 3.13.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.13.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-src.zip.sha512) |
| [apache-camel-quarkus-3.13.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.13.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.13.0/apache-camel-quarkus-3.13.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.13.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.13.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6291](https://github.com/apache/camel-quarkus/issues/6291)

camel-quarkus-syslog not compatible with quarkus-jdbc-oracle extension in native mode

[#6278](https://github.com/apache/camel-quarkus/issues/6278)

Status code 404 when upgrading quarkus-langchain4j > 0.16.2 invoking: Rest Client method: 'io.quarkiverse.langchain4j.ollama.OllamaRestApi#chat'

[#6271](https://github.com/apache/camel-quarkus/issues/6271)

\[fips\] jdbc/db2 native should be disabled for FIPS

[#6265](https://github.com/apache/camel-quarkus/issues/6265)

\[fips\] Jdbc - mysql : test fails on FIPS enabled system when executed in "jdbc-grupped" module

[#6248](https://github.com/apache/camel-quarkus/issues/6248)

Add azure-key-vault native support

[#6245](https://github.com/apache/camel-quarkus/issues/6245)

JPA testProducerNativeQuery fails for MySQL and MariaDB databases

[#6239](https://github.com/apache/camel-quarkus/issues/6239)

gRPC extension Gradle dev mode causes CNFE for io.quarkus.virtual.threads.VirtualThreadsConfig

[#6230](https://github.com/apache/camel-quarkus/issues/6230)

Caffeine does not work in native mode if stats are enabled

[#6224](https://github.com/apache/camel-quarkus/issues/6224)

Caffeine time based eviction policy does not work in native mode

[#6218](https://github.com/apache/camel-quarkus/issues/6218)

ical Dataformat fails in native

[#6214](https://github.com/apache/camel-quarkus/issues/6214)

Configure ArangoDB component to use the Quarkus managed Vertx instance

[#6212](https://github.com/apache/camel-quarkus/issues/6212)

Camel 4.7: Remove camel-quarkus-jaxb dependency from camel-quarkus-management

[#6199](https://github.com/apache/camel-quarkus/issues/6199)

Camel Quarkus Catalog - Add beans

[#6198](https://github.com/apache/camel-quarkus/issues/6198)

couchdb: native mode has to be fixed for a different implentation

[#6196](https://github.com/apache/camel-quarkus/issues/6196)

Log the Camel Quarkus version on startup

[#6172](https://github.com/apache/camel-quarkus/issues/6172)

Use elasticsearch-rest-client component configuration options in ElasticsearchRestTestResource

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).