# Apache camel 4.8.0 Release

## New and Noteworthy

This release is the new Camel 4.8.0 release.

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
      <version>4.8.0</version>
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
      <version>4.8.0</version>
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
| [apache-camel-4.8.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-src.zip.sha512) |
| [apache-camel-4.8.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.xml.sha512) |
| [apache-camel-4.8.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.0/apache-camel-4.8.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (64)

[CAMEL-21354](https://issues.apache.org/jira/browse/CAMEL-21354)

camel.main.shutdown-timeout is ignored in 4.4.3, default 45 is used

[CAMEL-21296](https://issues.apache.org/jira/browse/CAMEL-21296)

Camel AS2 Sender application couldn't validate MDN message

[CAMEL-21194](https://issues.apache.org/jira/browse/CAMEL-21194)

camel-jbang - Cannot run xxx.camel.yaml files

[CAMEL-21191](https://issues.apache.org/jira/browse/CAMEL-21191)

camel-catalog - Beans for aggregation repository are wrongly declared as aggregation strategy

[CAMEL-21185](https://issues.apache.org/jira/browse/CAMEL-21185)

DefaultShutdownStrategy cannot set timeout via JMX

[CAMEL-21182](https://issues.apache.org/jira/browse/CAMEL-21182)

camel-jbang - Run with json logging does not work

[CAMEL-21164](https://issues.apache.org/jira/browse/CAMEL-21164)

camel-rest - Code first should use actual values for property placeholders in dumped API spec

[CAMEL-21163](https://issues.apache.org/jira/browse/CAMEL-21163)

camel-jbang - Can not get service meta data from camel-jms and camel-sql with Quarkus runtime

[CAMEL-21162](https://issues.apache.org/jira/browse/CAMEL-21162)

Cannot reset StreamCache when the spool file has been deleted

[CAMEL-21161](https://issues.apache.org/jira/browse/CAMEL-21161)

camel-aws2-s3 is uploading always files as multipart when multiPartUpload is set true

[CAMEL-21160](https://issues.apache.org/jira/browse/CAMEL-21160)

camel-langchain4j-chat: consumer is not configured

[CAMEL-21159](https://issues.apache.org/jira/browse/CAMEL-21159)

camel-langchain4j-chat: producer is supported for chat with tools

[CAMEL-21155](https://issues.apache.org/jira/browse/CAMEL-21155)

camel-yaml-dsl - "parameters" property generated for "poll" EIP

[CAMEL-21154](https://issues.apache.org/jira/browse/CAMEL-21154)

camel-hashicorp-vault: Potential NPE in getSecret operation result handling

[CAMEL-21149](https://issues.apache.org/jira/browse/CAMEL-21149)

Camel debugger suspend on start is not working with SpringBoot

[CAMEL-21148](https://issues.apache.org/jira/browse/CAMEL-21148)

camel-jbang - camel run seems to get stuck at start up time when using camel-version config set

[CAMEL-21139](https://issues.apache.org/jira/browse/CAMEL-21139)

camel-jbang - Export to Q or SB should work with ignore-loading-error option

[CAMEL-21134](https://issues.apache.org/jira/browse/CAMEL-21134)

camel-jbang: unable to export Quarkus project due to missing CDIProvider

[CAMEL-21129](https://issues.apache.org/jira/browse/CAMEL-21129)

NPE rooted in RestBindingAdviceFactory in camel-support after upgrade 4.6->4.7

[CAMEL-21126](https://issues.apache.org/jira/browse/CAMEL-21126)

camel-jbang - Using source-dir and dropping a non route file causes reload issue

[CAMEL-21124](https://issues.apache.org/jira/browse/CAMEL-21124)

camel-jbang - unable to load properties from application.properties

[CAMEL-21114](https://issues.apache.org/jira/browse/CAMEL-21114)

camel-zipfile - ZipSplitter with AggregationStrategy does not aggregate all splits

[CAMEL-21112](https://issues.apache.org/jira/browse/CAMEL-21112)

camel-sql - Simple language to lookup parameter value is not compatible with batch mode

[CAMEL-21109](https://issues.apache.org/jira/browse/CAMEL-21109)

Choice evaluation behaves inconsistently when source is String and Value is Float.

[CAMEL-21101](https://issues.apache.org/jira/browse/CAMEL-21101)

Camel-Hashicorp-Vault: Get Secret operation doesn't take into account the secretPath configuration parameter

[CAMEL-21100](https://issues.apache.org/jira/browse/CAMEL-21100)

camel-azure-eventhubs: sharedAccessName & sharedAccessKey should not be required for credential type AZURE\_IDENTITY

[CAMEL-21096](https://issues.apache.org/jira/browse/CAMEL-21096)

interceptFrom with pattern specified are not executed with rest-dsl

[CAMEL-21093](https://issues.apache.org/jira/browse/CAMEL-21093)

fhir auth x springboot example is failing with ClassNotFoundException: org.apache.commons.io.function.Uncheck

[CAMEL-21090](https://issues.apache.org/jira/browse/CAMEL-21090)

Docs say CamelAs2.parameter but only CamelAS2.parameter works

[CAMEL-21082](https://issues.apache.org/jira/browse/CAMEL-21082)

camel-jbang init command is deleting existing routes/files when using --dir option

[CAMEL-21078](https://issues.apache.org/jira/browse/CAMEL-21078)

camel-test-junit5: enabling adviceWith should be available for consumer code.

[CAMEL-21076](https://issues.apache.org/jira/browse/CAMEL-21076)

camel-openapi-java: Incorrect schema is generated for array type request

[CAMEL-21075](https://issues.apache.org/jira/browse/CAMEL-21075)

camel-langchain4j-chat: unreliability due to failing to clear cached consumers

[CAMEL-21059](https://issues.apache.org/jira/browse/CAMEL-21059)

Cannot run or export when --repository is set before the integration file

[CAMEL-21057](https://issues.apache.org/jira/browse/CAMEL-21057)

REST OpenApi fails to resolve host from the URL

[CAMEL-21051](https://issues.apache.org/jira/browse/CAMEL-21051)

SftpOperations.retrieveFileToStreamInBody potentially hides exceptions

[CAMEL-21048](https://issues.apache.org/jira/browse/CAMEL-21048)

MLLP ACK invalid timestamp

[CAMEL-21045](https://issues.apache.org/jira/browse/CAMEL-21045)

camel-jbang - Export to quarkus will startup quarkus and hang JVM

[CAMEL-21044](https://issues.apache.org/jira/browse/CAMEL-21044)

azure-servicebus: FQNS not set correctly when credentialType is AZURE\_IDENTITY

[CAMEL-21035](https://issues.apache.org/jira/browse/CAMEL-21035)

Knative ceOverride property binding support misses first value being set

[CAMEL-21034](https://issues.apache.org/jira/browse/CAMEL-21034)

DefaultInjector created instead of SpringInjector when using custom ModelReifierFactory in Spring Boot app

[CAMEL-21014](https://issues.apache.org/jira/browse/CAMEL-21014)

The doFinally clause with a route template always generates an exception.

[CAMEL-21009](https://issues.apache.org/jira/browse/CAMEL-21009)

Camel-AWS2-Kinesis: CloudWatchAsyncClient and DynamoDbAsyncClient parameters are ignored from KCL Consumer

[CAMEL-21004](https://issues.apache.org/jira/browse/CAMEL-21004)

camel-jbang export does not use runtime from application.properties

[CAMEL-21003](https://issues.apache.org/jira/browse/CAMEL-21003)

camel-main: Unable to enable debug profile in Camel Quarkus due to FileNotFoundException

[CAMEL-20998](https://issues.apache.org/jira/browse/CAMEL-20998)

camel-google-storage: objectNames can conflict with each other

[CAMEL-20995](https://issues.apache.org/jira/browse/CAMEL-20995)

camel-azure-storage-blob uploadBlockBlob retry operation fails due to mark and reset issue / Flux

[CAMEL-20994](https://issues.apache.org/jira/browse/CAMEL-20994)

export fails to add camel-direct component when there is a rest consumer

[CAMEL-20993](https://issues.apache.org/jira/browse/CAMEL-20993)

camel-spring-boot: Failed route should be visible in spring-boot actuator/camelroutes endpoint

[CAMEL-20992](https://issues.apache.org/jira/browse/CAMEL-20992)

azure-service-bus component: When using RECEIVE\_AND\_DELETE mode, the ServiceBusConsumer onComplete and onFailure methods logs errors

[CAMEL-20991](https://issues.apache.org/jira/browse/CAMEL-20991)

camel-jbang - export error when there is placeholder in a kamelet endpoint url with a bean

[CAMEL-20988](https://issues.apache.org/jira/browse/CAMEL-20988)

camel-test-infra: some services are unable to properly log initialization failures

[CAMEL-20981](https://issues.apache.org/jira/browse/CAMEL-20981)

Knative ceOverrides option not possible with YAML config

[CAMEL-20969](https://issues.apache.org/jira/browse/CAMEL-20969)

camel-jbang: k8s plugin may generate conflicting docker build dependencies

[CAMEL-20966](https://issues.apache.org/jira/browse/CAMEL-20966)

Environment properties take precedence over route template's parameters

[CAMEL-20961](https://issues.apache.org/jira/browse/CAMEL-20961)

camel-jbang - NPE in log grep

[CAMEL-20960](https://issues.apache.org/jira/browse/CAMEL-20960)

camel-jbang - camel top processor should group by pid

[CAMEL-20958](https://issues.apache.org/jira/browse/CAMEL-20958)

camel-aws - Kinesis consumer loops on closed shards

[CAMEL-20954](https://issues.apache.org/jira/browse/CAMEL-20954)

Cannot share SSLContextParameters between camel-kafka and other components

[CAMEL-20953](https://issues.apache.org/jira/browse/CAMEL-20953)

camel-jbang - --max-\* options with --dev fails to terminate the Camel context

[CAMEL-20938](https://issues.apache.org/jira/browse/CAMEL-20938)

camel-http - Using disableStreamCache=true cannot read body later due to stream closed

[CAMEL-20918](https://issues.apache.org/jira/browse/CAMEL-20918)

Salesforce component does not resubscribe after exception

[CAMEL-20844](https://issues.apache.org/jira/browse/CAMEL-20844)

UseOriginalAggregationStrategy doesn't set EXCEPTION\_CAUGHT property on exception propagation

[CAMEL-20682](https://issues.apache.org/jira/browse/CAMEL-20682)

camel-kafka - KafkaIdempotentRepository misses continuous updates from its topic after startup

### Dependency upgrade (2)

[CAMEL-21074](https://issues.apache.org/jira/browse/CAMEL-21074)

camel-spring-boot - Upgrade to Spring Boot 3.3.3

[CAMEL-21002](https://issues.apache.org/jira/browse/CAMEL-21002)

Camel-Spring-Boot: Upgrade to Spring Boot 3.3.2

### Improvement (67)

[CAMEL-21177](https://issues.apache.org/jira/browse/CAMEL-21177)

camel-datasonnet: Enable libsonnet libraries to be discovered at build time

[CAMEL-21176](https://issues.apache.org/jira/browse/CAMEL-21176)

camel-core - DefaultExchangeHolder - Add option to store/read exchange variables

[CAMEL-21175](https://issues.apache.org/jira/browse/CAMEL-21175)

camel-jbang - automatically add package name when creating a Camel route with Java DSL in a src/main/java subfolder

[CAMEL-21170](https://issues.apache.org/jira/browse/CAMEL-21170)

camel-jbang - Dev console to show startup log

[CAMEL-21168](https://issues.apache.org/jira/browse/CAMEL-21168)

camel-core - Dev console to show startup configuration vs actual value

[CAMEL-21157](https://issues.apache.org/jira/browse/CAMEL-21157)

camel-core - PeriodicTask should be able to run a task forever

[CAMEL-21156](https://issues.apache.org/jira/browse/CAMEL-21156)

camel-hashicorp-vault: Allow SecretPath header to be used on create & delete operations

[CAMEL-21153](https://issues.apache.org/jira/browse/CAMEL-21153)

camel-langchain4j-chat: split function calling feature

[CAMEL-21150](https://issues.apache.org/jira/browse/CAMEL-21150)

camel-jbang - Make trace in standby mode and explicit enable to start tracing

[CAMEL-21144](https://issues.apache.org/jira/browse/CAMEL-21144)

camel-jbang - Run in dev mode can become slow when capturing trace data

[CAMEL-21140](https://issues.apache.org/jira/browse/CAMEL-21140)

camel-core - Add init and destroy method to @BindToRegistry

[CAMEL-21137](https://issues.apache.org/jira/browse/CAMEL-21137)

camel-core - Add lazy option to @BindToRegistry

[CAMEL-21136](https://issues.apache.org/jira/browse/CAMEL-21136)

camel-main - Add dev console for sending message to Camel via HTTP

[CAMEL-21135](https://issues.apache.org/jira/browse/CAMEL-21135)

camel-core - AdviceWith using toUri pattern should also support poll/enrich/pollEnrich EIPs

[CAMEL-21130](https://issues.apache.org/jira/browse/CAMEL-21130)

camel-jbang - Run with Q/SB runtime and dev mode for java source should update on save

[CAMEL-21120](https://issues.apache.org/jira/browse/CAMEL-21120)

camel-jbang - Reload with groovy code should flush cache script

[CAMEL-21118](https://issues.apache.org/jira/browse/CAMEL-21118)

camel-cxf - Add example to show how to integrate camel-cxfrs with opentelemetry

[CAMEL-21117](https://issues.apache.org/jira/browse/CAMEL-21117)

camel-jbang - Detect transacted dsl and add camel-jta automatically

[CAMEL-21116](https://issues.apache.org/jira/browse/CAMEL-21116)

Camel-AWS2-S3: Make ignoreBody supported also for getObject producer operation

[CAMEL-21099](https://issues.apache.org/jira/browse/CAMEL-21099)

camel-core - Source dev console to list files and raw mode

[CAMEL-21097](https://issues.apache.org/jira/browse/CAMEL-21097)

camel-as2 - Add more MIC security algorithms

[CAMEL-21089](https://issues.apache.org/jira/browse/CAMEL-21089)

camel-core: CamelBaseBulkConverterLoader should handle conversion to byte primitive

[CAMEL-21088](https://issues.apache.org/jira/browse/CAMEL-21088)

camel-jbang: Support Kubernetes export options in run command

[CAMEL-21086](https://issues.apache.org/jira/browse/CAMEL-21086)

camel-core - Add more complex functions to csimple language

[CAMEL-21081](https://issues.apache.org/jira/browse/CAMEL-21081)

camel-core - Add ternary if function to simple language

[CAMEL-21072](https://issues.apache.org/jira/browse/CAMEL-21072)

camel-test-infra-ollama: should use the Ollama container from testcontainers

[CAMEL-21071](https://issues.apache.org/jira/browse/CAMEL-21071)

camel-rest-openapi - Auto detect RestApiConsumerFactory from classpath

[CAMEL-21070](https://issues.apache.org/jira/browse/CAMEL-21070)

camel-jbang - rest and rest-openapi component should only be in included if in use

[CAMEL-21069](https://issues.apache.org/jira/browse/CAMEL-21069)

Review code: remove outdated items

[CAMEL-21066](https://issues.apache.org/jira/browse/CAMEL-21066)

Review documentation: remove outdated information

[CAMEL-21065](https://issues.apache.org/jira/browse/CAMEL-21065)

Enable Jolokia in camel.debug profile of generated Spring Boot project with Camel JBang

[CAMEL-21064](https://issues.apache.org/jira/browse/CAMEL-21064)

camel-as2 - Be case insensitive in http header parsing

[CAMEL-21055](https://issues.apache.org/jira/browse/CAMEL-21055)

camel-core-model - Add disabled to marshal and unmarshal EIP

[CAMEL-21054](https://issues.apache.org/jira/browse/CAMEL-21054)

camel-core-model - Can we make pollEnrich for static uri

[CAMEL-21053](https://issues.apache.org/jira/browse/CAMEL-21053)

camel-xslt - All exchange properties should be avaiable

[CAMEL-21052](https://issues.apache.org/jira/browse/CAMEL-21052)

camel-jbang - Export should not include camel-cli-connector by default

[CAMEL-21043](https://issues.apache.org/jira/browse/CAMEL-21043)

Make SyncPropertiesMojo dynamically determine the POM template version for the org.apache:apache parent

[CAMEL-21040](https://issues.apache.org/jira/browse/CAMEL-21040)

Review documentation: grammar, typos and other fixes

[CAMEL-21032](https://issues.apache.org/jira/browse/CAMEL-21032)

Generate k8s service for health endpoint

[CAMEL-21031](https://issues.apache.org/jira/browse/CAMEL-21031)

camel-aws-sqs: support for polling more than 10 messages from AWS SQS

[CAMEL-21026](https://issues.apache.org/jira/browse/CAMEL-21026)

camel-pdf: simplify conversion from byte array to PDF

[CAMEL-21017](https://issues.apache.org/jira/browse/CAMEL-21017)

camel-jbang: Consolidate OpenAPI options for export commands

[CAMEL-21016](https://issues.apache.org/jira/browse/CAMEL-21016)

camel-jbang: Add support for multiple build properties

[CAMEL-21015](https://issues.apache.org/jira/browse/CAMEL-21015)

When a plugin cannot be found, log a warning and continue execution instad of failing the command

[CAMEL-21011](https://issues.apache.org/jira/browse/CAMEL-21011)

Improve error message when Camel Jbang has unmatched arguments by mentioning possibility that a plugin is missing

[CAMEL-21006](https://issues.apache.org/jira/browse/CAMEL-21006)

Allow kubernetes export without image registry

[CAMEL-20990](https://issues.apache.org/jira/browse/CAMEL-20990)

camel-jbang: startup, readiness and liveness probes in kubernetes spring-boot

[CAMEL-20989](https://issues.apache.org/jira/browse/CAMEL-20989)

camel-jbang: Improve label matching in kubernetes spring-boot

[CAMEL-20979](https://issues.apache.org/jira/browse/CAMEL-20979)

null operation name when using contract first api

[CAMEL-20978](https://issues.apache.org/jira/browse/CAMEL-20978)

camel-core - Store timestamp for last route error

[CAMEL-20977](https://issues.apache.org/jira/browse/CAMEL-20977)

camel-core - Starting and stopping routes via jbang or JMX should WARN log if failing

[CAMEL-20976](https://issues.apache.org/jira/browse/CAMEL-20976)

camel-jbang: Consolidate export dependencies

[CAMEL-20975](https://issues.apache.org/jira/browse/CAMEL-20975)

camel-jbang: Derive image group from project groupId

[CAMEL-20973](https://issues.apache.org/jira/browse/CAMEL-20973)

log eip - Make it possible to configure log name more dynamic

[CAMEL-20972](https://issues.apache.org/jira/browse/CAMEL-20972)

camel-jbang - Be able to see route error message and stacktrace

[CAMEL-20970](https://issues.apache.org/jira/browse/CAMEL-20970)

camel-main - Allow to configure MainListener via application.properties

[CAMEL-20967](https://issues.apache.org/jira/browse/CAMEL-20967)

camel-main - Setting variable via properties should support int/long/boolean types

[CAMEL-20963](https://issues.apache.org/jira/browse/CAMEL-20963)

Migrate camel-main Kubernetes export functionality to JBang plugin

[CAMEL-20947](https://issues.apache.org/jira/browse/CAMEL-20947)

Enable Jolokia in camel.debug profile of generated Quarkus project with Camel JBang

[CAMEL-20869](https://issues.apache.org/jira/browse/CAMEL-20869)

camel-spring-rabbitmq properties of "skip" is not implement

[CAMEL-20774](https://issues.apache.org/jira/browse/CAMEL-20774)

camel-core-xml - Align the type tns:keyStoreParametersFactoryBean to the object KeyStoreParameters

[CAMEL-20638](https://issues.apache.org/jira/browse/CAMEL-20638)

camel-platform-http - Do not return http request headers

[CAMEL-20569](https://issues.apache.org/jira/browse/CAMEL-20569)

camel-catalog - Can we markup what functions and operations languages have for tooling assistance

[CAMEL-20393](https://issues.apache.org/jira/browse/CAMEL-20393)

Splunk-hec, splunk: add ssl configuration into the component

[CAMEL-20237](https://issues.apache.org/jira/browse/CAMEL-20237)

camel-platform-http-main - Make it possible to configure http auth

[CAMEL-20097](https://issues.apache.org/jira/browse/CAMEL-20097)

camel-platform-http-starter - Can we support the new useStreaming option

[CAMEL-19182](https://issues.apache.org/jira/browse/CAMEL-19182)

camel-platform-http-starter - Async processing with Spring Boot

### New Feature (29)

[CAMEL-21178](https://issues.apache.org/jira/browse/CAMEL-21178)

camel-jbang - Add browse command to browse endpoints

[CAMEL-21173](https://issues.apache.org/jira/browse/CAMEL-21173)

Camel-Jbang Dev Console: Add Kubernetes Vault support

[CAMEL-21172](https://issues.apache.org/jira/browse/CAMEL-21172)

Camel-Jbang Dev Console: Add Hashicorp Vault support

[CAMEL-21167](https://issues.apache.org/jira/browse/CAMEL-21167)

Camel-Spring-Boot: Kubernetes Secrets Trigger context reloading on update support

[CAMEL-21142](https://issues.apache.org/jira/browse/CAMEL-21142)

Kubernetes Secrets: Trigger context reloading on update

[CAMEL-21119](https://issues.apache.org/jira/browse/CAMEL-21119)

Improve support for java.nio.file.Path

[CAMEL-21110](https://issues.apache.org/jira/browse/CAMEL-21110)

camel-jbang - Make it easy to service HTML/JS pages

[CAMEL-21105](https://issues.apache.org/jira/browse/CAMEL-21105)

Camel-Kubernetes: Configmap creation should allow to add annotations

[CAMEL-21103](https://issues.apache.org/jira/browse/CAMEL-21103)

camel-platform-http-main - Add download functionality

[CAMEL-21094](https://issues.apache.org/jira/browse/CAMEL-21094)

Merge multiple PDF files in camel-pdf

[CAMEL-21036](https://issues.apache.org/jira/browse/CAMEL-21036)

Recovering cloud native properties

[CAMEL-21021](https://issues.apache.org/jira/browse/CAMEL-21021)

Camel-AWS-Secrets-Manager: Give the ability of refreshing the context on Secrets update by using Eventbridge service instead of pure Cloudtrail

[CAMEL-21001](https://issues.apache.org/jira/browse/CAMEL-21001)

camel-jbang: Kubernetes plugin: Add Route trait

[CAMEL-21000](https://issues.apache.org/jira/browse/CAMEL-21000)

camel-jbang: Kubernetes plugin: Add Ingress trait

[CAMEL-20996](https://issues.apache.org/jira/browse/CAMEL-20996)

camel-solr: revive component and upgrade to the latest version

[CAMEL-20987](https://issues.apache.org/jira/browse/CAMEL-20987)

camel-tahu: Create Sparkplug B component with Eclipse Tahu library

[CAMEL-20985](https://issues.apache.org/jira/browse/CAMEL-20985)

camel-jbang: Kubernetes plugin: Support Camel K integrations and pipes in export

[CAMEL-20984](https://issues.apache.org/jira/browse/CAMEL-20984)

camel-jbang: Kubernetes plugin: Complete container trait options

[CAMEL-20983](https://issues.apache.org/jira/browse/CAMEL-20983)

camel-jbang: Kubernetes plugin: Knative trait profile

[CAMEL-20982](https://issues.apache.org/jira/browse/CAMEL-20982)

camel-jbang: Kubernetes plugin: Add service trait

[CAMEL-20980](https://issues.apache.org/jira/browse/CAMEL-20980)

Allow to set custom Jackson object mapper on the JSON Schema Validator

[CAMEL-20971](https://issues.apache.org/jira/browse/CAMEL-20971)

camel - aws - S3 getObject consumer does not accept dynamic keyname

[CAMEL-20962](https://issues.apache.org/jira/browse/CAMEL-20962)

camel-jbang: SpringBoot support in Kubernetes plugin

[CAMEL-20956](https://issues.apache.org/jira/browse/CAMEL-20956)

camel-kafka - Add dev console

[CAMEL-20935](https://issues.apache.org/jira/browse/CAMEL-20935)

Camel langchain4j web-search

[CAMEL-20904](https://issues.apache.org/jira/browse/CAMEL-20904)

camel-jbang - Run and deploy to Kubernetes

[CAMEL-20896](https://issues.apache.org/jira/browse/CAMEL-20896)

Camel migration tool

[CAMEL-20468](https://issues.apache.org/jira/browse/CAMEL-20468)

Camel-AWS-Bedrock: Support available models

[CAMEL-6070](https://issues.apache.org/jira/browse/CAMEL-6070)

camel-test - Add annotations to configure test class instead of using methods

### Sub-task (5)

[CAMEL-21171](https://issues.apache.org/jira/browse/CAMEL-21171)

Kubernetes Secrets: Trigger context reloading on update - Add info for console with last update

[CAMEL-21169](https://issues.apache.org/jira/browse/CAMEL-21169)

Kubernetes Secrets: Trigger context reloading on update - Documentation

[CAMEL-21025](https://issues.apache.org/jira/browse/CAMEL-21025)

Camel-AWS-Secrets-Manager: Give the ability of refreshing the context on Secrets update by using Eventbridge service instead of pure Cloudtrail - Spring Boot support

[CAMEL-21024](https://issues.apache.org/jira/browse/CAMEL-21024)

Camel-AWS-Secrets-Manager: Eventbridge/SQS notifications documentation

[CAMEL-20765](https://issues.apache.org/jira/browse/CAMEL-20765)

Camel-AWS-Bedrock: Support Amazon Titan Text Embeddings V2

### Task (22)

[CAMEL-21270](https://issues.apache.org/jira/browse/CAMEL-21270)

camel-jbang: tests are using too much resources in the $TMP

[CAMEL-21106](https://issues.apache.org/jira/browse/CAMEL-21106)

camel-jbang - Export to main should keep support for jib/jkube

[CAMEL-21098](https://issues.apache.org/jira/browse/CAMEL-21098)

camel-test-support - Using junit global store is not working reliable

[CAMEL-21067](https://issues.apache.org/jira/browse/CAMEL-21067)

camel-univocity: deprecate due to unmaintained library

[CAMEL-21062](https://issues.apache.org/jira/browse/CAMEL-21062)

Azure Key Vault Properties function: Add documentation about creating required infra

[CAMEL-21061](https://issues.apache.org/jira/browse/CAMEL-21061)

Google Secrets Manager Properties function: Add documentation about creating required infra

[CAMEL-21060](https://issues.apache.org/jira/browse/CAMEL-21060)

AWS Secrets Manager Properties function: Add documentation about creating required infra

[CAMEL-21058](https://issues.apache.org/jira/browse/CAMEL-21058)

Camel-upgrade-recipes: cover upgrading camel 4.5 to 4.6

[CAMEL-21050](https://issues.apache.org/jira/browse/CAMEL-21050)

Camel-upgrade-recipes: cover upgradig camel 4.4 to 4.5

[CAMEL-21047](https://issues.apache.org/jira/browse/CAMEL-21047)

Camel-crypto: Bouncycastle dependency is not required with extracted PGPdataFormat

[CAMEL-21042](https://issues.apache.org/jira/browse/CAMEL-21042)

camel-guava-eventbus - Deprecate

[CAMEL-21038](https://issues.apache.org/jira/browse/CAMEL-21038)

Fix camel-spring.xsd generation to make it consistent

[CAMEL-21023](https://issues.apache.org/jira/browse/CAMEL-21023)

Camel-Spring-Boot: Add Langchain component starters Integration tests

[CAMEL-21022](https://issues.apache.org/jira/browse/CAMEL-21022)

Create Camel Langchain4j Web Search Starter

[CAMEL-21020](https://issues.apache.org/jira/browse/CAMEL-21020)

Remove obsolete integration tests for camel-restdsl-openapi-plugin

[CAMEL-21012](https://issues.apache.org/jira/browse/CAMEL-21012)

camel-milvus: action name mismatch with embeddings

[CAMEL-21010](https://issues.apache.org/jira/browse/CAMEL-21010)

camel-milvus: collection name mismatch with embeddings

[CAMEL-20986](https://issues.apache.org/jira/browse/CAMEL-20986)

camel-ai: improve chunking support

[CAMEL-20955](https://issues.apache.org/jira/browse/CAMEL-20955)

Add JBang plugin modules to Camel BOM

[CAMEL-20952](https://issues.apache.org/jira/browse/CAMEL-20952)

source javadoc issues

[CAMEL-20838](https://issues.apache.org/jira/browse/CAMEL-20838)

camel-test: block usages of internal APIs.

[CAMEL-20012](https://issues.apache.org/jira/browse/CAMEL-20012)

camel-quartz - replace Thread.sleep() in tests

### Test (6)

[CAMEL-21147](https://issues.apache.org/jira/browse/CAMEL-21147)

MulticastRouteTest.testRoute test is failing

[CAMEL-21146](https://issues.apache.org/jira/browse/CAMEL-21146)

Several soap tests are failing with java.lang.NoClassDefFoundError: org/jvnet/staxex/util/XMLStreamReaderToXMLStreamWriter$Breakpoint

[CAMEL-21143](https://issues.apache.org/jira/browse/CAMEL-21143)

camel-tahu: unstable tests are blocking the CI

[CAMEL-21125](https://issues.apache.org/jira/browse/CAMEL-21125)

Fix issue related to flaky test MulticastRouteTest.testRoute

[CAMEL-21123](https://issues.apache.org/jira/browse/CAMEL-21123)

Fix issue related to flaky test SimpleLRUCacheTest.concurrentPut

[CAMEL-21108](https://issues.apache.org/jira/browse/CAMEL-21108)

AMQPRouteTraceFrameTest.testTraceFrame is failing on main branch

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).