# Apache camel 3.1.0 Release

## New and Noteworthy

This release is the new Camel 3.1.0 major release.

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
      <version>3.1.0</version>
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
      <version>3.1.0</version>
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
| [apache-camel-3.1.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.1.0/apache-camel-3.1.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.1.0/apache-camel-3.1.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.1.0/apache-camel-3.1.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.1.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.1.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (65)

[CAMEL-14594](https://issues.apache.org/jira/browse/CAMEL-14594)

ProducerServicePool - Memory leak

[CAMEL-14593](https://issues.apache.org/jira/browse/CAMEL-14593)

Eager type converter creation breaks WildFly integration

[CAMEL-14591](https://issues.apache.org/jira/browse/CAMEL-14591)

Recipient List EIP - MemoryLeak

[CAMEL-14586](https://issues.apache.org/jira/browse/CAMEL-14586)

camel-core - Disable cache on some EIPs seems to not be working correlction

[CAMEL-14579](https://issues.apache.org/jira/browse/CAMEL-14579)

Camel-mail: MemoryLeak when sending mails using recipient list or dynamic to

[CAMEL-14577](https://issues.apache.org/jira/browse/CAMEL-14577)

QuartzEndpoint returns no trigger parameters

[CAMEL-14561](https://issues.apache.org/jira/browse/CAMEL-14561)

Camel-Blueprint fails on JDK8 with NPE

[CAMEL-14548](https://issues.apache.org/jira/browse/CAMEL-14548)

resilience4j doesn't catch configuration from spring boot

[CAMEL-14534](https://issues.apache.org/jira/browse/CAMEL-14534)

Wrong message in some cases in org.apache.camel.PropertyBindingException

[CAMEL-14529](https://issues.apache.org/jira/browse/CAMEL-14529)

Pipeline inconsistency due to mutable processors list

[CAMEL-14510](https://issues.apache.org/jira/browse/CAMEL-14510)

NullPointerException with @BeanInject

[CAMEL-14506](https://issues.apache.org/jira/browse/CAMEL-14506)

came-ftp - streamDownload=true and stepwise=true for larger files could cause deadlock

[CAMEL-14503](https://issues.apache.org/jira/browse/CAMEL-14503)

camel-package-maven-plugin:generate fails with NPE for component outside the camel source tree

[CAMEL-14492](https://issues.apache.org/jira/browse/CAMEL-14492)

EtcdKeysEndpoint cannot be cast to AbstractEtcdPollingEndpoint

[CAMEL-14462](https://issues.apache.org/jira/browse/CAMEL-14462)

Camel-Blueprint: Endpoint parameters not recognized

[CAMEL-14457](https://issues.apache.org/jira/browse/CAMEL-14457)

Groovy language: NoClassDefFoundError in OSGi environment

[CAMEL-14456](https://issues.apache.org/jira/browse/CAMEL-14456)

camel-master - RAW() parameter value in delegated URI gets encoded

[CAMEL-14453](https://issues.apache.org/jira/browse/CAMEL-14453)

ensure Camel Rest Swagger example work again

[CAMEL-14452](https://issues.apache.org/jira/browse/CAMEL-14452)

Unable to configure font or page size on PDF endpoints

[CAMEL-14449](https://issues.apache.org/jira/browse/CAMEL-14449)

camel-main: duration properties are ignored

[CAMEL-14447](https://issues.apache.org/jira/browse/CAMEL-14447)

OpenApi V3: ensure all variables are parsed for Server Url

[CAMEL-14442](https://issues.apache.org/jira/browse/CAMEL-14442)

Scheduler no longer shared between routes using the same scheduler name

[CAMEL-14441](https://issues.apache.org/jira/browse/CAMEL-14441)

Stomp connections are not established when the queues have additional features

[CAMEL-14439](https://issues.apache.org/jira/browse/CAMEL-14439)

camel-openapi-java: OasInfo may miss parent pointer

[CAMEL-14424](https://issues.apache.org/jira/browse/CAMEL-14424)

camel-salesforce - HTTP responses over 4 MB fail

[CAMEL-14420](https://issues.apache.org/jira/browse/CAMEL-14420)

Support \`KafkaOffsetBackingStore\` in camel-debezim

[CAMEL-14419](https://issues.apache.org/jira/browse/CAMEL-14419)

Enrich EIP - Should wrap in UoW

[CAMEL-14412](https://issues.apache.org/jira/browse/CAMEL-14412)

Maven central now requires HTTPS

[CAMEL-14396](https://issues.apache.org/jira/browse/CAMEL-14396)

websocket-jsr356 consumer fails when endpoint URI parameters are provided

[CAMEL-14390](https://issues.apache.org/jira/browse/CAMEL-14390)

websocket-jsr356 producer hangs

[CAMEL-14387](https://issues.apache.org/jira/browse/CAMEL-14387)

camel-salesforce - Null pointer exception when restart client in SubscriptionHelper

[CAMEL-14372](https://issues.apache.org/jira/browse/CAMEL-14372)

Validator component fails with java.lang.IllegalArgumentException: protocol = http host = null

[CAMEL-14368](https://issues.apache.org/jira/browse/CAMEL-14368)

can't gracefully shutdown a camel-undertow consumer endpoint

[CAMEL-14366](https://issues.apache.org/jira/browse/CAMEL-14366)

JUnit declared in compile scope

[CAMEL-14363](https://issues.apache.org/jira/browse/CAMEL-14363)

Camel netty requestTimeout doesn't work as expected

[CAMEL-14350](https://issues.apache.org/jira/browse/CAMEL-14350)

camel-main: xml routes discovery does not work outside the classpath

[CAMEL-14340](https://issues.apache.org/jira/browse/CAMEL-14340)

camel-core - Concurrency issue in multipool for non singleton producers

[CAMEL-14333](https://issues.apache.org/jira/browse/CAMEL-14333)

Camel Jgroups Component doesn't export org.apache.camel.component.jgroups.cluster

[CAMEL-14332](https://issues.apache.org/jira/browse/CAMEL-14332)

camel-blueprint - Camel route does not consider the value of ShutdownStrategy timeout.

[CAMEL-14327](https://issues.apache.org/jira/browse/CAMEL-14327)

Jt400PgmProducer doStop() method called on actively used instance

[CAMEL-14323](https://issues.apache.org/jira/browse/CAMEL-14323)

XMPP room with password disconnect after bootup

[CAMEL-14318](https://issues.apache.org/jira/browse/CAMEL-14318)

camel-blueprint - <proxy> in XSD is anyType

[CAMEL-14312](https://issues.apache.org/jira/browse/CAMEL-14312)

Fix issues reported by lgtm.com

[CAMEL-14306](https://issues.apache.org/jira/browse/CAMEL-14306)

Endpoint DSL - ToD sets hash parameter when using complex objects as parameters

[CAMEL-14303](https://issues.apache.org/jira/browse/CAMEL-14303)

Setting matchOnUriPrefix on netty-http Rest Component causes api route to fail

[CAMEL-14302](https://issues.apache.org/jira/browse/CAMEL-14302)

Camel-spring: No longer possible to invoke static method of non-spring bean

[CAMEL-14300](https://issues.apache.org/jira/browse/CAMEL-14300)

Java 8 Supplier overloadings break all DSLs

[CAMEL-14299](https://issues.apache.org/jira/browse/CAMEL-14299)

camel-sql - Dynamic producer (toD) problem

[CAMEL-14277](https://issues.apache.org/jira/browse/CAMEL-14277)

NPE when NATS server not configured

[CAMEL-14272](https://issues.apache.org/jira/browse/CAMEL-14272)

Configuring endpoint with bean reference should fail if no such bean found

[CAMEL-14271](https://issues.apache.org/jira/browse/CAMEL-14271)

camel di does not work for routes discovered from the registry

[CAMEL-14268](https://issues.apache.org/jira/browse/CAMEL-14268)

Component auto configuration fails in Java 11

[CAMEL-14267](https://issues.apache.org/jira/browse/CAMEL-14267)

Conversion fails with NullPointerException when the body is null at the end of a route and an outputType is set

[CAMEL-14265](https://issues.apache.org/jira/browse/CAMEL-14265)

camel-cdi - Standalone CDI with Camel Main discovers routes twice

[CAMEL-14257](https://issues.apache.org/jira/browse/CAMEL-14257)

allowUseOriginalMessage not configurable

[CAMEL-14243](https://issues.apache.org/jira/browse/CAMEL-14243)

Opentracing with JMS not working when JmsComponent is defined as a Spring bean

[CAMEL-14242](https://issues.apache.org/jira/browse/CAMEL-14242)

camel-rabbitmq - Binding parameters with x- is not possible when using endpointdsl

[CAMEL-14241](https://issues.apache.org/jira/browse/CAMEL-14241)

InfluxDb does not define its dependency on okio

[CAMEL-14234](https://issues.apache.org/jira/browse/CAMEL-14234)

Project generated with camel-archetype-spring-boot cannot be built

[CAMEL-14224](https://issues.apache.org/jira/browse/CAMEL-14224)

Camel-Websocket: The sendToAll method in the Producer is really slow

[CAMEL-14223](https://issues.apache.org/jira/browse/CAMEL-14223)

EndpointBuilderFactory is not updated whenever \`:camel-package:generate-endpoint-dsl\` is executed

[CAMEL-14220](https://issues.apache.org/jira/browse/CAMEL-14220)

camel-activemq - Setting brokerURL via camel-main issue

[CAMEL-14219](https://issues.apache.org/jira/browse/CAMEL-14219)

ReactiveStreams subscriber does not enforce type conversion

[CAMEL-14213](https://issues.apache.org/jira/browse/CAMEL-14213)

camel-jms - Using XA and having 2 or more connection factories issue

[CAMEL-11947](https://issues.apache.org/jira/browse/CAMEL-11947)

Race condition in iec60870 producer

### Improvement (131)

[CAMEL-14590](https://issues.apache.org/jira/browse/CAMEL-14590)

Camel-Pulsar consumer calls unsubscribe on doStop/doSuspend, potentially deleting subscription

[CAMEL-14589](https://issues.apache.org/jira/browse/CAMEL-14589)

camel-cxf - Service beans can only be set via context

[CAMEL-14582](https://issues.apache.org/jira/browse/CAMEL-14582)

camel-bean - Optimize excluded methods

[CAMEL-14580](https://issues.apache.org/jira/browse/CAMEL-14580)

camel-main - Add option to clear reifier when no need to add new routes

[CAMEL-14572](https://issues.apache.org/jira/browse/CAMEL-14572)

camel-core - Optimize type converter for some basic convertions

[CAMEL-14571](https://issues.apache.org/jira/browse/CAMEL-14571)

camel-core - Optimize type converter eager created

[CAMEL-14570](https://issues.apache.org/jira/browse/CAMEL-14570)

camel-zookeeper-master - Use testcontainers for testing

[CAMEL-14569](https://issues.apache.org/jira/browse/CAMEL-14569)

camel-zookeeper - Use test containers for testing

[CAMEL-14564](https://issues.apache.org/jira/browse/CAMEL-14564)

Webhook endpoint may not be fully initialized when the route policy is applied

[CAMEL-14563](https://issues.apache.org/jira/browse/CAMEL-14563)

The camel api generator maven plugin does not support packages correctly

[CAMEL-14560](https://issues.apache.org/jira/browse/CAMEL-14560)

Use a custom xref checker as the antora one is very slow

[CAMEL-14559](https://issues.apache.org/jira/browse/CAMEL-14559)

Use String in definition fields to be able to leverage property placeholders

[CAMEL-14546](https://issues.apache.org/jira/browse/CAMEL-14546)

camel-xmlsecurity - Split up into verify and sign endpoints

[CAMEL-14545](https://issues.apache.org/jira/browse/CAMEL-14545)

Document the Camel Catalog

[CAMEL-14538](https://issues.apache.org/jira/browse/CAMEL-14538)

camel-core - Do not load type converters via package scanning by default

[CAMEL-14523](https://issues.apache.org/jira/browse/CAMEL-14523)

Sort component options correctly

[CAMEL-14521](https://issues.apache.org/jira/browse/CAMEL-14521)

Unicode problem in Bindy component for fixed length data

[CAMEL-14517](https://issues.apache.org/jira/browse/CAMEL-14517)

camel-core - JAXB JARs should be dependencies on camel-xml-jaxb and not globally

[CAMEL-14515](https://issues.apache.org/jira/browse/CAMEL-14515)

camel-core - Include spi annotations in camel-api

[CAMEL-14509](https://issues.apache.org/jira/browse/CAMEL-14509)

camel-package-maven-plugin - generate-component - Make it generate so the code is in the JAR by default

[CAMEL-14502](https://issues.apache.org/jira/browse/CAMEL-14502)

JSR 356 Websocket component does not work properly on Spring Boot

[CAMEL-14501](https://issues.apache.org/jira/browse/CAMEL-14501)

gain fully control of xml parser used by saxon

[CAMEL-14500](https://issues.apache.org/jira/browse/CAMEL-14500)

camel-core - spi-annotations is not optional

[CAMEL-14498](https://issues.apache.org/jira/browse/CAMEL-14498)

camel-core - Make RuntimeCamelCatalog a simpler API

[CAMEL-14497](https://issues.apache.org/jira/browse/CAMEL-14497)

camel-core - Avoid camel-util-json if not needed

[CAMEL-14489](https://issues.apache.org/jira/browse/CAMEL-14489)

camel-core-engine - XML and JAXB should be optional

[CAMEL-14487](https://issues.apache.org/jira/browse/CAMEL-14487)

camel-jaxp - Rename to camel-xml-jaxp

[CAMEL-14485](https://issues.apache.org/jira/browse/CAMEL-14485)

camel-componentdsl - Sort the component in the pom.xml and ComponentsBuilderFactory

[CAMEL-14484](https://issues.apache.org/jira/browse/CAMEL-14484)

ValidateReifier requires camel-jaxp

[CAMEL-14483](https://issues.apache.org/jira/browse/CAMEL-14483)

camel-endpointdsl dependency on camel-jaxp and camel-util-json

[CAMEL-14481](https://issues.apache.org/jira/browse/CAMEL-14481)

camel-spring-boot: Remove camel-management to disable JMX by default

[CAMEL-14477](https://issues.apache.org/jira/browse/CAMEL-14477)

camel-netty - Disable object serialization

[CAMEL-14471](https://issues.apache.org/jira/browse/CAMEL-14471)

camel-spring-boot: Disable proxying of bean methods for auto-configuration classes

[CAMEL-14466](https://issues.apache.org/jira/browse/CAMEL-14466)

camel-core - Optimize reduce error handler memory usage

[CAMEL-14461](https://issues.apache.org/jira/browse/CAMEL-14461)

camel-core - Make RuntimeCatalog optional and in its own module

[CAMEL-14460](https://issues.apache.org/jira/browse/CAMEL-14460)

camel-core - Optimize and allow to turn off case insensitive headers

[CAMEL-14438](https://issues.apache.org/jira/browse/CAMEL-14438)

camel-core - Optimize core for checking for stop routing

[CAMEL-14436](https://issues.apache.org/jira/browse/CAMEL-14436)

CamelContext - Move ReactiveExecutor to ExtendedCamelContext

[CAMEL-14435](https://issues.apache.org/jira/browse/CAMEL-14435)

camel-core - Optimize using reactive executor

[CAMEL-14433](https://issues.apache.org/jira/browse/CAMEL-14433)

Optimize core - Message ID should default to be same as exchangeID

[CAMEL-14428](https://issues.apache.org/jira/browse/CAMEL-14428)

Terminate the JVM for OutOfMemoryError when running tests

[CAMEL-14427](https://issues.apache.org/jira/browse/CAMEL-14427)

camel-core - Optimize UnitOfWork route context push/pop

[CAMEL-14426](https://issues.apache.org/jira/browse/CAMEL-14426)

camel-core - Optimize inflight repository

[CAMEL-14425](https://issues.apache.org/jira/browse/CAMEL-14425)

Mail Consumer Performance Optimization

[CAMEL-14422](https://issues.apache.org/jira/browse/CAMEL-14422)

DefaultShutdownStrategy not masking sensitive information

[CAMEL-14421](https://issues.apache.org/jira/browse/CAMEL-14421)

optimize core - ServiceSupport should not have instance logger

[CAMEL-14418](https://issues.apache.org/jira/browse/CAMEL-14418)

camel-timer - Add option to turn on/off metadata

[CAMEL-14416](https://issues.apache.org/jira/browse/CAMEL-14416)

Camel Pulsar: support subscriptionInitialPosition for consumers

[CAMEL-14414](https://issues.apache.org/jira/browse/CAMEL-14414)

Aggregation completion has inconsistent property/header handling

[CAMEL-14411](https://issues.apache.org/jira/browse/CAMEL-14411)

Avoid using reflection when configuring DataFormats

[CAMEL-14409](https://issues.apache.org/jira/browse/CAMEL-14409)

camel-core - Optimize Exchange

[CAMEL-14406](https://issues.apache.org/jira/browse/CAMEL-14406)

Component configurer - Generate API for returning which properties the component have

[CAMEL-14403](https://issues.apache.org/jira/browse/CAMEL-14403)

Add capability to customize server endpoints created by websocket-jsr356 consumer

[CAMEL-14401](https://issues.apache.org/jira/browse/CAMEL-14401)

Restore default host/port options for IPFS

[CAMEL-14399](https://issues.apache.org/jira/browse/CAMEL-14399)

camel-osgi OsgiDefaultCamelContext does not use JmxManagementStrategyFactory

[CAMEL-14398](https://issues.apache.org/jira/browse/CAMEL-14398)

camel-core - MessageHistory off by default

[CAMEL-14397](https://issues.apache.org/jira/browse/CAMEL-14397)

DefaultComponent should prefer getting the configurers from the registry before checking the FactoryFinder

[CAMEL-14393](https://issues.apache.org/jira/browse/CAMEL-14393)

Components that are DelegateEndpoint need to set some basic options

[CAMEL-14392](https://issues.apache.org/jira/browse/CAMEL-14392)

Components that are consumer only should not have option lazyStartProducer

[CAMEL-14389](https://issues.apache.org/jira/browse/CAMEL-14389)

Make entrypoint for "endpoint dsl" static

[CAMEL-14384](https://issues.apache.org/jira/browse/CAMEL-14384)

camel-jsonpath: Do not use reflection on the annotation proxy in DefaultAnnotationExpressionFactory

[CAMEL-14383](https://issues.apache.org/jira/browse/CAMEL-14383)

camel-core - Bean language add support for declaring type explicit

[CAMEL-14380](https://issues.apache.org/jira/browse/CAMEL-14380)

camel-core - Add hostname function to simple language

[CAMEL-14379](https://issues.apache.org/jira/browse/CAMEL-14379)

camel-core - Route lifecycle should not log full endpoint uris

[CAMEL-14377](https://issues.apache.org/jira/browse/CAMEL-14377)

Add configuration option to disable BraintreeLogHandler

[CAMEL-14376](https://issues.apache.org/jira/browse/CAMEL-14376)

camel-netty-http - Drop servlet dependency

[CAMEL-14375](https://issues.apache.org/jira/browse/CAMEL-14375)

camel-kafka - The saslJaasConfig option may contain sensitive information that can be logged

[CAMEL-14374](https://issues.apache.org/jira/browse/CAMEL-14374)

Camel-irc validation of endpoint's url fails for correct url

[CAMEL-14371](https://issues.apache.org/jira/browse/CAMEL-14371)

Upgrade to velocity 2.1

[CAMEL-14367](https://issues.apache.org/jira/browse/CAMEL-14367)

review netty-all usage

[CAMEL-14364](https://issues.apache.org/jira/browse/CAMEL-14364)

Endpoint DSL - Add default values in javadoc

[CAMEL-14361](https://issues.apache.org/jira/browse/CAMEL-14361)

camel-http - Avoid reflection in creating http method

[CAMEL-14359](https://issues.apache.org/jira/browse/CAMEL-14359)

camel-bean - Let cache be default enabled

[CAMEL-14357](https://issues.apache.org/jira/browse/CAMEL-14357)

camel-bean - Add start/stop to BeanHolder so we can do eager lookup

[CAMEL-14356](https://issues.apache.org/jira/browse/CAMEL-14356)

camel-core - toString of processors should favour just outputting their node id

[CAMEL-14355](https://issues.apache.org/jira/browse/CAMEL-14355)

PDF producer should close PDF documents

[CAMEL-14354](https://issues.apache.org/jira/browse/CAMEL-14354)

camel-core - Optimize unnecessary object allocations

[CAMEL-14353](https://issues.apache.org/jira/browse/CAMEL-14353)

Eager init LRUCacheFactory

[CAMEL-14352](https://issues.apache.org/jira/browse/CAMEL-14352)

Add camel-openapi as api-doc discovered component

[CAMEL-14351](https://issues.apache.org/jira/browse/CAMEL-14351)

camel-rest - Rest producer may detect multiple rest producer factory

[CAMEL-14349](https://issues.apache.org/jira/browse/CAMEL-14349)

camel-core - Transformer and Validator registry should be on-demand

[CAMEL-14347](https://issues.apache.org/jira/browse/CAMEL-14347)

camel-core - Remove default producer/consumer service pool from CamelContext

[CAMEL-14346](https://issues.apache.org/jira/browse/CAMEL-14346)

Camel-CoAP: Add a recommendedCipherSuitesOnly option to the endpoint

[CAMEL-14345](https://issues.apache.org/jira/browse/CAMEL-14345)

camel-core - Optimize SendProcessor to not use ProducerCache when not needed

[CAMEL-14344](https://issues.apache.org/jira/browse/CAMEL-14344)

camel-milo - Upgrade to newer milo version

[CAMEL-14342](https://issues.apache.org/jira/browse/CAMEL-14342)

Add cacheSize option to recipientList EIP

[CAMEL-14339](https://issues.apache.org/jira/browse/CAMEL-14339)

JMX - ManagedProducer - should have routeId

[CAMEL-14338](https://issues.apache.org/jira/browse/CAMEL-14338)

Processor - Add RouteIdAware so EIP processors can know which route they are serving

[CAMEL-14336](https://issues.apache.org/jira/browse/CAMEL-14336)

Default shutdown timeout should be reduced to 45 seconds

[CAMEL-14330](https://issues.apache.org/jira/browse/CAMEL-14330)

camel-aws-lambda - Operation should invoke function by default

[CAMEL-14329](https://issues.apache.org/jira/browse/CAMEL-14329)

Adding component should not autowire singleton from registry in nested mode

[CAMEL-14328](https://issues.apache.org/jira/browse/CAMEL-14328)

camel-aws-lambda - Function should not be configurable on component level

[CAMEL-14325](https://issues.apache.org/jira/browse/CAMEL-14325)

Add new functions on camel-cmis component

[CAMEL-14321](https://issues.apache.org/jira/browse/CAMEL-14321)

camel-osgi-activator Allow RouteBuilders to be added Pre Camel Context Start

[CAMEL-14316](https://issues.apache.org/jira/browse/CAMEL-14316)

Http component - Tests cleanup

[CAMEL-14313](https://issues.apache.org/jira/browse/CAMEL-14313)

Camel-AWS Translate: Add terminology names support

[CAMEL-14311](https://issues.apache.org/jira/browse/CAMEL-14311)

Provide validation for Camel properties files

[CAMEL-14309](https://issues.apache.org/jira/browse/CAMEL-14309)

Include Camel Main in the catalog

[CAMEL-14308](https://issues.apache.org/jira/browse/CAMEL-14308)

Upgrade to Kafka 2.4.x

[CAMEL-14307](https://issues.apache.org/jira/browse/CAMEL-14307)

camel-rabbitmq - unable to set empty routing key when declaring DLX

[CAMEL-14292](https://issues.apache.org/jira/browse/CAMEL-14292)

Remove unwanted dependency to google-http-client library

[CAMEL-14288](https://issues.apache.org/jira/browse/CAMEL-14288)

Endpoint configurer should deal better with list types

[CAMEL-14287](https://issues.apache.org/jira/browse/CAMEL-14287)

getComponent on CamelContext should initialize component

[CAMEL-14284](https://issues.apache.org/jira/browse/CAMEL-14284)

Configuring endpoint should set properties on endpoint and not configuration object

[CAMEL-14278](https://issues.apache.org/jira/browse/CAMEL-14278)

Upgrade to microprofile config 1.5

[CAMEL-14275](https://issues.apache.org/jira/browse/CAMEL-14275)

Camel component option with Properties should be configurable in SB

[CAMEL-14273](https://issues.apache.org/jira/browse/CAMEL-14273)

Configuring endpoint which fails in setter should repot this as property binding exception

[CAMEL-14270](https://issues.apache.org/jira/browse/CAMEL-14270)

\[camel-quart2-starter\] Can't set properties using application.properties

[CAMEL-14266](https://issues.apache.org/jira/browse/CAMEL-14266)

Add getStartDate to CamelContext api

[CAMEL-14263](https://issues.apache.org/jira/browse/CAMEL-14263)

Generate configurers for types annotated with @UriParams

[CAMEL-14253](https://issues.apache.org/jira/browse/CAMEL-14253)

camel-nats - Configure brokers on component level

[CAMEL-14251](https://issues.apache.org/jira/browse/CAMEL-14251)

camel-nats - Store message payload in body/headers

[CAMEL-14250](https://issues.apache.org/jira/browse/CAMEL-14250)

Allow custom configurations into Kafka component

[CAMEL-14247](https://issues.apache.org/jira/browse/CAMEL-14247)

camel-netty - Turn off component level shared thread pool and use nettys workers directly

[CAMEL-14246](https://issues.apache.org/jira/browse/CAMEL-14246)

Camel-SQL: Relax the modifier for datasource setter by removing final

[CAMEL-14245](https://issues.apache.org/jira/browse/CAMEL-14245)

\[camel-main\] allow to enable/disable auto confioguiration per component/language/data-format

[CAMEL-14240](https://issues.apache.org/jira/browse/CAMEL-14240)

Add backlogTracing into the spring/blueprint XML

[CAMEL-14238](https://issues.apache.org/jira/browse/CAMEL-14238)

Ensure generated catalog is providing a valid json even if there is no description provided

[CAMEL-14233](https://issues.apache.org/jira/browse/CAMEL-14233)

camel-kafka - topic overriding not possible when using aggregation

[CAMEL-14229](https://issues.apache.org/jira/browse/CAMEL-14229)

STOMP headers are missing in the Exchange

[CAMEL-14228](https://issues.apache.org/jira/browse/CAMEL-14228)

camel-netty - Let netty calculate the default worker count

[CAMEL-14154](https://issues.apache.org/jira/browse/CAMEL-14154)

Add option to create cache if it doesn't exists in camel-infinispan

[CAMEL-14074](https://issues.apache.org/jira/browse/CAMEL-14074)

http - Allow restricted headers

[CAMEL-13830](https://issues.apache.org/jira/browse/CAMEL-13830)

Move examples to a new camel-examples git repo

[CAMEL-13575](https://issues.apache.org/jira/browse/CAMEL-13575)

Use strings instead of boolean/integer/long in definition fields

[CAMEL-13213](https://issues.apache.org/jira/browse/CAMEL-13213)

Cannot use rest-swagger component with swagger.json provided over HTTPS protocol

[CAMEL-12962](https://issues.apache.org/jira/browse/CAMEL-12962)

camel-elasticsearch - Allow from and size for SearchSource / SearchRequest to be set via URI

[CAMEL-12219](https://issues.apache.org/jira/browse/CAMEL-12219)

Camel-Solr: support for soft commit

[CAMEL-11833](https://issues.apache.org/jira/browse/CAMEL-11833)

camel-catalog : provide a catalog model

[CAMEL-11727](https://issues.apache.org/jira/browse/CAMEL-11727)

Upgrade Groovy to version containing Ivy fixes for cache resolution

[CAMEL-6950](https://issues.apache.org/jira/browse/CAMEL-6950)

camel-sjms: Lacks reconnection logic in case of exception

### New Feature (25)

[CAMEL-14588](https://issues.apache.org/jira/browse/CAMEL-14588)

MailConsumer: Move mail after processing

[CAMEL-14525](https://issues.apache.org/jira/browse/CAMEL-14525)

provide a bean definition to the auto configuration by property feature

[CAMEL-14475](https://issues.apache.org/jira/browse/CAMEL-14475)

camel-core - Make loading XML pluggable via SPI

[CAMEL-14468](https://issues.apache.org/jira/browse/CAMEL-14468)

Add support for classification in camel-weka

[CAMEL-14443](https://issues.apache.org/jira/browse/CAMEL-14443)

Add new producers to camel-jira

[CAMEL-14440](https://issues.apache.org/jira/browse/CAMEL-14440)

Add Workday report as a service component.

[CAMEL-14417](https://issues.apache.org/jira/browse/CAMEL-14417)

\[camel-jslt\] Create spring-boot starter for camel-jslt

[CAMEL-14400](https://issues.apache.org/jira/browse/CAMEL-14400)

Add support for Weka Data Mining

[CAMEL-14385](https://issues.apache.org/jira/browse/CAMEL-14385)

Camel-cron component

[CAMEL-14360](https://issues.apache.org/jira/browse/CAMEL-14360)

Allow overriding message key and partition key for aggregated kafka messages

[CAMEL-14348](https://issues.apache.org/jira/browse/CAMEL-14348)

Camel-AWS Lambda: Add alias operations

[CAMEL-14315](https://issues.apache.org/jira/browse/CAMEL-14315)

add openapi-rest-dsl-generator

[CAMEL-14301](https://issues.apache.org/jira/browse/CAMEL-14301)

Stomp Component has no option to set custom headers

[CAMEL-14282](https://issues.apache.org/jira/browse/CAMEL-14282)

came-nsq - Configure servers on component level

[CAMEL-14279](https://issues.apache.org/jira/browse/CAMEL-14279)

Move camel-core-osgi-activator to Components camel-osgi-activator

[CAMEL-14252](https://issues.apache.org/jira/browse/CAMEL-14252)

camel-nats - Add support for reply-to in consumer

[CAMEL-14235](https://issues.apache.org/jira/browse/CAMEL-14235)

camel-seda - Add option to discard if full

[CAMEL-14227](https://issues.apache.org/jira/browse/CAMEL-14227)

camel-rest-swagger - Add support for OpenApi 3.0 spec

[CAMEL-14221](https://issues.apache.org/jira/browse/CAMEL-14221)

Stomp Component has no option to set version

[CAMEL-14215](https://issues.apache.org/jira/browse/CAMEL-14215)

Camel Main for OSGi

[CAMEL-14159](https://issues.apache.org/jira/browse/CAMEL-14159)

camel-elytron - Security component

[CAMEL-13903](https://issues.apache.org/jira/browse/CAMEL-13903)

camel-telegram - use a stock HTTP client instead of the JAX-RS client

[CAMEL-13807](https://issues.apache.org/jira/browse/CAMEL-13807)

Component DSL - To configure components like endpoint DSL

[CAMEL-13699](https://issues.apache.org/jira/browse/CAMEL-13699)

Add Json to Json transformation using JSLT

[CAMEL-12619](https://issues.apache.org/jira/browse/CAMEL-12619)

camel-swagger-java - Add support for 3.0 spec

### Sub-task (19)

[CAMEL-14553](https://issues.apache.org/jira/browse/CAMEL-14553)

Create an AWS-SQS component based on SDK v2

[CAMEL-14552](https://issues.apache.org/jira/browse/CAMEL-14552)

Create an AWS-SNS component based on SDK v2

[CAMEL-14551](https://issues.apache.org/jira/browse/CAMEL-14551)

Create an AWS-SES component based on SDK v2

[CAMEL-14550](https://issues.apache.org/jira/browse/CAMEL-14550)

Create an AWS-SDB component based on SDK v2

[CAMEL-14519](https://issues.apache.org/jira/browse/CAMEL-14519)

Create an AWS-DDB component based on SDK v2

[CAMEL-14518](https://issues.apache.org/jira/browse/CAMEL-14518)

Create an AWS-EC2 component based on SDK v2

[CAMEL-14508](https://issues.apache.org/jira/browse/CAMEL-14508)

Create an AWS-CloudWatch component based on SDK v2

[CAMEL-14491](https://issues.apache.org/jira/browse/CAMEL-14491)

Create an AWS-IAM component based on SDK v2

[CAMEL-14478](https://issues.apache.org/jira/browse/CAMEL-14478)

Create an AWS-KMS component based on SDK v2

[CAMEL-14476](https://issues.apache.org/jira/browse/CAMEL-14476)

Able to extend workday component for futher entities support

[CAMEL-14464](https://issues.apache.org/jira/browse/CAMEL-14464)

Create an AWS-MSK component based on SDK v2

[CAMEL-14463](https://issues.apache.org/jira/browse/CAMEL-14463)

Create an AWS-MQ component based on SDK v2

[CAMEL-14458](https://issues.apache.org/jira/browse/CAMEL-14458)

Create an AWS-EKS component based on SDK v2

[CAMEL-14446](https://issues.apache.org/jira/browse/CAMEL-14446)

Create an AWS-ECS component based on SDK v2

[CAMEL-14408](https://issues.apache.org/jira/browse/CAMEL-14408)

Create an AWS-Translate component based on SDK v2

[CAMEL-13228](https://issues.apache.org/jira/browse/CAMEL-13228)

telegram - Games support

[CAMEL-13226](https://issues.apache.org/jira/browse/CAMEL-13226)

telegram - Stickers support

[CAMEL-13224](https://issues.apache.org/jira/browse/CAMEL-13224)

telegram - Inline mode

[CAMEL-13223](https://issues.apache.org/jira/browse/CAMEL-13223)

telegram - Implement methods to update messages

### Task (44)

[CAMEL-14585](https://issues.apache.org/jira/browse/CAMEL-14585)

camel-spring-boot - The BOM includes a wrong target artifactId

[CAMEL-14558](https://issues.apache.org/jira/browse/CAMEL-14558)

Execute camel-kafak tests with testcontainers

[CAMEL-14549](https://issues.apache.org/jira/browse/CAMEL-14549)

Remove camel-itest-karaf

[CAMEL-14543](https://issues.apache.org/jira/browse/CAMEL-14543)

Execute camel-etcd tests with testcontainers

[CAMEL-14539](https://issues.apache.org/jira/browse/CAMEL-14539)

camel-spring-boot - Add STARTER markers in doc files

[CAMEL-14532](https://issues.apache.org/jira/browse/CAMEL-14532)

Fix issues with camel-snakeyaml

[CAMEL-14530](https://issues.apache.org/jira/browse/CAMEL-14530)

camel-catalog - Remove html docs

[CAMEL-14528](https://issues.apache.org/jira/browse/CAMEL-14528)

Move camel-spring-boot-\* into a core folder

[CAMEL-14516](https://issues.apache.org/jira/browse/CAMEL-14516)

Components should use the endpoint configurer when possible

[CAMEL-14513](https://issues.apache.org/jira/browse/CAMEL-14513)

camel-cdi - Remove OSGi stuff

[CAMEL-14507](https://issues.apache.org/jira/browse/CAMEL-14507)

Enhance components/endpoints configurers to inherit the parent

[CAMEL-14505](https://issues.apache.org/jira/browse/CAMEL-14505)

Remove meta-annotations

[CAMEL-14504](https://issues.apache.org/jira/browse/CAMEL-14504)

camel-apt - No longer used replaced by camel-package-maven-plugin

[CAMEL-14474](https://issues.apache.org/jira/browse/CAMEL-14474)

Dead link in "Message Exchange" doc to "Exchange" doc

[CAMEL-14469](https://issues.apache.org/jira/browse/CAMEL-14469)

Switch to maven plugins and remove apt processors

[CAMEL-14459](https://issues.apache.org/jira/browse/CAMEL-14459)

camel-webhook - RAW() parameter value handling in delegated URI

[CAMEL-14451](https://issues.apache.org/jira/browse/CAMEL-14451)

Camel master doesn't build on JDK11

[CAMEL-14448](https://issues.apache.org/jira/browse/CAMEL-14448)

Move all generated source code in git

[CAMEL-14445](https://issues.apache.org/jira/browse/CAMEL-14445)

Remove the property placeholder resolution inside definitions

[CAMEL-14444](https://issues.apache.org/jira/browse/CAMEL-14444)

Build speed improvements

[CAMEL-14437](https://issues.apache.org/jira/browse/CAMEL-14437)

Use a single model / json representation for all internal tooling generators

[CAMEL-14415](https://issues.apache.org/jira/browse/CAMEL-14415)

Camel-itests-spring-boot should be removed from the main repository

[CAMEL-14404](https://issues.apache.org/jira/browse/CAMEL-14404)

Provide a lightweight xml parser

[CAMEL-14388](https://issues.apache.org/jira/browse/CAMEL-14388)

Camel-Slack: Remove username from SlackMessage, since the API doesn't return it anymore

[CAMEL-14382](https://issues.apache.org/jira/browse/CAMEL-14382)

camel-core test failures

[CAMEL-14365](https://issues.apache.org/jira/browse/CAMEL-14365)

Create OpenTracing SpanDecorator for platform-http component

[CAMEL-14334](https://issues.apache.org/jira/browse/CAMEL-14334)

camel-restdsl-openapi-plugin: tests are failing

[CAMEL-14331](https://issues.apache.org/jira/browse/CAMEL-14331)

camel-spring-boot - Dev profile fails

[CAMEL-14320](https://issues.apache.org/jira/browse/CAMEL-14320)

Update building instructions

[CAMEL-14314](https://issues.apache.org/jira/browse/CAMEL-14314)

Camel-AWS Translate: Being able of set source and target language as endpoint options

[CAMEL-14295](https://issues.apache.org/jira/browse/CAMEL-14295)

Camel-cm-sms: Karaf and Spring Boot integration tests are broken

[CAMEL-14290](https://issues.apache.org/jira/browse/CAMEL-14290)

Upgrade to pulsar 2.4.2

[CAMEL-14286](https://issues.apache.org/jira/browse/CAMEL-14286)

camel-osgi-activator Create Examples for Component Usage

[CAMEL-14285](https://issues.apache.org/jira/browse/CAMEL-14285)

came-osgi-activator create tests in project based on Karaf bundle install rather than features

[CAMEL-14276](https://issues.apache.org/jira/browse/CAMEL-14276)

Move camel-core-osgi-activator to components

[CAMEL-14274](https://issues.apache.org/jira/browse/CAMEL-14274)

camel-crypto-cms - Deprecate this component as its hard to maintain

[CAMEL-14259](https://issues.apache.org/jira/browse/CAMEL-14259)

camel-spring-boot - When using main-run-controller then CamelContext is initialized twice

[CAMEL-14255](https://issues.apache.org/jira/browse/CAMEL-14255)

Deadlink for ExchangePattern

[CAMEL-14254](https://issues.apache.org/jira/browse/CAMEL-14254)

Add Camel 3.x migration guide

[CAMEL-14244](https://issues.apache.org/jira/browse/CAMEL-14244)

camel-opentracing - Associate decorators with component FQN also

[CAMEL-14239](https://issues.apache.org/jira/browse/CAMEL-14239)

XSD schema for Camel 3 release for OSGi blueprint put online

[CAMEL-14232](https://issues.apache.org/jira/browse/CAMEL-14232)

camel-ftp: the sftp serverAliveInterval option documentation is not clear

[CAMEL-14226](https://issues.apache.org/jira/browse/CAMEL-14226)

Move spring-boot support into a different repository

[CAMEL-14188](https://issues.apache.org/jira/browse/CAMEL-14188)

Upgrade debezium to 1.0 Final

### Test (5)

[CAMEL-14566](https://issues.apache.org/jira/browse/CAMEL-14566)

camel-mongodb - Use testcontainers for testing

[CAMEL-14562](https://issues.apache.org/jira/browse/CAMEL-14562)

camel-elastichsearch - Use testcontainers for testing

[CAMEL-14547](https://issues.apache.org/jira/browse/CAMEL-14547)

camel-itest-karaf - JDK8 tests fails

[CAMEL-14304](https://issues.apache.org/jira/browse/CAMEL-14304)

Unit Test for STOMP Consumer Header Filter Strategy

[CAMEL-14260](https://issues.apache.org/jira/browse/CAMEL-14260)

camel-rabbitmq - Use testcontainers to test with docker

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).