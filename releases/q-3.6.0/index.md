# Apache camel-quarkus 3.6.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.6.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-src.zip.sha512) |
| [apache-camel-quarkus-3.6.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.6.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.6.0/apache-camel-quarkus-3.6.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.6.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.6.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#5536](https://github.com/apache/camel-quarkus/issues/5536)

Mail testAttachments fails on Windows

[#5522](https://github.com/apache/camel-quarkus/issues/5522)

Ftp: certificate used by the test is generated with a very short validity

[#5510](https://github.com/apache/camel-quarkus/issues/5510)

AWS SDSK >= 2.21.17 causes native build failures

[#5508](https://github.com/apache/camel-quarkus/issues/5508)

Clean up usage of hard coded hosts in tests that use containers

[#5497](https://github.com/apache/camel-quarkus/issues/5497)

Intermittent failure of QuartzQuarkusSchedulerAutowiredWithSchedulerBeanTest

[#5490](https://github.com/apache/camel-quarkus/issues/5490)

Add debug logging to gRPC extension class generation build steps

[#5464](https://github.com/apache/camel-quarkus/issues/5464)

Quarkus CDI add support for Primary beans

[#5462](https://github.com/apache/camel-quarkus/issues/5462)

Platform-http test fails in FIPS environment

[#5453](https://github.com/apache/camel-quarkus/issues/5453)

camel-spring-redis extension

[#5452](https://github.com/apache/camel-quarkus/issues/5452)

\[Camel 4.2\] perf-regression: mean throughput regression appears with Camel Quarkus 3.5.0

[#5450](https://github.com/apache/camel-quarkus/issues/5450)

camel-k-maven-plugin integration tests fail due to unable to resolve class groovy.util.XmlSlurper

[#5449](https://github.com/apache/camel-quarkus/issues/5449)

Document how users can upgrade to new Camel Quarkus releases without a Quarkus Platform release

[#5447](https://github.com/apache/camel-quarkus/issues/5447)

Enable tests and the native profiles after kubernetes client upgrade in quarkus 3.6.0

[#5444](https://github.com/apache/camel-quarkus/issues/5444)

SimpleIT.simpleExchangeMethods fails in native mode with Mandrel 23.1 JDK 21

[#5443](https://github.com/apache/camel-quarkus/issues/5443)

Intermittent failure of debug integration test

[#5442](https://github.com/apache/camel-quarkus/issues/5442)

cxf-soap CxfSoapMtomAwtIT fails with Mandrel 23.1 JDK 21

[#5427](https://github.com/apache/camel-quarkus/issues/5427)

camel-quarkus-jira WatchUpdates Bug

[#5378](https://github.com/apache/camel-quarkus/issues/5378)

Automatically register beans with methods annotated with \`@Handler\` for reflection

[#5349](https://github.com/apache/camel-quarkus/issues/5349)

Review Camel service include patterns

[#5330](https://github.com/apache/camel-quarkus/issues/5330)

OOM after migrating to 3.2.6

[#5278](https://github.com/apache/camel-quarkus/issues/5278)

DataformatTest.snakeYaml test throws NoClassDefFoundError trustedTagInspector

[#4713](https://github.com/apache/camel-quarkus/issues/4713)

Add support for Salesforce pub / sub API

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).