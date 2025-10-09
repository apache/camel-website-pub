# Apache camel 3.18.5 Release

## New and Noteworthy

This release is the new Camel 3.18.5 LTS patch release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.18.5</version>
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
      <version>3.18.5</version>
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
| [apache-camel-3.18.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.5/apache-camel-3.18.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.5/apache-camel-3.18.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.5/apache-camel-3.18.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (16)

[CAMEL-18968](https://issues.apache.org/jira/browse/CAMEL-18968)

Camel-aws2-sqs - Queue url might stay empty for the delayed queue.

[CAMEL-18871](https://issues.apache.org/jira/browse/CAMEL-18871)

camel-netty - Application does not recover (threads are WAITING) when NettyProducer pool is exhausted

[CAMEL-18842](https://issues.apache.org/jira/browse/CAMEL-18842)

camel-as2 failed to serve signed requests when compression is done before signing

[CAMEL-18835](https://issues.apache.org/jira/browse/CAMEL-18835)

camel-core-processor: OnCompletionProcessor#onFailure callback fires more than once

[CAMEL-18816](https://issues.apache.org/jira/browse/CAMEL-18816)

camel-ahc component crashes when a traffic starts too early

[CAMEL-18811](https://issues.apache.org/jira/browse/CAMEL-18811)

camel-ldap - InvalidSearchFilterException: invalid attribute description

[CAMEL-18809](https://issues.apache.org/jira/browse/CAMEL-18809)

camel-core-model: RouteDefinitionHelper should resolve the intercepted from URI which is configured with property placeholder

[CAMEL-18807](https://issues.apache.org/jira/browse/CAMEL-18807)

camel-yaml-dsl - Using method call in filter EIP not working

[CAMEL-18796](https://issues.apache.org/jira/browse/CAMEL-18796)

camel-kafka: kafka consumer stops in case of an authentication issue

[CAMEL-18795](https://issues.apache.org/jira/browse/CAMEL-18795)

camel-kafka: consumer not being closed during shutdown

[CAMEL-18782](https://issues.apache.org/jira/browse/CAMEL-18782)

Apache camel http component HTTP\_PATH header not working with toD

[CAMEL-18776](https://issues.apache.org/jira/browse/CAMEL-18776)

camel-hdfs - Fix HdfsNormalFileHandler to handle temporary file path correctly

[CAMEL-18766](https://issues.apache.org/jira/browse/CAMEL-18766)

camel-support: background tasks without maxDuration are reeschedulable

[CAMEL-18737](https://issues.apache.org/jira/browse/CAMEL-18737)

\[camel-kamelet\] parameter substitution does not work in bean instantiation when constructor or factory method is used

[CAMEL-18713](https://issues.apache.org/jira/browse/CAMEL-18713)

Loop processor interrupted when Camel engine shutdown

[CAMEL-15111](https://issues.apache.org/jira/browse/CAMEL-15111)

camel-as2 component failed to parse entity content for encrypted or compressed data

### Dependency upgrade (1)

[CAMEL-18843](https://issues.apache.org/jira/browse/CAMEL-18843)

camel-spring-boot - Upgrade to 2.7.7

### Improvement (4)

[CAMEL-18812](https://issues.apache.org/jira/browse/CAMEL-18812)

REST DSL configuration placeholder for .id() doesn't work

[CAMEL-18808](https://issues.apache.org/jira/browse/CAMEL-18808)

camel-azure-storage-blob producer doesn't use CamelAzureStorageBlobBlobSize-header

[CAMEL-18800](https://issues.apache.org/jira/browse/CAMEL-18800)

Support Camel K integration in JBang run command

[CAMEL-18797](https://issues.apache.org/jira/browse/CAMEL-18797)

camel-sql - Conditionally execute ps.getParameterMetaData() in SqlProducer populateStatement

### Task (1)

[CAMEL-18804](https://issues.apache.org/jira/browse/CAMEL-18804)

Camel-SFTP: Host key type ED25519 not supported

### Test (1)

[CAMEL-18960](https://issues.apache.org/jira/browse/CAMEL-18960)

CxfRsEndpointWithPropertiesTest is broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).