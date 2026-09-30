# Apache camel-quarkus 3.40.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.40.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-src.zip.sha512) |
| [apache-camel-quarkus-3.40.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.40.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.40.0/apache-camel-quarkus-3.40.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.40.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.40.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#9227](https://github.com/apache/camel-quarkus/issues/9227)

\[ftp, mina-sftp\] SFTP test resources crash in FIPS mode preventing FIPS-compatible tests from running

[#9225](https://github.com/apache/camel-quarkus/issues/9225)

langchain4j-embeddingstore: RAG augmentor auto-detection ignores synthetic EmbeddingStore/EmbeddingModel beans

[#9222](https://github.com/apache/camel-quarkus/issues/9222)

MySQL Testcontainers readiness check fails on FIPS (quartz-clustered, Debezium MySQL)

[#9218](https://github.com/apache/camel-quarkus/issues/9218)

Weaviate tests should fall back to the mock backend when the real API is not configured

[#9216](https://github.com/apache/camel-quarkus/issues/9216)

Add micrometer-observability traceCustomIdOnly configuration option

[#9213](https://github.com/apache/camel-quarkus/issues/9213)

Add opentelemetry2 traceCustomIdOnly configuration option

[#9200](https://github.com/apache/camel-quarkus/issues/9200)

\[camel-main\] SedaVirtualThreadsIT fails in native mode: CI-built Camel lacks the Java 21 multi-release classes

[#9195](https://github.com/apache/camel-quarkus/issues/9195)

openapi-java: native image logs WARN/ERROR from swagger ModelResolver and renders @JsonValue types as objects

[#9162](https://github.com/apache/camel-quarkus/issues/9162)

langchain4j-ingest: default the document id header to CamelLangChain4jIngestDocumentId

[#9153](https://github.com/apache/camel-quarkus/issues/9153)

Native build fails when the kamelet DelegatingSchemaResolver becomes reachable without camel-jackson

[#9144](https://github.com/apache/camel-quarkus/issues/9144)

langchain4j-ingest: write segment metadata as camel\_ingest\_\* ahead of the component delegation

[#9124](https://github.com/apache/camel-quarkus/issues/9124)

Add a dedicated support extension for Quarkus LangChain4j build time integration

[#9115](https://github.com/apache/camel-quarkus/issues/9115)

Apply Camel JAXP external access restrictions to the Xalan TransformerFactory

[#9113](https://github.com/apache/camel-quarkus/issues/9113)

tls-registry: quarkus.tls protocols and cipher suites are not applied to SSLContextParameters

[#9106](https://github.com/apache/camel-quarkus/issues/9106)

Document origin restrictions for vertx-websocket consumers

[#9104](https://github.com/apache/camel-quarkus/issues/9104)

quarkus.camel.native.reflection.serialization-enabled has no effect when set to false

[#9094](https://github.com/apache/camel-quarkus/issues/9094)

Weaviate: native compilation fails

[#9061](https://github.com/apache/camel-quarkus/issues/9061)

Release staging script publishes checksums for unverified downloads

[#9060](https://github.com/apache/camel-quarkus/issues/9060)

Maven wrapper distribution is not checksum-pinned

[#9059](https://github.com/apache/camel-quarkus/issues/9059)

Cron workflows declare no permissions block

[#9058](https://github.com/apache/camel-quarkus/issues/9058)

diagram dev route: narrow console selection, allowlist options, encode HTML output

[#9057](https://github.com/apache/camel-quarkus/issues/9057)

console: exposure-mode=ALL exposes the dev console in production

[#9056](https://github.com/apache/camel-quarkus/issues/9056)

JTA transaction policy swallows rollback and resume failures

[#9055](https://github.com/apache/camel-quarkus/issues/9055)

Servlet multipart configuration is always applied; the null check is dead

[#9054](https://github.com/apache/camel-quarkus/issues/9054)

LDAP securityAuthentication default contradicts its javadoc

[#9051](https://github.com/apache/camel-quarkus/issues/9051)

Debug enablement gates test for property presence, not value

[#9048](https://github.com/apache/camel-quarkus/issues/9048)

Oracle and DB2 jdbc-grouped tests in Quarkus Platform fails

[#9039](https://github.com/apache/camel-quarkus/issues/9039)

langchain4j-ingest: configurable idempotent repository for ingestion pipelines

[#8912](https://github.com/apache/camel-quarkus/issues/8912)

Restore aws-bedrock & aws2-athena extensions in integration-tests-aws2 module

[#8865](https://github.com/apache/camel-quarkus/issues/8865)

Add langchain4j-embeddingstore-ql4j integration test module

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).