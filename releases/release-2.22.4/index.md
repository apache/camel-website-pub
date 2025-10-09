# Apache camel 2.22.4 Release

## New and Noteworthy

This release is a minor update of the 2.22.x branch.

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
      <version>2.22.4</version>
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
      <version>2.22.4</version>
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
| [apache-camel-2.22.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.4/apache-camel-2.22.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.4/apache-camel-2.22.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.4/apache-camel-2.22.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.22.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (19)

[CAMEL-13388](https://issues.apache.org/jira/browse/CAMEL-13388)

Wrong removing parameters logic in ServiceComponent.

[CAMEL-13387](https://issues.apache.org/jira/browse/CAMEL-13387)

camel-twitter-direct-message doesn't filter by filterOld parameter

[CAMEL-13368](https://issues.apache.org/jira/browse/CAMEL-13368)

LevelDB NPE if persistentFileName has no paths in LevelDBAggregationRepository

[CAMEL-13357](https://issues.apache.org/jira/browse/CAMEL-13357)

Regression - Namespaces defined on the SOAP envelope get lost in PAYLOAD mode

[CAMEL-13355](https://issues.apache.org/jira/browse/CAMEL-13355)

MLLP Component 'maxConcurrentConsumers' configuration is ignored

[CAMEL-13351](https://issues.apache.org/jira/browse/CAMEL-13351)

camel-netty4-http: error resolving relative path

[CAMEL-13339](https://issues.apache.org/jira/browse/CAMEL-13339)

Partition revoke implemented to save offset state using KafkaConsumer.position API results in message loss

[CAMEL-13338](https://issues.apache.org/jira/browse/CAMEL-13338)

ConsumerRebalanceListener is not registered when topicIsPattern is turned off. Causing message loss or too many duplicates

[CAMEL-13321](https://issues.apache.org/jira/browse/CAMEL-13321)

camel-twitter-direct-message doesn't use default delay of 30s

[CAMEL-13320](https://issues.apache.org/jira/browse/CAMEL-13320)

DirectMessageConsumerHandler.java \[4\] pollConsume method calls Twitter.getDirectMessages(getLastIdPaging())

[CAMEL-13319](https://issues.apache.org/jira/browse/CAMEL-13319)

TwitterConverter calls deprecated getSenderScreenName, throws UnsupportedOperationException

[CAMEL-13230](https://issues.apache.org/jira/browse/CAMEL-13230)

Error starting SQS consumer due to config option missing that's required for producer only

[CAMEL-13191](https://issues.apache.org/jira/browse/CAMEL-13191)

URISupport sanitizeUri don't hide complete password if password contains colon

[CAMEL-13171](https://issues.apache.org/jira/browse/CAMEL-13171)

camel-restdsl-swagger xml generation can't find required method allowableValues(String)

[CAMEL-13168](https://issues.apache.org/jira/browse/CAMEL-13168)

Underlying File for StreamCache gets deleted too early with direct-vm

[CAMEL-13140](https://issues.apache.org/jira/browse/CAMEL-13140)

camel-kafka - consumer does not respect auto.commit.interval.ms with AutoCommitEnabled=true

[CAMEL-13132](https://issues.apache.org/jira/browse/CAMEL-13132)

uploadBlobBlocks and commitBlobBlockList operations does not work with List

[CAMEL-13037](https://issues.apache.org/jira/browse/CAMEL-13037)

camel-cxfrs - SimpleBinding ignores annotations on interface

[CAMEL-12948](https://issues.apache.org/jira/browse/CAMEL-12948)

Camel-Box: Download file version

### Improvement (2)

[CAMEL-13344](https://issues.apache.org/jira/browse/CAMEL-13344)

camel-sql - stored procedure loaded from file/classpath should skip comment lines

[CAMEL-13150](https://issues.apache.org/jira/browse/CAMEL-13150)

Add command "exchangeProperty" for dateExpression in ExpressionBuilder

### Task (2)

[CAMEL-13169](https://issues.apache.org/jira/browse/CAMEL-13169)

c3p0 dependent version (0.9.5.2) has a security vulnerability (CVE-2018-20433)

[CAMEL-13153](https://issues.apache.org/jira/browse/CAMEL-13153)

camel-mail - Strip newlines from exchange headers

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).