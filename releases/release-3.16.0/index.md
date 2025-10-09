# Apache camel 3.16.0 Release

## New and Noteworthy

This release is the new Camel 3.16.0 release.

## Supported Java version

This version supports Java 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.16.0</version>
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
      <version>3.16.0</version>
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
| [apache-camel-3.16.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.16.0/apache-camel-3.16.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.16.0/apache-camel-3.16.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.16.0/apache-camel-3.16.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.16.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.16.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (31)

[CAMEL-17813](https://issues.apache.org/jira/browse/CAMEL-17813)

camel-kafka - DNS unresolvable bootstrap servers causes consumer to endless loop

[CAMEL-17808](https://issues.apache.org/jira/browse/CAMEL-17808)

camel-yaml-dsl - Multicast EIP does not have output added correctly

[CAMEL-17798](https://issues.apache.org/jira/browse/CAMEL-17798)

camel-kafka - Offsets resetting when another Camel node is shutdown

[CAMEL-17773](https://issues.apache.org/jira/browse/CAMEL-17773)

camel-http: HttpSendDynamicAware parse uri incroectly if there are empty path and get parametrs in uri

[CAMEL-17768](https://issues.apache.org/jira/browse/CAMEL-17768)

Camel-cm-sms: Handle changed error message correctly

[CAMEL-17767](https://issues.apache.org/jira/browse/CAMEL-17767)

camel-csv - Empty header uri parameter interpreted as fixed column ""

[CAMEL-17764](https://issues.apache.org/jira/browse/CAMEL-17764)

Camel-quartz: endpoint enriches job detail with wrong type of data (should be String)

[CAMEL-17761](https://issues.apache.org/jira/browse/CAMEL-17761)

camel-test-infra: unable to define a custom Cassandra container

[CAMEL-17751](https://issues.apache.org/jira/browse/CAMEL-17751)

camel-saga - LRASagaService does not proceed to completion or compensation routes

[CAMEL-17738](https://issues.apache.org/jira/browse/CAMEL-17738)

camel-spring-boot - Cannot load resources from nested jar inside spring boot fat jar

[CAMEL-17730](https://issues.apache.org/jira/browse/CAMEL-17730)

Camel-AWS Secret Manager Properties Source: if the subkey contains a default value the actual won't substitute correctly the secret

[CAMEL-17704](https://issues.apache.org/jira/browse/CAMEL-17704)

camel-netty-starter - Unable to set camel.component.netty.decoders

[CAMEL-17702](https://issues.apache.org/jira/browse/CAMEL-17702)

\[camel-google-storage\] Payload type File causes NPE on consumer

[CAMEL-17658](https://issues.apache.org/jira/browse/CAMEL-17658)

camel-core - Configuring endpoint Map options with keys with dots have trimmed keys

[CAMEL-17655](https://issues.apache.org/jira/browse/CAMEL-17655)

OpenTracing throw NPE using onCompletion definition

[CAMEL-17651](https://issues.apache.org/jira/browse/CAMEL-17651)

RouteWatcherReloadStrategy crashes on Windows or if pattern is not specified

[CAMEL-17618](https://issues.apache.org/jira/browse/CAMEL-17618)

camel-ref: only add the endpoint into camelContext when not exist

[CAMEL-17609](https://issues.apache.org/jira/browse/CAMEL-17609)

camel-core - Problem with transacted routes

[CAMEL-17602](https://issues.apache.org/jira/browse/CAMEL-17602)

camel-aws2-sqs - Camel converts Number.Boolean messageAttribute into string "1" or "0" instead of Boolean

[CAMEL-17599](https://issues.apache.org/jira/browse/CAMEL-17599)

camel-jdbc - JdbcProducer leaks PreparedStatement

[CAMEL-17594](https://issues.apache.org/jira/browse/CAMEL-17594)

Try Catch WireTap OnPrepare ClassCastException

[CAMEL-17592](https://issues.apache.org/jira/browse/CAMEL-17592)

concurrentConsumers URI parameter not working with aws2-sqs endpoint

[CAMEL-17591](https://issues.apache.org/jira/browse/CAMEL-17591)

OgnlHelper problem after merge

[CAMEL-17579](https://issues.apache.org/jira/browse/CAMEL-17579)

camel-core - Message DataType lost on exchange copy

[CAMEL-17577](https://issues.apache.org/jira/browse/CAMEL-17577)

Greedy flag causing consumer health check to fail

[CAMEL-17570](https://issues.apache.org/jira/browse/CAMEL-17570)

camel-maven-plugin - mvn camel:run -Dcamel.logLevel=DEBUG

[CAMEL-17565](https://issues.apache.org/jira/browse/CAMEL-17565)

camel-jms - JmsBinding not closing the InputStream

[CAMEL-17558](https://issues.apache.org/jira/browse/CAMEL-17558)

camel-salesforce: don't complain about missing credentials with lazy login

[CAMEL-17554](https://issues.apache.org/jira/browse/CAMEL-17554)

camel-quickfix - lazy-create-engines option is not working

[CAMEL-17535](https://issues.apache.org/jira/browse/CAMEL-17535)

camel-example-spring-boot-rest-openapi-springdoc generates incorrect api doc

[CAMEL-17474](https://issues.apache.org/jira/browse/CAMEL-17474)

camel-core: deadlock with multicast in a transacted context

### Dependency upgrade (9)

[CAMEL-17827](https://issues.apache.org/jira/browse/CAMEL-17827)

Upgrade to MongoDB Driver Core 4.5.0

[CAMEL-17822](https://issues.apache.org/jira/browse/CAMEL-17822)

maven wrapper - Upgrade to maven 3.8.5

[CAMEL-17757](https://issues.apache.org/jira/browse/CAMEL-17757)

camel-hbase - Upgrade to 2.4.10

[CAMEL-17756](https://issues.apache.org/jira/browse/CAMEL-17756)

camel-tika - Upgrade to tika 2.x

[CAMEL-17748](https://issues.apache.org/jira/browse/CAMEL-17748)

camel-any23 - Upgrade to 2.7

[CAMEL-17715](https://issues.apache.org/jira/browse/CAMEL-17715)

upgrade to spring boot 2.6.4 and 2.5.10

[CAMEL-17630](https://issues.apache.org/jira/browse/CAMEL-17630)

camel-microprofile - Update to newer releases

[CAMEL-17603](https://issues.apache.org/jira/browse/CAMEL-17603)

camel-karaf - Upgrade Aries Blueprint

[CAMEL-17573](https://issues.apache.org/jira/browse/CAMEL-17573)

Upgrade HuaweiCloud SDK version to 3.0.76 & Fix some code issues

### Improvement (73)

[CAMEL-17836](https://issues.apache.org/jira/browse/CAMEL-17836)

camel-core - PropertiesSource should support ordering

[CAMEL-17824](https://issues.apache.org/jira/browse/CAMEL-17824)

camel-platform-http - Exchange exception causes always 500 error

[CAMEL-17817](https://issues.apache.org/jira/browse/CAMEL-17817)

camel-jbang: Trait configuration for health

[CAMEL-17815](https://issues.apache.org/jira/browse/CAMEL-17815)

camel-jbang - Modeline properties as initial properties so they can configure via camel-main

[CAMEL-17812](https://issues.apache.org/jira/browse/CAMEL-17812)

camel-mail - MaxMessagesPerPoll / FetchSize should ignore unfetchable mails

[CAMEL-17811](https://issues.apache.org/jira/browse/CAMEL-17811)

documentation - Explain better the difference between kamelet eip vs to kamelet

[CAMEL-17809](https://issues.apache.org/jira/browse/CAMEL-17809)

camel-vertx - Should have type converter from buffer to stream cache

[CAMEL-17793](https://issues.apache.org/jira/browse/CAMEL-17793)

camel-core - Processor ref should support # syntax

[CAMEL-17789](https://issues.apache.org/jira/browse/CAMEL-17789)

camel-fhir: Update FHIR dataformat metadata for fhirVersion option

[CAMEL-17788](https://issues.apache.org/jira/browse/CAMEL-17788)

camel-fhir: Support FHIR versions DSTU2\_HL7ORG & DSTU2\_1

[CAMEL-17787](https://issues.apache.org/jira/browse/CAMEL-17787)

camel-microprofile-health: Take health exposure level configuration into consideration

[CAMEL-17781](https://issues.apache.org/jira/browse/CAMEL-17781)

camel-jbang - List of known DSLs

[CAMEL-17774](https://issues.apache.org/jira/browse/CAMEL-17774)

ZipIterator can have null ZipInputStream

[CAMEL-17769](https://issues.apache.org/jira/browse/CAMEL-17769)

AWS Kinesis: Make the consumer set only the raw data on the body, and enrich the exchange with more header

[CAMEL-17755](https://issues.apache.org/jira/browse/CAMEL-17755)

camel-core - DoSwitch can be Choice with precondition set

[CAMEL-17750](https://issues.apache.org/jira/browse/CAMEL-17750)

Optimize implementation of HuaweiCloud FaceRecognition Service component

[CAMEL-17749](https://issues.apache.org/jira/browse/CAMEL-17749)

camel-health - Allow to enabled/disable custom health checks from camel-main configuration

[CAMEL-17739](https://issues.apache.org/jira/browse/CAMEL-17739)

Camel Google Secret Manager Properties Source: Support the usage of client default instance

[CAMEL-17732](https://issues.apache.org/jira/browse/CAMEL-17732)

Secrets Manager Properties Sources: if default value is provided, we should not fail with wrong credentials

[CAMEL-17720](https://issues.apache.org/jira/browse/CAMEL-17720)

camel-jackson - Add option to allow jackson to support null body

[CAMEL-17718](https://issues.apache.org/jira/browse/CAMEL-17718)

REST DSL RestSecuritiesDefinition cleanup

[CAMEL-17717](https://issues.apache.org/jira/browse/CAMEL-17717)

REST DSL securityRequirements cleanup

[CAMEL-17713](https://issues.apache.org/jira/browse/CAMEL-17713)

CAMEL-AWS2-S3 doesn't support uploading files with custom metadata headers

[CAMEL-17711](https://issues.apache.org/jira/browse/CAMEL-17711)

camel-jbang - Running Camel K integration to support spec/sources

[CAMEL-17708](https://issues.apache.org/jira/browse/CAMEL-17708)

camel-base-engine - Add ability to override BasePackageScanResolver initialization logic

[CAMEL-17707](https://issues.apache.org/jira/browse/CAMEL-17707)

Camel AWS Secrets Manager Properties Source: Fallback to default credential provider chain, if env vars or application properties not provided - Spring Boot Support

[CAMEL-17701](https://issues.apache.org/jira/browse/CAMEL-17701)

camel-core-model - Add labels to EIP options

[CAMEL-17700](https://issues.apache.org/jira/browse/CAMEL-17700)

AWS Secret Manager Properties Source: Provide a fallback default value

[CAMEL-17695](https://issues.apache.org/jira/browse/CAMEL-17695)

Camel AWS Secrets Manager Properties Source: Fallback to default credential provider chain, if env vars or application properties not provided

[CAMEL-17694](https://issues.apache.org/jira/browse/CAMEL-17694)

camel-vertx-websocket: Improve handling of SEND\_TO\_ALL header

[CAMEL-17683](https://issues.apache.org/jira/browse/CAMEL-17683)

Modify document of HuaweiCloud Face Recognition Service (FRS) Component and add some test cases

[CAMEL-17682](https://issues.apache.org/jira/browse/CAMEL-17682)

camel-archetype-main - Use the new test-main module

[CAMEL-17681](https://issues.apache.org/jira/browse/CAMEL-17681)

camel-stream - Should append new line to output in producer

[CAMEL-17675](https://issues.apache.org/jira/browse/CAMEL-17675)

Rest DSL - Removed inlined routes

[CAMEL-17673](https://issues.apache.org/jira/browse/CAMEL-17673)

camel-core-model - Rest DSL model cleanup

[CAMEL-17672](https://issues.apache.org/jira/browse/CAMEL-17672)

camel-main: Prevent superfluous warning - Cannot find HealthCheckRegistry from classpath

[CAMEL-17668](https://issues.apache.org/jira/browse/CAMEL-17668)

camel-core - WireTap - Remove function to tap as new body/header

[CAMEL-17664](https://issues.apache.org/jira/browse/CAMEL-17664)

REST model filenames in camel-catalog

[CAMEL-17662](https://issues.apache.org/jira/browse/CAMEL-17662)

REST DSL without restConfiguration fails with camel-jbang

[CAMEL-17660](https://issues.apache.org/jira/browse/CAMEL-17660)

camel-core - Error handler OnRedeliveryProcessor should be able to control to stop routing

[CAMEL-17656](https://issues.apache.org/jira/browse/CAMEL-17656)

camel-main - Add start and stop logging with app name and version

[CAMEL-17650](https://issues.apache.org/jira/browse/CAMEL-17650)

camel-vertx-websocket: sendToAll operation should consider the path WebSocket clients are connected to

[CAMEL-17646](https://issues.apache.org/jira/browse/CAMEL-17646)

camel-vertx-websocket - Server exception handler should check for cause ConnectionBase.CLOSED\_EXCEPTION

[CAMEL-17645](https://issues.apache.org/jira/browse/CAMEL-17645)

camel-jbang - Reload on modeline changes

[CAMEL-17640](https://issues.apache.org/jira/browse/CAMEL-17640)

camel-jbang: Add support for Integration spec:dependencies

[CAMEL-17639](https://issues.apache.org/jira/browse/CAMEL-17639)

camel-yaml-dsl - Add support for spec/dependencies

[CAMEL-17638](https://issues.apache.org/jira/browse/CAMEL-17638)

camel-core - EIP model options with old fashioned naming xxxRef style should be made modern style

[CAMEL-17629](https://issues.apache.org/jira/browse/CAMEL-17629)

camel-health - Context should always be enabled

[CAMEL-17617](https://issues.apache.org/jira/browse/CAMEL-17617)

camel-jbang - Specify minimal Java version in Jbang script

[CAMEL-17616](https://issues.apache.org/jira/browse/CAMEL-17616)

JdbcAggregationRepository will not start if it contains too many exchanges

[CAMEL-17611](https://issues.apache.org/jira/browse/CAMEL-17611)

Allow to create a Route from a route template in XML and YAML

[CAMEL-17610](https://issues.apache.org/jira/browse/CAMEL-17610)

camel-aws2-ses: Support CC and BCC as endpoint parameters

[CAMEL-17608](https://issues.apache.org/jira/browse/CAMEL-17608)

camel-salesforce: allow overriding sobject name when using DTOs

[CAMEL-17606](https://issues.apache.org/jira/browse/CAMEL-17606)

camel-core - Endpoint DSL - fluent builder to refer to property placeholder

[CAMEL-17593](https://issues.apache.org/jira/browse/CAMEL-17593)

camel-aws2-sqs - Camel skips messageAttributes if more then 10 without any info

[CAMEL-17587](https://issues.apache.org/jira/browse/CAMEL-17587)

camel-core - Make Health Check API simpler

[CAMEL-17585](https://issues.apache.org/jira/browse/CAMEL-17585)

camel-core-model - SagaOptionDefinition model metadata

[CAMEL-17583](https://issues.apache.org/jira/browse/CAMEL-17583)

camel-jbang - Reload properties component

[CAMEL-17581](https://issues.apache.org/jira/browse/CAMEL-17581)

camel-core - Add unbind method to Registry

[CAMEL-17580](https://issues.apache.org/jira/browse/CAMEL-17580)

camel-core - Make it possible to use CamelConfiguration outside camel-main

[CAMEL-17578](https://issues.apache.org/jira/browse/CAMEL-17578)

camel-core - Adding @Converter class should be easier programmatically

[CAMEL-17576](https://issues.apache.org/jira/browse/CAMEL-17576)

camel-core-model - Any23DataFormat baseUri attribute sync over DSLs

[CAMEL-17575](https://issues.apache.org/jira/browse/CAMEL-17575)

camel-examples - Update main example to use base package scanning

[CAMEL-17568](https://issues.apache.org/jira/browse/CAMEL-17568)

camel-core - TypeConverterExists change default to ignore

[CAMEL-17564](https://issues.apache.org/jira/browse/CAMEL-17564)

Add authSource connection parameter to MongoDB component

[CAMEL-17563](https://issues.apache.org/jira/browse/CAMEL-17563)

wireTap doesn't deep copy attachments

[CAMEL-17551](https://issues.apache.org/jira/browse/CAMEL-17551)

camel-pulsar: Pause Pulsar consumers when a Pulsar route is suspended

[CAMEL-17543](https://issues.apache.org/jira/browse/CAMEL-17543)

Camel Azure Eventhubs: Support adding properties to the Event mapped from Camel Header

[CAMEL-17308](https://issues.apache.org/jira/browse/CAMEL-17308)

camel-yaml-dsl: REST

[CAMEL-17293](https://issues.apache.org/jira/browse/CAMEL-17293)

camel-jbang: Add support for Integration configuration

[CAMEL-17292](https://issues.apache.org/jira/browse/CAMEL-17292)

camel-jbang: Add support for modeline

[CAMEL-17117](https://issues.apache.org/jira/browse/CAMEL-17117)

eip - Add Resume from Offset as an EIP to the docs

[CAMEL-16873](https://issues.apache.org/jira/browse/CAMEL-16873)

Route template parameter are not replaced when dumpRoutesAsXML

### New Feature (29)

[CAMEL-17826](https://issues.apache.org/jira/browse/CAMEL-17826)

camel-platform-http - Add muteException option and enable it by default

[CAMEL-17796](https://issues.apache.org/jira/browse/CAMEL-17796)

camel-core - SPI annotations for message headers to include in/out direction

[CAMEL-17754](https://issues.apache.org/jira/browse/CAMEL-17754)

camel-core - precondition to hard exclude route configurations

[CAMEL-17727](https://issues.apache.org/jira/browse/CAMEL-17727)

camel-kafka: add producer/consumer readiness checks

[CAMEL-17726](https://issues.apache.org/jira/browse/CAMEL-17726)

route controller: allow to mark a route as failed

[CAMEL-17706](https://issues.apache.org/jira/browse/CAMEL-17706)

camel-azure-servicebus: Add fullyQualifiedNamespace and tokenCredential to Azure ServiceBus component

[CAMEL-17693](https://issues.apache.org/jira/browse/CAMEL-17693)

Create a Camel Google Secret Manager Spring Boot Starter

[CAMEL-17691](https://issues.apache.org/jira/browse/CAMEL-17691)

Camel Google Secrets Manager: Support more operations

[CAMEL-17690](https://issues.apache.org/jira/browse/CAMEL-17690)

camel-test-main - Annotation based testing

[CAMEL-17685](https://issues.apache.org/jira/browse/CAMEL-17685)

Create a Camel Google Secrets Manager component

[CAMEL-17678](https://issues.apache.org/jira/browse/CAMEL-17678)

camel-jbang - Run without logging to console

[CAMEL-17663](https://issues.apache.org/jira/browse/CAMEL-17663)

camel-vertx-http - Should be RestProducer so it can be used in rest-dsl

[CAMEL-17654](https://issues.apache.org/jira/browse/CAMEL-17654)

camel-debug - Make it possible to do remote JMX RMI debugging

[CAMEL-17647](https://issues.apache.org/jira/browse/CAMEL-17647)

camel-core - Properties component should support pluggable functions

[CAMEL-17643](https://issues.apache.org/jira/browse/CAMEL-17643)

camel-jbang - Add support for github download dependency

[CAMEL-17642](https://issues.apache.org/jira/browse/CAMEL-17642)

camel-jbang: Add support for Kamelet spec:dependencies

[CAMEL-17637](https://issues.apache.org/jira/browse/CAMEL-17637)

camel-jbang - Add CLI option to add dependency from command args

[CAMEL-17636](https://issues.apache.org/jira/browse/CAMEL-17636)

camel-jbang - Auto download of JDBC drivers from beans configurations

[CAMEL-17633](https://issues.apache.org/jira/browse/CAMEL-17633)

Support JUnit 5 for Camel CDI

[CAMEL-17627](https://issues.apache.org/jira/browse/CAMEL-17627)

camel-health - Option for single output reponse

[CAMEL-17626](https://issues.apache.org/jira/browse/CAMEL-17626)

camel-health - SPI to plugin custom manipulation of health check

[CAMEL-17574](https://issues.apache.org/jira/browse/CAMEL-17574)

camel-test-main - Test module for camel-main applications

[CAMEL-17571](https://issues.apache.org/jira/browse/CAMEL-17571)

camel-main - Allow to bean inject beans from @Inject and other similar annotations

[CAMEL-17569](https://issues.apache.org/jira/browse/CAMEL-17569)

camel-jbang - Base package scan support

[CAMEL-17567](https://issues.apache.org/jira/browse/CAMEL-17567)

camel-main - add support for base package scanning

[CAMEL-17555](https://issues.apache.org/jira/browse/CAMEL-17555)

camel-core - Flag to include/exclude routes in route templates

[CAMEL-17334](https://issues.apache.org/jira/browse/CAMEL-17334)

camel-core - Routes loader - Add option to keep copy of loaded resource

[CAMEL-16628](https://issues.apache.org/jira/browse/CAMEL-16628)

camel-core - SPI annotations for message headers

[CAMEL-15562](https://issues.apache.org/jira/browse/CAMEL-15562)

repository & strategy to store and retrieve the latest state of a consumer and allow to resume upon restart

### Sub-task (1)

[CAMEL-17684](https://issues.apache.org/jira/browse/CAMEL-17684)

Support ability to load properties from Vault/Secrets cloud services - GCP Secrets Manager

### Task (35)

[CAMEL-17828](https://issues.apache.org/jira/browse/CAMEL-17828)

Remove Camel-MongoDB features from Camel-Karaf

[CAMEL-17795](https://issues.apache.org/jira/browse/CAMEL-17795)

camel-salesforce: add JAXB implementation

[CAMEL-17779](https://issues.apache.org/jira/browse/CAMEL-17779)

camel-elasticsearch-rest - Deprecate due to change of license

[CAMEL-17759](https://issues.apache.org/jira/browse/CAMEL-17759)

Console excluded from the catalog due to parallel build

[CAMEL-17752](https://issues.apache.org/jira/browse/CAMEL-17752)

camel-debug - Split packages warn by quarkus

[CAMEL-17745](https://issues.apache.org/jira/browse/CAMEL-17745)

camel-spring-boot - AutoConfigurations models aren't updated

[CAMEL-17743](https://issues.apache.org/jira/browse/CAMEL-17743)

camel-spring-boot - Schema generation fails for Resilience4jConfigurationCommon

[CAMEL-17741](https://issues.apache.org/jira/browse/CAMEL-17741)

camel-yaml-dsl - Improper way to get the default name of a field annotated with XmlElement

[CAMEL-17734](https://issues.apache.org/jira/browse/CAMEL-17734)

camel-jbang - Cannot load kamelets

[CAMEL-17733](https://issues.apache.org/jira/browse/CAMEL-17733)

camel-resume-api: create a delegating strategy

[CAMEL-17728](https://issues.apache.org/jira/browse/CAMEL-17728)

Camel-quartz: It is not possible to use "startDelayedSeconds" property as is in the documentation

[CAMEL-17698](https://issues.apache.org/jira/browse/CAMEL-17698)

Inconsistency in naming parts of camel-google-secrets-manager

[CAMEL-17692](https://issues.apache.org/jira/browse/CAMEL-17692)

camel-xmpp: component is depending on camel-testcontainers

[CAMEL-17680](https://issues.apache.org/jira/browse/CAMEL-17680)

camel-micrometer: documentation contain references to the metrics component

[CAMEL-17679](https://issues.apache.org/jira/browse/CAMEL-17679)

camel-micrometer: gauge is reported as invalid

[CAMEL-17667](https://issues.apache.org/jira/browse/CAMEL-17667)

camel-ahc - Deprecate component

[CAMEL-17666](https://issues.apache.org/jira/browse/CAMEL-17666)

camel-package-maven-plugin - Spring Boot source generator affected

[CAMEL-17665](https://issues.apache.org/jira/browse/CAMEL-17665)

camel-package-maven-plugin - False WARN about missing doc

[CAMEL-17631](https://issues.apache.org/jira/browse/CAMEL-17631)

camel-component-maven-plugin - Should generate for InvokeOnHeader

[CAMEL-17625](https://issues.apache.org/jira/browse/CAMEL-17625)

Replace deprecated test container components with test-infra

[CAMEL-17624](https://issues.apache.org/jira/browse/CAMEL-17624)

camel-testcontainers-spring-junit5: deprecate component

[CAMEL-17623](https://issues.apache.org/jira/browse/CAMEL-17623)

camel-testcontainers-spring: deprecate component

[CAMEL-17622](https://issues.apache.org/jira/browse/CAMEL-17622)

camel-testcontainers-junit5: deprecate component

[CAMEL-17621](https://issues.apache.org/jira/browse/CAMEL-17621)

camel-testcontainers: deprecate component

[CAMEL-17619](https://issues.apache.org/jira/browse/CAMEL-17619)

Remove the superfluous json-simple dependency from the Slack component

[CAMEL-17614](https://issues.apache.org/jira/browse/CAMEL-17614)

Be able to run infinispan spring-boot example out of the box

[CAMEL-17612](https://issues.apache.org/jira/browse/CAMEL-17612)

camel google functions documentation shows consumer example instead of producer

[CAMEL-17607](https://issues.apache.org/jira/browse/CAMEL-17607)

Using JDK new Files.list - Close stream to avoid leak

[CAMEL-17605](https://issues.apache.org/jira/browse/CAMEL-17605)

camel-jbang - Remove deprecated alias

[CAMEL-17596](https://issues.apache.org/jira/browse/CAMEL-17596)

camel-examples: Broken (main-xxx) examples relying on MainConfigurationProperties

[CAMEL-17584](https://issues.apache.org/jira/browse/CAMEL-17584)

camel-spring-boot-examples:xml and xml-import examples are broken

[CAMEL-17325](https://issues.apache.org/jira/browse/CAMEL-17325)

camel-jbang - User simpler logging from slf4j as logger

[CAMEL-17320](https://issues.apache.org/jira/browse/CAMEL-17320)

camel-maven-plugin - Maven warn about scope of dependencies

[CAMEL-17186](https://issues.apache.org/jira/browse/CAMEL-17186)

camel-aws2-kinesis: add support for resume strategies

[CAMEL-16387](https://issues.apache.org/jira/browse/CAMEL-16387)

camel-hdfs: AppendTest fails with Stream closed on Mac

### Test (27)

[CAMEL-17834](https://issues.apache.org/jira/browse/CAMEL-17834)

camel-spring-boot - Some itests are failing

[CAMEL-17807](https://issues.apache.org/jira/browse/CAMEL-17807)

add tests in camel-jaxb-starter

[CAMEL-17804](https://issues.apache.org/jira/browse/CAMEL-17804)

add tests in camel-jacksonxml-starter

[CAMEL-17801](https://issues.apache.org/jira/browse/CAMEL-17801)

add tests in camel-mongodb-starter

[CAMEL-17800](https://issues.apache.org/jira/browse/CAMEL-17800)

add tests in camel-sql-starter

[CAMEL-17797](https://issues.apache.org/jira/browse/CAMEL-17797)

camel-fhir: Test with FHIR version R4

[CAMEL-17794](https://issues.apache.org/jira/browse/CAMEL-17794)

add tests in camel-saxon-starter

[CAMEL-17791](https://issues.apache.org/jira/browse/CAMEL-17791)

add tests in camel-openapi-starter

[CAMEL-17778](https://issues.apache.org/jira/browse/CAMEL-17778)

add tests in camel-soap-starter

[CAMEL-17777](https://issues.apache.org/jira/browse/CAMEL-17777)

add tests in camel-webhook-starter

[CAMEL-17770](https://issues.apache.org/jira/browse/CAMEL-17770)

add tests in camel-telegram-starter

[CAMEL-17766](https://issues.apache.org/jira/browse/CAMEL-17766)

add tests in camel-slack-starter

[CAMEL-17758](https://issues.apache.org/jira/browse/CAMEL-17758)

add tests in camel-cassandraql-starter

[CAMEL-17747](https://issues.apache.org/jira/browse/CAMEL-17747)

add tests in camel-cron-starter

[CAMEL-17746](https://issues.apache.org/jira/browse/CAMEL-17746)

add tests in camel-gson-starter

[CAMEL-17742](https://issues.apache.org/jira/browse/CAMEL-17742)

Camel-quartz: fix and enable SpringQuartzPersistentStoreRestartAppChangeOptionsTest

[CAMEL-17740](https://issues.apache.org/jira/browse/CAMEL-17740)

add tests in camel-platform-http-starter

[CAMEL-17736](https://issues.apache.org/jira/browse/CAMEL-17736)

add tests in camel-jackson-protobuf-starter

[CAMEL-17735](https://issues.apache.org/jira/browse/CAMEL-17735)

add tests in camel-jackson-avro-starter

[CAMEL-17729](https://issues.apache.org/jira/browse/CAMEL-17729)

add tests in camel-jsonpath-starter

[CAMEL-17725](https://issues.apache.org/jira/browse/CAMEL-17725)

add tests in camel-fhir-starter

[CAMEL-17703](https://issues.apache.org/jira/browse/CAMEL-17703)

add tests in camel-hl7-starter

[CAMEL-17696](https://issues.apache.org/jira/browse/CAMEL-17696)

add tests in camel-jackson-starter

[CAMEL-17677](https://issues.apache.org/jira/browse/CAMEL-17677)

add tests in camel-jira-starter

[CAMEL-17661](https://issues.apache.org/jira/browse/CAMEL-17661)

add tests in camel-avro-starter

[CAMEL-17597](https://issues.apache.org/jira/browse/CAMEL-17597)

Enable camel-zookeeper-master : GroupTest on mac

[CAMEL-17589](https://issues.apache.org/jira/browse/CAMEL-17589)

Enable ITests of camel-infinispan on MacOSX

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).