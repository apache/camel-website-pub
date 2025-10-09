# Apache camel 4.10.0 Release

## New and Noteworthy

This release is the new Camel 4.10.0 release.

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
      <version>4.10.0</version>
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
      <version>4.10.0</version>
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
| [apache-camel-4.10.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-src.zip.sha512) |
| [apache-camel-4.10.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.xml.sha512) |
| [apache-camel-4.10.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.0/apache-camel-4.10.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (54)

[CAMEL-21721](https://issues.apache.org/jira/browse/CAMEL-21721)

camel-azure-key-vault: validation of the credentials in component is too strict

[CAMEL-21720](https://issues.apache.org/jira/browse/CAMEL-21720)

camel-kubernetes: Unhealthy pods may be elected as the cluster leader

[CAMEL-21715](https://issues.apache.org/jira/browse/CAMEL-21715)

Fix camel-test-infra-common test-jar dependencies

[CAMEL-21713](https://issues.apache.org/jira/browse/CAMEL-21713)

camel-aws-secret-manager: context reload task does not accept endpoint override url

[CAMEL-21704](https://issues.apache.org/jira/browse/CAMEL-21704)

camel-spring-boot - Platform HTTP does not add attchments

[CAMEL-21702](https://issues.apache.org/jira/browse/CAMEL-21702)

Unable to delete OpenShift deployment using 'camel kubernetes delete'

[CAMEL-21694](https://issues.apache.org/jira/browse/CAMEL-21694)

camel-jbang - Export to older Camel version does not work

[CAMEL-21692](https://issues.apache.org/jira/browse/CAMEL-21692)

camel-jbang: using mock in openapi contract first approach won't work anymore

[CAMEL-21690](https://issues.apache.org/jira/browse/CAMEL-21690)

camel-jbang - Image push option on Kubernetes run command not working

[CAMEL-21687](https://issues.apache.org/jira/browse/CAMEL-21687)

camel-core - Cannot add onCompletion after transacted in Java DSL

[CAMEL-21686](https://issues.apache.org/jira/browse/CAMEL-21686)

camel-jbang - Remove dependency on camel-kamelets-utils

[CAMEL-21684](https://issues.apache.org/jira/browse/CAMEL-21684)

camel-rest-openapi - Using x-forward headers is not included

[CAMEL-21672](https://issues.apache.org/jira/browse/CAMEL-21672)

camel-azure-servicebus: processorClient option is not honoured

[CAMEL-21668](https://issues.apache.org/jira/browse/CAMEL-21668)

camel-jbang: error on running transform command if ~/.camel folder doesn't exist

[CAMEL-21665](https://issues.apache.org/jira/browse/CAMEL-21665)

camel-jbang - kubernetes plugin not deleting deployed integration

[CAMEL-21656](https://issues.apache.org/jira/browse/CAMEL-21656)

camel-jms - Multiple routes with direct/activemq and recipientlist returns unexpected result

[CAMEL-21653](https://issues.apache.org/jira/browse/CAMEL-21653)

Camel Jbang run ignore "--repos" option

[CAMEL-21625](https://issues.apache.org/jira/browse/CAMEL-21625)

camel k8s run may not cleanup properly on openshift

[CAMEL-21621](https://issues.apache.org/jira/browse/CAMEL-21621)

camel-jbang - k8s-httpclient-vertx fails in shutdown hook

[CAMEL-21616](https://issues.apache.org/jira/browse/CAMEL-21616)

camel-main - Route exclude pattern does not work for discovered java classes

[CAMEL-21614](https://issues.apache.org/jira/browse/CAMEL-21614)

Simple expressions execute forever. Thread is RUNNABLE for ever. Issue appears with bean expressions inside simple expressions on SimpleLRUCache

[CAMEL-21612](https://issues.apache.org/jira/browse/CAMEL-21612)

\[Regression\] Camel JMX debugger is no more activated with org.apache.camel:camel-debug dependency

[CAMEL-21606](https://issues.apache.org/jira/browse/CAMEL-21606)

Camel route validation mojo fails if it depends on external sources

[CAMEL-21599](https://issues.apache.org/jira/browse/CAMEL-21599)

Global Error Handler does not take effect when a source Kamelet fails

[CAMEL-21595](https://issues.apache.org/jira/browse/CAMEL-21595)

camel-langchain4j-tools: code may thrown an NPE if no tools are called

[CAMEL-21594](https://issues.apache.org/jira/browse/CAMEL-21594)

Camel Langchain4j Tools bug where no need to execute a tool

[CAMEL-21580](https://issues.apache.org/jira/browse/CAMEL-21580)

Potential ConcurrentModificationException in MessageSupport.copyFromWithNewBody(MessageSupport.java:226)

[CAMEL-21575](https://issues.apache.org/jira/browse/CAMEL-21575)

camel-main: concurrency issues on Java 21

[CAMEL-21572](https://issues.apache.org/jira/browse/CAMEL-21572)

Camel JBang with --runtime=spring-boot throw NullPointerException

[CAMEL-21567](https://issues.apache.org/jira/browse/CAMEL-21567)

camel-jbang - Debug command should accept options from run

[CAMEL-21562](https://issues.apache.org/jira/browse/CAMEL-21562)

If HeadBucket call is not allowed, AWS2S3Endpoint fails to start

[CAMEL-21557](https://issues.apache.org/jira/browse/CAMEL-21557)

camel-platform-http-starter HttpBinding does not support concurrent multipart/form-data requests with the same key id

[CAMEL-21555](https://issues.apache.org/jira/browse/CAMEL-21555)

Smooks component parses DFDL EDIFACT schema upon the first message arrival only

[CAMEL-21552](https://issues.apache.org/jira/browse/CAMEL-21552)

camel-yaml-dsl - "param" property from YAML DSL is not present in Camel model

[CAMEL-21550](https://issues.apache.org/jira/browse/CAMEL-21550)

camel-aws-sqs - message is getting expired before extender changes the visibility

[CAMEL-21545](https://issues.apache.org/jira/browse/CAMEL-21545)

camel-jsonpath - Should not use XmlMapper

[CAMEL-21543](https://issues.apache.org/jira/browse/CAMEL-21543)

camel-main - MainListenerClasses loaded from application.properties is not activated

[CAMEL-21536](https://issues.apache.org/jira/browse/CAMEL-21536)

camel-platform-http-starter throws "No ThreadPoolTaskExecutor configured" if virtual threads are enabled

[CAMEL-21532](https://issues.apache.org/jira/browse/CAMEL-21532)

Camel JBang --logging-category is not respected on Windows

[CAMEL-21531](https://issues.apache.org/jira/browse/CAMEL-21531)

RestOpenApiReaderTest is broken for some locations

[CAMEL-21528](https://issues.apache.org/jira/browse/CAMEL-21528)

camel-vertx-http: Response handling may block the Vert.x event loop

[CAMEL-21526](https://issues.apache.org/jira/browse/CAMEL-21526)

camel-aws - Unable to set Timestamp in query parameters to initialize iterator of AT\_TIMESTAMP type for AWS Kinesis component

[CAMEL-21525](https://issues.apache.org/jira/browse/CAMEL-21525)

Issue camel-debezium-postgres-starter Auto-Configured Bean

[CAMEL-21516](https://issues.apache.org/jira/browse/CAMEL-21516)

camel-jbang - Transform route from xml to yaml with uri-as-parameters for context-path

[CAMEL-21512](https://issues.apache.org/jira/browse/CAMEL-21512)

camel-jbang - camel transform route with multiple <rest> only include last

[CAMEL-21506](https://issues.apache.org/jira/browse/CAMEL-21506)

camel-pdf: type converter doesn't work with the file component

[CAMEL-21505](https://issues.apache.org/jira/browse/CAMEL-21505)

camel-as2: Binary files get corrupt when using 'base64' content transfer encoding

[CAMEL-21504](https://issues.apache.org/jira/browse/CAMEL-21504)

camel-spring-boot - MicrometerTagsAutoConfiguration class puts http method in uri tag

[CAMEL-21495](https://issues.apache.org/jira/browse/CAMEL-21495)

camel-quarkus: REST route inlining works incorrectly when testing

[CAMEL-21486](https://issues.apache.org/jira/browse/CAMEL-21486)

camel k8s ... cannot push to image-registry.openshift-image-registry.svc:5000

[CAMEL-21463](https://issues.apache.org/jira/browse/CAMEL-21463)

Camel-jbang while running the process in background unable to access log if the process start fails with errors

[CAMEL-21442](https://issues.apache.org/jira/browse/CAMEL-21442)

camel-jbang export is not working when local-kamelet-dir set to current dir

[CAMEL-21418](https://issues.apache.org/jira/browse/CAMEL-21418)

camel-rest - Client request validation and multiple values in Accept header

[CAMEL-21400](https://issues.apache.org/jira/browse/CAMEL-21400)

StackOverflowError when processing files

### Dependency upgrade (16)

[CAMEL-21681](https://issues.apache.org/jira/browse/CAMEL-21681)

camel-microprofile-health - Upgrade to 4.2

[CAMEL-21655](https://issues.apache.org/jira/browse/CAMEL-21655)

Upgrade to CXF 4.1.0

[CAMEL-21651](https://issues.apache.org/jira/browse/CAMEL-21651)

Upgrade to Jolokia 2.2.1

[CAMEL-21635](https://issues.apache.org/jira/browse/CAMEL-21635)

camel-spring-boot - Upgrade to 3.4.2

[CAMEL-21627](https://issues.apache.org/jira/browse/CAMEL-21627)

camel-jbang - Upgrade jkube 1.18

[CAMEL-21607](https://issues.apache.org/jira/browse/CAMEL-21607)

camel-quickfix - Upgrade to 2.3.2

[CAMEL-21590](https://issues.apache.org/jira/browse/CAMEL-21590)

camel-pulsar - Upgrade to 3.3.3

[CAMEL-21571](https://issues.apache.org/jira/browse/CAMEL-21571)

camel-mina - Upgrade to 2.2.4

[CAMEL-21569](https://issues.apache.org/jira/browse/CAMEL-21569)

camel-wasm - Upgrade to 1.0

[CAMEL-21564](https://issues.apache.org/jira/browse/CAMEL-21564)

camel-spring-boot - Upgrade to SB 3.4.1

[CAMEL-21561](https://issues.apache.org/jira/browse/CAMEL-21561)

camel-kafka - Upgrade to kafka 3.8.1

[CAMEL-21548](https://issues.apache.org/jira/browse/CAMEL-21548)

camel-cxf - Upgrade to 4.1

[CAMEL-21514](https://issues.apache.org/jira/browse/CAMEL-21514)

camel-jgropus - Upgrade to 5.4 and remove cluster lock

[CAMEL-21509](https://issues.apache.org/jira/browse/CAMEL-21509)

camel-kubernetes - Upgrade to v7 of fabric8-client

[CAMEL-21465](https://issues.apache.org/jira/browse/CAMEL-21465)

camel-cassandraql: Upgrade java-driver dependencies to 4.18.x

[CAMEL-19839](https://issues.apache.org/jira/browse/CAMEL-19839)

camel-cxf-common jakarta dependencies not alligned with cxf transports

### Improvement (86)

[CAMEL-21728](https://issues.apache.org/jira/browse/CAMEL-21728)

camel-core - Add onPrepare for Loop EIP to allow deep copy of exchange

[CAMEL-21725](https://issues.apache.org/jira/browse/CAMEL-21725)

camel-jbang - Dependency list command to work on maven based project

[CAMEL-21717](https://issues.apache.org/jira/browse/CAMEL-21717)

camel-groovy - Make it easier to work with attachments

[CAMEL-21716](https://issues.apache.org/jira/browse/CAMEL-21716)

Customize base image in JBang Kubernetes plugin

[CAMEL-21714](https://issues.apache.org/jira/browse/CAMEL-21714)

camel-cxf: CachedCxfPayload needs to LOG the parsing XMLStreamReader exception

[CAMEL-21711](https://issues.apache.org/jira/browse/CAMEL-21711)

camel-core - IOConverter file/path to string should handle binary files

[CAMEL-21709](https://issues.apache.org/jira/browse/CAMEL-21709)

camel-jbang - use route as top-level attribute when creating a Camel Yaml dsl route

[CAMEL-21708](https://issues.apache.org/jira/browse/CAMEL-21708)

camel-attachments - Determine mime-type

[CAMEL-21706](https://issues.apache.org/jira/browse/CAMEL-21706)

Improve JBang Kubernetes run with quiet mode

[CAMEL-21703](https://issues.apache.org/jira/browse/CAMEL-21703)

camel-attachments - Add functions to simple language

[CAMEL-21701](https://issues.apache.org/jira/browse/CAMEL-21701)

camel-platform-http - Make single file upload easy to access from message body

[CAMEL-21700](https://issues.apache.org/jira/browse/CAMEL-21700)

camel-platform-http-main - Handle file uploads by default

[CAMEL-21699](https://issues.apache.org/jira/browse/CAMEL-21699)

camel-kafka - Batch consumer should not require message body to keep being List<Exchange>

[CAMEL-21697](https://issues.apache.org/jira/browse/CAMEL-21697)

camel-solr - The headers should use CamelSolrXXX prefix

[CAMEL-21695](https://issues.apache.org/jira/browse/CAMEL-21695)

Remove remaining camel-k code from camel-jbang

[CAMEL-21691](https://issues.apache.org/jira/browse/CAMEL-21691)

camel-kafka - Add pollIntervalMs option to trigger batch completion per interval

[CAMEL-21688](https://issues.apache.org/jira/browse/CAMEL-21688)

\[camel-jbang\] Export to Spring Boot may not work in certain cases

[CAMEL-21685](https://issues.apache.org/jira/browse/CAMEL-21685)

camel-jbang - Deprecate modeline and WARN if in use

[CAMEL-21683](https://issues.apache.org/jira/browse/CAMEL-21683)

camel-cxf - Configure jax-rs consumer via CxfRsEndpoint bean

[CAMEL-21682](https://issues.apache.org/jira/browse/CAMEL-21682)

Camel-Google-Storage: Introducing Override Bucket Header in Producer operations

[CAMEL-21680](https://issues.apache.org/jira/browse/CAMEL-21680)

Camel-AWS2-S3: Introducing Override Bucket Header in Producer operations

[CAMEL-21679](https://issues.apache.org/jira/browse/CAMEL-21679)

camel-azure-servicebus: azure-servicebus: Unable to set only senderClient or processorClient

[CAMEL-21678](https://issues.apache.org/jira/browse/CAMEL-21678)

Camel-Minio: Introducing Override Bucket Header in Producer operations

[CAMEL-21677](https://issues.apache.org/jira/browse/CAMEL-21677)

\[camel-core\] Strenghten org.apache.camel.NoSuchEndpointException

[CAMEL-21675](https://issues.apache.org/jira/browse/CAMEL-21675)

camel-kamelet - Allow to call another kamelet from within a kamelet

[CAMEL-21661](https://issues.apache.org/jira/browse/CAMEL-21661)

camel-micrometer - multiple registrations of gauge camel.exchanges.inflight

[CAMEL-21660](https://issues.apache.org/jira/browse/CAMEL-21660)

camel-kamelet - Allow to configure consumer bridgeErrorHandler option

[CAMEL-21659](https://issues.apache.org/jira/browse/CAMEL-21659)

Improve aws sqs TimeoutExtender by introducing deadline concept to messages

[CAMEL-21657](https://issues.apache.org/jira/browse/CAMEL-21657)

camel-ftp - Add dev console to dump jsch config

[CAMEL-21654](https://issues.apache.org/jira/browse/CAMEL-21654)

camel-micrometer - Use base endpoint uri as dynamic values can lead too many combinations

[CAMEL-21649](https://issues.apache.org/jira/browse/CAMEL-21649)

camel-micrometer - Add option to configure InstrumentedThreadPoolFactory

[CAMEL-21648](https://issues.apache.org/jira/browse/CAMEL-21648)

camel-opentelemetry: Provide a way to customize Span creation

[CAMEL-21645](https://issues.apache.org/jira/browse/CAMEL-21645)

\[camel-jbang\] implement camel export --property

[CAMEL-21643](https://issues.apache.org/jira/browse/CAMEL-21643)

camel-jbang - Export main runtime should not log to file

[CAMEL-21641](https://issues.apache.org/jira/browse/CAMEL-21641)

camel-jbang - Configuring components in Java DSL best practice

[CAMEL-21637](https://issues.apache.org/jira/browse/CAMEL-21637)

camel-jbang - Shell command to stop --watch when pressing ctrl-c

[CAMEL-21634](https://issues.apache.org/jira/browse/CAMEL-21634)

camel-jbang - Add camel-quartz as dependency if using camel-cron

[CAMEL-21632](https://issues.apache.org/jira/browse/CAMEL-21632)

camel-spring-xml - Can we avoid the duplicate ##other in XSD

[CAMEL-21630](https://issues.apache.org/jira/browse/CAMEL-21630)

camel-core - Remove inheritErrorHandler from DSL

[CAMEL-21628](https://issues.apache.org/jira/browse/CAMEL-21628)

camel-core: Make AggregateProcessor set the CamelContext on its AggregationRepository

[CAMEL-21622](https://issues.apache.org/jira/browse/CAMEL-21622)

camel-tracing - add route id in the tags of the span

[CAMEL-21620](https://issues.apache.org/jira/browse/CAMEL-21620)

camel-core - Fix onWhen to not include outputs in model

[CAMEL-21615](https://issues.apache.org/jira/browse/CAMEL-21615)

camel-jbang - Nicer error when export without name or gav

[CAMEL-21611](https://issues.apache.org/jira/browse/CAMEL-21611)

camel-jbang - camel shell - Use Camel as group name

[CAMEL-21608](https://issues.apache.org/jira/browse/CAMEL-21608)

Add support for message tags to Amazon SES component

[CAMEL-21605](https://issues.apache.org/jira/browse/CAMEL-21605)

camel-jbang - Send command should also be as dev console

[CAMEL-21596](https://issues.apache.org/jira/browse/CAMEL-21596)

Camel Qdrant add Vector search

[CAMEL-21593](https://issues.apache.org/jira/browse/CAMEL-21593)

camel-aws-ses - Add support for sending already created RawMessage

[CAMEL-21589](https://issues.apache.org/jira/browse/CAMEL-21589)

Make manual acknowledgements configurable in Paho-Mqtt5

[CAMEL-21582](https://issues.apache.org/jira/browse/CAMEL-21582)

PropertiesComponent requires LoadablePropertiesSource which was removed by CAMEL-21480 and CAMEL-21484

[CAMEL-21578](https://issues.apache.org/jira/browse/CAMEL-21578)

Avoid "'build.plugins.plugin.version' for org.apache.maven.plugins:maven-resources-plugin is missing." when exporting openshift project with Camel Jbang

[CAMEL-21568](https://issues.apache.org/jira/browse/CAMEL-21568)

camel-jbang - Debug should support step into/over

[CAMEL-21563](https://issues.apache.org/jira/browse/CAMEL-21563)

Camel-Jbang ps output in JSON

[CAMEL-21559](https://issues.apache.org/jira/browse/CAMEL-21559)

camel-mongodb - Improve save performance

[CAMEL-21558](https://issues.apache.org/jira/browse/CAMEL-21558)

camel-maven-package-plugin broken package name (velocity

[CAMEL-21549](https://issues.apache.org/jira/browse/CAMEL-21549)

camel-spring-boot - No CamelContext defined yet so cannot inject into bean: startupConditionStrategy

[CAMEL-21544](https://issues.apache.org/jira/browse/CAMEL-21544)

camel-http-common - Add option to turn on|off whether application/x-www-form-urlencoded should populate Map body with form

[CAMEL-21542](https://issues.apache.org/jira/browse/CAMEL-21542)

camel-jbang - Detect known beans from Java imports

[CAMEL-21538](https://issues.apache.org/jira/browse/CAMEL-21538)

\[camel-tracing\] Deprecate MDC in favour of implementation specific instrumentation

[CAMEL-21535](https://issues.apache.org/jira/browse/CAMEL-21535)

camel-groovy - Make it easier for low-code to validate scripts

[CAMEL-21524](https://issues.apache.org/jira/browse/CAMEL-21524)

camel-jbang - Report error/warning when a Camel catalog cannot be loaded

[CAMEL-21522](https://issues.apache.org/jira/browse/CAMEL-21522)

camel-core - Log EIP allow to use custom log name per log

[CAMEL-21519](https://issues.apache.org/jira/browse/CAMEL-21519)

camel-jbang - camel transform route - Expression should be quoted

[CAMEL-21518](https://issues.apache.org/jira/browse/CAMEL-21518)

camel-elasticsearch-rest: Add capability to set operation via a header

[CAMEL-21515](https://issues.apache.org/jira/browse/CAMEL-21515)

camel-google-pubsub - Add Support for Custom Retry Settings in Google Pub/Sub Publisher

[CAMEL-21511](https://issues.apache.org/jira/browse/CAMEL-21511)

camel-jbang - camel transform route with rest-dsl should not inline routes

[CAMEL-21510](https://issues.apache.org/jira/browse/CAMEL-21510)

camel-jbang - Kubernetes plugin support for parameter name

[CAMEL-21494](https://issues.apache.org/jira/browse/CAMEL-21494)

camel-file - Producer should be AsyncProducer based

[CAMEL-21491](https://issues.apache.org/jira/browse/CAMEL-21491)

\[camel-observability-services\] Add OTLP autoconfigure as default for main

[CAMEL-21484](https://issues.apache.org/jira/browse/CAMEL-21484)

DefaultPropertiesLookup loads all props from microprofile config per property value lookup

[CAMEL-21480](https://issues.apache.org/jira/browse/CAMEL-21480)

camel-microprofile-config: Add support in CamelMicroProfilePropertiesSource for multiple profile properties

[CAMEL-21479](https://issues.apache.org/jira/browse/CAMEL-21479)

Camel-Solr: Use HttpJdkSolrClient as default SolrClient implementation

[CAMEL-21478](https://issues.apache.org/jira/browse/CAMEL-21478)

camel-rest-openapi: Input and output types binding to java classes using $ref or title of the schema

[CAMEL-21468](https://issues.apache.org/jira/browse/CAMEL-21468)

camel-http - Add option to log raw request and raw response

[CAMEL-21456](https://issues.apache.org/jira/browse/CAMEL-21456)

Camel-Jbang Kubernetes Plugin Ingress add TLS

[CAMEL-21433](https://issues.apache.org/jira/browse/CAMEL-21433)

camel run/export --runtime quarkus can't use a route from subdirectory

[CAMEL-21359](https://issues.apache.org/jira/browse/CAMEL-21359)

camel-spring-boot - Add support for using MainListener

[CAMEL-21352](https://issues.apache.org/jira/browse/CAMEL-21352)

camel-smb - Based on camel-file to have many more features

[CAMEL-21325](https://issues.apache.org/jira/browse/CAMEL-21325)

camel-jbang - Kubernetes run should cleanup old temp folders

[CAMEL-21274](https://issues.apache.org/jira/browse/CAMEL-21274)

camel-test - Add option to dump routes for all tests

[CAMEL-21257](https://issues.apache.org/jira/browse/CAMEL-21257)

Camel GitHub commit consumer body does not match documentation

[CAMEL-21250](https://issues.apache.org/jira/browse/CAMEL-21250)

camel-report-maven-plugin - Can we cover anonymous routes if loaded from xml files

[CAMEL-21223](https://issues.apache.org/jira/browse/CAMEL-21223)

camel-jbang - Debug may not go inside Split EIP

[CAMEL-21184](https://issues.apache.org/jira/browse/CAMEL-21184)

Make more components Browseable

[CAMEL-19665](https://issues.apache.org/jira/browse/CAMEL-19665)

components that are polling can become batch polling

[CAMEL-17648](https://issues.apache.org/jira/browse/CAMEL-17648)

Optimizing File component performance when filtering file names.

### New Feature (20)

[CAMEL-21726](https://issues.apache.org/jira/browse/CAMEL-21726)

Add OpenAI and HuggingFace Chat Models to create RAG Kameletes

[CAMEL-21719](https://issues.apache.org/jira/browse/CAMEL-21719)

Camel Neo4j component : transform results of similarity search into List of texts

[CAMEL-21718](https://issues.apache.org/jira/browse/CAMEL-21718)

Camel Qdrant component : transform results of similarity search into List of texts

[CAMEL-21650](https://issues.apache.org/jira/browse/CAMEL-21650)

Camel JBang update command

[CAMEL-21626](https://issues.apache.org/jira/browse/CAMEL-21626)

Camel-Hashicorp-Vault: Support Hashicorp Cloud deployment in properties function

[CAMEL-21623](https://issues.apache.org/jira/browse/CAMEL-21623)

Expose test-infra services via Camel JBang

[CAMEL-21586](https://issues.apache.org/jira/browse/CAMEL-21586)

Create a OpenAI Embedding Model builder acting as Java Bean for a Kamelet

[CAMEL-21560](https://issues.apache.org/jira/browse/CAMEL-21560)

Create a HugginFace Embedding Model builder acting as Java Bean for a Kamelet

[CAMEL-21553](https://issues.apache.org/jira/browse/CAMEL-21553)

Vault Properties Functions: Make it possible to use them even in bean instantiation

[CAMEL-21547](https://issues.apache.org/jira/browse/CAMEL-21547)

Migrate bean routing functionality from Smooks Cartridge to Smooks Component

[CAMEL-21541](https://issues.apache.org/jira/browse/CAMEL-21541)

Neo4j - investigate on ingesting data with Neo4j and Langchain4j

[CAMEL-21529](https://issues.apache.org/jira/browse/CAMEL-21529)

camel-catalog - Consider adding another version discovery step

[CAMEL-21508](https://issues.apache.org/jira/browse/CAMEL-21508)

Add a component for KServe

[CAMEL-21497](https://issues.apache.org/jira/browse/CAMEL-21497)

Camel-Kubernetes: Add Configmap Dev Console

[CAMEL-21496](https://issues.apache.org/jira/browse/CAMEL-21496)

Camel-Azure-Key-Vault: Add Update Secret operation to Producer

[CAMEL-21461](https://issues.apache.org/jira/browse/CAMEL-21461)

camel-spring-boot - Add features to Camel Platform Http Starter

[CAMEL-21107](https://issues.apache.org/jira/browse/CAMEL-21107)

Camel-Kubernetes: Add ability to add annotation to create resources operation

[CAMEL-21019](https://issues.apache.org/jira/browse/CAMEL-21019)

Add a component for TensorFlow Serving

[CAMEL-18276](https://issues.apache.org/jira/browse/CAMEL-18276)

azure-service-bus component does not support session

[CAMEL-17881](https://issues.apache.org/jira/browse/CAMEL-17881)

TLS for MLLP Component

### Sub-task (1)

[CAMEL-21640](https://issues.apache.org/jira/browse/CAMEL-21640)

Camel-Hashicorp-Vault: Support Hashicorp Cloud deployment in properties function - Docs

### Task (34)

[CAMEL-21727](https://issues.apache.org/jira/browse/CAMEL-21727)

documentation - Add note in docs to not use crazy high loop counter

[CAMEL-21689](https://issues.apache.org/jira/browse/CAMEL-21689)

Apache Camel Kafka Batching Consumer behaviour discrepancy w.r.t pollTimeoutMs

[CAMEL-21676](https://issues.apache.org/jira/browse/CAMEL-21676)

Kamelet - loading a xml kamelet throws NPE

[CAMEL-21673](https://issues.apache.org/jira/browse/CAMEL-21673)

camel-spring-boot - Fix missing stream closes

[CAMEL-21666](https://issues.apache.org/jira/browse/CAMEL-21666)

camel-test-infra-cli - Should skip testing if using -Pfastinstall

[CAMEL-21664](https://issues.apache.org/jira/browse/CAMEL-21664)

camel-kafka: avoid unecessary secondary cache miss on record metadata

[CAMEL-21663](https://issues.apache.org/jira/browse/CAMEL-21663)

camel-sjms2: lack of null check causes NPE and affects performance

[CAMEL-21647](https://issues.apache.org/jira/browse/CAMEL-21647)

Create a jenkins job for Camel JBang IT test suite

[CAMEL-21642](https://issues.apache.org/jira/browse/CAMEL-21642)

Camel-Hashicorp-Vault: Support Hashicorp cloud Vault instance in the pure component

[CAMEL-21639](https://issues.apache.org/jira/browse/CAMEL-21639)

Camel-Hashicorp-Vault-Starter: Support Hashicorp Cloud deployment in properties function

[CAMEL-21638](https://issues.apache.org/jira/browse/CAMEL-21638)

Provide ppc64le architecture support to camel-elasticsearch

[CAMEL-21636](https://issues.apache.org/jira/browse/CAMEL-21636)

Camel-upgrade-recipes: cover upgrading camel 4.9 to 4.10

[CAMEL-21633](https://issues.apache.org/jira/browse/CAMEL-21633)

Provide ppc64le architecture support to camel-elasticsearch-rest-client

[CAMEL-21631](https://issues.apache.org/jira/browse/CAMEL-21631)

Enable Checksum algorithm on S3 streaming upload producer

[CAMEL-21629](https://issues.apache.org/jira/browse/CAMEL-21629)

Camel-upgrade-recipes: test classes has to stay public

[CAMEL-21618](https://issues.apache.org/jira/browse/CAMEL-21618)

Review documentation for the next LTS release

[CAMEL-21617](https://issues.apache.org/jira/browse/CAMEL-21617)

camel-core - Add doCatch and doFinally to doTry json model

[CAMEL-21592](https://issues.apache.org/jira/browse/CAMEL-21592)

camel-tests: use Awaitility globally

[CAMEL-21591](https://issues.apache.org/jira/browse/CAMEL-21591)

Fix components using Awaitility from TestContainers

[CAMEL-21585](https://issues.apache.org/jira/browse/CAMEL-21585)

camel-test-infra: select platform-specific containers dynamically

[CAMEL-21581](https://issues.apache.org/jira/browse/CAMEL-21581)

Fix HashiCorp Vault Tests for ppc64le in camel-spring-boot

[CAMEL-21576](https://issues.apache.org/jira/browse/CAMEL-21576)

camel-test-infra: container pulling adjustments

[CAMEL-21570](https://issues.apache.org/jira/browse/CAMEL-21570)

Add Profile to skip Tests for ppc64le Architecture in aws2

[CAMEL-21537](https://issues.apache.org/jira/browse/CAMEL-21537)

Camel-mongodb - Provide ppc64le arch support

[CAMEL-21530](https://issues.apache.org/jira/browse/CAMEL-21530)

camel-jbang - Remove deps on runtime and cluster-type where no longer needed

[CAMEL-21517](https://issues.apache.org/jira/browse/CAMEL-21517)

Deprecate camel-google-pubsub-lite

[CAMEL-21503](https://issues.apache.org/jira/browse/CAMEL-21503)

camel-langchain4j-chat: remove function calling

[CAMEL-21502](https://issues.apache.org/jira/browse/CAMEL-21502)

camel-langchain4j-tools: fix incorrect documentation

[CAMEL-21500](https://issues.apache.org/jira/browse/CAMEL-21500)

camel-observability-services - Is missing in camel-catalog

[CAMEL-21452](https://issues.apache.org/jira/browse/CAMEL-21452)

camel-test-infra: decouple the infrastructure from the testing API

[CAMEL-21350](https://issues.apache.org/jira/browse/CAMEL-21350)

camel-spring-boot-examples - Update old dependencies

[CAMEL-21281](https://issues.apache.org/jira/browse/CAMEL-21281)

camel-jbang - Remove camel k plugin

[CAMEL-21266](https://issues.apache.org/jira/browse/CAMEL-21266)

camel-smb: the consumer should follow the same creation pattern

[CAMEL-20883](https://issues.apache.org/jira/browse/CAMEL-20883)

Remove addPluginArtifactMetadata mojo usage

### Test (4)

[CAMEL-21602](https://issues.apache.org/jira/browse/CAMEL-21602)

Fix issue related to flaky test DefaultConsumerTemplateWithCustomCacheMaxSizeTest.testCacheConsumers

[CAMEL-21601](https://issues.apache.org/jira/browse/CAMEL-21601)

Fix issue related to flaky test GitConsumerTest.commitConsumerTest

[CAMEL-21346](https://issues.apache.org/jira/browse/CAMEL-21346)

Test failing on main branch: StreamingApiConsumerTest.shouldProcessPlatformEvents

[CAMEL-21145](https://issues.apache.org/jira/browse/CAMEL-21145)

SolrCloudProducerIT is failing on ppc64le architecture

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).