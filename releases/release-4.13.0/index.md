# Apache camel 4.13.0 Release

## New and Noteworthy

This release is the new Camel 4.13.0 release.

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
      <version>4.13.0</version>
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
      <version>4.13.0</version>
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
| [apache-camel-4.13.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-src.zip.sha512) |
| [apache-camel-4.13.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.xml.sha512) |
| [apache-camel-4.13.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.13.0/apache-camel-4.13.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.13.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.13.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (27)

[CAMEL-22217](https://issues.apache.org/jira/browse/CAMEL-22217)

camel-console: BrowseDevConsole doCallJson may throw ClassCastException

[CAMEL-22212](https://issues.apache.org/jira/browse/CAMEL-22212)

camel-smb - From smb to file with streamDownload and no stream caching

[CAMEL-22211](https://issues.apache.org/jira/browse/CAMEL-22211)

camel-smb - Always close connection and session when disconnect=true

[CAMEL-22208](https://issues.apache.org/jira/browse/CAMEL-22208)

camel-core - Stream caching spool to disk may cause OOME when low on memory

[CAMEL-22207](https://issues.apache.org/jira/browse/CAMEL-22207)

camel-jbang: camel run --runtime=quarkus does not shut down cleanly

[CAMEL-22204](https://issues.apache.org/jira/browse/CAMEL-22204)

Simple expression iif does not support Strings in predicate

[CAMEL-22202](https://issues.apache.org/jira/browse/CAMEL-22202)

camel-as2 - ApplicationEntity modifies original line endings on write

[CAMEL-22198](https://issues.apache.org/jira/browse/CAMEL-22198)

camel-resilience4j - throwExceptionWhenHalfOpenOrOpenState is not always thrown if in OPEN / HALF\_OPEN state

[CAMEL-22195](https://issues.apache.org/jira/browse/CAMEL-22195)

camel-resilience4j - record exception should handle wrapped exceptions

[CAMEL-22184](https://issues.apache.org/jira/browse/CAMEL-22184)

Camel JBang update list is broken java.lang.IndexOutOfBoundsException

[CAMEL-22176](https://issues.apache.org/jira/browse/CAMEL-22176)

High CPU Usage and Deadlock/Race Condition (?) in SimpleLRUCache after Upgrade (>4.8.2)

[CAMEL-22173](https://issues.apache.org/jira/browse/CAMEL-22173)

camel-salesforce - Checking initial replay id takes a lot of time or hangs

[CAMEL-22155](https://issues.apache.org/jira/browse/CAMEL-22155)

Detection od duplicated routeIDs might cause an issue with the inlined routes

[CAMEL-22150](https://issues.apache.org/jira/browse/CAMEL-22150)

camel-kafka - Issue with Batching: Missed Records Due to due hasExpiredRecords check

[CAMEL-22147](https://issues.apache.org/jira/browse/CAMEL-22147)

StackOverflowError when Running a Loop with Splitter & Transaction

[CAMEL-22146](https://issues.apache.org/jira/browse/CAMEL-22146)

camel-pgevent - Does not reconnect when PostgreSQL server goes down during runtime

[CAMEL-22142](https://issues.apache.org/jira/browse/CAMEL-22142)

Camel-weaviate query by vector does not work correctly

[CAMEL-22141](https://issues.apache.org/jira/browse/CAMEL-22141)

camel-jbang - camel run multiple routes with duplicate ids is not failing as intended

[CAMEL-22139](https://issues.apache.org/jira/browse/CAMEL-22139)

camel-jbang - Export to Quarkus should let property keys with their current case

[CAMEL-22134](https://issues.apache.org/jira/browse/CAMEL-22134)

camel-salesforce does not honour maxRecords nor locator

[CAMEL-22133](https://issues.apache.org/jira/browse/CAMEL-22133)

camel-platform-http-vertx: VertxPlatformHttpServer.stopVertx logic is incorrect

[CAMEL-22131](https://issues.apache.org/jira/browse/CAMEL-22131)

\[regression\] Camel JBang export is not working on Windows with Camel Jbang 4.12.0

[CAMEL-22129](https://issues.apache.org/jira/browse/CAMEL-22129)

rest-openapi contract-first no longer works when server.servlet.context-path is set

[CAMEL-22127](https://issues.apache.org/jira/browse/CAMEL-22127)

ConcurrentModificationException is coming inside Camel’s Vert.x WebSocket

[CAMEL-22117](https://issues.apache.org/jira/browse/CAMEL-22117)

camel-openapi-validator doesn't use query params or headers for validation

[CAMEL-22116](https://issues.apache.org/jira/browse/CAMEL-22116)

camel-openapi-validator doesn't work for contract-first api's with Spring Boot

[CAMEL-22073](https://issues.apache.org/jira/browse/CAMEL-22073)

camel-http - NTLM authentication doesn't work over http

### Dependency upgrade (3)

[CAMEL-22096](https://issues.apache.org/jira/browse/CAMEL-22096)

Upgrade Langchain4j to 1.0.0

[CAMEL-22072](https://issues.apache.org/jira/browse/CAMEL-22072)

camel-ai - Upgrade to langchain 1.0

[CAMEL-21429](https://issues.apache.org/jira/browse/CAMEL-21429)

camel-kafka - Upgrade to Kafka 3.9.1

### Improvement (37)

[CAMEL-22210](https://issues.apache.org/jira/browse/CAMEL-22210)

Add UUIDv4 option to simple uuid function

[CAMEL-22206](https://issues.apache.org/jira/browse/CAMEL-22206)

background tasks using BackOffTimer should be migrated to repeat task

[CAMEL-22201](https://issues.apache.org/jira/browse/CAMEL-22201)

camel-core - Exchange.getClock().getCreated() should be fixed

[CAMEL-22200](https://issues.apache.org/jira/browse/CAMEL-22200)

resource components - Make contentCache default true

[CAMEL-22199](https://issues.apache.org/jira/browse/CAMEL-22199)

camel-resilience4j - Add state of circuit breaker as exchange property

[CAMEL-22194](https://issues.apache.org/jira/browse/CAMEL-22194)

camel-freemarker - Add support for loading templates via ref|bean via ResourceLoader

[CAMEL-22190](https://issues.apache.org/jira/browse/CAMEL-22190)

Can't use language as parameter in a Kamelet

[CAMEL-22189](https://issues.apache.org/jira/browse/CAMEL-22189)

camel-support - Foreground and Background tasks make possible to manage and observe

[CAMEL-22185](https://issues.apache.org/jira/browse/CAMEL-22185)

camel-core - Beans with inlined script (such as groovy) add support for {{ }} property placeholders

[CAMEL-22181](https://issues.apache.org/jira/browse/CAMEL-22181)

camel-file/ftp - PollEnrich should allow to eager limit in case you dont need any kind of sorting

[CAMEL-22180](https://issues.apache.org/jira/browse/CAMEL-22180)

camel-simple - Using inlined jsonpath with 2-arg exp should trim so you can use space around comma

[CAMEL-22177](https://issues.apache.org/jira/browse/CAMEL-22177)

camel-ftp / camel-smb - Auto create starting dir - fail of not success

[CAMEL-22168](https://issues.apache.org/jira/browse/CAMEL-22168)

PollEnrich with FTP ignores maxMessagesPerPoll

[CAMEL-22166](https://issues.apache.org/jira/browse/CAMEL-22166)

camel-http - Also set HTTP\_RESPONSE\_CODE and HTTP\_RESPONSE\_TEXT when throw exception on failure

[CAMEL-22165](https://issues.apache.org/jira/browse/CAMEL-22165)

camel-jbang - Dependency runtime command to analyze parent poms

[CAMEL-22161](https://issues.apache.org/jira/browse/CAMEL-22161)

camel-amqp - Add brokerUrl to component level option

[CAMEL-22160](https://issues.apache.org/jira/browse/CAMEL-22160)

camel-http - Add skipControlHeaders option

[CAMEL-22145](https://issues.apache.org/jira/browse/CAMEL-22145)

camel-core - Failed to start route exception can output file location if present

[CAMEL-22136](https://issues.apache.org/jira/browse/CAMEL-22136)

camel-rest - Allow to use variables in {xxx} placeholder syntax in producer

[CAMEL-22132](https://issues.apache.org/jira/browse/CAMEL-22132)

Camel-weaviate update ignores properties and forces merge

[CAMEL-22130](https://issues.apache.org/jira/browse/CAMEL-22130)

camel-platform-http-verx - Add timeout option

[CAMEL-22126](https://issues.apache.org/jira/browse/CAMEL-22126)

camel-core - API on CamelContext to get routes by group

[CAMEL-22125](https://issues.apache.org/jira/browse/CAMEL-22125)

camel-platform-http-vertx - Writing response should favour input stream over ByteBuffer

[CAMEL-22124](https://issues.apache.org/jira/browse/CAMEL-22124)

camel-platform-http-vertx - Low default buffer size for writing streaming responses

[CAMEL-22122](https://issues.apache.org/jira/browse/CAMEL-22122)

camel-stub - No INFO about duplicates in use

[CAMEL-22121](https://issues.apache.org/jira/browse/CAMEL-22121)

rest-dsl - Open API validator improvements

[CAMEL-22119](https://issues.apache.org/jira/browse/CAMEL-22119)

camel-jbang - Remove spring and cdi JARs and detect their annotations using string names

[CAMEL-22118](https://issues.apache.org/jira/browse/CAMEL-22118)

camel-main - Cloud properties location: Optional\[@@CamelMagicValue@@\]

[CAMEL-22115](https://issues.apache.org/jira/browse/CAMEL-22115)

camel-jbang-kubernetes - Reduce number of maven dependencies

[CAMEL-22113](https://issues.apache.org/jira/browse/CAMEL-22113)

camel-as2 - Also send send file name header for PLAIN

[CAMEL-21862](https://issues.apache.org/jira/browse/CAMEL-21862)

camel-spring-boot - Remove deprecated camel.springboot. config prefix

[CAMEL-21844](https://issues.apache.org/jira/browse/CAMEL-21844)

Azure Service Bus - bridgeErrorHandler implementation

[CAMEL-21791](https://issues.apache.org/jira/browse/CAMEL-21791)

camel-kafka - Make kafka transactions more easier to use

[CAMEL-21437](https://issues.apache.org/jira/browse/CAMEL-21437)

rest-dsl - More logs in case of an invalid json object when using client request validator

[CAMEL-20018](https://issues.apache.org/jira/browse/CAMEL-20018)

camel-yaml-dsl - Remove kebab-case

[CAMEL-20015](https://issues.apache.org/jira/browse/CAMEL-20015)

camel-core: cleanup cyclic dependencies in the AbstractExchange

[CAMEL-19898](https://issues.apache.org/jira/browse/CAMEL-19898)

camel-core: investigate not attempt to convert stream caching types

### New Feature (7)

[CAMEL-22154](https://issues.apache.org/jira/browse/CAMEL-22154)

camel-core - BackOffTask make it possible to manage and observe

[CAMEL-22153](https://issues.apache.org/jira/browse/CAMEL-22153)

\[camel-micrometer-prometheus\] Add a exchanges\_last\_time metric

[CAMEL-22135](https://issues.apache.org/jira/browse/CAMEL-22135)

camel-spring-boot - Can we support timeout in platform-http

[CAMEL-22112](https://issues.apache.org/jira/browse/CAMEL-22112)

camel-jsonata - Allow running Jsonata specification from header

[CAMEL-21749](https://issues.apache.org/jira/browse/CAMEL-21749)

Camel NATS & Expanded header usage

[CAMEL-21658](https://issues.apache.org/jira/browse/CAMEL-21658)

camel-jbang - fat-jar launcher

[CAMEL-16483](https://issues.apache.org/jira/browse/CAMEL-16483)

Camel-Nats: Supports jetstream API

### Sub-task (1)

[CAMEL-22193](https://issues.apache.org/jira/browse/CAMEL-22193)

Camel-fury renamed to camel-fory: add migration note

### Task (6)

[CAMEL-22192](https://issues.apache.org/jira/browse/CAMEL-22192)

Camel-Fury: Rename the starter to Fory

[CAMEL-22186](https://issues.apache.org/jira/browse/CAMEL-22186)

Camel-azure-storage-datalake - wrong parameter in example in the \*.adoc file

[CAMEL-22183](https://issues.apache.org/jira/browse/CAMEL-22183)

camel-fury - Rename Fury to Fory

[CAMEL-22164](https://issues.apache.org/jira/browse/CAMEL-22164)

RoutesConfigurationTest in camel examples is failing

[CAMEL-22151](https://issues.apache.org/jira/browse/CAMEL-22151)

Standardize test disables based on ci.env.name

[CAMEL-22108](https://issues.apache.org/jira/browse/CAMEL-22108)

documentation - Add note in description for multivalued options

### Test (8)

[CAMEL-22159](https://issues.apache.org/jira/browse/CAMEL-22159)

FileConsumerIdempotentLoadStoreTest is failing on Windows

[CAMEL-22158](https://issues.apache.org/jira/browse/CAMEL-22158)

CamelSpringXSDValidateTest.testValidateXSD test is failing on Windows

[CAMEL-22157](https://issues.apache.org/jira/browse/CAMEL-22157)

MainPropertyPlaceholderWithEnvTest tests are failing on windows

[CAMEL-22156](https://issues.apache.org/jira/browse/CAMEL-22156)

ManagedBrowsableEndpointAsXmlFileTest and ManagedBrowsableEndpointAsJsonlFileTest are failing on Windows

[CAMEL-22148](https://issues.apache.org/jira/browse/CAMEL-22148)

An InterceptSendToEndpoint test is not working on Windows when using regex

[CAMEL-22140](https://issues.apache.org/jira/browse/CAMEL-22140)

Camel JBang export to Quarkus test is failing on Windows

[CAMEL-22138](https://issues.apache.org/jira/browse/CAMEL-22138)

Camel-JBang tests on Windows: ERROR Could not create plugin of type class org.apache.logging.log4j.core.appender.FileAppender

[CAMEL-22106](https://issues.apache.org/jira/browse/CAMEL-22106)

camel-jasypt-starter - Test failures on CSB

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).