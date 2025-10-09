# Apache camel 3.20.1 Release

## New and Noteworthy

This release is the new Camel 3.20.1 LTS patch release.

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
      <version>3.20.1</version>
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
      <version>3.20.1</version>
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
| [apache-camel-3.20.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.1/apache-camel-3.20.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.1/apache-camel-3.20.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.1/apache-camel-3.20.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-18844](https://issues.apache.org/jira/browse/CAMEL-18844)

Possible memory leak in org.apache.camel.impl.console.EventConsole

[CAMEL-18842](https://issues.apache.org/jira/browse/CAMEL-18842)

camel-as2 failed to serve signed requests when compression is done before signing

[CAMEL-18841](https://issues.apache.org/jira/browse/CAMEL-18841)

camel-kafka: producer idempotence is not enabled by default

[CAMEL-18840](https://issues.apache.org/jira/browse/CAMEL-18840)

camel-http - HTTP broken followRedirection

[CAMEL-18835](https://issues.apache.org/jira/browse/CAMEL-18835)

camel-core-processor: OnCompletionProcessor#onFailure callback fires more than once

[CAMEL-18834](https://issues.apache.org/jira/browse/CAMEL-18834)

camel-core - StringQuoteHelper should remove quotes for single element

[CAMEL-15111](https://issues.apache.org/jira/browse/CAMEL-15111)

camel-as2 component failed to parse entity content for encrypted or compressed data

### Dependency upgrade (1)

[CAMEL-18843](https://issues.apache.org/jira/browse/CAMEL-18843)

camel-spring-boot - Upgrade to 2.7.7

### Improvement (6)

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

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).