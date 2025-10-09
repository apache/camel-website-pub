# Apache camel 3.4.0 Release

## New and Noteworthy

This release is the new Camel 3.4.0 LTS release.

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
      <version>3.4.0</version>
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
      <version>3.4.0</version>
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
| [apache-camel-3.4.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.4.0/apache-camel-3.4.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.4.0/apache-camel-3.4.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.4.0/apache-camel-3.4.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.4.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.4.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (41)

[CAMEL-15031](https://issues.apache.org/jira/browse/CAMEL-15031)

splunk-hec component only accepts local domains

[CAMEL-15027](https://issues.apache.org/jira/browse/CAMEL-15027)

KafkaEndpoint Sourced Headers are Overwritten By Default Propagation

[CAMEL-15025](https://issues.apache.org/jira/browse/CAMEL-15025)

camel-restdsl-openapi-plugin: fix 'modelWithXml' parameter propagation

[CAMEL-15017](https://issues.apache.org/jira/browse/CAMEL-15017)

Can't use custom scheduler in polling consumer

[CAMEL-15009](https://issues.apache.org/jira/browse/CAMEL-15009)

Use pooled connection incorrectly initialized in ActiveMQComponentConfiguration

[CAMEL-15003](https://issues.apache.org/jira/browse/CAMEL-15003)

PropertyBindingSupport fails for anonymous classes

[CAMEL-14999](https://issues.apache.org/jira/browse/CAMEL-14999)

Camel 3 log showCaughtException is not working

[CAMEL-14996](https://issues.apache.org/jira/browse/CAMEL-14996)

Stack overflow error during aggregation when using completionSize

[CAMEL-14988](https://issues.apache.org/jira/browse/CAMEL-14988)

camel-undertow-spring-security: test rewrites meta-inf/services which causes failures with built artifact

[CAMEL-14987](https://issues.apache.org/jira/browse/CAMEL-14987)

camel-undertow: if securityProvider is not present, but allowedRoles are not empty, access has to be denied

[CAMEL-14986](https://issues.apache.org/jira/browse/CAMEL-14986)

camel-undertow-spring-security: don't allow access to resource if no token is provided and add logging

[CAMEL-14984](https://issues.apache.org/jira/browse/CAMEL-14984)

Sqs2EndpointBuilder is not respecting delay - polling continuously

[CAMEL-14982](https://issues.apache.org/jira/browse/CAMEL-14982)

Endpoint DSL - File never consumed using delay

[CAMEL-14972](https://issues.apache.org/jira/browse/CAMEL-14972)

Enricher does not reset stream cache for aggregator

[CAMEL-14969](https://issues.apache.org/jira/browse/CAMEL-14969)

Failed to start route \[A\] because of duplicate id detected: \[B\]

[CAMEL-14965](https://issues.apache.org/jira/browse/CAMEL-14965)

camel-restdsl-openapi-plugin not working with yaml

[CAMEL-14960](https://issues.apache.org/jira/browse/CAMEL-14960)

Camel Karaf feature does reference wrong bundle

[CAMEL-14937](https://issues.apache.org/jira/browse/CAMEL-14937)

ExpressionBuilder.headerExpression("name", class) results in ClassNotFoundException

[CAMEL-14930](https://issues.apache.org/jira/browse/CAMEL-14930)

controlbus stats - JMX is disabled, cannot get stats

[CAMEL-14928](https://issues.apache.org/jira/browse/CAMEL-14928)

Unable to configure box component with configuration properties

[CAMEL-14922](https://issues.apache.org/jira/browse/CAMEL-14922)

Cannot enable cors on platform-http

[CAMEL-14921](https://issues.apache.org/jira/browse/CAMEL-14921)

PahoEndpointBuilder not working

[CAMEL-14915](https://issues.apache.org/jira/browse/CAMEL-14915)

Trying to create directory (FtpOperations.buildDirectory) without starting directory in ftps URI

[CAMEL-14914](https://issues.apache.org/jira/browse/CAMEL-14914)

camel-jackson: remove dependency on jackson-module-jaxb-annotations

[CAMEL-14895](https://issues.apache.org/jira/browse/CAMEL-14895)

Camel-Website: Build is broken

[CAMEL-14891](https://issues.apache.org/jira/browse/CAMEL-14891)

Race condition using toD

[CAMEL-14877](https://issues.apache.org/jira/browse/CAMEL-14877)

Camel-Osgi-Activator: tests are failing

[CAMEL-14870](https://issues.apache.org/jira/browse/CAMEL-14870)

camel-test - Disabling JMX is not working

[CAMEL-14865](https://issues.apache.org/jira/browse/CAMEL-14865)

camel-telegram - missing the direct dependency of com.fasterxml.jackson.core:jackson-core

[CAMEL-14861](https://issues.apache.org/jira/browse/CAMEL-14861)

NPE happens in google pubsub component

[CAMEL-14859](https://issues.apache.org/jira/browse/CAMEL-14859)

Endpoint DSL does create endpoints with different uri causing problems

[CAMEL-14853](https://issues.apache.org/jira/browse/CAMEL-14853)

camel-jacksonxml classpath conflict

[CAMEL-14852](https://issues.apache.org/jira/browse/CAMEL-14852)

Endpoint DSL does not support resolvePropertyPlaceholder anymore

[CAMEL-14842](https://issues.apache.org/jira/browse/CAMEL-14842)

no main manifest attribute, in camel-jasypt-3.0.1.jar

[CAMEL-14840](https://issues.apache.org/jira/browse/CAMEL-14840)

Wrong weld version in camel-spring-boot used in examples, forbidding to launch 2 examples

[CAMEL-14838](https://issues.apache.org/jira/browse/CAMEL-14838)

maven camel:run fails about OSGi blueprint for standalone mode

[CAMEL-14806](https://issues.apache.org/jira/browse/CAMEL-14806)

Property camel.springboot.java-routes-exclude-pattern not working correctly

[CAMEL-14744](https://issues.apache.org/jira/browse/CAMEL-14744)

camel-salesforce : lazy-login

[CAMEL-14737](https://issues.apache.org/jira/browse/CAMEL-14737)

Spring-boot closes datasource before the last inflight messages are processed

[CAMEL-14703](https://issues.apache.org/jira/browse/CAMEL-14703)

Salesforce report consumer throws IllegalArgumentException

[CAMEL-14643](https://issues.apache.org/jira/browse/CAMEL-14643)

Configuring brokerurl leads to duplication in camel-activemq and spring-boot

### Improvement (65)

[CAMEL-15034](https://issues.apache.org/jira/browse/CAMEL-15034)

SupervisingRouteController - Allow to easily filter routes

[CAMEL-15033](https://issues.apache.org/jira/browse/CAMEL-15033)

Create index.adoc tables using indexer in 2.x branch

[CAMEL-15032](https://issues.apache.org/jira/browse/CAMEL-15032)

SupervisingRouteController - Make it simpler and unify across runtimes

[CAMEL-15024](https://issues.apache.org/jira/browse/CAMEL-15024)

Add support for ZonedDateTime

[CAMEL-15023](https://issues.apache.org/jira/browse/CAMEL-15023)

camel-restdsl-openapi-plugin: pass configOptions to swagger-codegen-maven-plugin

[CAMEL-15020](https://issues.apache.org/jira/browse/CAMEL-15020)

Improve FAQ: Why is the exception null when I use onException?

[CAMEL-15019](https://issues.apache.org/jira/browse/CAMEL-15019)

Migrate Mongo GridFS component to 4.x driver

[CAMEL-15015](https://issues.apache.org/jira/browse/CAMEL-15015)

Endpoint DSL - Add support for RAW() style for setting data unencoded

[CAMEL-15013](https://issues.apache.org/jira/browse/CAMEL-15013)

Template components - Add option to turn on|off allow using header with override template

[CAMEL-15010](https://issues.apache.org/jira/browse/CAMEL-15010)

Upgrade to Shiro 1.5.3

[CAMEL-15008](https://issues.apache.org/jira/browse/CAMEL-15008)

camel-core - ReactiveExecutor should run scheduled tasks more fairly

[CAMEL-15007](https://issues.apache.org/jira/browse/CAMEL-15007)

camel-undertow-spring-security create example of usage

[CAMEL-15006](https://issues.apache.org/jira/browse/CAMEL-15006)

Allow to configure camel-main's properties locations using system properties and env vars

[CAMEL-15005](https://issues.apache.org/jira/browse/CAMEL-15005)

Move configurationClasses and routeBuilderClasses to MainConfigurationProperties

[CAMEL-15004](https://issues.apache.org/jira/browse/CAMEL-15004)

Make VertxPlatformHttpServer public

[CAMEL-15002](https://issues.apache.org/jira/browse/CAMEL-15002)

Add a callback to be able to configure the BaseMainSupport early

[CAMEL-15001](https://issues.apache.org/jira/browse/CAMEL-15001)

Support Metadata#excludeProperties for component properties

[CAMEL-14998](https://issues.apache.org/jira/browse/CAMEL-14998)

component docs - Mark newly added artifacts as preview support level by default

[CAMEL-14989](https://issues.apache.org/jira/browse/CAMEL-14989)

\[camel-mongodb\] Missing ObjectId converter

[CAMEL-14983](https://issues.apache.org/jira/browse/CAMEL-14983)

Replace commons Base64 for JDK Base64

[CAMEL-14977](https://issues.apache.org/jira/browse/CAMEL-14977)

Create camel-undertow-spring-security component to provide implementation of security provider for spring security

[CAMEL-14975](https://issues.apache.org/jira/browse/CAMEL-14975)

Move camel-k languages documentation to camel-k-runtime repository

[CAMEL-14968](https://issues.apache.org/jira/browse/CAMEL-14968)

Configurable shutdownAwaitTermination on Kafka Consumer Graceful Shutdown

[CAMEL-14967](https://issues.apache.org/jira/browse/CAMEL-14967)

Update webstie build to antora 2.3.0; camel-quarks version not needed

[CAMEL-14962](https://issues.apache.org/jira/browse/CAMEL-14962)

camel-undertow create starter for easier setup with spring-security 5

[CAMEL-14961](https://issues.apache.org/jira/browse/CAMEL-14961)

Handle matchOnUriPrefix URI param in camel-platform-http-vertx

[CAMEL-14955](https://issues.apache.org/jira/browse/CAMEL-14955)

camel-core - @PropertyInject with primitive types should be injected first

[CAMEL-14954](https://issues.apache.org/jira/browse/CAMEL-14954)

camel-undertow - Implement doSuspend/doResume to support suspension

[CAMEL-14951](https://issues.apache.org/jira/browse/CAMEL-14951)

WireTap - If thread pool reject task then Camel error handler should be able to react

[CAMEL-14950](https://issues.apache.org/jira/browse/CAMEL-14950)

camel-undertow: add an option to secure endpoints with spring-security 5 (with token bearer)

[CAMEL-14947](https://issues.apache.org/jira/browse/CAMEL-14947)

camel-sftp: check for existance of remote directory using ls is very slow

[CAMEL-14945](https://issues.apache.org/jira/browse/CAMEL-14945)

\[Camel-quarkus, website\] Move camel-quarkus-last-release attribute to component descriptor

[CAMEL-14940](https://issues.apache.org/jira/browse/CAMEL-14940)

Backport 'latest' component table generation to 3.2.x branch

[CAMEL-14938](https://issues.apache.org/jira/browse/CAMEL-14938)

Groovy expression file name customization for compiled classes

[CAMEL-14933](https://issues.apache.org/jira/browse/CAMEL-14933)

Remove dependencies on spring in GenerateConfigurerMojo

[CAMEL-14925](https://issues.apache.org/jira/browse/CAMEL-14925)

Add CORS support to VertxPlatformHttpServer

[CAMEL-14912](https://issues.apache.org/jira/browse/CAMEL-14912)

Azure components should allow custom service URIs

[CAMEL-14911](https://issues.apache.org/jira/browse/CAMEL-14911)

camel-core - JMX enabled/disabled - Only log when its enabled

[CAMEL-14893](https://issues.apache.org/jira/browse/CAMEL-14893)

camel-grpc - Should handle if exchange failed as onError

[CAMEL-14892](https://issues.apache.org/jira/browse/CAMEL-14892)

Camel-influxdb uses deprecated methods in doInsert action

[CAMEL-14885](https://issues.apache.org/jira/browse/CAMEL-14885)

camel-main - Configuration names preserve mixed case

[CAMEL-14883](https://issues.apache.org/jira/browse/CAMEL-14883)

Make CamelBeanPostProcessor implement Ordered

[CAMEL-14882](https://issues.apache.org/jira/browse/CAMEL-14882)

camel-main - Make configuring default thread pool profile settings easier

[CAMEL-14876](https://issues.apache.org/jira/browse/CAMEL-14876)

componentdsl - metadata.json generated unordered

[CAMEL-14872](https://issues.apache.org/jira/browse/CAMEL-14872)

Add Headers to camel-mongodb component for Change Stream operationType and \_id

[CAMEL-14860](https://issues.apache.org/jira/browse/CAMEL-14860)

Avoid reflection in circuit breaker reifiers

[CAMEL-14850](https://issues.apache.org/jira/browse/CAMEL-14850)

Camel-AWS2-\*: Improve the verifiers to check if a particular service works on a specified region

[CAMEL-14848](https://issues.apache.org/jira/browse/CAMEL-14848)

Attach Camel Blueprint Schema as artifact

[CAMEL-14845](https://issues.apache.org/jira/browse/CAMEL-14845)

camel-aws-s3 - CopyObject doesn't support ServerSideEncryption

[CAMEL-14843](https://issues.apache.org/jira/browse/CAMEL-14843)

Outdated documentation for camel-jetty Basic Authentication

[CAMEL-14837](https://issues.apache.org/jira/browse/CAMEL-14837)

rest-dsl - Configuring some extra options may use reflection

[CAMEL-14835](https://issues.apache.org/jira/browse/CAMEL-14835)

json dataformats should expose unmarshal and collection type in configurer

[CAMEL-14834](https://issues.apache.org/jira/browse/CAMEL-14834)

Dataformats are generated with wrong name in META-INF

[CAMEL-14833](https://issues.apache.org/jira/browse/CAMEL-14833)

camel-tika: enhance TikaProducer to use different tika parser instead of AutodetectParser

[CAMEL-14830](https://issues.apache.org/jira/browse/CAMEL-14830)

camel-rest - Avoid using JAXBContext

[CAMEL-14829](https://issues.apache.org/jira/browse/CAMEL-14829)

camel-api - Make ModelJAXBContextFactory generic without JAXB api

[CAMEL-14822](https://issues.apache.org/jira/browse/CAMEL-14822)

Make the CouchDB component work with CouchDB releases > 2.2

[CAMEL-14820](https://issues.apache.org/jira/browse/CAMEL-14820)

rest-dsl - Configuring JSon and JAXB additional properties uses reflection

[CAMEL-14812](https://issues.apache.org/jira/browse/CAMEL-14812)

camel-karaf - We should not maintain versions in its root pom.xml

[CAMEL-14763](https://issues.apache.org/jira/browse/CAMEL-14763)

Allow S3 Consumer to be configured to not return/delete "directories"

[CAMEL-14638](https://issues.apache.org/jira/browse/CAMEL-14638)

Inconsistent library versions notice.

[CAMEL-14626](https://issues.apache.org/jira/browse/CAMEL-14626)

api maven plugin - Cannot load <T> class

[CAMEL-14618](https://issues.apache.org/jira/browse/CAMEL-14618)

Camel-aws-s3: Add an option to consumer to be able to move the consumed files to another bucket

[CAMEL-14612](https://issues.apache.org/jira/browse/CAMEL-14612)

camel-json-validator - update version

[CAMEL-13535](https://issues.apache.org/jira/browse/CAMEL-13535)

Camel main - Allow to configure supervising route controller

### New Feature (8)

[CAMEL-14934](https://issues.apache.org/jira/browse/CAMEL-14934)

Improve Component, Language, Data format, etc. descriptions in Camel Catalog

[CAMEL-14932](https://issues.apache.org/jira/browse/CAMEL-14932)

Camel Splunk HEC component

[CAMEL-14867](https://issues.apache.org/jira/browse/CAMEL-14867)

camel-catalog - Add deprecatedSince information to camel-catalog

[CAMEL-14866](https://issues.apache.org/jira/browse/CAMEL-14866)

camel website - Show on component table the supportLevel

[CAMEL-14808](https://issues.apache.org/jira/browse/CAMEL-14808)

camel-djl (Deep Java Library component)

[CAMEL-14655](https://issues.apache.org/jira/browse/CAMEL-14655)

Create camel-azure-storage-queue component based on SDKv12

[CAMEL-14654](https://issues.apache.org/jira/browse/CAMEL-14654)

Create camel-azure-storage-blob component based on SDKv12

[CAMEL-14179](https://issues.apache.org/jira/browse/CAMEL-14179)

camel-microprofile-fault-tolerance - Add circuit break support

### Sub-task (10)

[CAMEL-14942](https://issues.apache.org/jira/browse/CAMEL-14942)

Add EIP to playbook for 3.2.x branch

[CAMEL-14941](https://issues.apache.org/jira/browse/CAMEL-14941)

back port index table fixes to 3.2.x branch (source fixes)

[CAMEL-14903](https://issues.apache.org/jira/browse/CAMEL-14903)

2.x branch

[CAMEL-14902](https://issues.apache.org/jira/browse/CAMEL-14902)

3.2.x branch

[CAMEL-14901](https://issues.apache.org/jira/browse/CAMEL-14901)

latest/master branch

[CAMEL-14900](https://issues.apache.org/jira/browse/CAMEL-14900)

CAMEL-14874 camel-karaf

[CAMEL-14899](https://issues.apache.org/jira/browse/CAMEL-14899)

CAMEL-14874 camel 2.x

[CAMEL-14898](https://issues.apache.org/jira/browse/CAMEL-14898)

CAMEL-14874 camel 3.2.x

[CAMEL-14897](https://issues.apache.org/jira/browse/CAMEL-14897)

CAMEL-14874 camel master

[CAMEL-14896](https://issues.apache.org/jira/browse/CAMEL-14896)

CAMEL-14874 camel-website

### Task (22)

[CAMEL-15030](https://issues.apache.org/jira/browse/CAMEL-15030)

camel-package-maven-plugin - Writes updated docs to log but its not updated

[CAMEL-14995](https://issues.apache.org/jira/browse/CAMEL-14995)

\[CAMEL-K\] Not all traits pages are being generated

[CAMEL-14978](https://issues.apache.org/jira/browse/CAMEL-14978)

Create Karaf feature for components camel-azure-storage-queue and camel-azure-storage-blob

[CAMEL-14953](https://issues.apache.org/jira/browse/CAMEL-14953)

Camel-AWS2-S3: Add the possibility to setup notification of events on a S3 bucket

[CAMEL-14943](https://issues.apache.org/jira/browse/CAMEL-14943)

camel-core - ToD in Java DSL should be easier to set advanced options

[CAMEL-14939](https://issues.apache.org/jira/browse/CAMEL-14939)

Undertow support: From version 2.1.0.Final, undertow doesn't support OSGi

[CAMEL-14936](https://issues.apache.org/jira/browse/CAMEL-14936)

camel-core - Remove optional prefix in FactoryFinder

[CAMEL-14926](https://issues.apache.org/jira/browse/CAMEL-14926)

Camel-Infinispan: From release 11.0, Infinispan won't support OSGi anymore

[CAMEL-14923](https://issues.apache.org/jira/browse/CAMEL-14923)

camel-core - Deprecate InOnly and InOut DSL and use To DSL with pattern defined

[CAMEL-14916](https://issues.apache.org/jira/browse/CAMEL-14916)

camel-base - Move dump stats that uses JAXB to camel-xml-jaxb

[CAMEL-14913](https://issues.apache.org/jira/browse/CAMEL-14913)

Remove WARN log in UpdateReadmeMojo

[CAMEL-14887](https://issues.apache.org/jira/browse/CAMEL-14887)

Move camel-headersmap from core to components

[CAMEL-14879](https://issues.apache.org/jira/browse/CAMEL-14879)

camel-djl - Fix doc headings

[CAMEL-14868](https://issues.apache.org/jira/browse/CAMEL-14868)

Camel-AWS2-\*: Where possible, give the possiblity to the end user to pass an AWS Request pojo as body

[CAMEL-14864](https://issues.apache.org/jira/browse/CAMEL-14864)

Be able to generate configurer for any pojo

[CAMEL-14863](https://issues.apache.org/jira/browse/CAMEL-14863)

Camel-DJL: Create a Karaf feature

[CAMEL-14862](https://issues.apache.org/jira/browse/CAMEL-14862)

Camel-DJL: Create a Spring Boot starter for the component

[CAMEL-14851](https://issues.apache.org/jira/browse/CAMEL-14851)

The camel-endpointdsl jar is missing the jandex index

[CAMEL-14846](https://issues.apache.org/jira/browse/CAMEL-14846)

Website is rapidly decaying

[CAMEL-14841](https://issues.apache.org/jira/browse/CAMEL-14841)

Remove camel-main:generate maven plugin

[CAMEL-14839](https://issues.apache.org/jira/browse/CAMEL-14839)

xref checker camel-package-maven-plugin reporting non-broken xrefs

[CAMEL-14828](https://issues.apache.org/jira/browse/CAMEL-14828)

camel-core - Remove multiple camel context support for restContextRef

### Test (2)

[CAMEL-15028](https://issues.apache.org/jira/browse/CAMEL-15028)

Advice in CDI tests is broken

[CAMEL-14957](https://issues.apache.org/jira/browse/CAMEL-14957)

camel-kafka - fails container tests after upgrade to kafka 2.5

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).