# Apache camel 4.0.2 Release

## New and Noteworthy

This release is the new Camel 4.0.2 LTS patch release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.0.2</version>
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
      <version>4.0.2</version>
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
| [apache-camel-4.0.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.2/apache-camel-4.0.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.2/apache-camel-4.0.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.2/apache-camel-4.0.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (12)

[CAMEL-20023](https://issues.apache.org/jira/browse/CAMEL-20023)

camel-file - File readLock changed minAge issue

[CAMEL-20010](https://issues.apache.org/jira/browse/CAMEL-20010)

camel-sql - Can't change table name in JdbcMessageIdRepository by adding suffix/prefix

[CAMEL-19996](https://issues.apache.org/jira/browse/CAMEL-19996)

camel-lra NullPointerException when creating a saga with invalid lra-url

[CAMEL-19975](https://issues.apache.org/jira/browse/CAMEL-19975)

NIOConverter File to ByteBuffer conversion behavior is potentially non-deterministic

[CAMEL-19970](https://issues.apache.org/jira/browse/CAMEL-19970)

camel-jbang - IllegalArgumentException: Unable to determine file extension for resource when a file has no extension

[CAMEL-19968](https://issues.apache.org/jira/browse/CAMEL-19968)

camel-opentelemetry - The Tracing Strategy is failing when using pollEnrich with seda endpoint

[CAMEL-19967](https://issues.apache.org/jira/browse/CAMEL-19967)

camel-core - Default RouteConfigurationBuilder written in Java not enabled on XML routes

[CAMEL-19957](https://issues.apache.org/jira/browse/CAMEL-19957)

camel-jbang - On demand reload is not updating kamelets/routes

[CAMEL-19938](https://issues.apache.org/jira/browse/CAMEL-19938)

JBang camel CLI not working when using "run" option on Windows environments

[CAMEL-19931](https://issues.apache.org/jira/browse/CAMEL-19931)

camel-jbang - Reload with custom kamelet cannot find on update

[CAMEL-19918](https://issues.apache.org/jira/browse/CAMEL-19918)

camel-spring-boot - XPath language configuring saxon=true seems to not work

[CAMEL-19910](https://issues.apache.org/jira/browse/CAMEL-19910)

camel-jbang - Export may include hidden files

### Dependency upgrade (6)

[CAMEL-19990](https://issues.apache.org/jira/browse/CAMEL-19990)

camel-spring-boot - Upgrade to 3.1.5

[CAMEL-19980](https://issues.apache.org/jira/browse/CAMEL-19980)

Upgrade Infinispan to version 14.0.18.Final

[CAMEL-19979](https://issues.apache.org/jira/browse/CAMEL-19979)

Upgrade Vertx to version 4.4.6

[CAMEL-19978](https://issues.apache.org/jira/browse/CAMEL-19978)

Upgrade Netty to 4.1.100.Final

[CAMEL-19930](https://issues.apache.org/jira/browse/CAMEL-19930)

Camel-Jbang: Upgrade to Camel-Kamelets 4.0.1

[CAMEL-19920](https://issues.apache.org/jira/browse/CAMEL-19920)

camel-mina - Upgrade to newer versions

### Improvement (6)

[CAMEL-20013](https://issues.apache.org/jira/browse/CAMEL-20013)

AdviceWith requires camel-xml-io

[CAMEL-19988](https://issues.apache.org/jira/browse/CAMEL-19988)

camel-core - PropertyBindingSupport - Should not hide IllegalArgumentException with real cause if failing to set property

[CAMEL-19987](https://issues.apache.org/jira/browse/CAMEL-19987)

camel-core - Optimize EndpointHelper.matchEndpoint to avoid regexp

[CAMEL-19940](https://issues.apache.org/jira/browse/CAMEL-19940)

camel-jbang - init should create .camel-jbang folder

[CAMEL-19929](https://issues.apache.org/jira/browse/CAMEL-19929)

camel-main - Dev console for upload should support sub folders

[CAMEL-19919](https://issues.apache.org/jira/browse/CAMEL-19919)

camel-kafka: provided an out of the box byte\[\] to String header deserializer

### New Feature (1)

[CAMEL-19907](https://issues.apache.org/jira/browse/CAMEL-19907)

Introduce the ability to use the old Micrometer meter names or follow the new Micrometer naming conventions

### Task (4)

[CAMEL-19962](https://issues.apache.org/jira/browse/CAMEL-19962)

Camel-Azure-Datalake: Headers metadata are wrong

[CAMEL-19921](https://issues.apache.org/jira/browse/CAMEL-19921)

Update default values of kafka client configuration

[CAMEL-19909](https://issues.apache.org/jira/browse/CAMEL-19909)

camel-catalog: model catalog refers to not-existing DescriptionDefinition javaType

[CAMEL-19908](https://issues.apache.org/jira/browse/CAMEL-19908)

camel-quarkus-azure-servicebus - Fix typo in docs

### Test (1)

[CAMEL-19935](https://issues.apache.org/jira/browse/CAMEL-19935)

camel-cxf - Upgrade to 4.0.3 is causing some CI test errors

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).