# Apache camel 4.0.6 Release

## New and Noteworthy

This release is the new Camel 4.0.6 LTS patch release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.0.6</version>
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
      <version>4.0.6</version>
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
| [apache-camel-4.0.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-src.zip.sha512) |
| [apache-camel-4.0.6-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.xml.sha512) |
| [apache-camel-4.0.6-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.6/apache-camel-4.0.6-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (9)

[CAMEL-20995](https://issues.apache.org/jira/browse/CAMEL-20995)

camel-azure-storage-blob uploadBlockBlob retry operation fails due to mark and reset issue / Flux

[CAMEL-20988](https://issues.apache.org/jira/browse/CAMEL-20988)

camel-test-infra: some services are unable to properly log initialization failures

[CAMEL-20954](https://issues.apache.org/jira/browse/CAMEL-20954)

Cannot share SSLContextParameters between camel-kafka and other components

[CAMEL-20864](https://issues.apache.org/jira/browse/CAMEL-20864)

camel-kafka - With confluent schema registry does not work properly.

[CAMEL-20850](https://issues.apache.org/jira/browse/CAMEL-20850)

LRUCache evicts entries unexpectedly

[CAMEL-20835](https://issues.apache.org/jira/browse/CAMEL-20835)

OOM using RecipientList

[CAMEL-20834](https://issues.apache.org/jira/browse/CAMEL-20834)

camel-salesforce - A NullPointException in SubscriptionHelper.subscribe() interrupts platform-event subscription

[CAMEL-20731](https://issues.apache.org/jira/browse/CAMEL-20731)

Route coverage fails on routes with multiple doCatch blocks

[CAMEL-20692](https://issues.apache.org/jira/browse/CAMEL-20692)

camel-cxf - No Payload is logged when the logging feature is enabled

### Dependency upgrade (1)

[CAMEL-20781](https://issues.apache.org/jira/browse/CAMEL-20781)

camel-spring-boot - Upgrade to SB 3.1.12

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).