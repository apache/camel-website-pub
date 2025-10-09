# Apache camel 2.25.2 Release

## New and Noteworthy

This release is the new Camel 2.25.2 patch release.

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
      <version>2.25.2</version>
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
      <version>2.25.2</version>
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
| [apache-camel-2.25.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.25.2/apache-camel-2.25.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.25.2/apache-camel-2.25.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.25.2/apache-camel-2.25.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.25.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.25.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (6)

[CAMEL-16177](https://issues.apache.org/jira/browse/CAMEL-16177)

File stream cache problem with multicast parallel processing and encrypted stream

[CAMEL-15233](https://issues.apache.org/jira/browse/CAMEL-15233)

camel-salesforce - CometDReplayExtension does not keep replayId for each message/channel

[CAMEL-15174](https://issues.apache.org/jira/browse/CAMEL-15174)

need to set SpringBus to CxfRsSpringEndpoint

[CAMEL-15022](https://issues.apache.org/jira/browse/CAMEL-15022)

Opentracing doesn't work with Kafka Component

[CAMEL-14935](https://issues.apache.org/jira/browse/CAMEL-14935)

KafkaConsumer commits old offset values in a failure scenario causing message replays and offset reset error

[CAMEL-14533](https://issues.apache.org/jira/browse/CAMEL-14533)

camel-ftp: fileExist=Append and tempPrefix options do not work together

### Improvement (8)

[CAMEL-15377](https://issues.apache.org/jira/browse/CAMEL-15377)

camel-jms - Add back transactedInOut option

[CAMEL-15188](https://issues.apache.org/jira/browse/CAMEL-15188)

camel-telegram - Add SOCKS proxy support to telegram component

[CAMEL-15061](https://issues.apache.org/jira/browse/CAMEL-15061)

Performance issues with classMap.computeIfAbsent() in DefaultFactoryFinder

[CAMEL-15050](https://issues.apache.org/jira/browse/CAMEL-15050)

Templating components - Variable map to be limited to body/headers

[CAMEL-15013](https://issues.apache.org/jira/browse/CAMEL-15013)

Template components - Add option to turn on|off allow using header with override template

[CAMEL-14951](https://issues.apache.org/jira/browse/CAMEL-14951)

WireTap - If thread pool reject task then Camel error handler should be able to react

[CAMEL-14893](https://issues.apache.org/jira/browse/CAMEL-14893)

camel-grpc - Should handle if exchange failed as onError

[CAMEL-7810](https://issues.apache.org/jira/browse/CAMEL-7810)

Dropped exchanges when aggregating with JdbcAggregationRepository

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).