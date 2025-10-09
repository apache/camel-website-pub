# Apache camel 4.4.5 Release

## New and Noteworthy

This release is the new Camel 4.4.5 LTS patch release.

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
      <version>4.4.5</version>
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
      <version>4.4.5</version>
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
| [apache-camel-4.4.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-src.zip.sha512) |
| [apache-camel-4.4.5-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.xml.sha512) |
| [apache-camel-4.4.5-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.5/apache-camel-4.4.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (8)

[CAMEL-21550](https://issues.apache.org/jira/browse/CAMEL-21550)

camel-aws-sqs - message is getting expired before extender changes the visibility

[CAMEL-21545](https://issues.apache.org/jira/browse/CAMEL-21545)

camel-jsonpath - Should not use XmlMapper

[CAMEL-21493](https://issues.apache.org/jira/browse/CAMEL-21493)

camel-ref: should use CamelContext.hasEndpoint but not CamelContext.getEndpoint to check existence of an endpoint

[CAMEL-21471](https://issues.apache.org/jira/browse/CAMEL-21471)

camel-quartz ignores ignoreExpiredNextFireTime when endAt is expired

[CAMEL-21432](https://issues.apache.org/jira/browse/CAMEL-21432)

multicast function executes for ever. Thread is RUNNABLE for ever. Issue appears with multicast operating on SimpleLRUCache

[CAMEL-21423](https://issues.apache.org/jira/browse/CAMEL-21423)

camel-crypto - It is not possible to use "inline" with "AES/GCM/NoPadding"

[CAMEL-21406](https://issues.apache.org/jira/browse/CAMEL-21406)

camel-sql - RowMapperFactory should be configurable to refer a bean by id

[CAMEL-21302](https://issues.apache.org/jira/browse/CAMEL-21302)

camel-opentelemetry context leak with direct async producer

### Dependency upgrade (3)

[CAMEL-21571](https://issues.apache.org/jira/browse/CAMEL-21571)

camel-mina - Upgrade to 2.2.4

[CAMEL-21473](https://issues.apache.org/jira/browse/CAMEL-21473)

camel-spring-boot - Upgrade to SB 3.2.12

[CAMEL-21455](https://issues.apache.org/jira/browse/CAMEL-21455)

camel-beanio - Upgrade to 3.2.0

### Task (1)

[CAMEL-21576](https://issues.apache.org/jira/browse/CAMEL-21576)

camel-test-infra: container pulling adjustments

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).