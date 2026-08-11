# Apache camel 4.22.0 Release

## New and Noteworthy

This release is the new Camel 4.22.0 LTS release.

## Supported Java version

This version supports Java 17, 21 and 25.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.22.0</version>
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
      <version>4.22.0</version>
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
| [apache-camel-4.22.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.0/apache-camel-4.22.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-src.zip.sha512) |
| [apache-camel-4.22.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.xml.sha512) |
| [apache-camel-4.22.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.0/apache-camel-4.22.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.22.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.22.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (221)

[CAMEL-24371](https://issues.apache.org/jira/browse/CAMEL-24371)

camel-a2a - fix WebhookUrlValidator address classification and host matching

[CAMEL-24365](https://issues.apache.org/jira/browse/CAMEL-24365)

camel-core - Attachment trait lost when producer creates a fresh OUT message (regression from CAMEL-21755)

[CAMEL-24364](https://issues.apache.org/jira/browse/CAMEL-24364)

camel-http removes attachment since camel 4.10.1

[CAMEL-24363](https://issues.apache.org/jira/browse/CAMEL-24363)

camel-aws: minor fixes - iam endpoint doStop, eks catalog defaultValue, parameter-store value header

[CAMEL-24361](https://issues.apache.org/jira/browse/CAMEL-24361)

EIP model metadata does not propagate @XmlAttribute(required = true) to generated JSON

[CAMEL-24360](https://issues.apache.org/jira/browse/CAMEL-24360)

camel-undertow - UndertowEndpoint discards the UndertowHeaderFilterStrategy set by DefaultUndertowHttpBinding

[CAMEL-24357](https://issues.apache.org/jira/browse/CAMEL-24357)

camel-aws2-s3-vectors: consumer returns no results (topK forced to 0), ignores the delay option, and can lose vectors on failure

[CAMEL-24355](https://issues.apache.org/jira/browse/CAMEL-24355)

NIOConverter.toByteArray throws BufferUnderflowException when ByteBuffer has been fully read

[CAMEL-24354](https://issues.apache.org/jira/browse/CAMEL-24354)

camel-aws2-lambda: updateFunction never sets the code source, so UpdateFunctionCode always fails

[CAMEL-24351](https://issues.apache.org/jira/browse/CAMEL-24351)

camel-platform-http-starter: CamelRequestHandlerMapping is @Lazy, so every platform-http endpoint can silently return 404

[CAMEL-24346](https://issues.apache.org/jira/browse/CAMEL-24346)

camel-google-sheets: splitResults always reports range index 1 and NPEs on an empty range

[CAMEL-24345](https://issues.apache.org/jira/browse/CAMEL-24345)

camel-google-vertexai: streamOutputMode and jsonMode options are never applied

[CAMEL-24344](https://issues.apache.org/jira/browse/CAMEL-24344)

camel-google-mail: raw option always returns a null body and non-multipart messages produce no body

[CAMEL-24343](https://issues.apache.org/jira/browse/CAMEL-24343)

camel-google-calendar: stream consumer can skip events and only reads the first page

[CAMEL-24342](https://issues.apache.org/jira/browse/CAMEL-24342)

camel-google-storage: producer sets wrong blob metadata and NPEs on missing objects

[CAMEL-24341](https://issues.apache.org/jira/browse/CAMEL-24341)

camel-google-secret-manager: GCP vault refresh task reads the AWS vault configuration and reloads repeatedly

[CAMEL-24340](https://issues.apache.org/jira/browse/CAMEL-24340)

camel-salesforce: apexMethod is documented as an Apex method name but is used as the HTTP verb

[CAMEL-24320](https://issues.apache.org/jira/browse/CAMEL-24320)

camel-core - Kamelet route creation fails with virtual threads enabled on JDK 25

[CAMEL-24315](https://issues.apache.org/jira/browse/CAMEL-24315)

camel-google-pubsub: consumer stop misses subscribers still starting, thread parks forever in awaitTerminated

[CAMEL-24305](https://issues.apache.org/jira/browse/CAMEL-24305)

KafkaComponent does not autowire custom KafkaClientFactory because default instance is created before autowiring

[CAMEL-24301](https://issues.apache.org/jira/browse/CAMEL-24301)

RouteService NPE when startup-failure exception has no message

[CAMEL-24286](https://issues.apache.org/jira/browse/CAMEL-24286)

camel-support: BackgroundTask supplier exception hangs an unlimited-duration run() and leaks the task registration

[CAMEL-24273](https://issues.apache.org/jira/browse/CAMEL-24273)

camel-mina-ftp - After every SFTP transfer, the number of daemon threads increases.

[CAMEL-24262](https://issues.apache.org/jira/browse/CAMEL-24262)

camel-aws2: producer catch blocks eagerly dereference nullable awsErrorDetails() when logging the error code

[CAMEL-24261](https://issues.apache.org/jira/browse/CAMEL-24261)

camel-aws2: producers silently no-op when pojoRequest=true and the body has the wrong type (complete CAMEL-23462 across all producers)

[CAMEL-24257](https://issues.apache.org/jira/browse/CAMEL-24257)

camel export fails with MongoTimeoutException for kamelets using #class: Component beans

[CAMEL-24253](https://issues.apache.org/jira/browse/CAMEL-24253)

Endpoint DSL mangles + and % characters in option values

[CAMEL-24252](https://issues.apache.org/jira/browse/CAMEL-24252)

Container Version Upgrade workflow fails: metadata updater aborts PR loop

[CAMEL-24251](https://issues.apache.org/jira/browse/CAMEL-24251)

camel-aws2 producer health checks can throw NPE when AwsServiceException has no error details

[CAMEL-24249](https://issues.apache.org/jira/browse/CAMEL-24249)

camel-aws2 MSK/MQ/STS producers throw copy-pasted IllegalArgumentException messages naming the wrong parameter

[CAMEL-24248](https://issues.apache.org/jira/browse/CAMEL-24248)

Concurrent pollEnrich can fail to stop in-use consumers after cache eviction

[CAMEL-24247](https://issues.apache.org/jira/browse/CAMEL-24247)

camel export produces duplicate camel-micrometer-prometheus dependency in pom.xml

[CAMEL-24243](https://issues.apache.org/jira/browse/CAMEL-24243)

camel-aws2-athena: a still-running query is relaunched when waitTimeout expires and maxAttempts > 1

[CAMEL-24242](https://issues.apache.org/jira/browse/CAMEL-24242)

camel-aws2-athena: thread interruption during query polling is ignored, causing a busy poll loop

[CAMEL-24241](https://issues.apache.org/jira/browse/CAMEL-24241)

camel-ai-tool: AiToolExecutor skips the argument allowlist for tools declaring no parameters

[CAMEL-24238](https://issues.apache.org/jira/browse/CAMEL-24238)

camel-aws2-ses: a RawMessage body is sent as the SdkBytes descriptor instead of the message content

[CAMEL-24234](https://issues.apache.org/jira/browse/CAMEL-24234)

camel-http throws ZipException: Not in GZIP format against any gzip-compressing server with default settings

[CAMEL-24232](https://issues.apache.org/jira/browse/CAMEL-24232)

ProcessorTransformer does not copy variables to transform exchange

[CAMEL-24231](https://issues.apache.org/jira/browse/CAMEL-24231)

pollEnrich with dynamic fileName using exchangeProperty fails due to missing properties in dummy exchange

[CAMEL-24230](https://issues.apache.org/jira/browse/CAMEL-24230)

jsonpath language with writeAsString=true returns Map instead of JSON String for object expressions

[CAMEL-24225](https://issues.apache.org/jira/browse/CAMEL-24225)

AGENTS.md test-visibility guidance mandates non-compiling code (@Override, broken example, no base-class carve-out)

[CAMEL-24224](https://issues.apache.org/jira/browse/CAMEL-24224)

camel-aws-bedrock: streaming metadata never captured for Claude/Nova, and inference profile ids rejected

[CAMEL-24216](https://issues.apache.org/jira/browse/CAMEL-24216)

jdk.xml.xpathTotalOpLimit can be overriden and is not set back correctly after execution

[CAMEL-24208](https://issues.apache.org/jira/browse/CAMEL-24208)

pollOnError=ERROR\_HANDLER skips valid messages on other partitions due to SeekUtil bug

[CAMEL-24207](https://issues.apache.org/jira/browse/CAMEL-24207)

camel-aws2-transcribe: 21 declared operations are empty stubs that silently do nothing

[CAMEL-24203](https://issues.apache.org/jira/browse/CAMEL-24203)

camel-aws-security-hub: getFindingAggregator operation is declared but not implemented

[CAMEL-24201](https://issues.apache.org/jira/browse/CAMEL-24201)

camel-aws2-step-functions: listExecutions never sets stateMachineArn so the operation always fails

[CAMEL-24200](https://issues.apache.org/jira/browse/CAMEL-24200)

camel-aws2-timestream: createScheduledQuery writes the time column into tableName and never sets timeColumn

[CAMEL-24197](https://issues.apache.org/jira/browse/CAMEL-24197)

camel-aws2-kinesis - Fixed-shardId DescribeStream on every poll and batch partition key

[CAMEL-24196](https://issues.apache.org/jira/browse/CAMEL-24196)

camel-aws2-sqs - QueueDoesNotExist swallowed, thread pool leak, and batch chunking

[CAMEL-24195](https://issues.apache.org/jira/browse/CAMEL-24195)

camel-aws2-s3 - StreamUploadProducer race condition and timeout task exception handling

[CAMEL-24194](https://issues.apache.org/jira/browse/CAMEL-24194)

camel-aws-config: removeConformancePack reads the wrong header (RULE\_NAME instead of the conformance pack name)

[CAMEL-24193](https://issues.apache.org/jira/browse/CAMEL-24193)

camel-aws-secrets-manager: SQS-notification secret-refresh NPEs on missing queue and never drains the queue

[CAMEL-24191](https://issues.apache.org/jira/browse/CAMEL-24191)

camel-aws2-kinesis: KCL consumer ignores session credentials and mishandles checkpoint/error handling

[CAMEL-24189](https://issues.apache.org/jira/browse/CAMEL-24189)

camel-smb - SmbStreamDownloadIT fails with empty body on streamDownload

[CAMEL-24187](https://issues.apache.org/jira/browse/CAMEL-24187)

camel-core: CamelContext.getEndpoint() never caches a uri containing a % character (double-normalization in AbstractCamelContext.getEndpointKey)

[CAMEL-24183](https://issues.apache.org/jira/browse/CAMEL-24183)

camel-cxfrs - Spring rsClient producer silently drops endpoint URI options

[CAMEL-24182](https://issues.apache.org/jira/browse/CAMEL-24182)

camel-cxf - SpringBusFactoryBean never shuts down the bus it creates (Bus/BusApplicationContext leak)

[CAMEL-24181](https://issues.apache.org/jira/browse/CAMEL-24181)

camel-cxf - CxfSpringEndpoint shuts down the shared application-wide CXF bus on endpoint stop

[CAMEL-24180](https://issues.apache.org/jira/browse/CAMEL-24180)

camel-cxf - CxfMessageHelper fallback drops non-InputStream message bodies (sets null)

[CAMEL-24179](https://issues.apache.org/jira/browse/CAMEL-24179)

camel-cxf/camel-cxfrs - continuation timeout races with in-flight async processing (UoW closed twice, continuation double-resumed)

[CAMEL-24178](https://issues.apache.org/jira/browse/CAMEL-24178)

camel-cxfrs - producer matrix/query parsing throws on legal request URIs (valueless params, bridge scenario)

[CAMEL-24177](https://issues.apache.org/jira/browse/CAMEL-24177)

camel-cxfrs - DefaultCxfRsBinding.contentLanguage latches first request's value and races under concurrency

[CAMEL-24176](https://issues.apache.org/jira/browse/CAMEL-24176)

camel-cxfrs - async producer never maps HTTP errors to CxfOperationException (getClass().isInstance always false)

[CAMEL-24174](https://issues.apache.org/jira/browse/CAMEL-24174)

camel-jpa - Parallel EntityManager fix from CAMEL-22534 only covers Splitter, not Multicast/RecipientList/WireTap

[CAMEL-24170](https://issues.apache.org/jira/browse/CAMEL-24170)

camel dataformats - Umbrella: remaining high/medium findings from the July 2026 data format review

[CAMEL-24169](https://issues.apache.org/jira/browse/CAMEL-24169)

camel-jackson-avro / camel-jackson-protobuf - schema resolver latches the first resolved schema forever, breaking multi-type routes

[CAMEL-24168](https://issues.apache.org/jira/browse/CAMEL-24168)

camel-bindy - BigDecimal/Double @DataField without explicit precision throws ArithmeticException on unmarshal and truncates on marshal

[CAMEL-24167](https://issues.apache.org/jira/browse/CAMEL-24167)

camel-csv - 'format' option (EXCEL, MYSQL, ...) is silently ignored (dead guard), and mismatches commons-csv Predefined names

[CAMEL-24166](https://issues.apache.org/jira/browse/CAMEL-24166)

camel-zipfile / camel-tarfile - maxDecompressedSize is bypassed entirely in iterator/splitter mode (decompression-bomb protection defeated)

[CAMEL-24165](https://issues.apache.org/jira/browse/CAMEL-24165)

camel-soap - SoapDataFormat.Builder.ignoreUnmarshalledHeaders(boolean) infinitely recurses (StackOverflowError); option also dropped by reifier

[CAMEL-24164](https://issues.apache.org/jira/browse/CAMEL-24164)

camel-jaxb - CamelJaxbPartClass header permanently mutates the shared data format (state pollution + data race)

[CAMEL-24163](https://issues.apache.org/jira/browse/CAMEL-24163)

camel-core - JsonDataFormatReifier passes Jackson-only options to Gson/Fastjson/Jsonb, crashing route startup

[CAMEL-24162](https://issues.apache.org/jira/browse/CAMEL-24162)

camel-jacksonxml - moduleClassNames DSL option crashes route creation (reifier typo 'modulesClassNames')

[CAMEL-24161](https://issues.apache.org/jira/browse/CAMEL-24161)

camel-salesforce - Umbrella: medium-severity findings from July 2026 review

[CAMEL-24160](https://issues.apache.org/jira/browse/CAMEL-24160)

camel-salesforce - Umbrella: high-severity findings from July 2026 review (auth, streaming/pubsub, REST/bulk/composite)

[CAMEL-24159](https://issues.apache.org/jira/browse/CAMEL-24159)

camel-azure - Umbrella: medium-severity findings from July 2026 review (incl. cross-module credentialType override)

[CAMEL-24158](https://issues.apache.org/jira/browse/CAMEL-24158)

camel-azure - Umbrella: high-severity findings from July 2026 review (storage-blob, servicebus, eventhubs, storage-queue, storage-datalake)

[CAMEL-24157](https://issues.apache.org/jira/browse/CAMEL-24157)

camel-aws2 - Umbrella: medium-severity findings from July 2026 review (S3, SQS, SNS, Kinesis, DDB)

[CAMEL-24156](https://issues.apache.org/jira/browse/CAMEL-24156)

camel-aws2 - Umbrella: high-severity findings from July 2026 review (S3, SQS, SNS, Kinesis, DDB)

[CAMEL-24155](https://issues.apache.org/jira/browse/CAMEL-24155)

camel-salesforce - streamQueryResult iterator hangs the route thread forever when queryMore fails

[CAMEL-24154](https://issues.apache.org/jira/browse/CAMEL-24154)

camel-aws2-ddb - DDB Streams consumer never subscribes to shards created after startup - silent data loss on resharding

[CAMEL-24153](https://issues.apache.org/jira/browse/CAMEL-24153)

camel-aws2-s3 - Streaming upload silently truncates bodies larger than partSize and orphans multipart uploads

[CAMEL-24152](https://issues.apache.org/jira/browse/CAMEL-24152)

camel-snakeyaml - Concurrent marshal/unmarshal corrupts data: per-thread Yaml instances share one stateful constructor/representer

[CAMEL-24151](https://issues.apache.org/jira/browse/CAMEL-24151)

camel-saga/camel-lra: medium and low findings from Saga EIP code review (July 2026)

[CAMEL-24150](https://issues.apache.org/jira/browse/CAMEL-24150)

camel-saga: SagaProcessor.doStop() stops the shared CamelSagaService - stopping one saga route breaks sagas on all routes

[CAMEL-24149](https://issues.apache.org/jira/browse/CAMEL-24149)

camel-saga: saga:complete / saga:compensate only read the Long-Running-Action header - MANUAL completion broken after removeHeaders

[CAMEL-24148](https://issues.apache.org/jira/browse/CAMEL-24148)

camel-saga: option values are overwritten when the same saga step is enlisted multiple times in one saga

[CAMEL-24147](https://issues.apache.org/jira/browse/CAMEL-24147)

camel-lra: participant callback URLs are not URL-encoded and parseQuery is lossy - compensation breaks for URIs with query parameters or options with special characters

[CAMEL-24146](https://issues.apache.org/jira/browse/CAMEL-24146)

camel-saga: InMemorySagaCoordinator creates a FluentProducerTemplate per compensation/completion attempt and never stops it

[CAMEL-24145](https://issues.apache.org/jira/browse/CAMEL-24145)

camel-saga: InMemorySagaCoordinator compensate()/complete() return already-completed futures - finalization failures never propagate

[CAMEL-24144](https://issues.apache.org/jira/browse/CAMEL-24144)

camel-saga: InMemorySagaService never removes coordinators - unbounded memory growth

[CAMEL-24143](https://issues.apache.org/jira/browse/CAMEL-24143)

camel-core - Split & Aggregate EIP review follow-ups (medium findings)

[CAMEL-24142](https://issues.apache.org/jira/browse/CAMEL-24142)

camel-core - Multicast/Split timeout silently lost when it fires while a result is being aggregated (tryLock never retried)

[CAMEL-24141](https://issues.apache.org/jira/browse/CAMEL-24141)

camel-core - Aggregate EIP recovery and completionInterval background tasks are permanently cancelled by the first exception

[CAMEL-24140](https://issues.apache.org/jira/browse/CAMEL-24140)

camel-core - UseOriginalAggregationStrategy still not honored when shareUnitOfWork is enabled (Multicast/Split/RecipientList)

[CAMEL-24139](https://issues.apache.org/jira/browse/CAMEL-24139)

camel-core - Splitter watermark advances past unprocessed items when a streaming split aborts without an exception (data loss on resume)

[CAMEL-24138](https://issues.apache.org/jira/browse/CAMEL-24138)

camel-core - Splitter errorThreshold/maxFailedRecords: failure tracker leaks into nested splits and silently swallows their failures

[CAMEL-24136](https://issues.apache.org/jira/browse/CAMEL-24136)

Circuit Breaker EIP - umbrella for medium findings (FT exchange-property contract, parity gaps, dead option, docs)

[CAMEL-24135](https://issues.apache.org/jira/browse/CAMEL-24135)

camel-resilience4j - JMX getNumberOfSlowSuccessfulCalls returns total slow calls; console hides failure counts while failure rate is -1

[CAMEL-24134](https://issues.apache.org/jira/browse/CAMEL-24134)

camel-resilience4j / camel-microprofile-fault-tolerance - Circuit Breaker EIP: timed-out task writes results back to the original exchange, racing with fallback processing

[CAMEL-24133](https://issues.apache.org/jira/browse/CAMEL-24133)

camel-resilience4j / camel-microprofile-fault-tolerance - Circuit Breaker EIP corrupts in-flight exchange in pooled mode (releases original exchange instead of copy)

[CAMEL-24132](https://issues.apache.org/jira/browse/CAMEL-24132)

camel-jpa: medium-severity findings from July 2026 component review (umbrella)

[CAMEL-24131](https://issues.apache.org/jira/browse/CAMEL-24131)

camel-jpa: consumer with nativeQuery (no resultClass) and default consumeDelete fails to delete rows, causing endless reprocessing

[CAMEL-24130](https://issues.apache.org/jira/browse/CAMEL-24130)

camel-jpa: JpaMessageIdRepository can close the EntityManager owned by a JPA consumer sharing the same exchange

[CAMEL-24129](https://issues.apache.org/jira/browse/CAMEL-24129)

camel-jpa: JpaConsumer ignores the configured preDeleteHandler and re-derives it via reflection on every message

[CAMEL-24128](https://issues.apache.org/jira/browse/CAMEL-24128)

camel-jpa: JpaPollingConsumer.receive() leaks an EntityManager on every call

[CAMEL-24124](https://issues.apache.org/jira/browse/CAMEL-24124)

camel-jms: InOut exchanges in-flight during shutdown have AsyncCallback never completed - causes 45s graceful-shutdown stall

[CAMEL-24123](https://issues.apache.org/jira/browse/CAMEL-24123)

camel-smb: recursive=true with readLock=changed never consumes files in sub-directories - relative path is passed as SMB search pattern

[CAMEL-24122](https://issues.apache.org/jira/browse/CAMEL-24122)

camel-smb: readLockTimeout=0 (documented "0 or lower = forever") makes readLock=changed skip every file forever

[CAMEL-24121](https://issues.apache.org/jira/browse/CAMEL-24121)

camel-smb: producer with tempPrefix/tempFileName always fails with NullPointerException - existsFile is called before any connect

[CAMEL-24120](https://issues.apache.org/jira/browse/CAMEL-24120)

camel-smb: consumer downloads every file twice; streamDownload=true leaks a remote file handle per file (SmbFile.getBody bypasses the retrieved body)

[CAMEL-24118](https://issues.apache.org/jira/browse/CAMEL-24118)

camel-openapi-java: RestOpenApiReader emits invalid OpenAPI 3.x (formData params, collectionFormat styles, boolean/primitive-array/header types, 3.1 type loss) - umbrella

[CAMEL-24117](https://issues.apache.org/jira/browse/CAMEL-24117)

camel-rest-openapi: one strategy instance shared by all consumers - missingOperation/mockIncludePattern cross-talk, second consumer can silently disable fail-fast validation

[CAMEL-24116](https://issues.apache.org/jira/browse/CAMEL-24116)

camel-rest-openapi: RestOpenApiProcessor doInit/doStop are dead code since the advice conversion (CAMEL-22742) - services never stopped, stale platform-http registrations on route reload

[CAMEL-24115](https://issues.apache.org/jira/browse/CAMEL-24115)

camel-rest-openapi: operations without operationId validate against generated GENOPID\_\* ids but dispatch to direct:null at runtime

[CAMEL-24114](https://issues.apache.org/jira/browse/CAMEL-24114)

camel-rest-openapi: requestValidationEnabled rejects requests whose required query parameters are supplied as endpoint literals or exchange variables

[CAMEL-24113](https://issues.apache.org/jira/browse/CAMEL-24113)

camel-rest-openapi: producers for the same operation share one cached rest: delegate endpoint - produces/consumes/queryParameters cross-contamination between routes

[CAMEL-24112](https://issues.apache.org/jira/browse/CAMEL-24112)

camel-rest-openapi: path parameters leak into the query string when the operation has more than one parameter

[CAMEL-24111](https://issues.apache.org/jira/browse/CAMEL-24111)

camel-xslt: dead InputStream close logic in XsltBuilder.process() since the SourceHandlerFactory refactoring

[CAMEL-24110](https://issues.apache.org/jira/browse/CAMEL-24110)

camel-xslt-saxon: saxonReaderProperties null-guard is always true - stylesheets parsed by raw unhardened SAXParser, URIResolvers returning DOMSource broken

[CAMEL-24109](https://issues.apache.org/jira/browse/CAMEL-24109)

camel-xslt-saxon: doInit()/doStart() duplicate the parent lifecycle - stylesheet loaded and compiled twice on startup

[CAMEL-24108](https://issues.apache.org/jira/browse/CAMEL-24108)

camel-xslt-saxon: secureProcessing=true (documented default) is never applied unless saxonExtensionFunctions is configured; transformerFactoryConfigurationStrategy silently ignored

[CAMEL-24107](https://issues.apache.org/jira/browse/CAMEL-24107)

camel-xslt: stylesheet reload (contentCache=false / clearCachedStylesheet) is not thread-safe - stale pooled transformers keep serving the old stylesheet

[CAMEL-24106](https://issues.apache.org/jira/browse/CAMEL-24106)

camel-xslt: 'source' option silently ignored when the message body is an InputStream - transforms the wrong document

[CAMEL-24105](https://issues.apache.org/jira/browse/CAMEL-24105)

camel-bean: @RoutingSlip/@RecipientList/@DynamicRouter processors are added as CamelContext services on every MethodInfo creation and never removed

[CAMEL-24104](https://issues.apache.org/jira/browse/CAMEL-24104)

camel-bean: racy lazy Processor-adapter lookup in AbstractBeanProcessor (non-volatile fields, no retry on conversion failure)

[CAMEL-24103](https://issues.apache.org/jira/browse/CAMEL-24103)

camel-bean: bean method returning null CompletionStage causes opaque NullPointerException

[CAMEL-24102](https://issues.apache.org/jira/browse/CAMEL-24102)

camel-bean: AmbiguousMethodCallException from body-conversion matching lists the same method twice instead of the actual candidates

[CAMEL-24101](https://issues.apache.org/jira/browse/CAMEL-24101)

camel-bean: OGNL list index equal to list size escapes bounds handling - raw IndexOutOfBoundsException and broken null-safe

[CAMEL-24100](https://issues.apache.org/jira/browse/CAMEL-24100)

camel-bean: class: endpoint creates a new bean instance per message despite default Singleton scope

[CAMEL-24099](https://issues.apache.org/jira/browse/CAMEL-24099)

camel-bean: bean implementing Service is not restarted on route restart when used via bean() DSL

[CAMEL-24098](https://issues.apache.org/jira/browse/CAMEL-24098)

camel-ftp: SFTP ciphers/keyExchangeProtocols mutate global static JSch config - cross-endpoint contamination and races

[CAMEL-24097](https://issues.apache.org/jira/browse/CAMEL-24097)

camel-ftp: SFTP knownHostsUri/knownHosts silently clobbered by unconditional ~/.ssh/known\_hosts fallback - host key verification uses the wrong database

[CAMEL-24096](https://issues.apache.org/jira/browse/CAMEL-24096)

camel-ftp: readLockTimeout=0 (documented as forever) makes readLock=changed never acquire the lock on FTP/FTPS/SFTP - regression from CAMEL-17121 Tasks conversion

[CAMEL-24095](https://issues.apache.org/jira/browse/CAMEL-24095)

camel-file: tempFileName + fileExist=Move + eagerDeleteTargetFile=false silently overwrites the existing target instead of moving it (no Move branch in handleExistingTarget)

[CAMEL-24094](https://issues.apache.org/jira/browse/CAMEL-24094)

camel-file: forceWrites option is dead since Camel 2.20 - no fsync is ever performed despite documented durability guarantee

[CAMEL-24093](https://issues.apache.org/jira/browse/CAMEL-24093)

camel-file: idempotent read-lock strategies compute the release key from the post-preMove path - keys leak and same-named files are never consumed again

[CAMEL-24092](https://issues.apache.org/jira/browse/CAMEL-24092)

camel-file: readLock=fileLock claims the lock after an IOException - file processed with no lock held and marker file deleted (possible duplicate consumption)

[CAMEL-24091](https://issues.apache.org/jira/browse/CAMEL-24091)

camel-file: completion-time idempotentKey evaluated against route-mutated headers - failed files never retried (eager) or endless duplicates (non-eager); regression of CAMEL-21733

[CAMEL-24090](https://issues.apache.org/jira/browse/CAMEL-24090)

camel-file: eagerly-added idempotent keys are not drained when pollDirectory throws mid-poll - scanned files are never consumed (List drain overload missed by CAMEL-21830)

[CAMEL-24089](https://issues.apache.org/jira/browse/CAMEL-24089)

camel-file: file-to-file copy with readLock=fileLock silently truncates files larger than 2 GB on Linux (single transferTo, return value ignored)

[CAMEL-24088](https://issues.apache.org/jira/browse/CAMEL-24088)

camel-ftp: streamDownload treats a refused RETR as success - remote file is moved/deleted although it was never downloaded

[CAMEL-24086](https://issues.apache.org/jira/browse/CAMEL-24086)

camel-aws2-sqs: FIFO batch send assigns the same MessageDeduplicationId to every entry

[CAMEL-24083](https://issues.apache.org/jira/browse/CAMEL-24083)

camel-sjms - asyncConsumer failures are silently dropped (same bug as CAMEL-24069)

[CAMEL-24082](https://issues.apache.org/jira/browse/CAMEL-24082)

camel-aws-cloudtrail: consumer loses events (static cursor, no pagination, time-window skip)

[CAMEL-24080](https://issues.apache.org/jira/browse/CAMEL-24080)

camel-aws2-kinesis: consumer shard state is not thread-safe when consuming multiple shards

[CAMEL-24079](https://issues.apache.org/jira/browse/CAMEL-24079)

camel-quartz - QuartzScheduledPollConsumerScheduler may ignore startScheduler=false

[CAMEL-24078](https://issues.apache.org/jira/browse/CAMEL-24078)

camel-jms / camel-amqp code review (July 2026): umbrella for medium/low findings

[CAMEL-24077](https://issues.apache.org/jira/browse/CAMEL-24077)

camel-amqp: useSsl=true renders empty transport.\* options - breaks JVM-default trust store and server-only TLS

[CAMEL-24076](https://issues.apache.org/jira/browse/CAMEL-24076)

camel-jms: browseLimit URI option is dead - browsing is unlimited despite the documented default of 100 (CAMEL-21183 follow-up)

[CAMEL-24075](https://issues.apache.org/jira/browse/CAMEL-24075)

camel-jms: transferException=true silently swallows processing failures (and commits the transaction) when the message has no JMSReplyTo

[CAMEL-24074](https://issues.apache.org/jira/browse/CAMEL-24074)

camel-jms: TemporaryQueueReplyManager resolves the temporary reply queue without synchronization - replies can be black-holed (CAMEL-20769 follow-up)

[CAMEL-24073](https://issues.apache.org/jira/browse/CAMEL-24073)

camel-jms: InOut AsyncCallback.done() invoked twice when the JMS send fails after reply registration

[CAMEL-24072](https://issues.apache.org/jira/browse/CAMEL-24072)

camel-jms: component-level transacted=true breaks ConnectionFactory autowiring - startup fails with "connectionFactory must be specified"

[CAMEL-24071](https://issues.apache.org/jira/browse/CAMEL-24071)

camel-spring-rabbitmq - Inconsistent handling of comma-separated queues option (listener container does not trim; polling consumer broken with multiple queues)

[CAMEL-24070](https://issues.apache.org/jira/browse/CAMEL-24070)

camel-spring-rabbitmq - SpringRabbitMQProducer lazy template creation is not thread-safe and can leak started AsyncRabbitTemplates

[CAMEL-24069](https://issues.apache.org/jira/browse/CAMEL-24069)

camel-spring-rabbitmq - asyncConsumer failures are dropped because the endpoint exception handler is used instead of the consumer exception handler

[CAMEL-24068](https://issues.apache.org/jira/browse/CAMEL-24068)

camel-spring-rabbitmq - Effective default of replyTimeout is 5000 millis instead of the documented 30000

[CAMEL-24067](https://issues.apache.org/jira/browse/CAMEL-24067)

camel-spring - SpringInjector does not inject CamelContext into CamelContextAware beans created via factory method

[CAMEL-24066](https://issues.apache.org/jira/browse/CAMEL-24066)

camel-spring - SpringScheduledPollConsumerScheduler ignores startScheduler=false (breaks ScheduledPollConsumerScheduler contract)

[CAMEL-24065](https://issues.apache.org/jira/browse/CAMEL-24065)

camel-spring - spring-event: ConcurrentModificationException when a route is stopped while an ApplicationEvent is dispatched

[CAMEL-24064](https://issues.apache.org/jira/browse/CAMEL-24064)

camel-jackson3: type converter drops all but the last configured Jackson module and transformers let JacksonException escape unwrapped

[CAMEL-24062](https://issues.apache.org/jira/browse/CAMEL-24062)

UseOriginalAggregationStrategy silently ignored under Multicast (original never bound) — inconsistent with Splitter

[CAMEL-24061](https://issues.apache.org/jira/browse/CAMEL-24061)

camel-zeebe: grpc-stub-based operations were never wired for auth

[CAMEL-24060](https://issues.apache.org/jira/browse/CAMEL-24060)

camel-pqc: PQCMicrometerMetrics static reference breaks GraalVM native image compilation

[CAMEL-24055](https://issues.apache.org/jira/browse/CAMEL-24055)

QuartzEndpoint custom calendar name collision when multiple routes use customCalendar

[CAMEL-24052](https://issues.apache.org/jira/browse/CAMEL-24052)

dumpModelAsXml permanently destroys EndpointDSL builders on RouteDefinition

[CAMEL-24048](https://issues.apache.org/jira/browse/CAMEL-24048)

camel-sql - stale remove() silently completes in JdbcAggregationRepository; idempotent add() leaks DuplicateKeyException; TokenMgrError escapes stored template parser

[CAMEL-24047](https://issues.apache.org/jira/browse/CAMEL-24047)

camel-sql - verifyTableName rejects schema-qualified aggregation repository names (unreleased regression)

[CAMEL-24046](https://issues.apache.org/jira/browse/CAMEL-24046)

camel-sql - JdbcCachedMessageIdRepository: failed insert permanently poisons the cache; cache is not thread-safe

[CAMEL-24045](https://issues.apache.org/jira/browse/CAMEL-24045)

camel-sql - Connection leak with outputType=StreamList when the statement is not a query

[CAMEL-24044](https://issues.apache.org/jira/browse/CAMEL-24044)

camel-sql - Postgres aggregation repositories fail on insert: version bound without a placeholder

[CAMEL-24004](https://issues.apache.org/jira/browse/CAMEL-24004)

camel-restdsl-openapi-plugin - Generated YAML REST DSL omits required type field on param definitions

[CAMEL-24001](https://issues.apache.org/jira/browse/CAMEL-24001)

RestBindingAdvice.ensureHeaderContentType() sets Content-Type on body-less (e.g. 204) responses, and falls back to a raw multi-value "produces" list instead of a single media type

[CAMEL-23999](https://issues.apache.org/jira/browse/CAMEL-23999)

camel-spring-boot - Jars no longer contain spring-configuration-metadata.json after maven-compiler-plugin 3.15.0 upgrade

[CAMEL-23997](https://issues.apache.org/jira/browse/CAMEL-23997)

camel-kafka: medium-severity findings from code review (config, consumer, producer batch mode, transforms)

[CAMEL-23996](https://issues.apache.org/jira/browse/CAMEL-23996)

camel-kafka: KafkaIdempotentRepository and SingleNodeKafkaResumeStrategy correctness issues

[CAMEL-23995](https://issues.apache.org/jira/browse/CAMEL-23995)

camel-kafka: saslAuthType overrides explicit securityProtocol and generates non-working KERBEROS/OAUTH/AWS\_MSK\_IAM configurations

[CAMEL-23994](https://issues.apache.org/jira/browse/CAMEL-23994)

camel-kafka: consumer offset-handling bugs causing silent message loss (resume adapter, pollOnError seek, batching commit, offset repository)

[CAMEL-23992](https://issues.apache.org/jira/browse/CAMEL-23992)

camel-yaml-dsl-maven-plugin - GenerateYamlSchemaMojo.extractRequiredFromComposition has inverted $ref check: NPE on the branch it guards, no-op on the intended one

[CAMEL-23991](https://issues.apache.org/jira/browse/CAMEL-23991)

camel-yaml-dsl-validator-maven-plugin - application.yaml ignore check never matches, and static yamlFiles cache is unsafe under parallel builds and accumulates across modules

[CAMEL-23990](https://issues.apache.org/jira/browse/CAMEL-23990)

camel-yaml-dsl-validator - error messages fed to new MessageFormat(...): a '{' in the parse error crashes the validator instead of reporting

[CAMEL-23989](https://issues.apache.org/jira/browse/CAMEL-23989)

camel-yaml-dsl - YamlDeserializerSupport.nodeAt() matches later pointer segments at the wrong depth instead of returning null

[CAMEL-23988](https://issues.apache.org/jira/browse/CAMEL-23988)

camel-yaml-dsl - nested-map endpoint parameters (multiValue, CAMEL-22486) produce a corrupt URI unless the endpoint URI is scheme-only

[CAMEL-23987](https://issues.apache.org/jira/browse/CAMEL-23987)

camel-yaml-dsl - note property rejected on top-level from, routeConfiguration and kamelet (CAMEL-22576 asymmetry)

[CAMEL-23986](https://issues.apache.org/jira/browse/CAMEL-23986)

camel-yaml-dsl - routeConfiguration loses line number, source location and resource (construct() bypasses onNewTarget)

[CAMEL-23985](https://issues.apache.org/jira/browse/CAMEL-23985)

camel-yaml-dsl - Pipe preConfigurePipe lacks validation: unsupported ref kinds yield null/"null?params" endpoint URIs, NPE on sink without endpoint, IOOBE on empty errorHandler

[CAMEL-23984](https://issues.apache.org/jira/browse/CAMEL-23984)

camel-yaml-dsl - unsupported top-level mapping YAML is silently ignored: application starts with zero routes and no diagnostic

[CAMEL-23983](https://issues.apache.org/jira/browse/CAMEL-23983)

camel-yaml-dsl-maven-plugin - @YamlProperty flag emission broken: withRequired(isDeprecated) typo drops required/deprecated on non-String properties, secret never emits format=password

[CAMEL-23982](https://issues.apache.org/jira/browse/CAMEL-23982)

camel-yaml-dsl - shared bean cache cleared globally after each configure() causes beans to be created twice when loading multiple YAML files

[CAMEL-23981](https://issues.apache.org/jira/browse/CAMEL-23981)

camel-yaml-dsl - springTransactionErrorHandler constructs JtaTransactionErrorHandlerDefinition instead of SpringTransactionErrorHandlerDefinition

[CAMEL-23974](https://issues.apache.org/jira/browse/CAMEL-23974)

camel-zeebe: OAuth clientId/clientSecret/oAuthAPI configured on ZeebeComponent are never passed to ZeebeService, so no authentication occurs

[CAMEL-23962](https://issues.apache.org/jira/browse/CAMEL-23962)

camel-openai: McpToolConverter drops JSON Schema keywords beyond type/properties/required

[CAMEL-23961](https://issues.apache.org/jira/browse/CAMEL-23961)

camel-openai: empty choices array from an OpenAI-compatible provider fails with raw IndexOutOfBoundsException

[CAMEL-23960](https://issues.apache.org/jira/browse/CAMEL-23960)

camel-openai: unresolvable outputClass is silently ignored instead of failing

[CAMEL-23959](https://issues.apache.org/jira/browse/CAMEL-23959)

camel-openai: storeFullResponse is silently ignored by the embeddings operation

[CAMEL-23958](https://issues.apache.org/jira/browse/CAMEL-23958)

camel-openai: duplicate MCP tool names from multiple servers are all sent to the model

[CAMEL-23957](https://issues.apache.org/jira/browse/CAMEL-23957)

camel-openai: MCP reconnect mutates shared endpoint tool state without synchronization

[CAMEL-23956](https://issues.apache.org/jira/browse/CAMEL-23956)

camel-openai: malformed tool-call arguments crash the agentic loop instead of being returned to the model

[CAMEL-23955](https://issues.apache.org/jira/browse/CAMEL-23955)

camel-openai: conversation memory never persists user turns and the systemMessage reset is a no-op

[CAMEL-23949](https://issues.apache.org/jira/browse/CAMEL-23949)

camel-langchain4j-embeddingstore: ADD without embedding header calls EmbeddingStore.add(null) instead of failing

[CAMEL-23948](https://issues.apache.org/jira/browse/CAMEL-23948)

camel-langchain4j-agent: mcpToolProviderFilter not applied to endpoint-level MCP clients

[CAMEL-23947](https://issues.apache.org/jira/browse/CAMEL-23947)

camel-langchain4j-chat: remove unwired model builder helpers (logResponses silently dropped)

[CAMEL-23946](https://issues.apache.org/jira/browse/CAMEL-23946)

camel-langchain4j-web-search: safeSearch option is ignored - safe search cannot be disabled

[CAMEL-23945](https://issues.apache.org/jira/browse/CAMEL-23945)

camel-langchain4j-agent: producer race on shared agent field in agentFactory mode (fix needed on camel-4.18.x)

[CAMEL-23944](https://issues.apache.org/jira/browse/CAMEL-23944)

camel-langchain4j-agent: ToolExecutionErrorHandler and compensateOnToolErrors never invoked for Camel route tools

[CAMEL-23943](https://issues.apache.org/jira/browse/CAMEL-23943)

camel-langchain4j-tools: unbounded tool-calling loop, crash on hallucinated tool names, tool errors swallowed

[CAMEL-23939](https://issues.apache.org/jira/browse/CAMEL-23939)

Dependencies defined on Kamelet are ignored in Camel CLI

[CAMEL-23936](https://issues.apache.org/jira/browse/CAMEL-23936)

\[camel-http\] logHttpActivity cause exception on gzip encoded responses

[CAMEL-23914](https://issues.apache.org/jira/browse/CAMEL-23914)

camel-jbang export fails with TypeConversionException when kamelet has optional Long property

[CAMEL-23895](https://issues.apache.org/jira/browse/CAMEL-23895)

\[camel-azure-servicebus\] http 401 using connection string

[CAMEL-23883](https://issues.apache.org/jira/browse/CAMEL-23883)

Camel Kafka producer fails silently on unexpected message body type

[CAMEL-23881](https://issues.apache.org/jira/browse/CAMEL-23881)

camel-jbang export generates invalid Maven POM with literal \\$\\{citrus.version} instead of ${citrus.version}

[CAMEL-23877](https://issues.apache.org/jira/browse/CAMEL-23877)

camel-pinecone: tls option runtime default does not match its documented defaultValue

[CAMEL-23851](https://issues.apache.org/jira/browse/CAMEL-23851)

camel debug - breakpoint on first EIP incorrectly stops at route input

[CAMEL-23844](https://issues.apache.org/jira/browse/CAMEL-23844)

Camel-PQC: extractSecretKeyFromEncapsulation uses the raw enum name instead of the mapped JCE algorithm name

[CAMEL-23843](https://issues.apache.org/jira/browse/CAMEL-23843)

Camel-PQC: sign/verify only handle String payloads and use the platform default charset

[CAMEL-23842](https://issues.apache.org/jira/browse/CAMEL-23842)

Camel-PQC: PQCDataFormat uses ECB mode without integrity protection (use authenticated encryption)

[CAMEL-23840](https://issues.apache.org/jira/browse/CAMEL-23840)

pollEnrich with cacheSize(-1) does not disable consumer cache (dynamic endpoints)

[CAMEL-23838](https://issues.apache.org/jira/browse/CAMEL-23838)

camel-jbang TUI: F1/? help broken - NoClassDefFoundError from commonmark version conflict and ? not bound

### Dependency upgrade (5)

[CAMEL-24239](https://issues.apache.org/jira/browse/CAMEL-24239)

camel-jbang - Upgrade to jkube 1.20

[CAMEL-24212](https://issues.apache.org/jira/browse/CAMEL-24212)

camel-spring - Upgrade to spring-ai 2.0.x

[CAMEL-23562](https://issues.apache.org/jira/browse/CAMEL-23562)

Upgrade smack to 4.4.x

[CAMEL-23482](https://issues.apache.org/jira/browse/CAMEL-23482)

Upgrade weaviate client to 6.x

[CAMEL-23241](https://issues.apache.org/jira/browse/CAMEL-23241)

Upgrade minio to 9+

### Improvement (152)

[CAMEL-24366](https://issues.apache.org/jira/browse/CAMEL-24366)

langchain4j-embeddingstore: Add embeddingModel auto-embed support

[CAMEL-24362](https://issues.apache.org/jira/browse/CAMEL-24362)

Generate YAML DSL completion tree from canonical schema and catalog metadata

[CAMEL-24359](https://issues.apache.org/jira/browse/CAMEL-24359)

camel-atmosphere-websocket - align Exchange header constant names with Camel naming convention

[CAMEL-24336](https://issues.apache.org/jira/browse/CAMEL-24336)

camel-main metadata generator should detect Java enum types for cluster/vault TimeUnit options

[CAMEL-24334](https://issues.apache.org/jira/browse/CAMEL-24334)

camel-ai-tool - raw JSON Schema tool input (argSchema) for nested parameters

[CAMEL-24332](https://issues.apache.org/jira/browse/CAMEL-24332)

camel-ai-tool - MCP tool annotations (readOnly/destructive/idempotent hints) as endpoint metadata

[CAMEL-24330](https://issues.apache.org/jira/browse/CAMEL-24330)

Improve AI component documentation based on real-world user feedback

[CAMEL-24328](https://issues.apache.org/jira/browse/CAMEL-24328)

camel-jfr - Show JFR runtime event data in TUI JFR tab

[CAMEL-24321](https://issues.apache.org/jira/browse/CAMEL-24321)

Stream caching: allow the spool directory to be resolved per-Exchange

[CAMEL-24319](https://issues.apache.org/jira/browse/CAMEL-24319)

camel-keycloak: optional token type (typ) and authorized party (azp) validation in KeycloakSecurityPolicy

[CAMEL-24299](https://issues.apache.org/jira/browse/CAMEL-24299)

camel-core: set SUPPORT\_DTD=false in XmlStreamDetector for consistency with other XML parsers

[CAMEL-24298](https://issues.apache.org/jira/browse/CAMEL-24298)

Add an optional component/scheme allow-list to dynamic-URI EIPs (toD, recipientList, routingSlip, dynamicRouter, enrich, pollEnrich)

[CAMEL-24297](https://issues.apache.org/jira/browse/CAMEL-24297)

camel-ldif: add an opt-in for treating the message body as a URL to fetch

[CAMEL-24296](https://issues.apache.org/jira/browse/CAMEL-24296)

camel-core: allow configuring a JEP-290 ObjectInputFilter on CamelObjectInputStream

[CAMEL-24294](https://issues.apache.org/jira/browse/CAMEL-24294)

camel-snakeyaml: align TrustedTagInspector with the typeFilters allow-list

[CAMEL-24293](https://issues.apache.org/jira/browse/CAMEL-24293)

Strip path segments from externally-derived filenames before setting CamelFileName (platform-http-vertx, zipfile, tarfile)

[CAMEL-24291](https://issues.apache.org/jira/browse/CAMEL-24291)

camel-jsch and camel-ssh: align host-key checking option metadata with camel-ftp

[CAMEL-24288](https://issues.apache.org/jira/browse/CAMEL-24288)

Add IBM watsonx (Bob AI) support for TUI/CLI AI prompt (F8)

[CAMEL-24282](https://issues.apache.org/jira/browse/CAMEL-24282)

Resolve dynamic-URI property placeholders at build time instead of per message

[CAMEL-24281](https://issues.apache.org/jira/browse/CAMEL-24281)

camel-platform-http-main: fail closed when JWT authentication is enabled without an issuer or audience

[CAMEL-24279](https://issues.apache.org/jira/browse/CAMEL-24279)

camel-google-storage: contain downloadFileName downloads within the configured directory

[CAMEL-24278](https://issues.apache.org/jira/browse/CAMEL-24278)

camel-support - BackgroundTask should keep task registered in TaskManagerRegistry during blocking run

[CAMEL-24276](https://issues.apache.org/jira/browse/CAMEL-24276)

camel-tui: Add Azure OpenAI and GitHub Models support for AI prompt

[CAMEL-24275](https://issues.apache.org/jira/browse/CAMEL-24275)

camel-tui: Add Google Gemini native API support for AI prompt

[CAMEL-24274](https://issues.apache.org/jira/browse/CAMEL-24274)

camel-tui - Send Message should use camel-http to send to platform-http routes

[CAMEL-24272](https://issues.apache.org/jira/browse/CAMEL-24272)

Use BackgroundTask instead of ForegroundTask for reconnection loops so they are visible in internal tasks

[CAMEL-24271](https://issues.apache.org/jira/browse/CAMEL-24271)

camel-kafka - Use BackgroundTask for reconnection so it is visible in internal tasks

[CAMEL-24266](https://issues.apache.org/jira/browse/CAMEL-24266)

Delayer.delayValue has reverse-direction JMM visibility gap

[CAMEL-24265](https://issues.apache.org/jira/browse/CAMEL-24265)

DefaultTracer.traceCounter should use AtomicLong instead of plain long

[CAMEL-24260](https://issues.apache.org/jira/browse/CAMEL-24260)

camel-spring-boot - Dev console to expose Spring Boot configuration metadata for TUI quick docs

[CAMEL-24259](https://issues.apache.org/jira/browse/CAMEL-24259)

camel-jbang - TUI add tabs for more dev-consoles

[CAMEL-24258](https://issues.apache.org/jira/browse/CAMEL-24258)

camel-microprofile-fault-tolerance - Clean up dead code and improve JMX/observability parity

[CAMEL-24256](https://issues.apache.org/jira/browse/CAMEL-24256)

DefaultMaskingFormatter/SensitiveUtils: mask connection-string userinfo credentials and PEM private-key blocks

[CAMEL-24254](https://issues.apache.org/jira/browse/CAMEL-24254)

camel tui - Add history to shell and ai prompt

[CAMEL-24250](https://issues.apache.org/jira/browse/CAMEL-24250)

camel-spring-boot: Support component camel-cyberark-vault

[CAMEL-24240](https://issues.apache.org/jira/browse/CAMEL-24240)

camel-fhir: Align all FHIR core dependencies

[CAMEL-24237](https://issues.apache.org/jira/browse/CAMEL-24237)

camel-jbang - Add mcp tool for full docs avail from catalog

[CAMEL-24236](https://issues.apache.org/jira/browse/CAMEL-24236)

camel-cyberark-vault: add support for cyberark policies

[CAMEL-24233](https://issues.apache.org/jira/browse/CAMEL-24233)

camel-catalog - Include component and EIP documentation (adoc) in the catalog JAR

[CAMEL-24227](https://issues.apache.org/jira/browse/CAMEL-24227)

Add volatile to JMX-writable fields read on routing threads

[CAMEL-24226](https://issues.apache.org/jira/browse/CAMEL-24226)

camel export - support --resource-dirs to copy directories into src/main/resources preserving structure

[CAMEL-24223](https://issues.apache.org/jira/browse/CAMEL-24223)

Camel JBang MCP Server - Add camel\_route\_cost\_estimate tool for API cost estimation

[CAMEL-24222](https://issues.apache.org/jira/browse/CAMEL-24222)

Camel JBang MCP Server - Add camel\_dependency\_security\_audit tool for CVE analysis

[CAMEL-24221](https://issues.apache.org/jira/browse/CAMEL-24221)

Camel JBang MCP Server - Add camel\_runtime\_ai\_trace tool for AI exchange tracing

[CAMEL-24220](https://issues.apache.org/jira/browse/CAMEL-24220)

Camel JBang MCP Server - Add camel\_security\_scan tool for route security analysis

[CAMEL-24219](https://issues.apache.org/jira/browse/CAMEL-24219)

Camel JBang MCP Server - Add camel\_ai\_pipeline\_scaffold tool

[CAMEL-24218](https://issues.apache.org/jira/browse/CAMEL-24218)

Camel JBang MCP Server - Add Security-First execution layer

[CAMEL-24210](https://issues.apache.org/jira/browse/CAMEL-24210)

camel-openai: secrets passed via additionalHeader.\* are not redacted from sanitized URIs

[CAMEL-24209](https://issues.apache.org/jira/browse/CAMEL-24209)

Circuit Breaker EIP - true async processing with CompletionStage decorators

[CAMEL-24199](https://issues.apache.org/jira/browse/CAMEL-24199)

camel-jbang - Upgrade to 0.141.x

[CAMEL-24198](https://issues.apache.org/jira/browse/CAMEL-24198)

camel-azure-eventhubs - Redesign checkpoint store to use per-partition batching

[CAMEL-24192](https://issues.apache.org/jira/browse/CAMEL-24192)

camel-lra: Separate compensation/completion URI allowlists and prune on route removal

[CAMEL-24188](https://issues.apache.org/jira/browse/CAMEL-24188)

camel-jbang - Promote to stable

[CAMEL-24185](https://issues.apache.org/jira/browse/CAMEL-24185)

Circuit Breaker EIP - suspend/resume should preserve breaker state

[CAMEL-24173](https://issues.apache.org/jira/browse/CAMEL-24173)

camel-spring-rabbitmq: Cannot connect to latest rabbitmq server with autoDeclare=true due to deprecated feature

[CAMEL-24137](https://issues.apache.org/jira/browse/CAMEL-24137)

Circuit Breaker EIP - modernization umbrella (drop vavr, async completion, virtual threads, duration units, breaker events)

[CAMEL-24127](https://issues.apache.org/jira/browse/CAMEL-24127)

Fix flaky tests: Elasticsearch, LoopNoBreakOnShutdown, Hazelcast, LRA, OTel

[CAMEL-24126](https://issues.apache.org/jira/browse/CAMEL-24126)

Ensure no message sent before the VertxWebsocket is fully configured

[CAMEL-24125](https://issues.apache.org/jira/browse/CAMEL-24125)

camel-console - Expose dev console API contract via OpenAPI spec at /q/dev/api

[CAMEL-24119](https://issues.apache.org/jira/browse/CAMEL-24119)

camel-rest-openapi & camel-openapi-java: structural improvements from the July 2026 code review - umbrella

[CAMEL-24085](https://issues.apache.org/jira/browse/CAMEL-24085)

camel-ironmq: apply header filter strategy when mapping message envelope headers

[CAMEL-24084](https://issues.apache.org/jira/browse/CAMEL-24084)

camel-knative: apply header filter strategy to structured-mode CloudEvent extension headers

[CAMEL-24063](https://issues.apache.org/jira/browse/CAMEL-24063)

Fix flaky tests: JMS, Seda, Disruptor, Scheduler, and Direct timing issues

[CAMEL-24059](https://issues.apache.org/jira/browse/CAMEL-24059)

camel-wasm - Migrate to endive

[CAMEL-24056](https://issues.apache.org/jira/browse/CAMEL-24056)

camel-kafka - Mark sslEndpointAlgorithm as security=insecure:ssl

[CAMEL-24054](https://issues.apache.org/jira/browse/CAMEL-24054)

EvalLanguageDevConsole - Add POST method support and exchange variables

[CAMEL-24049](https://issues.apache.org/jira/browse/CAMEL-24049)

Fix flaky JMS Spring tests - queue name isolation and readiness checks (batch 12)

[CAMEL-24032](https://issues.apache.org/jira/browse/CAMEL-24032)

Add rolling 1-minute exchange rate to performance counters

[CAMEL-24025](https://issues.apache.org/jira/browse/CAMEL-24025)

camel-observability-services-starter: ship defaults via EnvironmentPostProcessor instead of config/application.properties so users can override them

[CAMEL-24003](https://issues.apache.org/jira/browse/CAMEL-24003)

BacklogTracer - Add activity queue to retain last N completed exchange summaries

[CAMEL-24002](https://issues.apache.org/jira/browse/CAMEL-24002)

camel cmd send exits 0 on failure; Terminated launcher entries make integration names ambiguous for exported runtimes

[CAMEL-24000](https://issues.apache.org/jira/browse/CAMEL-24000)

camel-spring-boot - Align core auto-configuration with Spring Boot 4 idioms

[CAMEL-23979](https://issues.apache.org/jira/browse/CAMEL-23979)

camel-jbang-mcp: expose CVE security advisories as MCP tool and resources

[CAMEL-23976](https://issues.apache.org/jira/browse/CAMEL-23976)

Add percentile latency statistics (p50/p95/p99) to Extended management statistics

[CAMEL-23973](https://issues.apache.org/jira/browse/CAMEL-23973)

camel export: add --parent-pom option to set parent POM in exported project

[CAMEL-23971](https://issues.apache.org/jira/browse/CAMEL-23971)

BaseOrderedProperties missing containsKey/contains/containsValue overrides

[CAMEL-23968](https://issues.apache.org/jira/browse/CAMEL-23968)

camel-openai: expose SDK client request timeout, max retries and custom request headers

[CAMEL-23964](https://issues.apache.org/jira/browse/CAMEL-23964)

camel-openai: MCP tool filtering per endpoint

[CAMEL-23963](https://issues.apache.org/jira/browse/CAMEL-23963)

camel-openai: configurable strategies for tool execution errors and hallucinated tool names in the agentic loop

[CAMEL-23952](https://issues.apache.org/jira/browse/CAMEL-23952)

camel-langchain4j-agent: support executeToolsConcurrently by making the Camel tool executor exchange-safe

[CAMEL-23951](https://issues.apache.org/jira/browse/CAMEL-23951)

camel-langchain4j-agent: expose Result.sources() and Result.toolExecutions() as message headers

[CAMEL-23942](https://issues.apache.org/jira/browse/CAMEL-23942)

camel-azure-storage-blob / camel-azure-storage-datalake: contain fileDir downloads within the configured directory

[CAMEL-23941](https://issues.apache.org/jira/browse/CAMEL-23941)

camel-platform-http-main: fail closed under prod when auth enabled without mechanism

[CAMEL-23935](https://issues.apache.org/jira/browse/CAMEL-23935)

camel-jbang - Route diagram - the mini tree should update

[CAMEL-23934](https://issues.apache.org/jira/browse/CAMEL-23934)

camel tui - Light theme has some colors hard to red

[CAMEL-23933](https://issues.apache.org/jira/browse/CAMEL-23933)

camel-tooling-maven depends on deprecated maven-resolver-supplier causing classpath conflicts with maven-resolver-supplier-mvn3

[CAMEL-23931](https://issues.apache.org/jira/browse/CAMEL-23931)

Apache Camel SFTP Consumer: pre-sort by last-modified time without creating Exchange objects for all files on server

[CAMEL-23927](https://issues.apache.org/jira/browse/CAMEL-23927)

Camel Kafka: metadataMaxAgeMs @UriParam label should be "common" instead of "producer"

[CAMEL-23923](https://issues.apache.org/jira/browse/CAMEL-23923)

Fix flaky tests in camel-syslog using Thread.sleep

[CAMEL-23921](https://issues.apache.org/jira/browse/CAMEL-23921)

Fix flaky tests in camel-mina-sftp

[CAMEL-23917](https://issues.apache.org/jira/browse/CAMEL-23917)

Fix flaky QuartzNameCollisionTest in camel-quartz

[CAMEL-23915](https://issues.apache.org/jira/browse/CAMEL-23915)

Fix flaky MockEndpointTimeClauseTest in camel-core

[CAMEL-23913](https://issues.apache.org/jira/browse/CAMEL-23913)

camel-uti - Add catalog tab

[CAMEL-23912](https://issues.apache.org/jira/browse/CAMEL-23912)

camel tui - Add tab to show maven dependencies

[CAMEL-23911](https://issues.apache.org/jira/browse/CAMEL-23911)

camel-jbang - TUI should support configuring HTTP proxy settings

[CAMEL-23910](https://issues.apache.org/jira/browse/CAMEL-23910)

camel-jbang - Quarkus version is now resolved automatic

[CAMEL-23898](https://issues.apache.org/jira/browse/CAMEL-23898)

TUI Configuration tab: add row selection with property details panel from Camel catalog

[CAMEL-23897](https://issues.apache.org/jira/browse/CAMEL-23897)

PropertiesDevConsole should show application properties from all runtimes (Spring Boot, Quarkus)

[CAMEL-23891](https://issues.apache.org/jira/browse/CAMEL-23891)

camel-mail: apply inbound Camel\* header filtering in MimeMultipartDataFormat unmarshal (headersInline=true), consistent with the mail consumer

[CAMEL-23882](https://issues.apache.org/jira/browse/CAMEL-23882)

camel - improve llms.txt for better AI assistance

[CAMEL-23879](https://issues.apache.org/jira/browse/CAMEL-23879)

Add SecureRandomHelper to camel-util, consolidate all SecureRandom usage

[CAMEL-23876](https://issues.apache.org/jira/browse/CAMEL-23876)

camel-a2a: pin the validated address when dispatching push-notification webhooks

[CAMEL-23875](https://issues.apache.org/jira/browse/CAMEL-23875)

camel-keycloak: add optional audience (aud) validation to token verification

[CAMEL-23874](https://issues.apache.org/jira/browse/CAMEL-23874)

DevConsole - add option metadata so consoles can declare supported options

[CAMEL-23871](https://issues.apache.org/jira/browse/CAMEL-23871)

camel-jbang - export to have option to exclude Docker generation

[CAMEL-23870](https://issues.apache.org/jira/browse/CAMEL-23870)

Add HeapHistogram dev console and TUI panel for class-level memory analysis

[CAMEL-23869](https://issues.apache.org/jira/browse/CAMEL-23869)

camel-jbang TUI - Add vulnerability scanning panel using OSV.dev

[CAMEL-23868](https://issues.apache.org/jira/browse/CAMEL-23868)

camel-file: make local work directory / starting directory containment checks path-boundary aware

[CAMEL-23867](https://issues.apache.org/jira/browse/CAMEL-23867)

camel tui - Add settings

[CAMEL-23865](https://issues.apache.org/jira/browse/CAMEL-23865)

LoadThroughput should use EWMA smoothing like LoadTriplet instead of instantaneous delta

[CAMEL-23862](https://issues.apache.org/jira/browse/CAMEL-23862)

Camel TUI - Add SQL Trace tab for tracking SQL query performance

[CAMEL-23860](https://issues.apache.org/jira/browse/CAMEL-23860)

camel-langchain4j-chat/agent/tools - Add token usage and finish reason as exchange headers

[CAMEL-23859](https://issues.apache.org/jira/browse/CAMEL-23859)

camel-weaviate: Add BATCH\_CREATE, HYBRID\_QUERY, BM25\_QUERY, and AGGREGATE operations

[CAMEL-23858](https://issues.apache.org/jira/browse/CAMEL-23858)

camel-spring-boot - Configuring camel.main.profile should be supported

[CAMEL-23857](https://issues.apache.org/jira/browse/CAMEL-23857)

camel-jbang - TUI allow to choose runtime when running from folder or examples

[CAMEL-23855](https://issues.apache.org/jira/browse/CAMEL-23855)

camel-jbang - TUI - Add F8 AI prompt panel when running with --mcp mode

[CAMEL-23853](https://issues.apache.org/jira/browse/CAMEL-23853)

Support --mcp flag on camel run/dev to embed MCP server in running Camel application

[CAMEL-23852](https://issues.apache.org/jira/browse/CAMEL-23852)

Add camel mcp CLI command

[CAMEL-23850](https://issues.apache.org/jira/browse/CAMEL-23850)

camel-diagram - Route diagram and topology - dump from source file

[CAMEL-23847](https://issues.apache.org/jira/browse/CAMEL-23847)

Camel-PQC: support streaming sign/verify for large payloads

[CAMEL-23845](https://issues.apache.org/jira/browse/CAMEL-23845)

Camel-PQC: implement InMemoryKeyLifecycleManager (currently documented but missing)

[CAMEL-23841](https://issues.apache.org/jira/browse/CAMEL-23841)

camel-jbang - TUI layout overflow at 120 columns (tab bar, footer, minimum size)

[CAMEL-23839](https://issues.apache.org/jira/browse/CAMEL-23839)

camel-jbang: switchable light/dark CSS theme for the TUI

[CAMEL-23829](https://issues.apache.org/jira/browse/CAMEL-23829)

camel-jbang - TUI shell panel: add a scrollbar to indicate scrollback position

[CAMEL-23815](https://issues.apache.org/jira/browse/CAMEL-23815)

camel-support: provide a shared ObjectInputFilter deserialization-filter resolver to deduplicate it across the HTTP/JMS/Netty components

[CAMEL-23768](https://issues.apache.org/jira/browse/CAMEL-23768)

camel-keycloak: select the JWKS verification key by the token kid

[CAMEL-23766](https://issues.apache.org/jira/browse/CAMEL-23766)

camel-crypto: use a constant-time comparison for HMAC verification in HMACAccumulator

[CAMEL-23727](https://issues.apache.org/jira/browse/CAMEL-23727)

camel-jbang - TUI shell panel improvements

[CAMEL-23720](https://issues.apache.org/jira/browse/CAMEL-23720)

camel-jbang - New look and feel

[CAMEL-23654](https://issues.apache.org/jira/browse/CAMEL-23654)

camel-jbang - Group commands in --help output for better navigation

[CAMEL-23628](https://issues.apache.org/jira/browse/CAMEL-23628)

camel-jbang - Organize commands in catgories

[CAMEL-23530](https://issues.apache.org/jira/browse/CAMEL-23530)

camel-dataweave - Move to indivdual component for better reuse

[CAMEL-23465](https://issues.apache.org/jira/browse/CAMEL-23465)

Camel-AWS-Bedrock: BedrockAgentRuntimeConfiguration.modelId enum lists only retired Anthropic Claude models

[CAMEL-23460](https://issues.apache.org/jira/browse/CAMEL-23460)

camel-telemetry - Add span decorators for Google Cloud

[CAMEL-23453](https://issues.apache.org/jira/browse/CAMEL-23453)

camel-keycloak: Add federated identity linking operations

[CAMEL-23441](https://issues.apache.org/jira/browse/CAMEL-23441)

camel-jbang - Export to support install camel wrapper

[CAMEL-23431](https://issues.apache.org/jira/browse/CAMEL-23431)

Migrate AS2 and other component tests from AvailablePortFinder to port-0 ServerSocket binding

[CAMEL-23394](https://issues.apache.org/jira/browse/CAMEL-23394)

camel-openai: Add conversation history size management to prevent context overflow

[CAMEL-23393](https://issues.apache.org/jira/browse/CAMEL-23393)

camel-openai: Add token budget enforcement to the MCP agentic loop

[CAMEL-23338](https://issues.apache.org/jira/browse/CAMEL-23338)

In Opensearch component, provide option to set OpenSearchClient

[CAMEL-23268](https://issues.apache.org/jira/browse/CAMEL-23268)

\[camel-jbang\] Wrapper command potential security permission issue

[CAMEL-23264](https://issues.apache.org/jira/browse/CAMEL-23264)

Enhance Splitter EIP with chunking, error threshold, failure tracking, and watermark support

[CAMEL-23226](https://issues.apache.org/jira/browse/CAMEL-23226)

Improve Camel JBang CLI user experience

[CAMEL-23218](https://issues.apache.org/jira/browse/CAMEL-23218)

camel-couchbase: Migrate consumer from deprecated MapReduce Views to SQL++ (N1QL) queries

[CAMEL-23117](https://issues.apache.org/jira/browse/CAMEL-23117)

camel-test-infra - Add infra for postregres with vector extension instsalled

[CAMEL-23096](https://issues.apache.org/jira/browse/CAMEL-23096)

camel-ssh - expose more CoreModuleProperties

[CAMEL-23078](https://issues.apache.org/jira/browse/CAMEL-23078)

camel-openai: MCP improvements — parallel tool execution and runtime tool refresh

[CAMEL-22616](https://issues.apache.org/jira/browse/CAMEL-22616)

camel-jbang - Add support for camel.cluster.xxx configurations

[CAMEL-22351](https://issues.apache.org/jira/browse/CAMEL-22351)

camel-main - Specify which option are required on vault configurations

[CAMEL-20428](https://issues.apache.org/jira/browse/CAMEL-20428)

Kafka Batch Consumer: Some common headers in the batch exchanges should be copied also to the original exchange

[CAMEL-20199](https://issues.apache.org/jira/browse/CAMEL-20199)

Complete support of Virtual Threads

[CAMEL-20141](https://issues.apache.org/jira/browse/CAMEL-20141)

camel-joor - Reloading compiled code should update beans created from inlined script

### New Feature (19)

[CAMEL-24287](https://issues.apache.org/jira/browse/CAMEL-24287)

camel-jbang-tui: Add plain text editor in source viewer for quick prototyping

[CAMEL-24255](https://issues.apache.org/jira/browse/CAMEL-24255)

camel-duckdb - A component for duckdb and test-infra

[CAMEL-24245](https://issues.apache.org/jira/browse/CAMEL-24245)

Camel-ClickHouse New Component Proposal

[CAMEL-24235](https://issues.apache.org/jira/browse/CAMEL-24235)

camel-jactl - A new language forjaclt

[CAMEL-24202](https://issues.apache.org/jira/browse/CAMEL-24202)

camel-tui - Run in web browser via web assembly

[CAMEL-23978](https://issues.apache.org/jira/browse/CAMEL-23978)

camel-jbang tui: AI panel Claude Code look, thinking animation, and Gemini/Azure OpenAI support

[CAMEL-23969](https://issues.apache.org/jira/browse/CAMEL-23969)

camel-openai: support the OpenAI Responses API

[CAMEL-23966](https://issues.apache.org/jira/browse/CAMEL-23966)

camel-openai: add audio speech (TTS) and audio translation operations

[CAMEL-23872](https://issues.apache.org/jira/browse/CAMEL-23872)

camel-tui - Add JFR Old Object Sample panel for memory leak diagnosis

[CAMEL-23849](https://issues.apache.org/jira/browse/CAMEL-23849)

Camel-PQC: add automated key rotation scheduling

[CAMEL-23848](https://issues.apache.org/jira/browse/CAMEL-23848)

Camel-PQC: add Micrometer metrics and observability for PQC operations and key state

[CAMEL-23846](https://issues.apache.org/jira/browse/CAMEL-23846)

Camel-PQC: make the PQC parameter set / NIST security level configurable on the endpoint

[CAMEL-23837](https://issues.apache.org/jira/browse/CAMEL-23837)

Add DataSource connection pool dev-console with HikariCP and Agroal support

[CAMEL-23831](https://issues.apache.org/jira/browse/CAMEL-23831)

camel-tui: add mouse support (tab clicks and scroll)

[CAMEL-23703](https://issues.apache.org/jira/browse/CAMEL-23703)

camel-cli - Distribute release to various 3rd-party package managers

[CAMEL-23467](https://issues.apache.org/jira/browse/CAMEL-23467)

Camel-AWS-Bedrock: Add support for InvokeAgent and InvokeInlineAgent operations in Bedrock Agent Runtime

[CAMEL-23383](https://issues.apache.org/jira/browse/CAMEL-23383)

Add JFR runtime instrumentation for exchanges, processors, and endpoints

[CAMEL-23382](https://issues.apache.org/jira/browse/CAMEL-23382)

Unified Camel AI tool abstraction for route-based tools across AI components

[CAMEL-18552](https://issues.apache.org/jira/browse/CAMEL-18552)

camel-jbang - Add q/openapi with swagger ui

### Sub-task (25)

[CAMEL-24329](https://issues.apache.org/jira/browse/CAMEL-24329)

camel-aws2-s3: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24326](https://issues.apache.org/jira/browse/CAMEL-24326)

camel-aws-config: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24324](https://issues.apache.org/jira/browse/CAMEL-24324)

camel-aws-bedrock (agent/agentruntime): throw when pojoRequest=true and the body is the wrong type

[CAMEL-24317](https://issues.apache.org/jira/browse/CAMEL-24317)

camel-aws2-eventbridge: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24316](https://issues.apache.org/jira/browse/CAMEL-24316)

camel-aws2-transcribe: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24314](https://issues.apache.org/jira/browse/CAMEL-24314)

Documentation: component page and security section

[CAMEL-24313](https://issues.apache.org/jira/browse/CAMEL-24313)

Tests: MCP SDK client IT and Spring Boot servlet SSE verification

[CAMEL-24312](https://issues.apache.org/jira/browse/CAMEL-24312)

MCP tool listing, invocation and notifications over AiToolRegistry

[CAMEL-24311](https://issues.apache.org/jira/browse/CAMEL-24311)

camel.server.mcp-\* configuration properties and camel-main autowiring

[CAMEL-24310](https://issues.apache.org/jira/browse/CAMEL-24310)

camel-mcp-server module: bridge, McpServerEngine SPI and default engine

[CAMEL-24309](https://issues.apache.org/jira/browse/CAMEL-24309)

AiToolRegistry listener SPI for tool registration changes

[CAMEL-24307](https://issues.apache.org/jira/browse/CAMEL-24307)

camel-aws2-rekognition: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24304](https://issues.apache.org/jira/browse/CAMEL-24304)

camel-aws2-step-functions: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24303](https://issues.apache.org/jira/browse/CAMEL-24303)

camel-aws2-redshift: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24302](https://issues.apache.org/jira/browse/CAMEL-24302)

camel-aws2-timestream: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24300](https://issues.apache.org/jira/browse/CAMEL-24300)

camel-aws2-ec2: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24289](https://issues.apache.org/jira/browse/CAMEL-24289)

camel-aws2-textract: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24285](https://issues.apache.org/jira/browse/CAMEL-24285)

camel-aws2-polly: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24283](https://issues.apache.org/jira/browse/CAMEL-24283)

camel-aws2-comprehend: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24280](https://issues.apache.org/jira/browse/CAMEL-24280)

camel-aws2-mq: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24277](https://issues.apache.org/jira/browse/CAMEL-24277)

camel-aws2-msk: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24264](https://issues.apache.org/jira/browse/CAMEL-24264)

camel-aws2-translate: throw when pojoRequest=true and the body is the wrong type

[CAMEL-24263](https://issues.apache.org/jira/browse/CAMEL-24263)

camel-aws2-sts: throw when pojoRequest=true and the body is the wrong type

[CAMEL-23358](https://issues.apache.org/jira/browse/CAMEL-23358)

\[JDK 26\] SSLContextParametersTest.testSignatureSchemesFilter is failing

[CAMEL-22538](https://issues.apache.org/jira/browse/CAMEL-22538)

Camel-PQC: Add Azure Key Vault Lifecycle Manager

### Task (34)

[CAMEL-24335](https://issues.apache.org/jira/browse/CAMEL-24335)

Update Artemis dependency groupId from \`org.apache.activemq to org.apache.artemis\`

[CAMEL-24318](https://issues.apache.org/jira/browse/CAMEL-24318)

Support Maven build and test using multiple cores

[CAMEL-24268](https://issues.apache.org/jira/browse/CAMEL-24268)

ThrottlingInflightRoutePolicy: resumeInflightExchanges field is write-only after holder refactoring

[CAMEL-24228](https://issues.apache.org/jira/browse/CAMEL-24228)

AGENTS.md - do not mention upgrade guide for new features

[CAMEL-24217](https://issues.apache.org/jira/browse/CAMEL-24217)

camel-main - Resilience4jConfigurationProperties Integer->String API break not in the 4.22 upgrade guide

[CAMEL-24215](https://issues.apache.org/jira/browse/CAMEL-24215)

camel-resilience4j - JMX waitDurationInOpenState still reports seconds while the option is now millis

[CAMEL-24214](https://issues.apache.org/jira/browse/CAMEL-24214)

camel-jbang - circuit-breaker example still uses seconds for waitDurationInOpenState (now millis)

[CAMEL-24211](https://issues.apache.org/jira/browse/CAMEL-24211)

Build is broken on jenkins to deploy Camel core snapshot

[CAMEL-24206](https://issues.apache.org/jira/browse/CAMEL-24206)

Removal of workaround for Apache fory --add-opens with Fory 1.4+

[CAMEL-24204](https://issues.apache.org/jira/browse/CAMEL-24204)

camel-jms - exposeListenerSession catalog metadata reports wrong default value (false instead of true)

[CAMEL-24184](https://issues.apache.org/jira/browse/CAMEL-24184)

camel-cxf - Umbrella: medium-severity findings from July 2026 code review

[CAMEL-24175](https://issues.apache.org/jira/browse/CAMEL-24175)

EIP documentation pages show incorrect "supports 0 options" count while options table lists options

[CAMEL-24081](https://issues.apache.org/jira/browse/CAMEL-24081)

CI - Do not run windows check

[CAMEL-23972](https://issues.apache.org/jira/browse/CAMEL-23972)

IBM MQ test infra does not handle unsupported Linux ARM64 centrally

[CAMEL-23970](https://issues.apache.org/jira/browse/CAMEL-23970)

camel-openai: annotate sslEndpointAlgorithm as an insecure-capable option per the security policy framework

[CAMEL-23932](https://issues.apache.org/jira/browse/CAMEL-23932)

Ensure AI agents are respecting the Git branch recommendations to not fill up the apache repo with outdated branches

[CAMEL-23890](https://issues.apache.org/jira/browse/CAMEL-23890)

Fix typos and casing issues in component descriptions

[CAMEL-23866](https://issues.apache.org/jira/browse/CAMEL-23866)

camel-aws2: Migrate AWS2 components to apache5-client

[CAMEL-23864](https://issues.apache.org/jira/browse/CAMEL-23864)

edi-x12-as2 and openapi/server JBang examples fail after YAML normalization

[CAMEL-23863](https://issues.apache.org/jira/browse/CAMEL-23863)

camel run --example=rest-api fails to start: invalid YAML in bundled rest-api example

[CAMEL-23732](https://issues.apache.org/jira/browse/CAMEL-23732)

camel-jbang - TUI cannot copy paste when mouse support

[CAMEL-23440](https://issues.apache.org/jira/browse/CAMEL-23440)

Replace usage of net.javacrumbs:spring-ws-test

[CAMEL-23439](https://issues.apache.org/jira/browse/CAMEL-23439)

camel-jbang - Add doc how to run MCP server without JBang

[CAMEL-23244](https://issues.apache.org/jira/browse/CAMEL-23244)

Remove deprecated component-specific CredentialType enums and migrate to shared camel-azure-common enum

[CAMEL-23135](https://issues.apache.org/jira/browse/CAMEL-23135)

camel-spring-boot-examples - Upgrade examples to use camel-jackson3-starter

[CAMEL-21955](https://issues.apache.org/jira/browse/CAMEL-21955)

Add Secrets Dev Console for IBM Secrets Manager

[CAMEL-21933](https://issues.apache.org/jira/browse/CAMEL-21933)

Camel-AWS-Eventbridge: Review localstack tests for PutRule, PutEvents and RemoveTargets

[CAMEL-21314](https://issues.apache.org/jira/browse/CAMEL-21314)

camel-aws - Fix S3CopyObjectCustomerKeyIT.sendIn which is failing on main branch

[CAMEL-19548](https://issues.apache.org/jira/browse/CAMEL-19548)

camel-zookeeper-master: replace Thread.sleep in tests

[CAMEL-19545](https://issues.apache.org/jira/browse/CAMEL-19545)

camel-stream: replace Thread.sleep in tests

[CAMEL-19542](https://issues.apache.org/jira/browse/CAMEL-19542)

camel-sjms: replace Thread.sleep in tests

[CAMEL-19540](https://issues.apache.org/jira/browse/CAMEL-19540)

camel-pulsar: replace Thread.sleep in tests

[CAMEL-19528](https://issues.apache.org/jira/browse/CAMEL-19528)

camel-jpa: replace Thread.sleep in tests

[CAMEL-16789](https://issues.apache.org/jira/browse/CAMEL-16789)

camel-microprofile-faulttolerance: timeoutScheduledExecutorServiceRef and bulkHead\* to be deprecated ?

### Test (71)

[CAMEL-24323](https://issues.apache.org/jira/browse/CAMEL-24323)

MongoDbSslConnectionIT test is broken "message":"Could not find the file / in container"

[CAMEL-24284](https://issues.apache.org/jira/browse/CAMEL-24284)

SjmsConnectionRecoveryTest is very flaky on Jenkins CI

[CAMEL-24053](https://issues.apache.org/jira/browse/CAMEL-24053)

camel-openapi-rest-dsl-generator tests fail on Windows due to CRLF line endings in .txt fixtures

[CAMEL-24043](https://issues.apache.org/jira/browse/CAMEL-24043)

Fix flaky tests - batch 11 (postprocessor, flatpack, hazelcast, mail, test-junit5)

[CAMEL-24042](https://issues.apache.org/jira/browse/CAMEL-24042)

Fix flaky tests in camel-core - batch 10 (throttle, mock, task, timeout, file)

[CAMEL-24041](https://issues.apache.org/jira/browse/CAMEL-24041)

Fix flaky tests in camel-core - batch 9 (resequencer, seda, aggregator, redelivery)

[CAMEL-24040](https://issues.apache.org/jira/browse/CAMEL-24040)

Fix flaky tests - timing issues in seda, throttle, aggregation, file, and JMS tests (batch 8)

[CAMEL-24039](https://issues.apache.org/jira/browse/CAMEL-24039)

Fix flaky core tests - seda, scheduler, and redelivery tests (batch 7)

[CAMEL-24038](https://issues.apache.org/jira/browse/CAMEL-24038)

Fix flaky AsyncWiretapTest in camel-telemetry and camel-telemetry-dev

[CAMEL-24037](https://issues.apache.org/jira/browse/CAMEL-24037)

Fix flaky camel-core tests: TwoSchedulerTest, DistributedTimeoutTest, ThrottlingExceptionRoutePolicyOpenViaConfigTest

[CAMEL-24036](https://issues.apache.org/jira/browse/CAMEL-24036)

Fix flaky AsyncWiretapTest in camel-telemetry and camel-telemetry-dev

[CAMEL-24035](https://issues.apache.org/jira/browse/CAMEL-24035)

Fix flaky camel-core tests: TwoSchedulerTest, DistributedTimeoutTest, ThrottlingExceptionRoutePolicyOpenViaConfigTest

[CAMEL-24034](https://issues.apache.org/jira/browse/CAMEL-24034)

Fix flaky SingleMessageSameTopicIT - topic subscription wait too short

[CAMEL-24033](https://issues.apache.org/jira/browse/CAMEL-24033)

Fix flaky camel-core tests (SedaBlockWhenFullTest, FileConsumePollEnrichFileTest, ThrottlingExceptionRoutePolicyHalfOpenHandlerSedaTest, SplitterParallelAsyncProcessorIssueTest)

[CAMEL-24031](https://issues.apache.org/jira/browse/CAMEL-24031)

Fix flaky JmsAddAndRemoveRouteManagementIT

[CAMEL-24030](https://issues.apache.org/jira/browse/CAMEL-24030)

Fix flaky SchedulerNoPolledMessagesTest

[CAMEL-24029](https://issues.apache.org/jira/browse/CAMEL-24029)

Fix flaky camel-core tests using timed assertions

[CAMEL-24028](https://issues.apache.org/jira/browse/CAMEL-24028)

Fix flaky JmsTransactedDeadLetterChannelNotHandlerRollbackOnExceptionIT

[CAMEL-24027](https://issues.apache.org/jira/browse/CAMEL-24027)

Fix flaky InOutQueueProducerAsyncLoadTest

[CAMEL-24026](https://issues.apache.org/jira/browse/CAMEL-24026)

Fix flaky XsltFromFileExceptionTest

[CAMEL-24024](https://issues.apache.org/jira/browse/CAMEL-24024)

Fix flaky InOutQueueProducerAsyncLoadTest

[CAMEL-24020](https://issues.apache.org/jira/browse/CAMEL-24020)

Fix flaky SjmsConnectionRecoveryTest

[CAMEL-24019](https://issues.apache.org/jira/browse/CAMEL-24019)

Fix flaky VertxWebsocketHandshakeHeadersTest

[CAMEL-24018](https://issues.apache.org/jira/browse/CAMEL-24018)

Fix flaky OpensearchIndexIT - disk usage exceeded flood-stage watermark

[CAMEL-24017](https://issues.apache.org/jira/browse/CAMEL-24017)

Fix flaky DynamicRouteIT in camel-jms (3.8% failure rate)

[CAMEL-24016](https://issues.apache.org/jira/browse/CAMEL-24016)

Fix flaky JmsSpringLoadBalanceFailOverJMSIT (3.8% failure rate)

[CAMEL-24015](https://issues.apache.org/jira/browse/CAMEL-24015)

Fix flaky VertxPlatformHttpOAuthProfileTest (7% failure rate)

[CAMEL-24014](https://issues.apache.org/jira/browse/CAMEL-24014)

Fix flaky JmsDurableTopicIT (2.8% failure rate)

[CAMEL-24013](https://issues.apache.org/jira/browse/CAMEL-24013)

Fix flaky RawMailMessageTest (12.4% failure rate)

[CAMEL-24012](https://issues.apache.org/jira/browse/CAMEL-24012)

Fix flaky DynamicRouteIT in camel-jms (3.8% failure rate)

[CAMEL-24011](https://issues.apache.org/jira/browse/CAMEL-24011)

Fix flaky JmsSpringLoadBalanceFailOverJMSIT (3.8% failure rate)

[CAMEL-24009](https://issues.apache.org/jira/browse/CAMEL-24009)

Fix flaky JmsDurableTopicIT (2.8% failure rate)

[CAMEL-24008](https://issues.apache.org/jira/browse/CAMEL-24008)

Fix flaky RawMailMessageTest (12.4% failure rate)

[CAMEL-24006](https://issues.apache.org/jira/browse/CAMEL-24006)

Fix flaky JpaPollingConsumerLockEntityTest

[CAMEL-24005](https://issues.apache.org/jira/browse/CAMEL-24005)

Fix flaky JmsTransactedDeadLetterChannel\*RollbackOnExceptionIT tests

[CAMEL-23993](https://issues.apache.org/jira/browse/CAMEL-23993)

Flaky SpanPropagationUpstreamTest - SpanComparator missing tie-breaking on equal timestamps

[CAMEL-23980](https://issues.apache.org/jira/browse/CAMEL-23980)

Flaky test: JmsAddAndRemoveRouteManagementIT (14% failure rate on Develocity)

[CAMEL-23930](https://issues.apache.org/jira/browse/CAMEL-23930)

Fix flaky test failures in Azure Key Vault EventHub listener

[CAMEL-23926](https://issues.apache.org/jira/browse/CAMEL-23926)

Flaky test: ElasticsearchBulkIT due to shared index and NRT search gap

[CAMEL-23909](https://issues.apache.org/jira/browse/CAMEL-23909)

Flaky test: CxfConsumerPayLoadFaultMessageTest in camel-cxf-soap on JDK 25

[CAMEL-23908](https://issues.apache.org/jira/browse/CAMEL-23908)

Flaky test: BacklogTracerAggregateTest in camel-management

[CAMEL-23907](https://issues.apache.org/jira/browse/CAMEL-23907)

Flaky test: ThreadsRejectedExecutionTest in camel-core

[CAMEL-23906](https://issues.apache.org/jira/browse/CAMEL-23906)

Flaky test: DelayerWhileShutdownTest in camel-core

[CAMEL-23905](https://issues.apache.org/jira/browse/CAMEL-23905)

Flaky test: LRAFailuresIT in camel-lra

[CAMEL-23904](https://issues.apache.org/jira/browse/CAMEL-23904)

Flaky test: CamelBeanDumpTest in camel-jbang-core

[CAMEL-23903](https://issues.apache.org/jira/browse/CAMEL-23903)

Flaky test: RouteIdTransactedIT in camel-jms

[CAMEL-23902](https://issues.apache.org/jira/browse/CAMEL-23902)

Flaky test: UndertowWsConsumerRouteTest.echo in camel-undertow

[CAMEL-23901](https://issues.apache.org/jira/browse/CAMEL-23901)

Flaky test: MulticastParallelStreamingTimeoutTest in camel-core

[CAMEL-23900](https://issues.apache.org/jira/browse/CAMEL-23900)

Flaky test: RecipientListParallelStreamingTest in camel-core

[CAMEL-23899](https://issues.apache.org/jira/browse/CAMEL-23899)

Flaky test: LogWriterRollOverUpdateAsyncWithContentionTest in camel-wal

[CAMEL-23896](https://issues.apache.org/jira/browse/CAMEL-23896)

Flaky test: camel-sql surefire tests fail intermittently in CI

[CAMEL-23894](https://issues.apache.org/jira/browse/CAMEL-23894)

Fix flaky ExportTest and DependencyUpdateTest for Spring Boot runtime in camel-jbang-core

[CAMEL-23893](https://issues.apache.org/jira/browse/CAMEL-23893)

Flaky SpringFileWatcherTest.testDefaultConfig on JDK 25

[CAMEL-23892](https://issues.apache.org/jira/browse/CAMEL-23892)

Fix flaky camel-sql JDBC aggregate surefire tests on JDK 17 and JDK 25

[CAMEL-23889](https://issues.apache.org/jira/browse/CAMEL-23889)

Fix flaky camel-vertx-websocket surefire tests

[CAMEL-23888](https://issues.apache.org/jira/browse/CAMEL-23888)

Fix flaky camel-platform-http-vertx surefire tests

[CAMEL-23887](https://issues.apache.org/jira/browse/CAMEL-23887)

Flaky test: camel-sjms surefire tests fail intermittently in CI

[CAMEL-23886](https://issues.apache.org/jira/browse/CAMEL-23886)

Flaky test: NatsConsumerWithRedeliveryIT.testConsumer fails intermittently in CI

[CAMEL-23885](https://issues.apache.org/jira/browse/CAMEL-23885)

Flaky test: camel-mllp surefire tests fail intermittently in CI

[CAMEL-23884](https://issues.apache.org/jira/browse/CAMEL-23884)

Fix flaky NatsConsumerWithRedeliveryIT by using Awaitility

[CAMEL-23673](https://issues.apache.org/jira/browse/CAMEL-23673)

Camel JBang IT test 4.18.x stay stuck

[CAMEL-23499](https://issues.apache.org/jira/browse/CAMEL-23499)

FiletoFtps\* tests are broken

[CAMEL-23246](https://issues.apache.org/jira/browse/CAMEL-23246)

LumberjackDisconnectionTest.shouldDisconnectUponError is failing regularly

[CAMEL-23223](https://issues.apache.org/jira/browse/CAMEL-23223)

Regular failure of ManagedMessageHistoryAutoConfigIT

[CAMEL-23216](https://issues.apache.org/jira/browse/CAMEL-23216)

Several mina sftp tests are very flaky

[CAMEL-23215](https://issues.apache.org/jira/browse/CAMEL-23215)

SpringAiImageOllamaIT test stays blocked

[CAMEL-23205](https://issues.apache.org/jira/browse/CAMEL-23205)

Several OpenAI tests broken when not specifying embedding model

[CAMEL-23201](https://issues.apache.org/jira/browse/CAMEL-23201)

XsltInclude\* tests are regularly failing

[CAMEL-23129](https://issues.apache.org/jira/browse/CAMEL-23129)

Tests frozen in camel-core on Jenkisn CI

[CAMEL-22527](https://issues.apache.org/jira/browse/CAMEL-22527)

\[camel-jetty\] testEchoEndpoint and testJettyFailoverRoundRobin flaky tests

[CAMEL-21438](https://issues.apache.org/jira/browse/CAMEL-21438)

tests: investigate flaky tests on alternative platforms

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).