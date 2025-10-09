# Apache camel 3.4.3 Release

## New and Noteworthy

This release is the new Camel 3.4.3 patch release.

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
      <version>3.4.3</version>
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
      <version>3.4.3</version>
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
| [apache-camel-3.4.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.3/apache-camel-3.4.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.3/apache-camel-3.4.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.3/apache-camel-3.4.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (25)

[CAMEL-15387](https://issues.apache.org/jira/browse/CAMEL-15387)

Can't set Salesforce packages via application properties.

[CAMEL-15378](https://issues.apache.org/jira/browse/CAMEL-15378)

File gets locked When using camel-flatpack delimited parser

[CAMEL-15370](https://issues.apache.org/jira/browse/CAMEL-15370)

CxfRsProducer: All but last value of query parameter with multiple values are lost

[CAMEL-15369](https://issues.apache.org/jira/browse/CAMEL-15369)

camel-aws2-kinesis: IndexOutOfBoundsException when polling

[CAMEL-15358](https://issues.apache.org/jira/browse/CAMEL-15358)

camel-aws-kinesis: IndexOutOfBoundsException when polling

[CAMEL-15355](https://issues.apache.org/jira/browse/CAMEL-15355)

unacceptable\_type,longstr error if we set 'arg.queue.x-single-active-consumer=true in rabbitmq endpoint url

[CAMEL-15350](https://issues.apache.org/jira/browse/CAMEL-15350)

SJMS Batch Consumer error recovery

[CAMEL-15349](https://issues.apache.org/jira/browse/CAMEL-15349)

camel-xmpp can't consume direct message chats

[CAMEL-15348](https://issues.apache.org/jira/browse/CAMEL-15348)

cxfEndpoint blueprint namespace handler - problem with QName vs String

[CAMEL-15344](https://issues.apache.org/jira/browse/CAMEL-15344)

ShutdownStrategy - Inflight count is reporting wrong with 2x the actual number

[CAMEL-15343](https://issues.apache.org/jira/browse/CAMEL-15343)

camel-main - Graceful shutdown from ctrl + c SIGTERM is not working correctly

[CAMEL-15338](https://issues.apache.org/jira/browse/CAMEL-15338)

Salesforce - Wrong Channel Name for Standard Platform Events

[CAMEL-15336](https://issues.apache.org/jira/browse/CAMEL-15336)

Wrong information for supported platforms in FAQ of website

[CAMEL-15326](https://issues.apache.org/jira/browse/CAMEL-15326)

camel-slack: incorrect handling of error responses

[CAMEL-15316](https://issues.apache.org/jira/browse/CAMEL-15316)

Camel Zipkin does not set correct span kind

[CAMEL-15315](https://issues.apache.org/jira/browse/CAMEL-15315)

Camel-Pulsar: Error when verifying/creating namespace

[CAMEL-15311](https://issues.apache.org/jira/browse/CAMEL-15311)

DefaultTracer traceBeforeRoute not calling dumpTrace

[CAMEL-15307](https://issues.apache.org/jira/browse/CAMEL-15307)

camel-spring - Graceful shutdown is not working anymore

[CAMEL-15298](https://issues.apache.org/jira/browse/CAMEL-15298)

Camel-Spring-Boot: No CamelContext defined yet so cannot inject into bean: org.apache.camel.impl.health.DefaultHealthCheckRegistry

[CAMEL-15297](https://issues.apache.org/jira/browse/CAMEL-15297)

camel-pgevent - Issue with URI verification

[CAMEL-15282](https://issues.apache.org/jira/browse/CAMEL-15282)

Wrong validation error reported for uri with netty component using env placeholder

[CAMEL-15230](https://issues.apache.org/jira/browse/CAMEL-15230)

RabbitMqSpanDecorator - Invalid Parent Span Id when EXCHANGE\_NAME header not set

[CAMEL-15012](https://issues.apache.org/jira/browse/CAMEL-15012)

Camel-Http: Endpoint parameters proxyHost and proxyPort are ignored

[CAMEL-14533](https://issues.apache.org/jira/browse/CAMEL-14533)

camel-ftp: fileExist=Append and tempPrefix options do not work together

[CAMEL-12971](https://issues.apache.org/jira/browse/CAMEL-12971)

SJMS Component javax.jms.JMSException: Unmatched acknowledge: MessageAck when transactionBatchTimeout expired

### Improvement (6)

[CAMEL-15381](https://issues.apache.org/jira/browse/CAMEL-15381)

Avoid use of reflection in CronComponent

[CAMEL-15357](https://issues.apache.org/jira/browse/CAMEL-15357)

Add example for Karaf to demonstrate how REST endpoint using servlet secured by Karaf JAAS service

[CAMEL-15346](https://issues.apache.org/jira/browse/CAMEL-15346)

Let xml-io pass the namespace info to NamespaceAware elements

[CAMEL-15328](https://issues.apache.org/jira/browse/CAMEL-15328)

Honor Optional http headers as method parameters to be null in camel-cxfrs producer

[CAMEL-15303](https://issues.apache.org/jira/browse/CAMEL-15303)

Reduce log level for autodiscovered ObjectMapper

[CAMEL-15244](https://issues.apache.org/jira/browse/CAMEL-15244)

AggregationStrategy - default timeout method should be empty

### Task (2)

[CAMEL-15388](https://issues.apache.org/jira/browse/CAMEL-15388)

Upgrade spring boot to 2.3.2 on 3.4.x LTS

[CAMEL-15314](https://issues.apache.org/jira/browse/CAMEL-15314)

camel-endpointdsl - StaticEndpointBuilders - may loose public

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).