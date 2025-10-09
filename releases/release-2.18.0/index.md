# Apache camel 2.18.0 Release

## New and Noteworthy

Welcome to the 2.18.0 release which resolved over 500 issues. This is first release that requires Java 8 and comes with a much-improved Spring Boot support, and ships with numerous new features, improvements and bug fixes.

-   Java DSL with experimental Java8 functional/lambda support. Check out the camel-example-java8. We love feedback on this DSL and expect to improved the API over the next couple of releases.
-   The XSD schema for `<camelContext>` and its other configuration elements are now also documented (before it was only `<routes>` and `<rests>`). The XSD schema now also documents the default values of all the options.
-   Introduced `FluentProducerTemplate` using fluent builder style as a alternative to ProducerTemplate
-   All Camel Components that has options to be configured now supports and include Spring Boot auto configuration for those options, so they can easily be configured in your application.yaml file when using Spring Boot with Camel. 
-   Camel Spring Boot now supports the same link:advanced-configuration-of-camelcontext-using-spring.html\[advanced configuration\] you can do with Spring XML, if the beans have been configured using `@Bean` style in a Spring Boot configuration class.
-   Added Hystrix EIP as EIP pattern that uses native Netflixx Hystrix as the Circuit Breaker implementation. This requires having `camel-hystrix` on the classpath.
-   Added Service Call EIP as EIP pattern that allows to call a remote service in a distributed system, where the service is looked up from a service registry of some sorts, such as kubernetes, consul, etcd, zookeeper etc.
-   Running Camel with Spring Boot now includes a Camel Health Indicator (actuator) if `spring-boot-starter-actuator` is on the classpath.
-   The Rest component allows to call REST services now (as a client), where you can pick one of the following Camel components for the HTTP transport: http, http4, netty4-http, jetty, restlet, undertow. You can also refer to a existing swagger api doc and include camel-swagger-java on the classpath, for automatic validation of rest endpoint is configured to use a valid rest operation/parameters.
-   The Rest DSL now auto discovers which HTTP component to use if no explicit component name has been configured, by the available components on the classpath (by their default name) and if there only exists one, then that is used.
-   Spring-DM for OSGi moved out of camel-spring into a separate camel-spring-dm module.
-   Improved the Bean component to better match method parameter types when using Simple language as parameter values.
-   Added `BindyConverter` that allows to implement custom data converters for Bindy
-   The access in the Rest DSL has been deprecated and no longer in use - its not part of swagger specification anymore.
-   Camel-NATS now uses JNATS client instead of the deprecated Java\_nats one.
-   During startup of link:../camelcontext.adoc\[CamelContext\] the services that are used as part of routes are now deferred being started to the end of the startup process. Some IoC frameworks like Spring can otherwise causes a circular dependency issue if services are started too early. A side effect is that if service startup failures happen when being started later, they are now wrapped in the `FailedToStartupRouteException` to better pin point which route thas the problem.
-   Improved the startup sequence of Spring Java Config to be similar to Spring Boot that helps prevent Spring initialization errors about circular dependencies issues.
-   Added PATCH to Rest DSL
-   Added “starts with” and “ends with” operator to the Simple language.
-   Added `BeanIOSplitter` to BeanIO that can be used with the Splitter EIP to split big payloads in streaming mode without reading the entire content into memory.
-   Some of the AWS components allows to specify ARN in the endpoint configuration. 
-   The create operation in Zookeeper now creates sub paths if missing.
-   Added support for async mode for SERVLET component to leverage Asynchronous Servlet from the Servlet 3.0 spec.
-   Bean component and Bean Language validates method name must be a valid according to java identifier rules, and also if parameter syntax has an ending parenthesis.
-   You can now use `@RunWith(CamelSpringBootJUnit4ClassRunner.class)` to test Camel Spring Boot applications and use the Camel test annotations from Spring Testing such as `@MockEndpoints`.
-   To turn on logging exhausted message body with the message history you can configure this easily on the CamelContext level with `setLogExhaustedMessageBody`
-   Camel-Infinispan now supports Aggregation Repository: InfinispanLocalAggregationRepository and InfinispanRemoteAggregationRepository
-   The SQL Component and ElSql now supports `outputType=StreamList` to use an iterator for the output of the SQL query that allows to process the data in a streaming fashion such as with the Splitter EIP to process the data row by row, and load data from the database as needed.
-   JPA now includes a `JpaPollingConsumer` implementation that better supports Content Enricher using `pollEnrich` to do a on-demand poll that returns either none, one or a list of entities as the result. 
-   Calling Bean with method parameters defined using Simple language parameters, now avoids an intermediate conversion of the parameters to a String value. This ensures the passed in values when calling the bean method is using the parameter type as-is from Simple language.
-   Camel CDI now supports importing Camel XML configuration files
-   Camel CDI does not deploy an empty Camel context bean anymore if not route builder beans nor Camel beans are deployed
-   Camel CDI adds the `@Named` qualifier to Camel route management events so that it’s possible to observe these events for a specific route with an explicit `id`
-   Camel BeanIO now supports the possibility to use a custom BeanReaderErrorHandler implementation in his configuration
-   Camel Kubernetes now supports Kubernetes ConfigMap feature
-   The Tokenizer and XMLTokenizer language now supports using Simple expressions as the token / xml tag names so they can be dynamic values.
-   Added `filterDirectory` and `filterFile` options to File2 so filtering can be done using Simple language or predicates. 
-   Optimize Camel to only enable AllowUseOriginalMessage if in use by error handler or OnCompletion. End user who manually access the original message using the Java API must configure AllowUseOriginalMessage=true.
-   Camel-AHC Camel-HTTP Camel-HTTP4 Camel-Jetty now support a connectionClose parameter to allow explicitly adding a Connection Close header to HTTP request
-   Bindy allows to plugin custom formatters for mapping to custom types.
-   Content Enricher using `pollEnrich` now supports consumers configured with `consumer.bridgeErrorHandler=true` to let any exceptions from the poll propagate to the route error handler, to let it be able to perform redeliveries and whatnot.
-   CXF and CXFRS now support setting of the SSL-context link:camel-configuration-utilities.html\[Using the JSSE Configuration Utility\]
-   MongoDB now is fully converted to MongoDB 3 although we still use BasicDBObject instead of Document
-   Camel Spring Boot can now scan for classes in Spring Boot FAR jars with embeds third party JARs.
-   You can now set the SNI Hostnames using the Camel Configuration Utilities to indicate the hostnames you try to connect
-   The XML DSL will preserve double spaces in the context-path of uri attributes when removing white space noise, when uri’s are configured using mutli lines.
-   The Camel Catalog module can now load older versions of Camel to be used when querying the catalog. There is a `camel-catalog-maven` module that is able to download catalog JARs from Maven central.
-   A new Camel Attachment interface was added that allows propagating headers for attachments. Camel CXF, Camel Mail (including the MIME-Multipart data format), and Camel-Jetty set and consume attachment headers.
-   Improved bean method call to validate if method name with parameters has valid number of parenthesis in the syntax.
-   The JSonPath now supports inlined Simple language expressions to allow more dynamic expressions.
-   Improved Netty4 producer to be fully asynchronous when connecting to remote server.
-   The Websocket component now uses a timeout when sending to websocket channels to avoid potentially blocking for a long time due networking issues with clients.
-   Hazelcast Component now provide a RoutePolicy.
-   Saxon has been upgraded to version 9.7

### Resolved Issues

-   Fixed Bean component to avoid ambiguous error for classes that extends generic interface and calling which could lead to falsely duplicate methods (due Java type erasure inserts bridge methods) 
-   Fixed splitting using tarfile could cause OOME if splitting big files which was mistakenly loaded into memory. Now we work on the tar stream directly.
-   Fixed Netty HTTP and Netty4 HTTP issue when not specifying a port number then port 80 would not be used but an error about port -1 is not allowed.
-   Fixed Swagger Java when using property placeholders in Rest DSL could cause invalid parameters to be included that was from the placeholder.
-   The `threads` EIP now lets Error handling in Camel perform redeliveries if the thread pool would otherwise reject accepting the task. This allows the error handler to perform redeliveries to attempt to put the task on the thread pool queue, or eventually move the message to a dead letter queue etc.
-   Fixed Rest DSL adding empty header if specifying a non required query parameter that has no default value assigned.
-   Fixed doWhile loop which could potentially loop forever.
-   Fixed a NPE in Zookeeper consumer if no zookeeper node path was set
-   When using continued with onException then dead letter channel endpooint should not be invoked.
-   Fixed Error Handler to not log exceptions when using `continued(true)` by default.
-   Fixed so using shareUnitOfWork would now also call specialized `AggregationStrategy` for onTimeout, onCompletion etc.
-   Fixed Jetty consumer incorrectly handle multipart/form data not being mapped as attachments on the Camel Message.
-   Fixed Netty4 HTTP may fail reading the http content from the raw netty stream if the Exchange was routed asynchronously.
-   Fixed Netty4 HTTP leak ByteBuf’s on the producer side which was not released in all corner cases before they may be gargage collected. 
-   Fixed Dozer not able to use variables in mapping files when using OSGi.
-   Fixed a potential dead-lock when doing request/reply over JMS and requests are timing out concurrently and continued routing the exchanges are calling another JMS endpoint that is also doing request/reply which also timeout. 
-   Fixed Load Balancer EIPs to support using _any_ property placeholder using the _prop:_ prefix.
-   Fixed context scoped OnCompletion would not stop/shutdown its processors when CamelContext is being shutdown. 
-   Fixed memory leak in Routing Slip when the slip routes to certain kind of Camel components.
-   Fixed SQL Component query parameter mis-match issue when using IN queries together with other named parameters.
-   Fixed a memory leak with CXF when continuation was expired could cause Camel message not to be unregisteted from in-flight registry.
-   Fixed a preformance regression when using `camel-jaxb`

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
      <version>2.18.0</version>
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
      <version>2.18.0</version>
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
| [apache-camel-2.18.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.0/apache-camel-2.18.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.0/apache-camel-2.18.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.0/apache-camel-2.18.0-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (168)

[CAMEL-10359](https://issues.apache.org/jira/browse/CAMEL-10359)

Fix failing test org.apache.camel.component.salesforce.RestApiIntegrationTest.testQueryAll

[CAMEL-10342](https://issues.apache.org/jira/browse/CAMEL-10342)

WebSockets options are ignored

[CAMEL-10340](https://issues.apache.org/jira/browse/CAMEL-10340)

camel-aws - SQS option deleteAfterRead not work if set deleteIfFiltered=false

[CAMEL-10338](https://issues.apache.org/jira/browse/CAMEL-10338)

Markdown formatting improvement for CDI-OSGI Example

[CAMEL-10326](https://issues.apache.org/jira/browse/CAMEL-10326)

Hazelcast aggregation repository tests may fail if multiple network interfaces are configured on th host

[CAMEL-10313](https://issues.apache.org/jira/browse/CAMEL-10313)

camel-example-swagger-xml - Fails with jetty:run

[CAMEL-10310](https://issues.apache.org/jira/browse/CAMEL-10310)

Lucene upgrade violates elasticsearch assertion

[CAMEL-10303](https://issues.apache.org/jira/browse/CAMEL-10303)

MllpTcpServerConsumer fails silently on acknowledgment failure

[CAMEL-10296](https://issues.apache.org/jira/browse/CAMEL-10296)

Guaranteed Delivery not working if no timeout is set

[CAMEL-10293](https://issues.apache.org/jira/browse/CAMEL-10293)

\[camel-maven-plugin\] When blueprint detected, plugin ignores useBlueprint, fileApplicationContextUri tags

[CAMEL-10291](https://issues.apache.org/jira/browse/CAMEL-10291)

Camel RabbitMQ invalid handling of message timestamp

[CAMEL-10282](https://issues.apache.org/jira/browse/CAMEL-10282)

\[Avro\] Issue on OSGi due to static cache

[CAMEL-10279](https://issues.apache.org/jira/browse/CAMEL-10279)

Can't use @ImportResource and configure() in the same SB app

[CAMEL-10273](https://issues.apache.org/jira/browse/CAMEL-10273)

\[Jetty\] missing jmx object if custom thread pool is used

[CAMEL-10271](https://issues.apache.org/jira/browse/CAMEL-10271)

camel-jt400 - Failed to resolve endpoint

[CAMEL-10254](https://issues.apache.org/jira/browse/CAMEL-10254)

Error may still block mail-consumer

[CAMEL-10253](https://issues.apache.org/jira/browse/CAMEL-10253)

NullPointer in ThrowExceptionProcessor.getTraceLabel

[CAMEL-10244](https://issues.apache.org/jira/browse/CAMEL-10244)

When same netty endpoint producer is used twice in a route, BlockingOperationException is raised

[CAMEL-10243](https://issues.apache.org/jira/browse/CAMEL-10243)

Force camel-atom feature to install abdera-parser

[CAMEL-10238](https://issues.apache.org/jira/browse/CAMEL-10238)

Camel-salesforce component never tries to reconnect after a disconnect

[CAMEL-10237](https://issues.apache.org/jira/browse/CAMEL-10237)

Problem setting JMSX jms properties on OracleAQ

[CAMEL-10232](https://issues.apache.org/jira/browse/CAMEL-10232)

\[camel-itest-karaf\] CamelJbpmTest fails as it requires com.sun.tools.xjc

[CAMEL-10231](https://issues.apache.org/jira/browse/CAMEL-10231)

\[camel-itest-karaf\] CamelIgniteTest fails as Ignite needs sun.nio.ch

[CAMEL-10229](https://issues.apache.org/jira/browse/CAMEL-10229)

camel-rabbitmq - Race condition when stopping context with autoack=false

[CAMEL-10221](https://issues.apache.org/jira/browse/CAMEL-10221)

Camel-Jcache: writeThrough option is never used

[CAMEL-10217](https://issues.apache.org/jira/browse/CAMEL-10217)

Remove logging implementations from compile scope

[CAMEL-10215](https://issues.apache.org/jira/browse/CAMEL-10215)

EventDrivenPollingConsumer is not thread safe when used with ConsumerCache

[CAMEL-10205](https://issues.apache.org/jira/browse/CAMEL-10205)

camel-example-spring-dm - Cannot install in Karaf 4.0.x

[CAMEL-10200](https://issues.apache.org/jira/browse/CAMEL-10200)

Mail consumer sets wrong Content-Type header for mails with attachment

[CAMEL-10195](https://issues.apache.org/jira/browse/CAMEL-10195)

rest-dsl - automatic binding failure with waitForTaskToComplete=Never

[CAMEL-10192](https://issues.apache.org/jira/browse/CAMEL-10192)

Specifying jobFromHeader in URI option throws exception

[CAMEL-10185](https://issues.apache.org/jira/browse/CAMEL-10185)

camel-ftp - fastExistsCheck issue

[CAMEL-10184](https://issues.apache.org/jira/browse/CAMEL-10184)

ChannelGroup option is not active for NettyProducer

[CAMEL-10181](https://issues.apache.org/jira/browse/CAMEL-10181)

Camel-undertow: UndertowHttpBinding should be initialized in the endpoint and not at component level

[CAMEL-10177](https://issues.apache.org/jira/browse/CAMEL-10177)

Camel-catalog: wireTap is missing from all oneOf lists

[CAMEL-10176](https://issues.apache.org/jira/browse/CAMEL-10176)

camel-cxf RawMessageContentRedirectInterceptor should be able to handle the case that OutputStream is null for an outgoing message

[CAMEL-10174](https://issues.apache.org/jira/browse/CAMEL-10174)

weaveByToString throws UnsupportedOperationException on CBR

[CAMEL-10171](https://issues.apache.org/jira/browse/CAMEL-10171)

Camel CXF expired continuations cause memory leak

[CAMEL-10162](https://issues.apache.org/jira/browse/CAMEL-10162)

AbstractCamelTestNGSpringContextTests does not support @ContextConfiguration for JavaConfig

[CAMEL-10161](https://issues.apache.org/jira/browse/CAMEL-10161)

camel-sql - Does not propagate headers for outputType=StreamList

[CAMEL-10157](https://issues.apache.org/jira/browse/CAMEL-10157)

Values in KafkaConstants don't fit their variable name

[CAMEL-10155](https://issues.apache.org/jira/browse/CAMEL-10155)

Reslet headers not getting filtered

[CAMEL-10151](https://issues.apache.org/jira/browse/CAMEL-10151)

camel-sql - Query parameter count mismatch when using IN and other names in SQL

[CAMEL-10150](https://issues.apache.org/jira/browse/CAMEL-10150)

Camel-Apt: Check for empty lines in parseAsMap method of EndpointAnnotationProcessor

[CAMEL-10149](https://issues.apache.org/jira/browse/CAMEL-10149)

Camel-Ftp: SftpOperations use sendKeepAliveMsg instead of sendIgnore method

[CAMEL-10147](https://issues.apache.org/jira/browse/CAMEL-10147)

MesssageHistory will take very long time for large expressions

[CAMEL-10145](https://issues.apache.org/jira/browse/CAMEL-10145)

Camel-Git: Pull and Push operations require the remote Name and not the remote Path to git repository

[CAMEL-10144](https://issues.apache.org/jira/browse/CAMEL-10144)

Salesforce keeps breaking backward compatibility by adding fields to older API versions

[CAMEL-10143](https://issues.apache.org/jira/browse/CAMEL-10143)

Camel Salesforce component field LastActivityDate is typed with java.lang.String, which is not consistent with the Salesforce SOAP type "xsd:date"

[CAMEL-10142](https://issues.apache.org/jira/browse/CAMEL-10142)

ScheduledPollingConsumer properties

[CAMEL-10136](https://issues.apache.org/jira/browse/CAMEL-10136)

Missing Group attribute for Tokenize DSL added to the Body Expression

[CAMEL-10128](https://issues.apache.org/jira/browse/CAMEL-10128)

camel-jt400 - Need to call configure consumer

[CAMEL-10120](https://issues.apache.org/jira/browse/CAMEL-10120)

Creating an InputStream from XMLStreamReader fails without default namespace

[CAMEL-10117](https://issues.apache.org/jira/browse/CAMEL-10117)

Camel-Elasticsearch: Default pathHome option should work on all the platforms

[CAMEL-10116](https://issues.apache.org/jira/browse/CAMEL-10116)

NullPointerException in DefaultAsyncProcessorAwaitManager

[CAMEL-10115](https://issues.apache.org/jira/browse/CAMEL-10115)

Kafka consumer stays running if no messages were received after shutdown start

[CAMEL-10111](https://issues.apache.org/jira/browse/CAMEL-10111)

Creating an InputStream from XMLStreamReader fails with ASCII default platform encoding

[CAMEL-10110](https://issues.apache.org/jira/browse/CAMEL-10110)

Marshaling using CSV will insert escape char in header if using a pipe as separator

[CAMEL-10104](https://issues.apache.org/jira/browse/CAMEL-10104)

Mail consumer does not work with quartz scheduler

[CAMEL-10103](https://issues.apache.org/jira/browse/CAMEL-10103)

Camel FTP - Unknown parser type

[CAMEL-10094](https://issues.apache.org/jira/browse/CAMEL-10094)

Camel-Linkedin: Sometimes LinkedInOAuthRequestFilter in API is using redirectQuery equal to null

[CAMEL-10091](https://issues.apache.org/jira/browse/CAMEL-10091)

Camel-Git: Always check if Git instance is null in GitProducer before closing

[CAMEL-10090](https://issues.apache.org/jira/browse/CAMEL-10090)

Salesforce doesn't support full ISO-8601 datetimes

[CAMEL-10087](https://issues.apache.org/jira/browse/CAMEL-10087)

camel-kafka does not work in OSGI container

[CAMEL-10082](https://issues.apache.org/jira/browse/CAMEL-10082)

camel-api-component-maven-plugin doesn't handle inner class names in Javadoc

[CAMEL-10064](https://issues.apache.org/jira/browse/CAMEL-10064)

Extra request parameter sent by the camel-jetty component

[CAMEL-10063](https://issues.apache.org/jira/browse/CAMEL-10063)

Camel on Karaf 4.0.5: java.lang.NoClassDefFoundError: org/apache/karaf/util/StringEscapeUtils

[CAMEL-10060](https://issues.apache.org/jira/browse/CAMEL-10060)

Cannot scan package to find custom converters

[CAMEL-10051](https://issues.apache.org/jira/browse/CAMEL-10051)

netty4 reuseChannel not working as expected

[CAMEL-10048](https://issues.apache.org/jira/browse/CAMEL-10048)

Memory leak in RoutingSlip

[CAMEL-10043](https://issues.apache.org/jira/browse/CAMEL-10043)

Camel-Jaxb: objectFactory is never checked. This leads to performance degradation.

[CAMEL-10039](https://issues.apache.org/jira/browse/CAMEL-10039)

LinkedIn broke login in LinnkedIn component by adding a redundant reference to the callback url

[CAMEL-10038](https://issues.apache.org/jira/browse/CAMEL-10038)

BlueprintPropertiesParser breaks propertyPlaceholder fallbackToUnaugmentedProperty behavior

[CAMEL-10034](https://issues.apache.org/jira/browse/CAMEL-10034)

Spring-boot health check causes application startup failure

[CAMEL-10033](https://issues.apache.org/jira/browse/CAMEL-10033)

camel-avro - Cannot install in karaf

[CAMEL-10032](https://issues.apache.org/jira/browse/CAMEL-10032)

camel-braintree - Cannot install in Karaf

[CAMEL-10024](https://issues.apache.org/jira/browse/CAMEL-10024)

Race condition in Mina2Producer/Mina2Consumer when closing connections with disconnect=true

[CAMEL-10017](https://issues.apache.org/jira/browse/CAMEL-10017)

Fix syntax for ironmq component

[CAMEL-10016](https://issues.apache.org/jira/browse/CAMEL-10016)

Fix syntax for crypto component

[CAMEL-10015](https://issues.apache.org/jira/browse/CAMEL-10015)

Fix syntax for braintree component

[CAMEL-10014](https://issues.apache.org/jira/browse/CAMEL-10014)

Fix syntax for kubernetes component

[CAMEL-10012](https://issues.apache.org/jira/browse/CAMEL-10012)

Add a Path Home option in camel-elasticsearch configuration

[CAMEL-10011](https://issues.apache.org/jira/browse/CAMEL-10011)

Overlap in management name for multiple contexts in OSGi bundle

[CAMEL-10009](https://issues.apache.org/jira/browse/CAMEL-10009)

Using <to> with id and ref fails

[CAMEL-10005](https://issues.apache.org/jira/browse/CAMEL-10005)

HDFS2 - ClassNotFoundException - org.apache.htrace.SamplerBuilder

[CAMEL-9994](https://issues.apache.org/jira/browse/CAMEL-9994)

Deadlock in Failover Loadbalancer

[CAMEL-9993](https://issues.apache.org/jira/browse/CAMEL-9993)

add NPE guard for camel-cxf RawMessageContentRedirectInterceptor

[CAMEL-9986](https://issues.apache.org/jira/browse/CAMEL-9986)

MIME-Multipart Data Format is inconsistent if trying to unmarshal non-MIME data

[CAMEL-9984](https://issues.apache.org/jira/browse/CAMEL-9984)

RabbitConsumer.stop() doesn't stop underlying AutorecoveringConnection obtained from supplied ConnectionFactory

[CAMEL-9982](https://issues.apache.org/jira/browse/CAMEL-9982)

Marshalling fixed length record with links fails

[CAMEL-9981](https://issues.apache.org/jira/browse/CAMEL-9981)

CamelSpringJUnit4ClassRunner registers listeners twice

[CAMEL-9978](https://issues.apache.org/jira/browse/CAMEL-9978)

Camel-Kafka: configuration type mismatch for parameter acks

[CAMEL-9973](https://issues.apache.org/jira/browse/CAMEL-9973)

CdiCamelExtension.shouldDeployDefaultCamelContext throws NPE with primitive injection points

[CAMEL-9972](https://issues.apache.org/jira/browse/CAMEL-9972)

Explicitly add Connection Close HTTP header with a parameter in URI

[CAMEL-9970](https://issues.apache.org/jira/browse/CAMEL-9970)

CamelFileLength header is wrong for long write file

[CAMEL-9968](https://issues.apache.org/jira/browse/CAMEL-9968)

camel restlet not populating body form parameters correctly for x-www-form-urlencoded

[CAMEL-9960](https://issues.apache.org/jira/browse/CAMEL-9960)

create ReaderInputStream align encoding with Exchange

[CAMEL-9953](https://issues.apache.org/jira/browse/CAMEL-9953)

Camel-ssh: Review logic in doStart and doStop in the SshConsumer and SshProducer

[CAMEL-9951](https://issues.apache.org/jira/browse/CAMEL-9951)

Setup default values for thread-connected properties in WebSocket component

[CAMEL-9950](https://issues.apache.org/jira/browse/CAMEL-9950)

Camel-Websocket: NPE in case minThreads, maxThreads and getThreadPool equals to null

[CAMEL-9941](https://issues.apache.org/jira/browse/CAMEL-9941)

Blueprint bug ARIES-1544 causes issues in Olingo2 configuration

[CAMEL-9933](https://issues.apache.org/jira/browse/CAMEL-9933)

Camel-CSV marshalling breaks characters not in default charset

[CAMEL-9929](https://issues.apache.org/jira/browse/CAMEL-9929)

camel-restlet - Using synchronous=false with no error handler leak inflight exchange

[CAMEL-9926](https://issues.apache.org/jira/browse/CAMEL-9926)

HTTP Proxy support in Salesforce component is broken with upgrade to Jetty9

[CAMEL-9921](https://issues.apache.org/jira/browse/CAMEL-9921)

Dozer variable mapping doesn't work on karaf

[CAMEL-9920](https://issues.apache.org/jira/browse/CAMEL-9920)

Handle SocketTimeoutException on accept

[CAMEL-9918](https://issues.apache.org/jira/browse/CAMEL-9918)

Support observing route events filtered by route id in Camel CDI

[CAMEL-9917](https://issues.apache.org/jira/browse/CAMEL-9917)

Route stopped events are sent in inconsistent order

[CAMEL-9911](https://issues.apache.org/jira/browse/CAMEL-9911)

RestBindingMode auto not honored

[CAMEL-9906](https://issues.apache.org/jira/browse/CAMEL-9906)

camel-sql - Should allow null values as a valid value

[CAMEL-9903](https://issues.apache.org/jira/browse/CAMEL-9903)

DumpRouteStatsAsXml do not work when jmx domain is customized

[CAMEL-9898](https://issues.apache.org/jira/browse/CAMEL-9898)

SimpleBuilder throws NullPointerException when replacing string using regexAll method and the regex contains }

[CAMEL-9896](https://issues.apache.org/jira/browse/CAMEL-9896)

Deadletter Failure processor is invoked even if error handling strategy defines to continue routing

[CAMEL-9891](https://issues.apache.org/jira/browse/CAMEL-9891)

ApplicationReadyEvent not dispatched if camel.springboot.main-run-controller = true

[CAMEL-9890](https://issues.apache.org/jira/browse/CAMEL-9890)

Migrate Camel-websocket to Jetty9

[CAMEL-9887](https://issues.apache.org/jira/browse/CAMEL-9887)

onCompletion not called on Splitter configured with CompletionAwareAggregationStrategy and shareUnitOfWork=true

[CAMEL-9881](https://issues.apache.org/jira/browse/CAMEL-9881)

Aggregator completionPredicate unusable with scala DSL

[CAMEL-9874](https://issues.apache.org/jira/browse/CAMEL-9874)

Camel Jetty consumer endpoint incorrectly handles multipart/form-data

[CAMEL-9872](https://issues.apache.org/jira/browse/CAMEL-9872)

VetoCamelContextStartException with rethrowException=false cases MainSupport class to hang

[CAMEL-9867](https://issues.apache.org/jira/browse/CAMEL-9867)

IndexOutOfBoundsException when MSH-18 is not present

[CAMEL-9866](https://issues.apache.org/jira/browse/CAMEL-9866)

@PropertyInject doesn't work with Spring-Boot

[CAMEL-9863](https://issues.apache.org/jira/browse/CAMEL-9863)

loopDoWhile will loop forever if using ahc component in the loop.

[CAMEL-9862](https://issues.apache.org/jira/browse/CAMEL-9862)

Potential NPE in UndertowComponent.unregisterConsumer

[CAMEL-9856](https://issues.apache.org/jira/browse/CAMEL-9856)

RestSwaggerProcessor fails with "Provider org.apache.xalan.processor.TransformerFactoryImpl not found"

[CAMEL-9854](https://issues.apache.org/jira/browse/CAMEL-9854)

CXF Stream Cache contains duplicate namespace definition

[CAMEL-9853](https://issues.apache.org/jira/browse/CAMEL-9853)

Camel-CXF: Possible NPE in DefaultCXFBinding

[CAMEL-9852](https://issues.apache.org/jira/browse/CAMEL-9852)

Camel-weather: freegeoip.net is no longer available. Need switch to something else.

[CAMEL-9851](https://issues.apache.org/jira/browse/CAMEL-9851)

Zookeeper RoutePolicy failing to create znode

[CAMEL-9850](https://issues.apache.org/jira/browse/CAMEL-9850)

Twitter: truncation has no effect

[CAMEL-9847](https://issues.apache.org/jira/browse/CAMEL-9847)

XMPP: private chat response issue

[CAMEL-9841](https://issues.apache.org/jira/browse/CAMEL-9841)

NPE in MIME-Multipart Data Format if no file name is defined on attachment

[CAMEL-9840](https://issues.apache.org/jira/browse/CAMEL-9840)

InfinispanIdempotentRepository should force return values for RemoteCaches

[CAMEL-9834](https://issues.apache.org/jira/browse/CAMEL-9834)

WatchConsumer does not properly set watchIndex

[CAMEL-9828](https://issues.apache.org/jira/browse/CAMEL-9828)

Swagger seems to inject empty headers

[CAMEL-9820](https://issues.apache.org/jira/browse/CAMEL-9820)

SFTP readLock=changed does not work with readLockMinAge option

[CAMEL-9819](https://issues.apache.org/jira/browse/CAMEL-9819)

camel-jetty8 test missing dependency

[CAMEL-9812](https://issues.apache.org/jira/browse/CAMEL-9812)

Camel leaves Kafka consumers running after shutdown

[CAMEL-9807](https://issues.apache.org/jira/browse/CAMEL-9807)

Blocking of CXF consumer endpoint by http GET request

[CAMEL-9805](https://issues.apache.org/jira/browse/CAMEL-9805)

camel-sql - body not copied from in to out when useing outputHeader and outputType=SelectOne when sql doesn't return a result

[CAMEL-9794](https://issues.apache.org/jira/browse/CAMEL-9794)

camel-http4 - The producer should check the response header in the reply for content-type

[CAMEL-9793](https://issues.apache.org/jira/browse/CAMEL-9793)

PropertyPlaceHolder not loading Property, thinks it is a Parameter

[CAMEL-9788](https://issues.apache.org/jira/browse/CAMEL-9788)

Jetty endpoint option "matchOnUriPrefix" does not work properly

[CAMEL-9784](https://issues.apache.org/jira/browse/CAMEL-9784)

Camel polling the files from S3 only once if deleteAfterRead is false

[CAMEL-9779](https://issues.apache.org/jira/browse/CAMEL-9779)

camel-netty4-http - Using no port number issue

[CAMEL-9777](https://issues.apache.org/jira/browse/CAMEL-9777)

camel-zipfile - Using zip iterator with dataformat may fail

[CAMEL-9774](https://issues.apache.org/jira/browse/CAMEL-9774)

CXFPayload may lose CDATA sections under stream caching

[CAMEL-9768](https://issues.apache.org/jira/browse/CAMEL-9768)

HTTP\[4\] component disableStreamCache issue: java.io.IOException: Attempted read from closed stream.

[CAMEL-9767](https://issues.apache.org/jira/browse/CAMEL-9767)

CDI deployment problem in JBoss EAP 6.3

[CAMEL-9766](https://issues.apache.org/jira/browse/CAMEL-9766)

camel-itest-karaf - Cannot install in karaf 4 Unknown protocol: wrap

[CAMEL-9741](https://issues.apache.org/jira/browse/CAMEL-9741)

recipientList stop if the second endpoint throw exception

[CAMEL-9739](https://issues.apache.org/jira/browse/CAMEL-9739)

Mina2Consumer exception handler do close session also for IOException

[CAMEL-9738](https://issues.apache.org/jira/browse/CAMEL-9738)

Thread leak for camel-mina2 consumers

[CAMEL-9728](https://issues.apache.org/jira/browse/CAMEL-9728)

change Reader to InputStream if the camel-cxf endpoint use RAW|MESSAGE DataFormat

[CAMEL-9656](https://issues.apache.org/jira/browse/CAMEL-9656)

Using SpringBoot HealthEndpoint bean throws AmbiguousMethodCallException

[CAMEL-9651](https://issues.apache.org/jira/browse/CAMEL-9651)

Restlet consumer request fails if there is a space '%20' in the url

[CAMEL-9642](https://issues.apache.org/jira/browse/CAMEL-9642)

restlet consumer request not propagating headers

[CAMEL-9631](https://issues.apache.org/jira/browse/CAMEL-9631)

The OsgiServiceRegistry class caches service references

[CAMEL-9463](https://issues.apache.org/jira/browse/CAMEL-9463)

Camel-guice OSGi dependency resolution fails

[CAMEL-9462](https://issues.apache.org/jira/browse/CAMEL-9462)

HTTP 1.1 Host header be dealt wrongly in proxy & load balancer

[CAMEL-9200](https://issues.apache.org/jira/browse/CAMEL-9200)

Context component conflates endpoints with the same local id from different CamelContexts

[CAMEL-9040](https://issues.apache.org/jira/browse/CAMEL-9040)

netty4-http - LEAK: ByteBuf.release() was not called before it's garbage-collected

[CAMEL-8789](https://issues.apache.org/jira/browse/CAMEL-8789)

Websocket with jetty 9 is not working due to class name and package name changes

[CAMEL-7884](https://issues.apache.org/jira/browse/CAMEL-7884)

camel-netty4-http does not work for HTTP POST requests on routingSlip

[CAMEL-7443](https://issues.apache.org/jira/browse/CAMEL-7443)

Remote Print URI changed to UNC Name

[CAMEL-7174](https://issues.apache.org/jira/browse/CAMEL-7174)

CacheManager should only be shutdown when last endpoint is stopped

[CAMEL-6720](https://issues.apache.org/jira/browse/CAMEL-6720)

SoapJaxbDataFormat not handling correctly SOAP action with request wrapper element

[CAMEL-6433](https://issues.apache.org/jira/browse/CAMEL-6433)

Invalid KeyStore format error is generated using camel websocket secure on osgi platform

[CAMEL-6256](https://issues.apache.org/jira/browse/CAMEL-6256)

Camel xmpp dynamic router is not sending incoming messages to openfire upon first failed groupchatroom join

### Improvement (223)

[CAMEL-10432](https://issues.apache.org/jira/browse/CAMEL-10432)

concurrentlinkedhashmap used by LRU cache consumes 100MB memory on 1024 core Solaris T5

[CAMEL-10347](https://issues.apache.org/jira/browse/CAMEL-10347)

Camel-scr todos and polish

[CAMEL-10343](https://issues.apache.org/jira/browse/CAMEL-10343)

Camel Netty4 allowSerializedHeaders

[CAMEL-10339](https://issues.apache.org/jira/browse/CAMEL-10339)

Allow date offsets and timezones with Simple language

[CAMEL-10334](https://issues.apache.org/jira/browse/CAMEL-10334)

Use of whitespaces in remotePath

[CAMEL-10331](https://issues.apache.org/jira/browse/CAMEL-10331)

Camel Docker Consumer

[CAMEL-10328](https://issues.apache.org/jira/browse/CAMEL-10328)

Enhance Slack component to support attachments in webhooks

[CAMEL-10325](https://issues.apache.org/jira/browse/CAMEL-10325)

Camel-Aws: EC2 component, add createTags and deleteTags operation

[CAMEL-10307](https://issues.apache.org/jira/browse/CAMEL-10307)

Upgrade docker java version

[CAMEL-10302](https://issues.apache.org/jira/browse/CAMEL-10302)

Extract body from nested multiparts

[CAMEL-10298](https://issues.apache.org/jira/browse/CAMEL-10298)

Unnecessary restriction on readLockTimeout with readLockMinAge

[CAMEL-10297](https://issues.apache.org/jira/browse/CAMEL-10297)

Camel-Ftp: Splitting the body doesn't parse the file content but the RemoteFile

[CAMEL-10290](https://issues.apache.org/jira/browse/CAMEL-10290)

Move RoutePolicy initialization logic in onStart

[CAMEL-10289](https://issues.apache.org/jira/browse/CAMEL-10289)

Move RoutePolicy initialization logic in onStart

[CAMEL-10288](https://issues.apache.org/jira/browse/CAMEL-10288)

Move RoutePolicy initialization logic in onStart

[CAMEL-10285](https://issues.apache.org/jira/browse/CAMEL-10285)

beanio - Allow custom error handler to access exchange

[CAMEL-10284](https://issues.apache.org/jira/browse/CAMEL-10284)

No shutdown for custom workerPool in NettyProducer

[CAMEL-10280](https://issues.apache.org/jira/browse/CAMEL-10280)

Don't require create privileges to publish to named SNS topic

[CAMEL-10276](https://issues.apache.org/jira/browse/CAMEL-10276)

Update camel-syslog to use Netty4

[CAMEL-10275](https://issues.apache.org/jira/browse/CAMEL-10275)

Allow @ProperyInject on bean method arguments

[CAMEL-10270](https://issues.apache.org/jira/browse/CAMEL-10270)

Jetty 9 X-Forwarded-For Configuration

[CAMEL-10269](https://issues.apache.org/jira/browse/CAMEL-10269)

Optimize DefaultCamelContext#getComponent

[CAMEL-10268](https://issues.apache.org/jira/browse/CAMEL-10268)

Camel-CouchDB: Add the ability to remove an entry from producer side

[CAMEL-10262](https://issues.apache.org/jira/browse/CAMEL-10262)

camel-kubernetes component should be able to rely on the current login token provided by kube config

[CAMEL-10260](https://issues.apache.org/jira/browse/CAMEL-10260)

Olingo2 component should declare runtime dependency on olingo-odata2-core

[CAMEL-10256](https://issues.apache.org/jira/browse/CAMEL-10256)

camel-cache - Upgrade to EHCache 3.x

[CAMEL-10248](https://issues.apache.org/jira/browse/CAMEL-10248)

camel-catalog - Include adoc documentation

[CAMEL-10246](https://issues.apache.org/jira/browse/CAMEL-10246)

camel-ftp - Add support for configuring active port range

[CAMEL-10245](https://issues.apache.org/jira/browse/CAMEL-10245)

Persistence Exception when trying to delete detached entity

[CAMEL-10242](https://issues.apache.org/jira/browse/CAMEL-10242)

camel-mllp - Enhance Camel to support idleTimeout to avoid network resource wastage due to leak in caller code

[CAMEL-10240](https://issues.apache.org/jira/browse/CAMEL-10240)

CamelHttpClient default pool size does not work on system with large number of cpus

[CAMEL-10235](https://issues.apache.org/jira/browse/CAMEL-10235)

Add fluentTemplate to XML DSL

[CAMEL-10234](https://issues.apache.org/jira/browse/CAMEL-10234)

Improve OSGi camel-jcache support

[CAMEL-10233](https://issues.apache.org/jira/browse/CAMEL-10233)

SpringCamelContext should lazy load ModelJAXBContextFactory

[CAMEL-10228](https://issues.apache.org/jira/browse/CAMEL-10228)

camel-sql - Preserver attachments

[CAMEL-10226](https://issues.apache.org/jira/browse/CAMEL-10226)

camel-jms ignores connection pool settings in spring-boot deployment

[CAMEL-10223](https://issues.apache.org/jira/browse/CAMEL-10223)

XmlRpc dataformat - Setting request=true should also apply for marshal

[CAMEL-10219](https://issues.apache.org/jira/browse/CAMEL-10219)

Add support in JAXB module to use injected CharacterEscapeHandler

[CAMEL-10216](https://issues.apache.org/jira/browse/CAMEL-10216)

Camel-Http4: Endpoint parameters proxyHost and proxyPort are ignored

[CAMEL-10213](https://issues.apache.org/jira/browse/CAMEL-10213)

Camel Kafka doesn't support setting "max.poll.records" and "session.timeout.ms"

[CAMEL-10212](https://issues.apache.org/jira/browse/CAMEL-10212)

Camel-Undertow: transferException and throwExceptionOnFailure options are never used in the component

[CAMEL-10211](https://issues.apache.org/jira/browse/CAMEL-10211)

spring boot - Auto configuration of tracer

[CAMEL-10210](https://issues.apache.org/jira/browse/CAMEL-10210)

Trace formatter - Add support for multiline

[CAMEL-10203](https://issues.apache.org/jira/browse/CAMEL-10203)

Spring boot - Auto configuration should not use primitive types

[CAMEL-10201](https://issues.apache.org/jira/browse/CAMEL-10201)

More Type Converters for Multipart

[CAMEL-10197](https://issues.apache.org/jira/browse/CAMEL-10197)

camel-spring-boot - Extend the configuration hints to nested properties

[CAMEL-10196](https://issues.apache.org/jira/browse/CAMEL-10196)

Camel KAfka doesn't support SASL\_PLAINTEXT security protocol

[CAMEL-10194](https://issues.apache.org/jira/browse/CAMEL-10194)

camel-spring-boot - Bind components and data format to the spring context so they are picked up automatically

[CAMEL-10190](https://issues.apache.org/jira/browse/CAMEL-10190)

Fallback lookup components, data-formats and languages using suffix in name to avoid clash

[CAMEL-10189](https://issues.apache.org/jira/browse/CAMEL-10189)

camel-jsonpath - Add support for simple functions

[CAMEL-10183](https://issues.apache.org/jira/browse/CAMEL-10183)

Camel-Aws: add list and delete buckets operations on the S3 Producer Endpoint

[CAMEL-10180](https://issues.apache.org/jira/browse/CAMEL-10180)

weaveByToUri - To make it easier to match sending to uris

[CAMEL-10179](https://issues.apache.org/jira/browse/CAMEL-10179)

Frequent BlockingOperationExceptions under load in NettyProducer.openChannel()

[CAMEL-10172](https://issues.apache.org/jira/browse/CAMEL-10172)

BeanProducer unlike BeanProcessor do not implement fully async protocol

[CAMEL-10168](https://issues.apache.org/jira/browse/CAMEL-10168)

Don't print stacktrace when Kinesis not available on startup

[CAMEL-10167](https://issues.apache.org/jira/browse/CAMEL-10167)

Camel-Github: Use constants instead of String for headers and registry names

[CAMEL-10166](https://issues.apache.org/jira/browse/CAMEL-10166)

Binding a queue on the default exchange is not always allowed

[CAMEL-10158](https://issues.apache.org/jira/browse/CAMEL-10158)

Support to add tags to workflow execution in camel-aws component

[CAMEL-10156](https://issues.apache.org/jira/browse/CAMEL-10156)

arguments of <bean method> ignored if syntax error in method call

[CAMEL-10140](https://issues.apache.org/jira/browse/CAMEL-10140)

Java 8 type safe process DSL

[CAMEL-10134](https://issues.apache.org/jira/browse/CAMEL-10134)

Camel-Kubernetes: Add the ability to consume events from Resources filtered by labels and/or name

[CAMEL-10132](https://issues.apache.org/jira/browse/CAMEL-10132)

Camel-Kubernetes: Add the ability to scale up and down a replication controller from Producer

[CAMEL-10131](https://issues.apache.org/jira/browse/CAMEL-10131)

Add exclusive queues support to RabbitMQ component

[CAMEL-10127](https://issues.apache.org/jira/browse/CAMEL-10127)

OsgiDefaultCamelContext should call parent constructor with registry

[CAMEL-10125](https://issues.apache.org/jira/browse/CAMEL-10125)

WARN on startup: "No Server set for org.apache.camel.component.jetty.JettyHttpComponent$1@3d484181"

[CAMEL-10122](https://issues.apache.org/jira/browse/CAMEL-10122)

spring boot - Auto configuration for http component has prefix https

[CAMEL-10121](https://issues.apache.org/jira/browse/CAMEL-10121)

ResponseHandler in Mina2Producer should not log errors

[CAMEL-10119](https://issues.apache.org/jira/browse/CAMEL-10119)

Upgrade to Spring 4.3.x

[CAMEL-10114](https://issues.apache.org/jira/browse/CAMEL-10114)

camel-spring-boot - Allow to configure stream caching using application.properties

[CAMEL-10113](https://issues.apache.org/jira/browse/CAMEL-10113)

camel-spring-boot - Add support for auto detection of advanced configuration

[CAMEL-10109](https://issues.apache.org/jira/browse/CAMEL-10109)

Camel Spring Boot does not load EventNotifiers

[CAMEL-10108](https://issues.apache.org/jira/browse/CAMEL-10108)

Improve api-component-framework

[CAMEL-10096](https://issues.apache.org/jira/browse/CAMEL-10096)

Camel tracer with stream caching should tracer after stream cache has been setup

[CAMEL-10095](https://issues.apache.org/jira/browse/CAMEL-10095)

bug in "remove whitespace noise from uri"

[CAMEL-10085](https://issues.apache.org/jira/browse/CAMEL-10085)

UnsafeUriCharactersEncoder.checkRAW compiles regex pattern every call

[CAMEL-10081](https://issues.apache.org/jira/browse/CAMEL-10081)

Camel OSGi examples - Update readme for karaf 4 style

[CAMEL-10080](https://issues.apache.org/jira/browse/CAMEL-10080)

CxfPayloadConverter to use a XMLStreamReader based conversion if applicable

[CAMEL-10072](https://issues.apache.org/jira/browse/CAMEL-10072)

camel-etcd : implement watching ServiceCallServerListStrategy

[CAMEL-10071](https://issues.apache.org/jira/browse/CAMEL-10071)

camel-sip - hard dependency on log4j 1.2.x JAR

[CAMEL-10070](https://issues.apache.org/jira/browse/CAMEL-10070)

Add XMLStreamReader to InputStream/Reader converter

[CAMEL-10068](https://issues.apache.org/jira/browse/CAMEL-10068)

Distribuited map, retrieve hashmap keys

[CAMEL-10062](https://issues.apache.org/jira/browse/CAMEL-10062)

For specialized Dataformats, provide default value in catalog

[CAMEL-10058](https://issues.apache.org/jira/browse/CAMEL-10058)

when cxf producer use MESSAGE DataFormat, it shouldn't also configure as messageType=text

[CAMEL-10057](https://issues.apache.org/jira/browse/CAMEL-10057)

Support Spring modular batch config

[CAMEL-10056](https://issues.apache.org/jira/browse/CAMEL-10056)

ServiceCall EIP : add missing configuration options to ConsulConfigurationDefinition

[CAMEL-10055](https://issues.apache.org/jira/browse/CAMEL-10055)

ServiceCall EIP : add missing configuration options to EtcdConfigurationDefinition

[CAMEL-10052](https://issues.apache.org/jira/browse/CAMEL-10052)

Adding spring-boot integration tests

[CAMEL-10050](https://issues.apache.org/jira/browse/CAMEL-10050)

Routing slip - Consider not caching error handlers

[CAMEL-10049](https://issues.apache.org/jira/browse/CAMEL-10049)

Context scoped processors should be shutdown when CamelContext is shutting down

[CAMEL-10045](https://issues.apache.org/jira/browse/CAMEL-10045)

camel-spring-boot - Allow to load sensitive options from external file

[CAMEL-10044](https://issues.apache.org/jira/browse/CAMEL-10044)

Mark secret options such as password/passphrase so tooling would be aware

[CAMEL-10042](https://issues.apache.org/jira/browse/CAMEL-10042)

camel-spring-boot - Add default values to auto configuration

[CAMEL-10041](https://issues.apache.org/jira/browse/CAMEL-10041)

camel-spring-boot - Add data format options as type-safe configuration properties

[CAMEL-10040](https://issues.apache.org/jira/browse/CAMEL-10040)

camel-ahc - Upgrade AHC client to 2.x

[CAMEL-10036](https://issues.apache.org/jira/browse/CAMEL-10036)

Dynamicaly Loaded XML Rests Bind to all RestConfigurations

[CAMEL-10030](https://issues.apache.org/jira/browse/CAMEL-10030)

BindyKeyValuePairDataFormat shold detect if the body is a map, a list of map or a simple value when marshalling

[CAMEL-10029](https://issues.apache.org/jira/browse/CAMEL-10029)

Allow camel-jackson to unmarshall more type by default

[CAMEL-10021](https://issues.apache.org/jira/browse/CAMEL-10021)

Class component - Should allow to call static method on class without ctr

[CAMEL-10020](https://issues.apache.org/jira/browse/CAMEL-10020)

Camel KafkaProducer should be able to return back RecordMetadata

[CAMEL-10019](https://issues.apache.org/jira/browse/CAMEL-10019)

camel-mongodb - Consider sortBy header when performing findOneByQuery operation

[CAMEL-10018](https://issues.apache.org/jira/browse/CAMEL-10018)

Support AWS assume role in Camel Aws components

[CAMEL-10007](https://issues.apache.org/jira/browse/CAMEL-10007)

camel-zipfile - ZipAggregationStrategy should ignore zero byte files

[CAMEL-10004](https://issues.apache.org/jira/browse/CAMEL-10004)

PollEnrich - Allow to bridge error handler

[CAMEL-10003](https://issues.apache.org/jira/browse/CAMEL-10003)

camel-netty4 - Add support for native transport

[CAMEL-10002](https://issues.apache.org/jira/browse/CAMEL-10002)

camel-netty4 - Upgrade to Netty 4.1.x

[CAMEL-10001](https://issues.apache.org/jira/browse/CAMEL-10001)

Add support for using any property placeholders on load balancers

[CAMEL-9996](https://issues.apache.org/jira/browse/CAMEL-9996)

Use passed in Camel Context in org.apache.camel.spi.RestConsumerFactory#createConsumer implementations

[CAMEL-9990](https://issues.apache.org/jira/browse/CAMEL-9990)

camel-ftp: Excessive loggging: JSCH -> Permanently added 'X' (RSA) to the list of known hosts.

[CAMEL-9979](https://issues.apache.org/jira/browse/CAMEL-9979)

Bean parameter binding should reset stream cache before evaluate message body

[CAMEL-9966](https://issues.apache.org/jira/browse/CAMEL-9966)

Restlet - Should not enable stream by default

[CAMEL-9963](https://issues.apache.org/jira/browse/CAMEL-9963)

camel-blueprint - Namespace parser should skip placeholders for component dependencies

[CAMEL-9962](https://issues.apache.org/jira/browse/CAMEL-9962)

Add a field in the consumer to define if it subscribed to the topic or not

[CAMEL-9957](https://issues.apache.org/jira/browse/CAMEL-9957)

camel-kafka producer sends the message in an async way

[CAMEL-9956](https://issues.apache.org/jira/browse/CAMEL-9956)

Add support for FluentProducerTemplate to CamelTestSupport

[CAMEL-9955](https://issues.apache.org/jira/browse/CAMEL-9955)

Add uptimeMillis as JMX attribute to CamelContextMBean

[CAMEL-9954](https://issues.apache.org/jira/browse/CAMEL-9954)

FormatFactory should be real Factory-pattern

[CAMEL-9944](https://issues.apache.org/jira/browse/CAMEL-9944)

FluentProducerTemplate - Make extract as part of UoW

[CAMEL-9940](https://issues.apache.org/jira/browse/CAMEL-9940)

ProducerTemplate - Make extract result set part of UoW

[CAMEL-9939](https://issues.apache.org/jira/browse/CAMEL-9939)

beanio - Add support for custom BeanReaderErrorHandler

[CAMEL-9938](https://issues.apache.org/jira/browse/CAMEL-9938)

TimerPatternConverter - Should be more strict

[CAMEL-9937](https://issues.apache.org/jira/browse/CAMEL-9937)

camel-catalog - Add api to validate time pattern

[CAMEL-9932](https://issues.apache.org/jira/browse/CAMEL-9932)

sql-stored - Add support for arrays in grammar

[CAMEL-9927](https://issues.apache.org/jira/browse/CAMEL-9927)

Reduce object creation in RedisProducer

[CAMEL-9925](https://issues.apache.org/jira/browse/CAMEL-9925)

Update Salesforce component to use Jetty9

[CAMEL-9919](https://issues.apache.org/jira/browse/CAMEL-9919)

camel-salesforce - Use a better http client

[CAMEL-9915](https://issues.apache.org/jira/browse/CAMEL-9915)

Allow to use the tarfile data format in XML marshal/unmarshal

[CAMEL-9910](https://issues.apache.org/jira/browse/CAMEL-9910)

Camel Rest - automatic component discovery

[CAMEL-9909](https://issues.apache.org/jira/browse/CAMEL-9909)

Camel-Cassandraql: Supports missing Load Balancing policies

[CAMEL-9905](https://issues.apache.org/jira/browse/CAMEL-9905)

TarAggregationStragegy should delete temporary files

[CAMEL-9904](https://issues.apache.org/jira/browse/CAMEL-9904)

Avoid creating an empty default Camel context in Camel CDI for empty deployments

[CAMEL-9900](https://issues.apache.org/jira/browse/CAMEL-9900)

camel-jms - provide option for MessageListenerContainer for reply managers to stop quicker when CamelContext is stopping

[CAMEL-9899](https://issues.apache.org/jira/browse/CAMEL-9899)

camel-rx - Use a worker pool for tasks such as stopping consumers

[CAMEL-9897](https://issues.apache.org/jira/browse/CAMEL-9897)

Add an Option to the XSLT Component to support custom EntityResolver

[CAMEL-9895](https://issues.apache.org/jira/browse/CAMEL-9895)

Setup a by default password to access the spring boot ssh server

[CAMEL-9892](https://issues.apache.org/jira/browse/CAMEL-9892)

Aggregator completionPredicate does not support a more complex block with scala DSL

[CAMEL-9889](https://issues.apache.org/jira/browse/CAMEL-9889)

Allow external components to provide custom mbeans for processors

[CAMEL-9885](https://issues.apache.org/jira/browse/CAMEL-9885)

Camel-NATS: Add an option to specify the optional reply subject

[CAMEL-9880](https://issues.apache.org/jira/browse/CAMEL-9880)

Header Support for Attachments in Camel 2.18

[CAMEL-9878](https://issues.apache.org/jira/browse/CAMEL-9878)

camel-commands - Add command to show top N inflight exchanges per routes

[CAMEL-9877](https://issues.apache.org/jira/browse/CAMEL-9877)

InflightRepository - Add browse that can limit per route

[CAMEL-9875](https://issues.apache.org/jira/browse/CAMEL-9875)

CamelBlueprintTestSupport lacks support for multiple PID loading

[CAMEL-9873](https://issues.apache.org/jira/browse/CAMEL-9873)

Component should provide detail if a consumer/producer is native async supported

[CAMEL-9871](https://issues.apache.org/jira/browse/CAMEL-9871)

FlatpackDataFormat ignores errors in Flatpack's DataSet

[CAMEL-9870](https://issues.apache.org/jira/browse/CAMEL-9870)

bean component - Add validation for parenthesis check

[CAMEL-9868](https://issues.apache.org/jira/browse/CAMEL-9868)

Rework Attachment Support in Camel Message and related Interfaces

[CAMEL-9865](https://issues.apache.org/jira/browse/CAMEL-9865)

Camel Karaf Commands - Upgrade to Karaf 3/4

[CAMEL-9861](https://issues.apache.org/jira/browse/CAMEL-9861)

camel-rx - Allow to consume/produce as observable

[CAMEL-9860](https://issues.apache.org/jira/browse/CAMEL-9860)

csv dataformat - Should have quoteMode option in model

[CAMEL-9859](https://issues.apache.org/jira/browse/CAMEL-9859)

Re-enable Netty4 Channel Options.

[CAMEL-9848](https://issues.apache.org/jira/browse/CAMEL-9848)

Add mapHttpMessageFormUrlEncodedBody option

[CAMEL-9845](https://issues.apache.org/jira/browse/CAMEL-9845)

camel-jdbc - Silent ignore close errors

[CAMEL-9844](https://issues.apache.org/jira/browse/CAMEL-9844)

support for arn in aws-sqs connection string

[CAMEL-9843](https://issues.apache.org/jira/browse/CAMEL-9843)

camel-beanio - Add BeanIOSplitter

[CAMEL-9842](https://issues.apache.org/jira/browse/CAMEL-9842)

Expose additional endpoint configuration options to UndertowHost handler methods

[CAMEL-9838](https://issues.apache.org/jira/browse/CAMEL-9838)

Add ends with operator to simple language

[CAMEL-9833](https://issues.apache.org/jira/browse/CAMEL-9833)

Add mapHttpMessage option to allow to turn off mapping by default

[CAMEL-9831](https://issues.apache.org/jira/browse/CAMEL-9831)

Camel-http4: Make possible to use System Properties for configuration

[CAMEL-9830](https://issues.apache.org/jira/browse/CAMEL-9830)

camel-spring-javaconfig - Add routes like spring-boot does

[CAMEL-9826](https://issues.apache.org/jira/browse/CAMEL-9826)

MongoDB consumer could potentially block during shutdown

[CAMEL-9822](https://issues.apache.org/jira/browse/CAMEL-9822)

Upgrade to DeltaSpike 1.6.1

[CAMEL-9818](https://issues.apache.org/jira/browse/CAMEL-9818)

Camel kafka consumer adds legacy (deprecated properties) in the kafka consumer

[CAMEL-9816](https://issues.apache.org/jira/browse/CAMEL-9816)

StreamCache - The cache method should support OUT as well

[CAMEL-9815](https://issues.apache.org/jira/browse/CAMEL-9815)

Add URI parameter to skip the declaration of the exchange

[CAMEL-9811](https://issues.apache.org/jira/browse/CAMEL-9811)

camel-cdi - Add support for consumer template injection

[CAMEL-9808](https://issues.apache.org/jira/browse/CAMEL-9808)

SFTP: Enable configuration of bulk requests

[CAMEL-9803](https://issues.apache.org/jira/browse/CAMEL-9803)

Camel-NATS: Switch to Jnats client as Java\_nats is deprecated

[CAMEL-9801](https://issues.apache.org/jira/browse/CAMEL-9801)

Camel Archetypes - Add Camel BOM as dependency management

[CAMEL-9798](https://issues.apache.org/jira/browse/CAMEL-9798)

camel-cdi - Add support for injecting default ProducerTemplate

[CAMEL-9796](https://issues.apache.org/jira/browse/CAMEL-9796)

Internal Access still displayed, no change to JSON generated

[CAMEL-9795](https://issues.apache.org/jira/browse/CAMEL-9795)

camel-zipkin - Reuse existing span for complex eips like multicast

[CAMEL-9791](https://issues.apache.org/jira/browse/CAMEL-9791)

DeadLetterChannel not triggered on RejectedExecutionException

[CAMEL-9790](https://issues.apache.org/jira/browse/CAMEL-9790)

camel-kafka 2.17 not throwing TimeoutException back which is throw by Kafka client

[CAMEL-9789](https://issues.apache.org/jira/browse/CAMEL-9789)

CamelContext.getEndpoint should not start endpoint if Camel is starting up

[CAMEL-9783](https://issues.apache.org/jira/browse/CAMEL-9783)

Allow ConnectionConfiguration to be be injected to endpoint during connection creation

[CAMEL-9782](https://issues.apache.org/jira/browse/CAMEL-9782)

camel-spring-boot - Allow to configure options on CamelContext using auto config

[CAMEL-9776](https://issues.apache.org/jira/browse/CAMEL-9776)

camel-braintree: add uri param to configure advanced options

[CAMEL-9775](https://issues.apache.org/jira/browse/CAMEL-9775)

Clean configuration meta-datat description

[CAMEL-9772](https://issues.apache.org/jira/browse/CAMEL-9772)

Make it easier to turn on/off logExhaustedMessageBody

[CAMEL-9769](https://issues.apache.org/jira/browse/CAMEL-9769)

camel-spring-javaconfig - Make the main class easier

[CAMEL-9765](https://issues.apache.org/jira/browse/CAMEL-9765)

Direct-VM: Add header filter strategy and property propagation flag

[CAMEL-9762](https://issues.apache.org/jira/browse/CAMEL-9762)

Add setters on SecureSocketProtocolsParameters and CipherSuitesParameters

[CAMEL-9761](https://issues.apache.org/jira/browse/CAMEL-9761)

camel-swagger-java - Allow to use custom CORS headers for api-docs

[CAMEL-9755](https://issues.apache.org/jira/browse/CAMEL-9755)

Allow for nickserv identification

[CAMEL-9752](https://issues.apache.org/jira/browse/CAMEL-9752)

Quartz2 Scheduled route too many workers

[CAMEL-9745](https://issues.apache.org/jira/browse/CAMEL-9745)

Splitter - Should skip null messages if iterator returns null

[CAMEL-9743](https://issues.apache.org/jira/browse/CAMEL-9743)

Apache Camel distro - Only keep camel JARs

[CAMEL-9740](https://issues.apache.org/jira/browse/CAMEL-9740)

Improve camel-infinispan

[CAMEL-9736](https://issues.apache.org/jira/browse/CAMEL-9736)

SolrComponent gets the wrong Content Type

[CAMEL-9735](https://issues.apache.org/jira/browse/CAMEL-9735)

camel-tarfile throws OutOfMemoryError when splitting large files

[CAMEL-9690](https://issues.apache.org/jira/browse/CAMEL-9690)

bean parameter binding should check parameter types when using simple expressions

[CAMEL-9683](https://issues.apache.org/jira/browse/CAMEL-9683)

native client side kubernetes based load balancer

[CAMEL-9600](https://issues.apache.org/jira/browse/CAMEL-9600)

camel-fop - Upgrade fop to 2.1

[CAMEL-9587](https://issues.apache.org/jira/browse/CAMEL-9587)

camel-restlet - Make it easy to turn on gson or jackson

[CAMEL-9549](https://issues.apache.org/jira/browse/CAMEL-9549)

camel-schematron - More fine grained error messages when compiling the schema

[CAMEL-9521](https://issues.apache.org/jira/browse/CAMEL-9521)

camel-spring - Move osgi/spring-dm to camel-spring-dm

[CAMEL-9476](https://issues.apache.org/jira/browse/CAMEL-9476)

camel-bindy doesn't pad fixed length records

[CAMEL-9428](https://issues.apache.org/jira/browse/CAMEL-9428)

Camel catalog - Include details about CamelContext XML

[CAMEL-9332](https://issues.apache.org/jira/browse/CAMEL-9332)

Support @MockEndpoint and @MockEndpointAndSkip in Spring Boot

[CAMEL-9273](https://issues.apache.org/jira/browse/CAMEL-9273)

Enhance camel-weather component to support all the options of Api 2.5

[CAMEL-9250](https://issues.apache.org/jira/browse/CAMEL-9250)

Configure AllowUseOriginalMessage to be disabled by default if not in use on error handler

[CAMEL-9176](https://issues.apache.org/jira/browse/CAMEL-9176)

CXFRS endpoint should ideally be singleton

[CAMEL-9131](https://issues.apache.org/jira/browse/CAMEL-9131)

Camel components - Add more labels to group the options

[CAMEL-9067](https://issues.apache.org/jira/browse/CAMEL-9067)

File consumer - Allow to filter by expression and have two options one for directory and another for file name

[CAMEL-9046](https://issues.apache.org/jira/browse/CAMEL-9046)

Support to setup the SSLContext of CXF client from camel ssl setting

[CAMEL-8854](https://issues.apache.org/jira/browse/CAMEL-8854)

Support setting sendServerVersion as parameter of the JettyHttpComponent

[CAMEL-8830](https://issues.apache.org/jira/browse/CAMEL-8830)

Upgrade to Saxon HE 9.7

[CAMEL-8776](https://issues.apache.org/jira/browse/CAMEL-8776)

Using MonogoClient class in camel-mongodb

[CAMEL-8668](https://issues.apache.org/jira/browse/CAMEL-8668)

Refactoring of Camel-MongoDB based on Java Driver 3.x

[CAMEL-8654](https://issues.apache.org/jira/browse/CAMEL-8654)

Camel http should not de-serialize the ObjectInputStream when it works in Proxy mode

[CAMEL-8633](https://issues.apache.org/jira/browse/CAMEL-8633)

Servlet & Multipart

[CAMEL-8380](https://issues.apache.org/jira/browse/CAMEL-8380)

Add documentation for spring/blueprint only types that are in the generated xml dsl

[CAMEL-8287](https://issues.apache.org/jira/browse/CAMEL-8287)

Schematron component does not work with includes in schematron

[CAMEL-8219](https://issues.apache.org/jira/browse/CAMEL-8219)

camel-smpp - use jsmpp version 2.2.x or later

[CAMEL-7891](https://issues.apache.org/jira/browse/CAMEL-7891)

SetMessageEmmiter addition not work with latest Saxon

[CAMEL-7853](https://issues.apache.org/jira/browse/CAMEL-7853)

Implement AggregationRepository based on Infinispan data grid

[CAMEL-7660](https://issues.apache.org/jira/browse/CAMEL-7660)

Add support for expression on tokenizeXml

[CAMEL-6707](https://issues.apache.org/jira/browse/CAMEL-6707)

Asynchronous Mode In camel-servlet, Servlet 3.0 AsyncContext

[CAMEL-6616](https://issues.apache.org/jira/browse/CAMEL-6616)

On SMPP producer start if SMSC returns a negative bind response producer will get stuck in an infinite reconnect loop

[CAMEL-6439](https://issues.apache.org/jira/browse/CAMEL-6439)

camel-jms - Add thread pool for handling timeout when doing request/reply and allow to configure this thread pool

[CAMEL-5690](https://issues.apache.org/jira/browse/CAMEL-5690)

Using bean component with beans that implement Service from Camel should have the lifecycle callbacks invoked

[CAMEL-5585](https://issues.apache.org/jira/browse/CAMEL-5585)

RedeliverErrorHandler - Should quicker reject running scheduled redeliver tasks if shutting down and not allowed to do redeliver

[CAMEL-5252](https://issues.apache.org/jira/browse/CAMEL-5252)

Simple language - Improved OGNL invocation with simple expression as functions for parameters

[CAMEL-4532](https://issues.apache.org/jira/browse/CAMEL-4532)

improve printer support on unix

### New Feature (66)

[CAMEL-10319](https://issues.apache.org/jira/browse/CAMEL-10319)

SNMP Producer

[CAMEL-10317](https://issues.apache.org/jira/browse/CAMEL-10317)

Add support to use Http synchronous client with Olingo2 Component

[CAMEL-10308](https://issues.apache.org/jira/browse/CAMEL-10308)

Provide a way to use async engine from ProducerTemplate

[CAMEL-10305](https://issues.apache.org/jira/browse/CAMEL-10305)

Add support for calling function imports from Olingo2 Component

[CAMEL-10295](https://issues.apache.org/jira/browse/CAMEL-10295)

hazelcast map data store documentation

[CAMEL-10286](https://issues.apache.org/jira/browse/CAMEL-10286)

Allow async bean method in bean language with J8 CompletableFuture

[CAMEL-10255](https://issues.apache.org/jira/browse/CAMEL-10255)

Camel Main - Make it easy to configure property placeholder

[CAMEL-10239](https://issues.apache.org/jira/browse/CAMEL-10239)

Extend Camel RabbitMQ with guaranteed delivery (basic.return)

[CAMEL-10222](https://issues.apache.org/jira/browse/CAMEL-10222)

camel-spring-boot - New starters and BOMs

[CAMEL-10209](https://issues.apache.org/jira/browse/CAMEL-10209)

spring boot - Auto configuration for languages

[CAMEL-10208](https://issues.apache.org/jira/browse/CAMEL-10208)

FluentProducerTemplate - Allow to be injected

[CAMEL-10169](https://issues.apache.org/jira/browse/CAMEL-10169)

supporting OSGi service.pid by registry

[CAMEL-10164](https://issues.apache.org/jira/browse/CAMEL-10164)

camel-swagger to component

[CAMEL-10159](https://issues.apache.org/jira/browse/CAMEL-10159)

github endpoint to support creating issues

[CAMEL-10133](https://issues.apache.org/jira/browse/CAMEL-10133)

New camel-lumberjack component

[CAMEL-10112](https://issues.apache.org/jira/browse/CAMEL-10112)

Camel-CoAP: Add Ping operation to CoAP Producer

[CAMEL-10100](https://issues.apache.org/jira/browse/CAMEL-10100)

Add support for copyObject in camel aws-s3

[CAMEL-10092](https://issues.apache.org/jira/browse/CAMEL-10092)

Camel catalog - Include offline details about previous releases

[CAMEL-10083](https://issues.apache.org/jira/browse/CAMEL-10083)

Add "disconnectOnBatchComplete" option to close FTP connection immediately after Batch of upload complete

[CAMEL-10066](https://issues.apache.org/jira/browse/CAMEL-10066)

Add support for InfluxDB

[CAMEL-10061](https://issues.apache.org/jira/browse/CAMEL-10061)

Add JSON Johnzon DataFormat

[CAMEL-10059](https://issues.apache.org/jira/browse/CAMEL-10059)

Add option to generate Java 1.8 Optional<?> based DTOs

[CAMEL-10025](https://issues.apache.org/jira/browse/CAMEL-10025)

Create a DNS based ServiceCall EIP

[CAMEL-10022](https://issues.apache.org/jira/browse/CAMEL-10022)

add a Spring Boot HealthIndicator to check that all camel contexts have started up and all the routes started OK

[CAMEL-10006](https://issues.apache.org/jira/browse/CAMEL-10006)

Create MongoDB Idempotent repository

[CAMEL-9989](https://issues.apache.org/jira/browse/CAMEL-9989)

Create a Consul based ServiceCall EIP

[CAMEL-9988](https://issues.apache.org/jira/browse/CAMEL-9988)

Create an Etcd based ServiceCall EIP

[CAMEL-9980](https://issues.apache.org/jira/browse/CAMEL-9980)

Allow to call OGNL on simple bodyAs function

[CAMEL-9974](https://issues.apache.org/jira/browse/CAMEL-9974)

camel-sjms - Add completionPredicate to batch component

[CAMEL-9969](https://issues.apache.org/jira/browse/CAMEL-9969)

Adding a component for Telegram

[CAMEL-9964](https://issues.apache.org/jira/browse/CAMEL-9964)

Annotation based DefaultProducer

[CAMEL-9946](https://issues.apache.org/jira/browse/CAMEL-9946)

Camel-Kubernetes: Add support for ConfigMap

[CAMEL-9943](https://issues.apache.org/jira/browse/CAMEL-9943)

Expose mail session as a URI option for camel-mail endpoints

[CAMEL-9916](https://issues.apache.org/jira/browse/CAMEL-9916)

SJMS component is not currently nodev/XML route compatible

[CAMEL-9907](https://issues.apache.org/jira/browse/CAMEL-9907)

Camel-Infinispan: Exposing cache stats through producer

[CAMEL-9888](https://issues.apache.org/jira/browse/CAMEL-9888)

Create a camel-consul component

[CAMEL-9886](https://issues.apache.org/jira/browse/CAMEL-9886)

Create an etcd based RoutePolicy

[CAMEL-9884](https://issues.apache.org/jira/browse/CAMEL-9884)

Create a camel-ehcache component

[CAMEL-9883](https://issues.apache.org/jira/browse/CAMEL-9883)

Add a SpringCache based idempotent repository

[CAMEL-9882](https://issues.apache.org/jira/browse/CAMEL-9882)

Support importing Camel XML configuration files in Camel CDI

[CAMEL-9879](https://issues.apache.org/jira/browse/CAMEL-9879)

Circuit Breaker EIP - That is using hystrix

[CAMEL-9869](https://issues.apache.org/jira/browse/CAMEL-9869)

Create Apache Flink Component

[CAMEL-9858](https://issues.apache.org/jira/browse/CAMEL-9858)

Add support for maven classifiers to camel-grape component

[CAMEL-9849](https://issues.apache.org/jira/browse/CAMEL-9849)

camel-sql - Add support for OutputType=StreamList in the producer

[CAMEL-9823](https://issues.apache.org/jira/browse/CAMEL-9823)

Exploring Consumer groups feature in Camel-kafka consumer side

[CAMEL-9759](https://issues.apache.org/jira/browse/CAMEL-9759)

camel-zipkin - Instrument Camel

[CAMEL-9744](https://issues.apache.org/jira/browse/CAMEL-9744)

camel-bindy - Add support for Java 8 date and time API

[CAMEL-9737](https://issues.apache.org/jira/browse/CAMEL-9737)

Create camel component for ServiceNow

[CAMEL-9729](https://issues.apache.org/jira/browse/CAMEL-9729)

Camel catalog - Allow to query older versions

[CAMEL-9727](https://issues.apache.org/jira/browse/CAMEL-9727)

New camel-cm component

[CAMEL-9716](https://issues.apache.org/jira/browse/CAMEL-9716)

Camel KafkaConsumer should be able to re-consume the Kafka stream.

[CAMEL-9650](https://issues.apache.org/jira/browse/CAMEL-9650)

<contextScan/> equivalent in Spring JavaConfig

[CAMEL-9647](https://issues.apache.org/jira/browse/CAMEL-9647)

Camel Circuit Breaker to output Hystrix metrics?

[CAMEL-9638](https://issues.apache.org/jira/browse/CAMEL-9638)

JSSE Security - Add support for new Java 8 stuff like SNIHostName

[CAMEL-9602](https://issues.apache.org/jira/browse/CAMEL-9602)

ProducerTemplateBuilder

[CAMEL-9541](https://issues.apache.org/jira/browse/CAMEL-9541)

Component docs - Maintain docs as part of the source code

[CAMEL-9419](https://issues.apache.org/jira/browse/CAMEL-9419)

camel-spring-boot - Add component options as type-safe configuration properties

[CAMEL-9098](https://issues.apache.org/jira/browse/CAMEL-9098)

Camel Hystrix component

[CAMEL-9018](https://issues.apache.org/jira/browse/CAMEL-9018)

camel-archetype-java8

[CAMEL-8723](https://issues.apache.org/jira/browse/CAMEL-8723)

Add desired message type to ProducerTemplate.sendBody methods

[CAMEL-7832](https://issues.apache.org/jira/browse/CAMEL-7832)

create a java 8 demo of RX to show typesafe filtering and transforming of messages

[CAMEL-7831](https://issues.apache.org/jira/browse/CAMEL-7831)

create a java8 only demo showing how to use lambda expressions for Predicate / Expression inside the Java DSL (using Message as a typesafe parameter)

[CAMEL-7536](https://issues.apache.org/jira/browse/CAMEL-7536)

camel mail: content-transfer-encoding configurable

[CAMEL-6399](https://issues.apache.org/jira/browse/CAMEL-6399)

hazelcast - route policy for having one route being master, and others as slaves

[CAMEL-6163](https://issues.apache.org/jira/browse/CAMEL-6163)

camel-bindy - Enable add custom data type converter.

[CAMEL-3142](https://issues.apache.org/jira/browse/CAMEL-3142)

JpaPollingConsumer - So you can more easily work with pollEnrich

### Sub-task (12)

[CAMEL-10170](https://issues.apache.org/jira/browse/CAMEL-10170)

Add support for Chronicle-Engine

[CAMEL-10107](https://issues.apache.org/jira/browse/CAMEL-10107)

\[api-component-framework\] Make ApiMethodImpl's arguments type safe

[CAMEL-10106](https://issues.apache.org/jira/browse/CAMEL-10106)

\[api-component-framework\] Reduce object allocation in ApiMethodHelper, ApiMethodImpl

[CAMEL-10105](https://issues.apache.org/jira/browse/CAMEL-10105)

\[api-component-framework\] Reduce object allocation in ApiCollection

[CAMEL-10102](https://issues.apache.org/jira/browse/CAMEL-10102)

\[api-component-framework\] api method resolution should not allocate temporary arrays

[CAMEL-10101](https://issues.apache.org/jira/browse/CAMEL-10101)

\[api-component-framework\] splitResult should not convert collections to array

[CAMEL-9987](https://issues.apache.org/jira/browse/CAMEL-9987)

Add Asciidoc documentation

[CAMEL-9985](https://issues.apache.org/jira/browse/CAMEL-9985)

Add Confluence documentation

[CAMEL-9961](https://issues.apache.org/jira/browse/CAMEL-9961)

Add camel-ehcache documentation

[CAMEL-9959](https://issues.apache.org/jira/browse/CAMEL-9959)

Create an ehcache based aggregation repository

[CAMEL-9958](https://issues.apache.org/jira/browse/CAMEL-9958)

Create an ehcache based idempotent repository

[CAMEL-9746](https://issues.apache.org/jira/browse/CAMEL-9746)

Write documentation for camel-servicenow

### Task (54)

[CAMEL-10361](https://issues.apache.org/jira/browse/CAMEL-10361)

Expose cassandra-unit version through BOM

[CAMEL-10346](https://issues.apache.org/jira/browse/CAMEL-10346)

Upgrade servicemix bundles from 2016.09

[CAMEL-10332](https://issues.apache.org/jira/browse/CAMEL-10332)

Define netty version in dependency management

[CAMEL-10318](https://issues.apache.org/jira/browse/CAMEL-10318)

Upgrade OpenWebBeans to version 1.7.0

[CAMEL-10316](https://issues.apache.org/jira/browse/CAMEL-10316)

Upgrade Weld to version 2.4.0.Final

[CAMEL-10311](https://issues.apache.org/jira/browse/CAMEL-10311)

Comprehensively define lucene artefacts used by elasticsearch

[CAMEL-10306](https://issues.apache.org/jira/browse/CAMEL-10306)

Upgrade from 3.6.5 to 3.7.1

[CAMEL-10294](https://issues.apache.org/jira/browse/CAMEL-10294)

Component docs - ExchangePattern

[CAMEL-10274](https://issues.apache.org/jira/browse/CAMEL-10274)

examples using mvn:jetty-run do not work after log4j2 upgrade

[CAMEL-10264](https://issues.apache.org/jira/browse/CAMEL-10264)

Minor version releases should carry .0 micro version

[CAMEL-10263](https://issues.apache.org/jira/browse/CAMEL-10263)

Several log refactoring/improvement suggestions

[CAMEL-10261](https://issues.apache.org/jira/browse/CAMEL-10261)

Mark camel-cache as deprecated

[CAMEL-10252](https://issues.apache.org/jira/browse/CAMEL-10252)

Upgrade Weld embedded Arquillian adapter to version 2.0.0.Beta3

[CAMEL-10250](https://issues.apache.org/jira/browse/CAMEL-10250)

spring boot - SpringBootStarterMojo should not use internal API

[CAMEL-10227](https://issues.apache.org/jira/browse/CAMEL-10227)

upgrade camel-flink

[CAMEL-10224](https://issues.apache.org/jira/browse/CAMEL-10224)

Upgrade log4j to lg4j2

[CAMEL-10214](https://issues.apache.org/jira/browse/CAMEL-10214)

File Component: doneFileName option of Consumer missing from generated documentation

[CAMEL-10202](https://issues.apache.org/jira/browse/CAMEL-10202)

camel-netty4-http - Spring Boot auto configuration

[CAMEL-10163](https://issues.apache.org/jira/browse/CAMEL-10163)

camel-twitter - Component docs - Some options are labelled wrong

[CAMEL-10137](https://issues.apache.org/jira/browse/CAMEL-10137)

Add a Camel-Kubernetes example

[CAMEL-10130](https://issues.apache.org/jira/browse/CAMEL-10130)

Removed deprecated vtdxml language

[CAMEL-10089](https://issues.apache.org/jira/browse/CAMEL-10089)

Extend jline package import range in Camel commands

[CAMEL-10079](https://issues.apache.org/jira/browse/CAMEL-10079)

Upgrade quickfixj to v1.6.2

[CAMEL-10077](https://issues.apache.org/jira/browse/CAMEL-10077)

Error formatting macro: snippet: java.lang.IndexOutOfBoundsException: Index: 20, Size: 20

[CAMEL-10075](https://issues.apache.org/jira/browse/CAMEL-10075)

using-propertyplaceholder - rror formatting macro: snippet: java.lang.IndexOutOfBoundsException

[CAMEL-10067](https://issues.apache.org/jira/browse/CAMEL-10067)

Add Camel-Johnzon documentation

[CAMEL-10037](https://issues.apache.org/jira/browse/CAMEL-10037)

ServiceCall EIP - Add missing documentation

[CAMEL-10035](https://issues.apache.org/jira/browse/CAMEL-10035)

Upgrade braintree sdk to v2.63.0

[CAMEL-9992](https://issues.apache.org/jira/browse/CAMEL-9992)

Push project into Camel

[CAMEL-9983](https://issues.apache.org/jira/browse/CAMEL-9983)

camel-hystrix - Lets removed the component now that we have the EIP

[CAMEL-9976](https://issues.apache.org/jira/browse/CAMEL-9976)

camel:rest-show command requires only context name as argument and not route Id

[CAMEL-9936](https://issues.apache.org/jira/browse/CAMEL-9936)

Camel-parent 17.0 uses incompatible logback-classic and slf4j-api

[CAMEL-9930](https://issues.apache.org/jira/browse/CAMEL-9930)

camel timer docs - add supported formats

[CAMEL-9913](https://issues.apache.org/jira/browse/CAMEL-9913)

Upgrading Beanshell for CVE-2016-2510

[CAMEL-9902](https://issues.apache.org/jira/browse/CAMEL-9902)

Remove ServiceMix scripting-api from Karaf features

[CAMEL-9837](https://issues.apache.org/jira/browse/CAMEL-9837)

Camel mail component documentation has BCC and CC options as upper-cased

[CAMEL-9825](https://issues.apache.org/jira/browse/CAMEL-9825)

Exclude CDI generated proxies from context tracker

[CAMEL-9806](https://issues.apache.org/jira/browse/CAMEL-9806)

Add camel-IronMQ Karaf feature

[CAMEL-9787](https://issues.apache.org/jira/browse/CAMEL-9787)

Migrate Maven Archetypes to new build system

[CAMEL-9785](https://issues.apache.org/jira/browse/CAMEL-9785)

camel-zipkin - If doing multiple client requests then assign new span id

[CAMEL-9781](https://issues.apache.org/jira/browse/CAMEL-9781)

Installing camel in Karaf 3.0.x

[CAMEL-9778](https://issues.apache.org/jira/browse/CAMEL-9778)

Remove deprecated camel-gae

[CAMEL-9764](https://issues.apache.org/jira/browse/CAMEL-9764)

Maven build: fix to support lambdas in code (JDK8)

[CAMEL-9760](https://issues.apache.org/jira/browse/CAMEL-9760)

Google drive component syntax inconsistency

[CAMEL-9758](https://issues.apache.org/jira/browse/CAMEL-9758)

Remove releasing xxxComponent.properties et all

[CAMEL-9757](https://issues.apache.org/jira/browse/CAMEL-9757)

camel-gae - Deprecate

[CAMEL-9750](https://issues.apache.org/jira/browse/CAMEL-9750)

Tests should not log on stdout by default

[CAMEL-9747](https://issues.apache.org/jira/browse/CAMEL-9747)

Java 8 upgrade - Set source and target to java 1.8

[CAMEL-9646](https://issues.apache.org/jira/browse/CAMEL-9646)

Upgrade Xalan bundle to 2.7.2\_3

[CAMEL-9571](https://issues.apache.org/jira/browse/CAMEL-9571)

Upgrade tests/camel-itest-osgi to use Karaf 4.0.x

[CAMEL-9397](https://issues.apache.org/jira/browse/CAMEL-9397)

remove camel-test-spring32

[CAMEL-8637](https://issues.apache.org/jira/browse/CAMEL-8637)

Upgrade Jetty version to 9.x in Camel-CometD

[CAMEL-8602](https://issues.apache.org/jira/browse/CAMEL-8602)

Java 8: ConcurrentLinkedHashMap -> Caffeine

[CAMEL-7698](https://issues.apache.org/jira/browse/CAMEL-7698)

camel-spring - Remove the old osgi namespace handler

### Test (9)

[CAMEL-10362](https://issues.apache.org/jira/browse/CAMEL-10362)

itest-spring-boot - Nagios and Jira fails locally

[CAMEL-10257](https://issues.apache.org/jira/browse/CAMEL-10257)

camel-cache - Test failures

[CAMEL-10207](https://issues.apache.org/jira/browse/CAMEL-10207)

spring boot - Integration test failures

[CAMEL-10204](https://issues.apache.org/jira/browse/CAMEL-10204)

Use narayana as TX manager for testing

[CAMEL-10198](https://issues.apache.org/jira/browse/CAMEL-10198)

JGroupsClusterTest and JGroupsComponentTest fail on some platforms

[CAMEL-10118](https://issues.apache.org/jira/browse/CAMEL-10118)

Spring-boot compatibility test results

[CAMEL-10047](https://issues.apache.org/jira/browse/CAMEL-10047)

camel-mqtt - Should use dynamic port during testing

[CAMEL-9827](https://issues.apache.org/jira/browse/CAMEL-9827)

MongoDB - The unit tests have some issues

[CAMEL-9797](https://issues.apache.org/jira/browse/CAMEL-9797)

camel-elastichsearch - Tests fails since recent upgrade

### Wish (4)

[CAMEL-10283](https://issues.apache.org/jira/browse/CAMEL-10283)

Add a timeout on WebSocketProducer sendMessages method

[CAMEL-9836](https://issues.apache.org/jira/browse/CAMEL-9836)

Add file id of the gridfs file created in the header of the exchange

[CAMEL-9835](https://issues.apache.org/jira/browse/CAMEL-9835)

Enable kafka consumer to subcribe to multiple topics

[CAMEL-9733](https://issues.apache.org/jira/browse/CAMEL-9733)

enable dynamic job name in component spring-batch

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).