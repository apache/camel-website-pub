# Apache camel 3.11.0 Release

## New and Noteworthy

This release is the new Camel 3.11.0 LTS minor release.

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
      <version>3.11.0</version>
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
      <version>3.11.0</version>
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
| [apache-camel-3.11.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.0/apache-camel-3.11.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.0/apache-camel-3.11.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.0/apache-camel-3.11.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (26)

[CAMEL-16761](https://issues.apache.org/jira/browse/CAMEL-16761)

camel-sql - auto-generated primary keys are not retuned for Postgres when using loop iteration

[CAMEL-16741](https://issues.apache.org/jira/browse/CAMEL-16741)

camel-yaml-dsl - Yaml schema validation error for rest endpoints

[CAMEL-16734](https://issues.apache.org/jira/browse/CAMEL-16734)

Recipient list does not wait for processing an exchange by recipients and ignores aggregation strategy when route is transacted.

[CAMEL-16722](https://issues.apache.org/jira/browse/CAMEL-16722)

camel-mock - In predicate should be one predicate

[CAMEL-16718](https://issues.apache.org/jira/browse/CAMEL-16718)

Conflict with Netty TCP + Resilience4J circuit breaker

[CAMEL-16716](https://issues.apache.org/jira/browse/CAMEL-16716)

camel-mongodb streamFilter component option not honored

[CAMEL-16715](https://issues.apache.org/jira/browse/CAMEL-16715)

ZipkinServerResponseAdapter#onResponse possible NullPointerException

[CAMEL-16707](https://issues.apache.org/jira/browse/CAMEL-16707)

camel-rabbitmq connection leak on error during 'declare'

[CAMEL-16705](https://issues.apache.org/jira/browse/CAMEL-16705)

camel-spring-boot - Changing LoggingLevel for Camel Log at runtime

[CAMEL-16701](https://issues.apache.org/jira/browse/CAMEL-16701)

Topic is not set if a KafkaConfiguration is used

[CAMEL-16682](https://issues.apache.org/jira/browse/CAMEL-16682)

camel-mock - ConcurrentModificationException when asserting mock endpoints

[CAMEL-16681](https://issues.apache.org/jira/browse/CAMEL-16681)

LazyStartProducer can result in NullPointerException in a multithreaded context

[CAMEL-16670](https://issues.apache.org/jira/browse/CAMEL-16670)

Camel Component & Package Maven Plugins fail on some JSON resource files

[CAMEL-16662](https://issues.apache.org/jira/browse/CAMEL-16662)

camel-spring-boot - Classloader cannot find xml route files inside spring boots proprietary layout

[CAMEL-16661](https://issues.apache.org/jira/browse/CAMEL-16661)

camel-spring-boot - XML example logs Camel is started many times

[CAMEL-16659](https://issues.apache.org/jira/browse/CAMEL-16659)

camel-core - Simple language parses minus sign (-) as a numeric value instead of a string value

[CAMEL-16658](https://issues.apache.org/jira/browse/CAMEL-16658)

AmbiguousMethodCallException when using Mockito mock as bean for camel-bean component.

[CAMEL-16657](https://issues.apache.org/jira/browse/CAMEL-16657)

camel-ftp - fileExists=Append and no file already exists

[CAMEL-16640](https://issues.apache.org/jira/browse/CAMEL-16640)

camel-kafka race conditions during shut down

[CAMEL-16634](https://issues.apache.org/jira/browse/CAMEL-16634)

karaf - Errors installing Karaf features after camel-kafka installation

[CAMEL-16632](https://issues.apache.org/jira/browse/CAMEL-16632)

camel-salesforce - NPE On Processing Composite Collections Response

[CAMEL-16629](https://issues.apache.org/jira/browse/CAMEL-16629)

camel-core - InterceptSendToEndpoint - AfterUri should only trigger if when was true

[CAMEL-16622](https://issues.apache.org/jira/browse/CAMEL-16622)

Validator component fails with java.lang.IllegalArgumentException: protocol = https host = null

[CAMEL-16532](https://issues.apache.org/jira/browse/CAMEL-16532)

CXFConsumer unexpectedly unregistered

[CAMEL-16509](https://issues.apache.org/jira/browse/CAMEL-16509)

Incorrect span timing information reported by camel-zipkin when using parallel processing with multicast/recipientList

[CAMEL-16263](https://issues.apache.org/jira/browse/CAMEL-16263)

camel-google-pubsub - Consumer does not recover from 500 series error from Google

### Dependency upgrade (6)

[CAMEL-16702](https://issues.apache.org/jira/browse/CAMEL-16702)

camel-grpc - Upgrade to 1.38

[CAMEL-16697](https://issues.apache.org/jira/browse/CAMEL-16697)

Upgrade to CXF 3.4.4

[CAMEL-16676](https://issues.apache.org/jira/browse/CAMEL-16676)

camel-yaml-dsl - Upgrade to snakeyaml 2.3

[CAMEL-16647](https://issues.apache.org/jira/browse/CAMEL-16647)

camel-spring-boot - Upgrade to Spring Boot 2.5.0

[CAMEL-16637](https://issues.apache.org/jira/browse/CAMEL-16637)

Camel-DJL: Upgrade to Deep Java Library 0.11.0

[CAMEL-16437](https://issues.apache.org/jira/browse/CAMEL-16437)

camel-opentelemetry - Upgrade to 1.0.x

### Improvement (44)

[CAMEL-16745](https://issues.apache.org/jira/browse/CAMEL-16745)

camel-ftp - excludeExt/includeExt not getting the right filename extension

[CAMEL-16744](https://issues.apache.org/jira/browse/CAMEL-16744)

camel-core - RemoveHeader EIP uses headerName

[CAMEL-16740](https://issues.apache.org/jira/browse/CAMEL-16740)

Camel-avro-rpc allow change of http server implementation using SPI

[CAMEL-16736](https://issues.apache.org/jira/browse/CAMEL-16736)

Preserve CSV headers when collected during Unmarshalling to List

[CAMEL-16733](https://issues.apache.org/jira/browse/CAMEL-16733)

Calling bean method by type results in creation of new bean rather using an existing one from the registry

[CAMEL-16732](https://issues.apache.org/jira/browse/CAMEL-16732)

camel-sql - DataSource should be autowired

[CAMEL-16730](https://issues.apache.org/jira/browse/CAMEL-16730)

openapi generator - Allow to specify the to endpoint

[CAMEL-16727](https://issues.apache.org/jira/browse/CAMEL-16727)

Camel-AWS2 S3: Add an ignoreBody option

[CAMEL-16724](https://issues.apache.org/jira/browse/CAMEL-16724)

camel-mock - Add option to log when a message is received

[CAMEL-16719](https://issues.apache.org/jira/browse/CAMEL-16719)

camel-kafka - Add option to configure group instance id

[CAMEL-16713](https://issues.apache.org/jira/browse/CAMEL-16713)

camel-core - Route template local bean should better report error if invalid syntax

[CAMEL-16711](https://issues.apache.org/jira/browse/CAMEL-16711)

components - Move OSGi dependenct code to camel-karaf

[CAMEL-16709](https://issues.apache.org/jira/browse/CAMEL-16709)

camel-core - camel resource handling of windows file uri problem

[CAMEL-16708](https://issues.apache.org/jira/browse/CAMEL-16708)

camel-pubnub - Allow to configure security on component level

[CAMEL-16700](https://issues.apache.org/jira/browse/CAMEL-16700)

main: allow to configure global options through properties

[CAMEL-16695](https://issues.apache.org/jira/browse/CAMEL-16695)

camel-core - Properties placeholder - Add support for negate boolean answer

[CAMEL-16693](https://issues.apache.org/jira/browse/CAMEL-16693)

yaml dsl: make YamlDeserializationMode.FLOW as default deserialization mode

[CAMEL-16689](https://issues.apache.org/jira/browse/CAMEL-16689)

camel-core - Lazy start producer should re-create in case it failed to create or start the producer

[CAMEL-16687](https://issues.apache.org/jira/browse/CAMEL-16687)

deliveryTimeoutMs cannot be set in camel-kafka configuration

[CAMEL-16685](https://issues.apache.org/jira/browse/CAMEL-16685)

camel-openapi-restdsl-generator - Split generated route builder into smaller code blocks

[CAMEL-16683](https://issues.apache.org/jira/browse/CAMEL-16683)

camel-jackson - Reduce logging noise for autoDiscoverObjectMapper

[CAMEL-16677](https://issues.apache.org/jira/browse/CAMEL-16677)

Move vertx component SSL configuration logic to camel-vertx-common

[CAMEL-16672](https://issues.apache.org/jira/browse/CAMEL-16672)

SimpleBuilder - Resolve property placeholder on expression text

[CAMEL-16671](https://issues.apache.org/jira/browse/CAMEL-16671)

camel-maven-plugin - Detect if kamelet-main is on classpath and use KameletMain as main class

[CAMEL-16669](https://issues.apache.org/jira/browse/CAMEL-16669)

website - Add EOL column to download page

[CAMEL-16664](https://issues.apache.org/jira/browse/CAMEL-16664)

camel-core - XML routes loader allow to not have root namespace defined

[CAMEL-16663](https://issues.apache.org/jira/browse/CAMEL-16663)

camel-file - excludeExt does not work if file has multiple extensions

[CAMEL-16650](https://issues.apache.org/jira/browse/CAMEL-16650)

kamelets: allow to set the location of kamelets

[CAMEL-16644](https://issues.apache.org/jira/browse/CAMEL-16644)

camel-consul - Spring Boot auto configuration camel.cloud.consul.service-registry

[CAMEL-16643](https://issues.apache.org/jira/browse/CAMEL-16643)

camel-saxon: Remove the dependency to xslt-saxon

[CAMEL-16641](https://issues.apache.org/jira/browse/CAMEL-16641)

AWS-Translate: List all the available languages in the enum

[CAMEL-16636](https://issues.apache.org/jira/browse/CAMEL-16636)

camel-core - kamelet auto discovery should log nicer error if not found

[CAMEL-16635](https://issues.apache.org/jira/browse/CAMEL-16635)

camel-main - The default routes include pattern is only for xml files

[CAMEL-16625](https://issues.apache.org/jira/browse/CAMEL-16625)

camel-core - ResourceEndpoint use Resource API

[CAMEL-16623](https://issues.apache.org/jira/browse/CAMEL-16623)

camel-jackson - The option autoDiscoverObjectMapper is set to false, Camel won't search in the registry

[CAMEL-16619](https://issues.apache.org/jira/browse/CAMEL-16619)

camel-rabbitmq - Producer destroys rabbit channels when returns it back to the pool

[CAMEL-16618](https://issues.apache.org/jira/browse/CAMEL-16618)

camel-spring-boot - No CamelContext defined yet so cannot inject into bean

[CAMEL-16542](https://issues.apache.org/jira/browse/CAMEL-16542)

Camel-Solr: Refactoring the component a bit

[CAMEL-16537](https://issues.apache.org/jira/browse/CAMEL-16537)

camel-mongodb: Allow to connect using credentails/connectionString

[CAMEL-16482](https://issues.apache.org/jira/browse/CAMEL-16482)

camel-hazelcast: add getAll for HazelcastListProducer and HazelcastSetProducer

[CAMEL-16468](https://issues.apache.org/jira/browse/CAMEL-16468)

camel-jbpm - Expose org.apache.camel.component.jbpm.JBPMProducer.Operation

[CAMEL-16404](https://issues.apache.org/jira/browse/CAMEL-16404)

camel-core - Move route templates into RouteTemplateBuilder

[CAMEL-16381](https://issues.apache.org/jira/browse/CAMEL-16381)

camel-dependencies - Move OSGi dependencies to camel-karaf

[CAMEL-13095](https://issues.apache.org/jira/browse/CAMEL-13095)

Salesforce component documentation - unclear about queryAll

### New Feature (10)

[CAMEL-16726](https://issues.apache.org/jira/browse/CAMEL-16726)

openapi generator: generate YAML DSL

[CAMEL-16717](https://issues.apache.org/jira/browse/CAMEL-16717)

Camel Component // Huawei Cloud IAM Component

[CAMEL-16674](https://issues.apache.org/jira/browse/CAMEL-16674)

Camel component // Huawei Cloud FunctionGraph Component

[CAMEL-16645](https://issues.apache.org/jira/browse/CAMEL-16645)

ResourceLoader to load from github

[CAMEL-16627](https://issues.apache.org/jira/browse/CAMEL-16627)

camel-core - Add common header for source timestamp

[CAMEL-16611](https://issues.apache.org/jira/browse/CAMEL-16611)

camel-smpp: Export JSMPP's pduProcessorDegree and queueCapacity to SmppConfiguration

[CAMEL-16585](https://issues.apache.org/jira/browse/CAMEL-16585)

camel-kamelet - Main class to easily bootstrap Camel with Kamelets

[CAMEL-16549](https://issues.apache.org/jira/browse/CAMEL-16549)

Create a test-infra module for Solr

[CAMEL-16390](https://issues.apache.org/jira/browse/CAMEL-16390)

camel-salesforce: Add raw operation

[CAMEL-16134](https://issues.apache.org/jira/browse/CAMEL-16134)

camel-smpp - Registered delivery flag on 1 of N segments of a long SMS

### Task (16)

[CAMEL-16735](https://issues.apache.org/jira/browse/CAMEL-16735)

camel-maven-plugin - run goal seems broken

[CAMEL-16731](https://issues.apache.org/jira/browse/CAMEL-16731)

False positive validation error for dataSource attribute when not using the # notation

[CAMEL-16723](https://issues.apache.org/jira/browse/CAMEL-16723)

Camel Huawei components catalog report warning

[CAMEL-16720](https://issues.apache.org/jira/browse/CAMEL-16720)

camel-aws - Component title - remove the using AWS SDK version 2.x.

[CAMEL-16686](https://issues.apache.org/jira/browse/CAMEL-16686)

camel-website - Asciidoc ERROR/WARN during build

[CAMEL-16684](https://issues.apache.org/jira/browse/CAMEL-16684)

camel-aws2-ddb streams has empty usage section in documentation

[CAMEL-16679](https://issues.apache.org/jira/browse/CAMEL-16679)

Upgrade to the latest MicroProfile component releases

[CAMEL-16678](https://issues.apache.org/jira/browse/CAMEL-16678)

Upgrade Vert.x to 4.1.0

[CAMEL-16675](https://issues.apache.org/jira/browse/CAMEL-16675)

camel-jsonpath - Add back to karaf feature

[CAMEL-16673](https://issues.apache.org/jira/browse/CAMEL-16673)

camel-maven-plugin - Move OSGi to its own camel-blueprint-maven-plugin

[CAMEL-16668](https://issues.apache.org/jira/browse/CAMEL-16668)

camel-dozer has conflicting OSGi javax.el bundles

[CAMEL-16654](https://issues.apache.org/jira/browse/CAMEL-16654)

camel-spring-boot - camel-jpa test error after 2.5 upgrade

[CAMEL-16519](https://issues.apache.org/jira/browse/CAMEL-16519)

Remove Camel-APNS

[CAMEL-16465](https://issues.apache.org/jira/browse/CAMEL-16465)

Camel-AWS: Add useDefaultCredentialProvider option to all the components

[CAMEL-16256](https://issues.apache.org/jira/browse/CAMEL-16256)

https://github.com/apache/camel-examples/tree/master/examples/camel-example-spring-ws doesn't run

[CAMEL-16198](https://issues.apache.org/jira/browse/CAMEL-16198)

camel-flatpack - Does not compile on JDK 16

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).