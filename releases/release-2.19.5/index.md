# Apache camel 2.19.5 Release

## New and Noteworthy

This release is a minor update of the 2.19.x branch.

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
      <version>2.19.5</version>
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
      <version>2.19.5</version>
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
| [apache-camel-2.19.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.5/apache-camel-2.19.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.5/apache-camel-2.19.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.5/apache-camel-2.19.5-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-12359](https://issues.apache.org/jira/browse/CAMEL-12359)

withAdvice() + weaveById() failing for global onException() route definitions

[CAMEL-12348](https://issues.apache.org/jira/browse/CAMEL-12348)

camel-core - Potential NPE in ExchangeHelper.isStreamCaching

[CAMEL-12342](https://issues.apache.org/jira/browse/CAMEL-12342)

Camel-weather: freegeoip.io has been moved to freegeoip.net

[CAMEL-12335](https://issues.apache.org/jira/browse/CAMEL-12335)

camel-sjms - Potential NPE in consumer

[CAMEL-12292](https://issues.apache.org/jira/browse/CAMEL-12292)

SnsProducer/SqsProducer setting MessageAttributes with empty values which causes errors

[CAMEL-12291](https://issues.apache.org/jira/browse/CAMEL-12291)

Blueprint error: "name is already instanciated as null and cannot be removed"

[CAMEL-12289](https://issues.apache.org/jira/browse/CAMEL-12289)

URISyntaxException in AbstractSpanDecorator

[CAMEL-12284](https://issues.apache.org/jira/browse/CAMEL-12284)

camel-beanio - Set encoding option does not work

[CAMEL-12256](https://issues.apache.org/jira/browse/CAMEL-12256)

AWS S3 Consumer does not return custom headers in S3 Headers

[CAMEL-12228](https://issues.apache.org/jira/browse/CAMEL-12228)

Print command fails in case of multiple copies

[CAMEL-12222](https://issues.apache.org/jira/browse/CAMEL-12222)

ResrSwaggerServlet removes last part of context root

[CAMEL-12196](https://issues.apache.org/jira/browse/CAMEL-12196)

Mock endpoint - message().body().matches().simple - Does not work

[CAMEL-12193](https://issues.apache.org/jira/browse/CAMEL-12193)

ThrowException DSL should support no-arg constructors

[CAMEL-12181](https://issues.apache.org/jira/browse/CAMEL-12181)

XML Signature: '#' missing in ObjectReference attribute of XADES element DataObjectFormat

[CAMEL-12149](https://issues.apache.org/jira/browse/CAMEL-12149)

Failed to invoke camel cxfrs client due to Content-Type header couldn't be retrieved and passed

[CAMEL-12131](https://issues.apache.org/jira/browse/CAMEL-12131)

CacheProducer should not put services in Camel context, that are not singletons and are not ServicePoolAware

[CAMEL-12098](https://issues.apache.org/jira/browse/CAMEL-12098)

URISyntaxException in OpenTracingTracer for endpoints with path parameters

[CAMEL-12094](https://issues.apache.org/jira/browse/CAMEL-12094)

fileExist=Move and tempFileName does not work together.

[CAMEL-12075](https://issues.apache.org/jira/browse/CAMEL-12075)

Piling up of threads in iterating splitter in pararllel processing

[CAMEL-12069](https://issues.apache.org/jira/browse/CAMEL-12069)

ActiveMQ/JMS component: transferExchange option does not transfer exchange properties anymore

[CAMEL-12031](https://issues.apache.org/jira/browse/CAMEL-12031)

KafkaConsumer stops consuming messages when exception occurs during offset commit

[CAMEL-12016](https://issues.apache.org/jira/browse/CAMEL-12016)

Invalid Pool Exhausted error on camel-netty4

[CAMEL-12009](https://issues.apache.org/jira/browse/CAMEL-12009)

Bindy - Missing Headers from OneToMany Field

[CAMEL-11996](https://issues.apache.org/jira/browse/CAMEL-11996)

RabbitConsumer could hang when RabbitMQ connection is lost and autoAck=false.

[CAMEL-11986](https://issues.apache.org/jira/browse/CAMEL-11986)

HTTP4 Producer for TLS schemes transforms endpoint URI to \`http4s\`

[CAMEL-11983](https://issues.apache.org/jira/browse/CAMEL-11983)

XsltAggregationStrategy thread safety during initialization

[CAMEL-11980](https://issues.apache.org/jira/browse/CAMEL-11980)

PushTopic client doesn't clear refresh token after a long disconnected period

[CAMEL-11628](https://issues.apache.org/jira/browse/CAMEL-11628)

MQTT Connection loop

[CAMEL-10165](https://issues.apache.org/jira/browse/CAMEL-10165)

DefaultCxfMessageMapper.getBasePath creates a incorrect http path

### Improvement (12)

[CAMEL-12358](https://issues.apache.org/jira/browse/CAMEL-12358)

Camel-SMPP: Use timeout when creating socket connection

[CAMEL-12352](https://issues.apache.org/jira/browse/CAMEL-12352)

simple - Lookup env var should be case-insensitive

[CAMEL-12305](https://issues.apache.org/jira/browse/CAMEL-12305)

IntrospectionSupport - Reduce DEBUG logging level

[CAMEL-12293](https://issues.apache.org/jira/browse/CAMEL-12293)

Avoid KeyAlreadyExistsException in ManagedTypeConverterRegistry.listTypeConverters()

[CAMEL-12251](https://issues.apache.org/jira/browse/CAMEL-12251)

Do not hide (so much) blueprint.container.ComponentDefinitionException

[CAMEL-12154](https://issues.apache.org/jira/browse/CAMEL-12154)

Camel does not set Saxon parameters in a XQuery 3.0 compatible way

[CAMEL-12090](https://issues.apache.org/jira/browse/CAMEL-12090)

camel-kafka - Better error if brokers not configured

[CAMEL-12029](https://issues.apache.org/jira/browse/CAMEL-12029)

CoAP component should handle method not allowed

[CAMEL-12010](https://issues.apache.org/jira/browse/CAMEL-12010)

Mock endpoint - Should reset StreamCache when evaluating expecations

[CAMEL-11997](https://issues.apache.org/jira/browse/CAMEL-11997)

camel-archetype-component - Should generate DefaultComponent

[CAMEL-11984](https://issues.apache.org/jira/browse/CAMEL-11984)

AggregationStrategy - Let EIPs support lifecycle of custom aggregation strategy to allow custom start/stop logic

[CAMEL-11932](https://issues.apache.org/jira/browse/CAMEL-11932)

For fixed length records crlf field is not honored during un-marshaling

### Task (1)

[CAMEL-12203](https://issues.apache.org/jira/browse/CAMEL-12203)

camel-fop - Upgrade to make it work again

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).