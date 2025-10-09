# Apache camel 3.18.0 Release

## New and Noteworthy

This release is the new Camel 3.18.0 LTS release.

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
      <version>3.18.0</version>
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
      <version>3.18.0</version>
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
| [apache-camel-3.18.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.0/apache-camel-3.18.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.0/apache-camel-3.18.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.0/apache-camel-3.18.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-18253](https://issues.apache.org/jira/browse/CAMEL-18253)

camel-kafka: idempotent repository may report incorrect number of messages

[CAMEL-18252](https://issues.apache.org/jira/browse/CAMEL-18252)

BridgeExceptionHandlerToErrorHandler with OnCompletion prevents processing Exception

[CAMEL-18250](https://issues.apache.org/jira/browse/CAMEL-18250)

When a Call to Salesforce timeouts then we have Exchange.HTTP\_RESPONSE\_CODE Exchange Header set as "0"

[CAMEL-18232](https://issues.apache.org/jira/browse/CAMEL-18232)

camel-core - Invalid ThreadName pattern

[CAMEL-18218](https://issues.apache.org/jira/browse/CAMEL-18218)

camel-jira: components field is not updated

[CAMEL-18210](https://issues.apache.org/jira/browse/CAMEL-18210)

camel-core - Pooled exchanges in batch consumer may use an exchange concurrently

[CAMEL-18202](https://issues.apache.org/jira/browse/CAMEL-18202)

camel-mongodb-gridfs - initial delay is not configured correctly

[CAMEL-18187](https://issues.apache.org/jira/browse/CAMEL-18187)

slack: inconsistent message payload when batch ends

[CAMEL-18185](https://issues.apache.org/jira/browse/CAMEL-18185)

slack: npe when processing batch messages

[CAMEL-18160](https://issues.apache.org/jira/browse/CAMEL-18160)

The typeConverterExists attribute in camel-spring-xml has no effect

[CAMEL-18159](https://issues.apache.org/jira/browse/CAMEL-18159)

camel-jms SendDynamicAware incorrectly parses destination if it starts with "jms|activemq|etc://" and doesn't have queue: or topic: prefix

[CAMEL-18157](https://issues.apache.org/jira/browse/CAMEL-18157)

camel-jdbc - The settings provided by the query parameter "parameters" are ignored when useHeadersAsParameters

[CAMEL-18146](https://issues.apache.org/jira/browse/CAMEL-18146)

camel-kafka - ssl.endpoint.identification.algorithm should be allowed to be an empty string

[CAMEL-18139](https://issues.apache.org/jira/browse/CAMEL-18139)

camel-jbang - Run from clipboard does not work for java

[CAMEL-18137](https://issues.apache.org/jira/browse/CAMEL-18137)

camel-mongodb - Cannot upsert in sharded collection

[CAMEL-18130](https://issues.apache.org/jira/browse/CAMEL-18130)

camel-ftp - Move-File Post Processing in (S)FTP not working if OutMessage is set

[CAMEL-18129](https://issues.apache.org/jira/browse/CAMEL-18129)

camel-quickfix - lazy-create-engines option is not working

[CAMEL-18123](https://issues.apache.org/jira/browse/CAMEL-18123)

Aws2-sqs: Operations PurgeQueue and DeleteQueue requires unnecessary header

[CAMEL-18119](https://issues.apache.org/jira/browse/CAMEL-18119)

Regression in 3.4 in date formatting of Simple expression

[CAMEL-18110](https://issues.apache.org/jira/browse/CAMEL-18110)

camel-smpp - DeliverSM handle message payload optional parameter

[CAMEL-18042](https://issues.apache.org/jira/browse/CAMEL-18042)

doCatch of a rollback only executes one line after doCatch and prune the rest of the route

[CAMEL-18039](https://issues.apache.org/jira/browse/CAMEL-18039)

endpoint-dsl - pollEnrich or file consumer polls file alphabetically despite specified fileName

[CAMEL-18027](https://issues.apache.org/jira/browse/CAMEL-18027)

camel-netty (producer) wrongly closes client channels

[CAMEL-17999](https://issues.apache.org/jira/browse/CAMEL-17999)

Simple Language: Invoke clone() method

[CAMEL-17949](https://issues.apache.org/jira/browse/CAMEL-17949)

camel-netty-http - Infinite loop when setting retries

[CAMEL-17925](https://issues.apache.org/jira/browse/CAMEL-17925)

camel-kafka: "breakOnFirstError" option is not respected

[CAMEL-17911](https://issues.apache.org/jira/browse/CAMEL-17911)

camel-olingo2 : I/O Dispatcher threads leak

[CAMEL-17723](https://issues.apache.org/jira/browse/CAMEL-17723)

camel-ssh - Dynamic Header is not resolved in pollCommand using endpoint-dsl

[CAMEL-17424](https://issues.apache.org/jira/browse/CAMEL-17424)

camel-kafka - Shutdown issues when attempting to consume from topic without authorization

### Dependency upgrade (8)

[CAMEL-18247](https://issues.apache.org/jira/browse/CAMEL-18247)

camel-test-infra - Upgrade to testcontainers 1.17.3

[CAMEL-18231](https://issues.apache.org/jira/browse/CAMEL-18231)

Upgrade Vert.x to 4.3.1

[CAMEL-18220](https://issues.apache.org/jira/browse/CAMEL-18220)

camel-jbang - Upgrade to quarkus camel 2.10.0

[CAMEL-18183](https://issues.apache.org/jira/browse/CAMEL-18183)

camel-karaf - Wrong definition in the camel-azure-storage-datalake feature

[CAMEL-18154](https://issues.apache.org/jira/browse/CAMEL-18154)

camel-kamelet-main - Capture all dependencies

[CAMEL-18153](https://issues.apache.org/jira/browse/CAMEL-18153)

camel-spring-boot - Upgrade to 2.7.x

[CAMEL-18144](https://issues.apache.org/jira/browse/CAMEL-18144)

camel-milo: Update Eclipse Milo from 0.3.7 to 0.6.6

[CAMEL-18122](https://issues.apache.org/jira/browse/CAMEL-18122)

bouncycastle - Upgrade to 1.71

### Improvement (52)

[CAMEL-18251](https://issues.apache.org/jira/browse/CAMEL-18251)

camel-jbang - Using microprofile-metrics should setup registry if none found

[CAMEL-18248](https://issues.apache.org/jira/browse/CAMEL-18248)

Provide ProducerTemplate as Injectable Bean for Camel Main test

[CAMEL-18245](https://issues.apache.org/jira/browse/CAMEL-18245)

camel-jbang - Using --console on mac have WARN log from Netty

[CAMEL-18237](https://issues.apache.org/jira/browse/CAMEL-18237)

camel-core - TimeUtils - Add method for reporting xxx Ago

[CAMEL-18233](https://issues.apache.org/jira/browse/CAMEL-18233)

camel-microprofile-config: CamelMicroProfilePropertiesSource loadProperties should handle NoSuchElementException

[CAMEL-18229](https://issues.apache.org/jira/browse/CAMEL-18229)

camel-maven-plugin - GenerateConfigurer to support builder pattern

[CAMEL-18228](https://issues.apache.org/jira/browse/CAMEL-18228)

camel-core - IntrospectionSupport isSetter for fluent builder interface returned

[CAMEL-18226](https://issues.apache.org/jira/browse/CAMEL-18226)

camel-core - Converter for InputStream to byte\[\] should close stream

[CAMEL-18224](https://issues.apache.org/jira/browse/CAMEL-18224)

camel-jbang - Auto download camel-kubernetes for configmap/secrets properties function

[CAMEL-18222](https://issues.apache.org/jira/browse/CAMEL-18222)

camel-kubernetes - KubernetesClient should be autowried

[CAMEL-18221](https://issues.apache.org/jira/browse/CAMEL-18221)

camel-rest-openapi: Support parsing OpenAPI documents in YAML

[CAMEL-18219](https://issues.apache.org/jira/browse/CAMEL-18219)

Enhance CamelTestSupport with a check to not run on quarkus

[CAMEL-18217](https://issues.apache.org/jira/browse/CAMEL-18217)

debugger - Allow to suspend messages

[CAMEL-18215](https://issues.apache.org/jira/browse/CAMEL-18215)

camel-test - Enable JMX when camel-debug is detected

[CAMEL-18214](https://issues.apache.org/jira/browse/CAMEL-18214)

Allow Backlog Debugger and test debugger to work at the same time

[CAMEL-18212](https://issues.apache.org/jira/browse/CAMEL-18212)

camel-reactive-streams: Throw a specific exception type when there are no active subscriptions

[CAMEL-18211](https://issues.apache.org/jira/browse/CAMEL-18211)

camel-bean: Make BeanInfo handle Quarkus Arc generated sub classes

[CAMEL-18209](https://issues.apache.org/jira/browse/CAMEL-18209)

endpoint lazyStartProducer should be labelled as advanced

[CAMEL-18207](https://issues.apache.org/jira/browse/CAMEL-18207)

camel-yaml-dsl - YAML Schema should be in schema sub folder

[CAMEL-18206](https://issues.apache.org/jira/browse/CAMEL-18206)

camel-catalog - Add API to check if an artifact exists with a given GAV

[CAMEL-18204](https://issues.apache.org/jira/browse/CAMEL-18204)

camel-jbang - Export to Spring Boot or Quarkus should lookup GAV in their specific catalogs

[CAMEL-18201](https://issues.apache.org/jira/browse/CAMEL-18201)

Enhance CamelTestSupport with an option to turn off stopping of the context

[CAMEL-18200](https://issues.apache.org/jira/browse/CAMEL-18200)

camel-core - Scheduled consumer should hide sensitive information if failed polling

[CAMEL-18199](https://issues.apache.org/jira/browse/CAMEL-18199)

camel-jbang. Dependencies management improvements for export

[CAMEL-18194](https://issues.apache.org/jira/browse/CAMEL-18194)

camel-jbang - Consolidate download helper to be setup once

[CAMEL-18193](https://issues.apache.org/jira/browse/CAMEL-18193)

camel-language - Language component should load resource from classpath by default

[CAMEL-18190](https://issues.apache.org/jira/browse/CAMEL-18190)

camel-jbang - Downloading dependencies - Did you mean

[CAMEL-18188](https://issues.apache.org/jira/browse/CAMEL-18188)

camel-jbang - Use apache maven to download JARs instead of groovy grape

[CAMEL-18175](https://issues.apache.org/jira/browse/CAMEL-18175)

camel-jbang - Download artifacts problem when they have custom classifier

[CAMEL-18173](https://issues.apache.org/jira/browse/CAMEL-18173)

camel-jbang - Add option to turn off download over the internet

[CAMEL-18172](https://issues.apache.org/jira/browse/CAMEL-18172)

camel-core - Eagerly resolve ref language when static to optimize

[CAMEL-18170](https://issues.apache.org/jira/browse/CAMEL-18170)

Add serviceAccountKey parameter to google components

[CAMEL-18167](https://issues.apache.org/jira/browse/CAMEL-18167)

aws2-s3 get a download link does not work in browser when checksum enabled

[CAMEL-18165](https://issues.apache.org/jira/browse/CAMEL-18165)

camel-jackson: split the uber type converter

[CAMEL-18150](https://issues.apache.org/jira/browse/CAMEL-18150)

camel-core - Events should include timestamp

[CAMEL-18141](https://issues.apache.org/jira/browse/CAMEL-18141)

camel-endpoint-dsl - Generate fluent builders for endpoint headers

[CAMEL-18117](https://issues.apache.org/jira/browse/CAMEL-18117)

camel-jbang - Package uber-jar should include application.properties if present

[CAMEL-18115](https://issues.apache.org/jira/browse/CAMEL-18115)

camel-jbang - Java DSL using Endpoint DSL

[CAMEL-18113](https://issues.apache.org/jira/browse/CAMEL-18113)

camel-ftp - Root cause exceptions "accidently" supressed in operations classes

[CAMEL-18092](https://issues.apache.org/jira/browse/CAMEL-18092)

Support reload with Camel JBang with files specified with a specific path

[CAMEL-18073](https://issues.apache.org/jira/browse/CAMEL-18073)

camel-jbang - Add openapi modeline

[CAMEL-18070](https://issues.apache.org/jira/browse/CAMEL-18070)

camel-core - Simple - Make it easy to check if property placeholder exists or not

[CAMEL-18045](https://issues.apache.org/jira/browse/CAMEL-18045)

camel-infinispan: Avoid usage of Protostuff marshaller

[CAMEL-18044](https://issues.apache.org/jira/browse/CAMEL-18044)

camel-infinispan: Avoid usage of JBossUserMarshaller in InfinispanRemoteAggregationRepository

[CAMEL-17966](https://issues.apache.org/jira/browse/CAMEL-17966)

YAML DSL Template in Kamelet definition

[CAMEL-17941](https://issues.apache.org/jira/browse/CAMEL-17941)

Dropbox: long-lived access tokens are retired, must use refresh token

[CAMEL-17848](https://issues.apache.org/jira/browse/CAMEL-17848)

camel-microprofile-health - Combined response for readiness or liveness should be different

[CAMEL-17100](https://issues.apache.org/jira/browse/CAMEL-17100)

Minio Consumer is really slow on listing initially if you have a lot of files

[CAMEL-14778](https://issues.apache.org/jira/browse/CAMEL-14778)

camel-cxf - Move Spring out into camel-cxf-spring

[CAMEL-14631](https://issues.apache.org/jira/browse/CAMEL-14631)

Support custom type converters for Enums

[CAMEL-9627](https://issues.apache.org/jira/browse/CAMEL-9627)

Splitup camel-cxf into modules so REST dont pull in old SOAP stuff

[CAMEL-7703](https://issues.apache.org/jira/browse/CAMEL-7703)

Introduce a dedicated camel-cxfrs module

### New Feature (17)

[CAMEL-18257](https://issues.apache.org/jira/browse/CAMEL-18257)

Camel-Hashicorp-vault: Support list secrets operation

[CAMEL-18223](https://issues.apache.org/jira/browse/CAMEL-18223)

camel-plugin - Propose a goal to debug with the textual route debugger

[CAMEL-18195](https://issues.apache.org/jira/browse/CAMEL-18195)

Add setExceptionListener(...) to SjmsComponent

[CAMEL-18184](https://issues.apache.org/jira/browse/CAMEL-18184)

camel-karaf - Support JUnit 5 for camel-test-blueprint

[CAMEL-18171](https://issues.apache.org/jira/browse/CAMEL-18171)

camel-kubernetes - Add configmap property placeholder function

[CAMEL-18166](https://issues.apache.org/jira/browse/CAMEL-18166)

camel-spring-boot - Route from LambdaEndpointRouteBuilder not starting

[CAMEL-18151](https://issues.apache.org/jira/browse/CAMEL-18151)

camel-jbang - Export to Quarkus and Spring Boot maven projects

[CAMEL-18149](https://issues.apache.org/jira/browse/CAMEL-18149)

camel-platform-http-console - A console using the platform http

[CAMEL-18125](https://issues.apache.org/jira/browse/CAMEL-18125)

camel-resume-api: improvements and additional support

[CAMEL-18124](https://issues.apache.org/jira/browse/CAMEL-18124)

camel-stream - stream:in to read entire content as byte\[\]

[CAMEL-18118](https://issues.apache.org/jira/browse/CAMEL-18118)

camel-jbang - Linux terminal scripting using pipes

[CAMEL-18099](https://issues.apache.org/jira/browse/CAMEL-18099)

Azure blob component does not support MS recommended auth. strategy

[CAMEL-18079](https://issues.apache.org/jira/browse/CAMEL-18079)

camel-jbang - Run to choose a specific Camel version

[CAMEL-17689](https://issues.apache.org/jira/browse/CAMEL-17689)

Create a Camel Hashicorp Vault Component

[CAMEL-17333](https://issues.apache.org/jira/browse/CAMEL-17333)

camel-jbang - Runtime statistics

[CAMEL-16834](https://issues.apache.org/jira/browse/CAMEL-16834)

camel-core - ErrorHandler as real model in camel-core-model

[CAMEL-14847](https://issues.apache.org/jira/browse/CAMEL-14847)

Create a camel-jq component

### Sub-task (2)

[CAMEL-18178](https://issues.apache.org/jira/browse/CAMEL-18178)

Create a Camel-hashicorp-vault spring boot starter

[CAMEL-18176](https://issues.apache.org/jira/browse/CAMEL-18176)

Create a camel-hashicorp-vault test-infra module

### Task (11)

[CAMEL-18249](https://issues.apache.org/jira/browse/CAMEL-18249)

camel-amqp: test log is missing

[CAMEL-18192](https://issues.apache.org/jira/browse/CAMEL-18192)

camel-jbang - Removed deprecated commands

[CAMEL-18174](https://issues.apache.org/jira/browse/CAMEL-18174)

camel-resume-api: allow intermittent offsets

[CAMEL-18136](https://issues.apache.org/jira/browse/CAMEL-18136)

osgi - improve Reproducible Build

[CAMEL-18135](https://issues.apache.org/jira/browse/CAMEL-18135)

camel-kafka: async manual commit is using sync commits and is broken

[CAMEL-18132](https://issues.apache.org/jira/browse/CAMEL-18132)

Some camel-examples fail with 3.17.0

[CAMEL-18128](https://issues.apache.org/jira/browse/CAMEL-18128)

camel-resume-api: resume endpoint self-configuration

[CAMEL-18127](https://issues.apache.org/jira/browse/CAMEL-18127)

camel-resume-api: adapter auto-configuration

[CAMEL-18126](https://issues.apache.org/jira/browse/CAMEL-18126)

camel-resume-api: investigate support with split EIP

[CAMEL-18116](https://issues.apache.org/jira/browse/CAMEL-18116)

camel-spring-boot-examples - twitter-salesforce - not working

[CAMEL-17814](https://issues.apache.org/jira/browse/CAMEL-17814)

camel-gson - Dataformat documentation doesn't cover all possible options

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).