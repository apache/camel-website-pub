# Apache camel 2.19.0 Release

## New and Noteworthy

Welcome to the 2.19.0 release which resolved over 670 issues including new features, improvements and bug fixes.

-   Introduced Camel Connector’s which is a simplified version of a Camel component that has been pre-configured for a specific use-case.
-   Upgraded to Spring Boot 1.5.x.
-   The Camel Maven Plugin now provides the `camel:validate` goal to parse your Java and XML source code for any Camel routes and report invalid Camel endpoint uri and simple expression errors. You can run this at code time (not runtime). 
-   Camel `Main` and Spring Boot and Camel Maven Plugin can now auto terminate the JVM after Camel has been running for maximum duration of seconds, processed messages or been idle for a period.
-   Camel source code can build with Java 9 in preparation for official support for Java 9 in a future release
-   All the Camel Spring Boot starter components now has more of the components default values included in their metadata which allows tooling to display such information
-   Deprecated more components and camel-core APIs that will be dropped in Camel 3.0 or sometime in the future
-   Introduced `ReloadStrategy` as SPI which allows custom providers to implement logic for triggering live reloads of Camel routes.
-   The Camel Maven Plugin now allows to live reload route changes from XML files when running Camel. This can also be enabled from the `Main` class.
-   Introduced a new `camel-catalog-rest` artifact which is a tiny standalone REST API of the CamelCatalog using JAX-RS and Swagger Annotations.
-   Added `camel-catalog-rest-app` as a standalone application which used Apache CXF with Jetty to host the Catalog REST API with embedded Swagger UI
-   Returning `null` from Bean should work similar to how `setBody` and `transform` works when they set a `null` body.
-   The Camel Spring Boot starter components now have their auto configuration depends on `org.apache.camel.springboot.CamelAutoConfiguration` which makes it easier writing unit tests where you can exclude `org.apache.camel.springboot.CamelAutoConfiguration` to turn off Camel Spring Boot auto configuration completely.
-   Camel now supports OWASP dependency check maven plugin
-   NATS component now supports TLS and explicit flushing (with timeout) of the connection
-   Metrics component now supports Gauge type
-   File consumer now supports idempotent-changed and idempotent-rename read lock strategies for clustering. 
-   Camel Catalog now supports custom runtime providers that only includes the supported Camel components, languages and data formats running in that container. For example for Karaf or Spring Boot in the camel-catalog-provider-karaf and camel-catalog-provider-springboot.
-   The bean component will when calling a method that returned an instance of `Callable` now call that callable to obtain the chained result. This allows to call Groovy functions/closures etc.
-   Failover Load Balancer with inheritErrorHandler=false, now allows Error Handler to react after the load balancer is exhausted.
-   Salesforce component now supports limits, recent items, approvals and composite API
-   Dumping Camel routes as XML now includes custom namespaces which are at xpath expressions etc. Likewise updating Camel routes from XML can now include namespaces which will be associated on xpath expressions.
-   Added `RouteIdFactory` which can auto assign route ids based on the consumer endpoints to use more sensitible names, instead of route1, route2, etc.
-   Add `skip` function to Simple language
-   Upgraded to Jetty 9.3 (Jetty 9.2 still supported for Karaf 4.0.x users)
-   `RouteBuilder` auto-configuration can now be disabled from Camel CDI configuration
-   Camel contexts automatic start can now be disabled from Camel CDI configuration
-   Camel CDI now provides support for `TransactionErrorHandler` and `TransactionPolicy` via JTA
-   Asynchronous support for CXF JAX-RS producers has been added
-   The JSonPath language now supports Map and List types and POJOs as well. For POJOs you need to have Jackson on the classpath. 
-   Data Format which marshal to JSon or XML now set the content-type header to application/json or application/xml appropriately.
-   The Kafka component can now store offset state offline (stateRepository) to preserve this information and be able to resume from previous offset.
-   The Kafka component has been improved to be easier to configure and use. Notice there is a backwards incompatible change so users need to migrate.
-   A topic based idempotent repository that is Kafka based for the Idempotent Consumer EIP
-   The Kafka component will automatic type convert the message body to the type specified by the configured serializer (is string by default) when sending to kafka. You can also now configure key and partitionKey in the endpoint uri, instead of having to specify as headers.
-   The Kafka consumer will now auto commit on stop to ensure the broker has the latest offset commit. The option `autoCommitOnStop` can be configured to be sync,async or none.
-   Added easy predicate parser to JSonPath to more easily define simple predicates without using the more complex jsonpath notation with all the symbols
-   The Box component has been migrated to use the Box v2 Java API as the old v1 API is going to be shutdown from summer 2017
-   Examples overview now generate from the source code to ensure its up to date
-   Added declarative Transformer and Validator which performs transformation/validation according to the data type information declared on a route by inputType and/or outputType. There’re a few examples demonstrates this feature: camel-example-transformer-blueprint, camel-example-transformer-cdi, camel-example-transformer-demo, and camel-example-validator-spring-boot
-   Added query support for JPA Producer

The following issues have been fixed

-   Fixed starting Camel on Oracle JDK 1.8.0\_19 or lower, which would throw an UnsupportedOperationException
-   Fixed running `mvn camel:run` when using OSGi Blueprint
-   Fixed Hystrix EIP to also execute fallback if execution was rejected or short-circuited or other reasons from Hystrix. 
-   Fixed Hystrix EIP race condition when timeout was hit and fallback is executed could let to Camel Exchange having wrong caused exception.
-   Fixed adding new routes to running CamelContext and if the new routes would fail to startup, then before these routes would “hang around”. Now only succesful started routes are added.
-   Adding or removing routes that starts from Undertow no longer restart the entire HTTP server
-   VM endpoint should prepare exchange with the CamelContext from the consumer and not from cached endpoint which can be different
-   Fixed a bug when using Rest DSL with SERVLET could cause a java.io.IOException: Stream closed exception when using Bean component in the route. 
-   Fixed an issue when using `pipeline` in Java DSL not setting up the EIP correctly which could lead to runtime route not as intended.
-   Fixed Dropbox to use Stream caching to avoid reading entire file into memory so Camel can process big files
-   Fixed `toD` issue with splitting uris when RAW values had + sign
-   Fixed adviceWith may behave differently when using multiple advices in the same order and you would advice on the same nodes.
-   Fixed camel-zipkin to be able to startup and work with Camel XML 
-   Fixed FTP2 readLock=changed not working (when fastFileExists=false) if no sub folder was specified as starting directory.
-   Fixed Simple language when using indexing with a nested function
-   Fixed issue with `@Consume` not having `CamelContext` injected and its lifecycle managed by `CamelContext`
-   Fixed Netty double buffer release leak in Netty4 and Netty4 HTTP

API breaking

-   The groovy DSL from camel-groovy has been moved into its own camel-groovy-dsl module. The camel-groovy now only contains the Camel Language
-   Camel-spring-LDAP now uses `java.util.function.BiFunction<L, Q, S>` instead of `org.apache.camel.component.springldap.LdapOperationsFunction<Q, S>`
-   The deprecated APIs from camel-spring-boot has been removed as part of upgrading and supporting Spring Boot 1.5.x
-   The `getComponentDocumentation` method on `CamelContext` is deprecated and returns null. The embedded HTML documentation in all the Camel components has been removed as they are not in use/maintained, and the JSon schema is the actual information. Use the camel-catalog for component documentation where you can get all the documentation in both ascii doc and html format.
-   camel-mongodb-gridf schema has been renamed from _gridfs_ to _mongodb-gridfs_ to avoid confusion.
-   The commands-core has the Catalog commands removed
-   The org.apache.camel.spring.boot.FatJarRouter has been removed, just use regular `RouteBuilder` classes in Spring Boot applications.
-   The Kafka endpoint option `seekToBeginning=true` should be migrated to `seekTo=beginning`
-   The Kafka endpoint option bridgeEndpoint has moved from endpoint to the KafkaConfiguration class so all options are together.
-   The Kafka component has been improved to be easier to configure and use. Notice there is a backwards incompatible change so users need to migrate. The kafka uri is changed from kafka:brokers to kafka:topic. So you need to specify the topic name in the context-path and the brokers as parameters, eg before `kafka:myserver?topic=sometopic` is now `kafka:sometopic?brokers=myserver`
-   The Infinispan uri syntax has changed from infinispan:hostName?options to infinispan:cacheName?options

Important changes to consider when upgrading

-   camel-spring-dm has been disabled from the karaf features file so users cannot install it out of the box as it does not work properly. camel-spring-dm has been deprecated for a long time and users are encouraged to use osgi blueprint instead. The JAR is still shipped and can be installed manually but then you are on your own. The JAR will be removed completed in a future release.
-   Groovy DSL and Scala DSL is deprecated and planned to be moved to Camel Extra and not distributed out of the box in the future.
-   Camel now uses Karaf 4.x API and therefore not possible to run on older Karaf versions.
-   `camel-blueprint` changed startup behavior to start on Blueprint.CREATED event which would be more `correct` way of startup instead of Blueprint.REGISTERED as before.
-   camel-spring-boot now don’t include prototype scoped beans when auto scanning for RouteBuilder instances, which is how camel-spring works. You can turn this back using the includeNonSingletons option.
-   camel-spring-javaconfig removed from Karaf features as it was not really supported in OSGi/Karaf.
-   camel spring-boot shell commands have been removed as spring-boot shell has been deprecated in spring-boot.
-   camel-mongodb-gridf schema has been renamed from gridfs to mongodb-gridfs to avoid confusion.
-   camel-box has been migrated to use box v2 api so there may be some migration needed as the old camel-box component was using box v1 api
-   The JSon schema from camel-catalog have changed to use boolean, integer and numeric values when applicable instead of using string values for everything. 
-   The camel-catalog Karaf commands has been removed

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
      <version>2.19.0</version>
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
      <version>2.19.0</version>
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
| [apache-camel-2.19.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.19.0/apache-camel-2.19.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.19.0/apache-camel-2.19.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.19.0/apache-camel-2.19.0-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.19.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.19.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (196)

[CAMEL-11213](https://issues.apache.org/jira/browse/CAMEL-11213)

camel-grpc doesn't terminate channel when producer stops

[CAMEL-11212](https://issues.apache.org/jira/browse/CAMEL-11212)

Don't allow Salesforce HTTP client to stop with outstanding requests

[CAMEL-11210](https://issues.apache.org/jira/browse/CAMEL-11210)

Don't return null for getErrors in SalesforceException

[CAMEL-11201](https://issues.apache.org/jira/browse/CAMEL-11201)

camel-reactive-streams - Cannot create service in spring-boot

[CAMEL-11198](https://issues.apache.org/jira/browse/CAMEL-11198)

OpenTracing trace context should cope with Hystrix using separate thread

[CAMEL-11197](https://issues.apache.org/jira/browse/CAMEL-11197)

camel-jpa consumer fails to poll after database connection is lost

[CAMEL-11177](https://issues.apache.org/jira/browse/CAMEL-11177)

CoAP component starts redundant server instance

[CAMEL-11173](https://issues.apache.org/jira/browse/CAMEL-11173)

Integration tests for camel-restdsl-swagger-plugin fail on JDK 9

[CAMEL-11171](https://issues.apache.org/jira/browse/CAMEL-11171)

camel-zookeeper-master - RAW() and child endpoint issue

[CAMEL-11139](https://issues.apache.org/jira/browse/CAMEL-11139)

ClassNotFoundException may silently be ignored in InProducer

[CAMEL-11138](https://issues.apache.org/jira/browse/CAMEL-11138)

ConsumerTemplate - If cache is full then polling consumer should be stopped to not leak resources

[CAMEL-11134](https://issues.apache.org/jira/browse/CAMEL-11134)

camel-http4 - Unable to configure https4 properties in spring-boot

[CAMEL-11131](https://issues.apache.org/jira/browse/CAMEL-11131)

Timer consumer - Should call start/stop of the processor

[CAMEL-11117](https://issues.apache.org/jira/browse/CAMEL-11117)

The searchTerm subjectOrBody breaks the searchTerm unseen

[CAMEL-11113](https://issues.apache.org/jira/browse/CAMEL-11113)

Camel catalog's asEndpointUri mangles endpoint URIs for unequal number of tokens

[CAMEL-11111](https://issues.apache.org/jira/browse/CAMEL-11111)

Camel-Undertow: throwExceptionOnFailure doesn't work as expected

[CAMEL-11110](https://issues.apache.org/jira/browse/CAMEL-11110)

REST component host parameter handling

[CAMEL-11099](https://issues.apache.org/jira/browse/CAMEL-11099)

Unhandled ClassCastException if fault detail is not JaxbElement

[CAMEL-11098](https://issues.apache.org/jira/browse/CAMEL-11098)

FacebookEndpointConfiguration bean not taken into account as a UriParam

[CAMEL-11093](https://issues.apache.org/jira/browse/CAMEL-11093)

NPE when defaultValueProvider not given

[CAMEL-11091](https://issues.apache.org/jira/browse/CAMEL-11091)

REST Swagger handling of empty specificationUri

[CAMEL-11080](https://issues.apache.org/jira/browse/CAMEL-11080)

OnExceptionDefinition validation ignores redeliveryPolicy field

[CAMEL-11074](https://issues.apache.org/jira/browse/CAMEL-11074)

Unable to load Schematron XSLT templates on windows

[CAMEL-11065](https://issues.apache.org/jira/browse/CAMEL-11065)

Cannot parse CSV record starting with separator character

[CAMEL-11063](https://issues.apache.org/jira/browse/CAMEL-11063)

PGP Decryptor does not make Integrity check

[CAMEL-11057](https://issues.apache.org/jira/browse/CAMEL-11057)

Undertow Producer : NPE if tryConvertTo fails to convert exchange body to ByteBuffer

[CAMEL-11052](https://issues.apache.org/jira/browse/CAMEL-11052)

Soap11DataFormatAdapter throwing exception when using JAXB/JAX-WS generated code

[CAMEL-11048](https://issues.apache.org/jira/browse/CAMEL-11048)

Jetty Producer always uses "Transfer-Encoding: chunked" header

[CAMEL-11047](https://issues.apache.org/jira/browse/CAMEL-11047)

STARTTLS broken with camel-mail

[CAMEL-11040](https://issues.apache.org/jira/browse/CAMEL-11040)

Authentication : provide a way to use refresh\_token mode in addition to password method

[CAMEL-11031](https://issues.apache.org/jira/browse/CAMEL-11031)

Use default ("") exchange for reply-to messages

[CAMEL-11028](https://issues.apache.org/jira/browse/CAMEL-11028)

camel-spark-rest - Adds duplicate content-type

[CAMEL-11026](https://issues.apache.org/jira/browse/CAMEL-11026)

RestletProducer should allow multiple values in HTTP Accept header

[CAMEL-11020](https://issues.apache.org/jira/browse/CAMEL-11020)

Camel Kubernetes consumers do not close watchers

[CAMEL-11015](https://issues.apache.org/jira/browse/CAMEL-11015)

Encoding issues in camel-salesforce-maven-plugin

[CAMEL-11012](https://issues.apache.org/jira/browse/CAMEL-11012)

bindy csv doesn't populate with defaultValue on marshal

[CAMEL-11009](https://issues.apache.org/jira/browse/CAMEL-11009)

Camel spring - spring.schemas file contains unexpaned maven properties in release artefact

[CAMEL-11008](https://issues.apache.org/jira/browse/CAMEL-11008)

Consumer/Producer templates are not stopped when auto-configured in Spring Boot

[CAMEL-11007](https://issues.apache.org/jira/browse/CAMEL-11007)

camel-spring-boot - Default values which was negative may have become positive

[CAMEL-11002](https://issues.apache.org/jira/browse/CAMEL-11002)

Camel-Blueprint - failed container fails to remove JMX object

[CAMEL-11000](https://issues.apache.org/jira/browse/CAMEL-11000)

Property 'accessExternalDTD' is not recognized by (all) Xerces

[CAMEL-10987](https://issues.apache.org/jira/browse/CAMEL-10987)

camel-test-karaf - Change breaks other tests

[CAMEL-10985](https://issues.apache.org/jira/browse/CAMEL-10985)

camel-coap fails to return results when enableCORS(true) is set

[CAMEL-10980](https://issues.apache.org/jira/browse/CAMEL-10980)

error with enableCORS(true) with camel-undertow

[CAMEL-10966](https://issues.apache.org/jira/browse/CAMEL-10966)

Salesforce Maven Plugin doesn't escape strings when doing the camel-salesforce:generate phase.

[CAMEL-10964](https://issues.apache.org/jira/browse/CAMEL-10964)

CXF http-jetty transport reverse proxy configuration will not work when using @BeanInject in RouteBuilder bean

[CAMEL-10963](https://issues.apache.org/jira/browse/CAMEL-10963)

KinesisFirehoseProducer sets the deliverStreamName using getEndpointKey() instead of getStreamName()

[CAMEL-10961](https://issues.apache.org/jira/browse/CAMEL-10961)

ZookeeperRoutingPolicy - Error setting up election node

[CAMEL-10954](https://issues.apache.org/jira/browse/CAMEL-10954)

Can't find dependency org.apache.camel:camel-box2

[CAMEL-10949](https://issues.apache.org/jira/browse/CAMEL-10949)

Websocket clients get message from all resources on one port

[CAMEL-10948](https://issues.apache.org/jira/browse/CAMEL-10948)

Camel-hdfs2: initialDelay option is overwritten with default value

[CAMEL-10936](https://issues.apache.org/jira/browse/CAMEL-10936)

Salesforce Login exception: the error code is not reported properly

[CAMEL-10931](https://issues.apache.org/jira/browse/CAMEL-10931)

Missing REST outTypeList attribute in Spring XML

[CAMEL-10929](https://issues.apache.org/jira/browse/CAMEL-10929)

Undertow producer wrongly configures HTTP request path

[CAMEL-10928](https://issues.apache.org/jira/browse/CAMEL-10928)

Restlet contract for RestProducerFactory wrongly configures request method

[CAMEL-10914](https://issues.apache.org/jira/browse/CAMEL-10914)

CxfConsumer doesn't clean up the CXF endpoint MBean upon stop

[CAMEL-10913](https://issues.apache.org/jira/browse/CAMEL-10913)

CORS header Access-Control-Allow-Credentials not managed correctly

[CAMEL-10912](https://issues.apache.org/jira/browse/CAMEL-10912)

camel-sjms - Session object created from connection that gets closed

[CAMEL-10906](https://issues.apache.org/jira/browse/CAMEL-10906)

http components: not all the options supported by component/endpoints are shown in the documentation

[CAMEL-10893](https://issues.apache.org/jira/browse/CAMEL-10893)

PDU is lost when SnmpMessage is copied

[CAMEL-10888](https://issues.apache.org/jira/browse/CAMEL-10888)

camel-spring-ws - Has problem with returning proper response due invalid IN vs OUT code

[CAMEL-10874](https://issues.apache.org/jira/browse/CAMEL-10874)

JettyHttpComponent sets selector threads to 0 when running on 1 CPU

[CAMEL-10873](https://issues.apache.org/jira/browse/CAMEL-10873)

camel-sjms transacted routes dead-lock when exceptions are thrown by asynchronous processors

[CAMEL-10856](https://issues.apache.org/jira/browse/CAMEL-10856)

ZipkinTracer does not trigger doStart() when used in XML DSL

[CAMEL-10855](https://issues.apache.org/jira/browse/CAMEL-10855)

Camel adviceWith behaves differently when changing the order of weave statements

[CAMEL-10849](https://issues.apache.org/jira/browse/CAMEL-10849)

Salesforce: subscription channel created per component

[CAMEL-10841](https://issues.apache.org/jira/browse/CAMEL-10841)

Move operation will create a warning log message

[CAMEL-10830](https://issues.apache.org/jira/browse/CAMEL-10830)

Race condition when reading principal for one-way web services

[CAMEL-10822](https://issues.apache.org/jira/browse/CAMEL-10822)

Camel Jasypt component throws NPE

[CAMEL-10820](https://issues.apache.org/jira/browse/CAMEL-10820)

DefaultFluentProducerTemplate mixes up data when sending asynchronously

[CAMEL-10817](https://issues.apache.org/jira/browse/CAMEL-10817)

dumpModelAsXml can return invalid XML namespace xmlns:xmlns

[CAMEL-10802](https://issues.apache.org/jira/browse/CAMEL-10802)

java.lang.ClassCastException when using FlexibleAggregationStrategy with Spring Boot

[CAMEL-10788](https://issues.apache.org/jira/browse/CAMEL-10788)

Multiple handlers with multiple endpoints on same port causes a handler loop

[CAMEL-10783](https://issues.apache.org/jira/browse/CAMEL-10783)

XSLT transform cannot use default DTM

[CAMEL-10782](https://issues.apache.org/jira/browse/CAMEL-10782)

SFTP: cannot get files from users home with readlock changed

[CAMEL-10771](https://issues.apache.org/jira/browse/CAMEL-10771)

CxfEndpoint shows WARNING altough endpoint-/port name is configured

[CAMEL-10767](https://issues.apache.org/jira/browse/CAMEL-10767)

Versions of swagger-models and swagger-parser in conflict

[CAMEL-10756](https://issues.apache.org/jira/browse/CAMEL-10756)

Mina2 Producer "hang" until timeout if the response message could not be decoded

[CAMEL-10747](https://issues.apache.org/jira/browse/CAMEL-10747)

CamelContext is not been set in VMConsumer when used with POJO @Consume

[CAMEL-10741](https://issues.apache.org/jira/browse/CAMEL-10741)

LogEndpoint error constructing LogProducer

[CAMEL-10738](https://issues.apache.org/jira/browse/CAMEL-10738)

direct-vm component behavior broken in 2.18.1 vs 2.17.4

[CAMEL-10736](https://issues.apache.org/jira/browse/CAMEL-10736)

Box component configuration problem

[CAMEL-10732](https://issues.apache.org/jira/browse/CAMEL-10732)

Remove from all caches when Groovy script is removed from Camel script cache

[CAMEL-10727](https://issues.apache.org/jira/browse/CAMEL-10727)

camel-ftp: knownHostsUri configuration with camel 2.18.1

[CAMEL-10717](https://issues.apache.org/jira/browse/CAMEL-10717)

Fix relativePath in camel/platforms/spring-boot/components-starter/pom.xml

[CAMEL-10716](https://issues.apache.org/jira/browse/CAMEL-10716)

Salesforce Composite API wrongly checks for minimum supported version

[CAMEL-10713](https://issues.apache.org/jira/browse/CAMEL-10713)

SCP not handling errors for failed transfers correctly

[CAMEL-10712](https://issues.apache.org/jira/browse/CAMEL-10712)

Camel-SFTP endpoints will silently not delete file on disconnect

[CAMEL-10709](https://issues.apache.org/jira/browse/CAMEL-10709)

camel-etcd: etcd stats endpoint fails because of a class cast exception

[CAMEL-10708](https://issues.apache.org/jira/browse/CAMEL-10708)

org.apache.camel.component.cxf.CxfEndpoint -- Lines 554 -558 should be Nullsafe

[CAMEL-10707](https://issues.apache.org/jira/browse/CAMEL-10707)

Throttling policy is broken because service suspension/resume is not symmetric

[CAMEL-10704](https://issues.apache.org/jira/browse/CAMEL-10704)

XSLT will fail if the XML document contains a default namespace

[CAMEL-10701](https://issues.apache.org/jira/browse/CAMEL-10701)

Classloader issue prevents from loading kafka authentication in OSGi environments

[CAMEL-10695](https://issues.apache.org/jira/browse/CAMEL-10695)

camel-mqtt: TimeoutException thrown on MQTTEndpoint stop

[CAMEL-10692](https://issues.apache.org/jira/browse/CAMEL-10692)

OptaPlanner cannot load config from deployment

[CAMEL-10689](https://issues.apache.org/jira/browse/CAMEL-10689)

NoFactoryAvailableException when invoking component-list ssh command

[CAMEL-10688](https://issues.apache.org/jira/browse/CAMEL-10688)

Camel-influxdb - The component should not store state

[CAMEL-10681](https://issues.apache.org/jira/browse/CAMEL-10681)

camel-ehcache - configUri does not work appropriately

[CAMEL-10677](https://issues.apache.org/jira/browse/CAMEL-10677)

SJMSBatchConsumer does not respect the consumerCount parameter

[CAMEL-10675](https://issues.apache.org/jira/browse/CAMEL-10675)

Swagger is not generating schema ref for body parameter

[CAMEL-10672](https://issues.apache.org/jira/browse/CAMEL-10672)

Test failing in camel-itest-osgi

[CAMEL-10664](https://issues.apache.org/jira/browse/CAMEL-10664)

SimpleIllegalSyntaxException in nested expression

[CAMEL-10663](https://issues.apache.org/jira/browse/CAMEL-10663)

Basic authentication information not sent on versions post 2.14.1

[CAMEL-10653](https://issues.apache.org/jira/browse/CAMEL-10653)

XQuery support broken in Camel 2.18.x

[CAMEL-10645](https://issues.apache.org/jira/browse/CAMEL-10645)

Camel-MongoDB3: component should not store state

[CAMEL-10644](https://issues.apache.org/jira/browse/CAMEL-10644)

Camel-MongoDB: component should not store state

[CAMEL-10640](https://issues.apache.org/jira/browse/CAMEL-10640)

Custom AsyncHttpClientConfig not used in WsEndpoint

[CAMEL-10635](https://issues.apache.org/jira/browse/CAMEL-10635)

camel-mongodb-gridfs - The component should not store state

[CAMEL-10616](https://issues.apache.org/jira/browse/CAMEL-10616)

shutdown timeout override not working in unit tests

[CAMEL-10603](https://issues.apache.org/jira/browse/CAMEL-10603)

Realm parameter cause Exception

[CAMEL-10602](https://issues.apache.org/jira/browse/CAMEL-10602)

camel:run with simple blueprint project failed "waiting for BlueprintContainer" although the route is active

[CAMEL-10597](https://issues.apache.org/jira/browse/CAMEL-10597)

Swagger prints child object types as string parameters rather than refs

[CAMEL-10594](https://issues.apache.org/jira/browse/CAMEL-10594)

Kafka consumer stays alive when camel context is shut down

[CAMEL-10590](https://issues.apache.org/jira/browse/CAMEL-10590)

Unable to invoke no-args constructor for class io.nats.client.ServerInfo

[CAMEL-10582](https://issues.apache.org/jira/browse/CAMEL-10582)

Spring Message headers are immutable

[CAMEL-10581](https://issues.apache.org/jira/browse/CAMEL-10581)

toD (ToDynamicDefinition) does not honor RAW( ) contract - 'removes + from password'

[CAMEL-10579](https://issues.apache.org/jira/browse/CAMEL-10579)

SOAP 1.1 unmarshalling fails for faults that lack a detail element

[CAMEL-10573](https://issues.apache.org/jira/browse/CAMEL-10573)

Align FallbackTypeConverter loading in OSGI environments

[CAMEL-10568](https://issues.apache.org/jira/browse/CAMEL-10568)

SftpChangedExclusiveReadLockStrategy integer overflow

[CAMEL-10564](https://issues.apache.org/jira/browse/CAMEL-10564)

camel-netty-http - Unable to change configuration through spring-boot properties

[CAMEL-10562](https://issues.apache.org/jira/browse/CAMEL-10562)

UnsupportedOperationException in DefaultCamelContext#safelyStartRouteServices

[CAMEL-10557](https://issues.apache.org/jira/browse/CAMEL-10557)

Salesforce bulk API getBatchRequest uses wrong URL pattern

[CAMEL-10556](https://issues.apache.org/jira/browse/CAMEL-10556)

camel-example-twitter-websocket-blueprint - Cannot load static html resources

[CAMEL-10555](https://issues.apache.org/jira/browse/CAMEL-10555)

camel-rest-show karaf command cannot load transformer class

[CAMEL-10548](https://issues.apache.org/jira/browse/CAMEL-10548)

Converter from List to String is not found when @EnableAutoConfiguration is used

[CAMEL-10542](https://issues.apache.org/jira/browse/CAMEL-10542)

DataFormat from registry is used for every dataformat operation (marshal/unmarshal)

[CAMEL-10539](https://issues.apache.org/jira/browse/CAMEL-10539)

When bridging http endpoints and end users do not enable the bridgeEndpoint option they may get a NPE exception

[CAMEL-10537](https://issues.apache.org/jira/browse/CAMEL-10537)

Unable to remove/add restful path to an existing endpoint

[CAMEL-10534](https://issues.apache.org/jira/browse/CAMEL-10534)

camel-stream - Producer writing to stream url need to set doOutput=true

[CAMEL-10526](https://issues.apache.org/jira/browse/CAMEL-10526)

Broken link in documentation Contributing->AsciiDoc

[CAMEL-10524](https://issues.apache.org/jira/browse/CAMEL-10524)

Components not created because of unsatisfied conditions

[CAMEL-10520](https://issues.apache.org/jira/browse/CAMEL-10520)

Lumberjack protocol v1 acknowlegment is not correcty implemented

[CAMEL-10514](https://issues.apache.org/jira/browse/CAMEL-10514)

Camel-Kubernetes: Copy headers from in to out in producer operations

[CAMEL-10511](https://issues.apache.org/jira/browse/CAMEL-10511)

MllpTcpClientProducer should read all available bytes in TCP buffer for acknowledgment

[CAMEL-10510](https://issues.apache.org/jira/browse/CAMEL-10510)

HL7AcknowledgementGenerator should set exchange property and not message header

[CAMEL-10505](https://issues.apache.org/jira/browse/CAMEL-10505)

"FILE" component with option "readLock=rename" throws FileNotFound exception in case of work file is locked/used by another application

[CAMEL-10504](https://issues.apache.org/jira/browse/CAMEL-10504)

Hiding an underlying exception if MongoDbBasicConverters fails to convert to DBObject

[CAMEL-10499](https://issues.apache.org/jira/browse/CAMEL-10499)

camel-sql - error in multiple dynamic IN replacement

[CAMEL-10495](https://issues.apache.org/jira/browse/CAMEL-10495)

camel-salesforce: EndpointConfiguration not taken into account by SubscriptionHelper

[CAMEL-10492](https://issues.apache.org/jira/browse/CAMEL-10492)

Camel Servlet, attachment object is empty

[CAMEL-10490](https://issues.apache.org/jira/browse/CAMEL-10490)

JpaPollingConsumer does not support consumeLockEntity and others

[CAMEL-10486](https://issues.apache.org/jira/browse/CAMEL-10486)

Google PubSub Component does not consume messages with parallel consumers

[CAMEL-10476](https://issues.apache.org/jira/browse/CAMEL-10476)

configAdminFile not used to populate property placeholders in camel-test-blueprint when run via camel-maven-plugin

[CAMEL-10466](https://issues.apache.org/jira/browse/CAMEL-10466)

OOM in Dropbox component (uses ByteArrayOutputStream for get)

[CAMEL-10465](https://issues.apache.org/jira/browse/CAMEL-10465)

camel ahc uses netty 4.0.41 transitively but 4.1.5 explicitly - leads to runtime exceptions

[CAMEL-10464](https://issues.apache.org/jira/browse/CAMEL-10464)

@ContextName CDI qualifier should be repeatable

[CAMEL-10461](https://issues.apache.org/jira/browse/CAMEL-10461)

camel-cmis - Parameters not taking in account

[CAMEL-10460](https://issues.apache.org/jira/browse/CAMEL-10460)

MetricsMessageHistoryFactory.java:138 Generate a NPE

[CAMEL-10455](https://issues.apache.org/jira/browse/CAMEL-10455)

camel-chronicle - has SNAPSHOT dependency

[CAMEL-10454](https://issues.apache.org/jira/browse/CAMEL-10454)

Unclear piece in IdempotentConsumer.java

[CAMEL-10453](https://issues.apache.org/jira/browse/CAMEL-10453)

camel-elsql does not set CamelSqlUpdateCount header on update operation

[CAMEL-10449](https://issues.apache.org/jira/browse/CAMEL-10449)

Set CXF SoapAction header correctly

[CAMEL-10443](https://issues.apache.org/jira/browse/CAMEL-10443)

findById does not work with ObjectId

[CAMEL-10442](https://issues.apache.org/jira/browse/CAMEL-10442)

Multicast leaks into Pipeline stages?

[CAMEL-10441](https://issues.apache.org/jira/browse/CAMEL-10441)

The WorkerGroup option is for NettyConsumer and NettyProducer

[CAMEL-10431](https://issues.apache.org/jira/browse/CAMEL-10431)

camel-elsql - Does not read named parameter from header properties

[CAMEL-10430](https://issues.apache.org/jira/browse/CAMEL-10430)

camel-hystrix - Should also execute fallback if exception not from Camel

[CAMEL-10429](https://issues.apache.org/jira/browse/CAMEL-10429)

CXFRS client requires Exchange.HTTP\_URI instead of HTTP\_PATH for Camel tranport

[CAMEL-10427](https://issues.apache.org/jira/browse/CAMEL-10427)

CXFRS client gets "Response timeout" exception when used with Camel transport

[CAMEL-10425](https://issues.apache.org/jira/browse/CAMEL-10425)

java.io.IOException: Stream closed - When setting result from bean in route

[CAMEL-10418](https://issues.apache.org/jira/browse/CAMEL-10418)

Deploy route with an error

[CAMEL-10414](https://issues.apache.org/jira/browse/CAMEL-10414)

Query is ignore if field filter header is set

[CAMEL-10411](https://issues.apache.org/jira/browse/CAMEL-10411)

Camel-Blueprint - failed container gets restarted automatically

[CAMEL-10409](https://issues.apache.org/jira/browse/CAMEL-10409)

Double release of netty buffer

[CAMEL-10407](https://issues.apache.org/jira/browse/CAMEL-10407)

camel-example-loan-broker : target directory is cleaned while testing so test are failing

[CAMEL-10406](https://issues.apache.org/jira/browse/CAMEL-10406)

VM endpoint caching leak the wrong camel context

[CAMEL-10399](https://issues.apache.org/jira/browse/CAMEL-10399)

OutOfMemoryError: Java heap space when sending large file to endpoint

[CAMEL-10396](https://issues.apache.org/jira/browse/CAMEL-10396)

Can't use parameter type to select among overloaded methods

[CAMEL-10394](https://issues.apache.org/jira/browse/CAMEL-10394)

BlueprintCamelContext cannot find components created in RouteBuilder.configure method

[CAMEL-10386](https://issues.apache.org/jira/browse/CAMEL-10386)

simple language nullsafe expression fails on empty array

[CAMEL-10385](https://issues.apache.org/jira/browse/CAMEL-10385)

simple ognl expression issue w/ list & spring boot

[CAMEL-10384](https://issues.apache.org/jira/browse/CAMEL-10384)

Shutdown broken when using Spring Boot

[CAMEL-10383](https://issues.apache.org/jira/browse/CAMEL-10383)

activemq-camel - Issue with parsing uri to determine queue vs topic

[CAMEL-10381](https://issues.apache.org/jira/browse/CAMEL-10381)

camel-google-mail getting NPE from component configuration

[CAMEL-10380](https://issues.apache.org/jira/browse/CAMEL-10380)

JettyHttpEndpoint9 ignores eagerCheckContentAvailable so Jetty builds a reuqest with "Transfer-Encoding: chunked"

[CAMEL-10376](https://issues.apache.org/jira/browse/CAMEL-10376)

BeanInfo#introspect does not work correctly with bridge methods

[CAMEL-10372](https://issues.apache.org/jira/browse/CAMEL-10372)

camel-stream - Component doc issue

[CAMEL-10370](https://issues.apache.org/jira/browse/CAMEL-10370)

Conversion to CxfPayload throws Exception for Non-XML payload

[CAMEL-10368](https://issues.apache.org/jira/browse/CAMEL-10368)

Unused deflater in ZipDataFormat

[CAMEL-10366](https://issues.apache.org/jira/browse/CAMEL-10366)

Missing input/output values in camel-catalog for several eips

[CAMEL-10365](https://issues.apache.org/jira/browse/CAMEL-10365)

\[Camel-consul\] Invalid syntax

[CAMEL-10364](https://issues.apache.org/jira/browse/CAMEL-10364)

\[Camel-Chronicle\] chronicle-engine component provide a wrong syntax

[CAMEL-10341](https://issues.apache.org/jira/browse/CAMEL-10341)

When using SSL, a NettyConsumer set to Client Mode does not initiate a handshake

[CAMEL-10322](https://issues.apache.org/jira/browse/CAMEL-10322)

Choice breaks Advice - UnsupportedOperationException

[CAMEL-10272](https://issues.apache.org/jira/browse/CAMEL-10272)

Unexpected behaviour in aggregator if recipient list is processed in parallel

[CAMEL-10236](https://issues.apache.org/jira/browse/CAMEL-10236)

BeanProccessor - method invocation with generics+annotations

[CAMEL-10139](https://issues.apache.org/jira/browse/CAMEL-10139)

Multiple verbs for same resource not working in camel-undertow (rest dsl)

[CAMEL-10084](https://issues.apache.org/jira/browse/CAMEL-10084)

AggregateProcessor/JdbcAggregationRepository : table COMPLETED not cleaned when AggregationStrategy.aggregate does not return oldExchange

[CAMEL-10008](https://issues.apache.org/jira/browse/CAMEL-10008)

camel-spring Karaf feature is incompatible with camel-jms

[CAMEL-9813](https://issues.apache.org/jira/browse/CAMEL-9813)

Zookeeper route policy requires first message to check if online.

[CAMEL-9606](https://issues.apache.org/jira/browse/CAMEL-9606)

SJMS Consumer-Producer in transaciton

[CAMEL-9552](https://issues.apache.org/jira/browse/CAMEL-9552)

Cannot consume and produce to beanstalk component in the same route

[CAMEL-9502](https://issues.apache.org/jira/browse/CAMEL-9502)

karaf - Re-installing bundle using camel-cxf throws javax.management.InstanceAlreadyExistsException

[CAMEL-8971](https://issues.apache.org/jira/browse/CAMEL-8971)

HazelcastAggregatorRepository redelivers incorrectly

[CAMEL-8947](https://issues.apache.org/jira/browse/CAMEL-8947)

LevelDBAggregatorRepository redelivers incorrectly

[CAMEL-8208](https://issues.apache.org/jira/browse/CAMEL-8208)

ZooKeeperRoutePolicy is not able to recover after session expiration

### Improvement (297)

[CAMEL-11211](https://issues.apache.org/jira/browse/CAMEL-11211)

Remove deprecated SpanManager from camel-opentracing

[CAMEL-11208](https://issues.apache.org/jira/browse/CAMEL-11208)

camel-swagger-java - Should use guava 20 and not 19

[CAMEL-11206](https://issues.apache.org/jira/browse/CAMEL-11206)

camel-twitter - The default delay is not used

[CAMEL-11204](https://issues.apache.org/jira/browse/CAMEL-11204)

camel-catalog - asEndpointUri to support connectors/component with no context-path part

[CAMEL-11203](https://issues.apache.org/jira/browse/CAMEL-11203)

Verifier should support exclusion of properties in option groups

[CAMEL-11193](https://issues.apache.org/jira/browse/CAMEL-11193)

Route from kafka topic to another kafka topic issue

[CAMEL-11191](https://issues.apache.org/jira/browse/CAMEL-11191)

Service Call - XML configuration of static servers called servers instead of server

[CAMEL-11190](https://issues.apache.org/jira/browse/CAMEL-11190)

Service Call - Allow to configure static server list from a property placholder

[CAMEL-11182](https://issues.apache.org/jira/browse/CAMEL-11182)

SolrParams are not honored when sending SolrInputDocument.

[CAMEL-11175](https://issues.apache.org/jira/browse/CAMEL-11175)

REST DSL Swagger generator default generated class/package names

[CAMEL-11170](https://issues.apache.org/jira/browse/CAMEL-11170)

Service Call : add a spi for component to provide a custom expression to build the camel uri

[CAMEL-11167](https://issues.apache.org/jira/browse/CAMEL-11167)

Include Camel name in spring boot health check

[CAMEL-11165](https://issues.apache.org/jira/browse/CAMEL-11165)

Add @Generated annotation to code generated by SpringBootAutoConfigurationMojo

[CAMEL-11164](https://issues.apache.org/jira/browse/CAMEL-11164)

Add @Generated annotation Salesforce generated code

[CAMEL-11163](https://issues.apache.org/jira/browse/CAMEL-11163)

Add @Generated annotation in REST DSL Swagger generated code

[CAMEL-11161](https://issues.apache.org/jira/browse/CAMEL-11161)

Service Call : allow to use properties to further customize the underlying camel component used to implement service-call concepts

[CAMEL-11152](https://issues.apache.org/jira/browse/CAMEL-11152)

camel-ssh - Allow to use message headers for username/password

[CAMEL-11148](https://issues.apache.org/jira/browse/CAMEL-11148)

camel-reactive-streams: too many backpressure strategies

[CAMEL-11141](https://issues.apache.org/jira/browse/CAMEL-11141)

Add support for VPC instances

[CAMEL-11133](https://issues.apache.org/jira/browse/CAMEL-11133)

Data format - Marshal and unmarshal should eager start their data formats

[CAMEL-11124](https://issues.apache.org/jira/browse/CAMEL-11124)

camel-reactive-streams - Allow to silently ignore discarded messages

[CAMEL-11123](https://issues.apache.org/jira/browse/CAMEL-11123)

Rename CamelReactiveStreamsServiceImpl to DefaultCamelReactiveStreamsService

[CAMEL-11116](https://issues.apache.org/jira/browse/CAMEL-11116)

Better handling of query parameters in RestProducer

[CAMEL-11115](https://issues.apache.org/jira/browse/CAMEL-11115)

Enhance binding support in RestComponent

[CAMEL-11108](https://issues.apache.org/jira/browse/CAMEL-11108)

camel-infinispan : change the uri syntax from infinispan:hostName to infinispan:cacheName

[CAMEL-11105](https://issues.apache.org/jira/browse/CAMEL-11105)

camel-eventadmin does not allow multiple consumers with the same URI

[CAMEL-11100](https://issues.apache.org/jira/browse/CAMEL-11100)

service-call : add an option configure the expression to use (i.e simple)

[CAMEL-11092](https://issues.apache.org/jira/browse/CAMEL-11092)

If setting Exchange.REST\_HTTP\_URI the RestProducer should remove Exchange.HTTP\_PATH header

[CAMEL-11090](https://issues.apache.org/jira/browse/CAMEL-11090)

Add trimToNull method to StringHelper

[CAMEL-11085](https://issues.apache.org/jira/browse/CAMEL-11085)

camel-kubernetes : make it easy to configure components and service-discovery in spring-boot

[CAMEL-11084](https://issues.apache.org/jira/browse/CAMEL-11084)

camel-dns : make it easy to configure components and service-discovery in spring-boot

[CAMEL-11083](https://issues.apache.org/jira/browse/CAMEL-11083)

camel-etcd : make it easy to configure components and service-discovery in spring-boot

[CAMEL-11082](https://issues.apache.org/jira/browse/CAMEL-11082)

camel-consul : make it easy to configure components and service-discovery in spring-boot

[CAMEL-11081](https://issues.apache.org/jira/browse/CAMEL-11081)

camel-consul: add support for additional http api

[CAMEL-11079](https://issues.apache.org/jira/browse/CAMEL-11079)

Batch SJMS Consumer Dies on Failover

[CAMEL-11077](https://issues.apache.org/jira/browse/CAMEL-11077)

Remove toString method in SalesforceException

[CAMEL-11076](https://issues.apache.org/jira/browse/CAMEL-11076)

Refactor addSecuirtyHandlerMethod to addProtocolHandlerMethod

[CAMEL-11075](https://issues.apache.org/jira/browse/CAMEL-11075)

AbstractSalesforceTestBase::doCreateRouteBuilder should be optional

[CAMEL-11073](https://issues.apache.org/jira/browse/CAMEL-11073)

camel-rest - Spring boot option named c-o-r-s

[CAMEL-11070](https://issues.apache.org/jira/browse/CAMEL-11070)

camel-aws - SQS - Allow to configure aws queue url

[CAMEL-11068](https://issues.apache.org/jira/browse/CAMEL-11068)

Remove deprecated usage from Salesforce component

[CAMEL-11067](https://issues.apache.org/jira/browse/CAMEL-11067)

camel-hystrix - Include default values in spring-boot auto configuration

[CAMEL-11066](https://issues.apache.org/jira/browse/CAMEL-11066)

Make salesforce authentication options simpler to configure

[CAMEL-11061](https://issues.apache.org/jira/browse/CAMEL-11061)

service call eip: add an option to set global defaults

[CAMEL-11060](https://issues.apache.org/jira/browse/CAMEL-11060)

dn shouldn't be strictly required for Spring LDAP component

[CAMEL-11054](https://issues.apache.org/jira/browse/CAMEL-11054)

Create SPI for Log EIP to enable other components to intercept/enrich logged messages

[CAMEL-11051](https://issues.apache.org/jira/browse/CAMEL-11051)

Support query parameters in rest-swagger

[CAMEL-11050](https://issues.apache.org/jira/browse/CAMEL-11050)

Support for optional query parameters in REST component

[CAMEL-11049](https://issues.apache.org/jira/browse/CAMEL-11049)

camel-package-maven-plugin - Add option to ignore no model in core for custom 3rd party data formats

[CAMEL-11046](https://issues.apache.org/jira/browse/CAMEL-11046)

camel-undertow - Allow to consume from root path more without ending slash

[CAMEL-11044](https://issues.apache.org/jira/browse/CAMEL-11044)

CLONE - EndpointHelper.resolveReferenceListParameter should not return immutable lists

[CAMEL-11043](https://issues.apache.org/jira/browse/CAMEL-11043)

ServiceCall : allow to use placeholders for name, uri, etc

[CAMEL-11033](https://issues.apache.org/jira/browse/CAMEL-11033)

Set \`operationId\` in generated Swagger specification

[CAMEL-11032](https://issues.apache.org/jira/browse/CAMEL-11032)

Component docs - Break long names so docs look better

[CAMEL-11027](https://issues.apache.org/jira/browse/CAMEL-11027)

Camel-Hazelcast: Support Reliable Topic

[CAMEL-11025](https://issues.apache.org/jira/browse/CAMEL-11025)

RestProducer should set Accept and Content-Type headers if given in endpoint configuration

[CAMEL-11024](https://issues.apache.org/jira/browse/CAMEL-11024)

service call eip: add an option to add additional configurations via spring-boot properties

[CAMEL-11023](https://issues.apache.org/jira/browse/CAMEL-11023)

Hystrix Starter : add an option to configure additional configuration via spring-boot properties

[CAMEL-11018](https://issues.apache.org/jira/browse/CAMEL-11018)

camel-ehcache: make it easy to create temporary caches

[CAMEL-11004](https://issues.apache.org/jira/browse/CAMEL-11004)

camel-connector - Allow to define what the data type is as output/input

[CAMEL-11003](https://issues.apache.org/jira/browse/CAMEL-11003)

camel-google-calendar - Easier to configure scopes

[CAMEL-10998](https://issues.apache.org/jira/browse/CAMEL-10998)

jetty producer - should be deprecated

[CAMEL-10996](https://issues.apache.org/jira/browse/CAMEL-10996)

camel-kafka - Upgrade to 0.10.2.0

[CAMEL-10995](https://issues.apache.org/jira/browse/CAMEL-10995)

camel-spring-boot - Generated auto configuration and default value problems

[CAMEL-10994](https://issues.apache.org/jira/browse/CAMEL-10994)

camel-kafka - Allow to configure more options on component level

[CAMEL-10993](https://issues.apache.org/jira/browse/CAMEL-10993)

camel-kafka - Do not WARN per message for no key or partition

[CAMEL-10984](https://issues.apache.org/jira/browse/CAMEL-10984)

Creating consumer should inject CamelContext if consumer is aware

[CAMEL-10983](https://issues.apache.org/jira/browse/CAMEL-10983)

Fail early and show meaningful log for invalid endpoint URI in Blueprint

[CAMEL-10978](https://issues.apache.org/jira/browse/CAMEL-10978)

Camel-Hazelcast: support client mode

[CAMEL-10976](https://issues.apache.org/jira/browse/CAMEL-10976)

camel-spring-boot - Configure rest configuration using auto configuration

[CAMEL-10975](https://issues.apache.org/jira/browse/CAMEL-10975)

camel-catalog-maven - Allow to configure temp folder

[CAMEL-10970](https://issues.apache.org/jira/browse/CAMEL-10970)

RuntimeCamelCatalog - Add JMX api

[CAMEL-10967](https://issues.apache.org/jira/browse/CAMEL-10967)

camel-catalog-connector - Add api to build endpoint uri based on connection options

[CAMEL-10962](https://issues.apache.org/jira/browse/CAMEL-10962)

camel-http4 - Allow to configure host, port and path using separate options

[CAMEL-10959](https://issues.apache.org/jira/browse/CAMEL-10959)

camel-catalog-core - Allow to reuse the validation and other apis in camel-core as well

[CAMEL-10957](https://issues.apache.org/jira/browse/CAMEL-10957)

Log a warning if the response cannot be unmarshalled in Composite API

[CAMEL-10953](https://issues.apache.org/jira/browse/CAMEL-10953)

Add messageAttribute support to AWS SNS component

[CAMEL-10944](https://issues.apache.org/jira/browse/CAMEL-10944)

camel-kafka - When consumer stop it should auto commit

[CAMEL-10941](https://issues.apache.org/jira/browse/CAMEL-10941)

Component docs - Remove raw marker

[CAMEL-10940](https://issues.apache.org/jira/browse/CAMEL-10940)

Component docs - Separate path and query parameters

[CAMEL-10938](https://issues.apache.org/jira/browse/CAMEL-10938)

Camel Salesforce : add an option to retrieve login information for testing purpose from env var or system properties

[CAMEL-10937](https://issues.apache.org/jira/browse/CAMEL-10937)

Camel components - Configured using setters should support property placeholders

[CAMEL-10934](https://issues.apache.org/jira/browse/CAMEL-10934)

Idempotent Consumer EIP - Should prepare idempotent repository better

[CAMEL-10930](https://issues.apache.org/jira/browse/CAMEL-10930)

Move groovy dsl into camel-groovy-dsl

[CAMEL-10926](https://issues.apache.org/jira/browse/CAMEL-10926)

Set the Host header in Undertow producer

[CAMEL-10919](https://issues.apache.org/jira/browse/CAMEL-10919)

Auto expose Hystrix metrics servlet in spring-boot web

[CAMEL-10917](https://issues.apache.org/jira/browse/CAMEL-10917)

Implementations of RestProducerFactory should handle empty or null basePath and uriTemplate

[CAMEL-10916](https://issues.apache.org/jira/browse/CAMEL-10916)

camel http4 component does not send a body when the http method DELETE is used

[CAMEL-10907](https://issues.apache.org/jira/browse/CAMEL-10907)

http components: have a common way to express concepts like proxy

[CAMEL-10900](https://issues.apache.org/jira/browse/CAMEL-10900)

OutOfMemoryError with big file in ftp or sftp producer with charset assigned

[CAMEL-10894](https://issues.apache.org/jira/browse/CAMEL-10894)

XML Validator: Improve DTD handling

[CAMEL-10886](https://issues.apache.org/jira/browse/CAMEL-10886)

Support Limits API response from Salesforce v39.0

[CAMEL-10884](https://issues.apache.org/jira/browse/CAMEL-10884)

Add a \`cleanrepo\` profile to Maven build

[CAMEL-10883](https://issues.apache.org/jira/browse/CAMEL-10883)

Support HTTP 1.1 continue in Undertow

[CAMEL-10882](https://issues.apache.org/jira/browse/CAMEL-10882)

camel-hazelcast - Allow to configure default operation as string value

[CAMEL-10878](https://issues.apache.org/jira/browse/CAMEL-10878)

camel-http / camel-http4 - Allow to specify HTTP operation as uri parameter

[CAMEL-10871](https://issues.apache.org/jira/browse/CAMEL-10871)

camel-kafka - allow to retrieve whether it's the last record before commit

[CAMEL-10870](https://issues.apache.org/jira/browse/CAMEL-10870)

camel-sql stored procedures don't support negative vendor-specific JDBC types

[CAMEL-10869](https://issues.apache.org/jira/browse/CAMEL-10869)

TRACE on ftp component reveals password

[CAMEL-10862](https://issues.apache.org/jira/browse/CAMEL-10862)

camel-consul - ConsultRoutePolicy - Allow to configure host port easier

[CAMEL-10861](https://issues.apache.org/jira/browse/CAMEL-10861)

camel-hazelcast - route policy should have JMX api

[CAMEL-10860](https://issues.apache.org/jira/browse/CAMEL-10860)

camel-hazelcast - route policy should have a better try lock default value

[CAMEL-10858](https://issues.apache.org/jira/browse/CAMEL-10858)

Add CSRF Support to Camel bonita component

[CAMEL-10853](https://issues.apache.org/jira/browse/CAMEL-10853)

CsvDataFormat should be completed with 'CSVFormat.withTrim'

[CAMEL-10851](https://issues.apache.org/jira/browse/CAMEL-10851)

getBody(Class<T> type) on originalMessage returns null

[CAMEL-10850](https://issues.apache.org/jira/browse/CAMEL-10850)

Autogenerate EIP options in documentation files

[CAMEL-10848](https://issues.apache.org/jira/browse/CAMEL-10848)

Salesforce: configure initialReplayIdMap requires keys to be prefixed with "/topic"

[CAMEL-10847](https://issues.apache.org/jira/browse/CAMEL-10847)

Component json schema - Include display name for options

[CAMEL-10846](https://issues.apache.org/jira/browse/CAMEL-10846)

Handle 404 situations more gracefully

[CAMEL-10844](https://issues.apache.org/jira/browse/CAMEL-10844)

Component docs - Remove .html generated files in components

[CAMEL-10843](https://issues.apache.org/jira/browse/CAMEL-10843)

Add readme.adoc files for other components

[CAMEL-10842](https://issues.apache.org/jira/browse/CAMEL-10842)

Component JSon schema - JSon values should not always be string types

[CAMEL-10840](https://issues.apache.org/jira/browse/CAMEL-10840)

CsvDataFormat.setRecordConverterRef not usable

[CAMEL-10838](https://issues.apache.org/jira/browse/CAMEL-10838)

camel-cache - Create a better body replacer processor

[CAMEL-10836](https://issues.apache.org/jira/browse/CAMEL-10836)

camel-salesforce - Allow to configure login details easier

[CAMEL-10832](https://issues.apache.org/jira/browse/CAMEL-10832)

camel-kafka - Allow to configure broker urls on component level

[CAMEL-10831](https://issues.apache.org/jira/browse/CAMEL-10831)

camel examples - Add readme files for missing examples

[CAMEL-10827](https://issues.apache.org/jira/browse/CAMEL-10827)

camel-twitter - The timeline should defer its first poll to after Camel is started

[CAMEL-10826](https://issues.apache.org/jira/browse/CAMEL-10826)

camel-salesforce - Logging in as null

[CAMEL-10819](https://issues.apache.org/jira/browse/CAMEL-10819)

examples - Generate list of examples with description

[CAMEL-10813](https://issues.apache.org/jira/browse/CAMEL-10813)

Host address ignored when creating a Restlet Server

[CAMEL-10812](https://issues.apache.org/jira/browse/CAMEL-10812)

FactoryFinder: make DefaultFactoryFinder and OsgiFactoryFinder thread safe

[CAMEL-10811](https://issues.apache.org/jira/browse/CAMEL-10811)

Provide sample Salesforce connector component and example

[CAMEL-10810](https://issues.apache.org/jira/browse/CAMEL-10810)

Component docs - Remove .0 from available from

[CAMEL-10808](https://issues.apache.org/jira/browse/CAMEL-10808)

refactoring of spring boot examples

[CAMEL-10801](https://issues.apache.org/jira/browse/CAMEL-10801)

ServiceCall : add the option to force the service call to use the default load balancer

[CAMEL-10800](https://issues.apache.org/jira/browse/CAMEL-10800)

camel-connector - Allow to generate json schema and include it in source code

[CAMEL-10799](https://issues.apache.org/jira/browse/CAMEL-10799)

camel-connector - Generate spring boot auto configuration

[CAMEL-10797](https://issues.apache.org/jira/browse/CAMEL-10797)

Create endpoint from uri without context-path

[CAMEL-10791](https://issues.apache.org/jira/browse/CAMEL-10791)

Add an option in the ZipFileDataFormat to let the iterator support the empty directory

[CAMEL-10790](https://issues.apache.org/jira/browse/CAMEL-10790)

gridfs should be renamed to mongodb-gridfs

[CAMEL-10784](https://issues.apache.org/jira/browse/CAMEL-10784)

camel-connector - Allow to rename options

[CAMEL-10779](https://issues.apache.org/jira/browse/CAMEL-10779)

Authentication : provide a way to use refresh\_token mode in addition to password method

[CAMEL-10772](https://issues.apache.org/jira/browse/CAMEL-10772)

Spring POJO @Produce @Consume Remoting auto detect binding usage improvement

[CAMEL-10770](https://issues.apache.org/jira/browse/CAMEL-10770)

Upgrade to Spring Boot 1.5.x

[CAMEL-10769](https://issues.apache.org/jira/browse/CAMEL-10769)

Tika Component - Support Multi-Value Metadata

[CAMEL-10765](https://issues.apache.org/jira/browse/CAMEL-10765)

Remove unused oauth dependency from camel-cxf pom

[CAMEL-10764](https://issues.apache.org/jira/browse/CAMEL-10764)

The use of BrowserCompatHostnameVerifier is deprecated

[CAMEL-10763](https://issues.apache.org/jira/browse/CAMEL-10763)

Make HTTP4 component easy to extend

[CAMEL-10761](https://issues.apache.org/jira/browse/CAMEL-10761)

ServiceCall EIP : support for chaining service filters/discovery

[CAMEL-10760](https://issues.apache.org/jira/browse/CAMEL-10760)

Allow OGNL expression on square bracket accessed properties and headers in simple language

[CAMEL-10759](https://issues.apache.org/jira/browse/CAMEL-10759)

RABBITMQ Component binding args

[CAMEL-10757](https://issues.apache.org/jira/browse/CAMEL-10757)

camel-jms - Use dash in destination type enum instead of colon

[CAMEL-10753](https://issues.apache.org/jira/browse/CAMEL-10753)

Box component uses out of date library

[CAMEL-10749](https://issues.apache.org/jira/browse/CAMEL-10749)

Quartz2 interrupt job

[CAMEL-10746](https://issues.apache.org/jira/browse/CAMEL-10746)

camel catalog - Allow to download custom version of runtime provider

[CAMEL-10745](https://issues.apache.org/jira/browse/CAMEL-10745)

POJO @Produce @Consume does not work with multiple arguments anymore.

[CAMEL-10739](https://issues.apache.org/jira/browse/CAMEL-10739)

camel-bindy: Unmarshall CSV fields with crlf characters

[CAMEL-10737](https://issues.apache.org/jira/browse/CAMEL-10737)

file component should support parent folder in tempFileName

[CAMEL-10734](https://issues.apache.org/jira/browse/CAMEL-10734)

Add support to track changes from specified sequence

[CAMEL-10729](https://issues.apache.org/jira/browse/CAMEL-10729)

Camel-AWS: S3 autocloseBody option

[CAMEL-10726](https://issues.apache.org/jira/browse/CAMEL-10726)

Correlation of JMS InOut exchanges with custom JMS property

[CAMEL-10725](https://issues.apache.org/jira/browse/CAMEL-10725)

camel-zipkin - Upgrade to zipkin brave 4.x

[CAMEL-10724](https://issues.apache.org/jira/browse/CAMEL-10724)

Improve Java DSL support for Java 8

[CAMEL-10722](https://issues.apache.org/jira/browse/CAMEL-10722)

ServiceCall : improve configuration of service-call components in Java DSL

[CAMEL-10720](https://issues.apache.org/jira/browse/CAMEL-10720)

Add deprecated to the description in the generated XSD schema

[CAMEL-10714](https://issues.apache.org/jira/browse/CAMEL-10714)

Replace ByteArrayOutputStream in JettyContentExchange9 with OutputStreamBuilder

[CAMEL-10710](https://issues.apache.org/jira/browse/CAMEL-10710)

ServiceCall EIP : improve Java DSL

[CAMEL-10705](https://issues.apache.org/jira/browse/CAMEL-10705)

Allow to use an SSLContextParameters object for Kafka

[CAMEL-10703](https://issues.apache.org/jira/browse/CAMEL-10703)

camel-catalog - Add api for validating any Camel languge

[CAMEL-10702](https://issues.apache.org/jira/browse/CAMEL-10702)

camel-jsonpath - Allow to define predicates even easier

[CAMEL-10700](https://issues.apache.org/jira/browse/CAMEL-10700)

camel-maven - validate simple predicates and property placeholders

[CAMEL-10699](https://issues.apache.org/jira/browse/CAMEL-10699)

Simple - Add short error message

[CAMEL-10698](https://issues.apache.org/jira/browse/CAMEL-10698)

camel-maven - validate simple expression predicate vs expression

[CAMEL-10697](https://issues.apache.org/jira/browse/CAMEL-10697)

Infinite loop sometimes happen at the shutdown of the Kafka consumer

[CAMEL-10691](https://issues.apache.org/jira/browse/CAMEL-10691)

HttpRestServletResolveConsumerStrategy should pick the path with longest prefix match

[CAMEL-10687](https://issues.apache.org/jira/browse/CAMEL-10687)

Component docs - Auto generate title so they are consistent

[CAMEL-10686](https://issues.apache.org/jira/browse/CAMEL-10686)

service-call eip : generate service-call auto configurations for spring-boot

[CAMEL-10684](https://issues.apache.org/jira/browse/CAMEL-10684)

camel-catalog - Simple validator should provide location index of the error

[CAMEL-10683](https://issues.apache.org/jira/browse/CAMEL-10683)

spring-boot: always create configuration properties for classes annotated with @UriParams

[CAMEL-10682](https://issues.apache.org/jira/browse/CAMEL-10682)

AbstractCamelContextFactorybean : add specific methods for servicecall/hystrix configuration

[CAMEL-10680](https://issues.apache.org/jira/browse/CAMEL-10680)

Camel catalog - validate endpoint properties - consumer vs producer

[CAMEL-10679](https://issues.apache.org/jira/browse/CAMEL-10679)

Producer does not populate attachments from response

[CAMEL-10678](https://issues.apache.org/jira/browse/CAMEL-10678)

Transformer registry JMX

[CAMEL-10667](https://issues.apache.org/jira/browse/CAMEL-10667)

Add tarFile data format to Java DSL

[CAMEL-10666](https://issues.apache.org/jira/browse/CAMEL-10666)

Serializable headers lost by JmsBinding

[CAMEL-10662](https://issues.apache.org/jira/browse/CAMEL-10662)

camel-hystrix - If hystrix timeout occurs then the hystrix timeout exception should be cause

[CAMEL-10661](https://issues.apache.org/jira/browse/CAMEL-10661)

camel-hystrix - Fallback should route exchange if it was marked as stop due delay timeout

[CAMEL-10658](https://issues.apache.org/jira/browse/CAMEL-10658)

Camel-InfluxDB: Support BatchPoints

[CAMEL-10655](https://issues.apache.org/jira/browse/CAMEL-10655)

Camel catalog - Include html copies of adoc documentation

[CAMEL-10650](https://issues.apache.org/jira/browse/CAMEL-10650)

camel-spring-boot - Allow to configure SSLContextParameters in auto configuration

[CAMEL-10648](https://issues.apache.org/jira/browse/CAMEL-10648)

camel-sjms - Batch consumer should support async start listener

[CAMEL-10646](https://issues.apache.org/jira/browse/CAMEL-10646)

support JSONPath on beans as well as Strings & InputStreams

[CAMEL-10643](https://issues.apache.org/jira/browse/CAMEL-10643)

camel-sjms - Should log connection issues out of the box

[CAMEL-10641](https://issues.apache.org/jira/browse/CAMEL-10641)

camel-core - In OSGi should unload the loaded type converters when bundle is removed

[CAMEL-10638](https://issues.apache.org/jira/browse/CAMEL-10638)

Refactor ServiceCall EIP

[CAMEL-10636](https://issues.apache.org/jira/browse/CAMEL-10636)

Component options docs - Add columns with default values

[CAMEL-10633](https://issues.apache.org/jira/browse/CAMEL-10633)

json dataformat should set a header "Content-Type: application/json" if there's no "Content-Type" header set

[CAMEL-10629](https://issues.apache.org/jira/browse/CAMEL-10629)

Add labels to component level options

[CAMEL-10625](https://issues.apache.org/jira/browse/CAMEL-10625)

Camel-Hystrix: Support allowMaximumSizeToDivergeFromCoreSize and maximumSize in Hystrix Threadpool configuration

[CAMEL-10619](https://issues.apache.org/jira/browse/CAMEL-10619)

Add spring boot configuration for configuring shutdown options

[CAMEL-10618](https://issues.apache.org/jira/browse/CAMEL-10618)

camel-sql - Allow to use Spring Boot DataSource

[CAMEL-10617](https://issues.apache.org/jira/browse/CAMEL-10617)

camel-sjms - Async start consumer should defer starting endpint

[CAMEL-10611](https://issues.apache.org/jira/browse/CAMEL-10611)

Align Aries namespace handlers to blueprint-core 1.7.x

[CAMEL-10607](https://issues.apache.org/jira/browse/CAMEL-10607)

camel-cxf - Allow to call no-arg methods more easier

[CAMEL-10606](https://issues.apache.org/jira/browse/CAMEL-10606)

Modify quartz2 endpoint to be a singleton

[CAMEL-10604](https://issues.apache.org/jira/browse/CAMEL-10604)

Camel-JacksonXML: Add an option to allow the UnmarshallType header use

[CAMEL-10595](https://issues.apache.org/jira/browse/CAMEL-10595)

Fix Checkstyle in camel-salesforce-maven-plugin

[CAMEL-10592](https://issues.apache.org/jira/browse/CAMEL-10592)

Improve naming and description for sip components

[CAMEL-10589](https://issues.apache.org/jira/browse/CAMEL-10589)

ServiceNow: add an option to convigure SSL/TLS

[CAMEL-10586](https://issues.apache.org/jira/browse/CAMEL-10586)

make the kafka endpoint a little easier to use

[CAMEL-10585](https://issues.apache.org/jira/browse/CAMEL-10585)

the URL format should include the topic name like the ActiiveMQ & AMQP endpoints

[CAMEL-10584](https://issues.apache.org/jira/browse/CAMEL-10584)

spring boot auto configuration mojo: use Class.isAssignableFrom instead of instanceof as the later may fail at compile time in case of final classes

[CAMEL-10577](https://issues.apache.org/jira/browse/CAMEL-10577)

Jetty9 producer only supports payloads up hardcoded limit (2MB)

[CAMEL-10576](https://issues.apache.org/jira/browse/CAMEL-10576)

snakeyaml : as the snakeyaml parser is not thread safe, object like Constructor, Resolver etc should be provided by a factory/supplier

[CAMEL-10575](https://issues.apache.org/jira/browse/CAMEL-10575)

snakeyaml: add an option to filter classes the yaml parser can construct

[CAMEL-10572](https://issues.apache.org/jira/browse/CAMEL-10572)

RefLanguage should support Predicates for Choice

[CAMEL-10571](https://issues.apache.org/jira/browse/CAMEL-10571)

camel-salesforce: implement support for SObject tree creation via Composite API

[CAMEL-10570](https://issues.apache.org/jira/browse/CAMEL-10570)

camel-salesforce: add metadata to generated DTOs

[CAMEL-10567](https://issues.apache.org/jira/browse/CAMEL-10567)

Camel-Jackson: Add an option to allow the UnmarshallType header use

[CAMEL-10565](https://issues.apache.org/jira/browse/CAMEL-10565)

camel-undertow - Allow configuring thread pool and other options

[CAMEL-10563](https://issues.apache.org/jira/browse/CAMEL-10563)

camel-hazelcast: add an option to provide a custom configuration (custom Config object or configuration file location)

[CAMEL-10558](https://issues.apache.org/jira/browse/CAMEL-10558)

camel-core - XmlConverter cannot load fallback TransformerFactory in OSGi

[CAMEL-10554](https://issues.apache.org/jira/browse/CAMEL-10554)

camel-mongodb evolution to driver 3

[CAMEL-10552](https://issues.apache.org/jira/browse/CAMEL-10552)

spring-boot: make component lazy loading

[CAMEL-10551](https://issues.apache.org/jira/browse/CAMEL-10551)

spring-boot: make auto configured dataformats and languages prototype

[CAMEL-10550](https://issues.apache.org/jira/browse/CAMEL-10550)

spring-boot: add a global option to disable data-format, language and components auto configuration

[CAMEL-10546](https://issues.apache.org/jira/browse/CAMEL-10546)

CamelContext - Rename getProperties to getConfiguration

[CAMEL-10527](https://issues.apache.org/jira/browse/CAMEL-10527)

camel-mail - Option skipFailedMessage should catch all exceptions

[CAMEL-10513](https://issues.apache.org/jira/browse/CAMEL-10513)

Start BlueprintCamelContext on BlueprintEvent.CREATED

[CAMEL-10509](https://issues.apache.org/jira/browse/CAMEL-10509)

ManagedCamelContextMBean - additional namespaces are removed

[CAMEL-10507](https://issues.apache.org/jira/browse/CAMEL-10507)

Make TypeReference inline anonymous classes constant

[CAMEL-10506](https://issues.apache.org/jira/browse/CAMEL-10506)

Camel-git : Refactor unit tests using Jgit

[CAMEL-10503](https://issues.apache.org/jira/browse/CAMEL-10503)

Camel-Git: Add RemoteAdd command

[CAMEL-10501](https://issues.apache.org/jira/browse/CAMEL-10501)

Allow Salesforce Maven plugin to run without Maven project

[CAMEL-10500](https://issues.apache.org/jira/browse/CAMEL-10500)

Camel-Git: Add allowEmpty commits option

[CAMEL-10491](https://issues.apache.org/jira/browse/CAMEL-10491)

Spring-LDAP - Add support for authenticate, modify\_attributes and function\_driven operations

[CAMEL-10488](https://issues.apache.org/jira/browse/CAMEL-10488)

ServiceNow : add an option to configure teh API version

[CAMEL-10483](https://issues.apache.org/jira/browse/CAMEL-10483)

RabbitMQ Component should allow header bindings

[CAMEL-10482](https://issues.apache.org/jira/browse/CAMEL-10482)

ServiceNow : add an option to set inbound and outbound models

[CAMEL-10473](https://issues.apache.org/jira/browse/CAMEL-10473)

Failover Loadbalancer - Error handler should kick in after exhausted when inheritErrorHandler is false

[CAMEL-10470](https://issues.apache.org/jira/browse/CAMEL-10470)

camel-mail - Should allow to configure SimpleSearchTerm as plain POJO

[CAMEL-10468](https://issues.apache.org/jira/browse/CAMEL-10468)

Java8 DSL: Add support for aggregation strategy with different body types

[CAMEL-10463](https://issues.apache.org/jira/browse/CAMEL-10463)

Update Camel Salesforce integration tests

[CAMEL-10462](https://issues.apache.org/jira/browse/CAMEL-10462)

Add MDC support to DefaultCamelContext startup/shutdown

[CAMEL-10459](https://issues.apache.org/jira/browse/CAMEL-10459)

camel-elsql - option batch is not implemented in producer

[CAMEL-10451](https://issues.apache.org/jira/browse/CAMEL-10451)

camel-undertow - Add multipart request support

[CAMEL-10450](https://issues.apache.org/jira/browse/CAMEL-10450)

bean/class component should be able to call groovy function directly

[CAMEL-10448](https://issues.apache.org/jira/browse/CAMEL-10448)

File read lock - idempotent and change/rename should be possible

[CAMEL-10446](https://issues.apache.org/jira/browse/CAMEL-10446)

Need to consolidate header mapping logic between Camel and CXF messages

[CAMEL-10444](https://issues.apache.org/jira/browse/CAMEL-10444)

Return header with key CamelMongoDbRecordsAffected from update and remove operations

[CAMEL-10438](https://issues.apache.org/jira/browse/CAMEL-10438)

Java8 DSL for Content Enricher and Aggregator

[CAMEL-10436](https://issues.apache.org/jira/browse/CAMEL-10436)

camel-archetype-spring-boot - Should create JAR not WAR

[CAMEL-10434](https://issues.apache.org/jira/browse/CAMEL-10434)

Camel catalog - Filter karaf / spring boot components

[CAMEL-10426](https://issues.apache.org/jira/browse/CAMEL-10426)

camel-zookeeper - Add Curator based Policy supporting multiple active nodes

[CAMEL-10424](https://issues.apache.org/jira/browse/CAMEL-10424)

Bean should act like transform/setBody when setting result

[CAMEL-10423](https://issues.apache.org/jira/browse/CAMEL-10423)

Introduce XmppDirectProducer

[CAMEL-10421](https://issues.apache.org/jira/browse/CAMEL-10421)

camel-spring-boot - CamelAutoConfiguration should allow to exclude non-singletons

[CAMEL-10419](https://issues.apache.org/jira/browse/CAMEL-10419)

camel-properties : allow to individually set whether to silently ignore a missing location

[CAMEL-10417](https://issues.apache.org/jira/browse/CAMEL-10417)

camel-properties: Support adding location using child nodes of propertyPlaceholder element

[CAMEL-10412](https://issues.apache.org/jira/browse/CAMEL-10412)

Unable to exclude CamelAutoConfiguration in Spring Boot

[CAMEL-10410](https://issues.apache.org/jira/browse/CAMEL-10410)

Karaf features: install camel-karaf-commands and camel-karaf-commands-catalog only if karaf shell is installed

[CAMEL-10408](https://issues.apache.org/jira/browse/CAMEL-10408)

Camel-JMS: Suspending/resuming won't work in case of timeout

[CAMEL-10404](https://issues.apache.org/jira/browse/CAMEL-10404)

Improve spring-boot-example

[CAMEL-10403](https://issues.apache.org/jira/browse/CAMEL-10403)

Camel-Nats: Add TLS Support

[CAMEL-10400](https://issues.apache.org/jira/browse/CAMEL-10400)

Upgrade EasyMock to version 3.4

[CAMEL-10398](https://issues.apache.org/jira/browse/CAMEL-10398)

Avoid NPE when neither of ConnectionResource nor ConnectionFactory is configured

[CAMEL-10397](https://issues.apache.org/jira/browse/CAMEL-10397)

SJMS - Raise an error against InOut+transacted producer as it causes a deadlock

[CAMEL-10395](https://issues.apache.org/jira/browse/CAMEL-10395)

DefaultComponent - Suppress old WARN log that no longer apply

[CAMEL-10393](https://issues.apache.org/jira/browse/CAMEL-10393)

camel-properties: Add an option to disable using default value if a property does not exists

[CAMEL-10392](https://issues.apache.org/jira/browse/CAMEL-10392)

HTTP session handling in Camel routes

[CAMEL-10391](https://issues.apache.org/jira/browse/CAMEL-10391)

Camel-CDI adds every RouteBuilder instance it can find to Camel context

[CAMEL-10390](https://issues.apache.org/jira/browse/CAMEL-10390)

ObjectHelper's after/before/between enhancements

[CAMEL-10389](https://issues.apache.org/jira/browse/CAMEL-10389)

Move string related function from ObjectHelper to StringHelper

[CAMEL-10387](https://issues.apache.org/jira/browse/CAMEL-10387)

JMS correlationIdAsBytes should return null and not byte array with zero values

[CAMEL-10371](https://issues.apache.org/jira/browse/CAMEL-10371)

Add Apache HttpComponents dependencies to BOM

[CAMEL-10369](https://issues.apache.org/jira/browse/CAMEL-10369)

update camel-amqp to use qpid-jms-client-0.11.1

[CAMEL-10356](https://issues.apache.org/jira/browse/CAMEL-10356)

camel-metrics - Add support for gauge type

[CAMEL-10352](https://issues.apache.org/jira/browse/CAMEL-10352)

Optionally delegate to Aries PropertyEvaluator services in BlueprintPropertiesParser

[CAMEL-10345](https://issues.apache.org/jira/browse/CAMEL-10345)

camel-test - Route coverage summary to be logged

[CAMEL-10337](https://issues.apache.org/jira/browse/CAMEL-10337)

camel-asterix - Endpoint should be singleton

[CAMEL-10335](https://issues.apache.org/jira/browse/CAMEL-10335)

Improve Saxon customization

[CAMEL-10323](https://issues.apache.org/jira/browse/CAMEL-10323)

MQTT producer creation fails if network is not available at startup

[CAMEL-10292](https://issues.apache.org/jira/browse/CAMEL-10292)

Move RoutePolicy initialization logic in onStart

[CAMEL-10186](https://issues.apache.org/jira/browse/CAMEL-10186)

camel-spring-boot - Add auto-configuration to components without properties

[CAMEL-10175](https://issues.apache.org/jira/browse/CAMEL-10175)

camel-jetty - Continuation timeout should send back HTTP timeout status code

[CAMEL-10124](https://issues.apache.org/jira/browse/CAMEL-10124)

Karaf commands - Switch to non deprecated

[CAMEL-10027](https://issues.apache.org/jira/browse/CAMEL-10027)

ServiceCall EIP : Support additional attributes in ServiceCallServer

[CAMEL-9965](https://issues.apache.org/jira/browse/CAMEL-9965)

Throw meaningful exception of a streamed body has been consumed already

[CAMEL-9945](https://issues.apache.org/jira/browse/CAMEL-9945)

Upgrade to jetty 9.3

[CAMEL-9678](https://issues.apache.org/jira/browse/CAMEL-9678)

camel-undertow - Keep restarting server when add/remove routes

[CAMEL-9597](https://issues.apache.org/jira/browse/CAMEL-9597)

camel-nagios - Mockito for testing

[CAMEL-9466](https://issues.apache.org/jira/browse/CAMEL-9466)

Camel model - We should be able to know if its a predicate or expression

[CAMEL-9372](https://issues.apache.org/jira/browse/CAMEL-9372)

camel java dsl - Parameters with uris should denote that with an annotation

[CAMEL-9210](https://issues.apache.org/jira/browse/CAMEL-9210)

Make credentials optional in AWS component. Use instance profile if not supplied.

[CAMEL-9047](https://issues.apache.org/jira/browse/CAMEL-9047)

Replace deprecated boxjavalibv2 with box-java-sdk

[CAMEL-8396](https://issues.apache.org/jira/browse/CAMEL-8396)

Update Salesforce component to support new REST APIs in Salesforce API V33.0

[CAMEL-8351](https://issues.apache.org/jira/browse/CAMEL-8351)

Spring-ws consumer ignores breadcrumbId http header

[CAMEL-7972](https://issues.apache.org/jira/browse/CAMEL-7972)

Make the Circuit Breaker EIP more robust - in state halfOpen let only one thread to perform a try

[CAMEL-7862](https://issues.apache.org/jira/browse/CAMEL-7862)

Allow empty csv files in the Camel Bindy unmarshalling process

[CAMEL-7809](https://issues.apache.org/jira/browse/CAMEL-7809)

Quartz PollConsumerScheduler in a cluster tries to create duplicate triggers, fails

[CAMEL-7519](https://issues.apache.org/jira/browse/CAMEL-7519)

camel-bindy - CSV unbinding does not escape embedded quote character

[CAMEL-7413](https://issues.apache.org/jira/browse/CAMEL-7413)

camel-salesforce-maven-plugin should allow to use a custom login URL

[CAMEL-6289](https://issues.apache.org/jira/browse/CAMEL-6289)

camel-example-loan-broker - The broker example should use broker.xml file to setup broker

[CAMEL-5719](https://issues.apache.org/jira/browse/CAMEL-5719)

ZooKeeper route policy should initialize using onInit to elect master

[CAMEL-5716](https://issues.apache.org/jira/browse/CAMEL-5716)

Validator - schema from memory/property

[CAMEL-5231](https://issues.apache.org/jira/browse/CAMEL-5231)

Loading routes from XML files using API on CamelContext should inject custom namespaces

### New Feature (76)

[CAMEL-11136](https://issues.apache.org/jira/browse/CAMEL-11136)

Create PubNub component

[CAMEL-11135](https://issues.apache.org/jira/browse/CAMEL-11135)

camel-protobuf component improvements

[CAMEL-11126](https://issues.apache.org/jira/browse/CAMEL-11126)

camel-connector - Make it easy to schedule a connector

[CAMEL-11118](https://issues.apache.org/jira/browse/CAMEL-11118)

PingCheck : validate rest component

[CAMEL-11062](https://issues.apache.org/jira/browse/CAMEL-11062)

New camel-digitalocean component

[CAMEL-11056](https://issues.apache.org/jira/browse/CAMEL-11056)

Create a new camel-olingo4 component for supporting OData 4.0

[CAMEL-11013](https://issues.apache.org/jira/browse/CAMEL-11013)

Support OAuth 2.0 JWT Bearer Token Flow

[CAMEL-11006](https://issues.apache.org/jira/browse/CAMEL-11006)

Auto generate REST DSL for Camel from Swagger2.0/OAI specification

[CAMEL-10986](https://issues.apache.org/jira/browse/CAMEL-10986)

zookeeper-master - Master component for cluster/slave

[CAMEL-10952](https://issues.apache.org/jira/browse/CAMEL-10952)

Kinesis Firehose support

[CAMEL-10950](https://issues.apache.org/jira/browse/CAMEL-10950)

Enable camel-docker configuration to accept a custom DockerCmdExecFactory

[CAMEL-10932](https://issues.apache.org/jira/browse/CAMEL-10932)

REST Swagger component

[CAMEL-10927](https://issues.apache.org/jira/browse/CAMEL-10927)

Add Kafka topic-based IdempotentRepository

[CAMEL-10925](https://issues.apache.org/jira/browse/CAMEL-10925)

spring-boot - Verify compatibility with latest spring-boot

[CAMEL-10920](https://issues.apache.org/jira/browse/CAMEL-10920)

camel-zipkin - Lookup SpanCollector from registry and support Zipkin Reporter

[CAMEL-10918](https://issues.apache.org/jira/browse/CAMEL-10918)

camel-sjms - JMS 2.0 shared subscriptions

[CAMEL-10915](https://issues.apache.org/jira/browse/CAMEL-10915)

Add type conversion support for java.net.URI

[CAMEL-10901](https://issues.apache.org/jira/browse/CAMEL-10901)

Add support to Kafka consumer to seek to end of topic

[CAMEL-10898](https://issues.apache.org/jira/browse/CAMEL-10898)

camel-catalog - Allow to add custom component/connector by download JAR via maven

[CAMEL-10897](https://issues.apache.org/jira/browse/CAMEL-10897)

camel-jcache - Allow to configure cache provider on component

[CAMEL-10889](https://issues.apache.org/jira/browse/CAMEL-10889)

camel-telegram and html styled messages

[CAMEL-10885](https://issues.apache.org/jira/browse/CAMEL-10885)

Add mask option to log EIP and log component

[CAMEL-10868](https://issues.apache.org/jira/browse/CAMEL-10868)

Create camel-spring-cloud-netflix component

[CAMEL-10865](https://issues.apache.org/jira/browse/CAMEL-10865)

camel catalog - Add catalog for connectors

[CAMEL-10828](https://issues.apache.org/jira/browse/CAMEL-10828)

camel-catalog - Allow to index a maven repo and add new components to the catalog

[CAMEL-10825](https://issues.apache.org/jira/browse/CAMEL-10825)

camel-opentracing component

[CAMEL-10814](https://issues.apache.org/jira/browse/CAMEL-10814)

Example for Camel Kafka Integration

[CAMEL-10804](https://issues.apache.org/jira/browse/CAMEL-10804)

Create a salesforce example

[CAMEL-10795](https://issues.apache.org/jira/browse/CAMEL-10795)

PingCheck API

[CAMEL-10786](https://issues.apache.org/jira/browse/CAMEL-10786)

Create camel-azure component

[CAMEL-10775](https://issues.apache.org/jira/browse/CAMEL-10775)

Add information to components which version they were added to Camel

[CAMEL-10774](https://issues.apache.org/jira/browse/CAMEL-10774)

camel-catalog - Include other kind of camel artifacts

[CAMEL-10766](https://issues.apache.org/jira/browse/CAMEL-10766)

Create a new camel-elasticsearch5 component for supporting ElasticSearch 5.x Java API

[CAMEL-10740](https://issues.apache.org/jira/browse/CAMEL-10740)

Add Tika Component

[CAMEL-10730](https://issues.apache.org/jira/browse/CAMEL-10730)

Camel-Telegram: Support for type "Document"

[CAMEL-10721](https://issues.apache.org/jira/browse/CAMEL-10721)

Camel Connectors

[CAMEL-10719](https://issues.apache.org/jira/browse/CAMEL-10719)

Add ability to manage ThrottlingExceptionRoutePolicy through JMX

[CAMEL-10718](https://issues.apache.org/jira/browse/CAMEL-10718)

Route Policy implements circuit breaker pattern to stop consuming from the endpoint

[CAMEL-10711](https://issues.apache.org/jira/browse/CAMEL-10711)

Consider using add\[Test\]CompileSourceRoot in api component maven plugin

[CAMEL-10696](https://issues.apache.org/jira/browse/CAMEL-10696)

Allow camel-kafka to resume from any offset

[CAMEL-10690](https://issues.apache.org/jira/browse/CAMEL-10690)

Camel-InfluxDB: Support Querying

[CAMEL-10685](https://issues.apache.org/jira/browse/CAMEL-10685)

TransactionErrorHandler and TransactionPolicy for Camel CDI / JavaEE

[CAMEL-10668](https://issues.apache.org/jira/browse/CAMEL-10668)

Hystrix / ServiceCall - Allow to configure global configuration

[CAMEL-10626](https://issues.apache.org/jira/browse/CAMEL-10626)

Add asynchronous support for CXF JAX-RS producers

[CAMEL-10614](https://issues.apache.org/jira/browse/CAMEL-10614)

Camel-Openstack Karaf support

[CAMEL-10612](https://issues.apache.org/jira/browse/CAMEL-10612)

camel-reactive-streams - New component

[CAMEL-10609](https://issues.apache.org/jira/browse/CAMEL-10609)

Simple - Add skip method

[CAMEL-10608](https://issues.apache.org/jira/browse/CAMEL-10608)

Karaf camel:endpoint-list command to list endpoints in all camel contexts

[CAMEL-10599](https://issues.apache.org/jira/browse/CAMEL-10599)

Add watcher to camel:run to reload on routes xml changes

[CAMEL-10596](https://issues.apache.org/jira/browse/CAMEL-10596)

RoutePolicy - To easily stop routes after X messages or time

[CAMEL-10593](https://issues.apache.org/jira/browse/CAMEL-10593)

camel-salesforce: implement support for Composite API batch

[CAMEL-10588](https://issues.apache.org/jira/browse/CAMEL-10588)

Add HTTP proxy config params to camel-servicenow

[CAMEL-10574](https://issues.apache.org/jira/browse/CAMEL-10574)

Create a camel-spring-cloud component

[CAMEL-10561](https://issues.apache.org/jira/browse/CAMEL-10561)

camel-catalog - Add REST JAX-RS application

[CAMEL-10559](https://issues.apache.org/jira/browse/CAMEL-10559)

tooling - route parser for java and xml to parse source code

[CAMEL-10498](https://issues.apache.org/jira/browse/CAMEL-10498)

Update Salesforce component to support approval REST API

[CAMEL-10494](https://issues.apache.org/jira/browse/CAMEL-10494)

Camel-Kubernetes: Consuming events from nodes

[CAMEL-10489](https://issues.apache.org/jira/browse/CAMEL-10489)

Camel-Nats: Add Flush option with timeout

[CAMEL-10472](https://issues.apache.org/jira/browse/CAMEL-10472)

Update Salesforce component to support recent items REST API

[CAMEL-10471](https://issues.apache.org/jira/browse/CAMEL-10471)

Update Salesforce component to support limits REST API

[CAMEL-10447](https://issues.apache.org/jira/browse/CAMEL-10447)

Add contract based type awareness

[CAMEL-10416](https://issues.apache.org/jira/browse/CAMEL-10416)

spring-boot native support for REST DSL and servlet

[CAMEL-10415](https://issues.apache.org/jira/browse/CAMEL-10415)

camel-servlet-starter - Autoconfigure Servlet Endpoint

[CAMEL-10402](https://issues.apache.org/jira/browse/CAMEL-10402)

camel-servicenow : Allow to configure credentials on ServiceNow component

[CAMEL-10401](https://issues.apache.org/jira/browse/CAMEL-10401)

ftp: Allow files to be chmod-ed after being produced

[CAMEL-10354](https://issues.apache.org/jira/browse/CAMEL-10354)

OWASP Dependency Check

[CAMEL-10350](https://issues.apache.org/jira/browse/CAMEL-10350)

New camel-bonita component

[CAMEL-10344](https://issues.apache.org/jira/browse/CAMEL-10344)

RouteIdFactory - That can assign route ids using derived values from uris

[CAMEL-10327](https://issues.apache.org/jira/browse/CAMEL-10327)

New Apache drill component

[CAMEL-10287](https://issues.apache.org/jira/browse/CAMEL-10287)

Infinispan RoutePolicy to have one route being master, and others as slaves

[CAMEL-10265](https://issues.apache.org/jira/browse/CAMEL-10265)

Allow named queries in JPA Producer

[CAMEL-10178](https://issues.apache.org/jira/browse/CAMEL-10178)

Google Cloud PubSub Component

[CAMEL-10160](https://issues.apache.org/jira/browse/CAMEL-10160)

create a zendesk endpoint for creating new issues

[CAMEL-9800](https://issues.apache.org/jira/browse/CAMEL-9800)

Create Spring Boot example with REST DSL and Swagger

[CAMEL-9748](https://issues.apache.org/jira/browse/CAMEL-9748)

Create Openstack Component

[CAMEL-5271](https://issues.apache.org/jira/browse/CAMEL-5271)

camel-snmp should provide a Producer for sending TRAPS/INFORMS

### Sub-task (13)

[CAMEL-11143](https://issues.apache.org/jira/browse/CAMEL-11143)

Create a Maven plugin that creates REST DSL source code from Swagger specification

[CAMEL-11107](https://issues.apache.org/jira/browse/CAMEL-11107)

Create a new camel-grpc component

[CAMEL-11016](https://issues.apache.org/jira/browse/CAMEL-11016)

Add an option in the TarFileDataFormat to let the iterator support the empty directory

[CAMEL-10992](https://issues.apache.org/jira/browse/CAMEL-10992)

Hystrix - Allow to configure global configuration

[CAMEL-10991](https://issues.apache.org/jira/browse/CAMEL-10991)

ServiceCall - Allow to configure global configuration

[CAMEL-10924](https://issues.apache.org/jira/browse/CAMEL-10924)

PingCheck API : Support validation through JMX

[CAMEL-10923](https://issues.apache.org/jira/browse/CAMEL-10923)

PingCheck API: Make camel-catalog aware of what verification scope a component supports

[CAMEL-10877](https://issues.apache.org/jira/browse/CAMEL-10877)

service-call eip : add a spring-cloud example

[CAMEL-10876](https://issues.apache.org/jira/browse/CAMEL-10876)

service-call eip : add a spring-boot example

[CAMEL-10538](https://issues.apache.org/jira/browse/CAMEL-10538)

Add declarative validator according to input/output type

[CAMEL-10532](https://issues.apache.org/jira/browse/CAMEL-10532)

Integrate Transformer with Rest DSL

[CAMEL-10531](https://issues.apache.org/jira/browse/CAMEL-10531)

Introduce fluent builder for Transformer

[CAMEL-10530](https://issues.apache.org/jira/browse/CAMEL-10530)

Introduce TransformerRegistry

### Task (86)

[CAMEL-11192](https://issues.apache.org/jira/browse/CAMEL-11192)

Service Call - Some unused code in camel-core

[CAMEL-11189](https://issues.apache.org/jira/browse/CAMEL-11189)

Upgrade zipkin

[CAMEL-11185](https://issues.apache.org/jira/browse/CAMEL-11185)

Remove camel-scr-starter spring boot module

[CAMEL-11183](https://issues.apache.org/jira/browse/CAMEL-11183)

Checkstyle errors in camel-package-maven-plugin

[CAMEL-11181](https://issues.apache.org/jira/browse/CAMEL-11181)

Replace gmaven with gmavenplus Maven plugin

[CAMEL-11180](https://issues.apache.org/jira/browse/CAMEL-11180)

Place Eclipse workspace setup in camel-etc in a profile

[CAMEL-11172](https://issues.apache.org/jira/browse/CAMEL-11172)

Java 9 - camel-restdsl-swagger-plugin fails integration test and camel-example-kotlin cannot compile

[CAMEL-11169](https://issues.apache.org/jira/browse/CAMEL-11169)

Create camel-example-swagger-spring-boot

[CAMEL-11160](https://issues.apache.org/jira/browse/CAMEL-11160)

Component docs - ascii doc warns

[CAMEL-11150](https://issues.apache.org/jira/browse/CAMEL-11150)

camel-ignite is removed from readme on each full build

[CAMEL-11145](https://issues.apache.org/jira/browse/CAMEL-11145)

Component docs - Fix broken links on github

[CAMEL-11112](https://issues.apache.org/jira/browse/CAMEL-11112)

Make sure streams are closed in camel-catalog

[CAMEL-11101](https://issues.apache.org/jira/browse/CAMEL-11101)

Update CXF dependency to latest version > 3.1.10

[CAMEL-11095](https://issues.apache.org/jira/browse/CAMEL-11095)

Enumerate all OperationName in @UriPath of operationName

[CAMEL-11072](https://issues.apache.org/jira/browse/CAMEL-11072)

Remove non-Maven plugin related executions from Salesforce Maven POM

[CAMEL-11064](https://issues.apache.org/jira/browse/CAMEL-11064)

Add activemq-amqp to parent POM

[CAMEL-11058](https://issues.apache.org/jira/browse/CAMEL-11058)

camel-olingo2 component doesn't support OData 3.0

[CAMEL-11055](https://issues.apache.org/jira/browse/CAMEL-11055)

Ping Check API - Allow to use lower case scopes

[CAMEL-11053](https://issues.apache.org/jira/browse/CAMEL-11053)

camel-undertow - Compile error

[CAMEL-11042](https://issues.apache.org/jira/browse/CAMEL-11042)

Compilation error about spring-cloud-netflix

[CAMEL-11039](https://issues.apache.org/jira/browse/CAMEL-11039)

Ping Check API - Add JMX api on component

[CAMEL-11037](https://issues.apache.org/jira/browse/CAMEL-11037)

Ping Check API - Add javadoc

[CAMEL-11022](https://issues.apache.org/jira/browse/CAMEL-11022)

camel-salesforce - Compile error

[CAMEL-11021](https://issues.apache.org/jira/browse/CAMEL-11021)

Missing javadoc on rest-dsl model

[CAMEL-10990](https://issues.apache.org/jira/browse/CAMEL-10990)

camel-kafka - Add doc for the new idempontent repo

[CAMEL-10977](https://issues.apache.org/jira/browse/CAMEL-10977)

Add a camel-hazelcast example on Kubernetes

[CAMEL-10974](https://issues.apache.org/jira/browse/CAMEL-10974)

Component docs - Show deprecation INFO

[CAMEL-10973](https://issues.apache.org/jira/browse/CAMEL-10973)

Deprecate ruby, python and php scripting languages

[CAMEL-10971](https://issues.apache.org/jira/browse/CAMEL-10971)

Remove camel-catalog karaf commands

[CAMEL-10958](https://issues.apache.org/jira/browse/CAMEL-10958)

camel-scala-starter starter module removed but references to it still exist

[CAMEL-10947](https://issues.apache.org/jira/browse/CAMEL-10947)

camel-box - Karaf and log4j2

[CAMEL-10933](https://issues.apache.org/jira/browse/CAMEL-10933)

camel-guice - Deprecate this module

[CAMEL-10921](https://issues.apache.org/jira/browse/CAMEL-10921)

Add Elasticsearch5 Karaf Feature

[CAMEL-10909](https://issues.apache.org/jira/browse/CAMEL-10909)

deprecate camel-scala and camel-groovy dsl

[CAMEL-10908](https://issues.apache.org/jira/browse/CAMEL-10908)

Introduce DataTypeAware interface and let MessageSupport implement it

[CAMEL-10890](https://issues.apache.org/jira/browse/CAMEL-10890)

Failed test in some http components

[CAMEL-10881](https://issues.apache.org/jira/browse/CAMEL-10881)

Include the Cassandra quickstart from Fabric8 into Camel

[CAMEL-10875](https://issues.apache.org/jira/browse/CAMEL-10875)

service-call eip: add examples

[CAMEL-10872](https://issues.apache.org/jira/browse/CAMEL-10872)

camel-jgroups : upgrade to JGroups 4.0

[CAMEL-10866](https://issues.apache.org/jira/browse/CAMEL-10866)

platforms/catalog - rename folders to match their artifact id name

[CAMEL-10859](https://issues.apache.org/jira/browse/CAMEL-10859)

camel-jasypt - Update docs about JAR dependency to run

[CAMEL-10857](https://issues.apache.org/jira/browse/CAMEL-10857)

Make Salesforce integration tests work with new Salesforce instance

[CAMEL-10824](https://issues.apache.org/jira/browse/CAMEL-10824)

Improve DefaultRuntimeProvider abstraction

[CAMEL-10823](https://issues.apache.org/jira/browse/CAMEL-10823)

Create camel-azure adoc documentation resource

[CAMEL-10796](https://issues.apache.org/jira/browse/CAMEL-10796)

camel-example-spring-boot - Remove shell

[CAMEL-10781](https://issues.apache.org/jira/browse/CAMEL-10781)

Add available from to misc list of components

[CAMEL-10754](https://issues.apache.org/jira/browse/CAMEL-10754)

Camel uses deprecated Dropbox API that will turned off

[CAMEL-10735](https://issues.apache.org/jira/browse/CAMEL-10735)

Mark code as deprecated on 2.x

[CAMEL-10731](https://issues.apache.org/jira/browse/CAMEL-10731)

Create a little example for Camel AWS S3 consumer

[CAMEL-10723](https://issues.apache.org/jira/browse/CAMEL-10723)

Errors in documentation for camel-kinesis

[CAMEL-10693](https://issues.apache.org/jira/browse/CAMEL-10693)

spring-boot: deprecate camel-spring-boot commands

[CAMEL-10676](https://issues.apache.org/jira/browse/CAMEL-10676)

Some javadoc warnings could be easily corrected in camel-sql and camel-http

[CAMEL-10673](https://issues.apache.org/jira/browse/CAMEL-10673)

Expose activemq-mqtt through parent POM

[CAMEL-10656](https://issues.apache.org/jira/browse/CAMEL-10656)

Component ascii docs - Fix conversion to html warnings

[CAMEL-10649](https://issues.apache.org/jira/browse/CAMEL-10649)

Transformers - Add documentation to dsl model

[CAMEL-10647](https://issues.apache.org/jira/browse/CAMEL-10647)

camel-test-karaf - Cause wrong build order

[CAMEL-10637](https://issues.apache.org/jira/browse/CAMEL-10637)

IllegalStateException that is not thrown in IgniteMessagingEndpoint

[CAMEL-10623](https://issues.apache.org/jira/browse/CAMEL-10623)

Camel CXF version not compatible with WildFly CXF

[CAMEL-10622](https://issues.apache.org/jira/browse/CAMEL-10622)

Move spring-boot components starter to platforms/spring-boot/

[CAMEL-10620](https://issues.apache.org/jira/browse/CAMEL-10620)

AMQP documentation out of date?

[CAMEL-10615](https://issues.apache.org/jira/browse/CAMEL-10615)

camel-sjms - BatchConsumer should use exception handler instead of warn log

[CAMEL-10598](https://issues.apache.org/jira/browse/CAMEL-10598)

Upgrade ehcache to 3.2.0

[CAMEL-10583](https://issues.apache.org/jira/browse/CAMEL-10583)

Typo in Camel JSON Documentation

[CAMEL-10566](https://issues.apache.org/jira/browse/CAMEL-10566)

Remove camel-spring-javaconfig from karaf

[CAMEL-10560](https://issues.apache.org/jira/browse/CAMEL-10560)

Add submittedFileName into AttachmentHttpBinding

[CAMEL-10553](https://issues.apache.org/jira/browse/CAMEL-10553)

Invalid links on camel.apache.org/components.html page

[CAMEL-10528](https://issues.apache.org/jira/browse/CAMEL-10528)

Contributing file for Apache Camel

[CAMEL-10521](https://issues.apache.org/jira/browse/CAMEL-10521)

Camel-Rabbitmq: Support RabbitMQ AMQP client 4.x

[CAMEL-10518](https://issues.apache.org/jira/browse/CAMEL-10518)

Fix bad suppress warning named with typo "uncheked"

[CAMEL-10517](https://issues.apache.org/jira/browse/CAMEL-10517)

Remove unnecessary SuppressWarnings

[CAMEL-10516](https://issues.apache.org/jira/browse/CAMEL-10516)

Clean code: remove the 308 import not used

[CAMEL-10508](https://issues.apache.org/jira/browse/CAMEL-10508)

Upgrade Chronicle Engine to v1.13.16

[CAMEL-10502](https://issues.apache.org/jira/browse/CAMEL-10502)

Camel-git : Copy headers from in to out

[CAMEL-10481](https://issues.apache.org/jira/browse/CAMEL-10481)

Camel does not expose cassandra-all any more

[CAMEL-10477](https://issues.apache.org/jira/browse/CAMEL-10477)

\[jruby\] Upgrade to 1.7.26

[CAMEL-10458](https://issues.apache.org/jira/browse/CAMEL-10458)

Upgrade to Spring Boot 1.4.2

[CAMEL-10457](https://issues.apache.org/jira/browse/CAMEL-10457)

Cannot generate javadoc for camel-jms-starter

[CAMEL-10445](https://issues.apache.org/jira/browse/CAMEL-10445)

Upgrade to CXF 3.1.8

[CAMEL-10437](https://issues.apache.org/jira/browse/CAMEL-10437)

Add camel-grape Karaf feature

[CAMEL-10435](https://issues.apache.org/jira/browse/CAMEL-10435)

Move spring-boot-dm to platforms directory

[CAMEL-10422](https://issues.apache.org/jira/browse/CAMEL-10422)

Broken image in Kura doc page

[CAMEL-10379](https://issues.apache.org/jira/browse/CAMEL-10379)

Improved component description

[CAMEL-10375](https://issues.apache.org/jira/browse/CAMEL-10375)

Move camel-couchbase from extra to ASF

[CAMEL-10373](https://issues.apache.org/jira/browse/CAMEL-10373)

camel-spring-boot-starter - Some starters has hibernate-validator

[CAMEL-10367](https://issues.apache.org/jira/browse/CAMEL-10367)

remove extraneous dependency from camel-amqp module

[CAMEL-8418](https://issues.apache.org/jira/browse/CAMEL-8418)

Add documentation to camel-atmos component

### Test (16)

[CAMEL-11154](https://issues.apache.org/jira/browse/CAMEL-11154)

itest - spring-boot fails for camel-hbase

[CAMEL-11153](https://issues.apache.org/jira/browse/CAMEL-11153)

camel-protobuf - itest starts to fail again

[CAMEL-11142](https://issues.apache.org/jira/browse/CAMEL-11142)

camel-undertow-starter - fails test

[CAMEL-11130](https://issues.apache.org/jira/browse/CAMEL-11130)

Jenkins - Camel.trunk.itest.karaf doesn't run all tests in camel-itest-karaf

[CAMEL-11014](https://issues.apache.org/jira/browse/CAMEL-11014)

camel-salesforce - One unit test failing on CI

[CAMEL-10997](https://issues.apache.org/jira/browse/CAMEL-10997)

test errors on master branch

[CAMEL-10989](https://issues.apache.org/jira/browse/CAMEL-10989)

camel-test-blueprint MyMainAppTest is failing

[CAMEL-10960](https://issues.apache.org/jira/browse/CAMEL-10960)

camel-aws - 2 unit test fail

[CAMEL-10945](https://issues.apache.org/jira/browse/CAMEL-10945)

camel-ssh - Unit test fails

[CAMEL-10935](https://issues.apache.org/jira/browse/CAMEL-10935)

camel-restlet - Two unit test fails

[CAMEL-10891](https://issues.apache.org/jira/browse/CAMEL-10891)

ManagedThrottlingExceptionRoutePolicyTest is to flaky on CI server

[CAMEL-10780](https://issues.apache.org/jira/browse/CAMEL-10780)

Add test for DefaultFactoryFinder

[CAMEL-10601](https://issues.apache.org/jira/browse/CAMEL-10601)

camel-mongodb-gridfs - Use dynamic ports for tests

[CAMEL-10536](https://issues.apache.org/jira/browse/CAMEL-10536)

camel-servlet-starter - Test failure

[CAMEL-10523](https://issues.apache.org/jira/browse/CAMEL-10523)

Make Test launchable as JUnit Test from IDEs

[CAMEL-10515](https://issues.apache.org/jira/browse/CAMEL-10515)

86 unit tests are failing on Windows

### Wish (1)

[CAMEL-11019](https://issues.apache.org/jira/browse/CAMEL-11019)

Customise message history dump format

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).