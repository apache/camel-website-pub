# Apache camel-quarkus 3.39.0 Release

## New and Noteworthy

## Supported Java version

This version supports Java 17 and 21.

## Apache Camel Quarkus

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-quarkus-3.39.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-src.zip.sha512) |
| [apache-camel-quarkus-3.39.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.xml.sha512) |
| [apache-camel-quarkus-3.39.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/camel-quarkus/3.39.0/apache-camel-quarkus-3.39.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `3.39.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel-quarkus.git
cd camel-quarkus
git checkout 3.39.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

[#9015](https://github.com/apache/camel-quarkus/issues/9015)

Add a langchain4j-ingest extension: declarative document ingestion into an embedding store

[#9013](https://github.com/apache/camel-quarkus/issues/9013)

Harden the RAG augmentor bridge: designated default resolution and retrieval filter hook

[#9010](https://github.com/apache/camel-quarkus/issues/9010)

Native build fails: camel-quarkus-support-aws2 ChecksumProviderSubstitutions conflicts with quarkus-amazon-common CrtSubstitutions

[#9002](https://github.com/apache/camel-quarkus/issues/9002)

Build/test fail on camel-quarkus app for quarkus-minio (client) version since 3.9.0

[#8993](https://github.com/apache/camel-quarkus/issues/8993)

CamelAiToolProvider attaches every registered ai-tool to Camel langchain4j-agent endpoints

[#8992](https://github.com/apache/camel-quarkus/issues/8992)

langchain4j-agent-ql4j integration tests are failing

[#8979](https://github.com/apache/camel-quarkus/issues/8979)

Make Quarkus LangChain4j named embedding stores usable from Camel routes

[#8966](https://github.com/apache/camel-quarkus/issues/8966)

Auto-produce RetrievalAugmentor bridging Camel ingestion with @RegisterAiService RAG

[#8949](https://github.com/apache/camel-quarkus/issues/8949)

camel-quarkus-mcp-server - expose ai-tool routes as MCP tools via quarkus-mcp-server

[#8932](https://github.com/apache/camel-quarkus/issues/8932)

Move AI Agents OSS Helper CEQ rules to the project

[#8928](https://github.com/apache/camel-quarkus/issues/8928)

Thousands of warning in build like \`\[io.quarkus.arc.processor.Methods\] JDK class java.util.concurrent.atomic.AtomicInteger with final method XXX\`\`

[#8921](https://github.com/apache/camel-quarkus/issues/8921)

Add support of ai-tool introduced by CAMEL-23382

[#8920](https://github.com/apache/camel-quarkus/issues/8920)

\[camel-main\] Enable minio tests/native once Quarkus bumps Minio to 9.0.3

[#8914](https://github.com/apache/camel-quarkus/issues/8914)

Enable langchain4j-agent tests with extension for ai-tool

[#8899](https://github.com/apache/camel-quarkus/issues/8899)

Intermittent failure of master-infinispan InfinispanClusterServiceTest.testFailover

[#8885](https://github.com/apache/camel-quarkus/issues/8885)

Support component camel-micrometer-observability

[#8880](https://github.com/apache/camel-quarkus/issues/8880)

data-extract-langchain4j example fails after Agent.chat() return type change

[#8878](https://github.com/apache/camel-quarkus/issues/8878)

Add integration test coverage for new weaviate operations (BATCH\_CREATE, HYBRID\_QUERY, BM25\_QUERY, AGGREGATE)

[#8871](https://github.com/apache/camel-quarkus/issues/8871)

Support BacklogTracer activityEnabled and activitySize options

[#8858](https://github.com/apache/camel-quarkus/issues/8858)

Add test coverage for recent openai component enhancements

[#8857](https://github.com/apache/camel-quarkus/issues/8857)

Add test coverage for recent langchain4j-agent component enhancements

[#8855](https://github.com/apache/camel-quarkus/issues/8855)

\[camel-main\]\[quarkus-main\] enable native tests for langchain4j-agent-ql4j

[#8854](https://github.com/apache/camel-quarkus/issues/8854)

\[camel-main\] Refactor weaviate client in integration-tests/weaviiate to reflect upgrade from v5 to v6

[#8848](https://github.com/apache/camel-quarkus/issues/8848)

\[camel-main\] Revert synchronization of quarkus-langchain4j in the main pom

[#8845](https://github.com/apache/camel-quarkus/issues/8845)

Upgarde com.ibm.mq.jakarta.client to 10.x

[#8825](https://github.com/apache/camel-quarkus/issues/8825)

Implement RuntimePropertiesProvider for Quarkus to show app properties in dev console

[#8768](https://github.com/apache/camel-quarkus/issues/8768)

Expose Camel routes as quarkus-langchain4j tools

[#8752](https://github.com/apache/camel-quarkus/issues/8752)

smallrye-reactive-messaging native compilation fails due to unresolved method DefaultExchange.getExchangeExtension()

[#7651](https://github.com/apache/camel-quarkus/issues/7651)

Remove CamelQuarkusDataFormatConfigLifecycleStrategy

[#4472](https://github.com/apache/camel-quarkus/issues/4472)

Support \`<xsl:include>\` in native mode

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).