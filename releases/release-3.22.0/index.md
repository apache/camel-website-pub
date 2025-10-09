# Apache camel 3.22.0 Release

## New and Noteworthy

This release is the new Camel 3.22.0 LTS release.

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
      <version>3.22.0</version>
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
      <version>3.22.0</version>
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
| [apache-camel-3.22.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-src.zip.sha512) |
| [apache-camel-3.22.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.xml.sha512) |
| [apache-camel-3.22.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.22.0/apache-camel-3.22.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-3.22.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.22.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (51)

[CAMEL-20214](https://issues.apache.org/jira/browse/CAMEL-20214)

camel-core - Timeout tasks of parallel splitter block further message processing

[CAMEL-20152](https://issues.apache.org/jira/browse/CAMEL-20152)

camel-jetty - OutOfMemoryError with big file upload via multipart

[CAMEL-20139](https://issues.apache.org/jira/browse/CAMEL-20139)

aggregate EIP: wrong correlation key set for the first aggregate exchange

[CAMEL-20092](https://issues.apache.org/jira/browse/CAMEL-20092)

camel-core - ScheduledPollConsumer should reset error count when greedy

[CAMEL-20079](https://issues.apache.org/jira/browse/CAMEL-20079)

EndpointDslMojo generates wrong header names

[CAMEL-20054](https://issues.apache.org/jira/browse/CAMEL-20054)

camel-kubernetes - Configuration of Kubernetes secrets with Camel K not working as expected

[CAMEL-20053](https://issues.apache.org/jira/browse/CAMEL-20053)

camel-jira: watchUpdates consumer does not see issues created after route startup

[CAMEL-20044](https://issues.apache.org/jira/browse/CAMEL-20044)

camel-kafka - On rejoining consumer group Camel can set offset incorrectly causing messages to be replayed

[CAMEL-20035](https://issues.apache.org/jira/browse/CAMEL-20035)

Program terminates with OutOfMemoryError

[CAMEL-20028](https://issues.apache.org/jira/browse/CAMEL-20028)

camel-mail - Missing attachments if disposition not set

[CAMEL-20010](https://issues.apache.org/jira/browse/CAMEL-20010)

camel-sql - Can't change table name in JdbcMessageIdRepository by adding suffix/prefix

[CAMEL-19996](https://issues.apache.org/jira/browse/CAMEL-19996)

camel-lra NullPointerException when creating a saga with invalid lra-url

[CAMEL-19976](https://issues.apache.org/jira/browse/CAMEL-19976)

camel-karaf: org.xml.sax.ext.EntityResolver2 not found by org.apache.servicemix.bundles.xmlresolver

[CAMEL-19970](https://issues.apache.org/jira/browse/CAMEL-19970)

camel-jbang - IllegalArgumentException: Unable to determine file extension for resource when a file has no extension

[CAMEL-19968](https://issues.apache.org/jira/browse/CAMEL-19968)

camel-opentelemetry - The Tracing Strategy is failing when using pollEnrich with seda endpoint

[CAMEL-19967](https://issues.apache.org/jira/browse/CAMEL-19967)

camel-core - Default RouteConfigurationBuilder written in Java not enabled on XML routes

[CAMEL-19895](https://issues.apache.org/jira/browse/CAMEL-19895)

Camel JBang dependency copy --output-directory doesn't respect absolute path

[CAMEL-19894](https://issues.apache.org/jira/browse/CAMEL-19894)

camel-kafka: enabling "breakOnFirstError" causes to skip records on exception

[CAMEL-19870](https://issues.apache.org/jira/browse/CAMEL-19870)

Camel AS2: Should accept MDN field name Disposition as case insensitive

[CAMEL-19822](https://issues.apache.org/jira/browse/CAMEL-19822)

camel-azure-files - assert failure in the implementation of move=

[CAMEL-19814](https://issues.apache.org/jira/browse/CAMEL-19814)

camel-rest - Should filter out query parameters that are for the producer endpoint

[CAMEL-19794](https://issues.apache.org/jira/browse/CAMEL-19794)

camel-karaf - OsgiEventAdminNotifier not getting registered

[CAMEL-19780](https://issues.apache.org/jira/browse/CAMEL-19780)

Camel JBang does not support relative paths

[CAMEL-19777](https://issues.apache.org/jira/browse/CAMEL-19777)

camel-jms: toD endpoint with FQQN

[CAMEL-19766](https://issues.apache.org/jira/browse/CAMEL-19766)

Routes loaded with xml-io-dsl don't find associated routeConfiguration

[CAMEL-19758](https://issues.apache.org/jira/browse/CAMEL-19758)

netty-http in proxy mode generates IllegalReferenceCountException for every success request.

[CAMEL-19756](https://issues.apache.org/jira/browse/CAMEL-19756)

camel-zeebe - ThrowError operation does not set Processor

[CAMEL-19744](https://issues.apache.org/jira/browse/CAMEL-19744)

camel-core - Backlog tracer capturing data as json when its not json

[CAMEL-19734](https://issues.apache.org/jira/browse/CAMEL-19734)

SEDA endpoint with multiple consumers produces strange message history from error handler

[CAMEL-19731](https://issues.apache.org/jira/browse/CAMEL-19731)

Camel-AS2: exception on empty response

[CAMEL-19719](https://issues.apache.org/jira/browse/CAMEL-19719)

camel-rest - Infinite loop when maximumRedeliveries > 0

[CAMEL-19701](https://issues.apache.org/jira/browse/CAMEL-19701)

camel-main - Filter out Kubernetes ENV injected service host/port

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

[CAMEL-19663](https://issues.apache.org/jira/browse/CAMEL-19663)

camel-core - ToD EIP multi-value property lost problem

[CAMEL-19650](https://issues.apache.org/jira/browse/CAMEL-19650)

Camel Kafka doesn't honor 'workerPool' configuration

[CAMEL-19607](https://issues.apache.org/jira/browse/CAMEL-19607)

camel-core - Checking redelivery reference while error handler creation

[CAMEL-19603](https://issues.apache.org/jira/browse/CAMEL-19603)

Spring Boot and Quarkus runtimes: @PeriodicTask annotated task are not running even if scheduled

[CAMEL-19575](https://issues.apache.org/jira/browse/CAMEL-19575)

camel-rabbitmq - RabbitMQConsumer keeps on consuming even when route shutdown is triggered.

[CAMEL-19509](https://issues.apache.org/jira/browse/CAMEL-19509)

java.lang.NullPointerException: Cannot invoke "org.apache.camel.model.FromDefinition.getLabel()" because "this.input" is null

[CAMEL-19498](https://issues.apache.org/jira/browse/CAMEL-19498)

camel-core / camel-ftp - memory leak in MultiplePool when using pollEnrich EIP

[CAMEL-19491](https://issues.apache.org/jira/browse/CAMEL-19491)

Failing healthcheck on aws2-\* polling consumers causes readiness check to be stuck

[CAMEL-19487](https://issues.apache.org/jira/browse/CAMEL-19487)

camel-core / camel-bean - Dynamic router instances pass messages to wrong endpoints with @DynamicRouter annotation

[CAMEL-18760](https://issues.apache.org/jira/browse/CAMEL-18760)

camel-kafka - Issue using ThrottlingExceptionRoutePolicy with Kafka consumer

[CAMEL-18759](https://issues.apache.org/jira/browse/CAMEL-18759)

camel-kafka - When Kafka pausable consumer is resumed, it reads all the messages from the earliest offset

[CAMEL-18234](https://issues.apache.org/jira/browse/CAMEL-18234)

Exception building aws2-sqs route when certificate validation is disabled and a proxy is configured

### Dependency upgrade (14)

[CAMEL-20146](https://issues.apache.org/jira/browse/CAMEL-20146)

camel-spring-boot - Upgrade to 2.7.18

[CAMEL-20049](https://issues.apache.org/jira/browse/CAMEL-20049)

camel-activemq - Upgrade to latest releases

[CAMEL-19989](https://issues.apache.org/jira/browse/CAMEL-19989)

camel-spring-boot - Upgrade to 2.7.17

[CAMEL-19978](https://issues.apache.org/jira/browse/CAMEL-19978)

Upgrade Netty to 4.1.100.Final

[CAMEL-19920](https://issues.apache.org/jira/browse/CAMEL-19920)

camel-mina - Upgrade to newer versions

[CAMEL-19901](https://issues.apache.org/jira/browse/CAMEL-19901)

camel-spring-boot - Upgrade to 2.7.16

[CAMEL-19882](https://issues.apache.org/jira/browse/CAMEL-19882)

camel-karaf - Upgrade to 4.4.4

[CAMEL-19799](https://issues.apache.org/jira/browse/CAMEL-19799)

Camel-Spring-Boot: Upgrade to SB 2.7.15 on Camel Spring Boot 3.x

[CAMEL-19743](https://issues.apache.org/jira/browse/CAMEL-19743)

Camel OpenTelemetry Upgrade GRPC

[CAMEL-19695](https://issues.apache.org/jira/browse/CAMEL-19695)

camel-google-bigquery - Upgrade org.json to resolve CVE-2022-45688

[CAMEL-19594](https://issues.apache.org/jira/browse/CAMEL-19594)

camel-jbang - Upgrade to hawtio 2.17.5

[CAMEL-19581](https://issues.apache.org/jira/browse/CAMEL-19581)

camel-jbang - Upgrade to picocli 4.7.4

[CAMEL-19503](https://issues.apache.org/jira/browse/CAMEL-19503)

camel-jbang - Upgrade to maven-resolver 1.9.13

[CAMEL-19323](https://issues.apache.org/jira/browse/CAMEL-19323)

Camel Karaf 3.20.X Saxon HE 11.5 Dependency Upgrade

### Improvement (19)

[CAMEL-20209](https://issues.apache.org/jira/browse/CAMEL-20209)

camel-azure - Adopt atomic overwrite feature of Azure Files

[CAMEL-20205](https://issues.apache.org/jira/browse/CAMEL-20205)

Add SBOM to release and release-sbom script to LTS 4.0.x, 3.22.x and 3.21.x

[CAMEL-19997](https://issues.apache.org/jira/browse/CAMEL-19997)

camel-cifs: new component for the Common Internet File System

[CAMEL-19961](https://issues.apache.org/jira/browse/CAMEL-19961)

Missing Features in Camel Spring RabbitMQ in Camel 3.21.0

[CAMEL-19852](https://issues.apache.org/jira/browse/CAMEL-19852)

Camel-platform-http-vertx: Always use normalized path from context

[CAMEL-19776](https://issues.apache.org/jira/browse/CAMEL-19776)

Provide tracing strategy to trace each processor for OpenTelemetry

[CAMEL-19760](https://issues.apache.org/jira/browse/CAMEL-19760)

netty-http:prevent the usage of proxy protocol in producer endpoint

[CAMEL-19752](https://issues.apache.org/jira/browse/CAMEL-19752)

Usage of "doc" prefix in some elasticsearch operations are regression to camel-elasticsearch-rest

[CAMEL-19736](https://issues.apache.org/jira/browse/CAMEL-19736)

Environment variables with the name 'secret' aren't masked in logs

[CAMEL-19691](https://issues.apache.org/jira/browse/CAMEL-19691)

camel-kafka - Allow sslKeystorePassword to be blank

[CAMEL-19677](https://issues.apache.org/jira/browse/CAMEL-19677)

camel-mllp - support more MLLP charsets

[CAMEL-19662](https://issues.apache.org/jira/browse/CAMEL-19662)

camel-bindy - Add option to @CsvRecord for trimeLine true or false

[CAMEL-19660](https://issues.apache.org/jira/browse/CAMEL-19660)

camel-mapstruct: Improve support for Mappers defined as abstract classes

[CAMEL-19627](https://issues.apache.org/jira/browse/CAMEL-19627)

paho-mqtt5: Allow password to be optional if username is provided

[CAMEL-19615](https://issues.apache.org/jira/browse/CAMEL-19615)

camel-ftp: chmodDirectory option try for each junk to change the directory permission and fails

[CAMEL-19587](https://issues.apache.org/jira/browse/CAMEL-19587)

camel-jira: optional header field IssueAssignee doesn't work

[CAMEL-19502](https://issues.apache.org/jira/browse/CAMEL-19502)

netty4-http - allow SSL SNI to be set using SSLContextClientParameters

[CAMEL-19479](https://issues.apache.org/jira/browse/CAMEL-19479)

camel-core - Add threadId as function to simple language

[CAMEL-19024](https://issues.apache.org/jira/browse/CAMEL-19024)

Camel Karaf Features missing camel-cxf-spring-\*

### New Feature (4)

[CAMEL-20115](https://issues.apache.org/jira/browse/CAMEL-20115)

Support for Start Date and End Date in camel-quartz

[CAMEL-19907](https://issues.apache.org/jira/browse/CAMEL-19907)

Introduce the ability to use the old Micrometer meter names or follow the new Micrometer naming conventions

[CAMEL-19601](https://issues.apache.org/jira/browse/CAMEL-19601)

camel-core - Limit auto conversion when stream caching is enabled

[CAMEL-19279](https://issues.apache.org/jira/browse/CAMEL-19279)

Introduce a file component for Azure Files (mimic the FTP component)

### Task (12)

[CAMEL-20094](https://issues.apache.org/jira/browse/CAMEL-20094)

camel-catalog: camel-spring.xsd keeps being regenerated

[CAMEL-19984](https://issues.apache.org/jira/browse/CAMEL-19984)

Re-add Camel-Cassandraql Karaf feature

[CAMEL-19962](https://issues.apache.org/jira/browse/CAMEL-19962)

Camel-Azure-Datalake: Headers metadata are wrong

[CAMEL-19921](https://issues.apache.org/jira/browse/CAMEL-19921)

Update default values of kafka client configuration

[CAMEL-19871](https://issues.apache.org/jira/browse/CAMEL-19871)

camel-jooq - Set the proper scope to all test dependencies

[CAMEL-19840](https://issues.apache.org/jira/browse/CAMEL-19840)

camel-core-api - Add a warning when the key store file cannot be found

[CAMEL-19751](https://issues.apache.org/jira/browse/CAMEL-19751)

camel-xchange: tests keep hitting the binance API

[CAMEL-19565](https://issues.apache.org/jira/browse/CAMEL-19565)

Create Azure Files SB starter

[CAMEL-19510](https://issues.apache.org/jira/browse/CAMEL-19510)

camel-spring-boot-examples - Fix the reactive-streams

[CAMEL-19499](https://issues.apache.org/jira/browse/CAMEL-19499)

camel-yaml-dsl: Missing rest-configuration in YAML DSL schema

[CAMEL-19489](https://issues.apache.org/jira/browse/CAMEL-19489)

camel-minio - Minor issues in documentation

[CAMEL-19425](https://issues.apache.org/jira/browse/CAMEL-19425)

camel-core: DynamicRouterConcurrentPOJOTest is flaky

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).