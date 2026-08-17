# Apache camel 4.18.4 Release

## New and Noteworthy

This release is the new Camel 4.18.4 LTS release.

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
      <version>4.18.4</version>
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
      <version>4.18.4</version>
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
| [apache-camel-4.18.4-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.4/apache-camel-4.18.4-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-src.zip.sha512) |
| [apache-camel-4.18.4-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.xml.sha512) |
| [apache-camel-4.18.4-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.4/apache-camel-4.18.4-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (48)

[CAMEL-24360](https://issues.apache.org/jira/browse/CAMEL-24360)

camel-undertow - UndertowEndpoint discards the UndertowHeaderFilterStrategy set by DefaultUndertowHttpBinding

[CAMEL-24358](https://issues.apache.org/jira/browse/CAMEL-24358)

camel-jbang - camel run --repos does not propagate to Quarkus export

[CAMEL-24355](https://issues.apache.org/jira/browse/CAMEL-24355)

NIOConverter.toByteArray throws BufferUnderflowException when ByteBuffer has been fully read

[CAMEL-24354](https://issues.apache.org/jira/browse/CAMEL-24354)

camel-aws2-lambda: updateFunction never sets the code source, so UpdateFunctionCode always fails

[CAMEL-24343](https://issues.apache.org/jira/browse/CAMEL-24343)

camel-google-calendar: stream consumer can skip events and only reads the first page

[CAMEL-24341](https://issues.apache.org/jira/browse/CAMEL-24341)

camel-google-secret-manager: GCP vault refresh task reads the AWS vault configuration and reloads repeatedly

[CAMEL-24325](https://issues.apache.org/jira/browse/CAMEL-24325)

camel-jbang - Export with --runtime quarkus ignores -Dcamel.jbang.quarkus.platform.url system property

[CAMEL-24315](https://issues.apache.org/jira/browse/CAMEL-24315)

camel-google-pubsub: consumer stop misses subscribers still starting, thread parks forever in awaitTerminated

[CAMEL-24257](https://issues.apache.org/jira/browse/CAMEL-24257)

camel export fails with MongoTimeoutException for kamelets using #class: Component beans

[CAMEL-24253](https://issues.apache.org/jira/browse/CAMEL-24253)

Endpoint DSL mangles + and % characters in option values

[CAMEL-24251](https://issues.apache.org/jira/browse/CAMEL-24251)

camel-aws2 producer health checks can throw NPE when AwsServiceException has no error details

[CAMEL-24249](https://issues.apache.org/jira/browse/CAMEL-24249)

camel-aws2 MSK/MQ/STS producers throw copy-pasted IllegalArgumentException messages naming the wrong parameter

[CAMEL-24248](https://issues.apache.org/jira/browse/CAMEL-24248)

Concurrent pollEnrich can fail to stop in-use consumers after cache eviction

[CAMEL-24247](https://issues.apache.org/jira/browse/CAMEL-24247)

camel export produces duplicate camel-micrometer-prometheus dependency in pom.xml

[CAMEL-24244](https://issues.apache.org/jira/browse/CAMEL-24244)

camel-base-engine: DefaultStreamCachingStrategy.updateSpool calls lock() instead of unlock() in finally, blocking other threads forever

[CAMEL-24243](https://issues.apache.org/jira/browse/CAMEL-24243)

camel-aws2-athena: a still-running query is relaunched when waitTimeout expires and maxAttempts > 1

[CAMEL-24242](https://issues.apache.org/jira/browse/CAMEL-24242)

camel-aws2-athena: thread interruption during query polling is ignored, causing a busy poll loop

[CAMEL-24238](https://issues.apache.org/jira/browse/CAMEL-24238)

camel-aws2-ses: a RawMessage body is sent as the SdkBytes descriptor instead of the message content

[CAMEL-24234](https://issues.apache.org/jira/browse/CAMEL-24234)

camel-http throws ZipException: Not in GZIP format against any gzip-compressing server with default settings

[CAMEL-24231](https://issues.apache.org/jira/browse/CAMEL-24231)

pollEnrich with dynamic fileName using exchangeProperty fails due to missing properties in dummy exchange

[CAMEL-24224](https://issues.apache.org/jira/browse/CAMEL-24224)

camel-aws-bedrock: streaming metadata never captured for Claude/Nova, and inference profile ids rejected

[CAMEL-24203](https://issues.apache.org/jira/browse/CAMEL-24203)

camel-aws-security-hub: getFindingAggregator operation is declared but not implemented

[CAMEL-24201](https://issues.apache.org/jira/browse/CAMEL-24201)

camel-aws2-step-functions: listExecutions never sets stateMachineArn so the operation always fails

[CAMEL-24200](https://issues.apache.org/jira/browse/CAMEL-24200)

camel-aws2-timestream: createScheduledQuery writes the time column into tableName and never sets timeColumn

[CAMEL-24194](https://issues.apache.org/jira/browse/CAMEL-24194)

camel-aws-config: removeConformancePack reads the wrong header (RULE\_NAME instead of the conformance pack name)

[CAMEL-24193](https://issues.apache.org/jira/browse/CAMEL-24193)

camel-aws-secrets-manager: SQS-notification secret-refresh NPEs on missing queue and never drains the queue

[CAMEL-24191](https://issues.apache.org/jira/browse/CAMEL-24191)

camel-aws2-kinesis: KCL consumer ignores session credentials and mishandles checkpoint/error handling

[CAMEL-24187](https://issues.apache.org/jira/browse/CAMEL-24187)

camel-core: CamelContext.getEndpoint() never caches a uri containing a % character (double-normalization in AbstractCamelContext.getEndpointKey)

[CAMEL-24169](https://issues.apache.org/jira/browse/CAMEL-24169)

camel-jackson-avro / camel-jackson-protobuf - schema resolver latches the first resolved schema forever, breaking multi-type routes

[CAMEL-24158](https://issues.apache.org/jira/browse/CAMEL-24158)

camel-azure - Umbrella: high-severity findings from July 2026 review (storage-blob, servicebus, eventhubs, storage-queue, storage-datalake)

[CAMEL-24086](https://issues.apache.org/jira/browse/CAMEL-24086)

camel-aws2-sqs: FIFO batch send assigns the same MessageDeduplicationId to every entry

[CAMEL-24082](https://issues.apache.org/jira/browse/CAMEL-24082)

camel-aws-cloudtrail: consumer loses events (static cursor, no pagination, time-window skip)

[CAMEL-24080](https://issues.apache.org/jira/browse/CAMEL-24080)

camel-aws2-kinesis: consumer shard state is not thread-safe when consuming multiple shards

[CAMEL-24062](https://issues.apache.org/jira/browse/CAMEL-24062)

UseOriginalAggregationStrategy silently ignored under Multicast (original never bound) — inconsistent with Splitter

[CAMEL-24061](https://issues.apache.org/jira/browse/CAMEL-24061)

camel-zeebe: grpc-stub-based operations were never wired for auth

[CAMEL-24046](https://issues.apache.org/jira/browse/CAMEL-24046)

camel-sql - JdbcCachedMessageIdRepository: failed insert permanently poisons the cache; cache is not thread-safe

[CAMEL-24045](https://issues.apache.org/jira/browse/CAMEL-24045)

camel-sql - Connection leak with outputType=StreamList when the statement is not a query

[CAMEL-24044](https://issues.apache.org/jira/browse/CAMEL-24044)

camel-sql - Postgres aggregation repositories fail on insert: version bound without a placeholder

[CAMEL-24001](https://issues.apache.org/jira/browse/CAMEL-24001)

RestBindingAdvice.ensureHeaderContentType() sets Content-Type on body-less (e.g. 204) responses, and falls back to a raw multi-value "produces" list instead of a single media type

[CAMEL-23974](https://issues.apache.org/jira/browse/CAMEL-23974)

camel-zeebe: OAuth clientId/clientSecret/oAuthAPI configured on ZeebeComponent are never passed to ZeebeService, so no authentication occurs

[CAMEL-23945](https://issues.apache.org/jira/browse/CAMEL-23945)

camel-langchain4j-agent: producer race on shared agent field in agentFactory mode (fix needed on camel-4.18.x)

[CAMEL-23937](https://issues.apache.org/jira/browse/CAMEL-23937)

camel-azure-servicebus consumer defeats SDK auto lock-renewal for async routes, causing silent message-lock expiry mid-processing

[CAMEL-23936](https://issues.apache.org/jira/browse/CAMEL-23936)

\[camel-http\] logHttpActivity cause exception on gzip encoded responses

[CAMEL-23914](https://issues.apache.org/jira/browse/CAMEL-23914)

camel-jbang export fails with TypeConversionException when kamelet has optional Long property

[CAMEL-23895](https://issues.apache.org/jira/browse/CAMEL-23895)

\[camel-azure-servicebus\] http 401 using connection string

[CAMEL-23844](https://issues.apache.org/jira/browse/CAMEL-23844)

Camel-PQC: extractSecretKeyFromEncapsulation uses the raw enum name instead of the mapped JCE algorithm name

[CAMEL-23843](https://issues.apache.org/jira/browse/CAMEL-23843)

Camel-PQC: sign/verify only handle String payloads and use the platform default charset

[CAMEL-23840](https://issues.apache.org/jira/browse/CAMEL-23840)

pollEnrich with cacheSize(-1) does not disable consumer cache (dynamic endpoints)

### Improvement (14)

[CAMEL-24359](https://issues.apache.org/jira/browse/CAMEL-24359)

camel-atmosphere-websocket - align Exchange header constant names with Camel naming convention

[CAMEL-24319](https://issues.apache.org/jira/browse/CAMEL-24319)

camel-keycloak: optional token type (typ) and authorized party (azp) validation in KeycloakSecurityPolicy

[CAMEL-24299](https://issues.apache.org/jira/browse/CAMEL-24299)

camel-core: set SUPPORT\_DTD=false in XmlStreamDetector for consistency with other XML parsers

[CAMEL-24279](https://issues.apache.org/jira/browse/CAMEL-24279)

camel-google-storage: contain downloadFileName downloads within the configured directory

[CAMEL-24240](https://issues.apache.org/jira/browse/CAMEL-24240)

camel-fhir: Align all FHIR core dependencies

[CAMEL-24085](https://issues.apache.org/jira/browse/CAMEL-24085)

camel-ironmq: apply header filter strategy when mapping message envelope headers

[CAMEL-24084](https://issues.apache.org/jira/browse/CAMEL-24084)

camel-knative: apply header filter strategy to structured-mode CloudEvent extension headers

[CAMEL-23942](https://issues.apache.org/jira/browse/CAMEL-23942)

camel-azure-storage-blob / camel-azure-storage-datalake: contain fileDir downloads within the configured directory

[CAMEL-23891](https://issues.apache.org/jira/browse/CAMEL-23891)

camel-mail: apply inbound Camel\* header filtering in MimeMultipartDataFormat unmarshal (headersInline=true), consistent with the mail consumer

[CAMEL-23875](https://issues.apache.org/jira/browse/CAMEL-23875)

camel-keycloak: add optional audience (aud) validation to token verification

[CAMEL-23868](https://issues.apache.org/jira/browse/CAMEL-23868)

camel-file: make local work directory / starting directory containment checks path-boundary aware

[CAMEL-23768](https://issues.apache.org/jira/browse/CAMEL-23768)

camel-keycloak: select the JWKS verification key by the token kid

[CAMEL-23766](https://issues.apache.org/jira/browse/CAMEL-23766)

camel-crypto: use a constant-time comparison for HMAC verification in HMACAccumulator

[CAMEL-23525](https://issues.apache.org/jira/browse/CAMEL-23525)

camel-platform-http-main: add optional JWT issuer and audience claim validation

### Task (2)

[CAMEL-24204](https://issues.apache.org/jira/browse/CAMEL-24204)

camel-jms - exposeListenerSession catalog metadata reports wrong default value (false instead of true)

[CAMEL-21314](https://issues.apache.org/jira/browse/CAMEL-21314)

camel-aws - Fix S3CopyObjectCustomerKeyIT.sendIn which is failing on main branch

### Test (2)

[CAMEL-24284](https://issues.apache.org/jira/browse/CAMEL-24284)

SjmsConnectionRecoveryTest is very flaky on Jenkins CI

[CAMEL-23940](https://issues.apache.org/jira/browse/CAMEL-23940)

4 Camel JBang IT tests are failng with "Option -D, must be part of a propertyBuilds and runs provided script." on Jenkins CI for 4.18.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).