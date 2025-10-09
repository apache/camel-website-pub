# Apache camel 3.14.8 Release

## New and Noteworthy

This release is the new Camel 3.14.8 LTS patch release.

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
      <version>3.14.8</version>
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
      <version>3.14.8</version>
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
| [apache-camel-3.14.8-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.8/apache-camel-3.14.8-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.8/apache-camel-3.14.8-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.8/apache-camel-3.14.8-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.8` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.8

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (10)

[CAMEL-19371](https://issues.apache.org/jira/browse/CAMEL-19371)

RedeliveryErrorHandler's suppressed exceptions cause memory leak and logging issue

[CAMEL-19169](https://issues.apache.org/jira/browse/CAMEL-19169)

camel-olingo2: queryParams option of read method does not work

[CAMEL-19162](https://issues.apache.org/jira/browse/CAMEL-19162)

camel-ehcache - llegalStateException: Close not supported from UNINITIALIZED. When context.addRouteDefinition() called multiple times in route with Ehcache consumer

[CAMEL-19150](https://issues.apache.org/jira/browse/CAMEL-19150)

camel-olingo4: queryParams option of read method does not work

[CAMEL-19081](https://issues.apache.org/jira/browse/CAMEL-19081)

Start a route with aggregation fails due to NPE in AggregateProcessor

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19031](https://issues.apache.org/jira/browse/CAMEL-19031)

When camel saga do compensated, the saga route don't stop it still run the next task.

[CAMEL-18871](https://issues.apache.org/jira/browse/CAMEL-18871)

camel-netty - Application does not recover (threads are WAITING) when NettyProducer pool is exhausted

[CAMEL-18835](https://issues.apache.org/jira/browse/CAMEL-18835)

camel-core-processor: OnCompletionProcessor#onFailure callback fires more than once

[CAMEL-18811](https://issues.apache.org/jira/browse/CAMEL-18811)

camel-ldap - InvalidSearchFilterException: invalid attribute description

### Dependency upgrade (2)

[CAMEL-19374](https://issues.apache.org/jira/browse/CAMEL-19374)

camel-spring-boot - Upgrade to 2.6.15

[CAMEL-19288](https://issues.apache.org/jira/browse/CAMEL-19288)

camel-jsonpath - Upgrade to 2.8

### Improvement (1)

[CAMEL-18636](https://issues.apache.org/jira/browse/CAMEL-18636)

azure data lake component: authentication can not be configured using string properties

### Task (1)

[CAMEL-19201](https://issues.apache.org/jira/browse/CAMEL-19201)

Unused assignment in AdviceWithBuilder::maxDeep()

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).