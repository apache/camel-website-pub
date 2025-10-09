# Apache camel 3.8.0 Release

## New and Noteworthy

This release is the new Camel 3.8.0 minor release.

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
      <version>3.8.0</version>
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
      <version>3.8.0</version>
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
| [apache-camel-3.8.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.8.0/apache-camel-3.8.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.8.0/apache-camel-3.8.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.8.0/apache-camel-3.8.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.8.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.8.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (55)

[CAMEL-16177](https://issues.apache.org/jira/browse/CAMEL-16177)

File stream cache problem with multicast parallel processing and encrypted stream

[CAMEL-16161](https://issues.apache.org/jira/browse/CAMEL-16161)

camel-core - Route template does not support autoStartup

[CAMEL-16152](https://issues.apache.org/jira/browse/CAMEL-16152)

XML DSL tokenize with token in simple language and group does not set the delimiter correctly

[CAMEL-16145](https://issues.apache.org/jira/browse/CAMEL-16145)

camel-report-maven-plugin: coverageThreshold cannot be set

[CAMEL-16135](https://issues.apache.org/jira/browse/CAMEL-16135)

Exception on routeinitialization when using split in onException-Block

[CAMEL-16114](https://issues.apache.org/jira/browse/CAMEL-16114)

DataFormat UnmarshalType defined as an Array Class Fails in Java DSL

[CAMEL-16112](https://issues.apache.org/jira/browse/CAMEL-16112)

Camel REST deserializes response to wrong type

[CAMEL-16111](https://issues.apache.org/jira/browse/CAMEL-16111)

camel-spring-boot - Bean reference by name in properties not working when there are custom property converters

[CAMEL-16110](https://issues.apache.org/jira/browse/CAMEL-16110)

camel-cxfrs - CxfRsProducer leaks Header when Exchange.HTTP\_QUERY is set

[CAMEL-16109](https://issues.apache.org/jira/browse/CAMEL-16109)

camel-hystrix-starter auto-config fails with multiple "servletRegistrationBean"

[CAMEL-16104](https://issues.apache.org/jira/browse/CAMEL-16104)

ProducerCache does not close producers when cacheSize is 1 (potential memory leak)

[CAMEL-16103](https://issues.apache.org/jira/browse/CAMEL-16103)

Stack size increases in split with transacted

[CAMEL-16092](https://issues.apache.org/jira/browse/CAMEL-16092)

Azure Storage Queue can not delete received message after Azure Storage Blob consume

[CAMEL-16091](https://issues.apache.org/jira/browse/CAMEL-16091)

Using netty-http with enricher causes buffer leak

[CAMEL-16086](https://issues.apache.org/jira/browse/CAMEL-16086)

camel-salesforce - CompositeApiProcessor requires too many fields in RAW mode

[CAMEL-16084](https://issues.apache.org/jira/browse/CAMEL-16084)

salesforce: Out of order execution

[CAMEL-16083](https://issues.apache.org/jira/browse/CAMEL-16083)

OnCompletion with After Consumer mode does not fire if defined in routeScope

[CAMEL-16082](https://issues.apache.org/jira/browse/CAMEL-16082)

Single choice() without otherwise() always executed

[CAMEL-16077](https://issues.apache.org/jira/browse/CAMEL-16077)

camel-undertow - not respect content-type specified by REST DSL produces when body returns null

[CAMEL-16068](https://issues.apache.org/jira/browse/CAMEL-16068)

Camel-AWS2-S3: Fix condition for throwing exception in case bucket does not exist

[CAMEL-16065](https://issues.apache.org/jira/browse/CAMEL-16065)

Camel Undertow Starter causes configuration issues with DirtiesContext

[CAMEL-16045](https://issues.apache.org/jira/browse/CAMEL-16045)

rest-dsl - xml or json binding should create new instance of data formats

[CAMEL-16043](https://issues.apache.org/jira/browse/CAMEL-16043)

\[camel-kafka\] additionalProperties option on endpoint level is broken

[CAMEL-16040](https://issues.apache.org/jira/browse/CAMEL-16040)

JAXB error Generating Swagger in Karaf

[CAMEL-16037](https://issues.apache.org/jira/browse/CAMEL-16037)

Minio: if autowiredEnabled is set to false on camelContext, minioClient is still autowired

[CAMEL-16035](https://issues.apache.org/jira/browse/CAMEL-16035)

HazelcastQueueConsumer : when using mode POLL, the consumer sends NULL

[CAMEL-16034](https://issues.apache.org/jira/browse/CAMEL-16034)

MDC Logging causing OutOfMemory with large split

[CAMEL-16032](https://issues.apache.org/jira/browse/CAMEL-16032)

\[camel-main\] autoconfiguration does not bind dataformat in the registry

[CAMEL-16018](https://issues.apache.org/jira/browse/CAMEL-16018)

HazelcastReplicatedConsumer not receiving events

[CAMEL-16016](https://issues.apache.org/jira/browse/CAMEL-16016)

Encoding special characters via UnsafeUriCharactersEncoder does not work in all cases

[CAMEL-16014](https://issues.apache.org/jira/browse/CAMEL-16014)

camel-test-infra-artemis: Invalid AMQP endpoint

[CAMEL-16009](https://issues.apache.org/jira/browse/CAMEL-16009)

OPC/UA Tree contains two nodes "Camel" that is incorrect

[CAMEL-16005](https://issues.apache.org/jira/browse/CAMEL-16005)

Route built from template with parallel processing recipient list fails to start because of duplicate node id.

[CAMEL-16000](https://issues.apache.org/jira/browse/CAMEL-16000)

Type converter regression in Camel 3.7.0

[CAMEL-15999](https://issues.apache.org/jira/browse/CAMEL-15999)

Camel-spring-boot: Property not found after upgrading to 3.7.0 when using camel-caffeine-starter

[CAMEL-15985](https://issues.apache.org/jira/browse/CAMEL-15985)

camel-jms - toD under heavy load can cause NPE when connection factory configured on JMS component level

[CAMEL-15983](https://issues.apache.org/jira/browse/CAMEL-15983)

URISupport have an bug in method doFastNormalizeUri for normalize EndpointKey

[CAMEL-15974](https://issues.apache.org/jira/browse/CAMEL-15974)

HttpSendDynamicAware doesn't resolve RAW properties

[CAMEL-15971](https://issues.apache.org/jira/browse/CAMEL-15971)

SimpleFileLanguage always null due to DummyExchange

[CAMEL-15949](https://issues.apache.org/jira/browse/CAMEL-15949)

Incorrect value getSupportExtendedInformation for ManagedPollEnricher

[CAMEL-15947](https://issues.apache.org/jira/browse/CAMEL-15947)

Hazelcast : client mode : search hazelcast client by name doesn't work

[CAMEL-15945](https://issues.apache.org/jira/browse/CAMEL-15945)

Don't require sObjectName or sObjectClass when streaming with raw payload

[CAMEL-15942](https://issues.apache.org/jira/browse/CAMEL-15942)

spring xml on camel-spring-boot may add route policy factory twice

[CAMEL-15940](https://issues.apache.org/jira/browse/CAMEL-15940)

camel-spring-boot - Issue with property placeholder in an example

[CAMEL-15937](https://issues.apache.org/jira/browse/CAMEL-15937)

camel-netty - WARN logging with disconnect=true

[CAMEL-15930](https://issues.apache.org/jira/browse/CAMEL-15930)

ClusteredRouteController cannot start clustered routes

[CAMEL-15928](https://issues.apache.org/jira/browse/CAMEL-15928)

TimeoutException does not trigger Resilience4j circuit breaker

[CAMEL-15522](https://issues.apache.org/jira/browse/CAMEL-15522)

AWS Xray Component issue

[CAMEL-15290](https://issues.apache.org/jira/browse/CAMEL-15290)

camel-cxfrs - CxfRsProducer leaks Header when Exchange.HTTP\_METHOD is set

[CAMEL-14138](https://issues.apache.org/jira/browse/CAMEL-14138)

Salesforce: a synchronous call that follow an asynchronous call will always result in a TimeoutException

[CAMEL-13553](https://issues.apache.org/jira/browse/CAMEL-13553)

OnCompletion behaves strange in combination with direct subroutes

[CAMEL-13443](https://issues.apache.org/jira/browse/CAMEL-13443)

Camel Blueprint JUnit Test keeps Filelock after Test

[CAMEL-13024](https://issues.apache.org/jira/browse/CAMEL-13024)

Camel-Mail breaks some attachment names with many special characters

[CAMEL-12871](https://issues.apache.org/jira/browse/CAMEL-12871)

Camel-salesforce component drops the streaming topic

[CAMEL-12428](https://issues.apache.org/jira/browse/CAMEL-12428)

Cannot use Camel exchange headers in Processor with cxf-rs

### Improvement (56)

[CAMEL-16436](https://issues.apache.org/jira/browse/CAMEL-16436)

SMN component-support custom service endpoint

[CAMEL-16181](https://issues.apache.org/jira/browse/CAMEL-16181)

KafkaIdempotentRepository cache incorrectly flagged as ready

[CAMEL-16163](https://issues.apache.org/jira/browse/CAMEL-16163)

camel-core - Routes loader to be a static service

[CAMEL-16160](https://issues.apache.org/jira/browse/CAMEL-16160)

camel-main - JVM system properties should override application.properties

[CAMEL-16154](https://issues.apache.org/jira/browse/CAMEL-16154)

@InvokeOnHeader - Improve parameter mapping to generated code

[CAMEL-16146](https://issues.apache.org/jira/browse/CAMEL-16146)

camel-core - Sensitive keys should handle different cases

[CAMEL-16142](https://issues.apache.org/jira/browse/CAMEL-16142)

Enable PubNub client to be autowired

[CAMEL-16138](https://issues.apache.org/jira/browse/CAMEL-16138)

Allow KafkaClientFactory to be used without explicit broker URLs

[CAMEL-16136](https://issues.apache.org/jira/browse/CAMEL-16136)

core: replace BaseServiceResolver with a static method

[CAMEL-16129](https://issues.apache.org/jira/browse/CAMEL-16129)

Avoid property binding via reflection in NettyConfiguration

[CAMEL-16127](https://issues.apache.org/jira/browse/CAMEL-16127)

Revisit PackageScanResourceResolver

[CAMEL-16126](https://issues.apache.org/jira/browse/CAMEL-16126)

camel-core - errorHandler(ref) to make it easier to specify error handler by refernce

[CAMEL-16120](https://issues.apache.org/jira/browse/CAMEL-16120)

Upgrade resilience4j to 1.7.x

[CAMEL-16118](https://issues.apache.org/jira/browse/CAMEL-16118)

camel-core - Json dataformats with json view should be configurable from XML DSL

[CAMEL-16106](https://issues.apache.org/jira/browse/CAMEL-16106)

camel-seda - Endpoints with custom queueSize to create queue lazy

[CAMEL-16102](https://issues.apache.org/jira/browse/CAMEL-16102)

camel components - Optimize components using @InvokeOnHeader to avoid reflection

[CAMEL-16096](https://issues.apache.org/jira/browse/CAMEL-16096)

camel-spring-boot - Autoconfiguration to support #class or #type syntax

[CAMEL-16095](https://issues.apache.org/jira/browse/CAMEL-16095)

Update camel-ssh to work with both SSHD 1.x and 2.x

[CAMEL-16094](https://issues.apache.org/jira/browse/CAMEL-16094)

camel-milo - Add ConnectionFactory SPI

[CAMEL-16093](https://issues.apache.org/jira/browse/CAMEL-16093)

camel-caffeine-lrucache - Deprecate and move out of core

[CAMEL-16081](https://issues.apache.org/jira/browse/CAMEL-16081)

camel-main - Defining beans creating new instances should avoid reflection

[CAMEL-16076](https://issues.apache.org/jira/browse/CAMEL-16076)

camel-core - Supervised route controller - better activity logging

[CAMEL-16075](https://issues.apache.org/jira/browse/CAMEL-16075)

camel-main - Add option to turn off auto configuration summary

[CAMEL-16074](https://issues.apache.org/jira/browse/CAMEL-16074)

camel-flight-recorder - Add option to filter on duration

[CAMEL-16072](https://issues.apache.org/jira/browse/CAMEL-16072)

camel-core - Nicer summary of total routes started in the log

[CAMEL-16071](https://issues.apache.org/jira/browse/CAMEL-16071)

Support custom Kafka client instances

[CAMEL-16070](https://issues.apache.org/jira/browse/CAMEL-16070)

camel-core - CamelContext should not be allowed to restart

[CAMEL-16066](https://issues.apache.org/jira/browse/CAMEL-16066)

camel-core - Add static methods for language expressions in Builder to use for Lambda DSL

[CAMEL-16061](https://issues.apache.org/jira/browse/CAMEL-16061)

JSLT-Component: Object-Mapper changes large Decimal-Numbers (to scientific notation)

[CAMEL-16057](https://issues.apache.org/jira/browse/CAMEL-16057)

camel-core - Fine grained event notifier for lifecycle of services

[CAMEL-16055](https://issues.apache.org/jira/browse/CAMEL-16055)

Camel Spring Boot BOM prevents performing release

[CAMEL-16052](https://issues.apache.org/jira/browse/CAMEL-16052)

camel-jslt - Allow to configure custom ObjectMapper

[CAMEL-16051](https://issues.apache.org/jira/browse/CAMEL-16051)

camel-spring-rabbitmq: Add usePublisherConnection option

[CAMEL-16049](https://issues.apache.org/jira/browse/CAMEL-16049)

camel-json-validator: Reuse Jackson ObjectMapper

[CAMEL-16042](https://issues.apache.org/jira/browse/CAMEL-16042)

Upgrade to Spring Boot 2.4.2

[CAMEL-16022](https://issues.apache.org/jira/browse/CAMEL-16022)

Add message ordering to Google Pubsub

[CAMEL-16020](https://issues.apache.org/jira/browse/CAMEL-16020)

Component - Remove general synchronous option

[CAMEL-16010](https://issues.apache.org/jira/browse/CAMEL-16010)

Extend import version range for pax-logging 2.x on camel-paxlogging

[CAMEL-16004](https://issues.apache.org/jira/browse/CAMEL-16004)

camel-fhir: Port the test to camel-test-infra

[CAMEL-16003](https://issues.apache.org/jira/browse/CAMEL-16003)

camel-rabbitmq - Rework component using spring-rabbitmq

[CAMEL-15998](https://issues.apache.org/jira/browse/CAMEL-15998)

Camel-Github: Better structure for consumer returned object

[CAMEL-15987](https://issues.apache.org/jira/browse/CAMEL-15987)

camel-sjms - camel-jms - Add support for DynamicAware endpoints for toD

[CAMEL-15986](https://issues.apache.org/jira/browse/CAMEL-15986)

camel-core - DynamicAware need to support component alias

[CAMEL-15984](https://issues.apache.org/jira/browse/CAMEL-15984)

camel-jms - Add support for DynamicAware endpoints for toD (take 2)

[CAMEL-15973](https://issues.apache.org/jira/browse/CAMEL-15973)

Camel-AWS2-SQS: Set the queue policy as file and not as plain String

[CAMEL-15969](https://issues.apache.org/jira/browse/CAMEL-15969)

Camel-AWS2-SNS: Set the topic policy as file and not as plain String

[CAMEL-15961](https://issues.apache.org/jira/browse/CAMEL-15961)

Calendar Stream component: implement proper synchonization

[CAMEL-15950](https://issues.apache.org/jira/browse/CAMEL-15950)

JMX data for processors - Expression/ExpressionLanguage

[CAMEL-15938](https://issues.apache.org/jira/browse/CAMEL-15938)

Catalog contains wrong "required" for aws2-iam "operation"

[CAMEL-15844](https://issues.apache.org/jira/browse/CAMEL-15844)

camel-core - RouteReifier createRoute move to earlier phase

[CAMEL-15759](https://issues.apache.org/jira/browse/CAMEL-15759)

Remove runtime camel-catalog from SendDynamicAware

[CAMEL-15578](https://issues.apache.org/jira/browse/CAMEL-15578)

Loop EIP - Add option to break out if shutting down Camel

[CAMEL-15529](https://issues.apache.org/jira/browse/CAMEL-15529)

camel-karaf - Features should use range for inner features repos

[CAMEL-15106](https://issues.apache.org/jira/browse/CAMEL-15106)

KafkaConsumer: Support Suspend & Resume

[CAMEL-13441](https://issues.apache.org/jira/browse/CAMEL-13441)

Dependency geronimo-jms\_2.0\_spec version 1.0-alpha-2 should be upgraded

[CAMEL-12808](https://issues.apache.org/jira/browse/CAMEL-12808)

Add support for PK Chunking in Salesforce Bulk API

### New Feature (29)

[CAMEL-16168](https://issues.apache.org/jira/browse/CAMEL-16168)

camel-oaipmh: Replace the JettyTestServer with wiremock

[CAMEL-16159](https://issues.apache.org/jira/browse/CAMEL-16159)

Add support for nats requests

[CAMEL-16108](https://issues.apache.org/jira/browse/CAMEL-16108)

camel-aws-s3 - Pass the value of \`GetObjectResponse::metadata\` as an Exchange Header

[CAMEL-16098](https://issues.apache.org/jira/browse/CAMEL-16098)

camel-direct - Add synchronous option

[CAMEL-16056](https://issues.apache.org/jira/browse/CAMEL-16056)

camel-jfr - Java Flight Recorder Event Notifier

[CAMEL-16050](https://issues.apache.org/jira/browse/CAMEL-16050)

camel-sjms - Add PollingConsumer

[CAMEL-16048](https://issues.apache.org/jira/browse/CAMEL-16048)

camel-spring-rabbit - PollingConsumer to receive one message on-demand

[CAMEL-16029](https://issues.apache.org/jira/browse/CAMEL-16029)

camel-core - Log on startup if multiple instances of same component are in use

[CAMEL-16021](https://issues.apache.org/jira/browse/CAMEL-16021)

Components - Add option to turn on|off autowiring per component

[CAMEL-16019](https://issues.apache.org/jira/browse/CAMEL-16019)

Create another Camel Paho component for MQTT 5 support

[CAMEL-16008](https://issues.apache.org/jira/browse/CAMEL-16008)

ActiveMQ/Artemis - Implement consumer priority in camel

[CAMEL-16001](https://issues.apache.org/jira/browse/CAMEL-16001)

Camel component // Huawei Cloud Simple Notification Services (SMN)

[CAMEL-15997](https://issues.apache.org/jira/browse/CAMEL-15997)

camel-redis: Port the test to camel-test-infra

[CAMEL-15995](https://issues.apache.org/jira/browse/CAMEL-15995)

camel-sjms - Make it more feature compatible with camel-jms

[CAMEL-15993](https://issues.apache.org/jira/browse/CAMEL-15993)

camel-amqp - Add support for DynamicAware endpoints for toD

[CAMEL-15992](https://issues.apache.org/jira/browse/CAMEL-15992)

camel-paho - Add support for DynamicAware endpoints for toD

[CAMEL-15991](https://issues.apache.org/jira/browse/CAMEL-15991)

camel-rabbitmq - Add support for DynamicAware endpoints for toD

[CAMEL-15990](https://issues.apache.org/jira/browse/CAMEL-15990)

camel-sjms - Support regular connection pool

[CAMEL-15989](https://issues.apache.org/jira/browse/CAMEL-15989)

camel-kafka - Add support for DynamicAware endpoints for toD

[CAMEL-15988](https://issues.apache.org/jira/browse/CAMEL-15988)

camel-sjms - producer Add support for override header with dynamic destination name

[CAMEL-15979](https://issues.apache.org/jira/browse/CAMEL-15979)

camel-file - Add includeExt/excludeExt to make it easy to filter based on file extension

[CAMEL-15959](https://issues.apache.org/jira/browse/CAMEL-15959)

Calendar Stream component - support for Google Service account

[CAMEL-15933](https://issues.apache.org/jira/browse/CAMEL-15933)

Create camel-stitch component to produce data to Stitch ETL platform

[CAMEL-15560](https://issues.apache.org/jira/browse/CAMEL-15560)

generic route loader

[CAMEL-15428](https://issues.apache.org/jira/browse/CAMEL-15428)

Create a proper camel BOM (for camel-spring-boot)

[CAMEL-15341](https://issues.apache.org/jira/browse/CAMEL-15341)

Create camel-azure-storage-datalake to serve Azure DataLakes Gen2

[CAMEL-14871](https://issues.apache.org/jira/browse/CAMEL-14871)

camel-aws-s3 - Support the \`doneFileName\` option

[CAMEL-13455](https://issues.apache.org/jira/browse/CAMEL-13455)

Requesting to add component for Salesforce Bulk API V2

[CAMEL-12489](https://issues.apache.org/jira/browse/CAMEL-12489)

camel-inifinspan: split remote and embedded components

### Task (24)

[CAMEL-16167](https://issues.apache.org/jira/browse/CAMEL-16167)

camel-cxf - Upgrade to CXF 3.4.2

[CAMEL-16166](https://issues.apache.org/jira/browse/CAMEL-16166)

camel-jetty - Upgrade to 9.4.36

[CAMEL-16164](https://issues.apache.org/jira/browse/CAMEL-16164)

Camel-Karaf: Remove not tested features

[CAMEL-16151](https://issues.apache.org/jira/browse/CAMEL-16151)

Using Camel component archetype, the XXXProducer.process contains extra space at end of line

[CAMEL-16150](https://issues.apache.org/jira/browse/CAMEL-16150)

Use https in readme created when creating a component using the archetype

[CAMEL-16132](https://issues.apache.org/jira/browse/CAMEL-16132)

Add description in README of spring-boot-widget-gadget

[CAMEL-16124](https://issues.apache.org/jira/browse/CAMEL-16124)

Create Huawei-smn starter for Camel-spring-boot

[CAMEL-16117](https://issues.apache.org/jira/browse/CAMEL-16117)

camel-debezium - Upgrade to 1.4.1

[CAMEL-16107](https://issues.apache.org/jira/browse/CAMEL-16107)

Deprecate Camel-AWS-\* components in favor of Camel-AWS2-\* ones

[CAMEL-16089](https://issues.apache.org/jira/browse/CAMEL-16089)

Split camel-infinispan and camel-infinispan-embedded in camel-spring-boot

[CAMEL-16087](https://issues.apache.org/jira/browse/CAMEL-16087)

Create camel-azure-storage-datalake SB starter

[CAMEL-16080](https://issues.apache.org/jira/browse/CAMEL-16080)

Migrate camel-kamelet component from camel-k-runtime to camel

[CAMEL-16054](https://issues.apache.org/jira/browse/CAMEL-16054)

Camel-AWS2-Kinesis: Support endpoint override like we have for S3

[CAMEL-16047](https://issues.apache.org/jira/browse/CAMEL-16047)

Error building camel 3.7.0 with jdk11

[CAMEL-16041](https://issues.apache.org/jira/browse/CAMEL-16041)

The managed dependency version through Camel Spring Boot BOM for com.google.guava:guava is from 2015

[CAMEL-16033](https://issues.apache.org/jira/browse/CAMEL-16033)

camel-core-languages should move out of generated list components in parent/pom.xml

[CAMEL-16027](https://issues.apache.org/jira/browse/CAMEL-16027)

camel-xml-jaxp should be put above the marker of camel components: START in parent/pom.xml

[CAMEL-16013](https://issues.apache.org/jira/browse/CAMEL-16013)

Camel-Kubernetes: Upgrade to Kubernetes client 5.x

[CAMEL-16007](https://issues.apache.org/jira/browse/CAMEL-16007)

\[camel-debezium\] Upgrade to Debezium 1.4

[CAMEL-15958](https://issues.apache.org/jira/browse/CAMEL-15958)

camel-vertx - Upgrade to 3.9.5

[CAMEL-15946](https://issues.apache.org/jira/browse/CAMEL-15946)

camel-endpointdsl - Generate valid javadoc

[CAMEL-15941](https://issues.apache.org/jira/browse/CAMEL-15941)

camel-flink - Upgrade to 1.12

[CAMEL-15934](https://issues.apache.org/jira/browse/CAMEL-15934)

camel-resilience4j - Upgrade to 1.6.x

[CAMEL-15700](https://issues.apache.org/jira/browse/CAMEL-15700)

Camel-Atlasmap: Add a Karaf feature

### Test (1)

[CAMEL-16053](https://issues.apache.org/jira/browse/CAMEL-16053)

camel-vertx-kafka - Test failures

### Wish (1)

[CAMEL-16131](https://issues.apache.org/jira/browse/CAMEL-16131)

huaweicloud-smn // Add functional testing stubs

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).