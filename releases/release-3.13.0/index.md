# Apache camel 3.13.0 Release

## New and Noteworthy

This release is the new Camel 3.13.0 minor release.

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
      <version>3.13.0</version>
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
      <version>3.13.0</version>
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
| [apache-camel-3.13.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.13.0/apache-camel-3.13.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.13.0/apache-camel-3.13.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.13.0/apache-camel-3.13.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.13.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.13.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (38)

[CAMEL-17198](https://issues.apache.org/jira/browse/CAMEL-17198)

Camel Salesforce Maven Plugin generates 'PicklistEnumConverter' imports, but that class doesn't exist

[CAMEL-17167](https://issues.apache.org/jira/browse/CAMEL-17167)

Camel-AWS2-SQS: Message attributes can be at most 10

[CAMEL-17159](https://issues.apache.org/jira/browse/CAMEL-17159)

rest-dsl - clientRequestValidation fails then operation produces more than just xml and/or json

[CAMEL-17153](https://issues.apache.org/jira/browse/CAMEL-17153)

afterprocess of UnitOfWork doesn't work properly

[CAMEL-17151](https://issues.apache.org/jira/browse/CAMEL-17151)

camel-openapi-java - Double slashes in api-doc

[CAMEL-17135](https://issues.apache.org/jira/browse/CAMEL-17135)

camel-debezium-mongodb-starter does not pupulate values from application.properties

[CAMEL-17128](https://issues.apache.org/jira/browse/CAMEL-17128)

MLLP charset is no longer overridable from the HL7 message MSH 18

[CAMEL-17124](https://issues.apache.org/jira/browse/CAMEL-17124)

HttpRestHeaderFilterStrategy doesn't filter queryParameter headers

[CAMEL-17114](https://issues.apache.org/jira/browse/CAMEL-17114)

camel-jslt cannot load files from classpath in quarkus dev-mode

[CAMEL-17109](https://issues.apache.org/jira/browse/CAMEL-17109)

camel-azure dependency bom causes conflicting dependencies to be downloaded

[CAMEL-17105](https://issues.apache.org/jira/browse/CAMEL-17105)

Transactions - Ignored property Exchange.markRollbackOnlyLast

[CAMEL-17095](https://issues.apache.org/jira/browse/CAMEL-17095)

camel-resilience4j - Using timeout and bulkhead together does not work

[CAMEL-17090](https://issues.apache.org/jira/browse/CAMEL-17090)

ClusteredRoutePolicy get locked on leader change

[CAMEL-17075](https://issues.apache.org/jira/browse/CAMEL-17075)

DatasonnetBuilder (and SimpleBuilder) does initialization in evaluate() which can cause issues under load

[CAMEL-17074](https://issues.apache.org/jira/browse/CAMEL-17074)

camel-spring-main - Camel from Spring XML has its own pre configuration that camel-main should not override

[CAMEL-17073](https://issues.apache.org/jira/browse/CAMEL-17073)

camel-core - Incorrect Simple expression behavior when cache enabled

[CAMEL-17068](https://issues.apache.org/jira/browse/CAMEL-17068)

FileLockClusterView doesn't work with CIFS

[CAMEL-17067](https://issues.apache.org/jira/browse/CAMEL-17067)

Datasonnet header can't be used to set bodyMediaType

[CAMEL-17065](https://issues.apache.org/jira/browse/CAMEL-17065)

The cluster view is not released on all routes stop, autoStartup flag is ignored.

[CAMEL-17060](https://issues.apache.org/jira/browse/CAMEL-17060)

camel-openapi-java - The rest api can fail due to two unknown properties on endpoint

[CAMEL-17055](https://issues.apache.org/jira/browse/CAMEL-17055)

Duplication options in json metadata in hazelcast spring boot starter

[CAMEL-17049](https://issues.apache.org/jira/browse/CAMEL-17049)

authUsername and authPassword parameters not passed to the underlaying endpoint

[CAMEL-17048](https://issues.apache.org/jira/browse/CAMEL-17048)

Exchange header null after upgrading to 3.12 from 3.11.2 when using transacted

[CAMEL-17046](https://issues.apache.org/jira/browse/CAMEL-17046)

camel-datasonnet - Datasonnet methods bodyMediaType and outputMediaType is missing in Java DSL

[CAMEL-17043](https://issues.apache.org/jira/browse/CAMEL-17043)

camel-rest-openapi - Endpoint query parameters not forwarded to underlaying component endpoint

[CAMEL-17039](https://issues.apache.org/jira/browse/CAMEL-17039)

Camel-AWS2-S3: When includeBody is false, the message Body should not be set

[CAMEL-17034](https://issues.apache.org/jira/browse/CAMEL-17034)

Camel-Github: StartingSha should be an URI param and not an URI path

[CAMEL-17018](https://issues.apache.org/jira/browse/CAMEL-17018)

camel-jbang: pre-processing dependencies variables is not reliable

[CAMEL-17017](https://issues.apache.org/jira/browse/CAMEL-17017)

camel-metrics - Cannot be used out of the box due to mixed jackson JARs

[CAMEL-17016](https://issues.apache.org/jira/browse/CAMEL-17016)

camel-leveldb - Error starting aggregation repository

[CAMEL-17015](https://issues.apache.org/jira/browse/CAMEL-17015)

camel-servlet - Issue with REST Service after Camel update - custom servletName does not work

[CAMEL-17012](https://issues.apache.org/jira/browse/CAMEL-17012)

camel-aws2-lambda: ListAliases unduly return "Function Version must be specified to list aliases for a function"

[CAMEL-17011](https://issues.apache.org/jira/browse/CAMEL-17011)

camel-ssh - The producer should not be singleton

[CAMEL-17009](https://issues.apache.org/jira/browse/CAMEL-17009)

camel-core - Camel does not clear MDC correctly

[CAMEL-16938](https://issues.apache.org/jira/browse/CAMEL-16938)

StackOverflowError in RedeliveryErrorHandler when using transacted

[CAMEL-16934](https://issues.apache.org/jira/browse/CAMEL-16934)

apiContextIdListing option does not work in camel-openapi-java

[CAMEL-16916](https://issues.apache.org/jira/browse/CAMEL-16916)

camel split with parallel processing true consumes lots of heap space when using camel-ftp

[CAMEL-15723](https://issues.apache.org/jira/browse/CAMEL-15723)

NPE when using PostgresAggregationRepository

### Dependency upgrade (10)

[CAMEL-17164](https://issues.apache.org/jira/browse/CAMEL-17164)

camel-ssh - Upgrade to SSHD 2.7.0

[CAMEL-17123](https://issues.apache.org/jira/browse/CAMEL-17123)

Upgrade to Spring Boot 2.5.6

[CAMEL-17098](https://issues.apache.org/jira/browse/CAMEL-17098)

Upgrade to CXF 3.4.5

[CAMEL-17089](https://issues.apache.org/jira/browse/CAMEL-17089)

camel-grpc - Upgrade to 1.41.0

[CAMEL-17082](https://issues.apache.org/jira/browse/CAMEL-17082)

camel-kubernetes - Upgrade to 5.9.x

[CAMEL-17071](https://issues.apache.org/jira/browse/CAMEL-17071)

camel-openapi-java - Upgrade to apicurio 1.1.x

[CAMEL-17053](https://issues.apache.org/jira/browse/CAMEL-17053)

Upgrade to Jandex 2.4.1

[CAMEL-17047](https://issues.apache.org/jira/browse/CAMEL-17047)

camel-karaf - upgrade aries proxy version to 1.1.11 to support JDK11+

[CAMEL-17044](https://issues.apache.org/jira/browse/CAMEL-17044)

camel-debezium - Upgrade to 1.7

[CAMEL-17000](https://issues.apache.org/jira/browse/CAMEL-17000)

Upgrade to junit 5.8.x

### Improvement (45)

[CAMEL-17172](https://issues.apache.org/jira/browse/CAMEL-17172)

camel-jetty and http server components - Mute exception configurable on component level

[CAMEL-17170](https://issues.apache.org/jira/browse/CAMEL-17170)

Aggregate EIP - pre completion should have access to correlation key

[CAMEL-17168](https://issues.apache.org/jira/browse/CAMEL-17168)

camel-health - Route health check with consumer should be DOWN until first poll executed

[CAMEL-17166](https://issues.apache.org/jira/browse/CAMEL-17166)

camel-jetty and http server components - Return empty body on error code 500 when muteException is enabled

[CAMEL-17156](https://issues.apache.org/jira/browse/CAMEL-17156)

camel-aws - Cancelling "Extending visibility window" while processing completed causes interruption exception

[CAMEL-17152](https://issues.apache.org/jira/browse/CAMEL-17152)

camel-core - Model json should output enum values in their ordinal order

[CAMEL-17145](https://issues.apache.org/jira/browse/CAMEL-17145)

camel-salesforce: Upsert should return UpsertSObjectResult

[CAMEL-17143](https://issues.apache.org/jira/browse/CAMEL-17143)

camel-health - Add success threshold

[CAMEL-17140](https://issues.apache.org/jira/browse/CAMEL-17140)

camel-core - Make it easier to get a route health-check by route id

[CAMEL-17138](https://issues.apache.org/jira/browse/CAMEL-17138)

Propagate error details from Camel health to MicroProfile Health

[CAMEL-17127](https://issues.apache.org/jira/browse/CAMEL-17127)

camel-salesforce - Default Bulk API V2 client does not allow locator and maxRecords query param to be added for get query results endpoint.

[CAMEL-17126](https://issues.apache.org/jira/browse/CAMEL-17126)

camel-restdsl plugin doesn't implement parameter clientRequestValidation

[CAMEL-17125](https://issues.apache.org/jira/browse/CAMEL-17125)

camel-salesforce: Improve support for polymorphic relationship queries

[CAMEL-17122](https://issues.apache.org/jira/browse/CAMEL-17122)

camel-mllp - Generate configurer for reflection free configuration

[CAMEL-17119](https://issues.apache.org/jira/browse/CAMEL-17119)

Camel-MLLP: add the option to close gracefully the socket when idleTimeout occurs

[CAMEL-17116](https://issues.apache.org/jira/browse/CAMEL-17116)

components - Loading resource from classpath should use ClassResolver API

[CAMEL-17112](https://issues.apache.org/jira/browse/CAMEL-17112)

camel-core - The starting counter for thread name should be 1

[CAMEL-17108](https://issues.apache.org/jira/browse/CAMEL-17108)

camel-couchdb: investigate adding resume strategy

[CAMEL-17102](https://issues.apache.org/jira/browse/CAMEL-17102)

camel-core - Events for CamelContextInitializingEvent and CamelContextInitializedEvent should emit eager

[CAMEL-17101](https://issues.apache.org/jira/browse/CAMEL-17101)

camel-core - Split EIP should be able to split a Map out of the box

[CAMEL-17081](https://issues.apache.org/jira/browse/CAMEL-17081)

Upgrade Infinispan to 13.0.0

[CAMEL-17080](https://issues.apache.org/jira/browse/CAMEL-17080)

camel-salesforce - Raw mode should store json payload directly

[CAMEL-17079](https://issues.apache.org/jira/browse/CAMEL-17079)

camel-core - Avoid using SimpleBuilder to make simple expressions similar to others

[CAMEL-17078](https://issues.apache.org/jira/browse/CAMEL-17078)

camel-file: add support for the resume from offset strategy

[CAMEL-17077](https://issues.apache.org/jira/browse/CAMEL-17077)

camel-aws-secret - Fix syntax in endpoint to be without slashes

[CAMEL-17070](https://issues.apache.org/jira/browse/CAMEL-17070)

Default values for duration type should be in numeric value to be more tooling friendly

[CAMEL-17069](https://issues.apache.org/jira/browse/CAMEL-17069)

openapi-rest-dsl-generator should not depend on camel-core

[CAMEL-17063](https://issues.apache.org/jira/browse/CAMEL-17063)

camel-openapi-java - Generated api-doc must use contextPath rest configuration

[CAMEL-17059](https://issues.apache.org/jira/browse/CAMEL-17059)

camel-file: benchmark and optimize the file component for large data sets

[CAMEL-17056](https://issues.apache.org/jira/browse/CAMEL-17056)

camel-spring-boot-hazelcast-starter - Remove the old customer code as its standard in camel-core now

[CAMEL-17045](https://issues.apache.org/jira/browse/CAMEL-17045)

camel-file: add support for the resume strategy

[CAMEL-17036](https://issues.apache.org/jira/browse/CAMEL-17036)

camel-salesforce: body should be preserved in some cases

[CAMEL-17035](https://issues.apache.org/jira/browse/CAMEL-17035)

camel-core - Rest DSL - Allow to set response message quickly

[CAMEL-17033](https://issues.apache.org/jira/browse/CAMEL-17033)

camel-core - ManagementStartegy - Optimize event notifiers

[CAMEL-17031](https://issues.apache.org/jira/browse/CAMEL-17031)

Performances/Profiling: Avoid boolean allocation in EventHelper

[CAMEL-17030](https://issues.apache.org/jira/browse/CAMEL-17030)

camel-ftp - Disconnect should ignore any kind of exception

[CAMEL-17029](https://issues.apache.org/jira/browse/CAMEL-17029)

camel-aws-s3 - File message body optimize in putObject

[CAMEL-17024](https://issues.apache.org/jira/browse/CAMEL-17024)

camel-aws-s3 - Determine content-length in a smarter way

[CAMEL-17023](https://issues.apache.org/jira/browse/CAMEL-17023)

Do not bundle Atlasmap DFDL module

[CAMEL-17022](https://issues.apache.org/jira/browse/CAMEL-17022)

camel-mina - MinaProducer does not disconnect on timeouts

[CAMEL-17021](https://issues.apache.org/jira/browse/CAMEL-17021)

camel-minio - Determine content-length in a smarter way

[CAMEL-17020](https://issues.apache.org/jira/browse/CAMEL-17020)

camel-restdsl plugins doesn't implement all documented parameters for xml and yaml

[CAMEL-16946](https://issues.apache.org/jira/browse/CAMEL-16946)

Add feature for bean validator to validate all elements if body is of type Iterable

[CAMEL-16706](https://issues.apache.org/jira/browse/CAMEL-16706)

camel-core - FactoryFinder create new instance of implementation class non reflective

[CAMEL-16646](https://issues.apache.org/jira/browse/CAMEL-16646)

camel-karaf - Missing the camel-aws2 OSGi deployment support in features.xml

### New Feature (14)

[CAMEL-17150](https://issues.apache.org/jira/browse/CAMEL-17150)

camel-yaml-dsl - Should be able to load camel-k yaml file

[CAMEL-17149](https://issues.apache.org/jira/browse/CAMEL-17149)

camel-main - Binding beans should allow to refer to other beans in the constructor parameters

[CAMEL-17133](https://issues.apache.org/jira/browse/CAMEL-17133)

camel-quartz: allow missfire execution for cron triggers

[CAMEL-17104](https://issues.apache.org/jira/browse/CAMEL-17104)

Support object download in Huaweicloud OBS component via producer mode

[CAMEL-17103](https://issues.apache.org/jira/browse/CAMEL-17103)

Support object upload to Huaweicloud OBS bucket in producer mode

[CAMEL-17096](https://issues.apache.org/jira/browse/CAMEL-17096)

camel-kafka - Add async commit support

[CAMEL-17072](https://issues.apache.org/jira/browse/CAMEL-17072)

camel-core - Allow to enable tracing in standby mode

[CAMEL-17061](https://issues.apache.org/jira/browse/CAMEL-17061)

camel-openapi-java - Support springdoc when running on Spring Boot

[CAMEL-17054](https://issues.apache.org/jira/browse/CAMEL-17054)

camel-nats - Support headers in nats consumer/producer

[CAMEL-17041](https://issues.apache.org/jira/browse/CAMEL-17041)

camel-jpa - Allow to configure alias for entity type class names

[CAMEL-17037](https://issues.apache.org/jira/browse/CAMEL-17037)

camel-ftp chmodDirectory in SFTP component

[CAMEL-16975](https://issues.apache.org/jira/browse/CAMEL-16975)

Components should be able to provide custom HealthCheck

[CAMEL-16612](https://issues.apache.org/jira/browse/CAMEL-16612)

camel-kamelet - Run with jbang

[CAMEL-15714](https://issues.apache.org/jira/browse/CAMEL-15714)

camel-karaf - Add camel-aws2-s3 feature

### Sub-task (1)

[CAMEL-16952](https://issues.apache.org/jira/browse/CAMEL-16952)

Improve documentation about testing with camel-spring-boot

### Task (8)

[CAMEL-17169](https://issues.apache.org/jira/browse/CAMEL-17169)

Three copies of same-named attribute in generated spring-boot.json file

[CAMEL-17146](https://issues.apache.org/jira/browse/CAMEL-17146)

SprintBoot pprovider of Catalog declares crypto-cms as a component but definition is missing

[CAMEL-17113](https://issues.apache.org/jira/browse/CAMEL-17113)

Camel-Website: for 3.12.x and 3.13.x the default value are not showing up for components

[CAMEL-17052](https://issues.apache.org/jira/browse/CAMEL-17052)

Azure BOM import forces incorrect Netty dependency version

[CAMEL-17042](https://issues.apache.org/jira/browse/CAMEL-17042)

upgrade to maven wrapper 3.8.3

[CAMEL-16945](https://issues.apache.org/jira/browse/CAMEL-16945)

Convert tests in camel-spring-boot to Junit 5

[CAMEL-16467](https://issues.apache.org/jira/browse/CAMEL-16467)

Camel-Examples: Group the example for grouped componets in a middle folder

[CAMEL-13804](https://issues.apache.org/jira/browse/CAMEL-13804)

website - Add page which lists which components supports which runtimes

### Test (2)

[CAMEL-17163](https://issues.apache.org/jira/browse/CAMEL-17163)

camel-ftp - Upgrade to SSHD 2.7.x

[CAMEL-17155](https://issues.apache.org/jira/browse/CAMEL-17155)

camel-openapi-java - Run tests in parallel to speedup testing

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).