# Apache camel 4.18.0 Release

## New and Noteworthy

This release is the new Camel 4.18.0 LTS release.

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
      <version>4.18.0</version>
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
      <version>4.18.0</version>
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
| [apache-camel-4.18.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-src.zip.sha512) |
| [apache-camel-4.18.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.xml.sha512) |
| [apache-camel-4.18.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.0/apache-camel-4.18.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (37)

[CAMEL-22998](https://issues.apache.org/jira/browse/CAMEL-22998)

camel-kamelet - Kamelet should inherit route configuration so error handler can take affect

[CAMEL-22997](https://issues.apache.org/jira/browse/CAMEL-22997)

camel-jbang - Using circuit breakers can cause an error creating processor

[CAMEL-22978](https://issues.apache.org/jira/browse/CAMEL-22978)

Camel Bean Constructor Fails to Resolve String Parameters with Quotes in Overloaded Factory Method

[CAMEL-22973](https://issues.apache.org/jira/browse/CAMEL-22973)

camel-core - ClassCastException in Splitter with exchange pooling

[CAMEL-22972](https://issues.apache.org/jira/browse/CAMEL-22972)

camel-as2 - AS2ClientConnection leaks HTTP connections on error paths

[CAMEL-22952](https://issues.apache.org/jira/browse/CAMEL-22952)

Camel JBang cmd receive - does not support when using stub

[CAMEL-22951](https://issues.apache.org/jira/browse/CAMEL-22951)

camel-jbang - The groovy example fails with Caused by: java.lang.IllegalArgumentException: Unsupported scheme: classpath:camel-groovy/Gold.groovy

[CAMEL-22950](https://issues.apache.org/jira/browse/CAMEL-22950)

RecipientList with UseOriginalAggregationStrategy fails to capture exception with NPE

[CAMEL-22947](https://issues.apache.org/jira/browse/CAMEL-22947)

Camel-Google-pubsub: consumer does not properly trigger ACK/NACK callbacks and lacks deliveryAttempt visibility

[CAMEL-22940](https://issues.apache.org/jira/browse/CAMEL-22940)

\[camel-milo\] Cannot configure certificate chain

[CAMEL-22939](https://issues.apache.org/jira/browse/CAMEL-22939)

camel-jbang: observe flag ignored when camel.jbang.dependencies is set

[CAMEL-22937](https://issues.apache.org/jira/browse/CAMEL-22937)

camel-jbang: using different custom ports for both embedded and management server runs into an error

[CAMEL-22936](https://issues.apache.org/jira/browse/CAMEL-22936)

camel-spring-boot - camel health check breaks if one component has exception without message

[CAMEL-22932](https://issues.apache.org/jira/browse/CAMEL-22932)

\[camel-opentelemetry-metrics\] Integration testing failure

[CAMEL-22926](https://issues.apache.org/jira/browse/CAMEL-22926)

GooglePubsubProducer applies HeaderFilterStrategy incorrectly, causing Camel headers to leak as Pub/Sub attributes

[CAMEL-22923](https://issues.apache.org/jira/browse/CAMEL-22923)

camel-jbang - Capturing last message in backlog tracer may hit 1000 limit

[CAMEL-22922](https://issues.apache.org/jira/browse/CAMEL-22922)

Camel JBang stub option is broken when stubbing kafka

[CAMEL-22916](https://issues.apache.org/jira/browse/CAMEL-22916)

camel-ftp - RemoteFileProducer ignores NOOP result when sendNoop() returns false without exception

[CAMEL-22907](https://issues.apache.org/jira/browse/CAMEL-22907)

Consumer errors with bridgeErrorHandler=true and handled=false do not propagate to subroutes

[CAMEL-22904](https://issues.apache.org/jira/browse/CAMEL-22904)

camel-core - Simple language ternary parser should not fail for log expressions

[CAMEL-22898](https://issues.apache.org/jira/browse/CAMEL-22898)

Memory Leak in google PubSub consumer

[CAMEL-22888](https://issues.apache.org/jira/browse/CAMEL-22888)

Most of the docling metadata are missing

[CAMEL-22874](https://issues.apache.org/jira/browse/CAMEL-22874)

Error handler in openapi-contract-first route is invoked twice when using handled(false)

[CAMEL-22858](https://issues.apache.org/jira/browse/CAMEL-22858)

camel-jbang - get history command may only show last step

[CAMEL-22854](https://issues.apache.org/jira/browse/CAMEL-22854)

Camel-Keycloak: KeycloakSecurityPolicy does not validate token issuer

[CAMEL-22849](https://issues.apache.org/jira/browse/CAMEL-22849)

AS2 server/listen does not resolve requestUriPattern wildcards when selecting consumer configuration

[CAMEL-22848](https://issues.apache.org/jira/browse/CAMEL-22848)

camel-file: checksumFileAlgorithm option is ignored due to missing mapping in GenericFileEndpoint

[CAMEL-22833](https://issues.apache.org/jira/browse/CAMEL-22833)

camel-jbang - Yaml DSL file with only templatedRoute is not loaded

[CAMEL-22830](https://issues.apache.org/jira/browse/CAMEL-22830)

camel-salesforce - ReplayId ignored when using multiple routes with same salesforce channel

[CAMEL-22828](https://issues.apache.org/jira/browse/CAMEL-22828)

camel-main - camel.main.endpoint-runtime-statistics-enabled not working since Camel 4.5

[CAMEL-22824](https://issues.apache.org/jira/browse/CAMEL-22824)

camel-core - Choice with bodyAs predicate may cause stream caching to be EOL

[CAMEL-22823](https://issues.apache.org/jira/browse/CAMEL-22823)

Ensure Null Response Entity will be honored when StreamCache kicks in

[CAMEL-22820](https://issues.apache.org/jira/browse/CAMEL-22820)

routeConfiguration onException does not propagate to direct endpoints for consumer-level exceptions

[CAMEL-22816](https://issues.apache.org/jira/browse/CAMEL-22816)

camel-telegram - Messages that don't require chatId fail when chatId is not configured

[CAMEL-22809](https://issues.apache.org/jira/browse/CAMEL-22809)

camel-main export failing to run when using --observe

[CAMEL-22648](https://issues.apache.org/jira/browse/CAMEL-22648)

\[camel-opentelemetry2\] don't propagate headers when creating a new trace

[CAMEL-22429](https://issues.apache.org/jira/browse/CAMEL-22429)

camel-aws2-sns component fails when sending CloudEvents with subjects over 100 characters

### Dependency upgrade (3)

[CAMEL-22982](https://issues.apache.org/jira/browse/CAMEL-22982)

camel-jbang - Upgrade to jkube 1.19

[CAMEL-22979](https://issues.apache.org/jira/browse/CAMEL-22979)

Upgrade to Jolokia 2.5.0

[CAMEL-22896](https://issues.apache.org/jira/browse/CAMEL-22896)

camel-spring-boot - Upgrade to Spring Boot 3.5.10

### Improvement (71)

[CAMEL-22993](https://issues.apache.org/jira/browse/CAMEL-22993)

Camel-Jbang-mcp: For hardening tool, static information and data could a Quarkus MCP Resource

[CAMEL-22991](https://issues.apache.org/jira/browse/CAMEL-22991)

Camel-Jbang-mcp: Support Transform route xml to yaml and yaml to xml in mcp tool

[CAMEL-22988](https://issues.apache.org/jira/browse/CAMEL-22988)

Camel JBang eval command cannot work without camel cli installed

[CAMEL-22985](https://issues.apache.org/jira/browse/CAMEL-22985)

camel-jbang-mcp - Add tool for yaml-dsl-validator

[CAMEL-22984](https://issues.apache.org/jira/browse/CAMEL-22984)

camel-docling - Add advanced docling-serve processing options and return DoclingDocument from JSON operations

[CAMEL-22977](https://issues.apache.org/jira/browse/CAMEL-22977)

DefaultCxfBinding: also populate credentials

[CAMEL-22976](https://issues.apache.org/jira/browse/CAMEL-22976)

Camel-jbang-MCP: Add doc tool for dataformat and language too

[CAMEL-22975](https://issues.apache.org/jira/browse/CAMEL-22975)

Camel-jbang-MCP: Add Kamelets catalog and doc tool

[CAMEL-22974](https://issues.apache.org/jira/browse/CAMEL-22974)

camel-coap - Add option to configure a shared existing soap client

[CAMEL-22971](https://issues.apache.org/jira/browse/CAMEL-22971)

camel-quarkus - Using rest-dsl contract-first should use fine grained vertx-web router

[CAMEL-22968](https://issues.apache.org/jira/browse/CAMEL-22968)

camel-vertx-http: Add configuration option to set TracingPolicy

[CAMEL-22966](https://issues.apache.org/jira/browse/CAMEL-22966)

Camel-LevelDB: Add ObjectInputFilter String pattern parameter in LevelDBAggregationRepository to be used in unmarshall operations

[CAMEL-22964](https://issues.apache.org/jira/browse/CAMEL-22964)

SB platform-http: undertow access log managed by camel logging

[CAMEL-22962](https://issues.apache.org/jira/browse/CAMEL-22962)

camel-jbang - infra run add a --port option

[CAMEL-22958](https://issues.apache.org/jira/browse/CAMEL-22958)

camel-core - EIPs should be able to disabled with String values

[CAMEL-22957](https://issues.apache.org/jira/browse/CAMEL-22957)

Not all the components support virtual threads

[CAMEL-22955](https://issues.apache.org/jira/browse/CAMEL-22955)

camel-core - Add resource function to load resource from classpath

[CAMEL-22954](https://issues.apache.org/jira/browse/CAMEL-22954)

camel-core - Add nested option to simple

[CAMEL-22953](https://issues.apache.org/jira/browse/CAMEL-22953)

camel-core - XML languages that are Namespace should support property placeholders in key/ns

[CAMEL-22949](https://issues.apache.org/jira/browse/CAMEL-22949)

Migrate components from Thread.sleep() to Camel's Task API for retry/backoff delays

[CAMEL-22935](https://issues.apache.org/jira/browse/CAMEL-22935)

camel-core - Allow to add custom functions to simple

[CAMEL-22931](https://issues.apache.org/jira/browse/CAMEL-22931)

camel-jbang - Command to validate YAML DSL file

[CAMEL-22927](https://issues.apache.org/jira/browse/CAMEL-22927)

camel-sql endpoint opening unnecessary connections to the database if service location is enabled

[CAMEL-22925](https://issues.apache.org/jira/browse/CAMEL-22925)

Enhance S3 producer to stream the payload of type GenericFile

[CAMEL-22924](https://issues.apache.org/jira/browse/CAMEL-22924)

Add setAttachment to simple language

[CAMEL-22918](https://issues.apache.org/jira/browse/CAMEL-22918)

camel-openai: Add metadata for header constants

[CAMEL-22917](https://issues.apache.org/jira/browse/CAMEL-22917)

camel-openai: Enable default baseUrl option for https://api.openai.com/v1

[CAMEL-22915](https://issues.apache.org/jira/browse/CAMEL-22915)

Camel-AWS-Polly: Expose headers element as endpoint options

[CAMEL-22914](https://issues.apache.org/jira/browse/CAMEL-22914)

Camel-AWS-Lambda: Add more producer operations

[CAMEL-22909](https://issues.apache.org/jira/browse/CAMEL-22909)

camel-spring-boot - Add camel.ssl.trustAllCertificates support in Spring Boot

[CAMEL-22908](https://issues.apache.org/jira/browse/CAMEL-22908)

camel-jbang - Add extra files to classpath should allow to use relative paths

[CAMEL-22901](https://issues.apache.org/jira/browse/CAMEL-22901)

Stream logs in Camel JBang Test plugin

[CAMEL-22900](https://issues.apache.org/jira/browse/CAMEL-22900)

camel-mail - Allow to use headers for additional mail properties - support smtps protocol

[CAMEL-22885](https://issues.apache.org/jira/browse/CAMEL-22885)

camel-core - Add trimResult to simple language

[CAMEL-22882](https://issues.apache.org/jira/browse/CAMEL-22882)

camel-core - Local assignment for temporary variables in simple expressions

[CAMEL-22880](https://issues.apache.org/jira/browse/CAMEL-22880)

camel-jbang: make kubernetes plugin generated project compatible with camel-dashboard

[CAMEL-22879](https://issues.apache.org/jira/browse/CAMEL-22879)

camel-jbang - Make camel-jbang more roboust when running in cloud with weird HOME dir

[CAMEL-22878](https://issues.apache.org/jira/browse/CAMEL-22878)

camel-core - Add note to from DSL

[CAMEL-22876](https://issues.apache.org/jira/browse/CAMEL-22876)

camel-launcher - remove/handle jbang dependency in camel-jbang-core

[CAMEL-22873](https://issues.apache.org/jira/browse/CAMEL-22873)

camel-core - Add support for ternary operator

[CAMEL-22871](https://issues.apache.org/jira/browse/CAMEL-22871)

camel-core - Add simple function to assign a variable

[CAMEL-22870](https://issues.apache.org/jira/browse/CAMEL-22870)

camel-core - Add elvis operator to simple language

[CAMEL-22868](https://issues.apache.org/jira/browse/CAMEL-22868)

camel-core - Add not variant to startsWith and endsWith operator in simple language

[CAMEL-22867](https://issues.apache.org/jira/browse/CAMEL-22867)

camel-core - Deprecate binary simple language operators with space in name

[CAMEL-22866](https://issues.apache.org/jira/browse/CAMEL-22866)

camel-core - Add base64 functions to simple

[CAMEL-22864](https://issues.apache.org/jira/browse/CAMEL-22864)

Camel-Kafka: Add KafkaSecurityConfigurer utility class to simplify Kafka authentication configuration

[CAMEL-22863](https://issues.apache.org/jira/browse/CAMEL-22863)

Camel-CassandraQL: Add requestTimeout parameter to camel-cassandraql component

[CAMEL-22862](https://issues.apache.org/jira/browse/CAMEL-22862)

camel-core - Simple language - Nested functions

[CAMEL-22856](https://issues.apache.org/jira/browse/CAMEL-22856)

camel-core - Add substring before|after to simple language

[CAMEL-22853](https://issues.apache.org/jira/browse/CAMEL-22853)

camel-core - Add convertTo function to simple language

[CAMEL-22852](https://issues.apache.org/jira/browse/CAMEL-22852)

camel-core - Add length/size function to simple language

[CAMEL-22847](https://issues.apache.org/jira/browse/CAMEL-22847)

camel-core - Optimize simple hash function to calc hash with low memory

[CAMEL-22846](https://issues.apache.org/jira/browse/CAMEL-22846)

camel-file - Write checksum file to store hex in a header

[CAMEL-22844](https://issues.apache.org/jira/browse/CAMEL-22844)

camel-core - Add pretty option to simple language

[CAMEL-22841](https://issues.apache.org/jira/browse/CAMEL-22841)

camel-core - Add concat function to simple language

[CAMEL-22835](https://issues.apache.org/jira/browse/CAMEL-22835)

camel-core - Add upper/lower case functions to simple language

[CAMEL-22834](https://issues.apache.org/jira/browse/CAMEL-22834)

camel-core - Add trim function to simple language

[CAMEL-22832](https://issues.apache.org/jira/browse/CAMEL-22832)

camel-azure-storage-blob: upload big files using uploadBlockBlobFromFile

[CAMEL-22831](https://issues.apache.org/jira/browse/CAMEL-22831)

camel-file-watch: Expose file hash in Exchange headers

[CAMEL-22818](https://issues.apache.org/jira/browse/CAMEL-22818)

camel-core - AdviceWith should pin point to same resource so route coverage can correlate

[CAMEL-22817](https://issues.apache.org/jira/browse/CAMEL-22817)

camel-route-coverage - Improve coverage information to better match when using advicing

[CAMEL-22810](https://issues.apache.org/jira/browse/CAMEL-22810)

camel-jbang - Remove project.build.outputTimestamp in pom.xml when exporting

[CAMEL-22802](https://issues.apache.org/jira/browse/CAMEL-22802)

camel-ice60780 - Add connection status

[CAMEL-22721](https://issues.apache.org/jira/browse/CAMEL-22721)

camel-zipfile - Zip iterator loads file entry into memory

[CAMEL-22646](https://issues.apache.org/jira/browse/CAMEL-22646)

Integrate additional camel-dapr operations

[CAMEL-22601](https://issues.apache.org/jira/browse/CAMEL-22601)

camel-jbang - Allow to route dump without running first

[CAMEL-22277](https://issues.apache.org/jira/browse/CAMEL-22277)

camel-jbang - infra command, specify a custom port

[CAMEL-22093](https://issues.apache.org/jira/browse/CAMEL-22093)

camel-jbang - version list --fresh should persist the result

[CAMEL-21254](https://issues.apache.org/jira/browse/CAMEL-21254)

Camel-Google-Big-Query: Cannot set a different projectId from default in particular conditions

[CAMEL-16826](https://issues.apache.org/jira/browse/CAMEL-16826)

Camel-Azure-Storage-Blob: Add deleteAfterRead option for consumer side

[CAMEL-14470](https://issues.apache.org/jira/browse/CAMEL-14470)

Camel-github: Implement a component supporting kohsuke github-api

### New Feature (30)

[CAMEL-22960](https://issues.apache.org/jira/browse/CAMEL-22960)

Camel-Jbang: Add an harden command and the related tool to camel-jbang-mcp

[CAMEL-22946](https://issues.apache.org/jira/browse/CAMEL-22946)

camel-spring-boot - make it easier to write application access logs only, without management access logs

[CAMEL-22942](https://issues.apache.org/jira/browse/CAMEL-22942)

camel-openai: add support for embeddings

[CAMEL-22929](https://issues.apache.org/jira/browse/CAMEL-22929)

Camel-AWS: Create an AWS Comprehend Spring Boot starter

[CAMEL-22928](https://issues.apache.org/jira/browse/CAMEL-22928)

Camel-AWS: Create an AWS comprehend component

[CAMEL-22921](https://issues.apache.org/jira/browse/CAMEL-22921)

Camel-AWS: Add a Security Hub Spring Boot Starter

[CAMEL-22919](https://issues.apache.org/jira/browse/CAMEL-22919)

Camel-AWS: Add a Security Hub component

[CAMEL-22912](https://issues.apache.org/jira/browse/CAMEL-22912)

Camel-Spring-Boot: Create an AWS Polly starter

[CAMEL-22911](https://issues.apache.org/jira/browse/CAMEL-22911)

Camel-AWS: Add Polly component

[CAMEL-22905](https://issues.apache.org/jira/browse/CAMEL-22905)

Camel-Spring-Boot: Add OCSF dataformat starter

[CAMEL-22903](https://issues.apache.org/jira/browse/CAMEL-22903)

Add OCSF (Open Cybersecurity Schema Framework) DataFormat component

[CAMEL-22899](https://issues.apache.org/jira/browse/CAMEL-22899)

camel-core - Add chain operator to the simple language

[CAMEL-22889](https://issues.apache.org/jira/browse/CAMEL-22889)

Camel-Jbang-MCP: Add the server option as exposing method, not stdio only

[CAMEL-22886](https://issues.apache.org/jira/browse/CAMEL-22886)

Camel-Jbang: Add an MCP module

[CAMEL-22881](https://issues.apache.org/jira/browse/CAMEL-22881)

Camel-Jbang: Add camel explain command to explain Camel routes using AI/LLM

[CAMEL-22859](https://issues.apache.org/jira/browse/CAMEL-22859)

Auto-generate JBang commands documentation

[CAMEL-22851](https://issues.apache.org/jira/browse/CAMEL-22851)

camel-langchain4j-tools - Implement native tool-search-tool

[CAMEL-22850](https://issues.apache.org/jira/browse/CAMEL-22850)

camel-langchain4j-\*: Use Spring Boot starters in Camel Spring Boot

[CAMEL-22843](https://issues.apache.org/jira/browse/CAMEL-22843)

camel-watsonx-ai component

[CAMEL-22822](https://issues.apache.org/jira/browse/CAMEL-22822)

Camel-Chroma: Create a Spring Boot starter

[CAMEL-22821](https://issues.apache.org/jira/browse/CAMEL-22821)

Camel-AWS-parameter-store: Create Spring Boot starter

[CAMEL-22819](https://issues.apache.org/jira/browse/CAMEL-22819)

Camel-AWS: Create a parameter store component

[CAMEL-22815](https://issues.apache.org/jira/browse/CAMEL-22815)

Support for Telegram Bot Payments API (Digital Goods)

[CAMEL-22814](https://issues.apache.org/jira/browse/CAMEL-22814)

Support for Telegram Bot Payments API (Physical Products)

[CAMEL-22805](https://issues.apache.org/jira/browse/CAMEL-22805)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense

[CAMEL-22804](https://issues.apache.org/jira/browse/CAMEL-22804)

Camel-AWS-IAM: Support more operations based on the API available

[CAMEL-22379](https://issues.apache.org/jira/browse/CAMEL-22379)

camel-mina-sftp - FTP component based on Mina SSHD FTP

[CAMEL-22292](https://issues.apache.org/jira/browse/CAMEL-22292)

camel-jbang - camel cmd send to work with infra services

[CAMEL-22179](https://issues.apache.org/jira/browse/CAMEL-22179)

Create AWS Rekognition component

[CAMEL-18272](https://issues.apache.org/jira/browse/CAMEL-18272)

Camel-AWS2-Lambda: Support Function URL management through producer operations

### Sub-task (11)

[CAMEL-22897](https://issues.apache.org/jira/browse/CAMEL-22897)

Camel-Chroma: Remove Spring Boot Starter

[CAMEL-22895](https://issues.apache.org/jira/browse/CAMEL-22895)

Camel-Chroma: Remove the component

[CAMEL-22861](https://issues.apache.org/jira/browse/CAMEL-22861)

Auto-generated Jbang commands documentation: Add support for adding examples

[CAMEL-22842](https://issues.apache.org/jira/browse/CAMEL-22842)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS Kinesis

[CAMEL-22840](https://issues.apache.org/jira/browse/CAMEL-22840)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS Eventbridge

[CAMEL-22838](https://issues.apache.org/jira/browse/CAMEL-22838)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS EKS

[CAMEL-22837](https://issues.apache.org/jira/browse/CAMEL-22837)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS ECS

[CAMEL-22836](https://issues.apache.org/jira/browse/CAMEL-22836)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS EC2

[CAMEL-22829](https://issues.apache.org/jira/browse/CAMEL-22829)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS DynamoDB

[CAMEL-22827](https://issues.apache.org/jira/browse/CAMEL-22827)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS CloudWatch

[CAMEL-22825](https://issues.apache.org/jira/browse/CAMEL-22825)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS Athena

### Task (23)

[CAMEL-22983](https://issues.apache.org/jira/browse/CAMEL-22983)

Several tests are failing with propertyDatabinding errors

[CAMEL-22980](https://issues.apache.org/jira/browse/CAMEL-22980)

Endless loop for org.apache.camel.component.zookeepermaster.group.GroupIT

[CAMEL-22970](https://issues.apache.org/jira/browse/CAMEL-22970)

camel-leveldb - Deprecate

[CAMEL-22961](https://issues.apache.org/jira/browse/CAMEL-22961)

Deprecate Camel-Github

[CAMEL-22956](https://issues.apache.org/jira/browse/CAMEL-22956)

camel-core - Simple function should be grouped

[CAMEL-22944](https://issues.apache.org/jira/browse/CAMEL-22944)

Camel-box: avoid using java.security.SecureRandom in the static initializers

[CAMEL-22938](https://issues.apache.org/jira/browse/CAMEL-22938)

Review changes in OpenTelemtry related to Map with wrong type for key

[CAMEL-22933](https://issues.apache.org/jira/browse/CAMEL-22933)

\[test-infra\] camel-test-infra-cli IT test failure

[CAMEL-22930](https://issues.apache.org/jira/browse/CAMEL-22930)

camel-observation-starter broken in 4.17.0

[CAMEL-22913](https://issues.apache.org/jira/browse/CAMEL-22913)

\[build\] Verify components coverage

[CAMEL-22906](https://issues.apache.org/jira/browse/CAMEL-22906)

\[camel-resilience4j\] Flaky test on JDK25

[CAMEL-22892](https://issues.apache.org/jira/browse/CAMEL-22892)

Weaviate: component documentation advertises different operations then are implemented

[CAMEL-22877](https://issues.apache.org/jira/browse/CAMEL-22877)

\[build\] Error generating source for Dhis and Olingo

[CAMEL-22872](https://issues.apache.org/jira/browse/CAMEL-22872)

camel-core - Missing doc for model onWhen / predicateValidator

[CAMEL-22869](https://issues.apache.org/jira/browse/CAMEL-22869)

cannot build camel-chroma on power and s390 platforms

[CAMEL-22865](https://issues.apache.org/jira/browse/CAMEL-22865)

Add a method to MockValueBuilder that allows json comparison that ignores element order

[CAMEL-22812](https://issues.apache.org/jira/browse/CAMEL-22812)

Deprecate olingo components

[CAMEL-22520](https://issues.apache.org/jira/browse/CAMEL-22520)

\[camel-plc4x\] Implement consumer unit test

[CAMEL-22357](https://issues.apache.org/jira/browse/CAMEL-22357)

Mark topics (from upgrade guide), which are covered by update tool

[CAMEL-20282](https://issues.apache.org/jira/browse/CAMEL-20282)

Keys verification download missing

[CAMEL-19525](https://issues.apache.org/jira/browse/CAMEL-19525)

camel-jetty: replace Thread.sleep in tests

[CAMEL-19524](https://issues.apache.org/jira/browse/CAMEL-19524)

camel-infinispan: replace Thread.sleep in tests

[CAMEL-18941](https://issues.apache.org/jira/browse/CAMEL-18941)

camel-spring-boot - AutoConfigurationMojo imports file creation

### Test (1)

[CAMEL-21196](https://issues.apache.org/jira/browse/CAMEL-21196)

camel-core: modernize throws/no throws assertions

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).