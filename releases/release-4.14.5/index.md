# Apache camel 4.14.5 Release

## New and Noteworthy

This release is the new Camel 4.14.5 LTS release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.14.5</version>
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
      <version>4.14.5</version>
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
| [apache-camel-4.14.5-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.5/apache-camel-4.14.5-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-src.zip.sha512) |
| [apache-camel-4.14.5-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.xml.sha512) |
| [apache-camel-4.14.5-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.14.5/apache-camel-4.14.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (16)

[CAMEL-22950](https://issues.apache.org/jira/browse/CAMEL-22950)

RecipientList with UseOriginalAggregationStrategy fails to capture exception with NPE

[CAMEL-22947](https://issues.apache.org/jira/browse/CAMEL-22947)

Camel-Google-pubsub: consumer does not properly trigger ACK/NACK callbacks and lacks deliveryAttempt visibility

[CAMEL-22939](https://issues.apache.org/jira/browse/CAMEL-22939)

camel-jbang: observe flag ignored when camel.jbang.dependencies is set

[CAMEL-22936](https://issues.apache.org/jira/browse/CAMEL-22936)

camel-spring-boot - camel health check breaks if one component has exception without message

[CAMEL-22926](https://issues.apache.org/jira/browse/CAMEL-22926)

GooglePubsubProducer applies HeaderFilterStrategy incorrectly, causing Camel headers to leak as Pub/Sub attributes

[CAMEL-22916](https://issues.apache.org/jira/browse/CAMEL-22916)

camel-ftp - RemoteFileProducer ignores NOOP result when sendNoop() returns false without exception

[CAMEL-22874](https://issues.apache.org/jira/browse/CAMEL-22874)

Error handler in openapi-contract-first route is invoked twice when using handled(false)

[CAMEL-22849](https://issues.apache.org/jira/browse/CAMEL-22849)

AS2 server/listen does not resolve requestUriPattern wildcards when selecting consumer configuration

[CAMEL-22848](https://issues.apache.org/jira/browse/CAMEL-22848)

camel-file: checksumFileAlgorithm option is ignored due to missing mapping in GenericFileEndpoint

[CAMEL-22833](https://issues.apache.org/jira/browse/CAMEL-22833)

camel-jbang - Yaml DSL file with only templatedRoute is not loaded

[CAMEL-22828](https://issues.apache.org/jira/browse/CAMEL-22828)

camel-main - camel.main.endpoint-runtime-statistics-enabled not working since Camel 4.5

[CAMEL-22824](https://issues.apache.org/jira/browse/CAMEL-22824)

camel-core - Choice with bodyAs predicate may cause stream caching to be EOL

[CAMEL-22823](https://issues.apache.org/jira/browse/CAMEL-22823)

Ensure Null Response Entity will be honored when StreamCache kicks in

[CAMEL-22820](https://issues.apache.org/jira/browse/CAMEL-22820)

routeConfiguration onException does not propagate to direct endpoints for consumer-level exceptions

[CAMEL-22784](https://issues.apache.org/jira/browse/CAMEL-22784)

Failover in FileLockClusterService is unreliable when running multiple JVMs

[CAMEL-22429](https://issues.apache.org/jira/browse/CAMEL-22429)

camel-aws2-sns component fails when sending CloudEvents with subjects over 100 characters

### Dependency upgrade (1)

[CAMEL-22896](https://issues.apache.org/jira/browse/CAMEL-22896)

camel-spring-boot - Upgrade to Spring Boot 3.5.10

### Improvement (5)

[CAMEL-22977](https://issues.apache.org/jira/browse/CAMEL-22977)

DefaultCxfBinding: also populate credentials

[CAMEL-22966](https://issues.apache.org/jira/browse/CAMEL-22966)

Camel-LevelDB: Add ObjectInputFilter String pattern parameter in LevelDBAggregationRepository to be used in unmarshall operations

[CAMEL-22927](https://issues.apache.org/jira/browse/CAMEL-22927)

camel-sql endpoint opening unnecessary connections to the database if service location is enabled

[CAMEL-22925](https://issues.apache.org/jira/browse/CAMEL-22925)

Enhance S3 producer to stream the payload of type GenericFile

[CAMEL-22832](https://issues.apache.org/jira/browse/CAMEL-22832)

camel-azure-storage-blob: upload big files using uploadBlockBlobFromFile

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).