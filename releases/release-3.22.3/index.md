# Apache camel 3.22.3 Release

## New and Noteworthy

This release is the new Camel 3.22.3 LTS release.

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
      <version>3.22.3</version>
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
      <version>3.22.3</version>
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
| [apache-camel-3.22.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-src.zip.sha512) |
| [apache-camel-3.22.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.xml.sha512) |
| [apache-camel-3.22.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.3/apache-camel-3.22.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-3.22.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.22.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (9)

[CAMEL-21545](https://issues.apache.org/jira/browse/CAMEL-21545)

camel-jsonpath - Should not use XmlMapper

[CAMEL-21520](https://issues.apache.org/jira/browse/CAMEL-21520)

camel-karaf - OSGi ErrorHandler package missing in import package

[CAMEL-21200](https://issues.apache.org/jira/browse/CAMEL-21200)

camel-activemq - OSGi javax.jms range is wrong

[CAMEL-21112](https://issues.apache.org/jira/browse/CAMEL-21112)

camel-sql - Simple language to lookup parameter value is not compatible with batch mode

[CAMEL-21109](https://issues.apache.org/jira/browse/CAMEL-21109)

Choice evaluation behaves inconsistently when source is String and Value is Float.

[CAMEL-21056](https://issues.apache.org/jira/browse/CAMEL-21056)

Delay when using readLockMinAge

[CAMEL-20954](https://issues.apache.org/jira/browse/CAMEL-20954)

Cannot share SSLContextParameters between camel-kafka and other components

[CAMEL-20864](https://issues.apache.org/jira/browse/CAMEL-20864)

camel-kafka - With confluent schema registry does not work properly.

[CAMEL-20835](https://issues.apache.org/jira/browse/CAMEL-20835)

OOM using RecipientList

### Dependency upgrade (1)

[CAMEL-21225](https://issues.apache.org/jira/browse/CAMEL-21225)

camel-pulsar - Upgrade to 2.10.6

### Improvement (1)

[CAMEL-21053](https://issues.apache.org/jira/browse/CAMEL-21053)

camel-xslt - All exchange properties should be avaiable

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).