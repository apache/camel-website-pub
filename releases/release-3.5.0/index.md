# Apache camel 3.5.0 Release

## New and Noteworthy

This release is the new Camel 3.5.0 patch release.

## Supported Java version

This version supports Java 8 and 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.5.0</version>
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
      <version>3.5.0</version>
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
| [apache-camel-3.5.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.5.0/apache-camel-3.5.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.5.0/apache-camel-3.5.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.5.0/apache-camel-3.5.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.5.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.5.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (70)

[CAMEL-15962](https://issues.apache.org/jira/browse/CAMEL-15962)

mimeMultipart dataformat is not included in the XML DSL for marshal/unmarshal

[CAMEL-15473](https://issues.apache.org/jira/browse/CAMEL-15473)

Spring Boot Swagger Example - API specification generation fails

[CAMEL-15460](https://issues.apache.org/jira/browse/CAMEL-15460)

FTP Reconnect not successful

[CAMEL-15457](https://issues.apache.org/jira/browse/CAMEL-15457)

camel-micrometer: NullPointer exception triggered by MicrometerExchangeEventNotifier

[CAMEL-15455](https://issues.apache.org/jira/browse/CAMEL-15455)

EndpointDSL breaks expressions in query parameters

[CAMEL-15454](https://issues.apache.org/jira/browse/CAMEL-15454)

camel-cluster - Adding a new route after camel is started should start the route if leader

[CAMEL-15450](https://issues.apache.org/jira/browse/CAMEL-15450)

ClusteredRoutePolicyFactory throw NullPointerException when adding a route to CamelContext that has been started

[CAMEL-15449](https://issues.apache.org/jira/browse/CAMEL-15449)

camel-salesforce - BulkAPI createBatchQuery swallows error

[CAMEL-15445](https://issues.apache.org/jira/browse/CAMEL-15445)

component lifecycle is differen when endpoints are created using endpointdsl

[CAMEL-15436](https://issues.apache.org/jira/browse/CAMEL-15436)

camel-azure-storage-blob: If the AppendFile does not exist, it will be created but it will not append to the end of the content

[CAMEL-15426](https://issues.apache.org/jira/browse/CAMEL-15426)

camel-main should not package test resource configurer config

[CAMEL-15425](https://issues.apache.org/jira/browse/CAMEL-15425)

camel-salesforce: SalesforceLoginConfig seems to be leaking the password

[CAMEL-15424](https://issues.apache.org/jira/browse/CAMEL-15424)

camel-box: addFolderCollaboration may throw an NPE

[CAMEL-15420](https://issues.apache.org/jira/browse/CAMEL-15420)

camel-http dynamic aware removes Exchange.HTTP\_QUERY header if Exchange.HTTP\_PATH header not specified

[CAMEL-15407](https://issues.apache.org/jira/browse/CAMEL-15407)

Merge operation in camel-olingo2 sets all entity properties to null

[CAMEL-15400](https://issues.apache.org/jira/browse/CAMEL-15400)

rest component - Endpoint DSL for multi valued has null as prefix

[CAMEL-15394](https://issues.apache.org/jira/browse/CAMEL-15394)

PropertyBindingSupport - Root object has issue with list and source code generated configurer

[CAMEL-15391](https://issues.apache.org/jira/browse/CAMEL-15391)

camel-aws2-sqs: amazonAWSHost is not set

[CAMEL-15387](https://issues.apache.org/jira/browse/CAMEL-15387)

Can't set Salesforce packages via application properties.

[CAMEL-15383](https://issues.apache.org/jira/browse/CAMEL-15383)

Camel 3 Velocity warns about deprecated configuration keys

[CAMEL-15382](https://issues.apache.org/jira/browse/CAMEL-15382)

Opentelemetry injection/extraction doesn't work

[CAMEL-15378](https://issues.apache.org/jira/browse/CAMEL-15378)

File gets locked When using camel-flatpack delimited parser

[CAMEL-15372](https://issues.apache.org/jira/browse/CAMEL-15372)

Missing classes for opentracing camel-spring-boot

[CAMEL-15370](https://issues.apache.org/jira/browse/CAMEL-15370)

CxfRsProducer: All but last value of query parameter with multiple values are lost

[CAMEL-15369](https://issues.apache.org/jira/browse/CAMEL-15369)

camel-aws2-kinesis: IndexOutOfBoundsException when polling

[CAMEL-15358](https://issues.apache.org/jira/browse/CAMEL-15358)

camel-aws-kinesis: IndexOutOfBoundsException when polling

[CAMEL-15355](https://issues.apache.org/jira/browse/CAMEL-15355)

unacceptable\_type,longstr error if we set 'arg.queue.x-single-active-consumer=true in rabbitmq endpoint url

[CAMEL-15350](https://issues.apache.org/jira/browse/CAMEL-15350)

SJMS Batch Consumer error recovery

[CAMEL-15349](https://issues.apache.org/jira/browse/CAMEL-15349)

camel-xmpp can't consume direct message chats

[CAMEL-15348](https://issues.apache.org/jira/browse/CAMEL-15348)

cxfEndpoint blueprint namespace handler - problem with QName vs String

[CAMEL-15347](https://issues.apache.org/jira/browse/CAMEL-15347)

Camel-aws2-s3: moveAfterRead true bucket not created

[CAMEL-15344](https://issues.apache.org/jira/browse/CAMEL-15344)

ShutdownStrategy - Inflight count is reporting wrong with 2x the actual number

[CAMEL-15343](https://issues.apache.org/jira/browse/CAMEL-15343)

camel-main - Graceful shutdown from ctrl + c SIGTERM is not working correctly

[CAMEL-15338](https://issues.apache.org/jira/browse/CAMEL-15338)

Salesforce - Wrong Channel Name for Standard Platform Events

[CAMEL-15336](https://issues.apache.org/jira/browse/CAMEL-15336)

Wrong information for supported platforms in FAQ of website

[CAMEL-15327](https://issues.apache.org/jira/browse/CAMEL-15327)

Azure storage blob IT fails due unsupported mark/reset with FileInputStream that being introduced Azure SDK 12.7.0

[CAMEL-15326](https://issues.apache.org/jira/browse/CAMEL-15326)

camel-slack: incorrect handling of error responses

[CAMEL-15324](https://issues.apache.org/jira/browse/CAMEL-15324)

Camel-as2 can fail on jdk8 because of java.lang.NoSuchMethodError: java.nio.CharBuffer

[CAMEL-15316](https://issues.apache.org/jira/browse/CAMEL-15316)

Camel Zipkin does not set correct span kind

[CAMEL-15315](https://issues.apache.org/jira/browse/CAMEL-15315)

Camel-Pulsar: Error when verifying/creating namespace

[CAMEL-15311](https://issues.apache.org/jira/browse/CAMEL-15311)

DefaultTracer traceBeforeRoute not calling dumpTrace

[CAMEL-15307](https://issues.apache.org/jira/browse/CAMEL-15307)

camel-spring - Graceful shutdown is not working anymore

[CAMEL-15299](https://issues.apache.org/jira/browse/CAMEL-15299)

FTP endpoints will silently not delete/move file on disconnect

[CAMEL-15298](https://issues.apache.org/jira/browse/CAMEL-15298)

Camel-Spring-Boot: No CamelContext defined yet so cannot inject into bean: org.apache.camel.impl.health.DefaultHealthCheckRegistry

[CAMEL-15297](https://issues.apache.org/jira/browse/CAMEL-15297)

camel-pgevent - Issue with URI verification

[CAMEL-15285](https://issues.apache.org/jira/browse/CAMEL-15285)

Broken image / invalid anchors

[CAMEL-15282](https://issues.apache.org/jira/browse/CAMEL-15282)

Wrong validation error reported for uri with netty component using env placeholder

[CAMEL-15276](https://issues.apache.org/jira/browse/CAMEL-15276)

GeoLocationProvider may not get initialized properly

[CAMEL-15272](https://issues.apache.org/jira/browse/CAMEL-15272)

Camel-jira: JSONObject\["name"\] not found when connecting to latest JIRA/Jira-cloud

[CAMEL-15265](https://issues.apache.org/jira/browse/CAMEL-15265)

StaticEndpointBuilders - The static methods should be public

[CAMEL-15262](https://issues.apache.org/jira/browse/CAMEL-15262)

ZooKeeperCuratorHelper: wrong argument order when creating a new ExponentialBackoffRetry

[CAMEL-15260](https://issues.apache.org/jira/browse/CAMEL-15260)

OpenTracing - camel tracer appears not to activate spans in global tracer

[CAMEL-15251](https://issues.apache.org/jira/browse/CAMEL-15251)

camel-cdi - MandatoryJtaTransactionPolicy and NeverJtaTransactionPolicy miss to call the runnable work

[CAMEL-15245](https://issues.apache.org/jira/browse/CAMEL-15245)

On route shutdown timeout DefaultShutdownStrategy.forceShutdown remains set to true

[CAMEL-15239](https://issues.apache.org/jira/browse/CAMEL-15239)

camel-velocity header option does not conform to documentation

[CAMEL-15233](https://issues.apache.org/jira/browse/CAMEL-15233)

camel-salesforce - CometDReplayExtension does not keep replayId for each message/channel

[CAMEL-15230](https://issues.apache.org/jira/browse/CAMEL-15230)

RabbitMqSpanDecorator - Invalid Parent Span Id when EXCHANGE\_NAME header not set

[CAMEL-15229](https://issues.apache.org/jira/browse/CAMEL-15229)

autoDiscoverObjectMapper is not propagated to JacksonDataFormat

[CAMEL-15219](https://issues.apache.org/jira/browse/CAMEL-15219)

camel-cassandraql: cannot use a custom resultSetConversionStrategy

[CAMEL-15214](https://issues.apache.org/jira/browse/CAMEL-15214)

\[regression\]Duration values are no more part of the validation

[CAMEL-15199](https://issues.apache.org/jira/browse/CAMEL-15199)

RestDefinition relies on Class.getCanonicalName instead of Class.getName for in/out types

[CAMEL-15195](https://issues.apache.org/jira/browse/CAMEL-15195)

camel-netty - RequestTimeout seems not working as expected

[CAMEL-15187](https://issues.apache.org/jira/browse/CAMEL-15187)

jsonpath does not reset StreamCache on CBR predicate

[CAMEL-15149](https://issues.apache.org/jira/browse/CAMEL-15149)

Invalid UTF8 character in iec60870-server.json

[CAMEL-15148](https://issues.apache.org/jira/browse/CAMEL-15148)

camel-main - Fluent configuration of rest are not working

[CAMEL-15022](https://issues.apache.org/jira/browse/CAMEL-15022)

Opentracing doesn't work with Kafka Component

[CAMEL-15012](https://issues.apache.org/jira/browse/CAMEL-15012)

Camel-Http: Endpoint parameters proxyHost and proxyPort are ignored

[CAMEL-14854](https://issues.apache.org/jira/browse/CAMEL-14854)

Camel Irc components Fails to rejoin the channels

[CAMEL-14533](https://issues.apache.org/jira/browse/CAMEL-14533)

camel-ftp: fileExist=Append and tempPrefix options do not work together

[CAMEL-12971](https://issues.apache.org/jira/browse/CAMEL-12971)

SJMS Component javax.jms.JMSException: Unmatched acknowledge: MessageAck when transactionBatchTimeout expired

### Improvement (77)

[CAMEL-15481](https://issues.apache.org/jira/browse/CAMEL-15481)

camel-cluster - Should defer starting routes if quickly elected leading during startup

[CAMEL-15476](https://issues.apache.org/jira/browse/CAMEL-15476)

Camel-DJL: Upgrade to Deep Java Library 0.6.0

[CAMEL-15474](https://issues.apache.org/jira/browse/CAMEL-15474)

camel-api-component - Source code generator should include parameter documentation

[CAMEL-15447](https://issues.apache.org/jira/browse/CAMEL-15447)

contextPath ignored for platform-http with REST DSL

[CAMEL-15439](https://issues.apache.org/jira/browse/CAMEL-15439)

configurer: use full qualified class name instead of simple class name

[CAMEL-15438](https://issues.apache.org/jira/browse/CAMEL-15438)

properties-binding: support for dash style keys

[CAMEL-15437](https://issues.apache.org/jira/browse/CAMEL-15437)

properties-binding: support binding from maps of maps

[CAMEL-15431](https://issues.apache.org/jira/browse/CAMEL-15431)

Redundant array creation on log messages

[CAMEL-15422](https://issues.apache.org/jira/browse/CAMEL-15422)

ScheduledPollEndpoint - Scheduler option should be Object type and not String

[CAMEL-15418](https://issues.apache.org/jira/browse/CAMEL-15418)

Support for enriching the Swagger API Document

[CAMEL-15417](https://issues.apache.org/jira/browse/CAMEL-15417)

camel-cmis - Add optional "fileName" property on copyDocument function

[CAMEL-15415](https://issues.apache.org/jira/browse/CAMEL-15415)

Upgrade to spring boot 2.3.3

[CAMEL-15414](https://issues.apache.org/jira/browse/CAMEL-15414)

Upgrade to Kafka 2.5.1

[CAMEL-15413](https://issues.apache.org/jira/browse/CAMEL-15413)

RouteBuilderConfigurer - Rename to LambdaRouteBuilder

[CAMEL-15406](https://issues.apache.org/jira/browse/CAMEL-15406)

Configure EntityProvider write properties on camel-olingo2

[CAMEL-15405](https://issues.apache.org/jira/browse/CAMEL-15405)

Propagate inline count in Olingo2 component when using splitResults=true

[CAMEL-15398](https://issues.apache.org/jira/browse/CAMEL-15398)

Add documentation page about properties binding (via camel-main)

[CAMEL-15397](https://issues.apache.org/jira/browse/CAMEL-15397)

\[properties-binding\] support for array binding

[CAMEL-15396](https://issues.apache.org/jira/browse/CAMEL-15396)

\[properties-binding\] support for list binding with gaps

[CAMEL-15381](https://issues.apache.org/jira/browse/CAMEL-15381)

Avoid use of reflection in CronComponent

[CAMEL-15377](https://issues.apache.org/jira/browse/CAMEL-15377)

camel-jms - Add back transactedInOut option

[CAMEL-15376](https://issues.apache.org/jira/browse/CAMEL-15376)

camel-examples - We should do tags with released versions

[CAMEL-15365](https://issues.apache.org/jira/browse/CAMEL-15365)

Camel-Azure-\* components: add a configuration in case autoDiscovery need to be enabled

[CAMEL-15362](https://issues.apache.org/jira/browse/CAMEL-15362)

Make DefaultFluentProducerTemplate not thread safe for processors/endpoints

[CAMEL-15361](https://issues.apache.org/jira/browse/CAMEL-15361)

Use predictible doc page name for threadpoolfactory-vertx

[CAMEL-15357](https://issues.apache.org/jira/browse/CAMEL-15357)

Add example for Karaf to demonstrate how REST endpoint using servlet secured by Karaf JAAS service

[CAMEL-15353](https://issues.apache.org/jira/browse/CAMEL-15353)

Add CamelK as category to the component fixed set of known categories

[CAMEL-15351](https://issues.apache.org/jira/browse/CAMEL-15351)

camel-core - Events for camel context initializing/initialized should have their own event type

[CAMEL-15346](https://issues.apache.org/jira/browse/CAMEL-15346)

Let xml-io pass the namespace info to NamespaceAware elements

[CAMEL-15345](https://issues.apache.org/jira/browse/CAMEL-15345)

camel-twitter - Should validate that mandatory access token has been configured

[CAMEL-15342](https://issues.apache.org/jira/browse/CAMEL-15342)

Camel-azure-storage-queue: Add more configurations from headers configurations into component/endpoint configurations

[CAMEL-15331](https://issues.apache.org/jira/browse/CAMEL-15331)

Cassandraql: refactor tests to use testcontainers

[CAMEL-15328](https://issues.apache.org/jira/browse/CAMEL-15328)

Honor Optional http headers as method parameters to be null in camel-cxfrs producer

[CAMEL-15319](https://issues.apache.org/jira/browse/CAMEL-15319)

\[CAMEL-JIRA\] listen for events using atlassian-event library

[CAMEL-15313](https://issues.apache.org/jira/browse/CAMEL-15313)

camel-core - Parameterized RouteBuilder - add routes while starting the camel context

[CAMEL-15312](https://issues.apache.org/jira/browse/CAMEL-15312)

camel-core - Parameterized RouteBuilder - add support for life cycle handlers

[CAMEL-15310](https://issues.apache.org/jira/browse/CAMEL-15310)

AWS\* - Support for more than 1 client in the registry

[CAMEL-15303](https://issues.apache.org/jira/browse/CAMEL-15303)

Reduce log level for autodiscovered ObjectMapper

[CAMEL-15295](https://issues.apache.org/jira/browse/CAMEL-15295)

snapshot archetypes maven command is documentation does not work

[CAMEL-15293](https://issues.apache.org/jira/browse/CAMEL-15293)

Cassandraql: Upgrade datastax driver to 4.7.2 (from 3.7.2)

[CAMEL-15278](https://issues.apache.org/jira/browse/CAMEL-15278)

camel-bean: @Handler annotation does not work for proxied beans

[CAMEL-15277](https://issues.apache.org/jira/browse/CAMEL-15277)

OpenAPI Java extension cannot always handle non-default API context path

[CAMEL-15268](https://issues.apache.org/jira/browse/CAMEL-15268)

camel-main - ConfigurerClass allow to provide CamelContext as parameter

[CAMEL-15261](https://issues.apache.org/jira/browse/CAMEL-15261)

Handle Debezium configurations with regex

[CAMEL-15255](https://issues.apache.org/jira/browse/CAMEL-15255)

camel-micrometer- Extend set of metrics provided

[CAMEL-15248](https://issues.apache.org/jira/browse/CAMEL-15248)

Create ArangoDB camel component

[CAMEL-15247](https://issues.apache.org/jira/browse/CAMEL-15247)

RestConfiguration - Generate configurer to avoid reflection

[CAMEL-15246](https://issues.apache.org/jira/browse/CAMEL-15246)

website - Remove 3.3 from website

[CAMEL-15244](https://issues.apache.org/jira/browse/CAMEL-15244)

AggregationStrategy - default timeout method should be empty

[CAMEL-15242](https://issues.apache.org/jira/browse/CAMEL-15242)

camel-debezium - Upgrade to 1.2

[CAMEL-15237](https://issues.apache.org/jira/browse/CAMEL-15237)

PackageArchetypeCatalogMojo - Order in generated archetype-catalog

[CAMEL-15236](https://issues.apache.org/jira/browse/CAMEL-15236)

camel-package-maven-plugin - Regen may gen type as String instead of Long etc

[CAMEL-15235](https://issues.apache.org/jira/browse/CAMEL-15235)

Add support for Java 14

[CAMEL-15225](https://issues.apache.org/jira/browse/CAMEL-15225)

camel-api-component - Generate source code in src/generated

[CAMEL-15224](https://issues.apache.org/jira/browse/CAMEL-15224)

camel-api-component - Avoid reflection when configured nested configuration classes

[CAMEL-15223](https://issues.apache.org/jira/browse/CAMEL-15223)

camel-log - Avoid reflection for configuring DefaultExchangeFormatter

[CAMEL-15221](https://issues.apache.org/jira/browse/CAMEL-15221)

Camel-DJL: Upgrade to Deep Java Library 0.5.0

[CAMEL-15218](https://issues.apache.org/jira/browse/CAMEL-15218)

camel-catalog - Store generated files in git

[CAMEL-15217](https://issues.apache.org/jira/browse/CAMEL-15217)

bean(Bean.class) should lookup the registry by type

[CAMEL-15213](https://issues.apache.org/jira/browse/CAMEL-15213)

camel-main - Add default values to configuration so tooling knows

[CAMEL-15210](https://issues.apache.org/jira/browse/CAMEL-15210)

camel-api-component-maven-plugin - Should generate test code in junit 5 format

[CAMEL-15209](https://issues.apache.org/jira/browse/CAMEL-15209)

camel-jaxb - Should depend on camel-xml-jaxb

[CAMEL-15208](https://issues.apache.org/jira/browse/CAMEL-15208)

camel-component-maven-plugin - Jandex must be generated first

[CAMEL-15198](https://issues.apache.org/jira/browse/CAMEL-15198)

Camel-azure-storage-blob: Add more configurations from headers configurations into component/endpoint configurations

[CAMEL-15193](https://issues.apache.org/jira/browse/CAMEL-15193)

camel-file-starter - Add back auto configuration for file cluster service

[CAMEL-15190](https://issues.apache.org/jira/browse/CAMEL-15190)

camel-main - Generate table in docs with all its configuration options

[CAMEL-15188](https://issues.apache.org/jira/browse/CAMEL-15188)

camel-telegram - Add SOCKS proxy support to telegram component

[CAMEL-15184](https://issues.apache.org/jira/browse/CAMEL-15184)

PackageScan.findImplementation - Should filter out abstract classes

[CAMEL-15160](https://issues.apache.org/jira/browse/CAMEL-15160)

Configurer - Generate details what type Map/List contains

[CAMEL-15124](https://issues.apache.org/jira/browse/CAMEL-15124)

error-handler-builder: allow to reference processors by name

[CAMEL-15119](https://issues.apache.org/jira/browse/CAMEL-15119)

Do not use reflection when configuring subclasses of AbstractApiComponent

[CAMEL-15113](https://issues.apache.org/jira/browse/CAMEL-15113)

camel-rabbitmq - Auto declare dead letter queues with custom args

[CAMEL-15102](https://issues.apache.org/jira/browse/CAMEL-15102)

camel-karaf-examples - Move examples for osgi/karaf to its own git repo

[CAMEL-15074](https://issues.apache.org/jira/browse/CAMEL-15074)

Camel website - Add easy to find links for examples for each sub project

[CAMEL-14622](https://issues.apache.org/jira/browse/CAMEL-14622)

camel component options - Favour annotation based options

[CAMEL-14578](https://issues.apache.org/jira/browse/CAMEL-14578)

Reformat files at build time to force compliance with code standards

[CAMEL-11807](https://issues.apache.org/jira/browse/CAMEL-11807)

Upgrade to JUnit 5

### New Feature (40)

[CAMEL-15469](https://issues.apache.org/jira/browse/CAMEL-15469)

AggregationStrategy using etcd3 as datastore

[CAMEL-15468](https://issues.apache.org/jira/browse/CAMEL-15468)

AggregationStrategy using redis as datastore

[CAMEL-15452](https://issues.apache.org/jira/browse/CAMEL-15452)

PropertyBindingSupport - Add reflection on|off option

[CAMEL-15448](https://issues.apache.org/jira/browse/CAMEL-15448)

Add tag and correlation context support for Opentelemetry

[CAMEL-15442](https://issues.apache.org/jira/browse/CAMEL-15442)

ArangoDb - backport new parameters to camel-spring-boot starter

[CAMEL-15429](https://issues.apache.org/jira/browse/CAMEL-15429)

Add Spring Boot Starter for camel-oaipmh

[CAMEL-15428](https://issues.apache.org/jira/browse/CAMEL-15428)

Create a proper camel BOM (for camel-spring-boot)

[CAMEL-15427](https://issues.apache.org/jira/browse/CAMEL-15427)

Add examples featuring Azure Eventhubs and Azure Blob

[CAMEL-15411](https://issues.apache.org/jira/browse/CAMEL-15411)

Add example for camel-oaipmh

[CAMEL-15409](https://issues.apache.org/jira/browse/CAMEL-15409)

ArangoDb - add operations on graphs in the producer

[CAMEL-15408](https://issues.apache.org/jira/browse/CAMEL-15408)

spring boot starter for oai-pmh component

[CAMEL-15386](https://issues.apache.org/jira/browse/CAMEL-15386)

Camel-Opentelemetry and Camel-opentracing: Semantic conventions are going to diverge

[CAMEL-15385](https://issues.apache.org/jira/browse/CAMEL-15385)

camel-main - Properties ordering should use #class: first

[CAMEL-15384](https://issues.apache.org/jira/browse/CAMEL-15384)

camel-http - Allow to configure http proxy on component level

[CAMEL-15380](https://issues.apache.org/jira/browse/CAMEL-15380)

Camel-aws2-s3: moveAfterRead define prefix or suffix

[CAMEL-15356](https://issues.apache.org/jira/browse/CAMEL-15356)

Create camel-azure-eventhub to integrate with Azure Event Hub service

[CAMEL-15352](https://issues.apache.org/jira/browse/CAMEL-15352)

Camel-AWS2-SQS: Add support for purgequeue operation

[CAMEL-15339](https://issues.apache.org/jira/browse/CAMEL-15339)

OpenTelementry component

[CAMEL-15308](https://issues.apache.org/jira/browse/CAMEL-15308)

RouteTemplate SPI for parameter sources

[CAMEL-15292](https://issues.apache.org/jira/browse/CAMEL-15292)

Camel-AWS2-S3: Support SSE-C on the consumer's side

[CAMEL-15283](https://issues.apache.org/jira/browse/CAMEL-15283)

Create a vertx web client component

[CAMEL-15280](https://issues.apache.org/jira/browse/CAMEL-15280)

Camel-AWS2-\*: Add the ability to trust all certificates when overidding the endpoint

[CAMEL-15274](https://issues.apache.org/jira/browse/CAMEL-15274)

camel-spring-boot - Add back http endpoint for route information

[CAMEL-15270](https://issues.apache.org/jira/browse/CAMEL-15270)

camel-main - Allow to create routes from route template via configuration properties

[CAMEL-15267](https://issues.apache.org/jira/browse/CAMEL-15267)

Add a ByteArrayOutputStream to ByteBuffer converter in core

[CAMEL-15264](https://issues.apache.org/jira/browse/CAMEL-15264)

Camel-AWS2-Kinesis: Add more operations support

[CAMEL-15257](https://issues.apache.org/jira/browse/CAMEL-15257)

camel jsonata integration

[CAMEL-15253](https://issues.apache.org/jira/browse/CAMEL-15253)

OAI-PMH Component

[CAMEL-15231](https://issues.apache.org/jira/browse/CAMEL-15231)

Support topic patterns in Pulsar when subscribing

[CAMEL-15228](https://issues.apache.org/jira/browse/CAMEL-15228)

camel-kafka - Missing end of polling signal in Processors

[CAMEL-15197](https://issues.apache.org/jira/browse/CAMEL-15197)

Thread pools in EIPs allow to use vertx thread pool instead

[CAMEL-15196](https://issues.apache.org/jira/browse/CAMEL-15196)

Add support for OpenTracing tags

[CAMEL-15186](https://issues.apache.org/jira/browse/CAMEL-15186)

Add support for Workday Common REST API.

[CAMEL-15170](https://issues.apache.org/jira/browse/CAMEL-15170)

camel-jt400 - IBM i \*MSGQ support

[CAMEL-14974](https://issues.apache.org/jira/browse/CAMEL-14974)

Java 14 Support

[CAMEL-14963](https://issues.apache.org/jira/browse/CAMEL-14963)

camel-core - Parameterized RouteBuilder

[CAMEL-14956](https://issues.apache.org/jira/browse/CAMEL-14956)

Create a websocket component based on Vertx

[CAMEL-14297](https://issues.apache.org/jira/browse/CAMEL-14297)

Introduce RouteBuilderConfigurer

[CAMEL-13934](https://issues.apache.org/jira/browse/CAMEL-13934)

camel-minio - Component to store/load files from blob store

[CAMEL-11547](https://issues.apache.org/jira/browse/CAMEL-11547)

camel-core: load route definitions from registry

### Task (48)

[CAMEL-15467](https://issues.apache.org/jira/browse/CAMEL-15467)

camel-cdi - Tests fails on JDK14

[CAMEL-15466](https://issues.apache.org/jira/browse/CAMEL-15466)

Create Karaf feature for Camel Azure Eventhubs component

[CAMEL-15463](https://issues.apache.org/jira/browse/CAMEL-15463)

Upgrade Jakarta JAXB to 2.3.3

[CAMEL-15461](https://issues.apache.org/jira/browse/CAMEL-15461)

Upgrade to jedis bundle 3.3.0\_2

[CAMEL-15459](https://issues.apache.org/jira/browse/CAMEL-15459)

update to CXF 3.4.0

[CAMEL-15458](https://issues.apache.org/jira/browse/CAMEL-15458)

spring-boot-starter should generate list of starters in the doc same way as camel-core

[CAMEL-15453](https://issues.apache.org/jira/browse/CAMEL-15453)

camel-jdbc: replacing deprecated code leads to test failures

[CAMEL-15444](https://issues.apache.org/jira/browse/CAMEL-15444)

Incorrect order for test assertions

[CAMEL-15441](https://issues.apache.org/jira/browse/CAMEL-15441)

Upgrade spring-data bundles version to 2.3.x in features repositorry

[CAMEL-15440](https://issues.apache.org/jira/browse/CAMEL-15440)

Use elasticsearch unique bundle (not client anymore)

[CAMEL-15393](https://issues.apache.org/jira/browse/CAMEL-15393)

camel-spring-javaconfig - Deprecate

[CAMEL-15390](https://issues.apache.org/jira/browse/CAMEL-15390)

CollectionStringBuilder - Use JDK util methods instead

[CAMEL-15389](https://issues.apache.org/jira/browse/CAMEL-15389)

camel-main - Add docs about camel.beans

[CAMEL-15379](https://issues.apache.org/jira/browse/CAMEL-15379)

camel-example-cdi - Some cdi examples fail tests

[CAMEL-15374](https://issues.apache.org/jira/browse/CAMEL-15374)

Camel-AWS2-STS: Add more operation to the producer

[CAMEL-15373](https://issues.apache.org/jira/browse/CAMEL-15373)

Create an AWS2-STS component

[CAMEL-15368](https://issues.apache.org/jira/browse/CAMEL-15368)

Camel-Main: Support raw syntax or being able to detect secret

[CAMEL-15359](https://issues.apache.org/jira/browse/CAMEL-15359)

Camel-Opentelemetry: Documentation is missing

[CAMEL-15354](https://issues.apache.org/jira/browse/CAMEL-15354)

camel-opentracing - Go back to 0.31.0 API of MP opentracing

[CAMEL-15334](https://issues.apache.org/jira/browse/CAMEL-15334)

Camel-CassandraQL Spring Boot integration test is failing after upgrade to Cassandra driver 4.x

[CAMEL-15330](https://issues.apache.org/jira/browse/CAMEL-15330)

Create Spring Boot starter for camel-vertx-http

[CAMEL-15322](https://issues.apache.org/jira/browse/CAMEL-15322)

CI Server: Migrate to https://ci-builds.apache.org from https://builds.apache.org

[CAMEL-15318](https://issues.apache.org/jira/browse/CAMEL-15318)

Deprecate the legacy Azure components

[CAMEL-15314](https://issues.apache.org/jira/browse/CAMEL-15314)

camel-endpointdsl - StaticEndpointBuilders - may loose public

[CAMEL-15309](https://issues.apache.org/jira/browse/CAMEL-15309)

Camel 3.4.1 was built with JDK 11 - Use BufferCaster everywhere

[CAMEL-15306](https://issues.apache.org/jira/browse/CAMEL-15306)

camel-jpa: example in documentation links to a web page that doesn't exist

[CAMEL-15305](https://issues.apache.org/jira/browse/CAMEL-15305)

Camel-ArangoDB: Create a Spring Boot starter

[CAMEL-15304](https://issues.apache.org/jira/browse/CAMEL-15304)

Camel-ArangoDB: Create a Karaf feature

[CAMEL-15284](https://issues.apache.org/jira/browse/CAMEL-15284)

Fix Maven build on Windows

[CAMEL-15271](https://issues.apache.org/jira/browse/CAMEL-15271)

Add example back in doc about stop aroute

[CAMEL-15266](https://issues.apache.org/jira/browse/CAMEL-15266)

camel-website - Contributing guide cleanup

[CAMEL-15259](https://issues.apache.org/jira/browse/CAMEL-15259)

camel-couchbase seems outdated or broken

[CAMEL-15258](https://issues.apache.org/jira/browse/CAMEL-15258)

Remove camel-reactive-executor-vertx-starter

[CAMEL-15241](https://issues.apache.org/jira/browse/CAMEL-15241)

Remove karaf feature for camel-couchbase

[CAMEL-15240](https://issues.apache.org/jira/browse/CAMEL-15240)

Camel-Velocity: Deprecation warnings

[CAMEL-15216](https://issues.apache.org/jira/browse/CAMEL-15216)

camel-website - Fix small adoc WARNs

[CAMEL-15215](https://issues.apache.org/jira/browse/CAMEL-15215)

Simplify and homogenize spring testing

[CAMEL-15205](https://issues.apache.org/jira/browse/CAMEL-15205)

camel-quartz documentation for Cron is incorrect

[CAMEL-15204](https://issues.apache.org/jira/browse/CAMEL-15204)

Need to fix terminology within JT400 component

[CAMEL-15192](https://issues.apache.org/jira/browse/CAMEL-15192)

AWS2-Kinesis-Firehose: Support creation of deliveryStream

[CAMEL-15191](https://issues.apache.org/jira/browse/CAMEL-15191)

AWS2-Kinesis-Firehose: Support for RecordBatchRequest

[CAMEL-15173](https://issues.apache.org/jira/browse/CAMEL-15173)

Example code missing in several pages

[CAMEL-14918](https://issues.apache.org/jira/browse/CAMEL-14918)

camel-cdi - Avoid @Resource injection

[CAMEL-14777](https://issues.apache.org/jira/browse/CAMEL-14777)

Replace EmbeddedEngine with the new Debezium APIs

[CAMEL-14565](https://issues.apache.org/jira/browse/CAMEL-14565)

camel-spring-boot - Some auto configuration options has no descriptions

[CAMEL-14319](https://issues.apache.org/jira/browse/CAMEL-14319)

Camel-Couchbase: Update client to 3.x

[CAMEL-14317](https://issues.apache.org/jira/browse/CAMEL-14317)

Remove log4j v1

[CAMEL-12336](https://issues.apache.org/jira/browse/CAMEL-12336)

speedup tests in tests/camel-itests

### Test (6)

[CAMEL-15477](https://issues.apache.org/jira/browse/CAMEL-15477)

Camel-Minio: Review how to run integration tests

[CAMEL-15470](https://issues.apache.org/jira/browse/CAMEL-15470)

Camel-Crypto-CMS: The sign endpoint tests are failing

[CAMEL-15464](https://issues.apache.org/jira/browse/CAMEL-15464)

FTP tests are failing on CI Server

[CAMEL-15451](https://issues.apache.org/jira/browse/CAMEL-15451)

camel-aws2-s3 - Test errors running local tests

[CAMEL-15403](https://issues.apache.org/jira/browse/CAMEL-15403)

camel-xmlsecurity - Some unit tests fails with Oracle JDK8 261

[CAMEL-14826](https://issues.apache.org/jira/browse/CAMEL-14826)

Add unit tests to the platform-http component

### Wish (2)

[CAMEL-15479](https://issues.apache.org/jira/browse/CAMEL-15479)

Clear up purpose of spring-boot and camel-spring-boot-starter

[CAMEL-15340](https://issues.apache.org/jira/browse/CAMEL-15340)

create kubernetes job example

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).