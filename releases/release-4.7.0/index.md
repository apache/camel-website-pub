# Apache camel 4.7.0 Release

## New and Noteworthy

This release is the new Camel 4.7.0 release.

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
      <version>4.7.0</version>
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
      <version>4.7.0</version>
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
| [apache-camel-4.7.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-src.zip.sha512) |
| [apache-camel-4.7.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.xml.sha512) |
| [apache-camel-4.7.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.7.0/apache-camel-4.7.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.7.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.7.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (57)

[CAMEL-20965](https://issues.apache.org/jira/browse/CAMEL-20965)

InputStreamCache is not thread-safe

[CAMEL-20949](https://issues.apache.org/jira/browse/CAMEL-20949)

camel-bean - Method parameters with both type and property placeholder does not work

[CAMEL-20946](https://issues.apache.org/jira/browse/CAMEL-20946)

Generated Quarkus project from JBang is not working with Camel Debug

[CAMEL-20939](https://issues.apache.org/jira/browse/CAMEL-20939)

camel-jbang - unable to load profile

[CAMEL-20932](https://issues.apache.org/jira/browse/CAMEL-20932)

camel-core - Error handler redelivery options should support template parameters for route templates

[CAMEL-20929](https://issues.apache.org/jira/browse/CAMEL-20929)

camel-core - Properties component with ignore missing property should also ignore from functions

[CAMEL-20921](https://issues.apache.org/jira/browse/CAMEL-20921)

Route configuration is not loaded on a Camel application XML file

[CAMEL-20920](https://issues.apache.org/jira/browse/CAMEL-20920)

RouteLoader: Can't load a valid route with the same location after a previous load error

[CAMEL-20911](https://issues.apache.org/jira/browse/CAMEL-20911)

Maven build failure for Camel JBang exported Quarkus app

[CAMEL-20906](https://issues.apache.org/jira/browse/CAMEL-20906)

NPE in RouteWatcherReloadStrategy.onRouteReload(RouteWatcherReloadStrategy.java:300)

[CAMEL-20890](https://issues.apache.org/jira/browse/CAMEL-20890)

Use Step ID's in routeTemplate

[CAMEL-20889](https://issues.apache.org/jira/browse/CAMEL-20889)

camel-core: Stream is not reset when Message.getBody(class) is invoked ans stream caching is enabled

[CAMEL-20887](https://issues.apache.org/jira/browse/CAMEL-20887)

generated PojoBeanModel is missing the artifact

[CAMEL-20877](https://issues.apache.org/jira/browse/CAMEL-20877)

camel-jbang ignores jib-maven-plugin-version

[CAMEL-20873](https://issues.apache.org/jira/browse/CAMEL-20873)

camel-platform-http-vertx: Responses may not complete if exceptions are thrown in VertxPlatformHttpSupport.writeResponse

[CAMEL-20866](https://issues.apache.org/jira/browse/CAMEL-20866)

SEDA with exchangepattern InOnly gives sometimes multiple responses

[CAMEL-20864](https://issues.apache.org/jira/browse/CAMEL-20864)

camel-kafka - With confluent schema registry does not work properly.

[CAMEL-20863](https://issues.apache.org/jira/browse/CAMEL-20863)

camel-langchain4j-chat: NPE if only producer is used

[CAMEL-20859](https://issues.apache.org/jira/browse/CAMEL-20859)

camel-jbang - Transforming a yaml route to xml specifying a folder is generating a yaml file

[CAMEL-20853](https://issues.apache.org/jira/browse/CAMEL-20853)

Rest DSL - Rest routes can not be grouped anymore

[CAMEL-20850](https://issues.apache.org/jira/browse/CAMEL-20850)

LRUCache evicts entries unexpectedly

[CAMEL-20847](https://issues.apache.org/jira/browse/CAMEL-20847)

camel-jbang - Run with jolokia enabled does not work

[CAMEL-20841](https://issues.apache.org/jira/browse/CAMEL-20841)

DataSonnet expressions are removed under memory load

[CAMEL-20840](https://issues.apache.org/jira/browse/CAMEL-20840)

Cannot cast ResumeActionAwareAdapter to KinesisResumeAdapter

[CAMEL-20839](https://issues.apache.org/jira/browse/CAMEL-20839)

camel-jbang - Run with openapi in sub folder does not work

[CAMEL-20835](https://issues.apache.org/jira/browse/CAMEL-20835)

OOM using RecipientList

[CAMEL-20834](https://issues.apache.org/jira/browse/CAMEL-20834)

camel-salesforce - A NullPointException in SubscriptionHelper.subscribe() interrupts platform-event subscription

[CAMEL-20823](https://issues.apache.org/jira/browse/CAMEL-20823)

camel-smb component polling doesn't account for directories

[CAMEL-20820](https://issues.apache.org/jira/browse/CAMEL-20820)

camel-core - Duplicate JMX MBean operation for resource endpoints

[CAMEL-20819](https://issues.apache.org/jira/browse/CAMEL-20819)

camel-jbang - Reload mode with supervising route controller does not reload routes

[CAMEL-20818](https://issues.apache.org/jira/browse/CAMEL-20818)

camel-yaml-dsl - errorHandler does not have id field as all other YAML elements

[CAMEL-20816](https://issues.apache.org/jira/browse/CAMEL-20816)

Camel-JBang: Export to quarkus does not honor quarkusGroupId setting

[CAMEL-20815](https://issues.apache.org/jira/browse/CAMEL-20815)

exchange.getVariable does not get Global variables in custom processor

[CAMEL-20812](https://issues.apache.org/jira/browse/CAMEL-20812)

camel-netty-http: hostnameVerification option not used

[CAMEL-20799](https://issues.apache.org/jira/browse/CAMEL-20799)

camel-catalog - Model schema for setHeaders and setVariables does not include array of element

[CAMEL-20790](https://issues.apache.org/jira/browse/CAMEL-20790)

kafka batching consumer polls randomly failing with NPE under load

[CAMEL-20783](https://issues.apache.org/jira/browse/CAMEL-20783)

camel export --runtime=quarkus does not work with custom camel.jbang.quarkusVersion

[CAMEL-20778](https://issues.apache.org/jira/browse/CAMEL-20778)

Intercept created using AdviceWithRouteBuilder causes issues with error handling (regression)

[CAMEL-20771](https://issues.apache.org/jira/browse/CAMEL-20771)

camel-jbang - Does not hot-reload java source changes

[CAMEL-20769](https://issues.apache.org/jira/browse/CAMEL-20769)

camel-jms: TemporaryReplyQueueExceptionListener may be causing an endless lock

[CAMEL-20768](https://issues.apache.org/jira/browse/CAMEL-20768)

camel-spring-redis - SpringRedisIdempotentRepository flushes DB on start

[CAMEL-20767](https://issues.apache.org/jira/browse/CAMEL-20767)

camel-spring-redis - Creating SpringRedisIdempotentRepository via SB should be possible

[CAMEL-20763](https://issues.apache.org/jira/browse/CAMEL-20763)

Rest template with underscore fails after Camel 4.2.0

[CAMEL-20761](https://issues.apache.org/jira/browse/CAMEL-20761)

camel-debug - Message history must be enabled

[CAMEL-20758](https://issues.apache.org/jira/browse/CAMEL-20758)

camel-spring-boot - Debugger is created twice

[CAMEL-20752](https://issues.apache.org/jira/browse/CAMEL-20752)

camel-saga - NPE in compesating

[CAMEL-20750](https://issues.apache.org/jira/browse/CAMEL-20750)

camel-yaml-dsl - Rest DSL with enableCORS does not work

[CAMEL-20746](https://issues.apache.org/jira/browse/CAMEL-20746)

Bean deserialisation from YAML displays message displays wrong nodeType

[CAMEL-20738](https://issues.apache.org/jira/browse/CAMEL-20738)

camel-jasypt-starter - PropertiesParser cannot be redefined

[CAMEL-20660](https://issues.apache.org/jira/browse/CAMEL-20660)

camel-azure-servicebus: Consumer fails to acknowledge messages

[CAMEL-20493](https://issues.apache.org/jira/browse/CAMEL-20493)

camel-core: concurrency issue copying headers

[CAMEL-18821](https://issues.apache.org/jira/browse/CAMEL-18821)

camel-core - Thread hangs on transacted routes after aggregation and multiplex (possibly more)

[CAMEL-18384](https://issues.apache.org/jira/browse/CAMEL-18384)

Split/Aggregation parallelProcessing+parallelAggregate is sequential

[CAMEL-17829](https://issues.apache.org/jira/browse/CAMEL-17829)

camel-as2 - issue in MDN response condition

[CAMEL-17110](https://issues.apache.org/jira/browse/CAMEL-17110)

Camel-Kamelets: While using AWS S3 source noticed files were deleted before being consumed at all

[CAMEL-16829](https://issues.apache.org/jira/browse/CAMEL-16829)

camel-core - Stuck processing with nested parallel splits and custom thread pool

[CAMEL-15903](https://issues.apache.org/jira/browse/CAMEL-15903)

Master component do not retry endpoint startup on failure

### Dependency upgrade (7)

[CAMEL-20941](https://issues.apache.org/jira/browse/CAMEL-20941)

camel-parquest-avro - Should include needed hadoop JARs

[CAMEL-20830](https://issues.apache.org/jira/browse/CAMEL-20830)

camel-jetty - Upgrading causes SSL tests to fail

[CAMEL-20800](https://issues.apache.org/jira/browse/CAMEL-20800)

camel-couchdb: gson upgrade to 2.11.0 breaks the component

[CAMEL-20788](https://issues.apache.org/jira/browse/CAMEL-20788)

Use another protobuf-maven-plugin

[CAMEL-20779](https://issues.apache.org/jira/browse/CAMEL-20779)

camel-spring-boot - Upgrade to SB 3.3.0

[CAMEL-20600](https://issues.apache.org/jira/browse/CAMEL-20600)

camel-activemq - Upgrade to ActiveMQ classic 6.x or create camel-activemq6

[CAMEL-20304](https://issues.apache.org/jira/browse/CAMEL-20304)

Upgrade dizitart nitrite to 4+

### Improvement (81)

[CAMEL-20948](https://issues.apache.org/jira/browse/CAMEL-20948)

camel-util-json doesn't handle streaming correctly

[CAMEL-20945](https://issues.apache.org/jira/browse/CAMEL-20945)

camel-jbang - Run java route without need for class wrapper

[CAMEL-20944](https://issues.apache.org/jira/browse/CAMEL-20944)

camel-jbang - Generate plugin should validate file exists

[CAMEL-20934](https://issues.apache.org/jira/browse/CAMEL-20934)

camel-seda - Sending to consumers should use callback for completion work

[CAMEL-20933](https://issues.apache.org/jira/browse/CAMEL-20933)

rest-dsl - Add option to configure stream cache per route

[CAMEL-20931](https://issues.apache.org/jira/browse/CAMEL-20931)

camel-core - Add substring function to simple languge

[CAMEL-20930](https://issues.apache.org/jira/browse/CAMEL-20930)

camel-core - Bean DSL dev console

[CAMEL-20928](https://issues.apache.org/jira/browse/CAMEL-20928)

camel-jbang - Export beans with ENV variable properties should silent ignore ENV missing

[CAMEL-20926](https://issues.apache.org/jira/browse/CAMEL-20926)

camel-core - Add fromRouteId function to simple language

[CAMEL-20924](https://issues.apache.org/jira/browse/CAMEL-20924)

camel-http - Add oauth2scope parameter

[CAMEL-20922](https://issues.apache.org/jira/browse/CAMEL-20922)

Camel-crypto: Extract PGPdataFormat to another component

[CAMEL-20903](https://issues.apache.org/jira/browse/CAMEL-20903)

camel-jbang - Only load custom plugin if in use

[CAMEL-20902](https://issues.apache.org/jira/browse/CAMEL-20902)

camel-jbang - Running with older version causes plugin download problems

[CAMEL-20901](https://issues.apache.org/jira/browse/CAMEL-20901)

camel-arangodb: Add the option to provide a custom Vertx instance

[CAMEL-20900](https://issues.apache.org/jira/browse/CAMEL-20900)

camel-jbang-plugin-k add --integration-profile flag on run command

[CAMEL-20898](https://issues.apache.org/jira/browse/CAMEL-20898)

camel-core - Deep copy of route templates

[CAMEL-20897](https://issues.apache.org/jira/browse/CAMEL-20897)

camel-core - Allow to use $simple{xxx} inside RAW(xxx) for more power

[CAMEL-20895](https://issues.apache.org/jira/browse/CAMEL-20895)

camel-djl - The image classification predictors should not round the resulted probabilities

[CAMEL-20892](https://issues.apache.org/jira/browse/CAMEL-20892)

Misleading error message when Kamelet misses mandatory field value

[CAMEL-20891](https://issues.apache.org/jira/browse/CAMEL-20891)

Improve the catalog documentation for Processor's Ref attribute.

[CAMEL-20881](https://issues.apache.org/jira/browse/CAMEL-20881)

camel-core - Log should not need to create DefaultPollingConsumerPollStrategy

[CAMEL-20879](https://issues.apache.org/jira/browse/CAMEL-20879)

camel-core - Unique exchange counter

[CAMEL-20868](https://issues.apache.org/jira/browse/CAMEL-20868)

camel-aws-xray-starter

[CAMEL-20865](https://issues.apache.org/jira/browse/CAMEL-20865)

camel-elasticsearch-rest-client: Add usage details to component documentation

[CAMEL-20861](https://issues.apache.org/jira/browse/CAMEL-20861)

Add endpoint service location to default tracing

[CAMEL-20860](https://issues.apache.org/jira/browse/CAMEL-20860)

camel-core - Endpoint should have isRemote method

[CAMEL-20857](https://issues.apache.org/jira/browse/CAMEL-20857)

Keep all extensions of filename when transforming routes from folder with Camel Jbang

[CAMEL-20856](https://issues.apache.org/jira/browse/CAMEL-20856)

camel-jbang - Do not write pid file if PID\_IS\_UNDEFINED

[CAMEL-20852](https://issues.apache.org/jira/browse/CAMEL-20852)

Allow empty files within ZipAggregationStrategy

[CAMEL-20851](https://issues.apache.org/jira/browse/CAMEL-20851)

camel-elasticsearch-rest-client: Sniffer should be closed on producer stop

[CAMEL-20849](https://issues.apache.org/jira/browse/CAMEL-20849)

Move TransformerKey and ValidatorKey to the SPI

[CAMEL-20848](https://issues.apache.org/jira/browse/CAMEL-20848)

camel-jbang - Export should only jib if no jkube is in use

[CAMEL-20846](https://issues.apache.org/jira/browse/CAMEL-20846)

camel-elasticsearch-rest-client: Add component options

[CAMEL-20845](https://issues.apache.org/jira/browse/CAMEL-20845)

camel-core - Simple language to make it easy to replace texts

[CAMEL-20842](https://issues.apache.org/jira/browse/CAMEL-20842)

Add endpoint service location to backlog tracing

[CAMEL-20836](https://issues.apache.org/jira/browse/CAMEL-20836)

camel-qdrant: Add support for deleting a collection

[CAMEL-20833](https://issues.apache.org/jira/browse/CAMEL-20833)

Add recursive option to camel-smb

[CAMEL-20832](https://issues.apache.org/jira/browse/CAMEL-20832)

camel-openapi-java - Validate message body for json using a json schema valdaitor

[CAMEL-20829](https://issues.apache.org/jira/browse/CAMEL-20829)

Streamline ServicePool synchronization

[CAMEL-20828](https://issues.apache.org/jira/browse/CAMEL-20828)

camel-platform-http - Allow to known if platform engine is in use or not without triggering creation

[CAMEL-20824](https://issues.apache.org/jira/browse/CAMEL-20824)

camel-core - Backlog tracer should include internal exchange properties

[CAMEL-20821](https://issues.apache.org/jira/browse/CAMEL-20821)

camel-opentelemetry - Add traceProcessors boolean option

[CAMEL-20810](https://issues.apache.org/jira/browse/CAMEL-20810)

camel-jbang - Add camel get platform-http command

[CAMEL-20808](https://issues.apache.org/jira/browse/CAMEL-20808)

camel-etcd - Setting endpoint should be tooling friendly

[CAMEL-20804](https://issues.apache.org/jira/browse/CAMEL-20804)

camel-cloud - Deprecate camel-cloud

[CAMEL-20803](https://issues.apache.org/jira/browse/CAMEL-20803)

camel-spring-rabbitmq - Configuring maximumRetryAttempts should accept 0

[CAMEL-20798](https://issues.apache.org/jira/browse/CAMEL-20798)

camel-tracing - Add servername to more decorators

[CAMEL-20795](https://issues.apache.org/jira/browse/CAMEL-20795)

camel-nats - NATS Credential file support

[CAMEL-20794](https://issues.apache.org/jira/browse/CAMEL-20794)

Camel-kinesis: Kinesis producer has a very low throughtput

[CAMEL-20789](https://issues.apache.org/jira/browse/CAMEL-20789)

camel-kubernetes - Secrets and Config Maps with binay content should be saved as binary file, instead of String in property resolver

[CAMEL-20787](https://issues.apache.org/jira/browse/CAMEL-20787)

Camel-kinesis: Kinesis consumer set body type InputStream, which is not a common record type

[CAMEL-20776](https://issues.apache.org/jira/browse/CAMEL-20776)

Camel-kinesis: Listing shard before every record request will increase extra latency

[CAMEL-20775](https://issues.apache.org/jira/browse/CAMEL-20775)

camel-hashicorp-vault - configure multiple engines

[CAMEL-20773](https://issues.apache.org/jira/browse/CAMEL-20773)

camel-health - Consumer health checks should be skipped for non autoStartup routes

[CAMEL-20766](https://issues.apache.org/jira/browse/CAMEL-20766)

camel-core - Running in dev mode should turn on JMX updateRouteEnabled

[CAMEL-20762](https://issues.apache.org/jira/browse/CAMEL-20762)

camel-core - Move detection of camel-debug JAR to camel-main

[CAMEL-20760](https://issues.apache.org/jira/browse/CAMEL-20760)

camel-core - Allow to turn on|off RMI connector for tooling based debuggers

[CAMEL-20759](https://issues.apache.org/jira/browse/CAMEL-20759)

camel-as2 update client to support compression before signing

[CAMEL-20757](https://issues.apache.org/jira/browse/CAMEL-20757)

camel-debug - Use the lightweight xml-io for route dumper

[CAMEL-20755](https://issues.apache.org/jira/browse/CAMEL-20755)

camel-kamelet - Default location should be without leading slash for classpath

[CAMEL-20749](https://issues.apache.org/jira/browse/CAMEL-20749)

camel-core - ThrottlingExceptionRoutePolicy should have default values

[CAMEL-20748](https://issues.apache.org/jira/browse/CAMEL-20748)

camel-core - Route policy should have Route injected if RouteAware

[CAMEL-20747](https://issues.apache.org/jira/browse/CAMEL-20747)

Remove usage of deprecated Spring Security classes for route policies

[CAMEL-20745](https://issues.apache.org/jira/browse/CAMEL-20745)

camel-core-dsl - Add support for constructors to lookup beans

[CAMEL-20743](https://issues.apache.org/jira/browse/CAMEL-20743)

camel-model - Load Balancer EIPs to be named with LoadBalancer to be consistent in naming style

[CAMEL-20645](https://issues.apache.org/jira/browse/CAMEL-20645)

camel-jbang-plugin-k run command telemetry trait parameters ignored

[CAMEL-20608](https://issues.apache.org/jira/browse/CAMEL-20608)

camel-jbang - Improve the docker image

[CAMEL-20586](https://issues.apache.org/jira/browse/CAMEL-20586)

camel-jbang - Export to CSB can use camel.main.xxx properties

[CAMEL-20547](https://issues.apache.org/jira/browse/CAMEL-20547)

camel-openapi-rest-dsl-generator - Migrate from apicurio models to openapi3 models

[CAMEL-20500](https://issues.apache.org/jira/browse/CAMEL-20500)

camel-jbang - Move generate commands to its own plugin

[CAMEL-20439](https://issues.apache.org/jira/browse/CAMEL-20439)

camel-cloudevents - Move API to camel-api

[CAMEL-20407](https://issues.apache.org/jira/browse/CAMEL-20407)

camel-datasonnet - Add support for variables

[CAMEL-20244](https://issues.apache.org/jira/browse/CAMEL-20244)

camel-core - Supervising route controller should default be DOWN during restarting and exhaust phase

[CAMEL-19915](https://issues.apache.org/jira/browse/CAMEL-19915)

Camel AS2 doesn't support compressed before signed

[CAMEL-19897](https://issues.apache.org/jira/browse/CAMEL-19897)

camel-core: remove isStatisticsEnabled from type converter statistics

[CAMEL-19398](https://issues.apache.org/jira/browse/CAMEL-19398)

camel-core: type converter performs slowly due to exception-based flow control

[CAMEL-19010](https://issues.apache.org/jira/browse/CAMEL-19010)

file component: confirm not called on idempotentRepository

[CAMEL-18962](https://issues.apache.org/jira/browse/CAMEL-18962)

camel-as2 - AS2Consumer always accepts unencrpted/unsigned data

[CAMEL-18186](https://issues.apache.org/jira/browse/CAMEL-18186)

camel-saga: tracing information is not propagate on compensation/completion

[CAMEL-17502](https://issues.apache.org/jira/browse/CAMEL-17502)

add documentation about event notifier

[CAMEL-17111](https://issues.apache.org/jira/browse/CAMEL-17111)

Camel-AWS2-S3: Supporting Consumer idempotency in some way

### New Feature (18)

[CAMEL-20909](https://issues.apache.org/jira/browse/CAMEL-20909)

Camel-Aws-Kinesis: Support KCL Consumers

[CAMEL-20905](https://issues.apache.org/jira/browse/CAMEL-20905)

camel-djl - Support more model applications

[CAMEL-20878](https://issues.apache.org/jira/browse/CAMEL-20878)

camel-jbang - get rest

[CAMEL-20827](https://issues.apache.org/jira/browse/CAMEL-20827)

Add endpoint service location to aws, azure and google components

[CAMEL-20825](https://issues.apache.org/jira/browse/CAMEL-20825)

camel-rest - Contract first for api-doc should include the spec

[CAMEL-20822](https://issues.apache.org/jira/browse/CAMEL-20822)

camel-langchain4j-chat - implement tool capabilities

[CAMEL-20754](https://issues.apache.org/jira/browse/CAMEL-20754)

Support MQTT5 Publish Properties in Paho-MQTT5 component

[CAMEL-20739](https://issues.apache.org/jira/browse/CAMEL-20739)

Camel-Pinecone: Add a datatype for transforming langchain embeddings in Pinecone objects

[CAMEL-20728](https://issues.apache.org/jira/browse/CAMEL-20728)

camel-aws2s3 Stream Producer should support multipart loading

[CAMEL-20725](https://issues.apache.org/jira/browse/CAMEL-20725)

Camel-Pinecone: Add more producer operations

[CAMEL-20679](https://issues.apache.org/jira/browse/CAMEL-20679)

camel-smb: create a producer for the component

[CAMEL-20617](https://issues.apache.org/jira/browse/CAMEL-20617)

camel-rest - Add RestRegistryConsole

[CAMEL-20573](https://issues.apache.org/jira/browse/CAMEL-20573)

Camel-Milvus: Evaluating if creating a converter like qdrant component makes sense

[CAMEL-20217](https://issues.apache.org/jira/browse/CAMEL-20217)

Provide option to create a Pipe file through Camel Jbang init

[CAMEL-20216](https://issues.apache.org/jira/browse/CAMEL-20216)

Provide documentation on option to create a kamelet file through Camel Jbang init

[CAMEL-19985](https://issues.apache.org/jira/browse/CAMEL-19985)

camel-smooks - Add component for Smooks for EDI data mapping

[CAMEL-18546](https://issues.apache.org/jira/browse/CAMEL-18546)

camel-core - HostedService - To mark a consumer as a Camel hosted service

[CAMEL-6070](https://issues.apache.org/jira/browse/CAMEL-6070)

camel-test - Add annotations to configure test class instead of using methods

### Sub-task (7)

[CAMEL-20916](https://issues.apache.org/jira/browse/CAMEL-20916)

Camel-AWS-Kinesis: KCL Consumers, add documentation

[CAMEL-20914](https://issues.apache.org/jira/browse/CAMEL-20914)

Camel-AWS-Kinesis: KCL Consumers add an example

[CAMEL-20913](https://issues.apache.org/jira/browse/CAMEL-20913)

Camel-AWS-Kinesis: KCL Consumers, add support for profile/default/session credentials for Cloudwatch and DynamoDB clients

[CAMEL-20912](https://issues.apache.org/jira/browse/CAMEL-20912)

Camel-AWS-Kinesis: KCL Consumers add parameters for passing Cloudwatch and DynamoDB Clients

[CAMEL-20764](https://issues.apache.org/jira/browse/CAMEL-20764)

Camel-AWS-Bedrock: Support Amazon Titan Text G1 Premier model

[CAMEL-20222](https://issues.apache.org/jira/browse/CAMEL-20222)

Provide documentation on option to create kamelet on Camel website

[CAMEL-20221](https://issues.apache.org/jira/browse/CAMEL-20221)

Provide documentation on option to create kamelet in CLI help

### Task (27)

[CAMEL-21077](https://issues.apache.org/jira/browse/CAMEL-21077)

Camel-upgrade-recipes: cover upgrading camel 4.6 to 4.7

[CAMEL-20917](https://issues.apache.org/jira/browse/CAMEL-20917)

camel-jbang: Camel Jbang is unable to load external plugins

[CAMEL-20893](https://issues.apache.org/jira/browse/CAMEL-20893)

camel-jms: simplify JmsRouteRequestReplyTest

[CAMEL-20885](https://issues.apache.org/jira/browse/CAMEL-20885)

Deprecate kotlin

[CAMEL-20884](https://issues.apache.org/jira/browse/CAMEL-20884)

Improve performance of Camel Package Maven plugin

[CAMEL-20880](https://issues.apache.org/jira/browse/CAMEL-20880)

Move AI related component to camel-ai middle folder

[CAMEL-20843](https://issues.apache.org/jira/browse/CAMEL-20843)

camel-test: extract interface and common parts from CamelTestSupport

[CAMEL-20826](https://issues.apache.org/jira/browse/CAMEL-20826)

The camel-package-maven-plugin:generate mvn goal does not produce reproducible jandex.idx files

[CAMEL-20813](https://issues.apache.org/jira/browse/CAMEL-20813)

camel-infinispan: tests should use singleton containers

[CAMEL-20792](https://issues.apache.org/jira/browse/CAMEL-20792)

camel-jpa: upgrade to OpenJPA 4 breaks the tests

[CAMEL-20785](https://issues.apache.org/jira/browse/CAMEL-20785)

camel-test: CamelTestSupport has become inadequatedly designed

[CAMEL-20782](https://issues.apache.org/jira/browse/CAMEL-20782)

camel-test-infra-mongodb: MongoDB 5 requires hosts with AVX

[CAMEL-20777](https://issues.apache.org/jira/browse/CAMEL-20777)

Intercept Java DSL is not supported on the route scope

[CAMEL-20751](https://issues.apache.org/jira/browse/CAMEL-20751)

camel-spring-xml - Add back <camel> to XSD

[CAMEL-20722](https://issues.apache.org/jira/browse/CAMEL-20722)

camel-kafka: reduce KafkaBreakOnFirstError tests are too unreliable for CIs

[CAMEL-20680](https://issues.apache.org/jira/browse/CAMEL-20680)

camel-kafka: reduce KafkaBreakOnFirstErrorSeekIssueIT test duration

[CAMEL-20648](https://issues.apache.org/jira/browse/CAMEL-20648)

Example for spring-boot-infinispan should update infinispan

[CAMEL-20634](https://issues.apache.org/jira/browse/CAMEL-20634)

Create a centralized variable for the header name CamelLangChain4jEmbeddingsVector

[CAMEL-20585](https://issues.apache.org/jira/browse/CAMEL-20585)

Camel-package-maven-plugin: generates test configurers in non-tests artifacts

[CAMEL-20414](https://issues.apache.org/jira/browse/CAMEL-20414)

Add CloudEvent Transformers to cloud oriented component

[CAMEL-20309](https://issues.apache.org/jira/browse/CAMEL-20309)

olingo2 build error using \`/component-test\` on CI

[CAMEL-19659](https://issues.apache.org/jira/browse/CAMEL-19659)

camel-fhir: slow tests

[CAMEL-19546](https://issues.apache.org/jira/browse/CAMEL-19546)

camel-tarfile: replace Thread.sleep in tests

[CAMEL-19544](https://issues.apache.org/jira/browse/CAMEL-19544)

camel-sql: replace Thread.sleep in tests

[CAMEL-19523](https://issues.apache.org/jira/browse/CAMEL-19523)

camel-iec60870: replace Thread.sleep in tests

[CAMEL-19228](https://issues.apache.org/jira/browse/CAMEL-19228)

camel-couchbase: Integration tests are unstable with Couchbase 7

[CAMEL-16364](https://issues.apache.org/jira/browse/CAMEL-16364)

Camel-tracing: Add more decorators

### Test (3)

[CAMEL-20943](https://issues.apache.org/jira/browse/CAMEL-20943)

camel-jbang - Add openapi generate integration test

[CAMEL-20215](https://issues.apache.org/jira/browse/CAMEL-20215)

camel-mllp - MllpTcpServerConsumerOptionalEndOfDataWithValidationTest.testMessageWithoutEndOfDataByte is failing on JDK21

[CAMEL-19639](https://issues.apache.org/jira/browse/CAMEL-19639)

camel-etc3 - Etcd3RoutePolicyIT is failing

### Wish (1)

[CAMEL-20894](https://issues.apache.org/jira/browse/CAMEL-20894)

EventNotifier: Not all steps are triggered as events

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).