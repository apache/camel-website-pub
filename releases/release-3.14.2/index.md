# Apache camel 3.14.2 Release

## New and Noteworthy

This release is the new Camel 3.14.2 LTS patch release.

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
      <version>3.14.2</version>
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
      <version>3.14.2</version>
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
| [apache-camel-3.14.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.2/apache-camel-3.14.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.2/apache-camel-3.14.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.2/apache-camel-3.14.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-17702](https://issues.apache.org/jira/browse/CAMEL-17702)

\[camel-google-storage\] Payload type File causes NPE on consumer

[CAMEL-17658](https://issues.apache.org/jira/browse/CAMEL-17658)

camel-core - Configuring endpoint Map options with keys with dots have trimmed keys

[CAMEL-17655](https://issues.apache.org/jira/browse/CAMEL-17655)

OpenTracing throw NPE using onCompletion definition

[CAMEL-17618](https://issues.apache.org/jira/browse/CAMEL-17618)

camel-ref: only add the endpoint into camelContext when not exist

[CAMEL-17609](https://issues.apache.org/jira/browse/CAMEL-17609)

camel-core - Problem with transacted routes

[CAMEL-17599](https://issues.apache.org/jira/browse/CAMEL-17599)

camel-jdbc - JdbcProducer leaks PreparedStatement

[CAMEL-17594](https://issues.apache.org/jira/browse/CAMEL-17594)

Try Catch WireTap OnPrepare ClassCastException

[CAMEL-17592](https://issues.apache.org/jira/browse/CAMEL-17592)

concurrentConsumers URI parameter not working with aws2-sqs endpoint

[CAMEL-17579](https://issues.apache.org/jira/browse/CAMEL-17579)

camel-core - Message DataType lost on exchange copy

[CAMEL-17577](https://issues.apache.org/jira/browse/CAMEL-17577)

Greedy flag causing consumer health check to fail

[CAMEL-17565](https://issues.apache.org/jira/browse/CAMEL-17565)

camel-jms - JmsBinding not closing the InputStream

[CAMEL-17558](https://issues.apache.org/jira/browse/CAMEL-17558)

camel-salesforce: don't complain about missing credentials with lazy login

[CAMEL-17474](https://issues.apache.org/jira/browse/CAMEL-17474)

camel-core: deadlock with multicast in a transacted context

### Dependency upgrade (2)

[CAMEL-17715](https://issues.apache.org/jira/browse/CAMEL-17715)

upgrade to spring boot 2.6.4 and 2.5.10

[CAMEL-17461](https://issues.apache.org/jira/browse/CAMEL-17461)

Migrate from commons-pool:commons-pool to org.apache.commons:commons-pool2

### Improvement (7)

[CAMEL-17713](https://issues.apache.org/jira/browse/CAMEL-17713)

CAMEL-AWS2-S3 doesn't support uploading files with custom metadata headers

[CAMEL-17708](https://issues.apache.org/jira/browse/CAMEL-17708)

camel-base-engine - Add ability to override BasePackageScanResolver initialization logic

[CAMEL-17694](https://issues.apache.org/jira/browse/CAMEL-17694)

camel-vertx-websocket: Improve handling of SEND\_TO\_ALL header

[CAMEL-17650](https://issues.apache.org/jira/browse/CAMEL-17650)

camel-vertx-websocket: sendToAll operation should consider the path WebSocket clients are connected to

[CAMEL-17646](https://issues.apache.org/jira/browse/CAMEL-17646)

camel-vertx-websocket - Server exception handler should check for cause ConnectionBase.CLOSED\_EXCEPTION

[CAMEL-17616](https://issues.apache.org/jira/browse/CAMEL-17616)

JdbcAggregationRepository will not start if it contains too many exchanges

[CAMEL-17543](https://issues.apache.org/jira/browse/CAMEL-17543)

Camel Azure Eventhubs: Support adding properties to the Event mapped from Camel Header

### New Feature (1)

[CAMEL-15951](https://issues.apache.org/jira/browse/CAMEL-15951)

Introduce configuration property to skip DescribeTable operation on start of aws2-ddb component

### Task (2)

[CAMEL-17680](https://issues.apache.org/jira/browse/CAMEL-17680)

camel-micrometer: documentation contain references to the metrics component

[CAMEL-17566](https://issues.apache.org/jira/browse/CAMEL-17566)

rest-openapi-simple of camel-spring-boot-examples is broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).