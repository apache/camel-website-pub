# Apache camel 2.25.1 Release

## New and Noteworthy

This release is the new Camel 2.25.1 patch release.

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
      <version>2.25.1</version>
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
      <version>2.25.1</version>
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
| [apache-camel-2.25.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.25.1/apache-camel-2.25.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.25.1/apache-camel-2.25.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.25.1/apache-camel-2.25.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.25.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.25.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (8)

[CAMEL-14865](https://issues.apache.org/jira/browse/CAMEL-14865)

camel-telegram - missing the direct dependency of com.fasterxml.jackson.core:jackson-core

[CAMEL-14792](https://issues.apache.org/jira/browse/CAMEL-14792)

ClassNotFoundException for onException(Class) in Java DSL in OSGi

[CAMEL-14789](https://issues.apache.org/jira/browse/CAMEL-14789)

camel-rabbitmq - Automatic recovery of temporary reply queue is not handled correctly

[CAMEL-14788](https://issues.apache.org/jira/browse/CAMEL-14788)

Unable to Start Jetty server in OSGi environment

[CAMEL-14633](https://issues.apache.org/jira/browse/CAMEL-14633)

Safe copy of exchange will not copy attachments on in message, unless headers are set

[CAMEL-14493](https://issues.apache.org/jira/browse/CAMEL-14493)

camel 2: mvn camel:run fails on spring projects

[CAMEL-14453](https://issues.apache.org/jira/browse/CAMEL-14453)

ensure Camel Rest Swagger example work again

[CAMEL-14432](https://issues.apache.org/jira/browse/CAMEL-14432)

camel-salesforce - Memory leak when toD is used with cacheSize < 0 in Camel 2.x

### Improvement (5)

[CAMEL-14711](https://issues.apache.org/jira/browse/CAMEL-14711)

Disable RabbitMQ Java serialization by default

[CAMEL-14639](https://issues.apache.org/jira/browse/CAMEL-14639)

DefaultHttpRegistry thread safety

[CAMEL-14501](https://issues.apache.org/jira/browse/CAMEL-14501)

gain fully control of xml parser used by saxon

[CAMEL-14477](https://issues.apache.org/jira/browse/CAMEL-14477)

camel-netty - Disable object serialization

[CAMEL-14414](https://issues.apache.org/jira/browse/CAMEL-14414)

Aggregation completion has inconsistent property/header handling

### Task (1)

[CAMEL-14532](https://issues.apache.org/jira/browse/CAMEL-14532)

Fix issues with camel-snakeyaml

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).