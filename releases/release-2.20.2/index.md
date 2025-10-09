# Apache camel 2.20.2 Release

## New and Noteworthy

This release is a minor update of the 2.20.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.20.2</version>
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
      <version>2.20.2</version>
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
| [apache-camel-2.20.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.20.2/apache-camel-2.20.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.20.2/apache-camel-2.20.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.20.2/apache-camel-2.20.2-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.20.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.20.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (26)

[CAMEL-12149](https://issues.apache.org/jira/browse/CAMEL-12149)

Failed to invoke camel cxfrs client due to Content-Type header couldn't be retrieved and passed

[CAMEL-12134](https://issues.apache.org/jira/browse/CAMEL-12134)

spring-boot: two camel contexts created when using xml configuration

[CAMEL-12131](https://issues.apache.org/jira/browse/CAMEL-12131)

CacheProducer should not put services in Camel context, that are not singletons and are not ServicePoolAware

[CAMEL-12112](https://issues.apache.org/jira/browse/CAMEL-12112)

Camel processing single file twice in 'file' endpoint

[CAMEL-12111](https://issues.apache.org/jira/browse/CAMEL-12111)

Reconnect doesn't work if camel is started with rabbit broker initially inaccessible and automaticRecoveryEnabled=true or not set

[CAMEL-12098](https://issues.apache.org/jira/browse/CAMEL-12098)

URISyntaxException in OpenTracingTracer for endpoints with path parameters

[CAMEL-12097](https://issues.apache.org/jira/browse/CAMEL-12097)

Combination of path param and query param does not work

[CAMEL-12096](https://issues.apache.org/jira/browse/CAMEL-12096)

RestConfiguration hostNameResolver property naming mismatch

[CAMEL-12094](https://issues.apache.org/jira/browse/CAMEL-12094)

fileExist=Move and tempFileName does not work together.

[CAMEL-12086](https://issues.apache.org/jira/browse/CAMEL-12086)

Service call definition - Simple language expresion in uri is not being evaluated

[CAMEL-12082](https://issues.apache.org/jira/browse/CAMEL-12082)

Camel route commands should set the TCCL when working with local camel context

[CAMEL-12075](https://issues.apache.org/jira/browse/CAMEL-12075)

Piling up of threads in iterating splitter in pararllel processing

[CAMEL-12072](https://issues.apache.org/jira/browse/CAMEL-12072)

Netty version in Camel 2.20.0+ not comptatable with Netty in camel-etcd component

[CAMEL-12069](https://issues.apache.org/jira/browse/CAMEL-12069)

ActiveMQ/JMS component: transferExchange option does not transfer exchange properties anymore

[CAMEL-12057](https://issues.apache.org/jira/browse/CAMEL-12057)

camel-olingo2 - Missing encoding for query params

[CAMEL-12038](https://issues.apache.org/jira/browse/CAMEL-12038)

rest-dsl - Allow to turn off vendor extension... NPE

[CAMEL-12037](https://issues.apache.org/jira/browse/CAMEL-12037)

File idempotent repository is always initialized with default 1000 cache size

[CAMEL-12031](https://issues.apache.org/jira/browse/CAMEL-12031)

KafkaConsumer stops consuming messages when exception occurs during offset commit

[CAMEL-12028](https://issues.apache.org/jira/browse/CAMEL-12028)

Flink requires internals to be visible by TCCL

[CAMEL-12025](https://issues.apache.org/jira/browse/CAMEL-12025)

Possible Intermittent failures in ReactorStreamsServiceTest

[CAMEL-12021](https://issues.apache.org/jira/browse/CAMEL-12021)

ProducerTemplate.requestBody with responseType throw a InvalidPayloadException instead of original exception (wrapped in a CamelExecutionException)

[CAMEL-12017](https://issues.apache.org/jira/browse/CAMEL-12017)

Google PubSub and BigQuery components miss dependency declarations

[CAMEL-12016](https://issues.apache.org/jira/browse/CAMEL-12016)

Invalid Pool Exhausted error on camel-netty4

[CAMEL-12009](https://issues.apache.org/jira/browse/CAMEL-12009)

Bindy - Missing Headers from OneToMany Field

[CAMEL-11792](https://issues.apache.org/jira/browse/CAMEL-11792)

New ftp connection for each file transfer with tempFileName option in URI

[CAMEL-10165](https://issues.apache.org/jira/browse/CAMEL-10165)

DefaultCxfMessageMapper.getBasePath creates a incorrect http path

### Improvement (10)

[CAMEL-12154](https://issues.apache.org/jira/browse/CAMEL-12154)

Camel does not set Saxon parameters in a XQuery 3.0 compatible way

[CAMEL-12113](https://issues.apache.org/jira/browse/CAMEL-12113)

Camel healthcheck spring-boot actuators don't honor "endpoints.\*.enabled" property

[CAMEL-12110](https://issues.apache.org/jira/browse/CAMEL-12110)

KafkaConsumer swallows exceptions from org.apache.kafka.clients.consumer.KafkaConsumer constructor

[CAMEL-12090](https://issues.apache.org/jira/browse/CAMEL-12090)

camel-kafka - Better error if brokers not configured

[CAMEL-12056](https://issues.apache.org/jira/browse/CAMEL-12056)

Add NotifyBuilder.destroy() method

[CAMEL-12046](https://issues.apache.org/jira/browse/CAMEL-12046)

camel-catalog - Add to plugin custom JSonSchemaResolver

[CAMEL-12029](https://issues.apache.org/jira/browse/CAMEL-12029)

CoAP component should handle method not allowed

[CAMEL-12019](https://issues.apache.org/jira/browse/CAMEL-12019)

camel-kafka - Add option max.poll.interval.ms

[CAMEL-12010](https://issues.apache.org/jira/browse/CAMEL-12010)

Mock endpoint - Should reset StreamCache when evaluating expecations

[CAMEL-12007](https://issues.apache.org/jira/browse/CAMEL-12007)

camel-catalog-maven - Add stop method to cleanup connections

### Task (1)

[CAMEL-12203](https://issues.apache.org/jira/browse/CAMEL-12203)

camel-fop - Upgrade to make it work again

### Test (1)

[CAMEL-12129](https://issues.apache.org/jira/browse/CAMEL-12129)

Broken integration test RabbitMQSupendResumeIntTest

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).