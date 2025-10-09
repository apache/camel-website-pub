# Apache camel 4.11.0 Release

## New and Noteworthy

This release is the new Camel 4.11.0 release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.11.0</version>
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
      <version>4.11.0</version>
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
| [apache-camel-4.11.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-src.zip.sha512) |
| [apache-camel-4.11.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.xml.sha512) |
| [apache-camel-4.11.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.11.0/apache-camel-4.11.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.11.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.11.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (50)

[CAMEL-21892](https://issues.apache.org/jira/browse/CAMEL-21892)

Stopped producer in DefaultProducerCache.lastUsedProducer

[CAMEL-21888](https://issues.apache.org/jira/browse/CAMEL-21888)

High CPU usage at startup due to Deque.size() iteration in SimpleLRUCache

[CAMEL-21883](https://issues.apache.org/jira/browse/CAMEL-21883)

Possible resource leak in camel-stringtemplate

[CAMEL-21877](https://issues.apache.org/jira/browse/CAMEL-21877)

ServiceNow incident update fails due to model/body type mismatch

[CAMEL-21868](https://issues.apache.org/jira/browse/CAMEL-21868)

\[camel-observation\] MicrometerObservationSpanAdapter cannot be cast to class OpenTelemetrySpanAdapter

[CAMEL-21865](https://issues.apache.org/jira/browse/CAMEL-21865)

camel-test - Using advice-with with route having XML namepaces as immutable Map.of

[CAMEL-21858](https://issues.apache.org/jira/browse/CAMEL-21858)

camel-tracing: Incorrect http method on trace record

[CAMEL-21856](https://issues.apache.org/jira/browse/CAMEL-21856)

Container restart caused by startup probe failure

[CAMEL-21855](https://issues.apache.org/jira/browse/CAMEL-21855)

camel-jbang - k8s delete may not work any more

[CAMEL-21854](https://issues.apache.org/jira/browse/CAMEL-21854)

Possible memory leak when using camel-observability

[CAMEL-21853](https://issues.apache.org/jira/browse/CAMEL-21853)

camel-salesforce - PubSub Client Initial Subscription Timeout Error with custom replayPresent

[CAMEL-21849](https://issues.apache.org/jira/browse/CAMEL-21849)

camel-kamelet - Using variableReceive should not loose message body

[CAMEL-21847](https://issues.apache.org/jira/browse/CAMEL-21847)

camel-http - Possible resource leak in camel-http when using oauth2

[CAMEL-21840](https://issues.apache.org/jira/browse/CAMEL-21840)

camel-http does not encode path correctly when used with HTTP\_QUERY header

[CAMEL-21839](https://issues.apache.org/jira/browse/CAMEL-21839)

camel-langchain4j-tools: No body passed on no-tools executed

[CAMEL-21836](https://issues.apache.org/jira/browse/CAMEL-21836)

Possible resource leak in camel minio in verifier extension

[CAMEL-21833](https://issues.apache.org/jira/browse/CAMEL-21833)

Kafka Batch Manual commit doesn't work if used in Kamelets

[CAMEL-21832](https://issues.apache.org/jira/browse/CAMEL-21832)

camel-core - Choice with when that has no output should not call otherwise

[CAMEL-21830](https://issues.apache.org/jira/browse/CAMEL-21830)

camel-file - Using consumer template to consume a single file issue with idempotentEager

[CAMEL-21808](https://issues.apache.org/jira/browse/CAMEL-21808)

Camel-pinecone: NullPointerException might be thrown in PineconeVectorDbProducer

[CAMEL-21807](https://issues.apache.org/jira/browse/CAMEL-21807)

camel-kamelet - Custom kamelet with dynamic query parameter with sql component

[CAMEL-21800](https://issues.apache.org/jira/browse/CAMEL-21800)

camel-smb - The scheduler options cannot be configured on the consumer

[CAMEL-21799](https://issues.apache.org/jira/browse/CAMEL-21799)

camel-coap - Exchange retrieve only the last block of Blockwise

[CAMEL-21794](https://issues.apache.org/jira/browse/CAMEL-21794)

camel-jbang - Export bean with lazy-bean should not initialize the bean if not needed

[CAMEL-21793](https://issues.apache.org/jira/browse/CAMEL-21793)

camel-kamelets - Kamelets and excessive load causes ConcurrentModificationException

[CAMEL-21792](https://issues.apache.org/jira/browse/CAMEL-21792)

camel-aws - KCL Kinesis Consumer fails with NPE when using custom async client

[CAMEL-21790](https://issues.apache.org/jira/browse/CAMEL-21790)

camel-kafka - Race condition in KafkaProducerMetadataCallBack

[CAMEL-21780](https://issues.apache.org/jira/browse/CAMEL-21780)

camel-core - Java DSL - StackOverflowError with Enrich EIP and assigning id

[CAMEL-21778](https://issues.apache.org/jira/browse/CAMEL-21778)

camel-core - Java DSL using id in processors after Threads EIP is not assigned

[CAMEL-21776](https://issues.apache.org/jira/browse/CAMEL-21776)

camel-core - DefaultRoute does not gather services for onException/onCompletion

[CAMEL-21775](https://issues.apache.org/jira/browse/CAMEL-21775)

Split or Multicast in onException route cannot be started using Supervised route controller

[CAMEL-21770](https://issues.apache.org/jira/browse/CAMEL-21770)

camel-kubernetes: Autowired KubernetesClient should not be closed

[CAMEL-21769](https://issues.apache.org/jira/browse/CAMEL-21769)

camel-aws-sqs - Error is causing the sqs message to be extended forever

[CAMEL-21758](https://issues.apache.org/jira/browse/CAMEL-21758)

camel-jms - TemporaryQueueReplyManager does not inherit doStop method

[CAMEL-21755](https://issues.apache.org/jira/browse/CAMEL-21755)

Enrich with exchangepattern=InOut doesn't return enriched body.

[CAMEL-21754](https://issues.apache.org/jira/browse/CAMEL-21754)

camel-mail - ClassCastException if using DEBUG logging

[CAMEL-21753](https://issues.apache.org/jira/browse/CAMEL-21753)

camel-jbang - Generates duplicate application.property entries

[CAMEL-21752](https://issues.apache.org/jira/browse/CAMEL-21752)

camel-smb - DFS doesn't work because SmbConfig cannot be set for smbclient

[CAMEL-21747](https://issues.apache.org/jira/browse/CAMEL-21747)

camel-debug - On timeout then remove suspended breakpoint state

[CAMEL-21746](https://issues.apache.org/jira/browse/CAMEL-21746)

When starting camel in standalone mode, configureVaultRefresh is called twice (thus refresh task is started twice)

[CAMEL-21741](https://issues.apache.org/jira/browse/CAMEL-21741)

MainHttpServer needs to get registered/started explicitly

[CAMEL-21740](https://issues.apache.org/jira/browse/CAMEL-21740)

camel-salesforce - pub/sub API corrupt replay id causes infinite resubscribe loop

[CAMEL-21739](https://issues.apache.org/jira/browse/CAMEL-21739)

camel-ftp - Implementation of GenericFileConsumer.getRelativeFilePath differs in camel-ftp to camel-file

[CAMEL-21737](https://issues.apache.org/jira/browse/CAMEL-21737)

camel-kubernetes: Multiple consumers are using the k8s client incorrectly

[CAMEL-21735](https://issues.apache.org/jira/browse/CAMEL-21735)

MongoDB component connecting to localhost event if connection data is set

[CAMEL-21732](https://issues.apache.org/jira/browse/CAMEL-21732)

camel-core - Poll EIP with dynamic simple language uri does not work

[CAMEL-21730](https://issues.apache.org/jira/browse/CAMEL-21730)

JBang export cannot validate route that depends on copied resources

[CAMEL-21707](https://issues.apache.org/jira/browse/CAMEL-21707)

camel-jbang: error on export command - ClassNotFoundException: org.apache.camel.kamelets.catalog.KameletsCatalog

[CAMEL-21662](https://issues.apache.org/jira/browse/CAMEL-21662)

Camel JBang - run with Spring boot / Quarkus fails on Windows

[CAMEL-21604](https://issues.apache.org/jira/browse/CAMEL-21604)

GZIP interceptor added as a CXF feature is not working properly for CXF SOAP and CXF REST on Camel Spring Boot

### Dependency upgrade (3)

[CAMEL-21870](https://issues.apache.org/jira/browse/CAMEL-21870)

camel-spring-boot - Upgrade to Spring Boot 3.4.4

[CAMEL-21772](https://issues.apache.org/jira/browse/CAMEL-21772)

camel-spring-boot - Upgrade to 3.4.3

[CAMEL-21600](https://issues.apache.org/jira/browse/CAMEL-21600)

camel-ognl - Upgrade to 3.4.6

### Improvement (50)

[CAMEL-21904](https://issues.apache.org/jira/browse/CAMEL-21904)

camel-jbang: Use cluster specific labels on Kubernetes deployment

[CAMEL-21903](https://issues.apache.org/jira/browse/CAMEL-21903)

camel-jbang: Adjustable container image name on Kubernetes export

[CAMEL-21900](https://issues.apache.org/jira/browse/CAMEL-21900)

Verify OIDC token on Knative service endpoint

[CAMEL-21895](https://issues.apache.org/jira/browse/CAMEL-21895)

REST DSL only pick last .to() definition if there are multiple definitions

[CAMEL-21893](https://issues.apache.org/jira/browse/CAMEL-21893)

EnvVar settings should overwrite default Kamelet property values

[CAMEL-21887](https://issues.apache.org/jira/browse/CAMEL-21887)

camel-platform-http-starter - Add support for Spring security context injection

[CAMEL-21885](https://issues.apache.org/jira/browse/CAMEL-21885)

HeaderFilter Strategies: add lowerCase where it's not present

[CAMEL-21881](https://issues.apache.org/jira/browse/CAMEL-21881)

camel-smooks: Move smooks-edi-cartridge dependency from test to compile scope

[CAMEL-21880](https://issues.apache.org/jira/browse/CAMEL-21880)

camel-kafka - add lowerCase to header filter strategy

[CAMEL-21861](https://issues.apache.org/jira/browse/CAMEL-21861)

camel-spring-boot - Actuator endpoint for dev console should respect if console has been disabled

[CAMEL-21852](https://issues.apache.org/jira/browse/CAMEL-21852)

camel-jbang - camel version list - add option to only show active releases

[CAMEL-21851](https://issues.apache.org/jira/browse/CAMEL-21851)

camel-bean - Improve method selector

[CAMEL-21848](https://issues.apache.org/jira/browse/CAMEL-21848)

camel-jbang - Consider including jolokia when using --console

[CAMEL-21846](https://issues.apache.org/jira/browse/CAMEL-21846)

camel-jbang - Add support for running on eclipse openj9 java

[CAMEL-21845](https://issues.apache.org/jira/browse/CAMEL-21845)

camel-sql - Improve performance of batch inserts

[CAMEL-21843](https://issues.apache.org/jira/browse/CAMEL-21843)

camel-kamelet - Move kamelet utils to corresponding components

[CAMEL-21829](https://issues.apache.org/jira/browse/CAMEL-21829)

camel-sql - Make it easier to use Map values for non-named SQL statements

[CAMEL-21828](https://issues.apache.org/jira/browse/CAMEL-21828)

camel-http - DefaultHeaderFilterStrategy optimize filter

[CAMEL-21823](https://issues.apache.org/jira/browse/CAMEL-21823)

camel-core - Propagate MDC custom keys for WireTap and OnCompletion EIPs

[CAMEL-21821](https://issues.apache.org/jira/browse/CAMEL-21821)

camel-smooks - Eliminate support for declaring route condition in element text

[CAMEL-21819](https://issues.apache.org/jira/browse/CAMEL-21819)

camel-pinecone - Add fetch action and add namespace to upsert

[CAMEL-21818](https://issues.apache.org/jira/browse/CAMEL-21818)

camel-core - Add list/map functions to simple language

[CAMEL-21817](https://issues.apache.org/jira/browse/CAMEL-21817)

camel-bean - Add better support for invoking varargs methods

[CAMEL-21814](https://issues.apache.org/jira/browse/CAMEL-21814)

Add additional arguments to camel-pinecone query

[CAMEL-21812](https://issues.apache.org/jira/browse/CAMEL-21812)

camel-jbang - Provide an option in camel k8s to trust a given cert

[CAMEL-21811](https://issues.apache.org/jira/browse/CAMEL-21811)

camel-oauth - Prefer Ingress over TLS configured on Keycloak directly

[CAMEL-21809](https://issues.apache.org/jira/browse/CAMEL-21809)

camel-coap - Does not provide the way to override the default CoapConfig

[CAMEL-21806](https://issues.apache.org/jira/browse/CAMEL-21806)

Add host to camel-pinecone

[CAMEL-21798](https://issues.apache.org/jira/browse/CAMEL-21798)

Add proxy settings to camel-pinecone

[CAMEL-21788](https://issues.apache.org/jira/browse/CAMEL-21788)

camel-kafka - Turn recordMetadata off by default

[CAMEL-21785](https://issues.apache.org/jira/browse/CAMEL-21785)

camel-main: Generate configurer classes for Kubernetes vault configuration

[CAMEL-21782](https://issues.apache.org/jira/browse/CAMEL-21782)

camel-file - The autoCreate option should be moved to doStart

[CAMEL-21779](https://issues.apache.org/jira/browse/CAMEL-21779)

camel-smb - The consumer should also support autoCreate

[CAMEL-21777](https://issues.apache.org/jira/browse/CAMEL-21777)

camel-jbang - Add option to show description in outputs

[CAMEL-21774](https://issues.apache.org/jira/browse/CAMEL-21774)

camel-kafka - Add topicMustExists option so consumer can fail if broker has no topic

[CAMEL-21762](https://issues.apache.org/jira/browse/CAMEL-21762)

camel-test - Make it easy to turn off auto starting specific routes

[CAMEL-21761](https://issues.apache.org/jira/browse/CAMEL-21761)

Significantly speed up MavenDependencyDownloader

[CAMEL-21759](https://issues.apache.org/jira/browse/CAMEL-21759)

camel-test - Add @StubEndpoints annotation to make it easy to test without the actual component

[CAMEL-21757](https://issues.apache.org/jira/browse/CAMEL-21757)

camel-kafka - Camel kafka Transactional ID with consumersCount>1 is not possible

[CAMEL-21738](https://issues.apache.org/jira/browse/CAMEL-21738)

camel-kubernetes: Unify listing resources in producer, in regard to namespace

[CAMEL-21734](https://issues.apache.org/jira/browse/CAMEL-21734)

camel-csv - Allow to configurer header via CsvFormat reference

[CAMEL-21733](https://issues.apache.org/jira/browse/CAMEL-21733)

camel-core - PollDynamicAware to reuse endpoints during dynamic poll EIP

[CAMEL-21729](https://issues.apache.org/jira/browse/CAMEL-21729)

camel-jbang - dependency list - Add update command to change the pom.xml

[CAMEL-21712](https://issues.apache.org/jira/browse/CAMEL-21712)

Add support for RFC8707 in HTTP component Oauth2

[CAMEL-21710](https://issues.apache.org/jira/browse/CAMEL-21710)

Set automatic parameter when running camel-jbang kubernetes run

[CAMEL-21671](https://issues.apache.org/jira/browse/CAMEL-21671)

camel-core - Issue with Camel Splitter and Asynchronous Processing in Parallel Mode can use many threads

[CAMEL-21588](https://issues.apache.org/jira/browse/CAMEL-21588)

Pinecone: configurations exclusive in the headers are not user friendly

[CAMEL-21551](https://issues.apache.org/jira/browse/CAMEL-21551)

Expose stream caching as a public processor

[CAMEL-20272](https://issues.apache.org/jira/browse/CAMEL-20272)

Camel-Azure components: Support SAS Authentication where is still not supported

[CAMEL-19667](https://issues.apache.org/jira/browse/CAMEL-19667)

camel-tracing: Context is not propagated from exchange header to OpenTelemetry Context

### New Feature (21)

[CAMEL-21906](https://issues.apache.org/jira/browse/CAMEL-21906)

Camel-IBM-Secrets-Manager: Support ServiceCredentials in producer getSecret

[CAMEL-21894](https://issues.apache.org/jira/browse/CAMEL-21894)

Camel-AWS-SNS: Support Batch Publishing

[CAMEL-21876](https://issues.apache.org/jira/browse/CAMEL-21876)

Undertow Header Filter Strategy: Considering also the in filter

[CAMEL-21872](https://issues.apache.org/jira/browse/CAMEL-21872)

Remove deprecated \*HttpHeaderFilterStrategy and deprecate \*HttpHeaderFilterStrategy implementation

[CAMEL-21867](https://issues.apache.org/jira/browse/CAMEL-21867)

camel-oauth - OAuth support for runtime=spring-boot

[CAMEL-21834](https://issues.apache.org/jira/browse/CAMEL-21834)

Camel-Spring-Boot: Create ApplicationEnvironmentPreparedEvent for Vault IBM Secrets Manager

[CAMEL-21826](https://issues.apache.org/jira/browse/CAMEL-21826)

Camel-IBM-Secrtes-manager: Support properties function in Spring boot

[CAMEL-21822](https://issues.apache.org/jira/browse/CAMEL-21822)

Camel-IBM-Secrets-Manager: Documentation for properties function

[CAMEL-21820](https://issues.apache.org/jira/browse/CAMEL-21820)

Camel-IBM-Secrets-manager: Support Arbitrary secrets type in properties function

[CAMEL-21805](https://issues.apache.org/jira/browse/CAMEL-21805)

Camel-IBM-Secrets-manager: Add ListSecrets operation

[CAMEL-21802](https://issues.apache.org/jira/browse/CAMEL-21802)

Camel Pinecone component : transform results of similarity search into List of texts

[CAMEL-21786](https://issues.apache.org/jira/browse/CAMEL-21786)

\[camel-opentelemetry2\] Implement a new opentelemetry component

[CAMEL-21768](https://issues.apache.org/jira/browse/CAMEL-21768)

Camel-IBM-Secrets-Manager: Create a properties function

[CAMEL-21767](https://issues.apache.org/jira/browse/CAMEL-21767)

Camel-IBM-Secrets-manager: Add more type of secrets for create secret operation

[CAMEL-21731](https://issues.apache.org/jira/browse/CAMEL-21731)

camel-openapi-java - Adding reference to external Open API docs

[CAMEL-21723](https://issues.apache.org/jira/browse/CAMEL-21723)

camel-jbang shell edit command

[CAMEL-21670](https://issues.apache.org/jira/browse/CAMEL-21670)

\[camel-telemetry\] Create a new abstract telemetry component

[CAMEL-21644](https://issues.apache.org/jira/browse/CAMEL-21644)

camel-daffodil - New component

[CAMEL-21539](https://issues.apache.org/jira/browse/CAMEL-21539)

Vector Database capabilities - Infinispan

[CAMEL-21198](https://issues.apache.org/jira/browse/CAMEL-21198)

Create an IBM Secrets Manager component

[CAMEL-20118](https://issues.apache.org/jira/browse/CAMEL-20118)

camel-salesforce: Maven plugin: Support JWT Client Credentials flow

### Task (14)

[CAMEL-21874](https://issues.apache.org/jira/browse/CAMEL-21874)

Three possible locations of resource leak in camel-aws

[CAMEL-21866](https://issues.apache.org/jira/browse/CAMEL-21866)

camel-etcd3: remove deprecate component etcd3

[CAMEL-21860](https://issues.apache.org/jira/browse/CAMEL-21860)

IntelliJ cannot run camel k8s tests

[CAMEL-21837](https://issues.apache.org/jira/browse/CAMEL-21837)

camel-api - Deprecate component.extension

[CAMEL-21827](https://issues.apache.org/jira/browse/CAMEL-21827)

documentation - Add note about using MDC logging has potential issues

[CAMEL-21795](https://issues.apache.org/jira/browse/CAMEL-21795)

Camel-AWS components: Adding STS dependency out of the box since it is used in case of DefaultCredentialsProvider

[CAMEL-21789](https://issues.apache.org/jira/browse/CAMEL-21789)

High Memory Usage During Gradle Dependency Resolution

[CAMEL-21781](https://issues.apache.org/jira/browse/CAMEL-21781)

Remove unnecessary TelemetrySimpleConfigurationPropertiesConfigurer service configuration

[CAMEL-21764](https://issues.apache.org/jira/browse/CAMEL-21764)

Create an IBM Secrets Manager Component starter

[CAMEL-21756](https://issues.apache.org/jira/browse/CAMEL-21756)

camel-jbang - Upgrade maven wrapper

[CAMEL-21750](https://issues.apache.org/jira/browse/CAMEL-21750)

camel-google - Avoid using their BOM as it has a huge dependency and cause slowness on builds

[CAMEL-21748](https://issues.apache.org/jira/browse/CAMEL-21748)

Upgrade to Camel-Kamelets 4.10.0 in camel-jbang

[CAMEL-19537](https://issues.apache.org/jira/browse/CAMEL-19537)

camel-mina: replace Thread.sleep in tests

[CAMEL-16335](https://issues.apache.org/jira/browse/CAMEL-16335)

Having a middle folder for Spring components

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).