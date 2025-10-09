# Apache camel 4.10.9 Release

## New and Noteworthy

This release is the new Camel 4.10.9 release.

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
      <version>4.10.9</version>
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
      <version>4.10.9</version>
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
| [apache-camel-4.10.9-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-src.zip.sha512) |
| [apache-camel-4.10.9-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.xml.sha512) |
| [apache-camel-4.10.9-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.9/apache-camel-4.10.9-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.9` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.9

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (4)

[CAMEL-22828](https://issues.apache.org/jira/browse/CAMEL-22828)

camel-main - camel.main.endpoint-runtime-statistics-enabled not working since Camel 4.5

[CAMEL-22824](https://issues.apache.org/jira/browse/CAMEL-22824)

camel-core - Choice with bodyAs predicate may cause stream caching to be EOL

[CAMEL-22820](https://issues.apache.org/jira/browse/CAMEL-22820)

routeConfiguration onException does not propagate to direct endpoints for consumer-level exceptions

[CAMEL-22789](https://issues.apache.org/jira/browse/CAMEL-22789)

camel-core - Using bridgeErrorHandler=true can cause endless loop if triggered from onCompletion (such as camel-aws-s3)

### Dependency upgrade (2)

[CAMEL-22794](https://issues.apache.org/jira/browse/CAMEL-22794)

camel-spring-boot - Upgrade to 3.4.13

[CAMEL-22788](https://issues.apache.org/jira/browse/CAMEL-22788)

Investigate upgrading to at.yawk.lz4:lz4-java 1.10.1

### Improvement (1)

[CAMEL-22966](https://issues.apache.org/jira/browse/CAMEL-22966)

Camel-LevelDB: Add ObjectInputFilter String pattern parameter in LevelDBAggregationRepository to be used in unmarshall operations

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).