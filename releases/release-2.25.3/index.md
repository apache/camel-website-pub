# Apache camel 2.25.3 Release

## New and Noteworthy

This release is the new Camel 2.25.3 patch release.

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
      <version>2.25.3</version>
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
      <version>2.25.3</version>
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
| [apache-camel-2.25.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.25.3/apache-camel-2.25.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.25.3/apache-camel-2.25.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.25.3/apache-camel-2.25.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.25.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.25.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-15962](https://issues.apache.org/jira/browse/CAMEL-15962)

mimeMultipart dataformat is not included in the XML DSL for marshal/unmarshal

[CAMEL-15891](https://issues.apache.org/jira/browse/CAMEL-15891)

camel-ahc body for String data

[CAMEL-15705](https://issues.apache.org/jira/browse/CAMEL-15705)

camel 2.x - camel-chronicle feature install failed due to xstream-java8 version

[CAMEL-15596](https://issues.apache.org/jira/browse/CAMEL-15596)

camel 2.x - camel-jacksonxml feature install failed due to stax2 version

[CAMEL-15557](https://issues.apache.org/jira/browse/CAMEL-15557)

Multicast parallel processing with timeout: Stream Cache file not deleted if CachedOutputStream created before timeout and writing to CachedOutputStream happens after timeout

[CAMEL-15532](https://issues.apache.org/jira/browse/CAMEL-15532)

Multicast parallel processing with timeout: Stream Cache file not deleted

[CAMEL-15420](https://issues.apache.org/jira/browse/CAMEL-15420)

camel-http dynamic aware removes Exchange.HTTP\_QUERY header if Exchange.HTTP\_PATH header not specified

### Improvement (4)

[CAMEL-15977](https://issues.apache.org/jira/browse/CAMEL-15977)

camel 2.x - upgrade netty to 4.1.56

[CAMEL-15976](https://issues.apache.org/jira/browse/CAMEL-15976)

camel 2.x - upgrade camel-corda

[CAMEL-15972](https://issues.apache.org/jira/browse/CAMEL-15972)

camel 2.x - Upgrade to spring boot 2.1.18

[CAMEL-15893](https://issues.apache.org/jira/browse/CAMEL-15893)

onJobExecute method of org.apache.camel.routepolicy.quartz2.ScheduledRoutePolicy should be public

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).