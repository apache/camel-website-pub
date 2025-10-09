# Apache camel-quarkus 3.32.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.32.0-src.zip](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-src.zip.sha512) |
| [apache-camel-quarkus-3.32.0-sbom.xml](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.32.0-sbom.json](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/camel-quarkus/3.32.0/apache-camel-quarkus-3.32.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.32.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.32.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#8308](https://github.com/apache/camel-quarkus/issues/8308)

Devise a way of keep example project Dockerfiles updated

[#8306](https://github.com/apache/camel-quarkus/issues/8306)

quarkus.scheduler.use-composite-scheduler=true + camel-quarkus-quartz causes startup failure

[#8297](https://github.com/apache/camel-quarkus/issues/8297)

cxf-soap - remove quarkus-cxf-rt-ws-security from the tests

[#8274](https://github.com/apache/camel-quarkus/issues/8274)

Google-secretmanager native profile & tests are disabled

[#8250](https://github.com/apache/camel-quarkus/issues/8250)

Support opentelemetry2 traceHeadersInclusion tracer option

[#8245](https://github.com/apache/camel-quarkus/issues/8245)

\[quarkus-main\] Extended ReflectiveHierarchyStep breaks netty-http integration test native compilation

[#8239](https://github.com/apache/camel-quarkus/issues/8239)

MongoDB client healthcheck fails when using Debezium MongoDB

[#8229](https://github.com/apache/camel-quarkus/issues/8229)

Metric bug using Rest DSL with contract-first

[#8219](https://github.com/apache/camel-quarkus/issues/8219)

Remove override of strimzi kafka container in dev service

[#8203](https://github.com/apache/camel-quarkus/issues/8203)

Add OpenAI extension

[#8200](https://github.com/apache/camel-quarkus/issues/8200)

Upgrade to LocalStack 4.13

[#8193](https://github.com/apache/camel-quarkus/issues/8193)

Introduce Semeru JDK CE testing as weekly job

[#8188](https://github.com/apache/camel-quarkus/issues/8188)

Remove cassandra-quarkus cq-maven-plugin BOM configuration for lz4-java

[#8163](https://github.com/apache/camel-quarkus/issues/8163)

Use Grafana OTel-LGTM Dev Service in observability example

[#8148](https://github.com/apache/camel-quarkus/issues/8148)

cxf-soap-grouped integration test native application fails to build due to NCDFE com.codahale.metrics.jmx.ObjectNameFactory

[#8126](https://github.com/apache/camel-quarkus/issues/8126)

Add infinispan-cluster-service extension

[#8122](https://github.com/apache/camel-quarkus/issues/8122)

\[JDK25\] Groovy native application fails to start due to Unsupported method java.lang.invoke.MethodHandleNatives.setCallSiteTargetNormal

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).