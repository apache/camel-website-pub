# Apache camel 4.15.0 Release

## New and Noteworthy

This release is the new Camel 4.15.0 release.

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
      <version>4.15.0</version>
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
      <version>4.15.0</version>
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
| [apache-camel-4.15.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-src.zip.sha512) |
| [apache-camel-4.15.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.xml.sha512) |
| [apache-camel-4.15.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.15.0/apache-camel-4.15.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.15.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.15.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (28)

[CAMEL-22488](https://issues.apache.org/jira/browse/CAMEL-22488)

camlel-sql - Error when automatically creating JdbcIdempotent table

[CAMEL-22484](https://issues.apache.org/jira/browse/CAMEL-22484)

camel-jbang-kubernetes fails to deploy to openshift when using custom GAV

[CAMEL-22480](https://issues.apache.org/jira/browse/CAMEL-22480)

camel-core - Using property placeholders in endpoint URIs in the context-path containing ? sign can lead to double ? in resolved URI

[CAMEL-22476](https://issues.apache.org/jira/browse/CAMEL-22476)

camel-plc4j - Cannot load drivers when using poll mode

[CAMEL-22474](https://issues.apache.org/jira/browse/CAMEL-22474)

camel-http - HttpActivityListener null exchange when redelivery

[CAMEL-22468](https://issues.apache.org/jira/browse/CAMEL-22468)

camel-bean - Bean cache should initialize later

[CAMEL-22418](https://issues.apache.org/jira/browse/CAMEL-22418)

camel run broken when --runtime quarkus|spring-boot

[CAMEL-22416](https://issues.apache.org/jira/browse/CAMEL-22416)

camel-jbang - Customize server port not working

[CAMEL-22414](https://issues.apache.org/jira/browse/CAMEL-22414)

In 4.14.0, after calling CXF HTTP, the response stream is not cached

[CAMEL-22410](https://issues.apache.org/jira/browse/CAMEL-22410)

SchedulingPollConsumer is not thread safe during graceful shutdown.

[CAMEL-22407](https://issues.apache.org/jira/browse/CAMEL-22407)

camel-jbang-plugin-kubernetes: --config and --resource fails when setting a key or destination file path

[CAMEL-22405](https://issues.apache.org/jira/browse/CAMEL-22405)

camel-ai: agent is unable to support different data types

[CAMEL-22404](https://issues.apache.org/jira/browse/CAMEL-22404)

camel-jbang-plugin-kubernetes: duplicate declaration of camel:observability-services in pom.xml

[CAMEL-22397](https://issues.apache.org/jira/browse/CAMEL-22397)

camel-ai: cannot create multiple agents due to missing route information

[CAMEL-22391](https://issues.apache.org/jira/browse/CAMEL-22391)

camel-core - Disabled does not work for inlined anonymous processors in Java DSL

[CAMEL-22388](https://issues.apache.org/jira/browse/CAMEL-22388)

\[camel-telemetry-dev\] Format hierarchy issue

[CAMEL-22385](https://issues.apache.org/jira/browse/CAMEL-22385)

OpenTelemetry: Unclosed Span Scope with Parallel Multicast

[CAMEL-22384](https://issues.apache.org/jira/browse/CAMEL-22384)

camel-catalog - The route.json for autoStartup should be boolean type

[CAMEL-22380](https://issues.apache.org/jira/browse/CAMEL-22380)

camel-platform-http-main - Authentication path does not work

[CAMEL-22373](https://issues.apache.org/jira/browse/CAMEL-22373)

camel-http - Headers may be lost when calling HTTP service fails and exception is thrown

[CAMEL-22366](https://issues.apache.org/jira/browse/CAMEL-22366)

camel-spring-boot - Nested property placeholder is turned off by mistake

[CAMEL-22364](https://issues.apache.org/jira/browse/CAMEL-22364)

camel-jms - Rare ConcurrentModificationException on message header map when using multiple camel-jms calls after each other in route

[CAMEL-22363](https://issues.apache.org/jira/browse/CAMEL-22363)

camel-azure - EventHub consumer updates checkout on every event

[CAMEL-22359](https://issues.apache.org/jira/browse/CAMEL-22359)

camel-as2: MDN multipart/report parsing issue with no Content-Type

[CAMEL-22352](https://issues.apache.org/jira/browse/CAMEL-22352)

camel-main: DataFormat auto configuration does not work

[CAMEL-22349](https://issues.apache.org/jira/browse/CAMEL-22349)

\[camel-observation\] Observations should not influence metrics

[CAMEL-22335](https://issues.apache.org/jira/browse/CAMEL-22335)

camel jbang kubernetes manifest options not picked up from application.properties

[CAMEL-22094](https://issues.apache.org/jira/browse/CAMEL-22094)

camel-openapi-java - Rest DSL with code-first - ClassCastException in openapi v3.1 parsing complex types

### Dependency upgrade (5)

[CAMEL-22490](https://issues.apache.org/jira/browse/CAMEL-22490)

camel-minio - Upgrade to 8.6.x

[CAMEL-22483](https://issues.apache.org/jira/browse/CAMEL-22483)

camel-debezium - Upgrade to 3.3.x

[CAMEL-22469](https://issues.apache.org/jira/browse/CAMEL-22469)

grpc-netty-shaded - Upgrade to 1.75

[CAMEL-22394](https://issues.apache.org/jira/browse/CAMEL-22394)

camel-vertx - Upgrade to 4.5.20

[CAMEL-22344](https://issues.apache.org/jira/browse/CAMEL-22344)

camel-spring-boot - Upgrade to SB 3.5.5

### Improvement (40)

[CAMEL-22486](https://issues.apache.org/jira/browse/CAMEL-22486)

camel-yaml-dsl - Should we support map and list notation in parameters

[CAMEL-22485](https://issues.apache.org/jira/browse/CAMEL-22485)

camel-core: ContextServicePlugin should support unload operations

[CAMEL-22482](https://issues.apache.org/jira/browse/CAMEL-22482)

camel-plc4j - Should be lenient endpoint

[CAMEL-22473](https://issues.apache.org/jira/browse/CAMEL-22473)

Camel-microsoft-mail doc doesn't contain example for Quarkus runtime

[CAMEL-22471](https://issues.apache.org/jira/browse/CAMEL-22471)

camel-jbang - Send command with file location should use absolute path

[CAMEL-22465](https://issues.apache.org/jira/browse/CAMEL-22465)

camel-solr - Allow multiple occurrences with SolrParam.x headers

[CAMEL-22456](https://issues.apache.org/jira/browse/CAMEL-22456)

Use route.openshift.io to detect the openshift cluster

[CAMEL-22455](https://issues.apache.org/jira/browse/CAMEL-22455)

Use mirror.gcr.io for base image

[CAMEL-22454](https://issues.apache.org/jira/browse/CAMEL-22454)

It would be nice to add a parameter "runtime" to camel-jbang's PluginExperter#getDependencies()

[CAMEL-22453](https://issues.apache.org/jira/browse/CAMEL-22453)

camel-sql - SQL query should support java text blocks

[CAMEL-22451](https://issues.apache.org/jira/browse/CAMEL-22451)

camel-consul - The ConsulClient should be autowired

[CAMEL-22442](https://issues.apache.org/jira/browse/CAMEL-22442)

camel-core - Add fallback resource resolver to load from file as well as classpath

[CAMEL-22441](https://issues.apache.org/jira/browse/CAMEL-22441)

components with supportFileReference should support resource: prefix

[CAMEL-22438](https://issues.apache.org/jira/browse/CAMEL-22438)

camel-catalog - Enum should be type: enum in catalog metadata

[CAMEL-22435](https://issues.apache.org/jira/browse/CAMEL-22435)

Camel CLI Infra run - use the default port for custom implementations

[CAMEL-22432](https://issues.apache.org/jira/browse/CAMEL-22432)

Camel-Kafka: Support breakOnFirstError for Batching mode too

[CAMEL-22430](https://issues.apache.org/jira/browse/CAMEL-22430)

Make FileLockClusterView more resilient to split-brain scenarios

[CAMEL-22422](https://issues.apache.org/jira/browse/CAMEL-22422)

\[camel-telemetry\] exclude processors when added in the filter

[CAMEL-22421](https://issues.apache.org/jira/browse/CAMEL-22421)

camel-mllp - HL7 version 2.5 requires ACK in MSH-9.3 in acknowledgment

[CAMEL-22420](https://issues.apache.org/jira/browse/CAMEL-22420)

camel-core - Detect duplicate processor ids within same route

[CAMEL-22419](https://issues.apache.org/jira/browse/CAMEL-22419)

camel-jbang - Route dumper should output in yaml by default

[CAMEL-22403](https://issues.apache.org/jira/browse/CAMEL-22403)

\[camel-google-pubsub\] Extend headers with some HeaderFilterStrategy

[CAMEL-22400](https://issues.apache.org/jira/browse/CAMEL-22400)

camel-zipfile - Add support for empty zip files / entries

[CAMEL-22398](https://issues.apache.org/jira/browse/CAMEL-22398)

camel-ai: allow agents to define the specifics of the exchange body

[CAMEL-22396](https://issues.apache.org/jira/browse/CAMEL-22396)

camel-test - Using @MockEndpoints is not allowed together with interceptSendToEndpoint

[CAMEL-22387](https://issues.apache.org/jira/browse/CAMEL-22387)

camel-quartz graceful shutdown issue

[CAMEL-22382](https://issues.apache.org/jira/browse/CAMEL-22382)

camel-main - Add authenticationRealm for server security

[CAMEL-22381](https://issues.apache.org/jira/browse/CAMEL-22381)

camel-platform-http-vertx - Do not log ERROR for unauthenticated requests

[CAMEL-22375](https://issues.apache.org/jira/browse/CAMEL-22375)

Enhance CamelContext API to get a list of groups

[CAMEL-22372](https://issues.apache.org/jira/browse/CAMEL-22372)

camel-langchain4j-embeddings : store the result embedding

[CAMEL-22370](https://issues.apache.org/jira/browse/CAMEL-22370)

camel-graphql - Allow to use custom HttpClient

[CAMEL-22368](https://issues.apache.org/jira/browse/CAMEL-22368)

camel-catalog - Add support for validating JQ language

[CAMEL-22365](https://issues.apache.org/jira/browse/CAMEL-22365)

Make additional sensitive words configurable in UriSupport.sanitizeUri

[CAMEL-22362](https://issues.apache.org/jira/browse/CAMEL-22362)

camel-exec - Use quote safe arg parser

[CAMEL-22356](https://issues.apache.org/jira/browse/CAMEL-22356)

Allow Google PubSub/Lite consumer pass exception through error handler

[CAMEL-22354](https://issues.apache.org/jira/browse/CAMEL-22354)

dataformats - Align all data formats getter setters to model

[CAMEL-22334](https://issues.apache.org/jira/browse/CAMEL-22334)

camel-ai: avoid deep nested classes

[CAMEL-22300](https://issues.apache.org/jira/browse/CAMEL-22300)

camel-jbang - Add IBM MQ test infra

[CAMEL-22011](https://issues.apache.org/jira/browse/CAMEL-22011)

camel-xslt - Allow to take input as JSon instead of XML

[CAMEL-21268](https://issues.apache.org/jira/browse/CAMEL-21268)

Google PubSub - pass headers (breadcrumb+) from publisher to subscriber

### New Feature (25)

[CAMEL-22487](https://issues.apache.org/jira/browse/CAMEL-22487)

Camel-Keycloak: Create a Consumer for user and admin events

[CAMEL-22481](https://issues.apache.org/jira/browse/CAMEL-22481)

Camel-Keycloak: Add more operations to producer

[CAMEL-22475](https://issues.apache.org/jira/browse/CAMEL-22475)

camel-langchain4j-agent : add the possibility to include custom tools / fonctions

[CAMEL-22470](https://issues.apache.org/jira/browse/CAMEL-22470)

Camel-Keycloak: Add test-infra module for Keycloak

[CAMEL-22464](https://issues.apache.org/jira/browse/CAMEL-22464)

Camel-Keycloak: Create producer for managing operations

[CAMEL-22462](https://issues.apache.org/jira/browse/CAMEL-22462)

Camel-Keycloak: Create Spring Boot Starter

[CAMEL-22459](https://issues.apache.org/jira/browse/CAMEL-22459)

Camel-Keycloak: Support permission based policies

[CAMEL-22457](https://issues.apache.org/jira/browse/CAMEL-22457)

Camel-Keycloak: Adding publicKey to the access token verification

[CAMEL-22445](https://issues.apache.org/jira/browse/CAMEL-22445)

Camel-AWS2-S3 Streaming Upload: Implement timestamp-based file grouping for AWS S3 streaming upload

[CAMEL-22440](https://issues.apache.org/jira/browse/CAMEL-22440)

Camel-AWS2-S3 Streaming upload: Add a timestamp naming strategy

[CAMEL-22437](https://issues.apache.org/jira/browse/CAMEL-22437)

Create Camel-Docling Spring Boot starter

[CAMEL-22433](https://issues.apache.org/jira/browse/CAMEL-22433)

Create a Camel Docling component

[CAMEL-22426](https://issues.apache.org/jira/browse/CAMEL-22426)

Create AWS Transcribe Starter for Spring-Boot

[CAMEL-22425](https://issues.apache.org/jira/browse/CAMEL-22425)

Create AWS Textract Starter for Spring-Boot

[CAMEL-22424](https://issues.apache.org/jira/browse/CAMEL-22424)

Create AWS Transcribe component

[CAMEL-22423](https://issues.apache.org/jira/browse/CAMEL-22423)

Make Camel extensible from 3d party dependencies via ServiceLoader

[CAMEL-22392](https://issues.apache.org/jira/browse/CAMEL-22392)

camel-resilience4j - Add micrometer support

[CAMEL-22361](https://issues.apache.org/jira/browse/CAMEL-22361)

camel-groovy-xml - Add data format that uses groovy xml so we dont need POJOs

[CAMEL-22337](https://issues.apache.org/jira/browse/CAMEL-22337)

camel-jbang : camel debug a quarkus app

[CAMEL-22178](https://issues.apache.org/jira/browse/CAMEL-22178)

Create AWS Textract component

[CAMEL-21889](https://issues.apache.org/jira/browse/CAMEL-21889)

\[camel-mdc\] Create a new component to handle MDC

[CAMEL-21869](https://issues.apache.org/jira/browse/CAMEL-21869)

\[camel-observation2\] Onboard a new implementation based on camel-telemetry

[CAMEL-21597](https://issues.apache.org/jira/browse/CAMEL-21597)

Camel AWS Bedrock: Support Amazon Nova models

[CAMEL-18597](https://issues.apache.org/jira/browse/CAMEL-18597)

Make Circuit Breakers and friends observable

[CAMEL-8249](https://issues.apache.org/jira/browse/CAMEL-8249)

camel-keycloak - A security component

### Task (22)

[CAMEL-22489](https://issues.apache.org/jira/browse/CAMEL-22489)

\[camel-core\]: enable cloud location .properties file

[CAMEL-22467](https://issues.apache.org/jira/browse/CAMEL-22467)

Move EmbeddingStoreFactory to an api module

[CAMEL-22466](https://issues.apache.org/jira/browse/CAMEL-22466)

Clean up spring-boot version references within camel project

[CAMEL-22461](https://issues.apache.org/jira/browse/CAMEL-22461)

camel-langchain4j-embeddingstore - set the embedding store from factory if factory isn't null

[CAMEL-22450](https://issues.apache.org/jira/browse/CAMEL-22450)

Camel JBang update dependency is failing when kamelet is missing some mandatory parameters in a Pipe file

[CAMEL-22448](https://issues.apache.org/jira/browse/CAMEL-22448)

Camel JBang dependency update is not adding dependency for component in Intercept/Intercept From/Intercept Send To Endpoint

[CAMEL-22447](https://issues.apache.org/jira/browse/CAMEL-22447)

Camel JBang Dependency update is not adding dependencies iif there is an OnException not configured

[CAMEL-22446](https://issues.apache.org/jira/browse/CAMEL-22446)

Camel JBang update dependency is failing for Avro Kamelet

[CAMEL-22444](https://issues.apache.org/jira/browse/CAMEL-22444)

Camel JBang update dependency is failing with NPE when Bean component is not yet configured

[CAMEL-22443](https://issues.apache.org/jira/browse/CAMEL-22443)

Camel JBang update dependency is failing when component/kamelet/processor is missing some mandatory parameters

[CAMEL-22428](https://issues.apache.org/jira/browse/CAMEL-22428)

Camel-AWS2-Transcribe: Improve Headers metadata in constant class

[CAMEL-22427](https://issues.apache.org/jira/browse/CAMEL-22427)

Camel-AWS2-Textract: Improve Headers metadata in constant class

[CAMEL-22413](https://issues.apache.org/jira/browse/CAMEL-22413)

Provide kamelet component vs. kamelet EIP info in catalog

[CAMEL-22412](https://issues.apache.org/jira/browse/CAMEL-22412)

Create a langchain4j-embeddingstore component

[CAMEL-22406](https://issues.apache.org/jira/browse/CAMEL-22406)

camel-jbang: update documentation around --observe

[CAMEL-22402](https://issues.apache.org/jira/browse/CAMEL-22402)

camel-resilience4j - Micrometer support throws NPE in Camel Quarkus

[CAMEL-22386](https://issues.apache.org/jira/browse/CAMEL-22386)

camel-catalog - Some components with boolean option should have defaultValue as boolean type in json metadata

[CAMEL-22376](https://issues.apache.org/jira/browse/CAMEL-22376)

camel-netty - Remove old deprecated options

[CAMEL-22374](https://issues.apache.org/jira/browse/CAMEL-22374)

Add documentation for group

[CAMEL-22371](https://issues.apache.org/jira/browse/CAMEL-22371)

camel-ognl - Deprecate

[CAMEL-21810](https://issues.apache.org/jira/browse/CAMEL-21810)

camel-jbang - Generated readme.md and Dockerfile are Quarkus specific

[CAMEL-21598](https://issues.apache.org/jira/browse/CAMEL-21598)

Camel AWS Bedrock: Update supported models

### Test (3)

[CAMEL-22452](https://issues.apache.org/jira/browse/CAMEL-22452)

camel-consul - Test errors about invalid key

[CAMEL-22399](https://issues.apache.org/jira/browse/CAMEL-22399)

camel-aws-sqs - SqsBatchConsumerConcurrentConsumersIT test failure

[CAMEL-20374](https://issues.apache.org/jira/browse/CAMEL-20374)

camel-google-pubsub - MessageOrderingIT is failing

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).