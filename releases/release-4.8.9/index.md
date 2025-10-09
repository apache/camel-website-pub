# Apache camel 4.8.9 Release

## New and Noteworthy

This release is the new Camel 4.8.9 release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.8.9</version>
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
      <version>4.8.9</version>
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
| [apache-camel-4.8.9-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-src.zip.sha512) |
| [apache-camel-4.8.9-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.xml.sha512) |
| [apache-camel-4.8.9-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.9/apache-camel-4.8.9-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.9` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.9

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (12)

[CAMEL-22364](https://issues.apache.org/jira/browse/CAMEL-22364)

camel-jms - Rare ConcurrentModificationException on message header map when using multiple camel-jms calls after each other in route

[CAMEL-22359](https://issues.apache.org/jira/browse/CAMEL-22359)

camel-as2: MDN multipart/report parsing issue with no Content-Type

[CAMEL-22273](https://issues.apache.org/jira/browse/CAMEL-22273)

Google Storage Component: Content disposition header is not set correctly

[CAMEL-22253](https://issues.apache.org/jira/browse/CAMEL-22253)

camel-sjms - Setting JMS delivery mode should not set via property

[CAMEL-22251](https://issues.apache.org/jira/browse/CAMEL-22251)

Incorrect Exchange status when using camel-rest

[CAMEL-22248](https://issues.apache.org/jira/browse/CAMEL-22248)

camel-jbang - Export http endpoint issue with http://@@CamelMagicValue@@

[CAMEL-22239](https://issues.apache.org/jira/browse/CAMEL-22239)

camel-catalog - Language model does not include functions

[CAMEL-22208](https://issues.apache.org/jira/browse/CAMEL-22208)

camel-core - Stream caching spool to disk may cause OOME when low on memory

[CAMEL-22198](https://issues.apache.org/jira/browse/CAMEL-22198)

camel-resilience4j - throwExceptionWhenHalfOpenOrOpenState is not always thrown if in OPEN / HALF\_OPEN state

[CAMEL-22195](https://issues.apache.org/jira/browse/CAMEL-22195)

camel-resilience4j - record exception should handle wrapped exceptions

[CAMEL-22191](https://issues.apache.org/jira/browse/CAMEL-22191)

camel-resilience4j - The option recordExceptions is configured as ignored

[CAMEL-22147](https://issues.apache.org/jira/browse/CAMEL-22147)

StackOverflowError when Running a Loop with Splitter & Transaction

### Improvement (2)

[CAMEL-22297](https://issues.apache.org/jira/browse/CAMEL-22297)

camel-jsonata does not support json array as input

[CAMEL-22199](https://issues.apache.org/jira/browse/CAMEL-22199)

camel-resilience4j - Add state of circuit breaker as exchange property

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).