# Apache camel 4.8.6 Release

## New and Noteworthy

This release is the new Camel 4.8.6 release.

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
      <version>4.8.6</version>
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
      <version>4.8.6</version>
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
| [apache-camel-4.8.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-src.zip.sha512) |
| [apache-camel-4.8.6-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.xml.sha512) |
| [apache-camel-4.8.6-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.6/apache-camel-4.8.6-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (4)

[CAMEL-21888](https://issues.apache.org/jira/browse/CAMEL-21888)

High CPU usage at startup due to Deque.size() iteration in SimpleLRUCache

[CAMEL-21865](https://issues.apache.org/jira/browse/CAMEL-21865)

camel-test - Using advice-with with route having XML namepaces as immutable Map.of

[CAMEL-21854](https://issues.apache.org/jira/browse/CAMEL-21854)

Possible memory leak when using camel-observability

[CAMEL-21604](https://issues.apache.org/jira/browse/CAMEL-21604)

GZIP interceptor added as a CXF feature is not working properly for CXF SOAP and CXF REST on Camel Spring Boot

### Improvement (1)

[CAMEL-21861](https://issues.apache.org/jira/browse/CAMEL-21861)

camel-spring-boot - Actuator endpoint for dev console should respect if console has been disabled

### New Feature (1)

[CAMEL-21876](https://issues.apache.org/jira/browse/CAMEL-21876)

Undertow Header Filter Strategy: Considering also the in filter

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).