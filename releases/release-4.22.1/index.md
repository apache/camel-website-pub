# Apache camel 4.22.1 Release

## New and Noteworthy

This release is the new Camel 4.22.1 LTS release.

## Supported Java version

This version supports Java 17, 21 and 25.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.22.1</version>
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
      <version>4.22.1</version>
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
| [apache-camel-4.22.1-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.1/apache-camel-4.22.1-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-src.zip.sha512) |
| [apache-camel-4.22.1-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.xml.sha512) |
| [apache-camel-4.22.1-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.1/apache-camel-4.22.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.22.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.22.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (85)

[CAMEL-24776](https://issues.apache.org/jira/browse/CAMEL-24776)

camel-jbang run does not auto-load camel-kubernetes for secret property functions

[CAMEL-24729](https://issues.apache.org/jira/browse/CAMEL-24729)

camel-infinispan: a lifespan set without its time unit is silently ignored

[CAMEL-24681](https://issues.apache.org/jira/browse/CAMEL-24681)

camel-jbang: export does not include Maven repositories from properties camel.jbang.repos and camel.extra.repos

[CAMEL-24669](https://issues.apache.org/jira/browse/CAMEL-24669)

camel-groovy - groovyJson/groovyXml: support Jackson 3 nodes and fix prettyPrint=false output

[CAMEL-24668](https://issues.apache.org/jira/browse/CAMEL-24668)

Camel MLLP consumer discards pipelined HL7 messages that arrive in a single TCP read

[CAMEL-24651](https://issues.apache.org/jira/browse/CAMEL-24651)

Regression on Camel 4.x NPE on evaluation of a Simple expression ${exception.stacktrace}

[CAMEL-24632](https://issues.apache.org/jira/browse/CAMEL-24632)

SSLException when GET/POST to https endpoint with proxy setting using camel-http component

[CAMEL-24630](https://issues.apache.org/jira/browse/CAMEL-24630)

camel-kamelet: supervised route reload creates duplicate internal routes and causes context console NPE

[CAMEL-24628](https://issues.apache.org/jira/browse/CAMEL-24628)

camel-cli: dependency update silently drops route files passed as positional arguments

[CAMEL-24626](https://issues.apache.org/jira/browse/CAMEL-24626)

camel-master: follow-ups to CAMEL-24583 - leadership lock, cancelled task registry entries, backoff documentation

[CAMEL-24623](https://issues.apache.org/jira/browse/CAMEL-24623)

camel-infinispan: the QUERY operation silently returns the input when no query builder is set

[CAMEL-24622](https://issues.apache.org/jira/browse/CAMEL-24622)

camel-infinispan: the aggregation repository implements RecoverableAggregationRepository without a recovery store

[CAMEL-24594](https://issues.apache.org/jira/browse/CAMEL-24594)

RestBindingAdvice response marshalling failure is silently swallowed

[CAMEL-24593](https://issues.apache.org/jira/browse/CAMEL-24593)

camel-platform-http-starter - accepted multipart uploads are copied to the servlet temp directory and never deleted

[CAMEL-24591](https://issues.apache.org/jira/browse/CAMEL-24591)

camel-seda - Send fails with "No queue available" after producer route restart (regression from CAMEL-24408)

[CAMEL-24590](https://issues.apache.org/jira/browse/CAMEL-24590)

ManagedRouteGroupMBean.getFailuresHandled() / getLastExchangeFailureHandledTimestamp() return 0/null even though a member route recorded a handled failure

[CAMEL-24585](https://issues.apache.org/jira/browse/CAMEL-24585)

The catalog validateLanguageExpression returns an invoke error when using jsonpath in a simple expression

[CAMEL-24584](https://issues.apache.org/jira/browse/CAMEL-24584)

camel-support: BackgroundTask.schedule keeps re-running a task that has completed or run out of budget

[CAMEL-24583](https://issues.apache.org/jira/browse/CAMEL-24583)

camel-master: losing leadership while a consumer start is pending leaves the delegated consumer running on a non-leader node

[CAMEL-24573](https://issues.apache.org/jira/browse/CAMEL-24573)

CXF REST: UnsupportedOperationException when copying factory bean with fixed-size features list

[CAMEL-24545](https://issues.apache.org/jira/browse/CAMEL-24545)

Camel Shutdown Locked State With ZookeeprCluster Service

[CAMEL-24542](https://issues.apache.org/jira/browse/CAMEL-24542)

camel-qdrant: the PayloadSelector header is declared and advertised but never read

[CAMEL-24539](https://issues.apache.org/jira/browse/CAMEL-24539)

camel-openai: embeddings/audio store their SDK response under the chat-typed RESPONSE property

[CAMEL-24535](https://issues.apache.org/jira/browse/CAMEL-24535)

camel-tensorflow-serving: the Target and Credentials headers are declared but never read

[CAMEL-24534](https://issues.apache.org/jira/browse/CAMEL-24534)

camel-qdrant: the embeddings data-type transformer casts every metadata value to String

[CAMEL-24530](https://issues.apache.org/jira/browse/CAMEL-24530)

camel-djl: DJLConverter leaks the InputStream opened from File/Path bodies

[CAMEL-24529](https://issues.apache.org/jira/browse/CAMEL-24529)

camel-djl: the loaded ZooModel is never closed (native-memory leak on restart)

[CAMEL-24528](https://issues.apache.org/jira/browse/CAMEL-24528)

camel-huggingface: four task predictors swallow Python inference errors as success

[CAMEL-24526](https://issues.apache.org/jira/browse/CAMEL-24526)

camel-djl: the zoo linear/softmax regression predictors are unimplemented no-ops

[CAMEL-24495](https://issues.apache.org/jira/browse/CAMEL-24495)

Authentication-type detection is not triggered via camel-salesforce-maven-plugin. It still uses grant-type USERNAME\_PASSWORD

[CAMEL-24493](https://issues.apache.org/jira/browse/CAMEL-24493)

camel-ibm-cos: the producer ignores multiPartUpload, partSize, storageClass and deleteAfterWrite options

[CAMEL-24491](https://issues.apache.org/jira/browse/CAMEL-24491)

camel-ibm-cos: consumer in-progress deduplication is inert, causing duplicate delivery

[CAMEL-24490](https://issues.apache.org/jira/browse/CAMEL-24490)

camel-ibm-watsonx-ai: the timeout option is never applied to the watsonx.ai service clients

[CAMEL-24488](https://issues.apache.org/jira/browse/CAMEL-24488)

camel-ibm-watson-speech-to-text: WatsonSpeechToTextProducer leaks the audio FileInputStream

[CAMEL-24486](https://issues.apache.org/jira/browse/CAMEL-24486)

camel-core - Simple language init block custom functions ($foo ~:= ...) fail with "No custom simple function" when CamelContext profile is dev

[CAMEL-24484](https://issues.apache.org/jira/browse/CAMEL-24484)

camel-file: readLockRemoveOnCommit=false is not respected when idempotent-changed/-rename/idempotent read lock fails to acquire an existing entry

[CAMEL-24483](https://issues.apache.org/jira/browse/CAMEL-24483)

camel-jbang export: explicit --dep version is ignored for auto-detected dependencies

[CAMEL-24482](https://issues.apache.org/jira/browse/CAMEL-24482)

Camel JBang YAML validator incorrectly requires all data formats inside unmarshal step

[CAMEL-24479](https://issues.apache.org/jira/browse/CAMEL-24479)

\[camel-jbang\] YAML validation incorrectly succeeds when containing invalid properties

[CAMEL-24475](https://issues.apache.org/jira/browse/CAMEL-24475)

camel-xpath - documentType=InputSource evaluates the payload with an unhardened XML parser

[CAMEL-24470](https://issues.apache.org/jira/browse/CAMEL-24470)

camel-ibm-secrets-manager: IBMEventStreamReloadTriggerTask rejects Event Stream credentials provided via environment variables

[CAMEL-24468](https://issues.apache.org/jira/browse/CAMEL-24468)

camel-ibm-secrets-manager - fix defects in IBMSecretsManagerPropertiesFunction (env-var credentials rejected, secret version pin ignored, missing KV field returns "null")

[CAMEL-24464](https://issues.apache.org/jira/browse/CAMEL-24464)

camel-exec ignores its documented CamelExecCommand\* headers (executable and args have no effect)

[CAMEL-24457](https://issues.apache.org/jira/browse/CAMEL-24457)

Camel Zookeeper Cluster Split brain issue when leader is isolated

[CAMEL-24456](https://issues.apache.org/jira/browse/CAMEL-24456)

camel-http - OAuth2 token cache key omits tokenEndpoint, scope and resourceIndicator

[CAMEL-24455](https://issues.apache.org/jira/browse/CAMEL-24455)

camel-platform-http - any path starting with "proxy" selects HTTP proxy mode

[CAMEL-24454](https://issues.apache.org/jira/browse/CAMEL-24454)

camel-mllp - logPhi defaults to true, so message content is written to the log at INFO/WARN

[CAMEL-24453](https://issues.apache.org/jira/browse/CAMEL-24453)

camel-platform-http - request-header echo suppression compares header names case-sensitively

[CAMEL-24452](https://issues.apache.org/jira/browse/CAMEL-24452)

camel-http - credentials are sent to redirect targets on a different host

[CAMEL-24450](https://issues.apache.org/jira/browse/CAMEL-24450)

camel-jetty - enableCORS installs Jetty's CrossOriginFilter with its allow-all defaults

[CAMEL-24449](https://issues.apache.org/jira/browse/CAMEL-24449)

camel-core - saga coordinator is selected from the unprefixed Long-Running-Action message header

[CAMEL-24448](https://issues.apache.org/jira/browse/CAMEL-24448)

camel-keycloak - introspection issuer validation is skipped when the iss claim is absent

[CAMEL-24447](https://issues.apache.org/jira/browse/CAMEL-24447)

camel-pqc - FileBasedKeyLifecycleManager writes private keys with default file permissions

[CAMEL-24445](https://issues.apache.org/jira/browse/CAMEL-24445)

camel-pqc - producer shares one Signature instance across concurrent exchanges without synchronization

[CAMEL-24443](https://issues.apache.org/jira/browse/CAMEL-24443)

camel-knative-http - enabling SSL without a truststore falls back to trusting all certificates

[CAMEL-24442](https://issues.apache.org/jira/browse/CAMEL-24442)

camel-thrift - unmarshal deserializes into and returns a single shared instance

[CAMEL-24441](https://issues.apache.org/jira/browse/CAMEL-24441)

camel-crypto-pgp - unmarshal accepts unsigned and non-integrity-protected messages by default

[CAMEL-24439](https://issues.apache.org/jira/browse/CAMEL-24439)

camel-shiro - presented password is not verified when the thread subject already matches the username

[CAMEL-24436](https://issues.apache.org/jira/browse/CAMEL-24436)

camel-platform-http-vertx - CORS handler allows any origin and always sends Access-Control-Allow-Credentials

[CAMEL-24435](https://issues.apache.org/jira/browse/CAMEL-24435)

camel-as2 - asynchronous MDN context attributes are reused across requests on the same connection

[CAMEL-24429](https://issues.apache.org/jira/browse/CAMEL-24429)

camel-as2 - ResponseMDN keeps per-request signing keys in shared mutable instance fields

[CAMEL-24427](https://issues.apache.org/jira/browse/CAMEL-24427)

camel-servlet, camel-jetty - fileNameExtWhitelist is checked against the wrong value in one binding and absent in the other

[CAMEL-24425](https://issues.apache.org/jira/browse/CAMEL-24425)

camel-azure-storage-blob - sasToken is not marked as a secret

[CAMEL-24424](https://issues.apache.org/jira/browse/CAMEL-24424)

camel-vertx-http - REST header filter strategy applies the inbound rules on the outbound direction

[CAMEL-24423](https://issues.apache.org/jira/browse/CAMEL-24423)

camel-tika - parsed document metadata is copied to exchange headers without filtering

[CAMEL-24419](https://issues.apache.org/jira/browse/CAMEL-24419)

camel-mail - MimeMultipartDataFormat unmarshal does not filter the mail.smtp/mail.smtps header namespace

[CAMEL-24417](https://issues.apache.org/jira/browse/CAMEL-24417)

camel-as2 - asynchronous MDN delivery address is used without scheme validation and always over a plain socket

[CAMEL-24413](https://issues.apache.org/jira/browse/CAMEL-24413)

camel-hazelcast - ReplicatedHazelcastAggregationRepository does not apply the default serialization filter

[CAMEL-24412](https://issues.apache.org/jira/browse/CAMEL-24412)

camel-netty-http - security constraint lookup must use the same case-insensitive path matching as dispatch

[CAMEL-24411](https://issues.apache.org/jira/browse/CAMEL-24411)

camel-oauth - stop the route when the OAuth processors do not authenticate the request

[CAMEL-24410](https://issues.apache.org/jira/browse/CAMEL-24410)

camel-jbang export fails to parse redeliveryDelay in YAML DSL (IllegalArgumentException: Error parsing as java.time.Duration)

[CAMEL-24409](https://issues.apache.org/jira/browse/CAMEL-24409)

rest-dsl - Binary data corrupted by rest client request validator

[CAMEL-24408](https://issues.apache.org/jira/browse/CAMEL-24408)

SEDA discardIfNoConsumers breaks after consumer removal when sharing the same URI

[CAMEL-24407](https://issues.apache.org/jira/browse/CAMEL-24407)

simple predicate fails for long digital strings

[CAMEL-24401](https://issues.apache.org/jira/browse/CAMEL-24401)

Camel-jms InOut pattern on to(...) with temporary queues can enter infinitely looping error state

[CAMEL-24392](https://issues.apache.org/jira/browse/CAMEL-24392)

BacklogTracerRouteAdvice drains non-re-readable InputStream body before stream caching

[CAMEL-24388](https://issues.apache.org/jira/browse/CAMEL-24388)

Camel JBang - PluginHelper should guard against duplicate subcommand registration

[CAMEL-24382](https://issues.apache.org/jira/browse/CAMEL-24382)

camel-azure-cosmosdb: change-feed consumer checkpoints the lease before the exchange is processed, losing events on failure

[CAMEL-24376](https://issues.apache.org/jira/browse/CAMEL-24376)

boolean zen not working with logical operator

[CAMEL-24375](https://issues.apache.org/jira/browse/CAMEL-24375)

parseDuration should handle plain millis value without relying on type converter

[CAMEL-24371](https://issues.apache.org/jira/browse/CAMEL-24371)

camel-a2a - fix WebhookUrlValidator address classification and host matching

[CAMEL-24350](https://issues.apache.org/jira/browse/CAMEL-24350)

camel-google-pubsub: producer NPEs on non-convertible headers and drops non-Exchange list elements

[CAMEL-24349](https://issues.apache.org/jira/browse/CAMEL-24349)

camel-google-functions: createFunction fails with an opaque NPE when required headers are missing

[CAMEL-24348](https://issues.apache.org/jira/browse/CAMEL-24348)

camel-google-bigquery: NPEs on a null body or unknown job id, and insertId is ignored for List bodies

[CAMEL-24347](https://issues.apache.org/jira/browse/CAMEL-24347)

camel-google-firestore: listCollections ignores the configured documentId and the realtime queue is unbounded

### Dependency upgrade (1)

[CAMEL-24675](https://issues.apache.org/jira/browse/CAMEL-24675)

camel-spring-boot - Upgrade to 4.1.1

### Improvement (29)

[CAMEL-24677](https://issues.apache.org/jira/browse/CAMEL-24677)

camel-smooks: align XML reader configuration with the other XML components

[CAMEL-24676](https://issues.apache.org/jira/browse/CAMEL-24676)

camel-jgroups: add a configurable deserialization filter and document serialization hardening for the consumer

[CAMEL-24653](https://issues.apache.org/jira/browse/CAMEL-24653)

SSLCertTrustTest: replace external badssl.com dependency with local self-signed HTTPS endpoint

[CAMEL-24627](https://issues.apache.org/jira/browse/CAMEL-24627)

camel-file: resolve symlinks when containing local work directory downloads (parity with camel-azure/google-storage)

[CAMEL-24620](https://issues.apache.org/jira/browse/CAMEL-24620)

camel-jackson - Add support to enable/disable features from DatatypeFeature enums

[CAMEL-24605](https://issues.apache.org/jira/browse/CAMEL-24605)

camel-fop: align FopProducer XML transformation with Camel's standard secure XML processing configuration

[CAMEL-24577](https://issues.apache.org/jira/browse/CAMEL-24577)

camel-platform-http-starter - path variable headers are derived from the undecoded request URI

[CAMEL-24576](https://issues.apache.org/jira/browse/CAMEL-24576)

camel-dynamic-router: align control endpoint parameter handling with the allowTemplateFromHeader convention

[CAMEL-24574](https://issues.apache.org/jira/browse/CAMEL-24574)

camel-google-bigquery - clarify that ${name} is literal substitution and steer value parameters to @name

[CAMEL-24513](https://issues.apache.org/jira/browse/CAMEL-24513)

camel-core - Error registry for handlded exception should point to origin of error

[CAMEL-24504](https://issues.apache.org/jira/browse/CAMEL-24504)

camel-spring-boot - extend the SpringTypeConverter String guard beyond InputStream targets

[CAMEL-24503](https://issues.apache.org/jira/browse/CAMEL-24503)

camel-spring-boot - security policy check does not see camel properties supplied as environment variables

[CAMEL-24502](https://issues.apache.org/jira/browse/CAMEL-24502)

Build and CI hardening - workflow token scope, job separation and Maven wrapper checksums

[CAMEL-24501](https://issues.apache.org/jira/browse/CAMEL-24501)

camel-spring-boot-generator-maven-plugin - generated configuration binding drops values silently in three places

[CAMEL-24499](https://issues.apache.org/jira/browse/CAMEL-24499)

camel-spring-boot - route detail view bypasses the route.start.exception serialization filter

[CAMEL-24497](https://issues.apache.org/jira/browse/CAMEL-24497)

camel-undertow-spring-security-starter - JWT decoder is built without an issuer or audience validator

[CAMEL-24496](https://issues.apache.org/jira/browse/CAMEL-24496)

camel-platform-http-starter - align SpringBootPlatformHttpBinding multipart and path handling with the other HTTP bindings

[CAMEL-24487](https://issues.apache.org/jira/browse/CAMEL-24487)

camel-ftp/sftp/mina-sftp/azure-files/smb: contain remote consumer operations within the configured directory

[CAMEL-24478](https://issues.apache.org/jira/browse/CAMEL-24478)

camel-grpc - add a muteException consumer option

[CAMEL-24477](https://issues.apache.org/jira/browse/CAMEL-24477)

camel-cxf - add a muteException consumer option

[CAMEL-24476](https://issues.apache.org/jira/browse/CAMEL-24476)

camel-mina - add a muteException consumer option

[CAMEL-24460](https://issues.apache.org/jira/browse/CAMEL-24460)

JSpecify: Make ProducerTemplate Body Parameters Nullable

[CAMEL-24437](https://issues.apache.org/jira/browse/CAMEL-24437)

camel-oauth - authorization code flow sends no state, nonce or PKCE parameter

[CAMEL-24428](https://issues.apache.org/jira/browse/CAMEL-24428)

camel-knative - add a muteException consumer option

[CAMEL-24422](https://issues.apache.org/jira/browse/CAMEL-24422)

camel-docling: make message body input-source interpretation explicit and configurable

[CAMEL-24421](https://issues.apache.org/jira/browse/CAMEL-24421)

camel-spring-redis: apply a configurable ObjectInputFilter to the default JDK serializer

[CAMEL-24390](https://issues.apache.org/jira/browse/CAMEL-24390)

camel-mcp-server: export all tools via special tag

[CAMEL-24322](https://issues.apache.org/jira/browse/CAMEL-24322)

camel-openai tool-calling via AiToolRegistry

[CAMEL-23397](https://issues.apache.org/jira/browse/CAMEL-23397)

camel-openai: Support tool annotations/hints for returnDirect and safety classification

### Task (5)

[CAMEL-24579](https://issues.apache.org/jira/browse/CAMEL-24579)

DataFormat.marshal graph parameter should be @Nullable

[CAMEL-24572](https://issues.apache.org/jira/browse/CAMEL-24572)

Use xtokenize as a language in the YAML DSL

[CAMEL-24549](https://issues.apache.org/jira/browse/CAMEL-24549)

camel-google-storage: Use symlink-aware containment for local downloads

[CAMEL-24548](https://issues.apache.org/jira/browse/CAMEL-24548)

camel-azure-storage: Use symlink-aware containment for local downloads

[CAMEL-24420](https://issues.apache.org/jira/browse/CAMEL-24420)

camel-hazelcast: Apply the default JavaSerializationFilterConfig to Camel-built client configurations

### Test (3)

[CAMEL-24597](https://issues.apache.org/jira/browse/CAMEL-24597)

Fix flaky test MailAttachmentDuplicateNamesTest.testSendAndReceiveMailWithAttachmentsWithDuplicateNames <Hello World> but was: <jakarta.mail.internet.MimeMultipart@XXXXX>

[CAMEL-24469](https://issues.apache.org/jira/browse/CAMEL-24469)

Crashed tests: org.apache.camel.dsl.jbang.core.common.PluginHelperTest on 4.22.x branch

[CAMEL-24458](https://issues.apache.org/jira/browse/CAMEL-24458)

Cassandra Integration Tests are broken on s390x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).