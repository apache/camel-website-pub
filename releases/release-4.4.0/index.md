# Apache camel 4.4.0 Release

## New and Noteworthy

This release is the new Camel 4.4.0 LTS release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.4.0</version>
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
      <version>4.4.0</version>
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
| [apache-camel-4.4.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-src.zip.sha512) |
| [apache-camel-4.4.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.xml.sha512) |
| [apache-camel-4.4.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.0/apache-camel-4.4.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (39)

[CAMEL-20664](https://issues.apache.org/jira/browse/CAMEL-20664)

camel-mapstruct - MapStruct mappers not found in Spring Boot

[CAMEL-20401](https://issues.apache.org/jira/browse/CAMEL-20401)

camel-kudu: Potential NullPointerException on endpoint stop

[CAMEL-20399](https://issues.apache.org/jira/browse/CAMEL-20399)

String to short type conversion fails

[CAMEL-20394](https://issues.apache.org/jira/browse/CAMEL-20394)

camel-jbang wrong transformation when rests and routes tags are used together

[CAMEL-20392](https://issues.apache.org/jira/browse/CAMEL-20392)

camel-jq - Inclined jq in simple language should keep quotes

[CAMEL-20380](https://issues.apache.org/jira/browse/CAMEL-20380)

Kafka Batch Consumer: doesn't honor the poll timeout set

[CAMEL-20378](https://issues.apache.org/jira/browse/CAMEL-20378)

Languages that can take source from header or property is not thread safe

[CAMEL-20375](https://issues.apache.org/jira/browse/CAMEL-20375)

Camel-ical: Camel-20370 brought a NPE in some cases

[CAMEL-20373](https://issues.apache.org/jira/browse/CAMEL-20373)

camel-kafka - KafkaIdempotentRepository may allow some duplicates after application restart

[CAMEL-20370](https://issues.apache.org/jira/browse/CAMEL-20370)

dataformat configurer is not generated for camel-beanio

[CAMEL-20362](https://issues.apache.org/jira/browse/CAMEL-20362)

Camel-Netty-HTTP: Headers validation should be enabled by default

[CAMEL-20357](https://issues.apache.org/jira/browse/CAMEL-20357)

camel-core - throttle EIP doesn't work as expected when it's in a loopDoWhile

[CAMEL-20356](https://issues.apache.org/jira/browse/CAMEL-20356)

camel-core - LoggerHelper returns wrong name for source code line precise

[CAMEL-20354](https://issues.apache.org/jira/browse/CAMEL-20354)

camel-jbang - Using camel run --source-dir component should be able to load from classpath

[CAMEL-20352](https://issues.apache.org/jira/browse/CAMEL-20352)

camel.springboot.includeNonSingletons is not respected anymore: prototype Route Builders are always initialized.

[CAMEL-20351](https://issues.apache.org/jira/browse/CAMEL-20351)

Camel Jbang execution from remote file doesn't work anymore

[CAMEL-20350](https://issues.apache.org/jira/browse/CAMEL-20350)

camel-observation - Null values should be null instead of a string null literal value

[CAMEL-20349](https://issues.apache.org/jira/browse/CAMEL-20349)

camel-salesforce: ClassCastException when a request is retried after a 401

[CAMEL-20342](https://issues.apache.org/jira/browse/CAMEL-20342)

camel-openapi-java - NPE in OpenApiHelper

[CAMEL-20340](https://issues.apache.org/jira/browse/CAMEL-20340)

camel-jbang - camel dependency list throws Exception for dataformats

[CAMEL-20339](https://issues.apache.org/jira/browse/CAMEL-20339)

camel-yaml-dsl - Saga EIP with options causes NPE

[CAMEL-20334](https://issues.apache.org/jira/browse/CAMEL-20334)

AWS S3 cloudevents data type does not set proper data Content-Type

[CAMEL-20307](https://issues.apache.org/jira/browse/CAMEL-20307)

camel-quickfix -Queue Full

[CAMEL-20301](https://issues.apache.org/jira/browse/CAMEL-20301)

Camel retains objects when restarting route via policy

[CAMEL-20292](https://issues.apache.org/jira/browse/CAMEL-20292)

Probable bug in DependencyDownloaderConsole - inverted flags in output

[CAMEL-20280](https://issues.apache.org/jira/browse/CAMEL-20280)

camel-jcache - JCachePolicy does not init bypassExpression

[CAMEL-20262](https://issues.apache.org/jira/browse/CAMEL-20262)

camel-spring-boot - TomcatEmbeddedWebappClassLoader return nested instead file in jar file path

[CAMEL-20254](https://issues.apache.org/jira/browse/CAMEL-20254)

camel-http - pre-emptive authentication breaks basic auth

[CAMEL-20250](https://issues.apache.org/jira/browse/CAMEL-20250)

camel-kinesis: resume API fails to resume properly

[CAMEL-20248](https://issues.apache.org/jira/browse/CAMEL-20248)

camel-salesforce: Most integration tests failing

[CAMEL-20239](https://issues.apache.org/jira/browse/CAMEL-20239)

Camel-Azure-Files: The component doesn't set account parameter on the URI

[CAMEL-20232](https://issues.apache.org/jira/browse/CAMEL-20232)

camel-core - Kamelets with Enrich and PollEnrich dynamic endpoints with template parameters

[CAMEL-20218](https://issues.apache.org/jira/browse/CAMEL-20218)

KafkaIdempotentRepository cache incorrectly flagged as ready

[CAMEL-20121](https://issues.apache.org/jira/browse/CAMEL-20121)

camel-smpp SMPPSession should be closed after receiving Unbind from peer

[CAMEL-19972](https://issues.apache.org/jira/browse/CAMEL-19972)

camel-kafka manual commit configuration inconsistency

[CAMEL-19849](https://issues.apache.org/jira/browse/CAMEL-19849)

camel-zipfile: fails to release exchange due to Exceptions

[CAMEL-19262](https://issues.apache.org/jira/browse/CAMEL-19262)

camel-azure-eventbus - Apache Camel wrapper for Service Bus stops receiving message.

[CAMEL-17722](https://issues.apache.org/jira/browse/CAMEL-17722)

MDC - custom properties in MDC Unit Of Work are not cleared at the end of route

[CAMEL-17721](https://issues.apache.org/jira/browse/CAMEL-17721)

MDC - custom MDC property value is fixed to first assigned value by MDCUnitOfWork

### Dependency upgrade (6)

[CAMEL-20344](https://issues.apache.org/jira/browse/CAMEL-20344)

camel-spring-boot - Upgrade to 3.2.2

[CAMEL-20278](https://issues.apache.org/jira/browse/CAMEL-20278)

Upgrade Wildfly Elytron to 2.x version

[CAMEL-20116](https://issues.apache.org/jira/browse/CAMEL-20116)

Upgrade to Jackson BOM 2.16.0

[CAMEL-19971](https://issues.apache.org/jira/browse/CAMEL-19971)

Camel-Consul: Consul-client repository is now read only

[CAMEL-19722](https://issues.apache.org/jira/browse/CAMEL-19722)

camel-etcd3 - Upgrade jedtc to 0.7.6

[CAMEL-19620](https://issues.apache.org/jira/browse/CAMEL-19620)

camel-coap - Upgrade to Californium Scandium 3.x

### Improvement (52)

[CAMEL-20409](https://issues.apache.org/jira/browse/CAMEL-20409)

camel-core - ModelReifierFactory should detect custom on classpath

[CAMEL-20403](https://issues.apache.org/jira/browse/CAMEL-20403)

Support Knative broker as source/sink in Pipe

[CAMEL-20400](https://issues.apache.org/jira/browse/CAMEL-20400)

Support for Knative SinkBinding

[CAMEL-20398](https://issues.apache.org/jira/browse/CAMEL-20398)

camel-kubernetes - Add option on component to create kubernetes client

[CAMEL-20396](https://issues.apache.org/jira/browse/CAMEL-20396)

camel-kudu: Allow KuduClient to be autowired

[CAMEL-20391](https://issues.apache.org/jira/browse/CAMEL-20391)

camel-core - All languages should support expression loaded from external resource

[CAMEL-20387](https://issues.apache.org/jira/browse/CAMEL-20387)

camel-tracing - Use case insensitive headers

[CAMEL-20386](https://issues.apache.org/jira/browse/CAMEL-20386)

camel-jq - Add @JQ for bean annotation

[CAMEL-20382](https://issues.apache.org/jira/browse/CAMEL-20382)

camel-kafka - RecordMetadata header should be named like the other headers

[CAMEL-20376](https://issues.apache.org/jira/browse/CAMEL-20376)

camel-xpath - XPath language add support for variables

[CAMEL-20369](https://issues.apache.org/jira/browse/CAMEL-20369)

camel-beanio - Bring back beanio as v3

[CAMEL-20365](https://issues.apache.org/jira/browse/CAMEL-20365)

camel-ftp - Add option to configure yes/no answer to create known host file

[CAMEL-20364](https://issues.apache.org/jira/browse/CAMEL-20364)

camel-jms - Remove JMSCorrelationIDAsBytes header as its not needed

[CAMEL-20363](https://issues.apache.org/jira/browse/CAMEL-20363)

camel-jms - Make getting JMSCorrelationID more robust for brokers that has bugs

[CAMEL-20359](https://issues.apache.org/jira/browse/CAMEL-20359)

camel-groovy - Consistent name to refer to exchangeProperties

[CAMEL-20358](https://issues.apache.org/jira/browse/CAMEL-20358)

camel-microprofile-config: CamelMicroProfilePropertiesSource should consider active profiles when loading properties

[CAMEL-20355](https://issues.apache.org/jira/browse/CAMEL-20355)

Throttle EIP: milliseconds not available anymore

[CAMEL-20346](https://issues.apache.org/jira/browse/CAMEL-20346)

camel-core - Simple language contains function can be improved

[CAMEL-20345](https://issues.apache.org/jira/browse/CAMEL-20345)

camel-core - Simple binary operator in predicates better detected by predicate parser

[CAMEL-20308](https://issues.apache.org/jira/browse/CAMEL-20308)

Change order of camel-spring-boot-bom and spring-boot-dependencies in dependencyManamgent

[CAMEL-20306](https://issues.apache.org/jira/browse/CAMEL-20306)

Camel-CassandraQL: Add ObjectInputFilter String pattern parameter in CassandraAggregationRepository to be used in unmarshall operations

[CAMEL-20303](https://issues.apache.org/jira/browse/CAMEL-20303)

Camel-Sql: Add ObjectInputFilter String pattern parameter in JdbcAggregationRepository to be used in unmarshall operations

[CAMEL-20298](https://issues.apache.org/jira/browse/CAMEL-20298)

Enhancing JSONata Compatibility for Full Reference Port

[CAMEL-20281](https://issues.apache.org/jira/browse/CAMEL-20281)

Camel-AWS Components: Make it possible to use AwsSessionCredentials to support temporary credentials

[CAMEL-20275](https://issues.apache.org/jira/browse/CAMEL-20275)

components - Mark options that can are used for text inputs such as a SQL query

[CAMEL-20274](https://issues.apache.org/jira/browse/CAMEL-20274)

camel-management - Add option to allow updating routes

[CAMEL-20273](https://issues.apache.org/jira/browse/CAMEL-20273)

camel-jbang - Stub dataformat and language during export

[CAMEL-20271](https://issues.apache.org/jira/browse/CAMEL-20271)

Camel-AWS-Cloudtrail: Improve consumers by adding more information as exchange headers

[CAMEL-20258](https://issues.apache.org/jira/browse/CAMEL-20258)

\[JBang\] Use quartz out of the box for camel-cron

[CAMEL-20253](https://issues.apache.org/jira/browse/CAMEL-20253)

camel-jbang - Add support for jolokia 2.x

[CAMEL-20249](https://issues.apache.org/jira/browse/CAMEL-20249)

camel-jbang - Reload routes with micrometer should clean up old routes

[CAMEL-20247](https://issues.apache.org/jira/browse/CAMEL-20247)

Rework Dynamic Router EIP Component

[CAMEL-20246](https://issues.apache.org/jira/browse/CAMEL-20246)

camel-core - WireTap should not create correlated exchange copy

[CAMEL-20245](https://issues.apache.org/jira/browse/CAMEL-20245)

camel-jbang - Startup should log http summary if already started such as when using supervised route controller

[CAMEL-20243](https://issues.apache.org/jira/browse/CAMEL-20243)

camel-main - Move route controller options into its own group

[CAMEL-20242](https://issues.apache.org/jira/browse/CAMEL-20242)

camel-routes health check reports UP right before routes were attempted to be setup when using supervising route controller

[CAMEL-20241](https://issues.apache.org/jira/browse/CAMEL-20241)

camel-jbang - Pretty print xml body should not have noisy empty lines

[CAMEL-20238](https://issues.apache.org/jira/browse/CAMEL-20238)

Add spring-boot-starter-jdbc dependency to camel-spring-jdbc-starter

[CAMEL-20236](https://issues.apache.org/jira/browse/CAMEL-20236)

camel-salesforce: add missing properties to bulk 2.0 Job class

[CAMEL-20233](https://issues.apache.org/jira/browse/CAMEL-20233)

camel-jbang - camel catalog other does not list kotlin-dsl

[CAMEL-20231](https://issues.apache.org/jira/browse/CAMEL-20231)

camel-jasypt - make generators configurable

[CAMEL-20230](https://issues.apache.org/jira/browse/CAMEL-20230)

camel-core - PollEnrich and Enrich EIP should eager start component if possible

[CAMEL-20228](https://issues.apache.org/jira/browse/CAMEL-20228)

camel-jbang - camel export doesn't recognize component in pollenrich

[CAMEL-20219](https://issues.apache.org/jira/browse/CAMEL-20219)

Add Protobuf data type transformer

[CAMEL-20202](https://issues.apache.org/jira/browse/CAMEL-20202)

camel-azure - Consumers should avoid loading entire payload into memory

[CAMEL-19956](https://issues.apache.org/jira/browse/CAMEL-19956)

camel-jbang - Run with custom log4j2.properties file

[CAMEL-19413](https://issues.apache.org/jira/browse/CAMEL-19413)

camel-parquet-avro: add some defaulted values as options on dataformat to make it more configurable

[CAMEL-19411](https://issues.apache.org/jira/browse/CAMEL-19411)

camel-kamelet - Should be using noErrorHandler

[CAMEL-19398](https://issues.apache.org/jira/browse/CAMEL-19398)

camel-core: type converter performs slowly due to exception-based flow control

[CAMEL-18969](https://issues.apache.org/jira/browse/CAMEL-18969)

Support mongodb connection string/uri to configure camel-mongodb component

[CAMEL-18590](https://issues.apache.org/jira/browse/CAMEL-18590)

Camel-Azure components: Define a unique configuration for authentication

[CAMEL-14028](https://issues.apache.org/jira/browse/CAMEL-14028)

Allow DataFormats to unmarshal known data formats without first converting to bytes

### New Feature (25)

[CAMEL-20408](https://issues.apache.org/jira/browse/CAMEL-20408)

camel-core - Tracer should include exchange variables

[CAMEL-20406](https://issues.apache.org/jira/browse/CAMEL-20406)

camel-core - Route scoped variables

[CAMEL-20379](https://issues.apache.org/jira/browse/CAMEL-20379)

\[camel-test-infra-cli\] Improve container configuration, adding external maven repositories

[CAMEL-20338](https://issues.apache.org/jira/browse/CAMEL-20338)

Camel JMS producer should add headers

[CAMEL-20336](https://issues.apache.org/jira/browse/CAMEL-20336)

Add a WebAssembly component and language

[CAMEL-20333](https://issues.apache.org/jira/browse/CAMEL-20333)

Kotlin API

[CAMEL-20289](https://issues.apache.org/jira/browse/CAMEL-20289)

camel-core - FluentProducerTemplate - Add withVariable and withProperty

[CAMEL-20288](https://issues.apache.org/jira/browse/CAMEL-20288)

camel-core - Convert header and variable To another name

[CAMEL-20286](https://issues.apache.org/jira/browse/CAMEL-20286)

camel-netty: add support for native transport over KQueue

[CAMEL-20285](https://issues.apache.org/jira/browse/CAMEL-20285)

camel-json-validator: Add ability to configure ObjectMapper using endpoint properties

[CAMEL-20277](https://issues.apache.org/jira/browse/CAMEL-20277)

camel-grpc: gRPC proxy with streaming

[CAMEL-20270](https://issues.apache.org/jira/browse/CAMEL-20270)

Introduce plugins for Camel JBang

[CAMEL-20251](https://issues.apache.org/jira/browse/CAMEL-20251)

Add Camel K commands to Camel JBang

[CAMEL-20229](https://issues.apache.org/jira/browse/CAMEL-20229)

Camel-Azure-Storage-Queue: Add CloudEvents Data Type Transformer

[CAMEL-20223](https://issues.apache.org/jira/browse/CAMEL-20223)

Camel-Spring-Boot: Camel Azure Key Vault should Support Azure Identity in the component and secrets function

[CAMEL-20220](https://issues.apache.org/jira/browse/CAMEL-20220)

Camel Azure Key Vault: Support Azure Identity in the component and secrets function

[CAMEL-19749](https://issues.apache.org/jira/browse/CAMEL-19749)

camel-core - Allow users to use variables in route to store data instead of headers

[CAMEL-19241](https://issues.apache.org/jira/browse/CAMEL-19241)

Adding a Kafka Batch Consumer

[CAMEL-18559](https://issues.apache.org/jira/browse/CAMEL-18559)

Components which do remote communication should be marked as such

[CAMEL-18082](https://issues.apache.org/jira/browse/CAMEL-18082)

camel-jbang - Prompt mode for required values

[CAMEL-17825](https://issues.apache.org/jira/browse/CAMEL-17825)

Hash generator in the Simple language

[CAMEL-17719](https://issues.apache.org/jira/browse/CAMEL-17719)

camel-salesforce: allow to retrieve CDC json schema from meta service

[CAMEL-16064](https://issues.apache.org/jira/browse/CAMEL-16064)

camel-kafka - Add batching consumer

[CAMEL-15570](https://issues.apache.org/jira/browse/CAMEL-15570)

camel-jte - Template Engine component

[CAMEL-15252](https://issues.apache.org/jira/browse/CAMEL-15252)

Google Pubsub Component manual acknowledgement mode

### Sub-task (1)

[CAMEL-20007](https://issues.apache.org/jira/browse/CAMEL-20007)

Java 21 - Fix test failures related to Ignite component

### Task (29)

[CAMEL-20397](https://issues.apache.org/jira/browse/CAMEL-20397)

camel-jms: fix incorrect details regarding JMS 1.1 and 2.0

[CAMEL-20384](https://issues.apache.org/jira/browse/CAMEL-20384)

modernization: modernize map operations

[CAMEL-20366](https://issues.apache.org/jira/browse/CAMEL-20366)

Dependabot: Define some exclusions in the yaml configuration

[CAMEL-20360](https://issues.apache.org/jira/browse/CAMEL-20360)

camel-jasypt: Improve and tidy documentation

[CAMEL-20347](https://issues.apache.org/jira/browse/CAMEL-20347)

Improve handling of interrupts

[CAMEL-20335](https://issues.apache.org/jira/browse/CAMEL-20335)

spring-xml build error using \`/component-test\` on GitHub Actions

[CAMEL-20305](https://issues.apache.org/jira/browse/CAMEL-20305)

camel-core: ensure log consistency

[CAMEL-20297](https://issues.apache.org/jira/browse/CAMEL-20297)

Swallowing interrupts

[CAMEL-20296](https://issues.apache.org/jira/browse/CAMEL-20296)

Allow testing through /component-test for projects having \`it\` folders

[CAMEL-20294](https://issues.apache.org/jira/browse/CAMEL-20294)

camel-facebook: review and/or deprecate

[CAMEL-20283](https://issues.apache.org/jira/browse/CAMEL-20283)

camel-elasticsearch - Deprecate

[CAMEL-20279](https://issues.apache.org/jira/browse/CAMEL-20279)

Fix issue related to some flaky tests using test container with AWS localstack or hashicorp

[CAMEL-20268](https://issues.apache.org/jira/browse/CAMEL-20268)

Several classes are reformatted during mvn install, causing pull/merge issues

[CAMEL-20267](https://issues.apache.org/jira/browse/CAMEL-20267)

camel-core: convert Throttler and SamplingThrottler to a monotonic time source

[CAMEL-20264](https://issues.apache.org/jira/browse/CAMEL-20264)

AvailablePortFinder is duplicated

[CAMEL-20261](https://issues.apache.org/jira/browse/CAMEL-20261)

camel-http ignoreCookies option value has been renamed

[CAMEL-20260](https://issues.apache.org/jira/browse/CAMEL-20260)

Remove Camel HDFS Starter

[CAMEL-20259](https://issues.apache.org/jira/browse/CAMEL-20259)

Remove Camel-HDFS Component

[CAMEL-20257](https://issues.apache.org/jira/browse/CAMEL-20257)

camel-core: convert AbstractContext to the clock API

[CAMEL-20256](https://issues.apache.org/jira/browse/CAMEL-20256)

camel-core: convert Throughput logger to a monotonic time source

[CAMEL-20252](https://issues.apache.org/jira/browse/CAMEL-20252)

camel-core: review performance tests

[CAMEL-20235](https://issues.apache.org/jira/browse/CAMEL-20235)

camel-kafka: consolidate commit management behavior between component and endpoint

[CAMEL-20234](https://issues.apache.org/jira/browse/CAMEL-20234)

camel-core: consolidate / simplify exchange constructors

[CAMEL-20225](https://issues.apache.org/jira/browse/CAMEL-20225)

camel-core: modernize management of duration and timestamps

[CAMEL-20224](https://issues.apache.org/jira/browse/CAMEL-20224)

Deprecate milliseconds-based input from StopWatch

[CAMEL-20169](https://issues.apache.org/jira/browse/CAMEL-20169)

camel-salesforce restore ResponseNotifier

[CAMEL-19746](https://issues.apache.org/jira/browse/CAMEL-19746)

\[DOCS \] Camel-mybatis component - missing code examples

[CAMEL-19519](https://issues.apache.org/jira/browse/CAMEL-19519)

camel-file: replace Thread.sleep in tests

[CAMEL-19338](https://issues.apache.org/jira/browse/CAMEL-19338)

Add integration tests for camel-jbang

### Test (6)

[CAMEL-20389](https://issues.apache.org/jira/browse/CAMEL-20389)

Fix incorrectly named integration tests

[CAMEL-20353](https://issues.apache.org/jira/browse/CAMEL-20353)

camel-rest-openapi: test broken after swagger upgrade

[CAMEL-20295](https://issues.apache.org/jira/browse/CAMEL-20295)

camel-grpc: Enable tests to run on more platforms

[CAMEL-20284](https://issues.apache.org/jira/browse/CAMEL-20284)

camel-ignite - Enable tests on JDK21

[CAMEL-20276](https://issues.apache.org/jira/browse/CAMEL-20276)

camel-jms: shared topic tests are broken

[CAMEL-20269](https://issues.apache.org/jira/browse/CAMEL-20269)

camel-test-infra-artemis: concurrency issues

### Wish (1)

[CAMEL-18482](https://issues.apache.org/jira/browse/CAMEL-18482)

camel-core - Pre 3.13 Split EIP behaviour

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).