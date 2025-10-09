# Apache camel-quarkus 3.9.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.9.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-src.zip.sha512) |
| [apache-camel-quarkus-3.9.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.9.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.9.0/apache-camel-quarkus-3.9.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.9.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.9.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5891](https://github.com/apache/camel-quarkus/issues/5891)

OpenAPI model not considering mixins in natibe build

[#5874](https://github.com/apache/camel-quarkus/issues/5874)

Jasypt password sysenv: prefix leads to an NPE at build time if the environment variable does not exist

[#5873](https://github.com/apache/camel-quarkus/issues/5873)

jsh-dsl integration test fails on Windows

[#5872](https://github.com/apache/camel-quarkus/issues/5872)

java-joor-dsl integration test fails on Windows

[#5870](https://github.com/apache/camel-quarkus/issues/5870)

git native integration test fails with NoSuchMethodException

[#5866](https://github.com/apache/camel-quarkus/issues/5866)

Adding camel-quarkus-google-pubsub to project leads to ClassNotFoundException: io.vertx.grpc.server.GrpcServer

[#5860](https://github.com/apache/camel-quarkus/issues/5860)

Create Qdrant JVM only extension

[#5853](https://github.com/apache/camel-quarkus/issues/5853)

Only include CloudEvents transformer service pattern if camel-quarkus-cloudevents is on the classpath

[#5835](https://github.com/apache/camel-quarkus/issues/5835)

Enable web.xml to be used to configure CamelHttpTransportServlet for the servlet extension

[#5834](https://github.com/apache/camel-quarkus/issues/5834)

Add additional options to Servlet extension configuration

[#5809](https://github.com/apache/camel-quarkus/issues/5809)

jt400: add mock tests and make them work in native

[#5803](https://github.com/apache/camel-quarkus/issues/5803)

beanio extension metadata is not up to date

[#5776](https://github.com/apache/camel-quarkus/issues/5776)

FOP FopTest.convertToPdf hangs on Windows

[#5650](https://github.com/apache/camel-quarkus/issues/5650)

\[quarkus-main\] Native build may fail with ClassNotFoundException when quarkus-jaxb is on the classpath

[#5326](https://github.com/apache/camel-quarkus/issues/5326)

Add capability to configure \`MultiPartConfig\` for \`CamelServlet\`

[#3204](https://github.com/apache/camel-quarkus/issues/3204)

Usage of \`CamelHttpTransportServlet\` results in CDI bean removal

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).