# Apache camel 4.0.5 Release

## New and Noteworthy

This release is the new Camel 4.0.5 LTS patch release.

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
      <version>4.0.5</version>
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
      <version>4.0.5</version>
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
| [apache-camel-4.0.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-src.zip.sha512) |
| [apache-camel-4.0.5-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.xml.sha512) |
| [apache-camel-4.0.5-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.5/apache-camel-4.0.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-20435](https://issues.apache.org/jira/browse/CAMEL-20435)

camel-core - Resequencer EIP cannot be started again after being stopped

[CAMEL-20362](https://issues.apache.org/jira/browse/CAMEL-20362)

Camel-Netty-HTTP: Headers validation should be enabled by default

[CAMEL-20356](https://issues.apache.org/jira/browse/CAMEL-20356)

camel-core - LoggerHelper returns wrong name for source code line precise

[CAMEL-20350](https://issues.apache.org/jira/browse/CAMEL-20350)

camel-observation - Null values should be null instead of a string null literal value

[CAMEL-20342](https://issues.apache.org/jira/browse/CAMEL-20342)

camel-openapi-java - NPE in OpenApiHelper

[CAMEL-20301](https://issues.apache.org/jira/browse/CAMEL-20301)

Camel retains objects when restarting route via policy

[CAMEL-20254](https://issues.apache.org/jira/browse/CAMEL-20254)

camel-http - pre-emptive authentication breaks basic auth

[CAMEL-20214](https://issues.apache.org/jira/browse/CAMEL-20214)

camel-core - Timeout tasks of parallel splitter block further message processing

[CAMEL-20152](https://issues.apache.org/jira/browse/CAMEL-20152)

camel-jetty - OutOfMemoryError with big file upload via multipart

[CAMEL-20139](https://issues.apache.org/jira/browse/CAMEL-20139)

aggregate EIP: wrong correlation key set for the first aggregate exchange

[CAMEL-20124](https://issues.apache.org/jira/browse/CAMEL-20124)

camel-netty - Fix ChannelHandlerFactories' usage of unsharable ByteArrayDecoder

[CAMEL-19734](https://issues.apache.org/jira/browse/CAMEL-19734)

SEDA endpoint with multiple consumers produces strange message history from error handler

[CAMEL-18760](https://issues.apache.org/jira/browse/CAMEL-18760)

camel-kafka - Issue using ThrottlingExceptionRoutePolicy with Kafka consumer

### Dependency upgrade (2)

[CAMEL-20343](https://issues.apache.org/jira/browse/CAMEL-20343)

camel-spring-boot - Upgrade to 3.1.8

[CAMEL-20147](https://issues.apache.org/jira/browse/CAMEL-20147)

camel-spring-boot: Upgrade to 3.1.6

### Improvement (7)

[CAMEL-20363](https://issues.apache.org/jira/browse/CAMEL-20363)

camel-jms - Make getting JMSCorrelationID more robust for brokers that has bugs

[CAMEL-20306](https://issues.apache.org/jira/browse/CAMEL-20306)

Camel-CassandraQL: Add ObjectInputFilter String pattern parameter in CassandraAggregationRepository to be used in unmarshall operations

[CAMEL-20303](https://issues.apache.org/jira/browse/CAMEL-20303)

Camel-Sql: Add ObjectInputFilter String pattern parameter in JdbcAggregationRepository to be used in unmarshall operations

[CAMEL-20209](https://issues.apache.org/jira/browse/CAMEL-20209)

camel-azure - Adopt atomic overwrite feature of Azure Files

[CAMEL-20205](https://issues.apache.org/jira/browse/CAMEL-20205)

Add SBOM to release and release-sbom script to LTS 4.0.x, 3.22.x and 3.21.x

[CAMEL-20114](https://issues.apache.org/jira/browse/CAMEL-20114)

camel-salesforce: generatePubSub plugin goal should clean up temporary schema JSON files

[CAMEL-20107](https://issues.apache.org/jira/browse/CAMEL-20107)

camel-salesforce: PubSubApiConsumer may fail to load pojo class

### Task (2)

[CAMEL-20305](https://issues.apache.org/jira/browse/CAMEL-20305)

camel-core: ensure log consistency

[CAMEL-20261](https://issues.apache.org/jira/browse/CAMEL-20261)

camel-http ignoreCookies option value has been renamed

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).