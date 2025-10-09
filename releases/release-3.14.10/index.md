# Apache camel 3.14.10 Release

## New and Noteworthy

This release is the new Camel 3.14.10 LTS patch release.

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
      <version>3.14.10</version>
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
      <version>3.14.10</version>
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
| [apache-camel-3.14.10-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.10/apache-camel-3.14.10-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.10/apache-camel-3.14.10-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.10/apache-camel-3.14.10-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.10` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.10

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-19870](https://issues.apache.org/jira/browse/CAMEL-19870)

Camel AS2: Should accept MDN field name Disposition as case insensitive

[CAMEL-19758](https://issues.apache.org/jira/browse/CAMEL-19758)

netty-http in proxy mode generates IllegalReferenceCountException for every success request.

[CAMEL-19671](https://issues.apache.org/jira/browse/CAMEL-19671)

camel-sql - Calling sql query without parameters in Oracle with jdbc driver 23.2.0.0

[CAMEL-19650](https://issues.apache.org/jira/browse/CAMEL-19650)

Camel Kafka doesn't honor 'workerPool' configuration

[CAMEL-19575](https://issues.apache.org/jira/browse/CAMEL-19575)

camel-rabbitmq - RabbitMQConsumer keeps on consuming even when route shutdown is triggered.

[CAMEL-19498](https://issues.apache.org/jira/browse/CAMEL-19498)

camel-core / camel-ftp - memory leak in MultiplePool when using pollEnrich EIP

[CAMEL-19476](https://issues.apache.org/jira/browse/CAMEL-19476)

rest-dsl - ClientRequestValidation accepted content-type may not validate correctly

### Dependency upgrade (3)

[CAMEL-20049](https://issues.apache.org/jira/browse/CAMEL-20049)

camel-activemq - Upgrade to latest releases

[CAMEL-19891](https://issues.apache.org/jira/browse/CAMEL-19891)

Update Apache CXF versions to mitigate CVE-2022-46364 and CVE-2022-46363

[CAMEL-19480](https://issues.apache.org/jira/browse/CAMEL-19480)

camel-netty - Upgrade to 4.1.94

### Improvement (2)

[CAMEL-19615](https://issues.apache.org/jira/browse/CAMEL-19615)

camel-ftp: chmodDirectory option try for each junk to change the directory permission and fails

[CAMEL-19477](https://issues.apache.org/jira/browse/CAMEL-19477)

MeterRegistry collects authorization data

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).