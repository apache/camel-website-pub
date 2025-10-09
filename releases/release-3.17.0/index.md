# Apache camel 3.17.0 Release

## New and Noteworthy

This release is the new Camel 3.17.0 release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.17.0</version>
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
      <version>3.17.0</version>
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
| [apache-camel-3.17.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.17.0/apache-camel-3.17.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.17.0/apache-camel-3.17.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.17.0/apache-camel-3.17.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.17.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.17.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (35)

[CAMEL-18470](https://issues.apache.org/jira/browse/CAMEL-18470)

camel-rabbitmq - skipQueueDeclare option is not working in 3.18.1. was working in 3.14.x

[CAMEL-18101](https://issues.apache.org/jira/browse/CAMEL-18101)

camel-core - Pooled exchanges with netty-http/jetty/servlet can cause reference leaks

[CAMEL-18100](https://issues.apache.org/jira/browse/CAMEL-18100)

camel-karaf - Cannot load OSGi blueprint due to Resumable classloading hell

[CAMEL-18091](https://issues.apache.org/jira/browse/CAMEL-18091)

camel-jbang - Health Check should report HTTP status codes for DOWN

[CAMEL-18089](https://issues.apache.org/jira/browse/CAMEL-18089)

camel-spring-boot - IllegalThreadStateException when trying to resume suspended Camel context

[CAMEL-18088](https://issues.apache.org/jira/browse/CAMEL-18088)

camel-aws2-sqs - Property messageHeaderExceededLimit doesn't work

[CAMEL-18084](https://issues.apache.org/jira/browse/CAMEL-18084)

camel-jbang - Run from gist with a kamelet cannot determine its file extension

[CAMEL-18064](https://issues.apache.org/jira/browse/CAMEL-18064)

Cannot set server side encryption SSE-S3 for S3 bucket

[CAMEL-18063](https://issues.apache.org/jira/browse/CAMEL-18063)

camel-jbang - Using --deps for debug may store null as GAV version

[CAMEL-18054](https://issues.apache.org/jira/browse/CAMEL-18054)

camel-jbang - Using --deps cannot download

[CAMEL-18052](https://issues.apache.org/jira/browse/CAMEL-18052)

openapi-rest-dsl-generator - Generates wrong yaml

[CAMEL-18015](https://issues.apache.org/jira/browse/CAMEL-18015)

camel-jt400 - Endpoint syntax is wrong in metadata

[CAMEL-17996](https://issues.apache.org/jira/browse/CAMEL-17996)

camel-microprofile-config: CamelMicroProfilePropertiesSource loadProperties cannot handle empty property values

[CAMEL-17992](https://issues.apache.org/jira/browse/CAMEL-17992)

camel-netty-starter - camel.component.netty.ssl-context-parameters does not work

[CAMEL-17979](https://issues.apache.org/jira/browse/CAMEL-17979)

camel-salesforce: field values are not restored correctly after operation

[CAMEL-17975](https://issues.apache.org/jira/browse/CAMEL-17975)

camel-core - Route watch reload will not start routes again if previous failed

[CAMEL-17948](https://issues.apache.org/jira/browse/CAMEL-17948)

Race condition in MockEndpoint with PER\_CLASS tests

[CAMEL-17940](https://issues.apache.org/jira/browse/CAMEL-17940)

Quartz Scheduler - unscheduleTask should check if scheduler is clustered

[CAMEL-17927](https://issues.apache.org/jira/browse/CAMEL-17927)

camel-jbang - Run from github issue with classpath resources

[CAMEL-17922](https://issues.apache.org/jira/browse/CAMEL-17922)

\[camel-web3j\] Incorrect default value supplier for header MIX\_DIGEST

[CAMEL-17912](https://issues.apache.org/jira/browse/CAMEL-17912)

camel-sjms2 - preserveMessageQoS seems to not work as expected

[CAMEL-17910](https://issues.apache.org/jira/browse/CAMEL-17910)

camel-jms - InOut with reply-to-type shared - race condition

[CAMEL-17901](https://issues.apache.org/jira/browse/CAMEL-17901)

camel-google-pubsub - concurrent access error on shutdown

[CAMEL-17886](https://issues.apache.org/jira/browse/CAMEL-17886)

MockValueBuilder behaves false positive

[CAMEL-17884](https://issues.apache.org/jira/browse/CAMEL-17884)

Guava is overriden to an older version in bigquery starter

[CAMEL-17883](https://issues.apache.org/jira/browse/CAMEL-17883)

camel-salesforce: DTO template has bad import

[CAMEL-17867](https://issues.apache.org/jira/browse/CAMEL-17867)

camel-main - NPE during stopping all routes

[CAMEL-17866](https://issues.apache.org/jira/browse/CAMEL-17866)

camel-sql: CamelSqlGeneratedKeyRows is not populated if already exists

[CAMEL-17865](https://issues.apache.org/jira/browse/CAMEL-17865)

camel-platform-http-vertx: CORS conflict in Camel REST

[CAMEL-17861](https://issues.apache.org/jira/browse/CAMEL-17861)

Streaming in Azure (Blob-Storage) component not working

[CAMEL-17857](https://issues.apache.org/jira/browse/CAMEL-17857)

camel-validator: remote xsd import not usable

[CAMEL-17850](https://issues.apache.org/jira/browse/CAMEL-17850)

camel-kafka: lock concurrency issue in the record fetcher

[CAMEL-17712](https://issues.apache.org/jira/browse/CAMEL-17712)

Memory leak in DefaultCamelContext reported by Tomcat 10

[CAMEL-17613](https://issues.apache.org/jira/browse/CAMEL-17613)

camel-sql - Race condition in AggregateProcessor with Jdbc Repository

[CAMEL-17588](https://issues.apache.org/jira/browse/CAMEL-17588)

Missing Clean-Up for DefaultReactiveExecutor.Worker-ThreadLocals

### Dependency upgrade (13)

[CAMEL-18107](https://issues.apache.org/jira/browse/CAMEL-18107)

camel-jbang - Upgrade to Kamelets 0.8.1

[CAMEL-18102](https://issues.apache.org/jira/browse/CAMEL-18102)

Upgrade Google Cloud Libraries BOM to 25.2.0

[CAMEL-18075](https://issues.apache.org/jira/browse/CAMEL-18075)

upgrade maven-bundle-plugin, fixes OSGi reproducibility issues

[CAMEL-18047](https://issues.apache.org/jira/browse/CAMEL-18047)

Upgrade jakarta.mail to 1.6.7

[CAMEL-18030](https://issues.apache.org/jira/browse/CAMEL-18030)

camel-jclouds - Upgrade to 2.5.x

[CAMEL-18011](https://issues.apache.org/jira/browse/CAMEL-18011)

upgrade to spring boot 2.6.7

[CAMEL-18000](https://issues.apache.org/jira/browse/CAMEL-18000)

camel-johnzon - Upgrade to 1.2.17

[CAMEL-17958](https://issues.apache.org/jira/browse/CAMEL-17958)

upgrade testcontainers to 1.17.x

[CAMEL-17950](https://issues.apache.org/jira/browse/CAMEL-17950)

camel-debezium - Upgrade to 1.9

[CAMEL-17899](https://issues.apache.org/jira/browse/CAMEL-17899)

spring4shell CVE means spring upgrades needed

[CAMEL-17877](https://issues.apache.org/jira/browse/CAMEL-17877)

camel-karaf - Missing dependency of JSON schema validator

[CAMEL-17832](https://issues.apache.org/jira/browse/CAMEL-17832)

camel-grpc - Does not work with netty 4.1.75

[CAMEL-17537](https://issues.apache.org/jira/browse/CAMEL-17537)

camel-djl - Upgrade to 0.16.0

### Improvement (90)

[CAMEL-18109](https://issues.apache.org/jira/browse/CAMEL-18109)

camel-yaml-dsl - Add backwards compatible loading of older routes/kamelets

[CAMEL-18106](https://issues.apache.org/jira/browse/CAMEL-18106)

camel-core - Optimize ExchangeHelper.getCharsetName(exchange)

[CAMEL-18104](https://issues.apache.org/jira/browse/CAMEL-18104)

camel-core: provide a byte\[\] to Double Integer .... converter

[CAMEL-18098](https://issues.apache.org/jira/browse/CAMEL-18098)

camel-core - Stream caching should not spool to disk by default

[CAMEL-18087](https://issues.apache.org/jira/browse/CAMEL-18087)

camel-core - Enable stream caching by default

[CAMEL-18086](https://issues.apache.org/jira/browse/CAMEL-18086)

camel-jbang - Uber Jar - Build from fresh without starting actual components

[CAMEL-18085](https://issues.apache.org/jira/browse/CAMEL-18085)

ManagementStatisticsLevel.RoutesOnly does not prevent creation of processors' statisctics

[CAMEL-18076](https://issues.apache.org/jira/browse/CAMEL-18076)

camel-core - Optimize ExchangeHelper getDefaultCharsetName

[CAMEL-18074](https://issues.apache.org/jira/browse/CAMEL-18074)

camel-jbang - Rename CamelJBang to Camel in app

[CAMEL-18069](https://issues.apache.org/jira/browse/CAMEL-18069)

camel-aws2-s3: Configure S3Presigner with URI endpoint override if required for download links

[CAMEL-18067](https://issues.apache.org/jira/browse/CAMEL-18067)

camel-jbang - Allow to provide custom log4j2.properties

[CAMEL-18066](https://issues.apache.org/jira/browse/CAMEL-18066)

OpenApi Specification Generator: Add support for discriminator for xOf

[CAMEL-18065](https://issues.apache.org/jira/browse/CAMEL-18065)

OpenApi Specification Generator - Support multiple tags for an operation

[CAMEL-18060](https://issues.apache.org/jira/browse/CAMEL-18060)

camel-jbang - Add option to turn off logging colours

[CAMEL-18059](https://issues.apache.org/jira/browse/CAMEL-18059)

camel-jsonpath - Add result type to jsonpathWriteAsString

[CAMEL-18056](https://issues.apache.org/jira/browse/CAMEL-18056)

camel-jbang - Dependency downloader - Use thread pool and report progress

[CAMEL-18053](https://issues.apache.org/jira/browse/CAMEL-18053)

camel-jbang - HTTP endpoint can list duplicates

[CAMEL-18050](https://issues.apache.org/jira/browse/CAMEL-18050)

camel-jbang - Package uber jar without first run

[CAMEL-18046](https://issues.apache.org/jira/browse/CAMEL-18046)

camel-salesforce: Support sObjectName parameter for query operations

[CAMEL-18040](https://issues.apache.org/jira/browse/CAMEL-18040)

OpenApi Specification Generator Does not generate oneOf, allOf and anyOf when annotation @Schema(oneOf|allOf|anyOf = {X.class, Y.class}) is specified on a class

[CAMEL-18037](https://issues.apache.org/jira/browse/CAMEL-18037)

camel-jbang - Have a higher shutdown timeout

[CAMEL-18035](https://issues.apache.org/jira/browse/CAMEL-18035)

camel-jbang - Run \* should better detect what is Camel routes and what are misc files

[CAMEL-18034](https://issues.apache.org/jira/browse/CAMEL-18034)

camel-jbang - Rename --reload to --dev

[CAMEL-18032](https://issues.apache.org/jira/browse/CAMEL-18032)

camel-jbang - Skip including docker-compose files

[CAMEL-18029](https://issues.apache.org/jira/browse/CAMEL-18029)

camel-jbang - Uber Jar - Specify custom properties file to override what was packaged

[CAMEL-18028](https://issues.apache.org/jira/browse/CAMEL-18028)

camel-jbang - camel run without args

[CAMEL-18026](https://issues.apache.org/jira/browse/CAMEL-18026)

camel-rest - Rest DSL - Output more fine grained http endpoints that are available

[CAMEL-18025](https://issues.apache.org/jira/browse/CAMEL-18025)

camel-jbang - Terminating running app with ctrl + c then has little to no logging output

[CAMEL-18023](https://issues.apache.org/jira/browse/CAMEL-18023)

camel-jbang command options from application.properties

[CAMEL-18021](https://issues.apache.org/jira/browse/CAMEL-18021)

camel-debezium - Add support of default value for list to the maven-plugin

[CAMEL-18016](https://issues.apache.org/jira/browse/CAMEL-18016)

Missing parameters for maven generate mojos

[CAMEL-18012](https://issues.apache.org/jira/browse/CAMEL-18012)

Fixed / Hard coded (additional) timeout value in DefaultMainShutdownStrategy should be made configurable

[CAMEL-18010](https://issues.apache.org/jira/browse/CAMEL-18010)

camel-jbang - Resolved downloaded JARs should consider jbang CP

[CAMEL-18008](https://issues.apache.org/jira/browse/CAMEL-18008)

camel-jbang deploy/undeploy command

[CAMEL-18006](https://issues.apache.org/jira/browse/CAMEL-18006)

camel-jbang package image command

[CAMEL-17997](https://issues.apache.org/jira/browse/CAMEL-17997)

camel-jbang - Reduce number of dependencies

[CAMEL-17995](https://issues.apache.org/jira/browse/CAMEL-17995)

REST DSL YAML Generator should optionally generate routes

[CAMEL-17990](https://issues.apache.org/jira/browse/CAMEL-17990)

FileInputStreamCache is missing some InputStream delegates

[CAMEL-17989](https://issues.apache.org/jira/browse/CAMEL-17989)

REST DSL YAML Generator uses incorrect 'to' tag

[CAMEL-17985](https://issues.apache.org/jira/browse/CAMEL-17985)

camel-core - ResourceHelper does not support ref: scheme

[CAMEL-17984](https://issues.apache.org/jira/browse/CAMEL-17984)

REST DSL generator in camel-jbang

[CAMEL-17980](https://issues.apache.org/jira/browse/CAMEL-17980)

camel-jbang - File lock should be false by default

[CAMEL-17978](https://issues.apache.org/jira/browse/CAMEL-17978)

camel-jbang - Skip adding readme files to classpath

[CAMEL-17977](https://issues.apache.org/jira/browse/CAMEL-17977)

camel-jbang - Output JVM name/version when starting up

[CAMEL-17974](https://issues.apache.org/jira/browse/CAMEL-17974)

camel-jbang - Reload local kamelets

[CAMEL-17973](https://issues.apache.org/jira/browse/CAMEL-17973)

camel-endpoint-dsl - Add overloaded java type so fluent builder can include special types

[CAMEL-17972](https://issues.apache.org/jira/browse/CAMEL-17972)

camel-main - Property placeholder kamelets summary

[CAMEL-17968](https://issues.apache.org/jira/browse/CAMEL-17968)

camel-jbang - Add option to specify override property

[CAMEL-17956](https://issues.apache.org/jira/browse/CAMEL-17956)

JSONPath option to use global registered ObjectMapper

[CAMEL-17944](https://issues.apache.org/jira/browse/CAMEL-17944)

camel-platform-http-vertx - Should disable file uploads by default

[CAMEL-17943](https://issues.apache.org/jira/browse/CAMEL-17943)

camel-core - Method call expression should not be required

[CAMEL-17935](https://issues.apache.org/jira/browse/CAMEL-17935)

camel-cassandraql: Use ClassLoadingAwareObjectInputStream in CassandraCamelCodec

[CAMEL-17934](https://issues.apache.org/jira/browse/CAMEL-17934)

camel-cassandraql: Provide a ClassLoder to CqlSessionBuilder

[CAMEL-17930](https://issues.apache.org/jira/browse/CAMEL-17930)

camel-yaml-dsl - Yaml schema - generate enums for logging levels

[CAMEL-17924](https://issues.apache.org/jira/browse/CAMEL-17924)

Only expose public headers in the documentation

[CAMEL-17923](https://issues.apache.org/jira/browse/CAMEL-17923)

Add the name of the constant to the header model

[CAMEL-17921](https://issues.apache.org/jira/browse/CAMEL-17921)

Some Hazelcast operations are misspelled

[CAMEL-17918](https://issues.apache.org/jira/browse/CAMEL-17918)

Define the header name provider in case the headers class is an enum

[CAMEL-17916](https://issues.apache.org/jira/browse/CAMEL-17916)

camel-bean: Make BeanInfo handle Quarkus Arc Client Proxy generated classes

[CAMEL-17913](https://issues.apache.org/jira/browse/CAMEL-17913)

camel-kafka - Not able to set IsolationLevel using consumer parameters

[CAMEL-17903](https://issues.apache.org/jira/browse/CAMEL-17903)

camel-component-maven-plugin - Add doc about recompile

[CAMEL-17902](https://issues.apache.org/jira/browse/CAMEL-17902)

camel-opentelemetry - OTEL MDC keys are not matching OTEL keys

[CAMEL-17898](https://issues.apache.org/jira/browse/CAMEL-17898)

Allow to retrieve header definitions from super classes

[CAMEL-17896](https://issues.apache.org/jira/browse/CAMEL-17896)

Extract the description of an header from the Javadoc by default

[CAMEL-17893](https://issues.apache.org/jira/browse/CAMEL-17893)

camel-yaml-dsl - Remove endpoint uri inlined mode

[CAMEL-17885](https://issues.apache.org/jira/browse/CAMEL-17885)

camel google bigquery: Allow to read service account key file from resolver

[CAMEL-17872](https://issues.apache.org/jira/browse/CAMEL-17872)

camel-spring-boot - Archetype should use camel-spring-boot-bom

[CAMEL-17871](https://issues.apache.org/jira/browse/CAMEL-17871)

camel-google-pubsub - Graceful shutdown for synchronous pull consumers

[CAMEL-17868](https://issues.apache.org/jira/browse/CAMEL-17868)

camel-core - json dataformat - more options should be advanced

[CAMEL-17863](https://issues.apache.org/jira/browse/CAMEL-17863)

camel-main - Is loading routes from directory twice due to early modeline detection

[CAMEL-17854](https://issues.apache.org/jira/browse/CAMEL-17854)

Camel-AWS-SNS: support byte arrays when mapping camel headers to sns attribute

[CAMEL-17849](https://issues.apache.org/jira/browse/CAMEL-17849)

camel-kafka: invalid log message on shutdown when using topic patterns

[CAMEL-17844](https://issues.apache.org/jira/browse/CAMEL-17844)

camel-bean: @Handler annotation doesn't work with FunctionalInterfaces

[CAMEL-17843](https://issues.apache.org/jira/browse/CAMEL-17843)

camel-test-infra-kafka: improve support for ARM

[CAMEL-17839](https://issues.apache.org/jira/browse/CAMEL-17839)

camel-health - Route health check - allow to configure initial state

[CAMEL-17837](https://issues.apache.org/jira/browse/CAMEL-17837)

camel-main - Loading properties from multiple PropertiesSource - Keys with difference case styles

[CAMEL-17835](https://issues.apache.org/jira/browse/CAMEL-17835)

Switch jsch from com.jcraft to com.github.mwiede

[CAMEL-17821](https://issues.apache.org/jira/browse/CAMEL-17821)

Pre-configure Camel main examples to be ready for textual debugging

[CAMEL-17816](https://issues.apache.org/jira/browse/CAMEL-17816)

aws2-sqs: support byte arrays when mapping camel headers to sqs attribute

[CAMEL-17806](https://issues.apache.org/jira/browse/CAMEL-17806)

camel-yaml-dsl - Better parser error with source loc:line of the problem

[CAMEL-17802](https://issues.apache.org/jira/browse/CAMEL-17802)

Check whether we need to manually commit offset upon stop when auto commit is enabled

[CAMEL-17784](https://issues.apache.org/jira/browse/CAMEL-17784)

camel-java-dsl - Joor to support multiple files compiled as single unit

[CAMEL-17714](https://issues.apache.org/jira/browse/CAMEL-17714)

Missing metadata in camel-catalog

[CAMEL-17705](https://issues.apache.org/jira/browse/CAMEL-17705)

Camel Salesforce - Http Client timeout is hardcoded

[CAMEL-17644](https://issues.apache.org/jira/browse/CAMEL-17644)

Support ability to load properties from Vault/Secrets cloud services

[CAMEL-17615](https://issues.apache.org/jira/browse/CAMEL-17615)

camel-kafka: cleanup Kafka client warnings

[CAMEL-17562](https://issues.apache.org/jira/browse/CAMEL-17562)

camel-yaml-dsl - Remove deprecated spec/flow in kamelet loader

[CAMEL-17515](https://issues.apache.org/jira/browse/CAMEL-17515)

Provide an option to mark Camel readiness as DOWN during graceful shutdown

[CAMEL-17512](https://issues.apache.org/jira/browse/CAMEL-17512)

Make tracing SpanDecorators work better with toD

[CAMEL-8781](https://issues.apache.org/jira/browse/CAMEL-8781)

camel-sip - SipConfiguration should be plain getter/setter

### New Feature (25)

[CAMEL-18080](https://issues.apache.org/jira/browse/CAMEL-18080)

camel-jbang - Run from clipboard

[CAMEL-18077](https://issues.apache.org/jira/browse/CAMEL-18077)

camel-github - Add gist resource resolver

[CAMEL-18072](https://issues.apache.org/jira/browse/CAMEL-18072)

mongodb: add a type converter to convert from byte\[\] to Document

[CAMEL-18018](https://issues.apache.org/jira/browse/CAMEL-18018)

camel-java-dsl - Add option to compile to disk to pre-load on next run

[CAMEL-18014](https://issues.apache.org/jira/browse/CAMEL-18014)

camel-java-dsl - Allow to capture compiled byte code

[CAMEL-18001](https://issues.apache.org/jira/browse/CAMEL-18001)

Support route generation from OpenAPi in jbang

[CAMEL-17998](https://issues.apache.org/jira/browse/CAMEL-17998)

camel-jbang - fat-jar command

[CAMEL-17991](https://issues.apache.org/jira/browse/CAMEL-17991)

camel-jbang - camel init - download source from github to local

[CAMEL-17981](https://issues.apache.org/jira/browse/CAMEL-17981)

Support --deps for Jbang

[CAMEL-17969](https://issues.apache.org/jira/browse/CAMEL-17969)

camel-main - Property-placeholder summary

[CAMEL-17967](https://issues.apache.org/jira/browse/CAMEL-17967)

camel-jbang - Init command like camel-k

[CAMEL-17897](https://issues.apache.org/jira/browse/CAMEL-17897)

camel-exec fail exit code

[CAMEL-17892](https://issues.apache.org/jira/browse/CAMEL-17892)

camel-rabbitmq - Bind queue to exchange even when declarations were skipped

[CAMEL-17831](https://issues.apache.org/jira/browse/CAMEL-17831)

camel-main - Auto configuration summary (show from where the option was taken)

[CAMEL-17820](https://issues.apache.org/jira/browse/CAMEL-17820)

camel-jbang - Add option to include resources to classpath

[CAMEL-17819](https://issues.apache.org/jira/browse/CAMEL-17819)

camel-jbang - Can we support --opena-api like camel-k have

[CAMEL-17818](https://issues.apache.org/jira/browse/CAMEL-17818)

camel-salesforce: "Stream List" for query results

[CAMEL-17792](https://issues.apache.org/jira/browse/CAMEL-17792)

Add documentation about the message headers

[CAMEL-17762](https://issues.apache.org/jira/browse/CAMEL-17762)

camel-resume-api: improvements and additional support

[CAMEL-17687](https://issues.apache.org/jira/browse/CAMEL-17687)

Create a Camel Azure Key Vault component

[CAMEL-17261](https://issues.apache.org/jira/browse/CAMEL-17261)

camel-jbang - Bind goal

[CAMEL-17051](https://issues.apache.org/jira/browse/CAMEL-17051)

camel-kafka: Need the ability to pause kafka consumer

[CAMEL-16757](https://issues.apache.org/jira/browse/CAMEL-16757)

camel-core - Allow to define global error handling in all DSL the same way

[CAMEL-15016](https://issues.apache.org/jira/browse/CAMEL-15016)

camel-kafka - Add support for Kafka transactions

[CAMEL-9190](https://issues.apache.org/jira/browse/CAMEL-9190)

support SIP MESSAGE method (IM/chat messaging)

### Sub-task (3)

[CAMEL-17686](https://issues.apache.org/jira/browse/CAMEL-17686)

Support ability to load properties from Vault/Secrets cloud services - Azure Key Vault

[CAMEL-17092](https://issues.apache.org/jira/browse/CAMEL-17092)

Debezium 1.7.0 - Oracle Connector

[CAMEL-17091](https://issues.apache.org/jira/browse/CAMEL-17091)

Debezium 1.7.0 - DB2 Connector

### Task (29)

[CAMEL-18138](https://issues.apache.org/jira/browse/CAMEL-18138)

camel-spring - XSD schema not updated in right path on website

[CAMEL-18071](https://issues.apache.org/jira/browse/CAMEL-18071)

Camel-http-platform-starter compilation problem in test module

[CAMEL-18068](https://issues.apache.org/jira/browse/CAMEL-18068)

Upgrade Azure dependencies based on com.azure:azure-sdk-bom:1.2.1

[CAMEL-18055](https://issues.apache.org/jira/browse/CAMEL-18055)

Create tracing SpanDecorator for ServiceBusComponent

[CAMEL-18048](https://issues.apache.org/jira/browse/CAMEL-18048)

Camel Spring boot Webhook Example

[CAMEL-18024](https://issues.apache.org/jira/browse/CAMEL-18024)

camel-kafka: rework last processed offset tracking

[CAMEL-18020](https://issues.apache.org/jira/browse/CAMEL-18020)

camel-kafka: The poll exception strategy is not properly initialized

[CAMEL-18019](https://issues.apache.org/jira/browse/CAMEL-18019)

camel-kafka: review fields for concurrent access

[CAMEL-17965](https://issues.apache.org/jira/browse/CAMEL-17965)

Camel-file: There is an unknowm parameter in documentation\`overruleFile\`

[CAMEL-17964](https://issues.apache.org/jira/browse/CAMEL-17964)

Camel website build broken due to non -relative link https://camel.apache.org/components/latest/others/main.md#\_specifying\_custom\_beans

[CAMEL-17962](https://issues.apache.org/jira/browse/CAMEL-17962)

Cleanup duplicated charsets

[CAMEL-17961](https://issues.apache.org/jira/browse/CAMEL-17961)

Could not locate xref:js/camel.js

[CAMEL-17957](https://issues.apache.org/jira/browse/CAMEL-17957)

camel-cxf - OSGi import range too restrictive

[CAMEL-17952](https://issues.apache.org/jira/browse/CAMEL-17952)

Several Hazelcast tests fail on Github

[CAMEL-17945](https://issues.apache.org/jira/browse/CAMEL-17945)

Fix the unstable test HazelcastSedaTransferExchangeTest

[CAMEL-17939](https://issues.apache.org/jira/browse/CAMEL-17939)

camel-main - Configure camel.beans map style using square brackets

[CAMEL-17937](https://issues.apache.org/jira/browse/CAMEL-17937)

camel-kafka - SSL configuration is common not producer only

[CAMEL-17931](https://issues.apache.org/jira/browse/CAMEL-17931)

camel-mongodb - Headers which starts with underscore causes website build problems

[CAMEL-17917](https://issues.apache.org/jira/browse/CAMEL-17917)

camel-mail - Documentation refers to missing example/demonstration code

[CAMEL-17882](https://issues.apache.org/jira/browse/CAMEL-17882)

Camel-Spring-Boot: Create a Camel Azure Key Vault component starter

[CAMEL-17879](https://issues.apache.org/jira/browse/CAMEL-17879)

Remove outdated components

[CAMEL-17864](https://issues.apache.org/jira/browse/CAMEL-17864)

maven-plugin-upgrades causes ERROR to be logged

[CAMEL-17862](https://issues.apache.org/jira/browse/CAMEL-17862)

camel-spring-boot - Dependencies generated add hadoop2 classifier

[CAMEL-17847](https://issues.apache.org/jira/browse/CAMEL-17847)

camel-examples - Some examples potentially fail or has problems

[CAMEL-17810](https://issues.apache.org/jira/browse/CAMEL-17810)

camel-resume-api: improve behavior with the master-component

[CAMEL-17763](https://issues.apache.org/jira/browse/CAMEL-17763)

camel-tests: cleanup unused exceptions in test code

[CAMEL-17560](https://issues.apache.org/jira/browse/CAMEL-17560)

camel-yaml-dsl - Remove deprecated spec/flow from loader

[CAMEL-17462](https://issues.apache.org/jira/browse/CAMEL-17462)

camel-atomix: likely incompatible with JDK 17

[CAMEL-16958](https://issues.apache.org/jira/browse/CAMEL-16958)

Camel and JDK17

### Test (26)

[CAMEL-18043](https://issues.apache.org/jira/browse/CAMEL-18043)

add tests in camel-mllp-starter

[CAMEL-18038](https://issues.apache.org/jira/browse/CAMEL-18038)

add tests in camel-validator-starter

[CAMEL-18036](https://issues.apache.org/jira/browse/CAMEL-18036)

add tests in camel-bean-validator-starter

[CAMEL-18009](https://issues.apache.org/jira/browse/CAMEL-18009)

add tests in camel-mail-starter

[CAMEL-18005](https://issues.apache.org/jira/browse/CAMEL-18005)

add tests in camel-paho-starter

[CAMEL-18002](https://issues.apache.org/jira/browse/CAMEL-18002)

Camel-netty-http: Test NettyHttpSimpleUriParametersTest fails.

[CAMEL-17994](https://issues.apache.org/jira/browse/CAMEL-17994)

Camel-aws2-kinesis: Integration test does not work - KinesisComponentManualIT

[CAMEL-17993](https://issues.apache.org/jira/browse/CAMEL-17993)

Add tests in camel-ftp-starter

[CAMEL-17988](https://issues.apache.org/jira/browse/CAMEL-17988)

add tests in camel-quartz-starter

[CAMEL-17987](https://issues.apache.org/jira/browse/CAMEL-17987)

log4j-slf4j-impl cannot be present with log4j-to-slf4j running CamelWebhookTest in camel-spring-boot

[CAMEL-17983](https://issues.apache.org/jira/browse/CAMEL-17983)

add tests in camel-zipfile-starter

[CAMEL-17959](https://issues.apache.org/jira/browse/CAMEL-17959)

Add tests in camel-file-starter

[CAMEL-17955](https://issues.apache.org/jira/browse/CAMEL-17955)

camel-mock - A few tests are failing since the recent mock change

[CAMEL-17954](https://issues.apache.org/jira/browse/CAMEL-17954)

IntegrationTest in camel-salesforce-component is broken

[CAMEL-17936](https://issues.apache.org/jira/browse/CAMEL-17936)

add tests in camel-salesforce-starter

[CAMEL-17908](https://issues.apache.org/jira/browse/CAMEL-17908)

add tests in camel-bindy-starter

[CAMEL-17900](https://issues.apache.org/jira/browse/CAMEL-17900)

add tests in camel-master-starter

[CAMEL-17890](https://issues.apache.org/jira/browse/CAMEL-17890)

Tests in two AWS examples fail with an error

[CAMEL-17878](https://issues.apache.org/jira/browse/CAMEL-17878)

add tests in camel-kamelet-starter

[CAMEL-17860](https://issues.apache.org/jira/browse/CAMEL-17860)

add tests in camel-aws2-sqs-starter

[CAMEL-17853](https://issues.apache.org/jira/browse/CAMEL-17853)

camel-zipfile: the case where the body is not a file is not tested

[CAMEL-17846](https://issues.apache.org/jira/browse/CAMEL-17846)

add tests in camel-aws2-ddb-starter

[CAMEL-17845](https://issues.apache.org/jira/browse/CAMEL-17845)

Create Kafka server once during IT

[CAMEL-17838](https://issues.apache.org/jira/browse/CAMEL-17838)

Create FHIR server once during tests

[CAMEL-17833](https://issues.apache.org/jira/browse/CAMEL-17833)

camel-aws - Secrets manager - Get binary secret is double encoded

[CAMEL-17771](https://issues.apache.org/jira/browse/CAMEL-17771)

camel-fhir-starter - Test failures with spring boot

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).