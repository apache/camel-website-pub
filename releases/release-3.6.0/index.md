# Apache camel 3.6.0 Release

## New and Noteworthy

This release is the new Camel 3.6.0 patch release.

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
      <version>3.6.0</version>
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
      <version>3.6.0</version>
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
| [apache-camel-3.6.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.6.0/apache-camel-3.6.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.6.0/apache-camel-3.6.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.6.0/apache-camel-3.6.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.6.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.6.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (42)

[CAMEL-15715](https://issues.apache.org/jira/browse/CAMEL-15715)

Simple performance regression

[CAMEL-15682](https://issues.apache.org/jira/browse/CAMEL-15682)

Aggregate route recovery fails to start up

[CAMEL-15678](https://issues.apache.org/jira/browse/CAMEL-15678)

camel-aws2-s3 multipart upload multiplies file by number of parts

[CAMEL-15676](https://issues.apache.org/jira/browse/CAMEL-15676)

openapi-restdsl-generator - redundant content-types with multiple responses

[CAMEL-15675](https://issues.apache.org/jira/browse/CAMEL-15675)

MicroProfileMetricsRoutePolicy may attempt to register duplicate metrics

[CAMEL-15669](https://issues.apache.org/jira/browse/CAMEL-15669)

When the registry does not have any nodes, ServiceCallDefinition will be blocked

[CAMEL-15666](https://issues.apache.org/jira/browse/CAMEL-15666)

Configurer for UniVocity\*Format is missing options from superclass

[CAMEL-15665](https://issues.apache.org/jira/browse/CAMEL-15665)

OnException and StreamCaching

[CAMEL-15646](https://issues.apache.org/jira/browse/CAMEL-15646)

camel-mongodb - Batch insert does not work

[CAMEL-15644](https://issues.apache.org/jira/browse/CAMEL-15644)

camel-salesforce - NullPointerException on route startup

[CAMEL-15628](https://issues.apache.org/jira/browse/CAMEL-15628)

camel-core - Safe copy message history may lead to ArrayIndexOutOfBoundsException

[CAMEL-15624](https://issues.apache.org/jira/browse/CAMEL-15624)

camel-undertow-starter: AutoConfiguration property type error

[CAMEL-15622](https://issues.apache.org/jira/browse/CAMEL-15622)

endpoint-dsl - Bean name evaluated as string in sql component

[CAMEL-15617](https://issues.apache.org/jira/browse/CAMEL-15617)

Reserved PubSub attributes are unintentionally passed on causing send to fail

[CAMEL-15615](https://issues.apache.org/jira/browse/CAMEL-15615)

Camel-Infinispan: Cannot consume events

[CAMEL-15610](https://issues.apache.org/jira/browse/CAMEL-15610)

NPE in CamelXmlTreeParserHelper.parseCamelRouteTree(CamelXmlTreeParserHelper.java:47) when routes are empty

[CAMEL-15602](https://issues.apache.org/jira/browse/CAMEL-15602)

camel-main - Add support for property placeholders in #class factory method parameters

[CAMEL-15581](https://issues.apache.org/jira/browse/CAMEL-15581)

Unable to load XML REST definitions with camel-main xmlRests config property

[CAMEL-15580](https://issues.apache.org/jira/browse/CAMEL-15580)

SJMS Batch Consumer startup race condition

[CAMEL-15577](https://issues.apache.org/jira/browse/CAMEL-15577)

Camel-stringtemplate: Misleading and incorrect implementation of parameter 'allowTemplateFromHeader'

[CAMEL-15576](https://issues.apache.org/jira/browse/CAMEL-15576)

Incorrect HTTP Method retrieved by camel-tracing

[CAMEL-15572](https://issues.apache.org/jira/browse/CAMEL-15572)

route template: placeholder unsing the #property: syntax does not get resolved

[CAMEL-15563](https://issues.apache.org/jira/browse/CAMEL-15563)

Sensitive keys are logged in auto-configuration summary

[CAMEL-15559](https://issues.apache.org/jira/browse/CAMEL-15559)

Validation returns wrong "Unknown option" in Properties file when there is a space before the \`=\`

[CAMEL-15558](https://issues.apache.org/jira/browse/CAMEL-15558)

pollEnrich timeout issue

[CAMEL-15557](https://issues.apache.org/jira/browse/CAMEL-15557)

Multicast parallel processing with timeout: Stream Cache file not deleted if CachedOutputStream created before timeout and writing to CachedOutputStream happens after timeout

[CAMEL-15547](https://issues.apache.org/jira/browse/CAMEL-15547)

Wrong URI with http dsl and query parameters

[CAMEL-15534](https://issues.apache.org/jira/browse/CAMEL-15534)

Camel-telegram wrongly parse chatId from headers

[CAMEL-15532](https://issues.apache.org/jira/browse/CAMEL-15532)

Multicast parallel processing with timeout: Stream Cache file not deleted

[CAMEL-15530](https://issues.apache.org/jira/browse/CAMEL-15530)

AWS2 S3 Component unclosed stream issue with includeFolders property

[CAMEL-15528](https://issues.apache.org/jira/browse/CAMEL-15528)

Project generated with camel-archetype-api-component cannot be compiled

[CAMEL-15526](https://issues.apache.org/jira/browse/CAMEL-15526)

Camel-AWS2-S3: Consume Gzip file from S3 not working.

[CAMEL-15525](https://issues.apache.org/jira/browse/CAMEL-15525)

camel-archetype-java: main class on pom file different than actual main class

[CAMEL-15521](https://issues.apache.org/jira/browse/CAMEL-15521)

InfluxDB connection bean creation fails

[CAMEL-15506](https://issues.apache.org/jira/browse/CAMEL-15506)

camel-bean: Do not use reflection on the annotation proxy in BeanAnnotationExpressionFactory

[CAMEL-15500](https://issues.apache.org/jira/browse/CAMEL-15500)

camel-azure-storage-blob: wrong syntax in the component json

[CAMEL-15499](https://issues.apache.org/jira/browse/CAMEL-15499)

camel-azure-storage-queue: wrong syntax in the component json

[CAMEL-15495](https://issues.apache.org/jira/browse/CAMEL-15495)

DefaultVertxHttpBinding ignores exchange content-type request header

[CAMEL-15493](https://issues.apache.org/jira/browse/CAMEL-15493)

Camel-Cdi throws NPE when attempting to inject an array property using Microprofile Config

[CAMEL-15490](https://issues.apache.org/jira/browse/CAMEL-15490)

Can't build -P enable-schemagen,release,apt with jdk 11

[CAMEL-15489](https://issues.apache.org/jira/browse/CAMEL-15489)

camel-sql - Persistence Aggregator not compatible with Oracle-Java Data Type

[CAMEL-15486](https://issues.apache.org/jira/browse/CAMEL-15486)

camel-test-spring - Mocking of Camel Endpoints breaks because adding 3rd party dependency with spring boot

### Improvement (72)

[CAMEL-15677](https://issues.apache.org/jira/browse/CAMEL-15677)

Camel-Slack: deprecate username, iconUrl and iconEmoji

[CAMEL-15673](https://issues.apache.org/jira/browse/CAMEL-15673)

endpoint-dsl - Reference bean by #type prefix

[CAMEL-15671](https://issues.apache.org/jira/browse/CAMEL-15671)

Performance overhead of bean post processor when using camel spring on bootstrap

[CAMEL-15664](https://issues.apache.org/jira/browse/CAMEL-15664)

Automatically wrap secret properites with RAW when computing the URI

[CAMEL-15659](https://issues.apache.org/jira/browse/CAMEL-15659)

Add back manually coded configurers for the languages

[CAMEL-15658](https://issues.apache.org/jira/browse/CAMEL-15658)

camel-pgevent : automate integration tests

[CAMEL-15656](https://issues.apache.org/jira/browse/CAMEL-15656)

\[camel-azure-strorage-blob\] Add the possibility to download all blobs from container

[CAMEL-15654](https://issues.apache.org/jira/browse/CAMEL-15654)

camel-core - Optimize language with properties

[CAMEL-15652](https://issues.apache.org/jira/browse/CAMEL-15652)

camel-bean - Optimize bean function in simple language add support for scope

[CAMEL-15651](https://issues.apache.org/jira/browse/CAMEL-15651)

Camel-twitter - small refactor

[CAMEL-15648](https://issues.apache.org/jira/browse/CAMEL-15648)

Avoid using reflection to clear exchange headers in camel-crypto DigitalSignatureProcessor

[CAMEL-15647](https://issues.apache.org/jira/browse/CAMEL-15647)

Camel-AWS2-Kinesis-\*: Added a CborEnabled option explicitly

[CAMEL-15643](https://issues.apache.org/jira/browse/CAMEL-15643)

camel-xpath - Add option to pre-compile xpath expression

[CAMEL-15642](https://issues.apache.org/jira/browse/CAMEL-15642)

camel-spring - SpEL should be pre-compiled

[CAMEL-15641](https://issues.apache.org/jira/browse/CAMEL-15641)

camel-core - Optimize simple expressions to eager init if possible

[CAMEL-15638](https://issues.apache.org/jira/browse/CAMEL-15638)

Print more details if camel-format-plugin:validate fails

[CAMEL-15636](https://issues.apache.org/jira/browse/CAMEL-15636)

camel-bean - Optimize @Pattern annotation discovery

[CAMEL-15634](https://issues.apache.org/jira/browse/CAMEL-15634)

camel-bean - Optimize to avoid NoSuchMethodException when discovering annotations

[CAMEL-15632](https://issues.apache.org/jira/browse/CAMEL-15632)

Geocoder - Mock API google Maps when no API key available

[CAMEL-15630](https://issues.apache.org/jira/browse/CAMEL-15630)

camel-bean - Optimize to lookup custom ParameterMappingStrategy once

[CAMEL-15627](https://issues.apache.org/jira/browse/CAMEL-15627)

camel-core - optiomize - Initialize of expression to avoid runtime check

[CAMEL-15621](https://issues.apache.org/jira/browse/CAMEL-15621)

Support partial route containing only the "from" for RouteBuilderParser.parseRouteBuilderTree

[CAMEL-15620](https://issues.apache.org/jira/browse/CAMEL-15620)

Add CBOR s transitive dependency of AWS Kinesis connectors

[CAMEL-15619](https://issues.apache.org/jira/browse/CAMEL-15619)

camel-shiro: allow custom implementation of serialization

[CAMEL-15611](https://issues.apache.org/jira/browse/CAMEL-15611)

Support prefix for camel namespace in XmlRouteParser

[CAMEL-15609](https://issues.apache.org/jira/browse/CAMEL-15609)

Camel-Infinispan: Add an explicit key uri parameter for producer

[CAMEL-15608](https://issues.apache.org/jira/browse/CAMEL-15608)

Add support for multipart uploads to platform-http-vertx

[CAMEL-15607](https://issues.apache.org/jira/browse/CAMEL-15607)

camel-core - When resolving language then only resolve via registry once

[CAMEL-15606](https://issues.apache.org/jira/browse/CAMEL-15606)

camel-core - Simple with bean function should resolve language once

[CAMEL-15605](https://issues.apache.org/jira/browse/CAMEL-15605)

camel-core - Languages should be singleton for better performance

[CAMEL-15604](https://issues.apache.org/jira/browse/CAMEL-15604)

MongoDB - Support allowDiskUse for find operation

[CAMEL-15603](https://issues.apache.org/jira/browse/CAMEL-15603)

Camel-Infinispan: Support Authentication through URI options

[CAMEL-15600](https://issues.apache.org/jira/browse/CAMEL-15600)

platoform http vertx: thread blocked calling knative REST

[CAMEL-15598](https://issues.apache.org/jira/browse/CAMEL-15598)

camel-kafka - Remove old reflection code setting partitioner class config

[CAMEL-15591](https://issues.apache.org/jira/browse/CAMEL-15591)

Put a configurable limit on the size of unzipped data using camel-zipfile + camel-tarfile

[CAMEL-15590](https://issues.apache.org/jira/browse/CAMEL-15590)

route templates: add an hook to further customize the RouteDefinition computed out of a template

[CAMEL-15588](https://issues.apache.org/jira/browse/CAMEL-15588)

Upgrade swagger-core version

[CAMEL-15586](https://issues.apache.org/jira/browse/CAMEL-15586)

camel-http-vertx - Add support for SendDynamicAware

[CAMEL-15585](https://issues.apache.org/jira/browse/CAMEL-15585)

Camel-health - small refactor

[CAMEL-15584](https://issues.apache.org/jira/browse/CAMEL-15584)

Switch UUID generator to new vanilla implementation

[CAMEL-15579](https://issues.apache.org/jira/browse/CAMEL-15579)

Optimize generated configurer to use static block for getAllOptions

[CAMEL-15573](https://issues.apache.org/jira/browse/CAMEL-15573)

camel-main: support LambdaRouteBuilder

[CAMEL-15567](https://issues.apache.org/jira/browse/CAMEL-15567)

components - Generate source code for creating endpoint uri via a map of properties

[CAMEL-15565](https://issues.apache.org/jira/browse/CAMEL-15565)

camel-main - camel.beans configuration should support lookup existing bean

[CAMEL-15561](https://issues.apache.org/jira/browse/CAMEL-15561)

Camel-AWS2-Eventbridge: More producer operations

[CAMEL-15554](https://issues.apache.org/jira/browse/CAMEL-15554)

camel-api-component - Add description to api proxy so we can specify missing docs

[CAMEL-15553](https://issues.apache.org/jira/browse/CAMEL-15553)

camel-component-maven-plugin issue adding configuration bean to component subclass

[CAMEL-15549](https://issues.apache.org/jira/browse/CAMEL-15549)

camel-api-component - API methods should have details if they are consumer or producer only

[CAMEL-15548](https://issues.apache.org/jira/browse/CAMEL-15548)

Enable shortened way to access headers in mvel templates

[CAMEL-15541](https://issues.apache.org/jira/browse/CAMEL-15541)

Add auto-configuration to camel-jasypt-starter

[CAMEL-15539](https://issues.apache.org/jira/browse/CAMEL-15539)

camel-spring-ws - Use messageIdStrategy on producer side

[CAMEL-15535](https://issues.apache.org/jira/browse/CAMEL-15535)

Camel Barcode : Add additional headers to the exchange such as orientation

[CAMEL-15524](https://issues.apache.org/jira/browse/CAMEL-15524)

camel-caffeine: use cacheName to lookup cache instances from the registry

[CAMEL-15518](https://issues.apache.org/jira/browse/CAMEL-15518)

Wong service generated for the ExtendedCamelContext

[CAMEL-15515](https://issues.apache.org/jira/browse/CAMEL-15515)

camel-core - Deprecate basicPropertyBinding

[CAMEL-15514](https://issues.apache.org/jira/browse/CAMEL-15514)

camel-rest-openapi component automatic operationId generation

[CAMEL-15512](https://issues.apache.org/jira/browse/CAMEL-15512)

Remove the default value for apiComponent on RestConfigurationDefinition

[CAMEL-15511](https://issues.apache.org/jira/browse/CAMEL-15511)

Camel-AHC: Wrapper async-http-client jars in camel-karaf feature are bundle

[CAMEL-15507](https://issues.apache.org/jira/browse/CAMEL-15507)

Make vertx-http component error handling consistent with other HTTP client components

[CAMEL-15505](https://issues.apache.org/jira/browse/CAMEL-15505)

camel-quickfix should not depend on quickfixj-all

[CAMEL-15504](https://issues.apache.org/jira/browse/CAMEL-15504)

Support alternative JNDI locations for TransactionManager

[CAMEL-15501](https://issues.apache.org/jira/browse/CAMEL-15501)

Enable Vert.x router to be configured on VertxWebsocketComponent

[CAMEL-15497](https://issues.apache.org/jira/browse/CAMEL-15497)

Unable to load the External config file for QuickFix component

[CAMEL-15496](https://issues.apache.org/jira/browse/CAMEL-15496)

camel-rabbitmq - Add support to add additional headers and properties

[CAMEL-15484](https://issues.apache.org/jira/browse/CAMEL-15484)

Update Attachment sample in documentation

[CAMEL-15446](https://issues.apache.org/jira/browse/CAMEL-15446)

AbstractCamelContext methods with similar behavior

[CAMEL-15433](https://issues.apache.org/jira/browse/CAMEL-15433)

Generators should run during a component build

[CAMEL-15399](https://issues.apache.org/jira/browse/CAMEL-15399)

\[properties-binding\] add documentation about how properties binding works

[CAMEL-14929](https://issues.apache.org/jira/browse/CAMEL-14929)

camel-aws2-s3 - Doesn't support stream download of large files.

[CAMEL-14736](https://issues.apache.org/jira/browse/CAMEL-14736)

Upgrade to Hadoop 3.x

[CAMEL-14647](https://issues.apache.org/jira/browse/CAMEL-14647)

\[camel-azure\] Add Scheduling feature to polling consumer

[CAMEL-14499](https://issues.apache.org/jira/browse/CAMEL-14499)

camel-core - SendDynamicAware avoid camel-core-catalog dependency

### New Feature (9)

[CAMEL-15639](https://issues.apache.org/jira/browse/CAMEL-15639)

camel-rabbitmq - Add support for requeue at the Consumer level

[CAMEL-15601](https://issues.apache.org/jira/browse/CAMEL-15601)

Upgrade to JAXB impl 2.3.3

[CAMEL-15531](https://issues.apache.org/jira/browse/CAMEL-15531)

Optaplanner - Upgrade component with usage of SolverManager

[CAMEL-15517](https://issues.apache.org/jira/browse/CAMEL-15517)

camel-azure-eventhubs: support producer to sent list of events

[CAMEL-15487](https://issues.apache.org/jira/browse/CAMEL-15487)

LambdaRouteBuilderTemplate - Allow to define a route template via lambda style

[CAMEL-15478](https://issues.apache.org/jira/browse/CAMEL-15478)

camel-api-component - Add label qualifier for api methods in generated configuration classes

[CAMEL-15471](https://issues.apache.org/jira/browse/CAMEL-15471)

Kinesis-Firehose: Add more operation to producer side

[CAMEL-15375](https://issues.apache.org/jira/browse/CAMEL-15375)

Create a Camel AWS2 Eventbridge component

[CAMEL-14672](https://issues.apache.org/jira/browse/CAMEL-14672)

Invoke customizers as part of services initialization

### Task (24)

[CAMEL-15684](https://issues.apache.org/jira/browse/CAMEL-15684)

Remove Camel-Hipchat

[CAMEL-15674](https://issues.apache.org/jira/browse/CAMEL-15674)

Upgrade to maven-archetype-plugin 3.2.0

[CAMEL-15667](https://issues.apache.org/jira/browse/CAMEL-15667)

camel-jira align dependencies with camel-parent

[CAMEL-15660](https://issues.apache.org/jira/browse/CAMEL-15660)

component json - Default value for boolean type should not be in quotes

[CAMEL-15637](https://issues.apache.org/jira/browse/CAMEL-15637)

Create tracing SpanDecorator for VertxHttpComponent

[CAMEL-15631](https://issues.apache.org/jira/browse/CAMEL-15631)

camel-debezium-\* : Upgrade Debezium to 1.3

[CAMEL-15629](https://issues.apache.org/jira/browse/CAMEL-15629)

PDF documetation not available

[CAMEL-15626](https://issues.apache.org/jira/browse/CAMEL-15626)

camel-core - Use StringBuilder instead of StringBuffer

[CAMEL-15594](https://issues.apache.org/jira/browse/CAMEL-15594)

incorrect bundle.symbolicName in camel-example-servlet-rest-karaf-jaas

[CAMEL-15587](https://issues.apache.org/jira/browse/CAMEL-15587)

simple/bean language - performance regression

[CAMEL-15575](https://issues.apache.org/jira/browse/CAMEL-15575)

Some stack traces are being printed to stdout

[CAMEL-15574](https://issues.apache.org/jira/browse/CAMEL-15574)

Move camel-test-infra from core to its own root folder

[CAMEL-15571](https://issues.apache.org/jira/browse/CAMEL-15571)

The order of loading settings is changed in the method AbstractLocationPropertiesSource::loadProperties(Predicate)

[CAMEL-15509](https://issues.apache.org/jira/browse/CAMEL-15509)

Camel-Minio: Create a karaf feature

[CAMEL-15508](https://issues.apache.org/jira/browse/CAMEL-15508)

Camel-NSQ: Support custom NSQLookup implementation

[CAMEL-15502](https://issues.apache.org/jira/browse/CAMEL-15502)

camel-core - Enum type converter should support dash style

[CAMEL-15498](https://issues.apache.org/jira/browse/CAMEL-15498)

camel-api-component - Add java source parser for generating API components

[CAMEL-15492](https://issues.apache.org/jira/browse/CAMEL-15492)

Camel-Karaf: Remove atmosphere-websocket feature

[CAMEL-15488](https://issues.apache.org/jira/browse/CAMEL-15488)

Upgrade to maven wrapper 0.5.6

[CAMEL-15485](https://issues.apache.org/jira/browse/CAMEL-15485)

Migrate camel-spring-boot-examples to use JUnit 5 style

[CAMEL-15482](https://issues.apache.org/jira/browse/CAMEL-15482)

Ensure spring boot examples uses -starter JARs for Camel dependencies

[CAMEL-15430](https://issues.apache.org/jira/browse/CAMEL-15430)

Potentially incorrect log placeholders

[CAMEL-14542](https://issues.apache.org/jira/browse/CAMEL-14542)

camel-core - Optimize simple language

[CAMEL-13923](https://issues.apache.org/jira/browse/CAMEL-13923)

Fix incorrectly escaped simple expressions in migrated manual pages

### Test (5)

[CAMEL-15649](https://issues.apache.org/jira/browse/CAMEL-15649)

camel-jasypt-starter : NativePRNG SecureRandom not available

[CAMEL-15614](https://issues.apache.org/jira/browse/CAMEL-15614)

camel-pg-replicationslot: Automate integration test

[CAMEL-15527](https://issues.apache.org/jira/browse/CAMEL-15527)

Create integration tests for archetypes

[CAMEL-15516](https://issues.apache.org/jira/browse/CAMEL-15516)

camel-nats: Automate TLS authentication test

[CAMEL-13337](https://issues.apache.org/jira/browse/CAMEL-13337)

camel-xmpp - Some unit tests fails

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).