# Apache camel 3.14.0 Release

## New and Noteworthy

This release is the new Camel 3.14.0 LTS release (last release to support Java 8).

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
      <version>3.14.0</version>
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
      <version>3.14.0</version>
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
| [apache-camel-3.14.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.0/apache-camel-3.14.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.0/apache-camel-3.14.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.0/apache-camel-3.14.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (31)

[CAMEL-17590](https://issues.apache.org/jira/browse/CAMEL-17590)

Camel sftp kafka source connector

[CAMEL-17516](https://issues.apache.org/jira/browse/CAMEL-17516)

Environment variables takes precedence over route template parameter

[CAMEL-17322](https://issues.apache.org/jira/browse/CAMEL-17322)

Google Pubsub needs scopes set on Credentials

[CAMEL-17303](https://issues.apache.org/jira/browse/CAMEL-17303)

camel-jbang: FailedToCreateRouteException

[CAMEL-17298](https://issues.apache.org/jira/browse/CAMEL-17298)

camel-vertx-http duplicates path

[CAMEL-17295](https://issues.apache.org/jira/browse/CAMEL-17295)

REST DSL (With Servlet Component) Fails to Resolve Endpoint if Query Parameter Is Part of URI Parameter

[CAMEL-17291](https://issues.apache.org/jira/browse/CAMEL-17291)

Camel-AWS2-SES: Don't set the replyTo/to addresses as List

[CAMEL-17274](https://issues.apache.org/jira/browse/CAMEL-17274)

camel-spring-boot - Using war packaging cannot load XML routes via routes collector

[CAMEL-17269](https://issues.apache.org/jira/browse/CAMEL-17269)

Splunk HEC: IP address not accepted

[CAMEL-17267](https://issues.apache.org/jira/browse/CAMEL-17267)

Query parameters not always set when calling api using rest-openapi

[CAMEL-17248](https://issues.apache.org/jira/browse/CAMEL-17248)

camel-jbang: kamelet catalog should be a runtime dependency

[CAMEL-17245](https://issues.apache.org/jira/browse/CAMEL-17245)

camel-kafka: investigate multiple bogus calls to commit when async

[CAMEL-17244](https://issues.apache.org/jira/browse/CAMEL-17244)

camel-kafka: invalid creation of multiple consumers

[CAMEL-17242](https://issues.apache.org/jira/browse/CAMEL-17242)

Azure producers delete headers from exchange

[CAMEL-17234](https://issues.apache.org/jira/browse/CAMEL-17234)

camel-ldap - LDAP bad parsing of '=' in base parameter

[CAMEL-17232](https://issues.apache.org/jira/browse/CAMEL-17232)

AWS 2 S3 Body is null with includeBody=false (3.13.0 regression)

[CAMEL-17228](https://issues.apache.org/jira/browse/CAMEL-17228)

camel-kamelet - Kamelet EIP restarting issue

[CAMEL-17225](https://issues.apache.org/jira/browse/CAMEL-17225)

camel-core - Using predicates in Java DSL with ValueBuilder should init as predicate

[CAMEL-17221](https://issues.apache.org/jira/browse/CAMEL-17221)

isIgnoreSslVerification not works in HuaweiCloud ImageRecognition component and SimpleNotification component

[CAMEL-17213](https://issues.apache.org/jira/browse/CAMEL-17213)

camel-sftp \`maximumReconnectAttempts\` property changed behaviour

[CAMEL-17202](https://issues.apache.org/jira/browse/CAMEL-17202)

camel-rest-openapi - If two openapi spec uses the same path only one rest endpoint is created

[CAMEL-17200](https://issues.apache.org/jira/browse/CAMEL-17200)

\[camel-google-storage\] includeFolders parameter doesn't work

[CAMEL-17189](https://issues.apache.org/jira/browse/CAMEL-17189)

camel-salesforce forcably overrides the httpclient from SalesforceEndpointConfig

[CAMEL-17181](https://issues.apache.org/jira/browse/CAMEL-17181)

camel-core - XPathBuilder never clears pool when using @XPath annotation and grows pool causing memory leak

[CAMEL-17174](https://issues.apache.org/jira/browse/CAMEL-17174)

UnitOfWorkHelper doesn't clear UoW when job is done

[CAMEL-17158](https://issues.apache.org/jira/browse/CAMEL-17158)

AWS2 SQS When sending messages to a queue that has delay, the delay is not respected

[CAMEL-17131](https://issues.apache.org/jira/browse/CAMEL-17131)

camel-kafka - JMX MBean InstanceAlreadyExistsException thrown

[CAMEL-16978](https://issues.apache.org/jira/browse/CAMEL-16978)

camel-xchange - Unable to configure multiple xchange endpoints with different crypto exchanges

[CAMEL-16906](https://issues.apache.org/jira/browse/CAMEL-16906)

Platform-http components fail when using unmarshal

[CAMEL-16370](https://issues.apache.org/jira/browse/CAMEL-16370)

Camel Salesforce component unable to reconnect after disconnect from Salesforce

[CAMEL-13170](https://issues.apache.org/jira/browse/CAMEL-13170)

Starting Salesforce pushtopic with initialReplayIdMap set to a value will eventually break after 24 hours.

### Dependency upgrade (6)

[CAMEL-17316](https://issues.apache.org/jira/browse/CAMEL-17316)

Remove log4j dependency in camel-corda and camel-nsq

[CAMEL-17311](https://issues.apache.org/jira/browse/CAMEL-17311)

camel-karaf - upgrade to newer servicemix bundles

[CAMEL-17309](https://issues.apache.org/jira/browse/CAMEL-17309)

upgrade to log4j 2.15.0

[CAMEL-17238](https://issues.apache.org/jira/browse/CAMEL-17238)

camel-opentelemetry - Upgrade to 1.9.x

[CAMEL-17220](https://issues.apache.org/jira/browse/CAMEL-17220)

camel-spring-boot - Upgrade to 2.6.0

[CAMEL-17196](https://issues.apache.org/jira/browse/CAMEL-17196)

camel-elasticsearch - Update to 7.10.2

### Improvement (45)

[CAMEL-17312](https://issues.apache.org/jira/browse/CAMEL-17312)

camel-openapi-java - Add support for array parameter types

[CAMEL-17302](https://issues.apache.org/jira/browse/CAMEL-17302)

camel-core - Route reload event to indicate index/total

[CAMEL-17294](https://issues.apache.org/jira/browse/CAMEL-17294)

camel-yaml-dsl - Json library enums are case sensitive

[CAMEL-17290](https://issues.apache.org/jira/browse/CAMEL-17290)

Enable platform-http-vertx to provide access to authenticated user info

[CAMEL-17288](https://issues.apache.org/jira/browse/CAMEL-17288)

camel-core - Route template parameters dash vs camel case keys and required

[CAMEL-17282](https://issues.apache.org/jira/browse/CAMEL-17282)

camel-core - RemoveHeader EIP remove headerName

[CAMEL-17279](https://issues.apache.org/jira/browse/CAMEL-17279)

camel-jbang - Using platform-http should include vertx-http-platform

[CAMEL-17277](https://issues.apache.org/jira/browse/CAMEL-17277)

camel-datasonnet - Don't try to detect body mediatype when the Datasonnet header is used

[CAMEL-17276](https://issues.apache.org/jira/browse/CAMEL-17276)

maven camel:run - Colour logging

[CAMEL-17275](https://issues.apache.org/jira/browse/CAMEL-17275)

camel-yaml-dsl - Should be able to load camel-k binding yaml file

[CAMEL-17263](https://issues.apache.org/jira/browse/CAMEL-17263)

Camel Kafka - Allow to configure KafkaManualCommitFactory on endpoint level

[CAMEL-17262](https://issues.apache.org/jira/browse/CAMEL-17262)

Camel Kafka - Allow to configure KafkaClientFactory option on endpoint level

[CAMEL-17255](https://issues.apache.org/jira/browse/CAMEL-17255)

interface KafkaClientFactory methods must return interfaces instead classes

[CAMEL-17253](https://issues.apache.org/jira/browse/CAMEL-17253)

SetBody YAML DSL

[CAMEL-17246](https://issues.apache.org/jira/browse/CAMEL-17246)

camel-health - The failure endpoint uri should be sanitized

[CAMEL-17240](https://issues.apache.org/jira/browse/CAMEL-17240)

camel-kafka: investigate improving the performance of the producer

[CAMEL-17237](https://issues.apache.org/jira/browse/CAMEL-17237)

Remove com.google.code.findbugs from dependencies

[CAMEL-17233](https://issues.apache.org/jira/browse/CAMEL-17233)

camel-core - Route reload reduce logging noise for stopping/shutdown routes

[CAMEL-17230](https://issues.apache.org/jira/browse/CAMEL-17230)

camel-jbang: add support for local kamelets

[CAMEL-17227](https://issues.apache.org/jira/browse/CAMEL-17227)

Add property to SpringTransactionPolicy to name TransactionTemplate

[CAMEL-17226](https://issues.apache.org/jira/browse/CAMEL-17226)

Master w/ Zookeeper should take namespace into account for leader election

[CAMEL-17223](https://issues.apache.org/jira/browse/CAMEL-17223)

camel-jbang - Add option to stop all routes instead of terminate JVM when duration hit

[CAMEL-17217](https://issues.apache.org/jira/browse/CAMEL-17217)

camel-kamelet-main - Auto download DSL when loading routes in different DSLs

[CAMEL-17216](https://issues.apache.org/jira/browse/CAMEL-17216)

camel-jbang - Allow to include properties file when running

[CAMEL-17215](https://issues.apache.org/jira/browse/CAMEL-17215)

camel-jbang - Reload should restart max-messages duration

[CAMEL-17214](https://issues.apache.org/jira/browse/CAMEL-17214)

camel-jbang - Add option to turn off that file-watcher route

[CAMEL-17212](https://issues.apache.org/jira/browse/CAMEL-17212)

camel-jbang - Run goal is not only for Kamelet

[CAMEL-17210](https://issues.apache.org/jira/browse/CAMEL-17210)

camel-jbang - Allow to run a file loaded via github resource loader

[CAMEL-17209](https://issues.apache.org/jira/browse/CAMEL-17209)

camel-jfr - Java Flight Recorder should be enabled if detected on classpath

[CAMEL-17206](https://issues.apache.org/jira/browse/CAMEL-17206)

camel-kamelet-main - Add support for route reload

[CAMEL-17205](https://issues.apache.org/jira/browse/CAMEL-17205)

camel-core - Error handler with custom prepare processor should have access to failure route id

[CAMEL-17201](https://issues.apache.org/jira/browse/CAMEL-17201)

camel-kamelet - Auto download JARs for new components in use when using regular routes

[CAMEL-17195](https://issues.apache.org/jira/browse/CAMEL-17195)

camel-salesforce: Implement fallbackReplayId for streaming API

[CAMEL-17190](https://issues.apache.org/jira/browse/CAMEL-17190)

camel-quickfix - Quickfix engine not stopped on route stop

[CAMEL-17187](https://issues.apache.org/jira/browse/CAMEL-17187)

camel-xpath - Allow to configure preCompile on @XPath annotation

[CAMEL-17185](https://issues.apache.org/jira/browse/CAMEL-17185)

camel-google-pubsub - Synchronous Pull Consumer disconnected after PubSub server error

[CAMEL-17175](https://issues.apache.org/jira/browse/CAMEL-17175)

Camel-MLLP: option 'logPhi' with value 'false' does not work for exception logging

[CAMEL-17165](https://issues.apache.org/jira/browse/CAMEL-17165)

camel-salesforce - Upgrade to newer API version than v50.0

[CAMEL-17141](https://issues.apache.org/jira/browse/CAMEL-17141)

camel-health - Add field for http error code

[CAMEL-16996](https://issues.apache.org/jira/browse/CAMEL-16996)

camel-kafka: investigate adding component level support to resume strategy

[CAMEL-16912](https://issues.apache.org/jira/browse/CAMEL-16912)

camel-jackson - Make it easy to configure property naming strategy

[CAMEL-16521](https://issues.apache.org/jira/browse/CAMEL-16521)

camel-kafka support string datatype for kafka.OVERRIDE\_TIMESTAMP

[CAMEL-15203](https://issues.apache.org/jira/browse/CAMEL-15203)

camel-salesforce - Camel looses subscription when Invalid Replay ID is trown by SFDC

[CAMEL-15133](https://issues.apache.org/jira/browse/CAMEL-15133)

camel health - Discover custom health checks from classpath

[CAMEL-11078](https://issues.apache.org/jira/browse/CAMEL-11078)

camel-salesforce - Expose HTTP status and message from REST API responses

### New Feature (17)

[CAMEL-17310](https://issues.apache.org/jira/browse/CAMEL-17310)

maven camel:run - Add option for route reload

[CAMEL-17301](https://issues.apache.org/jira/browse/CAMEL-17301)

camel-platform-http - Allow to list known endpoints

[CAMEL-17299](https://issues.apache.org/jira/browse/CAMEL-17299)

camel-jbang - Add --port option to enable embedded http server

[CAMEL-17278](https://issues.apache.org/jira/browse/CAMEL-17278)

camel-jbang - Add run in JVM debug mode

[CAMEL-17272](https://issues.apache.org/jira/browse/CAMEL-17272)

camel-spring-xml - Classic Spring XML add support for external route configuration XML files

[CAMEL-17266](https://issues.apache.org/jira/browse/CAMEL-17266)

camel-google-storage - Include body should use stream caching

[CAMEL-17264](https://issues.apache.org/jira/browse/CAMEL-17264)

camel-core - Properties component should allow reloading properties

[CAMEL-17260](https://issues.apache.org/jira/browse/CAMEL-17260)

camel-core - Reload routes - Should handle non changed routes

[CAMEL-17259](https://issues.apache.org/jira/browse/CAMEL-17259)

camel-jbang - Run to load files using wildcards

[CAMEL-17257](https://issues.apache.org/jira/browse/CAMEL-17257)

camel-core - RouteBuilder should store source location on running routes

[CAMEL-17256](https://issues.apache.org/jira/browse/CAMEL-17256)

camel-jbang - Allow to run multiple files

[CAMEL-17250](https://issues.apache.org/jira/browse/CAMEL-17250)

camel-component-maven-plugin - Add option to easily configure the output directory

[CAMEL-17247](https://issues.apache.org/jira/browse/CAMEL-17247)

camel-atlasmap - Allow to reload file to pickup updates

[CAMEL-17239](https://issues.apache.org/jira/browse/CAMEL-17239)

camel-jbang - Add option to enable colour logging

[CAMEL-17161](https://issues.apache.org/jira/browse/CAMEL-17161)

Support for Azure Copy Blob Operation in Camel component

[CAMEL-17026](https://issues.apache.org/jira/browse/CAMEL-17026)

camel-kafka: add resume support on the producer

[CAMEL-16656](https://issues.apache.org/jira/browse/CAMEL-16656)

camel-core - RoutesLoader SPI - Allow to reload on changes

### Task (9)

[CAMEL-17317](https://issues.apache.org/jira/browse/CAMEL-17317)

camel:run with fileWatcherDirectory property fails

[CAMEL-17300](https://issues.apache.org/jira/browse/CAMEL-17300)

camel-spring-boot - Add route reload example

[CAMEL-17224](https://issues.apache.org/jira/browse/CAMEL-17224)

upgrade maven wrapper to 3.8.4

[CAMEL-17218](https://issues.apache.org/jira/browse/CAMEL-17218)

camel-core - Javadoc on ExchangeHelper/UnitOfWork about original in message null vs exception

[CAMEL-17204](https://issues.apache.org/jira/browse/CAMEL-17204)

Warning message logged for S3 multipart uploads

[CAMEL-17199](https://issues.apache.org/jira/browse/CAMEL-17199)

Review Camel JBang documentation to align CLI usage with Karavan

[CAMEL-17178](https://issues.apache.org/jira/browse/CAMEL-17178)

doc: Fix some wrong links in documentation

[CAMEL-17121](https://issues.apache.org/jira/browse/CAMEL-17121)

Investigate and consolidate do-wait-retry logic in components

[CAMEL-17062](https://issues.apache.org/jira/browse/CAMEL-17062)

camel-dependencies needs a dependency on camel-catalog

### Test (6)

[CAMEL-17285](https://issues.apache.org/jira/browse/CAMEL-17285)

camel-kafka: async manual commit is not working

[CAMEL-17271](https://issues.apache.org/jira/browse/CAMEL-17271)

camel-cm-test - Fix failing CMTest

[CAMEL-17241](https://issues.apache.org/jira/browse/CAMEL-17241)

camel-kafka - Incorrect exception test

[CAMEL-17188](https://issues.apache.org/jira/browse/CAMEL-17188)

camel-support - Flaky test in the new task support

[CAMEL-17176](https://issues.apache.org/jira/browse/CAMEL-17176)

camel-jbpm - Error in an unit test

[CAMEL-17120](https://issues.apache.org/jira/browse/CAMEL-17120)

camel-xmlsecurity - Test cases failing on JDK 8

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).