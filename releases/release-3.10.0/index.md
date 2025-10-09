# Apache camel 3.10.0 Release

## New and Noteworthy

This release is the new Camel 3.10.0 minor release.

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
      <version>3.10.0</version>
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
      <version>3.10.0</version>
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
| [apache-camel-3.10.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.10.0/apache-camel-3.10.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.10.0/apache-camel-3.10.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.10.0/apache-camel-3.10.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.10.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.10.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (66)

[CAMEL-16761](https://issues.apache.org/jira/browse/CAMEL-16761)

camel-sql - auto-generated primary keys are not retuned for Postgres when using loop iteration

[CAMEL-16721](https://issues.apache.org/jira/browse/CAMEL-16721)

Issue with camel-google-pubsub-kafka-connector sink configuration

[CAMEL-16617](https://issues.apache.org/jira/browse/CAMEL-16617)

camel-core - Splitter may log WARN about splitter closed

[CAMEL-16604](https://issues.apache.org/jira/browse/CAMEL-16604)

camel-kamelet - YAML DSL: Specify an option as optional results in a mandatory option

[CAMEL-16587](https://issues.apache.org/jira/browse/CAMEL-16587)

camel-openstack - Cannot create ObjectStore V3 Client

[CAMEL-16586](https://issues.apache.org/jira/browse/CAMEL-16586)

camel-aws2-sns: messages for different endpoints are published to the same topic

[CAMEL-16582](https://issues.apache.org/jira/browse/CAMEL-16582)

camel-mail - Error Marshal mimeMultipart() with attachments

[CAMEL-16574](https://issues.apache.org/jira/browse/CAMEL-16574)

camel-salesforce - NPE On Response Callback - DefaultCompositeApiClient

[CAMEL-16569](https://issues.apache.org/jira/browse/CAMEL-16569)

camel-kamelet don't check for duplicate id routes during route creation from a template

[CAMEL-16567](https://issues.apache.org/jira/browse/CAMEL-16567)

Mocking of consul producers fails

[CAMEL-16566](https://issues.apache.org/jira/browse/CAMEL-16566)

camel-core - Nested enrich with shareUnitOfWork=true result in ConcurrentModificationException

[CAMEL-16559](https://issues.apache.org/jira/browse/CAMEL-16559)

camel-consul - Consul catalog action "LIST\_SERVICES" calls CatalogClient.getNodes

[CAMEL-16556](https://issues.apache.org/jira/browse/CAMEL-16556)

Multiple AtlasMap endpoints may overwrite each others' propertiesFiles

[CAMEL-16551](https://issues.apache.org/jira/browse/CAMEL-16551)

property placeholder not resolved in .marshal() and .unmarshal() DSL statements

[CAMEL-16550](https://issues.apache.org/jira/browse/CAMEL-16550)

camel-core - Split and Aggregate with Transacted may cause thread to stuck

[CAMEL-16547](https://issues.apache.org/jira/browse/CAMEL-16547)

camel-kamelet don't bind properties in this form: \`camel.component.kamelet.template-properties\[templateId\]\`

[CAMEL-16536](https://issues.apache.org/jira/browse/CAMEL-16536)

digitalocean: supress deprecated getOut

[CAMEL-16534](https://issues.apache.org/jira/browse/CAMEL-16534)

camel-core - Multiple doTry ..doCatch in Java DSL - issue setting outer doCatch blocks

[CAMEL-16530](https://issues.apache.org/jira/browse/CAMEL-16530)

AWS2-S3 component does not recognize or use proxy-host and proxy-port from application.properties

[CAMEL-16529](https://issues.apache.org/jira/browse/CAMEL-16529)

Kubernetes Custom Resources - listCustomResourcesByLabels returns all resources

[CAMEL-16527](https://issues.apache.org/jira/browse/CAMEL-16527)

Unable to disable component or endpoint autowiring with camel-main

[CAMEL-16526](https://issues.apache.org/jira/browse/CAMEL-16526)

Unreachable consul leads to NPE in CombinedServiceDiscovery

[CAMEL-16525](https://issues.apache.org/jira/browse/CAMEL-16525)

camel-core - FluentProducerTemplate - Thread safety issue

[CAMEL-16516](https://issues.apache.org/jira/browse/CAMEL-16516)

camel-salesforce - Maven plugin generated code AbstractDescribedSObjectBase can cause NPE

[CAMEL-16515](https://issues.apache.org/jira/browse/CAMEL-16515)

camel-github component possible OOM due to only adding elements to an unbuonded map

[CAMEL-16507](https://issues.apache.org/jira/browse/CAMEL-16507)

Camel-sql: Body for empty ResultSet no longer null when using outputType selectOne

[CAMEL-16503](https://issues.apache.org/jira/browse/CAMEL-16503)

\[camel-spring-xml\] Unresolved camel.spring.version in the generated spring.handlers and spring.schema

[CAMEL-16500](https://issues.apache.org/jira/browse/CAMEL-16500)

Unable to autowire KafkaClientFactory

[CAMEL-16498](https://issues.apache.org/jira/browse/CAMEL-16498)

Camel-Azure-Storage-queue consumer doesn't work

[CAMEL-16490](https://issues.apache.org/jira/browse/CAMEL-16490)

YAML DSL tod is no longer recognized (requires to-d)

[CAMEL-16489](https://issues.apache.org/jira/browse/CAMEL-16489)

YAML DSL is sensitive to key ordering

[CAMEL-16480](https://issues.apache.org/jira/browse/CAMEL-16480)

Simple expression behavior change after 3.4->3.7 migration

[CAMEL-16476](https://issues.apache.org/jira/browse/CAMEL-16476)

camel-core - XML DSL loader issue with doTry doCatch

[CAMEL-16472](https://issues.apache.org/jira/browse/CAMEL-16472)

kamelet: aggregation kamelet not wired properly

[CAMEL-16459](https://issues.apache.org/jira/browse/CAMEL-16459)

jsonpath: If used after platform-http-vertx, it causes PathNotFoundException

[CAMEL-16453](https://issues.apache.org/jira/browse/CAMEL-16453)

camel-zipkin - Incorrect spans created when using parallelProcessing with recipientList or multicast

[CAMEL-16447](https://issues.apache.org/jira/browse/CAMEL-16447)

camel-salesforce - Error in parsing some fields in AbstractSObjectBase

[CAMEL-16442](https://issues.apache.org/jira/browse/CAMEL-16442)

camel-spring-boot - Classpath discovery using wildcards for xml-io-dsl does not work

[CAMEL-16439](https://issues.apache.org/jira/browse/CAMEL-16439)

camel-couchbase : Timeout with Get and Remove operations

[CAMEL-16438](https://issues.apache.org/jira/browse/CAMEL-16438)

Kafka component properties randomly end up under camel.component.kafka or camel.component.kafka.configuration

[CAMEL-16423](https://issues.apache.org/jira/browse/CAMEL-16423)

Camel-Minio converts any body consumed to String

[CAMEL-16418](https://issues.apache.org/jira/browse/CAMEL-16418)

LEAK: ByteBuf.release() results when using circuit breaker with netty http producer

[CAMEL-16413](https://issues.apache.org/jira/browse/CAMEL-16413)

\[camel-kafka\] Avoid committing offsets onPartitionsRevoked during shutdown when autoCommitOnStop is "none"

[CAMEL-16412](https://issues.apache.org/jira/browse/CAMEL-16412)

camel-core - Environment Variables in Properties Source location no longer works

[CAMEL-16410](https://issues.apache.org/jira/browse/CAMEL-16410)

camel-zipfile - Unmarshal ZIP without error handling in Camel 3.8.0 when using split

[CAMEL-16407](https://issues.apache.org/jira/browse/CAMEL-16407)

camel-salesforce: SalesforceLoginConfig values are null

[CAMEL-16401](https://issues.apache.org/jira/browse/CAMEL-16401)

Ensure Route Templates inherit the error handler from the RouteBuilder

[CAMEL-16396](https://issues.apache.org/jira/browse/CAMEL-16396)

Configuring an interval and failure threshold for a health check does not work in all cases

[CAMEL-16393](https://issues.apache.org/jira/browse/CAMEL-16393)

camel-jsonpath - results from $.concat(...) seems to be cached on following calls

[CAMEL-16378](https://issues.apache.org/jira/browse/CAMEL-16378)

Camel MDC - Not propagating custom keys when using Split with Parallel Processing

[CAMEL-16377](https://issues.apache.org/jira/browse/CAMEL-16377)

camel-core - Recipient List EIP - Failed to create Producer for endpoint - NPE in ServicePool

[CAMEL-16316](https://issues.apache.org/jira/browse/CAMEL-16316)

ProducerTemplate asyncSend is not thread safe

[CAMEL-16242](https://issues.apache.org/jira/browse/CAMEL-16242)

camel-core - Route templates and the ONiel problem

[CAMEL-16197](https://issues.apache.org/jira/browse/CAMEL-16197)

CXF Attachment stay in file system after processing if file attachments has not been used

[CAMEL-16180](https://issues.apache.org/jira/browse/CAMEL-16180)

Camel mail fails after some time running

[CAMEL-16025](https://issues.apache.org/jira/browse/CAMEL-16025)

\[camel-mongodb\] ChangeStreams: Exception not gracefully handled

[CAMEL-16015](https://issues.apache.org/jira/browse/CAMEL-16015)

SFTP to file with local work directory is not using rename

[CAMEL-15750](https://issues.apache.org/jira/browse/CAMEL-15750)

camel-undertow-spring-security-starter always forbidden

[CAMEL-15410](https://issues.apache.org/jira/browse/CAMEL-15410)

REST endpoint has inconsistent URL Encoding

[CAMEL-13374](https://issues.apache.org/jira/browse/CAMEL-13374)

XMLTokenExpressionIterator Default Exchange charset overrides original xml encoding from InputStream

[CAMEL-13092](https://issues.apache.org/jira/browse/CAMEL-13092)

Gzipping HTTP response prevents writing chunked output

[CAMEL-13047](https://issues.apache.org/jira/browse/CAMEL-13047)

Validator Component Fails on XSD with file Relative Imports or include

[CAMEL-12764](https://issues.apache.org/jira/browse/CAMEL-12764)

camel-http4: basic auth no longer working when used in combination with a dynamic to

[CAMEL-12472](https://issues.apache.org/jira/browse/CAMEL-12472)

Downloading a large file with streamDownload and stepwise hangs

[CAMEL-12078](https://issues.apache.org/jira/browse/CAMEL-12078)

MIME-Mutipart DataFormat reads attachment DataSource twice

[CAMEL-11846](https://issues.apache.org/jira/browse/CAMEL-11846)

xtokenize and apply xslt to a string does not work with UTF-16BE

### Dependency upgrade (6)

[CAMEL-16601](https://issues.apache.org/jira/browse/CAMEL-16601)

kotlin-dsl - Upgrade to kotlin 1.5.0

[CAMEL-16531](https://issues.apache.org/jira/browse/CAMEL-16531)

camel-kafka - Kafka 2.8 release without zookeeper

[CAMEL-16492](https://issues.apache.org/jira/browse/CAMEL-16492)

camel-jackson - Upgrade to 2.12.3

[CAMEL-16473](https://issues.apache.org/jira/browse/CAMEL-16473)

camel-debezium - Upgrade to 1.5

[CAMEL-16434](https://issues.apache.org/jira/browse/CAMEL-16434)

Upgrade to CXF 3.4.3

[CAMEL-16416](https://issues.apache.org/jira/browse/CAMEL-16416)

Camel-DJL: Upgrade to Deep Java Library 0.10.0

### Improvement (75)

[CAMEL-16614](https://issues.apache.org/jira/browse/CAMEL-16614)

camel-core - Generated type converter should be CamelContextAware

[CAMEL-16610](https://issues.apache.org/jira/browse/CAMEL-16610)

Kamelet local bean - Using script should memorize so when using the bean multiple times its the same local bean

[CAMEL-16609](https://issues.apache.org/jira/browse/CAMEL-16609)

rest dsl - Add more security models for JWT bearer tokens etc

[CAMEL-16608](https://issues.apache.org/jira/browse/CAMEL-16608)

Kamelet local bean - Using script should allow to define return type of created bean

[CAMEL-16607](https://issues.apache.org/jira/browse/CAMEL-16607)

RouteTemplateBeanDefinition : add suport for #type and #class languages

[CAMEL-16606](https://issues.apache.org/jira/browse/CAMEL-16606)

rest dsl - Allow specifying security requirement(s) applicable to entire API

[CAMEL-16595](https://issues.apache.org/jira/browse/CAMEL-16595)

camel-openstack - Ability to filter by path in Swift getAll

[CAMEL-16591](https://issues.apache.org/jira/browse/CAMEL-16591)

Undocumented Bindy Feature

[CAMEL-16590](https://issues.apache.org/jira/browse/CAMEL-16590)

Kamelet local bean - Bind bean as templateBean to make it part of the spec

[CAMEL-16580](https://issues.apache.org/jira/browse/CAMEL-16580)

Remove deprecated code from MLLP component

[CAMEL-16575](https://issues.apache.org/jira/browse/CAMEL-16575)

camel-core - Lookup bean if value is Supplier then lazy eval

[CAMEL-16572](https://issues.apache.org/jira/browse/CAMEL-16572)

camel-spring-jdbc - Make camel-jdbc springless again

[CAMEL-16571](https://issues.apache.org/jira/browse/CAMEL-16571)

camel-core - @Consume annotation should not be marked for constructor injection

[CAMEL-16568](https://issues.apache.org/jira/browse/CAMEL-16568)

camel-activemq - Add destination options to endpoint options

[CAMEL-16561](https://issues.apache.org/jira/browse/CAMEL-16561)

camel-consul - Support agentClient.register

[CAMEL-16560](https://issues.apache.org/jira/browse/CAMEL-16560)

Consider empty string in clientRequestValidation for REST HTTP body

[CAMEL-16554](https://issues.apache.org/jira/browse/CAMEL-16554)

Add support for OpenSSH keys and encrypted OpenSSH keys

[CAMEL-16552](https://issues.apache.org/jira/browse/CAMEL-16552)

camel-spring-boot - Configuring route templates trouble setting route id when using spring yaml configuration

[CAMEL-16548](https://issues.apache.org/jira/browse/CAMEL-16548)

camel-core - Dump route as xml (customId false)

[CAMEL-16545](https://issues.apache.org/jira/browse/CAMEL-16545)

camel-core - ModelDumper to XML output is with doubling empty lines

[CAMEL-16541](https://issues.apache.org/jira/browse/CAMEL-16541)

Camel-Solr: Add autocommit option

[CAMEL-16533](https://issues.apache.org/jira/browse/CAMEL-16533)

camel-spring - XML DSL include more documentation in XSD

[CAMEL-16523](https://issues.apache.org/jira/browse/CAMEL-16523)

camel-github - Add option for commit consumer to poll from starting sha or from start

[CAMEL-16520](https://issues.apache.org/jira/browse/CAMEL-16520)

camel-spring-boot - Auto configuration options for cloud and cluster should not clash with component

[CAMEL-16514](https://issues.apache.org/jira/browse/CAMEL-16514)

Add an option to camel-github component to start gathering data from the beginning of repository history

[CAMEL-16513](https://issues.apache.org/jira/browse/CAMEL-16513)

Camel-Azure-Storage-Queue: Don't create queue automatically by default

[CAMEL-16512](https://issues.apache.org/jira/browse/CAMEL-16512)

Camel-Azure components: mark the clients as autowired

[CAMEL-16511](https://issues.apache.org/jira/browse/CAMEL-16511)

camel-rabbitmq - Make args(query parameter) bean arguments reusable

[CAMEL-16510](https://issues.apache.org/jira/browse/CAMEL-16510)

YAML Dsl : support for Kamelet EIP

[CAMEL-16504](https://issues.apache.org/jira/browse/CAMEL-16504)

YAML Dsl : support for "flow" like route definition

[CAMEL-16497](https://issues.apache.org/jira/browse/CAMEL-16497)

camel-kamelet - Use shorter UUIDs in created route ids

[CAMEL-16494](https://issues.apache.org/jira/browse/CAMEL-16494)

After VetoCamelContextStartException CamelContext instance broken forever

[CAMEL-16491](https://issues.apache.org/jira/browse/CAMEL-16491)

digitalocean: when finding a volume by name, bug while selecting the first element of the list

[CAMEL-16486](https://issues.apache.org/jira/browse/CAMEL-16486)

camel-yaml-dsl-deserializers ErrorHandlerBuilder can parse only Ref

[CAMEL-16481](https://issues.apache.org/jira/browse/CAMEL-16481)

camel-vertx-kafka set custom timestamp

[CAMEL-16477](https://issues.apache.org/jira/browse/CAMEL-16477)

camel-core - ProcessorDefinitionHelper: ruturn a collection instead of an iterator for filterTypeInOutputs methods

[CAMEL-16474](https://issues.apache.org/jira/browse/CAMEL-16474)

camel-azure - Blob consumer should extend scheduled endpoint

[CAMEL-16471](https://issues.apache.org/jira/browse/CAMEL-16471)

camel-huaweicloud-smn // Need URL based client initialization support

[CAMEL-16470](https://issues.apache.org/jira/browse/CAMEL-16470)

Problem when using multiple EntityManagerFactories for different datasources in the same route

[CAMEL-16462](https://issues.apache.org/jira/browse/CAMEL-16462)

camel-core - Optimize RecipientList EIP for default delimiter usage

[CAMEL-16460](https://issues.apache.org/jira/browse/CAMEL-16460)

The Content-Language of CxfRsProducer should be configurable

[CAMEL-16458](https://issues.apache.org/jira/browse/CAMEL-16458)

camel-core - Optimize Enrich and Poll Enrich EIP

[CAMEL-16457](https://issues.apache.org/jira/browse/CAMEL-16457)

camel-core - Optimize ExchangeHelper.copyResults - No need to copy message id not in use

[CAMEL-16455](https://issues.apache.org/jira/browse/CAMEL-16455)

camel-core - Optimize CircuitBreaker EIP with task pooling

[CAMEL-16454](https://issues.apache.org/jira/browse/CAMEL-16454)

camel-core - Optimize CircuitBreaker constants for fast exchange properties

[CAMEL-16450](https://issues.apache.org/jira/browse/CAMEL-16450)

camel-core - Optimize WireTap

[CAMEL-16449](https://issues.apache.org/jira/browse/CAMEL-16449)

camel-cloud - Make Exchange available to ServiceFilter

[CAMEL-16448](https://issues.apache.org/jira/browse/CAMEL-16448)

camel-spring-boot - Allow to define static service discovery with metadata from yml

[CAMEL-16444](https://issues.apache.org/jira/browse/CAMEL-16444)

camel-core - Optimize endpoint lookup

[CAMEL-16441](https://issues.apache.org/jira/browse/CAMEL-16441)

camel-core - Optimize EndpointKey can be NormalizedUri

[CAMEL-16440](https://issues.apache.org/jira/browse/CAMEL-16440)

camel-main - Main configurations - Add default values for tooling

[CAMEL-16433](https://issues.apache.org/jira/browse/CAMEL-16433)

avoid using deprecated CXF LogFeature and LoggingInterceptors

[CAMEL-16432](https://issues.apache.org/jira/browse/CAMEL-16432)

camel-catalog - Validate jsonpath language

[CAMEL-16414](https://issues.apache.org/jira/browse/CAMEL-16414)

camel-kafka set custom timestamp

[CAMEL-16408](https://issues.apache.org/jira/browse/CAMEL-16408)

camel-undertow - http producer includes CamelHttpMethod header

[CAMEL-16400](https://issues.apache.org/jira/browse/CAMEL-16400)

separate unit and integration tests

[CAMEL-16397](https://issues.apache.org/jira/browse/CAMEL-16397)

camel-jsonpath - Use JsonPath that allows to turn on|off caching

[CAMEL-16395](https://issues.apache.org/jira/browse/CAMEL-16395)

Unpredictable behaviour of camel main routes health check configuration

[CAMEL-16391](https://issues.apache.org/jira/browse/CAMEL-16391)

Deprecate and remove redundant code from camel-microprofile-health

[CAMEL-16384](https://issues.apache.org/jira/browse/CAMEL-16384)

camel-spring - BridgePropertyPlaceholderConfigurer should be LoadablePropertiesSource

[CAMEL-16383](https://issues.apache.org/jira/browse/CAMEL-16383)

camel-scheduler - ConcurrentTasks option vs core pool size

[CAMEL-16366](https://issues.apache.org/jira/browse/CAMEL-16366)

complex components to support exchange pooling

[CAMEL-16365](https://issues.apache.org/jira/browse/CAMEL-16365)

Support ecdsa-sha2-\* and ssh-ed25519 algorithms in camel-ssh

[CAMEL-16353](https://issues.apache.org/jira/browse/CAMEL-16353)

camel-core - Force eager classloading in build phase

[CAMEL-16350](https://issues.apache.org/jira/browse/CAMEL-16350)

camel-coap - Rename the names with plus sign

[CAMEL-16266](https://issues.apache.org/jira/browse/CAMEL-16266)

camel-ftp - Allow to configure KEX (key exchange protocol) in SFTP

[CAMEL-16260](https://issues.apache.org/jira/browse/CAMEL-16260)

camel-core - PooledExchange for PollingConsumer

[CAMEL-16230](https://issues.apache.org/jira/browse/CAMEL-16230)

Placeholders not Working with CamelSpringBootTest and AdviceWith

[CAMEL-16185](https://issues.apache.org/jira/browse/CAMEL-16185)

aws s3: improve multipart support

[CAMEL-16119](https://issues.apache.org/jira/browse/CAMEL-16119)

Update vertx to version 4.x

[CAMEL-16060](https://issues.apache.org/jira/browse/CAMEL-16060)

camel-kafka - decouple kafka.PARTITION\_KEY from kafka.KEY

[CAMEL-16028](https://issues.apache.org/jira/browse/CAMEL-16028)

Upgrade to MicroProfile 4

[CAMEL-15503](https://issues.apache.org/jira/browse/CAMEL-15503)

camel-openapi-java - Schema Definitions not generating correctly

[CAMEL-15158](https://issues.apache.org/jira/browse/CAMEL-15158)

camel-openapi-java - Support Description of Request and Response Bodies

[CAMEL-11565](https://issues.apache.org/jira/browse/CAMEL-11565)

Modular DefaultCamelContext in terms of loading and starting routes

### New Feature (32)

[CAMEL-16615](https://issues.apache.org/jira/browse/CAMEL-16615)

Create Jackson based dataformats for Avro and Protobuf

[CAMEL-16603](https://issues.apache.org/jira/browse/CAMEL-16603)

camel-spring-boot - Add starters for kamelet

[CAMEL-16600](https://issues.apache.org/jira/browse/CAMEL-16600)

camel-yaml-dsl - Support route-template bean factory

[CAMEL-16597](https://issues.apache.org/jira/browse/CAMEL-16597)

Kamelets local bean - bean language to support rtc as root object

[CAMEL-16596](https://issues.apache.org/jira/browse/CAMEL-16596)

camel-core - ScriptLanguage SPI

[CAMEL-16593](https://issues.apache.org/jira/browse/CAMEL-16593)

Kamelets local bean - Allow to use expression language to supply the bean

[CAMEL-16584](https://issues.apache.org/jira/browse/CAMEL-16584)

YAML Dsl : support for route template

[CAMEL-16577](https://issues.apache.org/jira/browse/CAMEL-16577)

camel-splunk-hec - Add support for setting the timestamp on events

[CAMEL-16570](https://issues.apache.org/jira/browse/CAMEL-16570)

kameletes: make it possible to discover kamelets at runtime

[CAMEL-16562](https://issues.apache.org/jira/browse/CAMEL-16562)

Stale docs paragraph about org.apache.camel.component.bean.BeanInvocation

[CAMEL-16558](https://issues.apache.org/jira/browse/CAMEL-16558)

openapi - Mark an endpoint as deprecated with camel-swagger-java or camel-openapi-java

[CAMEL-16557](https://issues.apache.org/jira/browse/CAMEL-16557)

Catalog: add a free form key value map on components, dataformats, languages, etc

[CAMEL-16546](https://issues.apache.org/jira/browse/CAMEL-16546)

Camel-Solr: Support Map as body while inserting, updating etc.

[CAMEL-16544](https://issues.apache.org/jira/browse/CAMEL-16544)

Camel-Solr: Support Query natively as producer operation

[CAMEL-16540](https://issues.apache.org/jira/browse/CAMEL-16540)

camel-splunk - Include options to only send message body or headers

[CAMEL-16539](https://issues.apache.org/jira/browse/CAMEL-16539)

splunk-hec: Option to include only the body or the headers

[CAMEL-16535](https://issues.apache.org/jira/browse/CAMEL-16535)

camel-main - Add option to dump routes as XML on startup

[CAMEL-16502](https://issues.apache.org/jira/browse/CAMEL-16502)

camel-restdsl-openapi-plugin - add basepath parameter

[CAMEL-16493](https://issues.apache.org/jira/browse/CAMEL-16493)

camel-kamelet - Kamelet EIP

[CAMEL-16478](https://issues.apache.org/jira/browse/CAMEL-16478)

Camel-AWS2-DDB: Add key scala type to endpoint options

[CAMEL-16475](https://issues.apache.org/jira/browse/CAMEL-16475)

\[camel-debezium\] Upgrade to debezium 1.5.FINAL

[CAMEL-16469](https://issues.apache.org/jira/browse/CAMEL-16469)

Camel-AWS2-S3 - Streaming upload: restart from the last index when using the progressive naming strategy

[CAMEL-16451](https://issues.apache.org/jira/browse/CAMEL-16451)

camel-core - ExchangePooling for EIPs

[CAMEL-16429](https://issues.apache.org/jira/browse/CAMEL-16429)

camel-core - Can we use unique TypeConverterLoader files for easy fat-jar assembly

[CAMEL-16427](https://issues.apache.org/jira/browse/CAMEL-16427)

Jdbc based IdempotentRepository should handle orphan lock

[CAMEL-16417](https://issues.apache.org/jira/browse/CAMEL-16417)

JT400 Component needs ability to reply to messages

[CAMEL-16405](https://issues.apache.org/jira/browse/CAMEL-16405)

camel-sql | sql-stored component queryTimeout option not present

[CAMEL-16394](https://issues.apache.org/jira/browse/CAMEL-16394)

Route Template local beans

[CAMEL-16368](https://issues.apache.org/jira/browse/CAMEL-16368)

camel-salesforce: Add support for Composite sObject Collections API

[CAMEL-16312](https://issues.apache.org/jira/browse/CAMEL-16312)

camel-core - Route template parameter - Specify type and valid input

[CAMEL-16116](https://issues.apache.org/jira/browse/CAMEL-16116)

False positive validation forsome special SpringBoot properties

[CAMEL-15655](https://issues.apache.org/jira/browse/CAMEL-15655)

Create camel-azure-cosmosdb component

### Task (25)

[CAMEL-16602](https://issues.apache.org/jira/browse/CAMEL-16602)

camel-kamelet-reify - Move this to camel3 project

[CAMEL-16583](https://issues.apache.org/jira/browse/CAMEL-16583)

Missing code samples in camel-cxf docs

[CAMEL-16576](https://issues.apache.org/jira/browse/CAMEL-16576)

Merge duplicate adoc and md files related to community topics

[CAMEL-16528](https://issues.apache.org/jira/browse/CAMEL-16528)

camel-main - Remove autowire.properties as the has been removed

[CAMEL-16524](https://issues.apache.org/jira/browse/CAMEL-16524)

Remove Camel-Crypto-CMS

[CAMEL-16518](https://issues.apache.org/jira/browse/CAMEL-16518)

Deprecate Camel-APNS

[CAMEL-16517](https://issues.apache.org/jira/browse/CAMEL-16517)

camel-bindy - Doc doesn't reflect FixeLengthRecord annotation changes after CAMEL-5958

[CAMEL-16505](https://issues.apache.org/jira/browse/CAMEL-16505)

camel-pulsar: tests broken after core optimization

[CAMEL-16495](https://issues.apache.org/jira/browse/CAMEL-16495)

Camel-AWS-S3 - Streaming upload: While restarting the listObject operation should be paginated

[CAMEL-16466](https://issues.apache.org/jira/browse/CAMEL-16466)

Remove Camel-geocoder karaf feature

[CAMEL-16464](https://issues.apache.org/jira/browse/CAMEL-16464)

Remove Camel-jsonpath karaf feature

[CAMEL-16463](https://issues.apache.org/jira/browse/CAMEL-16463)

Remove Camel-Chunk Karaf feature

[CAMEL-16456](https://issues.apache.org/jira/browse/CAMEL-16456)

Move usages of ActiveMQ broker service to test-infra

[CAMEL-16443](https://issues.apache.org/jira/browse/CAMEL-16443)

Yarn failure in the docs module

[CAMEL-16430](https://issues.apache.org/jira/browse/CAMEL-16430)

webhook: move the WebhookRoutePolicy from camel-k to the camel-webhook component

[CAMEL-16424](https://issues.apache.org/jira/browse/CAMEL-16424)

yaml dsl: re-introduce support for parameters in endpoint definitions

[CAMEL-16422](https://issues.apache.org/jira/browse/CAMEL-16422)

Remove Camel-Cassandraql Karaf feature

[CAMEL-16409](https://issues.apache.org/jira/browse/CAMEL-16409)

camel-google-cloud-functions - Better description

[CAMEL-16406](https://issues.apache.org/jira/browse/CAMEL-16406)

Camel-AWS-Secrets-Manager: Add replica to multiple regions operation

[CAMEL-16398](https://issues.apache.org/jira/browse/CAMEL-16398)

Camel-AWS-DDBStreams: Don't take the stream existence for granted

[CAMEL-16389](https://issues.apache.org/jira/browse/CAMEL-16389)

Remove json-smart

[CAMEL-16375](https://issues.apache.org/jira/browse/CAMEL-16375)

Getting rid of json-smart as explicit and transitive dependency

[CAMEL-16341](https://issues.apache.org/jira/browse/CAMEL-16341)

Having a middle folder for vertx components

[CAMEL-16259](https://issues.apache.org/jira/browse/CAMEL-16259)

Karaf examples don't get deployed

[CAMEL-15850](https://issues.apache.org/jira/browse/CAMEL-15850)

Upgrade to karaf 4.3

### Test (6)

[CAMEL-16613](https://issues.apache.org/jira/browse/CAMEL-16613)

camel-jetty and camel-netty-http - Do not run tests in parallel as CI server keeps randomly failing

[CAMEL-16543](https://issues.apache.org/jira/browse/CAMEL-16543)

bindy: add test for countGrapheme

[CAMEL-16508](https://issues.apache.org/jira/browse/CAMEL-16508)

camel-leveldb - Tests are failing due some google JAR

[CAMEL-16506](https://issues.apache.org/jira/browse/CAMEL-16506)

Camel-Azure-Storage-queue: Add Azurite IT Tests

[CAMEL-16445](https://issues.apache.org/jira/browse/CAMEL-16445)

openstack: add some wiremock local integration tests

[CAMEL-16385](https://issues.apache.org/jira/browse/CAMEL-16385)

camel-spring-boot - JbpmTest fails

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).