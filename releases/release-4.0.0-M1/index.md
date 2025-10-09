# Apache camel 4.0.0-M1 Release

## New and Noteworthy

This release is the first milestone towards the Camel 4.0.0 release.

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
      <version>4.0.0-M1</version>
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
      <version>4.0.0-M1</version>
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
| [apache-camel-4.0.0-M1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M1/apache-camel-4.0.0-M1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M1/apache-camel-4.0.0-M1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.0-M1/apache-camel-4.0.0-M1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.0-M1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.0-M1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (20)

[CAMEL-18968](https://issues.apache.org/jira/browse/CAMEL-18968)

Camel-aws2-sqs - Queue url might stay empty for the delayed queue.

[CAMEL-18959](https://issues.apache.org/jira/browse/CAMEL-18959)

camel-salesforce: deserialization failure for streaming query response gets swallowed

[CAMEL-18956](https://issues.apache.org/jira/browse/CAMEL-18956)

Camel-Jcache: It's using a bundle of javax-cache-api

[CAMEL-18953](https://issues.apache.org/jira/browse/CAMEL-18953)

camel-jetty - Should throw 504 error if continuation timeout was hit

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

[CAMEL-15111](https://issues.apache.org/jira/browse/CAMEL-15111)

camel-as2 component failed to parse entity content for encrypted or compressed data

[CAMEL-14008](https://issues.apache.org/jira/browse/CAMEL-14008)

camel-as2 - AS2 Connection can only handle one connection (connection recovery needed)

### Dependency upgrade (12)

[CAMEL-18961](https://issues.apache.org/jira/browse/CAMEL-18961)

change sun-mail to angus-mail

[CAMEL-18946](https://issues.apache.org/jira/browse/CAMEL-18946)

camel-spring-boot - Upgrade to 3.0.2

[CAMEL-18945](https://issues.apache.org/jira/browse/CAMEL-18945)

Upgrade rest assured

[CAMEL-18903](https://issues.apache.org/jira/browse/CAMEL-18903)

Upgrade swagger-core in camel-openapi-java to support jakarta namespace

[CAMEL-18888](https://issues.apache.org/jira/browse/CAMEL-18888)

Update swagger-codegen-maven-plugin to 3.0.36

[CAMEL-18887](https://issues.apache.org/jira/browse/CAMEL-18887)

camel-kotlin - Upgrade to 1.8

[CAMEL-18880](https://issues.apache.org/jira/browse/CAMEL-18880)

camel-jbang - upgrade maven-resolver-api to 1.9.4

[CAMEL-18843](https://issues.apache.org/jira/browse/CAMEL-18843)

camel-spring-boot - Upgrade to 2.7.7

[CAMEL-18830](https://issues.apache.org/jira/browse/CAMEL-18830)

camel-ehcache - Align to JAXB from camel

[CAMEL-18738](https://issues.apache.org/jira/browse/CAMEL-18738)

camel-resilience4j - Upgrade to 2.x

[CAMEL-18416](https://issues.apache.org/jira/browse/CAMEL-18416)

Upgrade to slf4j 2.0

[CAMEL-17136](https://issues.apache.org/jira/browse/CAMEL-17136)

Upgrade to Jarkarta EE APIs

### Improvement (26)

[CAMEL-18979](https://issues.apache.org/jira/browse/CAMEL-18979)

Add delimiter and prefix to the listObjects operation of AWS S3 Producer

[CAMEL-18967](https://issues.apache.org/jira/browse/CAMEL-18967)

camel-platform-http-vertx: Improve handling of whether an HTTP request body is allowed or not

[CAMEL-18952](https://issues.apache.org/jira/browse/CAMEL-18952)

camel-rest - Favour using platform-http if available on classpath

[CAMEL-18951](https://issues.apache.org/jira/browse/CAMEL-18951)

Introducing SBOM generation

[CAMEL-18942](https://issues.apache.org/jira/browse/CAMEL-18942)

openapi-rest-dsl-generator - Copy the description of the path/operation to the generated route

[CAMEL-18912](https://issues.apache.org/jira/browse/CAMEL-18912)

Sqs2ConsumerHealthCheck is broken when using injected client

[CAMEL-18877](https://issues.apache.org/jira/browse/CAMEL-18877)

camel-caffeine - Key should be string type

[CAMEL-18875](https://issues.apache.org/jira/browse/CAMEL-18875)

camel-jms - Logging less noisy when temporary reply queue is refreshed

[CAMEL-18873](https://issues.apache.org/jira/browse/CAMEL-18873)

Camel-Elasticsearch: CertificatePath should be readable through ResourceHelper

[CAMEL-18863](https://issues.apache.org/jira/browse/CAMEL-18863)

camel-pulsar - Support chunking to enable sending a large message

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

[CAMEL-18752](https://issues.apache.org/jira/browse/CAMEL-18752)

camel-micrometer - Include description in prometheus export

[CAMEL-18674](https://issues.apache.org/jira/browse/CAMEL-18674)

camel-jbang - Run in background

[CAMEL-18659](https://issues.apache.org/jira/browse/CAMEL-18659)

camel-openapi-java - Support for nullable

[CAMEL-16352](https://issues.apache.org/jira/browse/CAMEL-16352)

Generate JARS without OSGi metadata

[CAMEL-13090](https://issues.apache.org/jira/browse/CAMEL-13090)

Update to servlet api 4

### New Feature (11)

[CAMEL-18966](https://issues.apache.org/jira/browse/CAMEL-18966)

Add component for Camunda Zeebe support

[CAMEL-18940](https://issues.apache.org/jira/browse/CAMEL-18940)

camel-vertx-websocket: Support URI path and query params for WS server consumer

[CAMEL-18913](https://issues.apache.org/jira/browse/CAMEL-18913)

simple language - Add function to build a key=value string from a list

[CAMEL-18909](https://issues.apache.org/jira/browse/CAMEL-18909)

Add DTO generator option in camel-jbang generate command

[CAMEL-18823](https://issues.apache.org/jira/browse/CAMEL-18823)

Provide option to download dependencies to a specific folder with Camel JBang/camel CLI

[CAMEL-18687](https://issues.apache.org/jira/browse/CAMEL-18687)

camel-salesforce: Support Client Credentials OAuth Flow

[CAMEL-18538](https://issues.apache.org/jira/browse/CAMEL-18538)

camel-jbang - Add log command

[CAMEL-18523](https://issues.apache.org/jira/browse/CAMEL-18523)

camel-jbang - Add watch option

[CAMEL-18497](https://issues.apache.org/jira/browse/CAMEL-18497)

camel-jbang - camel run -v x.y.z

[CAMEL-17895](https://issues.apache.org/jira/browse/CAMEL-17895)

camel-vertx-websocket: Consumer as WS client

[CAMEL-5963](https://issues.apache.org/jira/browse/CAMEL-5963)

camel-smpp: Support TRX connection mode to the SMSC

### Sub-task (4)

[CAMEL-18908](https://issues.apache.org/jira/browse/CAMEL-18908)

Remove camel-jclouds

[CAMEL-18894](https://issues.apache.org/jira/browse/CAMEL-18894)

Remove camel-elasticsearch-rest in v4

[CAMEL-18891](https://issues.apache.org/jira/browse/CAMEL-18891)

Remove camel-xstream

[CAMEL-18889](https://issues.apache.org/jira/browse/CAMEL-18889)

Remove camel-rabbitmq

### Task (28)

[CAMEL-18978](https://issues.apache.org/jira/browse/CAMEL-18978)

Upgrade to atmosphere 3.0.2 - Add JSR356\_MAPPING\_PATH configuration

[CAMEL-18977](https://issues.apache.org/jira/browse/CAMEL-18977)

camel-joor - Make the code more flexible for native mode

[CAMEL-18975](https://issues.apache.org/jira/browse/CAMEL-18975)

Import sorting and code auto-formatting seems to be broken

[CAMEL-18970](https://issues.apache.org/jira/browse/CAMEL-18970)

Camel-Any23: Remove component

[CAMEL-18949](https://issues.apache.org/jira/browse/CAMEL-18949)

camel-examples - Remove examples using removed components

[CAMEL-18939](https://issues.apache.org/jira/browse/CAMEL-18939)

camel-examples - Migrate to logger 2 in v2

[CAMEL-18936](https://issues.apache.org/jira/browse/CAMEL-18936)

components - Add log4j-core so logging to logfile works

[CAMEL-18935](https://issues.apache.org/jira/browse/CAMEL-18935)

camel-jbang - Update to slf4j 2.0

[CAMEL-18934](https://issues.apache.org/jira/browse/CAMEL-18934)

camel-spring-boot - Salesforce Starter uses Jetty 9

[CAMEL-18932](https://issues.apache.org/jira/browse/CAMEL-18932)

camel-core - Upgrade to slf4j-api 2.0

[CAMEL-18929](https://issues.apache.org/jira/browse/CAMEL-18929)

camel-spring-boot - Remove deprecated components in v4

[CAMEL-18925](https://issues.apache.org/jira/browse/CAMEL-18925)

Remove camel-rest-swagger in v4

[CAMEL-18907](https://issues.apache.org/jira/browse/CAMEL-18907)

camel-datasonnet - Datasonnet is not JakartaEE compatible for v4

[CAMEL-18906](https://issues.apache.org/jira/browse/CAMEL-18906)

camel-salesforce - Uses old cometd client that uses Jetty 9.x in v4

[CAMEL-18893](https://issues.apache.org/jira/browse/CAMEL-18893)

Camel-Examples: Switch to Camel 4.x

[CAMEL-18890](https://issues.apache.org/jira/browse/CAMEL-18890)

Remove camel-vertx-kafka

[CAMEL-18884](https://issues.apache.org/jira/browse/CAMEL-18884)

camel-package-maven-plugin - Endpoint and Component DSL should skip v4 that are not migrated yet

[CAMEL-18883](https://issues.apache.org/jira/browse/CAMEL-18883)

Remove deprecated components in v4

[CAMEL-18882](https://issues.apache.org/jira/browse/CAMEL-18882)

camel-cdi - Remove in v4

[CAMEL-18881](https://issues.apache.org/jira/browse/CAMEL-18881)

Remove camel-swagger-java in v4

[CAMEL-18879](https://issues.apache.org/jira/browse/CAMEL-18879)

Remove Camel-Zipkin after deprecation

[CAMEL-18864](https://issues.apache.org/jira/browse/CAMEL-18864)

java-joor-dsl - Drop support of class files

[CAMEL-18860](https://issues.apache.org/jira/browse/CAMEL-18860)

java-joor-dsl - Adapt the code for native compilation

[CAMEL-18829](https://issues.apache.org/jira/browse/CAMEL-18829)

camel-yaml-dsl - generate-yaml-schema - Support \`additionalProperties: false\`

[CAMEL-18825](https://issues.apache.org/jira/browse/CAMEL-18825)

Make XML parser more secured out of the box

[CAMEL-18779](https://issues.apache.org/jira/browse/CAMEL-18779)

camel-test-infra: investigate replacing ActiveMQ with Artemis for embedded testing

[CAMEL-18539](https://issues.apache.org/jira/browse/CAMEL-18539)

camel-activemq: component tests depend on several deprecated artifacts

[CAMEL-14680](https://issues.apache.org/jira/browse/CAMEL-14680)

javax -> jakarta

### Test (7)

[CAMEL-18960](https://issues.apache.org/jira/browse/CAMEL-18960)

CxfRsEndpointWithPropertiesTest is broken

[CAMEL-18955](https://issues.apache.org/jira/browse/CAMEL-18955)

Fix camel-spring-boot tests after jakarta upgrade

[CAMEL-18921](https://issues.apache.org/jira/browse/CAMEL-18921)

itests jakarta upgrade: Use Artemis and JmsComponent

[CAMEL-18892](https://issues.apache.org/jira/browse/CAMEL-18892)

Restore MLLP tests

[CAMEL-18827](https://issues.apache.org/jira/browse/CAMEL-18827)

camel-kudu - Fix unit test failure with JDK 17

[CAMEL-18826](https://issues.apache.org/jira/browse/CAMEL-18826)

camel-kudu - Install libtinfo on CI to execute all Kudu's unit tests

[CAMEL-18620](https://issues.apache.org/jira/browse/CAMEL-18620)

Add redpanda container to test-infra

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).