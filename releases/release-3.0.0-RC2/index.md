# Apache camel 3.0.0-RC2 Release

## New and Noteworthy

This release the second release candidate towards Camel 3.0.0 release.

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
      <version>3.0.0-RC2</version>
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
      <version>3.0.0-RC2</version>
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
| [apache-camel-3.0.0-RC2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC2/apache-camel-3.0.0-RC2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC2/apache-camel-3.0.0-RC2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC2/apache-camel-3.0.0-RC2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.0.0-RC2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.0.0-RC2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (32)

[CAMEL-14002](https://issues.apache.org/jira/browse/CAMEL-14002)

camel-aws-sqs: amazonAWSHost is not honored when listing the queues

[CAMEL-13997](https://issues.apache.org/jira/browse/CAMEL-13997)

ProxyProtocolTest not releasing acquired ByteBuf

[CAMEL-13994](https://issues.apache.org/jira/browse/CAMEL-13994)

listPods operation of kubernetes component dont support namespace option

[CAMEL-13991](https://issues.apache.org/jira/browse/CAMEL-13991)

camel-main - Configuring component options with #class dont work

[CAMEL-13987](https://issues.apache.org/jira/browse/CAMEL-13987)

Expired certificates and outdated keys in test keystores

[CAMEL-13985](https://issues.apache.org/jira/browse/CAMEL-13985)

Maven plugin :prepare-readme is unable to populate documentation file with options due to case sensitivity

[CAMEL-13981](https://issues.apache.org/jira/browse/CAMEL-13981)

Daily Karaf builds failing

[CAMEL-13976](https://issues.apache.org/jira/browse/CAMEL-13976)

Allow AS2 Component to reply disposition type failed in the MDN

[CAMEL-13969](https://issues.apache.org/jira/browse/CAMEL-13969)

Invalid SpringBootAutoConfiguration for a component when you have a configuration with long class name

[CAMEL-13968](https://issues.apache.org/jira/browse/CAMEL-13968)

AS2 component treats http headers case sensitive. According to RFC this should be case insensitive

[CAMEL-13966](https://issues.apache.org/jira/browse/CAMEL-13966)

Unable to change body of the message in Netty-HTTP when proxying

[CAMEL-13962](https://issues.apache.org/jira/browse/CAMEL-13962)

OgnlHelper.splitOgnl not able to handle Regex properly

[CAMEL-13961](https://issues.apache.org/jira/browse/CAMEL-13961)

Reconsider default for xslt:allowStAX

[CAMEL-13960](https://issues.apache.org/jira/browse/CAMEL-13960)

Non-retained buffer when using Netty-HTTP as proxy

[CAMEL-13958](https://issues.apache.org/jira/browse/CAMEL-13958)

XPathBuilder threadSafe mode should also be enabled when the NodeList contains only 1 item

[CAMEL-13957](https://issues.apache.org/jira/browse/CAMEL-13957)

Dead link from Writing components documentation page

[CAMEL-13956](https://issues.apache.org/jira/browse/CAMEL-13956)

FileDataSet does not support a single file larger than 1024 bytes

[CAMEL-13954](https://issues.apache.org/jira/browse/CAMEL-13954)

Generated property configurator is using wrong method on endpoint (camel-file-watch component)

[CAMEL-13942](https://issues.apache.org/jira/browse/CAMEL-13942)

camel-undertow - UnitOfWork should be done after send back response

[CAMEL-13935](https://issues.apache.org/jira/browse/CAMEL-13935)

camel-properties: Properties with types different from string are not taken into account

[CAMEL-13931](https://issues.apache.org/jira/browse/CAMEL-13931)

camel-file - tempFileName directory is not auto-created if it is relative before the endpoint path

[CAMEL-13924](https://issues.apache.org/jira/browse/CAMEL-13924)

Camel-DirectVM: failIfNoConsumers option not taken into account when block is enabled

[CAMEL-13921](https://issues.apache.org/jira/browse/CAMEL-13921)

JMS Producer not useable under camel-blueprint

[CAMEL-13919](https://issues.apache.org/jira/browse/CAMEL-13919)

"camel-package:update-readme" throws ArrayIndexOutOfBoundsException when there is an empty "adoc" file

[CAMEL-13886](https://issues.apache.org/jira/browse/CAMEL-13886)

camel-servlet + camel-http4 with null body causes "Stream closed" IOException

[CAMEL-13878](https://issues.apache.org/jira/browse/CAMEL-13878)

Message is forwarded to the wrong Kafka Topic

[CAMEL-13504](https://issues.apache.org/jira/browse/CAMEL-13504)

Strange behaviour of SimpleLRUCache with ProducerTemplate

[CAMEL-13475](https://issues.apache.org/jira/browse/CAMEL-13475)

Camel with Olingo4 not shutting down

[CAMEL-13254](https://issues.apache.org/jira/browse/CAMEL-13254)

camel-file - Some Component Parameters have a different behaviour when used with Poll Enrich

[CAMEL-13245](https://issues.apache.org/jira/browse/CAMEL-13245)

RabbitMq producer not always honoring EXCHANGE\_OVERRIDE\_NAME header

[CAMEL-13121](https://issues.apache.org/jira/browse/CAMEL-13121)

Route irc->irc cycles the message because of "irc.target" header

[CAMEL-12471](https://issues.apache.org/jira/browse/CAMEL-12471)

Dots in RabbitMQ-component headers do not work

### Improvement (34)

[CAMEL-14021](https://issues.apache.org/jira/browse/CAMEL-14021)

HDFS Polling consumer returns incorrect count of processed messages

[CAMEL-14016](https://issues.apache.org/jira/browse/CAMEL-14016)

camel-zipkin - Allow clients to send custom tags to Zipkin server

[CAMEL-14011](https://issues.apache.org/jira/browse/CAMEL-14011)

Refactor camel-hdfs component to reduce issues reported by sonar

[CAMEL-14001](https://issues.apache.org/jira/browse/CAMEL-14001)

Camel-Pulsar: Add MessageRoutingMode and MessageRouter option to producer

[CAMEL-14000](https://issues.apache.org/jira/browse/CAMEL-14000)

ServicePool can cause memory leak

[CAMEL-13990](https://issues.apache.org/jira/browse/CAMEL-13990)

Add UriEndpoint annotation checks for the schema name in the apt compiler so the compilation can fail in case there are invalid options set

[CAMEL-13986](https://issues.apache.org/jira/browse/CAMEL-13986)

Camel-Kubernetes: Add deleteNode operation

[CAMEL-13983](https://issues.apache.org/jira/browse/CAMEL-13983)

Provide CreateNode feature in Kubernetes Component

[CAMEL-13982](https://issues.apache.org/jira/browse/CAMEL-13982)

Handle standard Gauge metric in MicroProfile metrics component

[CAMEL-13978](https://issues.apache.org/jira/browse/CAMEL-13978)

Create ConfigMap Watch feature in Kubernetes Component

[CAMEL-13977](https://issues.apache.org/jira/browse/CAMEL-13977)

Expose additional Camel metrics from MicroProfile metrics component

[CAMEL-13974](https://issues.apache.org/jira/browse/CAMEL-13974)

Many examples are missing camel component dependencies

[CAMEL-13973](https://issues.apache.org/jira/browse/CAMEL-13973)

Camel-AWS Translate: Detect the source language automatically

[CAMEL-13972](https://issues.apache.org/jira/browse/CAMEL-13972)

Camel-AWS Translate: Add a languages enum

[CAMEL-13967](https://issues.apache.org/jira/browse/CAMEL-13967)

Micrometer example metrics endpoint does not work

[CAMEL-13963](https://issues.apache.org/jira/browse/CAMEL-13963)

Netty-HTTP in proxy mode should support POST method

[CAMEL-13951](https://issues.apache.org/jira/browse/CAMEL-13951)

JdbcAggregationRepository doesn't work with PostgreSQL

[CAMEL-13949](https://issues.apache.org/jira/browse/CAMEL-13949)

camel-core vs camel-core-engine

[CAMEL-13947](https://issues.apache.org/jira/browse/CAMEL-13947)

Create a configuration service instead of leveraging the properties component

[CAMEL-13938](https://issues.apache.org/jira/browse/CAMEL-13938)

core artifacts should not depend con camel-core but camel-core-engine

[CAMEL-13930](https://issues.apache.org/jira/browse/CAMEL-13930)

camel-http4 - Basic auth and redelivery issue with streaming message body

[CAMEL-13929](https://issues.apache.org/jira/browse/CAMEL-13929)

camel3 - ApiEndpoint should extend ScheduledPollEndpoint

[CAMEL-13925](https://issues.apache.org/jira/browse/CAMEL-13925)

camel-seda - SedaConsumer should extend DefaultConsumer

[CAMEL-13911](https://issues.apache.org/jira/browse/CAMEL-13911)

Fix the endpoint DSL when a component uses multiple schemes

[CAMEL-13901](https://issues.apache.org/jira/browse/CAMEL-13901)

camel-main-plugin - Dont run it automatic on compile

[CAMEL-13900](https://issues.apache.org/jira/browse/CAMEL-13900)

Remove redundant classes from JAXB indexes

[CAMEL-13895](https://issues.apache.org/jira/browse/CAMEL-13895)

camel3 - TypeConverter(loader = true) rename to generateLoader

[CAMEL-13887](https://issues.apache.org/jira/browse/CAMEL-13887)

camel-mongodb-gridfs - Mongo to MongoClient

[CAMEL-13885](https://issues.apache.org/jira/browse/CAMEL-13885)

Add categories to examples that dont have this

[CAMEL-13869](https://issues.apache.org/jira/browse/CAMEL-13869)

camel-undertow - Upgrade to 2.x

[CAMEL-13840](https://issues.apache.org/jira/browse/CAMEL-13840)

Upgrade to quickfix 2.x

[CAMEL-13821](https://issues.apache.org/jira/browse/CAMEL-13821)

Upgrade Corda Version in camel parent pom to 4.0

[CAMEL-13820](https://issues.apache.org/jira/browse/CAMEL-13820)

ResolveEndpointFailedException should mask sensitive information in uri

[CAMEL-11011](https://issues.apache.org/jira/browse/CAMEL-11011)

Make all Services Closeable

### New Feature (8)

[CAMEL-14007](https://issues.apache.org/jira/browse/CAMEL-14007)

Expose BoxFolder.canUpload to let user check if a file can be uploaded

[CAMEL-13998](https://issues.apache.org/jira/browse/CAMEL-13998)

Kerberos authentication for HDFS connections

[CAMEL-13988](https://issues.apache.org/jira/browse/CAMEL-13988)

Enable camel-protobuf to marshal from objects of type Map to Proto using the message descriptor

[CAMEL-13936](https://issues.apache.org/jira/browse/CAMEL-13936)

SNMP Component support ‘snmp walk’

[CAMEL-13851](https://issues.apache.org/jira/browse/CAMEL-13851)

camel-xj component contribution

[CAMEL-13435](https://issues.apache.org/jira/browse/CAMEL-13435)

Create an AWS-Translate component

[CAMEL-12543](https://issues.apache.org/jira/browse/CAMEL-12543)

create a camel-debezium component

[CAMEL-9260](https://issues.apache.org/jira/browse/CAMEL-9260)

Dataformat Apache Any23

### Sub-task (2)

[CAMEL-13965](https://issues.apache.org/jira/browse/CAMEL-13965)

Create a camel-test-spring-junit5 module

[CAMEL-13826](https://issues.apache.org/jira/browse/CAMEL-13826)

Create a camel-test-junit5 module

### Task (15)

[CAMEL-14018](https://issues.apache.org/jira/browse/CAMEL-14018)

karaf feature for camel-elasticsearch-rest issue

[CAMEL-14015](https://issues.apache.org/jira/browse/CAMEL-14015)

Camel-Zipkin: Going back to non-ASF artifacts

[CAMEL-13989](https://issues.apache.org/jira/browse/CAMEL-13989)

Enhance the javadoc for the UriEndpoint annotation

[CAMEL-13980](https://issues.apache.org/jira/browse/CAMEL-13980)

Remove watermark from maven plugin model files

[CAMEL-13971](https://issues.apache.org/jira/browse/CAMEL-13971)

Camel-AWS Translate: Create Karaf and Spring Boot integration tests

[CAMEL-13970](https://issues.apache.org/jira/browse/CAMEL-13970)

Camel AWS-Translate: Create a Karaf feature

[CAMEL-13964](https://issues.apache.org/jira/browse/CAMEL-13964)

Create camel-debezium examples

[CAMEL-13946](https://issues.apache.org/jira/browse/CAMEL-13946)

Upgrade to Maven 3.6.2

[CAMEL-13945](https://issues.apache.org/jira/browse/CAMEL-13945)

Camel-elasticsearch-rest: Remove info operation from producer

[CAMEL-13939](https://issues.apache.org/jira/browse/CAMEL-13939)

camel3 - Rename camel-management-impl to camel-management

[CAMEL-13918](https://issues.apache.org/jira/browse/CAMEL-13918)

camel3 - camel-http - Remove deprecate url rewrite

[CAMEL-13917](https://issues.apache.org/jira/browse/CAMEL-13917)

camel3 - Deprecate and remove consumer.xxx syntax for delay options

[CAMEL-13916](https://issues.apache.org/jira/browse/CAMEL-13916)

website - Add migration guide page

[CAMEL-13913](https://issues.apache.org/jira/browse/CAMEL-13913)

camel3 - components - Use BeanIntrospection instead of IntrospectionSupport

[CAMEL-13905](https://issues.apache.org/jira/browse/CAMEL-13905)

camel-any23 - ascii doc warning

### Test (2)

[CAMEL-13984](https://issues.apache.org/jira/browse/CAMEL-13984)

camel-jms - 2 tests fails on CI

[CAMEL-13943](https://issues.apache.org/jira/browse/CAMEL-13943)

Camel-kafka Test cases getting failed

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).