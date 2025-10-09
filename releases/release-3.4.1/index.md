# Apache camel 3.4.1 Release

## New and Noteworthy

This release is the new Camel 3.4.1 patch release.

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
      <version>3.4.1</version>
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
      <version>3.4.1</version>
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
| [apache-camel-3.4.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.1/apache-camel-3.4.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.1/apache-camel-3.4.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.1/apache-camel-3.4.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (11)

[CAMEL-15272](https://issues.apache.org/jira/browse/CAMEL-15272)

Camel-jira: JSONObject\["name"\] not found when connecting to latest JIRA/Jira-cloud

[CAMEL-15265](https://issues.apache.org/jira/browse/CAMEL-15265)

StaticEndpointBuilders - The static methods should be public

[CAMEL-15262](https://issues.apache.org/jira/browse/CAMEL-15262)

ZooKeeperCuratorHelper: wrong argument order when creating a new ExponentialBackoffRetry

[CAMEL-15251](https://issues.apache.org/jira/browse/CAMEL-15251)

camel-cdi - MandatoryJtaTransactionPolicy and NeverJtaTransactionPolicy miss to call the runnable work

[CAMEL-15239](https://issues.apache.org/jira/browse/CAMEL-15239)

camel-velocity header option does not conform to documentation

[CAMEL-15229](https://issues.apache.org/jira/browse/CAMEL-15229)

autoDiscoverObjectMapper is not propagated to JacksonDataFormat

[CAMEL-15219](https://issues.apache.org/jira/browse/CAMEL-15219)

camel-cassandraql: cannot use a custom resultSetConversionStrategy

[CAMEL-15214](https://issues.apache.org/jira/browse/CAMEL-15214)

\[regression\]Duration values are no more part of the validation

[CAMEL-15195](https://issues.apache.org/jira/browse/CAMEL-15195)

camel-netty - RequestTimeout seems not working as expected

[CAMEL-15187](https://issues.apache.org/jira/browse/CAMEL-15187)

jsonpath does not reset StreamCache on CBR predicate

[CAMEL-15149](https://issues.apache.org/jira/browse/CAMEL-15149)

Invalid UTF8 character in iec60870-server.json

### Improvement (2)

[CAMEL-15277](https://issues.apache.org/jira/browse/CAMEL-15277)

OpenAPI Java extension cannot always handle non-default API context path

[CAMEL-15209](https://issues.apache.org/jira/browse/CAMEL-15209)

camel-jaxb - Should depend on camel-xml-jaxb

### New Feature (1)

[CAMEL-15267](https://issues.apache.org/jira/browse/CAMEL-15267)

Add a ByteArrayOutputStream to ByteBuffer converter in core

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).