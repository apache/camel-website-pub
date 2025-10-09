# Apache camel 3.2.0 Release

## New and Noteworthy

This release is the new Camel 3.2.0 major release.

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
      <version>3.2.0</version>
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
      <version>3.2.0</version>
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
| [apache-camel-3.2.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.2.0/apache-camel-3.2.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.2.0/apache-camel-3.2.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.2.0/apache-camel-3.2.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.2.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.2.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (30)

[CAMEL-14825](https://issues.apache.org/jira/browse/CAMEL-14825)

Bugfix for Bindy-Component

[CAMEL-14789](https://issues.apache.org/jira/browse/CAMEL-14789)

camel-rabbitmq - Automatic recovery of temporary reply queue is not handled correctly

[CAMEL-14788](https://issues.apache.org/jira/browse/CAMEL-14788)

Unable to Start Jetty server in OSGi environment

[CAMEL-14782](https://issues.apache.org/jira/browse/CAMEL-14782)

Camel-website: build is broken again

[CAMEL-14780](https://issues.apache.org/jira/browse/CAMEL-14780)

camel-undertow: UndertowSecurityProvider SPI API misses a method to change HttpHandler

[CAMEL-14768](https://issues.apache.org/jira/browse/CAMEL-14768)

Camel-Website: .htaccess redirects

[CAMEL-14767](https://issues.apache.org/jira/browse/CAMEL-14767)

Camel-website: Build is broken

[CAMEL-14764](https://issues.apache.org/jira/browse/CAMEL-14764)

header menus missing from antora site

[CAMEL-14761](https://issues.apache.org/jira/browse/CAMEL-14761)

JPAMessageIdRepository Not Releasing Connections for contains() method

[CAMEL-14752](https://issues.apache.org/jira/browse/CAMEL-14752)

Unmarshal TAR w/ error handling in Camel 3.x

[CAMEL-14749](https://issues.apache.org/jira/browse/CAMEL-14749)

Camel-AWS2: Error configuring AWS2 endpoints behind proxy server

[CAMEL-14748](https://issues.apache.org/jira/browse/CAMEL-14748)

Unmarshal ZIP w/ error handling in Camel 3.x

[CAMEL-14746](https://issues.apache.org/jira/browse/CAMEL-14746)

camel-rest-swagger java.lang.IllegalArgumentException when Swagger specification don't have "scheme" object and get this specification by "file;" resource

[CAMEL-14740](https://issues.apache.org/jira/browse/CAMEL-14740)

spring-boot - Error binding property in servlet-starter

[CAMEL-14739](https://issues.apache.org/jira/browse/CAMEL-14739)

RouteContext missing for RedeliveryErrorHandler

[CAMEL-14733](https://issues.apache.org/jira/browse/CAMEL-14733)

Properties of class Map does not work with Spring Boot

[CAMEL-14724](https://issues.apache.org/jira/browse/CAMEL-14724)

camel-swagger-java Semantic error. Methods in rest service with id have the same operationId

[CAMEL-14722](https://issues.apache.org/jira/browse/CAMEL-14722)

Warning message spawned by the telegram component

[CAMEL-14708](https://issues.apache.org/jira/browse/CAMEL-14708)

Camel 3.0.0 Failed to start route because of Multiple consumers for the same endpoint is not allowed

[CAMEL-14691](https://issues.apache.org/jira/browse/CAMEL-14691)

NPE when using reference to parameter in openapi-rest-dsl-generator

[CAMEL-14659](https://issues.apache.org/jira/browse/CAMEL-14659)

camel-core - Thread stuck if exception is thrown in handle(Predicate) with onException

[CAMEL-14651](https://issues.apache.org/jira/browse/CAMEL-14651)

Property placeholder not resolved in Log EIP

[CAMEL-14649](https://issues.apache.org/jira/browse/CAMEL-14649)

Cannot parse catalog/components/kafka.json

[CAMEL-14645](https://issues.apache.org/jira/browse/CAMEL-14645)

Wrong rest mapping on camel-undertow

[CAMEL-14632](https://issues.apache.org/jira/browse/CAMEL-14632)

Optimization of DefaultExchangeFormatter leeds to crapy log output

[CAMEL-14629](https://issues.apache.org/jira/browse/CAMEL-14629)

Install of camel-jackson on Karaf 4.2.7 w/ Camel 3.1.0 causes an error (same worked with Karaf 4.2.7 w/ Camel 3.0.1)

[CAMEL-14624](https://issues.apache.org/jira/browse/CAMEL-14624)

RouteCoverage in Test throws Exception for TransactedDefinition

[CAMEL-14621](https://issues.apache.org/jira/browse/CAMEL-14621)

Camel-spring-boot-starters have unnecessary JAX-B and JAX-WS dependencies on Java 11

[CAMEL-14615](https://issues.apache.org/jira/browse/CAMEL-14615)

camel kafka starter for spring does not consider camel.component.kafka.brokers property

[CAMEL-14601](https://issues.apache.org/jira/browse/CAMEL-14601)

Camel Kafka feature cannot be install on HPUX and Solaris arch

### Improvement (67)

[CAMEL-14821](https://issues.apache.org/jira/browse/CAMEL-14821)

camel-spark-rest - Remove this component

[CAMEL-14819](https://issues.apache.org/jira/browse/CAMEL-14819)

rest-dsl - XML binding mode should have JAXB initialization done in camel-jaxb

[CAMEL-14815](https://issues.apache.org/jira/browse/CAMEL-14815)

ComponentModel.name not set by generate-endpoint-schema mojo

[CAMEL-14814](https://issues.apache.org/jira/browse/CAMEL-14814)

Introduce ArtifactModel as an abstraction over Component, Language, Dataformat and Other models

[CAMEL-14811](https://issues.apache.org/jira/browse/CAMEL-14811)

Remove JMX Connector configuration

[CAMEL-14798](https://issues.apache.org/jira/browse/CAMEL-14798)

Separate Avro dataformat out of camel-avro component

[CAMEL-14795](https://issues.apache.org/jira/browse/CAMEL-14795)

camel-mail: allow dynamic setting of token in order to be able to support OAUTH

[CAMEL-14794](https://issues.apache.org/jira/browse/CAMEL-14794)

camel-weather - Upgrade to http client 4.x

[CAMEL-14793](https://issues.apache.org/jira/browse/CAMEL-14793)

camel-kafka - Decrease default consumer request timeout to 30s

[CAMEL-14779](https://issues.apache.org/jira/browse/CAMEL-14779)

Move Main out of camel-spring due to osgi circular dependency issue

[CAMEL-14775](https://issues.apache.org/jira/browse/CAMEL-14775)

camel-cxf - Move OSGi blueprint out into camel-cxf-blueprint

[CAMEL-14770](https://issues.apache.org/jira/browse/CAMEL-14770)

Sort nav the same as index pages

[CAMEL-14766](https://issues.apache.org/jira/browse/CAMEL-14766)

Rearrange 3.0.x components component similar to latest

[CAMEL-14765](https://issues.apache.org/jira/browse/CAMEL-14765)

Rearrange 2.x components component similar to latest

[CAMEL-14762](https://issues.apache.org/jira/browse/CAMEL-14762)

camel-core - Configurer to include API for method name and type

[CAMEL-14760](https://issues.apache.org/jira/browse/CAMEL-14760)

camel-main - Generate configurer for its own options

[CAMEL-14747](https://issues.apache.org/jira/browse/CAMEL-14747)

Put all the EIP documentation in one place, and possibly version it.

[CAMEL-14742](https://issues.apache.org/jira/browse/CAMEL-14742)

Prevent JMX rebinding

[CAMEL-14734](https://issues.apache.org/jira/browse/CAMEL-14734)

camel-hbase - Upgrade to newer 2.x release

[CAMEL-14726](https://issues.apache.org/jira/browse/CAMEL-14726)

Upgrade MongoDB client to 4.0.0

[CAMEL-14723](https://issues.apache.org/jira/browse/CAMEL-14723)

Adding a restConfiguration() make all rest properties to be ignored

[CAMEL-14721](https://issues.apache.org/jira/browse/CAMEL-14721)

camel-kafka - Include key.subject.name.strategy and value.subject.name.strategy as possible configurations

[CAMEL-14720](https://issues.apache.org/jira/browse/CAMEL-14720)

camel-core - Move cluster from core-engine to camel-cluster

[CAMEL-14719](https://issues.apache.org/jira/browse/CAMEL-14719)

camel-core - Camel context started events should be emitted after its status is started

[CAMEL-14717](https://issues.apache.org/jira/browse/CAMEL-14717)

camel-core - Binding properties add support for optional keys

[CAMEL-14716](https://issues.apache.org/jira/browse/CAMEL-14716)

@BeanConfigInject add support for Map

[CAMEL-14715](https://issues.apache.org/jira/browse/CAMEL-14715)

Move karaf/osgi to separate git repository

[CAMEL-14711](https://issues.apache.org/jira/browse/CAMEL-14711)

Disable RabbitMQ Java serialization by default

[CAMEL-14699](https://issues.apache.org/jira/browse/CAMEL-14699)

Platform HTTP endpoints should support matchOnUriPrefix

[CAMEL-14698](https://issues.apache.org/jira/browse/CAMEL-14698)

Consider rearranging site source to Antora norms

[CAMEL-14697](https://issues.apache.org/jira/browse/CAMEL-14697)

openapi-rest-dsl-generator not considering path parameters

[CAMEL-14696](https://issues.apache.org/jira/browse/CAMEL-14696)

Document working on the website on Windows

[CAMEL-14692](https://issues.apache.org/jira/browse/CAMEL-14692)

camel-pulsar: Support Key\_Shared subscription mode

[CAMEL-14690](https://issues.apache.org/jira/browse/CAMEL-14690)

Camel-AWS2: Better logging when checking client instance in the registry

[CAMEL-14687](https://issues.apache.org/jira/browse/CAMEL-14687)

Cannot build camel behind firewall

[CAMEL-14685](https://issues.apache.org/jira/browse/CAMEL-14685)

Camel-RabbitMQ: Introduce an HeaderFilterStrategy to RabbitMQMessageConverter

[CAMEL-14679](https://issues.apache.org/jira/browse/CAMEL-14679)

Support DROP\_ROOT\_MODE in XStream JSON dataformat

[CAMEL-14671](https://issues.apache.org/jira/browse/CAMEL-14671)

Make PropertiesFunction part of the PropertiesComponent SPI

[CAMEL-14658](https://issues.apache.org/jira/browse/CAMEL-14658)

Provide a simpler way to connect to a local s3 instance

[CAMEL-14648](https://issues.apache.org/jira/browse/CAMEL-14648)

camel-core - Optimize normalizeUri

[CAMEL-14646](https://issues.apache.org/jira/browse/CAMEL-14646)

\[camel-azure\] Add the possibility to set credentials as query parameters

[CAMEL-14644](https://issues.apache.org/jira/browse/CAMEL-14644)

camel-core - Optimize dynamic EIPs to only normalize uri once

[CAMEL-14642](https://issues.apache.org/jira/browse/CAMEL-14642)

camel-spring-boot - Using max duration and shutdown before should terminate scheduled thread quicker

[CAMEL-14641](https://issues.apache.org/jira/browse/CAMEL-14641)

camel-spring-boot - Using main controller should not double initialize from properties

[CAMEL-14639](https://issues.apache.org/jira/browse/CAMEL-14639)

DefaultHttpRegistry thread safety

[CAMEL-14635](https://issues.apache.org/jira/browse/CAMEL-14635)

camel-activemq - Rename BrokerURL to brokerUrl for spring boot auto configuration

[CAMEL-14625](https://issues.apache.org/jira/browse/CAMEL-14625)

camel-pulsar : Support asynchronous processing

[CAMEL-14620](https://issues.apache.org/jira/browse/CAMEL-14620)

camel-spring-boot - Use configurer classes for setting options

[CAMEL-14609](https://issues.apache.org/jira/browse/CAMEL-14609)

camel-core - Optimize URIScanner

[CAMEL-14608](https://issues.apache.org/jira/browse/CAMEL-14608)

Camel-Pulsar add the ability to add Dead Letter Policies to Consumers

[CAMEL-14607](https://issues.apache.org/jira/browse/CAMEL-14607)

Camel-Pulsar add Negative ack support

[CAMEL-14599](https://issues.apache.org/jira/browse/CAMEL-14599)

AdviceWithRouteBuilder - Inconherent test

[CAMEL-14595](https://issues.apache.org/jira/browse/CAMEL-14595)

camel-mail - Allow to use headers for additional mail properties

[CAMEL-14576](https://issues.apache.org/jira/browse/CAMEL-14576)

camel-hbase - Test using test containers

[CAMEL-14575](https://issues.apache.org/jira/browse/CAMEL-14575)

camel-core - TypeConverter from String to Long - drop time pattern

[CAMEL-14568](https://issues.apache.org/jira/browse/CAMEL-14568)

camel component configurations include nested configuration classes

[CAMEL-14544](https://issues.apache.org/jira/browse/CAMEL-14544)

Camel-Hazelcast: Upgrade to Hazelcast 4

[CAMEL-14514](https://issues.apache.org/jira/browse/CAMEL-14514)

Improving Google Pub/Sub performance

[CAMEL-14495](https://issues.apache.org/jira/browse/CAMEL-14495)

OPC UA Client samplingInterval parameter seems not take any effect

[CAMEL-14423](https://issues.apache.org/jira/browse/CAMEL-14423)

Migrate MongoDB component to mongodb-driver-sync dependency

[CAMEL-14407](https://issues.apache.org/jira/browse/CAMEL-14407)

Add a consumerTag on the RabbitMQ camel endpoint

[CAMEL-14395](https://issues.apache.org/jira/browse/CAMEL-14395)

camel-jms - Add option to turn off Artemis optimization for bytes messages

[CAMEL-14208](https://issues.apache.org/jira/browse/CAMEL-14208)

camel-undertow: add option to secure endpoints with Keycloak on spring-boot

[CAMEL-13844](https://issues.apache.org/jira/browse/CAMEL-13844)

RestConfiguration - Make it simpler and only have one

[CAMEL-13784](https://issues.apache.org/jira/browse/CAMEL-13784)

Update to AWS SDK V2

[CAMEL-13462](https://issues.apache.org/jira/browse/CAMEL-13462)

camel-azure - Allow a header to specify the blob name

[CAMEL-13440](https://issues.apache.org/jira/browse/CAMEL-13440)

camel3 - Cleanup so we no longer have need for RouteContext

### New Feature (10)

[CAMEL-14813](https://issues.apache.org/jira/browse/CAMEL-14813)

Remove CachingServiceDiscovery

[CAMEL-14776](https://issues.apache.org/jira/browse/CAMEL-14776)

Camel-Maven-Plugin: Moving blueprint support in a different plugin

[CAMEL-14738](https://issues.apache.org/jira/browse/CAMEL-14738)

Create a camel-platform-http-vertx component

[CAMEL-14670](https://issues.apache.org/jira/browse/CAMEL-14670)

@PropertyInject : support for complex - non primitive - injection

[CAMEL-14630](https://issues.apache.org/jira/browse/CAMEL-14630)

camel-gson: Add the possibility to get the unmarshal type from a header named CamelGsonUnmarshalType

[CAMEL-14598](https://issues.apache.org/jira/browse/CAMEL-14598)

Component Properties aliases

[CAMEL-14596](https://issues.apache.org/jira/browse/CAMEL-14596)

ToD and RecipientList with no cache can avoid caching endpoints

[CAMEL-14584](https://issues.apache.org/jira/browse/CAMEL-14584)

camel-elytron - Only use the JARs really needed

[CAMEL-14455](https://issues.apache.org/jira/browse/CAMEL-14455)

camel-rabbitmq - Option to override the Rabbit MQ DefaultExceptionHandler

[CAMEL-12863](https://issues.apache.org/jira/browse/CAMEL-12863)

Add configOptions to camel-restdsl-swagger-plugin for swagger-codegen-plugin

### Sub-task (18)

[CAMEL-14791](https://issues.apache.org/jira/browse/CAMEL-14791)

convert broken link: to checkable xref in camel-2.x

[CAMEL-14785](https://issues.apache.org/jira/browse/CAMEL-14785)

3.0.x xref fixes

[CAMEL-14784](https://issues.apache.org/jira/browse/CAMEL-14784)

2.x xref fixes.

[CAMEL-14783](https://issues.apache.org/jira/browse/CAMEL-14783)

website playbook update

[CAMEL-14758](https://issues.apache.org/jira/browse/CAMEL-14758)

aggregate eip content - camel-website - eip in components component

[CAMEL-14757](https://issues.apache.org/jira/browse/CAMEL-14757)

aggregate eip content - camel-website - separate eip component

[CAMEL-14756](https://issues.apache.org/jira/browse/CAMEL-14756)

aggregate eip content - 2.x branch

[CAMEL-14755](https://issues.apache.org/jira/browse/CAMEL-14755)

aggregate eip content - 3.0.x branch

[CAMEL-14754](https://issues.apache.org/jira/browse/CAMEL-14754)

aggregate eip content - master branch - part of components component

[CAMEL-14753](https://issues.apache.org/jira/browse/CAMEL-14753)

aggregate eip docs - master - as separate component

[CAMEL-14731](https://issues.apache.org/jira/browse/CAMEL-14731)

camel-website playbook rearrangement

[CAMEL-14730](https://issues.apache.org/jira/browse/CAMEL-14730)

2.x website source rearrangement

[CAMEL-14729](https://issues.apache.org/jira/browse/CAMEL-14729)

3.0.x branch website source rearrangement

[CAMEL-14728](https://issues.apache.org/jira/browse/CAMEL-14728)

master branch website source rearrangement

[CAMEL-14556](https://issues.apache.org/jira/browse/CAMEL-14556)

Create an AWS-Lambda component based on SDK v2

[CAMEL-14555](https://issues.apache.org/jira/browse/CAMEL-14555)

Create an AWS-S3 component based on SDK v2

[CAMEL-14554](https://issues.apache.org/jira/browse/CAMEL-14554)

Create an AWS-SWF component based on SDK v2

[CAMEL-14520](https://issues.apache.org/jira/browse/CAMEL-14520)

Create an AWS-Kinesis component based on SDK v2

### Task (33)

[CAMEL-14804](https://issues.apache.org/jira/browse/CAMEL-14804)

camel-servlet-osgi - Move osgi bits to camel-karaf

[CAMEL-14803](https://issues.apache.org/jira/browse/CAMEL-14803)

camel-karaf - Add docs for website

[CAMEL-14802](https://issues.apache.org/jira/browse/CAMEL-14802)

CI job for JDK 14

[CAMEL-14799](https://issues.apache.org/jira/browse/CAMEL-14799)

camel-blueprint - Does not start with recent changes

[CAMEL-14796](https://issues.apache.org/jira/browse/CAMEL-14796)

camel-catalog - has big dependency due that allcomponents thingy

[CAMEL-14790](https://issues.apache.org/jira/browse/CAMEL-14790)

camel-undertow: remove spring-boot starter after refactor of elytron component

[CAMEL-14787](https://issues.apache.org/jira/browse/CAMEL-14787)

camel-zookeeper-master - Test fails on CI

[CAMEL-14786](https://issues.apache.org/jira/browse/CAMEL-14786)

Move as much initialisation code from start() to init() phase

[CAMEL-14774](https://issues.apache.org/jira/browse/CAMEL-14774)

Camel-Package-Maven-Plugin: Add an option to avoid SyncPom execution on external project

[CAMEL-14773](https://issues.apache.org/jira/browse/CAMEL-14773)

Upgrade Debezium to 1.1.0.Final

[CAMEL-14743](https://issues.apache.org/jira/browse/CAMEL-14743)

camel-elytron: refactor component to use new SPI interface from camel-undertow

[CAMEL-14741](https://issues.apache.org/jira/browse/CAMEL-14741)

The FluentProducerTemplate.withTemplateCustomizer is broken

[CAMEL-14713](https://issues.apache.org/jira/browse/CAMEL-14713)

camel-main - Make caffeine optional

[CAMEL-14712](https://issues.apache.org/jira/browse/CAMEL-14712)

Provide an immutable lightweight camel context

[CAMEL-14706](https://issues.apache.org/jira/browse/CAMEL-14706)

camel-core - Optimize and remove JavaUuidGenerator

[CAMEL-14702](https://issues.apache.org/jira/browse/CAMEL-14702)

camel-core - Remove @XmlAdapter from model

[CAMEL-14669](https://issues.apache.org/jira/browse/CAMEL-14669)

Upgrade mockito to 3.3.x

[CAMEL-14665](https://issues.apache.org/jira/browse/CAMEL-14665)

Camel-AWS2 S3: Add downloadLink operation

[CAMEL-14664](https://issues.apache.org/jira/browse/CAMEL-14664)

Camel-AWS2-S3: add more integration tests

[CAMEL-14663](https://issues.apache.org/jira/browse/CAMEL-14663)

Camel-AWS2 S3: Add support for multipart upload

[CAMEL-14662](https://issues.apache.org/jira/browse/CAMEL-14662)

Upgrade to zookeeper 3.5.x

[CAMEL-14657](https://issues.apache.org/jira/browse/CAMEL-14657)

Make generate plugin less verbose

[CAMEL-14640](https://issues.apache.org/jira/browse/CAMEL-14640)

CVEs in the library dependencies

[CAMEL-14628](https://issues.apache.org/jira/browse/CAMEL-14628)

Make sure a compilation is triggered if the generators changed anything in the generated sources

[CAMEL-14627](https://issues.apache.org/jira/browse/CAMEL-14627)

Camel 3.2.x: We still have references to 3.1.0-SNAPSHOT

[CAMEL-14606](https://issues.apache.org/jira/browse/CAMEL-14606)

Yaml data format does not export snakeyaml version

[CAMEL-14605](https://issues.apache.org/jira/browse/CAMEL-14605)

EIP docs - The options are not automatic updated on build

[CAMEL-14604](https://issues.apache.org/jira/browse/CAMEL-14604)

camel-core - Wiretap.json is not up to date

[CAMEL-14592](https://issues.apache.org/jira/browse/CAMEL-14592)

Correct the camel-gson documentation

[CAMEL-14494](https://issues.apache.org/jira/browse/CAMEL-14494)

Breakdown azure-component into multiple components similar to the aws component

[CAMEL-14283](https://issues.apache.org/jira/browse/CAMEL-14283)

camel-website - Cleanup the EIP menu

[CAMEL-14020](https://issues.apache.org/jira/browse/CAMEL-14020)

Migrate deprecate getOut to getMessage in tests

[CAMEL-12191](https://issues.apache.org/jira/browse/CAMEL-12191)

Camel-Kafka: create an example on Kubernetes/Openshift by using Strimzi

### Test (2)

[CAMEL-14710](https://issues.apache.org/jira/browse/CAMEL-14710)

Camel-Jcache: Tests are failing

[CAMEL-14636](https://issues.apache.org/jira/browse/CAMEL-14636)

camel-spring-boot - camel-reactive-streams-starter fails test

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).