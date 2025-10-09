# Apache camel 3.19.0 Release

## New and Noteworthy

This release is the new Camel 3.19.0 release.

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
      <version>3.19.0</version>
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
      <version>3.19.0</version>
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
| [apache-camel-3.19.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.19.0/apache-camel-3.19.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.19.0/apache-camel-3.19.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.19.0/apache-camel-3.19.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.19.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.19.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (67)

[CAMEL-18544](https://issues.apache.org/jira/browse/CAMEL-18544)

camel-http - ToD optimized context-path with spaces problem

[CAMEL-18530](https://issues.apache.org/jira/browse/CAMEL-18530)

Camel box cannot authorize

[CAMEL-18514](https://issues.apache.org/jira/browse/CAMEL-18514)

camel-health - health check for not automatically started routes should always be up

[CAMEL-18510](https://issues.apache.org/jira/browse/CAMEL-18510)

camel-jbang - camel bind may not work with --local-kamelet-dir

[CAMEL-18490](https://issues.apache.org/jira/browse/CAMEL-18490)

camel-jbang - Reset statistics can cause JMX inflight counter to be negative

[CAMEL-18489](https://issues.apache.org/jira/browse/CAMEL-18489)

camel-file - Exclusive rename should handle windows locking the file

[CAMEL-18483](https://issues.apache.org/jira/browse/CAMEL-18483)

camel-microprofile-health: Routes and consumers health checks are not registered if routes are supervised

[CAMEL-18477](https://issues.apache.org/jira/browse/CAMEL-18477)

knative producer with ProducerTemplate is missing the fromRouteId

[CAMEL-18476](https://issues.apache.org/jira/browse/CAMEL-18476)

when artemis streaming enabled then Camel-jms component is not closing inputstream for Bytes message, blocking deletion of file after its archived in windows

[CAMEL-18473](https://issues.apache.org/jira/browse/CAMEL-18473)

Knative component : CloudEvents have wrong time format

[CAMEL-18444](https://issues.apache.org/jira/browse/CAMEL-18444)

camel-caffeine - Caffeine-cache query parameter action does not work

[CAMEL-18443](https://issues.apache.org/jira/browse/CAMEL-18443)

Problem using AdviceWith on routes with try-catch-finally

[CAMEL-18442](https://issues.apache.org/jira/browse/CAMEL-18442)

camel-github - Github commit consumer does not work

[CAMEL-18439](https://issues.apache.org/jira/browse/CAMEL-18439)

camel-github - Consumer that polls commits crashed when repository has more than 100 commits

[CAMEL-18435](https://issues.apache.org/jira/browse/CAMEL-18435)

camel-core - RAW values should be kept as-s

[CAMEL-18433](https://issues.apache.org/jira/browse/CAMEL-18433)

camel-yaml-dsl - Unsupported field: routeConfigurationId

[CAMEL-18432](https://issues.apache.org/jira/browse/CAMEL-18432)

DockerConfiguration malformerd UriPath for variable operation

[CAMEL-18427](https://issues.apache.org/jira/browse/CAMEL-18427)

Camel Debezium with Postgres on Spring Boot doesn't work

[CAMEL-18424](https://issues.apache.org/jira/browse/CAMEL-18424)

camel-jbang - Dependency downloaded issue with camel-aws-s3

[CAMEL-18421](https://issues.apache.org/jira/browse/CAMEL-18421)

camel-core - Adding route dynamic leak bootstraps

[CAMEL-18418](https://issues.apache.org/jira/browse/CAMEL-18418)

aws-s3-sink Kamelet returns 403

[CAMEL-18400](https://issues.apache.org/jira/browse/CAMEL-18400)

jbang does not use correct camel version

[CAMEL-18399](https://issues.apache.org/jira/browse/CAMEL-18399)

camel-sql - NullPointer exception for DBMaker PreparedStatement

[CAMEL-18396](https://issues.apache.org/jira/browse/CAMEL-18396)

NotifyBuilder.matches returns always true in conjunction with NotifyBuilderMatcher usage

[CAMEL-18394](https://issues.apache.org/jira/browse/CAMEL-18394)

CXF-Consumer does not start

[CAMEL-18393](https://issues.apache.org/jira/browse/CAMEL-18393)

Camel-bigquery: NPE if select \* is requested

[CAMEL-18391](https://issues.apache.org/jira/browse/CAMEL-18391)

camel-http - HttpSendDynamicAware not optimizing for url without slashes

[CAMEL-18387](https://issues.apache.org/jira/browse/CAMEL-18387)

camel-tarfile: TarAggregationStrategy throws error when first message is empty

[CAMEL-18379](https://issues.apache.org/jira/browse/CAMEL-18379)

camel-mail: attachments with empty fileName

[CAMEL-18377](https://issues.apache.org/jira/browse/CAMEL-18377)

camel-jpa producer does not reuse existing EntityManager in transaction and create its own one

[CAMEL-18375](https://issues.apache.org/jira/browse/CAMEL-18375)

Property description for FromDefinition is missing in camelYamlDsl.json

[CAMEL-18371](https://issues.apache.org/jira/browse/CAMEL-18371)

camel-resume-api: file component is not loading the cache

[CAMEL-18370](https://issues.apache.org/jira/browse/CAMEL-18370)

Bidning properties to route template local beans do not honor RAW()

[CAMEL-18362](https://issues.apache.org/jira/browse/CAMEL-18362)

camel-resume-api: kafka resume strategy fails to fetch the first batch

[CAMEL-18360](https://issues.apache.org/jira/browse/CAMEL-18360)

camel-jbang - Export --fresh with property placeholder using dash may fail

[CAMEL-18357](https://issues.apache.org/jira/browse/CAMEL-18357)

camel-core - Splitter issue with tokenizer with hashNext/next

[CAMEL-18355](https://issues.apache.org/jira/browse/CAMEL-18355)

HTTP component overwrites basic authentication credentials with proxy authentication

[CAMEL-18351](https://issues.apache.org/jira/browse/CAMEL-18351)

ExchangePropertyKey.SPLIT\_COMPLETE not set to true after zip splitting completed

[CAMEL-18347](https://issues.apache.org/jira/browse/CAMEL-18347)

camel-test-infra: instances are not properly singleton

[CAMEL-18338](https://issues.apache.org/jira/browse/CAMEL-18338)

IMAP MailConsumer NullPointerException due CAMEL-16180

[CAMEL-18336](https://issues.apache.org/jira/browse/CAMEL-18336)

camel-jbang: YAML DSL cannot find classes for local beans

[CAMEL-18331](https://issues.apache.org/jira/browse/CAMEL-18331)

camel-spring-xml - <endpoint> bean added via beans.xml are parsed twice

[CAMEL-18330](https://issues.apache.org/jira/browse/CAMEL-18330)

RouteTemplate: templateParameter not recognized

[CAMEL-18329](https://issues.apache.org/jira/browse/CAMEL-18329)

RouteTemplate: templateParameter doesn't get resolved

[CAMEL-18328](https://issues.apache.org/jira/browse/CAMEL-18328)

RouteConfiguration with RouteTemplate doesn't work

[CAMEL-18324](https://issues.apache.org/jira/browse/CAMEL-18324)

camel-core - Exception during preparing exchange task can block thread

[CAMEL-18322](https://issues.apache.org/jira/browse/CAMEL-18322)

Camel-Jbang export copy properties erroneously

[CAMEL-18321](https://issues.apache.org/jira/browse/CAMEL-18321)

camel-mybatis - Should support using Map message body as-is for insert/update

[CAMEL-18319](https://issues.apache.org/jira/browse/CAMEL-18319)

camel-core - Supervising route controller should not eager warmup routes

[CAMEL-18310](https://issues.apache.org/jira/browse/CAMEL-18310)

Global SSL Context Params Force SSL for All HTTP Connections

[CAMEL-18300](https://issues.apache.org/jira/browse/CAMEL-18300)

Google storage component does not set metadata appropriately

[CAMEL-18289](https://issues.apache.org/jira/browse/CAMEL-18289)

camel-xslt-saxon: XsltAggregationStrategyTest fails with removing the log definition

[CAMEL-18288](https://issues.apache.org/jira/browse/CAMEL-18288)

YAML DSL DoTry does not work

[CAMEL-18286](https://issues.apache.org/jira/browse/CAMEL-18286)

\[Camel Spring Boot\] camel-lra-starter needs camel-servlet-starter to work

[CAMEL-18279](https://issues.apache.org/jira/browse/CAMEL-18279)

When run 3.18.0 with Spring Boot, received java.io.FileNotFoundException: class path resource \[.class\] cannot be opened because it does not exist

[CAMEL-18278](https://issues.apache.org/jira/browse/CAMEL-18278)

AdviceWith fails with Spring XML and several route cross cutting concerns

[CAMEL-18275](https://issues.apache.org/jira/browse/CAMEL-18275)

onCompletion tasks don't get executed in a pipeline with several SEDA queues

[CAMEL-18274](https://issues.apache.org/jira/browse/CAMEL-18274)

OSGi - camel-file: ClassNotFoundException because of Private-Package

[CAMEL-18271](https://issues.apache.org/jira/browse/CAMEL-18271)

\[Camel Spring Boot Examples\] Infinispan example cannot be built

[CAMEL-18270](https://issues.apache.org/jira/browse/CAMEL-18270)

IMAP skipFailedMessage=true, but route blocked if mail is moved while download

[CAMEL-18266](https://issues.apache.org/jira/browse/CAMEL-18266)

Can not use bean uri in xslt component

[CAMEL-18262](https://issues.apache.org/jira/browse/CAMEL-18262)

Templated route exception handling not working

[CAMEL-18255](https://issues.apache.org/jira/browse/CAMEL-18255)

Memory Leak with MDCUnitOfWork

[CAMEL-18182](https://issues.apache.org/jira/browse/CAMEL-18182)

Camel servlet file upload with multipart/form-data not success

[CAMEL-18049](https://issues.apache.org/jira/browse/CAMEL-18049)

Camel Webhook - error to set Webhook URL

[CAMEL-17859](https://issues.apache.org/jira/browse/CAMEL-17859)

camel-smpp: Consumer sometimes tries to reconnect only once

[CAMEL-16287](https://issues.apache.org/jira/browse/CAMEL-16287)

camel-aws2-sqs should use pagination for deciding which aws sqs queues it should create

### Dependency upgrade (23)

[CAMEL-18560](https://issues.apache.org/jira/browse/CAMEL-18560)

Upgrade jetcd to 0.7.3

[CAMEL-18543](https://issues.apache.org/jira/browse/CAMEL-18543)

camel-zendesk - Upgrade to 0.18.x

[CAMEL-18542](https://issues.apache.org/jira/browse/CAMEL-18542)

camel-amqp - Upgrade qpid to 1.x

[CAMEL-18535](https://issues.apache.org/jira/browse/CAMEL-18535)

camel-hbase: Upgrade to 2.5.0

[CAMEL-18531](https://issues.apache.org/jira/browse/CAMEL-18531)

camel-karaf - Have karaf expose java 11 java packages

[CAMEL-18529](https://issues.apache.org/jira/browse/CAMEL-18529)

camel-jms - Upgrade to Artemis 2.25.x

[CAMEL-18520](https://issues.apache.org/jira/browse/CAMEL-18520)

Google-secrets-manager: dependency conflicts brought by the component

[CAMEL-18505](https://issues.apache.org/jira/browse/CAMEL-18505)

Camel-coap: Version conflict (californium-legal and element-connector)

[CAMEL-18499](https://issues.apache.org/jira/browse/CAMEL-18499)

camel-kubernetes - Upgrade to 6.x

[CAMEL-18464](https://issues.apache.org/jira/browse/CAMEL-18464)

camel-jbang - upgrade to kamelets 0.9.0

[CAMEL-18407](https://issues.apache.org/jira/browse/CAMEL-18407)

Align to spring-boot 2.7.3

[CAMEL-18365](https://issues.apache.org/jira/browse/CAMEL-18365)

camel-jsonpath - Upgrade to 2.7

[CAMEL-18361](https://issues.apache.org/jira/browse/CAMEL-18361)

camel-grpc: Upgrade gRPC to 1.48.1

[CAMEL-18353](https://issues.apache.org/jira/browse/CAMEL-18353)

camel-test - Upgrade to JUnit 5.9.x

[CAMEL-18344](https://issues.apache.org/jira/browse/CAMEL-18344)

Supporting camel "camel-google-pubsub" and "camel-grpc" OSGi deployment

[CAMEL-18332](https://issues.apache.org/jira/browse/CAMEL-18332)

\[camel-hyperledger-aries\] Upgrade to nessus-aries-0.2.0

[CAMEL-18294](https://issues.apache.org/jira/browse/CAMEL-18294)

upgrade to spring boot 2.7.2

[CAMEL-18246](https://issues.apache.org/jira/browse/CAMEL-18246)

CVE-2022-26612: Upgrade hadoop-common >= 3.3.3

[CAMEL-18203](https://issues.apache.org/jira/browse/CAMEL-18203)

camel-kotlin - Upgrade to 1.7.0

[CAMEL-18179](https://issues.apache.org/jira/browse/CAMEL-18179)

Supporting camel-jira OSGi deployment

[CAMEL-18121](https://issues.apache.org/jira/browse/CAMEL-18121)

camel-kafka - Upgrade to Kafka clients 3.2.x

[CAMEL-18031](https://issues.apache.org/jira/browse/CAMEL-18031)

camel-karaf - Upgrade to 4.4.x

[CAMEL-17171](https://issues.apache.org/jira/browse/CAMEL-17171)

camel-resteasy - Upgrade to 4.7.x

### Improvement (78)

[CAMEL-18557](https://issues.apache.org/jira/browse/CAMEL-18557)

camel-core - Total counter on ContextMBean is too high

[CAMEL-18556](https://issues.apache.org/jira/browse/CAMEL-18556)

camel-jbang - DevConsole should be started when used for Camel CLI

[CAMEL-18533](https://issues.apache.org/jira/browse/CAMEL-18533)

camel-netty - TimeoutCorrelationManagerSupport should stop created thread-pools

[CAMEL-18528](https://issues.apache.org/jira/browse/CAMEL-18528)

ensure CXF SpringBus honor camel graceful shutdown

[CAMEL-18521](https://issues.apache.org/jira/browse/CAMEL-18521)

camel-jbang - Sort Z..A

[CAMEL-18513](https://issues.apache.org/jira/browse/CAMEL-18513)

camel-jbang - Bind goal to support steps

[CAMEL-18507](https://issues.apache.org/jira/browse/CAMEL-18507)

camel-resilience4j - Add option to throw exception if CB rejected due to half-open/open state

[CAMEL-18500](https://issues.apache.org/jira/browse/CAMEL-18500)

camel-kamelet - Kamelet component should avoid reflection

[CAMEL-18493](https://issues.apache.org/jira/browse/CAMEL-18493)

camel-netty-http: Add maxInitialLineLength, maxChunkSize configuration parameters

[CAMEL-18492](https://issues.apache.org/jira/browse/CAMEL-18492)

Enterprise Feature of Saxon is Disabled in Camel 3.x versions.

[CAMEL-18491](https://issues.apache.org/jira/browse/CAMEL-18491)

camel-main - Configuring vault should avoid reflection

[CAMEL-18485](https://issues.apache.org/jira/browse/CAMEL-18485)

Error message when loading a routetemplate as resource

[CAMEL-18479](https://issues.apache.org/jira/browse/CAMEL-18479)

camel-aws - Capture aws secrets in use making refresh no need for declaring the secrets

[CAMEL-18472](https://issues.apache.org/jira/browse/CAMEL-18472)

deadlock when concurrently adding and removing routes

[CAMEL-18466](https://issues.apache.org/jira/browse/CAMEL-18466)

Camel-AWS2-SQS: Move from ComponentVerifierExtension to HealtCheck

[CAMEL-18461](https://issues.apache.org/jira/browse/CAMEL-18461)

camel-core - Add api\_key as a known secret parameter

[CAMEL-18458](https://issues.apache.org/jira/browse/CAMEL-18458)

camel-core - Remove eager loading classes

[CAMEL-18457](https://issues.apache.org/jira/browse/CAMEL-18457)

camel-resteasy - Deprecate

[CAMEL-18453](https://issues.apache.org/jira/browse/CAMEL-18453)

camel-core - Deprecate ServiceCall EIP

[CAMEL-18450](https://issues.apache.org/jira/browse/CAMEL-18450)

camel-jpa: improve to use transaction strategy in JpaMessageIdRepository

[CAMEL-18448](https://issues.apache.org/jira/browse/CAMEL-18448)

camel-jbang - Capture number of reloads

[CAMEL-18445](https://issues.apache.org/jira/browse/CAMEL-18445)

camel-caffeine - DynamicAware to optimize for action/key/value using expressions

[CAMEL-18440](https://issues.apache.org/jira/browse/CAMEL-18440)

camel-core - Stopping routes via management APIs should not make health-check fail

[CAMEL-18438](https://issues.apache.org/jira/browse/CAMEL-18438)

camel-main - Add option to configure context description

[CAMEL-18429](https://issues.apache.org/jira/browse/CAMEL-18429)

camel-jbang - Shutdown timeout 10 sec by default

[CAMEL-18423](https://issues.apache.org/jira/browse/CAMEL-18423)

camel-microprofile-config: Handle NoSuchElementException in CamelMicroProfilePropertiesSource. loadProperties(Predicate<String> filter)

[CAMEL-18420](https://issues.apache.org/jira/browse/CAMEL-18420)

Adapt CamelParallelExecutionStrategy for Junit 5.9.0

[CAMEL-18419](https://issues.apache.org/jira/browse/CAMEL-18419)

camel-management - Add last exchange received timestamp

[CAMEL-18417](https://issues.apache.org/jira/browse/CAMEL-18417)

StopWatch may provide incorrect measurements

[CAMEL-18415](https://issues.apache.org/jira/browse/CAMEL-18415)

camel-main - Add option to configure type converter statistics enabled

[CAMEL-18413](https://issues.apache.org/jira/browse/CAMEL-18413)

Improve tests classes of log component using log4j appenders

[CAMEL-18408](https://issues.apache.org/jira/browse/CAMEL-18408)

camel-console - Add dev console that lists the registered type converter pairs

[CAMEL-18406](https://issues.apache.org/jira/browse/CAMEL-18406)

camel-jbang - CLI to control routes such as suspend/resume/stats

[CAMEL-18390](https://issues.apache.org/jira/browse/CAMEL-18390)

\[camel-hyperledger-aries\] Component should not maintain websocket connection(s)

[CAMEL-18388](https://issues.apache.org/jira/browse/CAMEL-18388)

camel-jbang - add directory option to init to save to this folder

[CAMEL-18386](https://issues.apache.org/jira/browse/CAMEL-18386)

camel-kafka: Support using TypeConverter to parse kafka.OVERRIDE\_TOPIC

[CAMEL-18382](https://issues.apache.org/jira/browse/CAMEL-18382)

Google-bigquery allow different value types from headers

[CAMEL-18380](https://issues.apache.org/jira/browse/CAMEL-18380)

camel-kafka: Support using TypeConverter as a fallback in the header serializer

[CAMEL-18374](https://issues.apache.org/jira/browse/CAMEL-18374)

camel-core - Route template should be able to specify stream-caching option

[CAMEL-18368](https://issues.apache.org/jira/browse/CAMEL-18368)

Kamelet jslt-action not handling byte\[\] input

[CAMEL-18366](https://issues.apache.org/jira/browse/CAMEL-18366)

allow for per-route configuration of streamCaching in YAML

[CAMEL-18358](https://issues.apache.org/jira/browse/CAMEL-18358)

Support for mail attachments for camel freemarker

[CAMEL-18348](https://issues.apache.org/jira/browse/CAMEL-18348)

camel-yaml-dsl - Template should be named as routeTemplate

[CAMEL-18345](https://issues.apache.org/jira/browse/CAMEL-18345)

EMPTY\_ELEMENT\_AS\_NULL disabled by default in jackson-dataformat-xml

[CAMEL-18343](https://issues.apache.org/jira/browse/CAMEL-18343)

camel-yaml-dsl - Add route-policy

[CAMEL-18339](https://issues.apache.org/jira/browse/CAMEL-18339)

camel-joor - Java DSL - Allow compiled classes to be loadable from anywhere in Camel

[CAMEL-18337](https://issues.apache.org/jira/browse/CAMEL-18337)

\[camel-hyperledger-aries\] Add support for /issue-credential/send-proposal

[CAMEL-18333](https://issues.apache.org/jira/browse/CAMEL-18333)

camel-kafka: better error messages in the health check

[CAMEL-18325](https://issues.apache.org/jira/browse/CAMEL-18325)

camel-hyperledger-aries - Add support for /credentials endpoint

[CAMEL-18323](https://issues.apache.org/jira/browse/CAMEL-18323)

camel-jpa: introduce a transaction strategy

[CAMEL-18320](https://issues.apache.org/jira/browse/CAMEL-18320)

camel-core - Move xtokenize language into camel-stax

[CAMEL-18318](https://issues.apache.org/jira/browse/CAMEL-18318)

camel-quartz - Context fails to start when one of the cron configuration has expired

[CAMEL-18317](https://issues.apache.org/jira/browse/CAMEL-18317)

camel-salesforce - Endpoint syntax should have mandatory operationName

[CAMEL-18311](https://issues.apache.org/jira/browse/CAMEL-18311)

camel-jbang - Running files should detect duplicated names

[CAMEL-18307](https://issues.apache.org/jira/browse/CAMEL-18307)

camel-stub - Should accept lenient configuration

[CAMEL-18306](https://issues.apache.org/jira/browse/CAMEL-18306)

camel-jbang - Allow to specify open-api in application.properties

[CAMEL-18299](https://issues.apache.org/jira/browse/CAMEL-18299)

camel-core - ResumeAdapter should use FactoryFinder to lookup implementations

[CAMEL-18297](https://issues.apache.org/jira/browse/CAMEL-18297)

camel-core - Languages with namespace support should be exposed in model

[CAMEL-18293](https://issues.apache.org/jira/browse/CAMEL-18293)

camel-cxf - Move CXFTestSupport to test-jar

[CAMEL-18292](https://issues.apache.org/jira/browse/CAMEL-18292)

Datasonnet expression should not fail if body is empty

[CAMEL-18285](https://issues.apache.org/jira/browse/CAMEL-18285)

camel-file - Lazy-loading for file length and last modified attributes for faster performance

[CAMEL-18283](https://issues.apache.org/jira/browse/CAMEL-18283)

Upgrade Camel JBang to 3.18.0 by default

[CAMEL-18264](https://issues.apache.org/jira/browse/CAMEL-18264)

Camel SFTP: Cannot configure JSch client to use ssh-dss key

[CAMEL-18260](https://issues.apache.org/jira/browse/CAMEL-18260)

debugger - Reflect exchange changes on BacklogTracerEventMessage

[CAMEL-18258](https://issues.apache.org/jira/browse/CAMEL-18258)

Enhancements to camel-splunk and camel-splunk-hec

[CAMEL-18208](https://issues.apache.org/jira/browse/CAMEL-18208)

vault: allow to retrieve a specific secret version/revision

[CAMEL-18155](https://issues.apache.org/jira/browse/CAMEL-18155)

camel-jbang - Display sub commands by default

[CAMEL-18143](https://issues.apache.org/jira/browse/CAMEL-18143)

Autowire quartz scheduler in quartz component

[CAMEL-18057](https://issues.apache.org/jira/browse/CAMEL-18057)

rest-dsl - Combine rest and linked route together as single route

[CAMEL-17674](https://issues.apache.org/jira/browse/CAMEL-17674)

camel-core - Deprecate Service Call EIP

[CAMEL-17586](https://issues.apache.org/jira/browse/CAMEL-17586)

Camel mail consumer: Unable to handle multiple attachments with the same filename

[CAMEL-17287](https://issues.apache.org/jira/browse/CAMEL-17287)

YAML DSL Definitions required missing

[CAMEL-17197](https://issues.apache.org/jira/browse/CAMEL-17197)

camel-elasticsearch - Avoid using deprecated APIs

[CAMEL-16642](https://issues.apache.org/jira/browse/CAMEL-16642)

camel-salesforce: Detect SObject type from query result

[CAMEL-16578](https://issues.apache.org/jira/browse/CAMEL-16578)

Implement or remove MLLP component LogPhi functionality

[CAMEL-13436](https://issues.apache.org/jira/browse/CAMEL-13436)

Set TLS default to TLSv1.3 once we move to JDK11

[CAMEL-11252](https://issues.apache.org/jira/browse/CAMEL-11252)

camel-core : allow to retrieve components/endpoints/etc list with a predicate

[CAMEL-5695](https://issues.apache.org/jira/browse/CAMEL-5695)

Route with autoStartup=false should not pre start services

### New Feature (36)

[CAMEL-18534](https://issues.apache.org/jira/browse/CAMEL-18534)

camel-catalog - Include json schema for sensitive keys

[CAMEL-18527](https://issues.apache.org/jira/browse/CAMEL-18527)

Camel Kafka Component: batch producer with individual headers

[CAMEL-18526](https://issues.apache.org/jira/browse/CAMEL-18526)

camel-jbang - Did you mean

[CAMEL-18515](https://issues.apache.org/jira/browse/CAMEL-18515)

camel-jbang - Commands to list kamelets and init from an existing kamelet

[CAMEL-18503](https://issues.apache.org/jira/browse/CAMEL-18503)

Configure max ack extension period parameter in PubSub subscriber

[CAMEL-18494](https://issues.apache.org/jira/browse/CAMEL-18494)

camel-mllp - Allow the ability to set MIN\_BUFFER\_SIZE for SocketBuffer

[CAMEL-18488](https://issues.apache.org/jira/browse/CAMEL-18488)

camel-management - Statistic for current throughput

[CAMEL-18481](https://issues.apache.org/jira/browse/CAMEL-18481)

Allow Mail Consumer to handle duplicate/empty attachment filenames

[CAMEL-18480](https://issues.apache.org/jira/browse/CAMEL-18480)

camel-aws - Dev console for AWS secrets manager

[CAMEL-18475](https://issues.apache.org/jira/browse/CAMEL-18475)

camel-core - FactoryFinder for period background tasks

[CAMEL-18459](https://issues.apache.org/jira/browse/CAMEL-18459)

Set application properties in messages sent to Azure Service Bus

[CAMEL-18451](https://issues.apache.org/jira/browse/CAMEL-18451)

camel-azure-eventhubs: Add support for Azure-AD authentication

[CAMEL-18449](https://issues.apache.org/jira/browse/CAMEL-18449)

camel-spring-boot - platform-http implementation

[CAMEL-18426](https://issues.apache.org/jira/browse/CAMEL-18426)

camel-jbang - Export - Add support for local-kamelets-dir

[CAMEL-18425](https://issues.apache.org/jira/browse/CAMEL-18425)

camel-cli - Make regular Camel applications work with Camel CLI

[CAMEL-18412](https://issues.apache.org/jira/browse/CAMEL-18412)

camel-jbang - Add support for hawtio

[CAMEL-18389](https://issues.apache.org/jira/browse/CAMEL-18389)

camel-jbang - CLI to start|stop|list running Camel instances

[CAMEL-18376](https://issues.apache.org/jira/browse/CAMEL-18376)

camel-pulsar - Use RedeliveryBackoff for ack timeout and negative ack redelivery

[CAMEL-18369](https://issues.apache.org/jira/browse/CAMEL-18369)

camel-stream - Add http to read stream from remote http server

[CAMEL-18352](https://issues.apache.org/jira/browse/CAMEL-18352)

Camel-AWS Cloudtrail: Create an SB starter

[CAMEL-18315](https://issues.apache.org/jira/browse/CAMEL-18315)

\[camel-hyperledger-aries\] Add support for single tenancy agent

[CAMEL-18291](https://issues.apache.org/jira/browse/CAMEL-18291)

SSLContextParameters parsePropertyValue support for certAlias property

[CAMEL-18287](https://issues.apache.org/jira/browse/CAMEL-18287)

Camel-AWS Eventbridge: Support operation putEvents to send custom event to Eventbridge

[CAMEL-18267](https://issues.apache.org/jira/browse/CAMEL-18267)

Vault Support: Trigger a reload of properties from a particular Vault source based on events

[CAMEL-18256](https://issues.apache.org/jira/browse/CAMEL-18256)

Camel-Hashicorp-vault: Support Versioning of secret while reading

[CAMEL-18164](https://issues.apache.org/jira/browse/CAMEL-18164)

camel-spring-boot - Add platform-http-starter

[CAMEL-18163](https://issues.apache.org/jira/browse/CAMEL-18163)

camel-platform-http-verx - Add health-check endpoint

[CAMEL-18156](https://issues.apache.org/jira/browse/CAMEL-18156)

Add support for hyperledger-aries

[CAMEL-18093](https://issues.apache.org/jira/browse/CAMEL-18093)

camel-http - Add option to turn on follow redirects

[CAMEL-17841](https://issues.apache.org/jira/browse/CAMEL-17841)

camel-azure - Add checkpoint events by batch

[CAMEL-17823](https://issues.apache.org/jira/browse/CAMEL-17823)

UUID generator in the Simple language

[CAMEL-17780](https://issues.apache.org/jira/browse/CAMEL-17780)

camel-elasticsearch - Propose a new component using a client compatible with an Apache License

[CAMEL-16994](https://issues.apache.org/jira/browse/CAMEL-16994)

camel-python - Add support for using Python as expression language

[CAMEL-15566](https://issues.apache.org/jira/browse/CAMEL-15566)

Create a AWS Cloudtrail component

[CAMEL-11030](https://issues.apache.org/jira/browse/CAMEL-11030)

Add a vault service to manage secrets

[CAMEL-6643](https://issues.apache.org/jira/browse/CAMEL-6643)

camel-mapstruct - A component for type converters a like we have with camel-dozer

### Sub-task (12)

[CAMEL-18532](https://issues.apache.org/jira/browse/CAMEL-18532)

GCP Secret Manager Dev Console: Add to Vault command for camel-jbang

[CAMEL-18519](https://issues.apache.org/jira/browse/CAMEL-18519)

camel-azure-key-vault - Add dev console for secrets

[CAMEL-18518](https://issues.apache.org/jira/browse/CAMEL-18518)

Support Secrets Reload from Vault/Cloud Service in camel-spring-boot - Azure Key Vault

[CAMEL-18511](https://issues.apache.org/jira/browse/CAMEL-18511)

Camel-Azure-Key-Vault: Create a task looking for secrets update in Eventhubs

[CAMEL-18504](https://issues.apache.org/jira/browse/CAMEL-18504)

camel-google-secret-manager - Add dev console for secrets

[CAMEL-18502](https://issues.apache.org/jira/browse/CAMEL-18502)

Support Secrets Reload from Vault/Cloud Service in camel-spring-boot - Google Secret Manager

[CAMEL-18501](https://issues.apache.org/jira/browse/CAMEL-18501)

Camel-Google-Secret-Manager: Create a task looking for secrets update in PubSub

[CAMEL-18487](https://issues.apache.org/jira/browse/CAMEL-18487)

Camel-AWS-Secrets-Manager: Cloudtrail task should support environment variables as configuration too

[CAMEL-18478](https://issues.apache.org/jira/browse/CAMEL-18478)

Support Secrets Reload from Vault/Cloud Service in camel-spring-boot - AWS Secrets Manager

[CAMEL-18469](https://issues.apache.org/jira/browse/CAMEL-18469)

camel-main - Configure vault/cloud secrets reloader and auto detect via classpath

[CAMEL-18468](https://issues.apache.org/jira/browse/CAMEL-18468)

Camel-AWS-Secrets-Manager: Create a task looking for secrets update in CloudTrail

[CAMEL-17688](https://issues.apache.org/jira/browse/CAMEL-17688)

Support ability to load properties from Vault/Secrets cloud services - Hashicorp Vault

### Task (38)

[CAMEL-18553](https://issues.apache.org/jira/browse/CAMEL-18553)

Fix main-tiny example to remove unsupported property

[CAMEL-18506](https://issues.apache.org/jira/browse/CAMEL-18506)

Migrate components away from Async HTTP Client

[CAMEL-18495](https://issues.apache.org/jira/browse/CAMEL-18495)

Apache Chemistry is deprecated

[CAMEL-18467](https://issues.apache.org/jira/browse/CAMEL-18467)

\[DOCS\] Velocity component - missing java code sample

[CAMEL-18465](https://issues.apache.org/jira/browse/CAMEL-18465)

Remove outdated "jigsaw" profiles

[CAMEL-18460](https://issues.apache.org/jira/browse/CAMEL-18460)

Duplicate dependency in camel-spring-boot-bom

[CAMEL-18456](https://issues.apache.org/jira/browse/CAMEL-18456)

camel-test-infra: investigate consolidating usages of web server and servlets

[CAMEL-18455](https://issues.apache.org/jira/browse/CAMEL-18455)

Dozer project is not active anymore

[CAMEL-18454](https://issues.apache.org/jira/browse/CAMEL-18454)

Support Secrets Reload from Vault/Cloud Service through specific Tasks in components

[CAMEL-18452](https://issues.apache.org/jira/browse/CAMEL-18452)

Integrate azure-sdk-bom in a non-conflicting manner

[CAMEL-18428](https://issues.apache.org/jira/browse/CAMEL-18428)

Fhir component documentation describes the option password as the Username

[CAMEL-18422](https://issues.apache.org/jira/browse/CAMEL-18422)

Camel-AWS Component: Explicitly add AWS SDK Utils dependency

[CAMEL-18404](https://issues.apache.org/jira/browse/CAMEL-18404)

No documentation in camel-stax for XML DSL example

[CAMEL-18403](https://issues.apache.org/jira/browse/CAMEL-18403)

Improve controlbus docs

[CAMEL-18354](https://issues.apache.org/jira/browse/CAMEL-18354)

Camel AWS Cloudtrail: Create Karaf feature

[CAMEL-18346](https://issues.apache.org/jira/browse/CAMEL-18346)

Remove use of Xalan

[CAMEL-18308](https://issues.apache.org/jira/browse/CAMEL-18308)

ci: remove duplicated job group

[CAMEL-18296](https://issues.apache.org/jira/browse/CAMEL-18296)

camel-example tag is using snapshot camel version

[CAMEL-18290](https://issues.apache.org/jira/browse/CAMEL-18290)

Deploy CSB examples on openshift cluster using odo.

[CAMEL-18282](https://issues.apache.org/jira/browse/CAMEL-18282)

Fix checkstyle errors

[CAMEL-18273](https://issues.apache.org/jira/browse/CAMEL-18273)

\[Camel Spring Boot Examples\] Add Saga EIP example

[CAMEL-18269](https://issues.apache.org/jira/browse/CAMEL-18269)

\[Camel Spring Boot Examples\] Update version

[CAMEL-18268](https://issues.apache.org/jira/browse/CAMEL-18268)

Camel-dependencies is misaligned to current version in camel-spring-boot

[CAMEL-18263](https://issues.apache.org/jira/browse/CAMEL-18263)

Fix tests of BacklogDebuggerTest failing on Java 17

[CAMEL-18244](https://issues.apache.org/jira/browse/CAMEL-18244)

\[DOCS\] AWS SQS component - code samples needs to be updated

[CAMEL-18243](https://issues.apache.org/jira/browse/CAMEL-18243)

\[DOCS\] Kafka component - multiple options need updates

[CAMEL-18241](https://issues.apache.org/jira/browse/CAMEL-18241)

\[DOCS\] HTTP component - missing sample

[CAMEL-18240](https://issues.apache.org/jira/browse/CAMEL-18240)

\[DOCS\] FHIR component - documentation issues

[CAMEL-18239](https://issues.apache.org/jira/browse/CAMEL-18239)

\[DOCS\] Bean components - missing examples

[CAMEL-18152](https://issues.apache.org/jira/browse/CAMEL-18152)

camel-resume-api: investigate generating the adapter configuration during build

[CAMEL-17947](https://issues.apache.org/jira/browse/CAMEL-17947)

camel-kafka: fix concurrent access in camel-health

[CAMEL-17842](https://issues.apache.org/jira/browse/CAMEL-17842)

XML DSL documentation

[CAMEL-17507](https://issues.apache.org/jira/browse/CAMEL-17507)

No error handler invoked on exception with multipleConsumer=true and POJO @Consume Annotation

[CAMEL-16929](https://issues.apache.org/jira/browse/CAMEL-16929)

Document DSLs

[CAMEL-16810](https://issues.apache.org/jira/browse/CAMEL-16810)

Evaluating removal of Zipkin Component

[CAMEL-16742](https://issues.apache.org/jira/browse/CAMEL-16742)

camel-iota - Make TLS work to communicate with the online service

[CAMEL-16488](https://issues.apache.org/jira/browse/CAMEL-16488)

Investigate test speed up for camel-ftp

[CAMEL-15475](https://issues.apache.org/jira/browse/CAMEL-15475)

camel-jetty: incompatible HttpReturnDataNotInputStreamConvertableTest behavior

### Test (5)

[CAMEL-18509](https://issues.apache.org/jira/browse/CAMEL-18509)

use servlet transport for camel-cxf spring boot test

[CAMEL-18484](https://issues.apache.org/jira/browse/CAMEL-18484)

Camel-xchange: Enable mock testing without neaed of real account

[CAMEL-18349](https://issues.apache.org/jira/browse/CAMEL-18349)

Core - XPathRouteConcurrentBigTest - newly added limit of "operators an XPath expression can contain." fails the test

[CAMEL-18295](https://issues.apache.org/jira/browse/CAMEL-18295)

Restore couchbase IT tests

[CAMEL-18281](https://issues.apache.org/jira/browse/CAMEL-18281)

Fix aws integration tests

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).