# Apache camel 2.18.1 Release

## New and Noteworthy

This release is a minor update of the 2.18.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.18.1</version>
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
      <version>2.18.1</version>
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
| [apache-camel-2.18.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.1/apache-camel-2.18.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.1/apache-camel-2.18.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.1/apache-camel-2.18.1-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (42)

[CAMEL-10534](https://issues.apache.org/jira/browse/CAMEL-10534)

camel-stream - Producer writing to stream url need to set doOutput=true

[CAMEL-10520](https://issues.apache.org/jira/browse/CAMEL-10520)

Lumberjack protocol v1 acknowlegment is not correcty implemented

[CAMEL-10510](https://issues.apache.org/jira/browse/CAMEL-10510)

HL7AcknowledgementGenerator should set exchange property and not message header

[CAMEL-10505](https://issues.apache.org/jira/browse/CAMEL-10505)

"FILE" component with option "readLock=rename" throws FileNotFound exception in case of work file is locked/used by another application

[CAMEL-10504](https://issues.apache.org/jira/browse/CAMEL-10504)

Hiding an underlying exception if MongoDbBasicConverters fails to convert to DBObject

[CAMEL-10499](https://issues.apache.org/jira/browse/CAMEL-10499)

camel-sql - error in multiple dynamic IN replacement

[CAMEL-10480](https://issues.apache.org/jira/browse/CAMEL-10480)

MemoryLeak in the DatagramPacketObjectEncoder

[CAMEL-10476](https://issues.apache.org/jira/browse/CAMEL-10476)

configAdminFile not used to populate property placeholders in camel-test-blueprint when run via camel-maven-plugin

[CAMEL-10467](https://issues.apache.org/jira/browse/CAMEL-10467)

camel-servicenow : ServiceNowConstants not backward-compatible (2.18.0 --> 2.18.1)

[CAMEL-10466](https://issues.apache.org/jira/browse/CAMEL-10466)

OOM in Dropbox component (uses ByteArrayOutputStream for get)

[CAMEL-10465](https://issues.apache.org/jira/browse/CAMEL-10465)

camel ahc uses netty 4.0.41 transitively but 4.1.5 explicitly - leads to runtime exceptions

[CAMEL-10460](https://issues.apache.org/jira/browse/CAMEL-10460)

MetricsMessageHistoryFactory.java:138 Generate a NPE

[CAMEL-10455](https://issues.apache.org/jira/browse/CAMEL-10455)

camel-chronicle - has SNAPSHOT dependency

[CAMEL-10454](https://issues.apache.org/jira/browse/CAMEL-10454)

Unclear piece in IdempotentConsumer.java

[CAMEL-10453](https://issues.apache.org/jira/browse/CAMEL-10453)

camel-elsql does not set CamelSqlUpdateCount header on update operation

[CAMEL-10449](https://issues.apache.org/jira/browse/CAMEL-10449)

Set CXF SoapAction header correctly

[CAMEL-10443](https://issues.apache.org/jira/browse/CAMEL-10443)

findById does not work with ObjectId

[CAMEL-10441](https://issues.apache.org/jira/browse/CAMEL-10441)

The WorkerGroup option is for NettyConsumer and NettyProducer

[CAMEL-10431](https://issues.apache.org/jira/browse/CAMEL-10431)

camel-elsql - Does not read named parameter from header properties

[CAMEL-10430](https://issues.apache.org/jira/browse/CAMEL-10430)

camel-hystrix - Should also execute fallback if exception not from Camel

[CAMEL-10429](https://issues.apache.org/jira/browse/CAMEL-10429)

CXFRS client requires Exchange.HTTP\_URI instead of HTTP\_PATH for Camel tranport

[CAMEL-10427](https://issues.apache.org/jira/browse/CAMEL-10427)

CXFRS client gets "Response timeout" exception when used with Camel transport

[CAMEL-10425](https://issues.apache.org/jira/browse/CAMEL-10425)

java.io.IOException: Stream closed - When setting result from bean in route

[CAMEL-10414](https://issues.apache.org/jira/browse/CAMEL-10414)

Query is ignore if field filter header is set

[CAMEL-10411](https://issues.apache.org/jira/browse/CAMEL-10411)

Camel-Blueprint - failed container gets restarted automatically

[CAMEL-10409](https://issues.apache.org/jira/browse/CAMEL-10409)

Double release of netty buffer

[CAMEL-10407](https://issues.apache.org/jira/browse/CAMEL-10407)

camel-example-loan-broker : target directory is cleaned while testing so test are failing

[CAMEL-10406](https://issues.apache.org/jira/browse/CAMEL-10406)

VM endpoint caching leak the wrong camel context

[CAMEL-10399](https://issues.apache.org/jira/browse/CAMEL-10399)

OutOfMemoryError: Java heap space when sending large file to endpoint

[CAMEL-10394](https://issues.apache.org/jira/browse/CAMEL-10394)

BlueprintCamelContext cannot find components created in RouteBuilder.configure method

[CAMEL-10386](https://issues.apache.org/jira/browse/CAMEL-10386)

simple language nullsafe expression fails on empty array

[CAMEL-10385](https://issues.apache.org/jira/browse/CAMEL-10385)

simple ognl expression issue w/ list & spring boot

[CAMEL-10384](https://issues.apache.org/jira/browse/CAMEL-10384)

Shutdown broken when using Spring Boot

[CAMEL-10383](https://issues.apache.org/jira/browse/CAMEL-10383)

activemq-camel - Issue with parsing uri to determine queue vs topic

[CAMEL-10381](https://issues.apache.org/jira/browse/CAMEL-10381)

camel-google-mail getting NPE from component configuration

[CAMEL-10380](https://issues.apache.org/jira/browse/CAMEL-10380)

JettyHttpEndpoint9 ignores eagerCheckContentAvailable so Jetty builds a reuqest with "Transfer-Encoding: chunked"

[CAMEL-10376](https://issues.apache.org/jira/browse/CAMEL-10376)

BeanInfo#introspect does not work correctly with bridge methods

[CAMEL-10372](https://issues.apache.org/jira/browse/CAMEL-10372)

camel-stream - Component doc issue

[CAMEL-10370](https://issues.apache.org/jira/browse/CAMEL-10370)

Conversion to CxfPayload throws Exception for Non-XML payload

[CAMEL-10368](https://issues.apache.org/jira/browse/CAMEL-10368)

Unused deflater in ZipDataFormat

[CAMEL-10341](https://issues.apache.org/jira/browse/CAMEL-10341)

When using SSL, a NettyConsumer set to Client Mode does not initiate a handshake

[CAMEL-10236](https://issues.apache.org/jira/browse/CAMEL-10236)

BeanProccessor - method invocation with generics+annotations

### Improvement (19)

[CAMEL-10527](https://issues.apache.org/jira/browse/CAMEL-10527)

camel-mail - Option skipFailedMessage should catch all exceptions

[CAMEL-10488](https://issues.apache.org/jira/browse/CAMEL-10488)

ServiceNow : add an option to configure teh API version

[CAMEL-10482](https://issues.apache.org/jira/browse/CAMEL-10482)

ServiceNow : add an option to set inbound and outbound models

[CAMEL-10479](https://issues.apache.org/jira/browse/CAMEL-10479)

camel-servicenow: add missing @Deprecated annotations to ServiceNowConstants

[CAMEL-10473](https://issues.apache.org/jira/browse/CAMEL-10473)

Failover Loadbalancer - Error handler should kick in after exhausted when inheritErrorHandler is false

[CAMEL-10470](https://issues.apache.org/jira/browse/CAMEL-10470)

camel-mail - Should allow to configure SimpleSearchTerm as plain POJO

[CAMEL-10468](https://issues.apache.org/jira/browse/CAMEL-10468)

Java8 DSL: Add support for aggregation strategy with different body types

[CAMEL-10444](https://issues.apache.org/jira/browse/CAMEL-10444)

Return header with key CamelMongoDbRecordsAffected from update and remove operations

[CAMEL-10438](https://issues.apache.org/jira/browse/CAMEL-10438)

Java8 DSL for Content Enricher and Aggregator

[CAMEL-10434](https://issues.apache.org/jira/browse/CAMEL-10434)

Camel catalog - Filter karaf / spring boot components

[CAMEL-10424](https://issues.apache.org/jira/browse/CAMEL-10424)

Bean should act like transform/setBody when setting result

[CAMEL-10410](https://issues.apache.org/jira/browse/CAMEL-10410)

Karaf features: install camel-karaf-commands and camel-karaf-commands-catalog only if karaf shell is installed

[CAMEL-10408](https://issues.apache.org/jira/browse/CAMEL-10408)

Camel-JMS: Suspending/resuming won't work in case of timeout

[CAMEL-10400](https://issues.apache.org/jira/browse/CAMEL-10400)

Upgrade EasyMock to version 3.4

[CAMEL-10390](https://issues.apache.org/jira/browse/CAMEL-10390)

ObjectHelper's after/before/between enhancements

[CAMEL-10387](https://issues.apache.org/jira/browse/CAMEL-10387)

JMS correlationIdAsBytes should return null and not byte array with zero values

[CAMEL-10378](https://issues.apache.org/jira/browse/CAMEL-10378)

Upgrade log4j2 to v2.7

[CAMEL-10357](https://issues.apache.org/jira/browse/CAMEL-10357)

camel-servicenow - Add per release model

[CAMEL-10352](https://issues.apache.org/jira/browse/CAMEL-10352)

Optionally delegate to Aries PropertyEvaluator services in BlueprintPropertiesParser

### New Feature (2)

[CAMEL-10402](https://issues.apache.org/jira/browse/CAMEL-10402)

camel-servicenow : Allow to configure credentials on ServiceNow component

[CAMEL-10358](https://issues.apache.org/jira/browse/CAMEL-10358)

camel-spring-boot - Add example how to use Spring Boot Live Reload

### Task (6)

[CAMEL-10818](https://issues.apache.org/jira/browse/CAMEL-10818)

Unable to use JPA in camel 2.18.1 on Karaf 4.0.8

[CAMEL-10458](https://issues.apache.org/jira/browse/CAMEL-10458)

Upgrade to Spring Boot 1.4.2

[CAMEL-10457](https://issues.apache.org/jira/browse/CAMEL-10457)

Cannot generate javadoc for camel-jms-starter

[CAMEL-10445](https://issues.apache.org/jira/browse/CAMEL-10445)

Upgrade to CXF 3.1.8

[CAMEL-10379](https://issues.apache.org/jira/browse/CAMEL-10379)

Improved component description

[CAMEL-10367](https://issues.apache.org/jira/browse/CAMEL-10367)

remove extraneous dependency from camel-amqp module

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).