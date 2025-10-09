# Apache camel 2.21.0 Release

## New and Noteworthy

Welcome to the 2.21.0 release which resolved 400 issues including new features, improvements and bug fixes.

This release supports only Spring Boot 1.5.x. Support for Spring Boot 2.0.x is coming in Camel version 2.22 which is planned for early summer 2018.

-   Upgraded to JAXB 2.3.0 which is more JDK9 compliant.
-   Added better support for `javax.jms.StreamMessage` types in JMS component.
-   Optimised JMS to support ActiveMQ Artemis [http://activemq.apache.org/artemis/docs/latest/large-messages.html\[large](http://activemq.apache.org/artemis/docs/latest/large-messages.html[large) messages\] so you can send and receive big messages such as GB’s in size. There is an example demonstrating this in camel-example-artemis-large-messages.
-   Added support for route coverage reports which allows 3rd party tooling via SPI to visualise route coverage to Camel developers.
-   Added route-coverage goal to the [https://github.com/apache/camel/blob/master/tooling/maven/camel-maven-plugin/src/main/docs/camel-maven-plugin.adoc\[Camel](https://github.com/apache/camel/blob/master/tooling/maven/camel-maven-plugin/src/main/docs/camel-maven-plugin.adoc[Camel) Maven Plugin\] so you can report route coverage from Maven command line.
-   Added support for doing manual commits via Java code when using Kafka consumer.
-   Vendor extensions in the swagger generated API docs is now disabled turned off, when using REST DSL (not all 3rd party API gateways/tooling support vendor extensions). You can turn this back-on via the apiVendorExtension option.
-   The SFTP consumer now also supports the `useList` option which can be used to download a single known file without use LIST operation on the FTP server (which can be slow if the FTP server has many files in the LIST results)
-   Camel JSON with camel-jackson will now automatic use shared ObjectMapper instance if there is only one instance in the Registry. For example users with Spring Boot then allows Camel to easily use the default mapper from Spring Boot.
-   Added `ExtendedStartupListener` that allows a callback just after the CamelContext has been fully started.
-   You can now specify examples in the REST DSL that are included in the generated Swagger api-doc via camel-swagger-java.
-   Improved file/ftp consumer to use current thread to poll, instead of a scheduled background task, when using pollEnrich (content enricher).
-   Direct component now blocks by default if sending to a consumer which is not yet ready, which may happen during startup (little window of opportunity). This avoids `DirectConsumerNotAvailableException` being thrown during startup etc.
-   The FTP component can now log progress (turn on transferLoggingLevel) when perfomring download/upload and other operations. You can also find this information for the consumer in JMX. 
-   Added support for resuming downloads to FTP component. For example if you download big files and has connection problems with the FTP server. Then later when the connectivity works again, Camel can resume download the in-progress file.
-   The Jetty and Servlet consumers will now return HTTP Status 405 (method not allowed) for requests that would have been processed by another HTTP request method, for example calling REST services with the wrong method. Beforehand a 404 error code was always regardless.
-   Reworked the `FileIdempotentRepository` so the internal in-memory cache is only used for quick lookup of the most frequent file names, and lookup from disk as well. See more details in the class javadoc of the file.
-   The SQL Stored Procedure component now supports INOUT parameters.
-   Added restart action to link:controlbus-component.html\[ControlBus Component\] so you can easier restart a route.
-   camel-spring-boot actuator endpoints for routes is now in read-only mode by default. 
-   Added option to Aggregate EIP so make it easier to complete all previous groups on new incoming correlation key, and as well to force completion from Java code logic in the `AggregationStrategy` implementation. 
-   Using AdviceWith for unit testing now logs the routes before vs after in XML format so its easier to spot the change route models.
-   Added support for using SpEL in non-spring runtimes (however there may be functionality that SpEL may only be able to perform if using a Spring runtime).
-   Made it easier to configure timeout options on HTTP4 component.
-   Improvements to RabbitMQ component so for example its easier to route between RabbitMQ exchagnes without having to remove headers or turn on bridgeEndpoint option. Also reduced the logging noise that occurred at INFO level.
-   You can now configure many of the RabbitMQ options on the component level instead of having to repeat them on each endpoint.
-   The Bean component language can now refer to method name via the double colon syntax, eg `.to("bean:myBean::myMethod")`

The following issues has been fixed

-   Fixed afterApplicationStart callback on camel-spring-boot to be called later and after CamelContext has been fully started.
    
-   Fixed an issue testing with @UseAdviceWith and Camel on Spring Boot.
    
-   Fixed OnCompletion would not be triggered from a route using Split EIP and an exception was thrown during splitting.
    
-   Fixed Kafka consumer stops consuming messages when exception occurs during offset commit.
    
-   Fixed Netty4 consumer to stop taking in new requests while being shutdown, as otherwise it cannot graceful shutdown if new requests come in faster than it can process existing in-flight messages.
    
-   Fixed an issue with Routing Slip and Dynamic Router when using context scoped error handler, could cause the error handler to become stopped.
    
-   Fixed Rest DSL with Jetty security via custom define security handler and turned on api-doc as well would not startup Jetty server due missing NoLoginService error.
    
-   Fixed Blueprint error: “name is already instanciated as null and cannot be removed”
    
-   Fixed a CXF continuation timeout issue with camel-cxf consumer could cause the consumer to return a response with data instead of triggering a timeout to the calling SOAP client.
    
-   Fixed camel-cxf consumer doesn’t release UoW when using robust oneway operation
    
-   Fixed using AdviceWith and using weave methods on onException etc. not working.
    
-   Fixed Splitter in parallel processing and streaming mode may block, while iterating message body when the iterator throws exception in first invoked next() method call.
    
-   Fixed Kafka consumer to not auto commit if autoCommitEnable=false.
    
-   Fixed file consumer was using markerFile as read-lock by default, which should have been none.
    
-   Fixed using manual commit with Kafka to provide the current record offset and not the previous (and -1 for first)
    
-   Fixed Content Based Router in Java DSL may not resolve property placeholders in when predicates
    

Important changes to consider when upgrading

-   Jetty has been upgraded to 9.4 by default, and camel-jetty is requring version 9.3 or 9.4 to run in OSGi.
-   Direct component now blocks by default if sending to a consumer which is not yet ready, which may happen during startup (little window of opportunity). This avoids `DirectConsumerNotAvailableException` being thrown during startup etc. The old beavhaior can be turned on by setting `block=false` on the direct component level, or on endpoints where needed.
-   When using `camel-saxon` then the SaxonXpathFactory class is created in the [https://www.saxonica.com/html/documentation/xpath-api/jaxp-xpath/factory.html\[recommended](https://www.saxonica.com/html/documentation/xpath-api/jaxp-xpath/factory.html[recommended) way\] from Saxon. It will fallback and create the factory the old way if not possible.
-   The `camel-json-validator` component has switched from using Everit to NetworkNT JSon Schema validator library, as the former had ASF license implications and would not be allowed in future Camel releases. The NetworkNT supports v4 draft of JSon Schema as validation so make sure to use that draft version in your schemas.
-   Reworked the `FileIdempotentRepository` so the internal in-memory cache is only used for quick lookup of the most frequent file names, and lookup from disk as well. See more details in the class javadoc of the file.
-   The Karaf commands for routes is changed so the arguments for the camel context is first, and the route id is the 2nd argument. This allows the route completer to use the selected camel context name to only show route ids from that camel context, as otherwise it shows all the routes for every Camel application running in Karaf.
-   camel-spring-boot actuator endpoints for routes is now in read-only mode by default. This means operations to start,stop,suspend,resume routes is forbidden. You can turn off read-only mode by setting the spring boot configuration `endpoints.camelroutes.read-only = false`

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
      <version>2.21.0</version>
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
      <version>2.21.0</version>
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
| [apache-camel-2.21.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.21.0/apache-camel-2.21.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.21.0/apache-camel-2.21.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.21.0/apache-camel-2.21.0-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.21.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.21.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (134)

[CAMEL-12342](https://issues.apache.org/jira/browse/CAMEL-12342)

Camel-weather: freegeoip.io has been moved to freegeoip.net

[CAMEL-12340](https://issues.apache.org/jira/browse/CAMEL-12340)

camel uses org.springframework.boot.bind.RelaxedPropertyResolver which is removed from spring 2.0.0

[CAMEL-12335](https://issues.apache.org/jira/browse/CAMEL-12335)

camel-sjms - Potential NPE in consumer

[CAMEL-12333](https://issues.apache.org/jira/browse/CAMEL-12333)

MllpTcpServerConsumer resetting connections on idleTimout

[CAMEL-12328](https://issues.apache.org/jira/browse/CAMEL-12328)

Headers getting lost after calling kubernetes-services API

[CAMEL-12324](https://issues.apache.org/jira/browse/CAMEL-12324)

Issue:Camel rabbitmq publishes message to consumer exchange instead of publisher exchange

[CAMEL-12318](https://issues.apache.org/jira/browse/CAMEL-12318)

Exception from aggregate() of AggregationStrategy has been hiden since Camel 2.16.x

[CAMEL-12315](https://issues.apache.org/jira/browse/CAMEL-12315)

camel-mllp - AutoAcknowledgement issues

[CAMEL-12306](https://issues.apache.org/jira/browse/CAMEL-12306)

String -> Enum type conversion no longer work if Jackson converter is enabled

[CAMEL-12292](https://issues.apache.org/jira/browse/CAMEL-12292)

SnsProducer/SqsProducer setting MessageAttributes with empty values which causes errors

[CAMEL-12291](https://issues.apache.org/jira/browse/CAMEL-12291)

Blueprint error: "name is already instanciated as null and cannot be removed"

[CAMEL-12289](https://issues.apache.org/jira/browse/CAMEL-12289)

URISyntaxException in AbstractSpanDecorator

[CAMEL-12287](https://issues.apache.org/jira/browse/CAMEL-12287)

Allow overriding the server reported endpoint

[CAMEL-12286](https://issues.apache.org/jira/browse/CAMEL-12286)

Milo client broken

[CAMEL-12284](https://issues.apache.org/jira/browse/CAMEL-12284)

camel-beanio - Set encoding option does not work

[CAMEL-12282](https://issues.apache.org/jira/browse/CAMEL-12282)

rest-dsl - Inlined route has route id wrongly assigned

[CAMEL-12279](https://issues.apache.org/jira/browse/CAMEL-12279)

convertBodyTo w/Charset removes existing Charset from Exchange

[CAMEL-12278](https://issues.apache.org/jira/browse/CAMEL-12278)

camel-jsonpath - Should allow to load jackson adapter in OSGi

[CAMEL-12260](https://issues.apache.org/jira/browse/CAMEL-12260)

Default value for String field results in null for CSV / Bindy

[CAMEL-12258](https://issues.apache.org/jira/browse/CAMEL-12258)

use configured readTimeout for initial message

[CAMEL-12256](https://issues.apache.org/jira/browse/CAMEL-12256)

AWS S3 Consumer does not return custom headers in S3 Headers

[CAMEL-12255](https://issues.apache.org/jira/browse/CAMEL-12255)

camel-swagger-java - Body parameter fails to output type

[CAMEL-12249](https://issues.apache.org/jira/browse/CAMEL-12249)

Camel-JMS: transferExchange - send ExchangeProperties can not be accessed before first endpoint in route

[CAMEL-12247](https://issues.apache.org/jira/browse/CAMEL-12247)

camel-undertow not compatible with ahc-version 2.3.0

[CAMEL-12246](https://issues.apache.org/jira/browse/CAMEL-12246)

New AsciiDoc documentation has many broken links

[CAMEL-12244](https://issues.apache.org/jira/browse/CAMEL-12244)

RemoteFileProducer stopped instead of being released to the pool when "interceptSendToEndpoint" is used

[CAMEL-12236](https://issues.apache.org/jira/browse/CAMEL-12236)

Camel-AWS SWF: Region is not set during client creation

[CAMEL-12228](https://issues.apache.org/jira/browse/CAMEL-12228)

Print command fails in case of multiple copies

[CAMEL-12222](https://issues.apache.org/jira/browse/CAMEL-12222)

ResrSwaggerServlet removes last part of context root

[CAMEL-12217](https://issues.apache.org/jira/browse/CAMEL-12217)

Camel REST DSL API - Multiple Content Type - XML Error

[CAMEL-12211](https://issues.apache.org/jira/browse/CAMEL-12211)

Idempotent on camel 2.20.0 and 2.20.1 allows duplication

[CAMEL-12210](https://issues.apache.org/jira/browse/CAMEL-12210)

End of HL7 Message not always detected correctly

[CAMEL-12200](https://issues.apache.org/jira/browse/CAMEL-12200)

camel-mllp - Fix IndexOutOfBounds exception when generating acknowledgment

[CAMEL-12196](https://issues.apache.org/jira/browse/CAMEL-12196)

Mock endpoint - message().body().matches().simple - Does not work

[CAMEL-12195](https://issues.apache.org/jira/browse/CAMEL-12195)

camel redeliveries does not work with hystrix

[CAMEL-12193](https://issues.apache.org/jira/browse/CAMEL-12193)

ThrowException DSL should support no-arg constructors

[CAMEL-12184](https://issues.apache.org/jira/browse/CAMEL-12184)

EventNotifierSupport does not receive ExchangeSentEvents anymore

[CAMEL-12181](https://issues.apache.org/jira/browse/CAMEL-12181)

XML Signature: '#' missing in ObjectReference attribute of XADES element DataObjectFormat

[CAMEL-12176](https://issues.apache.org/jira/browse/CAMEL-12176)

Camel-Dropbox /search and /get are not working

[CAMEL-12166](https://issues.apache.org/jira/browse/CAMEL-12166)

FTPConsumer - no disconnect if polling files fails

[CAMEL-12157](https://issues.apache.org/jira/browse/CAMEL-12157)

Camel-Websocket Karaf feature installs bundles with different version of Jetty (9.4 and 9.3)

[CAMEL-12149](https://issues.apache.org/jira/browse/CAMEL-12149)

Failed to invoke camel cxfrs client due to Content-Type header couldn't be retrieved and passed

[CAMEL-12141](https://issues.apache.org/jira/browse/CAMEL-12141)

Jaxb unmarshall populating wrong value instead of exception when value type given wrong in Camel rest binding mode in rest DSL

[CAMEL-12136](https://issues.apache.org/jira/browse/CAMEL-12136)

camel-saxon - dump namespaces may cause a ClassCastException

[CAMEL-12134](https://issues.apache.org/jira/browse/CAMEL-12134)

spring-boot: two camel contexts created when using xml configuration

[CAMEL-12131](https://issues.apache.org/jira/browse/CAMEL-12131)

CacheProducer should not put services in Camel context, that are not singletons and are not ServicePoolAware

[CAMEL-12123](https://issues.apache.org/jira/browse/CAMEL-12123)

camel-salesforce - Http proxy support uses two inconsistent methods and is broken

[CAMEL-12120](https://issues.apache.org/jira/browse/CAMEL-12120)

ErrorHandler is closed after failure in RoutingSlip

[CAMEL-12112](https://issues.apache.org/jira/browse/CAMEL-12112)

Camel processing single file twice in 'file' endpoint

[CAMEL-12111](https://issues.apache.org/jira/browse/CAMEL-12111)

Reconnect doesn't work if camel is started with rabbit broker initially inaccessible and automaticRecoveryEnabled=true or not set

[CAMEL-12108](https://issues.apache.org/jira/browse/CAMEL-12108)

StreamCache file is removed before wireTap ends in a splitter wireTap combination route

[CAMEL-12103](https://issues.apache.org/jira/browse/CAMEL-12103)

Camel unable to shutdown gracefully because Netty4 consumer keep receiving and adding inflight exchanges

[CAMEL-12101](https://issues.apache.org/jira/browse/CAMEL-12101)

CXF endpoint doesn't work with try/catch when @Oneway is used

[CAMEL-12098](https://issues.apache.org/jira/browse/CAMEL-12098)

URISyntaxException in OpenTracingTracer for endpoints with path parameters

[CAMEL-12097](https://issues.apache.org/jira/browse/CAMEL-12097)

Combination of path param and query param does not work

[CAMEL-12096](https://issues.apache.org/jira/browse/CAMEL-12096)

RestConfiguration hostNameResolver property naming mismatch

[CAMEL-12094](https://issues.apache.org/jira/browse/CAMEL-12094)

fileExist=Move and tempFileName does not work together.

[CAMEL-12086](https://issues.apache.org/jira/browse/CAMEL-12086)

Service call definition - Simple language expresion in uri is not being evaluated

[CAMEL-12085](https://issues.apache.org/jira/browse/CAMEL-12085)

Don't mandate header case for custom Salesforce HTTP haders

[CAMEL-12082](https://issues.apache.org/jira/browse/CAMEL-12082)

Camel route commands should set the TCCL when working with local camel context

[CAMEL-12081](https://issues.apache.org/jira/browse/CAMEL-12081)

XQuery NPE going from saxon 9.5 to 9.7 (upgraded camel from2.17.4-> 2.20.1)

[CAMEL-12076](https://issues.apache.org/jira/browse/CAMEL-12076)

Camel Kafka producer: Specified topic is ignored ("No topic key set" error) when KafkaConfiguration is used

[CAMEL-12075](https://issues.apache.org/jira/browse/CAMEL-12075)

Piling up of threads in iterating splitter in pararllel processing

[CAMEL-12072](https://issues.apache.org/jira/browse/CAMEL-12072)

Netty version in Camel 2.20.0+ not comptatable with Netty in camel-etcd component

[CAMEL-12071](https://issues.apache.org/jira/browse/CAMEL-12071)

aws-sqs queue creation does not support FIFO queues

[CAMEL-12069](https://issues.apache.org/jira/browse/CAMEL-12069)

ActiveMQ/JMS component: transferExchange option does not transfer exchange properties anymore

[CAMEL-12065](https://issues.apache.org/jira/browse/CAMEL-12065)

\[Camel-consul\] firstIndex cannot be set if it is out of Long range

[CAMEL-12063](https://issues.apache.org/jira/browse/CAMEL-12063)

Spring Boot - xmlRoutesReloadDirectory & jmxCreateConnector issue - duplicated JMX

[CAMEL-12062](https://issues.apache.org/jira/browse/CAMEL-12062)

Jaxb component does not communicate charset when explicitly set

[CAMEL-12061](https://issues.apache.org/jira/browse/CAMEL-12061)

SFTP exception-handling more problemtatic than documented

[CAMEL-12058](https://issues.apache.org/jira/browse/CAMEL-12058)

Wrong order in file idempotent store.

[CAMEL-12057](https://issues.apache.org/jira/browse/CAMEL-12057)

camel-olingo2 - Missing encoding for query params

[CAMEL-12038](https://issues.apache.org/jira/browse/CAMEL-12038)

rest-dsl - Allow to turn off vendor extension... NPE

[CAMEL-12037](https://issues.apache.org/jira/browse/CAMEL-12037)

File idempotent repository is always initialized with default 1000 cache size

[CAMEL-12031](https://issues.apache.org/jira/browse/CAMEL-12031)

KafkaConsumer stops consuming messages when exception occurs during offset commit

[CAMEL-12028](https://issues.apache.org/jira/browse/CAMEL-12028)

Flink requires internals to be visible by TCCL

[CAMEL-12025](https://issues.apache.org/jira/browse/CAMEL-12025)

Possible Intermittent failures in ReactorStreamsServiceTest

[CAMEL-12021](https://issues.apache.org/jira/browse/CAMEL-12021)

ProducerTemplate.requestBody with responseType throw a InvalidPayloadException instead of original exception (wrapped in a CamelExecutionException)

[CAMEL-12017](https://issues.apache.org/jira/browse/CAMEL-12017)

Google PubSub and BigQuery components miss dependency declarations

[CAMEL-12016](https://issues.apache.org/jira/browse/CAMEL-12016)

Invalid Pool Exhausted error on camel-netty4

[CAMEL-12009](https://issues.apache.org/jira/browse/CAMEL-12009)

Bindy - Missing Headers from OneToMany Field

[CAMEL-12001](https://issues.apache.org/jira/browse/CAMEL-12001)

Cannot create a component based on the SqlComponent

[CAMEL-11999](https://issues.apache.org/jira/browse/CAMEL-11999)

Cannot create queue/message for Azure

[CAMEL-11996](https://issues.apache.org/jira/browse/CAMEL-11996)

RabbitConsumer could hang when RabbitMQ connection is lost and autoAck=false.

[CAMEL-11992](https://issues.apache.org/jira/browse/CAMEL-11992)

connectors : alias scheme is not used by the connector component

[CAMEL-11988](https://issues.apache.org/jira/browse/CAMEL-11988)

camel-jetty - Problem with latest Spring Boot 1.5.8

[CAMEL-11987](https://issues.apache.org/jira/browse/CAMEL-11987)

Camel-SalesForce DTO Issue while using camel-salesforce-maven

[CAMEL-11986](https://issues.apache.org/jira/browse/CAMEL-11986)

HTTP4 Producer for TLS schemes transforms endpoint URI to \`http4s\`

[CAMEL-11983](https://issues.apache.org/jira/browse/CAMEL-11983)

XsltAggregationStrategy thread safety during initialization

[CAMEL-11980](https://issues.apache.org/jira/browse/CAMEL-11980)

PushTopic client doesn't clear refresh token after a long disconnected period

[CAMEL-11977](https://issues.apache.org/jira/browse/CAMEL-11977)

MongoDB Tailable cursor consumer fails to stop on shutdown

[CAMEL-11976](https://issues.apache.org/jira/browse/CAMEL-11976)

Align pdfbox versions to 2.0.6

[CAMEL-11967](https://issues.apache.org/jira/browse/CAMEL-11967)

Restlet binding should not create jaxb marshaller when binding mode is set to json

[CAMEL-11963](https://issues.apache.org/jira/browse/CAMEL-11963)

camel-spring-boot - Actuator endpoints for MVC should only trigger if web application

[CAMEL-11962](https://issues.apache.org/jira/browse/CAMEL-11962)

AdviceWith weaveAddFirst using onCompletion issue

[CAMEL-11961](https://issues.apache.org/jira/browse/CAMEL-11961)

ClassCastException in HttpMessage

[CAMEL-11955](https://issues.apache.org/jira/browse/CAMEL-11955)

Using @AdviceWith and testing camel-spring-boot startup CamelContext eager

[CAMEL-11953](https://issues.apache.org/jira/browse/CAMEL-11953)

maven connector plugin: connector only properties are ignored in spring boot code generation

[CAMEL-11952](https://issues.apache.org/jira/browse/CAMEL-11952)

XSLT options not set when resource URI is http

[CAMEL-11951](https://issues.apache.org/jira/browse/CAMEL-11951)

Uri matching does not match request type

[CAMEL-11950](https://issues.apache.org/jira/browse/CAMEL-11950)

Inconsistent jar versions with apache curator

[CAMEL-11945](https://issues.apache.org/jira/browse/CAMEL-11945)

camel-spring-boot - CamelContextConfiguration afterApplicationStart should trigger later

[CAMEL-11939](https://issues.apache.org/jira/browse/CAMEL-11939)

asn1 dataformat is not part of xsd for global dataformat

[CAMEL-11938](https://issues.apache.org/jira/browse/CAMEL-11938)

Thrift data format is not part of the xsd for dataformats

[CAMEL-11937](https://issues.apache.org/jira/browse/CAMEL-11937)

Fix syntax for iec60870 component

[CAMEL-11936](https://issues.apache.org/jira/browse/CAMEL-11936)

Fix syntax for Atomix component

[CAMEL-11926](https://issues.apache.org/jira/browse/CAMEL-11926)

close JMXConnector on shutdown of JMXConsumer in camel-jmx

[CAMEL-11925](https://issues.apache.org/jira/browse/CAMEL-11925)

Atmos component fails to load atmos.properties in a modular class loading environment

[CAMEL-11922](https://issues.apache.org/jira/browse/CAMEL-11922)

Persistent tail tracking picks random tail tracker from mongoDB collection

[CAMEL-11920](https://issues.apache.org/jira/browse/CAMEL-11920)

camel-hdfs2 not working in osgi using documented HdfsOsgiHelper

[CAMEL-11917](https://issues.apache.org/jira/browse/CAMEL-11917)

camel-jgroups-starter : JGroupsLockClusterService auto configuration lacks enable flag

[CAMEL-11916](https://issues.apache.org/jira/browse/CAMEL-11916)

camel-jgroups-starter : JGroupsLockClusterServiceConfiguration lacks getter/setters

[CAMEL-11915](https://issues.apache.org/jira/browse/CAMEL-11915)

Fix incorrect elasticsearch5-rest documentation and OperationTypes

[CAMEL-11912](https://issues.apache.org/jira/browse/CAMEL-11912)

Camel Dropbox validator regex is too restrictive and fails for common paths

[CAMEL-11910](https://issues.apache.org/jira/browse/CAMEL-11910)

camel-maven-plugin - validate should not include route ids as consumer urls

[CAMEL-11909](https://issues.apache.org/jira/browse/CAMEL-11909)

camel-catalog-maven - Cannot load out of the box components

[CAMEL-11906](https://issues.apache.org/jira/browse/CAMEL-11906)

Missing compile scope dependencies in camel-pgevent

[CAMEL-11902](https://issues.apache.org/jira/browse/CAMEL-11902)

cluster-service : FileLockClusterView should not always return local member as leader

[CAMEL-11900](https://issues.apache.org/jira/browse/CAMEL-11900)

cluster-service : only the first event listener is notified about cluster events

[CAMEL-11898](https://issues.apache.org/jira/browse/CAMEL-11898)

camel-spring-ws - Attachments are lost

[CAMEL-11896](https://issues.apache.org/jira/browse/CAMEL-11896)

camel-spring-boot - set CamelLogDebugBodyMaxChars when 0 or negative

[CAMEL-11894](https://issues.apache.org/jira/browse/CAMEL-11894)

camel-karaf-commands deployment failed on karaf 4.0

[CAMEL-11889](https://issues.apache.org/jira/browse/CAMEL-11889)

Kie assumes that the TCCL can load its services

[CAMEL-11876](https://issues.apache.org/jira/browse/CAMEL-11876)

OsgiCamelContextPublisher might leak Service-References

[CAMEL-11792](https://issues.apache.org/jira/browse/CAMEL-11792)

New ftp connection for each file transfer with tempFileName option in URI

[CAMEL-11628](https://issues.apache.org/jira/browse/CAMEL-11628)

MQTT Connection loop

[CAMEL-11530](https://issues.apache.org/jira/browse/CAMEL-11530)

RabbitMQ component doesn't handle network failure properly when using autoAck=false and automaticRecovery=true

[CAMEL-11387](https://issues.apache.org/jira/browse/CAMEL-11387)

SFTP is delivered into incorrect location, without exception (file in subfolder + temp file is created + Camel running on Window & SFTP server running on LINUX)

[CAMEL-11370](https://issues.apache.org/jira/browse/CAMEL-11370)

Problem with MTOM in Camel-CXF

[CAMEL-11286](https://issues.apache.org/jira/browse/CAMEL-11286)

Imported Xquery modules will not resolve using classpath - Regression

[CAMEL-11045](https://issues.apache.org/jira/browse/CAMEL-11045)

onCompletion does not trigger on failure if split is in route

[CAMEL-10621](https://issues.apache.org/jira/browse/CAMEL-10621)

Issue with Rest DSL, Jetty and Basic authentication

[CAMEL-10241](https://issues.apache.org/jira/browse/CAMEL-10241)

MockEndpointAndSkip and DirtiesContext not working

[CAMEL-10165](https://issues.apache.org/jira/browse/CAMEL-10165)

DefaultCxfMessageMapper.getBasePath creates a incorrect http path

### Improvement (146)

[CAMEL-12341](https://issues.apache.org/jira/browse/CAMEL-12341)

camel-spring-boot - Add actuator to dump routes in xml format

[CAMEL-12339](https://issues.apache.org/jira/browse/CAMEL-12339)

Add jsonpath to RouteBuilder

[CAMEL-12330](https://issues.apache.org/jira/browse/CAMEL-12330)

camel-rabbitmq - Allow to configure connection settings on component level

[CAMEL-12329](https://issues.apache.org/jira/browse/CAMEL-12329)

camel-rabbitmq - Use another header for exchange override header in producer

[CAMEL-12327](https://issues.apache.org/jira/browse/CAMEL-12327)

camel-infinispan - Add GET check before PUT on add operation in idempontent repository

[CAMEL-12326](https://issues.apache.org/jira/browse/CAMEL-12326)

Improve CamelCxfClientImpl a bit ensure it can handle camel side usecase

[CAMEL-12321](https://issues.apache.org/jira/browse/CAMEL-12321)

camel-bindy - Allow to configure unmarshal to always return a list type

[CAMEL-12314](https://issues.apache.org/jira/browse/CAMEL-12314)

advice with - Log route before vs after advice on startup

[CAMEL-12311](https://issues.apache.org/jira/browse/CAMEL-12311)

Update Braintree SDK to 2.77.0

[CAMEL-12309](https://issues.apache.org/jira/browse/CAMEL-12309)

SpEL expression should be able to reference beans in non-Spring application context

[CAMEL-12308](https://issues.apache.org/jira/browse/CAMEL-12308)

Upgrade to CXF 3.2.2

[CAMEL-12305](https://issues.apache.org/jira/browse/CAMEL-12305)

IntrospectionSupport - Reduce DEBUG logging level

[CAMEL-12296](https://issues.apache.org/jira/browse/CAMEL-12296)

Aggregator - Add option to complete all groups on new correlation id

[CAMEL-12293](https://issues.apache.org/jira/browse/CAMEL-12293)

Avoid KeyAlreadyExistsException in ManagedTypeConverterRegistry.listTypeConverters()

[CAMEL-12283](https://issues.apache.org/jira/browse/CAMEL-12283)

camel-restdsl-swagger-plugin - Allow to filter operations

[CAMEL-12272](https://issues.apache.org/jira/browse/CAMEL-12272)

PgEventEndpoint should handle wrapped connections

[CAMEL-12270](https://issues.apache.org/jira/browse/CAMEL-12270)

camel-http4 - Make it easier to configure connection timeout

[CAMEL-12268](https://issues.apache.org/jira/browse/CAMEL-12268)

Camel-AWS: Lets call shutdown on the clients while stopping endpoints

[CAMEL-12267](https://issues.apache.org/jira/browse/CAMEL-12267)

Make CometD transport properties configurable

[CAMEL-12265](https://issues.apache.org/jira/browse/CAMEL-12265)

Reduce logging caused by load balancer probes

[CAMEL-12254](https://issues.apache.org/jira/browse/CAMEL-12254)

Add restart operation to route JMX mbean

[CAMEL-12253](https://issues.apache.org/jira/browse/CAMEL-12253)

Add restart action to controlbus

[CAMEL-12251](https://issues.apache.org/jira/browse/CAMEL-12251)

Do not hide (so much) blueprint.container.ComponentDefinitionException

[CAMEL-12235](https://issues.apache.org/jira/browse/CAMEL-12235)

Add Timestamp to Message header from ConsumerRecord in the camel-kafka component

[CAMEL-12233](https://issues.apache.org/jira/browse/CAMEL-12233)

spring-boot: add threadNamePattern property

[CAMEL-12226](https://issues.apache.org/jira/browse/CAMEL-12226)

Change HAPI version from 2.2 to 2.3

[CAMEL-12218](https://issues.apache.org/jira/browse/CAMEL-12218)

Make bridgeErrorHandler optional

[CAMEL-12215](https://issues.apache.org/jira/browse/CAMEL-12215)

Add lenient-bind option for MLLP Consumers

[CAMEL-12208](https://issues.apache.org/jira/browse/CAMEL-12208)

CAMEL-AWS Mq: Add UpdateBroker operation

[CAMEL-12206](https://issues.apache.org/jira/browse/CAMEL-12206)

createDoRemove in MongoDbProducer should expect org.bson.conversions.Bson instead of org.bson.Document

[CAMEL-12205](https://issues.apache.org/jira/browse/CAMEL-12205)

Camel-AWS S3: Add parameters to specify S3ClientOptions

[CAMEL-12198](https://issues.apache.org/jira/browse/CAMEL-12198)

Make camel-pgevent work in modular class loading environments

[CAMEL-12197](https://issues.apache.org/jira/browse/CAMEL-12197)

Automatic discovery of LogListener and UuidGenerator

[CAMEL-12194](https://issues.apache.org/jira/browse/CAMEL-12194)

Camel-AWS MQ: Add a reboot broker operation

[CAMEL-12192](https://issues.apache.org/jira/browse/CAMEL-12192)

BindyCsvDataFormat does not support skip fields

[CAMEL-12190](https://issues.apache.org/jira/browse/CAMEL-12190)

Camel-AWS S3: Add a parameter to specify chunkedEncodingDisabled option

[CAMEL-12182](https://issues.apache.org/jira/browse/CAMEL-12182)

Connection should be reset in the event of an acknowledgement timeout

[CAMEL-12178](https://issues.apache.org/jira/browse/CAMEL-12178)

Add getMessage and setMessage methods to the Exchange interface

[CAMEL-12175](https://issues.apache.org/jira/browse/CAMEL-12175)

Camel-AWS Kinesis Firehose: Expose options to avoid a required client in the registry

[CAMEL-12174](https://issues.apache.org/jira/browse/CAMEL-12174)

Camel-AWS Kinesis Firehose: Expose options to avoid a required client in the registry

[CAMEL-12173](https://issues.apache.org/jira/browse/CAMEL-12173)

Camel-AWS Kinesis Firehose: Add the ability to specify credentials and region at component level

[CAMEL-12172](https://issues.apache.org/jira/browse/CAMEL-12172)

Camel-AWS Kinesis: Add the ability to specify credentials and region at component level

[CAMEL-12171](https://issues.apache.org/jira/browse/CAMEL-12171)

Camel-AWS DDB Stream: Add the ability to specify credentials and region at component level

[CAMEL-12165](https://issues.apache.org/jira/browse/CAMEL-12165)

camel-jaxb - Allow to configure severity level on schema validation

[CAMEL-12164](https://issues.apache.org/jira/browse/CAMEL-12164)

Camel-AWS Kinesis: Expose options to avoid a required client in the registry

[CAMEL-12163](https://issues.apache.org/jira/browse/CAMEL-12163)

Camel-AWS Kinesis: Expose options to avoid a required client in the registry

[CAMEL-12162](https://issues.apache.org/jira/browse/CAMEL-12162)

Camel-AWS Kinesis: Expose options to avoid a required client in the registry

[CAMEL-12161](https://issues.apache.org/jira/browse/CAMEL-12161)

Camel-AWS DdbStream: Expose options to avoid a required client in the registry

[CAMEL-12160](https://issues.apache.org/jira/browse/CAMEL-12160)

Camel-AWS Kinesis Firehose: Use a configuration for the options like the other AWS components

[CAMEL-12159](https://issues.apache.org/jira/browse/CAMEL-12159)

Camel-AWS Kinesis: Use a configuration for the options like the other AWS components

[CAMEL-12158](https://issues.apache.org/jira/browse/CAMEL-12158)

Camel-AWS DdbStream: Use a configuration for the options like the other AWS components

[CAMEL-12156](https://issues.apache.org/jira/browse/CAMEL-12156)

Camel Karaf route commands - Should have camel context as required

[CAMEL-12154](https://issues.apache.org/jira/browse/CAMEL-12154)

Camel does not set Saxon parameters in a XQuery 3.0 compatible way

[CAMEL-12152](https://issues.apache.org/jira/browse/CAMEL-12152)

Camel-AWS DDB: Add the ability to specify credentials and region at component level

[CAMEL-12151](https://issues.apache.org/jira/browse/CAMEL-12151)

Camel-AWS CW: Add the ability to specify credentials and region at component level

[CAMEL-12150](https://issues.apache.org/jira/browse/CAMEL-12150)

Camel-AWS EC2: Add the ability to specify credentials and region at component level

[CAMEL-12148](https://issues.apache.org/jira/browse/CAMEL-12148)

File idempotent store - The 1st-level LRUCache should only be a means of quick lookup

[CAMEL-12147](https://issues.apache.org/jira/browse/CAMEL-12147)

Camel-AWS MQ: Add the ability to specify credentials and region at component level

[CAMEL-12146](https://issues.apache.org/jira/browse/CAMEL-12146)

Camel-AWS Lambda: Add the ability to specify credentials and region at component level

[CAMEL-12145](https://issues.apache.org/jira/browse/CAMEL-12145)

Camel-AWS SWF: Add the ability to specify credentials and region at component level

[CAMEL-12144](https://issues.apache.org/jira/browse/CAMEL-12144)

Camel-AWS SNS: Add the ability to specify credentials and region at component level

[CAMEL-12143](https://issues.apache.org/jira/browse/CAMEL-12143)

Camel-AWS SES: Add the ability to specify credentials and region at component level

[CAMEL-12139](https://issues.apache.org/jira/browse/CAMEL-12139)

Camel-AWS SQS: Add the ability to specify credentials and region at component level

[CAMEL-12135](https://issues.apache.org/jira/browse/CAMEL-12135)

Camel-AWS S3: Add the ability to specify credentials and region at component level

[CAMEL-12125](https://issues.apache.org/jira/browse/CAMEL-12125)

Add keepOpen to the ThrottlingExceptionRoutePolicy circuit breaker

[CAMEL-12124](https://issues.apache.org/jira/browse/CAMEL-12124)

Allow to configure cacheSize on dynamic router and routing slip EIP annotations

[CAMEL-12113](https://issues.apache.org/jira/browse/CAMEL-12113)

Camel healthcheck spring-boot actuators don't honor "endpoints.\*.enabled" property

[CAMEL-12110](https://issues.apache.org/jira/browse/CAMEL-12110)

KafkaConsumer swallows exceptions from org.apache.kafka.clients.consumer.KafkaConsumer constructor

[CAMEL-12106](https://issues.apache.org/jira/browse/CAMEL-12106)

Update camel-mllp with enhancements from fork

[CAMEL-12102](https://issues.apache.org/jira/browse/CAMEL-12102)

Improve camel-sap-netweaver documentation

[CAMEL-12099](https://issues.apache.org/jira/browse/CAMEL-12099)

Update camel-thrift to libthrift 0.11.0

[CAMEL-12090](https://issues.apache.org/jira/browse/CAMEL-12090)

camel-kafka - Better error if brokers not configured

[CAMEL-12089](https://issues.apache.org/jira/browse/CAMEL-12089)

Camel-AWS: Kinesis consumer starts consuming data from the beginning even though the shard is in Closed state

[CAMEL-12080](https://issues.apache.org/jira/browse/CAMEL-12080)

Allow creating csv content without last eol

[CAMEL-12079](https://issues.apache.org/jira/browse/CAMEL-12079)

Bean language: support bean::function notation

[CAMEL-12068](https://issues.apache.org/jira/browse/CAMEL-12068)

Camel Undertow support for http2

[CAMEL-12059](https://issues.apache.org/jira/browse/CAMEL-12059)

Remove redundant null checks from instanceof checks

[CAMEL-12056](https://issues.apache.org/jira/browse/CAMEL-12056)

Add NotifyBuilder.destroy() method

[CAMEL-12050](https://issues.apache.org/jira/browse/CAMEL-12050)

Camel Rest DSL returns 404 instead of 405, when http method is not supported

[CAMEL-12047](https://issues.apache.org/jira/browse/CAMEL-12047)

Allow to resolve JSonSchemaResolver from registry

[CAMEL-12046](https://issues.apache.org/jira/browse/CAMEL-12046)

camel-catalog - Add to plugin custom JSonSchemaResolver

[CAMEL-12043](https://issues.apache.org/jira/browse/CAMEL-12043)

Refactor Salesforce Maven plugin

[CAMEL-12036](https://issues.apache.org/jira/browse/CAMEL-12036)

camel-olingo4 support json strings as payload

[CAMEL-12034](https://issues.apache.org/jira/browse/CAMEL-12034)

camel-elasticsearch5 - Search Operation: If Map or String is used in Message Body, "size" and "from" parameters are always ignored

[CAMEL-12033](https://issues.apache.org/jira/browse/CAMEL-12033)

Rethink how default coapMethod URI option is handled

[CAMEL-12032](https://issues.apache.org/jira/browse/CAMEL-12032)

camel-json-validator - Switch to a different validator

[CAMEL-12030](https://issues.apache.org/jira/browse/CAMEL-12030)

Enhance CoAP producer to set a response code header

[CAMEL-12029](https://issues.apache.org/jira/browse/CAMEL-12029)

CoAP component should handle method not allowed

[CAMEL-12027](https://issues.apache.org/jira/browse/CAMEL-12027)

camel-asn1 - removal of import org.openmuc.jasn1.ber.BerByteArrayOutputStream from encode method's param and upgrade jasn1

[CAMEL-12022](https://issues.apache.org/jira/browse/CAMEL-12022)

direct component - Let the producer able to block and wait for consumers to be started

[CAMEL-12020](https://issues.apache.org/jira/browse/CAMEL-12020)

Add dedicated polling consumer for file/ftp components

[CAMEL-12019](https://issues.apache.org/jira/browse/CAMEL-12019)

camel-kafka - Add option max.poll.interval.ms

[CAMEL-12018](https://issues.apache.org/jira/browse/CAMEL-12018)

camel-shiro - Upgrade to 1.4.0

[CAMEL-12014](https://issues.apache.org/jira/browse/CAMEL-12014)

RabbitMQ redelivered flag tag.

[CAMEL-12011](https://issues.apache.org/jira/browse/CAMEL-12011)

Abstract Restlet server creation

[CAMEL-12010](https://issues.apache.org/jira/browse/CAMEL-12010)

Mock endpoint - Should reset StreamCache when evaluating expecations

[CAMEL-12008](https://issues.apache.org/jira/browse/CAMEL-12008)

Add type converter from byte array to java.io.Reader

[CAMEL-12007](https://issues.apache.org/jira/browse/CAMEL-12007)

camel-catalog-maven - Add stop method to cleanup connections

[CAMEL-12004](https://issues.apache.org/jira/browse/CAMEL-12004)

Add LOG.isDebugEnabled() guard for LOG.debug()

[CAMEL-11997](https://issues.apache.org/jira/browse/CAMEL-11997)

camel-archetype-component - Should generate DefaultComponent

[CAMEL-11991](https://issues.apache.org/jira/browse/CAMEL-11991)

camel-swagger-java - Allow to specify type as date format

[CAMEL-11989](https://issues.apache.org/jira/browse/CAMEL-11989)

camel-paho - Allow to specify topic via header

[CAMEL-11985](https://issues.apache.org/jira/browse/CAMEL-11985)

Add ExtendedStartupListener

[CAMEL-11984](https://issues.apache.org/jira/browse/CAMEL-11984)

AggregationStrategy - Let EIPs support lifecycle of custom aggregation strategy to allow custom start/stop logic

[CAMEL-11982](https://issues.apache.org/jira/browse/CAMEL-11982)

camel-jackson - Allow to configure timezone

[CAMEL-11979](https://issues.apache.org/jira/browse/CAMEL-11979)

camel-undertow - swagger api should match on uri prefix

[CAMEL-11978](https://issues.apache.org/jira/browse/CAMEL-11978)

camel-swagger-java - Include 200 status response as default in generated api-doc

[CAMEL-11975](https://issues.apache.org/jira/browse/CAMEL-11975)

camel-connector - Allow to set before/after consumer/producer processors per endpoint

[CAMEL-11971](https://issues.apache.org/jira/browse/CAMEL-11971)

sftp - Add support for useList option to allow consumer to download single file without list operation

[CAMEL-11970](https://issues.apache.org/jira/browse/CAMEL-11970)

JacksonDataFormat does not pickup custom ObjectMapper from Registry

[CAMEL-11968](https://issues.apache.org/jira/browse/CAMEL-11968)

Support literal values in endpoint parameters

[CAMEL-11964](https://issues.apache.org/jira/browse/CAMEL-11964)

Upgrade chemistry-opencmis to 1.1.0

[CAMEL-11960](https://issues.apache.org/jira/browse/CAMEL-11960)

camel-swagger-java - Generated swagger doc should use primitive types

[CAMEL-11958](https://issues.apache.org/jira/browse/CAMEL-11958)

rest-dsl - Disable vendor extension by default

[CAMEL-11957](https://issues.apache.org/jira/browse/CAMEL-11957)

rest-dsl - Allow to turn off vendor extension in generated api docs

[CAMEL-11954](https://issues.apache.org/jira/browse/CAMEL-11954)

Camel JMX name for cluster service

[CAMEL-11948](https://issues.apache.org/jira/browse/CAMEL-11948)

NPE on DefaultMessage setBody if deprecated constructor was used

[CAMEL-11944](https://issues.apache.org/jira/browse/CAMEL-11944)

Ensure HBaseConfiguration ClassLoader is set correctly

[CAMEL-11943](https://issues.apache.org/jira/browse/CAMEL-11943)

camel-kafka - use regular expression to subscribe to topics

[CAMEL-11935](https://issues.apache.org/jira/browse/CAMEL-11935)

Propagate Kafka record headers to camel headers

[CAMEL-11933](https://issues.apache.org/jira/browse/CAMEL-11933)

camel-kafka - Add better support for manual commits

[CAMEL-11932](https://issues.apache.org/jira/browse/CAMEL-11932)

For fixed length records crlf field is not honored during un-marshaling

[CAMEL-11931](https://issues.apache.org/jira/browse/CAMEL-11931)

camel-jms - Add better support for Stream JMS message type

[CAMEL-11929](https://issues.apache.org/jira/browse/CAMEL-11929)

camel-castor - Add more configuration

[CAMEL-11927](https://issues.apache.org/jira/browse/CAMEL-11927)

camel-spring-ws - Support for header transformation

[CAMEL-11919](https://issues.apache.org/jira/browse/CAMEL-11919)

Salesforce REST API request headers not included in update,upsert,create and query operations

[CAMEL-11908](https://issues.apache.org/jira/browse/CAMEL-11908)

camel-swagger-java to support example values

[CAMEL-11901](https://issues.apache.org/jira/browse/CAMEL-11901)

cluster-service : ClusterVie's getMaster() should be renamed to getLeader() for naming consistency

[CAMEL-11899](https://issues.apache.org/jira/browse/CAMEL-11899)

cluster-service : fire event on listener registration

[CAMEL-11895](https://issues.apache.org/jira/browse/CAMEL-11895)

camel-hystrix - Expose state of circuit breaker on JMX / processor

[CAMEL-11890](https://issues.apache.org/jira/browse/CAMEL-11890)

camel-connector - Use JSon parser to parse the camel-connector-schema.json

[CAMEL-11885](https://issues.apache.org/jira/browse/CAMEL-11885)

Add support for creating folder by path in camel-box

[CAMEL-11868](https://issues.apache.org/jira/browse/CAMEL-11868)

Migrate camel-elasticsearch5 java transport client to the new high level rest client

[CAMEL-11863](https://issues.apache.org/jira/browse/CAMEL-11863)

Add camel catalog JARs to the big readme file with overview

[CAMEL-11860](https://issues.apache.org/jira/browse/CAMEL-11860)

camel-oling4 - Upgrade to olingo 4.4

[CAMEL-11836](https://issues.apache.org/jira/browse/CAMEL-11836)

Upgrade to Jetty 9.4.x

[CAMEL-11656](https://issues.apache.org/jira/browse/CAMEL-11656)

Support default directory sorter for FileConsumer

[CAMEL-11599](https://issues.apache.org/jira/browse/CAMEL-11599)

XPath feature with Saxon implementation broken when ServiceMix jaxp-api is present in the endorsed classpath

[CAMEL-11598](https://issues.apache.org/jira/browse/CAMEL-11598)

camel-spring-boot - actuator endpoints - Make it read-only by default

[CAMEL-11532](https://issues.apache.org/jira/browse/CAMEL-11532)

java 8 dsl : allow to set the body using a supplier

[CAMEL-11474](https://issues.apache.org/jira/browse/CAMEL-11474)

Camel-Hipchat: Allow configurable http client

[CAMEL-11224](https://issues.apache.org/jira/browse/CAMEL-11224)

aws-sqs producer does not support new FIFO queues

[CAMEL-10748](https://issues.apache.org/jira/browse/CAMEL-10748)

ServiceNow : add support for Instambul release

[CAMEL-10474](https://issues.apache.org/jira/browse/CAMEL-10474)

Aggregator - Allow aggregate/preAggregate to force complete group

[CAMEL-10258](https://issues.apache.org/jira/browse/CAMEL-10258)

Camel-salesforce-maven-plugin generates classes with checked exception

[CAMEL-7345](https://issues.apache.org/jira/browse/CAMEL-7345)

File/ftp consumer - Implement specific PollingConsumer

### New Feature (45)

[CAMEL-12332](https://issues.apache.org/jira/browse/CAMEL-12332)

camel-csv - Add support for ordered Map in unmarshal

[CAMEL-12316](https://issues.apache.org/jira/browse/CAMEL-12316)

mongodb : Add allowDiskUse option to aggregate operation

[CAMEL-12302](https://issues.apache.org/jira/browse/CAMEL-12302)

camel-mongodb : Support for bulk writes operation

[CAMEL-12295](https://issues.apache.org/jira/browse/CAMEL-12295)

Add an option to Jms Endpoints so that they format JMS date properties according to the ISO 8601 standard

[CAMEL-12280](https://issues.apache.org/jira/browse/CAMEL-12280)

Camel AWS S3: Add other fields in the exchange returned from the consumer

[CAMEL-12275](https://issues.apache.org/jira/browse/CAMEL-12275)

Extend the AWS S3 integration to support the usage of IAM credentials

[CAMEL-12269](https://issues.apache.org/jira/browse/CAMEL-12269)

Bindy - Support regex expression as separator

[CAMEL-12266](https://issues.apache.org/jira/browse/CAMEL-12266)

camel-restdsl-swagger-plugin - Make it possible to chose XML generation

[CAMEL-12237](https://issues.apache.org/jira/browse/CAMEL-12237)

Camel-AWS: Create a KMS component

[CAMEL-12221](https://issues.apache.org/jira/browse/CAMEL-12221)

Let's create a camel-fhir component

[CAMEL-12212](https://issues.apache.org/jira/browse/CAMEL-12212)

sql-stored: support INOUT parameters

[CAMEL-12189](https://issues.apache.org/jira/browse/CAMEL-12189)

Camel-AWS Kinesis Firehose: Add a ComponentVerifier

[CAMEL-12188](https://issues.apache.org/jira/browse/CAMEL-12188)

Camel-AWS Kinesis: Add a ComponentVerifier

[CAMEL-12187](https://issues.apache.org/jira/browse/CAMEL-12187)

Camel-AWS DDBStream: Add a ComponentVerifier

[CAMEL-12186](https://issues.apache.org/jira/browse/CAMEL-12186)

Camel-AWS S3: Support KMS in S3 Producer related operations

[CAMEL-12185](https://issues.apache.org/jira/browse/CAMEL-12185)

mongodb - Add option outputType=DBCursor for aggregate operation

[CAMEL-12183](https://issues.apache.org/jira/browse/CAMEL-12183)

Add support for Wordpress REST API

[CAMEL-12177](https://issues.apache.org/jira/browse/CAMEL-12177)

Dns Routing Policy to start/stop routes based on dns changes.

[CAMEL-12168](https://issues.apache.org/jira/browse/CAMEL-12168)

\[XChange\] Add initial support for market data queries

[CAMEL-12167](https://issues.apache.org/jira/browse/CAMEL-12167)

\[XChange\] Get the list of supported currency pairs

[CAMEL-12137](https://issues.apache.org/jira/browse/CAMEL-12137)

Add Support for Braintree Auth

[CAMEL-12127](https://issues.apache.org/jira/browse/CAMEL-12127)

camel-ftp - Add option to turn on logging of transfer activity

[CAMEL-12126](https://issues.apache.org/jira/browse/CAMEL-12126)

camel-ftp - Add support for restarting downloads

[CAMEL-12122](https://issues.apache.org/jira/browse/CAMEL-12122)

S3: Add createDownloadLink functionality

[CAMEL-12118](https://issues.apache.org/jira/browse/CAMEL-12118)

DynamoDB: Execute query using secondary indexes

[CAMEL-12105](https://issues.apache.org/jira/browse/CAMEL-12105)

Add Additional TypeConverters to camel-hl7

[CAMEL-12074](https://issues.apache.org/jira/browse/CAMEL-12074)

Let okStatusCodeRange support multiple ranges

[CAMEL-12073](https://issues.apache.org/jira/browse/CAMEL-12073)

camel-zipkin - support Zipkin Reporter interface

[CAMEL-12066](https://issues.apache.org/jira/browse/CAMEL-12066)

\[XChange\] Add initial support for crypto currencies

[CAMEL-12055](https://issues.apache.org/jira/browse/CAMEL-12055)

Allow Jt400PgmProducer to call IBM i service programs

[CAMEL-12053](https://issues.apache.org/jira/browse/CAMEL-12053)

Camel-AWS: add a component for Amazon MQ service

[CAMEL-12051](https://issues.apache.org/jira/browse/CAMEL-12051)

Camel-Jsch: Allow to pass the privateKey as byte\[\] and not only via file

[CAMEL-12049](https://issues.apache.org/jira/browse/CAMEL-12049)

Camel-AWS: Add update function operation to AWS lambda component

[CAMEL-12012](https://issues.apache.org/jira/browse/CAMEL-12012)

Camel-AWS: Add component verifiers like S3 for all the AWS components

[CAMEL-12005](https://issues.apache.org/jira/browse/CAMEL-12005)

Add websocket support to camel-undertow

[CAMEL-11995](https://issues.apache.org/jira/browse/CAMEL-11995)

Support Composite API

[CAMEL-11981](https://issues.apache.org/jira/browse/CAMEL-11981)

Camel-AWS: Add a component verifier for AWS S3 and eventually use it for all the other components in Camel-AWS

[CAMEL-11969](https://issues.apache.org/jira/browse/CAMEL-11969)

Camel-AWS: add a deleteObject operation to the S3 Producer

[CAMEL-11959](https://issues.apache.org/jira/browse/CAMEL-11959)

New component YQL

[CAMEL-11949](https://issues.apache.org/jira/browse/CAMEL-11949)

Camel-Elasticsearch5-Rest: Add a Ping Operation to Producer

[CAMEL-11923](https://issues.apache.org/jira/browse/CAMEL-11923)

Camel-Hessian: Add Whitelisting feature

[CAMEL-11665](https://issues.apache.org/jira/browse/CAMEL-11665)

Define a saga DSL and implementation for long running actions

[CAMEL-11637](https://issues.apache.org/jira/browse/CAMEL-11637)

Unable to assign null value to a Salesforce object field

[CAMEL-8958](https://issues.apache.org/jira/browse/CAMEL-8958)

Add push/pop to the DSL so people can easily preserve and get back a message as-is

[CAMEL-8657](https://issues.apache.org/jira/browse/CAMEL-8657)

Add Maven Plugin to generate route coverage report

### Sub-task (3)

[CAMEL-12240](https://issues.apache.org/jira/browse/CAMEL-12240)

Create a real tests with Apache Qpid Broker-J

[CAMEL-11823](https://issues.apache.org/jira/browse/CAMEL-11823)

\[example\] cdi-cassandrasql - nodetool: Failed to connect to '127.0.0.1:7199' - ConnectException: 'Connection refused'

[CAMEL-11367](https://issues.apache.org/jira/browse/CAMEL-11367)

Provide equivalent support for XML REST DSL

### Task (58)

[CAMEL-12338](https://issues.apache.org/jira/browse/CAMEL-12338)

Add a Camel-Xchange Karaf feature

[CAMEL-12313](https://issues.apache.org/jira/browse/CAMEL-12313)

camel-maven-plugin - Add docs about run goal options

[CAMEL-12312](https://issues.apache.org/jira/browse/CAMEL-12312)

camel-undertow - Add examples to doc about using websocket

[CAMEL-12310](https://issues.apache.org/jira/browse/CAMEL-12310)

Update maven-bundle-plugin

[CAMEL-12304](https://issues.apache.org/jira/browse/CAMEL-12304)

camel-spring-sources - Misses some source files

[CAMEL-12303](https://issues.apache.org/jira/browse/CAMEL-12303)

Make building camel-spring and camel-blueprint work for XSD generation more cleanly

[CAMEL-12299](https://issues.apache.org/jira/browse/CAMEL-12299)

Upgrade to jcloud 2.1.x

[CAMEL-12297](https://issues.apache.org/jira/browse/CAMEL-12297)

Miscellaneous fixes to AsciiDoc format and layout

[CAMEL-12273](https://issues.apache.org/jira/browse/CAMEL-12273)

In component doc, tables are sometimes generated without body rows

[CAMEL-12262](https://issues.apache.org/jira/browse/CAMEL-12262)

DEFAULT\_CIPHER\_SUITES\_FILTER\_EXCLUDE Incorrect

[CAMEL-12261](https://issues.apache.org/jira/browse/CAMEL-12261)

Camel-AWS KMS: Add a scheduleKeyDeletion operation

[CAMEL-12248](https://issues.apache.org/jira/browse/CAMEL-12248)

Camel-Milo: Upgrade Milo to version 0.2.0

[CAMEL-12242](https://issues.apache.org/jira/browse/CAMEL-12242)

camel-wordpres feature

[CAMEL-12241](https://issues.apache.org/jira/browse/CAMEL-12241)

camel-elasticsearch5-rest karaf feature

[CAMEL-12239](https://issues.apache.org/jira/browse/CAMEL-12239)

Camel-Kubernetes: Renamed Openshift component with the openshift prefix

[CAMEL-12234](https://issues.apache.org/jira/browse/CAMEL-12234)

Camel-AWS: Since we are using builders, we need to remove the AWS endpoint options on the components that are using them

[CAMEL-12231](https://issues.apache.org/jira/browse/CAMEL-12231)

Camel-Amqp: Use Netty 4.1.x since Qpid-jms-client now use that version

[CAMEL-12227](https://issues.apache.org/jira/browse/CAMEL-12227)

camel-ahc - Upgrade to 2.3.0 version

[CAMEL-12225](https://issues.apache.org/jira/browse/CAMEL-12225)

Documentation - Should include a link id in top of file

[CAMEL-12224](https://issues.apache.org/jira/browse/CAMEL-12224)

Camel-Elasticsearch5-rest: deprecate camel-elasticsearch5 in favor of this component, rename it and upgrade it to support ES 6.x

[CAMEL-12223](https://issues.apache.org/jira/browse/CAMEL-12223)

camel-json-validator: Documentation and comments in code incorrectly mentions everit

[CAMEL-12204](https://issues.apache.org/jira/browse/CAMEL-12204)

camel-lra - Be JAX-RS 2.0 compatible

[CAMEL-12203](https://issues.apache.org/jira/browse/CAMEL-12203)

camel-fop - Upgrade to make it work again

[CAMEL-12180](https://issues.apache.org/jira/browse/CAMEL-12180)

camel-braintree - Downgrade to version without org.json

[CAMEL-12155](https://issues.apache.org/jira/browse/CAMEL-12155)

Indicate Camel-Dozer major upgrade in Camel 2.20 release note and specify how to migrate

[CAMEL-12153](https://issues.apache.org/jira/browse/CAMEL-12153)

Upgrade to OpenTracing Java API 0.31

[CAMEL-12133](https://issues.apache.org/jira/browse/CAMEL-12133)

Update Camel documentation for ThrottlingExceptionRoutePolicy

[CAMEL-12130](https://issues.apache.org/jira/browse/CAMEL-12130)

Upgrade braintree SDK to v2.74.0

[CAMEL-12115](https://issues.apache.org/jira/browse/CAMEL-12115)

Camel-Consul: Upgrade to 1.0.0 consul client

[CAMEL-12088](https://issues.apache.org/jira/browse/CAMEL-12088)

camel-zipkin - Karaf feature dont work with new upgrade

[CAMEL-12083](https://issues.apache.org/jira/browse/CAMEL-12083)

Some camel karaf features errors

[CAMEL-12064](https://issues.apache.org/jira/browse/CAMEL-12064)

Create a camel-example-olingo4-blueprint example

[CAMEL-12054](https://issues.apache.org/jira/browse/CAMEL-12054)

Camel-AWS Xray: Create the related Karaf feature

[CAMEL-12044](https://issues.apache.org/jira/browse/CAMEL-12044)

\[quartz2\] Duplicate initializaiton of Quartz component

[CAMEL-12024](https://issues.apache.org/jira/browse/CAMEL-12024)

Camel-CassandraQL: Add ErrorAwarePolicy to the Load Balancing Policies set

[CAMEL-12023](https://issues.apache.org/jira/browse/CAMEL-12023)

Camel CassandraQL: move configuration in a separated class

[CAMEL-12015](https://issues.apache.org/jira/browse/CAMEL-12015)

dead link in webpage http://camel.apache.org/log.html

[CAMEL-12013](https://issues.apache.org/jira/browse/CAMEL-12013)

Pull Request, Camel example AMQP Artemis

[CAMEL-11993](https://issues.apache.org/jira/browse/CAMEL-11993)

Upgrade to CXF 3.2.1

[CAMEL-11972](https://issues.apache.org/jira/browse/CAMEL-11972)

Upgrade to Kafka 1.0.0

[CAMEL-11965](https://issues.apache.org/jira/browse/CAMEL-11965)

camel BOM (and camel-hl7) lack the optional dependency to hapi-structures-v251

[CAMEL-11946](https://issues.apache.org/jira/browse/CAMEL-11946)

Invalid artifactId in docs for camel-json-validator

[CAMEL-11942](https://issues.apache.org/jira/browse/CAMEL-11942)

camel-spring build failure on windows

[CAMEL-11941](https://issues.apache.org/jira/browse/CAMEL-11941)

Online xsd is not the latest 2.20 one

[CAMEL-11924](https://issues.apache.org/jira/browse/CAMEL-11924)

DOAP has moved

[CAMEL-11921](https://issues.apache.org/jira/browse/CAMEL-11921)

Camel-Elasticsearch5-rest: Create Karaf feature

[CAMEL-11913](https://issues.apache.org/jira/browse/CAMEL-11913)

Upgrade to Spring Boot 2.0.0.M5

[CAMEL-11907](https://issues.apache.org/jira/browse/CAMEL-11907)

No test coverage for camel-pgevent

[CAMEL-11903](https://issues.apache.org/jira/browse/CAMEL-11903)

camel-checkstyle.xml - Should say Camel instead of ActiveMQ

[CAMEL-11874](https://issues.apache.org/jira/browse/CAMEL-11874)

spring-boot: shrink camel-spring-boot dependencies

[CAMEL-11869](https://issues.apache.org/jira/browse/CAMEL-11869)

Adopt mockito-core 2.11.0

[CAMEL-11858](https://issues.apache.org/jira/browse/CAMEL-11858)

Deprecate non working karaf features

[CAMEL-11856](https://issues.apache.org/jira/browse/CAMEL-11856)

camel-olingo4 : create karaf feature

[CAMEL-11822](https://issues.apache.org/jira/browse/CAMEL-11822)

Upgade jaxb-core

[CAMEL-11773](https://issues.apache.org/jira/browse/CAMEL-11773)

Popup message about SyntaxHiglighter when accessing camel 2.20 release note page

[CAMEL-11606](https://issues.apache.org/jira/browse/CAMEL-11606)

camel-olingo4 doesn't work in OSGi environments

[CAMEL-10837](https://issues.apache.org/jira/browse/CAMEL-10837)

Migrate EIP patterns to adoc

[CAMEL-10613](https://issues.apache.org/jira/browse/CAMEL-10613)

Upgrade to restlet 2.3.12

### Test (10)

[CAMEL-12301](https://issues.apache.org/jira/browse/CAMEL-12301)

camel-itest-spring-boot - CamelOpenTracing fails

[CAMEL-12300](https://issues.apache.org/jira/browse/CAMEL-12300)

camel-example - AMQP blueprint fails test

[CAMEL-12298](https://issues.apache.org/jira/browse/CAMEL-12298)

camel-aws - Unit test failure

[CAMEL-12209](https://issues.apache.org/jira/browse/CAMEL-12209)

StringHelperTest.testHumanReadableBytes() is not repeatable

[CAMEL-12142](https://issues.apache.org/jira/browse/CAMEL-12142)

Tests failed because of incorrect mongodb host

[CAMEL-12129](https://issues.apache.org/jira/browse/CAMEL-12129)

Broken integration test RabbitMQSupendResumeIntTest

[CAMEL-12084](https://issues.apache.org/jira/browse/CAMEL-12084)

Test encoding for query params in camel-olingo4

[CAMEL-12040](https://issues.apache.org/jira/browse/CAMEL-12040)

camel-example-cdi-rest-servlet - Test error due jetty JAR problem

[CAMEL-12039](https://issues.apache.org/jira/browse/CAMEL-12039)

camel-itest - Errors in some test about xslt 1.0 mode

[CAMEL-11845](https://issues.apache.org/jira/browse/CAMEL-11845)

Migrate easymock and powermock to mockito

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).