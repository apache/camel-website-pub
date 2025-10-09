# Apache camel 3.7.7 Release

## New and Noteworthy

This release is the new Camel 3.7.7 LTS release.

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
      <version>3.7.7</version>
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
      <version>3.7.7</version>
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
| [apache-camel-3.7.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.7/apache-camel-3.7.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.7/apache-camel-3.7.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.7/apache-camel-3.7.7-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-17181](https://issues.apache.org/jira/browse/CAMEL-17181)

camel-core - XPathBuilder never clears pool when using @XPath annotation and grows pool causing memory leak

[CAMEL-17073](https://issues.apache.org/jira/browse/CAMEL-17073)

camel-core - Incorrect Simple expression behavior when cache enabled

[CAMEL-17015](https://issues.apache.org/jira/browse/CAMEL-17015)

camel-servlet - Issue with REST Service after Camel update - custom servletName does not work

### Dependency upgrade (4)

[CAMEL-17335](https://issues.apache.org/jira/browse/CAMEL-17335)

upgrade to logback 1.2.8

[CAMEL-17327](https://issues.apache.org/jira/browse/CAMEL-17327)

Upgrade to log4j 2.16.0

[CAMEL-17324](https://issues.apache.org/jira/browse/CAMEL-17324)

camel-nsq and camel-corda - Exclude log4j-core

[CAMEL-17309](https://issues.apache.org/jira/browse/CAMEL-17309)

upgrade to log4j 2.15.0

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).