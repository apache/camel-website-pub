# Apache camel 3.21.0 Release

## New and Noteworthy

This release is the new Camel 3.21.0 LTS release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.21.0</version>
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
      <version>3.21.0</version>
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
| [apache-camel-3.21.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.21.0/apache-camel-3.21.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.21.0/apache-camel-3.21.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.21.0/apache-camel-3.21.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.21.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.21.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (93)

[CAMEL-19486](https://issues.apache.org/jira/browse/CAMEL-19486)

The $repos placeholder used by Camel JBang is not resolved

[CAMEL-19476](https://issues.apache.org/jira/browse/CAMEL-19476)

rest-dsl - ClientRequestValidation accepted content-type may not validate correctly

[CAMEL-19470](https://issues.apache.org/jira/browse/CAMEL-19470)

Exchange body is null when using Mongodb changeStreams with update operation

[CAMEL-19457](https://issues.apache.org/jira/browse/CAMEL-19457)

camel-dynamic-router - InflightRepository size can be negative

[CAMEL-19452](https://issues.apache.org/jira/browse/CAMEL-19452)

camel-jbang - Run with --open-api does not show log in console

[CAMEL-19443](https://issues.apache.org/jira/browse/CAMEL-19443)

camel-kamelet - Route templates should use route configured error handler

[CAMEL-19432](https://issues.apache.org/jira/browse/CAMEL-19432)

camel-azure-eventhubs: Providing a custom EventHubProducerAsyncClient has no effect

[CAMEL-19426](https://issues.apache.org/jira/browse/CAMEL-19426)

Spring-WS syntaxt and path properties inconsistency

[CAMEL-19421](https://issues.apache.org/jira/browse/CAMEL-19421)

Camel-Jira: Use Files.createTempFile in FileConverter instead of creating File directly

[CAMEL-19415](https://issues.apache.org/jira/browse/CAMEL-19415)

camel-stax: using xtokenize might be NPE on xml default namespace

[CAMEL-19399](https://issues.apache.org/jira/browse/CAMEL-19399)

camel-cxf - Prevent storing invalid entry in Converter cache on error

[CAMEL-19393](https://issues.apache.org/jira/browse/CAMEL-19393)

camel-kafka - Configuring kafka option should no longer all be string types

[CAMEL-19387](https://issues.apache.org/jira/browse/CAMEL-19387)

camel-kafka - Cannot set custom azure credential provider

[CAMEL-19383](https://issues.apache.org/jira/browse/CAMEL-19383)

camel-jslt: allowTemplateFromHeader ignores header on subsequent exchanges

[CAMEL-19381](https://issues.apache.org/jira/browse/CAMEL-19381)

Infinite loop creating processes with Camel JBang

[CAMEL-19373](https://issues.apache.org/jira/browse/CAMEL-19373)

spring-rabbitmq - Component does not Respect replyTimeout for InOut Exchanges

[CAMEL-19371](https://issues.apache.org/jira/browse/CAMEL-19371)

RedeliveryErrorHandler's suppressed exceptions cause memory leak and logging issue

[CAMEL-19359](https://issues.apache.org/jira/browse/CAMEL-19359)

camel-spring-boot - When camel start graceful shutdown, it still receive new request during graceful shutdown.

[CAMEL-19345](https://issues.apache.org/jira/browse/CAMEL-19345)

KameletDiscoveryTest fails to find routeTemplate

[CAMEL-19342](https://issues.apache.org/jira/browse/CAMEL-19342)

Rest Inline Routes mixed with direct routes.

[CAMEL-19339](https://issues.apache.org/jira/browse/CAMEL-19339)

karaf - ConnectionFactory not found when use camel-activemq

[CAMEL-19314](https://issues.apache.org/jira/browse/CAMEL-19314)

camel-aws - Connection pool shutdown when aws health checks are used

[CAMEL-19298](https://issues.apache.org/jira/browse/CAMEL-19298)

Snmp: version 3 is not supported for several actions for the component

[CAMEL-19296](https://issues.apache.org/jira/browse/CAMEL-19296)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.xml'

[CAMEL-19295](https://issues.apache.org/jira/browse/CAMEL-19295)

Concurrency issues with dynamicMap in AbstractDynamicRegistry

[CAMEL-19293](https://issues.apache.org/jira/browse/CAMEL-19293)

camel-spring-ldap - base is set twice when using SB AutoConfiguration

[CAMEL-19281](https://issues.apache.org/jira/browse/CAMEL-19281)

Aws2- healthchecks not closing resources for awsClient

[CAMEL-19259](https://issues.apache.org/jira/browse/CAMEL-19259)

camel-maven-plugin - Use configured main-class instead of KameletMain

[CAMEL-19257](https://issues.apache.org/jira/browse/CAMEL-19257)

camel-jslt: Exception when using camel-jslt in Tomcat Servlet

[CAMEL-19256](https://issues.apache.org/jira/browse/CAMEL-19256)

camel-jdbc: leaks the statement in doCreateAndExecuteSqlStatement

[CAMEL-19255](https://issues.apache.org/jira/browse/CAMEL-19255)

Jbang: jbang is not copying custom kamelets to /kametets

[CAMEL-19250](https://issues.apache.org/jira/browse/CAMEL-19250)

Classes generated by camel-restdsl-openapi-plugin are not added to jar

[CAMEL-19249](https://issues.apache.org/jira/browse/CAMEL-19249)

camel-salesforce: Creating blob data is broken

[CAMEL-19247](https://issues.apache.org/jira/browse/CAMEL-19247)

camel-zeebe - Set Default Host and Port for Zeebe connection

[CAMEL-19242](https://issues.apache.org/jira/browse/CAMEL-19242)

camel-jbang - camel doc may not work on main

[CAMEL-19224](https://issues.apache.org/jira/browse/CAMEL-19224)

camel-azure - BlobConsumer does not use prefix

[CAMEL-19199](https://issues.apache.org/jira/browse/CAMEL-19199)

Unable to start PLC4X route in camel-plc4x

[CAMEL-19198](https://issues.apache.org/jira/browse/CAMEL-19198)

Dynamic Router EIP component does not evaluate filters by order of priority attribute

[CAMEL-19190](https://issues.apache.org/jira/browse/CAMEL-19190)

camel-vertx-websocket: sendToAll option may not discover connected host peers correctly

[CAMEL-19181](https://issues.apache.org/jira/browse/CAMEL-19181)

camel-springboot - mapstruct component is not autoconfigured automatically

[CAMEL-19174](https://issues.apache.org/jira/browse/CAMEL-19174)

Jira component: duplicate messages with the new issues consumer

[CAMEL-19162](https://issues.apache.org/jira/browse/CAMEL-19162)

camel-ehcache - llegalStateException: Close not supported from UNINITIALIZED. When context.addRouteDefinition() called multiple times in route with Ehcache consumer

[CAMEL-19158](https://issues.apache.org/jira/browse/CAMEL-19158)

camel-core: ThrowExceptionProcessor may silently ignore exceptions in constructing the exception object

[CAMEL-19156](https://issues.apache.org/jira/browse/CAMEL-19156)

XML route configurations ignored without both XML IO and JAXB XML loaded

[CAMEL-19155](https://issues.apache.org/jira/browse/CAMEL-19155)

Azure Service Bus component completes messages instead of abandoning on error

[CAMEL-19151](https://issues.apache.org/jira/browse/CAMEL-19151)

The 'ignoreInvalidEndpoint' option isn't relevant for a static URI for WireTap component

[CAMEL-19150](https://issues.apache.org/jira/browse/CAMEL-19150)

camel-olingo4: queryParams option of read method does not work

[CAMEL-19136](https://issues.apache.org/jira/browse/CAMEL-19136)

camel-micrometer - Too many tags created by micrometer WebMvcTagsProvider

[CAMEL-19133](https://issues.apache.org/jira/browse/CAMEL-19133)

camel-zookeeper - Zookeeper's service registration and discovery is not working with serialized

[CAMEL-19124](https://issues.apache.org/jira/browse/CAMEL-19124)

Tracer doesn't continue spans for AbstractInternalSpanDecorator

[CAMEL-19113](https://issues.apache.org/jira/browse/CAMEL-19113)

Platform-http-vertx: consume with comma separated does not work

[CAMEL-19112](https://issues.apache.org/jira/browse/CAMEL-19112)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.yaml'

[CAMEL-19111](https://issues.apache.org/jira/browse/CAMEL-19111)

Yaml DSL does not seem to work with split/xtokenize

[CAMEL-19103](https://issues.apache.org/jira/browse/CAMEL-19103)

camel-jbang - can't run in background due to No Camel integration files to run

[CAMEL-19100](https://issues.apache.org/jira/browse/CAMEL-19100)

Milo component does not use dataChangeFilterTrigger value from route

[CAMEL-19098](https://issues.apache.org/jira/browse/CAMEL-19098)

Possible performance issue invoking a bean method with a string parameter

[CAMEL-19095](https://issues.apache.org/jira/browse/CAMEL-19095)

Camel Karaf using buggy Saxon bundle with wrong imports

[CAMEL-19081](https://issues.apache.org/jira/browse/CAMEL-19081)

Start a route with aggregation fails due to NPE in AggregateProcessor

[CAMEL-19079](https://issues.apache.org/jira/browse/CAMEL-19079)

NullPointerException thrown when using the language:xquery endpoint

[CAMEL-19075](https://issues.apache.org/jira/browse/CAMEL-19075)

camel-bean - Incorrect choice of overloaded method with several arguments, if one of them has brackets.

[CAMEL-19067](https://issues.apache.org/jira/browse/CAMEL-19067)

Camel-JBang | camel init creates file but errors out on Windows

[CAMEL-19066](https://issues.apache.org/jira/browse/CAMEL-19066)

Multicast EIP sets correlationId on original Exchange

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19026](https://issues.apache.org/jira/browse/CAMEL-19026)

camel-jbang - camel.main.backlogTracing=true

[CAMEL-19018](https://issues.apache.org/jira/browse/CAMEL-19018)

camel-vertx-http: Headers may get erroneously duplicated

[CAMEL-19014](https://issues.apache.org/jira/browse/CAMEL-19014)

SimpleLanguage cache issue

[CAMEL-19006](https://issues.apache.org/jira/browse/CAMEL-19006)

XML IO DSL do not load templatedRoutes without XML namespace

[CAMEL-19004](https://issues.apache.org/jira/browse/CAMEL-19004)

XML IO DSL do not parse route configuration with XML namespace

[CAMEL-19002](https://issues.apache.org/jira/browse/CAMEL-19002)

camel-jbang - Log command should detect lines without timestamp

[CAMEL-18985](https://issues.apache.org/jira/browse/CAMEL-18985)

camel-kafka: messages are getting lost with "breakOnFirstError"

[CAMEL-18980](https://issues.apache.org/jira/browse/CAMEL-18980)

camel snmp - SNMP Ver1 trap does not work

[CAMEL-18968](https://issues.apache.org/jira/browse/CAMEL-18968)

Camel-aws2-sqs - Queue url might stay empty for the delayed queue.

[CAMEL-18954](https://issues.apache.org/jira/browse/CAMEL-18954)

camel-micrometer - NPE on spring boot

[CAMEL-18944](https://issues.apache.org/jira/browse/CAMEL-18944)

REST YAML does not work in Spring Boot

[CAMEL-18922](https://issues.apache.org/jira/browse/CAMEL-18922)

TemplatedRoute fails to load with XML RouteLoader

[CAMEL-18878](https://issues.apache.org/jira/browse/CAMEL-18878)

Autowiring on endpoint works even if is disabled on component

[CAMEL-18872](https://issues.apache.org/jira/browse/CAMEL-18872)

camel-core-model - Rest DSL param example not available in XML and YAML DSL

[CAMEL-18871](https://issues.apache.org/jira/browse/CAMEL-18871)

camel-netty - Application does not recover (threads are WAITING) when NettyProducer pool is exhausted

[CAMEL-18868](https://issues.apache.org/jira/browse/CAMEL-18868)

Aws2-s3: CreateDownloadLink does not work with useDefaultCredentialsProvider

[CAMEL-18865](https://issues.apache.org/jira/browse/CAMEL-18865)

camel-main - Setters not invoked on bean that implements Map

[CAMEL-18856](https://issues.apache.org/jira/browse/CAMEL-18856)

camel-main - Unable to declare java.util.List bean

[CAMEL-18854](https://issues.apache.org/jira/browse/CAMEL-18854)

camel-rabbitmq x-queue-type no longer working

[CAMEL-18844](https://issues.apache.org/jira/browse/CAMEL-18844)

Possible memory leak in org.apache.camel.impl.console.EventConsole

[CAMEL-18842](https://issues.apache.org/jira/browse/CAMEL-18842)

camel-as2 failed to serve signed requests when compression is done before signing

[CAMEL-18841](https://issues.apache.org/jira/browse/CAMEL-18841)

camel-kafka: producer idempotence is not enabled by default

[CAMEL-18840](https://issues.apache.org/jira/browse/CAMEL-18840)

camel-http - HTTP broken followRedirection

[CAMEL-18834](https://issues.apache.org/jira/browse/CAMEL-18834)

camel-core - StringQuoteHelper should remove quotes for single element

[CAMEL-18780](https://issues.apache.org/jira/browse/CAMEL-18780)

Sqs2Consumer message extended causing rejected execution exception when used with threads EIP

[CAMEL-18619](https://issues.apache.org/jira/browse/CAMEL-18619)

Stream closed for onException with useOriginalMessage

[CAMEL-18437](https://issues.apache.org/jira/browse/CAMEL-18437)

Camel-bigquery: There is a difference in types between @name and ${name}

[CAMEL-17544](https://issues.apache.org/jira/browse/CAMEL-17544)

ServicePool.doStop still hangs during shutdown

[CAMEL-15111](https://issues.apache.org/jira/browse/CAMEL-15111)

camel-as2 component failed to parse entity content for encrypted or compressed data

[CAMEL-14008](https://issues.apache.org/jira/browse/CAMEL-14008)

camel-as2 - AS2 Connection can only handle one connection (connection recovery needed)

### Dependency upgrade (26)

[CAMEL-19488](https://issues.apache.org/jira/browse/CAMEL-19488)

Some OSGi features need snakeyaml 1.3.x

[CAMEL-19480](https://issues.apache.org/jira/browse/CAMEL-19480)

camel-netty - Upgrade to 4.1.94

[CAMEL-19473](https://issues.apache.org/jira/browse/CAMEL-19473)

camel-spring-boot - Upgrade to 2.7.13

[CAMEL-19458](https://issues.apache.org/jira/browse/CAMEL-19458)

Bouncycastle 1.73 to 1.74

[CAMEL-19390](https://issues.apache.org/jira/browse/CAMEL-19390)

camel-cxf - Upgrade to 3.6.1

[CAMEL-19372](https://issues.apache.org/jira/browse/CAMEL-19372)

camel-spring-boot - Upgrade to 2.7.12

[CAMEL-19351](https://issues.apache.org/jira/browse/CAMEL-19351)

camel-jackson - Upgrade to 2.14.3

[CAMEL-19340](https://issues.apache.org/jira/browse/CAMEL-19340)

camel-jbang - Upgrade to maven-resolver 1.9.10

[CAMEL-19301](https://issues.apache.org/jira/browse/CAMEL-19301)

camel-jbang - Upgrade to hawtio 2.17.2

[CAMEL-19288](https://issues.apache.org/jira/browse/CAMEL-19288)

camel-jsonpath - Upgrade to 2.8

[CAMEL-19278](https://issues.apache.org/jira/browse/CAMEL-19278)

camel-xslt-saxon - Upgrade to Saxon-HE 11.5

[CAMEL-19275](https://issues.apache.org/jira/browse/CAMEL-19275)

camel-spring-boot- Upgrade to 2.7.11

[CAMEL-19265](https://issues.apache.org/jira/browse/CAMEL-19265)

camel-jbang - Upgrade to Picoli 4.7.2

[CAMEL-19261](https://issues.apache.org/jira/browse/CAMEL-19261)

camel-jbang - Upgrade gradle wrapper to 8.x

[CAMEL-19153](https://issues.apache.org/jira/browse/CAMEL-19153)

camel-spring-boot - Upgrade to 2.7.10

[CAMEL-19131](https://issues.apache.org/jira/browse/CAMEL-19131)

Camel-DJL: Upgrade to Deep Java Library 0.21.0

[CAMEL-19123](https://issues.apache.org/jira/browse/CAMEL-19123)

camel-jbang - upgrade maven-resolver to 1.9.7

[CAMEL-19092](https://issues.apache.org/jira/browse/CAMEL-19092)

camel-jbang - upgrade maven-resolver-api to 1.9.5

[CAMEL-19039](https://issues.apache.org/jira/browse/CAMEL-19039)

camel-jms - Upgrade to Artemis 2.28.x

[CAMEL-19019](https://issues.apache.org/jira/browse/CAMEL-19019)

camel-kafka - Upgrade to Kafka 3.4.x

[CAMEL-18999](https://issues.apache.org/jira/browse/CAMEL-18999)

camel-sshd - Upgrade to 2.9.x

[CAMEL-18947](https://issues.apache.org/jira/browse/CAMEL-18947)

camel-spring-boot - Upgrade to 2.7.8

[CAMEL-18880](https://issues.apache.org/jira/browse/CAMEL-18880)

camel-jbang - upgrade maven-resolver-api to 1.9.4

[CAMEL-18843](https://issues.apache.org/jira/browse/CAMEL-18843)

camel-spring-boot - Upgrade to 2.7.7

[CAMEL-18839](https://issues.apache.org/jira/browse/CAMEL-18839)

upgrade to kafka 3.3.x

[CAMEL-18830](https://issues.apache.org/jira/browse/CAMEL-18830)

camel-ehcache - Align to JAXB from camel

### Improvement (104)

[CAMEL-19478](https://issues.apache.org/jira/browse/CAMEL-19478)

camel-core - Add synchronous option to some EIPs like split

[CAMEL-19477](https://issues.apache.org/jira/browse/CAMEL-19477)

MeterRegistry collects authorization data

[CAMEL-19471](https://issues.apache.org/jira/browse/CAMEL-19471)

camel-yaml-dsl - JSON library enum consistency

[CAMEL-19455](https://issues.apache.org/jira/browse/CAMEL-19455)

camel-cxf - Ensure REQUEST\_CONTEXT & RESPONSE\_CONTEXT headers are Map when populating CXF Message from Camel Message

[CAMEL-19454](https://issues.apache.org/jira/browse/CAMEL-19454)

camel-jbang - Export should support --open-api

[CAMEL-19453](https://issues.apache.org/jira/browse/CAMEL-19453)

camel-jbang - Run with --open-api to support yaml spec files

[CAMEL-19379](https://issues.apache.org/jira/browse/CAMEL-19379)

EndpointSchemaGeneratorMojo: Improve "Could not find component java type" error message

[CAMEL-19378](https://issues.apache.org/jira/browse/CAMEL-19378)

File Changed ReadLock Strategy with minAge only looks for lastModified

[CAMEL-19377](https://issues.apache.org/jira/browse/CAMEL-19377)

camel-platform-http - Return 503 if consumer is suspended

[CAMEL-19370](https://issues.apache.org/jira/browse/CAMEL-19370)

camel-jbang - Make it possible to show full url for very long endpoints

[CAMEL-19368](https://issues.apache.org/jira/browse/CAMEL-19368)

camel-main - Auto detect custom EventNotifer from registry

[CAMEL-19366](https://issues.apache.org/jira/browse/CAMEL-19366)

camel-core - Trigger reload via dev console make it async

[CAMEL-19362](https://issues.apache.org/jira/browse/CAMEL-19362)

camel-core - Tracing without inner details of Kamelets

[CAMEL-19361](https://issues.apache.org/jira/browse/CAMEL-19361)

camel-jbang - Parse trait.camel.apache.org/camel.properties from KameletBinding

[CAMEL-19360](https://issues.apache.org/jira/browse/CAMEL-19360)

camel-jbang - Export a set of files

[CAMEL-19357](https://issues.apache.org/jira/browse/CAMEL-19357)

camel-jbang - Use a vertx task for tasks to avoid blocking io thread

[CAMEL-19353](https://issues.apache.org/jira/browse/CAMEL-19353)

Camel-Jbang reload exception

[CAMEL-19352](https://issues.apache.org/jira/browse/CAMEL-19352)

Improve camel-mybatis documentation

[CAMEL-19350](https://issues.apache.org/jira/browse/CAMEL-19350)

camel-jpa: Output into header/property

[CAMEL-19327](https://issues.apache.org/jira/browse/CAMEL-19327)

camel-jpa: Single result

[CAMEL-19326](https://issues.apache.org/jira/browse/CAMEL-19326)

camel-jbang - Register reload services eager

[CAMEL-19322](https://issues.apache.org/jira/browse/CAMEL-19322)

camel-jbang - Source Dir to support application.properties

[CAMEL-19313](https://issues.apache.org/jira/browse/CAMEL-19313)

camel-jbang - Provide a way to append Maven repository provided from command-line to the one provided in configuration

[CAMEL-19311](https://issues.apache.org/jira/browse/CAMEL-19311)

Review the SimpleLRUCache to become thread-safe

[CAMEL-19306](https://issues.apache.org/jira/browse/CAMEL-19306)

camel-jbang - Allow to load yaml files with beans only

[CAMEL-19302](https://issues.apache.org/jira/browse/CAMEL-19302)

Use filename to generate id of route when creating Camel file in XML DSL with Camel JBang

[CAMEL-19276](https://issues.apache.org/jira/browse/CAMEL-19276)

camel-jq: Include jackson-jq extras module

[CAMEL-19266](https://issues.apache.org/jira/browse/CAMEL-19266)

Camel-AWS2-S3: Add a forcePathStyle option to configuration

[CAMEL-19237](https://issues.apache.org/jira/browse/CAMEL-19237)

camel-jbang - version list for newer releases to include details

[CAMEL-19231](https://issues.apache.org/jira/browse/CAMEL-19231)

Default REST DSL type in camel-jbang generator

[CAMEL-19227](https://issues.apache.org/jira/browse/CAMEL-19227)

camel-jbang - export should also add <pluginRepository> with repos

[CAMEL-19226](https://issues.apache.org/jira/browse/CAMEL-19226)

camel-jbang - Add repos option to export

[CAMEL-19222](https://issues.apache.org/jira/browse/CAMEL-19222)

Camel-Azure-CosmosDB: make the itemPartitionKey a String instead of a pojo

[CAMEL-19219](https://issues.apache.org/jira/browse/CAMEL-19219)

camel-kudu - add projection and limit support to the scan operation

[CAMEL-19216](https://issues.apache.org/jira/browse/CAMEL-19216)

camel-kudu - add predicate support to the scan operation

[CAMEL-19214](https://issues.apache.org/jira/browse/CAMEL-19214)

camel-hdfs - Add ShortWritable support to the HDFS component

[CAMEL-19211](https://issues.apache.org/jira/browse/CAMEL-19211)

camel-sql - Make it possible to configure custom RowMapper

[CAMEL-19210](https://issues.apache.org/jira/browse/CAMEL-19210)

camel-pulsar - Support for delayed delivery pulsar messages using deliverAt

[CAMEL-19205](https://issues.apache.org/jira/browse/CAMEL-19205)

camel-plc4x - Make it easier to configure tags in endpoint

[CAMEL-19193](https://issues.apache.org/jira/browse/CAMEL-19193)

Change default Micrometer meter names to follow Micrometer naming conventions

[CAMEL-19187](https://issues.apache.org/jira/browse/CAMEL-19187)

camel-jbang - dependency list should use user configured version

[CAMEL-19186](https://issues.apache.org/jira/browse/CAMEL-19186)

camel-core - Type function in simple language should use enum type instead of toString value

[CAMEL-19185](https://issues.apache.org/jira/browse/CAMEL-19185)

Camel Spring Boot Example: Twitter-Salesforce: camel-salesforce-maven-plugin - make TLS version configurable via system properties

[CAMEL-19180](https://issues.apache.org/jira/browse/CAMEL-19180)

Kafka Idempotent Repository does not give the user control over a randomized group id if the kafka broker requires the id to be in a specified form

[CAMEL-19178](https://issues.apache.org/jira/browse/CAMEL-19178)

camel-common-http - Make HttpBinding more reusable

[CAMEL-19177](https://issues.apache.org/jira/browse/CAMEL-19177)

camel-platform-http - Spring Boot implementation that use directly the HTTP server

[CAMEL-19176](https://issues.apache.org/jira/browse/CAMEL-19176)

camel-platform-http - Add listener for added/removed http endpoints

[CAMEL-19173](https://issues.apache.org/jira/browse/CAMEL-19173)

Splitting long uris in xml-io DSL doesn't work

[CAMEL-19168](https://issues.apache.org/jira/browse/CAMEL-19168)

camel-micrometer-starter - Make it possible to capture static uri path as tag

[CAMEL-19152](https://issues.apache.org/jira/browse/CAMEL-19152)

camel-azure - Add file client header and flush option

[CAMEL-19145](https://issues.apache.org/jira/browse/CAMEL-19145)

camel-jbang - Add known alias for maven repos

[CAMEL-19144](https://issues.apache.org/jira/browse/CAMEL-19144)

camel-catalog - Include information about existing Camel releases

[CAMEL-19137](https://issues.apache.org/jira/browse/CAMEL-19137)

Favor CompositeMeterRegistry instances in Camel registry

[CAMEL-19132](https://issues.apache.org/jira/browse/CAMEL-19132)

camel-core - Deprecate vm and direct-vm and remove in v4

[CAMEL-19122](https://issues.apache.org/jira/browse/CAMEL-19122)

camel-jbang - Export java code with existing package name

[CAMEL-19118](https://issues.apache.org/jira/browse/CAMEL-19118)

camel-health - Liveness check default false

[CAMEL-19109](https://issues.apache.org/jira/browse/CAMEL-19109)

camel-vertx-websocket: Consumer should avoid blocking the Vert.x event loop

[CAMEL-19108](https://issues.apache.org/jira/browse/CAMEL-19108)

camel-jbang - Export with local JAR should include the JAR in lib folder and add as dependency

[CAMEL-19101](https://issues.apache.org/jira/browse/CAMEL-19101)

Features for Camel-Micrometer

[CAMEL-19094](https://issues.apache.org/jira/browse/CAMEL-19094)

Tokenizer ignores includeTokens

[CAMEL-19093](https://issues.apache.org/jira/browse/CAMEL-19093)

camel-jbang - Run local JAR should add to classpath so can be used in Java DSL

[CAMEL-19083](https://issues.apache.org/jira/browse/CAMEL-19083)

camel-yaml-dsl: Add a doc section that links to the schema

[CAMEL-19078](https://issues.apache.org/jira/browse/CAMEL-19078)

camel-platform-http-vertx: Allow response headers with empty values to be returned

[CAMEL-19073](https://issues.apache.org/jira/browse/CAMEL-19073)

camel-core - Properties component - reload properties for only changed

[CAMEL-19071](https://issues.apache.org/jira/browse/CAMEL-19071)

camel-jbang - Reload all routes in changes to application.properties in dev mode

[CAMEL-19042](https://issues.apache.org/jira/browse/CAMEL-19042)

camel-quarkus-catalog - Uses 0.0.1 version

[CAMEL-19025](https://issues.apache.org/jira/browse/CAMEL-19025)

camel-jbang - doc command should be case insensitive in filter

[CAMEL-19017](https://issues.apache.org/jira/browse/CAMEL-19017)

camel-main - Tracing to output message headers

[CAMEL-19008](https://issues.apache.org/jira/browse/CAMEL-19008)

spring-rabbitmq component does not fail on sending to non-existent RabbitMQ topic

[CAMEL-18990](https://issues.apache.org/jira/browse/CAMEL-18990)

camel-jbang - Export to Quarkus should add resources for native compilation

[CAMEL-18986](https://issues.apache.org/jira/browse/CAMEL-18986)

camel-core - ProducerTemplate send exchange should set from endpoint if null

[CAMEL-18983](https://issues.apache.org/jira/browse/CAMEL-18983)

camel-jbang - Automatic detect atlassian maven repo when using camel-jira

[CAMEL-18979](https://issues.apache.org/jira/browse/CAMEL-18979)

Add delimiter and prefix to the listObjects operation of AWS S3 Producer

[CAMEL-18967](https://issues.apache.org/jira/browse/CAMEL-18967)

camel-platform-http-vertx: Improve handling of whether an HTTP request body is allowed or not

[CAMEL-18952](https://issues.apache.org/jira/browse/CAMEL-18952)

camel-rest - Favour using platform-http if available on classpath

[CAMEL-18942](https://issues.apache.org/jira/browse/CAMEL-18942)

openapi-rest-dsl-generator - Copy the description of the path/operation to the generated route

[CAMEL-18923](https://issues.apache.org/jira/browse/CAMEL-18923)

Cannot update a routeconfiguration with a routeloader

[CAMEL-18917](https://issues.apache.org/jira/browse/CAMEL-18917)

camel-as2 - Signature is not validated

[CAMEL-18912](https://issues.apache.org/jira/browse/CAMEL-18912)

Sqs2ConsumerHealthCheck is broken when using injected client

[CAMEL-18877](https://issues.apache.org/jira/browse/CAMEL-18877)

camel-caffeine - Key should be string type

[CAMEL-18875](https://issues.apache.org/jira/browse/CAMEL-18875)

camel-jms - Logging less noisy when temporary reply queue is refreshed

[CAMEL-18874](https://issues.apache.org/jira/browse/CAMEL-18874)

camel-file - When possible, pass the exchange to the exception handler

[CAMEL-18873](https://issues.apache.org/jira/browse/CAMEL-18873)

Camel-Elasticsearch: CertificatePath should be readable through ResourceHelper

[CAMEL-18863](https://issues.apache.org/jira/browse/CAMEL-18863)

camel-pulsar - Support chunking to enable sending a large message

[CAMEL-18862](https://issues.apache.org/jira/browse/CAMEL-18862)

Using Spring Boot Camel Starter the RoutesCollector doesn't see RoutesBuilder added via Camel Context Registry

[CAMEL-18857](https://issues.apache.org/jira/browse/CAMEL-18857)

camel-core - Auto assigned route ids for kamelets/templates should use tempate name as prefix

[CAMEL-18852](https://issues.apache.org/jira/browse/CAMEL-18852)

camel-atom/camel-rss - Deprecate basic auth

[CAMEL-18850](https://issues.apache.org/jira/browse/CAMEL-18850)

camel-core-model - @XmlAttributes should be String or Enum type only

[CAMEL-18849](https://issues.apache.org/jira/browse/CAMEL-18849)

camel-core-model - Route properties should be in top of route

[CAMEL-18848](https://issues.apache.org/jira/browse/CAMEL-18848)

camel-core-model - Rest DSL allowedValues should use definition model for value

[CAMEL-18847](https://issues.apache.org/jira/browse/CAMEL-18847)

camel-console - We need a camel-console-support JAR

[CAMEL-18846](https://issues.apache.org/jira/browse/CAMEL-18846)

camel-main - Performance overhead due to emitting events not needed

[CAMEL-18845](https://issues.apache.org/jira/browse/CAMEL-18845)

camel-core - Performance overhead for async processing event emitting

[CAMEL-18832](https://issues.apache.org/jira/browse/CAMEL-18832)

camel-spring-boot - Health Check output should include data in full exposure level

[CAMEL-18828](https://issues.apache.org/jira/browse/CAMEL-18828)

camel-kudu - Add DELETE, UPDATE, and UPSERT support to the producer

[CAMEL-18815](https://issues.apache.org/jira/browse/CAMEL-18815)

camel-jbang - Base package scan to search in downloaded JARs

[CAMEL-18769](https://issues.apache.org/jira/browse/CAMEL-18769)

camel-jbang - Catalog to select runtime

[CAMEL-18752](https://issues.apache.org/jira/browse/CAMEL-18752)

camel-micrometer - Include description in prometheus export

[CAMEL-18674](https://issues.apache.org/jira/browse/CAMEL-18674)

camel-jbang - Run in background

[CAMEL-18659](https://issues.apache.org/jira/browse/CAMEL-18659)

camel-openapi-java - Support for nullable

[CAMEL-18636](https://issues.apache.org/jira/browse/CAMEL-18636)

azure data lake component: authentication can not be configured using string properties

[CAMEL-18216](https://issues.apache.org/jira/browse/CAMEL-18216)

camel-core - expose universal error handlers in all DSLs

[CAMEL-17652](https://issues.apache.org/jira/browse/CAMEL-17652)

camel-minio - Auto create bucket should not be done in endpoint

[CAMEL-11767](https://issues.apache.org/jira/browse/CAMEL-11767)

camel-catalog-maven - Use real maven downloader (was: Maybe use shrinkwrap instead of gradle)

### New Feature (42)

[CAMEL-19349](https://issues.apache.org/jira/browse/CAMEL-19349)

camel-core - Dev console for source to support camel-jbang source-dir

[CAMEL-19344](https://issues.apache.org/jira/browse/CAMEL-19344)

camel-jbang - Reload to source dir via http

[CAMEL-19325](https://issues.apache.org/jira/browse/CAMEL-19325)

azure-cosmosdb: Add default identity authentication

[CAMEL-19320](https://issues.apache.org/jira/browse/CAMEL-19320)

camel-jbang - Add command to reload

[CAMEL-19309](https://issues.apache.org/jira/browse/CAMEL-19309)

camel-jbang - Run with empty folder

[CAMEL-19304](https://issues.apache.org/jira/browse/CAMEL-19304)

JPA paging support

[CAMEL-19299](https://issues.apache.org/jira/browse/CAMEL-19299)

camel-console - Add dev console for bean registry

[CAMEL-19270](https://issues.apache.org/jira/browse/CAMEL-19270)

camel-netty - Add support for Unix Domain Sockets

[CAMEL-19212](https://issues.apache.org/jira/browse/CAMEL-19212)

camel-groovy - provide a way to define global groovy variables

[CAMEL-19188](https://issues.apache.org/jira/browse/CAMEL-19188)

GraphQL component should support Exchange.HTTP\_QUERY or custom headers

[CAMEL-19143](https://issues.apache.org/jira/browse/CAMEL-19143)

Bindy - Add option to quote fields only when necessary

[CAMEL-19128](https://issues.apache.org/jira/browse/CAMEL-19128)

camel-jbang - Version command

[CAMEL-19120](https://issues.apache.org/jira/browse/CAMEL-19120)

camel-jbang - export configurable template

[CAMEL-19099](https://issues.apache.org/jira/browse/CAMEL-19099)

Camel-Jbang Export: Add a flag to include secret refresh properties in application.properties

[CAMEL-19069](https://issues.apache.org/jira/browse/CAMEL-19069)

Presigned urls in camel-minio component

[CAMEL-19050](https://issues.apache.org/jira/browse/CAMEL-19050)

DHIS2 Component

[CAMEL-19044](https://issues.apache.org/jira/browse/CAMEL-19044)

Camel-Jbang catalog output in JSON

[CAMEL-19033](https://issues.apache.org/jira/browse/CAMEL-19033)

camel-jbang - Add trace command

[CAMEL-19030](https://issues.apache.org/jira/browse/CAMEL-19030)

camel-jbang - doc and catalog to support --camel-version option

[CAMEL-19027](https://issues.apache.org/jira/browse/CAMEL-19027)

camel-console - Add dev console for backlog tracer

[CAMEL-19023](https://issues.apache.org/jira/browse/CAMEL-19023)

Add support for Micrometer Observation

[CAMEL-19020](https://issues.apache.org/jira/browse/CAMEL-19020)

camel-console - Add dev console for tracing messages (backlog tracer)

[CAMEL-18989](https://issues.apache.org/jira/browse/CAMEL-18989)

camel-jbang - Run custom distributions of Camel

[CAMEL-18981](https://issues.apache.org/jira/browse/CAMEL-18981)

camel-vertx-websocket: Add capability to capture peer connect / disconnect events

[CAMEL-18966](https://issues.apache.org/jira/browse/CAMEL-18966)

Add component for Camunda Zeebe support

[CAMEL-18940](https://issues.apache.org/jira/browse/CAMEL-18940)

camel-vertx-websocket: Support URI path and query params for WS server consumer

[CAMEL-18909](https://issues.apache.org/jira/browse/CAMEL-18909)

Add DTO generator option in camel-jbang generate command

[CAMEL-18904](https://issues.apache.org/jira/browse/CAMEL-18904)

camel-core - Add functions to simple language to create empty map/list/string/json

[CAMEL-18823](https://issues.apache.org/jira/browse/CAMEL-18823)

Provide option to download dependencies to a specific folder with Camel JBang/camel CLI

[CAMEL-18687](https://issues.apache.org/jira/browse/CAMEL-18687)

camel-salesforce: Support Client Credentials OAuth Flow

[CAMEL-18625](https://issues.apache.org/jira/browse/CAMEL-18625)

Provide an option to pass specific AWS SAML Profile

[CAMEL-18538](https://issues.apache.org/jira/browse/CAMEL-18538)

camel-jbang - Add log command

[CAMEL-18525](https://issues.apache.org/jira/browse/CAMEL-18525)

camel-jbang - CLI output in color

[CAMEL-18523](https://issues.apache.org/jira/browse/CAMEL-18523)

camel-jbang - Add watch option

[CAMEL-18508](https://issues.apache.org/jira/browse/CAMEL-18508)

camel-jbang - User config file

[CAMEL-18497](https://issues.apache.org/jira/browse/CAMEL-18497)

camel-jbang - camel run -v x.y.z

[CAMEL-18131](https://issues.apache.org/jira/browse/CAMEL-18131)

camel-health - Add health checks for components that has extension for connectivity verification

[CAMEL-17946](https://issues.apache.org/jira/browse/CAMEL-17946)

camel-as2 - Add https support

[CAMEL-17895](https://issues.apache.org/jira/browse/CAMEL-17895)

camel-vertx-websocket: Consumer as WS client

[CAMEL-17495](https://issues.apache.org/jira/browse/CAMEL-17495)

camel-as2 - No support for application/xml content type

[CAMEL-17066](https://issues.apache.org/jira/browse/CAMEL-17066)

camel-nats - Support authentication with Nats server

[CAMEL-5963](https://issues.apache.org/jira/browse/CAMEL-5963)

camel-smpp: Support TRX connection mode to the SMSC

### Sub-task (1)

[CAMEL-18991](https://issues.apache.org/jira/browse/CAMEL-18991)

Camel-Google-Storage: Health Check for consumer

### Task (28)

[CAMEL-19410](https://issues.apache.org/jira/browse/CAMEL-19410)

Camel 4.0.0-M3 with Velocity - Deprecation warning

[CAMEL-19392](https://issues.apache.org/jira/browse/CAMEL-19392)

Correct template bean definition schema

[CAMEL-19328](https://issues.apache.org/jira/browse/CAMEL-19328)

CamelAwsSesTo and CamelAwsSesReplyToAddresses update documentation with String instead of List

[CAMEL-19294](https://issues.apache.org/jira/browse/CAMEL-19294)

camel-test-infra-zookeeper: unable to use a custom Zookeeper container

[CAMEL-19248](https://issues.apache.org/jira/browse/CAMEL-19248)

Suspicious ignoring of a variable in CouchbaseConsumer

[CAMEL-19207](https://issues.apache.org/jira/browse/CAMEL-19207)

Missing version for mysql:mysql-connector-java in SB examples

[CAMEL-19202](https://issues.apache.org/jira/browse/CAMEL-19202)

Unused assignment in OnExceptionReifier

[CAMEL-19201](https://issues.apache.org/jira/browse/CAMEL-19201)

Unused assignment in AdviceWithBuilder::maxDeep()

[CAMEL-19200](https://issues.apache.org/jira/browse/CAMEL-19200)

Unused assignment in RouteControllerAction::getLast(Row r)

[CAMEL-19138](https://issues.apache.org/jira/browse/CAMEL-19138)

Maven 3.9.0 build fails with -Psourcecheck

[CAMEL-19119](https://issues.apache.org/jira/browse/CAMEL-19119)

\[Docs\] Missing examples in Camel JDBC

[CAMEL-19106](https://issues.apache.org/jira/browse/CAMEL-19106)

repair checkstyle in branch camel-3.x

[CAMEL-19009](https://issues.apache.org/jira/browse/CAMEL-19009)

camel-gson - Date Format with GsonBuilder

[CAMEL-19007](https://issues.apache.org/jira/browse/CAMEL-19007)

camel-yaml-dsl - Deprecate classic parsing mode

[CAMEL-18996](https://issues.apache.org/jira/browse/CAMEL-18996)

Camel-CassandraQL: Adding a parameter to pass a list of ExtraTypesCodec to SessionBuilder

[CAMEL-18977](https://issues.apache.org/jira/browse/CAMEL-18977)

camel-joor - Make the code more flexible for native mode

[CAMEL-18890](https://issues.apache.org/jira/browse/CAMEL-18890)

Remove camel-vertx-kafka

[CAMEL-18870](https://issues.apache.org/jira/browse/CAMEL-18870)

Error while generating OSGi manifest

[CAMEL-18866](https://issues.apache.org/jira/browse/CAMEL-18866)

camel-rabbitmq - Deprecate as should use camel-spring-rabbitmq instead

[CAMEL-18864](https://issues.apache.org/jira/browse/CAMEL-18864)

java-joor-dsl - Drop support of class files

[CAMEL-18860](https://issues.apache.org/jira/browse/CAMEL-18860)

java-joor-dsl - Adapt the code for native compilation

[CAMEL-18853](https://issues.apache.org/jira/browse/CAMEL-18853)

camel-swagger-java - Deprecate as we have camel-openapi-java

[CAMEL-18831](https://issues.apache.org/jira/browse/CAMEL-18831)

camel-xstream - Deprecate

[CAMEL-18829](https://issues.apache.org/jira/browse/CAMEL-18829)

camel-yaml-dsl - generate-yaml-schema - Support \`additionalProperties: false\`

[CAMEL-18825](https://issues.apache.org/jira/browse/CAMEL-18825)

Make XML parser more secured out of the box

[CAMEL-18779](https://issues.apache.org/jira/browse/CAMEL-18779)

camel-test-infra: investigate replacing ActiveMQ with Artemis for embedded testing

[CAMEL-18742](https://issues.apache.org/jira/browse/CAMEL-18742)

camel-jpa: deprecated transactionManager property

[CAMEL-18496](https://issues.apache.org/jira/browse/CAMEL-18496)

Remove deprecated components

### Test (3)

[CAMEL-18827](https://issues.apache.org/jira/browse/CAMEL-18827)

camel-kudu - Fix unit test failure with JDK 17

[CAMEL-18826](https://issues.apache.org/jira/browse/CAMEL-18826)

camel-kudu - Install libtinfo on CI to execute all Kudu's unit tests

[CAMEL-18620](https://issues.apache.org/jira/browse/CAMEL-18620)

Add redpanda container to test-infra

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).