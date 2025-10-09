# Apache camel 2.24.0 Release

## New and Noteworthy

This release is a minor update of the 2.24.x branch.

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
      <version>2.24.0</version>
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
      <version>2.24.0</version>
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
| [apache-camel-2.24.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.24.0/apache-camel-2.24.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.24.0/apache-camel-2.24.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.24.0/apache-camel-2.24.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.24.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.24.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (86)

[CAMEL-13496](https://issues.apache.org/jira/browse/CAMEL-13496)

maven-invoker-plugin taking as much heapspace as the Maven itself

[CAMEL-13489](https://issues.apache.org/jira/browse/CAMEL-13489)

camel-undertow: consumer thrown NPE when the body cannot be converted to ByteBuffer

[CAMEL-13477](https://issues.apache.org/jira/browse/CAMEL-13477)

KafkaConfiguration puts truststore password into keystore password property

[CAMEL-13468](https://issues.apache.org/jira/browse/CAMEL-13468)

Exception tag is missing when Camel Java DSL is converted into XML using dumpRouteAsXml() operation

[CAMEL-13464](https://issues.apache.org/jira/browse/CAMEL-13464)

Problem with Olingo4 and authenticated metadata

[CAMEL-13438](https://issues.apache.org/jira/browse/CAMEL-13438)

Camel jBPM WorkItemHandler should allow passthrough of Exceptions

[CAMEL-13437](https://issues.apache.org/jira/browse/CAMEL-13437)

ThrowExceptionProcessor should use 'getConstructor' instead of 'getDeclaredConstructor', so it doesn't force users to implement the constructors of their exception classes.

[CAMEL-13433](https://issues.apache.org/jira/browse/CAMEL-13433)

S3: Exchange body stream is loaded into memory to calculate content length which is already set via headers

[CAMEL-13428](https://issues.apache.org/jira/browse/CAMEL-13428)

camel-undertow - Response with large data gets truncated on cloud

[CAMEL-13410](https://issues.apache.org/jira/browse/CAMEL-13410)

Fix syntax for service component

[CAMEL-13409](https://issues.apache.org/jira/browse/CAMEL-13409)

Fix syntax for nsq component

[CAMEL-13397](https://issues.apache.org/jira/browse/CAMEL-13397)

RedisStringIdempotentRepository resetting expiry on existing keys

[CAMEL-13396](https://issues.apache.org/jira/browse/CAMEL-13396)

camel-leveldb can no longer use non-native leveldb libraries

[CAMEL-13388](https://issues.apache.org/jira/browse/CAMEL-13388)

Wrong removing parameters logic in ServiceComponent.

[CAMEL-13387](https://issues.apache.org/jira/browse/CAMEL-13387)

camel-twitter-direct-message doesn't filter by filterOld parameter

[CAMEL-13368](https://issues.apache.org/jira/browse/CAMEL-13368)

LevelDB NPE if persistentFileName has no paths in LevelDBAggregationRepository

[CAMEL-13366](https://issues.apache.org/jira/browse/CAMEL-13366)

MLLP Endpoint 'maxConcurrentConsumers' configuration support

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

[CAMEL-13282](https://issues.apache.org/jira/browse/CAMEL-13282)

Can't use validation of JaxbDataFormat of non Root JAXB Elements

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

[CAMEL-13176](https://issues.apache.org/jira/browse/CAMEL-13176)

camel yammer component is accessing non-existent page

[CAMEL-13171](https://issues.apache.org/jira/browse/CAMEL-13171)

camel-restdsl-swagger xml generation can't find required method allowableValues(String)

[CAMEL-13168](https://issues.apache.org/jira/browse/CAMEL-13168)

Underlying File for StreamCache gets deleted too early with direct-vm

[CAMEL-13166](https://issues.apache.org/jira/browse/CAMEL-13166)

ArrayBlockingQueueFactory ignores capacity argument

[CAMEL-13162](https://issues.apache.org/jira/browse/CAMEL-13162)

Unknown parameter issue on weaving from-with on a REST-DSL route

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

[CAMEL-13049](https://issues.apache.org/jira/browse/CAMEL-13049)

Karaf commands that start/resume contexts and routes should use proper TCCL

[CAMEL-13045](https://issues.apache.org/jira/browse/CAMEL-13045)

Camel-Slack: The verifier must be able to validate webhook and token at the same time

[CAMEL-13044](https://issues.apache.org/jira/browse/CAMEL-13044)

Camel-AWS MQ: it is not possible to set Broker "Public accessibility" parameter using createBroker command

[CAMEL-13037](https://issues.apache.org/jira/browse/CAMEL-13037)

camel-cxfrs - SimpleBinding ignores annotations on interface

[CAMEL-13028](https://issues.apache.org/jira/browse/CAMEL-13028)

camel-undertow - When using SSL with rest-dsl and api-doc then you can get a port already bound exception

[CAMEL-13022](https://issues.apache.org/jira/browse/CAMEL-13022)

camel-restlet - sending PATCH operation should include body

[CAMEL-13017](https://issues.apache.org/jira/browse/CAMEL-13017)

root-Path handling for SFTP on windows bug

[CAMEL-13016](https://issues.apache.org/jira/browse/CAMEL-13016)

camel-jetty - If multiple bundles uses the same context-path (pathspec) then Jetty should fail

[CAMEL-13014](https://issues.apache.org/jira/browse/CAMEL-13014)

camel mqtt crash using high volume traffic

[CAMEL-13012](https://issues.apache.org/jira/browse/CAMEL-13012)

camel-olingo4 - AbstractFutureCallback generates NPE when response is a 401

[CAMEL-13009](https://issues.apache.org/jira/browse/CAMEL-13009)

Error in generated XAdES 1.1.1 signature

[CAMEL-13008](https://issues.apache.org/jira/browse/CAMEL-13008)

Odata-connector assumes '/' at end of URI

[CAMEL-13006](https://issues.apache.org/jira/browse/CAMEL-13006)

Missing properties on Olingo4 consumer initialisation

[CAMEL-13005](https://issues.apache.org/jira/browse/CAMEL-13005)

olingo4 component serviceUri not set

[CAMEL-12999](https://issues.apache.org/jira/browse/CAMEL-12999)

Example documentation and feature not using new bundle artifactId

[CAMEL-12994](https://issues.apache.org/jira/browse/CAMEL-12994)

xquery syntax problem in SpringDSL with spring-boot

[CAMEL-12991](https://issues.apache.org/jira/browse/CAMEL-12991)

SftpEndpoint does not allow to use custom process strategy

[CAMEL-12987](https://issues.apache.org/jira/browse/CAMEL-12987)

camel-core-osgi: OsgiServiceRegistry.onContextStop never gets called.

[CAMEL-12985](https://issues.apache.org/jira/browse/CAMEL-12985)

TransactionErrorHandler fails if UnitOfWork is null -- This seems to happen sometimes with intercepted routes

[CAMEL-12980](https://issues.apache.org/jira/browse/CAMEL-12980)

Bundle in 'Active' State but Camel Context not initialized

[CAMEL-12974](https://issues.apache.org/jira/browse/CAMEL-12974)

Route coverage: When and otherwise are not marked as covered

[CAMEL-12973](https://issues.apache.org/jira/browse/CAMEL-12973)

AbstractCamelWorkItemHandler init fails when WIH is loaded before CamelContext is created.

[CAMEL-12969](https://issues.apache.org/jira/browse/CAMEL-12969)

camel-core-osgi: Slow Memory Leak in OsgiServiceRegistry

[CAMEL-12963](https://issues.apache.org/jira/browse/CAMEL-12963)

camel-salesforce-maven-plugin generates code that does not compile

[CAMEL-12958](https://issues.apache.org/jira/browse/CAMEL-12958)

Wrong camel context bound in service registry of jbpm/Kie Server

[CAMEL-12952](https://issues.apache.org/jira/browse/CAMEL-12952)

Camel-AHC-WS: does not send response to ping frame

[CAMEL-12951](https://issues.apache.org/jira/browse/CAMEL-12951)

Camel-AHC-WS: reconnect exception is not passed to exception handler

[CAMEL-12948](https://issues.apache.org/jira/browse/CAMEL-12948)

Camel-Box: Download file version

[CAMEL-12947](https://issues.apache.org/jira/browse/CAMEL-12947)

MockEndpoint.expectedHeaderReceived should fail when no exchange received

### Improvement (26)

[CAMEL-13481](https://issues.apache.org/jira/browse/CAMEL-13481)

Upgrade to shiro 1.4.1

[CAMEL-13352](https://issues.apache.org/jira/browse/CAMEL-13352)

Update document of HostAddresses

[CAMEL-13344](https://issues.apache.org/jira/browse/CAMEL-13344)

camel-sql - stored procedure loaded from file/classpath should skip comment lines

[CAMEL-13210](https://issues.apache.org/jira/browse/CAMEL-13210)

camel-test-spring - Add support for @ExcludeRoutes annotation when testing spring boot

[CAMEL-13186](https://issues.apache.org/jira/browse/CAMEL-13186)

camel-salesforce-maven-plugin additional customizations missing

[CAMEL-13185](https://issues.apache.org/jira/browse/CAMEL-13185)

Implement Olingo4 Consumer splitResults function

[CAMEL-13155](https://issues.apache.org/jira/browse/CAMEL-13155)

Add WidProcessor and Assembly configuration to Maven build to enable integration of WIH with jBPM Service Repository

[CAMEL-13150](https://issues.apache.org/jira/browse/CAMEL-13150)

Add command "exchangeProperty" for dateExpression in ExpressionBuilder

[CAMEL-13126](https://issues.apache.org/jira/browse/CAMEL-13126)

For Swagger, add an option whether to use X-Forward headers

[CAMEL-13120](https://issues.apache.org/jira/browse/CAMEL-13120)

camel-spring-boot - Add detailed option to turn on|off showing camel version etc

[CAMEL-13114](https://issues.apache.org/jira/browse/CAMEL-13114)

Provide single Cookie header for multiple cookies

[CAMEL-13072](https://issues.apache.org/jira/browse/CAMEL-13072)

In DefaultUnitOfWork:popRouteContext() avoid exception thrown

[CAMEL-13066](https://issues.apache.org/jira/browse/CAMEL-13066)

camel-hystrix - Do not fallback on HystrixBadRequestException

[CAMEL-13042](https://issues.apache.org/jira/browse/CAMEL-13042)

camel-core - File producer should by default not allow writing files to directories outside its starting directory

[CAMEL-13035](https://issues.apache.org/jira/browse/CAMEL-13035)

Camel telegram - Update made to channel not received by camel application

[CAMEL-13029](https://issues.apache.org/jira/browse/CAMEL-13029)

camel-swagger-java - Should default use scheme from rest-dsl configuration in swagger doc

[CAMEL-13025](https://issues.apache.org/jira/browse/CAMEL-13025)

camel-core - File read lock changed - If file gets deleted then break out loop

[CAMEL-13001](https://issues.apache.org/jira/browse/CAMEL-13001)

Route coverage: specify coverage to fail on

[CAMEL-12993](https://issues.apache.org/jira/browse/CAMEL-12993)

Have more informative message from springboot itests exceptions

[CAMEL-12979](https://issues.apache.org/jira/browse/CAMEL-12979)

Service beans with custom lifecycle on CxfRsEndpoint

[CAMEL-12978](https://issues.apache.org/jira/browse/CAMEL-12978)

Add support to configure CamelContext created by KIE-Server extension

[CAMEL-12967](https://issues.apache.org/jira/browse/CAMEL-12967)

Google sheets: Split value range result stream to separate exchanges per row

[CAMEL-12944](https://issues.apache.org/jira/browse/CAMEL-12944)

camel-ribbon : Avoid potentially conflicting jetty port during test execution

[CAMEL-12935](https://issues.apache.org/jira/browse/CAMEL-12935)

Camel Context restarts in Blueprint Test if isCreateCamelContextPerClass is set to true

[CAMEL-12919](https://issues.apache.org/jira/browse/CAMEL-12919)

Camel AWS-SQS: Creating Amazon SQS Queue with Server-Side Encryption

[CAMEL-12213](https://issues.apache.org/jira/browse/CAMEL-12213)

Update camel-thrift to libthrift 0.12.0

### New Feature (15)

[CAMEL-13345](https://issues.apache.org/jira/browse/CAMEL-13345)

route-coverage : Add option to generate a jacoco XML report

[CAMEL-13255](https://issues.apache.org/jira/browse/CAMEL-13255)

camel-spring-redis: Support for redis GEO-related functions

[CAMEL-13082](https://issues.apache.org/jira/browse/CAMEL-13082)

Introduce an Olingo4 results-already-seen property to filter old results

[CAMEL-13071](https://issues.apache.org/jira/browse/CAMEL-13071)

Elasticsearch rest component should support scroll api

[CAMEL-13023](https://issues.apache.org/jira/browse/CAMEL-13023)

Add camel-rest-swagger as Karaf feature

[CAMEL-13015](https://issues.apache.org/jira/browse/CAMEL-13015)

camel-spring-boot - load multiple route xml files

[CAMEL-12990](https://issues.apache.org/jira/browse/CAMEL-12990)

FTP endpoint with 'localWorkDirectory' considers File Consumer's 'noop' option

[CAMEL-12982](https://issues.apache.org/jira/browse/CAMEL-12982)

Add support for alternative RAW() syntax

[CAMEL-12964](https://issues.apache.org/jira/browse/CAMEL-12964)

Create new CamelWIH to integrate with recently added Camel support in jBPM/KIE-Server

[CAMEL-12954](https://issues.apache.org/jira/browse/CAMEL-12954)

Add a camel-websocket component 100% using only JSR356

[CAMEL-12930](https://issues.apache.org/jira/browse/CAMEL-12930)

Ability to execute DML statements in Google Bigquery component

[CAMEL-12815](https://issues.apache.org/jira/browse/CAMEL-12815)

A new Component IOTA

[CAMEL-12665](https://issues.apache.org/jira/browse/CAMEL-12665)

Create a Camel-Pulsar component

[CAMEL-11888](https://issues.apache.org/jira/browse/CAMEL-11888)

cluster service : add a cluster service based on JGroups Raft

[CAMEL-11157](https://issues.apache.org/jira/browse/CAMEL-11157)

Camel-Kubernetes: Add Support for DaemonSet resources

### Task (21)

[CAMEL-13445](https://issues.apache.org/jira/browse/CAMEL-13445)

Camel-Pulsar: Migrate to camel-testcontainers instead of using testcontainers directly

[CAMEL-13405](https://issues.apache.org/jira/browse/CAMEL-13405)

Camel-Pulsar: Create integration test for Karaf and SB

[CAMEL-13404](https://issues.apache.org/jira/browse/CAMEL-13404)

Camel-Pulsar: Create Karaf feature

[CAMEL-13348](https://issues.apache.org/jira/browse/CAMEL-13348)

Camel elasticsearch support search without specifying the indexName and indexType

[CAMEL-13332](https://issues.apache.org/jira/browse/CAMEL-13332)

camel-undertow: xnio-nio not installed

[CAMEL-13263](https://issues.apache.org/jira/browse/CAMEL-13263)

Lenient IPFS connection check on startup

[CAMEL-13240](https://issues.apache.org/jira/browse/CAMEL-13240)

Don't ship the jars in the source artifacts

[CAMEL-13238](https://issues.apache.org/jira/browse/CAMEL-13238)

Upgrade to Kafka 2.1.1

[CAMEL-13232](https://issues.apache.org/jira/browse/CAMEL-13232)

Simple language - Backwards compatible parser on 2.x should WARN

[CAMEL-13173](https://issues.apache.org/jira/browse/CAMEL-13173)

\[IPFS\] Remove transitive dependency on bitcoin and cipher

[CAMEL-13169](https://issues.apache.org/jira/browse/CAMEL-13169)

c3p0 dependent version (0.9.5.2) has a security vulnerability (CVE-2018-20433)

[CAMEL-13153](https://issues.apache.org/jira/browse/CAMEL-13153)

camel-mail - Strip newlines from exchange headers

[CAMEL-13105](https://issues.apache.org/jira/browse/CAMEL-13105)

Remove and deprecate camel-chronicle

[CAMEL-13041](https://issues.apache.org/jira/browse/CAMEL-13041)

Camel-AWS MQ: Create Broker operation is not working

[CAMEL-13039](https://issues.apache.org/jira/browse/CAMEL-13039)

Deprecate/Remove Camel-YQL

[CAMEL-13021](https://issues.apache.org/jira/browse/CAMEL-13021)

Remove camel-example-swagger-xml

[CAMEL-13010](https://issues.apache.org/jira/browse/CAMEL-13010)

Deprecate camel-script

[CAMEL-12995](https://issues.apache.org/jira/browse/CAMEL-12995)

Remove Camel XmlJson

[CAMEL-12988](https://issues.apache.org/jira/browse/CAMEL-12988)

Update doc to clarify how to specify routes to start up last

[CAMEL-12965](https://issues.apache.org/jira/browse/CAMEL-12965)

deprecate the Camel maven archetypes

[CAMEL-12937](https://issues.apache.org/jira/browse/CAMEL-12937)

Stream Caching Cipher is misspelled as chiper

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).