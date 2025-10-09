# Apache camel 4.2.0 Release

## New and Noteworthy

This release is the new Camel 4.2.0 release.

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
      <version>4.2.0</version>
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
      <version>4.2.0</version>
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
| [apache-camel-4.2.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-src.zip.sha512) |
| [apache-camel-4.2.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.xml.sha512) |
| [apache-camel-4.2.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.2.0/apache-camel-4.2.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.2.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.2.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-21288](https://issues.apache.org/jira/browse/CAMEL-21288)

Log processor causing memory leak in split for very large data sets

[CAMEL-20099](https://issues.apache.org/jira/browse/CAMEL-20099)

Camel-http is creating invalid Content-Encoding header based on charset from Content-Type header

[CAMEL-20092](https://issues.apache.org/jira/browse/CAMEL-20092)

camel-core - ScheduledPollConsumer should reset error count when greedy

[CAMEL-20086](https://issues.apache.org/jira/browse/CAMEL-20086)

Camel JBang loosing kamelets-version setting when using camel-version

[CAMEL-20079](https://issues.apache.org/jira/browse/CAMEL-20079)

EndpointDslMojo generates wrong header names

[CAMEL-20076](https://issues.apache.org/jira/browse/CAMEL-20076)

camel-jbang - Should skip jkube.yaml files

[CAMEL-20054](https://issues.apache.org/jira/browse/CAMEL-20054)

camel-kubernetes - Configuration of Kubernetes secrets with Camel K not working as expected

[CAMEL-20053](https://issues.apache.org/jira/browse/CAMEL-20053)

camel-jira: watchUpdates consumer does not see issues created after route startup

[CAMEL-20037](https://issues.apache.org/jira/browse/CAMEL-20037)

camel-http builds StringEntity with wrong contentEncoding

[CAMEL-20035](https://issues.apache.org/jira/browse/CAMEL-20035)

Program terminates with OutOfMemoryError

[CAMEL-20033](https://issues.apache.org/jira/browse/CAMEL-20033)

Camel JBang dependency is not supporting Windows path with Camel files written in Java

[CAMEL-20032](https://issues.apache.org/jira/browse/CAMEL-20032)

camel-yaml-dsl - Choice should not have steps in schema

[CAMEL-20031](https://issues.apache.org/jira/browse/CAMEL-20031)

camel-yaml-dsl: Description property have incorrect title and description

[CAMEL-20028](https://issues.apache.org/jira/browse/CAMEL-20028)

camel-mail - Missing attachments if disposition not set

[CAMEL-20023](https://issues.apache.org/jira/browse/CAMEL-20023)

camel-file - File readLock changed minAge issue

[CAMEL-20017](https://issues.apache.org/jira/browse/CAMEL-20017)

camel-yaml-dsl - ExchangeProperty language is duplicated in yaml schema

[CAMEL-20010](https://issues.apache.org/jira/browse/CAMEL-20010)

camel-sql - Can't change table name in JdbcMessageIdRepository by adding suffix/prefix

[CAMEL-20001](https://issues.apache.org/jira/browse/CAMEL-20001)

Overriden properties ignored with SpringPropertiesParser

[CAMEL-20000](https://issues.apache.org/jira/browse/CAMEL-20000)

camel-flatpack DataSetList iterator iterates only once

[CAMEL-19996](https://issues.apache.org/jira/browse/CAMEL-19996)

camel-lra NullPointerException when creating a saga with invalid lra-url

[CAMEL-19982](https://issues.apache.org/jira/browse/CAMEL-19982)

camel-jbang - Run with --jvm-debug as last parameter does not work

[CAMEL-19975](https://issues.apache.org/jira/browse/CAMEL-19975)

NIOConverter File to ByteBuffer conversion behavior is potentially non-deterministic

[CAMEL-19970](https://issues.apache.org/jira/browse/CAMEL-19970)

camel-jbang - IllegalArgumentException: Unable to determine file extension for resource when a file has no extension

[CAMEL-19968](https://issues.apache.org/jira/browse/CAMEL-19968)

camel-opentelemetry - The Tracing Strategy is failing when using pollEnrich with seda endpoint

[CAMEL-19967](https://issues.apache.org/jira/browse/CAMEL-19967)

camel-core - Default RouteConfigurationBuilder written in Java not enabled on XML routes

[CAMEL-19828](https://issues.apache.org/jira/browse/CAMEL-19828)

camel-twilio: conversion to PhoneNumber, .. fails after recent general converter change

[CAMEL-19827](https://issues.apache.org/jira/browse/CAMEL-19827)

Kafka Component generates huge logs infinitely when invalid configuration is provided.

[CAMEL-19068](https://issues.apache.org/jira/browse/CAMEL-19068)

SagaPropagationTest#testPropagationSupports fails with "Cannot begin: status is COMPLETED"

[CAMEL-18760](https://issues.apache.org/jira/browse/CAMEL-18760)

camel-kafka - Issue using ThrottlingExceptionRoutePolicy with Kafka consumer

### Dependency upgrade (20)

[CAMEL-20075](https://issues.apache.org/jira/browse/CAMEL-20075)

camel-kubernetes - upgrade to 6.9.2

[CAMEL-20074](https://issues.apache.org/jira/browse/CAMEL-20074)

Bump google-cloud-secretmanager-bom to version 2.29.0

[CAMEL-20073](https://issues.apache.org/jira/browse/CAMEL-20073)

Bump google-cloud-functions-bom to version 2.31.0

[CAMEL-20072](https://issues.apache.org/jira/browse/CAMEL-20072)

Upgrade Google Cloud BOM to version 26.26.0

[CAMEL-20069](https://issues.apache.org/jira/browse/CAMEL-20069)

Upgrade Azure SDK BOM to version 1.2.18

[CAMEL-20063](https://issues.apache.org/jira/browse/CAMEL-20063)

camel-jbang - Upgrade to kamelets 4.1.0

[CAMEL-20052](https://issues.apache.org/jira/browse/CAMEL-20052)

Upgrade Quarkus to 3.5.0 in Camel JBang to align with Camel Quarkus compatible with Camel 4.1+

[CAMEL-20049](https://issues.apache.org/jira/browse/CAMEL-20049)

camel-activemq - Upgrade to latest releases

[CAMEL-20006](https://issues.apache.org/jira/browse/CAMEL-20006)

Upgrade Google Cloud Functions BOM to version 2.30.0

[CAMEL-20005](https://issues.apache.org/jira/browse/CAMEL-20005)

Upgrade Google Secrets Manager BOM to version 2.28.0

[CAMEL-20003](https://issues.apache.org/jira/browse/CAMEL-20003)

Upgrade Google Cloud BOM to version 26.25.0

[CAMEL-19992](https://issues.apache.org/jira/browse/CAMEL-19992)

Upgrade bytebuddy that can support Java 21

[CAMEL-19990](https://issues.apache.org/jira/browse/CAMEL-19990)

camel-spring-boot - Upgrade to 3.1.5

[CAMEL-19980](https://issues.apache.org/jira/browse/CAMEL-19980)

Upgrade Infinispan to version 14.0.18.Final

[CAMEL-19979](https://issues.apache.org/jira/browse/CAMEL-19979)

Upgrade Vertx to version 4.4.6

[CAMEL-19978](https://issues.apache.org/jira/browse/CAMEL-19978)

Upgrade Netty to 4.1.100.Final

[CAMEL-19966](https://issues.apache.org/jira/browse/CAMEL-19966)

Upgrade Testcontainer to version 1.19.1

[CAMEL-19965](https://issues.apache.org/jira/browse/CAMEL-19965)

Camel-Plc4x: Upgrade to 0.11.0

[CAMEL-19963](https://issues.apache.org/jira/browse/CAMEL-19963)

camel-tooling-maven - Upgrade to resolver 1.9.16

[CAMEL-19638](https://issues.apache.org/jira/browse/CAMEL-19638)

Upgrade mockito to v5

### Improvement (37)

[CAMEL-20087](https://issues.apache.org/jira/browse/CAMEL-20087)

Backport data types from Kamelet utils to Camel

[CAMEL-20085](https://issues.apache.org/jira/browse/CAMEL-20085)

camel-aws - Sqs consumer throws unhandled exception during deleteMessage, should be caught by exception handler in consumer

[CAMEL-20081](https://issues.apache.org/jira/browse/CAMEL-20081)

camel-dynamic-router eip compnent: use existing multicast processor instead of custom impl

[CAMEL-20080](https://issues.apache.org/jira/browse/CAMEL-20080)

Removal of getExtentions() is not mentioned in migration guide to Camel 4

[CAMEL-20077](https://issues.apache.org/jira/browse/CAMEL-20077)

camel-core - Message history should be captured after debugger

[CAMEL-20071](https://issues.apache.org/jira/browse/CAMEL-20071)

camel-core - Backlog debugger must have node ids auto assigned eager to allow setting breakpoints on startup

[CAMEL-20070](https://issues.apache.org/jira/browse/CAMEL-20070)

camel-core: avoid unnecessary matching lookup

[CAMEL-20065](https://issues.apache.org/jira/browse/CAMEL-20065)

camel-core - BacklogDebugger as SPI

[CAMEL-20064](https://issues.apache.org/jira/browse/CAMEL-20064)

camel-main - Configure debugger options

[CAMEL-20061](https://issues.apache.org/jira/browse/CAMEL-20061)

SMPP interface version cannot be set from 3.4 to latest version 5.0, even though underlying library jSMPP supports versions 3.3, 3.4, and 5.0

[CAMEL-20060](https://issues.apache.org/jira/browse/CAMEL-20060)

Add Azure SAS support for azure blob storage

[CAMEL-20048](https://issues.apache.org/jira/browse/CAMEL-20048)

camel-core - Find single bean by type should use consistent method

[CAMEL-20042](https://issues.apache.org/jira/browse/CAMEL-20042)

camel-sql, use primary spring data source by default

[CAMEL-20039](https://issues.apache.org/jira/browse/CAMEL-20039)

camel-core - SimpleLRUCache add support for soft cache

[CAMEL-20038](https://issues.apache.org/jira/browse/CAMEL-20038)

camel-core - Deprecate LRUWeakCache

[CAMEL-20026](https://issues.apache.org/jira/browse/CAMEL-20026)

camel-jbang - Export allow to configure jib-maven-plugin version

[CAMEL-20025](https://issues.apache.org/jira/browse/CAMEL-20025)

camel-aws - Should we make region an enum

[CAMEL-20024](https://issues.apache.org/jira/browse/CAMEL-20024)

camel-core-model - Add description for new registry bean model

[CAMEL-20016](https://issues.apache.org/jira/browse/CAMEL-20016)

camel-lra - Allow accessing Exchange in LRAClient

[CAMEL-20013](https://issues.apache.org/jira/browse/CAMEL-20013)

AdviceWith requires camel-xml-io

[CAMEL-20011](https://issues.apache.org/jira/browse/CAMEL-20011)

camel-vertx: Avoid usage of deprecated Vertx.executeBlocking(Handler<Promise<T>>)

[CAMEL-20004](https://issues.apache.org/jira/browse/CAMEL-20004)

camel-core - DataTypeTransformer should be JdkService

[CAMEL-20002](https://issues.apache.org/jira/browse/CAMEL-20002)

camel-core: Make it easier to extend DefaultInjector

[CAMEL-19999](https://issues.apache.org/jira/browse/CAMEL-19999)

camel-bean - Allow to configure bean introspection cache on component

[CAMEL-19998](https://issues.apache.org/jira/browse/CAMEL-19998)

camel-core: cleanup cyclic dependencies in the AbstractCamelContext

[CAMEL-19997](https://issues.apache.org/jira/browse/CAMEL-19997)

camel-cifs: new component for the Common Internet File System

[CAMEL-19988](https://issues.apache.org/jira/browse/CAMEL-19988)

camel-core - PropertyBindingSupport - Should not hide IllegalArgumentException with real cause if failing to set property

[CAMEL-19987](https://issues.apache.org/jira/browse/CAMEL-19987)

camel-core - Optimize EndpointHelper.matchEndpoint to avoid regexp

[CAMEL-19977](https://issues.apache.org/jira/browse/CAMEL-19977)

camel-core - Java DSL to support text blocks for URI endpoints

[CAMEL-19905](https://issues.apache.org/jira/browse/CAMEL-19905)

camel-platform-http-vertx - Streaming mode for message body

[CAMEL-19830](https://issues.apache.org/jira/browse/CAMEL-19830)

camel-seda: investigate improvements and cleanups

[CAMEL-19707](https://issues.apache.org/jira/browse/CAMEL-19707)

camel-aws2-s3 multipart uploads crash with zero-byte files

[CAMEL-19437](https://issues.apache.org/jira/browse/CAMEL-19437)

Provide a profile to activate Camel Route debugger when generating Camel Quarkus project with Camel JBang export

[CAMEL-19398](https://issues.apache.org/jira/browse/CAMEL-19398)

camel-core: type converter performs slowly due to exception-based flow control

[CAMEL-17040](https://issues.apache.org/jira/browse/CAMEL-17040)

rest-dsl - Add option to return http 204 when no data in response

[CAMEL-15211](https://issues.apache.org/jira/browse/CAMEL-15211)

camel-main - Allow to configure SSL context parameters

[CAMEL-8306](https://issues.apache.org/jira/browse/CAMEL-8306)

rest-dsl - Add support for wildcards to match on prefix

### New Feature (13)

[CAMEL-20088](https://issues.apache.org/jira/browse/CAMEL-20088)

Camel-Azure-Schema-Registry component: Moving the bits from camel-kamelets and have a non-classic component

[CAMEL-20083](https://issues.apache.org/jira/browse/CAMEL-20083)

camel-opentelemtry - Make it easier to configure for camel-main

[CAMEL-20082](https://issues.apache.org/jira/browse/CAMEL-20082)

camel-jbang - Export to support javaagents

[CAMEL-20078](https://issues.apache.org/jira/browse/CAMEL-20078)

camel-jbang - Debug command

[CAMEL-20057](https://issues.apache.org/jira/browse/CAMEL-20057)

camel-azure - Allow to send binary files to azure service bus

[CAMEL-20050](https://issues.apache.org/jira/browse/CAMEL-20050)

camel-spring - Add support for @Primary spring bean autowiring

[CAMEL-20036](https://issues.apache.org/jira/browse/CAMEL-20036)

Provide endpoint producer builder for https endpoints

[CAMEL-19995](https://issues.apache.org/jira/browse/CAMEL-19995)

camel-jbang - Run and reload from clipboard

[CAMEL-19994](https://issues.apache.org/jira/browse/CAMEL-19994)

camel-platform-http-vertx - Allow access to vertx request object

[CAMEL-19945](https://issues.apache.org/jira/browse/CAMEL-19945)

camel-core - Add bean as property placeholder function

[CAMEL-19907](https://issues.apache.org/jira/browse/CAMEL-19907)

Introduce the ability to use the old Micrometer meter names or follow the new Micrometer naming conventions

[CAMEL-19085](https://issues.apache.org/jira/browse/CAMEL-19085)

camel-main - Allow to configure SSLContextParameters

[CAMEL-18637](https://issues.apache.org/jira/browse/CAMEL-18637)

camel-http - support OAuth 2.0

### Sub-task (1)

[CAMEL-20008](https://issues.apache.org/jira/browse/CAMEL-20008)

Java 21 - Test failures related to xml attribute order

### Task (18)

[CAMEL-20084](https://issues.apache.org/jira/browse/CAMEL-20084)

Create a Camel-SMB Spring Boot Starter

[CAMEL-20066](https://issues.apache.org/jira/browse/CAMEL-20066)

camel-language - Missing examples in docs

[CAMEL-20062](https://issues.apache.org/jira/browse/CAMEL-20062)

camel-core: type converter refactoring is causing a split package warning on Quarkus

[CAMEL-20051](https://issues.apache.org/jira/browse/CAMEL-20051)

camel-core: fallback conversions are not cached

[CAMEL-20043](https://issues.apache.org/jira/browse/CAMEL-20043)

Micrometer: unclear instructions of docInstrumentedThreadPoolFactory configuration in the documentation

[CAMEL-20030](https://issues.apache.org/jira/browse/CAMEL-20030)

camel-xslt-saxon - Non-working link in docs

[CAMEL-20029](https://issues.apache.org/jira/browse/CAMEL-20029)

camel-language - Missing examples in docs

[CAMEL-20022](https://issues.apache.org/jira/browse/CAMEL-20022)

camel-yaml-dsl: Add WARN log if kebab-case is detected

[CAMEL-19986](https://issues.apache.org/jira/browse/CAMEL-19986)

tests: create throtling executor

[CAMEL-19983](https://issues.apache.org/jira/browse/CAMEL-19983)

Camel-micrometer: Spring should not be mentioned as a part of the examples in the doc

[CAMEL-19974](https://issues.apache.org/jira/browse/CAMEL-19974)

camel-examples - Add missing descriptions

[CAMEL-19962](https://issues.apache.org/jira/browse/CAMEL-19962)

Camel-Azure-Datalake: Headers metadata are wrong

[CAMEL-19955](https://issues.apache.org/jira/browse/CAMEL-19955)

Camel-Infinispan: Review the usage of Protostream sample domain definition and implementation in tests

[CAMEL-19757](https://issues.apache.org/jira/browse/CAMEL-19757)

camel-examples - Move examples to root folder

[CAMEL-19557](https://issues.apache.org/jira/browse/CAMEL-19557)

camel-core: ensure tests have assertions

[CAMEL-19541](https://issues.apache.org/jira/browse/CAMEL-19541)

camel-quartz: replace Thread.sleep in tests

[CAMEL-19536](https://issues.apache.org/jira/browse/CAMEL-19536)

camel-micrometer: replace Thread.sleep in tests

[CAMEL-19526](https://issues.apache.org/jira/browse/CAMEL-19526)

camel-jms: replace Thread.sleep in tests

### Test (4)

[CAMEL-20098](https://issues.apache.org/jira/browse/CAMEL-20098)

camel-core - Flaky test using AbstractJsseParametersTest

[CAMEL-19993](https://issues.apache.org/jira/browse/CAMEL-19993)

camel-core - Fix XMLTokenizer tests for Java 21

[CAMEL-19958](https://issues.apache.org/jira/browse/CAMEL-19958)

Java 21 - Test failures on CI server

[CAMEL-18998](https://issues.apache.org/jira/browse/CAMEL-18998)

camel-ftp: FromFileToFtpSplitParallelIT tests a hanging up

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).