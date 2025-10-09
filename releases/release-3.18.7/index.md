# Apache camel 3.18.7 Release

## New and Noteworthy

This release is the new Camel 3.18.7 LTS patch release.

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
      <version>3.18.7</version>
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
      <version>3.18.7</version>
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
| [apache-camel-3.18.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.7/apache-camel-3.18.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.7/apache-camel-3.18.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.7/apache-camel-3.18.7-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (7)

[CAMEL-19371](https://issues.apache.org/jira/browse/CAMEL-19371)

RedeliveryErrorHandler's suppressed exceptions cause memory leak and logging issue

[CAMEL-19298](https://issues.apache.org/jira/browse/CAMEL-19298)

Snmp: version 3 is not supported for several actions for the component

[CAMEL-19293](https://issues.apache.org/jira/browse/CAMEL-19293)

camel-spring-ldap - base is set twice when using SB AutoConfiguration

[CAMEL-19256](https://issues.apache.org/jira/browse/CAMEL-19256)

camel-jdbc: leaks the statement in doCreateAndExecuteSqlStatement

[CAMEL-19249](https://issues.apache.org/jira/browse/CAMEL-19249)

camel-salesforce: Creating blob data is broken

[CAMEL-18985](https://issues.apache.org/jira/browse/CAMEL-18985)

camel-kafka: messages are getting lost with "breakOnFirstError"

[CAMEL-18834](https://issues.apache.org/jira/browse/CAMEL-18834)

camel-core - StringQuoteHelper should remove quotes for single element

### Dependency upgrade (3)

[CAMEL-19372](https://issues.apache.org/jira/browse/CAMEL-19372)

camel-spring-boot - Upgrade to 2.7.12

[CAMEL-19351](https://issues.apache.org/jira/browse/CAMEL-19351)

camel-jackson - Upgrade to 2.14.3

[CAMEL-19288](https://issues.apache.org/jira/browse/CAMEL-19288)

camel-jsonpath - Upgrade to 2.8

### Improvement (3)

[CAMEL-19333](https://issues.apache.org/jira/browse/CAMEL-19333)

ensure cxf springboot autoconfiguration works OOTB in camel-cxf springboot starters

[CAMEL-19324](https://issues.apache.org/jira/browse/CAMEL-19324)

Be able to convert all elements from CXF MessageContentsList.class to String.class if not in "CXF Context"

[CAMEL-19160](https://issues.apache.org/jira/browse/CAMEL-19160)

return null for CxfPayloadConverter fallback converter so that other fallback coverter can get a chance to try

### Task (2)

[CAMEL-19294](https://issues.apache.org/jira/browse/CAMEL-19294)

camel-test-infra-zookeeper: unable to use a custom Zookeeper container

[CAMEL-19248](https://issues.apache.org/jira/browse/CAMEL-19248)

Suspicious ignoring of a variable in CouchbaseConsumer

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).