# Apache camel-quarkus 3.20.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.20.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-src.zip.sha512) |
| [apache-camel-quarkus-3.20.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.20.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.20.0/apache-camel-quarkus-3.20.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.20.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.20.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#7148](https://github.com/apache/camel-quarkus/issues/7148)

Jolokia multiple dev mode reloads results in java.net.BindException: Address already in use

[#7142](https://github.com/apache/camel-quarkus/issues/7142)

Groovy: extend test coverage

[#7114](https://github.com/apache/camel-quarkus/issues/7114)

Jira extension should depend on quarkus-rest-client instead of quarkus-rest

[#7112](https://github.com/apache/camel-quarkus/issues/7112)

Intermittent failure of AzureServiceBusTest

[#7111](https://github.com/apache/camel-quarkus/issues/7111)

Align CXF JAX-RS dependencies with CXF version used by quarkus-cxf

[#7102](https://github.com/apache/camel-quarkus/issues/7102)

Jolokia extension redirect handler returns an invalid URL when ipv6 is enabled

[#7093](https://github.com/apache/camel-quarkus/issues/7093)

Add support for SimpleLanguageFunctionFactory

[#7088](https://github.com/apache/camel-quarkus/issues/7088)

camel-quarkus 3.19.1: problem with UnmarshalProcessor

[#7086](https://github.com/apache/camel-quarkus/issues/7086)

Smb: extend coverage with parameter 'path'

[#7077](https://github.com/apache/camel-quarkus/issues/7077)

NetworkNT JSON Schema: different validationMessages in native Quarkus application

[#7076](https://github.com/apache/camel-quarkus/issues/7076)

cxf-soap-grouped native build occasionally runs out of memory

[#7074](https://github.com/apache/camel-quarkus/issues/7074)

Contract first approach with Rest OpenApi component in Camel Quarkus overwrites the mapping for other Rest endpoints with @Path

[#7056](https://github.com/apache/camel-quarkus/issues/7056)

Azure tests grouped: key-vault test requires identity, which may fail for eventhubs

[#7051](https://github.com/apache/camel-quarkus/issues/7051)

Enable Jolokia Camel restrictor allowed MBean domains to be configurable

[#7050](https://github.com/apache/camel-quarkus/issues/7050)

Jolokia extension should set a default agent description

[#7045](https://github.com/apache/camel-quarkus/issues/7045)

Remove reflective class configuration for Kubernetes vault configuration

[#7044](https://github.com/apache/camel-quarkus/issues/7044)

Enable Kubernetes event testing for real clusters

[#7042](https://github.com/apache/camel-quarkus/issues/7042)

Enable Kubernetes context refresh tests

[#7011](https://github.com/apache/camel-quarkus/issues/7011)

Enable Kubernetes deployment test assertions

[#7001](https://github.com/apache/camel-quarkus/issues/7001)

Jolokia native support

[#6989](https://github.com/apache/camel-quarkus/issues/6989)

Add observability-services & Jolokia extensions to observability example project

[#6984](https://github.com/apache/camel-quarkus/issues/6984)

quarkus-micrometer-registry-jmx is not compatible with Quarkus >= 3.19.0

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).