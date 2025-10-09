# Apache camel-quarkus 2.14.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 11.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-2.14.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/2.14.0/apache-camel-quarkus-2.14.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/2.14.0/apache-camel-quarkus-2.14.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/2.14.0/apache-camel-quarkus-2.14.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `2.14.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 2.14.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#4242](https://github.com/apache/camel-quarkus/issues/4242)

camel-quarkus-xchange: MissingResourceException: Can't find bundle for base name sun.util.resources.CurrencyNames, locale en\_US

[#4211](https://github.com/apache/camel-quarkus/issues/4211)

Manage dependency \`com.jayway.jsonpath:json-path\`

[#4208](https://github.com/apache/camel-quarkus/issues/4208)

CxfSoapMtomIT fails in native mode

[#4203](https://github.com/apache/camel-quarkus/issues/4203)

Create test coverage for CXF SOAP MTOM

[#4180](https://github.com/apache/camel-quarkus/issues/4180)

Use official \`com.azure:azure-core-http-vertx:1.0.0-beta.1\` in Azure extensions

[#4171](https://github.com/apache/camel-quarkus/issues/4171)

Cxf-soap tests: Refactor and split

[#4169](https://github.com/apache/camel-quarkus/issues/4169)

Fallback to mocked back end for XChange tests if crypto API endpoints are not available

[#4161](https://github.com/apache/camel-quarkus/issues/4161)

SalesforceIntegrationTest.testCDCAndStreamingEvents fails

[#4149](https://github.com/apache/camel-quarkus/issues/4149)

XStream native integration test failure

[#4148](https://github.com/apache/camel-quarkus/issues/4148)

Native mode tests for serialization are failing

[#4138](https://github.com/apache/camel-quarkus/issues/4138)

Manage \`io.projectreactor:reactor-core\`

[#4123](https://github.com/apache/camel-quarkus/issues/4123)

Move org.apache.cxf.xjc-utils:cxf-xjc-runtime BOM entry to quarkus-cxf-bom

[#4117](https://github.com/apache/camel-quarkus/issues/4117)

rest-openapi: Add test cases for more specificationUri formats

[#4114](https://github.com/apache/camel-quarkus/issues/4114)

\[Quarkus 2.14.0\] PgeventTest application fails to start

[#4112](https://github.com/apache/camel-quarkus/issues/4112)

DefaultPackageScanClassResolver does not work in native mode

[#4111](https://github.com/apache/camel-quarkus/issues/4111)

kamelet-chucknorris example project tests are failing

[#4108](https://github.com/apache/camel-quarkus/issues/4108)

\[Quarkus Main\] Compatibility with Jandex 3

[#4090](https://github.com/apache/camel-quarkus/issues/4090)

\[Camel 3.19.0\] azure-core-http-client-vertx: Deployment tests are failing on java heap space

[#4086](https://github.com/apache/camel-quarkus/issues/4086)

Automatic configuration of kubernetes cluster service

[#4031](https://github.com/apache/camel-quarkus/issues/4031)

perf-regression: adopt hyperfoil-maven-plugin 0.22 when released

[#4010](https://github.com/apache/camel-quarkus/issues/4010)

Increase test coverage of ref extension

[#3951](https://github.com/apache/camel-quarkus/issues/3951)

Add a test in camel-quarkus-integration-test-jms-artemis-client with quarkus-pooled-jms

[#3904](https://github.com/apache/camel-quarkus/issues/3904)

Increase XSLT extension test coverage

[#3229](https://github.com/apache/camel-quarkus/issues/3229)

Reference Camel \`azure-sdk-bom-version\` property in \`azure-sdk-bom.version\`

[#2857](https://github.com/apache/camel-quarkus/issues/2857)

Make \`quarkus.artemis.url\` optional

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).