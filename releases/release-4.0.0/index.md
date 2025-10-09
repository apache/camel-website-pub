# Apache camel 4.0.0 Release

## New and Noteworthy

This release is the new Camel 4.0.0 major LTS release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.0.0</version>
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
      <version>4.0.0</version>
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
| [apache-camel-4.0.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.0/apache-camel-4.0.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.0/apache-camel-4.0.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.0/apache-camel-4.0.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (128)

[CAMEL-19724](https://issues.apache.org/jira/browse/CAMEL-19724)

camel-core: core may lose log messages under concurrent initialization

[CAMEL-19720](https://issues.apache.org/jira/browse/CAMEL-19720)

camel-test-infra: service initialization failure does not provide sufficient details

[CAMEL-19719](https://issues.apache.org/jira/browse/CAMEL-19719)

camel-rest - Infinite loop when maximumRedeliveries > 0

[CAMEL-19702](https://issues.apache.org/jira/browse/CAMEL-19702)

camel-jbang - camel version list --from-version=4

[CAMEL-19701](https://issues.apache.org/jira/browse/CAMEL-19701)

camel-main - Filter out Kubernetes ENV injected service host/port

[CAMEL-19697](https://issues.apache.org/jira/browse/CAMEL-19697)

camel-jbang - export dependency for platform-http-main

[CAMEL-19693](https://issues.apache.org/jira/browse/CAMEL-19693)

camel-main - Base package scan should detect @BindToRegistry beans

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

[CAMEL-19670](https://issues.apache.org/jira/browse/CAMEL-19670)

camel-core - Splitter fails with "Caused by: java.io.IOException: Stream closed"

[CAMEL-19668](https://issues.apache.org/jira/browse/CAMEL-19668)

camel-test-infra-artemis: incorrectly creating a singleton instance

[CAMEL-19666](https://issues.apache.org/jira/browse/CAMEL-19666)

camel-test-infra-artemis: queue auto-delete may lock tests

[CAMEL-19664](https://issues.apache.org/jira/browse/CAMEL-19664)

camel-test-infra-artemis: concurrency issues

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

[CAMEL-19569](https://issues.apache.org/jira/browse/CAMEL-19569)

\[observability|opentelemetry\].CurrentSpanTest.testContextDoesNotLeak() fail on Github Actions

[CAMEL-19568](https://issues.apache.org/jira/browse/CAMEL-19568)

camel-mail - HTTP/2 Multipart boundary

[CAMEL-19566](https://issues.apache.org/jira/browse/CAMEL-19566)

Camel micrometer documentation shows wrong parameter value name for summary

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

[CAMEL-19470](https://issues.apache.org/jira/browse/CAMEL-19470)

Exchange body is null when using Mongodb changeStreams with update operation

[CAMEL-19459](https://issues.apache.org/jira/browse/CAMEL-19459)

camel-report-maven-plugin fails to run due to missing class

[CAMEL-19457](https://issues.apache.org/jira/browse/CAMEL-19457)

camel-dynamic-router - InflightRepository size can be negative

[CAMEL-19452](https://issues.apache.org/jira/browse/CAMEL-19452)

camel-jbang - Run with --open-api does not show log in console

[CAMEL-19443](https://issues.apache.org/jira/browse/CAMEL-19443)

camel-kamelet - Route templates should use route configured error handler

[CAMEL-19432](https://issues.apache.org/jira/browse/CAMEL-19432)

camel-azure-eventhubs: Providing a custom EventHubProducerAsyncClient has no effect

[CAMEL-19426](https://issues.apache.org/jira/browse/CAMEL-19426)

Spring-WS syntaxt and path properties inconsistency

[CAMEL-19415](https://issues.apache.org/jira/browse/CAMEL-19415)

camel-stax: using xtokenize might be NPE on xml default namespace

[CAMEL-19405](https://issues.apache.org/jira/browse/CAMEL-19405)

camel-jbang - camel get circuitbreaker may not work

[CAMEL-19393](https://issues.apache.org/jira/browse/CAMEL-19393)

camel-kafka - Configuring kafka option should no longer all be string types

[CAMEL-19387](https://issues.apache.org/jira/browse/CAMEL-19387)

camel-kafka - Cannot set custom azure credential provider

[CAMEL-19383](https://issues.apache.org/jira/browse/CAMEL-19383)

camel-jslt: allowTemplateFromHeader ignores header on subsequent exchanges

[CAMEL-19381](https://issues.apache.org/jira/browse/CAMEL-19381)

Infinite loop creating processes with Camel JBang

[CAMEL-19373](https://issues.apache.org/jira/browse/CAMEL-19373)

spring-rabbitmq - Component does not Respect replyTimeout for InOut Exchanges

[CAMEL-19371](https://issues.apache.org/jira/browse/CAMEL-19371)

RedeliveryErrorHandler's suppressed exceptions cause memory leak and logging issue

[CAMEL-19364](https://issues.apache.org/jira/browse/CAMEL-19364)

Rest-openapi: lookup mechanism does not work after changes from Camel-18963

[CAMEL-19359](https://issues.apache.org/jira/browse/CAMEL-19359)

camel-spring-boot - When camel start graceful shutdown, it still receive new request during graceful shutdown.

[CAMEL-19345](https://issues.apache.org/jira/browse/CAMEL-19345)

KameletDiscoveryTest fails to find routeTemplate

[CAMEL-19343](https://issues.apache.org/jira/browse/CAMEL-19343)

Predicates are shared between templated routes in Java DSL with simple predicate builder

[CAMEL-19342](https://issues.apache.org/jira/browse/CAMEL-19342)

Rest Inline Routes mixed with direct routes.

[CAMEL-19314](https://issues.apache.org/jira/browse/CAMEL-19314)

camel-aws - Connection pool shutdown when aws health checks are used

[CAMEL-19298](https://issues.apache.org/jira/browse/CAMEL-19298)

Snmp: version 3 is not supported for several actions for the component

[CAMEL-19296](https://issues.apache.org/jira/browse/CAMEL-19296)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.xml'

[CAMEL-19295](https://issues.apache.org/jira/browse/CAMEL-19295)

Concurrency issues with dynamicMap in AbstractDynamicRegistry

[CAMEL-19293](https://issues.apache.org/jira/browse/CAMEL-19293)

camel-spring-ldap - base is set twice when using SB AutoConfiguration

[CAMEL-19285](https://issues.apache.org/jira/browse/CAMEL-19285)

Kafka consumer can flood brokers if TLS handshake fails and pollOnError is set to RECONNECT

[CAMEL-19281](https://issues.apache.org/jira/browse/CAMEL-19281)

Aws2- healthchecks not closing resources for awsClient

[CAMEL-19271](https://issues.apache.org/jira/browse/CAMEL-19271)

camel-jbang - trace with --latest should show last completed if no current inflight

[CAMEL-19259](https://issues.apache.org/jira/browse/CAMEL-19259)

camel-maven-plugin - Use configured main-class instead of KameletMain

[CAMEL-19257](https://issues.apache.org/jira/browse/CAMEL-19257)

camel-jslt: Exception when using camel-jslt in Tomcat Servlet

[CAMEL-19256](https://issues.apache.org/jira/browse/CAMEL-19256)

camel-jdbc: leaks the statement in doCreateAndExecuteSqlStatement

[CAMEL-19255](https://issues.apache.org/jira/browse/CAMEL-19255)

Jbang: jbang is not copying custom kamelets to /kametets

[CAMEL-19250](https://issues.apache.org/jira/browse/CAMEL-19250)

Classes generated by camel-restdsl-openapi-plugin are not added to jar

[CAMEL-19249](https://issues.apache.org/jira/browse/CAMEL-19249)

camel-salesforce: Creating blob data is broken

[CAMEL-19247](https://issues.apache.org/jira/browse/CAMEL-19247)

camel-zeebe - Set Default Host and Port for Zeebe connection

[CAMEL-19242](https://issues.apache.org/jira/browse/CAMEL-19242)

camel-jbang - camel doc may not work on main

[CAMEL-19224](https://issues.apache.org/jira/browse/CAMEL-19224)

camel-azure - BlobConsumer does not use prefix

[CAMEL-19220](https://issues.apache.org/jira/browse/CAMEL-19220)

camel-groovy - Avoid setting variables to initialize the binding

[CAMEL-19199](https://issues.apache.org/jira/browse/CAMEL-19199)

Unable to start PLC4X route in camel-plc4x

[CAMEL-19198](https://issues.apache.org/jira/browse/CAMEL-19198)

Dynamic Router EIP component does not evaluate filters by order of priority attribute

[CAMEL-19190](https://issues.apache.org/jira/browse/CAMEL-19190)

camel-vertx-websocket: sendToAll option may not discover connected host peers correctly

[CAMEL-19181](https://issues.apache.org/jira/browse/CAMEL-19181)

camel-springboot - mapstruct component is not autoconfigured automatically

[CAMEL-19174](https://issues.apache.org/jira/browse/CAMEL-19174)

Jira component: duplicate messages with the new issues consumer

[CAMEL-19162](https://issues.apache.org/jira/browse/CAMEL-19162)

camel-ehcache - llegalStateException: Close not supported from UNINITIALIZED. When context.addRouteDefinition() called multiple times in route with Ehcache consumer

[CAMEL-19161](https://issues.apache.org/jira/browse/CAMEL-19161)

camel-salesforce - Connection issue when using lazy login

[CAMEL-19158](https://issues.apache.org/jira/browse/CAMEL-19158)

camel-core: ThrowExceptionProcessor may silently ignore exceptions in constructing the exception object

[CAMEL-19156](https://issues.apache.org/jira/browse/CAMEL-19156)

XML route configurations ignored without both XML IO and JAXB XML loaded

[CAMEL-19155](https://issues.apache.org/jira/browse/CAMEL-19155)

Azure Service Bus component completes messages instead of abandoning on error

[CAMEL-19151](https://issues.apache.org/jira/browse/CAMEL-19151)

The 'ignoreInvalidEndpoint' option isn't relevant for a static URI for WireTap component

[CAMEL-19136](https://issues.apache.org/jira/browse/CAMEL-19136)

camel-micrometer - Too many tags created by micrometer WebMvcTagsProvider

[CAMEL-19133](https://issues.apache.org/jira/browse/CAMEL-19133)

camel-zookeeper - Zookeeper's service registration and discovery is not working with serialized

[CAMEL-19124](https://issues.apache.org/jira/browse/CAMEL-19124)

Tracer doesn't continue spans for AbstractInternalSpanDecorator

[CAMEL-19113](https://issues.apache.org/jira/browse/CAMEL-19113)

Platform-http-vertx: consume with comma separated does not work

[CAMEL-19112](https://issues.apache.org/jira/browse/CAMEL-19112)

Unable to init camel file with JBang for multi dot file name suffix - eg 'foo.camel.yaml'

[CAMEL-19111](https://issues.apache.org/jira/browse/CAMEL-19111)

Yaml DSL does not seem to work with split/xtokenize

[CAMEL-19103](https://issues.apache.org/jira/browse/CAMEL-19103)

camel-jbang - can't run in background due to No Camel integration files to run

[CAMEL-19098](https://issues.apache.org/jira/browse/CAMEL-19098)

Possible performance issue invoking a bean method with a string parameter

[CAMEL-19081](https://issues.apache.org/jira/browse/CAMEL-19081)

Start a route with aggregation fails due to NPE in AggregateProcessor

[CAMEL-19079](https://issues.apache.org/jira/browse/CAMEL-19079)

NullPointerException thrown when using the language:xquery endpoint

[CAMEL-19075](https://issues.apache.org/jira/browse/CAMEL-19075)

camel-bean - Incorrect choice of overloaded method with several arguments, if one of them has brackets.

[CAMEL-19067](https://issues.apache.org/jira/browse/CAMEL-19067)

Camel-JBang | camel init creates file but errors out on Windows

[CAMEL-19066](https://issues.apache.org/jira/browse/CAMEL-19066)

Multicast EIP sets correlationId on original Exchange

[CAMEL-19051](https://issues.apache.org/jira/browse/CAMEL-19051)

Camel-opentelemetry: Avoid using the GlobalOpenTelemetry.get() and allow for injection of ContextPropagators

[CAMEL-19047](https://issues.apache.org/jira/browse/CAMEL-19047)

CamelTestSupport (junit5) - quarkus and springboot checks are not executed with ContextPerClass

[CAMEL-19034](https://issues.apache.org/jira/browse/CAMEL-19034)

Camel-AWS2-S3: GetObject should preserve the metadata

[CAMEL-19026](https://issues.apache.org/jira/browse/CAMEL-19026)

camel-jbang - camel.main.backlogTracing=true

[CAMEL-19018](https://issues.apache.org/jira/browse/CAMEL-19018)

camel-vertx-http: Headers may get erroneously duplicated

[CAMEL-19014](https://issues.apache.org/jira/browse/CAMEL-19014)

SimpleLanguage cache issue

[CAMEL-19006](https://issues.apache.org/jira/browse/CAMEL-19006)

XML IO DSL do not load templatedRoutes without XML namespace

[CAMEL-19004](https://issues.apache.org/jira/browse/CAMEL-19004)

XML IO DSL do not parse route configuration with XML namespace

[CAMEL-19002](https://issues.apache.org/jira/browse/CAMEL-19002)

camel-jbang - Log command should detect lines without timestamp

[CAMEL-18980](https://issues.apache.org/jira/browse/CAMEL-18980)

camel snmp - SNMP Ver1 trap does not work

[CAMEL-18968](https://issues.apache.org/jira/browse/CAMEL-18968)

Camel-aws2-sqs - Queue url might stay empty for the delayed queue.

[CAMEL-18959](https://issues.apache.org/jira/browse/CAMEL-18959)

camel-salesforce: deserialization failure for streaming query response gets swallowed

[CAMEL-18956](https://issues.apache.org/jira/browse/CAMEL-18956)

Camel-Jcache: It's using a bundle of javax-cache-api

[CAMEL-18954](https://issues.apache.org/jira/browse/CAMEL-18954)

camel-micrometer - NPE on spring boot

[CAMEL-18953](https://issues.apache.org/jira/browse/CAMEL-18953)

camel-jetty - Should throw 504 error if continuation timeout was hit

[CAMEL-18944](https://issues.apache.org/jira/browse/CAMEL-18944)

REST YAML does not work in Spring Boot

[CAMEL-18922](https://issues.apache.org/jira/browse/CAMEL-18922)

TemplatedRoute fails to load with XML RouteLoader

[CAMEL-18878](https://issues.apache.org/jira/browse/CAMEL-18878)

Autowiring on endpoint works even if is disabled on component

[CAMEL-18872](https://issues.apache.org/jira/browse/CAMEL-18872)

camel-core-model - Rest DSL param example not available in XML and YAML DSL

[CAMEL-18871](https://issues.apache.org/jira/browse/CAMEL-18871)

camel-netty - Application does not recover (threads are WAITING) when NettyProducer pool is exhausted

[CAMEL-18868](https://issues.apache.org/jira/browse/CAMEL-18868)

Aws2-s3: CreateDownloadLink does not work with useDefaultCredentialsProvider

[CAMEL-18865](https://issues.apache.org/jira/browse/CAMEL-18865)

camel-main - Setters not invoked on bean that implements Map

[CAMEL-18856](https://issues.apache.org/jira/browse/CAMEL-18856)

camel-main - Unable to declare java.util.List bean

[CAMEL-18854](https://issues.apache.org/jira/browse/CAMEL-18854)

camel-rabbitmq x-queue-type no longer working

[CAMEL-18844](https://issues.apache.org/jira/browse/CAMEL-18844)

Possible memory leak in org.apache.camel.impl.console.EventConsole

[CAMEL-18842](https://issues.apache.org/jira/browse/CAMEL-18842)

camel-as2 failed to serve signed requests when compression is done before signing

[CAMEL-18841](https://issues.apache.org/jira/browse/CAMEL-18841)

camel-kafka: producer idempotence is not enabled by default

[CAMEL-18840](https://issues.apache.org/jira/browse/CAMEL-18840)

camel-http - HTTP broken followRedirection

[CAMEL-18834](https://issues.apache.org/jira/browse/CAMEL-18834)

camel-core - StringQuoteHelper should remove quotes for single element

[CAMEL-18780](https://issues.apache.org/jira/browse/CAMEL-18780)

Sqs2Consumer message extended causing rejected execution exception when used with threads EIP

[CAMEL-18619](https://issues.apache.org/jira/browse/CAMEL-18619)

Stream closed for onException with useOriginalMessage

[CAMEL-18234](https://issues.apache.org/jira/browse/CAMEL-18234)

Exception building aws2-sqs route when certificate validation is disabled and a proxy is configured

[CAMEL-17544](https://issues.apache.org/jira/browse/CAMEL-17544)

ServicePool.doStop still hangs during shutdown

[CAMEL-15111](https://issues.apache.org/jira/browse/CAMEL-15111)

camel-as2 component failed to parse entity content for encrypted or compressed data

[CAMEL-14008](https://issues.apache.org/jira/browse/CAMEL-14008)

camel-as2 - AS2 Connection can only handle one connection (connection recovery needed)

### Dependency upgrade (96)

[CAMEL-19661](https://issues.apache.org/jira/browse/CAMEL-19661)

camel-kafka - Upgrade to Kafka 3.5.1

[CAMEL-19658](https://issues.apache.org/jira/browse/CAMEL-19658)

camel-kubernetes - Upgrade to 6.8.x

[CAMEL-19654](https://issues.apache.org/jira/browse/CAMEL-19654)

camel-corda - Deprecate in 3.x and remove in v4

[CAMEL-19637](https://issues.apache.org/jira/browse/CAMEL-19637)

camel-tooling-maven - Upgrade to maven 3.9.4 and maven-resolver 1.9.14

[CAMEL-19626](https://issues.apache.org/jira/browse/CAMEL-19626)

camel-google - Upgrade from 1.32.x to 2.x

[CAMEL-19625](https://issues.apache.org/jira/browse/CAMEL-19625)

maven - Upgrade to plexus-utils 4.x

[CAMEL-19624](https://issues.apache.org/jira/browse/CAMEL-19624)

Upgrade Derby used for testing

[CAMEL-19618](https://issues.apache.org/jira/browse/CAMEL-19618)

camel-box - Upgrade to v4

[CAMEL-19614](https://issues.apache.org/jira/browse/CAMEL-19614)

camel-openapi-rest-dsl-generator - Upgrade apicurio-data-models

[CAMEL-19612](https://issues.apache.org/jira/browse/CAMEL-19612)

camel-arangodb - Upgrade to 7.x

[CAMEL-19606](https://issues.apache.org/jira/browse/CAMEL-19606)

camel-spring-boot - Upgrade to 3.1.2

[CAMEL-19605](https://issues.apache.org/jira/browse/CAMEL-19605)

camel-xchange - Upgrade to xchange 5.1.0

[CAMEL-19597](https://issues.apache.org/jira/browse/CAMEL-19597)

Upgrade dependencies before 4.0 GA

[CAMEL-19596](https://issues.apache.org/jira/browse/CAMEL-19596)

camel-javascript - Upgrade to graalvm 23.0

[CAMEL-19595](https://issues.apache.org/jira/browse/CAMEL-19595)

camel-kotlin - Upgrade to 1.9

[CAMEL-19594](https://issues.apache.org/jira/browse/CAMEL-19594)

camel-jbang - Upgrade to hawtio 2.17.5

[CAMEL-19581](https://issues.apache.org/jira/browse/CAMEL-19581)

camel-jbang - Upgrade to picocli 4.7.4

[CAMEL-19572](https://issues.apache.org/jira/browse/CAMEL-19572)

Camel-Google-Cloud components: Upgrade to a new Libraries BOM

[CAMEL-19507](https://issues.apache.org/jira/browse/CAMEL-19507)

Upgrade Wildfly Elytron to version 1.20.4.Final

[CAMEL-19506](https://issues.apache.org/jira/browse/CAMEL-19506)

Upgrade Huawei-cloud SDK core and related to 3.1.45

[CAMEL-19505](https://issues.apache.org/jira/browse/CAMEL-19505)

Upgrade Azure SDK BOM to version 1.2.14

[CAMEL-19490](https://issues.apache.org/jira/browse/CAMEL-19490)

camel-elasticsearch - Upgrade to 8.8.x

[CAMEL-19485](https://issues.apache.org/jira/browse/CAMEL-19485)

camel-debezium - Upgrade to 2.3

[CAMEL-19480](https://issues.apache.org/jira/browse/CAMEL-19480)

camel-netty - Upgrade to 4.1.94

[CAMEL-19472](https://issues.apache.org/jira/browse/CAMEL-19472)

camel-spring-boot - Upgrade to 3.1.1

[CAMEL-19468](https://issues.apache.org/jira/browse/CAMEL-19468)

camel-xslt-saxon - Upgrade to Saxon-HE 12.2

[CAMEL-19464](https://issues.apache.org/jira/browse/CAMEL-19464)

camel-kafka - Upgrade to 3.5.x

[CAMEL-19460](https://issues.apache.org/jira/browse/CAMEL-19460)

upgrade to apache 30

[CAMEL-19458](https://issues.apache.org/jira/browse/CAMEL-19458)

Bouncycastle 1.73 to 1.74

[CAMEL-19451](https://issues.apache.org/jira/browse/CAMEL-19451)

Import grpc-bom to build and test with a single deterministic set of gRPC dependencies

[CAMEL-19448](https://issues.apache.org/jira/browse/CAMEL-19448)

camel-jackson - Upgrade to 2.15.2

[CAMEL-19442](https://issues.apache.org/jira/browse/CAMEL-19442)

Manage Gson to build and test with a single deterministic version

[CAMEL-19440](https://issues.apache.org/jira/browse/CAMEL-19440)

Manage caffeine to build and test with a single deterministic version

[CAMEL-19439](https://issues.apache.org/jira/browse/CAMEL-19439)

Import jackson-bom to build and test with a single deterministic set of jackson dependencies

[CAMEL-19424](https://issues.apache.org/jira/browse/CAMEL-19424)

Upgrade MicroProfile component versions

[CAMEL-19407](https://issues.apache.org/jira/browse/CAMEL-19407)

camel-kubernetes - Upgrade to 6.7.x

[CAMEL-19389](https://issues.apache.org/jira/browse/CAMEL-19389)

camel-cxf - Upgrade to 4.0.2

[CAMEL-19348](https://issues.apache.org/jira/browse/CAMEL-19348)

camel-tracing - Upgrade to 1.11.0

[CAMEL-19347](https://issues.apache.org/jira/browse/CAMEL-19347)

camel-spring-boot- Upgrade to 3.1.0

[CAMEL-19317](https://issues.apache.org/jira/browse/CAMEL-19317)

camel-kubernetes - Upgrade to 6.6.x

[CAMEL-19301](https://issues.apache.org/jira/browse/CAMEL-19301)

camel-jbang - Upgrade to hawtio 2.17.2

[CAMEL-19300](https://issues.apache.org/jira/browse/CAMEL-19300)

camel-pulsar - Upgrade to 2.11.1

[CAMEL-19288](https://issues.apache.org/jira/browse/CAMEL-19288)

camel-jsonpath - Upgrade to 2.8

[CAMEL-19287](https://issues.apache.org/jira/browse/CAMEL-19287)

camel-debezium - Upgrade to 2.2

[CAMEL-19278](https://issues.apache.org/jira/browse/CAMEL-19278)

camel-xslt-saxon - Upgrade to Saxon-HE 11.5

[CAMEL-19274](https://issues.apache.org/jira/browse/CAMEL-19274)

camel-spring-ldap - Upgrade to spring ldap 3.0.x

[CAMEL-19268](https://issues.apache.org/jira/browse/CAMEL-19268)

camel-spring-boot - Upgrade to 3.0.6

[CAMEL-19265](https://issues.apache.org/jira/browse/CAMEL-19265)

camel-jbang - Upgrade to Picoli 4.7.2

[CAMEL-19261](https://issues.apache.org/jira/browse/CAMEL-19261)

camel-jbang - Upgrade gradle wrapper to 8.x

[CAMEL-19246](https://issues.apache.org/jira/browse/CAMEL-19246)

camel-kotlin - Upgrade to 1.8.20

[CAMEL-19206](https://issues.apache.org/jira/browse/CAMEL-19206)

camel-undertow - Upgrade to 2.3.5

[CAMEL-19191](https://issues.apache.org/jira/browse/CAMEL-19191)

Use 5.1.x version to be compatible with SB

[CAMEL-19175](https://issues.apache.org/jira/browse/CAMEL-19175)

camel-kubernetes - Upgrade to 6.5.1

[CAMEL-19141](https://issues.apache.org/jira/browse/CAMEL-19141)

camel-core - Upgrade to log4j 2.20.x

[CAMEL-19134](https://issues.apache.org/jira/browse/CAMEL-19134)

camel-kubernetes - Upgrade to 6.5.x

[CAMEL-19131](https://issues.apache.org/jira/browse/CAMEL-19131)

Camel-DJL: Upgrade to Deep Java Library 0.21.0

[CAMEL-19130](https://issues.apache.org/jira/browse/CAMEL-19130)

Upgrade to snakeyaml 2.x

[CAMEL-19126](https://issues.apache.org/jira/browse/CAMEL-19126)

camel-fhir upgrade to 6.4.2

[CAMEL-19123](https://issues.apache.org/jira/browse/CAMEL-19123)

camel-jbang - upgrade maven-resolver to 1.9.7

[CAMEL-19110](https://issues.apache.org/jira/browse/CAMEL-19110)

camel-spring-boot - Upgrade to 3.0.4

[CAMEL-19092](https://issues.apache.org/jira/browse/CAMEL-19092)

camel-jbang - upgrade maven-resolver-api to 1.9.5

[CAMEL-19059](https://issues.apache.org/jira/browse/CAMEL-19059)

camel-snmp - Use original JAR instead of SMX wrap

[CAMEL-19039](https://issues.apache.org/jira/browse/CAMEL-19039)

camel-jms - Upgrade to Artemis 2.28.x

[CAMEL-19019](https://issues.apache.org/jira/browse/CAMEL-19019)

camel-kafka - Upgrade to Kafka 3.4.x

[CAMEL-19005](https://issues.apache.org/jira/browse/CAMEL-19005)

Update PubNub to 6.x

[CAMEL-19003](https://issues.apache.org/jira/browse/CAMEL-19003)

Avoid using old guava versions

[CAMEL-18999](https://issues.apache.org/jira/browse/CAMEL-18999)

camel-sshd - Upgrade to 2.9.x

[CAMEL-18997](https://issues.apache.org/jira/browse/CAMEL-18997)

camel-mina - Upgrade to 2.2.1

[CAMEL-18994](https://issues.apache.org/jira/browse/CAMEL-18994)

Huawei Cloud SDK: Bump to 3.1.x

[CAMEL-18993](https://issues.apache.org/jira/browse/CAMEL-18993)

camel-qpid - Upgrade to 2.2 and 9.0 broker

[CAMEL-18987](https://issues.apache.org/jira/browse/CAMEL-18987)

camel-zookeeper - Upgrade to 3.8.x

[CAMEL-18974](https://issues.apache.org/jira/browse/CAMEL-18974)

downgrade pulsar version to 2.10.3

[CAMEL-18961](https://issues.apache.org/jira/browse/CAMEL-18961)

change sun-mail to angus-mail

[CAMEL-18958](https://issues.apache.org/jira/browse/CAMEL-18958)

camel-kubernetes - upgrade to 6.4.x

[CAMEL-18946](https://issues.apache.org/jira/browse/CAMEL-18946)

camel-spring-boot - Upgrade to 3.0.2

[CAMEL-18945](https://issues.apache.org/jira/browse/CAMEL-18945)

Upgrade rest assured

[CAMEL-18943](https://issues.apache.org/jira/browse/CAMEL-18943)

camel-xslt-saxon - Upgrade to Saxon-HE 12.0

[CAMEL-18924](https://issues.apache.org/jira/browse/CAMEL-18924)

camel-lucene - Upgrade to 9.6.0

[CAMEL-18920](https://issues.apache.org/jira/browse/CAMEL-18920)

camel-groovy - Upgrade to Groovy 4.x

[CAMEL-18915](https://issues.apache.org/jira/browse/CAMEL-18915)

Upgrade fhir component

[CAMEL-18911](https://issues.apache.org/jira/browse/CAMEL-18911)

camel-optaplanner - Upgrade to 9.x in v4

[CAMEL-18903](https://issues.apache.org/jira/browse/CAMEL-18903)

Upgrade swagger-core in camel-openapi-java to support jakarta namespace

[CAMEL-18888](https://issues.apache.org/jira/browse/CAMEL-18888)

Update swagger-codegen-maven-plugin to 3.0.36

[CAMEL-18887](https://issues.apache.org/jira/browse/CAMEL-18887)

camel-kotlin - Upgrade to 1.8

[CAMEL-18880](https://issues.apache.org/jira/browse/CAMEL-18880)

camel-jbang - upgrade maven-resolver-api to 1.9.4

[CAMEL-18843](https://issues.apache.org/jira/browse/CAMEL-18843)

camel-spring-boot - Upgrade to 2.7.7

[CAMEL-18838](https://issues.apache.org/jira/browse/CAMEL-18838)

upgrade to debezium 2.1.x

[CAMEL-18830](https://issues.apache.org/jira/browse/CAMEL-18830)

camel-ehcache - Align to JAXB from camel

[CAMEL-18824](https://issues.apache.org/jira/browse/CAMEL-18824)

upgrade to newer guava versions

[CAMEL-18738](https://issues.apache.org/jira/browse/CAMEL-18738)

camel-resilience4j - Upgrade to 2.x

[CAMEL-18610](https://issues.apache.org/jira/browse/CAMEL-18610)

Support Debezium 2.0

[CAMEL-18463](https://issues.apache.org/jira/browse/CAMEL-18463)

upgrade grpc to 1.54.x

[CAMEL-18416](https://issues.apache.org/jira/browse/CAMEL-18416)

Upgrade to slf4j 2.0

[CAMEL-18341](https://issues.apache.org/jira/browse/CAMEL-18341)

Upgrade from Codehaus Groovy 3.0.12 to Apache Groovy 4.x

[CAMEL-17887](https://issues.apache.org/jira/browse/CAMEL-17887)

Groovy 4.0 support

[CAMEL-17136](https://issues.apache.org/jira/browse/CAMEL-17136)

Upgrade to Jarkarta EE APIs

### Improvement (219)

[CAMEL-19721](https://issues.apache.org/jira/browse/CAMEL-19721)

camel-activemq - ActiveMQ component should use jakarta based connection pool

[CAMEL-19714](https://issues.apache.org/jira/browse/CAMEL-19714)

camel-jsonpath: Consider removing json-smart exclusion

[CAMEL-19710](https://issues.apache.org/jira/browse/CAMEL-19710)

camel-jbang - Run should compile java to default package if project has GAV

[CAMEL-19709](https://issues.apache.org/jira/browse/CAMEL-19709)

\[yaml dsl\] include additional information such as description and title in the jscon schema

[CAMEL-19708](https://issues.apache.org/jira/browse/CAMEL-19708)

camel-jbang - Export - Add support for jkube resource fragments

[CAMEL-19705](https://issues.apache.org/jira/browse/CAMEL-19705)

camel-main - Support a list of known FQN for fast packageScan

[CAMEL-19696](https://issues.apache.org/jira/browse/CAMEL-19696)

camel-main - Export should be able to have platform-http-main for health-check / console

[CAMEL-19694](https://issues.apache.org/jira/browse/CAMEL-19694)

camel-jbang - Export - Add option to not move java source into sub package

[CAMEL-19692](https://issues.apache.org/jira/browse/CAMEL-19692)

camel-vertx-websocket: Improve producer sendToAll handling of parameterized server paths

[CAMEL-19691](https://issues.apache.org/jira/browse/CAMEL-19691)

camel-kafka - Allow sslKeystorePassword to be blank

[CAMEL-19690](https://issues.apache.org/jira/browse/CAMEL-19690)

camel-salesforce: Generated DTOs are sometimes invalid with v55+

[CAMEL-19689](https://issues.apache.org/jira/browse/CAMEL-19689)

camel-jbang: Support loading data XML file

[CAMEL-19682](https://issues.apache.org/jira/browse/CAMEL-19682)

camel-core - Poll Enrich EIP should set TO\_ENDPOINT as exchange property and not header

[CAMEL-19677](https://issues.apache.org/jira/browse/CAMEL-19677)

camel-mllp - support more MLLP charsets

[CAMEL-19673](https://issues.apache.org/jira/browse/CAMEL-19673)

camel-aws - Polish label on configurations

[CAMEL-19662](https://issues.apache.org/jira/browse/CAMEL-19662)

camel-bindy - Add option to @CsvRecord for trimeLine true or false

[CAMEL-19660](https://issues.apache.org/jira/browse/CAMEL-19660)

camel-mapstruct: Improve support for Mappers defined as abstract classes

[CAMEL-19651](https://issues.apache.org/jira/browse/CAMEL-19651)

camel-kafka - Use default partitioning logic as the default

[CAMEL-19647](https://issues.apache.org/jira/browse/CAMEL-19647)

camel-platform-http-main - Use 503 for health check DOWN

[CAMEL-19645](https://issues.apache.org/jira/browse/CAMEL-19645)

health check - Should we enable producer based health check for AWS

[CAMEL-19641](https://issues.apache.org/jira/browse/CAMEL-19641)

camel-file-watch - Events options should be tooling friendly

[CAMEL-19627](https://issues.apache.org/jira/browse/CAMEL-19627)

paho-mqtt5: Allow password to be optional if username is provided

[CAMEL-19616](https://issues.apache.org/jira/browse/CAMEL-19616)

camel-restdsl-openapi-plugin - Do not use servlet as component by default

[CAMEL-19615](https://issues.apache.org/jira/browse/CAMEL-19615)

camel-ftp: chmodDirectory option try for each junk to change the directory permission and fails

[CAMEL-19602](https://issues.apache.org/jira/browse/CAMEL-19602)

components - Add metadata for an option that refers to a file resource for tooling

[CAMEL-19592](https://issues.apache.org/jira/browse/CAMEL-19592)

camel-jbang - Export to camel-main should include platform-http for rest-dsl

[CAMEL-19588](https://issues.apache.org/jira/browse/CAMEL-19588)

camel-jbang - Starting via jbang --verbose should output more details on startup

[CAMEL-19587](https://issues.apache.org/jira/browse/CAMEL-19587)

camel-jira: optional header field IssueAssignee doesn't work

[CAMEL-19586](https://issues.apache.org/jira/browse/CAMEL-19586)

camel-parquet-avro - Allow users to unmarshal Parquet file into Avro's GenericRecords

[CAMEL-19585](https://issues.apache.org/jira/browse/CAMEL-19585)

camel-jbang - Report if dependency was downloaded or resolved

[CAMEL-19583](https://issues.apache.org/jira/browse/CAMEL-19583)

Lack of multiple shards consumption of Camel aws2 Kinesis

[CAMEL-19580](https://issues.apache.org/jira/browse/CAMEL-19580)

camel-catalog-maven - Add getClassLoader API

[CAMEL-19574](https://issues.apache.org/jira/browse/CAMEL-19574)

Upgrade to Pulsar 3.0.0

[CAMEL-19573](https://issues.apache.org/jira/browse/CAMEL-19573)

Stop syncing version properties in git, generate the effective camel-dependencies during the build

[CAMEL-19571](https://issues.apache.org/jira/browse/CAMEL-19571)

camel-parquet-avro: Add other compression codecs than gzip

[CAMEL-19564](https://issues.apache.org/jira/browse/CAMEL-19564)

xml-io-dsl: Allow routes to use beans loaded directly from source

[CAMEL-19560](https://issues.apache.org/jira/browse/CAMEL-19560)

Manage micrometer artifacts to build and test with a single deterministic set of versions

[CAMEL-19559](https://issues.apache.org/jira/browse/CAMEL-19559)

Manage commons-codec to build and test with a single deterministic version

[CAMEL-19558](https://issues.apache.org/jira/browse/CAMEL-19558)

Manage protobuf to build and test with a single deterministic version

[CAMEL-19508](https://issues.apache.org/jira/browse/CAMEL-19508)

Add possibility to supply custom headers in LRAClient requests

[CAMEL-19502](https://issues.apache.org/jira/browse/CAMEL-19502)

netty4-http - allow SSL SNI to be set using SSLContextClientParameters

[CAMEL-19496](https://issues.apache.org/jira/browse/CAMEL-19496)

Manage single version of Guava

[CAMEL-19479](https://issues.apache.org/jira/browse/CAMEL-19479)

camel-core - Add threadId as function to simple language

[CAMEL-19478](https://issues.apache.org/jira/browse/CAMEL-19478)

camel-core - Add synchronous option to some EIPs like split

[CAMEL-19477](https://issues.apache.org/jira/browse/CAMEL-19477)

MeterRegistry collects authorization data

[CAMEL-19471](https://issues.apache.org/jira/browse/CAMEL-19471)

camel-yaml-dsl - JSON library enum consistency

[CAMEL-19467](https://issues.apache.org/jira/browse/CAMEL-19467)

should servlet and rest throw exceptions when duplicate and ambiguous paths occur

[CAMEL-19466](https://issues.apache.org/jira/browse/CAMEL-19466)

Skip Maven mojos in the fast profile properly

[CAMEL-19456](https://issues.apache.org/jira/browse/CAMEL-19456)

The invocation of the removeRoute() method is too slow when using RAW().

[CAMEL-19455](https://issues.apache.org/jira/browse/CAMEL-19455)

camel-cxf - Ensure REQUEST\_CONTEXT & RESPONSE\_CONTEXT headers are Map when populating CXF Message from Camel Message

[CAMEL-19454](https://issues.apache.org/jira/browse/CAMEL-19454)

camel-jbang - Export should support --open-api

[CAMEL-19453](https://issues.apache.org/jira/browse/CAMEL-19453)

camel-jbang - Run with --open-api to support yaml spec files

[CAMEL-19449](https://issues.apache.org/jira/browse/CAMEL-19449)

camel-yaml-io - YAML dumper configure if uri should be expanded into parameters

[CAMEL-19435](https://issues.apache.org/jira/browse/CAMEL-19435)

camel-core - Remove String -> File converter

[CAMEL-19423](https://issues.apache.org/jira/browse/CAMEL-19423)

camel-jira - Do not have file converter

[CAMEL-19417](https://issues.apache.org/jira/browse/CAMEL-19417)

camel-spring-rabbitmq - convert all message properties by default

[CAMEL-19414](https://issues.apache.org/jira/browse/CAMEL-19414)

camel-core - IOConverter from File to Path

[CAMEL-19396](https://issues.apache.org/jira/browse/CAMEL-19396)

camel-management - Add DoCatch and DoFinally as managed processors

[CAMEL-19380](https://issues.apache.org/jira/browse/CAMEL-19380)

camel-core - CamelContext should use plugin for RuntimeConfiguration

[CAMEL-19379](https://issues.apache.org/jira/browse/CAMEL-19379)

EndpointSchemaGeneratorMojo: Improve "Could not find component java type" error message

[CAMEL-19378](https://issues.apache.org/jira/browse/CAMEL-19378)

File Changed ReadLock Strategy with minAge only looks for lastModified

[CAMEL-19377](https://issues.apache.org/jira/browse/CAMEL-19377)

camel-platform-http - Return 503 if consumer is suspended

[CAMEL-19370](https://issues.apache.org/jira/browse/CAMEL-19370)

camel-jbang - Make it possible to show full url for very long endpoints

[CAMEL-19369](https://issues.apache.org/jira/browse/CAMEL-19369)

camel-jbang - Trace command to have endpoint URI information

[CAMEL-19368](https://issues.apache.org/jira/browse/CAMEL-19368)

camel-main - Auto detect custom EventNotifer from registry

[CAMEL-19366](https://issues.apache.org/jira/browse/CAMEL-19366)

camel-core - Trigger reload via dev console make it async

[CAMEL-19362](https://issues.apache.org/jira/browse/CAMEL-19362)

camel-core - Tracing without inner details of Kamelets

[CAMEL-19361](https://issues.apache.org/jira/browse/CAMEL-19361)

camel-jbang - Parse trait.camel.apache.org/camel.properties from KameletBinding

[CAMEL-19360](https://issues.apache.org/jira/browse/CAMEL-19360)

camel-jbang - Export a set of files

[CAMEL-19357](https://issues.apache.org/jira/browse/CAMEL-19357)

camel-jbang - Use a vertx task for tasks to avoid blocking io thread

[CAMEL-19354](https://issues.apache.org/jira/browse/CAMEL-19354)

camel-mybatis - Autowired sql connection factory

[CAMEL-19353](https://issues.apache.org/jira/browse/CAMEL-19353)

Camel-Jbang reload exception

[CAMEL-19352](https://issues.apache.org/jira/browse/CAMEL-19352)

Improve camel-mybatis documentation

[CAMEL-19350](https://issues.apache.org/jira/browse/CAMEL-19350)

camel-jpa: Output into header/property

[CAMEL-19337](https://issues.apache.org/jira/browse/CAMEL-19337)

camel-core-model - doTry and circuitBreaker outputs fix model

[CAMEL-19336](https://issues.apache.org/jira/browse/CAMEL-19336)

camel-core-model - EIP model json should have index order for properties

[CAMEL-19333](https://issues.apache.org/jira/browse/CAMEL-19333)

ensure cxf springboot autoconfiguration works OOTB in camel-cxf springboot starters

[CAMEL-19332](https://issues.apache.org/jira/browse/CAMEL-19332)

Prevent regen job from deletion of tabs-sync asiidoc attibute

[CAMEL-19331](https://issues.apache.org/jira/browse/CAMEL-19331)

camel-jbang - camel stop - should stop if there is only 1 running

[CAMEL-19330](https://issues.apache.org/jira/browse/CAMEL-19330)

camel-xml-io - Dump model for Choice should have otherwise last

[CAMEL-19327](https://issues.apache.org/jira/browse/CAMEL-19327)

camel-jpa: Single result

[CAMEL-19326](https://issues.apache.org/jira/browse/CAMEL-19326)

camel-jbang - Register reload services eager

[CAMEL-19324](https://issues.apache.org/jira/browse/CAMEL-19324)

Be able to convert all elements from CXF MessageContentsList.class to String.class if not in "CXF Context"

[CAMEL-19322](https://issues.apache.org/jira/browse/CAMEL-19322)

camel-jbang - Source Dir to support application.properties

[CAMEL-19313](https://issues.apache.org/jira/browse/CAMEL-19313)

camel-jbang - Provide a way to append Maven repository provided from command-line to the one provided in configuration

[CAMEL-19311](https://issues.apache.org/jira/browse/CAMEL-19311)

Review the SimpleLRUCache to become thread-safe

[CAMEL-19306](https://issues.apache.org/jira/browse/CAMEL-19306)

camel-jbang - Allow to load yaml files with beans only

[CAMEL-19302](https://issues.apache.org/jira/browse/CAMEL-19302)

Use filename to generate id of route when creating Camel file in XML DSL with Camel JBang

[CAMEL-19286](https://issues.apache.org/jira/browse/CAMEL-19286)

camel-ignite - Support the REPLACE operation in the Ignite Cache Producer

[CAMEL-19276](https://issues.apache.org/jira/browse/CAMEL-19276)

camel-jq: Include jackson-jq extras module

[CAMEL-19272](https://issues.apache.org/jira/browse/CAMEL-19272)

camel-jbang - Show jbang version

[CAMEL-19269](https://issues.apache.org/jira/browse/CAMEL-19269)

camel-jackson - Converter for jackson numeric wrappers

[CAMEL-19245](https://issues.apache.org/jira/browse/CAMEL-19245)

camel-java-joor-dsl - Ease the way to get all the compiled classes

[CAMEL-19244](https://issues.apache.org/jira/browse/CAMEL-19244)

camel-bean - Add signature parameter to specify parameter types

[CAMEL-19239](https://issues.apache.org/jira/browse/CAMEL-19239)

camel-vertx-websocket: Add options for configuring the origin header

[CAMEL-19238](https://issues.apache.org/jira/browse/CAMEL-19238)

camel-vertx-websocket: Apply default port when the wss scheme is used

[CAMEL-19237](https://issues.apache.org/jira/browse/CAMEL-19237)

camel-jbang - version list for newer releases to include details

[CAMEL-19235](https://issues.apache.org/jira/browse/CAMEL-19235)

camel-restdsl-openapi-plugin: Add platform-http to REST consumer components list

[CAMEL-19234](https://issues.apache.org/jira/browse/CAMEL-19234)

camel-core - When looking up a mandatory bean, look it up through its type first

[CAMEL-19232](https://issues.apache.org/jira/browse/CAMEL-19232)

Port REST DSL Generator in camel-jbang to Camel 4

[CAMEL-19231](https://issues.apache.org/jira/browse/CAMEL-19231)

Default REST DSL type in camel-jbang generator

[CAMEL-19227](https://issues.apache.org/jira/browse/CAMEL-19227)

camel-jbang - export should also add <pluginRepository> with repos

[CAMEL-19226](https://issues.apache.org/jira/browse/CAMEL-19226)

camel-jbang - Add repos option to export

[CAMEL-19225](https://issues.apache.org/jira/browse/CAMEL-19225)

camel-jpa: remove transactionManager property

[CAMEL-19223](https://issues.apache.org/jira/browse/CAMEL-19223)

camel-core - StreamCache to have position method

[CAMEL-19219](https://issues.apache.org/jira/browse/CAMEL-19219)

camel-kudu - add projection and limit support to the scan operation

[CAMEL-19216](https://issues.apache.org/jira/browse/CAMEL-19216)

camel-kudu - add predicate support to the scan operation

[CAMEL-19214](https://issues.apache.org/jira/browse/CAMEL-19214)

camel-hdfs - Add ShortWritable support to the HDFS component

[CAMEL-19211](https://issues.apache.org/jira/browse/CAMEL-19211)

camel-sql - Make it possible to configure custom RowMapper

[CAMEL-19210](https://issues.apache.org/jira/browse/CAMEL-19210)

camel-pulsar - Support for delayed delivery pulsar messages using deliverAt

[CAMEL-19205](https://issues.apache.org/jira/browse/CAMEL-19205)

camel-plc4x - Make it easier to configure tags in endpoint

[CAMEL-19197](https://issues.apache.org/jira/browse/CAMEL-19197)

camel-cxf-starter - Spring Boot starter for CXF should use -spring JARs

[CAMEL-19193](https://issues.apache.org/jira/browse/CAMEL-19193)

Change default Micrometer meter names to follow Micrometer naming conventions

[CAMEL-19187](https://issues.apache.org/jira/browse/CAMEL-19187)

camel-jbang - dependency list should use user configured version

[CAMEL-19186](https://issues.apache.org/jira/browse/CAMEL-19186)

camel-core - Type function in simple language should use enum type instead of toString value

[CAMEL-19185](https://issues.apache.org/jira/browse/CAMEL-19185)

Camel Spring Boot Example: Twitter-Salesforce: camel-salesforce-maven-plugin - make TLS version configurable via system properties

[CAMEL-19180](https://issues.apache.org/jira/browse/CAMEL-19180)

Kafka Idempotent Repository does not give the user control over a randomized group id if the kafka broker requires the id to be in a specified form

[CAMEL-19178](https://issues.apache.org/jira/browse/CAMEL-19178)

camel-common-http - Make HttpBinding more reusable

[CAMEL-19177](https://issues.apache.org/jira/browse/CAMEL-19177)

camel-platform-http - Spring Boot implementation that use directly the HTTP server

[CAMEL-19176](https://issues.apache.org/jira/browse/CAMEL-19176)

camel-platform-http - Add listener for added/removed http endpoints

[CAMEL-19173](https://issues.apache.org/jira/browse/CAMEL-19173)

Splitting long uris in xml-io DSL doesn't work

[CAMEL-19168](https://issues.apache.org/jira/browse/CAMEL-19168)

camel-micrometer-starter - Make it possible to capture static uri path as tag

[CAMEL-19152](https://issues.apache.org/jira/browse/CAMEL-19152)

camel-azure - Add file client header and flush option

[CAMEL-19145](https://issues.apache.org/jira/browse/CAMEL-19145)

camel-jbang - Add known alias for maven repos

[CAMEL-19144](https://issues.apache.org/jira/browse/CAMEL-19144)

camel-catalog - Include information about existing Camel releases

[CAMEL-19137](https://issues.apache.org/jira/browse/CAMEL-19137)

Favor CompositeMeterRegistry instances in Camel registry

[CAMEL-19135](https://issues.apache.org/jira/browse/CAMEL-19135)

components - Reduce number of different Category

[CAMEL-19132](https://issues.apache.org/jira/browse/CAMEL-19132)

camel-core - Deprecate vm and direct-vm and remove in v4

[CAMEL-19122](https://issues.apache.org/jira/browse/CAMEL-19122)

camel-jbang - Export java code with existing package name

[CAMEL-19121](https://issues.apache.org/jira/browse/CAMEL-19121)

camel-jbang - Adapt to Camel v4

[CAMEL-19118](https://issues.apache.org/jira/browse/CAMEL-19118)

camel-health - Liveness check default false

[CAMEL-19109](https://issues.apache.org/jira/browse/CAMEL-19109)

camel-vertx-websocket: Consumer should avoid blocking the Vert.x event loop

[CAMEL-19108](https://issues.apache.org/jira/browse/CAMEL-19108)

camel-jbang - Export with local JAR should include the JAR in lib folder and add as dependency

[CAMEL-19104](https://issues.apache.org/jira/browse/CAMEL-19104)

camel-bean - Move parameter type matching to a new parameterTypes option

[CAMEL-19101](https://issues.apache.org/jira/browse/CAMEL-19101)

Features for Camel-Micrometer

[CAMEL-19094](https://issues.apache.org/jira/browse/CAMEL-19094)

Tokenizer ignores includeTokens

[CAMEL-19093](https://issues.apache.org/jira/browse/CAMEL-19093)

camel-jbang - Run local JAR should add to classpath so can be used in Java DSL

[CAMEL-19089](https://issues.apache.org/jira/browse/CAMEL-19089)

camel-core - Remove ExchangePattern.InOptionalOut

[CAMEL-19087](https://issues.apache.org/jira/browse/CAMEL-19087)

camel-jbang - Trace to have pretty option

[CAMEL-19083](https://issues.apache.org/jira/browse/CAMEL-19083)

camel-yaml-dsl: Add a doc section that links to the schema

[CAMEL-19078](https://issues.apache.org/jira/browse/CAMEL-19078)

camel-platform-http-vertx: Allow response headers with empty values to be returned

[CAMEL-19076](https://issues.apache.org/jira/browse/CAMEL-19076)

camel-jbang - Tracer to have option to show also internal exchange properties

[CAMEL-19073](https://issues.apache.org/jira/browse/CAMEL-19073)

camel-core - Properties component - reload properties for only changed

[CAMEL-19072](https://issues.apache.org/jira/browse/CAMEL-19072)

camel-yaml-dsl - Remove backwards compatible 3.15 parser

[CAMEL-19071](https://issues.apache.org/jira/browse/CAMEL-19071)

camel-jbang - Reload all routes in changes to application.properties in dev mode

[CAMEL-19064](https://issues.apache.org/jira/browse/CAMEL-19064)

Camel-Freemarker: Do not set DEFAULT\_INCOMPATIBLE\_IMPROVEMENTS in the Freemarker configuration

[CAMEL-19063](https://issues.apache.org/jira/browse/CAMEL-19063)

Find a replacement library for abdera & axiom in camel-atom & camel-rss

[CAMEL-19055](https://issues.apache.org/jira/browse/CAMEL-19055)

camel-core - Backlog tracer capture thread id of the processed exchange

[CAMEL-19043](https://issues.apache.org/jira/browse/CAMEL-19043)

camel-core - Add Exchange.RECEIVED\_TIMESTAMP as internal exchange property

[CAMEL-19042](https://issues.apache.org/jira/browse/CAMEL-19042)

camel-quarkus-catalog - Uses 0.0.1 version

[CAMEL-19040](https://issues.apache.org/jira/browse/CAMEL-19040)

camel-core - Backlog tracer to capture exception and exchange properties

[CAMEL-19025](https://issues.apache.org/jira/browse/CAMEL-19025)

camel-jbang - doc command should be case insensitive in filter

[CAMEL-19017](https://issues.apache.org/jira/browse/CAMEL-19017)

camel-main - Tracing to output message headers

[CAMEL-19008](https://issues.apache.org/jira/browse/CAMEL-19008)

spring-rabbitmq component does not fail on sending to non-existent RabbitMQ topic

[CAMEL-18992](https://issues.apache.org/jira/browse/CAMEL-18992)

Health Check: Provide a way to disable health check on specific component/producer/consumers

[CAMEL-18990](https://issues.apache.org/jira/browse/CAMEL-18990)

camel-jbang - Export to Quarkus should add resources for native compilation

[CAMEL-18986](https://issues.apache.org/jira/browse/CAMEL-18986)

camel-core - ProducerTemplate send exchange should set from endpoint if null

[CAMEL-18983](https://issues.apache.org/jira/browse/CAMEL-18983)

camel-jbang - Automatic detect atlassian maven repo when using camel-jira

[CAMEL-18979](https://issues.apache.org/jira/browse/CAMEL-18979)

Add delimiter and prefix to the listObjects operation of AWS S3 Producer

[CAMEL-18967](https://issues.apache.org/jira/browse/CAMEL-18967)

camel-platform-http-vertx: Improve handling of whether an HTTP request body is allowed or not

[CAMEL-18963](https://issues.apache.org/jira/browse/CAMEL-18963)

Support latest version of OpenAPI Specification in Camel openapi components

[CAMEL-18957](https://issues.apache.org/jira/browse/CAMEL-18957)

Create a JUnit 5 extension for the Camel Context

[CAMEL-18952](https://issues.apache.org/jira/browse/CAMEL-18952)

camel-rest - Favour using platform-http if available on classpath

[CAMEL-18951](https://issues.apache.org/jira/browse/CAMEL-18951)

Introducing SBOM generation

[CAMEL-18942](https://issues.apache.org/jira/browse/CAMEL-18942)

openapi-rest-dsl-generator - Copy the description of the path/operation to the generated route

[CAMEL-18923](https://issues.apache.org/jira/browse/CAMEL-18923)

Cannot update a routeconfiguration with a routeloader

[CAMEL-18917](https://issues.apache.org/jira/browse/CAMEL-18917)

camel-as2 - Signature is not validated

[CAMEL-18912](https://issues.apache.org/jira/browse/CAMEL-18912)

Sqs2ConsumerHealthCheck is broken when using injected client

[CAMEL-18877](https://issues.apache.org/jira/browse/CAMEL-18877)

camel-caffeine - Key should be string type

[CAMEL-18875](https://issues.apache.org/jira/browse/CAMEL-18875)

camel-jms - Logging less noisy when temporary reply queue is refreshed

[CAMEL-18874](https://issues.apache.org/jira/browse/CAMEL-18874)

camel-file - When possible, pass the exchange to the exception handler

[CAMEL-18873](https://issues.apache.org/jira/browse/CAMEL-18873)

Camel-Elasticsearch: CertificatePath should be readable through ResourceHelper

[CAMEL-18863](https://issues.apache.org/jira/browse/CAMEL-18863)

camel-pulsar - Support chunking to enable sending a large message

[CAMEL-18861](https://issues.apache.org/jira/browse/CAMEL-18861)

Improving PLC4X component

[CAMEL-18857](https://issues.apache.org/jira/browse/CAMEL-18857)

camel-core - Auto assigned route ids for kamelets/templates should use tempate name as prefix

[CAMEL-18852](https://issues.apache.org/jira/browse/CAMEL-18852)

camel-atom/camel-rss - Deprecate basic auth

[CAMEL-18850](https://issues.apache.org/jira/browse/CAMEL-18850)

camel-core-model - @XmlAttributes should be String or Enum type only

[CAMEL-18849](https://issues.apache.org/jira/browse/CAMEL-18849)

camel-core-model - Route properties should be in top of route

[CAMEL-18848](https://issues.apache.org/jira/browse/CAMEL-18848)

camel-core-model - Rest DSL allowedValues should use definition model for value

[CAMEL-18847](https://issues.apache.org/jira/browse/CAMEL-18847)

camel-console - We need a camel-console-support JAR

[CAMEL-18846](https://issues.apache.org/jira/browse/CAMEL-18846)

camel-main - Performance overhead due to emitting events not needed

[CAMEL-18845](https://issues.apache.org/jira/browse/CAMEL-18845)

camel-core - Performance overhead for async processing event emitting

[CAMEL-18832](https://issues.apache.org/jira/browse/CAMEL-18832)

camel-spring-boot - Health Check output should include data in full exposure level

[CAMEL-18828](https://issues.apache.org/jira/browse/CAMEL-18828)

camel-kudu - Add DELETE, UPDATE, and UPSERT support to the producer

[CAMEL-18815](https://issues.apache.org/jira/browse/CAMEL-18815)

camel-jbang - Base package scan to search in downloaded JARs

[CAMEL-18769](https://issues.apache.org/jira/browse/CAMEL-18769)

camel-jbang - Catalog to select runtime

[CAMEL-18752](https://issues.apache.org/jira/browse/CAMEL-18752)

camel-micrometer - Include description in prometheus export

[CAMEL-18747](https://issues.apache.org/jira/browse/CAMEL-18747)

camel-test-infra: investigate upgrading Hadoop images to 3.x

[CAMEL-18744](https://issues.apache.org/jira/browse/CAMEL-18744)

ci: add tests for DSL changes

[CAMEL-18674](https://issues.apache.org/jira/browse/CAMEL-18674)

camel-jbang - Run in background

[CAMEL-18659](https://issues.apache.org/jira/browse/CAMEL-18659)

camel-openapi-java - Support for nullable

[CAMEL-18638](https://issues.apache.org/jira/browse/CAMEL-18638)

Deprecate label property on all annotations in favor of category.

[CAMEL-18636](https://issues.apache.org/jira/browse/CAMEL-18636)

azure data lake component: authentication can not be configured using string properties

[CAMEL-18536](https://issues.apache.org/jira/browse/CAMEL-18536)

camel-joor - Rename joor language to java

[CAMEL-18385](https://issues.apache.org/jira/browse/CAMEL-18385)

camel-kamelet - Endpoint URIs from parameters could be passed as-is without uri encoding

[CAMEL-18326](https://issues.apache.org/jira/browse/CAMEL-18326)

google-mail-stream - message body as raw

[CAMEL-18261](https://issues.apache.org/jira/browse/CAMEL-18261)

Add connection parameters to MongoDB component

[CAMEL-18177](https://issues.apache.org/jira/browse/CAMEL-18177)

camel-slack - Honour Retry-After when requests are rate-limited

[CAMEL-18120](https://issues.apache.org/jira/browse/CAMEL-18120)

camel-jbang - The openapi generator should support generating POJOs

[CAMEL-18078](https://issues.apache.org/jira/browse/CAMEL-18078)

CamelGoogleSheets.valueInputOption not documented for google-sheets://data/append

[CAMEL-17652](https://issues.apache.org/jira/browse/CAMEL-17652)

camel-minio - Auto create bucket should not be done in endpoint

[CAMEL-17528](https://issues.apache.org/jira/browse/CAMEL-17528)

camel-core-model - Description should just be text

[CAMEL-17032](https://issues.apache.org/jira/browse/CAMEL-17032)

camel-jdbc: investigate if resource usage can be improved

[CAMEL-16837](https://issues.apache.org/jira/browse/CAMEL-16837)

Camel-aws2-ddbstream: Batch consumer is not implemented although documentation says that it should be

[CAMEL-16592](https://issues.apache.org/jira/browse/CAMEL-16592)

camel-core - HasCamelContext use it more

[CAMEL-16352](https://issues.apache.org/jira/browse/CAMEL-16352)

Generate JARS without OSGi metadata

[CAMEL-15978](https://issues.apache.org/jira/browse/CAMEL-15978)

camel-xmpp - Upgrade to 1.0.x

[CAMEL-15968](https://issues.apache.org/jira/browse/CAMEL-15968)

Camel-Braintree: Add more Gateway classes

[CAMEL-15762](https://issues.apache.org/jira/browse/CAMEL-15762)

camel-core - Move constants on Exchange to its own class

[CAMEL-15462](https://issues.apache.org/jira/browse/CAMEL-15462)

route coverage report - May report 0 for doCatch even if its in use

[CAMEL-15176](https://issues.apache.org/jira/browse/CAMEL-15176)

Component - Use doInit for wiring instead of doStart (part 2)

[CAMEL-15105](https://issues.apache.org/jira/browse/CAMEL-15105)

camel-core - Extension or getter/setter on ExtendedCamelContext

[CAMEL-14104](https://issues.apache.org/jira/browse/CAMEL-14104)

Update FHIR to latest version

[CAMEL-13635](https://issues.apache.org/jira/browse/CAMEL-13635)

camel3 - Warmup routes and EIPs in init phase

[CAMEL-13611](https://issues.apache.org/jira/browse/CAMEL-13611)

Camel Web3j - Upgrade to Web3j 4.3.1

[CAMEL-13090](https://issues.apache.org/jira/browse/CAMEL-13090)

Update to servlet api 4

[CAMEL-13070](https://issues.apache.org/jira/browse/CAMEL-13070)

sftp incorrectly catches files with filename in Windows-1251 encoding

[CAMEL-11767](https://issues.apache.org/jira/browse/CAMEL-11767)

camel-catalog-maven - Use real maven downloader (was: Maybe use shrinkwrap instead of gradle)

[CAMEL-11567](https://issues.apache.org/jira/browse/CAMEL-11567)

ServiceNow : add suport for Jakarta release

### New Feature (75)

[CAMEL-19726](https://issues.apache.org/jira/browse/CAMEL-19726)

camel-jbang - Run with remote-debug enabled

[CAMEL-19716](https://issues.apache.org/jira/browse/CAMEL-19716)

camel-file - Add option to accept hidden files

[CAMEL-19601](https://issues.apache.org/jira/browse/CAMEL-19601)

camel-core - Limit auto conversion when stream caching is enabled

[CAMEL-19599](https://issues.apache.org/jira/browse/CAMEL-19599)

camel-jbang - Export to camel-main - Add support for Kubernetes

[CAMEL-19593](https://issues.apache.org/jira/browse/CAMEL-19593)

camel-main - Standalone web console

[CAMEL-19584](https://issues.apache.org/jira/browse/CAMEL-19584)

Camel aws2 Kinesis Asynchronous Client

[CAMEL-19567](https://issues.apache.org/jira/browse/CAMEL-19567)

Create a Camel-Opensearch Starter

[CAMEL-19349](https://issues.apache.org/jira/browse/CAMEL-19349)

camel-core - Dev console for source to support camel-jbang source-dir

[CAMEL-19344](https://issues.apache.org/jira/browse/CAMEL-19344)

camel-jbang - Reload to source dir via http

[CAMEL-19325](https://issues.apache.org/jira/browse/CAMEL-19325)

azure-cosmosdb: Add default identity authentication

[CAMEL-19320](https://issues.apache.org/jira/browse/CAMEL-19320)

camel-jbang - Add command to reload

[CAMEL-19309](https://issues.apache.org/jira/browse/CAMEL-19309)

camel-jbang - Run with empty folder

[CAMEL-19308](https://issues.apache.org/jira/browse/CAMEL-19308)

Add support for spring boot 3 native and AOT

[CAMEL-19307](https://issues.apache.org/jira/browse/CAMEL-19307)

camel-yaml-io - YAML route dumper

[CAMEL-19304](https://issues.apache.org/jira/browse/CAMEL-19304)

JPA paging support

[CAMEL-19299](https://issues.apache.org/jira/browse/CAMEL-19299)

camel-console - Add dev console for bean registry

[CAMEL-19280](https://issues.apache.org/jira/browse/CAMEL-19280)

camel-coap: support for coap observe (RFC-7641)

[CAMEL-19279](https://issues.apache.org/jira/browse/CAMEL-19279)

Introduce a file component for Azure Files (mimic the FTP component)

[CAMEL-19273](https://issues.apache.org/jira/browse/CAMEL-19273)

Create and release a container image for using camel-jbang

[CAMEL-19270](https://issues.apache.org/jira/browse/CAMEL-19270)

camel-netty - Add support for Unix Domain Sockets

[CAMEL-19236](https://issues.apache.org/jira/browse/CAMEL-19236)

camel-jbang - Command to send a message

[CAMEL-19230](https://issues.apache.org/jira/browse/CAMEL-19230)

Optaplanner 9

[CAMEL-19212](https://issues.apache.org/jira/browse/CAMEL-19212)

camel-groovy - provide a way to define global groovy variables

[CAMEL-19209](https://issues.apache.org/jira/browse/CAMEL-19209)

camel-observation-starter - For Camel 4

[CAMEL-19188](https://issues.apache.org/jira/browse/CAMEL-19188)

GraphQL component should support Exchange.HTTP\_QUERY or custom headers

[CAMEL-19183](https://issues.apache.org/jira/browse/CAMEL-19183)

camel-rest-openapi: Add an option to set the default content types used in the generated OpenAPI document

[CAMEL-19159](https://issues.apache.org/jira/browse/CAMEL-19159)

Camel-AWS: Support Profile Credential provider as configuration

[CAMEL-19143](https://issues.apache.org/jira/browse/CAMEL-19143)

Bindy - Add option to quote fields only when necessary

[CAMEL-19128](https://issues.apache.org/jira/browse/CAMEL-19128)

camel-jbang - Version command

[CAMEL-19120](https://issues.apache.org/jira/browse/CAMEL-19120)

camel-jbang - export configurable template

[CAMEL-19099](https://issues.apache.org/jira/browse/CAMEL-19099)

Camel-Jbang Export: Add a flag to include secret refresh properties in application.properties

[CAMEL-19069](https://issues.apache.org/jira/browse/CAMEL-19069)

Presigned urls in camel-minio component

[CAMEL-19050](https://issues.apache.org/jira/browse/CAMEL-19050)

DHIS2 Component

[CAMEL-19044](https://issues.apache.org/jira/browse/CAMEL-19044)

Camel-Jbang catalog output in JSON

[CAMEL-19033](https://issues.apache.org/jira/browse/CAMEL-19033)

camel-jbang - Add trace command

[CAMEL-19030](https://issues.apache.org/jira/browse/CAMEL-19030)

camel-jbang - doc and catalog to support --camel-version option

[CAMEL-19027](https://issues.apache.org/jira/browse/CAMEL-19027)

camel-console - Add dev console for backlog tracer

[CAMEL-19023](https://issues.apache.org/jira/browse/CAMEL-19023)

Add support for Micrometer Observation

[CAMEL-19020](https://issues.apache.org/jira/browse/CAMEL-19020)

camel-console - Add dev console for tracing messages (backlog tracer)

[CAMEL-18989](https://issues.apache.org/jira/browse/CAMEL-18989)

camel-jbang - Run custom distributions of Camel

[CAMEL-18981](https://issues.apache.org/jira/browse/CAMEL-18981)

camel-vertx-websocket: Add capability to capture peer connect / disconnect events

[CAMEL-18966](https://issues.apache.org/jira/browse/CAMEL-18966)

Add component for Camunda Zeebe support

[CAMEL-18940](https://issues.apache.org/jira/browse/CAMEL-18940)

camel-vertx-websocket: Support URI path and query params for WS server consumer

[CAMEL-18916](https://issues.apache.org/jira/browse/CAMEL-18916)

camel-xslt-saxon: allow logger injection

[CAMEL-18913](https://issues.apache.org/jira/browse/CAMEL-18913)

simple language - Add function to build a key=value string from a list

[CAMEL-18909](https://issues.apache.org/jira/browse/CAMEL-18909)

Add DTO generator option in camel-jbang generate command

[CAMEL-18904](https://issues.apache.org/jira/browse/CAMEL-18904)

camel-core - Add functions to simple language to create empty map/list/string/json

[CAMEL-18837](https://issues.apache.org/jira/browse/CAMEL-18837)

Component for Opensearch

[CAMEL-18823](https://issues.apache.org/jira/browse/CAMEL-18823)

Provide option to download dependencies to a specific folder with Camel JBang/camel CLI

[CAMEL-18793](https://issues.apache.org/jira/browse/CAMEL-18793)

camel-core - Log component - Pretty print xml or json

[CAMEL-18698](https://issues.apache.org/jira/browse/CAMEL-18698)

Add support for multiple data types on components

[CAMEL-18687](https://issues.apache.org/jira/browse/CAMEL-18687)

camel-salesforce: Support Client Credentials OAuth Flow

[CAMEL-18625](https://issues.apache.org/jira/browse/CAMEL-18625)

Provide an option to pass specific AWS SAML Profile

[CAMEL-18551](https://issues.apache.org/jira/browse/CAMEL-18551)

camel-salesforce: Add support for Salesforce Pub/Sub API

[CAMEL-18538](https://issues.apache.org/jira/browse/CAMEL-18538)

camel-jbang - Add log command

[CAMEL-18523](https://issues.apache.org/jira/browse/CAMEL-18523)

camel-jbang - Add watch option

[CAMEL-18508](https://issues.apache.org/jira/browse/CAMEL-18508)

camel-jbang - User config file

[CAMEL-18497](https://issues.apache.org/jira/browse/CAMEL-18497)

camel-jbang - camel run -v x.y.z

[CAMEL-18189](https://issues.apache.org/jira/browse/CAMEL-18189)

camel-core - XML DSL <beans> for custom beans and to embed Camel routes in same file

[CAMEL-17986](https://issues.apache.org/jira/browse/CAMEL-17986)

Camel pulsar consumer support key shared policy

[CAMEL-17946](https://issues.apache.org/jira/browse/CAMEL-17946)

camel-as2 - Add https support

[CAMEL-17895](https://issues.apache.org/jira/browse/CAMEL-17895)

camel-vertx-websocket: Consumer as WS client

[CAMEL-17840](https://issues.apache.org/jira/browse/CAMEL-17840)

Pulsar component - support retry letter topics

[CAMEL-17495](https://issues.apache.org/jira/browse/CAMEL-17495)

camel-as2 - No support for application/xml content type

[CAMEL-17330](https://issues.apache.org/jira/browse/CAMEL-17330)

Apache HTTP client/core: Moving to 5.x

[CAMEL-17066](https://issues.apache.org/jira/browse/CAMEL-17066)

camel-nats - Support authentication with Nats server

[CAMEL-16631](https://issues.apache.org/jira/browse/CAMEL-16631)

camel-core - Kamelet EIP allow to specify parameters as property paris

[CAMEL-16479](https://issues.apache.org/jira/browse/CAMEL-16479)

Camel-AWS-Kinesis: The consumer should be able to consume from multiple shards at the same time

[CAMEL-14824](https://issues.apache.org/jira/browse/CAMEL-14824)

Extend Camel Context functionnalities through the Extension mechanism

[CAMEL-14467](https://issues.apache.org/jira/browse/CAMEL-14467)

camel-jcache - Dynamically bypass the cache for lookups

[CAMEL-14248](https://issues.apache.org/jira/browse/CAMEL-14248)

Camel Route Test Coverage in JUnit5

[CAMEL-13573](https://issues.apache.org/jira/browse/CAMEL-13573)

Parquet Dataformat: supporting parquet files in marshal / unmarshal

[CAMEL-12608](https://issues.apache.org/jira/browse/CAMEL-12608)

Add default no-op implementation of RouteBuilder

[CAMEL-12317](https://issues.apache.org/jira/browse/CAMEL-12317)

Provide integration with AWS Step Functions

[CAMEL-5963](https://issues.apache.org/jira/browse/CAMEL-5963)

camel-smpp: Support TRX connection mode to the SMSC

### Sub-task (6)

[CAMEL-19640](https://issues.apache.org/jira/browse/CAMEL-19640)

fix camel-package-maven-plugin EOL dependency

[CAMEL-19335](https://issues.apache.org/jira/browse/CAMEL-19335)

Convert spring-boot openapi and springdoc components

[CAMEL-18908](https://issues.apache.org/jira/browse/CAMEL-18908)

Remove camel-jclouds

[CAMEL-18894](https://issues.apache.org/jira/browse/CAMEL-18894)

Remove camel-elasticsearch-rest in v4

[CAMEL-18891](https://issues.apache.org/jira/browse/CAMEL-18891)

Remove camel-xstream

[CAMEL-18889](https://issues.apache.org/jira/browse/CAMEL-18889)

Remove camel-rabbitmq

### Task (121)

[CAMEL-19728](https://issues.apache.org/jira/browse/CAMEL-19728)

parquetAvro is missing in dataformats model

[CAMEL-19687](https://issues.apache.org/jira/browse/CAMEL-19687)

Remove Camel-Atlasmap-starter

[CAMEL-19686](https://issues.apache.org/jira/browse/CAMEL-19686)

Remove Camel-Atlasmap

[CAMEL-19683](https://issues.apache.org/jira/browse/CAMEL-19683)

camel-jbang - Make RC2 as the current release

[CAMEL-19652](https://issues.apache.org/jira/browse/CAMEL-19652)

camel-console - Trace should include headers in json output

[CAMEL-19649](https://issues.apache.org/jira/browse/CAMEL-19649)

apache-camel - Source tarball should have apache-camel as name

[CAMEL-19642](https://issues.apache.org/jira/browse/CAMEL-19642)

camel-aws2-ec2 - Should not be scheduled poll endpoint

[CAMEL-19634](https://issues.apache.org/jira/browse/CAMEL-19634)

camel-zeebe - Only download from Maven central

[CAMEL-19632](https://issues.apache.org/jira/browse/CAMEL-19632)

camel-xml-jaxp: Split package warning

[CAMEL-19630](https://issues.apache.org/jira/browse/CAMEL-19630)

camel-hyperledger-aries - Remove

[CAMEL-19629](https://issues.apache.org/jira/browse/CAMEL-19629)

camel-weka - Remove this component

[CAMEL-19628](https://issues.apache.org/jira/browse/CAMEL-19628)

Restrict downloading JARs from Atlassian Maven

[CAMEL-19621](https://issues.apache.org/jira/browse/CAMEL-19621)

camel-elytron - Deprecate this component

[CAMEL-19600](https://issues.apache.org/jira/browse/CAMEL-19600)

camel-atom: investigate potential test cleanups

[CAMEL-19577](https://issues.apache.org/jira/browse/CAMEL-19577)

camel-jbang - Maven resolver logs verbose about downloading that we should get rid of

[CAMEL-19565](https://issues.apache.org/jira/browse/CAMEL-19565)

Create Azure Files SB starter

[CAMEL-19563](https://issues.apache.org/jira/browse/CAMEL-19563)

Investigate usages of raw types

[CAMEL-19561](https://issues.apache.org/jira/browse/CAMEL-19561)

Upgrade artemis after ARTEMIS-4338 is fixed

[CAMEL-19550](https://issues.apache.org/jira/browse/CAMEL-19550)

camel-dhis: ensure tests have assertions

[CAMEL-19539](https://issues.apache.org/jira/browse/CAMEL-19539)

camel-netty: replace Thread.sleep in tests

[CAMEL-19501](https://issues.apache.org/jira/browse/CAMEL-19501)

camel-grpc: upgrade proto gen to 1.56.0 (or newer)

[CAMEL-19499](https://issues.apache.org/jira/browse/CAMEL-19499)

camel-yaml-dsl: Missing rest-configuration in YAML DSL schema

[CAMEL-19492](https://issues.apache.org/jira/browse/CAMEL-19492)

camel-xml-io: fix modifier orders to comply with the JLS

[CAMEL-19489](https://issues.apache.org/jira/browse/CAMEL-19489)

camel-minio - Minor issues in documentation

[CAMEL-19475](https://issues.apache.org/jira/browse/CAMEL-19475)

camel-spring-boot: create a camel-activemq starter

[CAMEL-19465](https://issues.apache.org/jira/browse/CAMEL-19465)

Move Apache snapshots repository to a separate Maven profile for better build reproducibility

[CAMEL-19462](https://issues.apache.org/jira/browse/CAMEL-19462)

camel-package-maven-plugin - Make it Maven 4 compatible

[CAMEL-19438](https://issues.apache.org/jira/browse/CAMEL-19438)

camel-sftp: tests cause entry pollution on user's known hosts file

[CAMEL-19429](https://issues.apache.org/jira/browse/CAMEL-19429)

Re-add camel-activemq component

[CAMEL-19425](https://issues.apache.org/jira/browse/CAMEL-19425)

camel-core: DynamicRouterConcurrentPOJOTest is flaky

[CAMEL-19410](https://issues.apache.org/jira/browse/CAMEL-19410)

Camel 4.0.0-M3 with Velocity - Deprecation warning

[CAMEL-19408](https://issues.apache.org/jira/browse/CAMEL-19408)

camel-swift - Restore the component

[CAMEL-19403](https://issues.apache.org/jira/browse/CAMEL-19403)

Parquet Dataformat: Create Spring Boot Starter

[CAMEL-19402](https://issues.apache.org/jira/browse/CAMEL-19402)

test-infra - Reduce the boilerplate code needed

[CAMEL-19400](https://issues.apache.org/jira/browse/CAMEL-19400)

camel-elasticsearch - Reduce integration tests duration

[CAMEL-19386](https://issues.apache.org/jira/browse/CAMEL-19386)

Support object property on template bean

[CAMEL-19384](https://issues.apache.org/jira/browse/CAMEL-19384)

Wrong declaration of minimal Java version on pom (inherited)

[CAMEL-19376](https://issues.apache.org/jira/browse/CAMEL-19376)

camel-core - XmlStreamDetector security

[CAMEL-19375](https://issues.apache.org/jira/browse/CAMEL-19375)

Upgrade to angus-mail 2.0

[CAMEL-19363](https://issues.apache.org/jira/browse/CAMEL-19363)

Upgrade Spring Batch to version 5.x

[CAMEL-19355](https://issues.apache.org/jira/browse/CAMEL-19355)

maven wrapper - Upgrade to 3.9.2

[CAMEL-19341](https://issues.apache.org/jira/browse/CAMEL-19341)

camel-spring-boot - Example with ActiveMQ Artemis

[CAMEL-19321](https://issues.apache.org/jira/browse/CAMEL-19321)

maven - something is downloading json-smart/maven-metadata.xml from 3rd party repos

[CAMEL-19292](https://issues.apache.org/jira/browse/CAMEL-19292)

camel-core - Remove experimental LightweightCamelContext

[CAMEL-19290](https://issues.apache.org/jira/browse/CAMEL-19290)

camel-solr - Remove component as its not maintainable

[CAMEL-19289](https://issues.apache.org/jira/browse/CAMEL-19289)

camel-sql - Add docs that SQL can use message body (simple language)

[CAMEL-19248](https://issues.apache.org/jira/browse/CAMEL-19248)

Suspicious ignoring of a variable in CouchbaseConsumer

[CAMEL-19240](https://issues.apache.org/jira/browse/CAMEL-19240)

camel-core - JVM uptime vs camel uptime

[CAMEL-19233](https://issues.apache.org/jira/browse/CAMEL-19233)

Clean up code generation for <component>ApiCollection in camel-api-component-maven-plugin

[CAMEL-19221](https://issues.apache.org/jira/browse/CAMEL-19221)

camel-as2 - Unused variable in EntityParser

[CAMEL-19213](https://issues.apache.org/jira/browse/CAMEL-19213)

Camel DSL page documentation is missing groovy dsl

[CAMEL-19203](https://issues.apache.org/jira/browse/CAMEL-19203)

Unused assignment in SyncPropertiesMojo

[CAMEL-19202](https://issues.apache.org/jira/browse/CAMEL-19202)

Unused assignment in OnExceptionReifier

[CAMEL-19201](https://issues.apache.org/jira/browse/CAMEL-19201)

Unused assignment in AdviceWithBuilder::maxDeep()

[CAMEL-19200](https://issues.apache.org/jira/browse/CAMEL-19200)

Unused assignment in RouteControllerAction::getLast(Row r)

[CAMEL-19194](https://issues.apache.org/jira/browse/CAMEL-19194)

Method HMACAccumulator::compareTo() always returns false

[CAMEL-19192](https://issues.apache.org/jira/browse/CAMEL-19192)

Possible infinite recursion in JettyConfigurationBuilder

[CAMEL-19189](https://issues.apache.org/jira/browse/CAMEL-19189)

camel-groovy - Adapt the code for native mode

[CAMEL-19179](https://issues.apache.org/jira/browse/CAMEL-19179)

camel-jetty - Remove JettyHttpBinding which is not in use

[CAMEL-19163](https://issues.apache.org/jira/browse/CAMEL-19163)

camel-google-\*: Improve google dependency alignment across camel-google components

[CAMEL-19142](https://issues.apache.org/jira/browse/CAMEL-19142)

camel-spring-boot-example - Make it build with v4 M2

[CAMEL-19139](https://issues.apache.org/jira/browse/CAMEL-19139)

camel-core - Add build time in MANIFEST.MF

[CAMEL-19138](https://issues.apache.org/jira/browse/CAMEL-19138)

Maven 3.9.0 build fails with -Psourcecheck

[CAMEL-19119](https://issues.apache.org/jira/browse/CAMEL-19119)

\[Docs\] Missing examples in Camel JDBC

[CAMEL-19117](https://issues.apache.org/jira/browse/CAMEL-19117)

camel-catalog - Remove archetypeAsXml from CamelCatalog

[CAMEL-19102](https://issues.apache.org/jira/browse/CAMEL-19102)

camel-core: Producer cache offers poor performance due to the type check scalability issue

[CAMEL-19091](https://issues.apache.org/jira/browse/CAMEL-19091)

camel-core - Remove Discard and DiscardOldest from thread pool policy

[CAMEL-19090](https://issues.apache.org/jira/browse/CAMEL-19090)

camel-core - Remove deprecated APIs

[CAMEL-19088](https://issues.apache.org/jira/browse/CAMEL-19088)

camel-core - Remove SafeCopyProperty that was only in use for camel-zipkin

[CAMEL-19070](https://issues.apache.org/jira/browse/CAMEL-19070)

camel-elasticsearch: flaky tests on Apache CI

[CAMEL-19062](https://issues.apache.org/jira/browse/CAMEL-19062)

Clean up Parent POM

[CAMEL-19061](https://issues.apache.org/jira/browse/CAMEL-19061)

\[DOCS\] Broken links in Azure ServiceBus docs

[CAMEL-19058](https://issues.apache.org/jira/browse/CAMEL-19058)

Type check scalability issue

[CAMEL-19054](https://issues.apache.org/jira/browse/CAMEL-19054)

Camel-Fastjson: Switch to 2.x

[CAMEL-19052](https://issues.apache.org/jira/browse/CAMEL-19052)

Angus-Mail: Move to 2.x

[CAMEL-19012](https://issues.apache.org/jira/browse/CAMEL-19012)

Remove Camel v2 documentation

[CAMEL-19011](https://issues.apache.org/jira/browse/CAMEL-19011)

update release notes to point users to use camel-bom / camel-spring-boot-bom

[CAMEL-19009](https://issues.apache.org/jira/browse/CAMEL-19009)

camel-gson - Date Format with GsonBuilder

[CAMEL-19007](https://issues.apache.org/jira/browse/CAMEL-19007)

camel-yaml-dsl - Deprecate classic parsing mode

[CAMEL-18995](https://issues.apache.org/jira/browse/CAMEL-18995)

Upgrade to HttpComponents 5.x

[CAMEL-18984](https://issues.apache.org/jira/browse/CAMEL-18984)

camel-undertow-spring-security-starter - Migrate to Spring Boot 3

[CAMEL-18982](https://issues.apache.org/jira/browse/CAMEL-18982)

Avoid custom versions of maven javadoc and resource plugin

[CAMEL-18978](https://issues.apache.org/jira/browse/CAMEL-18978)

Upgrade to atmosphere 3.0.2 - Add JSR356\_MAPPING\_PATH configuration

[CAMEL-18977](https://issues.apache.org/jira/browse/CAMEL-18977)

camel-joor - Make the code more flexible for native mode

[CAMEL-18975](https://issues.apache.org/jira/browse/CAMEL-18975)

Import sorting and code auto-formatting seems to be broken

[CAMEL-18971](https://issues.apache.org/jira/browse/CAMEL-18971)

Camel-Spring-Boot: Add SBOM generation

[CAMEL-18970](https://issues.apache.org/jira/browse/CAMEL-18970)

Camel-Any23: Remove component

[CAMEL-18949](https://issues.apache.org/jira/browse/CAMEL-18949)

camel-examples - Remove examples using removed components

[CAMEL-18939](https://issues.apache.org/jira/browse/CAMEL-18939)

camel-examples - Migrate to logger 2 in v2

[CAMEL-18936](https://issues.apache.org/jira/browse/CAMEL-18936)

components - Add log4j-core so logging to logfile works

[CAMEL-18935](https://issues.apache.org/jira/browse/CAMEL-18935)

camel-jbang - Update to slf4j 2.0

[CAMEL-18934](https://issues.apache.org/jira/browse/CAMEL-18934)

camel-spring-boot - Salesforce Starter uses Jetty 9

[CAMEL-18933](https://issues.apache.org/jira/browse/CAMEL-18933)

camel-spring-boot - Adjust auto configuration to load Spring Boot 3

[CAMEL-18932](https://issues.apache.org/jira/browse/CAMEL-18932)

camel-core - Upgrade to slf4j-api 2.0

[CAMEL-18931](https://issues.apache.org/jira/browse/CAMEL-18931)

camel-websocket - Migrate to Jakarta EE for v4

[CAMEL-18930](https://issues.apache.org/jira/browse/CAMEL-18930)

camel-spring-boot - Migrate undertow-security

[CAMEL-18929](https://issues.apache.org/jira/browse/CAMEL-18929)

camel-spring-boot - Remove deprecated components in v4

[CAMEL-18928](https://issues.apache.org/jira/browse/CAMEL-18928)

Disable components not JakartaEE compatible

[CAMEL-18925](https://issues.apache.org/jira/browse/CAMEL-18925)

Remove camel-rest-swagger in v4

[CAMEL-18907](https://issues.apache.org/jira/browse/CAMEL-18907)

camel-datasonnet - Datasonnet is not JakartaEE compatible for v4

[CAMEL-18906](https://issues.apache.org/jira/browse/CAMEL-18906)

camel-salesforce - Uses old cometd client that uses Jetty 9.x in v4

[CAMEL-18893](https://issues.apache.org/jira/browse/CAMEL-18893)

Camel-Examples: Switch to Camel 4.x

[CAMEL-18890](https://issues.apache.org/jira/browse/CAMEL-18890)

Remove camel-vertx-kafka

[CAMEL-18884](https://issues.apache.org/jira/browse/CAMEL-18884)

camel-package-maven-plugin - Endpoint and Component DSL should skip v4 that are not migrated yet

[CAMEL-18883](https://issues.apache.org/jira/browse/CAMEL-18883)

Remove deprecated components in v4

[CAMEL-18882](https://issues.apache.org/jira/browse/CAMEL-18882)

camel-cdi - Remove in v4

[CAMEL-18881](https://issues.apache.org/jira/browse/CAMEL-18881)

Remove camel-swagger-java in v4

[CAMEL-18879](https://issues.apache.org/jira/browse/CAMEL-18879)

Remove Camel-Zipkin after deprecation

[CAMEL-18876](https://issues.apache.org/jira/browse/CAMEL-18876)

ErrorHandlerDefinition properties missing in camel-catalog

[CAMEL-18869](https://issues.apache.org/jira/browse/CAMEL-18869)

camel-stomp - Use Artemis for embedded testing

[CAMEL-18864](https://issues.apache.org/jira/browse/CAMEL-18864)

java-joor-dsl - Drop support of class files

[CAMEL-18860](https://issues.apache.org/jira/browse/CAMEL-18860)

java-joor-dsl - Adapt the code for native compilation

[CAMEL-18829](https://issues.apache.org/jira/browse/CAMEL-18829)

camel-yaml-dsl - generate-yaml-schema - Support \`additionalProperties: false\`

[CAMEL-18825](https://issues.apache.org/jira/browse/CAMEL-18825)

Make XML parser more secured out of the box

[CAMEL-18786](https://issues.apache.org/jira/browse/CAMEL-18786)

documentation: reorganize Camel Core documentation

[CAMEL-18779](https://issues.apache.org/jira/browse/CAMEL-18779)

camel-test-infra: investigate replacing ActiveMQ with Artemis for embedded testing

[CAMEL-18765](https://issues.apache.org/jira/browse/CAMEL-18765)

Extend PrepareParentPomMojo to automatically generate/replace catalog/core and other sections

[CAMEL-18410](https://issues.apache.org/jira/browse/CAMEL-18410)

Remove camel-test support for JUnit 4.x

[CAMEL-17894](https://issues.apache.org/jira/browse/CAMEL-17894)

build: investigate ways to make it faster

[CAMEL-17328](https://issues.apache.org/jira/browse/CAMEL-17328)

Avoid 3rd party maven repository - jboss

[CAMEL-14680](https://issues.apache.org/jira/browse/CAMEL-14680)

javax -> jakarta

### Test (15)

[CAMEL-19604](https://issues.apache.org/jira/browse/CAMEL-19604)

camel-knative: component is likely broken

[CAMEL-19484](https://issues.apache.org/jira/browse/CAMEL-19484)

camel-core: WireTapAbortPolicyTest is flaky

[CAMEL-19208](https://issues.apache.org/jira/browse/CAMEL-19208)

Adding power support for zookeeper image

[CAMEL-19184](https://issues.apache.org/jira/browse/CAMEL-19184)

Camel-http: Upgrade to http 5.x broke test case using httpContext

[CAMEL-19084](https://issues.apache.org/jira/browse/CAMEL-19084)

camel-yaml-dsl: Test resume strategies

[CAMEL-19028](https://issues.apache.org/jira/browse/CAMEL-19028)

camel-core - WireTapAbortPolicyTest - is a bit too flaky

[CAMEL-18960](https://issues.apache.org/jira/browse/CAMEL-18960)

CxfRsEndpointWithPropertiesTest is broken

[CAMEL-18955](https://issues.apache.org/jira/browse/CAMEL-18955)

Fix camel-spring-boot tests after jakarta upgrade

[CAMEL-18921](https://issues.apache.org/jira/browse/CAMEL-18921)

itests jakarta upgrade: Use Artemis and JmsComponent

[CAMEL-18892](https://issues.apache.org/jira/browse/CAMEL-18892)

Restore MLLP tests

[CAMEL-18827](https://issues.apache.org/jira/browse/CAMEL-18827)

camel-kudu - Fix unit test failure with JDK 17

[CAMEL-18826](https://issues.apache.org/jira/browse/CAMEL-18826)

camel-kudu - Install libtinfo on CI to execute all Kudu's unit tests

[CAMEL-18620](https://issues.apache.org/jira/browse/CAMEL-18620)

Add redpanda container to test-infra

[CAMEL-18595](https://issues.apache.org/jira/browse/CAMEL-18595)

camel-test-infra: add microprofile-lra implementation

[CAMEL-18197](https://issues.apache.org/jira/browse/CAMEL-18197)

DocumentationEnricher uses deprecated api

### Wish (1)

[CAMEL-19412](https://issues.apache.org/jira/browse/CAMEL-19412)

camel-kafka - Add kerberos config file location property

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).