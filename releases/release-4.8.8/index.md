# Apache camel 4.8.8 Release

## New and Noteworthy

This release is the new Camel 4.8.8 release.

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
      <version>4.8.8</version>
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
      <version>4.8.8</version>
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
| [apache-camel-4.8.8-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-src.zip.sha512) |
| [apache-camel-4.8.8-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.xml.sha512) |
| [apache-camel-4.8.8-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.8/apache-camel-4.8.8-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.8` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.8

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-22176](https://issues.apache.org/jira/browse/CAMEL-22176)

High CPU Usage and Deadlock/Race Condition (?) in SimpleLRUCache after Upgrade (>4.8.2)

[CAMEL-22133](https://issues.apache.org/jira/browse/CAMEL-22133)

camel-platform-http-vertx: VertxPlatformHttpServer.stopVertx logic is incorrect

[CAMEL-22127](https://issues.apache.org/jira/browse/CAMEL-22127)

ConcurrentModificationException is coming inside Camel’s Vert.x WebSocket

[CAMEL-22117](https://issues.apache.org/jira/browse/CAMEL-22117)

camel-openapi-validator doesn't use query params or headers for validation

[CAMEL-22116](https://issues.apache.org/jira/browse/CAMEL-22116)

camel-openapi-validator doesn't work for contract-first api's with Spring Boot

[CAMEL-22095](https://issues.apache.org/jira/browse/CAMEL-22095)

camel-core - Rest DSL with inlined routes does not work with AdviceWith testing

[CAMEL-22082](https://issues.apache.org/jira/browse/CAMEL-22082)

camel-stream - NPE if charset is not specified

[CAMEL-22068](https://issues.apache.org/jira/browse/CAMEL-22068)

Camel-bindy does not treat escaped double quotes in CSV data

[CAMEL-22065](https://issues.apache.org/jira/browse/CAMEL-22065)

camel-rest-openapi: OpenApi specification in the rest configuration will be ignored in Camel Spring Boot

[CAMEL-22062](https://issues.apache.org/jira/browse/CAMEL-22062)

camel-jsonata: outputType: Jackson does not output Jackson body

[CAMEL-22059](https://issues.apache.org/jira/browse/CAMEL-22059)

camel-ssh - Calling 2nd time does not keep correct exit value header

[CAMEL-22050](https://issues.apache.org/jira/browse/CAMEL-22050)

camel-rest-openapi - Component configuration should be used in endpoint

[CAMEL-22037](https://issues.apache.org/jira/browse/CAMEL-22037)

camel-as2 - In AS2Receiver, line feeds are replaced by CRLF

[CAMEL-21963](https://issues.apache.org/jira/browse/CAMEL-21963)

camel-infinispan - query parameters not working

### Dependency upgrade (1)

[CAMEL-22102](https://issues.apache.org/jira/browse/CAMEL-22102)

camel-spring-boot - Upgrade to 3.3.12

### Improvement (3)

[CAMEL-22180](https://issues.apache.org/jira/browse/CAMEL-22180)

camel-simple - Using inlined jsonpath with 2-arg exp should trim so you can use space around comma

[CAMEL-22125](https://issues.apache.org/jira/browse/CAMEL-22125)

camel-platform-http-vertx - Writing response should favour input stream over ByteBuffer

[CAMEL-22061](https://issues.apache.org/jira/browse/CAMEL-22061)

camel-test-junit - Make it easy to include more than 1 route builder in Java

### Task (1)

[CAMEL-22186](https://issues.apache.org/jira/browse/CAMEL-22186)

Camel-azure-storage-datalake - wrong parameter in example in the \*.adoc file

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).