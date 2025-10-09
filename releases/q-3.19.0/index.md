# Apache camel-quarkus 3.19.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.19.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-src.zip.sha512) |
| [apache-camel-quarkus-3.19.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.19.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.19.0/apache-camel-quarkus-3.19.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.19.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.19.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#7016](https://github.com/apache/camel-quarkus/issues/7016)

openapi-java: java.lang.IllegalArgumentException: Cannot construct instance of \`io.swagger.v3.oas.models.media.JsonSchema\` in native mode

[#7012](https://github.com/apache/camel-quarkus/issues/7012)

Use NativeMonitoringBuildItem to automatically enable native monitoring features

[#7004](https://github.com/apache/camel-quarkus/issues/7004)

Azure-key-vault: some tests might be unstable

[#7000](https://github.com/apache/camel-quarkus/issues/7000)

Enable Kubernetes tests to be run against a real cluster

[#6997](https://github.com/apache/camel-quarkus/issues/6997)

camel-console management endpoint

[#6992](https://github.com/apache/camel-quarkus/issues/6992)

azure-key-vault: make readme.adoc explicit about variables required for the test execution

[#6979](https://github.com/apache/camel-quarkus/issues/6979)

Azure-key-vault: better coverage for identity scenarios

[#6976](https://github.com/apache/camel-quarkus/issues/6976)

Aws-secrets-manager: extend test coverage for context reload with sqs service

[#6968](https://github.com/apache/camel-quarkus/issues/6968)

Test observability-services otel tracing and JMX metrics

[#6967](https://github.com/apache/camel-quarkus/issues/6967)

observability-services \`/observe\` endpoints may not be excluded from OpenTelemetry tracing

[#6960](https://github.com/apache/camel-quarkus/issues/6960)

Support \`camel.metrics.baseEndpointURIExchangeEventNotifier\`

[#6955](https://github.com/apache/camel-quarkus/issues/6955)

Evicted Pod Retains Leadership in Kubernetes

[#6954](https://github.com/apache/camel-quarkus/issues/6954)

Migrate extension configuration to @ConfigMapping

[#6952](https://github.com/apache/camel-quarkus/issues/6952)

Aws-secrets-manager: native support

[#6950](https://github.com/apache/camel-quarkus/issues/6950)

azure-servicebus: Unable to configure a custom ServiceBusProcessorClient

[#6942](https://github.com/apache/camel-quarkus/issues/6942)

Jolokia support

[#6941](https://github.com/apache/camel-quarkus/issues/6941)

ssh integration tests fail in the Quarkus Platform

[#6940](https://github.com/apache/camel-quarkus/issues/6940)

cxf-soap integration tests fail in the Quarkus Platform

[#6938](https://github.com/apache/camel-quarkus/issues/6938)

Fix missing / incorrect copyright notices

[#6934](https://github.com/apache/camel-quarkus/issues/6934)

Google-secret-manager and google-pubsub: create a common extension support

[#6933](https://github.com/apache/camel-quarkus/issues/6933)

Google-secret-manager: native support

[#6917](https://github.com/apache/camel-quarkus/issues/6917)

Ssh: refactor testResource to use embedded sshd only

[#6892](https://github.com/apache/camel-quarkus/issues/6892)

Quarkus kubernetes-client not compatible with Camel

[#6889](https://github.com/apache/camel-quarkus/issues/6889)

jt400 - Latest upgraded jt400 dependency fails in the native mode

[#6856](https://github.com/apache/camel-quarkus/issues/6856)

vertx-http event loop threads may be blocked from Camel error handler

[#6842](https://github.com/apache/camel-quarkus/issues/6842)

Intermittent failure of tests for inlined REST endpoints

[#6806](https://github.com/apache/camel-quarkus/issues/6806)

Reinstate solr extension

[#6790](https://github.com/apache/camel-quarkus/issues/6790)

Camel-observability-services extension

[#6690](https://github.com/apache/camel-quarkus/issues/6690)

Google-secret-manager: less important test coverage

[#6669](https://github.com/apache/camel-quarkus/issues/6669)

Remove OpenTelemetry thread factory service overrides

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).