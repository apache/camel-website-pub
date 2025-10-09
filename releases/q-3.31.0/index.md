# Apache camel-quarkus 3.31.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.31.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-src.zip.sha512) |
| [apache-camel-quarkus-3.31.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.31.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.31.0/apache-camel-quarkus-3.31.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.31.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.31.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#8186](https://github.com/apache/camel-quarkus/issues/8186)

Weaviate: when a request fails (i.e. when collection does not exist), the result code is missing in the native

[#8180](https://github.com/apache/camel-quarkus/issues/8180)

wiremock test support - handle correctly recording url ending with /

[#8165](https://github.com/apache/camel-quarkus/issues/8165)

Add support for type mappings when generating code from OpenAPI specifications.

[#8158](https://github.com/apache/camel-quarkus/issues/8158)

native build failed for smb+quartz

[#8153](https://github.com/apache/camel-quarkus/issues/8153)

Langchain4jAgentTest.agentWithMcpClient fails to match correct WireMock stub

[#8147](https://github.com/apache/camel-quarkus/issues/8147)

netty-http authentication tests fail due to NPE in native mode

[#8140](https://github.com/apache/camel-quarkus/issues/8140)

cyberark-vault tests fail on container startup on MacOs with Podman Machine

[#8137](https://github.com/apache/camel-quarkus/issues/8137)

Enable JMS IBM MQ tests

[#8130](https://github.com/apache/camel-quarkus/issues/8130)

Rename camel-quarkus-junit5 as camel-quarkus-junit

[#8117](https://github.com/apache/camel-quarkus/issues/8117)

Windows: tooling/perf-regression fails with CreateProcess error=193 (%1 not a valid Win32 application)

[#8114](https://github.com/apache/camel-quarkus/issues/8114)

Rationalize master extension integration testing

[#8113](https://github.com/apache/camel-quarkus/issues/8113)

Upgrade Mysql test container and dev service from 8 to 9

[#8111](https://github.com/apache/camel-quarkus/issues/8111)

Upgrade opensearch test container to 3.1.0

[#8110](https://github.com/apache/camel-quarkus/issues/8110)

Upgrade aws localstack test container to 4.9.2+ (from 3.x)

[#8109](https://github.com/apache/camel-quarkus/issues/8109)

Upgrade greenmail test container to 2.1.8

[#8108](https://github.com/apache/camel-quarkus/issues/8108)

Upgrade Debezium Postgres test container to 17

[#8107](https://github.com/apache/camel-quarkus/issues/8107)

Upgrade Splunk test container to 9.4.7

[#8103](https://github.com/apache/camel-quarkus/issues/8103)

Remove manual reflection configs registration from data extract example

[#8098](https://github.com/apache/camel-quarkus/issues/8098)

Camel 4.17 - camel-cluster updates from CAMEL-22807

[#8095](https://github.com/apache/camel-quarkus/issues/8095)

Native integration tests failing on startup due to quarkus.http.test-port not found in any config source

[#8081](https://github.com/apache/camel-quarkus/issues/8081)

Camel 4.17 - camel-once extension

[#8067](https://github.com/apache/camel-quarkus/issues/8067)

\[FOP\] Fix PDF generation in native when loading images using fo:external-graphic

[#8066](https://github.com/apache/camel-quarkus/issues/8066)

camel-openapi-java - Integrate Quarkus swagger console with camel rest-dsl

[#8064](https://github.com/apache/camel-quarkus/issues/8064)

\[examples\] Unify command for native build

[#8063](https://github.com/apache/camel-quarkus/issues/8063)

Kubernetes integration test native build fails due to Image generator watchdog detected no activity

[#8061](https://github.com/apache/camel-quarkus/issues/8061)

Default enabling of complete reflection types breaks netty-http & cxf-soap integration test native compilation

[#8059](https://github.com/apache/camel-quarkus/issues/8059)

BindToRegistry targets in RouteBuilder beans get instantiated twice

[#8049](https://github.com/apache/camel-quarkus/issues/8049)

Adapt to Testcontainers 2.0.x

[#8040](https://github.com/apache/camel-quarkus/issues/8040)

Camel 4.17 - camel-cli-debug extension

[#8037](https://github.com/apache/camel-quarkus/issues/8037)

CyberArk Vault native support

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).