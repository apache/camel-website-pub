# Apache camel 4.8.4 Release

## New and Noteworthy

This release is the new Camel 4.8.4 release.

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
      <version>4.8.4</version>
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
      <version>4.8.4</version>
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
| [apache-camel-4.8.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-src.zip.sha512) |
| [apache-camel-4.8.4-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.xml.sha512) |
| [apache-camel-4.8.4-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.4/apache-camel-4.8.4-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (20)

[CAMEL-21799](https://issues.apache.org/jira/browse/CAMEL-21799)

camel-coap - Exchange retrieve only the last block of Blockwise

[CAMEL-21790](https://issues.apache.org/jira/browse/CAMEL-21790)

camel-kafka - Race condition in KafkaProducerMetadataCallBack

[CAMEL-21778](https://issues.apache.org/jira/browse/CAMEL-21778)

camel-core - Java DSL using id in processors after Threads EIP is not assigned

[CAMEL-21776](https://issues.apache.org/jira/browse/CAMEL-21776)

camel-core - DefaultRoute does not gather services for onException/onCompletion

[CAMEL-21775](https://issues.apache.org/jira/browse/CAMEL-21775)

Split or Multicast in onException route cannot be started using Supervised route controller

[CAMEL-21769](https://issues.apache.org/jira/browse/CAMEL-21769)

camel-aws-sqs - Error is causing the sqs message to be extended forever

[CAMEL-21758](https://issues.apache.org/jira/browse/CAMEL-21758)

camel-jms - TemporaryQueueReplyManager does not inherit doStop method

[CAMEL-21747](https://issues.apache.org/jira/browse/CAMEL-21747)

camel-debug - On timeout then remove suspended breakpoint state

[CAMEL-21740](https://issues.apache.org/jira/browse/CAMEL-21740)

camel-salesforce - pub/sub API corrupt replay id causes infinite resubscribe loop

[CAMEL-21730](https://issues.apache.org/jira/browse/CAMEL-21730)

JBang export cannot validate route that depends on copied resources

[CAMEL-21687](https://issues.apache.org/jira/browse/CAMEL-21687)

camel-core - Cannot add onCompletion after transacted in Java DSL

[CAMEL-21684](https://issues.apache.org/jira/browse/CAMEL-21684)

camel-rest-openapi - Using x-forward headers is not included

[CAMEL-21662](https://issues.apache.org/jira/browse/CAMEL-21662)

Camel JBang - run with Spring boot / Quarkus fails on Windows

[CAMEL-21656](https://issues.apache.org/jira/browse/CAMEL-21656)

camel-jms - Multiple routes with direct/activemq and recipientlist returns unexpected result

[CAMEL-21653](https://issues.apache.org/jira/browse/CAMEL-21653)

Camel Jbang run ignore "--repos" option

[CAMEL-21614](https://issues.apache.org/jira/browse/CAMEL-21614)

Simple expressions execute forever. Thread is RUNNABLE for ever. Issue appears with bean expressions inside simple expressions on SimpleLRUCache

[CAMEL-21606](https://issues.apache.org/jira/browse/CAMEL-21606)

Camel route validation mojo fails if it depends on external sources

[CAMEL-21594](https://issues.apache.org/jira/browse/CAMEL-21594)

Camel Langchain4j Tools bug where no need to execute a tool

[CAMEL-21505](https://issues.apache.org/jira/browse/CAMEL-21505)

camel-as2: Binary files get corrupt when using 'base64' content transfer encoding

[CAMEL-21442](https://issues.apache.org/jira/browse/CAMEL-21442)

camel-jbang export is not working when local-kamelet-dir set to current dir

### Dependency upgrade (3)

[CAMEL-21773](https://issues.apache.org/jira/browse/CAMEL-21773)

camel-spring-boot - Upgrade to 3.3.9

[CAMEL-21607](https://issues.apache.org/jira/browse/CAMEL-21607)

camel-quickfix - Upgrade to 2.3.2

[CAMEL-21603](https://issues.apache.org/jira/browse/CAMEL-21603)

camel-spring-boot - Upgrade to 3.3.8

### Improvement (7)

[CAMEL-21761](https://issues.apache.org/jira/browse/CAMEL-21761)

Significantly speed up MavenDependencyDownloader

[CAMEL-21757](https://issues.apache.org/jira/browse/CAMEL-21757)

camel-kafka - Camel kafka Transactional ID with consumersCount>1 is not possible

[CAMEL-21714](https://issues.apache.org/jira/browse/CAMEL-21714)

camel-cxf: CachedCxfPayload needs to LOG the parsing XMLStreamReader exception

[CAMEL-21661](https://issues.apache.org/jira/browse/CAMEL-21661)

camel-micrometer - multiple registrations of gauge camel.exchanges.inflight

[CAMEL-21659](https://issues.apache.org/jira/browse/CAMEL-21659)

Improve aws sqs TimeoutExtender by introducing deadline concept to messages

[CAMEL-21634](https://issues.apache.org/jira/browse/CAMEL-21634)

camel-jbang - Add camel-quartz as dependency if using camel-cron

[CAMEL-21608](https://issues.apache.org/jira/browse/CAMEL-21608)

Add support for message tags to Amazon SES component

### Task (5)

[CAMEL-21750](https://issues.apache.org/jira/browse/CAMEL-21750)

camel-google - Avoid using their BOM as it has a huge dependency and cause slowness on builds

[CAMEL-21727](https://issues.apache.org/jira/browse/CAMEL-21727)

documentation - Add note in docs to not use crazy high loop counter

[CAMEL-21689](https://issues.apache.org/jira/browse/CAMEL-21689)

Apache Camel Kafka Batching Consumer behaviour discrepancy w.r.t pollTimeoutMs

[CAMEL-21664](https://issues.apache.org/jira/browse/CAMEL-21664)

camel-kafka: avoid unecessary secondary cache miss on record metadata

[CAMEL-21663](https://issues.apache.org/jira/browse/CAMEL-21663)

camel-sjms2: lack of null check causes NPE and affects performance

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).