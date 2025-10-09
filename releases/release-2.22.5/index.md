# Apache camel 2.22.5 Release

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
      <version>2.22.5</version>
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
      <version>2.22.5</version>
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
| [apache-camel-2.22.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.5/apache-camel-2.22.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.5/apache-camel-2.22.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.5/apache-camel-2.22.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.22.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (11)

[CAMEL-13587](https://issues.apache.org/jira/browse/CAMEL-13587)

InflightRepository, InflightEntry getElapsed is 0

[CAMEL-13576](https://issues.apache.org/jira/browse/CAMEL-13576)

avoid adding cxf message context map into camel exchange

[CAMEL-13541](https://issues.apache.org/jira/browse/CAMEL-13541)

Race condition in camel-hystrix when xecutionTimeoutInMilliseconds() and onFallback() are used

[CAMEL-13536](https://issues.apache.org/jira/browse/CAMEL-13536)

StackOverflow when using bean(this)

[CAMEL-13524](https://issues.apache.org/jira/browse/CAMEL-13524)

RuntimeCamelCatalog#asEndpointUri strips dash from url with toD and netty4-http

[CAMEL-13477](https://issues.apache.org/jira/browse/CAMEL-13477)

KafkaConfiguration puts truststore password into keystore password property

[CAMEL-13437](https://issues.apache.org/jira/browse/CAMEL-13437)

ThrowExceptionProcessor should use 'getConstructor' instead of 'getDeclaredConstructor', so it doesn't force users to implement the constructors of their exception classes.

[CAMEL-13428](https://issues.apache.org/jira/browse/CAMEL-13428)

camel-undertow - Response with large data gets truncated on cloud

[CAMEL-13400](https://issues.apache.org/jira/browse/CAMEL-13400)

Camel FTP Cannot list directory with 'File not found' prepending additional '/' in front of directory automatically

[CAMEL-13376](https://issues.apache.org/jira/browse/CAMEL-13376)

camel-cxf - failure processor for custom exception handling cannot get the original message

[CAMEL-12963](https://issues.apache.org/jira/browse/CAMEL-12963)

camel-salesforce-maven-plugin generates code that does not compile

### Improvement (2)

[CAMEL-13593](https://issues.apache.org/jira/browse/CAMEL-13593)

avoid “expected resource not found” warnings when using camel-mail in OSGi

[CAMEL-13527](https://issues.apache.org/jira/browse/CAMEL-13527)

Implement missing optimisation for DelimiterBasedFrameDecoder

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).