# Apache camel 3.14.6 Release

## New and Noteworthy

This release is the new Camel 3.14.6 LTS patch release.

## Supported Java version

This version supports Java 8 and 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.14.6</version>
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
      <version>3.14.6</version>
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
| [apache-camel-3.14.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.6/apache-camel-3.14.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.6/apache-camel-3.14.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.6/apache-camel-3.14.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (10)

[CAMEL-18544](https://issues.apache.org/jira/browse/CAMEL-18544)

camel-http - ToD optimized context-path with spaces problem

[CAMEL-18530](https://issues.apache.org/jira/browse/CAMEL-18530)

Camel box cannot authorize

[CAMEL-18490](https://issues.apache.org/jira/browse/CAMEL-18490)

camel-jbang - Reset statistics can cause JMX inflight counter to be negative

[CAMEL-18432](https://issues.apache.org/jira/browse/CAMEL-18432)

DockerConfiguration malformerd UriPath for variable operation

[CAMEL-18421](https://issues.apache.org/jira/browse/CAMEL-18421)

camel-core - Adding route dynamic leak bootstraps

[CAMEL-18411](https://issues.apache.org/jira/browse/CAMEL-18411)

camel-bean: MethodNotFoundException when using OSGi service reference

[CAMEL-18399](https://issues.apache.org/jira/browse/CAMEL-18399)

camel-sql - NullPointer exception for DBMaker PreparedStatement

[CAMEL-18387](https://issues.apache.org/jira/browse/CAMEL-18387)

camel-tarfile: TarAggregationStrategy throws error when first message is empty

[CAMEL-18350](https://issues.apache.org/jira/browse/CAMEL-18350)

camel-kafka: enabling "breakOnFirstError" causes camel to reconsume all records on error

[CAMEL-18255](https://issues.apache.org/jira/browse/CAMEL-18255)

Memory Leak with MDCUnitOfWork

### Dependency upgrade (2)

[CAMEL-18632](https://issues.apache.org/jira/browse/CAMEL-18632)

camel-spring-boot - Upgrade to 2.6.13

[CAMEL-18409](https://issues.apache.org/jira/browse/CAMEL-18409)

Align to spring-boot 2.6.11

### Task (1)

[CAMEL-18303](https://issues.apache.org/jira/browse/CAMEL-18303)

camel 3.14.4 XSD schemas are not published

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).