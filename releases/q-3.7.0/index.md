# Apache camel-quarkus 3.7.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.7.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-src.zip.sha512) |
| [apache-camel-quarkus-3.7.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.7.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.7.0/apache-camel-quarkus-3.7.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.7.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.7.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5667](https://github.com/apache/camel-quarkus/issues/5667)

Promote camel-quarkus-xj to support native mode

[#5666](https://github.com/apache/camel-quarkus/issues/5666)

JdbcTemplate is missing a resource bunde for native

[#5663](https://github.com/apache/camel-quarkus/issues/5663)

Broken icon URL in quarkus-extension.yaml

[#5661](https://github.com/apache/camel-quarkus/issues/5661)

Remove Camel Facebook extension

[#5639](https://github.com/apache/camel-quarkus/issues/5639)

Add support for s390x architecture to gRPC codegen

[#5633](https://github.com/apache/camel-quarkus/issues/5633)

Use Quarkus Derby DevServices for SQL integration test

[#5631](https://github.com/apache/camel-quarkus/issues/5631)

Replace \`tinyproxy\` container image with an embedded HTTP proxy server

[#5626](https://github.com/apache/camel-quarkus/issues/5626)

Use Strimzi Kafka container image for Kafka testing

[#5617](https://github.com/apache/camel-quarkus/issues/5617)

Camel 4.4 - HDFS component removed

[#5603](https://github.com/apache/camel-quarkus/issues/5603)

Remove JFR & BigQuery Netty tryReflectionSetAccessible native workaround from application.properties

[#5582](https://github.com/apache/camel-quarkus/issues/5582)

Adding extension for SMB

[#5578](https://github.com/apache/camel-quarkus/issues/5578)

Use Java source for Kotlin extension build time code

[#5559](https://github.com/apache/camel-quarkus/issues/5559)

Some openapi-java array types cannot be configured

[#5554](https://github.com/apache/camel-quarkus/issues/5554)

openapi-java native applications fail at runtime when REST DSL param arrayType and allowableValues are specified

[#5549](https://github.com/apache/camel-quarkus/issues/5549)

Publish SBOM in dist/release

[#5538](https://github.com/apache/camel-quarkus/issues/5538)

Tarfile enable tests when common-compress 1.25.0 is consumed from Quarkus

[#5528](https://github.com/apache/camel-quarkus/issues/5528)

Revist RestOpenApiReaderSubstitutions

[#5515](https://github.com/apache/camel-quarkus/issues/5515)

Native build runs out of memory on GitHub actions when io.fabric8:openshift-client is on the classpath

[#5502](https://github.com/apache/camel-quarkus/issues/5502)

Salesforce PubSubApiConsumer fails to load POJO class in test mode

[#5493](https://github.com/apache/camel-quarkus/issues/5493)

flatten-bom goal fails due to unresolved versions \`org.jboss:jdk-misc:${version.jdk-misc}\`

[#5332](https://github.com/apache/camel-quarkus/issues/5332)

Reinstate CI workflow job \`integration-tests-alternative-jdk\` for JDK 21

[#5110](https://github.com/apache/camel-quarkus/issues/5110)

Debezium tests fail with NoSuchMethodException

[#5081](https://github.com/apache/camel-quarkus/issues/5081)

HazelcastMapTest fails when run after HazelcastIdempotentTest and HazelcastInstanceTest

[#4989](https://github.com/apache/camel-quarkus/issues/4989)

Intermittent failure of integration test \`HazelcastListTest\`

[#792](https://github.com/apache/camel-quarkus/issues/792)

Jasypt native support

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).