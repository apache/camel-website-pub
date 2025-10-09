# Apache camel 4.5.0 Release

## New and Noteworthy

This release is the new Camel 4.5.0 release.

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
      <version>4.5.0</version>
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
      <version>4.5.0</version>
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
| [apache-camel-4.5.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-src.zip.sha512) |
| [apache-camel-4.5.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.xml.sha512) |
| [apache-camel-4.5.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.5.0/apache-camel-4.5.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.5.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.5.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (35)

[CAMEL-20597](https://issues.apache.org/jira/browse/CAMEL-20597)

camel-salesforce - NullPointerException when query header is missing

[CAMEL-20588](https://issues.apache.org/jira/browse/CAMEL-20588)

camel-salesforce: java.lang.IllegalArgumentException: Request header too large Exception

[CAMEL-20579](https://issues.apache.org/jira/browse/CAMEL-20579)

camel-xchange: ticker action may throw NotYetImplementedForExchangeException

[CAMEL-20577](https://issues.apache.org/jira/browse/CAMEL-20577)

Spring Beans XML Camel context duplicates rest routes defined in java or xml-io DSL

[CAMEL-20576](https://issues.apache.org/jira/browse/CAMEL-20576)

camel-jbang-plugin-k run command kebab-case parsing invalid

[CAMEL-20563](https://issues.apache.org/jira/browse/CAMEL-20563)

camel-kafka - breakOnFirstError causes thread and memory leaks

[CAMEL-20558](https://issues.apache.org/jira/browse/CAMEL-20558)

Ability to use the old Micrometer meter names does not work on MicrometerExchangeEventNotifier

[CAMEL-20551](https://issues.apache.org/jira/browse/CAMEL-20551)

camel-core: Default registry should not ignore beans in repositories

[CAMEL-20549](https://issues.apache.org/jira/browse/CAMEL-20549)

camel-kafka - Using sslKeystoreType should work with PEM

[CAMEL-20545](https://issues.apache.org/jira/browse/CAMEL-20545)

AdviceWith -> replaceFromWith fails when using several templated routes

[CAMEL-20542](https://issues.apache.org/jira/browse/CAMEL-20542)

camel-spring-boot - Using Duration as option may fail

[CAMEL-20532](https://issues.apache.org/jira/browse/CAMEL-20532)

camel-test-infra: singleton services should not be allowed to stop/start services manually

[CAMEL-20530](https://issues.apache.org/jira/browse/CAMEL-20530)

camel-mongodb: unable to convert InputStream to org.bson.conversions.Bson

[CAMEL-20526](https://issues.apache.org/jira/browse/CAMEL-20526)

Jbang camel CLI "run" and "log" commands are not working on Windows environments

[CAMEL-20523](https://issues.apache.org/jira/browse/CAMEL-20523)

camel-xpath - The resultQName converter is wrong causing CSB not to work with xpath in language endpoint

[CAMEL-20517](https://issues.apache.org/jira/browse/CAMEL-20517)

camel-jbang-plugin-k doesn't recognize command

[CAMEL-20512](https://issues.apache.org/jira/browse/CAMEL-20512)

camel-jbang - camel debug may not work on windows

[CAMEL-20509](https://issues.apache.org/jira/browse/CAMEL-20509)

camel-jbang - Loading custom kamelets from relative file dir does not work

[CAMEL-20498](https://issues.apache.org/jira/browse/CAMEL-20498)

camel-http OAuth2 support is not adding the text "Bearer " to the Authorization header

[CAMEL-20487](https://issues.apache.org/jira/browse/CAMEL-20487)

REST API generator issue with typeOut

[CAMEL-20483](https://issues.apache.org/jira/browse/CAMEL-20483)

camel-core - Rest DSL with api-context-path may append null in host name

[CAMEL-20481](https://issues.apache.org/jira/browse/CAMEL-20481)

camel-core - Rest DSL should resolve placeholder for context-path and others

[CAMEL-20475](https://issues.apache.org/jira/browse/CAMEL-20475)

camel-bindy - Handle values with quotes better

[CAMEL-20470](https://issues.apache.org/jira/browse/CAMEL-20470)

camel-jbang - Rest dsl with /api context path should auto detect platform-http as consumer

[CAMEL-20458](https://issues.apache.org/jira/browse/CAMEL-20458)

Writing custom dev console does not work

[CAMEL-20457](https://issues.apache.org/jira/browse/CAMEL-20457)

camel-core - NullPointerException for Split parallel and timeout without AggregationStrategy

[CAMEL-20444](https://issues.apache.org/jira/browse/CAMEL-20444)

Camel-Azure-Servicebus: Support setting of CorrelationId on producer

[CAMEL-20440](https://issues.apache.org/jira/browse/CAMEL-20440)

Camel JBang 4.4 - Windows 11 errors with every command

[CAMEL-20438](https://issues.apache.org/jira/browse/CAMEL-20438)

camel-xslt - XPath evaluation fails in Java DSL routes

[CAMEL-20437](https://issues.apache.org/jira/browse/CAMEL-20437)

camel-core - Configuring rabbitmq x-args from properties should preserve dash in key

[CAMEL-20435](https://issues.apache.org/jira/browse/CAMEL-20435)

camel-core - Resequencer EIP cannot be started again after being stopped

[CAMEL-20434](https://issues.apache.org/jira/browse/CAMEL-20434)

camel-http - Use NullEntity when request body is null

[CAMEL-20433](https://issues.apache.org/jira/browse/CAMEL-20433)

camel-jbang - Log command - java.lang.IllegalArgumentException: Comparison method violates its general contract!

[CAMEL-20431](https://issues.apache.org/jira/browse/CAMEL-20431)

camel-jbang - Run and debug route with 'org.apache.camel.debugger.suspend=true' property is not working for different jbang cli and --camel-version versions

[CAMEL-20420](https://issues.apache.org/jira/browse/CAMEL-20420)

CSimple: use of builder throws UnsupportedOperationException

### Dependency upgrade (3)

[CAMEL-20592](https://issues.apache.org/jira/browse/CAMEL-20592)

camel-kafka - Upgrade to 3.7

[CAMEL-20491](https://issues.apache.org/jira/browse/CAMEL-20491)

camel-shiro - Upgrade to 2.0 that is jakarta ee compatible

[CAMEL-20448](https://issues.apache.org/jira/browse/CAMEL-20448)

camel-spring-boot - Upgrade to 3.2.3

### Improvement (61)

[CAMEL-20604](https://issues.apache.org/jira/browse/CAMEL-20604)

camel-jbang - Remove -p for run command

[CAMEL-20602](https://issues.apache.org/jira/browse/CAMEL-20602)

Support user properties in Camel JBang bind command

[CAMEL-20601](https://issues.apache.org/jira/browse/CAMEL-20601)

Support error handler in Camel JBang bind command

[CAMEL-20596](https://issues.apache.org/jira/browse/CAMEL-20596)

Propagate Azure Service Bus message headers (properties) to Camel Message

[CAMEL-20590](https://issues.apache.org/jira/browse/CAMEL-20590)

Delay to execute timeout to Camel RabbitMQ (InOut)

[CAMEL-20589](https://issues.apache.org/jira/browse/CAMEL-20589)

camel-jbang - Make it easy to run activemq with vm transport

[CAMEL-20583](https://issues.apache.org/jira/browse/CAMEL-20583)

Java 21 - Reduce the noise from the ThreadType logger

[CAMEL-20568](https://issues.apache.org/jira/browse/CAMEL-20568)

Set errorHandler on route level in YAML DSL

[CAMEL-20567](https://issues.apache.org/jira/browse/CAMEL-20567)

Add support for restConfiguration in XML DSL IO

[CAMEL-20564](https://issues.apache.org/jira/browse/CAMEL-20564)

camel-xslt: Make variables available as xsl:param

[CAMEL-20561](https://issues.apache.org/jira/browse/CAMEL-20561)

camel-core - Properties component - Load properties in the same order as given when having multiple locations

[CAMEL-20555](https://issues.apache.org/jira/browse/CAMEL-20555)

camel-lra html response when creating a saga with invalid lra-url

[CAMEL-20554](https://issues.apache.org/jira/browse/CAMEL-20554)

camel-micrometer-prometheus - Should be GET verb

[CAMEL-20548](https://issues.apache.org/jira/browse/CAMEL-20548)

catalog: include a capability section to advertise which artifact provides a specific feature

[CAMEL-20541](https://issues.apache.org/jira/browse/CAMEL-20541)

Include arbitrary metadata to the camel-catalog

[CAMEL-20539](https://issues.apache.org/jira/browse/CAMEL-20539)

camel-tooling-maven - Make it possible to turn off completely maven central and apache snapshots

[CAMEL-20538](https://issues.apache.org/jira/browse/CAMEL-20538)

camel-jbang - The jbang DEPS with ${ } should be supported

[CAMEL-20535](https://issues.apache.org/jira/browse/CAMEL-20535)

Camel-AWS-Bedrock: Add the component for the bedrock runtime agent for knowledge base support

[CAMEL-20534](https://issues.apache.org/jira/browse/CAMEL-20534)

camel-grpc: Port validation should check if a port was specified

[CAMEL-20533](https://issues.apache.org/jira/browse/CAMEL-20533)

camel-rest - Binding mode json or xml should defer produces HTTP header

[CAMEL-20531](https://issues.apache.org/jira/browse/CAMEL-20531)

camel-console - Add metadata for camel-catalog about dev consoles

[CAMEL-20529](https://issues.apache.org/jira/browse/CAMEL-20529)

Misleading summary on components page

[CAMEL-20528](https://issues.apache.org/jira/browse/CAMEL-20528)

camel-console - Make it possible to easily start and stop routes via dev console

[CAMEL-20525](https://issues.apache.org/jira/browse/CAMEL-20525)

camel-micrometer - Remove serviceName from tags

[CAMEL-20520](https://issues.apache.org/jira/browse/CAMEL-20520)

camel-rest-openapi - Generate OpenApi scheme once on startup

[CAMEL-20510](https://issues.apache.org/jira/browse/CAMEL-20510)

camel-micrometer - Add metrics for context level

[CAMEL-20508](https://issues.apache.org/jira/browse/CAMEL-20508)

camel-jsonpath - Align how it converts to resultType like camel-jq

[CAMEL-20507](https://issues.apache.org/jira/browse/CAMEL-20507)

camel-core - Java fluent builder for expression can allow to use enum class directly

[CAMEL-20502](https://issues.apache.org/jira/browse/CAMEL-20502)

Avro data format should default use jacksonAvro

[CAMEL-20501](https://issues.apache.org/jira/browse/CAMEL-20501)

camel-core - JsonDataformat schemaResolver should include class type for tooling

[CAMEL-20495](https://issues.apache.org/jira/browse/CAMEL-20495)

camel-jsonpath - ResultType List should store single element into a List so it can be used afterwards with Split EIP

[CAMEL-20490](https://issues.apache.org/jira/browse/CAMEL-20490)

camel-openapi-java - Empty server url due to X-Forward-Headers

[CAMEL-20488](https://issues.apache.org/jira/browse/CAMEL-20488)

camel-openapi-java - Drop support for openapi v2

[CAMEL-20484](https://issues.apache.org/jira/browse/CAMEL-20484)

camel-jbang - Using rest with /api context should have content-type in http summary

[CAMEL-20482](https://issues.apache.org/jira/browse/CAMEL-20482)

camel-file - Can ant filter be optimized when using min/max depth with orphan marker file check

[CAMEL-20479](https://issues.apache.org/jira/browse/CAMEL-20479)

camel-test-infra-artemis: delay broker configuration

[CAMEL-20474](https://issues.apache.org/jira/browse/CAMEL-20474)

camel-platform-http-main - Add /q/info to show some basic details

[CAMEL-20472](https://issues.apache.org/jira/browse/CAMEL-20472)

camel-main - Add group for configuring tracing

[CAMEL-20471](https://issues.apache.org/jira/browse/CAMEL-20471)

camel-jbang - trace command should have show-exchange-variables option

[CAMEL-20466](https://issues.apache.org/jira/browse/CAMEL-20466)

camel-core - Rest DSL to be inlined by default to avoid clutter up list of routes

[CAMEL-20461](https://issues.apache.org/jira/browse/CAMEL-20461)

camel-micrometer - Add statistics for context level

[CAMEL-20460](https://issues.apache.org/jira/browse/CAMEL-20460)

camel-platform-http - Rest DSL consume/produces should be in summary

[CAMEL-20459](https://issues.apache.org/jira/browse/CAMEL-20459)

EIP Documentation: grammar, typos and other fixes

[CAMEL-20447](https://issues.apache.org/jira/browse/CAMEL-20447)

camel-platform-http - Move jolokia JARs to the new jolokia-platform-http

[CAMEL-20446](https://issues.apache.org/jira/browse/CAMEL-20446)

camel-jbang - Add support for reloading open-api file in dev mode

[CAMEL-20445](https://issues.apache.org/jira/browse/CAMEL-20445)

JMX - Support update of variables through MBean for JMX debugger

[CAMEL-20442](https://issues.apache.org/jira/browse/CAMEL-20442)

Camel JBang with --open-api flag, stop watching the route

[CAMEL-20425](https://issues.apache.org/jira/browse/CAMEL-20425)

camel-yaml-dsl - Add support for multi extension

[CAMEL-20422](https://issues.apache.org/jira/browse/CAMEL-20422)

Move component json into META-INF

[CAMEL-20421](https://issues.apache.org/jira/browse/CAMEL-20421)

KnativeProducer creates Platform Http Service in JBang

[CAMEL-20419](https://issues.apache.org/jira/browse/CAMEL-20419)

components with cloud events should generate metadata for camel-catalog

[CAMEL-20418](https://issues.apache.org/jira/browse/CAMEL-20418)

camel-core - Log EIP should only use source line:name if enabled

[CAMEL-20413](https://issues.apache.org/jira/browse/CAMEL-20413)

camel-spring-boot - Use hardcoded version in released BOM

[CAMEL-20411](https://issues.apache.org/jira/browse/CAMEL-20411)

camel-mongodb: Add findAndModify Operation

[CAMEL-20410](https://issues.apache.org/jira/browse/CAMEL-20410)

Documentation: grammar, typos and other fixes

[CAMEL-20381](https://issues.apache.org/jira/browse/CAMEL-20381)

camel-core - EIPs that enrich exchange with exchange properties should be annotated and exposed in catalog

[CAMEL-20361](https://issues.apache.org/jira/browse/CAMEL-20361)

camel-jbang - Make jolokia pluggable for camel-platform-http-main

[CAMEL-20300](https://issues.apache.org/jira/browse/CAMEL-20300)

camel-jms - Consider adding option to override/enhance creation of temporary destinations simmilar to DestinationResolver

[CAMEL-20299](https://issues.apache.org/jira/browse/CAMEL-20299)

camel-spring-rabbitmq - Cannot Create or Bind Producers

[CAMEL-20091](https://issues.apache.org/jira/browse/CAMEL-20091)

autoDeclare for Producers in Spring Rabbit MQ

[CAMEL-13909](https://issues.apache.org/jira/browse/CAMEL-13909)

Camel Rest-DSL doesn't generate type & outType from openapi 2.0 file

### New Feature (20)

[CAMEL-20594](https://issues.apache.org/jira/browse/CAMEL-20594)

Camel-Milvus: Add a datatype for transforming langchain embeddings in Milvus objects

[CAMEL-20587](https://issues.apache.org/jira/browse/CAMEL-20587)

Camel-Qdrant: Add a datatype for transforming langchain embeddings in qdrant objects

[CAMEL-20572](https://issues.apache.org/jira/browse/CAMEL-20572)

Camel-Milvus: Create Spring Boot Starter

[CAMEL-20570](https://issues.apache.org/jira/browse/CAMEL-20570)

Camel-Langchain-\*: Create starters for Spring Boot

[CAMEL-20565](https://issues.apache.org/jira/browse/CAMEL-20565)

Azure Service Bus Component: Support dead-lettering at application level

[CAMEL-20544](https://issues.apache.org/jira/browse/CAMEL-20544)

Camel-AWS-Bedrock-Agent: Add a consumer for polling the status of ingestion or more ingestions

[CAMEL-20543](https://issues.apache.org/jira/browse/CAMEL-20543)

Camel-AWS-Bedrock-Agent: Support more operations on the producer side

[CAMEL-20537](https://issues.apache.org/jira/browse/CAMEL-20537)

Camel-AWS-Bedrock: Add more headers to retrieve and generate operation for Bedrock Agent Runtime

[CAMEL-20536](https://issues.apache.org/jira/browse/CAMEL-20536)

Camel-AWS-Bedrock: Add the component for Bedrock Agent

[CAMEL-20485](https://issues.apache.org/jira/browse/CAMEL-20485)

Create a Camel-Milvus component

[CAMEL-20467](https://issues.apache.org/jira/browse/CAMEL-20467)

Camel AWS Bedrock: Create Spring Boot starter

[CAMEL-20463](https://issues.apache.org/jira/browse/CAMEL-20463)

Create an AWS Bedrock Runtime component

[CAMEL-20423](https://issues.apache.org/jira/browse/CAMEL-20423)

AWS STS Component: Provide a way of setting the duration of AssumeRoleRequest through header

[CAMEL-20404](https://issues.apache.org/jira/browse/CAMEL-20404)

Create a component for Qdrant Vector Database

[CAMEL-20019](https://issues.apache.org/jira/browse/CAMEL-20019)

camel-platform-http-vertx - Add support for cookie handler

[CAMEL-19284](https://issues.apache.org/jira/browse/CAMEL-19284)

camel-restdsl-openapi-plugin - Add type and outType to Rest DSL

[CAMEL-18858](https://issues.apache.org/jira/browse/CAMEL-18858)

camel-core - Filter out kamelet routes so they do not clutter the list of routes

[CAMEL-18090](https://issues.apache.org/jira/browse/CAMEL-18090)

camel-main - Loading properties with profiles for prod/dev/qa

[CAMEL-17641](https://issues.apache.org/jira/browse/CAMEL-17641)

camel-catalog - Generate metadata for all known implementations of camel SPI interfaces

[CAMEL-17386](https://issues.apache.org/jira/browse/CAMEL-17386)

camel-main - Developer Mode

### Sub-task (16)

[CAMEL-20560](https://issues.apache.org/jira/browse/CAMEL-20560)

Camel-AWS-Bedrock: Support Anthropic models

[CAMEL-20516](https://issues.apache.org/jira/browse/CAMEL-20516)

Camel-AWS-Bedrock: Support AI21 Jurassic2 Mid model

[CAMEL-20515](https://issues.apache.org/jira/browse/CAMEL-20515)

Camel-AWS-Bedrock: Support AI21 Jurassic2 Ultra model

[CAMEL-20511](https://issues.apache.org/jira/browse/CAMEL-20511)

Camel-AWS-Bedrock: Support Amazon Titan Embeddings G1 Model

[CAMEL-20504](https://issues.apache.org/jira/browse/CAMEL-20504)

Google Pubsub CloudEvent Transformer

[CAMEL-20476](https://issues.apache.org/jira/browse/CAMEL-20476)

Camel-AWS-Bedrock: Support Amazon Titan Image Generator G1 model

[CAMEL-20469](https://issues.apache.org/jira/browse/CAMEL-20469)

Camel-AWS-Bedrock: Support Amazon Titan Text G1 Lite Model

[CAMEL-20464](https://issues.apache.org/jira/browse/CAMEL-20464)

Slack CloudEvent transformer

[CAMEL-20453](https://issues.apache.org/jira/browse/CAMEL-20453)

Azure CosmosDB CloudEvent transformer

[CAMEL-20452](https://issues.apache.org/jira/browse/CAMEL-20452)

Azure Storage Datalake CloudEvent transformer

[CAMEL-20451](https://issues.apache.org/jira/browse/CAMEL-20451)

Azure Eventhubs CloudEvent transformer

[CAMEL-20450](https://issues.apache.org/jira/browse/CAMEL-20450)

Azure Servicebus CloudEvent transformer

[CAMEL-20449](https://issues.apache.org/jira/browse/CAMEL-20449)

Azure Storage Files CloudEvent transformer

[CAMEL-20417](https://issues.apache.org/jira/browse/CAMEL-20417)

AWS DDBStreams CloudEvent Transformer

[CAMEL-20416](https://issues.apache.org/jira/browse/CAMEL-20416)

AWS Kinesis CloudEvent Transformer

[CAMEL-20415](https://issues.apache.org/jira/browse/CAMEL-20415)

AWS Cloudtrail CloudEvent transformer

### Task (11)

[CAMEL-20599](https://issues.apache.org/jira/browse/CAMEL-20599)

camel-ai - pom.xml should be clean

[CAMEL-20598](https://issues.apache.org/jira/browse/CAMEL-20598)

camel-jbang - Cannot use hawtio v4

[CAMEL-20595](https://issues.apache.org/jira/browse/CAMEL-20595)

camel-dlj - Move into camel-ai

[CAMEL-20578](https://issues.apache.org/jira/browse/CAMEL-20578)

generated configurer should use lower case first-char name

[CAMEL-20566](https://issues.apache.org/jira/browse/CAMEL-20566)

Jaxb version should be present in parent/pom.xml not pom/xml

[CAMEL-20519](https://issues.apache.org/jira/browse/CAMEL-20519)

camel-servlet: Tidy and improve documentation

[CAMEL-20518](https://issues.apache.org/jira/browse/CAMEL-20518)

Camel project - doesn't build on Windows anymore

[CAMEL-20462](https://issues.apache.org/jira/browse/CAMEL-20462)

Beans component typo

[CAMEL-20456](https://issues.apache.org/jira/browse/CAMEL-20456)

camel-http: charset being used to set Content-Encoding field since camel

[CAMEL-20255](https://issues.apache.org/jira/browse/CAMEL-20255)

camel-core: remove deprecated timestamp-based methods

[CAMEL-20014](https://issues.apache.org/jira/browse/CAMEL-20014)

camel-core: remove deprecated methods

### Test (7)

[CAMEL-20581](https://issues.apache.org/jira/browse/CAMEL-20581)

camel-test-infra-artemis: ensure components use the correct lifecycle for service

[CAMEL-20478](https://issues.apache.org/jira/browse/CAMEL-20478)

camel-jms: review and split Integration tests from Unit tests

[CAMEL-20477](https://issues.apache.org/jira/browse/CAMEL-20477)

camel-jms: test flakiness

[CAMEL-20405](https://issues.apache.org/jira/browse/CAMEL-20405)

Rename classes from \*IntegrationTest.java to \*IT.java

[CAMEL-20377](https://issues.apache.org/jira/browse/CAMEL-20377)

\*IT tests should be run with failsafe instead of surefire

[CAMEL-20324](https://issues.apache.org/jira/browse/CAMEL-20324)

Tests failing in camel-openapi-java

[CAMEL-16660](https://issues.apache.org/jira/browse/CAMEL-16660)

Hazelcast : tests : create camel-test-infra-Hazelcast

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).