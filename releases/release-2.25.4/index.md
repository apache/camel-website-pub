# Apache camel 2.25.4 Release

## New and Noteworthy

This release is the new Camel 2.25.4 patch release.

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
      <version>2.25.4</version>
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
      <version>2.25.4</version>
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
| [apache-camel-2.25.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.25.4/apache-camel-2.25.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.25.4/apache-camel-2.25.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.25.4/apache-camel-2.25.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.25.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.25.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-16622](https://issues.apache.org/jira/browse/CAMEL-16622)

Validator component fails with java.lang.IllegalArgumentException: protocol = https host = null

[CAMEL-16428](https://issues.apache.org/jira/browse/CAMEL-16428)

camel-maven-plugin failing on Camel 2.25.x

[CAMEL-16393](https://issues.apache.org/jira/browse/CAMEL-16393)

camel-jsonpath - results from $.concat(...) seems to be cached on following calls

[CAMEL-16291](https://issues.apache.org/jira/browse/CAMEL-16291)

camel-cxfrs producer shouldn't try to read Entity from javax.ws.rs.core.Response

[CAMEL-16063](https://issues.apache.org/jira/browse/CAMEL-16063)

should consider multiple ApplicationContext instances when specifying another management.server.port

[CAMEL-15974](https://issues.apache.org/jira/browse/CAMEL-15974)

HttpSendDynamicAware doesn't resolve RAW properties

[CAMEL-15971](https://issues.apache.org/jira/browse/CAMEL-15971)

SimpleFileLanguage always null due to DummyExchange

### Dependency upgrade (3)

[CAMEL-17327](https://issues.apache.org/jira/browse/CAMEL-17327)

Upgrade to log4j 2.16.0

[CAMEL-16626](https://issues.apache.org/jira/browse/CAMEL-16626)

camel 2.25.x - Upgrade to newer 3rd party dependencies

[CAMEL-16031](https://issues.apache.org/jira/browse/CAMEL-16031)

camel 2.x - upgrade to latest Groovy (2.5.14)

### Improvement (1)

[CAMEL-16533](https://issues.apache.org/jira/browse/CAMEL-16533)

camel-spring - XML DSL include more documentation in XSD

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).