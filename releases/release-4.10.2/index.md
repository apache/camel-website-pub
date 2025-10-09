# Apache camel 4.10.2 Release

## New and Noteworthy

This release is the new Camel 4.10.2 release.

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
      <version>4.10.2</version>
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
      <version>4.10.2</version>
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
| [apache-camel-4.10.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-src.zip.sha512) |
| [apache-camel-4.10.2-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.xml.sha512) |
| [apache-camel-4.10.2-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.2/apache-camel-4.10.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-21849](https://issues.apache.org/jira/browse/CAMEL-21849)

camel-kamelet - Using variableReceive should not loose message body

[CAMEL-21847](https://issues.apache.org/jira/browse/CAMEL-21847)

camel-http - Possible resource leak in camel-http when using oauth2

[CAMEL-21840](https://issues.apache.org/jira/browse/CAMEL-21840)

camel-http does not encode path correctly when used with HTTP\_QUERY header

[CAMEL-21836](https://issues.apache.org/jira/browse/CAMEL-21836)

Possible resource leak in camel minio in verifier extension

[CAMEL-21832](https://issues.apache.org/jira/browse/CAMEL-21832)

camel-core - Choice with when that has no output should not call otherwise

[CAMEL-21830](https://issues.apache.org/jira/browse/CAMEL-21830)

camel-file - Using consumer template to consume a single file issue with idempotentEager

[CAMEL-21604](https://issues.apache.org/jira/browse/CAMEL-21604)

GZIP interceptor added as a CXF feature is not working properly for CXF SOAP and CXF REST on Camel Spring Boot

### Improvement (7)

[CAMEL-21851](https://issues.apache.org/jira/browse/CAMEL-21851)

camel-bean - Improve method selector

[CAMEL-21846](https://issues.apache.org/jira/browse/CAMEL-21846)

camel-jbang - Add support for running on eclipse openj9 java

[CAMEL-21845](https://issues.apache.org/jira/browse/CAMEL-21845)

camel-sql - Improve performance of batch inserts

[CAMEL-21829](https://issues.apache.org/jira/browse/CAMEL-21829)

camel-sql - Make it easier to use Map values for non-named SQL statements

[CAMEL-21828](https://issues.apache.org/jira/browse/CAMEL-21828)

camel-http - DefaultHeaderFilterStrategy optimize filter

[CAMEL-21823](https://issues.apache.org/jira/browse/CAMEL-21823)

camel-core - Propagate MDC custom keys for WireTap and OnCompletion EIPs

[CAMEL-21671](https://issues.apache.org/jira/browse/CAMEL-21671)

camel-core - Issue with Camel Splitter and Asynchronous Processing in Parallel Mode can use many threads

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).