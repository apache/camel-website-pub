# Apache camel-quarkus 3.30.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.30.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-src.zip.sha512) |
| [apache-camel-quarkus-3.30.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.30.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.30.0/apache-camel-quarkus-3.30.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.30.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.30.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#7971](https://github.com/apache/camel-quarkus/issues/7971)

Automatic reloading not working with yaml and xml dsl using filename pattern \*.camel.(yaml|xml)

[#7964](https://github.com/apache/camel-quarkus/issues/7964)

opentelemetry2 trace-processors does not work

[#7955](https://github.com/apache/camel-quarkus/issues/7955)

\[camel-quarkus-qute\] Allow dynamic templates to set the content-type not linked to template file extensions

[#7953](https://github.com/apache/camel-quarkus/issues/7953)

jms-artemis-ra integration tests fail during augmentation phase due to ClassCastException

[#7944](https://github.com/apache/camel-quarkus/issues/7944)

CXF Soap Grouped tests failing on CI

[#7942](https://github.com/apache/camel-quarkus/issues/7942)

Add generation of pqc-dataformat xref

[#7941](https://github.com/apache/camel-quarkus/issues/7941)

Native debezium-oracle test failure

[#7916](https://github.com/apache/camel-quarkus/issues/7916)

Camel Quarkus OpenAPI codegen outputs Java files under target/generated-sources/camel-quarkus-rest-openapi/src/main/java, causing package mismatch

[#7899](https://github.com/apache/camel-quarkus/issues/7899)

Remove Derby database testing

[#7897](https://github.com/apache/camel-quarkus/issues/7897)

Flaky test GrpcTest.forwardOnError (on windows?)

[#7895](https://github.com/apache/camel-quarkus/issues/7895)

\[JDK25\] JpaTestBase.findFruit ServiceConfiguration jakarta.json.bind.spi.JsonbProvider: org.eclipse.yasson.JsonBindingProvider not a subtype

[#7894](https://github.com/apache/camel-quarkus/issues/7894)

\[JDK25\] JolokiaKubernetesClientSSLTest.clientSSLAuthentication JolokiaKubernetesClientSSLTest.clientSSLAuthentication

[#7893](https://github.com/apache/camel-quarkus/issues/7893)

\[JDK25\]InfinispanCommonTest.query: No marshaller registered for object of Java type org.apache.camel.quarkus.component.infinispan.common.model.Person

[#7843](https://github.com/apache/camel-quarkus/issues/7843)

jboss logmanager breaks exception logging

[#7806](https://github.com/apache/camel-quarkus/issues/7806)

Increase opentelemetry2 extension test coverage

[#6698](https://github.com/apache/camel-quarkus/issues/6698)

maven-release-plugin 3.1.1 release:prepare fails to resolve version expression : ${camel-quarkus.version}

[#6517](https://github.com/apache/camel-quarkus/issues/6517)

Debezium tests are failing on the Platform due to failed startup of \`mcr.microsoft.com/mssql/server:2022-latest\`

[#6104](https://github.com/apache/camel-quarkus/issues/6104)

Camel 4.7 - camel-activemq6

[#5478](https://github.com/apache/camel-quarkus/issues/5478)

Add support & test coverage for \`transformer\` features

[#4259](https://github.com/apache/camel-quarkus/issues/4259)

\[Quarkus 2.14.0\] Kudu integration tests are failing in Quarkus platform

[#3037](https://github.com/apache/camel-quarkus/issues/3037)

Intermittent failure of GrpcTest.forwardOnError

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).