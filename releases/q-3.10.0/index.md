# Apache camel-quarkus 3.10.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.10.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-src.zip.sha512) |
| [apache-camel-quarkus-3.10.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.10.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.10.0/apache-camel-quarkus-3.10.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.10.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.10.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6029](https://github.com/apache/camel-quarkus/issues/6029)

Jt400: possible missing resource in the native

[#6021](https://github.com/apache/camel-quarkus/issues/6021)

Activate \`format\` profile as part of CI checks

[#6018](https://github.com/apache/camel-quarkus/issues/6018)

JT400 tests can not be run in parallel

[#5999](https://github.com/apache/camel-quarkus/issues/5999)

Jt400: tests are not cleaning after themselves and parallel run fails

[#5993](https://github.com/apache/camel-quarkus/issues/5993)

jdbc-db2: fails in fips environment

[#5979](https://github.com/apache/camel-quarkus/issues/5979)

Cxf-soap: tests are not working in FIPS environment

[#5975](https://github.com/apache/camel-quarkus/issues/5975)

Simplify the process of adding example projects

[#5970](https://github.com/apache/camel-quarkus/issues/5970)

Camel 4.5 : create langchain-embeddings extension

[#5966](https://github.com/apache/camel-quarkus/issues/5966)

Http: tests are not working in FIPS environment

[#5962](https://github.com/apache/camel-quarkus/issues/5962)

camel-quarkus-spring-redis doesn't autowire RedisTemplate so it cannot be used for e.g. RedisIdempotentRepository

[#5957](https://github.com/apache/camel-quarkus/issues/5957)

Dev mode compilation error when gRPC is present

[#5953](https://github.com/apache/camel-quarkus/issues/5953)

Jt400: test for replying to an inquiry message on a message queue is missing

[#5949](https://github.com/apache/camel-quarkus/issues/5949)

Create Milvus Extension

[#5946](https://github.com/apache/camel-quarkus/issues/5946)

JasyptDevUITest fails due to the jasypt password not being configured

[#5927](https://github.com/apache/camel-quarkus/issues/5927)

JT400: Use better name of workspace in the readme.adoc

[#5926](https://github.com/apache/camel-quarkus/issues/5926)

QuarkusCxfProcessor throws NoSuchFieldError: type

[#5924](https://github.com/apache/camel-quarkus/issues/5924)

Camel 4.5: Create AWS bedrock extensions

[#5914](https://github.com/apache/camel-quarkus/issues/5914)

Jt400: integration tests should be run without flat classpath

[#5912](https://github.com/apache/camel-quarkus/issues/5912)

azure-storage-queue native build fails with UnsatisfiedLinkError

[#5899](https://github.com/apache/camel-quarkus/issues/5899)

jt400 \`com.ibm.as400.access.AS400\` should be registered for runtime reinitialization

[#5896](https://github.com/apache/camel-quarkus/issues/5896)

jt400MockTest.testWriteKeyedDataQueue fails in the Quarkus Platform

[#5893](https://github.com/apache/camel-quarkus/issues/5893)

Catalog throws IllegalArgumentException: Unexpected kind model

[#5855](https://github.com/apache/camel-quarkus/issues/5855)

Camel 4.5 - Include dev-consoles into camel-catalog

[#5851](https://github.com/apache/camel-quarkus/issues/5851)

Observability example project fails to compile. Cannot find symbol method getUptimeMillis()

[#5850](https://github.com/apache/camel-quarkus/issues/5850)

SSH tests fail due to NoSuchMethodError: boolean org.apache.sshd.client.future.ConnectFuture.await(long)

[#5849](https://github.com/apache/camel-quarkus/issues/5849)

Kamelet tests fail at build time due to StackOverflowError

[#5843](https://github.com/apache/camel-quarkus/issues/5843)

Camel 4.5 - New configuration option for camel-micrometer

[#5816](https://github.com/apache/camel-quarkus/issues/5816)

Create extension for the camel-wasm component

[#5815](https://github.com/apache/camel-quarkus/issues/5815)

Promote the Qdrant extension to native mode

[#5798](https://github.com/apache/camel-quarkus/issues/5798)

google-bigquery: tests are failing on quarkus-platform since camel-quarkus 3.8.0 release

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).