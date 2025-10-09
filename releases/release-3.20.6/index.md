# Apache camel 3.20.6 Release

## New and Noteworthy

This release is the new Camel 3.20.6 LTS patch release.

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
      <version>3.20.6</version>
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
      <version>3.20.6</version>
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
| [apache-camel-3.20.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.6/apache-camel-3.20.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.6/apache-camel-3.20.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.6/apache-camel-3.20.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-19452](https://issues.apache.org/jira/browse/CAMEL-19452)

camel-jbang - Run with --open-api does not show log in console

[CAMEL-19443](https://issues.apache.org/jira/browse/CAMEL-19443)

camel-kamelet - Route templates should use route configured error handler

[CAMEL-19432](https://issues.apache.org/jira/browse/CAMEL-19432)

camel-azure-eventhubs: Providing a custom EventHubProducerAsyncClient has no effect

[CAMEL-19426](https://issues.apache.org/jira/browse/CAMEL-19426)

Spring-WS syntaxt and path properties inconsistency

[CAMEL-19421](https://issues.apache.org/jira/browse/CAMEL-19421)

Camel-Jira: Use Files.createTempFile in FileConverter instead of creating File directly

[CAMEL-19415](https://issues.apache.org/jira/browse/CAMEL-19415)

camel-stax: using xtokenize might be NPE on xml default namespace

[CAMEL-19401](https://issues.apache.org/jira/browse/CAMEL-19401)

Typo in kafka image name in ContainerLocalKafkaService

[CAMEL-19399](https://issues.apache.org/jira/browse/CAMEL-19399)

camel-cxf - Prevent storing invalid entry in Converter cache on error

[CAMEL-19393](https://issues.apache.org/jira/browse/CAMEL-19393)

camel-kafka - Configuring kafka option should no longer all be string types

[CAMEL-19387](https://issues.apache.org/jira/browse/CAMEL-19387)

camel-kafka - Cannot set custom azure credential provider

[CAMEL-19383](https://issues.apache.org/jira/browse/CAMEL-19383)

camel-jslt: allowTemplateFromHeader ignores header on subsequent exchanges

[CAMEL-19381](https://issues.apache.org/jira/browse/CAMEL-19381)

Infinite loop creating processes with Camel JBang

[CAMEL-18965](https://issues.apache.org/jira/browse/CAMEL-18965)

Camel-CXF: OnCompletion not working anymore

### Improvement (4)

[CAMEL-19455](https://issues.apache.org/jira/browse/CAMEL-19455)

camel-cxf - Ensure REQUEST\_CONTEXT & RESPONSE\_CONTEXT headers are Map when populating CXF Message from Camel Message

[CAMEL-19454](https://issues.apache.org/jira/browse/CAMEL-19454)

camel-jbang - Export should support --open-api

[CAMEL-19453](https://issues.apache.org/jira/browse/CAMEL-19453)

camel-jbang - Run with --open-api to support yaml spec files

[CAMEL-19378](https://issues.apache.org/jira/browse/CAMEL-19378)

File Changed ReadLock Strategy with minAge only looks for lastModified

### Task (2)

[CAMEL-19418](https://issues.apache.org/jira/browse/CAMEL-19418)

camel-cxf - "Description of relayHeaders option" section of CXF component page is out of date

[CAMEL-19207](https://issues.apache.org/jira/browse/CAMEL-19207)

Missing version for mysql:mysql-connector-java in SB examples

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).