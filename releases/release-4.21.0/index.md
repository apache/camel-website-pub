# Apache camel 4.21.0 Release

## New and Noteworthy

This release is the new Camel 4.21.0 release.

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
      <version>4.21.0</version>
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
      <version>4.21.0</version>
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
| [apache-camel-4.21.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.21.0/apache-camel-4.21.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-src.zip.sha512) |
| [apache-camel-4.21.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.xml.sha512) |
| [apache-camel-4.21.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.21.0/apache-camel-4.21.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.21.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.21.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (70)

[CAMEL-23835](https://issues.apache.org/jira/browse/CAMEL-23835)

camel-launcher: 'camel tui' fails with "No BackendProvider found" because embedded plugins are loaded without a classloader

[CAMEL-23834](https://issues.apache.org/jira/browse/CAMEL-23834)

camel-smb forward slashes rejected on Windows System STATUS\_OBJECT\_NAME\_INVALID

[CAMEL-23824](https://issues.apache.org/jira/browse/CAMEL-23824)

camel-jbang - dependency list should always include version for Spring Boot and Quarkus runtimes

[CAMEL-23821](https://issues.apache.org/jira/browse/CAMEL-23821)

camel-jbang: camel validate plugin doesn't find any files

[CAMEL-23819](https://issues.apache.org/jira/browse/CAMEL-23819)

camel-milo (browse): NullPointerException in Camel Milo Browse with Siemens S7

[CAMEL-23818](https://issues.apache.org/jira/browse/CAMEL-23818)

camel tui: Actions menu (F2) leaves stray characters when scrolling over emoji rows

[CAMEL-23814](https://issues.apache.org/jira/browse/CAMEL-23814)

camel-core - Optional secret property placeholders in YAML DSL parameters not stripped due to RAW() wrapping

[CAMEL-23811](https://issues.apache.org/jira/browse/CAMEL-23811)

camel-micrometer: app.info gauge value uses weak reference causing NaN values

[CAMEL-23809](https://issues.apache.org/jira/browse/CAMEL-23809)

camel-diagram - the html diagram has garbage chars in the metrics

[CAMEL-23805](https://issues.apache.org/jira/browse/CAMEL-23805)

HTTP endpoint summary not logged on startup when supervised route controller is enabled

[CAMEL-23799](https://issues.apache.org/jira/browse/CAMEL-23799)

Simple language: sort init-block substitution keys by length to prevent prefix collision

[CAMEL-23796](https://issues.apache.org/jira/browse/CAMEL-23796)

Simple language: fix wrong token reported in logical operator right-hand-side error message

[CAMEL-23763](https://issues.apache.org/jira/browse/CAMEL-23763)

camel-xml-io ModelWriter writes kamelet child element as route attribute breaking XML round-trip

[CAMEL-23740](https://issues.apache.org/jira/browse/CAMEL-23740)

LangChain4jAgentConverter WrappedFile converter fails for FTP/SFTP GenericFile — requires manual convertBodyTo workaround

[CAMEL-23739](https://issues.apache.org/jira/browse/CAMEL-23739)

camel-openai: support WrappedFile, byte\[\], and InputStream bodies for vision models

[CAMEL-23735](https://issues.apache.org/jira/browse/CAMEL-23735)

camel-dynamic-router: default aggregation keeps the FIRST reply, contradicting the documented "last reply" behavior (regression since 4.4.0)

[CAMEL-23730](https://issues.apache.org/jira/browse/CAMEL-23730)

AggregateReifier.mandatoryLookup fails during export dry-run even with lazyBean=true

[CAMEL-23719](https://issues.apache.org/jira/browse/CAMEL-23719)

\[camel-micrometer\] When ProducerTemplate sends to a SEDA endpoint, Exchange.getFromRouteId() returns null

[CAMEL-23708](https://issues.apache.org/jira/browse/CAMEL-23708)

OpenTelemetry2 - Missing RECEIVED spans for routes consuming from stub/seda in nested async paths

[CAMEL-23707](https://issues.apache.org/jira/browse/CAMEL-23707)

\`camel get vault\` reports wrong vault type when multiple vault providers are configured with a single secret each

[CAMEL-23698](https://issues.apache.org/jira/browse/CAMEL-23698)

camel-rest-openapi - Producer appends trailing ? to URL when no query parameters are set

[CAMEL-23692](https://issues.apache.org/jira/browse/CAMEL-23692)

BacklogTracer drops late-arriving trace events from async multicast branches

[CAMEL-23676](https://issues.apache.org/jira/browse/CAMEL-23676)

camel-nats - Camel routes body back to the consumer?

[CAMEL-23674](https://issues.apache.org/jira/browse/CAMEL-23674)

camel-jbang - Export silent run fails on non-stubbed components with property placeholders

[CAMEL-23662](https://issues.apache.org/jira/browse/CAMEL-23662)

logMask of camel context not overridden in route

[CAMEL-23659](https://issues.apache.org/jira/browse/CAMEL-23659)

camel-jbang - Stub mode should ignore property bindings for stubbed components

[CAMEL-23652](https://issues.apache.org/jira/browse/CAMEL-23652)

\[kamelet\] Bean is not registered

[CAMEL-23646](https://issues.apache.org/jira/browse/CAMEL-23646)

BackgroundTask callbacks return inverted boolean in sjms, pgevent, and master causing infinite retry loops after successful recovery

[CAMEL-23627](https://issues.apache.org/jira/browse/CAMEL-23627)

Exception not caught when Slack returns a response code > 299

[CAMEL-23608](https://issues.apache.org/jira/browse/CAMEL-23608)

camel-jbang - CLI commands leak terminal escape sequences from JLine terminal width detection

[CAMEL-23603](https://issues.apache.org/jira/browse/CAMEL-23603)

Build is broken with JDK 25 on CI org.jspecify.annotations.Nullable not found

[CAMEL-23602](https://issues.apache.org/jira/browse/CAMEL-23602)

threads EIP does not respect maxQueueSize when using virtual threads

[CAMEL-23594](https://issues.apache.org/jira/browse/CAMEL-23594)

Content type in kamelets is being URL endoded, leading to errors/timeouts

[CAMEL-23571](https://issues.apache.org/jira/browse/CAMEL-23571)

Google PubSub component leaves orphaned channels when using PubSub emulator

[CAMEL-23553](https://issues.apache.org/jira/browse/CAMEL-23553)

camel-platform-http-vertx: VertxPlatformHttpConsumer fails to resolve RestRegistry

[CAMEL-23550](https://issues.apache.org/jira/browse/CAMEL-23550)

canel-kamelet - AbstractReifier Local Bean Repository Lookup

[CAMEL-23547](https://issues.apache.org/jira/browse/CAMEL-23547)

camel-core - Properties component should eager start custom functions resolver

[CAMEL-23542](https://issues.apache.org/jira/browse/CAMEL-23542)

Main branch has broken tests due to Validator non Null requirements

[CAMEL-23534](https://issues.apache.org/jira/browse/CAMEL-23534)

Schema properties are URL-encoded when passed from Pipe to Kamelet, breaking Protobuf/Avro schema parsers

[CAMEL-23523](https://issues.apache.org/jira/browse/CAMEL-23523)

camel-kafka: batchingIntervalMs timer not reset on new accumulation cycle, causing premature single-message batches after idle periods

[CAMEL-23521](https://issues.apache.org/jira/browse/CAMEL-23521)

camel-core: XML route dumping is missing target element closing tags

[CAMEL-23513](https://issues.apache.org/jira/browse/CAMEL-23513)

completeAllOnStop() does not complete aggregations when used with completionInterval()

[CAMEL-23505](https://issues.apache.org/jira/browse/CAMEL-23505)

camel-splunk-hec: align hostname verification with system default in SplunkHECProducer

[CAMEL-23504](https://issues.apache.org/jira/browse/CAMEL-23504)

camel-keycloak: KeycloakSecurityHelper.parseAndVerifyAccessToken should include the IS\_ACTIVE predicate on TokenVerifier

[CAMEL-23494](https://issues.apache.org/jira/browse/CAMEL-23494)

preparingShutdown flag not reset on error handlers after suspend/resume — causes silent transaction rollback and redelivery suppression

[CAMEL-23479](https://issues.apache.org/jira/browse/CAMEL-23479)

camel-main: camel.main.virtualThreadsEnabled does not work

[CAMEL-23469](https://issues.apache.org/jira/browse/CAMEL-23469)

Infinite redelivery loop when child route with NoErrorHandler uses removeHeaders("\*")

[CAMEL-23464](https://issues.apache.org/jira/browse/CAMEL-23464)

Camel-AWS-Bedrock: BedrockAgentConfiguration.modelId is required but never used by ingestion operations

[CAMEL-23463](https://issues.apache.org/jira/browse/CAMEL-23463)

Camel-AWS-Bedrock: invokeTextModel throws "Unexpected model" for image/embedding/rerank/Stability/Nova-canvas models declared in BedrockModels

[CAMEL-23462](https://issues.apache.org/jira/browse/CAMEL-23462)

Camel-AWS-Bedrock: invoke\*Model operations silently produce no output when pojoRequest body has wrong type

[CAMEL-23461](https://issues.apache.org/jira/browse/CAMEL-23461)

Camel-AWS-Bedrock: applyGuardrail reads guardrail identifier from wrong header

[CAMEL-23457](https://issues.apache.org/jira/browse/CAMEL-23457)

camel-docling: OCR fails to detect footer regions in scanned images

[CAMEL-23456](https://issues.apache.org/jira/browse/CAMEL-23456)

camel-docling: Document title and type metadata not extracted reliably

[CAMEL-23448](https://issues.apache.org/jira/browse/CAMEL-23448)

camel-launcher jolokia fails to attach agent — JAR path unresolvable from nested Spring Boot JAR

[CAMEL-23419](https://issues.apache.org/jira/browse/CAMEL-23419)

camel-nats - Consumer does not work in pull mode

[CAMEL-23406](https://issues.apache.org/jira/browse/CAMEL-23406)

camel-yaml-dsl - camel-jacksonxml: Unknown node id: org.apache.camel.model.dataformat.JacksonXMLDataFormat

[CAMEL-23384](https://issues.apache.org/jira/browse/CAMEL-23384)

camel-kamelet-main: camel export fails with IllegalArgumentException on kamelets using transformDataType EIP

[CAMEL-23380](https://issues.apache.org/jira/browse/CAMEL-23380)

\`TracingRoutePolicy.onExchangeBegin\` opens scopes and spans that are never closed/ended

[CAMEL-23378](https://issues.apache.org/jira/browse/CAMEL-23378)

camel-spring-boot - Block String to InputStream conversion in SpringTypeConverter

[CAMEL-23377](https://issues.apache.org/jira/browse/CAMEL-23377)

simple language - Multiline init blocks aren't initialized properly

[CAMEL-23370](https://issues.apache.org/jira/browse/CAMEL-23370)

camel.main.routes-include-pattern with classpath:\*\*/\*.xml fails in Spring Boot fat JAR (works in IDE, regression since 4.11.0)

[CAMEL-23355](https://issues.apache.org/jira/browse/CAMEL-23355)

camel-jbang: export with kamelet aws-ddb-sink - transformer aws2-ddb is not working

[CAMEL-23293](https://issues.apache.org/jira/browse/CAMEL-23293)

\[camel-jbang\] Files are not synched in dev-mode with Quarkus runtime

[CAMEL-23291](https://issues.apache.org/jira/browse/CAMEL-23291)

EventHubs and Google PubSub consumers lack ShutdownAware support, causing potential message loss during graceful shutdown

[CAMEL-23132](https://issues.apache.org/jira/browse/CAMEL-23132)

camel-aws2-s3 does not use listObjectV2 for listing objects

[CAMEL-23124](https://issues.apache.org/jira/browse/CAMEL-23124)

camel-docling - Fix CLI mode ProcessBuilder deadlock with sequential stream reading

[CAMEL-23120](https://issues.apache.org/jira/browse/CAMEL-23120)

camel-docling - Implement batchSize sub-batch partitioning in batch processing

[CAMEL-21937](https://issues.apache.org/jira/browse/CAMEL-21937)

camel-ai - Tool route upsets component when step 'stop' is used mid-way

[CAMEL-21935](https://issues.apache.org/jira/browse/CAMEL-21935)

camel-jbang - kubernetes plugin fails to run when knative-service.enabled=true in openshift

[CAMEL-20227](https://issues.apache.org/jira/browse/CAMEL-20227)

Kafka offset advances when using Pausable EIP and messages are lost when resumed

### Dependency upgrade (12)

[CAMEL-23742](https://issues.apache.org/jira/browse/CAMEL-23742)

Remove Apache Derby dependencies from camel-examples

[CAMEL-23741](https://issues.apache.org/jira/browse/CAMEL-23741)

camel-infinispan - Upgrade to 16.2

[CAMEL-23538](https://issues.apache.org/jira/browse/CAMEL-23538)

Upgrade testcontainers to 2.0.4+

[CAMEL-23498](https://issues.apache.org/jira/browse/CAMEL-23498)

Cleanup remaining SLF4J 1.x artifacts after upgrade to 2.0.x

[CAMEL-23481](https://issues.apache.org/jira/browse/CAMEL-23481)

Remove Apache Derby dependencies

[CAMEL-23442](https://issues.apache.org/jira/browse/CAMEL-23442)

camel-vertx-http - Does not work with undertow 2.4.0

[CAMEL-23401](https://issues.apache.org/jira/browse/CAMEL-23401)

Upgrade JSch to 2.28.2 (RSA certificate authentication fix)

[CAMEL-23375](https://issues.apache.org/jira/browse/CAMEL-23375)

Upgrade to Http Client 5.6+

[CAMEL-23368](https://issues.apache.org/jira/browse/CAMEL-23368)

camel-spring-boot - Upgrade to SB 4.1.0

[CAMEL-23311](https://issues.apache.org/jira/browse/CAMEL-23311)

Upgrade to Apache Artemis 2.5.x

[CAMEL-23296](https://issues.apache.org/jira/browse/CAMEL-23296)

maven wrapper - upgrade to 3.9.14+

[CAMEL-23118](https://issues.apache.org/jira/browse/CAMEL-23118)

camel-kubernetes - Upgrade to 7.6 client

### Improvement (221)

[CAMEL-23833](https://issues.apache.org/jira/browse/CAMEL-23833)

camel-core - Add alias to EIP model to map EIP to AI patterns

[CAMEL-23830](https://issues.apache.org/jira/browse/CAMEL-23830)

camel-jbang - TUI shell panel: command echo and error output render in hard-to-read dark red

[CAMEL-23820](https://issues.apache.org/jira/browse/CAMEL-23820)

camel-yaml-dsl-validator-maven-plugin: support other directories

[CAMEL-23817](https://issues.apache.org/jira/browse/CAMEL-23817)

Embed test plugin in Camel Launcher

[CAMEL-23816](https://issues.apache.org/jira/browse/CAMEL-23816)

camel-core-model - Improve descriptions in model

[CAMEL-23812](https://issues.apache.org/jira/browse/CAMEL-23812)

camel-milo - Add support for explicit username and password parameters in Milo client to safely handle credentials with special characters

[CAMEL-23808](https://issues.apache.org/jira/browse/CAMEL-23808)

camel-diagram - Topology dev console to render PNG and html visual diagram

[CAMEL-23807](https://issues.apache.org/jira/browse/CAMEL-23807)

camel-platform-http-main - Use the new html diagram render

[CAMEL-23806](https://issues.apache.org/jira/browse/CAMEL-23806)

Split long documentation pages into focused sub-pages

[CAMEL-23804](https://issues.apache.org/jira/browse/CAMEL-23804)

camel-platform-http-vertx: SSE (text/event-stream) responses buffer events instead of flushing eagerly

[CAMEL-23803](https://issues.apache.org/jira/browse/CAMEL-23803)

camel-jackson-avro / camel-jackson-protobuf: block unsafe polymorphic base types by default in the data format ObjectMapper

[CAMEL-23797](https://issues.apache.org/jira/browse/CAMEL-23797)

Simple language: collapse duplicate evalBinary/evalOther/evalTernary into a single helper

[CAMEL-23793](https://issues.apache.org/jira/browse/CAMEL-23793)

Camel MCP server - expose component headers from catalog

[CAMEL-23792](https://issues.apache.org/jira/browse/CAMEL-23792)

camel-endpointdsl - Build java constant classes with all the component header keys

[CAMEL-23789](https://issues.apache.org/jira/browse/CAMEL-23789)

Improve component docs code examples to be multi-DSL friendly (XML/YAML tabs)

[CAMEL-23787](https://issues.apache.org/jira/browse/CAMEL-23787)

camel-jacksonxml: block unsafe polymorphic base types by default in the XmlMapper

[CAMEL-23786](https://issues.apache.org/jira/browse/CAMEL-23786)

camel-jackson: block unsafe polymorphic base types by default in the data format ObjectMapper

[CAMEL-23785](https://issues.apache.org/jira/browse/CAMEL-23785)

camel-http: mark x509HostnameVerifier with security="insecure:ssl"

[CAMEL-23784](https://issues.apache.org/jira/browse/CAMEL-23784)

camel-splunk-hec: mark skipTlsVerify with security="insecure:ssl"

[CAMEL-23783](https://issues.apache.org/jira/browse/CAMEL-23783)

camel-schematron: harden the rules TransformerFactory against external entities (XXE)

[CAMEL-23782](https://issues.apache.org/jira/browse/CAMEL-23782)

camel-leveldb: apply an ObjectInputFilter to aggregation-repository key deserialization

[CAMEL-23777](https://issues.apache.org/jira/browse/CAMEL-23777)

camel-jbang - Move camel get route-dump to camel cmd route-dump

[CAMEL-23776](https://issues.apache.org/jira/browse/CAMEL-23776)

camel-a2a: Add a2aSubTask YAML route step for scoped progress events

[CAMEL-23775](https://issues.apache.org/jira/browse/CAMEL-23775)

Add YAML DSL extension point for component-provided route step deserializers

[CAMEL-23773](https://issues.apache.org/jira/browse/CAMEL-23773)

camel-cxf - separate ws-security into its own module to avoid opensaml/shibboleth dependency

[CAMEL-23772](https://issues.apache.org/jira/browse/CAMEL-23772)

dataformat: endpoints ignore global camel.dataformat.\* configuration in camel quarkus

[CAMEL-23769](https://issues.apache.org/jira/browse/CAMEL-23769)

camel-http-common: apply a configurable ObjectInputFilter when deserializing Java objects

[CAMEL-23767](https://issues.apache.org/jira/browse/CAMEL-23767)

camel-platform-http-main: warn or fail fast when authentication is enabled but no mechanism is configured

[CAMEL-23765](https://issues.apache.org/jira/browse/CAMEL-23765)

camel-ftp/sftp/mina-sftp/azure-files/smb: contain localWorkDirectory downloads within the work directory

[CAMEL-23764](https://issues.apache.org/jira/browse/CAMEL-23764)

camel-as2: fail closed when an inbound signed message cannot be verified

[CAMEL-23762](https://issues.apache.org/jira/browse/CAMEL-23762)

camel-whatsapp: support X-Hub-Signature-256 verification of inbound webhook payloads

[CAMEL-23760](https://issues.apache.org/jira/browse/CAMEL-23760)

camel-oauth: require a JWK set to verify token signatures in UserProfile

[CAMEL-23759](https://issues.apache.org/jira/browse/CAMEL-23759)

camel-spring-ws: apply a HeaderFilterStrategy to inbound SOAP headers

[CAMEL-23757](https://issues.apache.org/jira/browse/CAMEL-23757)

Add Java DSL model writer for full-circle DSL transformation (XML/YAML to Java DSL)

[CAMEL-23756](https://issues.apache.org/jira/browse/CAMEL-23756)

camel-jbang - MCP tool for route transform should support java source

[CAMEL-23749](https://issues.apache.org/jira/browse/CAMEL-23749)

Embrace MCP Java SDK new 2.0.0 API

[CAMEL-23747](https://issues.apache.org/jira/browse/CAMEL-23747)

camel-mail - useHeader\* options should default to false for secure-by-default

[CAMEL-23745](https://issues.apache.org/jira/browse/CAMEL-23745)

docs: security page Post-Quantum section should cover message-layer PQC (camel-pqc), not only TLS

[CAMEL-23744](https://issues.apache.org/jira/browse/CAMEL-23744)

camel-xmlsecurity: update XML Encryption docs example from 3DES (TRIPLEDES) to AES-256-GCM

[CAMEL-23743](https://issues.apache.org/jira/browse/CAMEL-23743)

camel-http: expose hostnameVerificationPolicy option to allow opting into httpclient 5.6 handshake-time hostname verification

[CAMEL-23738](https://issues.apache.org/jira/browse/CAMEL-23738)

camel-keycloak: always verify the access token in KeycloakSecurityPolicy regardless of configured roles/permissions

[CAMEL-23737](https://issues.apache.org/jira/browse/CAMEL-23737)

camel-pqc: surface hybrid operations and cross-reference the Hybrid Cryptography section in the docs

[CAMEL-23736](https://issues.apache.org/jira/browse/CAMEL-23736)

camel-main: make the self-signed (dev) certificate key algorithm configurable, default to EC

[CAMEL-23726](https://issues.apache.org/jira/browse/CAMEL-23726)

camel-pqc: Use JSON instead of Java serialization for key metadata in AWS and HashiCorp Vault lifecycle managers

[CAMEL-23724](https://issues.apache.org/jira/browse/CAMEL-23724)

camel-core - Make simple syntax understandable for AIs and tooling

[CAMEL-23722](https://issues.apache.org/jira/browse/CAMEL-23722)

camel-jbang - Break up documentation

[CAMEL-23716](https://issues.apache.org/jira/browse/CAMEL-23716)

camel-salesforce - align Exchange header constant names with Camel naming convention

[CAMEL-23715](https://issues.apache.org/jira/browse/CAMEL-23715)

camel-core - Improve simple docs with more examples in the function descriptions

[CAMEL-23713](https://issues.apache.org/jira/browse/CAMEL-23713)

camel-jbang - TUI otel span update

[CAMEL-23709](https://issues.apache.org/jira/browse/CAMEL-23709)

camel-opentelemtry2 - Span verbosity for core processors that also emit events

[CAMEL-23706](https://issues.apache.org/jira/browse/CAMEL-23706)

camel-opentelemetry2 - Auto-configure in-memory span exporter for dev profile

[CAMEL-23704](https://issues.apache.org/jira/browse/CAMEL-23704)

camel-ai - Use correlated exchange copy for multi-tool invocations in langchain4j-tools

[CAMEL-23702](https://issues.apache.org/jira/browse/CAMEL-23702)

camel-ai: Camel CLI/Jbang exported project should be adjusted for greater AI relevance

[CAMEL-23700](https://issues.apache.org/jira/browse/CAMEL-23700)

camel-website - Update agents.md and llms.txt

[CAMEL-23699](https://issues.apache.org/jira/browse/CAMEL-23699)

camel-jbang - Rebrand as Camel CLI

[CAMEL-23697](https://issues.apache.org/jira/browse/CAMEL-23697)

camel-langchain4j-agent - support Java class as response format for structured outputs

[CAMEL-23695](https://issues.apache.org/jira/browse/CAMEL-23695)

Langchain4j-agent: improve structured output when Langchain4j 1.16.0 is out

[CAMEL-23693](https://issues.apache.org/jira/browse/CAMEL-23693)

camel-core - Optimize CaseInsensitiveMap hash function for ASCII keys

[CAMEL-23691](https://issues.apache.org/jira/browse/CAMEL-23691)

camel-core - Improve CaseInsensitiveMap with O(1) hash table and header key deduplication

[CAMEL-23686](https://issues.apache.org/jira/browse/CAMEL-23686)

Reduce Exchange memory pressure and fix pooled exchange issues

[CAMEL-23685](https://issues.apache.org/jira/browse/CAMEL-23685)

Expose public token validation API for incoming Bearer tokens (JWT and opaque)

[CAMEL-23684](https://issues.apache.org/jira/browse/CAMEL-23684)

BacklogTracer message history should correlate exchanges by breadcrumb ID for full end-to-end flow

[CAMEL-23682](https://issues.apache.org/jira/browse/CAMEL-23682)

camel-undertow - Expose common UndertowOptions on UndertowHostOptions for server-level configuration

[CAMEL-23681](https://issues.apache.org/jira/browse/CAMEL-23681)

Optimize Exchange memory pressure: copy-on-write headers and lazy initialization

[CAMEL-23680](https://issues.apache.org/jira/browse/CAMEL-23680)

Add group as scope to variables

[CAMEL-23669](https://issues.apache.org/jira/browse/CAMEL-23669)

camel-hl7 - Support converting to XML

[CAMEL-23667](https://issues.apache.org/jira/browse/CAMEL-23667)

Add --stub=remote flag to stub only remote components via catalog resolution

[CAMEL-23666](https://issues.apache.org/jira/browse/CAMEL-23666)

\[Kamelet/Route Templates\] Support optionals for endpoints uris

[CAMEL-23663](https://issues.apache.org/jira/browse/CAMEL-23663)

camel-jbang - Add config to turn off the banner showing plugins you can install with --help

[CAMEL-23661](https://issues.apache.org/jira/browse/CAMEL-23661)

camel-diagram - Add topology diagram renderer for inter-route visualization

[CAMEL-23658](https://issues.apache.org/jira/browse/CAMEL-23658)

camel-jbang - Add camel dev as alias for camel run --dev

[CAMEL-23657](https://issues.apache.org/jira/browse/CAMEL-23657)

Enhance component metadata to mark destination-identity query parameters for topology matching

[CAMEL-23655](https://issues.apache.org/jira/browse/CAMEL-23655)

Update GitHub topics for better discoverability by AI and developers

[CAMEL-23653](https://issues.apache.org/jira/browse/CAMEL-23653)

camel-jbang - Make it easy to use plugins

[CAMEL-23651](https://issues.apache.org/jira/browse/CAMEL-23651)

camel-netty-http and camel-undertow: align muteException default with the other HTTP components

[CAMEL-23650](https://issues.apache.org/jira/browse/CAMEL-23650)

camel-micrometer - Do not spam log at WARN in dev mode

[CAMEL-23643](https://issues.apache.org/jira/browse/CAMEL-23643)

camel-test-infra - Add service version to metadata - such as Artemis Broker version etc

[CAMEL-23641](https://issues.apache.org/jira/browse/CAMEL-23641)

camel-test-infra - Can we have an infra for OpenTelemetry

[CAMEL-23640](https://issues.apache.org/jira/browse/CAMEL-23640)

camel-jbang - Add restart command to infra service

[CAMEL-23638](https://issues.apache.org/jira/browse/CAMEL-23638)

camel-jbang - Add CLI meta-tools to camel ask for full command access

[CAMEL-23637](https://issues.apache.org/jira/browse/CAMEL-23637)

camel-jbang - TUI add Run Infra Service action to F2 menu

[CAMEL-23634](https://issues.apache.org/jira/browse/CAMEL-23634)

camel-jbang - TUI Send Message dialog

[CAMEL-23633](https://issues.apache.org/jira/browse/CAMEL-23633)

camel-jbang - TUI auto-reselect integration after restart

[CAMEL-23632](https://issues.apache.org/jira/browse/CAMEL-23632)

camel-jbang - Add CLI usage examples (footer) to commands

[CAMEL-23631](https://issues.apache.org/jira/browse/CAMEL-23631)

Route diagram - highlight error path from ErrorRegistry message history

[CAMEL-23630](https://issues.apache.org/jira/browse/CAMEL-23630)

camel-dapr - add HeaderFilterStrategy and avoid copying routing-relevant CloudEvent fields into Camel exchange headers

[CAMEL-23629](https://issues.apache.org/jira/browse/CAMEL-23629)

camel-irc - align Exchange header constant names with Camel naming convention

[CAMEL-23624](https://issues.apache.org/jira/browse/CAMEL-23624)

camel-jbang - Add camel get error command

[CAMEL-23623](https://issues.apache.org/jira/browse/CAMEL-23623)

camel-jbang - Add error tab using information from error registry

[CAMEL-23622](https://issues.apache.org/jira/browse/CAMEL-23622)

camel-jbang - Avoid readme files in startup summary

[CAMEL-23621](https://issues.apache.org/jira/browse/CAMEL-23621)

camel-langchain4j-tools / camel-langchain4j-agent / camel-spring-ai-tools: tool argument headers should be filtered against declared parameters

[CAMEL-23616](https://issues.apache.org/jira/browse/CAMEL-23616)

camel-management - Add stepId to producer and processor mbeans

[CAMEL-23614](https://issues.apache.org/jira/browse/CAMEL-23614)

Add getFromRouteGroup() method to the Exchange API

[CAMEL-23611](https://issues.apache.org/jira/browse/CAMEL-23611)

camel-yaml-dsl - Add WARN logging about recommendation to use canonical/normalized style

[CAMEL-23609](https://issues.apache.org/jira/browse/CAMEL-23609)

Tighten in-code ObjectInputFilter defaults with JEP-290 graph-shape limits

[CAMEL-23600](https://issues.apache.org/jira/browse/CAMEL-23600)

camel-milo: expose the underlying Eclipse Milo OpcUaClient for custom OPC UA DataType handling

[CAMEL-23597](https://issues.apache.org/jira/browse/CAMEL-23597)

camel-solr - align Exchange header prefix constants with Camel naming convention

[CAMEL-23596](https://issues.apache.org/jira/browse/CAMEL-23596)

camel-yaml-io - Replace hand-written YamlWriter with generated direct YAML writer

[CAMEL-23595](https://issues.apache.org/jira/browse/CAMEL-23595)

camel-jbang-examples - Include metadata whether testing is included

[CAMEL-23593](https://issues.apache.org/jira/browse/CAMEL-23593)

camel validate normalize does not handle REST DSL, routeConfiguration, and beans-only files

[CAMEL-23592](https://issues.apache.org/jira/browse/CAMEL-23592)

camel-shiro - align Exchange header constant names with Camel naming convention

[CAMEL-23591](https://issues.apache.org/jira/browse/CAMEL-23591)

camel-mail - align consumer-side dispatch header constant names with Camel naming convention

[CAMEL-23590](https://issues.apache.org/jira/browse/CAMEL-23590)

camel-milo - align Exchange header constant names with Camel naming convention

[CAMEL-23589](https://issues.apache.org/jira/browse/CAMEL-23589)

camel-solr - align Solr field/param header prefixes with Camel naming convention

[CAMEL-23588](https://issues.apache.org/jira/browse/CAMEL-23588)

camel-undertow - align websocket header names with Camel naming convention (CAMEL-23532 follow-on)

[CAMEL-23587](https://issues.apache.org/jira/browse/CAMEL-23587)

camel-jt400 - align Exchange header constant names with Camel naming convention

[CAMEL-23586](https://issues.apache.org/jira/browse/CAMEL-23586)

camel-mongodb-gridfs - align Exchange header constant names with Camel naming convention

[CAMEL-23585](https://issues.apache.org/jira/browse/CAMEL-23585)

camel-arangodb - align Exchange header constant names with Camel naming convention

[CAMEL-23584](https://issues.apache.org/jira/browse/CAMEL-23584)

camel-kafka - align Exchange header constant names with Camel naming convention

[CAMEL-23583](https://issues.apache.org/jira/browse/CAMEL-23583)

camel-google-{functions,secret-manager,vision,text-to-speech,speech-to-text} - align Exchange header constant names with Camel naming convention

[CAMEL-23582](https://issues.apache.org/jira/browse/CAMEL-23582)

camel-github - align Exchange header constant names with Camel naming convention

[CAMEL-23581](https://issues.apache.org/jira/browse/CAMEL-23581)

camel-elasticsearch + camel-opensearch - align Exchange header constant names with Camel naming convention

[CAMEL-23580](https://issues.apache.org/jira/browse/CAMEL-23580)

camel-openstack - align Exchange header constant names with Camel naming convention

[CAMEL-23579](https://issues.apache.org/jira/browse/CAMEL-23579)

camel-pdf - align Exchange header constant names with Camel naming convention

[CAMEL-23578](https://issues.apache.org/jira/browse/CAMEL-23578)

camel-web3j - align Exchange header constant names with Camel naming convention

[CAMEL-23577](https://issues.apache.org/jira/browse/CAMEL-23577)

align Exchange header constant names with Camel naming convention - global sweep

[CAMEL-23576](https://issues.apache.org/jira/browse/CAMEL-23576)

camel-jira - align Exchange header constant names with Camel naming convention

[CAMEL-23575](https://issues.apache.org/jira/browse/CAMEL-23575)

camel-mongodb-gridfs: align Exchange header constant names with Camel naming convention

[CAMEL-23574](https://issues.apache.org/jira/browse/CAMEL-23574)

camel-dns - align Exchange header constant names with Camel naming convention

[CAMEL-23572](https://issues.apache.org/jira/browse/CAMEL-23572)

camel-tui - Add F2 actions menu with Run an example to overview page

[CAMEL-23569](https://issues.apache.org/jira/browse/CAMEL-23569)

camel-tui: Add support for camel-test-infra services

[CAMEL-23566](https://issues.apache.org/jira/browse/CAMEL-23566)

camel-jbang - Improve --example to source from camel-jbang-examples repository

[CAMEL-23565](https://issues.apache.org/jira/browse/CAMEL-23565)

CI incremental-build should not test all modules when only the root pom.xml changes

[CAMEL-23564](https://issues.apache.org/jira/browse/CAMEL-23564)

Baggage customization doesn't seem to work

[CAMEL-23560](https://issues.apache.org/jira/browse/CAMEL-23560)

camel-jbang - Eliminate the usage of a built time Quarkus Platform version literal

[CAMEL-23555](https://issues.apache.org/jira/browse/CAMEL-23555)

Per-operation HTTP metrics for REST services in RestRegistry

[CAMEL-23554](https://issues.apache.org/jira/browse/CAMEL-23554)

RuntimeEndpointRegistry does not track out hits for InOut consumer endpoints

[CAMEL-23549](https://issues.apache.org/jira/browse/CAMEL-23549)

Need a org.apache.camel.processor.transformer.DataTypeProcessor which can discover fromType/toType at runtime

[CAMEL-23548](https://issues.apache.org/jira/browse/CAMEL-23548)

AWS S3- allow simple expression in destinationBucketPrefix and destinationBucketSuffix

[CAMEL-23544](https://issues.apache.org/jira/browse/CAMEL-23544)

Fix null fromRouteId and endpoint tracking for delegating consumers (e.g. platform-http)

[CAMEL-23543](https://issues.apache.org/jira/browse/CAMEL-23543)

camel-core - Investigate centralizing Camel\* inbound header filtering in DefaultHeaderFilterStrategy

[CAMEL-23535](https://issues.apache.org/jira/browse/CAMEL-23535)

camel-api - Enhance documentation and add links to relevant pages in user manual

[CAMEL-23533](https://issues.apache.org/jira/browse/CAMEL-23533)

camel-core - ErrorHandlerRegistry improvements

[CAMEL-23532](https://issues.apache.org/jira/browse/CAMEL-23532)

camel-vertx-websocket / camel-atmosphere-websocket / camel-iggy - use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23529](https://issues.apache.org/jira/browse/CAMEL-23529)

camel-jbang-mcp - Add theme to route diagram so it can return ascii diagram

[CAMEL-23528](https://issues.apache.org/jira/browse/CAMEL-23528)

camel-neo4j: validate property names when building MATCH/DELETE WHERE clause

[CAMEL-23526](https://issues.apache.org/jira/browse/CAMEL-23526)

camel-cxf: align Exchange header constant names with Camel naming convention

[CAMEL-23525](https://issues.apache.org/jira/browse/CAMEL-23525)

camel-platform-http-main: add optional JWT issuer and audience claim validation

[CAMEL-23524](https://issues.apache.org/jira/browse/CAMEL-23524)

camel-couchdb / camel-couchbase - align Exchange header constant values with Camel naming convention

[CAMEL-23522](https://issues.apache.org/jira/browse/CAMEL-23522)

camel-mail: filter mail.smtp.\* / mail.smtps.\* namespace from producer headers

[CAMEL-23520](https://issues.apache.org/jira/browse/CAMEL-23520)

camel-mail: option to lock recipients/sender/subject to endpoint URI

[CAMEL-23519](https://issues.apache.org/jira/browse/CAMEL-23519)

camel-jbang - TUI to show (n) notifications

[CAMEL-23518](https://issues.apache.org/jira/browse/CAMEL-23518)

camel-jbang - Refactor TUI trace tab with two-level exchange drill-down

[CAMEL-23517](https://issues.apache.org/jira/browse/CAMEL-23517)

camel-jbang - Add history tab to TUI

[CAMEL-23516](https://issues.apache.org/jira/browse/CAMEL-23516)

camel-xmpp - Use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23515](https://issues.apache.org/jira/browse/CAMEL-23515)

camel-nats - Use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23514](https://issues.apache.org/jira/browse/CAMEL-23514)

camel-diagram - Add metric to ascii diagram

[CAMEL-23511](https://issues.apache.org/jira/browse/CAMEL-23511)

camel-jgroups-raft: align Exchange header constant names with Camel naming convention

[CAMEL-23510](https://issues.apache.org/jira/browse/CAMEL-23510)

camel-jgroups: align Exchange header constant names with Camel naming convention

[CAMEL-23509](https://issues.apache.org/jira/browse/CAMEL-23509)

camel-lucene: align Exchange header constant names with Camel naming convention

[CAMEL-23508](https://issues.apache.org/jira/browse/CAMEL-23508)

camel-elasticsearch-rest-client: align Exchange header constant names with Camel naming convention

[CAMEL-23507](https://issues.apache.org/jira/browse/CAMEL-23507)

camel-cometd: Integrate HeaderFilterStrategy for inbound header mapping

[CAMEL-23506](https://issues.apache.org/jira/browse/CAMEL-23506)

camel-aws2-sqs / camel-aws2-sns - align HeaderFilterStrategy with sibling components

[CAMEL-23495](https://issues.apache.org/jira/browse/CAMEL-23495)

Replace Thread.sleep() with Awaitility and fix ~30 flaky tests in camel-core and camel-management

[CAMEL-23491](https://issues.apache.org/jira/browse/CAMEL-23491)

camel-jbang - Add list of known 3rd party plugins

[CAMEL-23483](https://issues.apache.org/jira/browse/CAMEL-23483)

camel-nats - Manual acknowledgement

[CAMEL-23477](https://issues.apache.org/jira/browse/CAMEL-23477)

camel-jbang-mcp: stop re-embedding pomContent inside migrateProject prompt

[CAMEL-23476](https://issues.apache.org/jira/browse/CAMEL-23476)

camel-jbang-mcp: strip null fields from MCP JSON responses

[CAMEL-23475](https://issues.apache.org/jira/browse/CAMEL-23475)

camel-jbang-mcp: make ComponentDetailResult lean by default with option filtering

[CAMEL-23474](https://issues.apache.org/jira/browse/CAMEL-23474)

camel-jbang-mcp: stop echoing input route in camel\_route\_context response

[CAMEL-23473](https://issues.apache.org/jira/browse/CAMEL-23473)

camel-jbang-mcp: drop verbose description from catalog list responses and lower default limit

[CAMEL-23472](https://issues.apache.org/jira/browse/CAMEL-23472)

camel-jbang-mcp: deduplicate @ToolArg descriptions to shrink tool schema payload

[CAMEL-23471](https://issues.apache.org/jira/browse/CAMEL-23471)

camel-jbang - Diagram action to be visual only

[CAMEL-23459](https://issues.apache.org/jira/browse/CAMEL-23459)

camel-docling: Add TTL cleanup for pending async tasks to prevent memory leak

[CAMEL-23454](https://issues.apache.org/jira/browse/CAMEL-23454)

camel-keycloak: Add token revocation and session logout operations

[CAMEL-23452](https://issues.apache.org/jira/browse/CAMEL-23452)

camel-keycloak: Add Organizations API operations (Keycloak 26+)

[CAMEL-23446](https://issues.apache.org/jira/browse/CAMEL-23446)

camel-solr: Add SSLContextParameters support for TLS configuration

[CAMEL-23445](https://issues.apache.org/jira/browse/CAMEL-23445)

camel-elasticsearch-rest-client: Add SSLContextParameters support for TLS configuration

[CAMEL-23444](https://issues.apache.org/jira/browse/CAMEL-23444)

camel-elasticsearch: Add SSLContextParameters support for TLS configuration

[CAMEL-23443](https://issues.apache.org/jira/browse/CAMEL-23443)

camel-pulsar - Expose enableBatchIndexAcknowledgment as a consumer configuration option

[CAMEL-23438](https://issues.apache.org/jira/browse/CAMEL-23438)

camel-jbang - Wrapper to install scripts as camel instead of camelw

[CAMEL-23437](https://issues.apache.org/jira/browse/CAMEL-23437)

Fix and re-enable flaky DisruptorReconfigureWithBlockingProducerTest

[CAMEL-23436](https://issues.apache.org/jira/browse/CAMEL-23436)

camel-netty - Add type convert from InputStream to ByteBuf

[CAMEL-23434](https://issues.apache.org/jira/browse/CAMEL-23434)

camel-diagram - Adjusting nodeWidth does not adjust padding

[CAMEL-23426](https://issues.apache.org/jira/browse/CAMEL-23426)

camel-console - json response for ArrayList vs JsonArray should be only one kind

[CAMEL-23425](https://issues.apache.org/jira/browse/CAMEL-23425)

camel-openai - Add reasoning\_content support and generic response header extraction

[CAMEL-23424](https://issues.apache.org/jira/browse/CAMEL-23424)

camel-diagram - Add option to use description over code

[CAMEL-23423](https://issues.apache.org/jira/browse/CAMEL-23423)

camel-jbang - diagram command to have theme=text

[CAMEL-23420](https://issues.apache.org/jira/browse/CAMEL-23420)

camel-jbang - Add graphical route diagram rendering to TUI monitor

[CAMEL-23418](https://issues.apache.org/jira/browse/CAMEL-23418)

camel-ocsf: Upgrade OCSF schema to 1.8.0

[CAMEL-23417](https://issues.apache.org/jira/browse/CAMEL-23417)

camel-diagram - Add option to make the boxes bigger

[CAMEL-23416](https://issues.apache.org/jira/browse/CAMEL-23416)

camel-diagram - Add dev console

[CAMEL-23412](https://issues.apache.org/jira/browse/CAMEL-23412)

Add getChildren() to NamedNode for uniform model tree traversal

[CAMEL-23409](https://issues.apache.org/jira/browse/CAMEL-23409)

camel-sjms - Disable ObjectMessage by default

[CAMEL-23402](https://issues.apache.org/jira/browse/CAMEL-23402)

camel-core - Route structure dumper does not include doCatch

[CAMEL-23399](https://issues.apache.org/jira/browse/CAMEL-23399)

camel-mina - Upgrade to 2.2.7

[CAMEL-23392](https://issues.apache.org/jira/browse/CAMEL-23392)

camel-vertx: Improve SSL/TLS configuration

[CAMEL-23391](https://issues.apache.org/jira/browse/CAMEL-23391)

camel-salesforce - Improve error resilience in subscription failure handling

[CAMEL-23387](https://issues.apache.org/jira/browse/CAMEL-23387)

camel-telemetry - Add span decorators for AWS

[CAMEL-23386](https://issues.apache.org/jira/browse/CAMEL-23386)

camel-jbang - cmd route-structure to support non running integrations

[CAMEL-23385](https://issues.apache.org/jira/browse/CAMEL-23385)

camel-jbang - Diagram to show live counters

[CAMEL-23381](https://issues.apache.org/jira/browse/CAMEL-23381)

simple language - Set the resulttype directly on xpath and jsonpath functions

[CAMEL-23379](https://issues.apache.org/jira/browse/CAMEL-23379)

camel-core - DefaultHeaderFilterStrategy should be lower-case by default

[CAMEL-23374](https://issues.apache.org/jira/browse/CAMEL-23374)

camel-core - Remove IOConverter for Java serialized objects

[CAMEL-23373](https://issues.apache.org/jira/browse/CAMEL-23373)

camel-jms - Disable ObjectMessage by default

[CAMEL-23372](https://issues.apache.org/jira/browse/CAMEL-23372)

Tighten default ObjectInputFilter to deny java.net.\*\* before java.\*\*

[CAMEL-23367](https://issues.apache.org/jira/browse/CAMEL-23367)

org.apache.camel.management.mbean.ManagedCamelContext generates illegal XML

[CAMEL-23363](https://issues.apache.org/jira/browse/CAMEL-23363)

camel-platform-http-main - NPE if you enable healt-check but lack JAR

[CAMEL-23362](https://issues.apache.org/jira/browse/CAMEL-23362)

camel-mqtt - Use exception handler when ACK fails

[CAMEL-23361](https://issues.apache.org/jira/browse/CAMEL-23361)

camel-aws2-s3 does not return any status code in CamelHttpResponseCode

[CAMEL-23359](https://issues.apache.org/jira/browse/CAMEL-23359)

Jetty Endpoint should return effective port number

[CAMEL-23356](https://issues.apache.org/jira/browse/CAMEL-23356)

camel-micrometer-observability-starter has excessive dep on micrometer-tracing-test

[CAMEL-23354](https://issues.apache.org/jira/browse/CAMEL-23354)

camel-jbang: quarkus-junit5 is deprecated, template should use quarkus-junit

[CAMEL-23353](https://issues.apache.org/jira/browse/CAMEL-23353)

camel-jbang: Support configurable default Maven repositories and dynamic Quarkus platform version resolution from registry

[CAMEL-23352](https://issues.apache.org/jira/browse/CAMEL-23352)

AggregateProcessor: Add configuration option for synchronous Optimistic Locking retry behavior

[CAMEL-23346](https://issues.apache.org/jira/browse/CAMEL-23346)

camel-jbang - Plugin config file has endless backup files

[CAMEL-23335](https://issues.apache.org/jira/browse/CAMEL-23335)

Lazy-load JBang plugins only when the command actually needs them

[CAMEL-23312](https://issues.apache.org/jira/browse/CAMEL-23312)

Opentelemetry2: SpanLifecycleManager.create() missing SpanKind parameter causing incorrect span types

[CAMEL-23302](https://issues.apache.org/jira/browse/CAMEL-23302)

camel-xslt - In dev mode then we could have contentCache=false to make it possible to update xslt live

[CAMEL-23250](https://issues.apache.org/jira/browse/CAMEL-23250)

Security policy enforcement for insecure configuration at startup

[CAMEL-23236](https://issues.apache.org/jira/browse/CAMEL-23236)

camel-jbang - Improve beginner UX with interactive init, top-level doc, and contextual shell help

[CAMEL-23220](https://issues.apache.org/jira/browse/CAMEL-23220)

Camel-atom not longer supports idempotent consumption

[CAMEL-23181](https://issues.apache.org/jira/browse/CAMEL-23181)

\[camel-jbang-mcp\] Add camel\_properties\_translate tool

[CAMEL-23180](https://issues.apache.org/jira/browse/CAMEL-23180)

\[camel-jbang-mcp\] Add camel\_component\_properties tool

[CAMEL-23179](https://issues.apache.org/jira/browse/CAMEL-23179)

\[camel-jbang-mcp\]: Add camel\_configuration\_validate tool for validating Camel configuration properties

[CAMEL-22987](https://issues.apache.org/jira/browse/CAMEL-22987)

camel-yaml-dsl - yaml spec is overly complex and large due to implicits

[CAMEL-22760](https://issues.apache.org/jira/browse/CAMEL-22760)

camel-kafka isn't auto-configured from spring.kafka configuration from Spring Boot

[CAMEL-22640](https://issues.apache.org/jira/browse/CAMEL-22640)

camel-core - Decorate API with NotNull / Null annotations

[CAMEL-22544](https://issues.apache.org/jira/browse/CAMEL-22544)

camel-jbang - Enhance dependency update to Sync Dependencies from Route Definitions

[CAMEL-21960](https://issues.apache.org/jira/browse/CAMEL-21960)

camel-jbang - Should camel run | export auto-detect application.properties and include the file always

[CAMEL-21208](https://issues.apache.org/jira/browse/CAMEL-21208)

camel-jbang: use a template engine for code generation

### New Feature (41)

[CAMEL-23788](https://issues.apache.org/jira/browse/CAMEL-23788)

Generate versioned offline documentation bundles for AI coding agents

[CAMEL-23771](https://issues.apache.org/jira/browse/CAMEL-23771)

Add Java DSL model writer to Camel CLI, JMX, and TUI

[CAMEL-23718](https://issues.apache.org/jira/browse/CAMEL-23718)

camel-jbang - Add camel run with java agent

[CAMEL-23712](https://issues.apache.org/jira/browse/CAMEL-23712)

camel-telemetry - Add traceCustomIdOnly option to only trace processors/endpoints with custom IDs

[CAMEL-23687](https://issues.apache.org/jira/browse/CAMEL-23687)

camel-jbang - TUI with otel tab

[CAMEL-23683](https://issues.apache.org/jira/browse/CAMEL-23683)

Create a new camel-shell component

[CAMEL-23679](https://issues.apache.org/jira/browse/CAMEL-23679)

camel-tui - Add structured data access MCP tools

[CAMEL-23678](https://issues.apache.org/jira/browse/CAMEL-23678)

camel-jbang-mcp - Add runtime tools for topology, errors, thread-dump, history, stop, and receive

[CAMEL-23656](https://issues.apache.org/jira/browse/CAMEL-23656)

Add route topology service to compute inter-route relationships

[CAMEL-23649](https://issues.apache.org/jira/browse/CAMEL-23649)

camel-langchain4j-agent: Allow Camel to create the agent internally from AgentConfiguration

[CAMEL-23642](https://issues.apache.org/jira/browse/CAMEL-23642)

Langchain4j-agent : support jsonSchema in internal AIService

[CAMEL-23639](https://issues.apache.org/jira/browse/CAMEL-23639)

Publish the Camel JBang MCP server as a Claude Code plugin

[CAMEL-23636](https://issues.apache.org/jira/browse/CAMEL-23636)

Add embeddable web component to camel-diagram for interactive route visualization

[CAMEL-23635](https://issues.apache.org/jira/browse/CAMEL-23635)

camel-jbang - TUI add a tab for shell for advanced CLI use

[CAMEL-23618](https://issues.apache.org/jira/browse/CAMEL-23618)

camel-tui - Add metrics for payload sizes

[CAMEL-23617](https://issues.apache.org/jira/browse/CAMEL-23617)

camel-core - Add option to capture message payload size for observation

[CAMEL-23615](https://issues.apache.org/jira/browse/CAMEL-23615)

Add getLastExchangeFailureHandledTimestamp() to ManagedRouteGroupMBean and ManagedRouteMBean

[CAMEL-23606](https://issues.apache.org/jira/browse/CAMEL-23606)

camel-jbang - TUI embedded MCP server for AI agent screen observation

[CAMEL-23601](https://issues.apache.org/jira/browse/CAMEL-23601)

camel-jbang - Export container-optimized layered packaging for Camel Main and Spring Boot runtimes

[CAMEL-23598](https://issues.apache.org/jira/browse/CAMEL-23598)

camel-jbang - TUI screenshot action (Shift+F5) to capture screen as ASCII art

[CAMEL-23485](https://issues.apache.org/jira/browse/CAMEL-23485)

camel-diagram - Add theme for ascii art diagrams

[CAMEL-23466](https://issues.apache.org/jira/browse/CAMEL-23466)

Camel-AWS-Bedrock: Add support for Retrieve operation in Bedrock Agent Runtime

[CAMEL-23433](https://issues.apache.org/jira/browse/CAMEL-23433)

\[camel-telemetry\] Develope includePatterns parameter

[CAMEL-23415](https://issues.apache.org/jira/browse/CAMEL-23415)

\[camel-micrometer-observability\] Baggage management

[CAMEL-23400](https://issues.apache.org/jira/browse/CAMEL-23400)

camel-test - Generate route diagrams for documentation

[CAMEL-23390](https://issues.apache.org/jira/browse/CAMEL-23390)

Add audio transcription support to camel-openai component

[CAMEL-23388](https://issues.apache.org/jira/browse/CAMEL-23388)

camel-jbang-mcp - Add tool for generating visual route diagram

[CAMEL-23342](https://issues.apache.org/jira/browse/CAMEL-23342)

camel-azure-storage-blob - Add support for listing blob versions

[CAMEL-23341](https://issues.apache.org/jira/browse/CAMEL-23341)

camel-azure-storage-blob - Add support for changing access tier of existing blobs

[CAMEL-23340](https://issues.apache.org/jira/browse/CAMEL-23340)

camel-azure-storage-blob - Add support for blob undelete (soft delete recovery)

[CAMEL-23339](https://issues.apache.org/jira/browse/CAMEL-23339)

camel-azure-storage-blob - Add support for immutability policy and legal hold operations

[CAMEL-23336](https://issues.apache.org/jira/browse/CAMEL-23336)

camel-mongodb - Expose Resume Token (Change Streams Consumer)

[CAMEL-23332](https://issues.apache.org/jira/browse/CAMEL-23332)

camel-jsoup - Add jsoup simple functions to clean and decode HTML

[CAMEL-23330](https://issues.apache.org/jira/browse/CAMEL-23330)

camel-azure-storage-blob - Add support for blob version ID access

[CAMEL-23329](https://issues.apache.org/jira/browse/CAMEL-23329)

camel-azure-storage-blob - Add support for finding blobs by index tags

[CAMEL-23328](https://issues.apache.org/jira/browse/CAMEL-23328)

camel-azure-storage-blob - Add support for blob index tags (set and get)

[CAMEL-23327](https://issues.apache.org/jira/browse/CAMEL-23327)

Langchain4j agent: document and test structured output

[CAMEL-23079](https://issues.apache.org/jira/browse/CAMEL-23079)

camel-core - Registry for capturing errors during routing messages

[CAMEL-23063](https://issues.apache.org/jira/browse/CAMEL-23063)

Add camel-a2a component for Agent-to-Agent (A2A) protocol integration

[CAMEL-21975](https://issues.apache.org/jira/browse/CAMEL-21975)

camel-jbang - Diagram command to show routes visually

[CAMEL-17598](https://issues.apache.org/jira/browse/CAMEL-17598)

camel-bindy: Handle parse failures

### Sub-task (1)

[CAMEL-23660](https://issues.apache.org/jira/browse/CAMEL-23660)

Provide a weekly Job on Jenkins CI for JDK 26

### Task (40)

[CAMEL-23827](https://issues.apache.org/jira/browse/CAMEL-23827)

camel-threadpoolfactory-vertx: Deprecate

[CAMEL-23826](https://issues.apache.org/jira/browse/CAMEL-23826)

camel-reactive-executor-vertx: Deprecate

[CAMEL-23802](https://issues.apache.org/jira/browse/CAMEL-23802)

camel-jbang - TUI remove tamboui hacks when upgrading to 0.4

[CAMEL-23801](https://issues.apache.org/jira/browse/CAMEL-23801)

documentation - Remove spring boot autoconfiguration

[CAMEL-23780](https://issues.apache.org/jira/browse/CAMEL-23780)

\[camel-jbang\] camel export with jib profile

[CAMEL-23755](https://issues.apache.org/jira/browse/CAMEL-23755)

camel-spring-boot build compilation error due to jooq requiring Java 21

[CAMEL-23750](https://issues.apache.org/jira/browse/CAMEL-23750)

\[build\] Multi manifest Camel CLI container image

[CAMEL-23733](https://issues.apache.org/jira/browse/CAMEL-23733)

camel-jbang - TUI properties files should have colors

[CAMEL-23689](https://issues.apache.org/jira/browse/CAMEL-23689)

camel-headersmap - Deprecate

[CAMEL-23665](https://issues.apache.org/jira/browse/CAMEL-23665)

OpenSearch is using deprecated setTlsDetailsFactory which is no more doing anything

[CAMEL-23648](https://issues.apache.org/jira/browse/CAMEL-23648)

check-container-versions workflow should regenerate metadata.json after updating container.properties

[CAMEL-23612](https://issues.apache.org/jira/browse/CAMEL-23612)

example MapStruct build is failing on CI: class org.apache.http.impl.client.BasicAuthCache cannot be cast to class org.apache.http.client.AuthCache

[CAMEL-23610](https://issues.apache.org/jira/browse/CAMEL-23610)

documentation - Migrate YAML DSL to normalized YAML DSL

[CAMEL-23607](https://issues.apache.org/jira/browse/CAMEL-23607)

camel-github - Removed component caused website build error

[CAMEL-23573](https://issues.apache.org/jira/browse/CAMEL-23573)

camel-tui - Refactor CamelMonitor into per-tab classes

[CAMEL-23563](https://issues.apache.org/jira/browse/CAMEL-23563)

Support @CommandLine.Mixin when generating documentation for Camel CLI commands

[CAMEL-23552](https://issues.apache.org/jira/browse/CAMEL-23552)

camel-api - The JSpecify and null/non-null contracts - part2

[CAMEL-23531](https://issues.apache.org/jira/browse/CAMEL-23531)

documentation: Jackson 3 collides with Jackson 2 on dataformats docs

[CAMEL-23512](https://issues.apache.org/jira/browse/CAMEL-23512)

camel-jbang-plugin-tui: TamboUI API misuse, Unicode bugs, and improvements

[CAMEL-23500](https://issues.apache.org/jira/browse/CAMEL-23500)

Document camel-openai usage with OpenAI-compatible providers (OpenRouter)

[CAMEL-23492](https://issues.apache.org/jira/browse/CAMEL-23492)

Can we avoid npm in the doc build

[CAMEL-23451](https://issues.apache.org/jira/browse/CAMEL-23451)

\[build\] Tests not executed when change affect a non pom.xml directory

[CAMEL-23450](https://issues.apache.org/jira/browse/CAMEL-23450)

Remove usage of unmaintained junit-toolbox

[CAMEL-23435](https://issues.apache.org/jira/browse/CAMEL-23435)

documentation - Getting Started mention Camel Launcher

[CAMEL-23432](https://issues.apache.org/jira/browse/CAMEL-23432)

\[camel-telemetry\] Distinguish custom process from inner process

[CAMEL-23414](https://issues.apache.org/jira/browse/CAMEL-23414)

camel-hazelcast: Allow customization of SerializationConfig on managed Hazelcast instances

[CAMEL-23408](https://issues.apache.org/jira/browse/CAMEL-23408)

camel-jbang - Route diagram with choice and doTry render a line that does not exist

[CAMEL-23407](https://issues.apache.org/jira/browse/CAMEL-23407)

The "binaryMavenPlugins" attribute is deprecated for removal in v5.0.0. Please replace

[CAMEL-23405](https://issues.apache.org/jira/browse/CAMEL-23405)

camel-core - Remove ReifierStrategy

[CAMEL-23404](https://issues.apache.org/jira/browse/CAMEL-23404)

camel-ftp - Improve doc about need for strictHostKeyChecking

[CAMEL-23389](https://issues.apache.org/jira/browse/CAMEL-23389)

Remove usage of deprecated https://packages.atlassian.com/maven-external/ maven repository

[CAMEL-23371](https://issues.apache.org/jira/browse/CAMEL-23371)

Warning for a misconfiguration of dependabot group related to micrometer and opentelemetry

[CAMEL-23364](https://issues.apache.org/jira/browse/CAMEL-23364)

components are promoted to quickly from preview to stable

[CAMEL-22999](https://issues.apache.org/jira/browse/CAMEL-22999)

camel-examples - Some of these examples does not work/test success

[CAMEL-22894](https://issues.apache.org/jira/browse/CAMEL-22894)

Refactor Simple/CSimple language implementation for better maintainability

[CAMEL-22583](https://issues.apache.org/jira/browse/CAMEL-22583)

\[camel-jbang\] Replace org.fusesource.jansi dependency

[CAMEL-22504](https://issues.apache.org/jira/browse/CAMEL-22504)

\[camel-jasypt\] Deprecate and eventually drop CLI entrypoint

[CAMEL-19745](https://issues.apache.org/jira/browse/CAMEL-19745)

camel-cxf-soap - Downloads JARs from 3rd party repo

[CAMEL-19549](https://issues.apache.org/jira/browse/CAMEL-19549)

camel-core: replace Thread.sleep in tests

[CAMEL-19517](https://issues.apache.org/jira/browse/CAMEL-19517)

camel-cxf: replace Thread.sleep in tests

### Test (20)

[CAMEL-23758](https://issues.apache.org/jira/browse/CAMEL-23758)

spring boot Camel SalesforceIT test is failing Detected incompatible Protobuf Gencode/Runtime versions when loading ReplayPreset: gencode 4.35.1, runtime 4.34.2

[CAMEL-23751](https://issues.apache.org/jira/browse/CAMEL-23751)

Sns2HeaderFilterStrategyTest.outboundFiltersCamelAndBreadcrumbHeaders is broken

[CAMEL-23734](https://issues.apache.org/jira/browse/CAMEL-23734)

VertxHttpTransferExceptionTest.testTransferException is failing

[CAMEL-23711](https://issues.apache.org/jira/browse/CAMEL-23711)

Proide automated test for camel-test-infra-jaeger

[CAMEL-23696](https://issues.apache.org/jira/browse/CAMEL-23696)

Cxf spring-boot examples have 3 tests failing

[CAMEL-23675](https://issues.apache.org/jira/browse/CAMEL-23675)

ExportTest.shouldGenerateJavaContent(RuntimeType) is broken

[CAMEL-23672](https://issues.apache.org/jira/browse/CAMEL-23672)

InfrastructureITCase.sendMessageTest is broken

[CAMEL-23671](https://issues.apache.org/jira/browse/CAMEL-23671)

ManagePluginsITCase.testPluginInstallation is broken

[CAMEL-23619](https://issues.apache.org/jira/browse/CAMEL-23619)

CouchBaseTest is failing in camel-examples repository - missign migration to 8.0.0

[CAMEL-23497](https://issues.apache.org/jira/browse/CAMEL-23497)

NPE in a management test

[CAMEL-23430](https://issues.apache.org/jira/browse/CAMEL-23430)

Flaky tests in camel-kafka: KafkaConsumerAutoInstResumeRouteStrategyIT and KafkaIdempotentRepositoryEagerIT

[CAMEL-23429](https://issues.apache.org/jira/browse/CAMEL-23429)

Flaky test: TimerRouteAutoConfigIT in camel-opentelemetry-metrics

[CAMEL-23428](https://issues.apache.org/jira/browse/CAMEL-23428)

Flaky test: RabbitMQProducerInvalidExchangeIT in camel-spring-rabbitmq

[CAMEL-23427](https://issues.apache.org/jira/browse/CAMEL-23427)

Flaky test: SpanPropagationUpstreamTest in camel-telemetry-dev

[CAMEL-23421](https://issues.apache.org/jira/browse/CAMEL-23421)

Upgrade Infinispan test container to 16.2+

[CAMEL-23410](https://issues.apache.org/jira/browse/CAMEL-23410)

Very flaky test LangChain4jEmbeddingsComponentInfinispanTargetIT

[CAMEL-23365](https://issues.apache.org/jira/browse/CAMEL-23365)

camel-spring-boot - Ensure camel-kafka-starter integration tests run on Jenkins daily builds

[CAMEL-23247](https://issues.apache.org/jira/browse/CAMEL-23247)

Test MailContentTypeResolverTest.testCustomContentTypeResolver is regularly failing

[CAMEL-22539](https://issues.apache.org/jira/browse/CAMEL-22539)

\[camel-core\] Flaky unit test

[CAMEL-22525](https://issues.apache.org/jira/browse/CAMEL-22525)

Fix flaky as2 tests with "java.net.BindException: Address already in use"

### Wish (1)

[CAMEL-23403](https://issues.apache.org/jira/browse/CAMEL-23403)

camel-jbang - Move route-diagram render to components/camel-diagram

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).