# Apache camel 3.21.5 Release

## New and Noteworthy

This release is the new Camel 3.21.5 LTS patch release.

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
      <version>3.21.5</version>
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
      <version>3.21.5</version>
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
| [apache-camel-3.21.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-src.zip.sha512) |
| [apache-camel-3.21.5-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.xml.sha512) |
| [apache-camel-3.21.5-sbom.json](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.21.5/apache-camel-3.21.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-3.21.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.21.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-20864](https://issues.apache.org/jira/browse/CAMEL-20864)

camel-kafka - With confluent schema registry does not work properly.

[CAMEL-20677](https://issues.apache.org/jira/browse/CAMEL-20677)

camel-hazelcast: Seda nested transactions are not allowed

[CAMEL-20630](https://issues.apache.org/jira/browse/CAMEL-20630)

CVE-2024-25710, CVE-2024-26308 - Vulnerabilities with Camel-zip-deflater-starter maven dependency

[CAMEL-20563](https://issues.apache.org/jira/browse/CAMEL-20563)

camel-kafka - breakOnFirstError causes thread and memory leaks

[CAMEL-20558](https://issues.apache.org/jira/browse/CAMEL-20558)

Ability to use the old Micrometer meter names does not work on MicrometerExchangeEventNotifier

[CAMEL-20549](https://issues.apache.org/jira/browse/CAMEL-20549)

camel-kafka - Using sslKeystoreType should work with PEM

[CAMEL-20521](https://issues.apache.org/jira/browse/CAMEL-20521)

camel-amqp - AMQP publisher application is losing messages with local JMS transaction enabled

[CAMEL-20457](https://issues.apache.org/jira/browse/CAMEL-20457)

camel-core - NullPointerException for Split parallel and timeout without AggregationStrategy

[CAMEL-20435](https://issues.apache.org/jira/browse/CAMEL-20435)

camel-core - Resequencer EIP cannot be started again after being stopped

[CAMEL-20388](https://issues.apache.org/jira/browse/CAMEL-20388)

Salesforce component does not handshake on the connection failure

[CAMEL-20372](https://issues.apache.org/jira/browse/CAMEL-20372)

kafka Consumer - fix for config maxPollIntervalMs configuration in 3.21.x and 3.22.x

[CAMEL-20356](https://issues.apache.org/jira/browse/CAMEL-20356)

camel-core - LoggerHelper returns wrong name for source code line precise

[CAMEL-20350](https://issues.apache.org/jira/browse/CAMEL-20350)

camel-observation - Null values should be null instead of a string null literal value

### Improvement (4)

[CAMEL-20627](https://issues.apache.org/jira/browse/CAMEL-20627)

camel-cdi - remove deprecated fireEvent method

[CAMEL-20590](https://issues.apache.org/jira/browse/CAMEL-20590)

Delay to execute timeout to Camel RabbitMQ (InOut)

[CAMEL-20495](https://issues.apache.org/jira/browse/CAMEL-20495)

camel-jsonpath - ResultType List should store single element into a List so it can be used afterwards with Split EIP

[CAMEL-20363](https://issues.apache.org/jira/browse/CAMEL-20363)

camel-jms - Make getting JMSCorrelationID more robust for brokers that has bugs

### Task (1)

[CAMEL-19229](https://issues.apache.org/jira/browse/CAMEL-19229)

camel-tarfile: Common compress 1.23 is causing test failures

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).