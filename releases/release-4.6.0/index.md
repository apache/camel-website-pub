# Apache camel 4.6.0 Release

## New and Noteworthy

This release is the new Camel 4.6.0 release.

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
      <version>4.6.0</version>
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
      <version>4.6.0</version>
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
| [apache-camel-4.6.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-src.zip.sha512) |
| [apache-camel-4.6.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.xml.sha512) |
| [apache-camel-4.6.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.6.0/apache-camel-4.6.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.6.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.6.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (37)

[CAMEL-20737](https://issues.apache.org/jira/browse/CAMEL-20737)

camel-jbang - Export to spring boot does not include jdbc driver

[CAMEL-20732](https://issues.apache.org/jira/browse/CAMEL-20732)

RestDefinition does not properly handle array of primitives for\` in/out types

[CAMEL-20731](https://issues.apache.org/jira/browse/CAMEL-20731)

Route coverage fails on routes with multiple doCatch blocks

[CAMEL-20724](https://issues.apache.org/jira/browse/CAMEL-20724)

camel-saxon: xquery fluent API does not work with namespaces (regression)

[CAMEL-20718](https://issues.apache.org/jira/browse/CAMEL-20718)

\[camel-kafka\] Fix JMSRedelivered in JMSDeserializer

[CAMEL-20717](https://issues.apache.org/jira/browse/CAMEL-20717)

camel-mllp - Exception not thrown in TcpSocketConsumerRunnable line 192

[CAMEL-20716](https://issues.apache.org/jira/browse/CAMEL-20716)

camel-quickfix - Exception not thrown in FixMessageRouter line 102

[CAMEL-20715](https://issues.apache.org/jira/browse/CAMEL-20715)

camel-olingo2 and 4 - ApiName DEFAULT should be accepted

[CAMEL-20713](https://issues.apache.org/jira/browse/CAMEL-20713)

Equals() in TagData doesn't check the type of parameter

[CAMEL-20710](https://issues.apache.org/jira/browse/CAMEL-20710)

Strings are compared with != in NettyServerBootstrapConfiguration

[CAMEL-20707](https://issues.apache.org/jira/browse/CAMEL-20707)

Two Optionals in HttpComponentVerifierExtension are checked for null

[CAMEL-20703](https://issues.apache.org/jira/browse/CAMEL-20703)

Typo in OutputAwareFromDefinitionDeserializer - non-null string literal is null checked

[CAMEL-20700](https://issues.apache.org/jira/browse/CAMEL-20700)

camel-core: ReflectionHelper.setField may fail for numeric type fields

[CAMEL-20699](https://issues.apache.org/jira/browse/CAMEL-20699)

camel-azure-servicebus: Broker properties not propagated to Camel Exchange

[CAMEL-20693](https://issues.apache.org/jira/browse/CAMEL-20693)

camel-azure-servicebus: Service Bus Listener Not Stopping After Stopping Route in Latest Camel Version(4.4.0)

[CAMEL-20692](https://issues.apache.org/jira/browse/CAMEL-20692)

camel-cxf - No Payload is logged when the logging feature is enabled

[CAMEL-20691](https://issues.apache.org/jira/browse/CAMEL-20691)

camel-azure-servicebus: Broker properties should not be propagated into application properties

[CAMEL-20678](https://issues.apache.org/jira/browse/CAMEL-20678)

camel-google-sheets - Error setting scopes parameter when using google-sheets-stream

[CAMEL-20677](https://issues.apache.org/jira/browse/CAMEL-20677)

camel-hazelcast: Seda nested transactions are not allowed

[CAMEL-20676](https://issues.apache.org/jira/browse/CAMEL-20676)

camel-snmp - Delay cannot be configured

[CAMEL-20672](https://issues.apache.org/jira/browse/CAMEL-20672)

Camel-jbang does not use application.properties when run with --source-dir

[CAMEL-20669](https://issues.apache.org/jira/browse/CAMEL-20669)

Camel-jbang export does not work if camel.jbang.metrics=true

[CAMEL-20663](https://issues.apache.org/jira/browse/CAMEL-20663)

camel-main: baseMainSupport may fail to doConfigureCamelContextFromMainConfiguration

[CAMEL-20656](https://issues.apache.org/jira/browse/CAMEL-20656)

camel-vertx-websocket - Error when using consumeAsClient and upgrade to websocket because of invalid query parameters

[CAMEL-20640](https://issues.apache.org/jira/browse/CAMEL-20640)

rest-dsl - Using code first and setting consumes/produces on rest configuration should be used for api-doc

[CAMEL-20637](https://issues.apache.org/jira/browse/CAMEL-20637)

camel-rest-dsl - Matching rest operation may not select correct

[CAMEL-20635](https://issues.apache.org/jira/browse/CAMEL-20635)

camel-jbang - Export to quarkus does not work with newer Q releases

[CAMEL-20628](https://issues.apache.org/jira/browse/CAMEL-20628)

camel-micrometer-starter - Potential NPE due to CamelContext not set

[CAMEL-20624](https://issues.apache.org/jira/browse/CAMEL-20624)

camel-http - OAuth2 support adds duplicate Authorization header if one already exists on the Exchange

[CAMEL-20615](https://issues.apache.org/jira/browse/CAMEL-20615)

YAML DSL issue with variables

[CAMEL-20614](https://issues.apache.org/jira/browse/CAMEL-20614)

KameletConsumerNotAvailableException is thrown when two or more threads call toD

[CAMEL-20613](https://issues.apache.org/jira/browse/CAMEL-20613)

ConcurrentModificationException when a new endpoint is created with toD

[CAMEL-20521](https://issues.apache.org/jira/browse/CAMEL-20521)

camel-amqp - AMQP publisher application is losing messages with local JMS transaction enabled

[CAMEL-20388](https://issues.apache.org/jira/browse/CAMEL-20388)

Salesforce component does not handshake on the connection failure

[CAMEL-19730](https://issues.apache.org/jira/browse/CAMEL-19730)

Camel-AS2: client connection pool problems

[CAMEL-19358](https://issues.apache.org/jira/browse/CAMEL-19358)

camel-kafka - Kafka consumer is still able to consume message with keepOpen as true in ThrottlingExceptionRoutePolicy

[CAMEL-18017](https://issues.apache.org/jira/browse/CAMEL-18017)

camel-as2 - Signed content in MDN gets corrupted and is not possible to validate

### Dependency upgrade (7)

[CAMEL-20734](https://issues.apache.org/jira/browse/CAMEL-20734)

Aws-xray: bump of aws-xray-recorder-sdk-bom brought conflict in dependencies

[CAMEL-20720](https://issues.apache.org/jira/browse/CAMEL-20720)

camel-jbang - Upgrade camel-k command to CK 2.3.0

[CAMEL-20689](https://issues.apache.org/jira/browse/CAMEL-20689)

camel-spring-boot - Upgrade to SB 3.2.5

[CAMEL-20661](https://issues.apache.org/jira/browse/CAMEL-20661)

camel-crypto: does not work with BouncyCastle 1.78

[CAMEL-20571](https://issues.apache.org/jira/browse/CAMEL-20571)

camel-infinispan: Upgrade to 15.x

[CAMEL-20473](https://issues.apache.org/jira/browse/CAMEL-20473)

camel-kafka - Upgrade to 3.7.x

[CAMEL-19164](https://issues.apache.org/jira/browse/CAMEL-19164)

camel-as2 - Upgrade to HttpComponents 5.x

### Improvement (46)

[CAMEL-20736](https://issues.apache.org/jira/browse/CAMEL-20736)

camel-jbang - Catalog downloaded should not start CamelContext

[CAMEL-20735](https://issues.apache.org/jira/browse/CAMEL-20735)

camel-jbang - Add support for spring-boot datasource

[CAMEL-20733](https://issues.apache.org/jira/browse/CAMEL-20733)

camel-catalog - Make log eip and component name more easier to see difference

[CAMEL-20730](https://issues.apache.org/jira/browse/CAMEL-20730)

camel-jbang - Parse OSGi blueprint <camelContext> attributes

[CAMEL-20727](https://issues.apache.org/jira/browse/CAMEL-20727)

camel-azure - Data lake upload should not read content into memory

[CAMEL-20721](https://issues.apache.org/jira/browse/CAMEL-20721)

camel-jbang - Make it possible to set logging-level per package individually from CLI

[CAMEL-20719](https://issues.apache.org/jira/browse/CAMEL-20719)

camel-milvus: Exclude troublesome bulk writer related dependencies

[CAMEL-20701](https://issues.apache.org/jira/browse/CAMEL-20701)

camel-kafka: simplify de-serialization of JMS headers

[CAMEL-20698](https://issues.apache.org/jira/browse/CAMEL-20698)

YAML DSL Consistency question - RegistryBeanDefinition vs TemplatedRouteBeanDefinition

[CAMEL-20696](https://issues.apache.org/jira/browse/CAMEL-20696)

camel-sql - Add support for using variables with named query parameters

[CAMEL-20695](https://issues.apache.org/jira/browse/CAMEL-20695)

camel-kotlin-api - Add setHeaders/setVariables EIP

[CAMEL-20688](https://issues.apache.org/jira/browse/CAMEL-20688)

camel-core - Allow @PropertyInject to split a string into array via delimiter option

[CAMEL-20687](https://issues.apache.org/jira/browse/CAMEL-20687)

camel-kamelet - Make kamelets that have ids assigned - to use nodePrefixId for avoid duplicate id clashes

[CAMEL-20685](https://issues.apache.org/jira/browse/CAMEL-20685)

camel-jbang - Debug with doTry .. doCatch .. doFinally should only step actual used

[CAMEL-20684](https://issues.apache.org/jira/browse/CAMEL-20684)

camel-microprofile-fault-tolerance: ThreadTimer should be a singleton

[CAMEL-20675](https://issues.apache.org/jira/browse/CAMEL-20675)

camel-spring-boot: move cluster service implementations to dedicated starters

[CAMEL-20674](https://issues.apache.org/jira/browse/CAMEL-20674)

camel-core - XML DSL should trim endpoint uris

[CAMEL-20673](https://issues.apache.org/jira/browse/CAMEL-20673)

camel-core - Add type converter for string to TimeUnit

[CAMEL-20670](https://issues.apache.org/jira/browse/CAMEL-20670)

camel-platform-http-vertx: Multipart attachment id should be consistent with other HTTP components

[CAMEL-20667](https://issues.apache.org/jira/browse/CAMEL-20667)

YAML DSL Consistency question - ErrorHandlerDefinition vs ErrorHandlerFactory

[CAMEL-20666](https://issues.apache.org/jira/browse/CAMEL-20666)

RouteDefinition DSL Consistency for XML vs YAML DSL

[CAMEL-20665](https://issues.apache.org/jira/browse/CAMEL-20665)

YAML DSL Inconsistency - StreamCaching vs streamCache

[CAMEL-20662](https://issues.apache.org/jira/browse/CAMEL-20662)

camel-grpc: Add more consumer options for the Netty server setup

[CAMEL-20652](https://issues.apache.org/jira/browse/CAMEL-20652)

camel-rest - Contract First - Make it possible to build response from example data

[CAMEL-20651](https://issues.apache.org/jira/browse/CAMEL-20651)

camel-jbang - The open-api should use the new contract-first openapi

[CAMEL-20650](https://issues.apache.org/jira/browse/CAMEL-20650)

camel-spring-boot - Platform http should report server port

[CAMEL-20649](https://issues.apache.org/jira/browse/CAMEL-20649)

camel-test-infra-artemis: stop using a custom container for Artemis

[CAMEL-20644](https://issues.apache.org/jira/browse/CAMEL-20644)

Camel-AWS-Bedrock-Agent-Runtime: Support usage of sessionId to continue the same session with the knowledge base

[CAMEL-20643](https://issues.apache.org/jira/browse/CAMEL-20643)

camel-opentelemetry - OpenTelemetryTracingStrategy does not propagate OpenTelemetry Context in some cases

[CAMEL-20641](https://issues.apache.org/jira/browse/CAMEL-20641)

Camel-AWS-Bedrock-Agent: Add information about failures in ingestion job as header

[CAMEL-20639](https://issues.apache.org/jira/browse/CAMEL-20639)

Support Strimzi KafkaTopic endpoint reference in Pipes

[CAMEL-20633](https://issues.apache.org/jira/browse/CAMEL-20633)

camel-rest-dsl - Client request validation should return 405 for missing body

[CAMEL-20631](https://issues.apache.org/jira/browse/CAMEL-20631)

Support Knative endpoint references in Pipes

[CAMEL-20629](https://issues.apache.org/jira/browse/CAMEL-20629)

camel-platform-http-vertx - Header filter strategy should be HttpHeaderFilterStrategy

[CAMEL-20623](https://issues.apache.org/jira/browse/CAMEL-20623)

camel-rest-openapi - Use another json validator that is jakartaee compatible

[CAMEL-20622](https://issues.apache.org/jira/browse/CAMEL-20622)

camel-qdrant: add support for collection info

[CAMEL-20621](https://issues.apache.org/jira/browse/CAMEL-20621)

camel-core - Single scheduled thread pool should have max queue of 1

[CAMEL-20620](https://issues.apache.org/jira/browse/CAMEL-20620)

camel-platform-http-vertx - Path parameters should not leak back to calling client

[CAMEL-20607](https://issues.apache.org/jira/browse/CAMEL-20607)

camel-core - Using variableReceive should only set result if exchange was process succesfully

[CAMEL-20606](https://issues.apache.org/jira/browse/CAMEL-20606)

Add Camel K bind command

[CAMEL-20546](https://issues.apache.org/jira/browse/CAMEL-20546)

Move dataformat,language json into META-INF

[CAMEL-20514](https://issues.apache.org/jira/browse/CAMEL-20514)

camel-model - Add support for bean constructors for beans in route templates or kamelets

[CAMEL-20492](https://issues.apache.org/jira/browse/CAMEL-20492)

camel-core - Rest DSL with clientRequestValidation can support allowed values

[CAMEL-20266](https://issues.apache.org/jira/browse/CAMEL-20266)

camel-azure-eventbus - Use high-level client (ServiceBusProcessorClient)

[CAMEL-19779](https://issues.apache.org/jira/browse/CAMEL-19779)

camel-core: investigate externalizing large builtin texts

[CAMEL-15279](https://issues.apache.org/jira/browse/CAMEL-15279)

Camel-AS2 - mdn message handling and also Receipt-Delivery-Option header

### New Feature (9)

[CAMEL-20723](https://issues.apache.org/jira/browse/CAMEL-20723)

Add a Pinecone Spring Boot Starter component

[CAMEL-20702](https://issues.apache.org/jira/browse/CAMEL-20702)

Add a Pinecone component

[CAMEL-20694](https://issues.apache.org/jira/browse/CAMEL-20694)

camel-core - Add serVariables EIP to set multiple at once

[CAMEL-20625](https://issues.apache.org/jira/browse/CAMEL-20625)

Create a camel-google-pubsub-lite component

[CAMEL-20574](https://issues.apache.org/jira/browse/CAMEL-20574)

Camel-Milvus: Add more producer operation

[CAMEL-20557](https://issues.apache.org/jira/browse/CAMEL-20557)

camel-rest - Add openapi to rest-dsl so you can expose rest services from existing schema

[CAMEL-20095](https://issues.apache.org/jira/browse/CAMEL-20095)

Create a component for OpenAI

[CAMEL-19253](https://issues.apache.org/jira/browse/CAMEL-19253)

camel-jbang - Make it easier to use JDBC datasource

[CAMEL-19041](https://issues.apache.org/jira/browse/CAMEL-19041)

camel-jbang - Run with runtime

### Sub-task (6)

[CAMEL-20642](https://issues.apache.org/jira/browse/CAMEL-20642)

Camel-AWS-Bedrock: Support Anthropic Haiku model

[CAMEL-20562](https://issues.apache.org/jira/browse/CAMEL-20562)

Camel-AWS-Bedrock: Support Mistral AI models

[CAMEL-20513](https://issues.apache.org/jira/browse/CAMEL-20513)

Camel-AWS-Bedrock: Support Amazon Titan Multimodal Embeddings G1 Model

[CAMEL-20506](https://issues.apache.org/jira/browse/CAMEL-20506)

Google Mail Stream CloudEvent transformer

[CAMEL-20505](https://issues.apache.org/jira/browse/CAMEL-20505)

Google Calendar Streams CloudEvent Transformer

[CAMEL-20454](https://issues.apache.org/jira/browse/CAMEL-20454)

Google Sheets CloudEvent transformer

### Task (16)

[CAMEL-20714](https://issues.apache.org/jira/browse/CAMEL-20714)

SourceCache implements Externalizable but doesn't have a public no-arg constructor

[CAMEL-20705](https://issues.apache.org/jira/browse/CAMEL-20705)

camel-core: ScheduledPollConsumer has non-atomic operations on volatile fields

[CAMEL-20671](https://issues.apache.org/jira/browse/CAMEL-20671)

camel-core-model - DSL description should be attribute and not element in json metadata

[CAMEL-20658](https://issues.apache.org/jira/browse/CAMEL-20658)

camel-kafka: make the subscription logic flexible

[CAMEL-20632](https://issues.apache.org/jira/browse/CAMEL-20632)

Dox not showing up for Camel langchain4j chat component

[CAMEL-20626](https://issues.apache.org/jira/browse/CAMEL-20626)

deprecate JavaScript and JavaShell experimental DSLs

[CAMEL-20611](https://issues.apache.org/jira/browse/CAMEL-20611)

camel-langchain - Rename to camel-langchain4j

[CAMEL-20610](https://issues.apache.org/jira/browse/CAMEL-20610)

camel-spring-boot - camel-k-starter should be in dsl-starter

[CAMEL-20575](https://issues.apache.org/jira/browse/CAMEL-20575)

Camel-Milvus: Improve documentation

[CAMEL-20499](https://issues.apache.org/jira/browse/CAMEL-20499)

tests: consolidate failsafe configuration

[CAMEL-20383](https://issues.apache.org/jira/browse/CAMEL-20383)

camel CI: investigate consolidating Jenkinsfiles

[CAMEL-20113](https://issues.apache.org/jira/browse/CAMEL-20113)

camel-tests: investigate consolidating tests

[CAMEL-19713](https://issues.apache.org/jira/browse/CAMEL-19713)

camel-endpointdsl: logging does not work during tests

[CAMEL-19543](https://issues.apache.org/jira/browse/CAMEL-19543)

camel-sjms2: replace Thread.sleep in tests

[CAMEL-19535](https://issues.apache.org/jira/browse/CAMEL-19535)

camel-master: replace Thread.sleep in tests

[CAMEL-19533](https://issues.apache.org/jira/browse/CAMEL-19533)

camel-mail: replace Thread.sleep in tests

### Test (1)

[CAMEL-19797](https://issues.apache.org/jira/browse/CAMEL-19797)

tests: Flakiness due to artemis connections failures

### Wish (1)

[CAMEL-20646](https://issues.apache.org/jira/browse/CAMEL-20646)

camel-catalog - Use "labels" in the properties from the models catalog

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).