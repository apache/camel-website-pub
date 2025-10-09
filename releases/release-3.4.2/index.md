# Apache camel 3.4.2 Release

## New and Noteworthy

This release is the new Camel 3.4.2 patch release.

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
      <version>3.4.2</version>
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
      <version>3.4.2</version>
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
| [apache-camel-3.4.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.2/apache-camel-3.4.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.2/apache-camel-3.4.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.2/apache-camel-3.4.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (5)

[CAMEL-15324](https://issues.apache.org/jira/browse/CAMEL-15324)

Camel-as2 can fail on jdk8 because of java.lang.NoSuchMethodError: java.nio.CharBuffer

[CAMEL-15299](https://issues.apache.org/jira/browse/CAMEL-15299)

FTP endpoints will silently not delete/move file on disconnect

[CAMEL-15260](https://issues.apache.org/jira/browse/CAMEL-15260)

OpenTracing - camel tracer appears not to activate spans in global tracer

[CAMEL-15233](https://issues.apache.org/jira/browse/CAMEL-15233)

camel-salesforce - CometDReplayExtension does not keep replayId for each message/channel

[CAMEL-15022](https://issues.apache.org/jira/browse/CAMEL-15022)

Opentracing doesn't work with Kafka Component

### Improvement (1)

[CAMEL-15278](https://issues.apache.org/jira/browse/CAMEL-15278)

camel-bean: @Handler annotation does not work for proxied beans

### Task (1)

[CAMEL-15309](https://issues.apache.org/jira/browse/CAMEL-15309)

Camel 3.4.1 was built with JDK 11 - Use BufferCaster everywhere

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).