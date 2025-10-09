# Apache camel 3.15.0 Release

## New and Noteworthy

This release is the new Camel 3.15.0 release. Java 8 support has been dropped with this release.

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
      <version>3.15.0</version>
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
      <version>3.15.0</version>
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
| [apache-camel-3.15.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.15.0/apache-camel-3.15.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.15.0/apache-camel-3.15.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.15.0/apache-camel-3.15.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.15.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.15.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (49)

[CAMEL-17548](https://issues.apache.org/jira/browse/CAMEL-17548)

camel-springdoc-starter: throwing NPE when apiProperties is not set

[CAMEL-17545](https://issues.apache.org/jira/browse/CAMEL-17545)

camel elasticsearch rest on spring boot - class not found error

[CAMEL-17536](https://issues.apache.org/jira/browse/CAMEL-17536)

ServicePool.doStop hangs during shutdown

[CAMEL-17526](https://issues.apache.org/jira/browse/CAMEL-17526)

camel-fhir: the serverUrl configuration on camel-fhir endpoint shouldn't be ignored

[CAMEL-17524](https://issues.apache.org/jira/browse/CAMEL-17524)

Camel loading of resources using ClassResolver API doesn't work in OSGi enviroments

[CAMEL-17523](https://issues.apache.org/jira/browse/CAMEL-17523)

camel-spring-boot-examples：rest-jpa is broken

[CAMEL-17521](https://issues.apache.org/jira/browse/CAMEL-17521)

camel-http - httpClient parameters are not filtered out

[CAMEL-17520](https://issues.apache.org/jira/browse/CAMEL-17520)

Cannot use square brackets in HTTP parameters

[CAMEL-17514](https://issues.apache.org/jira/browse/CAMEL-17514)

BreadcrumbId MDC Value not set even MDCLogging is true during ErrorHandling Processor

[CAMEL-17511](https://issues.apache.org/jira/browse/CAMEL-17511)

Spring boot actuator endpoint parameters issues

[CAMEL-17506](https://issues.apache.org/jira/browse/CAMEL-17506)

olingo4 should always look for a single entity when a predicate key is used

[CAMEL-17504](https://issues.apache.org/jira/browse/CAMEL-17504)

BridgeExceptionHandlerToErrorHandler broken with DefaultErrorHandler

[CAMEL-17503](https://issues.apache.org/jira/browse/CAMEL-17503)

camel-ahc-ws - Unable to reconnect to Server after server reboot

[CAMEL-17501](https://issues.apache.org/jira/browse/CAMEL-17501)

camel-core - FailedToCreateRouteException issue if route is very long and complex uris that cannot be sanitized

[CAMEL-17493](https://issues.apache.org/jira/browse/CAMEL-17493)

camel-kafka: safe unsubscription should ignore safe exceptions

[CAMEL-17492](https://issues.apache.org/jira/browse/CAMEL-17492)

CamelBeanPostProcessor fails if @Producer is used in EventNotifier

[CAMEL-17491](https://issues.apache.org/jira/browse/CAMEL-17491)

camel-openapi-java - Operation paths are incorrect if contextPath is set

[CAMEL-17489](https://issues.apache.org/jira/browse/CAMEL-17489)

camel-kafka - Unsubscribing fails due to already closed consumer

[CAMEL-17487](https://issues.apache.org/jira/browse/CAMEL-17487)

camel-karaf: verify goal error for karaf-maven-plugin

[CAMEL-17486](https://issues.apache.org/jira/browse/CAMEL-17486)

camel-core - ThrottlePermit compareTo cast to int causes issues

[CAMEL-17485](https://issues.apache.org/jira/browse/CAMEL-17485)

Camel-JSLT: Currently it could only load resources from classpath

[CAMEL-17477](https://issues.apache.org/jira/browse/CAMEL-17477)

camel-smpp: reconnection logic is not respecting the reconnectDelay

[CAMEL-17473](https://issues.apache.org/jira/browse/CAMEL-17473)

camel-github: startingSha=last doesn't work properly

[CAMEL-17472](https://issues.apache.org/jira/browse/CAMEL-17472)

camel-smpp: Consumer reconnect no longer works after updating to 3.14.0

[CAMEL-17471](https://issues.apache.org/jira/browse/CAMEL-17471)

Snakeyaml: Use safe constructor where the default one has been used

[CAMEL-17457](https://issues.apache.org/jira/browse/CAMEL-17457)

camel-openapi-java - Incorrect tags in openapi

[CAMEL-17454](https://issues.apache.org/jira/browse/CAMEL-17454)

camel-undertow - Adds duplicate content-type

[CAMEL-17452](https://issues.apache.org/jira/browse/CAMEL-17452)

camel-util - URISupport#sanitizeUri sanitizes passwords incorrectly if remaining uri contains expression ${<expr>}

[CAMEL-17446](https://issues.apache.org/jira/browse/CAMEL-17446)

Trigger start time for Quartz causes confusion with short trigger intervals

[CAMEL-17441](https://issues.apache.org/jira/browse/CAMEL-17441)

camel-health - Loading custom health-check from classpath scanning is not added to registry

[CAMEL-17440](https://issues.apache.org/jira/browse/CAMEL-17440)

camel-quartz - Fires twice on first cron job when using startDelayed

[CAMEL-17437](https://issues.apache.org/jira/browse/CAMEL-17437)

Camel-aws2-sqs: Deadletter fails with sqs client from registry (could impact more components)

[CAMEL-17436](https://issues.apache.org/jira/browse/CAMEL-17436)

camel-spring-boot - Disabling health check for single route or consumer is not possible

[CAMEL-17430](https://issues.apache.org/jira/browse/CAMEL-17430)

Rest endpoint query parameters not set on underlying endpoint

[CAMEL-17426](https://issues.apache.org/jira/browse/CAMEL-17426)

microprofile healt checks: do not conflate camel checks

[CAMEL-17425](https://issues.apache.org/jira/browse/CAMEL-17425)

camel-quartz - OSGi compatibility is broken for loading resources from classloader

[CAMEL-17413](https://issues.apache.org/jira/browse/CAMEL-17413)

camel-core - Route configurations may not have source loc:line

[CAMEL-17393](https://issues.apache.org/jira/browse/CAMEL-17393)

Debugger - Source locations are not available in Spring Boot configurations

[CAMEL-17390](https://issues.apache.org/jira/browse/CAMEL-17390)

camel-core - Cannot set tracer on a started CamelContext

[CAMEL-17373](https://issues.apache.org/jira/browse/CAMEL-17373)

camel-fhir unrecognized camel.component.fhir.server-url in 3.15.0-SNAPSHOT

[CAMEL-17372](https://issues.apache.org/jira/browse/CAMEL-17372)

Camel-Azure-Servicebus is missing in Camel catalog

[CAMEL-17367](https://issues.apache.org/jira/browse/CAMEL-17367)

Kafka endpoint DSL for producer doesn't strip //

[CAMEL-17358](https://issues.apache.org/jira/browse/CAMEL-17358)

AWS SDK2 Producer does not set the Content Type at all

[CAMEL-17344](https://issues.apache.org/jira/browse/CAMEL-17344)

camel-salesforce: collections operations swallow exceptions

[CAMEL-17337](https://issues.apache.org/jira/browse/CAMEL-17337)

camel-fhir - FhirComponent regression between 2.2x and 3.x releases

[CAMEL-17336](https://issues.apache.org/jira/browse/CAMEL-17336)

camel-jackson: Can't operate in \`List\` mode and use a custom ObjectMapper

[CAMEL-17296](https://issues.apache.org/jira/browse/CAMEL-17296)

Multicast option stopOnAggregateException has no effect

[CAMEL-17137](https://issues.apache.org/jira/browse/CAMEL-17137)

camel-karaf - Error while adding camel-cxf

[CAMEL-17118](https://issues.apache.org/jira/browse/CAMEL-17118)

mapHttpMessageFormUrlEncodedBody does not work - it will always map the POST parameters to headers

### Dependency upgrade (21)

[CAMEL-17572](https://issues.apache.org/jira/browse/CAMEL-17572)

Bump Caffeine to 3.x

[CAMEL-17547](https://issues.apache.org/jira/browse/CAMEL-17547)

camel-jbang - Upgrade to kamelets 0.7.0

[CAMEL-17542](https://issues.apache.org/jira/browse/CAMEL-17542)

camel-kubernetes - Upgrade to 5.12.x

[CAMEL-17538](https://issues.apache.org/jira/browse/CAMEL-17538)

camel-microprofile - Update to newer releases

[CAMEL-17532](https://issues.apache.org/jira/browse/CAMEL-17532)

Upgrade Google API services dependencies to 1.32.1

[CAMEL-17529](https://issues.apache.org/jira/browse/CAMEL-17529)

camel-spring-boot - Upgrade to 2.6.3

[CAMEL-17490](https://issues.apache.org/jira/browse/CAMEL-17490)

camel-debezium - Upgrade to 1.8

[CAMEL-17475](https://issues.apache.org/jira/browse/CAMEL-17475)

upgrade to CXF 3.5.0

[CAMEL-17469](https://issues.apache.org/jira/browse/CAMEL-17469)

camel-jackson - Upgrade to 2.13.x

[CAMEL-17461](https://issues.apache.org/jira/browse/CAMEL-17461)

Migrate from commons-pool:commons-pool to org.apache.commons:commons-pool2

[CAMEL-17456](https://issues.apache.org/jira/browse/CAMEL-17456)

camel-any23 - Upgrade to 2.6

[CAMEL-17395](https://issues.apache.org/jira/browse/CAMEL-17395)

upgrade to log4j 2.17.1

[CAMEL-17379](https://issues.apache.org/jira/browse/CAMEL-17379)

camel-optaplanner - Upgrade to 8.16.x

[CAMEL-17376](https://issues.apache.org/jira/browse/CAMEL-17376)

camel-vertx - Upgrade to vertx 4.2.x

[CAMEL-17360](https://issues.apache.org/jira/browse/CAMEL-17360)

upgrade to bouncycastle 1.70

[CAMEL-17353](https://issues.apache.org/jira/browse/CAMEL-17353)

Upgrade to log4j 2.17.0

[CAMEL-17335](https://issues.apache.org/jira/browse/CAMEL-17335)

upgrade to logback 1.2.8

[CAMEL-17327](https://issues.apache.org/jira/browse/CAMEL-17327)

Upgrade to log4j 2.16.0

[CAMEL-17313](https://issues.apache.org/jira/browse/CAMEL-17313)

camel-netty - Upgrade to 4.1.72

[CAMEL-17284](https://issues.apache.org/jira/browse/CAMEL-17284)

camel-kafka - Upgrade to kafka clients 3.1.x

[CAMEL-17099](https://issues.apache.org/jira/browse/CAMEL-17099)

Upgrade to Jackson 2.13.x

### Improvement (73)

[CAMEL-17556](https://issues.apache.org/jira/browse/CAMEL-17556)

camel-aws-2-ses: add configuration set parameter

[CAMEL-17553](https://issues.apache.org/jira/browse/CAMEL-17553)

simple language - Evaluate expression with null value guard against NPE

[CAMEL-17549](https://issues.apache.org/jira/browse/CAMEL-17549)

log component - Add option to have it use source location:line as logger name

[CAMEL-17540](https://issues.apache.org/jira/browse/CAMEL-17540)

CamelJms Request Reply QueueReplyManager is coupled with DefaultMessageListenerContainer

[CAMEL-17531](https://issues.apache.org/jira/browse/CAMEL-17531)

endpoint should have multiValueOptions source code generated to uri factory

[CAMEL-17527](https://issues.apache.org/jira/browse/CAMEL-17527)

Polish the grammar of SyncPropertiesMojo's documentation

[CAMEL-17525](https://issues.apache.org/jira/browse/CAMEL-17525)

camel-stub - StubEndpoint should be lenient properties

[CAMEL-17519](https://issues.apache.org/jira/browse/CAMEL-17519)

Make Camel MainSupport internalBeforeStart method protected

[CAMEL-17517](https://issues.apache.org/jira/browse/CAMEL-17517)

Be able to run fhir spring-boot example out of the box

[CAMEL-17509](https://issues.apache.org/jira/browse/CAMEL-17509)

camel-kafka: invalid topic info displayed when using topic patterns

[CAMEL-17508](https://issues.apache.org/jira/browse/CAMEL-17508)

camel-core - Process ref should support #class syntax

[CAMEL-17500](https://issues.apache.org/jira/browse/CAMEL-17500)

Make dynamic router eip component subscription easier

[CAMEL-17499](https://issues.apache.org/jira/browse/CAMEL-17499)

dataformats should use camelCase in model names

[CAMEL-17498](https://issues.apache.org/jira/browse/CAMEL-17498)

gzip dataformat renamed to gzipdeflator

[CAMEL-17497](https://issues.apache.org/jira/browse/CAMEL-17497)

DataFormat resources consistency

[CAMEL-17496](https://issues.apache.org/jira/browse/CAMEL-17496)

camel-core - Exchange events toString polish

[CAMEL-17488](https://issues.apache.org/jira/browse/CAMEL-17488)

camel-cloudevent - Drop old 0.x specs

[CAMEL-17481](https://issues.apache.org/jira/browse/CAMEL-17481)

camel-caffeine: Various improvements

[CAMEL-17479](https://issues.apache.org/jira/browse/CAMEL-17479)

camel-core - Configuring properties with optional syntax in value on beans also

[CAMEL-17478](https://issues.apache.org/jira/browse/CAMEL-17478)

camel-aws2-s3 Operation downloadLink requires aws credentails even if client is aurowired from registry

[CAMEL-17470](https://issues.apache.org/jira/browse/CAMEL-17470)

camel-ahc - Binary file upload fails to the target system

[CAMEL-17468](https://issues.apache.org/jira/browse/CAMEL-17468)

camel-core - Filter EIP - add option to turn on exchange property with filter status

[CAMEL-17467](https://issues.apache.org/jira/browse/CAMEL-17467)

camel-core - Add method to ValueBuilder for java based predicate/expressions

[CAMEL-17458](https://issues.apache.org/jira/browse/CAMEL-17458)

camel-jira - Authentication via bearer access token

[CAMEL-17455](https://issues.apache.org/jira/browse/CAMEL-17455)

camel-core - RouteBuilder deprecate endpoint methods as they resolve endpoint to eager

[CAMEL-17451](https://issues.apache.org/jira/browse/CAMEL-17451)

camel-yaml-dsl - Line number missing for sink in kamelets

[CAMEL-17450](https://issues.apache.org/jira/browse/CAMEL-17450)

camel-yaml-dsl - Source location for KameletBinding

[CAMEL-17444](https://issues.apache.org/jira/browse/CAMEL-17444)

camel-core - Add message history operation to debugger

[CAMEL-17428](https://issues.apache.org/jira/browse/CAMEL-17428)

camel-jbang - Add -flight-recorder to startup JFR capturing

[CAMEL-17427](https://issues.apache.org/jira/browse/CAMEL-17427)

Option to restore old behaviour of scheduled consumers healthcheck

[CAMEL-17421](https://issues.apache.org/jira/browse/CAMEL-17421)

camel-catalog - EIPs should include if they are abstract in the metadata

[CAMEL-17416](https://issues.apache.org/jira/browse/CAMEL-17416)

camel-core - Debugger to have operation for ids that can be used as breakpoints

[CAMEL-17415](https://issues.apache.org/jira/browse/CAMEL-17415)

camel-jbang - Add --trace option

[CAMEL-17414](https://issues.apache.org/jira/browse/CAMEL-17414)

camel-core - Resource to have absolute vs relative location

[CAMEL-17412](https://issues.apache.org/jira/browse/CAMEL-17412)

camel-xml-io - Line number is the tag end line - We need a tag start line number

[CAMEL-17411](https://issues.apache.org/jira/browse/CAMEL-17411)

camel-yaml-dsl - May be parsed twice when using routes configuration

[CAMEL-17408](https://issues.apache.org/jira/browse/CAMEL-17408)

camel-core - Log EIP should use source:line as logger name if available

[CAMEL-17407](https://issues.apache.org/jira/browse/CAMEL-17407)

camel-core - Processor should support LineNumberAware

[CAMEL-17406](https://issues.apache.org/jira/browse/CAMEL-17406)

camel-core - InterceptFrom header with intercepted endpoint should be done without affecting model

[CAMEL-17403](https://issues.apache.org/jira/browse/CAMEL-17403)

camel-core - Dump route as xml include source location:line if debugger enabled

[CAMEL-17402](https://issues.apache.org/jira/browse/CAMEL-17402)

camel-spring-boot - camel-management-starter

[CAMEL-17399](https://issues.apache.org/jira/browse/CAMEL-17399)

camel-catalog - Add DSL to misc components

[CAMEL-17392](https://issues.apache.org/jira/browse/CAMEL-17392)

Camel-google-storage - Provide a way to filter blobs in a bucket

[CAMEL-17389](https://issues.apache.org/jira/browse/CAMEL-17389)

toD (Dynamic To URI) doesn't work with Windows paths with file component

[CAMEL-17380](https://issues.apache.org/jira/browse/CAMEL-17380)

camel-yaml-dsl - Should not dependt on endpointdsl

[CAMEL-17371](https://issues.apache.org/jira/browse/CAMEL-17371)

Debugger should be able to set and remove exchange properties on suspended nodes

[CAMEL-17370](https://issues.apache.org/jira/browse/CAMEL-17370)

rename CamelJBang app to camel

[CAMEL-17365](https://issues.apache.org/jira/browse/CAMEL-17365)

camel-salesforce: getResources should not be hard coded

[CAMEL-17363](https://issues.apache.org/jira/browse/CAMEL-17363)

camel-endpointdsl and componentdsl - Allow to filter components based on exclude list

[CAMEL-17361](https://issues.apache.org/jira/browse/CAMEL-17361)

camel-management - Move routecontroller mbeans to services

[CAMEL-17359](https://issues.apache.org/jira/browse/CAMEL-17359)

camel-debug JAR to make camel debugging easier from tooling

[CAMEL-17351](https://issues.apache.org/jira/browse/CAMEL-17351)

Camel Google Functions: Make it possible to configure service account key file as we do in Pubsub and Storage

[CAMEL-17346](https://issues.apache.org/jira/browse/CAMEL-17346)

camel-salesforce: handle password expired better

[CAMEL-17342](https://issues.apache.org/jira/browse/CAMEL-17342)

camel-core - Debugger should be able to dump Exchange properties in XML

[CAMEL-17341](https://issues.apache.org/jira/browse/CAMEL-17341)

Add expression evaluation option to the backlog debugger

[CAMEL-17332](https://issues.apache.org/jira/browse/CAMEL-17332)

camel-management - Dump stats with source location/line number

[CAMEL-17331](https://issues.apache.org/jira/browse/CAMEL-17331)

camel-core - Add line number metadata to model

[CAMEL-17326](https://issues.apache.org/jira/browse/CAMEL-17326)

camel-rest-swagger: Resolve Swagger references

[CAMEL-17323](https://issues.apache.org/jira/browse/CAMEL-17323)

camel-main - Add option to turn on debug

[CAMEL-17307](https://issues.apache.org/jira/browse/CAMEL-17307)

Possibility to define the exception thrown when predicate is used in validate camel dsl node

[CAMEL-17306](https://issues.apache.org/jira/browse/CAMEL-17306)

camel-salesforce: refactor dto generation

[CAMEL-17304](https://issues.apache.org/jira/browse/CAMEL-17304)

camel-yaml-dsl: consistency of from

[CAMEL-17286](https://issues.apache.org/jira/browse/CAMEL-17286)

camel-core - RemoveProperty EIP propertyName should be renamed to name

[CAMEL-17283](https://issues.apache.org/jira/browse/CAMEL-17283)

RouteTemplateBeanDefinition YAML DSL Schema

[CAMEL-17281](https://issues.apache.org/jira/browse/CAMEL-17281)

camel-yaml-dsl - Error handlers have options not in the json model schema

[CAMEL-17265](https://issues.apache.org/jira/browse/CAMEL-17265)

Inconsistency between camel-catalog and camel-core-model

[CAMEL-17251](https://issues.apache.org/jira/browse/CAMEL-17251)

camel-spring - Load type converters should be false

[CAMEL-17236](https://issues.apache.org/jira/browse/CAMEL-17236)

camel-core - Remove classic startup summary level

[CAMEL-17207](https://issues.apache.org/jira/browse/CAMEL-17207)

camel-core - Stopping a kamelet route should stop the child route as well

[CAMEL-17057](https://issues.apache.org/jira/browse/CAMEL-17057)

camel-mongodb - Make it easier to configuring that dreadful MongoDBClientURI

[CAMEL-13181](https://issues.apache.org/jira/browse/CAMEL-13181)

camel-salesforce - rest exception parsing produces useless messages

[CAMEL-11001](https://issues.apache.org/jira/browse/CAMEL-11001)

Improve camel-salesforce documentation

[CAMEL-4271](https://issues.apache.org/jira/browse/CAMEL-4271)

jdbc aggregation repository - recovery taks and cluster issue

### New Feature (29)

[CAMEL-17552](https://issues.apache.org/jira/browse/CAMEL-17552)

camel-core - Switch EIP that can optimize during bootstrap

[CAMEL-17510](https://issues.apache.org/jira/browse/CAMEL-17510)

camel-yaml-dsl - Generate json schema in camelCase

[CAMEL-17476](https://issues.apache.org/jira/browse/CAMEL-17476)

Google OAuth2 for service account

[CAMEL-17420](https://issues.apache.org/jira/browse/CAMEL-17420)

camel-core - Add flag to turn on|off source loc:line

[CAMEL-17419](https://issues.apache.org/jira/browse/CAMEL-17419)

camel-core - Backlog tracer to include source loc:line

[CAMEL-17418](https://issues.apache.org/jira/browse/CAMEL-17418)

camel-core - Message history to include source loc:line

[CAMEL-17417](https://issues.apache.org/jira/browse/CAMEL-17417)

camel-core - Route stack trace to include source file:line

[CAMEL-17405](https://issues.apache.org/jira/browse/CAMEL-17405)

camel-xml-io - Add source location to parsed models

[CAMEL-17400](https://issues.apache.org/jira/browse/CAMEL-17400)

camel-java-dsl - Add source line number to loaded model

[CAMEL-17385](https://issues.apache.org/jira/browse/CAMEL-17385)

camel-jbang - Developer Console

[CAMEL-17384](https://issues.apache.org/jira/browse/CAMEL-17384)

camel-core - Developer Console SPI

[CAMEL-17383](https://issues.apache.org/jira/browse/CAMEL-17383)

camel-management - Add operations to list the registered components, data formats and languages

[CAMEL-17382](https://issues.apache.org/jira/browse/CAMEL-17382)

camel-jsh-dsl - JavaShell DSL support

[CAMEL-17378](https://issues.apache.org/jira/browse/CAMEL-17378)

camel-spring-boot - Should have starters for endpoint and component dsl

[CAMEL-17377](https://issues.apache.org/jira/browse/CAMEL-17377)

camel-spring-boot - Should have starters for groovy, kotlin and js

[CAMEL-17352](https://issues.apache.org/jira/browse/CAMEL-17352)

log-component - Add plain option

[CAMEL-17345](https://issues.apache.org/jira/browse/CAMEL-17345)

camel-jbang - Add command to create as a maven project

[CAMEL-17340](https://issues.apache.org/jira/browse/CAMEL-17340)

camel-core - BacklogDebugger - Get source location and line number for suspends breakpoints

[CAMEL-17338](https://issues.apache.org/jira/browse/CAMEL-17338)

camel-core - Tracer to include source file:line in output

[CAMEL-17321](https://issues.apache.org/jira/browse/CAMEL-17321)

Add HuaweiCloud FaceRecognitionService(FRS) Component

[CAMEL-17319](https://issues.apache.org/jira/browse/CAMEL-17319)

camel-milo: Add support for Eclipse Milo browsing functionality

[CAMEL-17289](https://issues.apache.org/jira/browse/CAMEL-17289)

camel-yaml-dsl - Add support for knative in kamelet bindings

[CAMEL-17280](https://issues.apache.org/jira/browse/CAMEL-17280)

camel-jbang - Run from github using wildcards

[CAMEL-17258](https://issues.apache.org/jira/browse/CAMEL-17258)

Possibility to change lengths of output groups in tracing (DefaultTracer)

[CAMEL-17154](https://issues.apache.org/jira/browse/CAMEL-17154)

Create alternate dynamic router implementation that allows registration

[CAMEL-15951](https://issues.apache.org/jira/browse/CAMEL-15951)

Introduce configuration property to skip DescribeTable operation on start of aws2-ddb component

[CAMEL-15275](https://issues.apache.org/jira/browse/CAMEL-15275)

Create camel-knative component in main Camel components based on camel-knative for camel-k

[CAMEL-13335](https://issues.apache.org/jira/browse/CAMEL-13335)

create camel-cloudevents data type

[CAMEL-13180](https://issues.apache.org/jira/browse/CAMEL-13180)

camel-salesforce - Apex calls could support more flexible response parsing

### Sub-task (4)

[CAMEL-17349](https://issues.apache.org/jira/browse/CAMEL-17349)

AggregateTimeoutWithExecutorServiceTest sometimes fails

[CAMEL-17343](https://issues.apache.org/jira/browse/CAMEL-17343)

SedaDiscardWhenFullTest frequently fails

[CAMEL-17229](https://issues.apache.org/jira/browse/CAMEL-17229)

The file consumer finds files before they have content

[CAMEL-16972](https://issues.apache.org/jira/browse/CAMEL-16972)

tests in camel-cdi failed with JDK17

### Task (37)

[CAMEL-17566](https://issues.apache.org/jira/browse/CAMEL-17566)

rest-openapi-simple of camel-spring-boot-examples is broken

[CAMEL-17561](https://issues.apache.org/jira/browse/CAMEL-17561)

camel-opentracing - Deprecate

[CAMEL-17557](https://issues.apache.org/jira/browse/CAMEL-17557)

undertow-spring-security camel-spring-boot-examples is broken

[CAMEL-17550](https://issues.apache.org/jira/browse/CAMEL-17550)

Use same-version image container for Pulsar as client

[CAMEL-17541](https://issues.apache.org/jira/browse/CAMEL-17541)

camel-yaml-dsl - Remove deprecated tod workaround name

[CAMEL-17533](https://issues.apache.org/jira/browse/CAMEL-17533)

Remove Camel-Jooq karaf feature

[CAMEL-17483](https://issues.apache.org/jira/browse/CAMEL-17483)

camel-cxf: avoid using deprecated API

[CAMEL-17464](https://issues.apache.org/jira/browse/CAMEL-17464)

Avoid duplication of API Mapping link for ServiceNow

[CAMEL-17463](https://issues.apache.org/jira/browse/CAMEL-17463)

Little issues in twitter attributes description

[CAMEL-17460](https://issues.apache.org/jira/browse/CAMEL-17460)

camel-spring-javaconfig - Remove as it has been deprecated for a long time

[CAMEL-17459](https://issues.apache.org/jira/browse/CAMEL-17459)

camel-cdi - Deprecate legacy XML camel context support

[CAMEL-17445](https://issues.apache.org/jira/browse/CAMEL-17445)

Dead link in javadoc of org.apache.camel.CamelContextLifecycle.start()

[CAMEL-17442](https://issues.apache.org/jira/browse/CAMEL-17442)

camel-test-infra: adjust scope for camel-test-infra-common

[CAMEL-17439](https://issues.apache.org/jira/browse/CAMEL-17439)

Remove <p\\/> from generated javadoc / json

[CAMEL-17435](https://issues.apache.org/jira/browse/CAMEL-17435)

build: review dependencies (java 8 to java 10)

[CAMEL-17432](https://issues.apache.org/jira/browse/CAMEL-17432)

build: replace --source and --target with --release

[CAMEL-17431](https://issues.apache.org/jira/browse/CAMEL-17431)

build: Java target and source leaking from Apache parent pom

[CAMEL-17429](https://issues.apache.org/jira/browse/CAMEL-17429)

build: remove or adjust Maven profiles for deprecated JDKs

[CAMEL-17422](https://issues.apache.org/jira/browse/CAMEL-17422)

Correct the grammatically incorrect use of "splitted" with "split"

[CAMEL-17398](https://issues.apache.org/jira/browse/CAMEL-17398)

camel-catalog - Add misc from core

[CAMEL-17397](https://issues.apache.org/jira/browse/CAMEL-17397)

Clarify the grammar of the "Still problems" section of FAQ page

[CAMEL-17396](https://issues.apache.org/jira/browse/CAMEL-17396)

camel-spring-boot - Starter for the java shell DSL

[CAMEL-17391](https://issues.apache.org/jira/browse/CAMEL-17391)

org.elasticsearch.client.sniff.Sniffer : error while sniffing nodes

[CAMEL-17388](https://issues.apache.org/jira/browse/CAMEL-17388)

camel-yaml-dsl - Loading kamelet binding error handler DLC renamed to sink

[CAMEL-17387](https://issues.apache.org/jira/browse/CAMEL-17387)

camel-karaf - Remove deprecated camel-osgi-activator

[CAMEL-17381](https://issues.apache.org/jira/browse/CAMEL-17381)

camel-karaf - Feature validation has some errors after JDK8 drop

[CAMEL-17355](https://issues.apache.org/jira/browse/CAMEL-17355)

camel-examples - Reduce number of cdi examples

[CAMEL-17354](https://issues.apache.org/jira/browse/CAMEL-17354)

deprecate and cleanup outdated components

[CAMEL-17329](https://issues.apache.org/jira/browse/CAMEL-17329)

Drop support for Java 8

[CAMEL-17273](https://issues.apache.org/jira/browse/CAMEL-17273)

camel-karaf - Removed deprecated camel-osgi-activator

[CAMEL-17249](https://issues.apache.org/jira/browse/CAMEL-17249)

camel-jbang: failing to resolve updated kamelets path

[CAMEL-17194](https://issues.apache.org/jira/browse/CAMEL-17194)

Generate source for camel-endpointdsl and camel-componentdsl only once

[CAMEL-17192](https://issues.apache.org/jira/browse/CAMEL-17192)

Move camel-endpointdsl and camel-componentdsl into dsl folder

[CAMEL-17064](https://issues.apache.org/jira/browse/CAMEL-17064)

Investigate causes of flakes in camel unit tests

[CAMEL-16855](https://issues.apache.org/jira/browse/CAMEL-16855)

camel-karaf - Remove <repository></repository> from camel karaf features repo

[CAMEL-15727](https://issues.apache.org/jira/browse/CAMEL-15727)

Simplify camel-cdi dependencies

[CAMEL-15724](https://issues.apache.org/jira/browse/CAMEL-15724)

Decouple camel-cdi from JTA

### Test (4)

[CAMEL-17494](https://issues.apache.org/jira/browse/CAMEL-17494)

camel-spring-boot: ServiceRegistry not started

[CAMEL-17465](https://issues.apache.org/jira/browse/CAMEL-17465)

the test for camel-archetype-cdi is broken

[CAMEL-17453](https://issues.apache.org/jira/browse/CAMEL-17453)

MTOM/XOP tests in camel-cxf are broken

[CAMEL-16141](https://issues.apache.org/jira/browse/CAMEL-16141)

Investigate failing mina tests on JDK >= 11

### Wish (1)

[CAMEL-17546](https://issues.apache.org/jira/browse/CAMEL-17546)

Introduce camel.failsafe.forkTimeout property for maven-failsafe-plugin

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).