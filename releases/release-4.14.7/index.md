# Apache camel 4.14.7 Release

## New and Noteworthy

This release is the new Camel 4.14.7 LTS release.

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
      <version>4.14.7</version>
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
      <version>4.14.7</version>
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
| [apache-camel-4.14.7-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.7/apache-camel-4.14.7-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-src.zip.sha512) |
| [apache-camel-4.14.7-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.xml.sha512) |
| [apache-camel-4.14.7-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.7/apache-camel-4.14.7-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Improvement (3)

[CAMEL-23322](https://issues.apache.org/jira/browse/CAMEL-23322)

camel-infinispan: align remote aggregation repository options with sibling repos

[CAMEL-23321](https://issues.apache.org/jira/browse/CAMEL-23321)

camel-jms, camel-sjms, camel-amqp - Add deserialization filtering for ObjectMessage handling

[CAMEL-23320](https://issues.apache.org/jira/browse/CAMEL-23320)

camel-platform-http-starter - Fix binary data corruption due to Spring Boot's default UTF-8 charset

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).