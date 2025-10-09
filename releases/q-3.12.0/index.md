# Apache camel-quarkus 3.12.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.12.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-src.zip.sha512) |
| [apache-camel-quarkus-3.12.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.12.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.12.0/apache-camel-quarkus-3.12.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.12.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.12.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6190](https://github.com/apache/camel-quarkus/issues/6190)

Jasypt SecretKeyHandler config cannot use configuration coming from Configurable Config sources

[#6182](https://github.com/apache/camel-quarkus/issues/6182)

Aws2-kinesis-firehose: test fails because STS service is not available when test is started from the integration-test-groups/was2/was2-kinesis

[#6179](https://github.com/apache/camel-quarkus/issues/6179)

\[quarkus-main\] CXF SOAP tests fail with NCDFE for io/quarkus/vertx/core/runtime/VertxBufferImpl

[#6173](https://github.com/apache/camel-quarkus/issues/6173)

Add elasticsearch-rest-client native support

[#6164](https://github.com/apache/camel-quarkus/issues/6164)

Wrong RestConsumer is used when trying to connect to Elasticsearch

[#6163](https://github.com/apache/camel-quarkus/issues/6163)

elasticsearch-rest-client host options only work if autowiring is disabled

[#6157](https://github.com/apache/camel-quarkus/issues/6157)

azure-key-vault unable to create HTTP Client

[#6154](https://github.com/apache/camel-quarkus/issues/6154)

aws2-cw flaky tests with a real service

[#6143](https://github.com/apache/camel-quarkus/issues/6143)

Add traceProcessors boolean option to opentelemetry camel extension

[#6136](https://github.com/apache/camel-quarkus/issues/6136)

\[fips\] MySql test fails in native with profile "fips"

[#6133](https://github.com/apache/camel-quarkus/issues/6133)

langchain4j-chat native support

[#6127](https://github.com/apache/camel-quarkus/issues/6127)

Ldap: try to use test-support-certificate-generator

[#6126](https://github.com/apache/camel-quarkus/issues/6126)

\[fips\] Nats - use test-support-certificate-generator

[#6125](https://github.com/apache/camel-quarkus/issues/6125)

\[fips\] Platform-http: use -support-certificate-generator

[#6065](https://github.com/apache/camel-quarkus/issues/6065)

Create Pinecone Extension

[#6047](https://github.com/apache/camel-quarkus/issues/6047)

Use WireMock in weather extension integration tests

[#5967](https://github.com/apache/camel-quarkus/issues/5967)

Improve keystore generation

[#5824](https://github.com/apache/camel-quarkus/issues/5824)

Camel 4.5 - Trace config

[#5737](https://github.com/apache/camel-quarkus/issues/5737)

Elasticsearch Low Level Rest Client : Increase test coverage

[#5704](https://github.com/apache/camel-quarkus/issues/5704)

extensions-support httpclient: The BasicAuthCache alias may not be needed anymore when adopting http client >= 5.4

[#5668](https://github.com/apache/camel-quarkus/issues/5668)

Add a Saga LRA example

[#4703](https://github.com/apache/camel-quarkus/issues/4703)

Exclude http 4.x from http extension if possible.

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).