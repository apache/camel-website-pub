# Apache camel 4.10.1 Release

## New and Noteworthy

This release is the new Camel 4.10.1 release.

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
      <version>4.10.1</version>
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
      <version>4.10.1</version>
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
| [apache-camel-4.10.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-src.zip.sha512) |
| [apache-camel-4.10.1-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.xml.sha512) |
| [apache-camel-4.10.1-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.1/apache-camel-4.10.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (25)

[CAMEL-21807](https://issues.apache.org/jira/browse/CAMEL-21807)

camel-kamelet - Custom kamelet with dynamic query parameter with sql component

[CAMEL-21800](https://issues.apache.org/jira/browse/CAMEL-21800)

camel-smb - The scheduler options cannot be configured on the consumer

[CAMEL-21799](https://issues.apache.org/jira/browse/CAMEL-21799)

camel-coap - Exchange retrieve only the last block of Blockwise

[CAMEL-21794](https://issues.apache.org/jira/browse/CAMEL-21794)

camel-jbang - Export bean with lazy-bean should not initialize the bean if not needed

[CAMEL-21793](https://issues.apache.org/jira/browse/CAMEL-21793)

camel-kamelets - Kamelets and excessive load causes ConcurrentModificationException

[CAMEL-21792](https://issues.apache.org/jira/browse/CAMEL-21792)

camel-aws - KCL Kinesis Consumer fails with NPE when using custom async client

[CAMEL-21790](https://issues.apache.org/jira/browse/CAMEL-21790)

camel-kafka - Race condition in KafkaProducerMetadataCallBack

[CAMEL-21780](https://issues.apache.org/jira/browse/CAMEL-21780)

camel-core - Java DSL - StackOverflowError with Enrich EIP and assigning id

[CAMEL-21778](https://issues.apache.org/jira/browse/CAMEL-21778)

camel-core - Java DSL using id in processors after Threads EIP is not assigned

[CAMEL-21776](https://issues.apache.org/jira/browse/CAMEL-21776)

camel-core - DefaultRoute does not gather services for onException/onCompletion

[CAMEL-21775](https://issues.apache.org/jira/browse/CAMEL-21775)

Split or Multicast in onException route cannot be started using Supervised route controller

[CAMEL-21770](https://issues.apache.org/jira/browse/CAMEL-21770)

camel-kubernetes: Autowired KubernetesClient should not be closed

[CAMEL-21769](https://issues.apache.org/jira/browse/CAMEL-21769)

camel-aws-sqs - Error is causing the sqs message to be extended forever

[CAMEL-21758](https://issues.apache.org/jira/browse/CAMEL-21758)

camel-jms - TemporaryQueueReplyManager does not inherit doStop method

[CAMEL-21755](https://issues.apache.org/jira/browse/CAMEL-21755)

Enrich with exchangepattern=InOut doesn't return enriched body.

[CAMEL-21754](https://issues.apache.org/jira/browse/CAMEL-21754)

camel-mail - ClassCastException if using DEBUG logging

[CAMEL-21752](https://issues.apache.org/jira/browse/CAMEL-21752)

camel-smb - DFS doesn't work because SmbConfig cannot be set for smbclient

[CAMEL-21747](https://issues.apache.org/jira/browse/CAMEL-21747)

camel-debug - On timeout then remove suspended breakpoint state

[CAMEL-21746](https://issues.apache.org/jira/browse/CAMEL-21746)

When starting camel in standalone mode, configureVaultRefresh is called twice (thus refresh task is started twice)

[CAMEL-21740](https://issues.apache.org/jira/browse/CAMEL-21740)

camel-salesforce - pub/sub API corrupt replay id causes infinite resubscribe loop

[CAMEL-21739](https://issues.apache.org/jira/browse/CAMEL-21739)

camel-ftp - Implementation of GenericFileConsumer.getRelativeFilePath differs in camel-ftp to camel-file

[CAMEL-21737](https://issues.apache.org/jira/browse/CAMEL-21737)

camel-kubernetes: Multiple consumers are using the k8s client incorrectly

[CAMEL-21732](https://issues.apache.org/jira/browse/CAMEL-21732)

camel-core - Poll EIP with dynamic simple language uri does not work

[CAMEL-21730](https://issues.apache.org/jira/browse/CAMEL-21730)

JBang export cannot validate route that depends on copied resources

[CAMEL-21662](https://issues.apache.org/jira/browse/CAMEL-21662)

Camel JBang - run with Spring boot / Quarkus fails on Windows

### Dependency upgrade (1)

[CAMEL-21772](https://issues.apache.org/jira/browse/CAMEL-21772)

camel-spring-boot - Upgrade to 3.4.3

### Improvement (8)

[CAMEL-21788](https://issues.apache.org/jira/browse/CAMEL-21788)

camel-kafka - Turn recordMetadata off by default

[CAMEL-21785](https://issues.apache.org/jira/browse/CAMEL-21785)

camel-main: Generate configurer classes for Kubernetes vault configuration

[CAMEL-21782](https://issues.apache.org/jira/browse/CAMEL-21782)

camel-file - The autoCreate option should be moved to doStart

[CAMEL-21779](https://issues.apache.org/jira/browse/CAMEL-21779)

camel-smb - The consumer should also support autoCreate

[CAMEL-21761](https://issues.apache.org/jira/browse/CAMEL-21761)

Significantly speed up MavenDependencyDownloader

[CAMEL-21757](https://issues.apache.org/jira/browse/CAMEL-21757)

camel-kafka - Camel kafka Transactional ID with consumersCount>1 is not possible

[CAMEL-21734](https://issues.apache.org/jira/browse/CAMEL-21734)

camel-csv - Allow to configurer header via CsvFormat reference

[CAMEL-21729](https://issues.apache.org/jira/browse/CAMEL-21729)

camel-jbang - dependency list - Add update command to change the pom.xml

### New Feature (1)

[CAMEL-21723](https://issues.apache.org/jira/browse/CAMEL-21723)

camel-jbang shell edit command

### Task (5)

[CAMEL-21795](https://issues.apache.org/jira/browse/CAMEL-21795)

Camel-AWS components: Adding STS dependency out of the box since it is used in case of DefaultCredentialsProvider

[CAMEL-21789](https://issues.apache.org/jira/browse/CAMEL-21789)

High Memory Usage During Gradle Dependency Resolution

[CAMEL-21756](https://issues.apache.org/jira/browse/CAMEL-21756)

camel-jbang - Upgrade maven wrapper

[CAMEL-21750](https://issues.apache.org/jira/browse/CAMEL-21750)

camel-google - Avoid using their BOM as it has a huge dependency and cause slowness on builds

[CAMEL-21748](https://issues.apache.org/jira/browse/CAMEL-21748)

Upgrade to Camel-Kamelets 4.10.0 in camel-jbang

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).