# Apache camel 2.22.0 Release

## New and Noteworthy

Welcome to the 2.22.0 release which resolved 216 issues including new features, improvements and bug fixes.

This release supports only Spring Boot 2. Spring Boot v1 is no longer supported.

-   Camel has upgraded from Spring Boot v1 to v2 and therefore v1 is no longer supported.
    
-   Upgraded to Spring Framework 5. Camel should work with Spring 4.3.x as well, but going forward Spring 5.x will be the minimum Spring version in future releases.
    
-   Upgraded to Karaf 4.2. You may run Camel on Karaf 4.1 but we only officially support Karaf 4.2 in this release.
    
-   Optimised using toD DSL to reuse endpoints and producers for components where its possible. For example HTTP based components will now reuse producer (http clients) with dynamic uris sending to the same host. See more details in the toD documentation.
    
-   The File2 consumer with read-lock idempotent/idempotent-changed can now be configured to delay the release tasks to expand the window when a file is regarded as in-process, which is usable in active/active cluster settings with a shared idempotent repository to ensure other nodes dont too quickly see a processed file as a file they can process (only needed if you have readLockRemoveOnCommit=true).
    
-   Allow to plugin a custom request/reply correlation id manager implementation on Netty4 producer in request/reply mode. The Twitter component now uses extended mode by default to support tweets > 140 characters
    
-   Rest DSL producer now supports being configured in rest configuration via endpointProperties.
    
-   The Kafka component now supports HeaderFilterStrategy to plugin custom implementations for controlling header mappings between Camel and Kafka messages.
    
-   Rest DSL now supports client request validation to validate that Content-Type/Accept headers is possible for the rest service.
    
-   Camel has now a Service Registry SPI which allow to register routes to a service registry such as consul, etcd, zookeeper using a Camel implementation or Spring Cloud
    
-   The SEDA component now has a default queue size of 1000 instead of unlimited. And these important fixes:
    
-   Fixed a CXF continuation timeout issue with camel-cxf consumer could cause the consumer to return a response with data instead of triggering a timeout to the calling SOAP client.
    
-   Fixed camel-cxf consumer doesn’t release UoW when using robust oneway operation
    
-   Fixed using AdviceWith and using weave methods on onException etc. not working.
    
-   Fixed Splitter in parallel processing and streaming mode may block, while iterating message body when the iterator throws exception in first invoked next() method call.
    
-   Fixed Kafka consumer to not auto commit if autoCommitEnable=false.
    
-   Fixed file consumer was using markerFile as read-lock by default, which should have been none.
    
-   Fixed using manual commit with Kafka to provide the current record offset and not the previous (and -1 for first)
    
-   Fixed Content Based Router in Java DSL may not resolve property placeholders in when predicates
    

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
      <version>2.22.0</version>
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
      <version>2.22.0</version>
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
| [apache-camel-2.22.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.22.0/apache-camel-2.22.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.22.0/apache-camel-2.22.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.22.0/apache-camel-2.22.0-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.22.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.22.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (70)

[CAMEL-13004](https://issues.apache.org/jira/browse/CAMEL-13004)

Camel Proxy/Bridge - Premature end of Content-Length delimited message body

[CAMEL-12606](https://issues.apache.org/jira/browse/CAMEL-12606)

regression in camel test blueprint behaviour

[CAMEL-12602](https://issues.apache.org/jira/browse/CAMEL-12602)

Camel Wordpress don't set basic authentication even if user and password are provided

[CAMEL-12601](https://issues.apache.org/jira/browse/CAMEL-12601)

camel-bindy: DefaultFactoryRegistry.unregister throws ConcurrentModificationException

[CAMEL-12581](https://issues.apache.org/jira/browse/CAMEL-12581)

Camel-google-mail: Remove scopes from configuration. This option is never really used.

[CAMEL-12577](https://issues.apache.org/jira/browse/CAMEL-12577)

Re-apply CAMEL-12104 Unintuitive default cxf timeout behavior

[CAMEL-12573](https://issues.apache.org/jira/browse/CAMEL-12573)

ClassCastException thrown KafkaSpanDecorator

[CAMEL-12570](https://issues.apache.org/jira/browse/CAMEL-12570)

Support fixed property placeholders from Aries blueprint

[CAMEL-12568](https://issues.apache.org/jira/browse/CAMEL-12568)

camel-univocity-parsers: Upgrade to version 2.6.4 once released

[CAMEL-12562](https://issues.apache.org/jira/browse/CAMEL-12562)

camel-dns: starter ignores serviceCall EIP configuration

[CAMEL-12561](https://issues.apache.org/jira/browse/CAMEL-12561)

camel-kubernetes: serviceCall EIP throws NullPointerException

[CAMEL-12560](https://issues.apache.org/jira/browse/CAMEL-12560)

camel-kubernetes: serviceCall EIP configuration is not read from application.properties

[CAMEL-12558](https://issues.apache.org/jira/browse/CAMEL-12558)

camel-catalog - Transacted and Policy should not have outputs

[CAMEL-12555](https://issues.apache.org/jira/browse/CAMEL-12555)

saga-eip: do not hang if option cannot be computed

[CAMEL-12551](https://issues.apache.org/jira/browse/CAMEL-12551)

Camel does not have logic that checks that it should only retry when its a new/changed file

[CAMEL-12550](https://issues.apache.org/jira/browse/CAMEL-12550)

Camel-Twilio: Karaf feature is not working

[CAMEL-12548](https://issues.apache.org/jira/browse/CAMEL-12548)

NullPointerException in camel-cmis when using wrong credentials

[CAMEL-12541](https://issues.apache.org/jira/browse/CAMEL-12541)

camel-cxfrs - rsClient does not work programmatically, only with XML

[CAMEL-12540](https://issues.apache.org/jira/browse/CAMEL-12540)

We should avoid the address setting of CxfRsEndpointConfigurer

[CAMEL-12536](https://issues.apache.org/jira/browse/CAMEL-12536)

camel-google-mail: adding the camel component to a spring boot project leads to java.lang.NoSuchMethodError: javax.servlet.ServletContext.getClassLoader()Ljava/lang/ClassLoader;

[CAMEL-12535](https://issues.apache.org/jira/browse/CAMEL-12535)

Fix syntax for wordpress component

[CAMEL-12532](https://issues.apache.org/jira/browse/CAMEL-12532)

Content Based Router in Java DSL may not resolve property placeholders in when predicates

[CAMEL-12511](https://issues.apache.org/jira/browse/CAMEL-12511)

camel-consul - NPE on ConsulEventConsumer start

[CAMEL-12506](https://issues.apache.org/jira/browse/CAMEL-12506)

SqsProducer doesn't support Boolean attributes

[CAMEL-12500](https://issues.apache.org/jira/browse/CAMEL-12500)

Incorrect URL for AWS SQS queues

[CAMEL-12498](https://issues.apache.org/jira/browse/CAMEL-12498)

One of the camel-jcache tests is failing

[CAMEL-12497](https://issues.apache.org/jira/browse/CAMEL-12497)

Fix CXF-Blueprint tests

[CAMEL-12491](https://issues.apache.org/jira/browse/CAMEL-12491)

route-coverage : report summary problem

[CAMEL-12490](https://issues.apache.org/jira/browse/CAMEL-12490)

Camel-jms: ClassNotFoundException: org.springframework.messaging.handler.annotation.support.MessageHandlerMethodFactory in Spring-Boot

[CAMEL-12487](https://issues.apache.org/jira/browse/CAMEL-12487)

S3Producer must close the streams it opens

[CAMEL-12483](https://issues.apache.org/jira/browse/CAMEL-12483)

route-coverage : endChoice() problem

[CAMEL-12480](https://issues.apache.org/jira/browse/CAMEL-12480)

HttpOperationFailedException exposes password when using basic auth with user:password@host notation

[CAMEL-12475](https://issues.apache.org/jira/browse/CAMEL-12475)

Undertow consumer with http4 producer results in Undertow throwing NullPointerException

[CAMEL-12474](https://issues.apache.org/jira/browse/CAMEL-12474)

Remove servicemix repository

[CAMEL-12465](https://issues.apache.org/jira/browse/CAMEL-12465)

Don't carry soapAction forward if operationName is specified explicitly for the CxfProducer

[CAMEL-12457](https://issues.apache.org/jira/browse/CAMEL-12457)

file consumer - Should not use readlock by default

[CAMEL-12454](https://issues.apache.org/jira/browse/CAMEL-12454)

camel-kafka - AutoCommitEnabled=false should not auto commit

[CAMEL-12451](https://issues.apache.org/jira/browse/CAMEL-12451)

Memory leak: camel-cxf componet don't release UoW in case of using "robust" property

[CAMEL-12449](https://issues.apache.org/jira/browse/CAMEL-12449)

DefaultServiceLoadBalancer throws IndexOutOfBoundsException after applying ServiceFilter

[CAMEL-12448](https://issues.apache.org/jira/browse/CAMEL-12448)

camel-consul - service health state calculated from all services with same name

[CAMEL-12441](https://issues.apache.org/jira/browse/CAMEL-12441)

MulticastProcessor doProcessParallel blocks indefinitly if exception occurs in it.next()

[CAMEL-12436](https://issues.apache.org/jira/browse/CAMEL-12436)

camel-undertow - should extract body message from PATCH request

[CAMEL-12435](https://issues.apache.org/jira/browse/CAMEL-12435)

camel-netty4 - Shared connection pool should re-create connection if its no longer valid

[CAMEL-12434](https://issues.apache.org/jira/browse/CAMEL-12434)

camel-salesforce - Limits can not be deserialized in API versions >= 41.0

[CAMEL-12425](https://issues.apache.org/jira/browse/CAMEL-12425)

SqsProducer doesn't support Number attributes

[CAMEL-12424](https://issues.apache.org/jira/browse/CAMEL-12424)

HTTPHelper.setCharsetFromContentType can't properly extract the charset if it isn't the last parameter

[CAMEL-12422](https://issues.apache.org/jira/browse/CAMEL-12422)

Wrong language syntax declarations for code samples in documentation

[CAMEL-12420](https://issues.apache.org/jira/browse/CAMEL-12420)

Swagger definition broken when working with dataType array

[CAMEL-12418](https://issues.apache.org/jira/browse/CAMEL-12418)

camel-consul - High CPU load on events watching

[CAMEL-12415](https://issues.apache.org/jira/browse/CAMEL-12415)

Camel-jaxb option "encoding" with option "filterNonXmlChars" generate wrong data

[CAMEL-12412](https://issues.apache.org/jira/browse/CAMEL-12412)

camel-jclouds - Fallback type converter is wrong

[CAMEL-12407](https://issues.apache.org/jira/browse/CAMEL-12407)

camel-olingo4-api should explicitly depend on commons-io

[CAMEL-12406](https://issues.apache.org/jira/browse/CAMEL-12406)

camel-dropbox - Need to use force to check for file/folder exists

[CAMEL-12399](https://issues.apache.org/jira/browse/CAMEL-12399)

CxfRsProducer doesn't configure CxfRsEndpointConfigurer while using the Proxy API

[CAMEL-12395](https://issues.apache.org/jira/browse/CAMEL-12395)

HttpProducer cookie handling broken

[CAMEL-12386](https://issues.apache.org/jira/browse/CAMEL-12386)

file:onlyname.noext gives wrong results

[CAMEL-12384](https://issues.apache.org/jira/browse/CAMEL-12384)

camel-influxdb Query

[CAMEL-12379](https://issues.apache.org/jira/browse/CAMEL-12379)

Shutdown only AWS clients owned by the context

[CAMEL-12370](https://issues.apache.org/jira/browse/CAMEL-12370)

Camel-SFTP: errors in SSH routes after changes in read-lock

[CAMEL-12367](https://issues.apache.org/jira/browse/CAMEL-12367)

camel-aws - aws-s3 - Thread leak in pollEnrich with dynamic uri

[CAMEL-12364](https://issues.apache.org/jira/browse/CAMEL-12364)

ensure a SOAP 1.2 enabled camel-cxf consumer endpoint can handle SOAP 1.1 request correctly

[CAMEL-12359](https://issues.apache.org/jira/browse/CAMEL-12359)

withAdvice() + weaveById() failing for global onException() route definitions

[CAMEL-12356](https://issues.apache.org/jira/browse/CAMEL-12356)

Claim Check EPI: ManagedManagementStrategy: Can not register service: ClaimCheck\[\*\] as Service MBean

[CAMEL-12355](https://issues.apache.org/jira/browse/CAMEL-12355)

simple - Body.ognl function should validate that OGNL starts with a dot

[CAMEL-12348](https://issues.apache.org/jira/browse/CAMEL-12348)

camel-core - Potential NPE in ExchangeHelper.isStreamCaching

[CAMEL-12345](https://issues.apache.org/jira/browse/CAMEL-12345)

LinkedIn component throws IllegalArgumentException on API requests

[CAMEL-12325](https://issues.apache.org/jira/browse/CAMEL-12325)

lastConnectionActivityTicks is not getting updated by MllpTcpClientProducer

[CAMEL-12252](https://issues.apache.org/jira/browse/CAMEL-12252)

Dynamic setting the DESTINATION\_OVERRIDE\_URL doesn't work on CXFRS producer

[CAMEL-12104](https://issues.apache.org/jira/browse/CAMEL-12104)

Unintuitive default cxf timeout behavior

[CAMEL-11595](https://issues.apache.org/jira/browse/CAMEL-11595)

camel-univocity-parsers - A number of stream closed exception in tests

### Improvement (58)

[CAMEL-12600](https://issues.apache.org/jira/browse/CAMEL-12600)

Camel-Twilio: the credentials can be set only at component level

[CAMEL-12588](https://issues.apache.org/jira/browse/CAMEL-12588)

AggregateProcessor does not stop AggregateTimeoutChecker threads on stop call

[CAMEL-12584](https://issues.apache.org/jira/browse/CAMEL-12584)

Allow seda producers to offer data to the queue with timeout

[CAMEL-12580](https://issues.apache.org/jira/browse/CAMEL-12580)

camel-servicenow: suport java.lang.String as output model

[CAMEL-12578](https://issues.apache.org/jira/browse/CAMEL-12578)

camel-servicenow: add metadata option to list available tables

[CAMEL-12572](https://issues.apache.org/jira/browse/CAMEL-12572)

Upgrade to jaxb 2.3.0.1

[CAMEL-12569](https://issues.apache.org/jira/browse/CAMEL-12569)

service call : create a dns+srv resolver for kubernetes

[CAMEL-12556](https://issues.apache.org/jira/browse/CAMEL-12556)

camel-servicenow: add metadata option to list available import set

[CAMEL-12553](https://issues.apache.org/jira/browse/CAMEL-12553)

Using cxf new LoggingFeature

[CAMEL-12547](https://issues.apache.org/jira/browse/CAMEL-12547)

Create a camel-google-mail-stream component

[CAMEL-12542](https://issues.apache.org/jira/browse/CAMEL-12542)

seda - Have a default queue size limit

[CAMEL-12533](https://issues.apache.org/jira/browse/CAMEL-12533)

rest-dsl - Should check for required parameters generally

[CAMEL-12514](https://issues.apache.org/jira/browse/CAMEL-12514)

Extract undertow component name to allow extensibility

[CAMEL-12507](https://issues.apache.org/jira/browse/CAMEL-12507)

SqsProducer support for Number custom data types

[CAMEL-12493](https://issues.apache.org/jira/browse/CAMEL-12493)

Make additional HL7 Type Converters optional

[CAMEL-12482](https://issues.apache.org/jira/browse/CAMEL-12482)

Add support for auto configuring ExecutorServiceManager in Spring Boot

[CAMEL-12476](https://issues.apache.org/jira/browse/CAMEL-12476)

Make YQL header name constants public

[CAMEL-12473](https://issues.apache.org/jira/browse/CAMEL-12473)

Use Counter in Caffeine's dropwizard metrics

[CAMEL-12466](https://issues.apache.org/jira/browse/CAMEL-12466)

camel-seda : support configuring endpoint defaults on component

[CAMEL-12462](https://issues.apache.org/jira/browse/CAMEL-12462)

toD with HTTP endpoints - Optimise dynamic query to leverage HTTP\_QUERY header

[CAMEL-12459](https://issues.apache.org/jira/browse/CAMEL-12459)

camel-spring-boot - Add route group to route actuator

[CAMEL-12458](https://issues.apache.org/jira/browse/CAMEL-12458)

camel-twitter - Should support extended mode by default

[CAMEL-12455](https://issues.apache.org/jira/browse/CAMEL-12455)

camel-rabbitmq - Property DELIVERY\_MODE is not set to exchange

[CAMEL-12446](https://issues.apache.org/jira/browse/CAMEL-12446)

Splitter - Make it easier to turn off propgate exception

[CAMEL-12444](https://issues.apache.org/jira/browse/CAMEL-12444)

XML Validator - Improve DTD handling

[CAMEL-12442](https://issues.apache.org/jira/browse/CAMEL-12442)

rest-dsl - Rest producer should use RestConfiguration

[CAMEL-12440](https://issues.apache.org/jira/browse/CAMEL-12440)

Upgrade camel-dozer to 6.2

[CAMEL-12439](https://issues.apache.org/jira/browse/CAMEL-12439)

FailedToCreateRouteException should mask sensitive information in uris

[CAMEL-12438](https://issues.apache.org/jira/browse/CAMEL-12438)

camel-netty4 - Add timeout support for SPI correlation manager

[CAMEL-12437](https://issues.apache.org/jira/browse/CAMEL-12437)

Ability to define dynamic bucket name for s3 router using standard S3Constants.BUCKET\_NAME supplied in header

[CAMEL-12429](https://issues.apache.org/jira/browse/CAMEL-12429)

Avoid restlet response header warnings by using Restlet HeaderUtils

[CAMEL-12427](https://issues.apache.org/jira/browse/CAMEL-12427)

camel-netty4 - Add SPI to plugin custom correlation state for request/reply in producer

[CAMEL-12421](https://issues.apache.org/jira/browse/CAMEL-12421)

camel-elasticsearch-rest should use Camel converter pattern

[CAMEL-12419](https://issues.apache.org/jira/browse/CAMEL-12419)

camel-elasticsearch-rest should return complete bulk response instead of just ids

[CAMEL-12408](https://issues.apache.org/jira/browse/CAMEL-12408)

camel-cxf feature should not be tied to cxf-http-jetty feature

[CAMEL-12403](https://issues.apache.org/jira/browse/CAMEL-12403)

Documentation - Update build instructions to be per module

[CAMEL-12401](https://issues.apache.org/jira/browse/CAMEL-12401)

CoAP component should support REST context path configuration

[CAMEL-12394](https://issues.apache.org/jira/browse/CAMEL-12394)

Camel Bindy: marshal doesn't quote headers

[CAMEL-12389](https://issues.apache.org/jira/browse/CAMEL-12389)

camel-test - Using CamelTestSupport in Spring Boot

[CAMEL-12388](https://issues.apache.org/jira/browse/CAMEL-12388)

Camel AWS-KMS: Add describeKey operation

[CAMEL-12382](https://issues.apache.org/jira/browse/CAMEL-12382)

FileConsumer - Allow to delay readLock release tasks on idempotent read-lock

[CAMEL-12369](https://issues.apache.org/jira/browse/CAMEL-12369)

Camel-Git: Add GC operation

[CAMEL-12368](https://issues.apache.org/jira/browse/CAMEL-12368)

Camel-Git: add clean operation

[CAMEL-12363](https://issues.apache.org/jira/browse/CAMEL-12363)

Upgrade to spring batch 4.x

[CAMEL-12358](https://issues.apache.org/jira/browse/CAMEL-12358)

Camel-SMPP: Use timeout when creating socket connection

[CAMEL-12357](https://issues.apache.org/jira/browse/CAMEL-12357)

Unexpected change in JSON formatting due to CAMEL-11970

[CAMEL-12354](https://issues.apache.org/jira/browse/CAMEL-12354)

Camel-Kubernetes: Add scale operation to deployment component

[CAMEL-12353](https://issues.apache.org/jira/browse/CAMEL-12353)

Camel-Kubernetes: Add the ability to create or replace resources from file

[CAMEL-12352](https://issues.apache.org/jira/browse/CAMEL-12352)

simple - Lookup env var should be case-insensitive

[CAMEL-12337](https://issues.apache.org/jira/browse/CAMEL-12337)

camel-ftp - ignoreFileNotFoundOrPermissionError not work when folder not found

[CAMEL-12334](https://issues.apache.org/jira/browse/CAMEL-12334)

Salesforce DTO does not use correct datatype for "date" and "time" field

[CAMEL-12276](https://issues.apache.org/jira/browse/CAMEL-12276)

Stop requiring scribe transport for zipkin

[CAMEL-11879](https://issues.apache.org/jira/browse/CAMEL-11879)

Upgrade to lucene 7

[CAMEL-11669](https://issues.apache.org/jira/browse/CAMEL-11669)

Routes : add 'group'

[CAMEL-11651](https://issues.apache.org/jira/browse/CAMEL-11651)

Component Extension : load extensions from classpath/service-loader

[CAMEL-11162](https://issues.apache.org/jira/browse/CAMEL-11162)

camel-rest - Should we add content-type check for server side

[CAMEL-10452](https://issues.apache.org/jira/browse/CAMEL-10452)

camel-salesforce: Add an option to simulate SELECT \* from

[CAMEL-8494](https://issues.apache.org/jira/browse/CAMEL-8494)

camel-ganglia: add unit tests for packets sent to the wire

### New Feature (30)

[CAMEL-12567](https://issues.apache.org/jira/browse/CAMEL-12567)

camel-stream - Add support for configuring timeout for HTTP urls

[CAMEL-12566](https://issues.apache.org/jira/browse/CAMEL-12566)

camel-stream - Add support for HTTP headers

[CAMEL-12534](https://issues.apache.org/jira/browse/CAMEL-12534)

create camel-testcontainers

[CAMEL-12530](https://issues.apache.org/jira/browse/CAMEL-12530)

camel-web3j - Finish the work

[CAMEL-12527](https://issues.apache.org/jira/browse/CAMEL-12527)

Camel-AWS S3: Add a listObjects operation to list the content of a bucket

[CAMEL-12526](https://issues.apache.org/jira/browse/CAMEL-12526)

Camel-AWS KMS: Add enableKey operation

[CAMEL-12503](https://issues.apache.org/jira/browse/CAMEL-12503)

Kafka component should be able to propagate camel headers to kafka

[CAMEL-12501](https://issues.apache.org/jira/browse/CAMEL-12501)

Camel-Paho: add component verifier from Syndesis project

[CAMEL-12495](https://issues.apache.org/jira/browse/CAMEL-12495)

Camel-Slack: add component verifier from Syndesis project

[CAMEL-12478](https://issues.apache.org/jira/browse/CAMEL-12478)

camel-telegram - Allow use of custom keyboard

[CAMEL-12463](https://issues.apache.org/jira/browse/CAMEL-12463)

camel-core: allow to add metadata/properties to a route

[CAMEL-12461](https://issues.apache.org/jira/browse/CAMEL-12461)

camel-consul: support service metadata

[CAMEL-12402](https://issues.apache.org/jira/browse/CAMEL-12402)

Camel-Git: Add show tags operation

[CAMEL-12400](https://issues.apache.org/jira/browse/CAMEL-12400)

Camel-Git: Add Merge operation

[CAMEL-12397](https://issues.apache.org/jira/browse/CAMEL-12397)

Camel-Dropbox: Add a component verifier

[CAMEL-12392](https://issues.apache.org/jira/browse/CAMEL-12392)

Camel-Elasticsearch-rest: Add a component verifier extension

[CAMEL-12391](https://issues.apache.org/jira/browse/CAMEL-12391)

Camel-Elasticsearch-rest: Add info operation to producer

[CAMEL-12360](https://issues.apache.org/jira/browse/CAMEL-12360)

Add logRetryAttemptedInterval to RedeliveryPolicy

[CAMEL-12288](https://issues.apache.org/jira/browse/CAMEL-12288)

Need method call feature for milo client component

[CAMEL-12285](https://issues.apache.org/jira/browse/CAMEL-12285)

Add support for integration with MyBatis defined via interface (not XML)

[CAMEL-12138](https://issues.apache.org/jira/browse/CAMEL-12138)

Expose Braintree Dispute API

[CAMEL-11600](https://issues.apache.org/jira/browse/CAMEL-11600)

camel-micrometer - Add support for micrometer for metrics capture

[CAMEL-11430](https://issues.apache.org/jira/browse/CAMEL-11430)

Add support for Spring Boot 2.0.x

[CAMEL-11257](https://issues.apache.org/jira/browse/CAMEL-11257)

Provide AS2 component to support Business Data Interchange Using HTTP

[CAMEL-10806](https://issues.apache.org/jira/browse/CAMEL-10806)

Create camel-rxjava2 component

[CAMEL-10793](https://issues.apache.org/jira/browse/CAMEL-10793)

camel cloud: expose routes as a service

[CAMEL-10785](https://issues.apache.org/jira/browse/CAMEL-10785)

Add revapi-maven-plugin for API modification reports

[CAMEL-10671](https://issues.apache.org/jira/browse/CAMEL-10671)

camel-example-celyon

[CAMEL-10193](https://issues.apache.org/jira/browse/CAMEL-10193)

add support for lookup field using an sObject external id

[CAMEL-9751](https://issues.apache.org/jira/browse/CAMEL-9751)

Add support for security requirements to swagger java component

### Sub-task (20)

[CAMEL-12531](https://issues.apache.org/jira/browse/CAMEL-12531)

camel cloud : create a spring cloud based camel-service example

[CAMEL-12518](https://issues.apache.org/jira/browse/CAMEL-12518)

camel cloud : leverage spring-cloud ServiceRegistry to register routes

[CAMEL-12502](https://issues.apache.org/jira/browse/CAMEL-12502)

camel cloud : create a service registration route policy

[CAMEL-12499](https://issues.apache.org/jira/browse/CAMEL-12499)

Spring Boot 2 - Quoting map keys no longer needed

[CAMEL-12496](https://issues.apache.org/jira/browse/CAMEL-12496)

Spring Boot 2 - Fix Infinispan starter

[CAMEL-12485](https://issues.apache.org/jira/browse/CAMEL-12485)

camel cloud : create camel-service component

[CAMEL-12460](https://issues.apache.org/jira/browse/CAMEL-12460)

Spring Boot 2 - Camel routes actuator trouble

[CAMEL-12423](https://issues.apache.org/jira/browse/CAMEL-12423)

Spring Boot 2 - Upgrade to Spring Boot 2.0.1

[CAMEL-12396](https://issues.apache.org/jira/browse/CAMEL-12396)

Spring Boot 2 - CamelCloudServiceCallSimpleExpressionTest fails

[CAMEL-12387](https://issues.apache.org/jira/browse/CAMEL-12387)

Spring Boot 2 - Update readme's and documentation

[CAMEL-12385](https://issues.apache.org/jira/browse/CAMEL-12385)

Spring Boot 2 - Camel info contributor to show basic details

[CAMEL-12383](https://issues.apache.org/jira/browse/CAMEL-12383)

Spring Boot 2 - Migrate application.properties to new names

[CAMEL-12378](https://issues.apache.org/jira/browse/CAMEL-12378)

Spring Boot 2 - Fix the camel-example-spring-cloud-servicecall

[CAMEL-12377](https://issues.apache.org/jira/browse/CAMEL-12377)

Spring Boot 2 - Fix the camel-example-spring-boot-rest-jpa

[CAMEL-12376](https://issues.apache.org/jira/browse/CAMEL-12376)

Spring Boot 2 - Fix the tests/camel-itest-karaf

[CAMEL-12375](https://issues.apache.org/jira/browse/CAMEL-12375)

Spring Boot 2 - Upgrade Spring SMX bundles to latest releases

[CAMEL-12374](https://issues.apache.org/jira/browse/CAMEL-12374)

Spring Boot 2 - Upgrade Karaf to spring 5

[CAMEL-12373](https://issues.apache.org/jira/browse/CAMEL-12373)

Spring Boot 2 - Add back some of the latest functionality from actuator in camel-spring-boot

[CAMEL-12372](https://issues.apache.org/jira/browse/CAMEL-12372)

Spring Boot 2 - Fix the tests/camel-itest-spring-boot

[CAMEL-12362](https://issues.apache.org/jira/browse/CAMEL-12362)

Upgrade to Karaf 4.2.x

### Task (33)

[CAMEL-12599](https://issues.apache.org/jira/browse/CAMEL-12599)

Upgrade to CXF 3.2.5

[CAMEL-12585](https://issues.apache.org/jira/browse/CAMEL-12585)

Delete boot2 and boot2ga branches

[CAMEL-12582](https://issues.apache.org/jira/browse/CAMEL-12582)

Create a Camel-micrometer Karaf feature

[CAMEL-12579](https://issues.apache.org/jira/browse/CAMEL-12579)

Disable Google Analytics phone home

[CAMEL-12576](https://issues.apache.org/jira/browse/CAMEL-12576)

Bump to Lucene and Solr 7.2.1

[CAMEL-12564](https://issues.apache.org/jira/browse/CAMEL-12564)

Camel-Grpc: Bump to version 1.12.0

[CAMEL-12559](https://issues.apache.org/jira/browse/CAMEL-12559)

camel-testcontainers : add documentation

[CAMEL-12552](https://issues.apache.org/jira/browse/CAMEL-12552)

camel-rest - Send the error reason in the resonse body

[CAMEL-12544](https://issues.apache.org/jira/browse/CAMEL-12544)

Camel-Couchdb: Add a get method to have a complete CRUD support

[CAMEL-12539](https://issues.apache.org/jira/browse/CAMEL-12539)

camel-caffeine: improve documentation

[CAMEL-12537](https://issues.apache.org/jira/browse/CAMEL-12537)

Add docs how to configure additional parameters in camel-infinispan

[CAMEL-12524](https://issues.apache.org/jira/browse/CAMEL-12524)

camel cloud: deprecate AggregatingServiceDiscovery and replace it with CombinedServiceDiscovery

[CAMEL-12522](https://issues.apache.org/jira/browse/CAMEL-12522)

camel-rxjava2: remove dependency on rx extensions

[CAMEL-12517](https://issues.apache.org/jira/browse/CAMEL-12517)

Camel-MongoDB and Camel-MongoDB3: Make them extend DefaultComponent

[CAMEL-12509](https://issues.apache.org/jira/browse/CAMEL-12509)

camel cloud: deprecate ChainedServiceFilter and replace it with CombinedServiceFilter

[CAMEL-12494](https://issues.apache.org/jira/browse/CAMEL-12494)

spring-boot: use ApplicationContextRunner in spring-boot test to test AutoConfigurations

[CAMEL-12488](https://issues.apache.org/jira/browse/CAMEL-12488)

Use secure repository URL

[CAMEL-12468](https://issues.apache.org/jira/browse/CAMEL-12468)

Add dependency-management entry for camel-azure-starter

[CAMEL-12447](https://issues.apache.org/jira/browse/CAMEL-12447)

camel-jms - Exclude spring-messaging JAR

[CAMEL-12405](https://issues.apache.org/jira/browse/CAMEL-12405)

upgrade to CXF 3.2.4

[CAMEL-12381](https://issues.apache.org/jira/browse/CAMEL-12381)

upgrade to CXF 3.2.3

[CAMEL-12366](https://issues.apache.org/jira/browse/CAMEL-12366)

OSGi bundles for various spring JARs that has been upgraded to spring 5

[CAMEL-12365](https://issues.apache.org/jira/browse/CAMEL-12365)

Upgrade consul client to 1.1.1

[CAMEL-12351](https://issues.apache.org/jira/browse/CAMEL-12351)

Camel-Kubernetes: Port Kubernetes resources support to Openshift too

[CAMEL-12347](https://issues.apache.org/jira/browse/CAMEL-12347)

Reduce the usage of 3rd party maven repos

[CAMEL-12346](https://issues.apache.org/jira/browse/CAMEL-12346)

Deprecate camel-jira as the java lib is deprecated by atlassian

[CAMEL-12344](https://issues.apache.org/jira/browse/CAMEL-12344)

upgrade json-validator

[CAMEL-12214](https://issues.apache.org/jira/browse/CAMEL-12214)

Camel-Zipkin: From > 4.13.4 Brave-core and spancollector-scribe are no longer released

[CAMEL-11956](https://issues.apache.org/jira/browse/CAMEL-11956)

Support Spring 5.0.x

[CAMEL-11905](https://issues.apache.org/jira/browse/CAMEL-11905)

No test coverage for camel-ganglia

[CAMEL-11893](https://issues.apache.org/jira/browse/CAMEL-11893)

No test coverage for camel-solr

[CAMEL-11650](https://issues.apache.org/jira/browse/CAMEL-11650)

Use Hibernate Validator 6.x where possible

[CAMEL-11186](https://issues.apache.org/jira/browse/CAMEL-11186)

Upgrade dropwizard metrics

### Test (2)

[CAMEL-12505](https://issues.apache.org/jira/browse/CAMEL-12505)

service-call : include ServiceDefinition metatdata when computing the final URI

[CAMEL-12430](https://issues.apache.org/jira/browse/CAMEL-12430)

camel-itest-karaf - A few failing tests

### Wish (3)

[CAMEL-12521](https://issues.apache.org/jira/browse/CAMEL-12521)

Expose websocket remote address as a header

[CAMEL-12512](https://issues.apache.org/jira/browse/CAMEL-12512)

camel-consul - Option to inject Consul client

[CAMEL-12274](https://issues.apache.org/jira/browse/CAMEL-12274)

Bindy - Unescape double quotes inside CSV field

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).