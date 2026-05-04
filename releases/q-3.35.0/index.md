# Apache camel-quarkus 3.35.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.35.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-src.zip.sha512) |
| [apache-camel-quarkus-3.35.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.35.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.35.0/apache-camel-quarkus-3.35.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.35.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.35.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#8544](https://github.com/apache/camel-quarkus/issues/8544)

pollEnrich with file endpoint simple expressions do not work in native mode

[#8526](https://github.com/apache/camel-quarkus/issues/8526)

Enable recorded WireMock stubs to be loaded from isolated sub directories

[#8522](https://github.com/apache/camel-quarkus/issues/8522)

IBMMQ tests do not work on rootless podman

[#8481](https://github.com/apache/camel-quarkus/issues/8481)

Native Build Failure in mina-sftp (GraalVM 21.x)

[#8460](https://github.com/apache/camel-quarkus/issues/8460)

json-validator tests fail in the Quarkus Platform

[#8444](https://github.com/apache/camel-quarkus/pull/8444)

fix: extension metadata status is a string value

[#8377](https://github.com/apache/camel-quarkus/issues/8377)

Cover (in JVM) base langchain4j tests when quarkus-langchain4j is on claspath

[#8355](https://github.com/apache/camel-quarkus/issues/8355)

camel-minio error writing to object store since migration to 3.32.0

[#8304](https://github.com/apache/camel-quarkus/issues/8304)

Add Grafana dashboards to camel-quarkus-observability example

[#8288](https://github.com/apache/camel-quarkus/issues/8288)

Add a integration test module for Quarkus LangChain4j integration

[#8287](https://github.com/apache/camel-quarkus/issues/8287)

Disable langchain4j extension native builds steps if Quarkus LangChain4j is detected

[#8252](https://github.com/apache/camel-quarkus/issues/8252)

Debezium extensions native compilation is broken

[#8047](https://github.com/apache/camel-quarkus/issues/8047)

Increase test coverage for IBM Cloud Object Storage

[#7991](https://github.com/apache/camel-quarkus/issues/7991)

Add ibm-watson-language native support and integration tests

[#7990](https://github.com/apache/camel-quarkus/issues/7990)

Add ibm-watson-discovery native support and integration tests

[#7841](https://github.com/apache/camel-quarkus/issues/7841)

Inspect Camel route to auto-detect onException classes for native build

[#7608](https://github.com/apache/camel-quarkus/issues/7608)

Consider registering common Camel types used in onException for reflection

[#7543](https://github.com/apache/camel-quarkus/issues/7543)

Hashicorp Vault tests fail to start due to LinkageError

[#6195](https://github.com/apache/camel-quarkus/issues/6195)

Add tests in camel-quarkus-example saga

[#2777](https://github.com/apache/camel-quarkus/issues/2777)

Expand SQS test coverage

[#2402](https://github.com/apache/camel-quarkus/issues/2402)

Test AWS 2 MSK

[#2401](https://github.com/apache/camel-quarkus/issues/2401)

Test AWS 2 MQ

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).