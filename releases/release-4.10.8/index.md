# Apache camel 4.10.8 Release

## New and Noteworthy

This release is the new Camel 4.10.8 release.

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
      <version>4.10.8</version>
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
      <version>4.10.8</version>
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
| [apache-camel-4.10.8-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-src.zip.sha512) |
| [apache-camel-4.10.8-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.xml.sha512) |
| [apache-camel-4.10.8-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.8/apache-camel-4.10.8-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.8` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.8

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-22741](https://issues.apache.org/jira/browse/CAMEL-22741)

pollEnrich EIP doesn't preserve the original headers

[CAMEL-22691](https://issues.apache.org/jira/browse/CAMEL-22691)

camel-cxf - Memory leak in CXF producer

[CAMEL-22571](https://issues.apache.org/jira/browse/CAMEL-22571)

\[camel-beanio\] No type converter for encoding

[CAMEL-22565](https://issues.apache.org/jira/browse/CAMEL-22565)

camel-sql - DefaultSqlPrepareStatementStrategy is missing exchange in tryConverter

[CAMEL-22558](https://issues.apache.org/jira/browse/CAMEL-22558)

Jira - Consumer ignores delay option

[CAMEL-22557](https://issues.apache.org/jira/browse/CAMEL-22557)

camel-as2 - Server-side DecryptingPrivateKey Conflict: Key from first route started is enforced for all subsequent routes on the same serverPortNumber

[CAMEL-22533](https://issues.apache.org/jira/browse/CAMEL-22533)

ConcurrentModificationException thrown in JMX-enabled application using Split EIP w/ shared UoW

[CAMEL-22529](https://issues.apache.org/jira/browse/CAMEL-22529)

route configuration in Java DSL with multiple onException does not work

[CAMEL-22494](https://issues.apache.org/jira/browse/CAMEL-22494)

camel-as2 - AS2 consumer URI remains active after route stop/removal

[CAMEL-22488](https://issues.apache.org/jira/browse/CAMEL-22488)

camlel-sql - Error when automatically creating JdbcIdempotent table

[CAMEL-22476](https://issues.apache.org/jira/browse/CAMEL-22476)

camel-plc4j - Cannot load drivers when using poll mode

[CAMEL-22474](https://issues.apache.org/jira/browse/CAMEL-22474)

camel-http - HttpActivityListener null exchange when redelivery

[CAMEL-22468](https://issues.apache.org/jira/browse/CAMEL-22468)

camel-bean - Bean cache should initialize later

[CAMEL-22458](https://issues.apache.org/jira/browse/CAMEL-22458)

flatpack converter accesses invalid column names for header and trailer record value retrieval of fixed width files

### Dependency upgrade (5)

[CAMEL-22757](https://issues.apache.org/jira/browse/CAMEL-22757)

camel-tika - Upgrade to tika 3.x

[CAMEL-22700](https://issues.apache.org/jira/browse/CAMEL-22700)

camel-spring-boot - Upgrade to 3.4.12

[CAMEL-22594](https://issues.apache.org/jira/browse/CAMEL-22594)

camel-spring-boot - Upgrade to 3.4.11

[CAMEL-22563](https://issues.apache.org/jira/browse/CAMEL-22563)

camel-spring - Upgrade to spring 6.2.12

[CAMEL-22490](https://issues.apache.org/jira/browse/CAMEL-22490)

camel-minio - Upgrade to 8.6.x

### Improvement (4)

[CAMEL-22719](https://issues.apache.org/jira/browse/CAMEL-22719)

camel-neo4j - Improve detection of message body

[CAMEL-22611](https://issues.apache.org/jira/browse/CAMEL-22611)

SmbComponent: file move error if the user does not have "Full Control" permissions

[CAMEL-22471](https://issues.apache.org/jira/browse/CAMEL-22471)

camel-jbang - Send command with file location should use absolute path

[CAMEL-17348](https://issues.apache.org/jira/browse/CAMEL-17348)

camel-jira component newIssue does not work across multiple projects

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).