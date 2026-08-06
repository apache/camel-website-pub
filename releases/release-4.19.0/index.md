# Apache camel 4.19.0 Release

## New and Noteworthy

This release is the new Camel 4.19.0 release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.19.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-core</artifactId>
  </dependency>
  <dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-COMPONENT</artifactId>
  </dependency>
</dependencies>
```

To use this release in a Spring Boot application, use Spring Boot `spring-boot-dependencies` and Camel `camel-spring-boot-bom` Bill of Materials (BOM):

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version> SPRING BOOT VERSION HERE </version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.camel.springboot</groupId>
      <artifactId>camel-spring-boot-bom</artifactId>
      <version>4.19.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-COMPONENT-starter</artifactId>
  </dependency>
</dependencies>
```

## Apache Camel

| Download | Signature and checksum |
| --- | --- |
| [apache-camel-4.19.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-src.zip.sha512) |
| [apache-camel-4.19.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.xml.sha512) |
| [apache-camel-4.19.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.19.0/apache-camel-4.19.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.19.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.19.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (67)

[CAMEL-23310](https://issues.apache.org/jira/browse/CAMEL-23310)

camel-core - Suspend/resume on CamelContext should reset prepare shutdown flag

[CAMEL-23307](https://issues.apache.org/jira/browse/CAMEL-23307)

Infinispan schema registration retry does not catch HotRodClientException wrapping IllegalLifecycleStateException

[CAMEL-23306](https://issues.apache.org/jira/browse/CAMEL-23306)

SpringSamplingThrottlerTest.testSamplingWithPropertyPlaceholder always fails - missing route in Spring XML config

[CAMEL-23303](https://issues.apache.org/jira/browse/CAMEL-23303)

Fix JBang metadata generation to detect all commands and resolve completion candidates

[CAMEL-23299](https://issues.apache.org/jira/browse/CAMEL-23299)

Aggregated exchange does not preserve the transacted flag from the original exchange

[CAMEL-23295](https://issues.apache.org/jira/browse/CAMEL-23295)

Fix resource leak and improve error handling in camel-splunk-hec producer

[CAMEL-23294](https://issues.apache.org/jira/browse/CAMEL-23294)

\[camel-sql\] JDBC-based Idempotent repository strategy fails in racing conditions.

[CAMEL-23288](https://issues.apache.org/jira/browse/CAMEL-23288)

JBang - Issues with kubernetes plugin when exporting with a selected runtime

[CAMEL-23284](https://issues.apache.org/jira/browse/CAMEL-23284)

Pipe YAML Kamelet properties with {{placeholder}} get URL-encoded, preventing property resolution

[CAMEL-23282](https://issues.apache.org/jira/browse/CAMEL-23282)

Simple OGNL ${body.xxx} causes unbounded BeanInfo cache growth for ephemeral message bodies

[CAMEL-23281](https://issues.apache.org/jira/browse/CAMEL-23281)

\[camel-core\] split/aggregator stuck in tx

[CAMEL-23279](https://issues.apache.org/jira/browse/CAMEL-23279)

SamplingDefinition.description() fails with NumberFormatException when samplePeriod uses property placeholders

[CAMEL-23272](https://issues.apache.org/jira/browse/CAMEL-23272)

\`--management-port\` is overriding \`restConfiguration > port\`

[CAMEL-23267](https://issues.apache.org/jira/browse/CAMEL-23267)

File consumer does not release items in SimpleLRUCache

[CAMEL-23260](https://issues.apache.org/jira/browse/CAMEL-23260)

ServiceBusComponent: RejectedExecutionException during graceful shutdown after successful exchange completion

[CAMEL-23249](https://issues.apache.org/jira/browse/CAMEL-23249)

CXF RS Rest service loses content-type with stream caching enabled

[CAMEL-23235](https://issues.apache.org/jira/browse/CAMEL-23235)

camel-jbang - Propagate --java-version option to jbang run/debug commands

[CAMEL-23234](https://issues.apache.org/jira/browse/CAMEL-23234)

camel transacted committing on rollback

[CAMEL-23230](https://issues.apache.org/jira/browse/CAMEL-23230)

camel-jbang: Camel Main does not exit with RabbitMQ and durationMaxIdleSeconds

[CAMEL-23213](https://issues.apache.org/jira/browse/CAMEL-23213)

ExportTest fails on JDK 17 after camel-spring-boot moved to Spring Boot 4 (JDK 21)

[CAMEL-23208](https://issues.apache.org/jira/browse/CAMEL-23208)

camel-jbang: not possible to change minimal java version during RUN

[CAMEL-23194](https://issues.apache.org/jira/browse/CAMEL-23194)

Deadlock can happen when JMS service is shutdown

[CAMEL-23193](https://issues.apache.org/jira/browse/CAMEL-23193)

JmsMessage does not copy attachments to new instance

[CAMEL-23192](https://issues.apache.org/jira/browse/CAMEL-23192)

jbang export to quarkus generates wrong dockerfiles

[CAMEL-23191](https://issues.apache.org/jira/browse/CAMEL-23191)

Path parameters incorrectly extracted when server.servlet.context-path is configured

[CAMEL-23190](https://issues.apache.org/jira/browse/CAMEL-23190)

\[camel-jbang-mcp\] DefaultCamelCatalog.getCatalogVersion() ignores VersionManager and returns compiled-in version

[CAMEL-23186](https://issues.apache.org/jira/browse/CAMEL-23186)

\[camel-jbang-mcp\] CatalogLoader.loadCatalog() fails with NoClassDefFoundError for versioned catalogs

[CAMEL-23183](https://issues.apache.org/jira/browse/CAMEL-23183)

\[camel-jbang-mcp\] ClassNotFoundException: org.apache.camel.catalog.impl.AbstractCamelCatalog

[CAMEL-23174](https://issues.apache.org/jira/browse/CAMEL-23174)

Kamelet: transformer in aws-ddb-sink is not executed

[CAMEL-23123](https://issues.apache.org/jira/browse/CAMEL-23123)

S3Presigner does not honor forcePathStyle configuration in createDownloadLink/createUploadLink operations

[CAMEL-23122](https://issues.apache.org/jira/browse/CAMEL-23122)

camel-core - DefaultErrorHandler with logExhausted(false) still logs

[CAMEL-23116](https://issues.apache.org/jira/browse/CAMEL-23116)

CamelContext is never stopped when using @TestInstance(Lifecycle.PER\_CLASS) with CamelTestSupport

[CAMEL-23115](https://issues.apache.org/jira/browse/CAMEL-23115)

camel-openapi-java - base.path option will never survive if context-path is set

[CAMEL-23106](https://issues.apache.org/jira/browse/CAMEL-23106)

camel-docling - Remove temp file in DoclingProducer.getInputPath()

[CAMEL-23105](https://issues.apache.org/jira/browse/CAMEL-23105)

camel-docling - Fix broken async conversion workflow (discarded result and error masking)

[CAMEL-23101](https://issues.apache.org/jira/browse/CAMEL-23101)

camel-minio error writing to object store

[CAMEL-23083](https://issues.apache.org/jira/browse/CAMEL-23083)

Camel geocoder no more working on Nominatim due to missing user-agent

[CAMEL-23072](https://issues.apache.org/jira/browse/CAMEL-23072)

camel-as2 - Receiving messages: AS2 server endpoint does not support Expect: 100-continue — causes 3-second delay on every inbound message

[CAMEL-23070](https://issues.apache.org/jira/browse/CAMEL-23070)

camel-as2 - AS2AsyncMDNServerConnection uses strict RequestValidateHost — async MDNs rejected with HTTP 421

[CAMEL-23068](https://issues.apache.org/jira/browse/CAMEL-23068)

camel-as2 - Signed MDN signature verification fails at receiving partner — CRLF/LF mismatch in TextPlainEntity.writeTo() (regression from CAMEL-22037)

[CAMEL-23067](https://issues.apache.org/jira/browse/CAMEL-23067)

camel-as2 - Async MDN signature verification fails — receipt API modifies raw body bytes before signature validation

[CAMEL-23066](https://issues.apache.org/jira/browse/CAMEL-23066)

camel-as2 - AS2Utils.createMessageId() produces duplicate Message-IDs after JVM restart (nanoTime-based)

[CAMEL-23065](https://issues.apache.org/jira/browse/CAMEL-23065)

camel-as2 - MicUtils.createReceivedContentMic() computes wrong MIC for compressed messages (RFC 5402 violation)

[CAMEL-23064](https://issues.apache.org/jira/browse/CAMEL-23064)

camel-as2 - HttpMessageUtils.extractEdiPayload() rejects valid AS2 messages with non-standard content types (text/plain, application/octet-stream, etc.)

[CAMEL-23062](https://issues.apache.org/jira/browse/CAMEL-23062)

camel-openai: encodingFormat option does not take effect

[CAMEL-23061](https://issues.apache.org/jira/browse/CAMEL-23061)

camel-sql - SqlConsumer NPE if using exchange factory statistics

[CAMEL-23051](https://issues.apache.org/jira/browse/CAMEL-23051)

camel-yaml-dsl-validator - Tooling for offline validate should support property placeholders

[CAMEL-23036](https://issues.apache.org/jira/browse/CAMEL-23036)

camel-core - NPE when pooled exchange in split at UoW done

[CAMEL-23035](https://issues.apache.org/jira/browse/CAMEL-23035)

camel-core - Simple language using colon or question mark can conflict with ternary operator

[CAMEL-23033](https://issues.apache.org/jira/browse/CAMEL-23033)

camel-yaml-dsl - Setting routePolicy on route should be routePolicyRef

[CAMEL-23032](https://issues.apache.org/jira/browse/CAMEL-23032)

camel-nats consumer sends ACK regardless of the Exchange processing/delivery result

[CAMEL-23031](https://issues.apache.org/jira/browse/CAMEL-23031)

Regression from CAMEL-22354 in camel-csv

[CAMEL-23030](https://issues.apache.org/jira/browse/CAMEL-23030)

Streaming splitter with aggregation using synchronous executor results in StackOverflowError

[CAMEL-23028](https://issues.apache.org/jira/browse/CAMEL-23028)

camel-jbang - Transform route with transacted does not include following steps

[CAMEL-23024](https://issues.apache.org/jira/browse/CAMEL-23024)

camel-jbang - Route dumper for YAML with setHeaders / setVariables EIP

[CAMEL-23023](https://issues.apache.org/jira/browse/CAMEL-23023)

camel-kafka - Kafka consumers are started to eager before CamelContext is fully started

[CAMEL-23018](https://issues.apache.org/jira/browse/CAMEL-23018)

camel-rest-openapi - Response operation with content-type by no schema causes NPE

[CAMEL-23016](https://issues.apache.org/jira/browse/CAMEL-23016)

camel-mcp - camel\_version\_list - wrong quarkus version

[CAMEL-23015](https://issues.apache.org/jira/browse/CAMEL-23015)

camel-jbang - YAML DSL dump of route with Saga EIP does not dump completion/compensation correctly

[CAMEL-23012](https://issues.apache.org/jira/browse/CAMEL-23012)

camel-jbang - Resequence EIP route dump to YAML is wrong for batch config

[CAMEL-23011](https://issues.apache.org/jira/browse/CAMEL-23011)

camel-mcp - camel\_catalog\_components returns Internal Server Error

[CAMEL-23002](https://issues.apache.org/jira/browse/CAMEL-23002)

camel plugin add xyz - should ignore the gav in the camel-jbang-user.properties

[CAMEL-22992](https://issues.apache.org/jira/browse/CAMEL-22992)

camel-jbang - Unable to use camel test plugin on a Windows

[CAMEL-22941](https://issues.apache.org/jira/browse/CAMEL-22941)

"POST\_Exchange\_\_\_\_Id\_\_" metrics

[CAMEL-22672](https://issues.apache.org/jira/browse/CAMEL-22672)

\[camel-observation\] observations and metrics

[CAMEL-22090](https://issues.apache.org/jira/browse/CAMEL-22090)

couchbase - consumer does not work if jackson is on classpath

[CAMEL-21932](https://issues.apache.org/jira/browse/CAMEL-21932)

Kubernetes Secrets and Config maps context reloading doesn't work together

### Dependency upgrade (9)

[CAMEL-23292](https://issues.apache.org/jira/browse/CAMEL-23292)

Upgrade dependency json-schema-validator to 2.x

[CAMEL-23177](https://issues.apache.org/jira/browse/CAMEL-23177)

undertow and cxf as misaligned

[CAMEL-23161](https://issues.apache.org/jira/browse/CAMEL-23161)

Upgrade to OpenTelemtry 1.60+

[CAMEL-23156](https://issues.apache.org/jira/browse/CAMEL-23156)

Upgrade to protobuf 4.x

[CAMEL-23144](https://issues.apache.org/jira/browse/CAMEL-23144)

Upgrade quickfixj to 3.x

[CAMEL-23019](https://issues.apache.org/jira/browse/CAMEL-23019)

camel-cxf - Upgrade to CXF 4.2.x

[CAMEL-22572](https://issues.apache.org/jira/browse/CAMEL-22572)

camel-netty - Upgrade to 4.2.x

[CAMEL-22369](https://issues.apache.org/jira/browse/CAMEL-22369)

camel-groovy - Upgrade to groovy 5

[CAMEL-22213](https://issues.apache.org/jira/browse/CAMEL-22213)

camel-kafka - Upgrade to Kafka 4

### Improvement (94)

[CAMEL-23308](https://issues.apache.org/jira/browse/CAMEL-23308)

camel-mail - Using a custom JavaMailSender should still be default configured

[CAMEL-23300](https://issues.apache.org/jira/browse/CAMEL-23300)

camel-couchbase: add connectionString option to support dynamic KV port mapping

[CAMEL-23297](https://issues.apache.org/jira/browse/CAMEL-23297)

Improve error handling and add input validation in camel-netty converters

[CAMEL-23289](https://issues.apache.org/jira/browse/CAMEL-23289)

camel-drill - Fix empty catch blocks and resource leaks in DrillProducer

[CAMEL-23287](https://issues.apache.org/jira/browse/CAMEL-23287)

Camel-Jbang-mcp: Unify MCP tool return types to use typed records instead of raw JSON strings

[CAMEL-23285](https://issues.apache.org/jira/browse/CAMEL-23285)

Embedded test services (Hazelcast, Ignite, FTP) unnecessarily require Docker

[CAMEL-23280](https://issues.apache.org/jira/browse/CAMEL-23280)

camel-openai SSL improvements

[CAMEL-23277](https://issues.apache.org/jira/browse/CAMEL-23277)

camel-jsch: Add OpenSSH certificate support to jsch based components

[CAMEL-23273](https://issues.apache.org/jira/browse/CAMEL-23273)

Camel-Jbang-mcp: Warn about sensitive data in POM content passed to migration tools

[CAMEL-23270](https://issues.apache.org/jira/browse/CAMEL-23270)

Camel-Jbang-MCP: Add MCP tool annotations (readOnlyHint, destructiveHint, openWorldHint) to all tools

[CAMEL-23263](https://issues.apache.org/jira/browse/CAMEL-23263)

Camel-Netty: Make SSL fallback path PQC-capable with TLSv1.3 and named groups auto-configuration

[CAMEL-23259](https://issues.apache.org/jira/browse/CAMEL-23259)

Camel-netty: Close channel on SSL/TLS handshake failure

[CAMEL-23256](https://issues.apache.org/jira/browse/CAMEL-23256)

Camel-IBM-Watsonx: New component for IBM watsonx.data lakehouse integration

[CAMEL-23255](https://issues.apache.org/jira/browse/CAMEL-23255)

Infinispan Remote component should retry schema registration on IllegalLifecycleStateException

[CAMEL-23254](https://issues.apache.org/jira/browse/CAMEL-23254)

Add Milvus helper beans for YAML DSL usage

[CAMEL-23248](https://issues.apache.org/jira/browse/CAMEL-23248)

Camel-PQC: Add stateful key usage tracking and warnings for XMSS/LMS

[CAMEL-23243](https://issues.apache.org/jira/browse/CAMEL-23243)

Enhance the OpenAI operation property

[CAMEL-23237](https://issues.apache.org/jira/browse/CAMEL-23237)

camel-jbang: Adapt CLI table output to terminal width

[CAMEL-23232](https://issues.apache.org/jira/browse/CAMEL-23232)

Camel-Azure components: Standardize CredentialType enums across all Azure components

[CAMEL-23229](https://issues.apache.org/jira/browse/CAMEL-23229)

Camel-AWS2-DDB: Add PartiQL, transactional, and batch write operations

[CAMEL-23227](https://issues.apache.org/jira/browse/CAMEL-23227)

Enhance camel-datasonnet with utility functions and standard library

[CAMEL-23224](https://issues.apache.org/jira/browse/CAMEL-23224)

camel-mail - MailHeaderFilterStrategy should also filter inbound headers

[CAMEL-23222](https://issues.apache.org/jira/browse/CAMEL-23222)

camel-coap: Integrate HeaderFilterStrategy for CoAP query parameter to header mapping

[CAMEL-23214](https://issues.apache.org/jira/browse/CAMEL-23214)

Migrate AvailablePortFinder.getNextAvailable() to @RegisterExtension for proper port lifecycle

[CAMEL-23212](https://issues.apache.org/jira/browse/CAMEL-23212)

Camel-Docling: Harden CLI argument injection validation in camel-docling

[CAMEL-23211](https://issues.apache.org/jira/browse/CAMEL-23211)

Camel-Docling: Use secure temp file creation in camel-docling

[CAMEL-23204](https://issues.apache.org/jira/browse/CAMEL-23204)

Camel-PQC: Enforce key status checks before cryptographic operations in PQCProducer

[CAMEL-23203](https://issues.apache.org/jira/browse/CAMEL-23203)

Camel-PQC: Add algorithm metadata to hybrid wire formats

[CAMEL-23197](https://issues.apache.org/jira/browse/CAMEL-23197)

\[camel-jbang-mcp\] Extract shared CatalogService with caching and add version parameters to all catalog tools

[CAMEL-23188](https://issues.apache.org/jira/browse/CAMEL-23188)

Core: Auto-configure PQC TLS named groups when JVM supports X25519MLKEM768

[CAMEL-23185](https://issues.apache.org/jira/browse/CAMEL-23185)

Post-Quantum Cryptography (PQC) readiness: camel-as2: Upgrade test RSA keys from 1024-bit to 2048-bit

[CAMEL-23184](https://issues.apache.org/jira/browse/CAMEL-23184)

Deprecate Camel-Splunk component

[CAMEL-23182](https://issues.apache.org/jira/browse/CAMEL-23182)

Post-Quantum Cryptography (PQC) readiness: camel-mongodb: Add SSLContextParameters support and fix hardcoded TLS version

[CAMEL-23178](https://issues.apache.org/jira/browse/CAMEL-23178)

\[camel-jbang-mcp\] Allow configuring additional Maven repositories for catalog resolution

[CAMEL-23170](https://issues.apache.org/jira/browse/CAMEL-23170)

camel-core - Add simple jsonpath to Camels JsonObject

[CAMEL-23169](https://issues.apache.org/jira/browse/CAMEL-23169)

camel-jbang - Export to camel main as fat-jar should can cause overrides in META-INF services files that camel-jq needs

[CAMEL-23168](https://issues.apache.org/jira/browse/CAMEL-23168)

Camel-Jbang-mcp: Make MCP exception catalog resource doc links version-aware

[CAMEL-23167](https://issues.apache.org/jira/browse/CAMEL-23167)

Camel-jbang-mcp - Extract static reference data from tools into MCP Resources

[CAMEL-23160](https://issues.apache.org/jira/browse/CAMEL-23160)

camel-core - Add type converter for camel-util-json

[CAMEL-23150](https://issues.apache.org/jira/browse/CAMEL-23150)

camel-jbang - Be able to install and run camel-launcher as maven wrapper like

[CAMEL-23149](https://issues.apache.org/jira/browse/CAMEL-23149)

camel-iggy - Add option to configure TLS

[CAMEL-23147](https://issues.apache.org/jira/browse/CAMEL-23147)

camel-launcher - Embed citrus test plugin

[CAMEL-23130](https://issues.apache.org/jira/browse/CAMEL-23130)

camel-seda - SedaConsumer should have timeout for graceful shutdown if using concurrentConsumers

[CAMEL-23127](https://issues.apache.org/jira/browse/CAMEL-23127)

camel-jbang - Route transform to YAML with inlined errorHandler is empty

[CAMEL-23126](https://issues.apache.org/jira/browse/CAMEL-23126)

Camel-jbang-mcp: Add MCP Prompts for structured multi-step workflows to camel-jbang-mcp

[CAMEL-23119](https://issues.apache.org/jira/browse/CAMEL-23119)

camel-launcher - Add validate plugin

[CAMEL-23114](https://issues.apache.org/jira/browse/CAMEL-23114)

camel-jbang - camel version list - Add --vendor flag

[CAMEL-23112](https://issues.apache.org/jira/browse/CAMEL-23112)

Review Support for JDK 17

[CAMEL-23111](https://issues.apache.org/jira/browse/CAMEL-23111)

camel-jbang - camel run - YAML parsing errors not published to OTEL

[CAMEL-23110](https://issues.apache.org/jira/browse/CAMEL-23110)

camel-http: deprecate NTLM as authentication method

[CAMEL-23107](https://issues.apache.org/jira/browse/CAMEL-23107)

camel-docling - Add CLI command validation in buildDoclingCommand

[CAMEL-23102](https://issues.apache.org/jira/browse/CAMEL-23102)

camel-jbang - Automatic keep up to date list of Camel FactoryFinder as known dependencies

[CAMEL-23098](https://issues.apache.org/jira/browse/CAMEL-23098)

Camel-PQC: Wire KeyLifecycleManager into PQC producer to enable key lifecycle operations

[CAMEL-23094](https://issues.apache.org/jira/browse/CAMEL-23094)

camel-core - Saga EIP fix model for completion and compensation

[CAMEL-23085](https://issues.apache.org/jira/browse/CAMEL-23085)

camel-nats - Make more options configurable on component level

[CAMEL-23084](https://issues.apache.org/jira/browse/CAMEL-23084)

camel-jbang - camel infra log - May log duplicate

[CAMEL-23082](https://issues.apache.org/jira/browse/CAMEL-23082)

camel-as2 - Replace deprecated api

[CAMEL-23081](https://issues.apache.org/jira/browse/CAMEL-23081)

camel-milo - Allow overriding the server reported endpoint port

[CAMEL-23077](https://issues.apache.org/jira/browse/CAMEL-23077)

Camel-OCSF: Add missing class UID constants and fix generation script

[CAMEL-23074](https://issues.apache.org/jira/browse/CAMEL-23074)

camel-langchain4j-tools - Handle required Tool parameters and enums

[CAMEL-23073](https://issues.apache.org/jira/browse/CAMEL-23073)

camel-jbang - Transform route should stub properties functions

[CAMEL-23071](https://issues.apache.org/jira/browse/CAMEL-23071)

camel-as2 - Sending messages: AS2 client should provide endpoint parameter to optionally enable Expect: 100-continue

[CAMEL-23060](https://issues.apache.org/jira/browse/CAMEL-23060)

camel-docling - Expose docling serve chunking mechanism

[CAMEL-23059](https://issues.apache.org/jira/browse/CAMEL-23059)

camel-git - Add depth option to provide shallow clone

[CAMEL-23053](https://issues.apache.org/jira/browse/CAMEL-23053)

camel-core - Add toJson functions to simple

[CAMEL-23052](https://issues.apache.org/jira/browse/CAMEL-23052)

camel-http-base - typeconverter should be used when providing a HTTP query header

[CAMEL-23049](https://issues.apache.org/jira/browse/CAMEL-23049)

Add getLastError to ManagedRouteGroupMBean API

[CAMEL-23048](https://issues.apache.org/jira/browse/CAMEL-23048)

camel-core - Simple init block to require using semi colon to end each variable

[CAMEL-23047](https://issues.apache.org/jira/browse/CAMEL-23047)

camel-core - Add val function to simple

[CAMEL-23046](https://issues.apache.org/jira/browse/CAMEL-23046)

camel-mail - Auto start IdempotentRepository

[CAMEL-23034](https://issues.apache.org/jira/browse/CAMEL-23034)

Generalize Google services authentication with common module

[CAMEL-23029](https://issues.apache.org/jira/browse/CAMEL-23029)

Camel-Consul: Add ObjectInputFilter String pattern parameter in ConsulRegistry to be used in deserialize operations

[CAMEL-23025](https://issues.apache.org/jira/browse/CAMEL-23025)

camel-core - Tokenizer language should work with \\n out of the box in XML and YAML DSL

[CAMEL-23022](https://issues.apache.org/jira/browse/CAMEL-23022)

Camel MCP - Add migration/upgrade tools

[CAMEL-23017](https://issues.apache.org/jira/browse/CAMEL-23017)

camel-core - WireTap EIP should not have pattern option

[CAMEL-23014](https://issues.apache.org/jira/browse/CAMEL-23014)

camel-core - YAML DSL to respect @XmlType(propOrder ...

[CAMEL-23013](https://issues.apache.org/jira/browse/CAMEL-23013)

Enhance the OpenAPI component's description

[CAMEL-23008](https://issues.apache.org/jira/browse/CAMEL-23008)

camel-jbang - Transform route that refers to beans via #class should be possible

[CAMEL-23007](https://issues.apache.org/jira/browse/CAMEL-23007)

camel-jbang - Add a support JAR for neutral common code that can be reused by other tooling

[CAMEL-23006](https://issues.apache.org/jira/browse/CAMEL-23006)

camel-jbang - Transform route with Kamelet EIP should stub

[CAMEL-23005](https://issues.apache.org/jira/browse/CAMEL-23005)

camel-core - Failover Loadbalancer should mark stick and round robin as boolean types

[CAMEL-23004](https://issues.apache.org/jira/browse/CAMEL-23004)

camel-jbang - Transform route should better support Java DSL with inlined expressions

[CAMEL-23003](https://issues.apache.org/jira/browse/CAMEL-23003)

camel-test-infra - Align Jackson JARs for testcontainers

[CAMEL-23001](https://issues.apache.org/jira/browse/CAMEL-23001)

camel-groovy - Add groovy-json as dependency

[CAMEL-23000](https://issues.apache.org/jira/browse/CAMEL-23000)

camel-ssh - idleTimeout

[CAMEL-22890](https://issues.apache.org/jira/browse/CAMEL-22890)

camel-jbang - include opentelemtry2 dependency if camel.opentelemetry2.enabled

[CAMEL-22884](https://issues.apache.org/jira/browse/CAMEL-22884)

Provide error at build time or runtime when a \`method\` attribute is used inside a when clause in xml dsl

[CAMEL-22801](https://issues.apache.org/jira/browse/CAMEL-22801)

camel-jbang - Remove gradle build tool

[CAMEL-22745](https://issues.apache.org/jira/browse/CAMEL-22745)

camel-yaml-dsl - Add transformer/validator to root

[CAMEL-22562](https://issues.apache.org/jira/browse/CAMEL-22562)

camel-graphql - Extend camel-http as base component

[CAMEL-22325](https://issues.apache.org/jira/browse/CAMEL-22325)

camel-jbang - Update description for infra containers

[CAMEL-21966](https://issues.apache.org/jira/browse/CAMEL-21966)

camel-jbang - Add small examples in the help text

[CAMEL-21913](https://issues.apache.org/jira/browse/CAMEL-21913)

camel-jbang - Make using JPA easier to use and export

[CAMEL-19329](https://issues.apache.org/jira/browse/CAMEL-19329)

Consider MiMa as alternative to pure maven-resolver

### New Feature (39)

[CAMEL-23276](https://issues.apache.org/jira/browse/CAMEL-23276)

Allow JBang plugins to customize Run command before CamelContext is built

[CAMEL-23269](https://issues.apache.org/jira/browse/CAMEL-23269)

Add new component camel-camunda for Camunda 8

[CAMEL-23258](https://issues.apache.org/jira/browse/CAMEL-23258)

camel-google-mail: Add DataTypeTransformer for Gmail Draft creation

[CAMEL-23252](https://issues.apache.org/jira/browse/CAMEL-23252)

Add onReload SPI method to ContextServicePlugin for dev-mode hot-reload hooks

[CAMEL-23251](https://issues.apache.org/jira/browse/CAMEL-23251)

Google mail Add DataTypeTransformer for Gmail ModifyMessageRequest to update labels

[CAMEL-23231](https://issues.apache.org/jira/browse/CAMEL-23231)

Camel-Google-common: Add Workload Identity Federation support for all Google components

[CAMEL-23228](https://issues.apache.org/jira/browse/CAMEL-23228)

Add DataWeave to DataSonnet transpiler in camel-jbang

[CAMEL-23219](https://issues.apache.org/jira/browse/CAMEL-23219)

google-mail-stream consumer expose threadId, Message-ID and labelIds as exchange headers

[CAMEL-23210](https://issues.apache.org/jira/browse/CAMEL-23210)

Camel-PQC: Add input validation for algorithm combinations and key sizes in PQCProducer

[CAMEL-23207](https://issues.apache.org/jira/browse/CAMEL-23207)

Camel-aws-eventbridge: Add EventBridge consumer implementation with SQS-backed polling

[CAMEL-23199](https://issues.apache.org/jira/browse/CAMEL-23199)

Camel-Spring-Boot: Create Google Speech-to-text and text-to-speech Starters

[CAMEL-23198](https://issues.apache.org/jira/browse/CAMEL-23198)

Camel-Google: Like AWS and IBM, create text-to-speech and speech-to-text components

[CAMEL-23173](https://issues.apache.org/jira/browse/CAMEL-23173)

camel-eventlistener component

[CAMEL-23162](https://issues.apache.org/jira/browse/CAMEL-23162)

Post-Quantum Cryptography (PQC) readiness: Add PQC readiness support to Camel Spring Boot SSL auto-configuration

[CAMEL-23159](https://issues.apache.org/jira/browse/CAMEL-23159)

Post-Quantum Cryptography (PQC) readiness: Add signatureSchemes support to BaseSSLContextParameters and SSLConfigurationProperties for PQC readiness

[CAMEL-23158](https://issues.apache.org/jira/browse/CAMEL-23158)

Post-Quantum Cryptography (PQC) readiness: Expose PQC named groups in SSLConfigurationProperties

[CAMEL-23155](https://issues.apache.org/jira/browse/CAMEL-23155)

Camel-Google: Add Google Cloud Vision AI starter for Spring Boot

[CAMEL-23154](https://issues.apache.org/jira/browse/CAMEL-23154)

Post-Quantum Cryptography (PQC) readiness: Add namedGroups support to BaseSSLContextParameters

[CAMEL-23153](https://issues.apache.org/jira/browse/CAMEL-23153)

Camel-Google: Add Google Cloud Vision AI component

[CAMEL-23142](https://issues.apache.org/jira/browse/CAMEL-23142)

camel-google-pubsub: Add maxDeliveryAttempts enforcement to prevent infinite redelivery loops

[CAMEL-23139](https://issues.apache.org/jira/browse/CAMEL-23139)

camel-launcher: implement a dockerfile for camel-launcher

[CAMEL-23138](https://issues.apache.org/jira/browse/CAMEL-23138)

Camel-jbang-mcp: Add camel\_route\_test\_scaffold MCP tool

[CAMEL-23134](https://issues.apache.org/jira/browse/CAMEL-23134)

Camel-jbang-mcp: Add camel\_dependency\_check MCP tool for dependency hygiene

[CAMEL-23133](https://issues.apache.org/jira/browse/CAMEL-23133)

\[camel-mdc\] Enable headers and properties pattern matching

[CAMEL-23131](https://issues.apache.org/jira/browse/CAMEL-23131)

Camel-jbang-mcp: Add camel\_error\_diagnose MCP tool for stack trace diagnosis

[CAMEL-23093](https://issues.apache.org/jira/browse/CAMEL-23093)

Add OAuth SPI for multi-IdP Client Credentials support

[CAMEL-23089](https://issues.apache.org/jira/browse/CAMEL-23089)

\[camel-observability-services\] Log metrics when shutting down

[CAMEL-23076](https://issues.apache.org/jira/browse/CAMEL-23076)

camel-openai - Add MCP Client Support to camel-openai

[CAMEL-23069](https://issues.apache.org/jira/browse/CAMEL-23069)

Add MCP client support to camel-langchain4j-agent

[CAMEL-23054](https://issues.apache.org/jira/browse/CAMEL-23054)

Camel-PQC: Add hybrid cryptography support

[CAMEL-23021](https://issues.apache.org/jira/browse/CAMEL-23021)

Camel-Google: Create a Google Firestore Starter

[CAMEL-23020](https://issues.apache.org/jira/browse/CAMEL-23020)

Camel-Google: Create a Firestore component

[CAMEL-23010](https://issues.apache.org/jira/browse/CAMEL-23010)

Camel-Spring-Boot: Create an Azure Functions starter

[CAMEL-23009](https://issues.apache.org/jira/browse/CAMEL-23009)

Camel-Azure: Create a native Azure Functions component

[CAMEL-22811](https://issues.apache.org/jira/browse/CAMEL-22811)

camel-kafka: Support Kafka 4.0 KIP-848 consumer rebalance protocol (group.protocol=consumer)

[CAMEL-22545](https://issues.apache.org/jira/browse/CAMEL-22545)

New camel-huggingface component

[CAMEL-22463](https://issues.apache.org/jira/browse/CAMEL-22463)

camel-spring-boot - Add support for Spring Boot v4

[CAMEL-21540](https://issues.apache.org/jira/browse/CAMEL-21540)

Add PGVector component for PostgreSQL vector database

[CAMEL-21095](https://issues.apache.org/jira/browse/CAMEL-21095)

camel-core - Make it easier to configure SSL using XML and YAML DSL

### Sub-task (12)

[CAMEL-23166](https://issues.apache.org/jira/browse/CAMEL-23166)

Generalize Google services authentication with common module - Google Firestore

[CAMEL-23090](https://issues.apache.org/jira/browse/CAMEL-23090)

Failing test JmsToJmsTransactedSecurityIT with JDK 25

[CAMEL-23088](https://issues.apache.org/jira/browse/CAMEL-23088)

Provide jdk 25 dockerfile template in jbang

[CAMEL-23045](https://issues.apache.org/jira/browse/CAMEL-23045)

Generalize Google services authentication with common module - Google Vertex AI

[CAMEL-23044](https://issues.apache.org/jira/browse/CAMEL-23044)

Generalize Google services authentication with common module - Google Sheets

[CAMEL-23043](https://issues.apache.org/jira/browse/CAMEL-23043)

Generalize Google services authentication with common module - Google Secrets Manager

[CAMEL-23042](https://issues.apache.org/jira/browse/CAMEL-23042)

Generalize Google services authentication with common module - Google Pubsub

[CAMEL-23041](https://issues.apache.org/jira/browse/CAMEL-23041)

Generalize Google services authentication with common module - Google Drive

[CAMEL-23040](https://issues.apache.org/jira/browse/CAMEL-23040)

Generalize Google services authentication with common module - Google Mail

[CAMEL-23039](https://issues.apache.org/jira/browse/CAMEL-23039)

Generalize Google services authentication with common module - Google Cloud Functions

[CAMEL-23038](https://issues.apache.org/jira/browse/CAMEL-23038)

Generalize Google services authentication with common module - Google Calendar

[CAMEL-23037](https://issues.apache.org/jira/browse/CAMEL-23037)

Generalize Google services authentication with common module - Google Bigquery

### Task (44)

[CAMEL-23298](https://issues.apache.org/jira/browse/CAMEL-23298)

camel-core - PGC and ODCF dataformats are missing in model

[CAMEL-23262](https://issues.apache.org/jira/browse/CAMEL-23262)

Upgrade actions/upload-artifact not using node 20

[CAMEL-23238](https://issues.apache.org/jira/browse/CAMEL-23238)

Camel-Google-VertexAI: Implement streaming, image generation, embeddings, multimodal, and streamRawPredict operations

[CAMEL-23202](https://issues.apache.org/jira/browse/CAMEL-23202)

Build failure with code coverage related to CamelThreadFactory

[CAMEL-23200](https://issues.apache.org/jira/browse/CAMEL-23200)

Camel-PQC: Replace Java serialization with PKCS#8/X.509 in FileBasedKeyLifecycleManager

[CAMEL-23171](https://issues.apache.org/jira/browse/CAMEL-23171)

Camel JBang compilation failure of tests

[CAMEL-23152](https://issues.apache.org/jira/browse/CAMEL-23152)

camel-jbang - Deprecate bind command

[CAMEL-23151](https://issues.apache.org/jira/browse/CAMEL-23151)

camel-csimple - Deprecate

[CAMEL-23148](https://issues.apache.org/jira/browse/CAMEL-23148)

camel-torchservce - Remove deprecated component

[CAMEL-23146](https://issues.apache.org/jira/browse/CAMEL-23146)

camel-launcher - Should install embedded plugins so they appear in --help

[CAMEL-23145](https://issues.apache.org/jira/browse/CAMEL-23145)

camel-launcher - Use version from parent/pom

[CAMEL-23128](https://issues.apache.org/jira/browse/CAMEL-23128)

Documentation build failure on update

[CAMEL-23113](https://issues.apache.org/jira/browse/CAMEL-23113)

Dependabot for Maven dependencies is no more working "Passed \`nil\` into T.must"

[CAMEL-23109](https://issues.apache.org/jira/browse/CAMEL-23109)

camel-spring-boot - Remove SB native

[CAMEL-23108](https://issues.apache.org/jira/browse/CAMEL-23108)

camel-spring-boot - Cleanup root pom.xml for unusued stuff

[CAMEL-23103](https://issues.apache.org/jira/browse/CAMEL-23103)

camel-json-patch - Deprecate

[CAMEL-23099](https://issues.apache.org/jira/browse/CAMEL-23099)

Remove camel-test references

[CAMEL-23097](https://issues.apache.org/jira/browse/CAMEL-23097)

Sample Eip: default value is not set via ProcessorDefinitiion

[CAMEL-23095](https://issues.apache.org/jira/browse/CAMEL-23095)

Remove nitrite component

[CAMEL-23086](https://issues.apache.org/jira/browse/CAMEL-23086)

Camel-Kafka: Upgrade to Kafka 4.2.x

[CAMEL-23075](https://issues.apache.org/jira/browse/CAMEL-23075)

Camel-ocsf: Fix broken inheritance in generated model classes

[CAMEL-23057](https://issues.apache.org/jira/browse/CAMEL-23057)

Upgrade cxf to 4.2.0

[CAMEL-23056](https://issues.apache.org/jira/browse/CAMEL-23056)

Camel JBang MCP - Add contract-first OpenAPI REST DSL support tools

[CAMEL-23055](https://issues.apache.org/jira/browse/CAMEL-23055)

Camel-Jbang: Upgrade to Camel-Kamelets 4.18.0

[CAMEL-22995](https://issues.apache.org/jira/browse/CAMEL-22995)

\[build\] Delete "automated/upgrade..." container branches on merge

[CAMEL-22994](https://issues.apache.org/jira/browse/CAMEL-22994)

\[build\] Comment and label GH task

[CAMEL-22965](https://issues.apache.org/jira/browse/CAMEL-22965)

\[build\] Exclude tooling and test-infra from coverage

[CAMEL-22943](https://issues.apache.org/jira/browse/CAMEL-22943)

camel-google-pubsub-lite - Remove this component

[CAMEL-22891](https://issues.apache.org/jira/browse/CAMEL-22891)

Replace arquillian usage in camel-spring-boot itests

[CAMEL-22780](https://issues.apache.org/jira/browse/CAMEL-22780)

Update camel from JUnit5 to JUnit6

[CAMEL-22774](https://issues.apache.org/jira/browse/CAMEL-22774)

\[build\] Refactor java21 special code when dropping support for java17

[CAMEL-22750](https://issues.apache.org/jira/browse/CAMEL-22750)

junit-bom import : junit 5 to junit 6 migration

[CAMEL-22729](https://issues.apache.org/jira/browse/CAMEL-22729)

Upgrade camel from jackson 2.19 -> 2.20.1

[CAMEL-22556](https://issues.apache.org/jira/browse/CAMEL-22556)

\[build\] Parameter 'resources' is read-only

[CAMEL-22524](https://issues.apache.org/jira/browse/CAMEL-22524)

\[camel-hazelcast\] Automate HazelcastRoutePolicy test

[CAMEL-22519](https://issues.apache.org/jira/browse/CAMEL-22519)

\[camel-mina\] Automate MinaProducerShutdownManualIT

[CAMEL-22515](https://issues.apache.org/jira/browse/CAMEL-22515)

\[camel-cometd\] Automate CometdProducerConsumerInteractiveAuthenticatedManualTest

[CAMEL-22506](https://issues.apache.org/jira/browse/CAMEL-22506)

\[camel-hazelcast\] Flaky unit test HazelcastReplicatedmapConsumerTest.testRemove

[CAMEL-22479](https://issues.apache.org/jira/browse/CAMEL-22479)

\[camel-telemetry\] Deprecate older tracing components

[CAMEL-22477](https://issues.apache.org/jira/browse/CAMEL-22477)

\[camel-mdc\] Promote the component and deprecate older MDC

[CAMEL-22409](https://issues.apache.org/jira/browse/CAMEL-22409)

website: zwsp invisible character breaks property at runtime

[CAMEL-22290](https://issues.apache.org/jira/browse/CAMEL-22290)

camel-core - Remove deprecated camel-cloud

[CAMEL-22289](https://issues.apache.org/jira/browse/CAMEL-22289)

camel-core - Remove deprecated service call EIP

[CAMEL-19434](https://issues.apache.org/jira/browse/CAMEL-19434)

camel-spring-boot - Remove arquilliam based tests

### Test (11)

[CAMEL-23253](https://issues.apache.org/jira/browse/CAMEL-23253)

LangChain4jEmbeddingsComponentInfinispanTargetIT is flaky due to Infinispan Hot Rod connection timeout

[CAMEL-23217](https://issues.apache.org/jira/browse/CAMEL-23217)

CamelSalesforceIT is failing on SpringBoot with NoClassDefFoundError: com/google/protobuf/RuntimeVersion$RuntimeDomain

[CAMEL-23209](https://issues.apache.org/jira/browse/CAMEL-23209)

Regular failure of Smb\* tests

[CAMEL-23206](https://issues.apache.org/jira/browse/CAMEL-23206)

SpringAiChatParameterOverrideIT.testTopPOverrideViaHeader test failing on main branch

[CAMEL-23189](https://issues.apache.org/jira/browse/CAMEL-23189)

Avoid flakiness of xslt tests

[CAMEL-23187](https://issues.apache.org/jira/browse/CAMEL-23187)

Failing test RunCommandITCase.runWithProperties

[CAMEL-23140](https://issues.apache.org/jira/browse/CAMEL-23140)

camel-spring-xml - MisspelledRouteRefTest.testApplicationContextFailed test is failing

[CAMEL-23121](https://issues.apache.org/jira/browse/CAMEL-23121)

Kafka tests are failing on Jenkins CI since upgrade to Kafka 4.2

[CAMEL-23104](https://issues.apache.org/jira/browse/CAMEL-23104)

camel-jbang-it - CustomJarsITCase test is failing locally

[CAMEL-22635](https://issues.apache.org/jira/browse/CAMEL-22635)

camel-netty - LogCaptureTest cannot setup capturer due to some log4j NPE

[CAMEL-22110](https://issues.apache.org/jira/browse/CAMEL-22110)

Fix issue related to flaky test HazelcastQueueConsumerPollTest.add

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).