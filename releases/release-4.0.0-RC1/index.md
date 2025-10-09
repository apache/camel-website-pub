# Apache camel 4.0.0-RC1 Release

## New and Noteworthy

This release is the first release candidate towards the Camel 4.0.0 release.

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
      <version>4.0.0-RC1</version>
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
      <version>4.0.0-RC1</version>
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
| [apache-camel-4.0.0-RC1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC1/apache-camel-4.0.0-RC1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC1/apache-camel-4.0.0-RC1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC1/apache-camel-4.0.0-RC1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.0-RC1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.0-RC1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (28)

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

[CAMEL-19421](https://issues.apache.org/jira/browse/CAMEL-19421)

Camel-Jira: Use Files.createTempFile in FileConverter instead of creating File directly

[CAMEL-19415](https://issues.apache.org/jira/browse/CAMEL-19415)

camel-stax: using xtokenize might be NPE on xml default namespace

[CAMEL-19405](https://issues.apache.org/jira/browse/CAMEL-19405)

camel-jbang - camel get circuitbreaker may not work

[CAMEL-19399](https://issues.apache.org/jira/browse/CAMEL-19399)

camel-cxf - Prevent storing invalid entry in Converter cache on error

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

[CAMEL-19342](https://issues.apache.org/jira/browse/CAMEL-19342)

Rest Inline Routes mixed with direct routes.

[CAMEL-19314](https://issues.apache.org/jira/browse/CAMEL-19314)

camel-aws - Connection pool shutdown when aws health checks are used

[CAMEL-19298](https://issues.apache.org/jira/browse/CAMEL-19298)

Snmp: version 3 is not supported for several actions for the component

[CAMEL-19295](https://issues.apache.org/jira/browse/CAMEL-19295)

Concurrency issues with dynamicMap in AbstractDynamicRegistry

[CAMEL-19281](https://issues.apache.org/jira/browse/CAMEL-19281)

Aws2- healthchecks not closing resources for awsClient

[CAMEL-18965](https://issues.apache.org/jira/browse/CAMEL-18965)

Camel-CXF: OnCompletion not working anymore

### Dependency upgrade (22)

[CAMEL-19503](https://issues.apache.org/jira/browse/CAMEL-19503)

camel-jbang - Upgrade to maven-resolver 1.9.13

[CAMEL-19490](https://issues.apache.org/jira/browse/CAMEL-19490)

camel-elasticsearch - Upgrade to 8.8.x

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

[CAMEL-19340](https://issues.apache.org/jira/browse/CAMEL-19340)

camel-jbang - Upgrade to maven-resolver 1.9.10

[CAMEL-19317](https://issues.apache.org/jira/browse/CAMEL-19317)

camel-kubernetes - Upgrade to 6.6.x

[CAMEL-19301](https://issues.apache.org/jira/browse/CAMEL-19301)

camel-jbang - Upgrade to hawtio 2.17.2

[CAMEL-19287](https://issues.apache.org/jira/browse/CAMEL-19287)

camel-debezium - Upgrade to 2.2

[CAMEL-18924](https://issues.apache.org/jira/browse/CAMEL-18924)

camel-lucene - Upgrade to 9.6.0

### Improvement (49)

[CAMEL-19478](https://issues.apache.org/jira/browse/CAMEL-19478)

camel-core - Add synchronous option to some EIPs like split

[CAMEL-19477](https://issues.apache.org/jira/browse/CAMEL-19477)

MeterRegistry collects authorization data

[CAMEL-19471](https://issues.apache.org/jira/browse/CAMEL-19471)

camel-yaml-dsl - JSON library enum consistency

[CAMEL-19467](https://issues.apache.org/jira/browse/CAMEL-19467)

should servlet and rest throw exceptions when duplicate and ambiguous paths occur

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

[CAMEL-19336](https://issues.apache.org/jira/browse/CAMEL-19336)

camel-core-model - EIP model json should have index order for properties

[CAMEL-19331](https://issues.apache.org/jira/browse/CAMEL-19331)

camel-jbang - camel stop - should stop if there is only 1 running

[CAMEL-19327](https://issues.apache.org/jira/browse/CAMEL-19327)

camel-jpa: Single result

[CAMEL-19326](https://issues.apache.org/jira/browse/CAMEL-19326)

camel-jbang - Register reload services eager

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

[CAMEL-19135](https://issues.apache.org/jira/browse/CAMEL-19135)

components - Reduce number of different Category

[CAMEL-18874](https://issues.apache.org/jira/browse/CAMEL-18874)

camel-file - When possible, pass the exchange to the exception handler

[CAMEL-18769](https://issues.apache.org/jira/browse/CAMEL-18769)

camel-jbang - Catalog to select runtime

[CAMEL-18638](https://issues.apache.org/jira/browse/CAMEL-18638)

Deprecate label property on all annotations in favor of category.

[CAMEL-18536](https://issues.apache.org/jira/browse/CAMEL-18536)

camel-joor - Rename joor language to java

[CAMEL-18177](https://issues.apache.org/jira/browse/CAMEL-18177)

camel-slack - Honour Retry-After when requests are rate-limited

[CAMEL-18078](https://issues.apache.org/jira/browse/CAMEL-18078)

CamelGoogleSheets.valueInputOption not documented for google-sheets://data/append

[CAMEL-17652](https://issues.apache.org/jira/browse/CAMEL-17652)

camel-minio - Auto create bucket should not be done in endpoint

[CAMEL-17528](https://issues.apache.org/jira/browse/CAMEL-17528)

camel-core-model - Description should just be text

[CAMEL-15462](https://issues.apache.org/jira/browse/CAMEL-15462)

route coverage report - May report 0 for doCatch even if its in use

[CAMEL-15105](https://issues.apache.org/jira/browse/CAMEL-15105)

camel-core - Extension or getter/setter on ExtendedCamelContext

### New Feature (15)

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

[CAMEL-19273](https://issues.apache.org/jira/browse/CAMEL-19273)

Create and release a container image for using camel-jbang

[CAMEL-19159](https://issues.apache.org/jira/browse/CAMEL-19159)

Camel-AWS: Support Profile Credential provider as configuration

[CAMEL-18793](https://issues.apache.org/jira/browse/CAMEL-18793)

camel-core - Log component - Pretty print xml or json

[CAMEL-17946](https://issues.apache.org/jira/browse/CAMEL-17946)

camel-as2 - Add https support

[CAMEL-17495](https://issues.apache.org/jira/browse/CAMEL-17495)

camel-as2 - No support for application/xml content type

[CAMEL-13573](https://issues.apache.org/jira/browse/CAMEL-13573)

Parquet Dataformat: supporting parquet files in marshal / unmarshal

### Task (22)

[CAMEL-19475](https://issues.apache.org/jira/browse/CAMEL-19475)

camel-spring-boot: create a camel-activemq starter

[CAMEL-19429](https://issues.apache.org/jira/browse/CAMEL-19429)

Re-add camel-activemq component

[CAMEL-19418](https://issues.apache.org/jira/browse/CAMEL-19418)

camel-cxf - "Description of relayHeaders option" section of CXF component page is out of date

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

[CAMEL-19365](https://issues.apache.org/jira/browse/CAMEL-19365)

camel-undertow: UndertowHttpsSpringTest broken after upgrade

[CAMEL-19363](https://issues.apache.org/jira/browse/CAMEL-19363)

Upgrade Spring Batch to version 5.x

[CAMEL-19328](https://issues.apache.org/jira/browse/CAMEL-19328)

CamelAwsSesTo and CamelAwsSesReplyToAddresses update documentation with String instead of List

[CAMEL-19319](https://issues.apache.org/jira/browse/CAMEL-19319)

Type check misses

[CAMEL-19290](https://issues.apache.org/jira/browse/CAMEL-19290)

camel-solr - Remove component as its not maintainable

[CAMEL-19163](https://issues.apache.org/jira/browse/CAMEL-19163)

camel-google-\*: Improve google dependency alignment across camel-google components

[CAMEL-19102](https://issues.apache.org/jira/browse/CAMEL-19102)

camel-core: Producer cache offers poor performance due to the type check scalability issue

[CAMEL-19060](https://issues.apache.org/jira/browse/CAMEL-19060)

Scalability ceiling: seda

[CAMEL-19058](https://issues.apache.org/jira/browse/CAMEL-19058)

Type check scalability issue

[CAMEL-19052](https://issues.apache.org/jira/browse/CAMEL-19052)

Angus-Mail: Move to 2.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).