# Apache camel 4.1.0 Release

## New and Noteworthy

This release is the new Camel 4.1.0 release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.1.0</version>
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
      <version>4.1.0</version>
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
| [apache-camel-4.1.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.1.0/apache-camel-4.1.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.1.0/apache-camel-4.1.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.1.0/apache-camel-4.1.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.1.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.1.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (45)

[CAMEL-19957](https://issues.apache.org/jira/browse/CAMEL-19957)

camel-jbang - On demand reload is not updating kamelets/routes

[CAMEL-19938](https://issues.apache.org/jira/browse/CAMEL-19938)

JBang camel CLI not working when using "run" option on Windows environments

[CAMEL-19931](https://issues.apache.org/jira/browse/CAMEL-19931)

camel-jbang - Reload with custom kamelet cannot find on update

[CAMEL-19923](https://issues.apache.org/jira/browse/CAMEL-19923)

Camel JBang dependency is not working on Windows not finding mvn in .camel-jbang\\export

[CAMEL-19922](https://issues.apache.org/jira/browse/CAMEL-19922)

Camel JBang dependency is not supporting absolute path on Windows

[CAMEL-19918](https://issues.apache.org/jira/browse/CAMEL-19918)

camel-spring-boot - XPath language configuring saxon=true seems to not work

[CAMEL-19910](https://issues.apache.org/jira/browse/CAMEL-19910)

camel-jbang - Export may include hidden files

[CAMEL-19899](https://issues.apache.org/jira/browse/CAMEL-19899)

camel-servlet: Multipart attachment processing does not work on Undertow

[CAMEL-19895](https://issues.apache.org/jira/browse/CAMEL-19895)

Camel JBang dependency copy --output-directory doesn't respect absolute path

[CAMEL-19892](https://issues.apache.org/jira/browse/CAMEL-19892)

openapi-rest-dsl-generator - Use jakarta instead of javax annotation

[CAMEL-19885](https://issues.apache.org/jira/browse/CAMEL-19885)

Default auth scope on google-sheets-streams not working

[CAMEL-19878](https://issues.apache.org/jira/browse/CAMEL-19878)

camel-main - Using Camel- as context name causes ENV name clash running on Kubernetes

[CAMEL-19875](https://issues.apache.org/jira/browse/CAMEL-19875)

HealthCheck is broken for KafkaConsumer

[CAMEL-19870](https://issues.apache.org/jira/browse/CAMEL-19870)

Camel AS2: Should accept MDN field name Disposition as case insensitive

[CAMEL-19860](https://issues.apache.org/jira/browse/CAMEL-19860)

camel-zipfile: Splitter may create unnecessary input streams

[CAMEL-19859](https://issues.apache.org/jira/browse/CAMEL-19859)

camel-spring-rabbitmq set headerfilter not effective

[CAMEL-19857](https://issues.apache.org/jira/browse/CAMEL-19857)

Cannot run Kotlin DSL 1.8 in a fatjar

[CAMEL-19843](https://issues.apache.org/jira/browse/CAMEL-19843)

HTTP/2 pseudo-headers such as :status should not be propagated from CXF message to Camel message

[CAMEL-19842](https://issues.apache.org/jira/browse/CAMEL-19842)

camel-zookeeper-master: fix MasterEndpointFailoverIT

[CAMEL-19837](https://issues.apache.org/jira/browse/CAMEL-19837)

Converters - unpredictable behavior linked to type hierarchy (flatpack)

[CAMEL-19825](https://issues.apache.org/jira/browse/CAMEL-19825)

Kubernetes cluster service is produced but absent in camel services

[CAMEL-19822](https://issues.apache.org/jira/browse/CAMEL-19822)

camel-azure-files - assert failure in the implementation of move=

[CAMEL-19818](https://issues.apache.org/jira/browse/CAMEL-19818)

camel-openapi-java - A response type containing an array generates incorrect schema reference

[CAMEL-19815](https://issues.apache.org/jira/browse/CAMEL-19815)

camel-seda: cached queue reference can become invalid

[CAMEL-19814](https://issues.apache.org/jira/browse/CAMEL-19814)

camel-rest - Should filter out query parameters that are for the producer endpoint

[CAMEL-19811](https://issues.apache.org/jira/browse/CAMEL-19811)

camel-aws - Restore multi-shard handling in Kinesis

[CAMEL-19798](https://issues.apache.org/jira/browse/CAMEL-19798)

Inconsistent camel-kamelets version in Camel JBang

[CAMEL-19793](https://issues.apache.org/jira/browse/CAMEL-19793)

camel-springdoc-starter contains old (javax) dependencies

[CAMEL-19789](https://issues.apache.org/jira/browse/CAMEL-19789)

Kinesis2Consumer repeatedly reads first record in stream

[CAMEL-19785](https://issues.apache.org/jira/browse/CAMEL-19785)

camel-yaml-dsl - Order of beans should not matter

[CAMEL-19784](https://issues.apache.org/jira/browse/CAMEL-19784)

camel-core - PropertyBindingSupport - mandatory reference should fail if cannot resolve bean

[CAMEL-19783](https://issues.apache.org/jira/browse/CAMEL-19783)

camel-salesforce - grpc will not resubscribe on connection failure if no messages have been received

[CAMEL-19780](https://issues.apache.org/jira/browse/CAMEL-19780)

Camel JBang does not support relative paths

[CAMEL-19777](https://issues.apache.org/jira/browse/CAMEL-19777)

camel-jms: toD endpoint with FQQN

[CAMEL-19775](https://issues.apache.org/jira/browse/CAMEL-19775)

camel-main: main duration event is not enabled for exchange completed

[CAMEL-19768](https://issues.apache.org/jira/browse/CAMEL-19768)

camel-http - HTTP message body encoded with wrong charset

[CAMEL-19766](https://issues.apache.org/jira/browse/CAMEL-19766)

Routes loaded with xml-io-dsl don't find associated routeConfiguration

[CAMEL-19764](https://issues.apache.org/jira/browse/CAMEL-19764)

camel-openapi - basic and bearer token

[CAMEL-19758](https://issues.apache.org/jira/browse/CAMEL-19758)

netty-http in proxy mode generates IllegalReferenceCountException for every success request.

[CAMEL-19756](https://issues.apache.org/jira/browse/CAMEL-19756)

camel-zeebe - ThrowError operation does not set Processor

[CAMEL-19738](https://issues.apache.org/jira/browse/CAMEL-19738)

camel-core - Loop EIP can have wrong pending inflight in case of early loop exit due to exception

[CAMEL-19737](https://issues.apache.org/jira/browse/CAMEL-19737)

camel-aws - SNS component subscription to SQS error

[CAMEL-19731](https://issues.apache.org/jira/browse/CAMEL-19731)

Camel-AS2: exception on empty response

[CAMEL-19729](https://issues.apache.org/jira/browse/CAMEL-19729)

camel-jbang - camel get route-dump should handle 2+ routes in the source files

[CAMEL-18759](https://issues.apache.org/jira/browse/CAMEL-18759)

camel-kafka - When Kafka pausable consumer is resumed, it reads all the messages from the earliest offset

### Dependency upgrade (13)

[CAMEL-19954](https://issues.apache.org/jira/browse/CAMEL-19954)

Bump Debezium to version 2.4.0.Final

[CAMEL-19944](https://issues.apache.org/jira/browse/CAMEL-19944)

Upgrade Azure SDK BOM to version 1.2.17

[CAMEL-19930](https://issues.apache.org/jira/browse/CAMEL-19930)

Camel-Jbang: Upgrade to Camel-Kamelets 4.0.1

[CAMEL-19920](https://issues.apache.org/jira/browse/CAMEL-19920)

camel-mina - Upgrade to newer versions

[CAMEL-19903](https://issues.apache.org/jira/browse/CAMEL-19903)

Upgrade Debezium to 2.3.4.Final

[CAMEL-19884](https://issues.apache.org/jira/browse/CAMEL-19884)

pooled-jms - Upgrade to 3.1.3

[CAMEL-19881](https://issues.apache.org/jira/browse/CAMEL-19881)

camel-spring-boot - Upgrade to 3.1.4

[CAMEL-19850](https://issues.apache.org/jira/browse/CAMEL-19850)

Bump Camel-Kamelets to version 4.0.0

[CAMEL-19841](https://issues.apache.org/jira/browse/CAMEL-19841)

Camel-test-infra: Bump Testcontainers to 1.19.0

[CAMEL-19838](https://issues.apache.org/jira/browse/CAMEL-19838)

Camel-Debezium: Upgrade to Debezium 2.3.3.Final

[CAMEL-19831](https://issues.apache.org/jira/browse/CAMEL-19831)

Camel-Azure: Upgrade Azure SDK BOM to version 1.2.16

[CAMEL-19796](https://issues.apache.org/jira/browse/CAMEL-19796)

camel-pdf - Upgrade to pdfbox 3.x

[CAMEL-19791](https://issues.apache.org/jira/browse/CAMEL-19791)

camel-spring-boot - Upgrade to 3.1.3

### Improvement (60)

[CAMEL-19953](https://issues.apache.org/jira/browse/CAMEL-19953)

camel-kamelet - Add scriptLanguage to local beans

[CAMEL-19952](https://issues.apache.org/jira/browse/CAMEL-19952)

camel-core-model - Add script to bean model

[CAMEL-19950](https://issues.apache.org/jira/browse/CAMEL-19950)

camel-report-maven-plugin - Use camel-tooling-maven instead of grape

[CAMEL-19949](https://issues.apache.org/jira/browse/CAMEL-19949)

camel-jbang - Allow to set a custom remote debugging port

[CAMEL-19948](https://issues.apache.org/jira/browse/CAMEL-19948)

camel jbang - Transform with no files should not show null.properties

[CAMEL-19942](https://issues.apache.org/jira/browse/CAMEL-19942)

Camel-Jbang: Improve SBOM generator by supporting also SPDX format

[CAMEL-19940](https://issues.apache.org/jira/browse/CAMEL-19940)

camel-jbang - init should create .camel-jbang folder

[CAMEL-19939](https://issues.apache.org/jira/browse/CAMEL-19939)

camel-jbang - dependency copy - Use camel-tooling-maven

[CAMEL-19937](https://issues.apache.org/jira/browse/CAMEL-19937)

camel-core - Properties component - Add option to ignore unresolved property

[CAMEL-19936](https://issues.apache.org/jira/browse/CAMEL-19936)

camel-xml-io - Parsing error with line precise error

[CAMEL-19934](https://issues.apache.org/jira/browse/CAMEL-19934)

camel-bean - Add option to turn of method validation

[CAMEL-19933](https://issues.apache.org/jira/browse/CAMEL-19933)

camel-jbang - Stub bean and processor for transform/migration

[CAMEL-19929](https://issues.apache.org/jira/browse/CAMEL-19929)

camel-main - Dev console for upload should support sub folders

[CAMEL-19926](https://issues.apache.org/jira/browse/CAMEL-19926)

camel-xml-io - Make parsing lenient for parsing legacy OSGi blueprint files

[CAMEL-19924](https://issues.apache.org/jira/browse/CAMEL-19924)

camel-jbang - Java compiled classes should be available for classloading by components

[CAMEL-19919](https://issues.apache.org/jira/browse/CAMEL-19919)

camel-kafka: provided an out of the box byte\[\] to String header deserializer

[CAMEL-19917](https://issues.apache.org/jira/browse/CAMEL-19917)

Camel JBang dependency copy is not working on not yet compiling files

[CAMEL-19913](https://issues.apache.org/jira/browse/CAMEL-19913)

camel-jbang - Transform to output to console

[CAMEL-19912](https://issues.apache.org/jira/browse/CAMEL-19912)

camel-core-model - Add factory-method parameter

[CAMEL-19911](https://issues.apache.org/jira/browse/CAMEL-19911)

Camel-Azure-CosmosDB: IndexingPolicy should be directly a POJO in configuration

[CAMEL-19906](https://issues.apache.org/jira/browse/CAMEL-19906)

Camel-Jbang: No need to have specific application properties exports for Secret Refresh features

[CAMEL-19902](https://issues.apache.org/jira/browse/CAMEL-19902)

Azure CosmosDB: Expose an IndexingPolicy parameter for createContainer operation

[CAMEL-19890](https://issues.apache.org/jira/browse/CAMEL-19890)

camel-jbang - Downloading dependencies from a list with white spaces

[CAMEL-19888](https://issues.apache.org/jira/browse/CAMEL-19888)

Preserve openapi tags order while generating api-doc

[CAMEL-19880](https://issues.apache.org/jira/browse/CAMEL-19880)

camel-salesforce: component still depends on javax.annotation-api

[CAMEL-19874](https://issues.apache.org/jira/browse/CAMEL-19874)

Documentation of Spring Webservice component

[CAMEL-19868](https://issues.apache.org/jira/browse/CAMEL-19868)

camel-core-catalog: duplicated code

[CAMEL-19866](https://issues.apache.org/jira/browse/CAMEL-19866)

Camel-Pulsar: Support HashingScheme as uri parameter for producers

[CAMEL-19852](https://issues.apache.org/jira/browse/CAMEL-19852)

Camel-platform-http-vertx: Always use normalized path from context

[CAMEL-19851](https://issues.apache.org/jira/browse/CAMEL-19851)

spring-boot Allow to configure timeouts natively

[CAMEL-19846](https://issues.apache.org/jira/browse/CAMEL-19846)

camel-yaml-dsl: Support setting MessageHistoryFactory.setCopyMessage(true) from YAML DSL

[CAMEL-19833](https://issues.apache.org/jira/browse/CAMEL-19833)

camel-bindy: race condition in BindyAbstractFactory.link()

[CAMEL-19823](https://issues.apache.org/jira/browse/CAMEL-19823)

camel-spring-rabbitmq - Add allowNullBody as endpoint option

[CAMEL-19820](https://issues.apache.org/jira/browse/CAMEL-19820)

camel-core-model - Add constructor parameters

[CAMEL-19817](https://issues.apache.org/jira/browse/CAMEL-19817)

camel-timer - Remove the old firedTime header

[CAMEL-19816](https://issues.apache.org/jira/browse/CAMEL-19816)

camel-platform-http-vertx: Add headers for local address & remote address

[CAMEL-19813](https://issues.apache.org/jira/browse/CAMEL-19813)

camel-yaml-dsl - Error handler should be oneOf

[CAMEL-19812](https://issues.apache.org/jira/browse/CAMEL-19812)

camel-tracing - Decorators should use otel naming convention for metadata

[CAMEL-19810](https://issues.apache.org/jira/browse/CAMEL-19810)

\[test-infra\] Inifinispan test container using podman

[CAMEL-19808](https://issues.apache.org/jira/browse/CAMEL-19808)

camel-core-model - Add start and stop method to <bean>

[CAMEL-19805](https://issues.apache.org/jira/browse/CAMEL-19805)

Support IntegrationSpec as part of Pipe/KameletBinding

[CAMEL-19803](https://issues.apache.org/jira/browse/CAMEL-19803)

camel-core-model - Error handlers should have redelivery policy come sooner in the model json

[CAMEL-19802](https://issues.apache.org/jira/browse/CAMEL-19802)

camel-jbang - Add option to exclude files by pattern

[CAMEL-19795](https://issues.apache.org/jira/browse/CAMEL-19795)

camel-java-joor-dsl - Eager load classes to make them available for classloading by other DSL

[CAMEL-19792](https://issues.apache.org/jira/browse/CAMEL-19792)

camel-core - PropertyBinding - Constructor args for beans should be mandatory lookup

[CAMEL-19786](https://issues.apache.org/jira/browse/CAMEL-19786)

camel-jbang - Allow to load spring <beans> with embedded <camelContext>

[CAMEL-19776](https://issues.apache.org/jira/browse/CAMEL-19776)

Provide tracing strategy to trace each processor for OpenTelemetry

[CAMEL-19774](https://issues.apache.org/jira/browse/CAMEL-19774)

camel-jbang - Rename bind goal to pipe

[CAMEL-19773](https://issues.apache.org/jira/browse/CAMEL-19773)

camel-jbang - camel init xml - Use <camel> instead of <routes>

[CAMEL-19771](https://issues.apache.org/jira/browse/CAMEL-19771)

camel-core-model - RouteConfigurationsDefinition should be id and resource

[CAMEL-19765](https://issues.apache.org/jira/browse/CAMEL-19765)

camel-core - SPI for DumpRouteStrategy

[CAMEL-19760](https://issues.apache.org/jira/browse/CAMEL-19760)

netty-http:prevent the usage of proxy protocol in producer endpoint

[CAMEL-19752](https://issues.apache.org/jira/browse/CAMEL-19752)

Usage of "doc" prefix in some elasticsearch operations are regression to camel-elasticsearch-rest

[CAMEL-19736](https://issues.apache.org/jira/browse/CAMEL-19736)

Environment variables with the name 'secret' aren't masked in logs

[CAMEL-19718](https://issues.apache.org/jira/browse/CAMEL-19718)

camel-util-json should allow to configure escape forward slashes or not

[CAMEL-19717](https://issues.apache.org/jira/browse/CAMEL-19717)

\[yaml dsl\] replace jackson with camel-util-json for json schema generation

[CAMEL-19656](https://issues.apache.org/jira/browse/CAMEL-19656)

camel-aws - SQS consumer should batch visibility extender task

[CAMEL-17173](https://issues.apache.org/jira/browse/CAMEL-17173)

camel-jetty and http server components - Mute exception should default be enabled

[CAMEL-17027](https://issues.apache.org/jira/browse/CAMEL-17027)

camel-aws-a3 - Streaming mode upload avoid stream into memory

[CAMEL-16651](https://issues.apache.org/jira/browse/CAMEL-16651)

yaml dsl: Include description for elements in Yaml schema

### New Feature (20)

[CAMEL-19960](https://issues.apache.org/jira/browse/CAMEL-19960)

camel-jbang - Add camel get startup

[CAMEL-19932](https://issues.apache.org/jira/browse/CAMEL-19932)

camel-jbang - Run/Transform from existing maven based structure

[CAMEL-19889](https://issues.apache.org/jira/browse/CAMEL-19889)

camel-xslt - Add allowTemplateFromHeader option

[CAMEL-19879](https://issues.apache.org/jira/browse/CAMEL-19879)

camel-rest- Add option to set headerfilterStrategy

[CAMEL-19877](https://issues.apache.org/jira/browse/CAMEL-19877)

camel-file - Add option to accept hidden folders

[CAMEL-19876](https://issues.apache.org/jira/browse/CAMEL-19876)

Add maven-settings to camel-jbang export command

[CAMEL-19806](https://issues.apache.org/jira/browse/CAMEL-19806)

camel-jbang - Allow to load OSGi <blueprint> with embedded <camelContext>

[CAMEL-19778](https://issues.apache.org/jira/browse/CAMEL-19778)

camel-jbang - Add DSL transform command

[CAMEL-19772](https://issues.apache.org/jira/browse/CAMEL-19772)

camel-core - Dump routes to include custom beans

[CAMEL-19755](https://issues.apache.org/jira/browse/CAMEL-19755)

Create a camel-thymeleaf component, similar to camel-freemarker and camel-velocity

[CAMEL-19747](https://issues.apache.org/jira/browse/CAMEL-19747)

camel-jbang - Add command to browse stub queues

[CAMEL-19740](https://issues.apache.org/jira/browse/CAMEL-19740)

camel-stub - Add dev console

[CAMEL-19739](https://issues.apache.org/jira/browse/CAMEL-19739)

camel run - Add stub option to run in stub mode

[CAMEL-19644](https://issues.apache.org/jira/browse/CAMEL-19644)

camel-jbang - Add command to generate SBOM report

[CAMEL-19218](https://issues.apache.org/jira/browse/CAMEL-19218)

Add request validation feature for REST OPENAPI

[CAMEL-18948](https://issues.apache.org/jira/browse/CAMEL-18948)

camel-jbang - Route loader to load classic spring xml files

[CAMEL-18635](https://issues.apache.org/jira/browse/CAMEL-18635)

Add Maven plugin to generate HTML and XLSX route coverage reports

[CAMEL-17318](https://issues.apache.org/jira/browse/CAMEL-17318)

Add an AWS Timestream component

[CAMEL-17315](https://issues.apache.org/jira/browse/CAMEL-17315)

Create an AWS Redshift Data Component

[CAMEL-15625](https://issues.apache.org/jira/browse/CAMEL-15625)

camel-main - Capture startup events and report time in a report for humans

### Task (35)

[CAMEL-19927](https://issues.apache.org/jira/browse/CAMEL-19927)

Camel-Jbang: Remove secrets-refresh flags from export command

[CAMEL-19921](https://issues.apache.org/jira/browse/CAMEL-19921)

Update default values of kafka client configuration

[CAMEL-19909](https://issues.apache.org/jira/browse/CAMEL-19909)

camel-catalog: model catalog refers to not-existing DescriptionDefinition javaType

[CAMEL-19908](https://issues.apache.org/jira/browse/CAMEL-19908)

camel-quarkus-azure-servicebus - Fix typo in docs

[CAMEL-19904](https://issues.apache.org/jira/browse/CAMEL-19904)

camel-spring - Remove old unmaintained version mappings in spring.schemas

[CAMEL-19893](https://issues.apache.org/jira/browse/CAMEL-19893)

Migrate from jackson-module-jsonSchema to jackson-module-jsonSchema-jakarta

[CAMEL-19886](https://issues.apache.org/jira/browse/CAMEL-19886)

\[Camel Spring Boot Examples\] Add rest-cxf example

[CAMEL-19871](https://issues.apache.org/jira/browse/CAMEL-19871)

camel-jooq - Set the proper scope to all test dependencies

[CAMEL-19864](https://issues.apache.org/jira/browse/CAMEL-19864)

spring-boot - Fix integration test CamelUnivocityParsersTest

[CAMEL-19863](https://issues.apache.org/jira/browse/CAMEL-19863)

spring-boot - Fix Kamelet test

[CAMEL-19862](https://issues.apache.org/jira/browse/CAMEL-19862)

Update SyncPropertiesMojo

[CAMEL-19854](https://issues.apache.org/jira/browse/CAMEL-19854)

spring-boot - Fix the test KafkaConsumerHealthCheckIT

[CAMEL-19847](https://issues.apache.org/jira/browse/CAMEL-19847)

Camel-Thymeleaf: Create a SB starter

[CAMEL-19845](https://issues.apache.org/jira/browse/CAMEL-19845)

Camel-Spring-Boot: Add SBOM to release

[CAMEL-19844](https://issues.apache.org/jira/browse/CAMEL-19844)

Add SBOM to release

[CAMEL-19840](https://issues.apache.org/jira/browse/CAMEL-19840)

camel-core-api - Add a warning when the key store file cannot be found

[CAMEL-19836](https://issues.apache.org/jira/browse/CAMEL-19836)

camel-yaml-dsl: schema: fix routeConfiguration/onException

[CAMEL-19826](https://issues.apache.org/jira/browse/CAMEL-19826)

Update camel-examples for Camel 4.x

[CAMEL-19790](https://issues.apache.org/jira/browse/CAMEL-19790)

\[Camel Spring Boot Examples\] Add camel-spring-jdbc example

[CAMEL-19782](https://issues.apache.org/jira/browse/CAMEL-19782)

\[DOCS\] Camel JPA wrong transaction manager documentation

[CAMEL-19751](https://issues.apache.org/jira/browse/CAMEL-19751)

camel-xchange: tests keep hitting the binance API

[CAMEL-19748](https://issues.apache.org/jira/browse/CAMEL-19748)

core: cleanup remaining catches of Throwables

[CAMEL-19741](https://issues.apache.org/jira/browse/CAMEL-19741)

camel-sjms: refactor to support concurrent tests

[CAMEL-19733](https://issues.apache.org/jira/browse/CAMEL-19733)

Migrate CRDs used from camel.apache.org/v1alpha1 to camel.apache.org/v1

[CAMEL-19732](https://issues.apache.org/jira/browse/CAMEL-19732)

KameletBinding renamed to Pipe

[CAMEL-19725](https://issues.apache.org/jira/browse/CAMEL-19725)

camel-opensearch: replace Thread.sleep in tests

[CAMEL-19712](https://issues.apache.org/jira/browse/CAMEL-19712)

camel-test-junit5: adapt to support JUnit 5.10

[CAMEL-19711](https://issues.apache.org/jira/browse/CAMEL-19711)

Upgrade to Junit 5.10.x

[CAMEL-19703](https://issues.apache.org/jira/browse/CAMEL-19703)

\[yaml dsl\] remove kebab-case schema definition

[CAMEL-19700](https://issues.apache.org/jira/browse/CAMEL-19700)

camel-yaml-dsl: Add "additionalProperties: false" on every sub schema

[CAMEL-19699](https://issues.apache.org/jira/browse/CAMEL-19699)

camel-yaml-dsl: schema: Express languages/dataformats are mutually exclusive

[CAMEL-19698](https://issues.apache.org/jira/browse/CAMEL-19698)

camel-yaml-dsl: Express "simple" and "expression.simple" are mutually exclusive if possible

[CAMEL-19555](https://issues.apache.org/jira/browse/CAMEL-19555)

camel-spring: ensure tests have assertions

[CAMEL-19516](https://issues.apache.org/jira/browse/CAMEL-19516)

camel-consul: replace Thread.sleep in tests

[CAMEL-19229](https://issues.apache.org/jira/browse/CAMEL-19229)

camel-tarfile: Common compress 1.23 is causing test failures

### Test (3)

[CAMEL-19935](https://issues.apache.org/jira/browse/CAMEL-19935)

camel-cxf - Upgrade to 4.0.3 is causing some CI test errors

[CAMEL-19928](https://issues.apache.org/jira/browse/CAMEL-19928)

FileSedaShutdownCompleteAllTasksTest is failing on Windows

[CAMEL-19853](https://issues.apache.org/jira/browse/CAMEL-19853)

Camel-Thymeleaf: Fix Camel Catalog test and review the syntax

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).