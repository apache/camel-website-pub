# Apache camel 3.21.2 Release

## New and Noteworthy

This release is the new Camel 3.21.2 LTS patch release.

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
      <version>3.21.2</version>
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
      <version>3.21.2</version>
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
| [apache-camel-3.21.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.21.2/apache-camel-3.21.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.21.2/apache-camel-3.21.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.21.2/apache-camel-3.21.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.21.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.21.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (6)

[CAMEL-20010](https://issues.apache.org/jira/browse/CAMEL-20010)

camel-sql - Can't change table name in JdbcMessageIdRepository by adding suffix/prefix

[CAMEL-19996](https://issues.apache.org/jira/browse/CAMEL-19996)

camel-lra NullPointerException when creating a saga with invalid lra-url

[CAMEL-19976](https://issues.apache.org/jira/browse/CAMEL-19976)

camel-karaf: org.xml.sax.ext.EntityResolver2 not found by org.apache.servicemix.bundles.xmlresolver

[CAMEL-19970](https://issues.apache.org/jira/browse/CAMEL-19970)

camel-jbang - IllegalArgumentException: Unable to determine file extension for resource when a file has no extension

[CAMEL-19968](https://issues.apache.org/jira/browse/CAMEL-19968)

camel-opentelemetry - The Tracing Strategy is failing when using pollEnrich with seda endpoint

[CAMEL-19967](https://issues.apache.org/jira/browse/CAMEL-19967)

camel-core - Default RouteConfigurationBuilder written in Java not enabled on XML routes

### Dependency upgrade (3)

[CAMEL-19989](https://issues.apache.org/jira/browse/CAMEL-19989)

camel-spring-boot - Upgrade to 2.7.17

[CAMEL-19978](https://issues.apache.org/jira/browse/CAMEL-19978)

Upgrade Netty to 4.1.100.Final

[CAMEL-19920](https://issues.apache.org/jira/browse/CAMEL-19920)

camel-mina - Upgrade to newer versions

### New Feature (1)

[CAMEL-19907](https://issues.apache.org/jira/browse/CAMEL-19907)

Introduce the ability to use the old Micrometer meter names or follow the new Micrometer naming conventions

### Task (1)

[CAMEL-19984](https://issues.apache.org/jira/browse/CAMEL-19984)

Re-add Camel-Cassandraql Karaf feature

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).