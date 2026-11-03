# Apache camel 3.12.0 Release

## New and Noteworthy

This release is the new Camel 3.12.0 minor release.

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
      <version>3.12.0</version>
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
      <version>3.12.0</version>
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
| [apache-camel-3.12.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.12.0/apache-camel-3.12.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.12.0/apache-camel-3.12.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.12.0/apache-camel-3.12.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.12.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.12.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (66)

[CAMEL-17008](https://issues.apache.org/jira/browse/CAMEL-17008)

okStatusCodeRange does not permit single status code

[CAMEL-17007](https://issues.apache.org/jira/browse/CAMEL-17007)

camel-aws2-lambda: GetAlias is not working

[CAMEL-17004](https://issues.apache.org/jira/browse/CAMEL-17004)

camel-servlet - Should not close HttpServletInputStream when reading body into stream caching

[CAMEL-16990](https://issues.apache.org/jira/browse/CAMEL-16990)

camel-core - Stream caching checking for caused exception can lead to converter problem

[CAMEL-16957](https://issues.apache.org/jira/browse/CAMEL-16957)

NettyHttpHelper appends slash to an URI in case of empty CamelHttpPath

[CAMEL-16936](https://issues.apache.org/jira/browse/CAMEL-16936)

camel-aws2-s3: Not setting CONTENT-MD5 header which breaks putObject with object locks

[CAMEL-16932](https://issues.apache.org/jira/browse/CAMEL-16932)

Configuration properties (AS2Configuration) of an AS2 client endpoint are ignored

[CAMEL-16927](https://issues.apache.org/jira/browse/CAMEL-16927)

camel-spring - Using Spring XML can create multiple SpringCamelContext instances causing a deadlock when multiple camel proxies involved

[CAMEL-16925](https://issues.apache.org/jira/browse/CAMEL-16925)

Integration tests on REST services broken since 3.5.0 with camel-spring-boot

[CAMEL-16924](https://issues.apache.org/jira/browse/CAMEL-16924)

After upgrade to Camel 3.11.0. Cannot write to HttpServletResponse when aggregator is used.

[CAMEL-16923](https://issues.apache.org/jira/browse/CAMEL-16923)

Specifying OpenAPI license & contact info causes a NullPointerException

[CAMEL-16922](https://issues.apache.org/jira/browse/CAMEL-16922)

StringHelper.removeLeadingAndEndingQuotes() may cause IndexOutOfBoundsException

[CAMEL-16921](https://issues.apache.org/jira/browse/CAMEL-16921)

KafkaSpanDecorator sometimes sets the wrong message\_bus.destination tag value

[CAMEL-16920](https://issues.apache.org/jira/browse/CAMEL-16920)

Dump routes does not show uri with endpointdsl

[CAMEL-16918](https://issues.apache.org/jira/browse/CAMEL-16918)

Datasonnet expression fails on first runs in a route called in multicast

[CAMEL-16917](https://issues.apache.org/jira/browse/CAMEL-16917)

more general way to determine if a Spring ApplicationContext is self management ApplicationContext

[CAMEL-16904](https://issues.apache.org/jira/browse/CAMEL-16904)

Camel Swagger API response message headers of type string generate an empty enum even when allowableValues are not specified.

[CAMEL-16903](https://issues.apache.org/jira/browse/CAMEL-16903)

JdbcAggregationRepository not storing properties interfers with AggregateProcessor to restore completiontimeouts

[CAMEL-16902](https://issues.apache.org/jira/browse/CAMEL-16902)

camel-core - WireTap should preserve OUT message when copying

[CAMEL-16895](https://issues.apache.org/jira/browse/CAMEL-16895)

Log masking results in stackoverflow for large inputs

[CAMEL-16893](https://issues.apache.org/jira/browse/CAMEL-16893)

Potential NPE in GrpcStreamingExchangeForwarder

[CAMEL-16892](https://issues.apache.org/jira/browse/CAMEL-16892)

Camel-InfluxDB: Don't check database existence each time we perform a producer operation

[CAMEL-16878](https://issues.apache.org/jira/browse/CAMEL-16878)

using breadcrumbs can cause ClassCastException in MailBinding

[CAMEL-16877](https://issues.apache.org/jira/browse/CAMEL-16877)

camel-salesforce: any salesforce operation inside transaction times out

[CAMEL-16874](https://issues.apache.org/jira/browse/CAMEL-16874)

PollEnrich with file and option sendEmptyMessageWhenIdle keeps sending empty messages

[CAMEL-16865](https://issues.apache.org/jira/browse/CAMEL-16865)

Xtokenize does not track a level up again once it detects a non matching namespace

[CAMEL-16863](https://issues.apache.org/jira/browse/CAMEL-16863)

camel-spring-ws - use wiretap eip will lost the original message body for InOptionalOut MEP

[CAMEL-16857](https://issues.apache.org/jira/browse/CAMEL-16857)

breakOnFirstError causes thread and memory leaks in camel-kafka

[CAMEL-16853](https://issues.apache.org/jira/browse/CAMEL-16853)

camel-xslt: setting resultHandlerFactory via URI is broken

[CAMEL-16850](https://issues.apache.org/jira/browse/CAMEL-16850)

camel-main - Unable to reference properties after bootstrap

[CAMEL-16846](https://issues.apache.org/jira/browse/CAMEL-16846)

camel-kubernetes: missing operation parameter may lead to a NPE

[CAMEL-16843](https://issues.apache.org/jira/browse/CAMEL-16843)

camel-kubernetes: NULL watcher is causing a NPE when stopping the sub-component consumers

[CAMEL-16841](https://issues.apache.org/jira/browse/CAMEL-16841)

camel-kubernetes: NULL watcher is causing a NPE when stopping the configmaps component

[CAMEL-16832](https://issues.apache.org/jira/browse/CAMEL-16832)

camel-kafka - file descriptor leak

[CAMEL-16821](https://issues.apache.org/jira/browse/CAMEL-16821)

camel-bean - BeanProcessor with Process bean does not handle Throwable

[CAMEL-16820](https://issues.apache.org/jira/browse/CAMEL-16820)

camel-core - CircuitBreaker - java.lang.UnsupportedOperationException: Is this really correct

[CAMEL-16818](https://issues.apache.org/jira/browse/CAMEL-16818)

camel-core - route dump dose not print correct route with kamelet eip

[CAMEL-16815](https://issues.apache.org/jira/browse/CAMEL-16815)

OpenTracing with Avro keys causes warning

[CAMEL-16811](https://issues.apache.org/jira/browse/CAMEL-16811)

Cannot consume messages from sjms2 endpoint with deliveryMode set

[CAMEL-16807](https://issues.apache.org/jira/browse/CAMEL-16807)

camel-kafka - problem using two kafka connections in the same application

[CAMEL-16806](https://issues.apache.org/jira/browse/CAMEL-16806)

AWS2 S3 Documentation contains references to obsolete AWS 1 API

[CAMEL-16804](https://issues.apache.org/jira/browse/CAMEL-16804)

NullPointerException when using try-with-resources and MainConfigurationProperties

[CAMEL-16802](https://issues.apache.org/jira/browse/CAMEL-16802)

camel-core - Split / Aggregate with parallelprocessing aggregates in random order

[CAMEL-16796](https://issues.apache.org/jira/browse/CAMEL-16796)

camel-cxf - Problem with inflight message count being -1

[CAMEL-16795](https://issues.apache.org/jira/browse/CAMEL-16795)

camel-file - read-lock fails for minimum length files

[CAMEL-16794](https://issues.apache.org/jira/browse/CAMEL-16794)

camel-core - race condition in LoopProcessor

[CAMEL-16793](https://issues.apache.org/jira/browse/CAMEL-16793)

apiHost option in REST DSL is ignored

[CAMEL-16788](https://issues.apache.org/jira/browse/CAMEL-16788)

camel-kamelet - Local parameters get overridden by environment variable

[CAMEL-16782](https://issues.apache.org/jira/browse/CAMEL-16782)

Getting FailedToCreateProducerException with reason java.util.ConcurrentModificationException randomly when using huge split

[CAMEL-16776](https://issues.apache.org/jira/browse/CAMEL-16776)

camel-test - Dependency injected Endpoint via @EndpointInject should have components autowired eager

[CAMEL-16775](https://issues.apache.org/jira/browse/CAMEL-16775)

camel-core - simple("${body} starts with /startsWith 'xyz'") fails

[CAMEL-16772](https://issues.apache.org/jira/browse/CAMEL-16772)

camel-sjms - Messages not filing to amq if using onCompletion() and transacted=true.

[CAMEL-16767](https://issues.apache.org/jira/browse/CAMEL-16767)

camel-core - Stoping route failed with NPE when route contains loopDoWhile

[CAMEL-16764](https://issues.apache.org/jira/browse/CAMEL-16764)

Box component does not reuse BoxAPIConnection when configured at the component level

[CAMEL-16763](https://issues.apache.org/jira/browse/CAMEL-16763)

camel-sjms - Null JMS Correlation ID using Camel-SJMS Request/Reply with Artemis JMS Client

[CAMEL-16762](https://issues.apache.org/jira/browse/CAMEL-16762)

camel-jms - Only the first payload chunk will be read when using jmsMessageType=Stream

[CAMEL-16761](https://issues.apache.org/jira/browse/CAMEL-16761)

camel-sql - auto-generated primary keys are not retuned for Postgres when using loop iteration

[CAMEL-16755](https://issues.apache.org/jira/browse/CAMEL-16755)

camel-jackson: cannot resolve unmarshal type

[CAMEL-16725](https://issues.apache.org/jira/browse/CAMEL-16725)

camel-jira - Jira newIssues endpoint can fail if an issue was deleted

[CAMEL-16704](https://issues.apache.org/jira/browse/CAMEL-16704)

camel-ahc - Requests getting timed out because the threads assigned to channels are busy

[CAMEL-16692](https://issues.apache.org/jira/browse/CAMEL-16692)

SFTP sometimes doesn't receive all files

[CAMEL-16688](https://issues.apache.org/jira/browse/CAMEL-16688)

HttpComponent : Connection pool shut down

[CAMEL-16594](https://issues.apache.org/jira/browse/CAMEL-16594)

DynamoDB stream updates are missed when there are more than one active shards

[CAMEL-16581](https://issues.apache.org/jira/browse/CAMEL-16581)

quartz - jobs are not interrupted even if requested

[CAMEL-16555](https://issues.apache.org/jira/browse/CAMEL-16555)

JIRA Source Component -- Oauth 401 after time

[CAMEL-14823](https://issues.apache.org/jira/browse/CAMEL-14823)

Support to disable the stream caching in camel-servlet from the camel context - once more

### Dependency upgrade (14)

[CAMEL-17002](https://issues.apache.org/jira/browse/CAMEL-17002)

upgrade to vertx 4.1.4

[CAMEL-16999](https://issues.apache.org/jira/browse/CAMEL-16999)

camel-spring-boot - Update to 2.5.5

[CAMEL-16980](https://issues.apache.org/jira/browse/CAMEL-16980)

Add commons dependency to camel-huaweicloud-smn pom

[CAMEL-16910](https://issues.apache.org/jira/browse/CAMEL-16910)

Update Commons Compress to 1.21

[CAMEL-16890](https://issues.apache.org/jira/browse/CAMEL-16890)

upgrade to kotlin 1.5.30

[CAMEL-16880](https://issues.apache.org/jira/browse/CAMEL-16880)

Upgrade thrift to 0.14.1

[CAMEL-16872](https://issues.apache.org/jira/browse/CAMEL-16872)

Upgrade xchange to 5.0.11

[CAMEL-16856](https://issues.apache.org/jira/browse/CAMEL-16856)

camel-karaf - Add azure-blob-changefeed bundle to the camel-azure-blob-storage feature

[CAMEL-16845](https://issues.apache.org/jira/browse/CAMEL-16845)

Upgrade to test containers 1.16.0

[CAMEL-16799](https://issues.apache.org/jira/browse/CAMEL-16799)

camel-microprofile - Update to newer releases

[CAMEL-16778](https://issues.apache.org/jira/browse/CAMEL-16778)

upgrade to vertx 4.1.1

[CAMEL-16774](https://issues.apache.org/jira/browse/CAMEL-16774)

camel-debezium - Upgrade to 1.6

[CAMEL-16771](https://issues.apache.org/jira/browse/CAMEL-16771)

camel-spring-boot - Upgrade to 2.5.2

[CAMEL-15650](https://issues.apache.org/jira/browse/CAMEL-15650)

Upgrade to apache spark 3.x

### Improvement (64)

[CAMEL-17006](https://issues.apache.org/jira/browse/CAMEL-17006)

rest-dsl - clientRequestValidation should report error 400 if json/xml binding and invalid payload

[CAMEL-17005](https://issues.apache.org/jira/browse/CAMEL-17005)

xml dsl - Avoid having <whenSkipSendToEndpoint> in the XSD

[CAMEL-16995](https://issues.apache.org/jira/browse/CAMEL-16995)

\[camel-karaf\] Support multiple CamelContexts in CamelBlueprintTestSupport

[CAMEL-16991](https://issues.apache.org/jira/browse/CAMEL-16991)

Thread safety with ClientConfigurations object in Huaweicloud components

[CAMEL-16988](https://issues.apache.org/jira/browse/CAMEL-16988)

camel-dataformat - Do not use reflection when configuring dataformats

[CAMEL-16987](https://issues.apache.org/jira/browse/CAMEL-16987)

camel-csv - Allow to configurer header in endpoint uri via dataformat component

[CAMEL-16986](https://issues.apache.org/jira/browse/CAMEL-16986)

camel-openapi-java - Add support for description and example in @Schema annotation

[CAMEL-16981](https://issues.apache.org/jira/browse/CAMEL-16981)

camel-kafka: improve the documentation about consumer streams vs consumers count

[CAMEL-16974](https://issues.apache.org/jira/browse/CAMEL-16974)

camel-kafka: make the resume strategy configurable

[CAMEL-16955](https://issues.apache.org/jira/browse/CAMEL-16955)

camel-huaweicloud-components: rename authenticationKey to accessKey

[CAMEL-16953](https://issues.apache.org/jira/browse/CAMEL-16953)

camel-zip-deflater - Use Commons Compress to be able to un-zip large payloads

[CAMEL-16951](https://issues.apache.org/jira/browse/CAMEL-16951)

yaml dsl - Cannot use expression language options

[CAMEL-16950](https://issues.apache.org/jira/browse/CAMEL-16950)

camel-servlet-starter doesn't support multipart requests

[CAMEL-16947](https://issues.apache.org/jira/browse/CAMEL-16947)

camel-core - Constant language to allow setting result type

[CAMEL-16937](https://issues.apache.org/jira/browse/CAMEL-16937)

SessionExpiryInterval in Mqtt5-Paho-Camel not configurable

[CAMEL-16933](https://issues.apache.org/jira/browse/CAMEL-16933)

Remove jackson-dataformat-xml from camel-openapi-java

[CAMEL-16931](https://issues.apache.org/jira/browse/CAMEL-16931)

Preserve quotes in log mask formatter

[CAMEL-16930](https://issues.apache.org/jira/browse/CAMEL-16930)

Sns2Producer does not handle headers containing numbers

[CAMEL-16915](https://issues.apache.org/jira/browse/CAMEL-16915)

Log masking - Make it easier to add custom key words

[CAMEL-16913](https://issues.apache.org/jira/browse/CAMEL-16913)

camel-core - ConvertBodyTo EIP - Add option to turn off mandatory

[CAMEL-16908](https://issues.apache.org/jira/browse/CAMEL-16908)

camel-core - Log Mask should use the known sensitive keys

[CAMEL-16907](https://issues.apache.org/jira/browse/CAMEL-16907)

camel-jt400 - Program Call usability concerns

[CAMEL-16905](https://issues.apache.org/jira/browse/CAMEL-16905)

camel-mock - Remove old code that checks for header values as Expression/Predicate

[CAMEL-16900](https://issues.apache.org/jira/browse/CAMEL-16900)

camel-core - ExchangeFactory should create exchange with default MEP from its endpoint

[CAMEL-16899](https://issues.apache.org/jira/browse/CAMEL-16899)

camel-jt400 - Documentation or ability to handle parameters returned from RPG program

[CAMEL-16898](https://issues.apache.org/jira/browse/CAMEL-16898)

camel-core - weaveByToUri should match toD EIP

[CAMEL-16897](https://issues.apache.org/jira/browse/CAMEL-16897)

camel-google-sheets - The stream component is not API component

[CAMEL-16891](https://issues.apache.org/jira/browse/CAMEL-16891)

camel-jaxb: avoid using the reflection for SunJaxb21NamespacePrefixMapper

[CAMEL-16889](https://issues.apache.org/jira/browse/CAMEL-16889)

camel-jms - Artemis streaming mode should be supported on producer when using pooled CF

[CAMEL-16883](https://issues.apache.org/jira/browse/CAMEL-16883)

camel-google-pubsub - Support GKE's workload identity

[CAMEL-16882](https://issues.apache.org/jira/browse/CAMEL-16882)

camel-debezium - Add ddl sql output in exchange header to the camel-debezium

[CAMEL-16873](https://issues.apache.org/jira/browse/CAMEL-16873)

Route template parameter are not replaced when dumpRoutesAsXML

[CAMEL-16864](https://issues.apache.org/jira/browse/CAMEL-16864)

camel-core - Mis configuring endpoints should report error if reference lookup is wrongly configured

[CAMEL-16858](https://issues.apache.org/jira/browse/CAMEL-16858)

Enhance SjmsPollingConsumer to take messageSelector option into consideration

[CAMEL-16852](https://issues.apache.org/jira/browse/CAMEL-16852)

Common package for HuaweiCloud components

[CAMEL-16851](https://issues.apache.org/jira/browse/CAMEL-16851)

camel-salesforce: JWT audience value is wrong in some cases

[CAMEL-16844](https://issues.apache.org/jira/browse/CAMEL-16844)

component docs - Tables for component vs endpoint options should have more clear titles

[CAMEL-16830](https://issues.apache.org/jira/browse/CAMEL-16830)

Use GrpcSslContexts.configure for gRPC producer sslContext configuration

[CAMEL-16828](https://issues.apache.org/jira/browse/CAMEL-16828)

Subclasses of ServiceCallConfiguration should not need to be registered for reflection

[CAMEL-16824](https://issues.apache.org/jira/browse/CAMEL-16824)

camel-jpa - Do not lose headers

[CAMEL-16823](https://issues.apache.org/jira/browse/CAMEL-16823)

camel-kamelet - Kamelet EIP should support dynamic endpoints from toD or recipientList

[CAMEL-16822](https://issues.apache.org/jira/browse/CAMEL-16822)

camel-core - CamelContext - getComponentNames should return Set and not List

[CAMEL-16816](https://issues.apache.org/jira/browse/CAMEL-16816)

Change log component throughput counters to long

[CAMEL-16813](https://issues.apache.org/jira/browse/CAMEL-16813)

\[Doc\] RAW function - escape ) character

[CAMEL-16792](https://issues.apache.org/jira/browse/CAMEL-16792)

camel-core - OGNL \`properties\` variable should use \`allProperties\`

[CAMEL-16790](https://issues.apache.org/jira/browse/CAMEL-16790)

camel-pulsar is prone to uneven message distribution with large backlog

[CAMEL-16781](https://issues.apache.org/jira/browse/CAMEL-16781)

camel-json-validator defaults to an old JSON schema version

[CAMEL-16780](https://issues.apache.org/jira/browse/CAMEL-16780)

camel-json-validator does not work with local referenced schema

[CAMEL-16777](https://issues.apache.org/jira/browse/CAMEL-16777)

camel-core - Add constant() overload that adds a trim parameter

[CAMEL-16760](https://issues.apache.org/jira/browse/CAMEL-16760)

camel-core - Dataformat models with Class<?> should use the loaded class directly

[CAMEL-16759](https://issues.apache.org/jira/browse/CAMEL-16759)

camel-core - Kamelet add support for factory method in #class local bean

[CAMEL-16756](https://issues.apache.org/jira/browse/CAMEL-16756)

Improve handling of Vert.x Buffer payloads in platform-http-vertx

[CAMEL-16753](https://issues.apache.org/jira/browse/CAMEL-16753)

camel-main - Split main documentation into categories

[CAMEL-16750](https://issues.apache.org/jira/browse/CAMEL-16750)

Do not propagate exception when concurrent FILE component consumers try to acquire lock in JdbcMessageIdRepository

[CAMEL-16748](https://issues.apache.org/jira/browse/CAMEL-16748)

camel-main - Setting thread pool configuration uses reflection for custom pools

[CAMEL-16747](https://issues.apache.org/jira/browse/CAMEL-16747)

camel-core - Log should show all properties

[CAMEL-16739](https://issues.apache.org/jira/browse/CAMEL-16739)

camel-websocket - Provide connection relative path for routing

[CAMEL-16605](https://issues.apache.org/jira/browse/CAMEL-16605)

camel-zipkin custom tags should be attached to exchange automatically

[CAMEL-16392](https://issues.apache.org/jira/browse/CAMEL-16392)

Camel-Pulsar: Make the client configurable from component parameters

[CAMEL-16374](https://issues.apache.org/jira/browse/CAMEL-16374)

camel-core - OnCompletion - Allow to define onFailure and onComplete on the same onCompletion

[CAMEL-16237](https://issues.apache.org/jira/browse/CAMEL-16237)

camel-http - Allow to easily set user-agent on component level

[CAMEL-16122](https://issues.apache.org/jira/browse/CAMEL-16122)

camel-graphql - Add support for query via body or header

[CAMEL-15864](https://issues.apache.org/jira/browse/CAMEL-15864)

Need way to dynamically set graphql variables

[CAMEL-15663](https://issues.apache.org/jira/browse/CAMEL-15663)

camel-json-validator should return full error message by default

### New Feature (20)

[CAMEL-16983](https://issues.apache.org/jira/browse/CAMEL-16983)

camel-spring-main - Add option to allow multiple camelContext when migrating from legacy Spring XML files

[CAMEL-16979](https://issues.apache.org/jira/browse/CAMEL-16979)

Camel component // Huawei Cloud Image Recognition Service

[CAMEL-16944](https://issues.apache.org/jira/browse/CAMEL-16944)

Camel component // Huawei Cloud Image Recognition Component

[CAMEL-16876](https://issues.apache.org/jira/browse/CAMEL-16876)

Camel Component // Huawei Cloud DMS Component

[CAMEL-16833](https://issues.apache.org/jira/browse/CAMEL-16833)

camel-core - LambdaEndpointRouteBuilder

[CAMEL-16819](https://issues.apache.org/jira/browse/CAMEL-16819)

camel-core - Add support for configurable ExceptionPolicyStrategy in error handler

[CAMEL-16773](https://issues.apache.org/jira/browse/CAMEL-16773)

camel-quartz - ScheduledPollConsumer should support quartz trigger and job parameters

[CAMEL-16770](https://issues.apache.org/jira/browse/CAMEL-16770)

Add support for caching JDBC Idempotent Repository

[CAMEL-16768](https://issues.apache.org/jira/browse/CAMEL-16768)

camel-core - Allow to use BiFunction as AggregationStrategy

[CAMEL-16758](https://issues.apache.org/jira/browse/CAMEL-16758)

Camel Component // Huawei Cloud OBS Component

[CAMEL-16738](https://issues.apache.org/jira/browse/CAMEL-16738)

camel-websocket - Support for websocket subprotocols

[CAMEL-16630](https://issues.apache.org/jira/browse/CAMEL-16630)

camel-core - Route model to allow inlined local beans for XML and other DSLs

[CAMEL-16589](https://issues.apache.org/jira/browse/CAMEL-16589)

\[camel-azure-servicebus\] Create Azure ServiceBus component

[CAMEL-16588](https://issues.apache.org/jira/browse/CAMEL-16588)

\[camel-azure-storage-blob\] Add ChangeFeed support to camel-azure-storage-blob in order to capture blob events

[CAMEL-16379](https://issues.apache.org/jira/browse/CAMEL-16379)

Support for JDK 16

[CAMEL-16088](https://issues.apache.org/jira/browse/CAMEL-16088)

camel-karaf - Create camel-azure-storage-datalake Karaf feature

[CAMEL-15955](https://issues.apache.org/jira/browse/CAMEL-15955)

camel-core - API and SPI for Camel components to resume from offset

[CAMEL-13768](https://issues.apache.org/jira/browse/CAMEL-13768)

camel-kafka: seek to specific offset and KafkaConsumer access

[CAMEL-13590](https://issues.apache.org/jira/browse/CAMEL-13590)

creation of JSON-Patch component

[CAMEL-12879](https://issues.apache.org/jira/browse/CAMEL-12879)

Implement MDC Logging Integration for camel-opentracing Similar to CAMEL-12721

### Sub-task (3)

[CAMEL-16968](https://issues.apache.org/jira/browse/CAMEL-16968)

tests in camel-salesforce failed with JDK17

[CAMEL-16961](https://issues.apache.org/jira/browse/CAMEL-16961)

NettySSLClientCertHeadersTest in camel-netty failed with JDK17

[CAMEL-16959](https://issues.apache.org/jira/browse/CAMEL-16959)

tests in camel-crypto failed with JDK17

### Task (29)

[CAMEL-17003](https://issues.apache.org/jira/browse/CAMEL-17003)

camel-core - doc changes and website build error

[CAMEL-16993](https://issues.apache.org/jira/browse/CAMEL-16993)

camel-kafka: update migration guide

[CAMEL-16989](https://issues.apache.org/jira/browse/CAMEL-16989)

Spring-redis: Add header constans to the doc

[CAMEL-16949](https://issues.apache.org/jira/browse/CAMEL-16949)

camel-kafka: investigate alternatives to remove Thread.sleep from the record fetcher

[CAMEL-16935](https://issues.apache.org/jira/browse/CAMEL-16935)

camel-main and camel-base-engine both exports org.apache.camel.main package

[CAMEL-16928](https://issues.apache.org/jira/browse/CAMEL-16928)

camel-kafka: usage of deprecated method may cause Camel to block indefinitely

[CAMEL-16914](https://issues.apache.org/jira/browse/CAMEL-16914)

camel-kafka: possible corruption of idempotency messages when using KafkaIdempotentRepository

[CAMEL-16885](https://issues.apache.org/jira/browse/CAMEL-16885)

Camel-Json-Patch: Create SB Starter

[CAMEL-16884](https://issues.apache.org/jira/browse/CAMEL-16884)

Camel-Json-Patch: Create Karaf feature

[CAMEL-16881](https://issues.apache.org/jira/browse/CAMEL-16881)

camel-catalog - Remove the documentation files (adoc) as they are not in use

[CAMEL-16869](https://issues.apache.org/jira/browse/CAMEL-16869)

camel-dozer - deprecate the dozer type converter

[CAMEL-16867](https://issues.apache.org/jira/browse/CAMEL-16867)

upgrade to maven wrapper 3.8.2

[CAMEL-16854](https://issues.apache.org/jira/browse/CAMEL-16854)

Component docs -- generate tables from json during website build

[CAMEL-16847](https://issues.apache.org/jira/browse/CAMEL-16847)

camel-kubernetes: upgrade client version

[CAMEL-16842](https://issues.apache.org/jira/browse/CAMEL-16842)

camel-jbang - Cannot build on JDK8

[CAMEL-16840](https://issues.apache.org/jira/browse/CAMEL-16840)

camel-cloud - The generated configurer for kubernetes, consul etc jumps between List and String

[CAMEL-16838](https://issues.apache.org/jira/browse/CAMEL-16838)

camel-kubernetes: configmap documentation refers to invalid query parameters

[CAMEL-16831](https://issues.apache.org/jira/browse/CAMEL-16831)

Upgrade to apache 24 parent in pon.xml

[CAMEL-16817](https://issues.apache.org/jira/browse/CAMEL-16817)

camel-karaf - Error building with maven 3.8.1

[CAMEL-16803](https://issues.apache.org/jira/browse/CAMEL-16803)

remove unnecessary dependency from JDK9+ profile

[CAMEL-16798](https://issues.apache.org/jira/browse/CAMEL-16798)

JdbcCachedMessageIdempotentRepository broken on case changing SQL implementations

[CAMEL-16786](https://issues.apache.org/jira/browse/CAMEL-16786)

JARs with missing label

[CAMEL-16765](https://issues.apache.org/jira/browse/CAMEL-16765)

Update Camel K Serverless api examples to not use --property-file

[CAMEL-16752](https://issues.apache.org/jira/browse/CAMEL-16752)

camel-spring feature should install camel-spring-xml bundle

[CAMEL-16421](https://issues.apache.org/jira/browse/CAMEL-16421)

component summary doc - Move the camel-xxx-summary.adoc to parent folder

[CAMEL-16184](https://issues.apache.org/jira/browse/CAMEL-16184)

camel-test - Deprecate junit 4.x test modules

[CAMEL-15939](https://issues.apache.org/jira/browse/CAMEL-15939)

camel-website - Remove old FAQs

[CAMEL-13215](https://issues.apache.org/jira/browse/CAMEL-13215)

camel-kafka -consumerCount vs consumerStreams problem with pool size

[CAMEL-12671](https://issues.apache.org/jira/browse/CAMEL-12671)

camel-iec60870 - Add documentation for missing field

### Test (8)

[CAMEL-16954](https://issues.apache.org/jira/browse/CAMEL-16954)

Some camel-spring-cloud tests fail with ClassNotFoundException

[CAMEL-16939](https://issues.apache.org/jira/browse/CAMEL-16939)

XPathTransformTest only check JDK ea version when it's 16-ea

[CAMEL-16911](https://issues.apache.org/jira/browse/CAMEL-16911)

The test case SpringJacksonJsonDataFormatTest fails

[CAMEL-16886](https://issues.apache.org/jira/browse/CAMEL-16886)

NewCommentsConsumerTest#singleIssueCommentsTest fails intermitently

[CAMEL-16839](https://issues.apache.org/jira/browse/CAMEL-16839)

camel-kubernetes: some tests are failing

[CAMEL-16814](https://issues.apache.org/jira/browse/CAMEL-16814)

camel-jms - a testcase to demonstrate that Messages filing to amq if using onCompletion() and transacted=true.

[CAMEL-16784](https://issues.apache.org/jira/browse/CAMEL-16784)

camel-ftp - Disable some FTP tests

[CAMEL-15696](https://issues.apache.org/jira/browse/CAMEL-15696)

Spark tests fail with CAMEL\_SPARK\_HIVE\_TESTS=true

### Wish (1)

[CAMEL-16388](https://issues.apache.org/jira/browse/CAMEL-16388)

camel-salesforce: drop support for XML as a serialization format

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).