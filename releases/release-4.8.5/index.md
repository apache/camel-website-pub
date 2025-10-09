# Apache camel 4.8.5 Release

## New and Noteworthy

This release is the new Camel 4.8.5 release.

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
      <version>4.8.5</version>
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
      <version>4.8.5</version>
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
| [apache-camel-4.8.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-src.zip.sha512) |
| [apache-camel-4.8.5-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.xml.sha512) |
| [apache-camel-4.8.5-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.5/apache-camel-4.8.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-21840](https://issues.apache.org/jira/browse/CAMEL-21840)

camel-http does not encode path correctly when used with HTTP\_QUERY header

[CAMEL-21836](https://issues.apache.org/jira/browse/CAMEL-21836)

Possible resource leak in camel minio in verifier extension

[CAMEL-21830](https://issues.apache.org/jira/browse/CAMEL-21830)

camel-file - Using consumer template to consume a single file issue with idempotentEager

### Improvement (2)

[CAMEL-21828](https://issues.apache.org/jira/browse/CAMEL-21828)

camel-http - DefaultHeaderFilterStrategy optimize filter

[CAMEL-21622](https://issues.apache.org/jira/browse/CAMEL-21622)

camel-tracing - add route id in the tags of the span

### Task (1)

[CAMEL-21584](https://issues.apache.org/jira/browse/CAMEL-21584)

Camel 4.8.x build is failing on CI for camel-kotlin-api module

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).