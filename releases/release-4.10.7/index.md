# Apache camel 4.10.7 Release

## New and Noteworthy

This release is the new Camel 4.10.7 release.

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
      <version>4.10.7</version>
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
      <version>4.10.7</version>
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
| [apache-camel-4.10.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-src.zip.sha512) |
| [apache-camel-4.10.7-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.xml.sha512) |
| [apache-camel-4.10.7-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.7/apache-camel-4.10.7-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-22410](https://issues.apache.org/jira/browse/CAMEL-22410)

SchedulingPollConsumer is not thread safe during graceful shutdown.

[CAMEL-22364](https://issues.apache.org/jira/browse/CAMEL-22364)

camel-jms - Rare ConcurrentModificationException on message header map when using multiple camel-jms calls after each other in route

[CAMEL-22363](https://issues.apache.org/jira/browse/CAMEL-22363)

camel-azure - EventHub consumer updates checkout on every event

[CAMEL-22359](https://issues.apache.org/jira/browse/CAMEL-22359)

camel-as2: MDN multipart/report parsing issue with no Content-Type

[CAMEL-22342](https://issues.apache.org/jira/browse/CAMEL-22342)

camel-jbang - Export using Maven GAV that has number can cause java compilation error

[CAMEL-22296](https://issues.apache.org/jira/browse/CAMEL-22296)

Rest-dsl: when openapi contract first defines both context-path and from, the endpoint does not work

[CAMEL-22294](https://issues.apache.org/jira/browse/CAMEL-22294)

camel-zipfile - decompression of multi-member archive

[CAMEL-22282](https://issues.apache.org/jira/browse/CAMEL-22282)

platform-http using spring boot won't create the producer URL correctly in case of bridged url

[CAMEL-22273](https://issues.apache.org/jira/browse/CAMEL-22273)

Google Storage Component: Content disposition header is not set correctly

[CAMEL-22264](https://issues.apache.org/jira/browse/CAMEL-22264)

camel-catalog - XPath language doesn't seem to validate

[CAMEL-22262](https://issues.apache.org/jira/browse/CAMEL-22262)

Wrong handling SftpConsumer.getRelativeFilePath and FtpConsumer.getRelativeFilePath

[CAMEL-22261](https://issues.apache.org/jira/browse/CAMEL-22261)

camel-kafka - Kafka producer should reuse existing transaction if already transacted

[CAMEL-22253](https://issues.apache.org/jira/browse/CAMEL-22253)

camel-sjms - Setting JMS delivery mode should not set via property

[CAMEL-22251](https://issues.apache.org/jira/browse/CAMEL-22251)

Incorrect Exchange status when using camel-rest

[CAMEL-22248](https://issues.apache.org/jira/browse/CAMEL-22248)

camel-jbang - Export http endpoint issue with http://@@CamelMagicValue@@

[CAMEL-22239](https://issues.apache.org/jira/browse/CAMEL-22239)

camel-catalog - Language model does not include functions

[CAMEL-22235](https://issues.apache.org/jira/browse/CAMEL-22235)

camel-smb - SmbOperations may swallow exception and can cause NPE with camel-file

[CAMEL-22229](https://issues.apache.org/jira/browse/CAMEL-22229)

camel-core - Inlined anonymous DataFormat in java based route template is not supported

[CAMEL-22217](https://issues.apache.org/jira/browse/CAMEL-22217)

camel-console: BrowseDevConsole doCallJson may throw ClassCastException

[CAMEL-22212](https://issues.apache.org/jira/browse/CAMEL-22212)

camel-smb - From smb to file with streamDownload and no stream caching

[CAMEL-22211](https://issues.apache.org/jira/browse/CAMEL-22211)

camel-smb - Always close connection and session when disconnect=true

[CAMEL-22208](https://issues.apache.org/jira/browse/CAMEL-22208)

camel-core - Stream caching spool to disk may cause OOME when low on memory

[CAMEL-22204](https://issues.apache.org/jira/browse/CAMEL-22204)

Simple expression iif does not support Strings in predicate

[CAMEL-22202](https://issues.apache.org/jira/browse/CAMEL-22202)

camel-as2 - ApplicationEntity modifies original line endings on write

[CAMEL-22198](https://issues.apache.org/jira/browse/CAMEL-22198)

camel-resilience4j - throwExceptionWhenHalfOpenOrOpenState is not always thrown if in OPEN / HALF\_OPEN state

[CAMEL-22195](https://issues.apache.org/jira/browse/CAMEL-22195)

camel-resilience4j - record exception should handle wrapped exceptions

[CAMEL-22191](https://issues.apache.org/jira/browse/CAMEL-22191)

camel-resilience4j - The option recordExceptions is configured as ignored

[CAMEL-22174](https://issues.apache.org/jira/browse/CAMEL-22174)

camel-smb : doesn't recover from TransportException if smb share disappears from network

[CAMEL-22147](https://issues.apache.org/jira/browse/CAMEL-22147)

StackOverflowError when Running a Loop with Splitter & Transaction

### Dependency upgrade (3)

[CAMEL-22394](https://issues.apache.org/jira/browse/CAMEL-22394)

camel-vertx - Upgrade to 4.5.20

[CAMEL-22343](https://issues.apache.org/jira/browse/CAMEL-22343)

camel-spring-boot - Upgrade to SB 3.4.9

[CAMEL-22275](https://issues.apache.org/jira/browse/CAMEL-22275)

camel-spring-boot - Upgrade to 3.4.8

### Improvement (5)

[CAMEL-22297](https://issues.apache.org/jira/browse/CAMEL-22297)

camel-jsonata does not support json array as input

[CAMEL-22278](https://issues.apache.org/jira/browse/CAMEL-22278)

spring-rabbitmq - producer performance

[CAMEL-22201](https://issues.apache.org/jira/browse/CAMEL-22201)

camel-core - Exchange.getClock().getCreated() should be fixed

[CAMEL-22199](https://issues.apache.org/jira/browse/CAMEL-22199)

camel-resilience4j - Add state of circuit breaker as exchange property

[CAMEL-22177](https://issues.apache.org/jira/browse/CAMEL-22177)

camel-ftp / camel-smb - Auto create starting dir - fail of not success

### Task (1)

[CAMEL-22240](https://issues.apache.org/jira/browse/CAMEL-22240)

camel-kafka - Remove camel-console dependency

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).