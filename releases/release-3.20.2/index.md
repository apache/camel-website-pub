# Apache camel 3.20.2 Release

## New and Noteworthy

This release is the new Camel 3.20.2 LTS patch release.

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
      <version>3.20.2</version>
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
      <version>3.20.2</version>
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
| [apache-camel-3.20.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.2/apache-camel-3.20.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.2/apache-camel-3.20.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.2/apache-camel-3.20.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (12)

[CAMEL-18980](https://issues.apache.org/jira/browse/CAMEL-18980)

camel snmp - SNMP Ver1 trap does not work

[CAMEL-18968](https://issues.apache.org/jira/browse/CAMEL-18968)

Camel-aws2-sqs - Queue url might stay empty for the delayed queue.

[CAMEL-18954](https://issues.apache.org/jira/browse/CAMEL-18954)

camel-micrometer - NPE on spring boot

[CAMEL-18922](https://issues.apache.org/jira/browse/CAMEL-18922)

TemplatedRoute fails to load with XML RouteLoader

[CAMEL-18878](https://issues.apache.org/jira/browse/CAMEL-18878)

Autowiring on endpoint works even if is disabled on component

[CAMEL-18872](https://issues.apache.org/jira/browse/CAMEL-18872)

camel-core-model - Rest DSL param example not available in XML and YAML DSL

[CAMEL-18871](https://issues.apache.org/jira/browse/CAMEL-18871)

camel-netty - Application does not recover (threads are WAITING) when NettyProducer pool is exhausted

[CAMEL-18868](https://issues.apache.org/jira/browse/CAMEL-18868)

Aws2-s3: CreateDownloadLink does not work with useDefaultCredentialsProvider

[CAMEL-18865](https://issues.apache.org/jira/browse/CAMEL-18865)

camel-main - Setters not invoked on bean that implements Map

[CAMEL-18856](https://issues.apache.org/jira/browse/CAMEL-18856)

camel-main - Unable to declare java.util.List bean

[CAMEL-18854](https://issues.apache.org/jira/browse/CAMEL-18854)

camel-rabbitmq x-queue-type no longer working

[CAMEL-18780](https://issues.apache.org/jira/browse/CAMEL-18780)

Sqs2Consumer message extended causing rejected execution exception when used with threads EIP

### Dependency upgrade (2)

[CAMEL-18999](https://issues.apache.org/jira/browse/CAMEL-18999)

camel-sshd - Upgrade to 2.9.x

[CAMEL-18947](https://issues.apache.org/jira/browse/CAMEL-18947)

camel-spring-boot - Upgrade to 2.7.8

### Improvement (9)

[CAMEL-19001](https://issues.apache.org/jira/browse/CAMEL-19001)

camel-jbang - Backport 3.21 fixes and others to 3.20.x

[CAMEL-18990](https://issues.apache.org/jira/browse/CAMEL-18990)

camel-jbang - Export to Quarkus should add resources for native compilation

[CAMEL-18967](https://issues.apache.org/jira/browse/CAMEL-18967)

camel-platform-http-vertx: Improve handling of whether an HTTP request body is allowed or not

[CAMEL-18952](https://issues.apache.org/jira/browse/CAMEL-18952)

camel-rest - Favour using platform-http if available on classpath

[CAMEL-18942](https://issues.apache.org/jira/browse/CAMEL-18942)

openapi-rest-dsl-generator - Copy the description of the path/operation to the generated route

[CAMEL-18912](https://issues.apache.org/jira/browse/CAMEL-18912)

Sqs2ConsumerHealthCheck is broken when using injected client

[CAMEL-18862](https://issues.apache.org/jira/browse/CAMEL-18862)

Using Spring Boot Camel Starter the RoutesCollector doesn't see RoutesBuilder added via Camel Context Registry

[CAMEL-18815](https://issues.apache.org/jira/browse/CAMEL-18815)

camel-jbang - Base package scan to search in downloaded JARs

[CAMEL-18674](https://issues.apache.org/jira/browse/CAMEL-18674)

camel-jbang - Run in background

### New Feature (6)

[CAMEL-18989](https://issues.apache.org/jira/browse/CAMEL-18989)

camel-jbang - Run custom distributions of Camel

[CAMEL-18909](https://issues.apache.org/jira/browse/CAMEL-18909)

Add DTO generator option in camel-jbang generate command

[CAMEL-18538](https://issues.apache.org/jira/browse/CAMEL-18538)

camel-jbang - Add log command

[CAMEL-18523](https://issues.apache.org/jira/browse/CAMEL-18523)

camel-jbang - Add watch option

[CAMEL-18497](https://issues.apache.org/jira/browse/CAMEL-18497)

camel-jbang - camel run -v x.y.z

[CAMEL-18131](https://issues.apache.org/jira/browse/CAMEL-18131)

camel-health - Add health checks for components that has extension for connectivity verification

### Sub-task (1)

[CAMEL-18991](https://issues.apache.org/jira/browse/CAMEL-18991)

Camel-Google-Storage: Health Check for consumer

### Task (1)

[CAMEL-18996](https://issues.apache.org/jira/browse/CAMEL-18996)

Camel-CassandraQL: Adding a parameter to pass a list of ExtraTypesCodec to SessionBuilder

### Test (1)

[CAMEL-18960](https://issues.apache.org/jira/browse/CAMEL-18960)

CxfRsEndpointWithPropertiesTest is broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).