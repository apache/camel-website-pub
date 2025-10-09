# Apache camel 3.4.6 Release

## New and Noteworthy

This release is the new Camel 3.4.6 patch release.

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
      <version>3.4.6</version>
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
      <version>3.4.6</version>
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
| [apache-camel-3.4.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.6/apache-camel-3.4.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.6/apache-camel-3.4.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.6/apache-camel-3.4.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (4)

[CAMEL-16622](https://issues.apache.org/jira/browse/CAMEL-16622)

Validator component fails with java.lang.IllegalArgumentException: protocol = https host = null

[CAMEL-16393](https://issues.apache.org/jira/browse/CAMEL-16393)

camel-jsonpath - results from $.concat(...) seems to be cached on following calls

[CAMEL-16152](https://issues.apache.org/jira/browse/CAMEL-16152)

XML DSL tokenize with token in simple language and group does not set the delimiter correctly

[CAMEL-15928](https://issues.apache.org/jira/browse/CAMEL-15928)

TimeoutException does not trigger Resilience4j circuit breaker

### Dependency upgrade (3)

[CAMEL-16694](https://issues.apache.org/jira/browse/CAMEL-16694)

camel - Update dependencies in 3.4.x

[CAMEL-16621](https://issues.apache.org/jira/browse/CAMEL-16621)

camel-jetty - Upgrade to 9.4.39 on last Camel 3.4.x LTS release

[CAMEL-16620](https://issues.apache.org/jira/browse/CAMEL-16620)

camel-spring-boot - Upgrade to Spring Boot 2.3.10 for last Camel 3.4.x release

### New Feature (1)

[CAMEL-15428](https://issues.apache.org/jira/browse/CAMEL-15428)

Create a proper camel BOM (for camel-spring-boot)

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).