# Apache camel 3.0.0-RC1 Release

## New and Noteworthy

This release the first release candidate towards Camel 3.0.0 release.

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
      <version>3.0.0-RC1</version>
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
      <version>3.0.0-RC1</version>
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
| [apache-camel-3.0.0-RC1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC1/apache-camel-3.0.0-RC1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC1/apache-camel-3.0.0-RC1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.0.0-RC1/apache-camel-3.0.0-RC1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.0.0-RC1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.0.0-RC1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (23)

[CAMEL-13904](https://issues.apache.org/jira/browse/CAMEL-13904)

JMX - Early registered services may not be enlisted in XML DSL

[CAMEL-13877](https://issues.apache.org/jira/browse/CAMEL-13877)

RouteHealthCheck has NPE when JMX disabled

[CAMEL-13861](https://issues.apache.org/jira/browse/CAMEL-13861)

Camel Olingo: incorrect result in consumer

[CAMEL-13854](https://issues.apache.org/jira/browse/CAMEL-13854)

camel-microprofile-config: service file point to the wrong class

[CAMEL-13847](https://issues.apache.org/jira/browse/CAMEL-13847)

camel-webhook - Should be lenient properties

[CAMEL-13796](https://issues.apache.org/jira/browse/CAMEL-13796)

Salesforce Component IDLE\_TIMEOUT Blocks Async Request Responses

[CAMEL-13795](https://issues.apache.org/jira/browse/CAMEL-13795)

TokenXMLExpressionIterator with inheritNamespaceToken creates duplicate default namespace definition

[CAMEL-13783](https://issues.apache.org/jira/browse/CAMEL-13783)

Fix the camel-archetype-component to inherit from DefaultConsumer instead of ScheduledPollConsumer

[CAMEL-13776](https://issues.apache.org/jira/browse/CAMEL-13776)

\[MongoDB\] autoclosable cursor

[CAMEL-13770](https://issues.apache.org/jira/browse/CAMEL-13770)

Properties of class Map does not work with Spring Boot 2.x

[CAMEL-13751](https://issues.apache.org/jira/browse/CAMEL-13751)

camel-caffeine: exclude transitive dependencies not required

[CAMEL-13750](https://issues.apache.org/jira/browse/CAMEL-13750)

Incoming JMSCorrelationID is passed along when useMessageIDAsCorrelationID

[CAMEL-13746](https://issues.apache.org/jira/browse/CAMEL-13746)

camel-salesforce integration tests deserialization issue

[CAMEL-13711](https://issues.apache.org/jira/browse/CAMEL-13711)

Files.createTempFile not equivalent to File.createTempFile

[CAMEL-13707](https://issues.apache.org/jira/browse/CAMEL-13707)

camel-netty4-http - Query string issues

[CAMEL-13592](https://issues.apache.org/jira/browse/CAMEL-13592)

camel-sql - Repeated parameters in URI are not treated correctly

[CAMEL-13561](https://issues.apache.org/jira/browse/CAMEL-13561)

camel-hystrix - HystrixBadRequestException is swallowed

[CAMEL-13548](https://issues.apache.org/jira/browse/CAMEL-13548)

camel-spring build fails on windows

[CAMEL-13424](https://issues.apache.org/jira/browse/CAMEL-13424)

Rest Component custom routeId is not accessible in processor

[CAMEL-13267](https://issues.apache.org/jira/browse/CAMEL-13267)

Camel stops consuming queue after restart of RabbitMQ broker

[CAMEL-13094](https://issues.apache.org/jira/browse/CAMEL-13094)

Context MBean not unregistered on startup failure

[CAMEL-12968](https://issues.apache.org/jira/browse/CAMEL-12968)

DefaultFluentProducerTemplate is not thread safe (endpoint, etc.)

[CAMEL-12851](https://issues.apache.org/jira/browse/CAMEL-12851)

org.apache.camel.component.validator.CustomSchemaFactoryFeatureTest.testCustomSchemaFactory() failing with JDK 10

### Improvement (76)

[CAMEL-13896](https://issues.apache.org/jira/browse/CAMEL-13896)

camel3 - Use BeanIntrospection SPI instead of IntrospectionSupport

[CAMEL-13891](https://issues.apache.org/jira/browse/CAMEL-13891)

camel-cxf - Add spring.schemas for -spring URL so it works for same online url

[CAMEL-13879](https://issues.apache.org/jira/browse/CAMEL-13879)

Fix Corda's component's documentation

[CAMEL-13870](https://issues.apache.org/jira/browse/CAMEL-13870)

camel3 - Fast configuring of endpoint options

[CAMEL-13867](https://issues.apache.org/jira/browse/CAMEL-13867)

Upgrade to apache pulsar 2.4.0

[CAMEL-13864](https://issues.apache.org/jira/browse/CAMEL-13864)

JMS Component does not support non-durable shared subscription

[CAMEL-13863](https://issues.apache.org/jira/browse/CAMEL-13863)

camel3 - Optimize XmlConverterLoader

[CAMEL-13860](https://issues.apache.org/jira/browse/CAMEL-13860)

camel-properties: get\[Inital|Override\]Properties should never return null

[CAMEL-13859](https://issues.apache.org/jira/browse/CAMEL-13859)

came-properties: allow to filter properties by key when loading all

[CAMEL-13858](https://issues.apache.org/jira/browse/CAMEL-13858)

camel-properties: load properties should iterate through loadable property source in reverse order

[CAMEL-13857](https://issues.apache.org/jira/browse/CAMEL-13857)

camel-microprofile-config: should implement LoadablePropertiesSource

[CAMEL-13856](https://issues.apache.org/jira/browse/CAMEL-13856)

camel-microprofile-config: sould have an option to enable/disable automatic lookup of properties sources

[CAMEL-13855](https://issues.apache.org/jira/browse/CAMEL-13855)

camel-microprofile-config: discover properties sources from registry

[CAMEL-13853](https://issues.apache.org/jira/browse/CAMEL-13853)

camel-test AvailablePortFinder fails on WSL for Windows 10

[CAMEL-13850](https://issues.apache.org/jira/browse/CAMEL-13850)

camel3 - Property placeholders on EIP models can be optimized

[CAMEL-13848](https://issues.apache.org/jira/browse/CAMEL-13848)

Support room password in camel-xmpp

[CAMEL-13846](https://issues.apache.org/jira/browse/CAMEL-13846)

Make PropertyBindingSupport a fluent builder only

[CAMEL-13845](https://issues.apache.org/jira/browse/CAMEL-13845)

camel-telegram - Do not show authorizationToken in uri

[CAMEL-13841](https://issues.apache.org/jira/browse/CAMEL-13841)

Pulsar: Add the ability to manually acknowledge a message consumed from Pulsar

[CAMEL-13837](https://issues.apache.org/jira/browse/CAMEL-13837)

camel3 - FactoryFinder - Return null if not found instead of exception

[CAMEL-13832](https://issues.apache.org/jira/browse/CAMEL-13832)

Properties component - Check ENV before JVM System property

[CAMEL-13829](https://issues.apache.org/jira/browse/CAMEL-13829)

Deprecate transferExchange option

[CAMEL-13828](https://issues.apache.org/jira/browse/CAMEL-13828)

DefaultExchangeHolder - Do not propgate exchange id

[CAMEL-13810](https://issues.apache.org/jira/browse/CAMEL-13810)

camel3 - Always log ERROR if failed to start CamelContext

[CAMEL-13808](https://issues.apache.org/jira/browse/CAMEL-13808)

Intercept - Should only be configurable one time per route builder / camelcontext

[CAMEL-13801](https://issues.apache.org/jira/browse/CAMEL-13801)

camel3 - Use @BindToRegistry wherever possible

[CAMEL-13799](https://issues.apache.org/jira/browse/CAMEL-13799)

camel-cdi: Remove support for multiple context via @ContextName (was: NPE with recent camel-cdi changes)

[CAMEL-13797](https://issues.apache.org/jira/browse/CAMEL-13797)

Move @InvokeOnHeader/@InvokeOnHeaders to org.apache.camel.spi package

[CAMEL-13793](https://issues.apache.org/jira/browse/CAMEL-13793)

camel3 - Camel annotations with context ids should be deprecated

[CAMEL-13792](https://issues.apache.org/jira/browse/CAMEL-13792)

Rename components to default names

[CAMEL-13791](https://issues.apache.org/jira/browse/CAMEL-13791)

incoming message: Add QoS Information into a header

[CAMEL-13790](https://issues.apache.org/jira/browse/CAMEL-13790)

camel3 - Rename camel-http4 to camel-http

[CAMEL-13788](https://issues.apache.org/jira/browse/CAMEL-13788)

camel3 - Message API - Deprecate OUT

[CAMEL-13779](https://issues.apache.org/jira/browse/CAMEL-13779)

Camel AWS | SNS message attributes should support String.Array

[CAMEL-13774](https://issues.apache.org/jira/browse/CAMEL-13774)

camel-zipfile - Accept an iterator as body for zip

[CAMEL-13772](https://issues.apache.org/jira/browse/CAMEL-13772)

camel-cdi - Remove XML support

[CAMEL-13764](https://issues.apache.org/jira/browse/CAMEL-13764)

\[MongoDB\] provide connectionBean setting to component

[CAMEL-13763](https://issues.apache.org/jira/browse/CAMEL-13763)

elasticsearch-rest producer closes connection when route is reloaded from xml and stays closed

[CAMEL-13761](https://issues.apache.org/jira/browse/CAMEL-13761)

StartupListener runs before routes are started, contrary to Javadoc

[CAMEL-13760](https://issues.apache.org/jira/browse/CAMEL-13760)

camel3 - Property placeholder - Deprecate changing prefix/suffix tokens

[CAMEL-13759](https://issues.apache.org/jira/browse/CAMEL-13759)

camel3 - Remove poor mans debugger

[CAMEL-13755](https://issues.apache.org/jira/browse/CAMEL-13755)

camel3 - Handle fault should be internal advice instead of intercept strategy

[CAMEL-13749](https://issues.apache.org/jira/browse/CAMEL-13749)

Extend SpEL evaluation context with MapAccessor

[CAMEL-13747](https://issues.apache.org/jira/browse/CAMEL-13747)

Adding basic auth support to camel-solr

[CAMEL-13742](https://issues.apache.org/jira/browse/CAMEL-13742)

Extend сamel-cmis component with new operations

[CAMEL-13740](https://issues.apache.org/jira/browse/CAMEL-13740)

Document for XStream JSON not proper

[CAMEL-13739](https://issues.apache.org/jira/browse/CAMEL-13739)

Camel-test createJndiContext warning

[CAMEL-13736](https://issues.apache.org/jira/browse/CAMEL-13736)

Camel main - Support bean post processing on @BindToRegistry

[CAMEL-13733](https://issues.apache.org/jira/browse/CAMEL-13733)

camel-cloud - depend on camel-core-engine

[CAMEL-13732](https://issues.apache.org/jira/browse/CAMEL-13732)

Converting to boolean should always be strict

[CAMEL-13731](https://issues.apache.org/jira/browse/CAMEL-13731)

Implement String AggregationStrategy

[CAMEL-13712](https://issues.apache.org/jira/browse/CAMEL-13712)

If a javax.mail.Session gets referred to using the "session" URL parameter, Apache Camel Mail ignored its hostnames.

[CAMEL-13678](https://issues.apache.org/jira/browse/CAMEL-13678)

Attachments API on Message - Deprecate and remove

[CAMEL-13677](https://issues.apache.org/jira/browse/CAMEL-13677)

Move AttachmentConverterLoader out of camel-core

[CAMEL-13668](https://issues.apache.org/jira/browse/CAMEL-13668)

camel-main-maven-plugin - Generate java source for fast configuration

[CAMEL-13429](https://issues.apache.org/jira/browse/CAMEL-13429)

Rest DSL - Allow templating path parameters

[CAMEL-13399](https://issues.apache.org/jira/browse/CAMEL-13399)

ZipAggregationStrategy become slower when size of zip grows

[CAMEL-13259](https://issues.apache.org/jira/browse/CAMEL-13259)

Camel BOM - Add camel catalog and others

[CAMEL-13183](https://issues.apache.org/jira/browse/CAMEL-13183)

add support for jandex indexer

[CAMEL-13175](https://issues.apache.org/jira/browse/CAMEL-13175)

Consider removing useOriginalMessage functionality

[CAMEL-13083](https://issues.apache.org/jira/browse/CAMEL-13083)

Upgrade to latest Guava version for Swagger dependency

[CAMEL-13036](https://issues.apache.org/jira/browse/CAMEL-13036)

Add the possibility to disable the invocation of ModelHelper.dumpModelAsXml() during testing

[CAMEL-12872](https://issues.apache.org/jira/browse/CAMEL-12872)

When no route is defined, mention in log that it is the reason why it shutdowns the Camel Context automatically

[CAMEL-12864](https://issues.apache.org/jira/browse/CAMEL-12864)

rest: Host header should not overwrite host attribute on rest-swagger component

[CAMEL-11097](https://issues.apache.org/jira/browse/CAMEL-11097)

Injection of CamelContext inside a CamelContextAware bean

[CAMEL-10533](https://issues.apache.org/jira/browse/CAMEL-10533)

AggregateController - Add forceDiscardOfGroup method

[CAMEL-10456](https://issues.apache.org/jira/browse/CAMEL-10456)

Camel leaks TCCL

[CAMEL-10126](https://issues.apache.org/jira/browse/CAMEL-10126)

Aggregate - Has name clash for some options

[CAMEL-9971](https://issues.apache.org/jira/browse/CAMEL-9971)

file2 component should support appending chars in append mode

[CAMEL-7970](https://issues.apache.org/jira/browse/CAMEL-7970)

Container does not see the unregister event

[CAMEL-7677](https://issues.apache.org/jira/browse/CAMEL-7677)

advice with - Allow to influence interceptor/onException

[CAMEL-7550](https://issues.apache.org/jira/browse/CAMEL-7550)

Adding ability to look up objects using EntityManager.find in JPA component.

[CAMEL-7444](https://issues.apache.org/jira/browse/CAMEL-7444)

Camel MDC - Should propagate all keys

[CAMEL-6901](https://issues.apache.org/jira/browse/CAMEL-6901)

Intercept send to endpoint - Make it easier to do AOP before|after|around

[CAMEL-6715](https://issues.apache.org/jira/browse/CAMEL-6715)

camel-test-blueprint - Only one Camel context gets started on test startup

[CAMEL-5832](https://issues.apache.org/jira/browse/CAMEL-5832)

camel-jms - JMS consumer should detect JMSReplyTo being sending to itself to avoid circular looping

### New Feature (12)

[CAMEL-13898](https://issues.apache.org/jira/browse/CAMEL-13898)

ensure camel-cxf consumer can propagate protocol headers from camel exchange headers when throwing a soap fault

[CAMEL-13876](https://issues.apache.org/jira/browse/CAMEL-13876)

enable camel-undertow component to set custom HttpHandler

[CAMEL-13852](https://issues.apache.org/jira/browse/CAMEL-13852)

Support OData action's in camel-olingo4

[CAMEL-13838](https://issues.apache.org/jira/browse/CAMEL-13838)

camel - Add support for microprofile metrics

[CAMEL-13833](https://issues.apache.org/jira/browse/CAMEL-13833)

Properties component - Fallback to ENV should replace dots with underscores

[CAMEL-13786](https://issues.apache.org/jira/browse/CAMEL-13786)

camel-jms - Add option to configure deliveryDelay on JmsTemplate

[CAMEL-13734](https://issues.apache.org/jira/browse/CAMEL-13734)

camel-undertow - Support streaming of large data for HTTP endpoints

[CAMEL-13628](https://issues.apache.org/jira/browse/CAMEL-13628)

Implement camel-file-watch component

[CAMEL-13598](https://issues.apache.org/jira/browse/CAMEL-13598)

camel-olingo4 - Support ETag / If-Match Headers when using CUD operations

[CAMEL-13287](https://issues.apache.org/jira/browse/CAMEL-13287)

AggregationStrategy - Access original exchange in aggregate method

[CAMEL-13244](https://issues.apache.org/jira/browse/CAMEL-13244)

camel-salesforce : lazily log in to salesforce

[CAMEL-12983](https://issues.apache.org/jira/browse/CAMEL-12983)

camel-netty4-http - Allow direct streaming from big files to file output stream to disk

### Sub-task (1)

[CAMEL-11502](https://issues.apache.org/jira/browse/CAMEL-11502)

Cleanup .htaccess

### Task (27)

[CAMEL-13907](https://issues.apache.org/jira/browse/CAMEL-13907)

camel3 - JMX can clear its bean introspection cache after all MBeans have been registered

[CAMEL-13906](https://issues.apache.org/jira/browse/CAMEL-13906)

Component options - Only include if they have @Metadata

[CAMEL-13893](https://issues.apache.org/jira/browse/CAMEL-13893)

REST DSL Swagger Maven plugin integration test failure

[CAMEL-13871](https://issues.apache.org/jira/browse/CAMEL-13871)

documentation - Remove all the see also sections

[CAMEL-13843](https://issues.apache.org/jira/browse/CAMEL-13843)

PropertyBindingSupport: add an option to configure if properties have to be removed or not from the source map

[CAMEL-13836](https://issues.apache.org/jira/browse/CAMEL-13836)

camel-util: move SedaConstants to camel-seda

[CAMEL-13835](https://issues.apache.org/jira/browse/CAMEL-13835)

camel-util : cleanup pom

[CAMEL-13834](https://issues.apache.org/jira/browse/CAMEL-13834)

camel-util does not provide a sfl4j binding for testing

[CAMEL-13824](https://issues.apache.org/jira/browse/CAMEL-13824)

the documentation references a deleted component

[CAMEL-13822](https://issues.apache.org/jira/browse/CAMEL-13822)

Add missing Override annotations

[CAMEL-13811](https://issues.apache.org/jira/browse/CAMEL-13811)

Deprecate and remove camel-boon

[CAMEL-13806](https://issues.apache.org/jira/browse/CAMEL-13806)

camel-ejb - Deprecate and remove

[CAMEL-13767](https://issues.apache.org/jira/browse/CAMEL-13767)

Camel-elasticsearch-rest: Types are deprecated, we need to remove them and check if everything is still ok

[CAMEL-13765](https://issues.apache.org/jira/browse/CAMEL-13765)

Camel-Solr: Upgrade Solr to 8.x

[CAMEL-13762](https://issues.apache.org/jira/browse/CAMEL-13762)

Camel-Lucene: Upgrade Lucene to 8.x

[CAMEL-13756](https://issues.apache.org/jira/browse/CAMEL-13756)

Camel-Elasticsearch: Upgrade to 7.x

[CAMEL-13748](https://issues.apache.org/jira/browse/CAMEL-13748)

Create Spring Boot integration test for camel-file-watch component

[CAMEL-13738](https://issues.apache.org/jira/browse/CAMEL-13738)

parent/pom.xml - use dash in version properties

[CAMEL-13735](https://issues.apache.org/jira/browse/CAMEL-13735)

error-handler documentation refers to a method that has been removed in camel 3

[CAMEL-13730](https://issues.apache.org/jira/browse/CAMEL-13730)

NotifyBuilder MockComponent methods are deprecated and there is no replacement

[CAMEL-13623](https://issues.apache.org/jira/browse/CAMEL-13623)

Website - Multiproject components not listed in Component Reference

[CAMEL-13505](https://issues.apache.org/jira/browse/CAMEL-13505)

Camel-Tracer: New implementation

[CAMEL-13311](https://issues.apache.org/jira/browse/CAMEL-13311)

camel-cdi and camel-blueprint - Cleanup bean post processor

[CAMEL-13219](https://issues.apache.org/jira/browse/CAMEL-13219)

camel-http4 - move back as camel-http and/or add http as alternative default component

[CAMEL-13218](https://issues.apache.org/jira/browse/CAMEL-13218)

Can we get rid of jetty 9.2

[CAMEL-10910](https://issues.apache.org/jira/browse/CAMEL-10910)

Revisit if Pipeline should wrap single processor or not

[CAMEL-10013](https://issues.apache.org/jira/browse/CAMEL-10013)

Write automatic test validating syntax of every endpoint of the catalog

### Test (1)

[CAMEL-13629](https://issues.apache.org/jira/browse/CAMEL-13629)

Some tests are excluded from maven build because of wrong class name

### Wish (2)

[CAMEL-12003](https://issues.apache.org/jira/browse/CAMEL-12003)

FailFast mode for unit tests

[CAMEL-6325](https://issues.apache.org/jira/browse/CAMEL-6325)

Enhance aggregator pattern by discardOnFailure() route directive

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).