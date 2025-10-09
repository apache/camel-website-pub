# Apache camel-quarkus 3.17.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.17.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-src.zip.sha512) |
| [apache-camel-quarkus-3.17.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.17.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.17.0/apache-camel-quarkus-3.17.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.17.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.17.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#6838](https://github.com/apache/camel-quarkus/issues/6838)

AI services that could not be resolved by interface name

[#6832](https://github.com/apache/camel-quarkus/issues/6832)

Camel 4.9 - Add routePolicyExcludePattern to micrometer extension

[#6821](https://github.com/apache/camel-quarkus/issues/6821)

Message-bridge example: does not work if there is less then 10% of free disk space

[#6814](https://github.com/apache/camel-quarkus/issues/6814)

Camel OpenTelemetry enabled when quarkus.otel.sdk.disabled=true

[#6811](https://github.com/apache/camel-quarkus/issues/6811)

Camel JIRA - move REST underlying dependency from Quarkus Resteasy to Quarkus Rest

[#6807](https://github.com/apache/camel-quarkus/issues/6807)

Remove AdviceWithRouteBuilder type from build time route discovery

[#6792](https://github.com/apache/camel-quarkus/issues/6792)

Panache Entity not working inside routebuilder

[#6780](https://github.com/apache/camel-quarkus/issues/6780)

Native build fails when combining camel-quarkus-grpc and camel-quarkus-kafka

[#6777](https://github.com/apache/camel-quarkus/issues/6777)

Remove dependency on optional dependency org.brotli:dec

[#6772](https://github.com/apache/camel-quarkus/issues/6772)

Crypto: allow test to use SunPKCS11-NSS-FIPS security provider

[#6754](https://github.com/apache/camel-quarkus/issues/6754)

findbugs can not be excluded when depends on quarkus-grpc-common

[#6747](https://github.com/apache/camel-quarkus/issues/6747)

Opentelemetry: make sure the order of spans is correct

[#6743](https://github.com/apache/camel-quarkus/issues/6743)

Documentation for issue 5244 : Fop native failures due to pdfbox 3 upgrade

[#6736](https://github.com/apache/camel-quarkus/issues/6736)

Missing RegisterForReflection import when array schema in the spec

[#6721](https://github.com/apache/camel-quarkus/issues/6721)

jackson-avro not compatibile with Avro 1.12.x

[#6716](https://github.com/apache/camel-quarkus/issues/6716)

camel-quarkus-rest-openapi: Add @JsonIgnoreProperties configuration option

[#6709](https://github.com/apache/camel-quarkus/issues/6709)

SplunkHecTest.produceWithWrongCertificate fails in the Quarkus Platform

[#6705](https://github.com/apache/camel-quarkus/issues/6705)

Remove testing and documentation for Quarkus Amazon Services extensions

[#6702](https://github.com/apache/camel-quarkus/issues/6702)

camel-quarkus-rest-openapi: Allow custom OpenAPI specification location

[#6701](https://github.com/apache/camel-quarkus/issues/6701)

camel-quarkus-rest-openapi: Add support for OpenAPI specifications written in YAML format

[#6688](https://github.com/apache/camel-quarkus/issues/6688)

google-secret-manager: extend test coverage

[#6664](https://github.com/apache/camel-quarkus/issues/6664)

Camel 4.9 - Add support for startup condition

[#6630](https://github.com/apache/camel-quarkus/issues/6630)

Camel 4.9 - Add boot clock to CamelContext to capture boot time

[#6610](https://github.com/apache/camel-quarkus/issues/6610)

Camel 4.9 - Remove camel-groovy-dsl, camel-js-dsl and camel-jsh-dsl

[#6602](https://github.com/apache/camel-quarkus/issues/6602)

SmallRye Fault Tolerance not compatible with camel-microprofile-fault-tolerance #6584

[#6584](https://github.com/apache/camel-quarkus/issues/6584)

SmallRye Fault Tolerance 6.4.1 not compatible with camel-microprofile-fault-tolerance

[#6560](https://github.com/apache/camel-quarkus/issues/6560)

\[camel-main\] Enable csv test once quarkus upgrades commons-io to 2.17.0

[#6556](https://github.com/apache/camel-quarkus/issues/6556)

Remove workaround for catalog - beans

[#6446](https://github.com/apache/camel-quarkus/issues/6446)

Remove kotlin extensions

[#6067](https://github.com/apache/camel-quarkus/issues/6067)

Restore BootstrapConfig.enabled functionality

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).