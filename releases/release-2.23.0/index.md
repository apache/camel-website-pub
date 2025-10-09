# Apache camel 2.23.0 Release

## New and Noteworthy

Welcome to the Apache Camel 2.23.0 release which is a new minor release and resolved 262 issues including new features, improvements and bux fixes.

-   Upgraded to Spring Boot 2.1.
-   Additional component level options can now be configured via spring-boot auto-configuration and these options is included in spring-boot component metadata json file descriptor for tooling assistance.
-   Added section with all the spring boot auto configuration options for all the components, data-formats and languages to the documentation.
-   All the Camel Spring Boot starter JARs now include META-INF/spring-autoconfigure-metadata.properties file in their JARs to optimize Spring Boot auto-configuration
-   The Throttler now supports correlation groups based on dynamic expression so you can group messages into different throttled sets.
-   The Hystrix EIP now allows to inherit Camel’s error handler so you retry the entire Hystrix EIP block again if you have enabled error handling with redeliveries.
-   SQL and ElSql consumers now support dynamic query parameters in route from. Notice it’s limited to be mostly about calling beans via simple expressions.
-   The swagger-restdsl maven plugin now has supports for generating DTO model classes from the swagger specification file.

The following noteworthy bugs has been fixed:

-   The Aggregator2 has been fixed to not propagate control headers for forcing completion of all groups, so it will not happen again if another aggregator EIP are in use later during routing.
-   Fixed Tracer not working if redelivery was turned on the error handler
-   The built-in type converter for XML Documents may output parsing errors to stdout, which has now been fixed to output via the logging API.
-   Fixed SFTP writing files via the charset option would not work if the message body was streaming based.
-   Fixed Zipkin root id to not be reused when routing over multiple routes to group them together into a single parent span.
-   Fixed optimised toD when using HTTP endpoints had a bug when hostname contains ip address with digits.
-   Fixed issue with RabbitMQ with request/reply over temporary queues and using manual acknowledge mode, would not acknowledge the temporary queue (which is needed to make request/reply possible)
-   Fixed various HTTP consumer components may not return all allowed HTTP verbs in Allow header for OPTIONS requests (such as when using rest-dsl)
-   Fixed thread-safety issue with FluentProducerTemplate

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
      <version>2.23.0</version>
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
      <version>2.23.0</version>
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
| [apache-camel-2.23.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.23.0/apache-camel-2.23.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.23.0/apache-camel-2.23.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.23.0/apache-camel-2.23.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.23.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.23.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (116)

[CAMEL-13651](https://issues.apache.org/jira/browse/CAMEL-13651)

Rest DSL seems to duplicate the routes, therefore we can experience on having duplicated ids issues

[CAMEL-12986](https://issues.apache.org/jira/browse/CAMEL-12986)

Salesforce streaming api breaks after access token expires and a timeout happens when re logging in.

[CAMEL-12943](https://issues.apache.org/jira/browse/CAMEL-12943)

Rest DSL generates invalid swagger operation Id

[CAMEL-12942](https://issues.apache.org/jira/browse/CAMEL-12942)

camel-dropbox: upload file does not work

[CAMEL-12940](https://issues.apache.org/jira/browse/CAMEL-12940)

Dynamic doneFileName is not working with filename containing 2 dots

[CAMEL-12933](https://issues.apache.org/jira/browse/CAMEL-12933)

Camel FTP regression: RemoteFile does not override populateHeaders method

[CAMEL-12932](https://issues.apache.org/jira/browse/CAMEL-12932)

Camel-AHC-WS: Consumer parameters are not set

[CAMEL-12929](https://issues.apache.org/jira/browse/CAMEL-12929)

error in camel-core/src/main/docs/rest-dsl.adoc

[CAMEL-12926](https://issues.apache.org/jira/browse/CAMEL-12926)

null pointer exceptions accessing swagger url in blueprint projects

[CAMEL-12916](https://issues.apache.org/jira/browse/CAMEL-12916)

camel-http4 - The sslContextParameters option should be documented on endpoint as well

[CAMEL-12912](https://issues.apache.org/jira/browse/CAMEL-12912)

Action Request Converter is reseting ID on index request to header that is not set

[CAMEL-12911](https://issues.apache.org/jira/browse/CAMEL-12911)

gzip Content-Encoding problems after upgrading to Jetty 9.4.12

[CAMEL-12908](https://issues.apache.org/jira/browse/CAMEL-12908)

Cannot start route using rest dsl due to a mysterious duplicate routeId

[CAMEL-12905](https://issues.apache.org/jira/browse/CAMEL-12905)

Camel context inconsistencies in Spring Cloud Environment

[CAMEL-12900](https://issues.apache.org/jira/browse/CAMEL-12900)

Route contract validate does not throw validation exception when validation fails

[CAMEL-12899](https://issues.apache.org/jira/browse/CAMEL-12899)

Handle LinkedIn Captcha redirects gracefully

[CAMEL-12897](https://issues.apache.org/jira/browse/CAMEL-12897)

PGP Decryption in XML DSL not working

[CAMEL-12893](https://issues.apache.org/jira/browse/CAMEL-12893)

Swagger REST DSL generator not honoring basePath

[CAMEL-12891](https://issues.apache.org/jira/browse/CAMEL-12891)

camel-kubernetes getConfigMap does not use Namespace Header

[CAMEL-12890](https://issues.apache.org/jira/browse/CAMEL-12890)

Camel Printer unable to print to the network printer

[CAMEL-12888](https://issues.apache.org/jira/browse/CAMEL-12888)

The camel-maven-package-plugin issue wrong short java type

[CAMEL-12883](https://issues.apache.org/jira/browse/CAMEL-12883)

WeaveByType not working for OnExceptionDefinition in camel 2.21.0

[CAMEL-12882](https://issues.apache.org/jira/browse/CAMEL-12882)

Camel Jms headers missing if producer endpoint has transferExchange=true

[CAMEL-12880](https://issues.apache.org/jira/browse/CAMEL-12880)

Atom consumer stops polling

[CAMEL-12874](https://issues.apache.org/jira/browse/CAMEL-12874)

Camel-google-calendar-stream: Last update date must consider UpdatedMin field instead of TimeMin when used

[CAMEL-12873](https://issues.apache.org/jira/browse/CAMEL-12873)

camel-servlet - Example for HttpRegistry no longer works throwing FinalModifierException

[CAMEL-12870](https://issues.apache.org/jira/browse/CAMEL-12870)

make cxf consumer endpoints suspendable

[CAMEL-12867](https://issues.apache.org/jira/browse/CAMEL-12867)

Camel-Slack: Must configure Consumer before using it.

[CAMEL-12860](https://issues.apache.org/jira/browse/CAMEL-12860)

Camel-AWS IAM: The accessKey delete operation need to specify an AccessKey Id instead of a username

[CAMEL-12852](https://issues.apache.org/jira/browse/CAMEL-12852)

Fix unstable test PubNubPresenceTest

[CAMEL-12850](https://issues.apache.org/jira/browse/CAMEL-12850)

camel-ftp tries reconnects twice as much as maximumReconnectAttempts

[CAMEL-12848](https://issues.apache.org/jira/browse/CAMEL-12848)

camel-sftp : on windows stepwise = true change directory fails to change directory

[CAMEL-12844](https://issues.apache.org/jira/browse/CAMEL-12844)

splitter with grouping looses encoding property

[CAMEL-12843](https://issues.apache.org/jira/browse/CAMEL-12843)

CamelContext Start command shouldn't start a Suspended context

[CAMEL-12842](https://issues.apache.org/jira/browse/CAMEL-12842)

"-" dash is not a valid characters for keys in JMS headers

[CAMEL-12838](https://issues.apache.org/jira/browse/CAMEL-12838)

Camel Twitter Send Direct Message Endpoint not working

[CAMEL-12836](https://issues.apache.org/jira/browse/CAMEL-12836)

Type Converter Loader Exception: Elasticsearch-Rest cannot find any in package defined

[CAMEL-12835](https://issues.apache.org/jira/browse/CAMEL-12835)

camel-json-validator - Potential issue with reading from streams

[CAMEL-12831](https://issues.apache.org/jira/browse/CAMEL-12831)

Camel-zipkin: useFallbackServiceNames leaks passwords

[CAMEL-12830](https://issues.apache.org/jira/browse/CAMEL-12830)

FTP producer stuck if timeout occurs just after connect

[CAMEL-12829](https://issues.apache.org/jira/browse/CAMEL-12829)

An autocreated CXF Bus not shut down in CxfSpringEndpoint

[CAMEL-12827](https://issues.apache.org/jira/browse/CAMEL-12827)

camel-http-common HttpSendDynamicAware setting port to -1 when port is not defined in uri

[CAMEL-12826](https://issues.apache.org/jira/browse/CAMEL-12826)

Camel Grape component is missing documentation for some endpoints

[CAMEL-12821](https://issues.apache.org/jira/browse/CAMEL-12821)

Fix MQTT URI param typo

[CAMEL-12820](https://issues.apache.org/jira/browse/CAMEL-12820)

SQS: Malformed queue URL due to bad region parsing

[CAMEL-12809](https://issues.apache.org/jira/browse/CAMEL-12809)

Threading issues with the throttler when using a correlation key

[CAMEL-12807](https://issues.apache.org/jira/browse/CAMEL-12807)

Avoid to use endpoint attribute when MqttConnectOptions is declared once

[CAMEL-12805](https://issues.apache.org/jira/browse/CAMEL-12805)

camel-restdsl-swagger-plugin doesn't convert integer default value to string

[CAMEL-12787](https://issues.apache.org/jira/browse/CAMEL-12787)

Accept header is not respected anymore in CXFRS consumer when POST

[CAMEL-12786](https://issues.apache.org/jira/browse/CAMEL-12786)

Option readLockLoggingLevel not working for SFTP changed read lock strategy

[CAMEL-12785](https://issues.apache.org/jira/browse/CAMEL-12785)

ServletComponent ignores httpBinding option

[CAMEL-12782](https://issues.apache.org/jira/browse/CAMEL-12782)

swagger-java - Provide more clear exception when model class is not visible to ClassResolver

[CAMEL-12780](https://issues.apache.org/jira/browse/CAMEL-12780)

Regression in Camel Salesforce - consumer blocks producer in same route

[CAMEL-12779](https://issues.apache.org/jira/browse/CAMEL-12779)

camel-spring-redis - When stopping consumer it should stop the message listener

[CAMEL-12778](https://issues.apache.org/jira/browse/CAMEL-12778)

CamelCatalog - Should be JMX compliant

[CAMEL-12775](https://issues.apache.org/jira/browse/CAMEL-12775)

Using StubComponent can block routes depending on MEP

[CAMEL-12774](https://issues.apache.org/jira/browse/CAMEL-12774)

Error during type conversion from type: java.lang.String to the required type: org.elasticsearch.action.update.UpdateRequest

[CAMEL-12769](https://issues.apache.org/jira/browse/CAMEL-12769)

Combination of File consumer with charset and Split DSL with XPath doesn't parse XML correctly

[CAMEL-12762](https://issues.apache.org/jira/browse/CAMEL-12762)

camel-sjms - MessageProducer is not closed when using shared session

[CAMEL-12758](https://issues.apache.org/jira/browse/CAMEL-12758)

SOAP request causing null namespace URI in SimpleNsStreamWriter camel-cxf/woodstox

[CAMEL-12753](https://issues.apache.org/jira/browse/CAMEL-12753)

OPTIONS Http request on REST resource returns incorrect content of Allow header

[CAMEL-12748](https://issues.apache.org/jira/browse/CAMEL-12748)

Netty4 and Restlet components should support SSLContextParameters

[CAMEL-12746](https://issues.apache.org/jira/browse/CAMEL-12746)

Temporary reply queues being created with main endpoint autoAck setting

[CAMEL-12745](https://issues.apache.org/jira/browse/CAMEL-12745)

NullPointerException in APT IOHelper

[CAMEL-12744](https://issues.apache.org/jira/browse/CAMEL-12744)

Restlet when used as client doesn't use the configured SSL properties

[CAMEL-12741](https://issues.apache.org/jira/browse/CAMEL-12741)

SjmsMessage should set Exchange in copyFrom

[CAMEL-12740](https://issues.apache.org/jira/browse/CAMEL-12740)

Olingo4Component creates and ignores HttpAsyncClientBuilder

[CAMEL-12739](https://issues.apache.org/jira/browse/CAMEL-12739)

TypeConverters are not registered to all contexts

[CAMEL-12733](https://issues.apache.org/jira/browse/CAMEL-12733)

camel-sftp : stepwise=false is not working on windows

[CAMEL-12732](https://issues.apache.org/jira/browse/CAMEL-12732)

Kafka manual commit to file repository doesn't work properly (using Spring boot)

[CAMEL-12728](https://issues.apache.org/jira/browse/CAMEL-12728)

Configured SSL Context on Undertow component not honored by camel-rest-swagger

[CAMEL-12727](https://issues.apache.org/jira/browse/CAMEL-12727)

java.util.ConcurrentModificationException at org.apache.camel.impl.DefaultExchange.createProperties(DefaultExchange.java:550) in 2.20.1

[CAMEL-12726](https://issues.apache.org/jira/browse/CAMEL-12726)

FindBugs warnings: Invocation of toString on an array

[CAMEL-12725](https://issues.apache.org/jira/browse/CAMEL-12725)

\[ERROR\] /sobject-pojo-optional.vm: Encountered "(" at line 64, column 8.

[CAMEL-12724](https://issues.apache.org/jira/browse/CAMEL-12724)

Simple SFTP-to-File integration with charset options fails

[CAMEL-12720](https://issues.apache.org/jira/browse/CAMEL-12720)

Krati implementation does not work properly persistence after put operation.

[CAMEL-12713](https://issues.apache.org/jira/browse/CAMEL-12713)

relative paths can remove scheme from xslt URI

[CAMEL-12709](https://issues.apache.org/jira/browse/CAMEL-12709)

UseOriginalAggregationStrategy in outer loops

[CAMEL-12705](https://issues.apache.org/jira/browse/CAMEL-12705)

Optimising toD via SendDynamicAware component removes the 3rd octet from IP address

[CAMEL-12703](https://issues.apache.org/jira/browse/CAMEL-12703)

Support JSON as a ContentType for JobInfo

[CAMEL-12701](https://issues.apache.org/jira/browse/CAMEL-12701)

servicenow: meta data serivce ignores tables without parent when retrieving table list

[CAMEL-12690](https://issues.apache.org/jira/browse/CAMEL-12690)

Annotation processors used in build should error out

[CAMEL-12689](https://issues.apache.org/jira/browse/CAMEL-12689)

EndpointRegistry, TransformerRegistry and ValidatorRegistry use wrong generics

[CAMEL-12685](https://issues.apache.org/jira/browse/CAMEL-12685)

relative references for nested xslt inclusions don't get resolved

[CAMEL-12681](https://issues.apache.org/jira/browse/CAMEL-12681)

BreadcrumbId not required for aws-sqs aws-sns endpoints

[CAMEL-12680](https://issues.apache.org/jira/browse/CAMEL-12680)

Fix syntax for micrometer endpoint

[CAMEL-12659](https://issues.apache.org/jira/browse/CAMEL-12659)

MllpTcpServerConsumer logging failure to set HL7 headers even when setting HL7 headers is disabled

[CAMEL-12656](https://issues.apache.org/jira/browse/CAMEL-12656)

camel-zipkin - Root Span Id is not reported if the route calls multiple route

[CAMEL-12654](https://issues.apache.org/jira/browse/CAMEL-12654)

RabbitMQ Headers - Headers with null value are skipped.

[CAMEL-12648](https://issues.apache.org/jira/browse/CAMEL-12648)

ExchangeSentEvent not fired if no EventNotifier is accepting ExchangeSendingEvent

[CAMEL-12647](https://issues.apache.org/jira/browse/CAMEL-12647)

Problem in setting region for camel AWS-SQS endpoint

[CAMEL-12638](https://issues.apache.org/jira/browse/CAMEL-12638)

DefaultFluentProducerTemplate is not thread safe

[CAMEL-12637](https://issues.apache.org/jira/browse/CAMEL-12637)

XmlConverter can't transform StAXSource when external xalan lib available

[CAMEL-12635](https://issues.apache.org/jira/browse/CAMEL-12635)

Potential NPE in CamelEndpointDetails.hashCode method

[CAMEL-12630](https://issues.apache.org/jira/browse/CAMEL-12630)

Better attachment handling in camel-mail component

[CAMEL-12626](https://issues.apache.org/jira/browse/CAMEL-12626)

Camel Tracing is not working for route with redelivery strategy

[CAMEL-12624](https://issues.apache.org/jira/browse/CAMEL-12624)

ActiveMQ Artemis AMQP integration issue with topic prefix hardcode

[CAMEL-12621](https://issues.apache.org/jira/browse/CAMEL-12621)

Rest DSL with Jetty9|netty4-http components returns 404 instead of 405, when http method is not supported

[CAMEL-12613](https://issues.apache.org/jira/browse/CAMEL-12613)

Camel file endpoint loses modification date and length information when preMove is used

[CAMEL-12610](https://issues.apache.org/jira/browse/CAMEL-12610)

Camel bean component invokes cached instance of bean (that impl processor) in Registry

[CAMEL-12607](https://issues.apache.org/jira/browse/CAMEL-12607)

When using Tokenizer skipFirst - java.util.NoSuchElementException if only one element

[CAMEL-12603](https://issues.apache.org/jira/browse/CAMEL-12603)

Thread stuck in re-delivery loop after interrupting it

[CAMEL-12594](https://issues.apache.org/jira/browse/CAMEL-12594)

Rest Producer - Query Parameters : Wrong query parameter name is used when header substitution is performed

[CAMEL-12593](https://issues.apache.org/jira/browse/CAMEL-12593)

Source and javadoc jars not published to snapshot maven repository

[CAMEL-12590](https://issues.apache.org/jira/browse/CAMEL-12590)

Type converter confusion when camel-cxf and camel-mail are in same classpath

[CAMEL-12589](https://issues.apache.org/jira/browse/CAMEL-12589)

Surviving Header AGGREGATION\_COMPLETE\_ALL\_GROUPS\_INCLUSIVE affects following aggregations

[CAMEL-12575](https://issues.apache.org/jira/browse/CAMEL-12575)

camel-cxfrs: NPE on GET request with Content-Type header

[CAMEL-12571](https://issues.apache.org/jira/browse/CAMEL-12571)

Seda component forgets URI setting when duplicates are present

[CAMEL-12565](https://issues.apache.org/jira/browse/CAMEL-12565)

outputTypeWithValidate (or inputTypeWithValidate) + validator()... doesn't work as expected

[CAMEL-12548](https://issues.apache.org/jira/browse/CAMEL-12548)

NullPointerException in camel-cmis when using wrong credentials

[CAMEL-12525](https://issues.apache.org/jira/browse/CAMEL-12525)

camel-kafka component commits the offset as soon as it is retrieved

[CAMEL-12484](https://issues.apache.org/jira/browse/CAMEL-12484)

Camel-salesforce component does not try to reconnect on specific error

[CAMEL-12414](https://issues.apache.org/jira/browse/CAMEL-12414)

Empty/null response from netty4-http template producer

[CAMEL-12410](https://issues.apache.org/jira/browse/CAMEL-12410)

No type converter from java.lang.String to java.math.BigInteger required for firstIndex

[CAMEL-12229](https://issues.apache.org/jira/browse/CAMEL-12229)

Some RabbitMQ channels are never started when target queue doesn't exist during component startup

[CAMEL-12087](https://issues.apache.org/jira/browse/CAMEL-12087)

camel-core: WARN No CamelContext defined yet so cannot inject into bean

### Improvement (75)

[CAMEL-12931](https://issues.apache.org/jira/browse/CAMEL-12931)

Upgrade jBPM component to use 7 series with consumer capability to react to produced events by jBPM

[CAMEL-12924](https://issues.apache.org/jira/browse/CAMEL-12924)

Camel-Elasticsearch-rest: Use not deprecated methods after the client upgrade

[CAMEL-12922](https://issues.apache.org/jira/browse/CAMEL-12922)

camel-JGroups "Keeping singleton route within the cluster" documentation outdated

[CAMEL-12921](https://issues.apache.org/jira/browse/CAMEL-12921)

Camel-AWS SQS: Add an option to create a SQS delay queue

[CAMEL-12903](https://issues.apache.org/jira/browse/CAMEL-12903)

camel-core : add service definition header to service call

[CAMEL-12878](https://issues.apache.org/jira/browse/CAMEL-12878)

camel-jpa: Allow for passing named-query parameters via message header and/or body

[CAMEL-12869](https://issues.apache.org/jira/browse/CAMEL-12869)

ReplyTo destination must match endpoint type (topic or queue) that the message is sent on

[CAMEL-12865](https://issues.apache.org/jira/browse/CAMEL-12865)

camel-restdsl-swagger-plugin - Allow for specifying apiContextPath

[CAMEL-12833](https://issues.apache.org/jira/browse/CAMEL-12833)

Do CDI CamelContext creation with an apporpriate TCCL

[CAMEL-12832](https://issues.apache.org/jira/browse/CAMEL-12832)

Improve Camel CDI context XML resource loading

[CAMEL-12813](https://issues.apache.org/jira/browse/CAMEL-12813)

Camel-netty4: Add DEBUG log when codecs does not apply to the provided content

[CAMEL-12806](https://issues.apache.org/jira/browse/CAMEL-12806)

Camel-Slack: Add a check on the messages list while consuming

[CAMEL-12771](https://issues.apache.org/jira/browse/CAMEL-12771)

Do not use deprecated methods on ObjectHelper

[CAMEL-12770](https://issues.apache.org/jira/browse/CAMEL-12770)

Allow endpoints to migrate from the dynamic to the static map in the endpoint registry

[CAMEL-12768](https://issues.apache.org/jira/browse/CAMEL-12768)

Upgrade camel-dozer to dozer v6.4.1

[CAMEL-12763](https://issues.apache.org/jira/browse/CAMEL-12763)

Improve the logic to related the consumer to the producer in the direct component

[CAMEL-12761](https://issues.apache.org/jira/browse/CAMEL-12761)

Upgrade to JUnit 4

[CAMEL-12756](https://issues.apache.org/jira/browse/CAMEL-12756)

\`@ConditionalOnProperty\` target property with no metadata

[CAMEL-12751](https://issues.apache.org/jira/browse/CAMEL-12751)

http producer - Ignore content length header

[CAMEL-12749](https://issues.apache.org/jira/browse/CAMEL-12749)

MultiSearchRequest in elasticsearch rest plugin

[CAMEL-12735](https://issues.apache.org/jira/browse/CAMEL-12735)

XmlRouteParser does not handle usage of xml namespace prefix for camel

[CAMEL-12729](https://issues.apache.org/jira/browse/CAMEL-12729)

Align Swagger and Rest DSL implementation for camel-example-spring-boot-rest-\* examples

[CAMEL-12717](https://issues.apache.org/jira/browse/CAMEL-12717)

Upgrade camel-dozer to dozer v6.4.0

[CAMEL-12714](https://issues.apache.org/jira/browse/CAMEL-12714)

support handlers in cxf payload data format without SEI

[CAMEL-12711](https://issues.apache.org/jira/browse/CAMEL-12711)

SFTP: Cannot specify bind address of local network interface

[CAMEL-12710](https://issues.apache.org/jira/browse/CAMEL-12710)

Projects depending upon java-hamcrest have different versions of some classes on the classpath

[CAMEL-12707](https://issues.apache.org/jira/browse/CAMEL-12707)

Docker integration test profiles should respect the skipTests property

[CAMEL-12704](https://issues.apache.org/jira/browse/CAMEL-12704)

Include all IDE Toolings in http://camel.apache.org/tools.html

[CAMEL-12702](https://issues.apache.org/jira/browse/CAMEL-12702)

camel-spring-boot - Improve its auto configuration docs

[CAMEL-12699](https://issues.apache.org/jira/browse/CAMEL-12699)

Unable to combine retry with Hystrix circuit breaker

[CAMEL-12698](https://issues.apache.org/jira/browse/CAMEL-12698)

Unmarshaling a CSV file with the NEL (next line) character will cause Bindy to misread the entire file

[CAMEL-12697](https://issues.apache.org/jira/browse/CAMEL-12697)

Add hapi-structures-v21 to camel-parent

[CAMEL-12696](https://issues.apache.org/jira/browse/CAMEL-12696)

Update dozer docs

[CAMEL-12693](https://issues.apache.org/jira/browse/CAMEL-12693)

Upgrade camel-dozer to dozer v6.3.0

[CAMEL-12692](https://issues.apache.org/jira/browse/CAMEL-12692)

Add camel-as2 to camel-parent POM

[CAMEL-12691](https://issues.apache.org/jira/browse/CAMEL-12691)

Allow configuration of org.xml.sax.ErrorHandler on DocumentBuilders used in Camel

[CAMEL-12688](https://issues.apache.org/jira/browse/CAMEL-12688)

Improve Camel startup performances

[CAMEL-12687](https://issues.apache.org/jira/browse/CAMEL-12687)

camel-itest-spring-boot : update shrinkwrap & arquillian versions with changes in ArquillianPackager

[CAMEL-12682](https://issues.apache.org/jira/browse/CAMEL-12682)

Custom ApplicationContextRegistry extension NOT discovered

[CAMEL-12679](https://issues.apache.org/jira/browse/CAMEL-12679)

ensure camel-xmlsecurity can try key directly to decrypt message

[CAMEL-12675](https://issues.apache.org/jira/browse/CAMEL-12675)

Camel-Nats: Add a way to provide a connection to Nats server already instantiated

[CAMEL-12674](https://issues.apache.org/jira/browse/CAMEL-12674)

Update sshd-version

[CAMEL-12673](https://issues.apache.org/jira/browse/CAMEL-12673)

enable to configure passPhrase of XMLSecurityDataFormat as byte\[\]

[CAMEL-12670](https://issues.apache.org/jira/browse/CAMEL-12670)

Camel-Nats: add authentication examples

[CAMEL-12669](https://issues.apache.org/jira/browse/CAMEL-12669)

Camel-Nats: add new client options available with client 2.x

[CAMEL-12667](https://issues.apache.org/jira/browse/CAMEL-12667)

camel-spring-boot - Turn of options with @NestedConfigurationProperty in generated auto configuration source

[CAMEL-12661](https://issues.apache.org/jira/browse/CAMEL-12661)

Spring Boot auto configuration - NestedConfigurationProperty should only be for known Camel types

[CAMEL-12660](https://issues.apache.org/jira/browse/CAMEL-12660)

Spring Boot configuration documentation should be polished

[CAMEL-12653](https://issues.apache.org/jira/browse/CAMEL-12653)

JaxbDataFormat.unmarshal should use passed Exchange when converting given InputStream into XMLStreamReader

[CAMEL-12650](https://issues.apache.org/jira/browse/CAMEL-12650)

Log messages that do not match with their method function

[CAMEL-12646](https://issues.apache.org/jira/browse/CAMEL-12646)

camel-spring-boot - Auto configuration of complex types should be more tooling friendly

[CAMEL-12645](https://issues.apache.org/jira/browse/CAMEL-12645)

camel-jdbc - Allow to use default datasource from spring-boot

[CAMEL-12643](https://issues.apache.org/jira/browse/CAMEL-12643)

camel-rabbitmq - Inadequate information for handling catch clauses

[CAMEL-12641](https://issues.apache.org/jira/browse/CAMEL-12641)

Aws-sns and aws-sqs components not accepting Date type message attributes

[CAMEL-12640](https://issues.apache.org/jira/browse/CAMEL-12640)

tooling - Provide character position in validation result

[CAMEL-12639](https://issues.apache.org/jira/browse/CAMEL-12639)

tooling - Provide line numbers for CamelEndpointDetails for java dsl

[CAMEL-12636](https://issues.apache.org/jira/browse/CAMEL-12636)

camel-jmx - Should use a thread pool for routing notifications

[CAMEL-12634](https://issues.apache.org/jira/browse/CAMEL-12634)

Automate Artmemis download and config for camel-example-artemis-\*

[CAMEL-12633](https://issues.apache.org/jira/browse/CAMEL-12633)

camel-jmx - Add support for monitoring boolean attribute changes

[CAMEL-12631](https://issues.apache.org/jira/browse/CAMEL-12631)

SFTP: Socket timeout overwrites Server Alive Interval

[CAMEL-12628](https://issues.apache.org/jira/browse/CAMEL-12628)

\[doc\] camel-hawtdb documentation should be updated

[CAMEL-12627](https://issues.apache.org/jira/browse/CAMEL-12627)

Use Spring Boot autoconfigure-processor to optimize auto-configurations

[CAMEL-12622](https://issues.apache.org/jira/browse/CAMEL-12622)

camel-ssh - Potential NullPointerException due to unboxing if channel.getExitStatus() is null

[CAMEL-12609](https://issues.apache.org/jira/browse/CAMEL-12609)

DefaultExchangeFormatter: Make it easy to override the header and property formatting

[CAMEL-12597](https://issues.apache.org/jira/browse/CAMEL-12597)

camel-servlet - Add whitelist for accepted file types

[CAMEL-12587](https://issues.apache.org/jira/browse/CAMEL-12587)

camel-zipkin-starter fails mapping service names

[CAMEL-12554](https://issues.apache.org/jira/browse/CAMEL-12554)

camel-geocoder - Use new API

[CAMEL-12546](https://issues.apache.org/jira/browse/CAMEL-12546)

rest-dsl - Allow to configure rest configuration via spring boot auto configuration

[CAMEL-12520](https://issues.apache.org/jira/browse/CAMEL-12520)

FluentProducerTemplate.withExchange() does not seem to send exchange

[CAMEL-12519](https://issues.apache.org/jira/browse/CAMEL-12519)

camel-snmp - add treeList option of given PDU has child elements but will be resulted as list

[CAMEL-12320](https://issues.apache.org/jira/browse/CAMEL-12320)

camel-restlet - Should match better on uri pattern and return 404 for invalid urls

[CAMEL-12114](https://issues.apache.org/jira/browse/CAMEL-12114)

Have XmlLineNumberParser respecting namespace uri

[CAMEL-11783](https://issues.apache.org/jira/browse/CAMEL-11783)

Updates to http://camel.apache.org/rest-dsl.html

[CAMEL-11687](https://issues.apache.org/jira/browse/CAMEL-11687)

Camel-spring-boot documentation should also cover testing

[CAMEL-11327](https://issues.apache.org/jira/browse/CAMEL-11327)

Improve Salesforce streaming consumer shutdown

### New Feature (31)

[CAMEL-12950](https://issues.apache.org/jira/browse/CAMEL-12950)

Create a Camel Google Sheets component

[CAMEL-12925](https://issues.apache.org/jira/browse/CAMEL-12925)

Camel-Slack: Consumer must be able to use a different server than the default one

[CAMEL-12917](https://issues.apache.org/jira/browse/CAMEL-12917)

Camel-NSQ: Add Karaf feature

[CAMEL-12884](https://issues.apache.org/jira/browse/CAMEL-12884)

Camel-AWS Lambda: Add support for event source mapping

[CAMEL-12859](https://issues.apache.org/jira/browse/CAMEL-12859)

Camel-AWS: Add more operations to the AWS IAM producer

[CAMEL-12855](https://issues.apache.org/jira/browse/CAMEL-12855)

camel-swagger-java not honoring the x-forwarded-\[host,proto,prefix\] headers.

[CAMEL-12847](https://issues.apache.org/jira/browse/CAMEL-12847)

IntrospectionSupport - Allow to use dash style naming

[CAMEL-12846](https://issues.apache.org/jira/browse/CAMEL-12846)

Allow customization of REST API documentation Content-Type

[CAMEL-12841](https://issues.apache.org/jira/browse/CAMEL-12841)

camel-restdsl-swagger:generate - Add restConfiguration with common defaults

[CAMEL-12828](https://issues.apache.org/jira/browse/CAMEL-12828)

camel-restdsl-swagger:generate - Add option to generate dto objects

[CAMEL-12824](https://issues.apache.org/jira/browse/CAMEL-12824)

camel-route-parser - Add parser for rest-dsl

[CAMEL-12822](https://issues.apache.org/jira/browse/CAMEL-12822)

camel-http4 - Expose connection pool stats in JMX

[CAMEL-12810](https://issues.apache.org/jira/browse/CAMEL-12810)

\[IPFS\] Add initial support for IPFS

[CAMEL-12784](https://issues.apache.org/jira/browse/CAMEL-12784)

Create a Camel-google-calendar-stream component

[CAMEL-12747](https://issues.apache.org/jira/browse/CAMEL-12747)

Camel-Slack: Add consumer

[CAMEL-12734](https://issues.apache.org/jira/browse/CAMEL-12734)

camel-sql - Add support for basic dynamic query parameters in consumer

[CAMEL-12721](https://issues.apache.org/jira/browse/CAMEL-12721)

camel-zipkin - Add support for easy enabling of logging integration

[CAMEL-12666](https://issues.apache.org/jira/browse/CAMEL-12666)

Create push tag operation

[CAMEL-12651](https://issues.apache.org/jira/browse/CAMEL-12651)

Allow to override serializing and deserializing default mechanism for kafka headers

[CAMEL-12649](https://issues.apache.org/jira/browse/CAMEL-12649)

Upgrade Braintree SDK to 2.83.1 and Expose Transaction Fees API

[CAMEL-12644](https://issues.apache.org/jira/browse/CAMEL-12644)

Generate documentation for Spring Boot starters

[CAMEL-12642](https://issues.apache.org/jira/browse/CAMEL-12642)

No support for http4 feature authenticationPreemptive in pollEnrich

[CAMEL-12629](https://issues.apache.org/jira/browse/CAMEL-12629)

came-ssh - add support for Channel.CHANNEL\_SHELL command execution

[CAMEL-12625](https://issues.apache.org/jira/browse/CAMEL-12625)

Create FHIR Camel component with example

[CAMEL-12238](https://issues.apache.org/jira/browse/CAMEL-12238)

Camel-AWS: Create an IAM component

[CAMEL-12170](https://issues.apache.org/jira/browse/CAMEL-12170)

\[XChange\] Add initial support for account management

[CAMEL-12109](https://issues.apache.org/jira/browse/CAMEL-12109)

camel-zipkin - Generate tracing identifiers on exchange begin if they do not exist

[CAMEL-11803](https://issues.apache.org/jira/browse/CAMEL-11803)

Add Support for Salesforce Platform Events

[CAMEL-11158](https://issues.apache.org/jira/browse/CAMEL-11158)

Camel-Kubernetes: Add support for Job resources

[CAMEL-6840](https://issues.apache.org/jira/browse/CAMEL-6840)

Allow Throttler EIP to specify SLA per client/correlated-group

[CAMEL-5558](https://issues.apache.org/jira/browse/CAMEL-5558)

Add fileExist option to write file with a new name in case file already exists

### Sub-task (5)

[CAMEL-12663](https://issues.apache.org/jira/browse/CAMEL-12663)

camel-api-component-maven-plugin unable to parse Java 11 style Javadoc

[CAMEL-12616](https://issues.apache.org/jira/browse/CAMEL-12616)

Disable or remove camel-example-ceylon

[CAMEL-12615](https://issues.apache.org/jira/browse/CAMEL-12615)

tools.jar missing in Java 9+ needed by camel-chronicle-starter

[CAMEL-12614](https://issues.apache.org/jira/browse/CAMEL-12614)

Missing javax.xml.bind.DatatypeConverter in camel-asn1 on Java 9+

[CAMEL-10968](https://issues.apache.org/jira/browse/CAMEL-10968)

camel-cxf tests fails on Java 9

### Task (33)

[CAMEL-12902](https://issues.apache.org/jira/browse/CAMEL-12902)

<qpid-bundle-version> is no longer needed and is confusing

[CAMEL-12886](https://issues.apache.org/jira/browse/CAMEL-12886)

Various asynchronous engine issues

[CAMEL-12881](https://issues.apache.org/jira/browse/CAMEL-12881)

Fix the camel-infinispan integration test

[CAMEL-12849](https://issues.apache.org/jira/browse/CAMEL-12849)

Camel-AWS MQ: Add a describeBroker operation to the producer side

[CAMEL-12816](https://issues.apache.org/jira/browse/CAMEL-12816)

Checkstyle issues in components

[CAMEL-12802](https://issues.apache.org/jira/browse/CAMEL-12802)

Camel-google-mail, Camel-google-mail-stream: Add Google Mail verifier Extension

[CAMEL-12781](https://issues.apache.org/jira/browse/CAMEL-12781)

Published Async Documentation is missing code samples

[CAMEL-12777](https://issues.apache.org/jira/browse/CAMEL-12777)

Checkstyle issues

[CAMEL-12760](https://issues.apache.org/jira/browse/CAMEL-12760)

deprecate camel-xmlrpc

[CAMEL-12759](https://issues.apache.org/jira/browse/CAMEL-12759)

Misleading documentation for Netty components

[CAMEL-12757](https://issues.apache.org/jira/browse/CAMEL-12757)

add camel-jclouds-starter

[CAMEL-12755](https://issues.apache.org/jira/browse/CAMEL-12755)

Upgrade Infinispan

[CAMEL-12754](https://issues.apache.org/jira/browse/CAMEL-12754)

Upgrade Apache Ignite

[CAMEL-12752](https://issues.apache.org/jira/browse/CAMEL-12752)

Upgrade jetty to 9.4.11

[CAMEL-12743](https://issues.apache.org/jira/browse/CAMEL-12743)

Some @link javadoc notations not handled well in auto-generated adocs

[CAMEL-12742](https://issues.apache.org/jira/browse/CAMEL-12742)

Upgrade maven wrapper to 0.4.2

[CAMEL-12736](https://issues.apache.org/jira/browse/CAMEL-12736)

Create FHIR authorization and transaction quickstart

[CAMEL-12731](https://issues.apache.org/jira/browse/CAMEL-12731)

FindBugs warnings: Array formatted in useless way using format string

[CAMEL-12730](https://issues.apache.org/jira/browse/CAMEL-12730)

FindBugs warnings: Suspicious reference comparison

[CAMEL-12716](https://issues.apache.org/jira/browse/CAMEL-12716)

Some spring-boot-starters generated have wrong component name in their javadoc documentation

[CAMEL-12715](https://issues.apache.org/jira/browse/CAMEL-12715)

camel-script - Upgrade to Groovy 2.5.1 and check camel-itest-karaf and feature.

[CAMEL-12706](https://issues.apache.org/jira/browse/CAMEL-12706)

camel-as2 - Missing documentation for some options

[CAMEL-12700](https://issues.apache.org/jira/browse/CAMEL-12700)

Checkstyle issues in camel-core

[CAMEL-12677](https://issues.apache.org/jira/browse/CAMEL-12677)

Create FHIR spring boot quickstart

[CAMEL-12664](https://issues.apache.org/jira/browse/CAMEL-12664)

Camel-Nats: Bump to version 2.0.0 of Jnats

[CAMEL-12658](https://issues.apache.org/jira/browse/CAMEL-12658)

camel-weather: Freegeoip service is no longer avaiable, we need to switch to apilayer IPstack

[CAMEL-12632](https://issues.apache.org/jira/browse/CAMEL-12632)

Pass CXF service class to EndpointInfo

[CAMEL-12612](https://issues.apache.org/jira/browse/CAMEL-12612)

Camel-RabbitMQ: Add support for Exclusive Consumer

[CAMEL-12611](https://issues.apache.org/jira/browse/CAMEL-12611)

Deprecate camel-mongodb

[CAMEL-12583](https://issues.apache.org/jira/browse/CAMEL-12583)

Camel-Kubernetes: Add an HPA component

[CAMEL-12549](https://issues.apache.org/jira/browse/CAMEL-12549)

Upgrade to Groovy 2.5

[CAMEL-12479](https://issues.apache.org/jira/browse/CAMEL-12479)

Remove support for XML format in for Salesforce limits API

[CAMEL-11325](https://issues.apache.org/jira/browse/CAMEL-11325)

Upgrade to Apache Spark 2.x

### Test (3)

[CAMEL-12918](https://issues.apache.org/jira/browse/CAMEL-12918)

Camel-NSQ: Add Karaf and Spring Boot Integration tests

[CAMEL-12914](https://issues.apache.org/jira/browse/CAMEL-12914)

camel-rest-swagger - Unit test fails after jetty upgrade

[CAMEL-12853](https://issues.apache.org/jira/browse/CAMEL-12853)

camel-sftp: SftpConsumerDisconnectTest.testConsumeDelete almost always fail

### Wish (1)

[CAMEL-12486](https://issues.apache.org/jira/browse/CAMEL-12486)

Placeholders are not resolved in Simple language while using resource: prefix

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).