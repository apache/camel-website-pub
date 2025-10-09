# Apache camel 4.0.0-M2 Release

## New and Noteworthy

This release is the second milestone towards the Camel 4.0.0 release.

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
      <version>4.0.0-M2</version>
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
      <version>4.0.0-M2</version>
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
| [apache-camel-4.0.0-M2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M2/apache-camel-4.0.0-M2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M2/apache-camel-4.0.0-M2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M2/apache-camel-4.0.0-M2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.0-M2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.0-M2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (18)

[CAMEL-19112](https://issues.apache.org/jira/browse/CAMEL-19112)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.yaml'

[CAMEL-19111](https://issues.apache.org/jira/browse/CAMEL-19111)

Yaml DSL does not seem to work with split/xtokenize

[CAMEL-19098](https://issues.apache.org/jira/browse/CAMEL-19098)

Possible performance issue invoking a bean method with a string parameter

[CAMEL-19079](https://issues.apache.org/jira/browse/CAMEL-19079)

NullPointerException thrown when using the language:xquery endpoint

[CAMEL-19075](https://issues.apache.org/jira/browse/CAMEL-19075)

camel-bean - Incorrect choice of overloaded method with several arguments, if one of them has brackets.

[CAMEL-19067](https://issues.apache.org/jira/browse/CAMEL-19067)

Camel-JBang | camel init creates file but errors out on Windows

[CAMEL-19066](https://issues.apache.org/jira/browse/CAMEL-19066)

Multicast EIP sets correlationId on original Exchange

[CAMEL-19051](https://issues.apache.org/jira/browse/CAMEL-19051)

Camel-opentelemetry: Avoid using the GlobalOpenTelemetry.get() and allow for injection of ContextPropagators

[CAMEL-19047](https://issues.apache.org/jira/browse/CAMEL-19047)

CamelTestSupport (junit5) - quarkus and springboot checks are not executed with ContextPerClass

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19031](https://issues.apache.org/jira/browse/CAMEL-19031)

When camel saga do compensated, the saga route don't stop it still run the next task.

[CAMEL-19026](https://issues.apache.org/jira/browse/CAMEL-19026)

camel-jbang - camel.main.backlogTracing=true

[CAMEL-19018](https://issues.apache.org/jira/browse/CAMEL-19018)

camel-vertx-http: Headers may get erroneously duplicated

[CAMEL-19006](https://issues.apache.org/jira/browse/CAMEL-19006)

XML IO DSL do not load templatedRoutes without XML namespace

[CAMEL-19004](https://issues.apache.org/jira/browse/CAMEL-19004)

XML IO DSL do not parse route configuration with XML namespace

[CAMEL-19002](https://issues.apache.org/jira/browse/CAMEL-19002)

camel-jbang - Log command should detect lines without timestamp

[CAMEL-18980](https://issues.apache.org/jira/browse/CAMEL-18980)

camel snmp - SNMP Ver1 trap does not work

[CAMEL-18954](https://issues.apache.org/jira/browse/CAMEL-18954)

camel-micrometer - NPE on spring boot

### Dependency upgrade (15)

[CAMEL-19123](https://issues.apache.org/jira/browse/CAMEL-19123)

camel-jbang - upgrade maven-resolver to 1.9.7

[CAMEL-19110](https://issues.apache.org/jira/browse/CAMEL-19110)

camel-spring-boot - Upgrade to 3.0.4

[CAMEL-19092](https://issues.apache.org/jira/browse/CAMEL-19092)

camel-jbang - upgrade maven-resolver-api to 1.9.5

[CAMEL-19059](https://issues.apache.org/jira/browse/CAMEL-19059)

camel-snmp - Use original JAR instead of SMX wrap

[CAMEL-19039](https://issues.apache.org/jira/browse/CAMEL-19039)

camel-jms - Upgrade to Artemis 2.28.x

[CAMEL-19029](https://issues.apache.org/jira/browse/CAMEL-19029)

camel-twilio - Upgrade twilio-java to a version Jakarta compatible

[CAMEL-19005](https://issues.apache.org/jira/browse/CAMEL-19005)

Update PubNub to 6.x

[CAMEL-19003](https://issues.apache.org/jira/browse/CAMEL-19003)

Avoid using old guava versions

[CAMEL-18999](https://issues.apache.org/jira/browse/CAMEL-18999)

camel-sshd - Upgrade to 2.9.x

[CAMEL-18997](https://issues.apache.org/jira/browse/CAMEL-18997)

camel-mina - Upgrade to 2.2.1

[CAMEL-18994](https://issues.apache.org/jira/browse/CAMEL-18994)

Huawei Cloud SDK: Bump to 3.1.x

[CAMEL-18993](https://issues.apache.org/jira/browse/CAMEL-18993)

camel-qpid - Upgrade to 2.2 and 9.0 broker

[CAMEL-18987](https://issues.apache.org/jira/browse/CAMEL-18987)

camel-zookeeper - Upgrade to 3.8.x

[CAMEL-18824](https://issues.apache.org/jira/browse/CAMEL-18824)

upgrade to newer guava versions

[CAMEL-18610](https://issues.apache.org/jira/browse/CAMEL-18610)

Support Debezium 2.0

### Improvement (19)

[CAMEL-19109](https://issues.apache.org/jira/browse/CAMEL-19109)

camel-vertx-websocket: Consumer should avoid blocking the Vert.x event loop

[CAMEL-19094](https://issues.apache.org/jira/browse/CAMEL-19094)

Tokenizer ignores includeTokens

[CAMEL-19093](https://issues.apache.org/jira/browse/CAMEL-19093)

camel-jbang - Run local JAR should add to classpath so can be used in Java DSL

[CAMEL-19089](https://issues.apache.org/jira/browse/CAMEL-19089)

camel-core - Remove ExchangePattern.InOptionalOut

[CAMEL-19083](https://issues.apache.org/jira/browse/CAMEL-19083)

camel-yaml-dsl: Add a doc section that links to the schema

[CAMEL-19078](https://issues.apache.org/jira/browse/CAMEL-19078)

camel-platform-http-vertx: Allow response headers with empty values to be returned

[CAMEL-19076](https://issues.apache.org/jira/browse/CAMEL-19076)

camel-jbang - Tracer to have option to show also internal exchange properties

[CAMEL-19073](https://issues.apache.org/jira/browse/CAMEL-19073)

camel-core - Properties component - reload properties for only changed

[CAMEL-19072](https://issues.apache.org/jira/browse/CAMEL-19072)

camel-yaml-dsl - Remove backwards compatible 3.15 parser

[CAMEL-19071](https://issues.apache.org/jira/browse/CAMEL-19071)

camel-jbang - Reload all routes in changes to application.properties in dev mode

[CAMEL-19064](https://issues.apache.org/jira/browse/CAMEL-19064)

Camel-Freemarker: Do not set DEFAULT\_INCOMPATIBLE\_IMPROVEMENTS in the Freemarker configuration

[CAMEL-19055](https://issues.apache.org/jira/browse/CAMEL-19055)

camel-core - Backlog tracer capture thread id of the processed exchange

[CAMEL-19043](https://issues.apache.org/jira/browse/CAMEL-19043)

camel-core - Add Exchange.RECEIVED\_TIMESTAMP as internal exchange property

[CAMEL-19042](https://issues.apache.org/jira/browse/CAMEL-19042)

camel-quarkus-catalog - Uses 0.0.1 version

[CAMEL-19040](https://issues.apache.org/jira/browse/CAMEL-19040)

camel-core - Backlog tracer to capture exception and exchange properties

[CAMEL-19025](https://issues.apache.org/jira/browse/CAMEL-19025)

camel-jbang - doc command should be case insensitive in filter

[CAMEL-19008](https://issues.apache.org/jira/browse/CAMEL-19008)

spring-rabbitmq component does not fail on sending to non-existent RabbitMQ topic

[CAMEL-18990](https://issues.apache.org/jira/browse/CAMEL-18990)

camel-jbang - Export to Quarkus should add resources for native compilation

[CAMEL-18986](https://issues.apache.org/jira/browse/CAMEL-18986)

camel-core - ProducerTemplate send exchange should set from endpoint if null

### New Feature (7)

[CAMEL-19069](https://issues.apache.org/jira/browse/CAMEL-19069)

Presigned urls in camel-minio component

[CAMEL-19044](https://issues.apache.org/jira/browse/CAMEL-19044)

Camel-Jbang catalog output in JSON

[CAMEL-19033](https://issues.apache.org/jira/browse/CAMEL-19033)

camel-jbang - Add trace command

[CAMEL-19030](https://issues.apache.org/jira/browse/CAMEL-19030)

camel-jbang - doc and catalog to support --camel-version option

[CAMEL-19027](https://issues.apache.org/jira/browse/CAMEL-19027)

camel-console - Add dev console for backlog tracer

[CAMEL-18989](https://issues.apache.org/jira/browse/CAMEL-18989)

camel-jbang - Run custom distributions of Camel

[CAMEL-18131](https://issues.apache.org/jira/browse/CAMEL-18131)

camel-health - Add health checks for components that has extension for connectivity verification

### Sub-task (1)

[CAMEL-18991](https://issues.apache.org/jira/browse/CAMEL-18991)

Camel-Google-Storage: Health Check for consumer

### Task (13)

[CAMEL-19117](https://issues.apache.org/jira/browse/CAMEL-19117)

camel-catalog - Remove archetypeAsXml from CamelCatalog

[CAMEL-19091](https://issues.apache.org/jira/browse/CAMEL-19091)

camel-core - Remove Discard and DiscardOldest from thread pool policy

[CAMEL-19088](https://issues.apache.org/jira/browse/CAMEL-19088)

camel-core - Remove SafeCopyProperty that was only in use for camel-zipkin

[CAMEL-19070](https://issues.apache.org/jira/browse/CAMEL-19070)

camel-elasticsearch: flaky tests on Apache CI

[CAMEL-19054](https://issues.apache.org/jira/browse/CAMEL-19054)

Camel-Fastjson: Switch to 2.x

[CAMEL-19011](https://issues.apache.org/jira/browse/CAMEL-19011)

update release notes to point users to use camel-bom / camel-spring-boot-bom

[CAMEL-19009](https://issues.apache.org/jira/browse/CAMEL-19009)

camel-gson - Date Format with GsonBuilder

[CAMEL-19007](https://issues.apache.org/jira/browse/CAMEL-19007)

camel-yaml-dsl - Deprecate classic parsing mode

[CAMEL-18996](https://issues.apache.org/jira/browse/CAMEL-18996)

Camel-CassandraQL: Adding a parameter to pass a list of ExtraTypesCodec to SessionBuilder

[CAMEL-18984](https://issues.apache.org/jira/browse/CAMEL-18984)

camel-undertow-spring-security-starter - Migrate to Spring Boot 3

[CAMEL-18982](https://issues.apache.org/jira/browse/CAMEL-18982)

Avoid custom versions of maven javadoc and resource plugin

[CAMEL-18971](https://issues.apache.org/jira/browse/CAMEL-18971)

Camel-Spring-Boot: Add SBOM generation

[CAMEL-18930](https://issues.apache.org/jira/browse/CAMEL-18930)

camel-spring-boot - Migrate undertow-security

### Test (2)

[CAMEL-19084](https://issues.apache.org/jira/browse/CAMEL-19084)

camel-yaml-dsl: Test resume strategies

[CAMEL-18988](https://issues.apache.org/jira/browse/CAMEL-18988)

camel-core: tests failing due to (likely) OOM

### Wish (1)

[CAMEL-18305](https://issues.apache.org/jira/browse/CAMEL-18305)

Make XML Dumper work XML-IO

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).