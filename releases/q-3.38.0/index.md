# Apache camel-quarkus 3.38.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.38.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-src.zip.sha512) |
| [apache-camel-quarkus-3.38.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.38.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.38.0/apache-camel-quarkus-3.38.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.38.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.38.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#8898](https://github.com/apache/camel-quarkus/issues/8898)

Use Develocity Apache instance to track flaky tests

[#8897](https://github.com/apache/camel-quarkus/issues/8897)

\[example\] CyberArk-vault example

[#8886](https://github.com/apache/camel-quarkus/issues/8886)

Add integration test coverage for CyberArk Vault alternative authentication methods

[#8884](https://github.com/apache/camel-quarkus/issues/8884)

Add integration test coverage for CyberArk Vault property placeholder, dynamic headers, and secret versioning

[#8860](https://github.com/apache/camel-quarkus/issues/8860)

Native image build failure: unresolved zstd-jni reference in httpclient5 support extension

[#8796](https://github.com/apache/camel-quarkus/issues/8796)

camel-quarkus-core extension incorrectly marked as deprecated

[#8783](https://github.com/apache/camel-quarkus/issues/8783)

SpringKotlinProcessor isKotlinStdlibAvailable check incorrectly matches kotlin-stdlib from -dependency artifacts

[#8780](https://github.com/apache/camel-quarkus/issues/8780)

Add A2A extension

[#8760](https://github.com/apache/camel-quarkus/issues/8760)

Migrate from localstack to floci

[#8754](https://github.com/apache/camel-quarkus/issues/8754)

Document vertx-websocket limitations when used with knative extension

[#8734](https://github.com/apache/camel-quarkus/issues/8734)

Add root pom.xml to camel-quarkus-examples

[#8729](https://github.com/apache/camel-quarkus/issues/8729)

Counter not working in Camel Quarkus Kafka Example

[#8720](https://github.com/apache/camel-quarkus/issues/8720)

\[quarkus-main\] cxf-soap-grouped native application fails to compile due to service registration with GeneratedResourceBuildItem

[#8702](https://github.com/apache/camel-quarkus/issues/8702)

Add Quarkus configuration support for ErrorRegistry SPI (CAMEL-23079)

[#8701](https://github.com/apache/camel-quarkus/issues/8701)

Remove camel-quarkus-github extension (camel-github was removed from Camel core)

[#8700](https://github.com/apache/camel-quarkus/issues/8700)

Camel Quarkus 3.36.0 - FTP test failing in Quarkus platform

[#8691](https://github.com/apache/camel-quarkus/issues/8691)

\[examples\] cxf-soap: fix the example after CAMEL-23526

[#8690](https://github.com/apache/camel-quarkus/issues/8690)

Move langchain4j-agent-ql4j integration test to native mode support

[#8686](https://github.com/apache/camel-quarkus/issues/8686)

Do not hit repo.maven.apache.org from tests

[#8685](https://github.com/apache/camel-quarkus/issues/8685)

Add github2 extension

[#8624](https://github.com/apache/camel-quarkus/issues/8624)

Camel 4.21 - Diagram routes into quarkus dev console

[#8621](https://github.com/apache/camel-quarkus/issues/8621)

Test Debezium with KafkaOffsetBackingStore offset storage

[#8592](https://github.com/apache/camel-quarkus/issues/8592)

Camel 4.21 - camel-jsoup extension

[#8584](https://github.com/apache/camel-quarkus/issues/8584)

CAMEL-23250: Add Camel Quarkus auto-configuration for security policy properties (Camel 4.21)

[#8534](https://github.com/apache/camel-quarkus/issues/8534)

\[Camel 4.18.2\] OpenSSH certificate-based authentication and host verification for remote file (ftp / jsch / mina-sftp)

[#8530](https://github.com/apache/camel-quarkus/issues/8530)

Debezium extensions not compatible with kafka-clients 4.2.0

[#8504](https://github.com/apache/camel-quarkus/issues/8504)

Create an OCSF extension

[#8412](https://github.com/apache/camel-quarkus/issues/8412)

Langchain4jAgentQl4jTest.simpleUserMessage application fails on startup due to UnsatisfiedLinkError

[#8318](https://github.com/apache/camel-quarkus/issues/8318)

Test framework: flaky tests after upgrade to Camel 4.18.0

[#7733](https://github.com/apache/camel-quarkus/issues/7733)

Intermittent failure of GroupedAws2KinesisTest#failingDefaultCredentialsProviderTest

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).