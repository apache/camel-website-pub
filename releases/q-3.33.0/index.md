# Apache camel-quarkus 3.33.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.33.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-src.zip.sha512) |
| [apache-camel-quarkus-3.33.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.33.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.33.0/apache-camel-quarkus-3.33.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.33.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.33.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#8405](https://github.com/apache/camel-quarkus/issues/8405)

SQL integration test throws LinkageError for org.springframework.core.convert.ConversionService

[#8400](https://github.com/apache/camel-quarkus/issues/8400)

Remove deprecated Jolokia register-management-endpoint config option

[#8391](https://github.com/apache/camel-quarkus/issues/8391)

Move file-cluster-service config options to ConfigPhase.RUN\_TIME

[#8388](https://github.com/apache/camel-quarkus/issues/8388)

REST OpenApi: missing import for @RegisterForReflection

[#8370](https://github.com/apache/camel-quarkus/issues/8370)

langchain4j-agent: issue when using OnnxBertBiEncoder models in rag scenarios

[#8349](https://github.com/apache/camel-quarkus/issues/8349)

Cannot reflectively access the proxy class inheriting \['org.apache.fop.fonts.FontEventProducer'\] with native Apache FOP

[#8333](https://github.com/apache/camel-quarkus/issues/8333)

Add mina-sftp integration tests & native support

[#8319](https://github.com/apache/camel-quarkus/issues/8319)

Elasticsearch-jvm: flaky test "testElasticsearchBulk"

[#8136](https://github.com/apache/camel-quarkus/issues/8136)

Infinispan stats operation always returns -1

[#8091](https://github.com/apache/camel-quarkus/issues/8091)

camel-keycloak - add test and native support for camel 4.17 features

[#8090](https://github.com/apache/camel-quarkus/issues/8090)

camel-keycloak - Increase tests coverage of Keycloak component

[#7813](https://github.com/apache/camel-quarkus/issues/7813)

camel-quarkus-opentelemetry2 disconnected platform-http spans

[#6025](https://github.com/apache/camel-quarkus/issues/6025)

Milvus native support

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).