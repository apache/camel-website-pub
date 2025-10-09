# Apache camel 3.9.0 Release

## New and Noteworthy

This release is the new Camel 3.9.0 minor release.

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
      <version>3.9.0</version>
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
      <version>3.9.0</version>
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
| [apache-camel-3.9.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.9.0/apache-camel-3.9.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.9.0/apache-camel-3.9.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.9.0/apache-camel-3.9.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.9.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.9.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (46)

[CAMEL-16699](https://issues.apache.org/jira/browse/CAMEL-16699)

HttpProducer skip request headers for query params on bridge endpoint broken for common types

[CAMEL-16538](https://issues.apache.org/jira/browse/CAMEL-16538)

java.lang.IllegalArgumentException: Data format 'jacksonxml' could not be created

[CAMEL-16382](https://issues.apache.org/jira/browse/CAMEL-16382)

Unable to disable autowiring on Infinispan component

[CAMEL-16356](https://issues.apache.org/jira/browse/CAMEL-16356)

custom LdapEndpoint: inconsistent type for pageSize leads to NPE

[CAMEL-16345](https://issues.apache.org/jira/browse/CAMEL-16345)

camel-main fails to load component properties from Enviroment variables

[CAMEL-16344](https://issues.apache.org/jira/browse/CAMEL-16344)

camel-spring-ws - Skip Content-Type as SOAP:ENV response header

[CAMEL-16343](https://issues.apache.org/jira/browse/CAMEL-16343)

\[camel-kafka\] Avoid committing offsets onPartitionsRevoked if the user is manually committing the offsets

[CAMEL-16340](https://issues.apache.org/jira/browse/CAMEL-16340)

SalesforceProducer.doStart() is called before SalesforceComponent.doStart()

[CAMEL-16327](https://issues.apache.org/jira/browse/CAMEL-16327)

Kafka Consumer Component always commits latest offset on shutdown even if autoCommitOnStop == none

[CAMEL-16324](https://issues.apache.org/jira/browse/CAMEL-16324)

camel-core - Spring Transactions does not work due recent optimization

[CAMEL-16318](https://issues.apache.org/jira/browse/CAMEL-16318)

camel-kafka - LoginCallbackHandler causes ClassNotFoudException on OSGi

[CAMEL-16317](https://issues.apache.org/jira/browse/CAMEL-16317)

NPE on SFTP component query parameter for options that are duration

[CAMEL-16309](https://issues.apache.org/jira/browse/CAMEL-16309)

The Rest Openapi schema generator has a typo; "sting" instead of "string"

[CAMEL-16307](https://issues.apache.org/jira/browse/CAMEL-16307)

azure-storage-datalake:...?operation=getFile appends newline to the file content

[CAMEL-16305](https://issues.apache.org/jira/browse/CAMEL-16305)

camel-servicenow-maven-plugin generated model classes wont compile

[CAMEL-16298](https://issues.apache.org/jira/browse/CAMEL-16298)

camel-core - pollEnrich with endpoint-dsl should use EndpointConsumerBuilder

[CAMEL-16297](https://issues.apache.org/jira/browse/CAMEL-16297)

camel-core - Splitter does not call aggregation strategy when transacted is enabled

[CAMEL-16296](https://issues.apache.org/jira/browse/CAMEL-16296)

camel-as2 - Restarting bundle on karaf causes PortNumberInUse error

[CAMEL-16295](https://issues.apache.org/jira/browse/CAMEL-16295)

split with AggregationStrategy is ignored when using transacted

[CAMEL-16291](https://issues.apache.org/jira/browse/CAMEL-16291)

camel-cxfrs producer shouldn't try to read Entity from javax.ws.rs.core.Response

[CAMEL-16284](https://issues.apache.org/jira/browse/CAMEL-16284)

camel-couchbase: Incorrect Endpoint URI breaks CKC's couchbase connector

[CAMEL-16283](https://issues.apache.org/jira/browse/CAMEL-16283)

camel-jetty - NPE in binding for query parsing

[CAMEL-16282](https://issues.apache.org/jira/browse/CAMEL-16282)

VertxBufferConverter does not handle encoding correctly

[CAMEL-16280](https://issues.apache.org/jira/browse/CAMEL-16280)

NettyEndpointUriFactory#buildUri() not compatible with Netty endpoint URL

[CAMEL-16276](https://issues.apache.org/jira/browse/CAMEL-16276)

WireTap does not work with NoErrorHandler

[CAMEL-16258](https://issues.apache.org/jira/browse/CAMEL-16258)

camel-spring-boot - @ExcludeRoutes not working anymore

[CAMEL-16252](https://issues.apache.org/jira/browse/CAMEL-16252)

\[camel-azure-storage-blob\] Stream caching bug due to unsupported InputStream mark operation

[CAMEL-16244](https://issues.apache.org/jira/browse/CAMEL-16244)

Multiple consumers for the same endpoint using camel-restdsl-openapi-plugin

[CAMEL-16241](https://issues.apache.org/jira/browse/CAMEL-16241)

Endpoint DSL (http component) Properties are not correctly set for Basic Authentications

[CAMEL-16235](https://issues.apache.org/jira/browse/CAMEL-16235)

camel-servlet-starter does not ServletComponent

[CAMEL-16233](https://issues.apache.org/jira/browse/CAMEL-16233)

camel-jetty - type converter error after last optimization

[CAMEL-16227](https://issues.apache.org/jira/browse/CAMEL-16227)

Netty with reuseChannel=true invokes wrong callback

[CAMEL-16226](https://issues.apache.org/jira/browse/CAMEL-16226)

camel-cbor: Unexpected character ('¿' (code 191)): expected a valid value

[CAMEL-16225](https://issues.apache.org/jira/browse/CAMEL-16225)

camel-karaf - route-list command fail with NPE

[CAMEL-16210](https://issues.apache.org/jira/browse/CAMEL-16210)

camel-core - Choice EIP exception from predicate may trigger otherwise

[CAMEL-16206](https://issues.apache.org/jira/browse/CAMEL-16206)

camel-sql: Message body is not preserved when CamelSqlRetrieveGeneratedKeys == true

[CAMEL-16196](https://issues.apache.org/jira/browse/CAMEL-16196)

camel-main - Configure using Java only does not configure for some types

[CAMEL-16189](https://issues.apache.org/jira/browse/CAMEL-16189)

AWS2S3Producer not setting serverside encryption values

[CAMEL-16179](https://issues.apache.org/jira/browse/CAMEL-16179)

NPE during MongoDB initialization

[CAMEL-16178](https://issues.apache.org/jira/browse/CAMEL-16178)

Enrich with REST+netty hangs when connection is closed without response

[CAMEL-16177](https://issues.apache.org/jira/browse/CAMEL-16177)

File stream cache problem with multicast parallel processing and encrypted stream

[CAMEL-16176](https://issues.apache.org/jira/browse/CAMEL-16176)

camel-kafka - Bug in header filter strategy regexp pattern

[CAMEL-16173](https://issues.apache.org/jira/browse/CAMEL-16173)

Camel Resilience4j Bulkhead seems to not limit concurrent requests

[CAMEL-16079](https://issues.apache.org/jira/browse/CAMEL-16079)

aws-sn2 does not recognise FIFO queue configured though arn

[CAMEL-16063](https://issues.apache.org/jira/browse/CAMEL-16063)

should consider multiple ApplicationContext instances when specifying another management.server.port

[CAMEL-14980](https://issues.apache.org/jira/browse/CAMEL-14980)

camel-kafka - SerializationException - consumer keeps leaving and rejoining the group

### Dependency upgrade (1)

[CAMEL-16376](https://issues.apache.org/jira/browse/CAMEL-16376)

camel-spring-boot - Upgrade to Spring Boot 2.4.4

### Improvement (67)

[CAMEL-16522](https://issues.apache.org/jira/browse/CAMEL-16522)

Apache Camel Jars for latest versions

[CAMEL-16359](https://issues.apache.org/jira/browse/CAMEL-16359)

Camel-spring-rabbitmq - Allow null body

[CAMEL-16358](https://issues.apache.org/jira/browse/CAMEL-16358)

camel-spring-rabbitmq - Configure consumer retry strategies more easily

[CAMEL-16357](https://issues.apache.org/jira/browse/CAMEL-16357)

Camel-splunk: tcp mode can not work with port/host mapping (e.g. in docker environment)

[CAMEL-16355](https://issues.apache.org/jira/browse/CAMEL-16355)

camel-core - Optimize Filter and Choice EIP

[CAMEL-16351](https://issues.apache.org/jira/browse/CAMEL-16351)

camel-core - Camel JARs OSGi MANIFEST.MF has unwanted include-resources

[CAMEL-16349](https://issues.apache.org/jira/browse/CAMEL-16349)

camel-core - MainHelper load list from file in classpath to reduce memory

[CAMEL-16348](https://issues.apache.org/jira/browse/CAMEL-16348)

camel-core - Optimize shutdown strategy forceShutdown check

[CAMEL-16342](https://issues.apache.org/jira/browse/CAMEL-16342)

Upgrade common-compression to 1.20 and fix camel-tarfile accordingly

[CAMEL-16339](https://issues.apache.org/jira/browse/CAMEL-16339)

camel-seda - Optimize to avoid unnesssary exchange copy

[CAMEL-16337](https://issues.apache.org/jira/browse/CAMEL-16337)

camel-core - pooled exchanges - Can we optimize exchangeId

[CAMEL-16336](https://issues.apache.org/jira/browse/CAMEL-16336)

Make CustomSlackHttpClient compatible with okhttp 3.x

[CAMEL-16331](https://issues.apache.org/jira/browse/CAMEL-16331)

camel-core - DefaultConsumer used as PolllingConsumer EIP should not be pooled exchanges

[CAMEL-16328](https://issues.apache.org/jira/browse/CAMEL-16328)

Restore support for Slack custom server URL

[CAMEL-16326](https://issues.apache.org/jira/browse/CAMEL-16326)

camel-core - Optimize EIP storing information in exchange properties

[CAMEL-16322](https://issues.apache.org/jira/browse/CAMEL-16322)

Have a middle folder for google components

[CAMEL-16321](https://issues.apache.org/jira/browse/CAMEL-16321)

Have a middle folder for azure components

[CAMEL-16319](https://issues.apache.org/jira/browse/CAMEL-16319)

camel-core - Optimize consumer done callback

[CAMEL-16315](https://issues.apache.org/jira/browse/CAMEL-16315)

Camel-Netty: Support Hostname verification even though we are on Netty 4.1.x

[CAMEL-16314](https://issues.apache.org/jira/browse/CAMEL-16314)

camel-core - Some components does not work well with pooled exchanges

[CAMEL-16313](https://issues.apache.org/jira/browse/CAMEL-16313)

camel-splunk: can not use component without credentials (to be able to communicate with free splunk server)

[CAMEL-16311](https://issues.apache.org/jira/browse/CAMEL-16311)

camel-freemarker - Localized lookup should be disabled

[CAMEL-16294](https://issues.apache.org/jira/browse/CAMEL-16294)

camel-core - PollingConsumer - add option to handover the UoW

[CAMEL-16292](https://issues.apache.org/jira/browse/CAMEL-16292)

Upgrade to spring boot 2.4.3

[CAMEL-16288](https://issues.apache.org/jira/browse/CAMEL-16288)

camel-core - Endpoint should have getMaskedEndpointUri

[CAMEL-16286](https://issues.apache.org/jira/browse/CAMEL-16286)

camel-core - Services should invoke doBuild on child services

[CAMEL-16279](https://issues.apache.org/jira/browse/CAMEL-16279)

camel-core - Optimize routing engine to reuse internal state objects for GC reduction

[CAMEL-16272](https://issues.apache.org/jira/browse/CAMEL-16272)

camel-core - Optimize routing engine to reduce object allocation in redelivery error handler

[CAMEL-16271](https://issues.apache.org/jira/browse/CAMEL-16271)

camel-core - ReactiveExecutor add option to turn on|off statistics

[CAMEL-16270](https://issues.apache.org/jira/browse/CAMEL-16270)

Vertx Buffer converter should sharable among vertx components and not tied with vertx-web.

[CAMEL-16265](https://issues.apache.org/jira/browse/CAMEL-16265)

camel-microprofile-metrics - Mask sensitive data in endpoint URLs

[CAMEL-16264](https://issues.apache.org/jira/browse/CAMEL-16264)

camel-http - Add option to ignore response headers

[CAMEL-16262](https://issues.apache.org/jira/browse/CAMEL-16262)

camel-http - Add disable options on component to turn features off

[CAMEL-16253](https://issues.apache.org/jira/browse/CAMEL-16253)

Improve the way that the LRA client determines the new LRA URL

[CAMEL-16250](https://issues.apache.org/jira/browse/CAMEL-16250)

Support text finishing with a dash in StringHelper.dashToCamelCase

[CAMEL-16245](https://issues.apache.org/jira/browse/CAMEL-16245)

Improvement camel-google-storage guava dependency

[CAMEL-16238](https://issues.apache.org/jira/browse/CAMEL-16238)

Registry is not released after camelcontext calls the shutdown method

[CAMEL-16232](https://issues.apache.org/jira/browse/CAMEL-16232)

Camel-http: component doesn't use system properties \`javax.net.ssl.keyStorePassword\` and \`javax.net.ssl.keyStore\` if parameter \`useSystemPr0perties\` is set to true

[CAMEL-16231](https://issues.apache.org/jira/browse/CAMEL-16231)

camel-core - Optimize HeaderFilterStrategy to not include header value

[CAMEL-16222](https://issues.apache.org/jira/browse/CAMEL-16222)

camel-core - ExchangeFactory SPI

[CAMEL-16220](https://issues.apache.org/jira/browse/CAMEL-16220)

camel-http - optimize producer when sending to uri without any change

[CAMEL-16219](https://issues.apache.org/jira/browse/CAMEL-16219)

camel-core - Kamelet - Add support for optional template parameters

[CAMEL-16218](https://issues.apache.org/jira/browse/CAMEL-16218)

Mark use of java.util.Random with NOSONAR to not have false flags in code analysis reports

[CAMEL-16217](https://issues.apache.org/jira/browse/CAMEL-16217)

camel-core - FluentProducerTemplate - optimize to uri when its the same endpoint

[CAMEL-16215](https://issues.apache.org/jira/browse/CAMEL-16215)

camel-http - Optimize isStatusCodeOk

[CAMEL-16207](https://issues.apache.org/jira/browse/CAMEL-16207)

camel-core - Optimize HeaderFilterStrategy with startsWith pattern

[CAMEL-16205](https://issues.apache.org/jira/browse/CAMEL-16205)

camel-http - Optimize extract response body for small payloads

[CAMEL-16203](https://issues.apache.org/jira/browse/CAMEL-16203)

camel-core - Optimize removeHeaders all

[CAMEL-16202](https://issues.apache.org/jira/browse/CAMEL-16202)

camel-core - Optimize DefaultHeaderFilterStrategy filtering

[CAMEL-16201](https://issues.apache.org/jira/browse/CAMEL-16201)

camel-jfr - Save camel-recording in current dir by default

[CAMEL-16199](https://issues.apache.org/jira/browse/CAMEL-16199)

camel-http - Optimize headers added as request headers in producer

[CAMEL-16194](https://issues.apache.org/jira/browse/CAMEL-16194)

Optaplanner : upgrade to optaplanner 8.x

[CAMEL-16192](https://issues.apache.org/jira/browse/CAMEL-16192)

camel-spring-boot-engine-starter

[CAMEL-16183](https://issues.apache.org/jira/browse/CAMEL-16183)

camel-spring - XML DSL remove remoting/proxy

[CAMEL-16182](https://issues.apache.org/jira/browse/CAMEL-16182)

test-infra modules don't support testcontainers hub.image.name.prefix configuration

[CAMEL-16175](https://issues.apache.org/jira/browse/CAMEL-16175)

camel javascript routes loader

[CAMEL-16174](https://issues.apache.org/jira/browse/CAMEL-16174)

camel-zookeeper - Upgrade to latest 3.5.x

[CAMEL-16172](https://issues.apache.org/jira/browse/CAMEL-16172)

Upgrade to version 0.15.0 of OpenTelemetry

[CAMEL-16170](https://issues.apache.org/jira/browse/CAMEL-16170)

camel-spring-core - spring module with XML

[CAMEL-16169](https://issues.apache.org/jira/browse/CAMEL-16169)

camel-core - context.addComponent(name, instance) should auto start if needed

[CAMEL-16162](https://issues.apache.org/jira/browse/CAMEL-16162)

camel-core - OnCompletion EIP - Only 1 allowed

[CAMEL-16155](https://issues.apache.org/jira/browse/CAMEL-16155)

camel-zookeeper-master: add option to set a custom ManagedGroupFactory

[CAMEL-16105](https://issues.apache.org/jira/browse/CAMEL-16105)

camel-kafka - AllowManualCommit does not ensure full control of the commit flows

[CAMEL-15924](https://issues.apache.org/jira/browse/CAMEL-15924)

\[camel-vertx-kafka\] Add the ability to commit the offsets manually

[CAMEL-15741](https://issues.apache.org/jira/browse/CAMEL-15741)

camel-joor - Add function for header and exchange property with default value

[CAMEL-14490](https://issues.apache.org/jira/browse/CAMEL-14490)

Have a middle folder for aws and aws2 components

[CAMEL-10956](https://issues.apache.org/jira/browse/CAMEL-10956)

camel-core: more flexible route loader

### New Feature (12)

[CAMEL-16323](https://issues.apache.org/jira/browse/CAMEL-16323)

Create a Camel-AWS-Secret-Manager component

[CAMEL-16310](https://issues.apache.org/jira/browse/CAMEL-16310)

Allow to configure type of MessageListenerContainer in camel-spring-rabbitmq

[CAMEL-16302](https://issues.apache.org/jira/browse/CAMEL-16302)

camel-core - Optional property placeholders

[CAMEL-16301](https://issues.apache.org/jira/browse/CAMEL-16301)

Allow endpoint to override prefetchCount from component

[CAMEL-16285](https://issues.apache.org/jira/browse/CAMEL-16285)

Extensible ResourceHelper

[CAMEL-16255](https://issues.apache.org/jira/browse/CAMEL-16255)

Use of the slack-api-model to create rich content

[CAMEL-16213](https://issues.apache.org/jira/browse/CAMEL-16213)

camel-core - Exchange pooling

[CAMEL-16153](https://issues.apache.org/jira/browse/CAMEL-16153)

camel-report-maven-plugin: overallCoverageThreshold

[CAMEL-15964](https://issues.apache.org/jira/browse/CAMEL-15964)

Create a Google Cloud Storage component

[CAMEL-15963](https://issues.apache.org/jira/browse/CAMEL-15963)

Create a Google Cloud Functions component

[CAMEL-14053](https://issues.apache.org/jira/browse/CAMEL-14053)

Routes Loader SPI

[CAMEL-12545](https://issues.apache.org/jira/browse/CAMEL-12545)

create a yaml based route loader

### Sub-task (1)

[CAMEL-16012](https://issues.apache.org/jira/browse/CAMEL-16012)

Remove camel-example- prefix in folder names in camel-examples

### Task (33)

[CAMEL-16363](https://issues.apache.org/jira/browse/CAMEL-16363)

Create Camel-aws-secrets-manager starter

[CAMEL-16362](https://issues.apache.org/jira/browse/CAMEL-16362)

camel-spring-boot - BOM generator JAR alignments error

[CAMEL-16347](https://issues.apache.org/jira/browse/CAMEL-16347)

Camel test-infra: Create a module for AWS Secrets manager

[CAMEL-16334](https://issues.apache.org/jira/browse/CAMEL-16334)

Having a middle folder for test (unit + testcontainers) components

[CAMEL-16333](https://issues.apache.org/jira/browse/CAMEL-16333)

Having a middle folder for debezium components

[CAMEL-16332](https://issues.apache.org/jira/browse/CAMEL-16332)

Have a middle folder for microprofile components

[CAMEL-16329](https://issues.apache.org/jira/browse/CAMEL-16329)

Camel-Google-Mail-Stream: Set markAsRead as true by default

[CAMEL-16308](https://issues.apache.org/jira/browse/CAMEL-16308)

Camel-Google-bigquery-sql: Rename query parameter in bigquery sql component

[CAMEL-16303](https://issues.apache.org/jira/browse/CAMEL-16303)

URI generation: if a part of the component name is equal to a path parameter the URI generation will fail

[CAMEL-16300](https://issues.apache.org/jira/browse/CAMEL-16300)

Camel-Examples: Add a google pubsub example

[CAMEL-16299](https://issues.apache.org/jira/browse/CAMEL-16299)

Test infra: allow greater service configuration

[CAMEL-16293](https://issues.apache.org/jira/browse/CAMEL-16293)

Camel-AWS2-Components: Autocreation of entities should be false by default

[CAMEL-16278](https://issues.apache.org/jira/browse/CAMEL-16278)

Use azure-sdk-bom instead of individual azure artifact versions

[CAMEL-16277](https://issues.apache.org/jira/browse/CAMEL-16277)

Camel-File: Use appendChar for the first message too

[CAMEL-16275](https://issues.apache.org/jira/browse/CAMEL-16275)

Move the RouteBuilderLoader from camel-joor, camel-xml-io and camel-xml-jaxb to a dedicated artifact in the dsl folder

[CAMEL-16274](https://issues.apache.org/jira/browse/CAMEL-16274)

Camel-google-storage: serviceAccountKey should be supported as file, classpath, remote etc.

[CAMEL-16268](https://issues.apache.org/jira/browse/CAMEL-16268)

camel-xstream - Test dependency of junit-vintage-engine not set to scope test

[CAMEL-16267](https://issues.apache.org/jira/browse/CAMEL-16267)

camel-examples - Add yaml-dsl example

[CAMEL-16261](https://issues.apache.org/jira/browse/CAMEL-16261)

Github PR Template: Make it optional

[CAMEL-16254](https://issues.apache.org/jira/browse/CAMEL-16254)

\[camel-debezium-common\] Support nested Structs

[CAMEL-16251](https://issues.apache.org/jira/browse/CAMEL-16251)

Move Performance and jmh itests in a separated repository

[CAMEL-16246](https://issues.apache.org/jira/browse/CAMEL-16246)

Remove deprecated Camel-Azure component

[CAMEL-16229](https://issues.apache.org/jira/browse/CAMEL-16229)

Mocking Existing Endpoints Doc Not Updated

[CAMEL-16224](https://issues.apache.org/jira/browse/CAMEL-16224)

Create Spring Boot starter for camel-google-storage

[CAMEL-16211](https://issues.apache.org/jira/browse/CAMEL-16211)

Revisit RoutesDefinition::route(RouteDefinition route)

[CAMEL-16195](https://issues.apache.org/jira/browse/CAMEL-16195)

Remove camel-optaplanner Karaf feature

[CAMEL-16193](https://issues.apache.org/jira/browse/CAMEL-16193)

Use SecureRandom instead of Random

[CAMEL-16190](https://issues.apache.org/jira/browse/CAMEL-16190)

Sensitive configuration values not redacted in Auto-configuration summary

[CAMEL-16186](https://issues.apache.org/jira/browse/CAMEL-16186)

Camel-AWS2-SQS: Support String as body for batch message

[CAMEL-16171](https://issues.apache.org/jira/browse/CAMEL-16171)

Add uri-endpoint-override options to all AWS2 components

[CAMEL-16156](https://issues.apache.org/jira/browse/CAMEL-16156)

Improve the usage of org.apache.camel.jmx.disabled

[CAMEL-16137](https://issues.apache.org/jira/browse/CAMEL-16137)

Investigate the usage of java.awt.headless system property in tests

[CAMEL-16115](https://issues.apache.org/jira/browse/CAMEL-16115)

Remove Camel-AWS-\* components

### Test (2)

[CAMEL-16369](https://issues.apache.org/jira/browse/CAMEL-16369)

camel-endpointdsl and camel-componentdsl - Test without JMX enabled

[CAMEL-15635](https://issues.apache.org/jira/browse/CAMEL-15635)

Some Kudu tests are failing in JDK >= 12 builds

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).