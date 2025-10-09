# Apache camel 3.22.1 Release

## New and Noteworthy

This release is the new Camel 3.22.1 LTS release.

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
      <version>3.22.1</version>
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
      <version>3.22.1</version>
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
| [apache-camel-3.22.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-src.zip.sha512) |
| [apache-camel-3.22.1-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.xml.sha512) |
| [apache-camel-3.22.1-sbom.json](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.1/apache-camel-3.22.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-3.22.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.22.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-20356](https://issues.apache.org/jira/browse/CAMEL-20356)

camel-core - LoggerHelper returns wrong name for source code line precise

[CAMEL-20350](https://issues.apache.org/jira/browse/CAMEL-20350)

camel-observation - Null values should be null instead of a string null literal value

[CAMEL-20218](https://issues.apache.org/jira/browse/CAMEL-20218)

KafkaIdempotentRepository cache incorrectly flagged as ready

### Improvement (3)

[CAMEL-20363](https://issues.apache.org/jira/browse/CAMEL-20363)

camel-jms - Make getting JMSCorrelationID more robust for brokers that has bugs

[CAMEL-20306](https://issues.apache.org/jira/browse/CAMEL-20306)

Camel-CassandraQL: Add ObjectInputFilter String pattern parameter in CassandraAggregationRepository to be used in unmarshall operations

[CAMEL-20303](https://issues.apache.org/jira/browse/CAMEL-20303)

Camel-Sql: Add ObjectInputFilter String pattern parameter in JdbcAggregationRepository to be used in unmarshall operations

### Task (1)

[CAMEL-20305](https://issues.apache.org/jira/browse/CAMEL-20305)

camel-core: ensure log consistency

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).