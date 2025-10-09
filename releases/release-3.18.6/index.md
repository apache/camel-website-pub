# Apache camel 3.18.6 Release

## New and Noteworthy

This release is the new Camel 3.18.6 LTS patch release.

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
      <version>3.18.6</version>
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
      <version>3.18.6</version>
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
| [apache-camel-3.18.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.6/apache-camel-3.18.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.6/apache-camel-3.18.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.6/apache-camel-3.18.6-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (18)

[CAMEL-19198](https://issues.apache.org/jira/browse/CAMEL-19198)

Dynamic Router EIP component does not evaluate filters by order of priority attribute

[CAMEL-19174](https://issues.apache.org/jira/browse/CAMEL-19174)

Jira component: duplicate messages with the new issues consumer

[CAMEL-19169](https://issues.apache.org/jira/browse/CAMEL-19169)

camel-olingo2: queryParams option of read method does not work

[CAMEL-19162](https://issues.apache.org/jira/browse/CAMEL-19162)

camel-ehcache - llegalStateException: Close not supported from UNINITIALIZED. When context.addRouteDefinition() called multiple times in route with Ehcache consumer

[CAMEL-19158](https://issues.apache.org/jira/browse/CAMEL-19158)

camel-core: ThrowExceptionProcessor may silently ignore exceptions in constructing the exception object

[CAMEL-19151](https://issues.apache.org/jira/browse/CAMEL-19151)

The 'ignoreInvalidEndpoint' option isn't relevant for a static URI for WireTap component

[CAMEL-19150](https://issues.apache.org/jira/browse/CAMEL-19150)

camel-olingo4: queryParams option of read method does not work

[CAMEL-19113](https://issues.apache.org/jira/browse/CAMEL-19113)

Platform-http-vertx: consume with comma separated does not work

[CAMEL-19098](https://issues.apache.org/jira/browse/CAMEL-19098)

Possible performance issue invoking a bean method with a string parameter

[CAMEL-19081](https://issues.apache.org/jira/browse/CAMEL-19081)

Start a route with aggregation fails due to NPE in AggregateProcessor

[CAMEL-19075](https://issues.apache.org/jira/browse/CAMEL-19075)

camel-bean - Incorrect choice of overloaded method with several arguments, if one of them has brackets.

[CAMEL-19066](https://issues.apache.org/jira/browse/CAMEL-19066)

Multicast EIP sets correlationId on original Exchange

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19031](https://issues.apache.org/jira/browse/CAMEL-19031)

When camel saga do compensated, the saga route don't stop it still run the next task.

[CAMEL-19018](https://issues.apache.org/jira/browse/CAMEL-19018)

camel-vertx-http: Headers may get erroneously duplicated

[CAMEL-19006](https://issues.apache.org/jira/browse/CAMEL-19006)

XML IO DSL do not load templatedRoutes without XML namespace

[CAMEL-19004](https://issues.apache.org/jira/browse/CAMEL-19004)

XML IO DSL do not parse route configuration with XML namespace

[CAMEL-18980](https://issues.apache.org/jira/browse/CAMEL-18980)

camel snmp - SNMP Ver1 trap does not work

### Dependency upgrade (2)

[CAMEL-18999](https://issues.apache.org/jira/browse/CAMEL-18999)

camel-sshd - Upgrade to 2.9.x

[CAMEL-18947](https://issues.apache.org/jira/browse/CAMEL-18947)

camel-spring-boot - Upgrade to 2.7.8

### Improvement (5)

[CAMEL-19109](https://issues.apache.org/jira/browse/CAMEL-19109)

camel-vertx-websocket: Consumer should avoid blocking the Vert.x event loop

[CAMEL-19083](https://issues.apache.org/jira/browse/CAMEL-19083)

camel-yaml-dsl: Add a doc section that links to the schema

[CAMEL-19078](https://issues.apache.org/jira/browse/CAMEL-19078)

camel-platform-http-vertx: Allow response headers with empty values to be returned

[CAMEL-18967](https://issues.apache.org/jira/browse/CAMEL-18967)

camel-platform-http-vertx: Improve handling of whether an HTTP request body is allowed or not

[CAMEL-18636](https://issues.apache.org/jira/browse/CAMEL-18636)

azure data lake component: authentication can not be configured using string properties

### Task (1)

[CAMEL-19201](https://issues.apache.org/jira/browse/CAMEL-19201)

Unused assignment in AdviceWithBuilder::maxDeep()

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).