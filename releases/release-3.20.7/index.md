# Apache camel 3.20.7 Release

## New and Noteworthy

This release is the new Camel 3.20.7 LTS patch release.

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
      <version>3.20.7</version>
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
      <version>3.20.7</version>
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
| [apache-camel-3.20.7-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.7/apache-camel-3.20.7-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.7/apache-camel-3.20.7-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.7/apache-camel-3.20.7-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.7` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.7

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (30)

[CAMEL-19870](https://issues.apache.org/jira/browse/CAMEL-19870)

Camel AS2: Should accept MDN field name Disposition as case insensitive

[CAMEL-19814](https://issues.apache.org/jira/browse/CAMEL-19814)

camel-rest - Should filter out query parameters that are for the producer endpoint

[CAMEL-19780](https://issues.apache.org/jira/browse/CAMEL-19780)

Camel JBang does not support relative paths

[CAMEL-19758](https://issues.apache.org/jira/browse/CAMEL-19758)

netty-http in proxy mode generates IllegalReferenceCountException for every success request.

[CAMEL-19738](https://issues.apache.org/jira/browse/CAMEL-19738)

camel-core - Loop EIP can have wrong pending inflight in case of early loop exit due to exception

[CAMEL-19731](https://issues.apache.org/jira/browse/CAMEL-19731)

Camel-AS2: exception on empty response

[CAMEL-19719](https://issues.apache.org/jira/browse/CAMEL-19719)

camel-rest - Infinite loop when maximumRedeliveries > 0

[CAMEL-19701](https://issues.apache.org/jira/browse/CAMEL-19701)

camel-main - Filter out Kubernetes ENV injected service host/port

[CAMEL-19688](https://issues.apache.org/jira/browse/CAMEL-19688)

camel-core - exception in onCompletionProcessor should be suppressed, other than be lost

[CAMEL-19679](https://issues.apache.org/jira/browse/CAMEL-19679)

camel-flatpack - Strange concurrency with DataSet iterator

[CAMEL-19676](https://issues.apache.org/jira/browse/CAMEL-19676)

Do not log sensitive query parameters when route cannot be created

[CAMEL-19675](https://issues.apache.org/jira/browse/CAMEL-19675)

Attachment removed from Exchange after AggregationStrategy

[CAMEL-19671](https://issues.apache.org/jira/browse/CAMEL-19671)

camel-sql - Calling sql query without parameters in Oracle with jdbc driver 23.2.0.0

[CAMEL-19663](https://issues.apache.org/jira/browse/CAMEL-19663)

camel-core - ToD EIP multi-value property lost problem

[CAMEL-19650](https://issues.apache.org/jira/browse/CAMEL-19650)

Camel Kafka doesn't honor 'workerPool' configuration

[CAMEL-19646](https://issues.apache.org/jira/browse/CAMEL-19646)

camel-health reports UP when route controller is used and routes fail

[CAMEL-19607](https://issues.apache.org/jira/browse/CAMEL-19607)

camel-core - Checking redelivery reference while error handler creation

[CAMEL-19603](https://issues.apache.org/jira/browse/CAMEL-19603)

Spring Boot and Quarkus runtimes: @PeriodicTask annotated task are not running even if scheduled

[CAMEL-19575](https://issues.apache.org/jira/browse/CAMEL-19575)

camel-rabbitmq - RabbitMQConsumer keeps on consuming even when route shutdown is triggered.

[CAMEL-19562](https://issues.apache.org/jira/browse/CAMEL-19562)

aws sqs visibility extender is running forever

[CAMEL-19509](https://issues.apache.org/jira/browse/CAMEL-19509)

java.lang.NullPointerException: Cannot invoke "org.apache.camel.model.FromDefinition.getLabel()" because "this.input" is null

[CAMEL-19498](https://issues.apache.org/jira/browse/CAMEL-19498)

camel-core / camel-ftp - memory leak in MultiplePool when using pollEnrich EIP

[CAMEL-19491](https://issues.apache.org/jira/browse/CAMEL-19491)

Failing healthcheck on aws2-\* polling consumers causes readiness check to be stuck

[CAMEL-19487](https://issues.apache.org/jira/browse/CAMEL-19487)

camel-core / camel-bean - Dynamic router instances pass messages to wrong endpoints with @DynamicRouter annotation

[CAMEL-19486](https://issues.apache.org/jira/browse/CAMEL-19486)

The $repos placeholder used by Camel JBang is not resolved

[CAMEL-19476](https://issues.apache.org/jira/browse/CAMEL-19476)

rest-dsl - ClientRequestValidation accepted content-type may not validate correctly

[CAMEL-19457](https://issues.apache.org/jira/browse/CAMEL-19457)

camel-dynamic-router - InflightRepository size can be negative

[CAMEL-19373](https://issues.apache.org/jira/browse/CAMEL-19373)

spring-rabbitmq - Component does not Respect replyTimeout for InOut Exchanges

[CAMEL-19285](https://issues.apache.org/jira/browse/CAMEL-19285)

Kafka consumer can flood brokers if TLS handshake fails and pollOnError is set to RECONNECT

[CAMEL-18234](https://issues.apache.org/jira/browse/CAMEL-18234)

Exception building aws2-sqs route when certificate validation is disabled and a proxy is configured

### Dependency upgrade (8)

[CAMEL-19901](https://issues.apache.org/jira/browse/CAMEL-19901)

camel-spring-boot - Upgrade to 2.7.16

[CAMEL-19882](https://issues.apache.org/jira/browse/CAMEL-19882)

camel-karaf - Upgrade to 4.4.4

[CAMEL-19799](https://issues.apache.org/jira/browse/CAMEL-19799)

Camel-Spring-Boot: Upgrade to SB 2.7.15 on Camel Spring Boot 3.x

[CAMEL-19695](https://issues.apache.org/jira/browse/CAMEL-19695)

camel-google-bigquery - Upgrade org.json to resolve CVE-2022-45688

[CAMEL-19480](https://issues.apache.org/jira/browse/CAMEL-19480)

camel-netty - Upgrade to 4.1.94

[CAMEL-19473](https://issues.apache.org/jira/browse/CAMEL-19473)

camel-spring-boot - Upgrade to 2.7.13

[CAMEL-19458](https://issues.apache.org/jira/browse/CAMEL-19458)

Bouncycastle 1.73 to 1.74

[CAMEL-19323](https://issues.apache.org/jira/browse/CAMEL-19323)

Camel Karaf 3.20.X Saxon HE 11.5 Dependency Upgrade

### Improvement (13)

[CAMEL-19852](https://issues.apache.org/jira/browse/CAMEL-19852)

Camel-platform-http-vertx: Always use normalized path from context

[CAMEL-19760](https://issues.apache.org/jira/browse/CAMEL-19760)

netty-http:prevent the usage of proxy protocol in producer endpoint

[CAMEL-19752](https://issues.apache.org/jira/browse/CAMEL-19752)

Usage of "doc" prefix in some elasticsearch operations are regression to camel-elasticsearch-rest

[CAMEL-19736](https://issues.apache.org/jira/browse/CAMEL-19736)

Environment variables with the name 'secret' aren't masked in logs

[CAMEL-19691](https://issues.apache.org/jira/browse/CAMEL-19691)

camel-kafka - Allow sslKeystorePassword to be blank

[CAMEL-19677](https://issues.apache.org/jira/browse/CAMEL-19677)

camel-mllp - support more MLLP charsets

[CAMEL-19662](https://issues.apache.org/jira/browse/CAMEL-19662)

camel-bindy - Add option to @CsvRecord for trimeLine true or false

[CAMEL-19660](https://issues.apache.org/jira/browse/CAMEL-19660)

camel-mapstruct: Improve support for Mappers defined as abstract classes

[CAMEL-19627](https://issues.apache.org/jira/browse/CAMEL-19627)

paho-mqtt5: Allow password to be optional if username is provided

[CAMEL-19615](https://issues.apache.org/jira/browse/CAMEL-19615)

camel-ftp: chmodDirectory option try for each junk to change the directory permission and fails

[CAMEL-19587](https://issues.apache.org/jira/browse/CAMEL-19587)

camel-jira: optional header field IssueAssignee doesn't work

[CAMEL-19477](https://issues.apache.org/jira/browse/CAMEL-19477)

MeterRegistry collects authorization data

[CAMEL-19024](https://issues.apache.org/jira/browse/CAMEL-19024)

Camel Karaf Features missing camel-cxf-spring-\*

### Task (5)

[CAMEL-19871](https://issues.apache.org/jira/browse/CAMEL-19871)

camel-jooq - Set the proper scope to all test dependencies

[CAMEL-19840](https://issues.apache.org/jira/browse/CAMEL-19840)

camel-core-api - Add a warning when the key store file cannot be found

[CAMEL-19751](https://issues.apache.org/jira/browse/CAMEL-19751)

camel-xchange: tests keep hitting the binance API

[CAMEL-19489](https://issues.apache.org/jira/browse/CAMEL-19489)

camel-minio - Minor issues in documentation

[CAMEL-19425](https://issues.apache.org/jira/browse/CAMEL-19425)

camel-core: DynamicRouterConcurrentPOJOTest is flaky

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).