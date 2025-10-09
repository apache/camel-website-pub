# Apache camel 2.23.2 Release

## New and Noteworthy

This release is a minor update of the 2.23.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.23.2</version>
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
      <version>2.23.2</version>
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
| [apache-camel-2.23.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.23.2/apache-camel-2.23.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.23.2/apache-camel-2.23.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.23.2/apache-camel-2.23.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.23.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.23.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (47)

[CAMEL-13410](https://issues.apache.org/jira/browse/CAMEL-13410)

Fix syntax for service component

[CAMEL-13388](https://issues.apache.org/jira/browse/CAMEL-13388)

Wrong removing parameters logic in ServiceComponent.

[CAMEL-13387](https://issues.apache.org/jira/browse/CAMEL-13387)

camel-twitter-direct-message doesn't filter by filterOld parameter

[CAMEL-13368](https://issues.apache.org/jira/browse/CAMEL-13368)

LevelDB NPE if persistentFileName has no paths in LevelDBAggregationRepository

[CAMEL-13366](https://issues.apache.org/jira/browse/CAMEL-13366)

MLLP Endpoint 'maxConcurrentConsumers' configuration support

[CAMEL-13357](https://issues.apache.org/jira/browse/CAMEL-13357)

Regression - Namespaces defined on the SOAP envelope get lost in PAYLOAD mode

[CAMEL-13355](https://issues.apache.org/jira/browse/CAMEL-13355)

MLLP Component 'maxConcurrentConsumers' configuration is ignored

[CAMEL-13351](https://issues.apache.org/jira/browse/CAMEL-13351)

camel-netty4-http: error resolving relative path

[CAMEL-13340](https://issues.apache.org/jira/browse/CAMEL-13340)

Invalid swagger json/yaml generated for Rest DSL

[CAMEL-13339](https://issues.apache.org/jira/browse/CAMEL-13339)

Partition revoke implemented to save offset state using KafkaConsumer.position API results in message loss

[CAMEL-13338](https://issues.apache.org/jira/browse/CAMEL-13338)

ConsumerRebalanceListener is not registered when topicIsPattern is turned off. Causing message loss or too many duplicates

[CAMEL-13330](https://issues.apache.org/jira/browse/CAMEL-13330)

Camel JBPM WID definitions contain incorrect WIH classname

[CAMEL-13321](https://issues.apache.org/jira/browse/CAMEL-13321)

camel-twitter-direct-message doesn't use default delay of 30s

[CAMEL-13320](https://issues.apache.org/jira/browse/CAMEL-13320)

DirectMessageConsumerHandler.java \[4\] pollConsume method calls Twitter.getDirectMessages(getLastIdPaging())

[CAMEL-13319](https://issues.apache.org/jira/browse/CAMEL-13319)

TwitterConverter calls deprecated getSenderScreenName, throws UnsupportedOperationException

[CAMEL-13305](https://issues.apache.org/jira/browse/CAMEL-13305)

camel-sql cannot resolve nested simple expression

[CAMEL-13304](https://issues.apache.org/jira/browse/CAMEL-13304)

Camel Bindy Tab delimited - Handling Blank Values

[CAMEL-13249](https://issues.apache.org/jira/browse/CAMEL-13249)

Header filtering in HTTP producers from RestProducerFactory filters IN instead of OUT headers

[CAMEL-13241](https://issues.apache.org/jira/browse/CAMEL-13241)

Missing backport-util-concurrent-version property defined in the parent pom.xml

[CAMEL-13236](https://issues.apache.org/jira/browse/CAMEL-13236)

mock endpoint - Small glitch in logging excepted failure

[CAMEL-13230](https://issues.apache.org/jira/browse/CAMEL-13230)

Error starting SQS consumer due to config option missing that's required for producer only

[CAMEL-13211](https://issues.apache.org/jira/browse/CAMEL-13211)

SMPP: Host, port and systemid component configuration is always overridden by URI configuration

[CAMEL-13191](https://issues.apache.org/jira/browse/CAMEL-13191)

URISupport sanitizeUri don't hide complete password if password contains colon

[CAMEL-13179](https://issues.apache.org/jira/browse/CAMEL-13179)

camel-linkedin - IllegalArgumentException: Error authorizing application during linkedin authentication

[CAMEL-13171](https://issues.apache.org/jira/browse/CAMEL-13171)

camel-restdsl-swagger xml generation can't find required method allowableValues(String)

[CAMEL-13168](https://issues.apache.org/jira/browse/CAMEL-13168)

Underlying File for StreamCache gets deleted too early with direct-vm

[CAMEL-13166](https://issues.apache.org/jira/browse/CAMEL-13166)

ArrayBlockingQueueFactory ignores capacity argument

[CAMEL-13162](https://issues.apache.org/jira/browse/CAMEL-13162)

Unknown parameter issue on weaving from-with on a REST-DSL route

[CAMEL-13154](https://issues.apache.org/jira/browse/CAMEL-13154)

camel-example-spring-boot-master running error

[CAMEL-13152](https://issues.apache.org/jira/browse/CAMEL-13152)

Camel-JBPM KIE-Server extension should use KJAR project classloaded in deployment-scoped CamelContext

[CAMEL-13140](https://issues.apache.org/jira/browse/CAMEL-13140)

camel-kafka - consumer does not respect auto.commit.interval.ms with AutoCommitEnabled=true

[CAMEL-13132](https://issues.apache.org/jira/browse/CAMEL-13132)

uploadBlobBlocks and commitBlobBlockList operations does not work with List

[CAMEL-13125](https://issues.apache.org/jira/browse/CAMEL-13125)

Camel-MongoDB: Endpoint shutdown closes mongo connection, killing the connection for everyone

[CAMEL-13123](https://issues.apache.org/jira/browse/CAMEL-13123)

Endpoint shutdown closes mongo connection, killing the connection for everyone

[CAMEL-13098](https://issues.apache.org/jira/browse/CAMEL-13098)

Camel-google-mail: Stream component doesn't work in OSGi

[CAMEL-13097](https://issues.apache.org/jira/browse/CAMEL-13097)

Camel-google-calendar: Stream component doesn't work in OSGi

[CAMEL-13093](https://issues.apache.org/jira/browse/CAMEL-13093)

Output of route-profile is empty if there are same route-id for multiple camel-contexts.

[CAMEL-13084](https://issues.apache.org/jira/browse/CAMEL-13084)

javax.servlet.http.MappingMatch not found when starting camel-example-spring-boot

[CAMEL-13077](https://issues.apache.org/jira/browse/CAMEL-13077)

Olingo4 Consumer appears to not work with backoffIdleThreshold

[CAMEL-13063](https://issues.apache.org/jira/browse/CAMEL-13063)

Olingo2Endpoint swallowing consumer. options

[CAMEL-13062](https://issues.apache.org/jira/browse/CAMEL-13062)

olingo2 component serviceUri not set

[CAMEL-13061](https://issues.apache.org/jira/browse/CAMEL-13061)

Missing properties on Olingo2 consumer initialisation

[CAMEL-13059](https://issues.apache.org/jira/browse/CAMEL-13059)

camel-olingo2 assumes '/' at end of URI

[CAMEL-13058](https://issues.apache.org/jira/browse/CAMEL-13058)

AbstractFutureCallback generates NPE when response is a 401

[CAMEL-13054](https://issues.apache.org/jira/browse/CAMEL-13054)

Olingo4Endpoint swallowing consumer. options

[CAMEL-13037](https://issues.apache.org/jira/browse/CAMEL-13037)

camel-cxfrs - SimpleBinding ignores annotations on interface

[CAMEL-12948](https://issues.apache.org/jira/browse/CAMEL-12948)

Camel-Box: Download file version

### Improvement (7)

[CAMEL-13352](https://issues.apache.org/jira/browse/CAMEL-13352)

Update document of HostAddresses

[CAMEL-13344](https://issues.apache.org/jira/browse/CAMEL-13344)

camel-sql - stored procedure loaded from file/classpath should skip comment lines

[CAMEL-13155](https://issues.apache.org/jira/browse/CAMEL-13155)

Add WidProcessor and Assembly configuration to Maven build to enable integration of WIH with jBPM Service Repository

[CAMEL-13150](https://issues.apache.org/jira/browse/CAMEL-13150)

Add command "exchangeProperty" for dateExpression in ExpressionBuilder

[CAMEL-13114](https://issues.apache.org/jira/browse/CAMEL-13114)

Provide single Cookie header for multiple cookies

[CAMEL-13072](https://issues.apache.org/jira/browse/CAMEL-13072)

In DefaultUnitOfWork:popRouteContext() avoid exception thrown

[CAMEL-13066](https://issues.apache.org/jira/browse/CAMEL-13066)

camel-hystrix - Do not fallback on HystrixBadRequestException

### Task (5)

[CAMEL-13348](https://issues.apache.org/jira/browse/CAMEL-13348)

Camel elasticsearch support search without specifying the indexName and indexType

[CAMEL-13263](https://issues.apache.org/jira/browse/CAMEL-13263)

Lenient IPFS connection check on startup

[CAMEL-13173](https://issues.apache.org/jira/browse/CAMEL-13173)

\[IPFS\] Remove transitive dependency on bitcoin and cipher

[CAMEL-13169](https://issues.apache.org/jira/browse/CAMEL-13169)

c3p0 dependent version (0.9.5.2) has a security vulnerability (CVE-2018-20433)

[CAMEL-13153](https://issues.apache.org/jira/browse/CAMEL-13153)

camel-mail - Strip newlines from exchange headers

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).