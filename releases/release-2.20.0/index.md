# Apache camel 2.20.0 Release

## New and Noteworthy

Welcome to the 2.20.0 release which resolved over 550 issues including new features, improvements and bug fixes.

-   Support for Java 9 as a technical preview. Official support for Java 9 will be forthcoming in the following releases. (source code builds and tests on a Java 9 JVM). 
-   Many internal optimisations in the Camel routing engine, such as reducing thread contention when updating JMX statistics, reducing internal state objects to claim less memory, and reducing the number of allocated objects to reduce overhead on GC etc, and much more. 
-   Camel Spring Boot now supports referring to bean’s (lookup in Spring Boot) by their id names in the configuration files (application.properties|yaml file) when you configure any of the Camel starter components.
-   Camel Spring Boot now also supports using Spring (auto) configuration to configure CamelContext when using Spring XML files with `<camelContext>`. 
-   Worked to make Apache Camel more ready and compatible with the upcoming Spring Boot 2 and Spring Framework 5. Officially support for these is expected in Camel 2.21 release.
-   The JMS component now includes JMS 2.0 functionality to use shared (durable and non-durable) topic.
-   The Camel Maven Plugin can now validate for duplicate route ids in your source code.
-   Splitted Twitter component into 4, now directmessage, seach, streaming and timeline has its own endpoint and scheme. See documentation for more details
-   Introduced `HeadersMapFactory` SPI which allows to plugin different implementations, or to use case sensitive maps that are faster than the default.
-   Allow Kafka consumer to break on first unhandled exception, sync the offset from last known good, and then re-connect after one timeout cycle, to restart consuming again. This avoids loosing the failed message, but retry it again on either this consumer, or another consume which was re-balanced by Kafka. This requires to be turned on with the new option breakOnFirstError which can be set on both component or endpoint level.
-   Starting and stoping the CamelContext when used with Spring framework (SpringCamelContext) was revised to ensure that the Camel context is started last - when all resources should be available, and stopped first

-   while all resources are still available

-   The SQL Stored Procedure now supports specifying custom types as FQN classnames and scale in numeric values.
-   Using Camel with Spring now supports calling Bean by their FQN name and let Spring instantiate the bean using auto-wired constructor’s as opposed to only supporting a no-arg constructor. 
-   Using Camel with Spring Boot can now easily filter Java RouteBuilder routes via ANT-path pattern style to either include or exclude class names, which can be configured using Spring configuration properties.
-   The Wire Tap EIP can now be configured to use static endpoint uri instead of being dynamic evaluated via the Simple language. 
-   The Wire Tap EIP will now complete any inflight wire tapped exchanges while shutting down to give them time to complete graceful.
-   The JSonPath can now split and write each row as a string value (JSon format) instead of using a Map/POJO type with the new writeAsString option.
-   The POJO Consuming Consume annotation on POJO classes now support a predicate (using simple language) to filter the message. See the camel-example-spring-boot-pojo for more.
-   The internal JSon parser that is used by camel-catalog and runtime camel-catalog (from camel-core) now embeds a simple-json v2 parser which means it can parse any kind of json formatted document (before it was confined to its own dense format)
-   Infinispan, Ehcache and Hazelcast caches can automatically discover cache managers in spring-boot
-   Introduced an experimental _Health Checks SPI_ that can be leveraged in in cloud environments to detect non healthy contexts.
-   Introduced an experimental _Cluster SPI_ for high availability contexts, out of the box Camel supports: atomix, consul, file, kubernetes and zookeeper as underlying clustering technologies through the respective components.
-   Introduced an experimental _Route Controller SPI_ which is aimed to provide more fine-grained control of routes, out of the box Camel provides the following implementations:
-   _SupervisingRouteController_ which delays startup of the routes after the camel context is properly started and attempt to restart routes that have not been starter successfully
-   _ClusteredRouteController_ which leverages _Cluster SPI_ to start routes only when the context is elected as leader

Fixed these issues

-   Fixed a infinitive recursion in Camel’s link:error-handler.html\[Error Handler\] when an onException was routing to another route using direct endpoint and this route would throw a new exception that would circle back to the same onException or at a later point, which will cause an endless recursion.
-   Fixed a potential issue with masking password from URI using RAW(xxx) would reveal part of the password if the password contains a & character.
-   The Restlet component is now internally using curly brackets for its uri patterns instead of regular parentheses so it works similar to the other REST component and as Restlet framework itself does
-   Fixed Hystrix EIP having wrong default for circuitBreakerForceClose when using camel-hystrix-starter with Spring Boot. The default should be false and not true
-   Fixed Hystrix EIP when failing and running fallback not signaling to Hystrix itself so it can keep state of the failure and react accordingly to run in half-open mode as well.
-   Fixed MDC logging loosing route id after calling a direct route from within a transacted route
-   Fixed a regression with Bean component and Simple language OGNL expressions causing ambiguous method call exception when calling method implemented by super class when method is defined by interface and abstract class
-   Fixed Rest DSL (server side) not returning response on all valid uri paths when clients call using a HTTP OPTIONS request
-   Fixed Rest producer not using HTTP method (verb such as PUT) from the endpoint uri when calling a remote REST service
-   Fixed Timer routes to shutdown more graceful and allow pending tasks to complete while they are in-flight.
-   Fixed configuring Rest DSL via application.properties|yaml in Spring Boot not working. 
-   Fixed Simple Language to add support negative numbers(without single or double quotes) in predicates
-   Fixed configuring Rest DSL in Spring Boot application.properties / yaml for properties to data format, component, api, cors etc to use a map structure and make it work.
-   Fixed configuring Rest DSL using property placeholders in the path parameters such as the defaultValue.
-   Fixed an issue with parallel processing (in non-streaming mode) in some EIPs may cause CPU burning cycles while waiting for pending tasks to complete or timeout.
-   Fixed an issue with copying streams could block forever due IBM application server would mistakenly return 0 instead of -1 to indicate EOL for an empty stream. 
-   Fixed an issue with making JMS and SJMS components work with ActiveMQ Artemis that would otherwise causes a ClassCastException
-   Fixed RabbitMQ component to better recover connection if exchange/queue has been deleted manually on the broker.
-   Fixed Websocket component wasn’t working with returning static content

Important changes to consider when upgrading

-   Maven 3.3.3 or newer is required to build the project
-   camel-dropbox - upgraded to v2 api as v1 is EOL and no longer possible to use with dropbox. The v2 upgrade was not straightforward so there can be backward compatible issues, which is out of our hands.
-   camel-infinispan - the result is not more set in the CamelInfinispanOperationResult header but in the in body. To change this behavior you can set the header CamelInfinispanOperationResultHeader with the name of the header that should contains the result or with the resultHeader uri option
-   camel-infinispan - the uri option _command_ has been deprecated and replaced by _operation_ for consistency
-   camel-infinispan - the commands are now int the short form PUT, GET etc. old operation names like CamelInfinispanOperationPut, CamelInfinispanOperationGet etc have been deprecated.
-   camel-undertow - matchOnUriPrefix option is defaulted to be FALSE in order to make it consistent with other components like Camel HTTP components.
-   Splitted Twitter component into 4, now directmessage, seach, streaming and timeline has its own endpoint and scheme.
-   RuntimeEndpointRegistry is no longer in extended mode by default. To use that you need to set management statistics level to Extended explicit.
-   There is no RuntimeEndpointRegistry in use by default. You need to explicit configure a registry to be used, or turn it on via management agent, or set the statics level to extended mode.
-   Camel with Spring XML routes will no longer register endpoints in the Spring registry from Camel routes where `<from>` or `<to>` have endpoints assigned with an explicit id attribute. The option registerEndpointIdsFromRoute can be set to true on `<camelContext>` to be backwards compatible. However this registration is deprecated, instead you should use `<endpoint>` to register Camel endpoints with id’s in Spring registry.
-   camel-spring-dm has been removed as it was not working properly anyway and was deprecated some releases ago. For XML DSL with OSGi use camel-blueprint instead.
-   Copying streams in IOHelper from came-core now regard EOL of data if the first read byte is zero to work around issues on some application servers like IBM WebSphere. This can be turned off by setting JVM system property “camel.zeroByteEOLEnabled=false”.
-   The camel-jms component now dependes by default on the JMS 2.0 API (geronimo-jms\_2.0\_spec) instead of JMS 1.1 API (geronimo-jms\_1.1\_spec). However camel-jms works at runtime with both JMS 1.1 or 2.0 specs so include the JMS spec JARs of your choice.
-   camel-kura upgraded to newer OSGi API version
-   camel-stomp uses the destination as-is, where as before it would replace all slash characters with colon. But according to the STOMP spec the destination should be used as-is, and is broker specific.
-   camel-ignite is updated from using Ignite version 1.9.x to 2.2.x

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
      <version>2.20.0</version>
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
      <version>2.20.0</version>
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
| [apache-camel-2.20.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.20.0/apache-camel-2.20.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.20.0/apache-camel-2.20.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.20.0/apache-camel-2.20.0-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.20.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.20.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (167)

[CAMEL-11884](https://issues.apache.org/jira/browse/CAMEL-11884)

NPE when stopping Salesforce component that failed to start

[CAMEL-11882](https://issues.apache.org/jira/browse/CAMEL-11882)

ServiceDefinition.metadata not passed to RibbonServiceLoadBalancer

[CAMEL-11881](https://issues.apache.org/jira/browse/CAMEL-11881)

Queue/Exchange parameters need to be numeric when declaring in RabbitMQ

[CAMEL-11871](https://issues.apache.org/jira/browse/CAMEL-11871)

Stomp component should not modify the destination name

[CAMEL-11867](https://issues.apache.org/jira/browse/CAMEL-11867)

camel-bom needs <distributionManagement/>

[CAMEL-11866](https://issues.apache.org/jira/browse/CAMEL-11866)

Simple Expression Language bean doesn't throw exception when bean not found

[CAMEL-11848](https://issues.apache.org/jira/browse/CAMEL-11848)

Using MongoDB Tailable Cursor Consumer on non-capped collection results in NullPointerException (instead of proper error message)

[CAMEL-11844](https://issues.apache.org/jira/browse/CAMEL-11844)

camel-azure - Should work with Camel file component OOTB

[CAMEL-11843](https://issues.apache.org/jira/browse/CAMEL-11843)

Unable to configure some URI options on DockerEndpoint

[CAMEL-11842](https://issues.apache.org/jira/browse/CAMEL-11842)

ClassNotFoundException when configuring camel-docker SSL options

[CAMEL-11838](https://issues.apache.org/jira/browse/CAMEL-11838)

camel-websocket - Static resource returns empty body

[CAMEL-11814](https://issues.apache.org/jira/browse/CAMEL-11814)

camel-spring-boot - Recent change in startup behaviour can cause camel-test-spring problems

[CAMEL-11813](https://issues.apache.org/jira/browse/CAMEL-11813)

Wrong check in ConnectorCatalogNexusRepository

[CAMEL-11811](https://issues.apache.org/jira/browse/CAMEL-11811)

Camel FTP fails to create intermediate directory

[CAMEL-11798](https://issues.apache.org/jira/browse/CAMEL-11798)

Connector API assumes flat classpath

[CAMEL-11797](https://issues.apache.org/jira/browse/CAMEL-11797)

CamelMessageHistoryOutputFormat global option ignored for message history

[CAMEL-11793](https://issues.apache.org/jira/browse/CAMEL-11793)

Camel-box component occasionally hangs

[CAMEL-11791](https://issues.apache.org/jira/browse/CAMEL-11791)

RabbitMQ Producer/Consumer does not recover if exchange/queue is deleted manually

[CAMEL-11785](https://issues.apache.org/jira/browse/CAMEL-11785)

CompositeApiClient cannot handle null ResponseStream

[CAMEL-11779](https://issues.apache.org/jira/browse/CAMEL-11779)

camel-facebook should not transitively depend on spi-annotations

[CAMEL-11772](https://issues.apache.org/jira/browse/CAMEL-11772)

Sjms with Artemis causes NullPointerException due to a ClassCastException

[CAMEL-11769](https://issues.apache.org/jira/browse/CAMEL-11769)

camel-hazelcast-starter : hazelcast customizer have been deleted

[CAMEL-11768](https://issues.apache.org/jira/browse/CAMEL-11768)

camel-itest-karaf - CamelDockerTest fails

[CAMEL-11765](https://issues.apache.org/jira/browse/CAMEL-11765)

camel-undertow - Consumer adds duplicate headers

[CAMEL-11760](https://issues.apache.org/jira/browse/CAMEL-11760)

camel-itest-karaf - CamelServicenowTest fails

[CAMEL-11759](https://issues.apache.org/jira/browse/CAMEL-11759)

camel-itest-karaf - CamelNagiosTest fails

[CAMEL-11750](https://issues.apache.org/jira/browse/CAMEL-11750)

Camel route with multicast (parallel) generate huge CPU load

[CAMEL-11748](https://issues.apache.org/jira/browse/CAMEL-11748)

Camel-Undertow: transferException option doesn't work

[CAMEL-11742](https://issues.apache.org/jira/browse/CAMEL-11742)

File consumer - Delete orphan lock files on startup may not match a lock file when using include/antInclude filtering

[CAMEL-11735](https://issues.apache.org/jira/browse/CAMEL-11735)

Camel-Chunk Karaf feature doesn't work

[CAMEL-11733](https://issues.apache.org/jira/browse/CAMEL-11733)

camel-google-bigquery : Incorrectly set partition name

[CAMEL-11725](https://issues.apache.org/jira/browse/CAMEL-11725)

Atmosphere framework has changed initialisation API

[CAMEL-11724](https://issues.apache.org/jira/browse/CAMEL-11724)

Camel-Hdfs2: No need for initialDelay and delay as configuration properties since they are already parameters of ScheduledPollConsumer

[CAMEL-11723](https://issues.apache.org/jira/browse/CAMEL-11723)

ManagedCamelContext.dumpRestsAsXml can fail if default charset is not utf-8

[CAMEL-11716](https://issues.apache.org/jira/browse/CAMEL-11716)

error in handling return parameters in db functions

[CAMEL-11715](https://issues.apache.org/jira/browse/CAMEL-11715)

Camel Spring : unable to mix xml and java routes

[CAMEL-11711](https://issues.apache.org/jira/browse/CAMEL-11711)

Camel-example-spring-cloud-servicecall doesn't work out of the box

[CAMEL-11709](https://issues.apache.org/jira/browse/CAMEL-11709)

Camel-Milo component cannot write to newer server versions

[CAMEL-11705](https://issues.apache.org/jira/browse/CAMEL-11705)

Camel-Caffeine: ExpireAfterAccess set two times instead of ExpireAfterWrite

[CAMEL-11698](https://issues.apache.org/jira/browse/CAMEL-11698)

S3 Consumer does not close S3 Object Input Streams and this causes HTTP connection leaks

[CAMEL-11697](https://issues.apache.org/jira/browse/CAMEL-11697)

S3 Consumer: If maxMessagesPerPoll is greater than 50 consumer fails to poll objects from bucket

[CAMEL-11690](https://issues.apache.org/jira/browse/CAMEL-11690)

Done() called two times in RoutingSlip processor

[CAMEL-11688](https://issues.apache.org/jira/browse/CAMEL-11688)

ensure transport endpoint configuration will be take into account when create JettyRestHttpBinding from REST DSL

[CAMEL-11681](https://issues.apache.org/jira/browse/CAMEL-11681)

camel-cxf - getting TypeConversionException when schema-validation-enabled=true for unwrapped response

[CAMEL-11674](https://issues.apache.org/jira/browse/CAMEL-11674)

Couchbase client is never shut down

[CAMEL-11672](https://issues.apache.org/jira/browse/CAMEL-11672)

Input stream infinitive loop

[CAMEL-11671](https://issues.apache.org/jira/browse/CAMEL-11671)

camel-ahc - No way to disable url encoding

[CAMEL-11668](https://issues.apache.org/jira/browse/CAMEL-11668)

CompositeApiClient class in the camel-salesforces component cannot close a null InputStream

[CAMEL-11666](https://issues.apache.org/jira/browse/CAMEL-11666)

Camel Hazelcast Queue Cosumer implementation

[CAMEL-11662](https://issues.apache.org/jira/browse/CAMEL-11662)

camel-ahc does not support multi-value HTTP headers properly

[CAMEL-11657](https://issues.apache.org/jira/browse/CAMEL-11657)

Camel-spring-security: The Karaf feature need spring-security-config to be installed

[CAMEL-11652](https://issues.apache.org/jira/browse/CAMEL-11652)

Upgrade dozer to 6.1

[CAMEL-11649](https://issues.apache.org/jira/browse/CAMEL-11649)

Cookie Handling only works for one cookie

[CAMEL-11648](https://issues.apache.org/jira/browse/CAMEL-11648)

camel-mongodb-gridfs - Created document cannot be read by the new MongoDB GridFS API

[CAMEL-11643](https://issues.apache.org/jira/browse/CAMEL-11643)

Extensions: registerExtension method has to avoid final in his declaration to work in CDI

[CAMEL-11636](https://issues.apache.org/jira/browse/CAMEL-11636)

property placeholder is not replaced in REST DSL in blueprint context

[CAMEL-11632](https://issues.apache.org/jira/browse/CAMEL-11632)

QuartzScheduledPollConsumerScheduler causes trigger misfires on each application start

[CAMEL-11631](https://issues.apache.org/jira/browse/CAMEL-11631)

Camel-Paho Missiong reconnect logic

[CAMEL-11630](https://issues.apache.org/jira/browse/CAMEL-11630)

JPAMessageIdRepository Not Releasing Connections

[CAMEL-11627](https://issues.apache.org/jira/browse/CAMEL-11627)

Camel-Undertow doesn't work in OSGi

[CAMEL-11626](https://issues.apache.org/jira/browse/CAMEL-11626)

ServiceNowException is printing "%d" (not replacing value)

[CAMEL-11624](https://issues.apache.org/jira/browse/CAMEL-11624)

REST DSL/component method Uppercase

[CAMEL-11623](https://issues.apache.org/jira/browse/CAMEL-11623)

LevelDB Java implementation wont be tried on Errors

[CAMEL-11620](https://issues.apache.org/jira/browse/CAMEL-11620)

Requiredement for date string to be longer than pattern is invalid.

[CAMEL-11615](https://issues.apache.org/jira/browse/CAMEL-11615)

WorkerPool is null in DefaultCamelReactiveStreamsService

[CAMEL-11610](https://issues.apache.org/jira/browse/CAMEL-11610)

UnsatisfiedDependencyException: Error creating bean with name 'openTracingEventNotifier'

[CAMEL-11609](https://issues.apache.org/jira/browse/CAMEL-11609)

camel-univocity-parsers: marshaller not thread safe

[CAMEL-11608](https://issues.apache.org/jira/browse/CAMEL-11608)

Camel-AWS: Camel-Kinesis needs Jackson Dataformat CBOR to work in OSGi

[CAMEL-11607](https://issues.apache.org/jira/browse/CAMEL-11607)

NPE in MBeanInfoAssembler when debug is enabled

[CAMEL-11605](https://issues.apache.org/jira/browse/CAMEL-11605)

Invalid accept header

[CAMEL-11593](https://issues.apache.org/jira/browse/CAMEL-11593)

Global rest configuration gets overridden by default

[CAMEL-11591](https://issues.apache.org/jira/browse/CAMEL-11591)

ClassNotFound: javax.servlet.ServletOutputStream in opentracing example client

[CAMEL-11589](https://issues.apache.org/jira/browse/CAMEL-11589)

MockEndpoint.expectedPropertyReceived needs improvement

[CAMEL-11588](https://issues.apache.org/jira/browse/CAMEL-11588)

SupervisingRouteController - Routes may be started in wrong order

[CAMEL-11576](https://issues.apache.org/jira/browse/CAMEL-11576)

camel-catalog is not generating camel-stream URI properly

[CAMEL-11575](https://issues.apache.org/jira/browse/CAMEL-11575)

Component name mismatch: https4 or http4s

[CAMEL-11572](https://issues.apache.org/jira/browse/CAMEL-11572)

camel-lumberjack component doesn't restart

[CAMEL-11564](https://issues.apache.org/jira/browse/CAMEL-11564)

avoid ClassCastException when the gzip is enabled for the cxf endpoint with camel destination

[CAMEL-11559](https://issues.apache.org/jira/browse/CAMEL-11559)

NPE when not setting a sampling interval on client subscriptions

[CAMEL-11549](https://issues.apache.org/jira/browse/CAMEL-11549)

Cant run camel zipkin example with latest zipkin-server

[CAMEL-11548](https://issues.apache.org/jira/browse/CAMEL-11548)

camel-undertow consumer shall use InOut ExchangePattern

[CAMEL-11540](https://issues.apache.org/jira/browse/CAMEL-11540)

Unable to disable ProducerCache by setting cacheSize="-1"

[CAMEL-11537](https://issues.apache.org/jira/browse/CAMEL-11537)

undertown consumer : consumer silently fails to start if manually started after a failure

[CAMEL-11533](https://issues.apache.org/jira/browse/CAMEL-11533)

Simple language - comparison againist negative value fails with unknown token

[CAMEL-11529](https://issues.apache.org/jira/browse/CAMEL-11529)

Wrong syntax definitions in camel catalog

[CAMEL-11524](https://issues.apache.org/jira/browse/CAMEL-11524)

Camel File Consumer fails when doneFileName contains '$'

[CAMEL-11523](https://issues.apache.org/jira/browse/CAMEL-11523)

JasyptPropertiesParser fails on properties references with default value

[CAMEL-11520](https://issues.apache.org/jira/browse/CAMEL-11520)

camel-hipchat: Unable to send to room name containing spaces

[CAMEL-11518](https://issues.apache.org/jira/browse/CAMEL-11518)

Add an Mvc Actuator endpoint for exposing Camel routes

[CAMEL-11511](https://issues.apache.org/jira/browse/CAMEL-11511)

Camel bean binding issues

[CAMEL-11510](https://issues.apache.org/jira/browse/CAMEL-11510)

The consumer endpoint for Twitter component timeline/user doesn't poll the tweets even if the type is set to polling and delay attribute doesn't work

[CAMEL-11509](https://issues.apache.org/jira/browse/CAMEL-11509)

Cannot set content type with parameters without specifying charset

[CAMEL-11489](https://issues.apache.org/jira/browse/CAMEL-11489)

Declaring AWS endpoint with accessKey and secretKey, and without amazonS3Client should be possible.

[CAMEL-11486](https://issues.apache.org/jira/browse/CAMEL-11486)

NullPointerException for invalid payload with session handling enabled

[CAMEL-11482](https://issues.apache.org/jira/browse/CAMEL-11482)

SSLContextParameters settings are not properly copied to SslContextFactory

[CAMEL-11480](https://issues.apache.org/jira/browse/CAMEL-11480)

camel-rabbitmq - autorecovery creates additional channels

[CAMEL-11477](https://issues.apache.org/jira/browse/CAMEL-11477)

Can not override isUseAdviceWith in CamelBlueprintTestSupport

[CAMEL-11476](https://issues.apache.org/jira/browse/CAMEL-11476)

spring-boot - routes not loaded when setting a management.port

[CAMEL-11471](https://issues.apache.org/jira/browse/CAMEL-11471)

Unable to update the cron details from Quartz scheduler MBean

[CAMEL-11470](https://issues.apache.org/jira/browse/CAMEL-11470)

Camel-Core: DefaultShutdownStrategy, pass the logInflightExchangesOnTimeout to the ShutdownTask

[CAMEL-11469](https://issues.apache.org/jira/browse/CAMEL-11469)

Camel-Hipchat - Configure via xml is broken

[CAMEL-11467](https://issues.apache.org/jira/browse/CAMEL-11467)

Camel-bindy tests fail depending on the locale

[CAMEL-11465](https://issues.apache.org/jira/browse/CAMEL-11465)

NPE caused by IrcMessage

[CAMEL-11462](https://issues.apache.org/jira/browse/CAMEL-11462)

Nashorn javascript library can not be found in OSGi

[CAMEL-11460](https://issues.apache.org/jira/browse/CAMEL-11460)

Camel-Infinispan: If a Default Configuration is not provided then a DefaultCacheName must be provided

[CAMEL-11457](https://issues.apache.org/jira/browse/CAMEL-11457)

camel-atomix - No new leader when all nodes are killed forcefully

[CAMEL-11455](https://issues.apache.org/jira/browse/CAMEL-11455)

Automatic transform String to DBObject after previous conversion error

[CAMEL-11454](https://issues.apache.org/jira/browse/CAMEL-11454)

camel-zipfile dataformat cannot remove successfully processed files

[CAMEL-11453](https://issues.apache.org/jira/browse/CAMEL-11453)

Fix camel-box feature

[CAMEL-11441](https://issues.apache.org/jira/browse/CAMEL-11441)

Main - setPropertyPlaceholderLocations should be public

[CAMEL-11437](https://issues.apache.org/jira/browse/CAMEL-11437)

Bug using file endpoint probeContentType and preMove attributes together causes Exchange.FILE\_CONTENT\_TYPE to get dropped. (2.19.0)

[CAMEL-11433](https://issues.apache.org/jira/browse/CAMEL-11433)

Unable to use camel-box in OSGI environment

[CAMEL-11429](https://issues.apache.org/jira/browse/CAMEL-11429)

camel-box is not assigning default configuration values

[CAMEL-11427](https://issues.apache.org/jira/browse/CAMEL-11427)

camel-leveldb does not work on Solaris -- no native code library and no Java fallback

[CAMEL-11424](https://issues.apache.org/jira/browse/CAMEL-11424)

Endless wait when unhandled exception occurs in camel-olingo

[CAMEL-11423](https://issues.apache.org/jira/browse/CAMEL-11423)

Accept header is not compliant with IETF RFC-7231

[CAMEL-11419](https://issues.apache.org/jira/browse/CAMEL-11419)

Camel IgniteComponent fails to create cache with underscore e.g cache\_name

[CAMEL-11414](https://issues.apache.org/jira/browse/CAMEL-11414)

camel-restlet - Rest DSL issue with empty path variables

[CAMEL-11413](https://issues.apache.org/jira/browse/CAMEL-11413)

camel-olingo - Potential NPE in getting content-type header

[CAMEL-11407](https://issues.apache.org/jira/browse/CAMEL-11407)

camel-opentracing loggingtracer needs to build before client

[CAMEL-11402](https://issues.apache.org/jira/browse/CAMEL-11402)

Logic error in authentication type determination

[CAMEL-11394](https://issues.apache.org/jira/browse/CAMEL-11394)

Undertow endpoint option REUSE\_ADDRESS is configured using the value for TCP\_NO\_DELAY

[CAMEL-11392](https://issues.apache.org/jira/browse/CAMEL-11392)

String to ByteBuffer conversion causes overflow due to multibyte chars

[CAMEL-11390](https://issues.apache.org/jira/browse/CAMEL-11390)

camel maven plugin (2.19.0) downloading catalog when configuration disabled it

[CAMEL-11388](https://issues.apache.org/jira/browse/CAMEL-11388)

camel-infinispan - InfinispanRoutePolicy issue with locking from remote server

[CAMEL-11386](https://issues.apache.org/jira/browse/CAMEL-11386)

Potential NullPointerException if HTTP client not started and stop was performed

[CAMEL-11385](https://issues.apache.org/jira/browse/CAMEL-11385)

Camel-metrics Karaf feature can't be installed

[CAMEL-11382](https://issues.apache.org/jira/browse/CAMEL-11382)

Creating IgniteComponent from Ignite Instance throws IllegalStateException

[CAMEL-11369](https://issues.apache.org/jira/browse/CAMEL-11369)

camel-spring-boot-starter generator paste incorrect default value

[CAMEL-11352](https://issues.apache.org/jira/browse/CAMEL-11352)

duplicated/missing logs when camel-paxlogging work with pax-logging-log4j2

[CAMEL-11322](https://issues.apache.org/jira/browse/CAMEL-11322)

Swagger Rest DSL Generator needs to build before its maven plugin

[CAMEL-11317](https://issues.apache.org/jira/browse/CAMEL-11317)

\[OSGi, camel-jpa\] Problems with mapping idempotent.jpa.MessageProcessed with Aries + Hibernate

[CAMEL-11305](https://issues.apache.org/jira/browse/CAMEL-11305)

camel-test - Using dump route coverage with custom processor may cause NPE

[CAMEL-11299](https://issues.apache.org/jira/browse/CAMEL-11299)

Camel Rest DSL Does Not Creating OPTIONS routes for defined routes

[CAMEL-11298](https://issues.apache.org/jira/browse/CAMEL-11298)

Using chmodDirectory with full paths makes file producer to created directories relative to source

[CAMEL-11293](https://issues.apache.org/jira/browse/CAMEL-11293)

Rest DSL Producer HTTP ignores http verb from uri

[CAMEL-11290](https://issues.apache.org/jira/browse/CAMEL-11290)

Camel-Infinispan: Continuous Query, add support for recordUpdated event

[CAMEL-11288](https://issues.apache.org/jira/browse/CAMEL-11288)

camel-grpc producer incorrectly called async services

[CAMEL-11287](https://issues.apache.org/jira/browse/CAMEL-11287)

MDC routeId value is lost after calling a direct route from a transacted route

[CAMEL-11283](https://issues.apache.org/jira/browse/CAMEL-11283)

camel-hystrix-starter - The circuitBreakerForceClose option is default true which should be false

[CAMEL-11281](https://issues.apache.org/jira/browse/CAMEL-11281)

camel-spring is not usable in an osgi-context

[CAMEL-11280](https://issues.apache.org/jira/browse/CAMEL-11280)

camel-twitter : hard-coded component scheme

[CAMEL-11279](https://issues.apache.org/jira/browse/CAMEL-11279)

Camel hystrix does not handle exceptions properly

[CAMEL-11273](https://issues.apache.org/jira/browse/CAMEL-11273)

ReloadStrategySupport does take changed routeContext files into account

[CAMEL-11272](https://issues.apache.org/jira/browse/CAMEL-11272)

ReloadStrategySupport wrongly logs "Routes with no id's detected"

[CAMEL-11269](https://issues.apache.org/jira/browse/CAMEL-11269)

URISupport sanitizeUri partial support for RAW()

[CAMEL-11266](https://issues.apache.org/jira/browse/CAMEL-11266)

The ehcache component creates a separate CacheManager per producer route

[CAMEL-11264](https://issues.apache.org/jira/browse/CAMEL-11264)

Potential NPE in DefaultUndertowHttpBinding

[CAMEL-11255](https://issues.apache.org/jira/browse/CAMEL-11255)

Error handler may be called twice if routing from onException to direct with global scoped error handler

[CAMEL-11240](https://issues.apache.org/jira/browse/CAMEL-11240)

Simple Language: MethodNotFoundException when calling interface method implemented by super class

[CAMEL-11235](https://issues.apache.org/jira/browse/CAMEL-11235)

Simple Language: AmbiguousMethodCallException when calling method implemented by super class when method is defined by interface and abstract class

[CAMEL-11234](https://issues.apache.org/jira/browse/CAMEL-11234)

NullPointerException while trying to get the Route Status on startup

[CAMEL-11232](https://issues.apache.org/jira/browse/CAMEL-11232)

Fix camel-example-spring-boot-rest-jpa example

[CAMEL-11229](https://issues.apache.org/jira/browse/CAMEL-11229)

Infinite recursion if exception happens inside exception handler

[CAMEL-11227](https://issues.apache.org/jira/browse/CAMEL-11227)

Simple expression colon in sql-stored component

[CAMEL-11225](https://issues.apache.org/jira/browse/CAMEL-11225)

Deadlock in component creation

[CAMEL-11221](https://issues.apache.org/jira/browse/CAMEL-11221)

camel-netty4-http cannot have a URL larger than 409 bytes by default, rather than the assumed 4096 byte limit

[CAMEL-11215](https://issues.apache.org/jira/browse/CAMEL-11215)

Camel Kafka component commits offsets in case of exceptions

[CAMEL-11202](https://issues.apache.org/jira/browse/CAMEL-11202)

Salesforce verifier should not throw exceptions

[CAMEL-11198](https://issues.apache.org/jira/browse/CAMEL-11198)

OpenTracing trace context should cope with Hystrix using separate thread

[CAMEL-11137](https://issues.apache.org/jira/browse/CAMEL-11137)

@UriParam should support real enums

[CAMEL-10728](https://issues.apache.org/jira/browse/CAMEL-10728)

Camel MongoDB Multiple Insert issue

[CAMEL-10225](https://issues.apache.org/jira/browse/CAMEL-10225)

Camel-Saxon is not thread safe

[CAMEL-9935](https://issues.apache.org/jira/browse/CAMEL-9935)

Rest DSL passes blank query parameters as null

[CAMEL-8419](https://issues.apache.org/jira/browse/CAMEL-8419)

Camel StreamCache does not work with CXF consumer for InOut messages

[CAMEL-8010](https://issues.apache.org/jira/browse/CAMEL-8010)

Race condition in AggregatorProcessor recovery sometimes causes duplicates (still)

[CAMEL-5356](https://issues.apache.org/jira/browse/CAMEL-5356)

CXF endpoint doesn't play nice with doTry/doCatch

### Improvement (221)

[CAMEL-11880](https://issues.apache.org/jira/browse/CAMEL-11880)

Use full version of BoxGroup.createGroup in camel-box

[CAMEL-11875](https://issues.apache.org/jira/browse/CAMEL-11875)

Add support for BoxGroup.updateInfo in camel-box

[CAMEL-11873](https://issues.apache.org/jira/browse/CAMEL-11873)

Exclude validation-api from Salesforce component

[CAMEL-11872](https://issues.apache.org/jira/browse/CAMEL-11872)

Handle MIME folded and MIME encoded email headers

[CAMEL-11862](https://issues.apache.org/jira/browse/CAMEL-11862)

Convert to requested type values retrieved from the repository

[CAMEL-11847](https://issues.apache.org/jira/browse/CAMEL-11847)

cluster-service : support multiple cluster services

[CAMEL-11841](https://issues.apache.org/jira/browse/CAMEL-11841)

cluster service : make a simple FileLock based service

[CAMEL-11837](https://issues.apache.org/jira/browse/CAMEL-11837)

cluster-service : camel-kubernetes spring boot support

[CAMEL-11835](https://issues.apache.org/jira/browse/CAMEL-11835)

cluster service : make a JGroups based cluster service

[CAMEL-11820](https://issues.apache.org/jira/browse/CAMEL-11820)

Upgrade optaplanner

[CAMEL-11819](https://issues.apache.org/jira/browse/CAMEL-11819)

camel-velocity - Upgrade to 2.x

[CAMEL-11816](https://issues.apache.org/jira/browse/CAMEL-11816)

cluster-service : camel-consul spring boot support

[CAMEL-11815](https://issues.apache.org/jira/browse/CAMEL-11815)

cluster-service : camel-zookeeper spring boot support

[CAMEL-11801](https://issues.apache.org/jira/browse/CAMEL-11801)

cluster service : use reference count to join/leave a cluster

[CAMEL-11800](https://issues.apache.org/jira/browse/CAMEL-11800)

cluster service : there should be an option to leave a cluster view

[CAMEL-11796](https://issues.apache.org/jira/browse/CAMEL-11796)

Add headerName option to jsonpath expression

[CAMEL-11789](https://issues.apache.org/jira/browse/CAMEL-11789)

camel-iec60870 : create karaf feature

[CAMEL-11788](https://issues.apache.org/jira/browse/CAMEL-11788)

Chunk may not find templates in modular class loading environments

[CAMEL-11781](https://issues.apache.org/jira/browse/CAMEL-11781)

Support BoxUser.moveFolderToUser in camel-box

[CAMEL-11777](https://issues.apache.org/jira/browse/CAMEL-11777)

Transactional hazelcast:seda component uses not transaction aware queue

[CAMEL-11764](https://issues.apache.org/jira/browse/CAMEL-11764)

connector maven plugin : generated connectors should have a schema that does not clash wit components

[CAMEL-11761](https://issues.apache.org/jira/browse/CAMEL-11761)

Camel-Caffeine: Add support for StatsCounter in the component

[CAMEL-11755](https://issues.apache.org/jira/browse/CAMEL-11755)

toD should ignore when dynamic uri is empty

[CAMEL-11754](https://issues.apache.org/jira/browse/CAMEL-11754)

Apache Camel FTP getting Cannot retrieve file: RemoteFile error

[CAMEL-11752](https://issues.apache.org/jira/browse/CAMEL-11752)

camel-spring-boot : improve handling classic spring xml with spring-boot

[CAMEL-11744](https://issues.apache.org/jira/browse/CAMEL-11744)

Allow update of OwnerId field

[CAMEL-11743](https://issues.apache.org/jira/browse/CAMEL-11743)

camel-ldap - Make it possible to use ENV when configuring DirContext

[CAMEL-11739](https://issues.apache.org/jira/browse/CAMEL-11739)

camel-jms - Allow to configure a list of header names to preserve despite being invalid JMS spec type

[CAMEL-11738](https://issues.apache.org/jira/browse/CAMEL-11738)

camel-jsch - Allow to load key file from classpath

[CAMEL-11732](https://issues.apache.org/jira/browse/CAMEL-11732)

Add or update READMEs to itests

[CAMEL-11730](https://issues.apache.org/jira/browse/CAMEL-11730)

camel-connector-maven-plugin : it should be possible to configure connector only properties

[CAMEL-11729](https://issues.apache.org/jira/browse/CAMEL-11729)

camel-connector-maven-plugin : generated spring boot starters should support customizers

[CAMEL-11728](https://issues.apache.org/jira/browse/CAMEL-11728)

Camel-AWS S3: Avoid warn log message about content length

[CAMEL-11726](https://issues.apache.org/jira/browse/CAMEL-11726)

Elsql producer inconsistent behavior compare to sql component producer

[CAMEL-11721](https://issues.apache.org/jira/browse/CAMEL-11721)

Camel Kafka component JSON metadata is invalid

[CAMEL-11720](https://issues.apache.org/jira/browse/CAMEL-11720)

GoogleDriveProducer should be able to honor the http.proxyPort and http.proxyHost properties from the CamelContext

[CAMEL-11719](https://issues.apache.org/jira/browse/CAMEL-11719)

add a string to ChildReference converter for camel-google-drive

[CAMEL-11718](https://issues.apache.org/jira/browse/CAMEL-11718)

Setting camel.dataformat.json-jackson.object-mapper throws exception

[CAMEL-11713](https://issues.apache.org/jira/browse/CAMEL-11713)

Camel-AWS S3: Support Client side Symmetric/Asymmetric Encryption

[CAMEL-11712](https://issues.apache.org/jira/browse/CAMEL-11712)

Camel-Caffeine: Add support for Removal Listener

[CAMEL-11710](https://issues.apache.org/jira/browse/CAMEL-11710)

trim for fixlength only trim one direction

[CAMEL-11706](https://issues.apache.org/jira/browse/CAMEL-11706)

Remove duplicate type converter methods from HBaseModelConverter

[CAMEL-11694](https://issues.apache.org/jira/browse/CAMEL-11694)

Camel-Hazelcast: Add more operation to queue

[CAMEL-11692](https://issues.apache.org/jira/browse/CAMEL-11692)

Set ClassLoader property on HBase configuration

[CAMEL-11691](https://issues.apache.org/jira/browse/CAMEL-11691)

Should resubscribe when reconnect MQTT

[CAMEL-11684](https://issues.apache.org/jira/browse/CAMEL-11684)

HealthCheck : expose health check info through JMX

[CAMEL-11682](https://issues.apache.org/jira/browse/CAMEL-11682)

camel-kafka - Support configuration parameter sasl.jaas.config

[CAMEL-11680](https://issues.apache.org/jira/browse/CAMEL-11680)

Camel-dropbox should support Put not only from localPath

[CAMEL-11679](https://issues.apache.org/jira/browse/CAMEL-11679)

camel-dropbox - Documentation should warn about remotePath being not set

[CAMEL-11678](https://issues.apache.org/jira/browse/CAMEL-11678)

camel-dropbox - Option clientIdentifier should not be mandatory

[CAMEL-11676](https://issues.apache.org/jira/browse/CAMEL-11676)

Upgrade HBase to 1.2.6

[CAMEL-11663](https://issues.apache.org/jira/browse/CAMEL-11663)

Create Karaf features for IEC 60870

[CAMEL-11661](https://issues.apache.org/jira/browse/CAMEL-11661)

ClusteredRouteControler : add an option to filter the routes to be included in the cluster

[CAMEL-11654](https://issues.apache.org/jira/browse/CAMEL-11654)

Add missing CXF dependencies to parent POM

[CAMEL-11642](https://issues.apache.org/jira/browse/CAMEL-11642)

Broker Credentials should be set from endpoint

[CAMEL-11641](https://issues.apache.org/jira/browse/CAMEL-11641)

SupervisingRouteController : backOff should be renamed deaultBackoff

[CAMEL-11640](https://issues.apache.org/jira/browse/CAMEL-11640)

SupervisingRouteController : Add a SPI to filter routes to supervise

[CAMEL-11639](https://issues.apache.org/jira/browse/CAMEL-11639)

camel-jms - Add support for changing JMS message selector on consumer at runtime via jmx

[CAMEL-11634](https://issues.apache.org/jira/browse/CAMEL-11634)

clean up dbcp 1 dependencies and move it (where possible) to dbcp 2

[CAMEL-11621](https://issues.apache.org/jira/browse/CAMEL-11621)

extend simple date formatter for properties

[CAMEL-11614](https://issues.apache.org/jira/browse/CAMEL-11614)

rest-dsl - Allow to configure api hostname

[CAMEL-11613](https://issues.apache.org/jira/browse/CAMEL-11613)

camel-spring-boot - Add auto configuration for FluentProducerTemplate

[CAMEL-11611](https://issues.apache.org/jira/browse/CAMEL-11611)

Add a knownHosts option to the camel-ssh component

[CAMEL-11604](https://issues.apache.org/jira/browse/CAMEL-11604)

New method expectedPropertyValuesReceivedInAnyOrder in MockEndpoint

[CAMEL-11603](https://issues.apache.org/jira/browse/CAMEL-11603)

Netty4 consumer in clientMode=true doesn't share channel with subsequent netty4 producers using reuseChannel=true

[CAMEL-11601](https://issues.apache.org/jira/browse/CAMEL-11601)

change camel-file default value for readLockLoggingLevel from WARN to DEBUG

[CAMEL-11597](https://issues.apache.org/jira/browse/CAMEL-11597)

Adding support for setting authentication client properties for elasticsearch

[CAMEL-11596](https://issues.apache.org/jira/browse/CAMEL-11596)

camel-spring-boot - actuator endpoint routes - Get single route only

[CAMEL-11594](https://issues.apache.org/jira/browse/CAMEL-11594)

rest configuration in spring boot should use map instead of list

[CAMEL-11587](https://issues.apache.org/jira/browse/CAMEL-11587)

SupervisingRouteController : add option for initial delay

[CAMEL-11586](https://issues.apache.org/jira/browse/CAMEL-11586)

camel-spring-boot - Have default value for endpoints.camelroutes.path

[CAMEL-11585](https://issues.apache.org/jira/browse/CAMEL-11585)

camel-spring-boot - Allow to reset route statistics via actuator

[CAMEL-11584](https://issues.apache.org/jira/browse/CAMEL-11584)

Add javadoc to spring boot auto configuration of camel.supervising.controller

[CAMEL-11583](https://issues.apache.org/jira/browse/CAMEL-11583)

SupervisingRouteController should honor if a route was explicit set to autoStartup=false

[CAMEL-11582](https://issues.apache.org/jira/browse/CAMEL-11582)

SupervisingRouteController should have better INFO logging on startup

[CAMEL-11577](https://issues.apache.org/jira/browse/CAMEL-11577)

apt plugin should generate URL as URL and not U R L in displayName

[CAMEL-11574](https://issues.apache.org/jira/browse/CAMEL-11574)

camel-lumberjack should support longs

[CAMEL-11570](https://issues.apache.org/jira/browse/CAMEL-11570)

Add an example for camel-google-pubsub

[CAMEL-11569](https://issues.apache.org/jira/browse/CAMEL-11569)

Implements CAMEL-11425 for camel-olingo4

[CAMEL-11568](https://issues.apache.org/jira/browse/CAMEL-11568)

Allow to set a CookiePolicy to CookieHandler

[CAMEL-11560](https://issues.apache.org/jira/browse/CAMEL-11560)

ServiceNow : allow to expand reference types in import\_set response

[CAMEL-11558](https://issues.apache.org/jira/browse/CAMEL-11558)

camel-jsonpath - Split via jsonpath looses quotes in json output

[CAMEL-11557](https://issues.apache.org/jira/browse/CAMEL-11557)

ServiceNow : support to get a resource with a full url

[CAMEL-11556](https://issues.apache.org/jira/browse/CAMEL-11556)

ServiceNow : add annotations on the model to customize sysparms

[CAMEL-11552](https://issues.apache.org/jira/browse/CAMEL-11552)

Provide FailureEvent interface as a general means of retrieving the cause

[CAMEL-11551](https://issues.apache.org/jira/browse/CAMEL-11551)

Use abstract base class for all context and route events

[CAMEL-11543](https://issues.apache.org/jira/browse/CAMEL-11543)

Camel doesn't support @TestPropertySource

[CAMEL-11542](https://issues.apache.org/jira/browse/CAMEL-11542)

camel-kafka - Add any new options from kafka 0.11.0 to the endpoint

[CAMEL-11539](https://issues.apache.org/jira/browse/CAMEL-11539)

WireTap - Add support for defer shutdown if pending tasks are active

[CAMEL-11531](https://issues.apache.org/jira/browse/CAMEL-11531)

camel-http-common; dependency servlet-api should be set to provided

[CAMEL-11528](https://issues.apache.org/jira/browse/CAMEL-11528)

WireTap - Allow to specify the url as non-dynamic

[CAMEL-11526](https://issues.apache.org/jira/browse/CAMEL-11526)

Several files in user manual issue warnings when processing with asciidoctor

[CAMEL-11515](https://issues.apache.org/jira/browse/CAMEL-11515)

Aggregator is not working correctly when completionTimeout < 1000ms

[CAMEL-11514](https://issues.apache.org/jira/browse/CAMEL-11514)

xslt component - Add support for ref and bean in resource uri

[CAMEL-11507](https://issues.apache.org/jira/browse/CAMEL-11507)

camel-servicenow : add an header to indicate the answer data type

[CAMEL-11506](https://issues.apache.org/jira/browse/CAMEL-11506)

MavenVersionManager blocks on unavailable URL

[CAMEL-11490](https://issues.apache.org/jira/browse/CAMEL-11490)

camel-spring-boot - Make it easy to filter Java RoutesBuilder from properties

[CAMEL-11487](https://issues.apache.org/jira/browse/CAMEL-11487)

Support resources load through custom defined protocols by registering custom UrlHandlers

[CAMEL-11484](https://issues.apache.org/jira/browse/CAMEL-11484)

Optimise - Simple Language / ExpressionBuilder can use cache of frequent used expressions when having nested functions

[CAMEL-11483](https://issues.apache.org/jira/browse/CAMEL-11483)

Optimise - Recording time taken for each processor should be advice

[CAMEL-11479](https://issues.apache.org/jira/browse/CAMEL-11479)

beanio - Unmarshalling multiline values as multiple records

[CAMEL-11473](https://issues.apache.org/jira/browse/CAMEL-11473)

camel-kafka - Use unique groupId by default

[CAMEL-11466](https://issues.apache.org/jira/browse/CAMEL-11466)

camel-tarfile dataformat cannot remove successfully processed files

[CAMEL-11464](https://issues.apache.org/jira/browse/CAMEL-11464)

Upgrade to rhino 1.7.7.1

[CAMEL-11461](https://issues.apache.org/jira/browse/CAMEL-11461)

SEDA - resolve references for concurrentConsumers, limitConcurrentConsumers

[CAMEL-11459](https://issues.apache.org/jira/browse/CAMEL-11459)

Upgrade CXF to 3.2

[CAMEL-11458](https://issues.apache.org/jira/browse/CAMEL-11458)

Avoid the use of the scriptengines libraries from google code

[CAMEL-11456](https://issues.apache.org/jira/browse/CAMEL-11456)

Make the camel-grpc component more cloud service friendly

[CAMEL-11452](https://issues.apache.org/jira/browse/CAMEL-11452)

It should be possible to add extra headers for STOMP subscriptions

[CAMEL-11450](https://issues.apache.org/jira/browse/CAMEL-11450)

Optimise - Calling a bean without method name defined can be optimised

[CAMEL-11449](https://issues.apache.org/jira/browse/CAMEL-11449)

start.spring.io - Define version range

[CAMEL-11448](https://issues.apache.org/jira/browse/CAMEL-11448)

Optimise - Routing engine can avoid check for interrupted exception which does not occur anymore

[CAMEL-11447](https://issues.apache.org/jira/browse/CAMEL-11447)

Optimise - MessageHistoryFactory should use long instead of Date

[CAMEL-11446](https://issues.apache.org/jira/browse/CAMEL-11446)

Look at using awaitility in camel-core tests when we wait via thread sleep etc

[CAMEL-11445](https://issues.apache.org/jira/browse/CAMEL-11445)

Declare JEE namespace in beans.xml

[CAMEL-11444](https://issues.apache.org/jira/browse/CAMEL-11444)

Optimise - Type converter registry can share known TypeMapping keys

[CAMEL-11442](https://issues.apache.org/jira/browse/CAMEL-11442)

Optimise - Use existing exchange id as breadcrumb

[CAMEL-11434](https://issues.apache.org/jira/browse/CAMEL-11434)

camel-hazelcast: auto discovery of hazelcast instances in spring-boot

[CAMEL-11432](https://issues.apache.org/jira/browse/CAMEL-11432)

Unable to skip tests when building camel-grpc

[CAMEL-11431](https://issues.apache.org/jira/browse/CAMEL-11431)

Spring beans with autowired constructors

[CAMEL-11425](https://issues.apache.org/jira/browse/CAMEL-11425)

Camel Olingo needs a way to dynamically set and receive HTTP headers

[CAMEL-11422](https://issues.apache.org/jira/browse/CAMEL-11422)

Mark plugin as threadsafe

[CAMEL-11421](https://issues.apache.org/jira/browse/CAMEL-11421)

Tokenizer - Allow to define group number as simple language

[CAMEL-11416](https://issues.apache.org/jira/browse/CAMEL-11416)

The overrides removal loop from BeanInfo.introspect(Class<?>) is no more necessary

[CAMEL-11410](https://issues.apache.org/jira/browse/CAMEL-11410)

camel-spring - Should not list uris as spring bean ids from Camel routes

[CAMEL-11409](https://issues.apache.org/jira/browse/CAMEL-11409)

The time camel waits for a WriteFuture to complete is hard-coded 10 seconds, this should be configurable

[CAMEL-11404](https://issues.apache.org/jira/browse/CAMEL-11404)

Upgrade to JPA 2.1

[CAMEL-11400](https://issues.apache.org/jira/browse/CAMEL-11400)

RoutePolicySupport - Should have separated suspend/resume vs start/stop consumer

[CAMEL-11399](https://issues.apache.org/jira/browse/CAMEL-11399)

ZooKeeperRoutePolicy only suspends and not stops JMSConsumer

[CAMEL-11398](https://issues.apache.org/jira/browse/CAMEL-11398)

camel-google-calendar should throw more friendly exception when the required credentials lack

[CAMEL-11396](https://issues.apache.org/jira/browse/CAMEL-11396)

Upgrade wsdl4j to 1.6.3

[CAMEL-11393](https://issues.apache.org/jira/browse/CAMEL-11393)

sql-stored - Add support for typeNames and scale in grammar

[CAMEL-11384](https://issues.apache.org/jira/browse/CAMEL-11384)

camel-spring-boot - Add auto configuration for turning on MDC logging

[CAMEL-11383](https://issues.apache.org/jira/browse/CAMEL-11383)

Replace Jersey JAX-RS client with CXF in Bonita component

[CAMEL-11381](https://issues.apache.org/jira/browse/CAMEL-11381)

Upgrade camel-opentracing to use OpenTracing-Java 0.30.0 with active span management

[CAMEL-11380](https://issues.apache.org/jira/browse/CAMEL-11380)

Optimise - Allow to turn DataType on or off on Message

[CAMEL-11379](https://issues.apache.org/jira/browse/CAMEL-11379)

Optimise - core type converters to be invoked faster

[CAMEL-11378](https://issues.apache.org/jira/browse/CAMEL-11378)

Upgrade to Apache Flink 1.3.0

[CAMEL-11377](https://issues.apache.org/jira/browse/CAMEL-11377)

Optimise - Bean expression invoking bean can use static method instead of creating new objects

[CAMEL-11375](https://issues.apache.org/jira/browse/CAMEL-11375)

Optimise - BeanProcessor - Make light-weight not as service

[CAMEL-11368](https://issues.apache.org/jira/browse/CAMEL-11368)

Optimise - Runtime endpoint registry - Turn off by default

[CAMEL-11365](https://issues.apache.org/jira/browse/CAMEL-11365)

camel-spring-boot - allowUseOriginalMessage should have same default as camel-core

[CAMEL-11364](https://issues.apache.org/jira/browse/CAMEL-11364)

Runtime endpoint registry - Do not use extended mode as default

[CAMEL-11363](https://issues.apache.org/jira/browse/CAMEL-11363)

Optimise - Use ArrayDeque instead of Stack

[CAMEL-11360](https://issues.apache.org/jira/browse/CAMEL-11360)

Optimise - Disable Tracer and use BacklogTracer instead

[CAMEL-11359](https://issues.apache.org/jira/browse/CAMEL-11359)

Deprecate TracedRouteNodes in favour of message history

[CAMEL-11358](https://issues.apache.org/jira/browse/CAMEL-11358)

Optimise - Event listener to avoid copy on write array list

[CAMEL-11355](https://issues.apache.org/jira/browse/CAMEL-11355)

Consumer - ErrorHandler should ignore rejected exception due to shutdown

[CAMEL-11354](https://issues.apache.org/jira/browse/CAMEL-11354)

Optimise - JMX oldest inflight can be optimised

[CAMEL-11353](https://issues.apache.org/jira/browse/CAMEL-11353)

Optimise - JMX Statistic split into specialized classes

[CAMEL-11351](https://issues.apache.org/jira/browse/CAMEL-11351)

Optimize - ProducerCache - Avoid creating new processor for each send if result processor

[CAMEL-11350](https://issues.apache.org/jira/browse/CAMEL-11350)

Optimize - StopWatch should be tiny to have less memory footprint

[CAMEL-11349](https://issues.apache.org/jira/browse/CAMEL-11349)

Optimize EventNotifer to reuse Event instance

[CAMEL-11348](https://issues.apache.org/jira/browse/CAMEL-11348)

Small Performance optimization in RestConsumerContextPathMatcher

[CAMEL-11347](https://issues.apache.org/jira/browse/CAMEL-11347)

Optimize AsyncCallback in EIPs to use reusable static classes

[CAMEL-11346](https://issues.apache.org/jira/browse/CAMEL-11346)

Optimize EventNotifier sending/sent exchange

[CAMEL-11345](https://issues.apache.org/jira/browse/CAMEL-11345)

Remove dependency on spring-core from gRPC component

[CAMEL-11344](https://issues.apache.org/jira/browse/CAMEL-11344)

Categorize and split examples in cloud, spring-boot, plain etc.

[CAMEL-11343](https://issues.apache.org/jira/browse/CAMEL-11343)

gRPC component cannot load service class

[CAMEL-11342](https://issues.apache.org/jira/browse/CAMEL-11342)

Optimize ManagedRoute

[CAMEL-11341](https://issues.apache.org/jira/browse/CAMEL-11341)

Optimize DefaultEndpointUtilizationStatistics

[CAMEL-11340](https://issues.apache.org/jira/browse/CAMEL-11340)

JMX performance statistics - Consider optimise to LongAdder

[CAMEL-11339](https://issues.apache.org/jira/browse/CAMEL-11339)

LRUCache - Optimise to use LongAdder instead of AtomicLong

[CAMEL-11338](https://issues.apache.org/jira/browse/CAMEL-11338)

New DefaultUuidGenerator to startup Camel faster

[CAMEL-11330](https://issues.apache.org/jira/browse/CAMEL-11330)

DefaultExchange - Look at optimize the Map implementation used for storing properties

[CAMEL-11329](https://issues.apache.org/jira/browse/CAMEL-11329)

swagger-dsl-generator artifact changed names to camel-swagger-dsl-generator, need to fix poms

[CAMEL-11323](https://issues.apache.org/jira/browse/CAMEL-11323)

Query Params are not mapped to camel headers with SparkJava

[CAMEL-11319](https://issues.apache.org/jira/browse/CAMEL-11319)

sql-stored - Add support for function

[CAMEL-11318](https://issues.apache.org/jira/browse/CAMEL-11318)

camel-ehcache: allow to configure named caches programmatically

[CAMEL-11316](https://issues.apache.org/jira/browse/CAMEL-11316)

camel-restlet - Rest-DSL should support OPTIONS

[CAMEL-11313](https://issues.apache.org/jira/browse/CAMEL-11313)

set defaultValue for FixedLength and other factories

[CAMEL-11312](https://issues.apache.org/jira/browse/CAMEL-11312)

camel-undertow - Rest-DSL should support OPTIONS

[CAMEL-11310](https://issues.apache.org/jira/browse/CAMEL-11310)

"code too large" when generating Salesforce DTOs

[CAMEL-11309](https://issues.apache.org/jira/browse/CAMEL-11309)

Components missing from parent POM dependency management

[CAMEL-11308](https://issues.apache.org/jira/browse/CAMEL-11308)

MongoDB: No (auto) conversion for BigDecimal

[CAMEL-11304](https://issues.apache.org/jira/browse/CAMEL-11304)

Add Distinct queries to camel-mongodb3

[CAMEL-11297](https://issues.apache.org/jira/browse/CAMEL-11297)

camel-ehcache-starter : auto discovery cache manager

[CAMEL-11291](https://issues.apache.org/jira/browse/CAMEL-11291)

spring boot starters: allow to hook into auto configuration process

[CAMEL-11284](https://issues.apache.org/jira/browse/CAMEL-11284)

camel-ehcache: allow to configure some options like a global cache manager on component level

[CAMEL-11278](https://issues.apache.org/jira/browse/CAMEL-11278)

camel-opentracing - Should deal with curly brackets may be encoded

[CAMEL-11277](https://issues.apache.org/jira/browse/CAMEL-11277)

camel-restlet - Should include component name in from endpoint uri

[CAMEL-11276](https://issues.apache.org/jira/browse/CAMEL-11276)

camel-restlet URI uses ( ) rather than { } for path parameters

[CAMEL-11275](https://issues.apache.org/jira/browse/CAMEL-11275)

FileWatcherReloadStrategy only watches on specific folder and no sub-folders

[CAMEL-11274](https://issues.apache.org/jira/browse/CAMEL-11274)

ReloadStrategySupport is not easy extendable because of a number of private's

[CAMEL-11271](https://issues.apache.org/jira/browse/CAMEL-11271)

Support placeholders on attributes of camelContext element

[CAMEL-11268](https://issues.apache.org/jira/browse/CAMEL-11268)

Upgrade camel-infinispan to support Infinispan 9.x

[CAMEL-11267](https://issues.apache.org/jira/browse/CAMEL-11267)

Add SpanDecorator for 'rest' component

[CAMEL-11263](https://issues.apache.org/jira/browse/CAMEL-11263)

set HeaderFilterStrategy before setting properties

[CAMEL-11261](https://issues.apache.org/jira/browse/CAMEL-11261)

Revise Camel context destruction in Spring (Boot) applications

[CAMEL-11259](https://issues.apache.org/jira/browse/CAMEL-11259)

Add Distinct queries to camel-mongodb

[CAMEL-11258](https://issues.apache.org/jira/browse/CAMEL-11258)

Use TracerResolver to obtain Tracer

[CAMEL-11256](https://issues.apache.org/jira/browse/CAMEL-11256)

Make camel-docker work on OSGi

[CAMEL-11254](https://issues.apache.org/jira/browse/CAMEL-11254)

Default matchOnUriPrefix to false on Undertow endpoint

[CAMEL-11253](https://issues.apache.org/jira/browse/CAMEL-11253)

camel-http4 - Add missing doc to component option

[CAMEL-11247](https://issues.apache.org/jira/browse/CAMEL-11247)

camel-spring-boot - Improve BOM to work better with start.spring.io

[CAMEL-11244](https://issues.apache.org/jira/browse/CAMEL-11244)

camel-hazelcast: use string/enum instead of numeric operation type

[CAMEL-11233](https://issues.apache.org/jira/browse/CAMEL-11233)

Allow overriding the setting of instanceUrl

[CAMEL-11222](https://issues.apache.org/jira/browse/CAMEL-11222)

Spring Boot Mojo should use formatter properties from JBoss Forge

[CAMEL-11220](https://issues.apache.org/jira/browse/CAMEL-11220)

camel-twitter - Allow to sort tweets so oldest come first

[CAMEL-11216](https://issues.apache.org/jira/browse/CAMEL-11216)

REST-DSL - Producer fails with NPE or other exceptions if you have not set a hostname

[CAMEL-11214](https://issues.apache.org/jira/browse/CAMEL-11214)

FluentProducerTemplate - Should allow non default uri

[CAMEL-11208](https://issues.apache.org/jira/browse/CAMEL-11208)

camel-swagger-java - Should use guava 20 and not 19

[CAMEL-11207](https://issues.apache.org/jira/browse/CAMEL-11207)

camel-twitter - Default poll delay is 60s we can lower it to 30s

[CAMEL-11204](https://issues.apache.org/jira/browse/CAMEL-11204)

camel-catalog - asEndpointUri to support connectors/component with no context-path part

[CAMEL-11188](https://issues.apache.org/jira/browse/CAMEL-11188)

Use Files.newFileInputStream instead of new FileInputStream

[CAMEL-11178](https://issues.apache.org/jira/browse/CAMEL-11178)

Default method on interface is invisible during Camel Simple evaluation

[CAMEL-11168](https://issues.apache.org/jira/browse/CAMEL-11168)

Add deprecationNote to @Metadata

[CAMEL-11155](https://issues.apache.org/jira/browse/CAMEL-11155)

camel-infinispan - producer command and operation discrepancies

[CAMEL-11140](https://issues.apache.org/jira/browse/CAMEL-11140)

camel-reactive-streams - Add uuid for CamelSubscription

[CAMEL-11125](https://issues.apache.org/jira/browse/CAMEL-11125)

camel-reactive-streams - Consumer should allow to not refill so frequently

[CAMEL-11005](https://issues.apache.org/jira/browse/CAMEL-11005)

camel-connector - Generate json using jackson

[CAMEL-10988](https://issues.apache.org/jira/browse/CAMEL-10988)

Improve performance of CaseInsensitiveMap

[CAMEL-10969](https://issues.apache.org/jira/browse/CAMEL-10969)

JSonSchemaHelper - Json parser should we use json-simple instead

[CAMEL-10896](https://issues.apache.org/jira/browse/CAMEL-10896)

camel-infinispan - Stores result in header and not body

[CAMEL-10798](https://issues.apache.org/jira/browse/CAMEL-10798)

camel-twitter, camel-ignite - Make the uri endpoints separated

[CAMEL-10768](https://issues.apache.org/jira/browse/CAMEL-10768)

Dropbox component should support specifying route params using headers

[CAMEL-10659](https://issues.apache.org/jira/browse/CAMEL-10659)

Camel-InfluxDB: Check if Database exists and if not create it

[CAMEL-10544](https://issues.apache.org/jira/browse/CAMEL-10544)

Upgrade to smack 4.2.0

[CAMEL-10512](https://issues.apache.org/jira/browse/CAMEL-10512)

camel-mllp - Add JMX attributes for connections & connection status

[CAMEL-10086](https://issues.apache.org/jira/browse/CAMEL-10086)

Remove Pattern.compile usages

[CAMEL-7414](https://issues.apache.org/jira/browse/CAMEL-7414)

camel-salesforce component should be able to return "raw" data

### New Feature (53)

[CAMEL-12220](https://issues.apache.org/jira/browse/CAMEL-12220)

Add Trigger based download to RemoteFileComponent

[CAMEL-11832](https://issues.apache.org/jira/browse/CAMEL-11832)

camel-aws - Add support for Lambda

[CAMEL-11806](https://issues.apache.org/jira/browse/CAMEL-11806)

cluster service : add JMX support

[CAMEL-11778](https://issues.apache.org/jira/browse/CAMEL-11778)

New camel-ldif component

[CAMEL-11704](https://issues.apache.org/jira/browse/CAMEL-11704)

Camel-RabbitMQ: Allow passive queue declaration

[CAMEL-11693](https://issues.apache.org/jira/browse/CAMEL-11693)

HealthCheck : add health check support for camel-undertow

[CAMEL-11685](https://issues.apache.org/jira/browse/CAMEL-11685)

Camel-Hazelcast: Add removeAll and removeIf to queue component

[CAMEL-11660](https://issues.apache.org/jira/browse/CAMEL-11660)

ClusteredRouteControler : add an option to delay the startup of the routes

[CAMEL-11659](https://issues.apache.org/jira/browse/CAMEL-11659)

Create a ClusteredRouteController

[CAMEL-11645](https://issues.apache.org/jira/browse/CAMEL-11645)

Add possibility to filter routes which will report spans

[CAMEL-11612](https://issues.apache.org/jira/browse/CAMEL-11612)

Create ASN.1 dataformat

[CAMEL-11581](https://issues.apache.org/jira/browse/CAMEL-11581)

SupervisingRouteController should have spring-boot auto configuration

[CAMEL-11580](https://issues.apache.org/jira/browse/CAMEL-11580)

Add JMX api RouteController and SupervisingRouteController

[CAMEL-11573](https://issues.apache.org/jira/browse/CAMEL-11573)

Enable MultipleConsumersSupport for Jt400Endpoint

[CAMEL-11571](https://issues.apache.org/jira/browse/CAMEL-11571)

Google Cloud BigQuery

[CAMEL-11563](https://issues.apache.org/jira/browse/CAMEL-11563)

Add predicate option to @Consume so the bean is only called if its evaluated to true

[CAMEL-11555](https://issues.apache.org/jira/browse/CAMEL-11555)

ServiceNow : create a maven plugin to generate models based on table layout

[CAMEL-11554](https://issues.apache.org/jira/browse/CAMEL-11554)

ServiceNow : add meta data extension to retrieve table's structure

[CAMEL-11550](https://issues.apache.org/jira/browse/CAMEL-11550)

Component extensions

[CAMEL-11485](https://issues.apache.org/jira/browse/CAMEL-11485)

Camel-Caffeine: Add idempotent repository to component

[CAMEL-11443](https://issues.apache.org/jira/browse/CAMEL-11443)

Add a RouteController SPI to allow to customize routes life-cycle

[CAMEL-11439](https://issues.apache.org/jira/browse/CAMEL-11439)

Camel-Caffeine: Create an Aggregation Repository using Caffeine

[CAMEL-11438](https://issues.apache.org/jira/browse/CAMEL-11438)

New crypto component CMS (Cryptographic Message Syntax)

[CAMEL-11435](https://issues.apache.org/jira/browse/CAMEL-11435)

Camel-Caffeine: Support Time-based and size-based eviction in Caffeine

[CAMEL-11420](https://issues.apache.org/jira/browse/CAMEL-11420)

Add contains ignore case operator to simple language

[CAMEL-11389](https://issues.apache.org/jira/browse/CAMEL-11389)

add karaf feature for camel-fastjson

[CAMEL-11373](https://issues.apache.org/jira/browse/CAMEL-11373)

Create a Camel Twilio component

[CAMEL-11362](https://issues.apache.org/jira/browse/CAMEL-11362)

create a LeaderElectionservice

[CAMEL-11337](https://issues.apache.org/jira/browse/CAMEL-11337)

Camel-Infinispan: Add support for GetOrDefault operation on Producer

[CAMEL-11335](https://issues.apache.org/jira/browse/CAMEL-11335)

Create Actuator endpoint to expose route information

[CAMEL-11331](https://issues.apache.org/jira/browse/CAMEL-11331)

camel-kubernetes - Add Kubernetes based RoutePolicy

[CAMEL-11302](https://issues.apache.org/jira/browse/CAMEL-11302)

camel-infinispan-starter : enable cache manager auto discovery

[CAMEL-11296](https://issues.apache.org/jira/browse/CAMEL-11296)

camel-maven-plugin:validate - Allow to detect duplicate route ids

[CAMEL-11236](https://issues.apache.org/jira/browse/CAMEL-11236)

camel-grpc - improve streaming capabilities to bridge reactive streams

[CAMEL-11196](https://issues.apache.org/jira/browse/CAMEL-11196)

Camel connectors - Allow to configure in one place and let it figure out component vs endpoint level

[CAMEL-11156](https://issues.apache.org/jira/browse/CAMEL-11156)

Camel-Kubernetes: Add support for Deployment resources

[CAMEL-11149](https://issues.apache.org/jira/browse/CAMEL-11149)

SPI - Allow to plugin different headers map implementation

[CAMEL-11147](https://issues.apache.org/jira/browse/CAMEL-11147)

camel-jms2 - JMS component using JMS 2.x api

[CAMEL-11122](https://issues.apache.org/jira/browse/CAMEL-11122)

camel-reactive-streams - Add more JMX information

[CAMEL-10807](https://issues.apache.org/jira/browse/CAMEL-10807)

Create camel-reactor component

[CAMEL-10744](https://issues.apache.org/jira/browse/CAMEL-10744)

Camel Salesforce maven plugin should generate JSON schema

[CAMEL-10743](https://issues.apache.org/jira/browse/CAMEL-10743)

Add support in Salesforce component for plain JSON input and output

[CAMEL-10715](https://issues.apache.org/jira/browse/CAMEL-10715)

service-call : create ZooKeeper based ServiceDiscovery

[CAMEL-10320](https://issues.apache.org/jira/browse/CAMEL-10320)

Provide a LeaderPolicy to ease the implementation of master/slave route/context

[CAMEL-10267](https://issues.apache.org/jira/browse/CAMEL-10267)

Create a Caffeine component

[CAMEL-10054](https://issues.apache.org/jira/browse/CAMEL-10054)

Create camel-atomix component

[CAMEL-10026](https://issues.apache.org/jira/browse/CAMEL-10026)

HealthCheck API

[CAMEL-9799](https://issues.apache.org/jira/browse/CAMEL-9799)

JSON/JSON Schema validator

[CAMEL-9008](https://issues.apache.org/jira/browse/CAMEL-9008)

Contributing GRPC / Thrift support to Camel

[CAMEL-8502](https://issues.apache.org/jira/browse/CAMEL-8502)

Camel BOM for Maven users

[CAMEL-7672](https://issues.apache.org/jira/browse/CAMEL-7672)

camel-stomp - Add support for reply-to header

[CAMEL-7621](https://issues.apache.org/jira/browse/CAMEL-7621)

camel-bindy - Two new properties to StringFormat through DataField: toUppercase and mapToASCII

[CAMEL-5723](https://issues.apache.org/jira/browse/CAMEL-5723)

camel-jaxb: partClass and partNamespace dynamically set by header

### Sub-task (22)

[CAMEL-11859](https://issues.apache.org/jira/browse/CAMEL-11859)

Deprecate camel-spark-rest as it does not play well in OSGi

[CAMEL-11831](https://issues.apache.org/jira/browse/CAMEL-11831)

\[example\] twitter-websocket, twitter-websocket-blueprint - http://localhost:9090/index.html returns empty page

[CAMEL-11830](https://issues.apache.org/jira/browse/CAMEL-11830)

\[example\] sql - no application log on karaf

[CAMEL-11829](https://issues.apache.org/jira/browse/CAMEL-11829)

\[example\] spring-boot-health-checks - 'application' keep emitting ERRORs

[CAMEL-11828](https://issues.apache.org/jira/browse/CAMEL-11828)

\[example\] camel context doesn't start on some examples

[CAMEL-11827](https://issues.apache.org/jira/browse/CAMEL-11827)

\[example\] spring-boot-servicecall - service1 returns 404 not found

[CAMEL-11826](https://issues.apache.org/jira/browse/CAMEL-11826)

\[example\] hystrix, opentracing - spring-boot:run throws NPE

[CAMEL-11825](https://issues.apache.org/jira/browse/CAMEL-11825)

\[example\] etl - unable to resolve dependency on karaf

[CAMEL-11824](https://issues.apache.org/jira/browse/CAMEL-11824)

\[example\] cxf-proxy, loan-broker-cxf - port 1101/1102 is unexpectedly used

[CAMEL-11762](https://issues.apache.org/jira/browse/CAMEL-11762)

Add Karaf Feature for ASN.1 DataFormat

[CAMEL-11717](https://issues.apache.org/jira/browse/CAMEL-11717)

HealthCheck : create a consul based health check repository

[CAMEL-11699](https://issues.apache.org/jira/browse/CAMEL-11699)

HealthCheck : grab service status from external service status repository

[CAMEL-11696](https://issues.apache.org/jira/browse/CAMEL-11696)

Add security and advanced properties to the camel-thrift component

[CAMEL-11695](https://issues.apache.org/jira/browse/CAMEL-11695)

Add security and advanced properties to the camel-grpc component

[CAMEL-11689](https://issues.apache.org/jira/browse/CAMEL-11689)

HealthCheck : add health check support for camel-servicenow

[CAMEL-11491](https://issues.apache.org/jira/browse/CAMEL-11491)

Apply non-mandatory nature of amazon client to AWS components being able to specify accessKey and secretKey

[CAMEL-11333](https://issues.apache.org/jira/browse/CAMEL-11333)

Create a new camel-thrift RPC component

[CAMEL-11332](https://issues.apache.org/jira/browse/CAMEL-11332)

Create a new camel-thrift data format

[CAMEL-11315](https://issues.apache.org/jira/browse/CAMEL-11315)

Replace dummy URI paths on directmessage and search with something meaningful

[CAMEL-11243](https://issues.apache.org/jira/browse/CAMEL-11243)

Split camel-kubernetes component

[CAMEL-11242](https://issues.apache.org/jira/browse/CAMEL-11242)

Split camel-twitter component

[CAMEL-11237](https://issues.apache.org/jira/browse/CAMEL-11237)

camel-grpc - Add a grpc consumer

### Task (74)

[CAMEL-11883](https://issues.apache.org/jira/browse/CAMEL-11883)

New arguments to createGroup unintentionally made mandatory

[CAMEL-11857](https://issues.apache.org/jira/browse/CAMEL-11857)

camel-zendesk : create karaf feature

[CAMEL-11855](https://issues.apache.org/jira/browse/CAMEL-11855)

camel-opentracing : create karaf feature

[CAMEL-11854](https://issues.apache.org/jira/browse/CAMEL-11854)

camel-pubnub : create karaf feature

[CAMEL-11853](https://issues.apache.org/jira/browse/CAMEL-11853)

camel-reactor : create karaf feature

[CAMEL-11852](https://issues.apache.org/jira/browse/CAMEL-11852)

camel-milo : create karaf feature

[CAMEL-11851](https://issues.apache.org/jira/browse/CAMEL-11851)

camel-kura : create karaf feature

[CAMEL-11849](https://issues.apache.org/jira/browse/CAMEL-11849)

camel-crypto-cms : create karaf feature

[CAMEL-11821](https://issues.apache.org/jira/browse/CAMEL-11821)

camel-xstream - tests should initialize xstream

[CAMEL-11817](https://issues.apache.org/jira/browse/CAMEL-11817)

cluster-service : camel-atomix spring boot support should have better bean names

[CAMEL-11808](https://issues.apache.org/jira/browse/CAMEL-11808)

log4j2 2.9 upgrade causes errors in camel-salesforce and others

[CAMEL-11805](https://issues.apache.org/jira/browse/CAMEL-11805)

Upgrade to Apache Ignite 2.x

[CAMEL-11794](https://issues.apache.org/jira/browse/CAMEL-11794)

Remove commons-codec and commons-land deps from the Consul component

[CAMEL-11790](https://issues.apache.org/jira/browse/CAMEL-11790)

camel-headersmap : create karaf feature

[CAMEL-11786](https://issues.apache.org/jira/browse/CAMEL-11786)

Component docs - Generated docs should be in proper ascii doc format

[CAMEL-11776](https://issues.apache.org/jira/browse/CAMEL-11776)

Rename the twitter-search-connector

[CAMEL-11775](https://issues.apache.org/jira/browse/CAMEL-11775)

Upgrade to Spring Boot 1.5.7 or better

[CAMEL-11770](https://issues.apache.org/jira/browse/CAMEL-11770)

spring-boot examples - Should not import camel-parent

[CAMEL-11766](https://issues.apache.org/jira/browse/CAMEL-11766)

camel-kubernetes adoc file missing

[CAMEL-11757](https://issues.apache.org/jira/browse/CAMEL-11757)

Upgrade CometD library

[CAMEL-11756](https://issues.apache.org/jira/browse/CAMEL-11756)

camel-spring-boot2 - Create experimental spring boot 2 component

[CAMEL-11751](https://issues.apache.org/jira/browse/CAMEL-11751)

Dropbox Component - Update to APIv2

[CAMEL-11746](https://issues.apache.org/jira/browse/CAMEL-11746)

Deprecate Camel-Hessian

[CAMEL-11745](https://issues.apache.org/jira/browse/CAMEL-11745)

Deprecate Camel-Castor

[CAMEL-11741](https://issues.apache.org/jira/browse/CAMEL-11741)

\[Documentation\] Correct a link

[CAMEL-11740](https://issues.apache.org/jira/browse/CAMEL-11740)

camel-bean-validator - Should use validation 1.x api

[CAMEL-11737](https://issues.apache.org/jira/browse/CAMEL-11737)

Remove deprecated code from camel-aws tests

[CAMEL-11736](https://issues.apache.org/jira/browse/CAMEL-11736)

Camel-AWS: Use regional client instead of define region for single operation

[CAMEL-11734](https://issues.apache.org/jira/browse/CAMEL-11734)

Upgrade grpc-java to 1.6.1

[CAMEL-11714](https://issues.apache.org/jira/browse/CAMEL-11714)

Add a Kubernetes Camel-gRPC spring-boot example

[CAMEL-11703](https://issues.apache.org/jira/browse/CAMEL-11703)

Camel-AWS: Use builders instead of different constructors

[CAMEL-11701](https://issues.apache.org/jira/browse/CAMEL-11701)

Camel-AWS S3: Use AmazonS3ClientBuilder instead of different constructors

[CAMEL-11655](https://issues.apache.org/jira/browse/CAMEL-11655)

Camel-Nagios: Deprecate EncryptionMethod and use Encryption Enum

[CAMEL-11653](https://issues.apache.org/jira/browse/CAMEL-11653)

Camel-Nagios: Switch to jsendnsca ported library

[CAMEL-11644](https://issues.apache.org/jira/browse/CAMEL-11644)

Create a Camel-gRPC example

[CAMEL-11638](https://issues.apache.org/jira/browse/CAMEL-11638)

Upgrade to Apache SSHD 1.6.x

[CAMEL-11635](https://issues.apache.org/jira/browse/CAMEL-11635)

wrong groupId in camel examples readme.md and features.xml

[CAMEL-11633](https://issues.apache.org/jira/browse/CAMEL-11633)

Upgrade client mqtt paho base lib

[CAMEL-11618](https://issues.apache.org/jira/browse/CAMEL-11618)

Add a Camel-Infinispan example using his starter

[CAMEL-11579](https://issues.apache.org/jira/browse/CAMEL-11579)

Add unit test / example for SupervisingRouteController

[CAMEL-11578](https://issues.apache.org/jira/browse/CAMEL-11578)

Add javadoc to util.backoff

[CAMEL-11561](https://issues.apache.org/jira/browse/CAMEL-11561)

Cleanup Salesforce integration tests setup

[CAMEL-11553](https://issues.apache.org/jira/browse/CAMEL-11553)

Upgrade to Brave 4

[CAMEL-11545](https://issues.apache.org/jira/browse/CAMEL-11545)

Avoid double dot in enriched with default value in XML XSD

[CAMEL-11544](https://issues.apache.org/jira/browse/CAMEL-11544)

camel-facebook - Upgrade to 2.4.10

[CAMEL-11478](https://issues.apache.org/jira/browse/CAMEL-11478)

Revise what Salesforce component properties are marked as secret

[CAMEL-11428](https://issues.apache.org/jira/browse/CAMEL-11428)

Remove IDEA plugin and doc

[CAMEL-11411](https://issues.apache.org/jira/browse/CAMEL-11411)

camel-opentracing example uses incorrect groupId

[CAMEL-11395](https://issues.apache.org/jira/browse/CAMEL-11395)

upgrade maven-surefire-plugin

[CAMEL-11357](https://issues.apache.org/jira/browse/CAMEL-11357)

Change examples groupId and disable publishing to Maven central

[CAMEL-11356](https://issues.apache.org/jira/browse/CAMEL-11356)

Camel-Kubernetes: refactoring tests by using Kubernetes-server-mock and Openshift-server-mock

[CAMEL-11336](https://issues.apache.org/jira/browse/CAMEL-11336)

Update dozer to latest

[CAMEL-11326](https://issues.apache.org/jira/browse/CAMEL-11326)

Exclude org.json from camel-spark

[CAMEL-11324](https://issues.apache.org/jira/browse/CAMEL-11324)

Deprecate camel-krati

[CAMEL-11320](https://issues.apache.org/jira/browse/CAMEL-11320)

sql-stored - Should not extend polling endpoint as its not for consumer

[CAMEL-11311](https://issues.apache.org/jira/browse/CAMEL-11311)

example - Add example for Spring Boot with external ActiveMQ broker

[CAMEL-11307](https://issues.apache.org/jira/browse/CAMEL-11307)

Create Camel-Azure Karaf feature

[CAMEL-11301](https://issues.apache.org/jira/browse/CAMEL-11301)

Camel-weather and camel-geocoder: freegeoip.io/json has been moved permanently

[CAMEL-11295](https://issues.apache.org/jira/browse/CAMEL-11295)

Spelling mistake in Apache Routing Policy

[CAMEL-11294](https://issues.apache.org/jira/browse/CAMEL-11294)

Repair not-working-examples or mark as deprecated

[CAMEL-11285](https://issues.apache.org/jira/browse/CAMEL-11285)

Camel-Elasticsearch5: Upgrade to Elasticsearch 5.3.x

[CAMEL-11265](https://issues.apache.org/jira/browse/CAMEL-11265)

Fix maven warning about fork option

[CAMEL-11260](https://issues.apache.org/jira/browse/CAMEL-11260)

Use Couchbase client OSGi bundle in Karaf feature

[CAMEL-11245](https://issues.apache.org/jira/browse/CAMEL-11245)

camel-opentracing refers to no longer used GlobalTracer

[CAMEL-11239](https://issues.apache.org/jira/browse/CAMEL-11239)

camel-catalog-maven - Remove sl4j logger

[CAMEL-11219](https://issues.apache.org/jira/browse/CAMEL-11219)

Upgrade to RxJava 2.1.x

[CAMEL-11209](https://issues.apache.org/jira/browse/CAMEL-11209)

camel-core-starter - Should not have caffeine dependency

[CAMEL-11194](https://issues.apache.org/jira/browse/CAMEL-11194)

Upgrade Checkstyle and update rules

[CAMEL-11187](https://issues.apache.org/jira/browse/CAMEL-11187)

Java 9 - building camel-spring has a maven WARN

[CAMEL-11146](https://issues.apache.org/jira/browse/CAMEL-11146)

Update description for all data formats and languages on big readme file

[CAMEL-11121](https://issues.apache.org/jira/browse/CAMEL-11121)

Create a Camel-gRPC karaf feature

[CAMEL-11103](https://issues.apache.org/jira/browse/CAMEL-11103)

Add camel-digitalocean Karaf feature

[CAMEL-11059](https://issues.apache.org/jira/browse/CAMEL-11059)

camel-spring-dm - Should be removed

[CAMEL-10665](https://issues.apache.org/jira/browse/CAMEL-10665)

Restlet header warnings - again

### Test (20)

[CAMEL-11850](https://issues.apache.org/jira/browse/CAMEL-11850)

camel-hdfs2 - test fails on jdk9

[CAMEL-11840](https://issues.apache.org/jira/browse/CAMEL-11840)

camel-itest-karaf - CamelLinkedinTest fails

[CAMEL-11839](https://issues.apache.org/jira/browse/CAMEL-11839)

camel-itest-karaf - CamelBoxTest fails

[CAMEL-11812](https://issues.apache.org/jira/browse/CAMEL-11812)

spring-boot-starter - Unit test fail in netty

[CAMEL-11804](https://issues.apache.org/jira/browse/CAMEL-11804)

Add tests that check DESTINATION\_OVERRIDE\_URL

[CAMEL-11782](https://issues.apache.org/jira/browse/CAMEL-11782)

Test failure in CxfEndpointBeansTest after update to CXF 3.2.0: Unresolved ref/idref to component:

[CAMEL-11771](https://issues.apache.org/jira/browse/CAMEL-11771)

Remove commons-logging import

[CAMEL-11758](https://issues.apache.org/jira/browse/CAMEL-11758)

camel-itest-karaf - CamelBeanValidatorTest fails on Jenkins

[CAMEL-11747](https://issues.apache.org/jira/browse/CAMEL-11747)

Change SupervisingRouteControllerRestartTest to not use Jetty in test

[CAMEL-11617](https://issues.apache.org/jira/browse/CAMEL-11617)

spring-boot - service-call tests uses hardcoded port numbers

[CAMEL-11602](https://issues.apache.org/jira/browse/CAMEL-11602)

camel-cxf - there are failing test cases on Windows

[CAMEL-11534](https://issues.apache.org/jira/browse/CAMEL-11534)

Incorrect transferExchange option test in camel-jms component

[CAMEL-11516](https://issues.apache.org/jira/browse/CAMEL-11516)

FtpConsumerFileSplitTest fails on windows due to platform line.seperator

[CAMEL-11436](https://issues.apache.org/jira/browse/CAMEL-11436)

camel-spring-ldap - Has test failures

[CAMEL-11334](https://issues.apache.org/jira/browse/CAMEL-11334)

camel-grpc - Unit test fails due port number issue

[CAMEL-11328](https://issues.apache.org/jira/browse/CAMEL-11328)

camel-example-cdi-test - Fix invalid logging format

[CAMEL-11314](https://issues.apache.org/jira/browse/CAMEL-11314)

Fix failing tests in camel-swagger-java

[CAMEL-11184](https://issues.apache.org/jira/browse/CAMEL-11184)

tests - Add missing tests to itest spring boot

[CAMEL-11144](https://issues.apache.org/jira/browse/CAMEL-11144)

camel-milo - Use dynamic port in test

[CAMEL-10141](https://issues.apache.org/jira/browse/CAMEL-10141)

Test Apache Camel on Java 9

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).