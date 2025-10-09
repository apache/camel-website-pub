# Apache camel 4.3.0 Release

## New and Noteworthy

This release is the new Camel 4.3.0 release.

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
      <version>4.3.0</version>
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
      <version>4.3.0</version>
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
| [apache-camel-4.3.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-src.zip.sha512) |
| [apache-camel-4.3.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.xml.sha512) |
| [apache-camel-4.3.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.3.0/apache-camel-4.3.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.3.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.3.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (19)

[CAMEL-20214](https://issues.apache.org/jira/browse/CAMEL-20214)

camel-core - Timeout tasks of parallel splitter block further message processing

[CAMEL-20213](https://issues.apache.org/jira/browse/CAMEL-20213)

camel-core - Dependency injection for @BeanInject for private fields

[CAMEL-20210](https://issues.apache.org/jira/browse/CAMEL-20210)

camel-core - Rest DSL Narrow content-type with charset fails clientRequestValidation

[CAMEL-20204](https://issues.apache.org/jira/browse/CAMEL-20204)

StringSource and SourceCache using the isEmpty method will always return true

[CAMEL-20203](https://issues.apache.org/jira/browse/CAMEL-20203)

test-infra - Azure test infra has NPE

[CAMEL-20173](https://issues.apache.org/jira/browse/CAMEL-20173)

camel-jbang - Camel run with --download=false should load from local JARs

[CAMEL-20156](https://issues.apache.org/jira/browse/CAMEL-20156)

openapi-java: REST DSL param arrayType with allowableValues can lead to NoSuchMethodException

[CAMEL-20155](https://issues.apache.org/jira/browse/CAMEL-20155)

camel-jbang - camel get processor - Cannot show processors with nodePrefixId

[CAMEL-20152](https://issues.apache.org/jira/browse/CAMEL-20152)

camel-jetty - OutOfMemoryError with big file upload via multipart

[CAMEL-20143](https://issues.apache.org/jira/browse/CAMEL-20143)

camel-core - Dump route when debugger enable should include source line

[CAMEL-20140](https://issues.apache.org/jira/browse/CAMEL-20140)

camel-report:route-coverage results in no code coverage

[CAMEL-20139](https://issues.apache.org/jira/browse/CAMEL-20139)

aggregate EIP: wrong correlation key set for the first aggregate exchange

[CAMEL-20124](https://issues.apache.org/jira/browse/CAMEL-20124)

camel-netty - Fix ChannelHandlerFactories' usage of unsharable ByteArrayDecoder

[CAMEL-20109](https://issues.apache.org/jira/browse/CAMEL-20109)

Endpoints with special characters (especially '#' like in spring-redis when specifying a redisTemplate)) can't be removed anymore with context.removeEndpoint

[CAMEL-20103](https://issues.apache.org/jira/browse/CAMEL-20103)

DefaultProducerCache returns wrong ProducerTemplate under high concurrency load

[CAMEL-20100](https://issues.apache.org/jira/browse/CAMEL-20100)

Camel-jsonpath can't fetch missing field in some cases when body is returned from a http/https call

[CAMEL-20044](https://issues.apache.org/jira/browse/CAMEL-20044)

camel-kafka - On rejoining consumer group Camel can set offset incorrectly causing messages to be replayed

[CAMEL-19894](https://issues.apache.org/jira/browse/CAMEL-19894)

camel-kafka: enabling "breakOnFirstError" causes to skip records on exception

[CAMEL-19734](https://issues.apache.org/jira/browse/CAMEL-19734)

SEDA endpoint with multiple consumers produces strange message history from error handler

### Dependency upgrade (12)

[CAMEL-20198](https://issues.apache.org/jira/browse/CAMEL-20198)

camel-google - Upgrade to newer google-api-services

[CAMEL-20168](https://issues.apache.org/jira/browse/CAMEL-20168)

Camel-jaxb: jaxb-impl was upgraded but not jaxb-core

[CAMEL-20148](https://issues.apache.org/jira/browse/CAMEL-20148)

camel-spring-boot - Upgrade to 3.2

[CAMEL-20144](https://issues.apache.org/jira/browse/CAMEL-20144)

camel-jbang - Upgrade to openapi-generator 7.x

[CAMEL-20142](https://issues.apache.org/jira/browse/CAMEL-20142)

Camel-http: brings transitively 2 core versions

[CAMEL-20129](https://issues.apache.org/jira/browse/CAMEL-20129)

Upgrade Localstack to version 3.0.0

[CAMEL-20117](https://issues.apache.org/jira/browse/CAMEL-20117)

Johnzon-jsonb: Update to 2.0.0

[CAMEL-20034](https://issues.apache.org/jira/browse/CAMEL-20034)

Upgrade to Spring Boot 3.2

[CAMEL-19991](https://issues.apache.org/jira/browse/CAMEL-19991)

camel-jetty - Upgrade to jetty 12

[CAMEL-19981](https://issues.apache.org/jira/browse/CAMEL-19981)

camel-kafka - Upgrade to Kafka 3.6.1

[CAMEL-19959](https://issues.apache.org/jira/browse/CAMEL-19959)

camel-kubernetes - Upgrade to 6.9.x

[CAMEL-19631](https://issues.apache.org/jira/browse/CAMEL-19631)

camel-spring-boot - Upgrade graalsdk

### Improvement (42)

[CAMEL-20212](https://issues.apache.org/jira/browse/CAMEL-20212)

Move MemoryStateRepository and FileStateRepository to camel-support

[CAMEL-20211](https://issues.apache.org/jira/browse/CAMEL-20211)

camel-jbang - Export should not start IdempotentConsumer

[CAMEL-20209](https://issues.apache.org/jira/browse/CAMEL-20209)

camel-azure - Adopt atomic overwrite feature of Azure Files

[CAMEL-20208](https://issues.apache.org/jira/browse/CAMEL-20208)

camel-core-model - Route id and description should be ranked higher

[CAMEL-20207](https://issues.apache.org/jira/browse/CAMEL-20207)

camel-core-model - Resequence stream and batch config should use camelCase

[CAMEL-20197](https://issues.apache.org/jira/browse/CAMEL-20197)

camel-catalog - Allow to provide options for validateLanguage

[CAMEL-20193](https://issues.apache.org/jira/browse/CAMEL-20193)

openapi-java: RestModelConverters is not using 3.1 ModelConverters

[CAMEL-20191](https://issues.apache.org/jira/browse/CAMEL-20191)

camel-yaml-dsl - A few option has not same name as in catalog

[CAMEL-20189](https://issues.apache.org/jira/browse/CAMEL-20189)

camel-sftp: report consumer UP after connection is established

[CAMEL-20182](https://issues.apache.org/jira/browse/CAMEL-20182)

camel-http - Configuring full url in httpUri should allow to have http/https protocol

[CAMEL-20181](https://issues.apache.org/jira/browse/CAMEL-20181)

openapi-java: Make sure the tests support both OpenAPI 3.0 and 3.1

[CAMEL-20180](https://issues.apache.org/jira/browse/CAMEL-20180)

camel-console - JSon output for date/time should be computer value

[CAMEL-20179](https://issues.apache.org/jira/browse/CAMEL-20179)

camel-management - Add IdleSince MBean attribute

[CAMEL-20178](https://issues.apache.org/jira/browse/CAMEL-20178)

camel-jbang - Transform message to support components and data formats

[CAMEL-20174](https://issues.apache.org/jira/browse/CAMEL-20174)

camel-ssh: Provide support to configure algorithms

[CAMEL-20170](https://issues.apache.org/jira/browse/CAMEL-20170)

camel-jbang - Report more accurately maven downloads

[CAMEL-20165](https://issues.apache.org/jira/browse/CAMEL-20165)

camel-jbang - Should we have modeline for JBang style of DEPS

[CAMEL-20151](https://issues.apache.org/jira/browse/CAMEL-20151)

camel-xpath - Add xpath as function to simple for basic templating

[CAMEL-20150](https://issues.apache.org/jira/browse/CAMEL-20150)

camel-jq - Optimize to load functions once and use child scopes per exchange

[CAMEL-20145](https://issues.apache.org/jira/browse/CAMEL-20145)

camel-micrometer-prometheus - Need to init earlier to ensure route policy can be in use

[CAMEL-20137](https://issues.apache.org/jira/browse/CAMEL-20137)

camel-joor - Allow to use java as language name also

[CAMEL-20136](https://issues.apache.org/jira/browse/CAMEL-20136)

camel-core - Enable source location if debug or tracing in standby mode

[CAMEL-20134](https://issues.apache.org/jira/browse/CAMEL-20134)

camel-joor - Allow to compile scrip with classloader from Camel

[CAMEL-20131](https://issues.apache.org/jira/browse/CAMEL-20131)

camel-core - SetHeaders EIP some small things we can improve

[CAMEL-20127](https://issues.apache.org/jira/browse/CAMEL-20127)

camel-core - Add messageAs function to simple language

[CAMEL-20125](https://issues.apache.org/jira/browse/CAMEL-20125)

camel-jbang - Export to camel-main - Allow to configure auth for jib-maven-plugin

[CAMEL-20122](https://issues.apache.org/jira/browse/CAMEL-20122)

Improve Stream component to handle HTTP headers in a more intuitive format

[CAMEL-20120](https://issues.apache.org/jira/browse/CAMEL-20120)

Add showRouteId and ShowRouteGroup to the Log component

[CAMEL-20119](https://issues.apache.org/jira/browse/CAMEL-20119)

camel-stream - Http stream headers should use colon as key value separator

[CAMEL-20114](https://issues.apache.org/jira/browse/CAMEL-20114)

camel-salesforce: generatePubSub plugin goal should clean up temporary schema JSON files

[CAMEL-20112](https://issues.apache.org/jira/browse/CAMEL-20112)

camel-jbang - Debug command should not step inside kamelets

[CAMEL-20110](https://issues.apache.org/jira/browse/CAMEL-20110)

camel-jetty - Allow to configure idleTimeout on jetty server

[CAMEL-20107](https://issues.apache.org/jira/browse/CAMEL-20107)

camel-salesforce: PubSubApiConsumer may fail to load pojo class

[CAMEL-20106](https://issues.apache.org/jira/browse/CAMEL-20106)

camel-spring-xml - Generate correct error handler in XSD

[CAMEL-20102](https://issues.apache.org/jira/browse/CAMEL-20102)

camel-vertx-http - Make configuring http method tooling friendly

[CAMEL-20101](https://issues.apache.org/jira/browse/CAMEL-20101)

camel-jolt - query parameter allowContextMapAll is ignored

[CAMEL-20067](https://issues.apache.org/jira/browse/CAMEL-20067)

camel-core - Add debuggingStandby option

[CAMEL-19835](https://issues.apache.org/jira/browse/CAMEL-19835)

camel-core: replace temporary dir logic in test code

[CAMEL-19648](https://issues.apache.org/jira/browse/CAMEL-19648)

camel-spring-boot - Actuator health check should handle readiness vs liveness checks

[CAMEL-19398](https://issues.apache.org/jira/browse/CAMEL-19398)

camel-core: type converter performs slowly due to exception-based flow control

[CAMEL-18768](https://issues.apache.org/jira/browse/CAMEL-18768)

camel-jq - Make it easier to grab elements in a template like fashion

[CAMEL-16099](https://issues.apache.org/jira/browse/CAMEL-16099)

camel-core - Throttler EIP to support max inflight messages without time period

### New Feature (19)

[CAMEL-20192](https://issues.apache.org/jira/browse/CAMEL-20192)

Introduce a kamelet for AMQPS

[CAMEL-20190](https://issues.apache.org/jira/browse/CAMEL-20190)

Camel-Spring-Boot: Kubernetes Cronjob starter

[CAMEL-20187](https://issues.apache.org/jira/browse/CAMEL-20187)

Add basic support of virtual threads

[CAMEL-20186](https://issues.apache.org/jira/browse/CAMEL-20186)

camel-jbang - Add option to camel dependencies to add jbang style //DEPS to source file

[CAMEL-20185](https://issues.apache.org/jira/browse/CAMEL-20185)

Kubernetes CronJob Component

[CAMEL-20172](https://issues.apache.org/jira/browse/CAMEL-20172)

Add checksum feature to camel-file/ftp

[CAMEL-20166](https://issues.apache.org/jira/browse/CAMEL-20166)

Elasticsearch Low level client

[CAMEL-20164](https://issues.apache.org/jira/browse/CAMEL-20164)

camel-core - Dev console for consumer

[CAMEL-20162](https://issues.apache.org/jira/browse/CAMEL-20162)

Camel-AWS-Config: Add Describe Compliance By Config Rule operation

[CAMEL-20160](https://issues.apache.org/jira/browse/CAMEL-20160)

Camel-AWS-Config: Create Spring Boot Starter

[CAMEL-20159](https://issues.apache.org/jira/browse/CAMEL-20159)

Camel-AWS-Config: Add Test-infra module

[CAMEL-20157](https://issues.apache.org/jira/browse/CAMEL-20157)

Add a Camel-AWS-Config component

[CAMEL-20154](https://issues.apache.org/jira/browse/CAMEL-20154)

camel-jsonpath - Make it easier to grab elements in a template like fashion

[CAMEL-20153](https://issues.apache.org/jira/browse/CAMEL-20153)

camel-jbang - Transform message command

[CAMEL-20130](https://issues.apache.org/jira/browse/CAMEL-20130)

camel-core - Creating bean from another builder bean

[CAMEL-20115](https://issues.apache.org/jira/browse/CAMEL-20115)

Support for Start Date and End Date in camel-quartz

[CAMEL-20105](https://issues.apache.org/jira/browse/CAMEL-20105)

camel-micromemter - Make it easier to configure for camel-main

[CAMEL-20056](https://issues.apache.org/jira/browse/CAMEL-20056)

camel-core - SetHeaders EIP to set multiple headers in a single EIP

[CAMEL-19723](https://issues.apache.org/jira/browse/CAMEL-19723)

camel-core - EIP - Allow convert for the header

### Task (12)

[CAMEL-20196](https://issues.apache.org/jira/browse/CAMEL-20196)

Deprecate camel-hdfs

[CAMEL-20188](https://issues.apache.org/jira/browse/CAMEL-20188)

camel-yaml-dsl - Schema has a lot of inheritErrorHandler that should be removed

[CAMEL-20163](https://issues.apache.org/jira/browse/CAMEL-20163)

Duplicated HTTP handling code

[CAMEL-20161](https://issues.apache.org/jira/browse/CAMEL-20161)

Fix usages of restricted identifiers

[CAMEL-20149](https://issues.apache.org/jira/browse/CAMEL-20149)

Release guide: Add instructions to sign and publish SBOM files to dist/release folder

[CAMEL-20135](https://issues.apache.org/jira/browse/CAMEL-20135)

A newly added EIP doesn't appear in the website

[CAMEL-20132](https://issues.apache.org/jira/browse/CAMEL-20132)

Fix incorrect logger instances

[CAMEL-20123](https://issues.apache.org/jira/browse/CAMEL-20123)

camel-test-infra: externalize container information

[CAMEL-20108](https://issues.apache.org/jira/browse/CAMEL-20108)

Update Camel examples to use Camel Case instead of deprecated kebab case

[CAMEL-20094](https://issues.apache.org/jira/browse/CAMEL-20094)

camel-catalog: camel-spring.xsd keeps being regenerated

[CAMEL-19973](https://issues.apache.org/jira/browse/CAMEL-19973)

Camel-AWS components: Revisit description

[CAMEL-19770](https://issues.apache.org/jira/browse/CAMEL-19770)

components: cleanup remaining catches of Throwables

### Test (6)

[CAMEL-20201](https://issues.apache.org/jira/browse/CAMEL-20201)

camel-mongodb - docker tests fails

[CAMEL-20200](https://issues.apache.org/jira/browse/CAMEL-20200)

camel-itests - The itests with CXF needs to be migrated from Jetty

[CAMEL-20194](https://issues.apache.org/jira/browse/CAMEL-20194)

Rename container.properties files in test-infra

[CAMEL-20175](https://issues.apache.org/jira/browse/CAMEL-20175)

camel-salesforce - Unit test error testReconnectOnErrorAfterReplayIdNonNull

[CAMEL-20158](https://issues.apache.org/jira/browse/CAMEL-20158)

camel-core - Fix Throttle tests after recent change in the EIP

[CAMEL-19809](https://issues.apache.org/jira/browse/CAMEL-19809)

camel-core: flaky tests on GitHub

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).