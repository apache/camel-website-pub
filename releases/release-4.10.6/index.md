# Apache camel 4.10.6 Release

## New and Noteworthy

This release is the new Camel 4.10.6 release.

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
      <version>4.10.6</version>
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
      <version>4.10.6</version>
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
| [apache-camel-4.10.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-src.zip.sha512) |
| [apache-camel-4.10.6-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.xml.sha512) |
| [apache-camel-4.10.6-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.6/apache-camel-4.10.6-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (10)

[CAMEL-22176](https://issues.apache.org/jira/browse/CAMEL-22176)

High CPU Usage and Deadlock/Race Condition (?) in SimpleLRUCache after Upgrade (>4.8.2)

[CAMEL-22155](https://issues.apache.org/jira/browse/CAMEL-22155)

Detection od duplicated routeIDs might cause an issue with the inlined routes

[CAMEL-22150](https://issues.apache.org/jira/browse/CAMEL-22150)

camel-kafka - Issue with Batching: Missed Records Due to due hasExpiredRecords check

[CAMEL-22141](https://issues.apache.org/jira/browse/CAMEL-22141)

camel-jbang - camel run multiple routes with duplicate ids is not failing as intended

[CAMEL-22139](https://issues.apache.org/jira/browse/CAMEL-22139)

camel-jbang - Export to Quarkus should let property keys with their current case

[CAMEL-22133](https://issues.apache.org/jira/browse/CAMEL-22133)

camel-platform-http-vertx: VertxPlatformHttpServer.stopVertx logic is incorrect

[CAMEL-22129](https://issues.apache.org/jira/browse/CAMEL-22129)

rest-openapi contract-first no longer works when server.servlet.context-path is set

[CAMEL-22127](https://issues.apache.org/jira/browse/CAMEL-22127)

ConcurrentModificationException is coming inside Camel’s Vert.x WebSocket

[CAMEL-22117](https://issues.apache.org/jira/browse/CAMEL-22117)

camel-openapi-validator doesn't use query params or headers for validation

[CAMEL-22116](https://issues.apache.org/jira/browse/CAMEL-22116)

camel-openapi-validator doesn't work for contract-first api's with Spring Boot

### Improvement (3)

[CAMEL-22180](https://issues.apache.org/jira/browse/CAMEL-22180)

camel-simple - Using inlined jsonpath with 2-arg exp should trim so you can use space around comma

[CAMEL-22130](https://issues.apache.org/jira/browse/CAMEL-22130)

camel-platform-http-verx - Add timeout option

[CAMEL-22125](https://issues.apache.org/jira/browse/CAMEL-22125)

camel-platform-http-vertx - Writing response should favour input stream over ByteBuffer

### Task (1)

[CAMEL-22186](https://issues.apache.org/jira/browse/CAMEL-22186)

Camel-azure-storage-datalake - wrong parameter in example in the \*.adoc file

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).