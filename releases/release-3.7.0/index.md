# Apache camel 3.7.0 Release

## New and Noteworthy

This release is the new Camel 3.7.0 LTS release.

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
      <version>3.7.0</version>
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
      <version>3.7.0</version>
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
| [apache-camel-3.7.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.0/apache-camel-3.7.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.0/apache-camel-3.7.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.0/apache-camel-3.7.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (46)

[CAMEL-15931](https://issues.apache.org/jira/browse/CAMEL-15931)

Camel 3.6 fails to resolve #bean:name notation for camel.component.pulsar.pulsar-client

[CAMEL-15920](https://issues.apache.org/jira/browse/CAMEL-15920)

Cannot parse CSV if the last (not required) field is empty when using a tab separator

[CAMEL-15919](https://issues.apache.org/jira/browse/CAMEL-15919)

Response message definition does not correctly handle java.io.File as response model

[CAMEL-15902](https://issues.apache.org/jira/browse/CAMEL-15902)

Camel-Opentelemetry-starter: Spring Boot starter is broken

[CAMEL-15899](https://issues.apache.org/jira/browse/CAMEL-15899)

HazelcastConsumers do not remove their listeners

[CAMEL-15891](https://issues.apache.org/jira/browse/CAMEL-15891)

camel-ahc body for String data

[CAMEL-15890](https://issues.apache.org/jira/browse/CAMEL-15890)

camel-salesforce: URLs for Composite APIs not encoded correctly

[CAMEL-15884](https://issues.apache.org/jira/browse/CAMEL-15884)

camel-salesforce: include all related objects in generated DTOs

[CAMEL-15882](https://issues.apache.org/jira/browse/CAMEL-15882)

camel-salesforce: Upsert should return an UpsertResult

[CAMEL-15871](https://issues.apache.org/jira/browse/CAMEL-15871)

camel-milo - CamelServerItem replaces name of the node

[CAMEL-15856](https://issues.apache.org/jira/browse/CAMEL-15856)

camel-salesforce: duplicate enums generated from picklist values

[CAMEL-15855](https://issues.apache.org/jira/browse/CAMEL-15855)

camel-salesforce - Generates DTOs with illegal Java strings

[CAMEL-15852](https://issues.apache.org/jira/browse/CAMEL-15852)

properties binding: issues binding to map when the key contains a dot

[CAMEL-15840](https://issues.apache.org/jira/browse/CAMEL-15840)

camel-aws2-sns: duplicate copies of configuration objects lead to undefined behavior

[CAMEL-15834](https://issues.apache.org/jira/browse/CAMEL-15834)

NATS consumer throws NullPointerException on connection failure

[CAMEL-15833](https://issues.apache.org/jira/browse/CAMEL-15833)

camel-aws2-sqs: create queue logic is susceptible to TOC/TOU errors

[CAMEL-15822](https://issues.apache.org/jira/browse/CAMEL-15822)

\[camel-file\] fileExist=Move doesn't use FileMoveExistingStrategy when tempFile is also configured

[CAMEL-15819](https://issues.apache.org/jira/browse/CAMEL-15819)

Camel-jsonb: Artifact 'johnzon-jsonb' is required with default settings.

[CAMEL-15815](https://issues.apache.org/jira/browse/CAMEL-15815)

endpoint-dsl should support dynamic uri in Enrich EIP

[CAMEL-15811](https://issues.apache.org/jira/browse/CAMEL-15811)

report-maven-plugin fails to validate simple expression

[CAMEL-15810](https://issues.apache.org/jira/browse/CAMEL-15810)

Can't call overloaded method using simple expression returning subtype of expected parameter

[CAMEL-15809](https://issues.apache.org/jira/browse/CAMEL-15809)

PredicateBuilder doesn't init predicates properly

[CAMEL-15808](https://issues.apache.org/jira/browse/CAMEL-15808)

camel-mock: MockEndpoint doesn't init predicates

[CAMEL-15807](https://issues.apache.org/jira/browse/CAMEL-15807)

Simple expression regression with contains operator in 3.6.0

[CAMEL-15803](https://issues.apache.org/jira/browse/CAMEL-15803)

missing jar libraries in download zip

[CAMEL-15801](https://issues.apache.org/jira/browse/CAMEL-15801)

DefaultConfigurerResolver always resolves to ExtendedCamelContextConfigurer if name contains CamelContext

[CAMEL-15797](https://issues.apache.org/jira/browse/CAMEL-15797)

AWS2 S3 component option isIncludeFolders check fails in some cases

[CAMEL-15794](https://issues.apache.org/jira/browse/CAMEL-15794)

CxfRsEndpoint recreates SSL context for each message

[CAMEL-15793](https://issues.apache.org/jira/browse/CAMEL-15793)

MethodNotFoundException when calling method on OSGi service reference in Blueprint

[CAMEL-15789](https://issues.apache.org/jira/browse/CAMEL-15789)

camel-couchbase: bucket not parsed

[CAMEL-15788](https://issues.apache.org/jira/browse/CAMEL-15788)

Apache Camel Yammer component does not work in 3.x (from 3.1)

[CAMEL-15786](https://issues.apache.org/jira/browse/CAMEL-15786)

Camel OpenAPI ignores apiVendorExtension option for REST binding

[CAMEL-15768](https://issues.apache.org/jira/browse/CAMEL-15768)

camel-main - can not use the camel.lra.enabled=true

[CAMEL-15766](https://issues.apache.org/jira/browse/CAMEL-15766)

camel-spring-boot - No converter found capable of converting from type \[java.lang.String\] to type \[org.apache.camel.component.http.HttpClientConfigurer\]

[CAMEL-15760](https://issues.apache.org/jira/browse/CAMEL-15760)

org.osgi.service.blueprint.container.NoSuchComponentException: No component with id 'blueprintBundle' could be found

[CAMEL-15752](https://issues.apache.org/jira/browse/CAMEL-15752)

Camel-Kafka: Exception java.lang.NoClassDefFoundError: com/fasterxml/jackson/databind/JsonNode on Camel-Kafka component

[CAMEL-15749](https://issues.apache.org/jira/browse/CAMEL-15749)

Unable to configure hash symbol as commentMarker for csv data format

[CAMEL-15748](https://issues.apache.org/jira/browse/CAMEL-15748)

Paho consumer never connects if the broker is not reachable at startup

[CAMEL-15742](https://issues.apache.org/jira/browse/CAMEL-15742)

xpath uses previous return type definition

[CAMEL-15718](https://issues.apache.org/jira/browse/CAMEL-15718)

Camel lumberjack server component not thread safe

[CAMEL-15711](https://issues.apache.org/jira/browse/CAMEL-15711)

Incorrect includes from EIP documentation to Quarkus documentation

[CAMEL-15710](https://issues.apache.org/jira/browse/CAMEL-15710)

OpenTracingTracer does not activate created span

[CAMEL-15708](https://issues.apache.org/jira/browse/CAMEL-15708)

loopDoWhile with delay does not see end of loop

[CAMEL-15706](https://issues.apache.org/jira/browse/CAMEL-15706)

UpdateReadmeMojo fails when executed outside the camel tree

[CAMEL-15623](https://issues.apache.org/jira/browse/CAMEL-15623)

osgi - Reference methods not found in blueprint context

[CAMEL-14480](https://issues.apache.org/jira/browse/CAMEL-14480)

camel-salesforce - Duplicate Properties between Relationship Name and Child Relationship Name

### Improvement (91)

[CAMEL-15926](https://issues.apache.org/jira/browse/CAMEL-15926)

camel route templates - Add support for spring boot auto configuration

[CAMEL-15925](https://issues.apache.org/jira/browse/CAMEL-15925)

camel-spring-cloud-netflix - Deprecate

[CAMEL-15923](https://issues.apache.org/jira/browse/CAMEL-15923)

upgrade to apache pulsar 2.7.0

[CAMEL-15917](https://issues.apache.org/jira/browse/CAMEL-15917)

Resilience4j Property Component doesn't work for configurationRef

[CAMEL-15914](https://issues.apache.org/jira/browse/CAMEL-15914)

camel-csimple - Add information whether compiled source is from predicate or expression

[CAMEL-15908](https://issues.apache.org/jira/browse/CAMEL-15908)

Add additional exchange metrics to MicrometerRoutePolicy

[CAMEL-15904](https://issues.apache.org/jira/browse/CAMEL-15904)

camel-salesforce: streaming replayId should default to -1 (new events)

[CAMEL-15896](https://issues.apache.org/jira/browse/CAMEL-15896)

Upgrade google-cloud-pubsub to 1.109.0

[CAMEL-15894](https://issues.apache.org/jira/browse/CAMEL-15894)

Update opentelemetry component to use opentelemetry 0.11

[CAMEL-15893](https://issues.apache.org/jira/browse/CAMEL-15893)

onJobExecute method of org.apache.camel.routepolicy.quartz2.ScheduledRoutePolicy should be public

[CAMEL-15888](https://issues.apache.org/jira/browse/CAMEL-15888)

ConfigurerResolver should return PropertyConfigurer instead of GeneratedPropertyConfigurer

[CAMEL-15887](https://issues.apache.org/jira/browse/CAMEL-15887)

properties binding: add support for java.util.Properties

[CAMEL-15886](https://issues.apache.org/jira/browse/CAMEL-15886)

components - Configurers for components dont include collection value metadata

[CAMEL-15879](https://issues.apache.org/jira/browse/CAMEL-15879)

Update avro version to 1.10.x (1.10.0)

[CAMEL-15877](https://issues.apache.org/jira/browse/CAMEL-15877)

camel-salesforce: Use XStream's security framework

[CAMEL-15873](https://issues.apache.org/jira/browse/CAMEL-15873)

Upgrade Google BigQuery libraries

[CAMEL-15866](https://issues.apache.org/jira/browse/CAMEL-15866)

camel-salesforce: Support new SOSL search result

[CAMEL-15863](https://issues.apache.org/jira/browse/CAMEL-15863)

camel-salesforce: HttpClient default RequestBufferSize is too small

[CAMEL-15861](https://issues.apache.org/jira/browse/CAMEL-15861)

Add the capability to provide a custom serializer to GooglePubSubProducer

[CAMEL-15860](https://issues.apache.org/jira/browse/CAMEL-15860)

Use a real logger instead of stdio for MavenVersionManger

[CAMEL-15859](https://issues.apache.org/jira/browse/CAMEL-15859)

camel-salesforce: Don't generate unnecessary enums

[CAMEL-15854](https://issues.apache.org/jira/browse/CAMEL-15854)

camel - Automate dependencies included in assembly

[CAMEL-15851](https://issues.apache.org/jira/browse/CAMEL-15851)

Upgrade debezium to 1.3.1

[CAMEL-15849](https://issues.apache.org/jira/browse/CAMEL-15849)

Upgrade to spring boot 2.4

[CAMEL-15848](https://issues.apache.org/jira/browse/CAMEL-15848)

Update Camel-CMIS to accept VersioningState parameter.

[CAMEL-15847](https://issues.apache.org/jira/browse/CAMEL-15847)

Remove camel-core dependency from camel-workday

[CAMEL-15846](https://issues.apache.org/jira/browse/CAMEL-15846)

camel-core - Remove basicPropertyBinding

[CAMEL-15843](https://issues.apache.org/jira/browse/CAMEL-15843)

Camel-AWS2: Rename useIamCredentials to useDefaultCredentialProvider where it is used

[CAMEL-15839](https://issues.apache.org/jira/browse/CAMEL-15839)

camel-core - Do not list error handlers in JMX

[CAMEL-15836](https://issues.apache.org/jira/browse/CAMEL-15836)

components - Automatic autowire by type - Specify which options support this

[CAMEL-15835](https://issues.apache.org/jira/browse/CAMEL-15835)

camel-sjms - Add option allowAutoWiredConnection​Factory

[CAMEL-15827](https://issues.apache.org/jira/browse/CAMEL-15827)

Improve Camel Maven Archetype for component

[CAMEL-15826](https://issues.apache.org/jira/browse/CAMEL-15826)

camel-main - Remove autowire by type

[CAMEL-15825](https://issues.apache.org/jira/browse/CAMEL-15825)

Enable scheduler configuration to be set on camel-github consumers

[CAMEL-15824](https://issues.apache.org/jira/browse/CAMEL-15824)

camel-core - Optimize configurer to have getOptionType api

[CAMEL-15823](https://issues.apache.org/jira/browse/CAMEL-15823)

camel-core - Optimize RedeliveryPolicy copied per EIP

[CAMEL-15821](https://issues.apache.org/jira/browse/CAMEL-15821)

camel-core - Lightweight mode and route templates

[CAMEL-15818](https://issues.apache.org/jira/browse/CAMEL-15818)

camel-saxon - Allow to configure custom Saxon Configuration on xquery language

[CAMEL-15817](https://issues.apache.org/jira/browse/CAMEL-15817)

Support comments on fields in the srcgen tool

[CAMEL-15814](https://issues.apache.org/jira/browse/CAMEL-15814)

Camel-Git: Commit consumer should be able to be based on specific branch

[CAMEL-15813](https://issues.apache.org/jira/browse/CAMEL-15813)

camel-grpc add ClientInterceptors to the channel

[CAMEL-15812](https://issues.apache.org/jira/browse/CAMEL-15812)

Camel-Git: Better structure for consumer returned object

[CAMEL-15805](https://issues.apache.org/jira/browse/CAMEL-15805)

route-coverage goal does not find coverage data when camel-report-maven-plugin is configured in parent pom

[CAMEL-15802](https://issues.apache.org/jira/browse/CAMEL-15802)

camel-core - Optimize lightweight to unref all models

[CAMEL-15796](https://issues.apache.org/jira/browse/CAMEL-15796)

camel-core - Optimize reifier to reduce memory via intermediate lambda classes

[CAMEL-15795](https://issues.apache.org/jira/browse/CAMEL-15795)

camel-core - Reduce tangle from impl engine to model

[CAMEL-15790](https://issues.apache.org/jira/browse/CAMEL-15790)

Provide validation for method name for API based components

[CAMEL-15784](https://issues.apache.org/jira/browse/CAMEL-15784)

camel-core - Optimize with Bootstrap marker interface

[CAMEL-15783](https://issues.apache.org/jira/browse/CAMEL-15783)

camel-core - Add order to @Converter so we can generate in hardcoded order

[CAMEL-15782](https://issues.apache.org/jira/browse/CAMEL-15782)

camel-main - Optimize to clear camel-main own initial properties after startup

[CAMEL-15781](https://issues.apache.org/jira/browse/CAMEL-15781)

camel-core - Optimize FilePathResolver to use simpler parser than regexp

[CAMEL-15779](https://issues.apache.org/jira/browse/CAMEL-15779)

Use DefaultAWSCredentialsProviderChain to load AWS credentials from different sources

[CAMEL-15778](https://issues.apache.org/jira/browse/CAMEL-15778)

camel-main - Optimize and clear main configuration configurers after started

[CAMEL-15776](https://issues.apache.org/jira/browse/CAMEL-15776)

camel-core - Remove reflection in enum converter used as fallback

[CAMEL-15770](https://issues.apache.org/jira/browse/CAMEL-15770)

Kafka serialize/deserialize properties are inconsistently named

[CAMEL-15769](https://issues.apache.org/jira/browse/CAMEL-15769)

Ability to disable tokenization on jsonpath split returning a single element as string

[CAMEL-15765](https://issues.apache.org/jira/browse/CAMEL-15765)

camel-core - Optimize base converters

[CAMEL-15764](https://issues.apache.org/jira/browse/CAMEL-15764)

Twilo camel case endpoint URI options leads to reflective property binding

[CAMEL-15763](https://issues.apache.org/jira/browse/CAMEL-15763)

camel-main - Add option to clear reifier after starting

[CAMEL-15761](https://issues.apache.org/jira/browse/CAMEL-15761)

camel-core - Optimize TimeUtils to calculate without regexp

[CAMEL-15758](https://issues.apache.org/jira/browse/CAMEL-15758)

camel-core - Modularize - camel-base-engine

[CAMEL-15754](https://issues.apache.org/jira/browse/CAMEL-15754)

camel-grpc Improve the propagation consumer strategy

[CAMEL-15753](https://issues.apache.org/jira/browse/CAMEL-15753)

camel-core - Modularize move some parts from camel-base to camel-support

[CAMEL-15745](https://issues.apache.org/jira/browse/CAMEL-15745)

Rest DSL input/output type class

[CAMEL-15740](https://issues.apache.org/jira/browse/CAMEL-15740)

camel-core - camel-core-builder

[CAMEL-15739](https://issues.apache.org/jira/browse/CAMEL-15739)

camel-core - Move AdviceWith from Reifier to Builder

[CAMEL-15737](https://issues.apache.org/jira/browse/CAMEL-15737)

AS2 component URI parameter resolution requires reflection

[CAMEL-15736](https://issues.apache.org/jira/browse/CAMEL-15736)

LevelDB: Update/add karaf features regarding camel-leveldb and camel-levedb-legacy

[CAMEL-15735](https://issues.apache.org/jira/browse/CAMEL-15735)

levelDB: create starter for camel-leveldb-legacy

[CAMEL-15733](https://issues.apache.org/jira/browse/CAMEL-15733)

camel-core - ToD remove multi language

[CAMEL-15732](https://issues.apache.org/jira/browse/CAMEL-15732)

camel-core - Untangle reifier from impl and builder

[CAMEL-15731](https://issues.apache.org/jira/browse/CAMEL-15731)

Add support for receiving MLLP messages without sending any acknowledgment

[CAMEL-15730](https://issues.apache.org/jira/browse/CAMEL-15730)

camel-core - SimpleBuilder should just be a facade

[CAMEL-15726](https://issues.apache.org/jira/browse/CAMEL-15726)

camel-core - Simple language concat expressions optimize for constant parts

[CAMEL-15722](https://issues.apache.org/jira/browse/CAMEL-15722)

endpoint uri builder: add an option to URL encode the returned uri or not

[CAMEL-15721](https://issues.apache.org/jira/browse/CAMEL-15721)

camel-core - Simple with external resource should load resource once during init

[CAMEL-15716](https://issues.apache.org/jira/browse/CAMEL-15716)

Allow to specify subprotocol when using camel-vertx-websocket component

[CAMEL-15713](https://issues.apache.org/jira/browse/CAMEL-15713)

camel-joor - Add support for dependency injection

[CAMEL-15712](https://issues.apache.org/jira/browse/CAMEL-15712)

camel-core - Optimize languages to only pass in configuration when any is not default

[CAMEL-15694](https://issues.apache.org/jira/browse/CAMEL-15694)

camel-core - Optmize EventNotifier to seperate exchange vs other events

[CAMEL-15693](https://issues.apache.org/jira/browse/CAMEL-15693)

Camel-File-watch: Event type should be a simple string on the consumer side

[CAMEL-15690](https://issues.apache.org/jira/browse/CAMEL-15690)

camel-core - Optimize direct producer

[CAMEL-15687](https://issues.apache.org/jira/browse/CAMEL-15687)

Camel-DJL: Upgrade to Deep Java Library 0.8.0

[CAMEL-15686](https://issues.apache.org/jira/browse/CAMEL-15686)

Enable EndpointDSL with simple expressions within an Endpoint Builder bean

[CAMEL-15680](https://issues.apache.org/jira/browse/CAMEL-15680)

\[camel-azure\] Add blob batch filtering capability

[CAMEL-15679](https://issues.apache.org/jira/browse/CAMEL-15679)

LevelDB: Consider replacing of serizalization via org.fusesource.hawtbuf:hawtbuf with Jackson

[CAMEL-15661](https://issues.apache.org/jira/browse/CAMEL-15661)

\[camel-azure-strorage-blob\] Use Testcontainers and Azurite at integration tests

[CAMEL-15653](https://issues.apache.org/jira/browse/CAMEL-15653)

Improve SJMS Batch Logging

[CAMEL-15533](https://issues.apache.org/jira/browse/CAMEL-15533)

Camel-Slack: Improve the error messages

[CAMEL-15434](https://issues.apache.org/jira/browse/CAMEL-15434)

Support connectionString in Azure Blob and Azure Queue components

[CAMEL-11731](https://issues.apache.org/jira/browse/CAMEL-11731)

Servlet Component isn't really async

### New Feature (18)

[CAMEL-15881](https://issues.apache.org/jira/browse/CAMEL-15881)

Add a rebalancing cluster service

[CAMEL-15867](https://issues.apache.org/jira/browse/CAMEL-15867)

Camel-AWS2-S3: Add a an Autowired S3Presigner UriParam in Configuration

[CAMEL-15862](https://issues.apache.org/jira/browse/CAMEL-15862)

Camel-AWS2-S3: Support Creation of presignedUrl like downloadLink in Camel-AWS-S3

[CAMEL-15858](https://issues.apache.org/jira/browse/CAMEL-15858)

camel-restdsl-openapi-plugin - allow remote openapi specifications

[CAMEL-15845](https://issues.apache.org/jira/browse/CAMEL-15845)

GitHub consumer for events API

[CAMEL-15837](https://issues.apache.org/jira/browse/CAMEL-15837)

camel-nats: add an option to enable connection protocol fine tracing

[CAMEL-15806](https://issues.apache.org/jira/browse/CAMEL-15806)

Camel-AWS2-SNS: Support FIFO Topic

[CAMEL-15804](https://issues.apache.org/jira/browse/CAMEL-15804)

Support DataSonnet as an Expression Language

[CAMEL-15772](https://issues.apache.org/jira/browse/CAMEL-15772)

camel-pulsar - should support readCompacted configuration

[CAMEL-15757](https://issues.apache.org/jira/browse/CAMEL-15757)

camel-salesforce: Add rawPayload support in camel-salesforce composite

[CAMEL-15751](https://issues.apache.org/jira/browse/CAMEL-15751)

camel-grpc - Provide access to stream observer in the camel Exchange

[CAMEL-15707](https://issues.apache.org/jira/browse/CAMEL-15707)

examples - Add camel-coor example

[CAMEL-15704](https://issues.apache.org/jira/browse/CAMEL-15704)

camel-core - Compiled simple language

[CAMEL-15697](https://issues.apache.org/jira/browse/CAMEL-15697)

camel-joor - Camel expression language using jOOR

[CAMEL-15692](https://issues.apache.org/jira/browse/CAMEL-15692)

Add JSON-B dataformat support

[CAMEL-15689](https://issues.apache.org/jira/browse/CAMEL-15689)

Add camel-atlasmap component

[CAMEL-15510](https://issues.apache.org/jira/browse/CAMEL-15510)

Create camel-vertx-kafka component

[CAMEL-14003](https://issues.apache.org/jira/browse/CAMEL-14003)

Camel-Kubernetes: Support CRD

### Sub-task (4)

[CAMEL-15832](https://issues.apache.org/jira/browse/CAMEL-15832)

\[component archetype\] XXXEndpoint contains deprecated annotation @UriEndpoint.consumerClass and @UriEndpoint.label

[CAMEL-15831](https://issues.apache.org/jira/browse/CAMEL-15831)

\[component archetype\] some classes contains unused import

[CAMEL-15830](https://issues.apache.org/jira/browse/CAMEL-15830)

\[component archetype\] EventBushelper provides order of specifiers which doesn't respect Java language specification

[CAMEL-15829](https://issues.apache.org/jira/browse/CAMEL-15829)

\[component archetype\] typo in EventBushelper "implementy"

### Task (22)

[CAMEL-15935](https://issues.apache.org/jira/browse/CAMEL-15935)

Fix example snippets for properties component spring to camel property bridge

[CAMEL-15932](https://issues.apache.org/jira/browse/CAMEL-15932)

Camel-Google-\* Stream components: Review the documentation

[CAMEL-15915](https://issues.apache.org/jira/browse/CAMEL-15915)

camel-ftp - CI test failures on master about logo wrong size

[CAMEL-15880](https://issues.apache.org/jira/browse/CAMEL-15880)

Camel-Minio: Upgrade to Minio 8.x

[CAMEL-15878](https://issues.apache.org/jira/browse/CAMEL-15878)

Camel-Infinispan: Support authentication in idempotent repository

[CAMEL-15870](https://issues.apache.org/jira/browse/CAMEL-15870)

Remove Camel-Openstack Karaf feature

[CAMEL-15865](https://issues.apache.org/jira/browse/CAMEL-15865)

GitHub API dropped support for username/password credentials

[CAMEL-15799](https://issues.apache.org/jira/browse/CAMEL-15799)

Please delete old releases from the mirroring system

[CAMEL-15785](https://issues.apache.org/jira/browse/CAMEL-15785)

Camel-AWS2: make possibile to use a client based on DefaultCredentialProvider in all the interested components

[CAMEL-15775](https://issues.apache.org/jira/browse/CAMEL-15775)

Upgrade to spring boot 2.3.5

[CAMEL-15756](https://issues.apache.org/jira/browse/CAMEL-15756)

Remove camel-jbpm and camel-optaplanner from Karaf features

[CAMEL-15738](https://issues.apache.org/jira/browse/CAMEL-15738)

camel-fastjson|camel-fhir|camel-gson|camel-jackson|camel-jacksonxml|camel-jaxb|camel-xstream doc mismatch the value in src code

[CAMEL-15728](https://issues.apache.org/jira/browse/CAMEL-15728)

\[cdi\] @ContextName does not exist anymore

[CAMEL-15725](https://issues.apache.org/jira/browse/CAMEL-15725)

Make camel-cdi OSGi CDI friendly

[CAMEL-15702](https://issues.apache.org/jira/browse/CAMEL-15702)

Camel-Karaf and camel-spring-boot: Generated documentation for 3.4.x LTS, should point to correct components/dataformat/languages documentation

[CAMEL-15701](https://issues.apache.org/jira/browse/CAMEL-15701)

Camel-Atlasmap: Create a Spring Boot starter

[CAMEL-15699](https://issues.apache.org/jira/browse/CAMEL-15699)

Camel-Jsonb: Create Spring-boot starter

[CAMEL-15698](https://issues.apache.org/jira/browse/CAMEL-15698)

Camel-Jsonb: Create Karaf feature

[CAMEL-15695](https://issues.apache.org/jira/browse/CAMEL-15695)

Maven archetypes for OSGi and spring-boot move to their project

[CAMEL-15691](https://issues.apache.org/jira/browse/CAMEL-15691)

Johnzon DataFormat doc references Jackson instead of Johnzon

[CAMEL-15688](https://issues.apache.org/jira/browse/CAMEL-15688)

Camel-couchbase: Make the configuration of the endpoint less complex

[CAMEL-15094](https://issues.apache.org/jira/browse/CAMEL-15094)

Create an Endpoint DSL archetype

### Test (3)

[CAMEL-15792](https://issues.apache.org/jira/browse/CAMEL-15792)

Migrate camel-couchbase tests to the new test-infra

[CAMEL-15767](https://issues.apache.org/jira/browse/CAMEL-15767)

Complete camel-nagios tests with a mock nsca server based test

[CAMEL-13163](https://issues.apache.org/jira/browse/CAMEL-13163)

camel-kafka - Use testcontainers for testing

### Wish (1)

[CAMEL-15872](https://issues.apache.org/jira/browse/CAMEL-15872)

Make it possible to change Authorization -header JWT-token type

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).