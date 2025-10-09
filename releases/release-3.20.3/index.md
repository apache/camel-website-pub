# Apache camel 3.20.3 Release

## New and Noteworthy

This release is the new Camel 3.20.3 LTS patch release.

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
      <version>3.20.3</version>
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
      <version>3.20.3</version>
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
| [apache-camel-3.20.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.3/apache-camel-3.20.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.3/apache-camel-3.20.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.3/apache-camel-3.20.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (25)

[CAMEL-19181](https://issues.apache.org/jira/browse/CAMEL-19181)

camel-springboot - mapstruct component is not autoconfigured automatically

[CAMEL-19174](https://issues.apache.org/jira/browse/CAMEL-19174)

Jira component: duplicate messages with the new issues consumer

[CAMEL-19158](https://issues.apache.org/jira/browse/CAMEL-19158)

camel-core: ThrowExceptionProcessor may silently ignore exceptions in constructing the exception object

[CAMEL-19155](https://issues.apache.org/jira/browse/CAMEL-19155)

Azure Service Bus component completes messages instead of abandoning on error

[CAMEL-19151](https://issues.apache.org/jira/browse/CAMEL-19151)

The 'ignoreInvalidEndpoint' option isn't relevant for a static URI for WireTap component

[CAMEL-19150](https://issues.apache.org/jira/browse/CAMEL-19150)

camel-olingo4: queryParams option of read method does not work

[CAMEL-19136](https://issues.apache.org/jira/browse/CAMEL-19136)

camel-micrometer - Too many tags created by micrometer WebMvcTagsProvider

[CAMEL-19133](https://issues.apache.org/jira/browse/CAMEL-19133)

camel-zookeeper - Zookeeper's service registration and discovery is not working with serialized

[CAMEL-19113](https://issues.apache.org/jira/browse/CAMEL-19113)

Platform-http-vertx: consume with comma separated does not work

[CAMEL-19112](https://issues.apache.org/jira/browse/CAMEL-19112)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.yaml'

[CAMEL-19111](https://issues.apache.org/jira/browse/CAMEL-19111)

Yaml DSL does not seem to work with split/xtokenize

[CAMEL-19103](https://issues.apache.org/jira/browse/CAMEL-19103)

camel-jbang - can't run in background due to No Camel integration files to run

[CAMEL-19100](https://issues.apache.org/jira/browse/CAMEL-19100)

Milo component does not use dataChangeFilterTrigger value from route

[CAMEL-19098](https://issues.apache.org/jira/browse/CAMEL-19098)

Possible performance issue invoking a bean method with a string parameter

[CAMEL-19081](https://issues.apache.org/jira/browse/CAMEL-19081)

Start a route with aggregation fails due to NPE in AggregateProcessor

[CAMEL-19075](https://issues.apache.org/jira/browse/CAMEL-19075)

camel-bean - Incorrect choice of overloaded method with several arguments, if one of them has brackets.

[CAMEL-19067](https://issues.apache.org/jira/browse/CAMEL-19067)

Camel-JBang | camel init creates file but errors out on Windows

[CAMEL-19066](https://issues.apache.org/jira/browse/CAMEL-19066)

Multicast EIP sets correlationId on original Exchange

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19031](https://issues.apache.org/jira/browse/CAMEL-19031)

When camel saga do compensated, the saga route don't stop it still run the next task.

[CAMEL-19026](https://issues.apache.org/jira/browse/CAMEL-19026)

camel-jbang - camel.main.backlogTracing=true

[CAMEL-19018](https://issues.apache.org/jira/browse/CAMEL-19018)

camel-vertx-http: Headers may get erroneously duplicated

[CAMEL-19006](https://issues.apache.org/jira/browse/CAMEL-19006)

XML IO DSL do not load templatedRoutes without XML namespace

[CAMEL-19004](https://issues.apache.org/jira/browse/CAMEL-19004)

XML IO DSL do not parse route configuration with XML namespace

[CAMEL-19002](https://issues.apache.org/jira/browse/CAMEL-19002)

camel-jbang - Log command should detect lines without timestamp

### Dependency upgrade (3)

[CAMEL-19153](https://issues.apache.org/jira/browse/CAMEL-19153)

camel-spring-boot - Upgrade to 2.7.10

[CAMEL-19125](https://issues.apache.org/jira/browse/CAMEL-19125)

camel-jbang - Upgrade to kamelets 4M1 and 3.20.2

[CAMEL-18839](https://issues.apache.org/jira/browse/CAMEL-18839)

upgrade to kafka 3.3.x

### Improvement (11)

[CAMEL-19186](https://issues.apache.org/jira/browse/CAMEL-19186)

camel-core - Type function in simple language should use enum type instead of toString value

[CAMEL-19185](https://issues.apache.org/jira/browse/CAMEL-19185)

Camel Spring Boot Example: Twitter-Salesforce: camel-salesforce-maven-plugin - make TLS version configurable via system properties

[CAMEL-19168](https://issues.apache.org/jira/browse/CAMEL-19168)

camel-micrometer-starter - Make it possible to capture static uri path as tag

[CAMEL-19144](https://issues.apache.org/jira/browse/CAMEL-19144)

camel-catalog - Include information about existing Camel releases

[CAMEL-19137](https://issues.apache.org/jira/browse/CAMEL-19137)

Favor CompositeMeterRegistry instances in Camel registry

[CAMEL-19122](https://issues.apache.org/jira/browse/CAMEL-19122)

camel-jbang - Export java code with existing package name

[CAMEL-19109](https://issues.apache.org/jira/browse/CAMEL-19109)

camel-vertx-websocket: Consumer should avoid blocking the Vert.x event loop

[CAMEL-19083](https://issues.apache.org/jira/browse/CAMEL-19083)

camel-yaml-dsl: Add a doc section that links to the schema

[CAMEL-19078](https://issues.apache.org/jira/browse/CAMEL-19078)

camel-platform-http-vertx: Allow response headers with empty values to be returned

[CAMEL-19025](https://issues.apache.org/jira/browse/CAMEL-19025)

camel-jbang - doc command should be case insensitive in filter

[CAMEL-18636](https://issues.apache.org/jira/browse/CAMEL-18636)

azure data lake component: authentication can not be configured using string properties

### New Feature (4)

[CAMEL-19128](https://issues.apache.org/jira/browse/CAMEL-19128)

camel-jbang - Version command

[CAMEL-19120](https://issues.apache.org/jira/browse/CAMEL-19120)

camel-jbang - export configurable template

[CAMEL-18508](https://issues.apache.org/jira/browse/CAMEL-18508)

camel-jbang - User config file

[CAMEL-18131](https://issues.apache.org/jira/browse/CAMEL-18131)

camel-health - Add health checks for components that has extension for connectivity verification

### Task (1)

[CAMEL-19119](https://issues.apache.org/jira/browse/CAMEL-19119)

\[Docs\] Missing examples in Camel JDBC

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).