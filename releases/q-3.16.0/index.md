# Apache camel-quarkus 3.16.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.16.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-src.zip.sha512) |
| [apache-camel-quarkus-3.16.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.16.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.16.0/apache-camel-quarkus-3.16.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.16.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.16.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6676](https://github.com/apache/camel-quarkus/issues/6676)

Get rid of crypto entries in The BOM with classifier bcfips.

[#6657](https://github.com/apache/camel-quarkus/issues/6657)

Jdbc/mysql Not it is inot necessary to use external DB for the FIPS testing

[#6651](https://github.com/apache/camel-quarkus/issues/6651)

jq extension does not load built in functions in native mode

[#6633](https://github.com/apache/camel-quarkus/issues/6633)

cluster-leader-election example is missing kubernetes-cluster-service extension dependency

[#6632](https://github.com/apache/camel-quarkus/issues/6632)

Add BeanIO native support

[#6618](https://github.com/apache/camel-quarkus/issues/6618)

Set sponsor field in extension metadata

[#6608](https://github.com/apache/camel-quarkus/issues/6608)

Groovy-dsl extension should be deprecated

[#6581](https://github.com/apache/camel-quarkus/issues/6581)

Kamelet with bean definitions results in bytecode serialization issues at build time

[#6576](https://github.com/apache/camel-quarkus/issues/6576)

Smb: extend test coverage for producer

[#6575](https://github.com/apache/camel-quarkus/issues/6575)

Make Camel Tracer beans unremovable

[#6565](https://github.com/apache/camel-quarkus/issues/6565)

Development of AbstractTestSupport marks some method deprecated in Camel

[#6559](https://github.com/apache/camel-quarkus/issues/6559)

git extension native compilation fails due to ClassNotFoundException: org.eclipse.jgit.lib.GpgSigner

[#6553](https://github.com/apache/camel-quarkus/issues/6553)

Issue in maven-plugin for generation of beans json

[#6543](https://github.com/apache/camel-quarkus/issues/6543)

Quarkus LangChain4j 0.19.0.CR1: Fix usage of camel annotations with Ai Services

[#6538](https://github.com/apache/camel-quarkus/issues/6538)

aws-bedrock and aws2-eventbridge native compilation fails due to missing camel-quarkus-support-aws2 extension

[#6536](https://github.com/apache/camel-quarkus/issues/6536)

sjms & sjms2 extensions should depend on jakarta.jms-api

[#6534](https://github.com/apache/camel-quarkus/issues/6534)

Create camel-quarkus-langchain4j extension

[#6531](https://github.com/apache/camel-quarkus/issues/6531)

Dropbox native compilation fails due to missing quarkus-netty dependency

[#6530](https://github.com/apache/camel-quarkus/issues/6530)

FHIR native compilation fails due to CNFE for org.apache.commons.collections4.CollectionUtils

[#6528](https://github.com/apache/camel-quarkus/issues/6528)

hashicorp-vault tests fail in the Quarkus Platform

[#6499](https://github.com/apache/camel-quarkus/issues/6499)

Switch to io.smallrye.certs:smallrye-certificate-generator-junit5

[#6498](https://github.com/apache/camel-quarkus/issues/6498)

openapi-java deployment module fails to compile due to missing DefinitionReader class

[#6489](https://github.com/apache/camel-quarkus/issues/6489)

Investigate Windows BindException occurrences on netty and syslog tests

[#6479](https://github.com/apache/camel-quarkus/issues/6479)

Make BindToRegistry work outside of RouteBuilder classes

[#6418](https://github.com/apache/camel-quarkus/issues/6418)

UpdateExtensionDocPageMojo is broken

[#4127](https://github.com/apache/camel-quarkus/issues/4127)

Splunk: extend test coverage by TLS

[#4091](https://github.com/apache/camel-quarkus/issues/4091)

Investigate whether \`netty-tcnative-boringssl-static\` can be removed from \`azure-core\` extension

[#2957](https://github.com/apache/camel-quarkus/issues/2957)

JmsTest.testJmsTransaction() and JmsTest.testResequence() fail intermittently

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).