# Apache camel 2.21.2 Release

## New and Noteworthy

This release is a minor update of the 2.21.x branch.

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
      <version>2.21.2</version>
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
      <version>2.21.2</version>
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
| [apache-camel-2.21.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.21.2/apache-camel-2.21.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.21.2/apache-camel-2.21.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.21.2/apache-camel-2.21.2-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.21.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.21.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (36)

[CAMEL-12659](https://issues.apache.org/jira/browse/CAMEL-12659)

MllpTcpServerConsumer logging failure to set HL7 headers even when setting HL7 headers is disabled

[CAMEL-12647](https://issues.apache.org/jira/browse/CAMEL-12647)

Problem in setting region for camel AWS-SQS endpoint

[CAMEL-12637](https://issues.apache.org/jira/browse/CAMEL-12637)

XmlConverter can't transform StAXSource when external xalan lib available

[CAMEL-12630](https://issues.apache.org/jira/browse/CAMEL-12630)

Better attachment handling in camel-mail component

[CAMEL-12624](https://issues.apache.org/jira/browse/CAMEL-12624)

ActiveMQ Artemis AMQP integration issue with topic prefix hardcode

[CAMEL-12621](https://issues.apache.org/jira/browse/CAMEL-12621)

Rest DSL with Jetty9|netty4-http components returns 404 instead of 405, when http method is not supported

[CAMEL-12613](https://issues.apache.org/jira/browse/CAMEL-12613)

Camel file endpoint loses modification date and length information when preMove is used

[CAMEL-12607](https://issues.apache.org/jira/browse/CAMEL-12607)

When using Tokenizer skipFirst - java.util.NoSuchElementException if only one element

[CAMEL-12606](https://issues.apache.org/jira/browse/CAMEL-12606)

regression in camel test blueprint behaviour

[CAMEL-12603](https://issues.apache.org/jira/browse/CAMEL-12603)

Thread stuck in re-delivery loop after interrupting it

[CAMEL-12602](https://issues.apache.org/jira/browse/CAMEL-12602)

Camel Wordpress don't set basic authentication even if user and password are provided

[CAMEL-12601](https://issues.apache.org/jira/browse/CAMEL-12601)

camel-bindy: DefaultFactoryRegistry.unregister throws ConcurrentModificationException

[CAMEL-12594](https://issues.apache.org/jira/browse/CAMEL-12594)

Rest Producer - Query Parameters : Wrong query parameter name is used when header substitution is performed

[CAMEL-12589](https://issues.apache.org/jira/browse/CAMEL-12589)

Surviving Header AGGREGATION\_COMPLETE\_ALL\_GROUPS\_INCLUSIVE affects following aggregations

[CAMEL-12573](https://issues.apache.org/jira/browse/CAMEL-12573)

ClassCastException thrown KafkaSpanDecorator

[CAMEL-12570](https://issues.apache.org/jira/browse/CAMEL-12570)

Support fixed property placeholders from Aries blueprint

[CAMEL-12562](https://issues.apache.org/jira/browse/CAMEL-12562)

camel-dns: starter ignores serviceCall EIP configuration

[CAMEL-12561](https://issues.apache.org/jira/browse/CAMEL-12561)

camel-kubernetes: serviceCall EIP throws NullPointerException

[CAMEL-12560](https://issues.apache.org/jira/browse/CAMEL-12560)

camel-kubernetes: serviceCall EIP configuration is not read from application.properties

[CAMEL-12558](https://issues.apache.org/jira/browse/CAMEL-12558)

camel-catalog - Transacted and Policy should not have outputs

[CAMEL-12550](https://issues.apache.org/jira/browse/CAMEL-12550)

Camel-Twilio: Karaf feature is not working

[CAMEL-12548](https://issues.apache.org/jira/browse/CAMEL-12548)

NullPointerException in camel-cmis when using wrong credentials

[CAMEL-12541](https://issues.apache.org/jira/browse/CAMEL-12541)

camel-cxfrs - rsClient does not work programmatically, only with XML

[CAMEL-12540](https://issues.apache.org/jira/browse/CAMEL-12540)

We should avoid the address setting of CxfRsEndpointConfigurer

[CAMEL-12536](https://issues.apache.org/jira/browse/CAMEL-12536)

camel-google-mail: adding the camel component to a spring boot project leads to java.lang.NoSuchMethodError: javax.servlet.ServletContext.getClassLoader()Ljava/lang/ClassLoader;

[CAMEL-12535](https://issues.apache.org/jira/browse/CAMEL-12535)

Fix syntax for wordpress component

[CAMEL-12532](https://issues.apache.org/jira/browse/CAMEL-12532)

Content Based Router in Java DSL may not resolve property placeholders in when predicates

[CAMEL-12511](https://issues.apache.org/jira/browse/CAMEL-12511)

camel-consul - NPE on ConsulEventConsumer start

[CAMEL-12506](https://issues.apache.org/jira/browse/CAMEL-12506)

SqsProducer doesn't support Boolean attributes

[CAMEL-12491](https://issues.apache.org/jira/browse/CAMEL-12491)

route-coverage : report summary problem

[CAMEL-12490](https://issues.apache.org/jira/browse/CAMEL-12490)

Camel-jms: ClassNotFoundException: org.springframework.messaging.handler.annotation.support.MessageHandlerMethodFactory in Spring-Boot

[CAMEL-12487](https://issues.apache.org/jira/browse/CAMEL-12487)

S3Producer must close the streams it opens

[CAMEL-12483](https://issues.apache.org/jira/browse/CAMEL-12483)

route-coverage : endChoice() problem

[CAMEL-12480](https://issues.apache.org/jira/browse/CAMEL-12480)

HttpOperationFailedException exposes password when using basic auth with user:password@host notation

[CAMEL-12475](https://issues.apache.org/jira/browse/CAMEL-12475)

Undertow consumer with http4 producer results in Undertow throwing NullPointerException

[CAMEL-11595](https://issues.apache.org/jira/browse/CAMEL-11595)

camel-univocity-parsers - A number of stream closed exception in tests

### Improvement (6)

[CAMEL-12639](https://issues.apache.org/jira/browse/CAMEL-12639)

tooling - Provide line numbers for CamelEndpointDetails for java dsl

[CAMEL-12588](https://issues.apache.org/jira/browse/CAMEL-12588)

AggregateProcessor does not stop AggregateTimeoutChecker threads on stop call

[CAMEL-12514](https://issues.apache.org/jira/browse/CAMEL-12514)

Extract undertow component name to allow extensibility

[CAMEL-12507](https://issues.apache.org/jira/browse/CAMEL-12507)

SqsProducer support for Number custom data types

[CAMEL-12493](https://issues.apache.org/jira/browse/CAMEL-12493)

Make additional HL7 Type Converters optional

[CAMEL-12404](https://issues.apache.org/jira/browse/CAMEL-12404)

Upgrade jackson-databind minor version in Camel 2.20.x and 2.21.x

### New Feature (1)

[CAMEL-12360](https://issues.apache.org/jira/browse/CAMEL-12360)

Add logRetryAttemptedInterval to RedeliveryPolicy

### Task (2)

[CAMEL-12632](https://issues.apache.org/jira/browse/CAMEL-12632)

Pass CXF service class to EndpointInfo

[CAMEL-12579](https://issues.apache.org/jira/browse/CAMEL-12579)

Disable Google Analytics phone home

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).