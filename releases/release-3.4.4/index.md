# Apache camel 3.4.4 Release

## New and Noteworthy

This release is the new Camel 3.4.4 patch release.

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
      <version>3.4.4</version>
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
      <version>3.4.4</version>
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
| [apache-camel-3.4.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.4/apache-camel-3.4.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.4/apache-camel-3.4.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.4/apache-camel-3.4.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (22)

[CAMEL-15563](https://issues.apache.org/jira/browse/CAMEL-15563)

Sensitive keys are logged in auto-configuration summary

[CAMEL-15557](https://issues.apache.org/jira/browse/CAMEL-15557)

Multicast parallel processing with timeout: Stream Cache file not deleted if CachedOutputStream created before timeout and writing to CachedOutputStream happens after timeout

[CAMEL-15547](https://issues.apache.org/jira/browse/CAMEL-15547)

Wrong URI with http dsl and query parameters

[CAMEL-15534](https://issues.apache.org/jira/browse/CAMEL-15534)

Camel-telegram wrongly parse chatId from headers

[CAMEL-15532](https://issues.apache.org/jira/browse/CAMEL-15532)

Multicast parallel processing with timeout: Stream Cache file not deleted

[CAMEL-15530](https://issues.apache.org/jira/browse/CAMEL-15530)

AWS2 S3 Component unclosed stream issue with includeFolders property

[CAMEL-15525](https://issues.apache.org/jira/browse/CAMEL-15525)

camel-archetype-java: main class on pom file different than actual main class

[CAMEL-15521](https://issues.apache.org/jira/browse/CAMEL-15521)

InfluxDB connection bean creation fails

[CAMEL-15500](https://issues.apache.org/jira/browse/CAMEL-15500)

camel-azure-storage-blob: wrong syntax in the component json

[CAMEL-15493](https://issues.apache.org/jira/browse/CAMEL-15493)

Camel-Cdi throws NPE when attempting to inject an array property using Microprofile Config

[CAMEL-15489](https://issues.apache.org/jira/browse/CAMEL-15489)

camel-sql - Persistence Aggregator not compatible with Oracle-Java Data Type

[CAMEL-15473](https://issues.apache.org/jira/browse/CAMEL-15473)

Spring Boot Swagger Example - API specification generation fails

[CAMEL-15460](https://issues.apache.org/jira/browse/CAMEL-15460)

FTP Reconnect not successful

[CAMEL-15455](https://issues.apache.org/jira/browse/CAMEL-15455)

EndpointDSL breaks expressions in query parameters

[CAMEL-15449](https://issues.apache.org/jira/browse/CAMEL-15449)

camel-salesforce - BulkAPI createBatchQuery swallows error

[CAMEL-15445](https://issues.apache.org/jira/browse/CAMEL-15445)

component lifecycle is differen when endpoints are created using endpointdsl

[CAMEL-15436](https://issues.apache.org/jira/browse/CAMEL-15436)

camel-azure-storage-blob: If the AppendFile does not exist, it will be created but it will not append to the end of the content

[CAMEL-15425](https://issues.apache.org/jira/browse/CAMEL-15425)

camel-salesforce: SalesforceLoginConfig seems to be leaking the password

[CAMEL-15424](https://issues.apache.org/jira/browse/CAMEL-15424)

camel-box: addFolderCollaboration may throw an NPE

[CAMEL-15420](https://issues.apache.org/jira/browse/CAMEL-15420)

camel-http dynamic aware removes Exchange.HTTP\_QUERY header if Exchange.HTTP\_PATH header not specified

[CAMEL-15400](https://issues.apache.org/jira/browse/CAMEL-15400)

rest component - Endpoint DSL for multi valued has null as prefix

[CAMEL-15391](https://issues.apache.org/jira/browse/CAMEL-15391)

camel-aws2-sqs: amazonAWSHost is not set

### Improvement (3)

[CAMEL-15511](https://issues.apache.org/jira/browse/CAMEL-15511)

Camel-AHC: Wrapper async-http-client jars in camel-karaf feature are bundle

[CAMEL-15418](https://issues.apache.org/jira/browse/CAMEL-15418)

Support for enriching the Swagger API Document

[CAMEL-15415](https://issues.apache.org/jira/browse/CAMEL-15415)

Upgrade to spring boot 2.3.3

### New Feature (1)

[CAMEL-15428](https://issues.apache.org/jira/browse/CAMEL-15428)

Create a proper camel BOM (for camel-spring-boot)

### Task (4)

[CAMEL-15461](https://issues.apache.org/jira/browse/CAMEL-15461)

Upgrade to jedis bundle 3.3.0\_2

[CAMEL-15441](https://issues.apache.org/jira/browse/CAMEL-15441)

Upgrade spring-data bundles version to 2.3.x in features repositorry

[CAMEL-15440](https://issues.apache.org/jira/browse/CAMEL-15440)

Use elasticsearch unique bundle (not client anymore)

[CAMEL-14918](https://issues.apache.org/jira/browse/CAMEL-14918)

camel-cdi - Avoid @Resource injection

### Test (1)

[CAMEL-15403](https://issues.apache.org/jira/browse/CAMEL-15403)

camel-xmlsecurity - Some unit tests fails with Oracle JDK8 261

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).