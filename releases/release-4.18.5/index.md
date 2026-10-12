# Apache camel 4.18.5 Release

## New and Noteworthy

This release is the new Camel 4.18.5 LTS release.

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
      <version>4.18.5</version>
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
      <version>4.18.5</version>
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
| [apache-camel-4.18.5-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.5/apache-camel-4.18.5-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-src.zip.sha512) |
| [apache-camel-4.18.5-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.xml.sha512) |
| [apache-camel-4.18.5-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.5/apache-camel-4.18.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (75)

[CAMEL-25437](https://issues.apache.org/jira/browse/CAMEL-25437)

camel-jbang - camel run --prop key=value with a space is silently ignored

[CAMEL-25227](https://issues.apache.org/jira/browse/CAMEL-25227)

camel-azure-eventhubs: partition header conflict and no default header filter

[CAMEL-25164](https://issues.apache.org/jira/browse/CAMEL-25164)

camel-infinispan - the aggregation repositories recover a completed exchange without the message that completed the group

[CAMEL-25103](https://issues.apache.org/jira/browse/CAMEL-25103)

camel-vertx - Client authentication, cipher suites and protocols of SSLContextParameters are not applied

[CAMEL-25085](https://issues.apache.org/jira/browse/CAMEL-25085)

Rest DSL: under json/xml binding a response without Content-Type ignores the verb's produces

[CAMEL-25023](https://issues.apache.org/jira/browse/CAMEL-25023)

camel-util - IOHelper.copy counts copied bytes in an int, so zipFile/tarFile maxDecompressedSize values of 2 GiB or more are not enforced

[CAMEL-24973](https://issues.apache.org/jira/browse/CAMEL-24973)

camel-util - URISupport.sanitizeUri does not follow the endpoint URI parser for RAW values, userinfo, dash-case option names and additional keywords

[CAMEL-24935](https://issues.apache.org/jira/browse/CAMEL-24935)

camel-pulsar - the producer replaces the message body with the MessageId

[CAMEL-24932](https://issues.apache.org/jira/browse/CAMEL-24932)

camel-pulsar - the polling loop dies on a NullPointerException when a receive fails

[CAMEL-24811](https://issues.apache.org/jira/browse/CAMEL-24811)

camel-servlet - async=true without executorRef completes the AsyncContext before a truly-asynchronous route finishes

[CAMEL-24691](https://issues.apache.org/jira/browse/CAMEL-24691)

camel-saxon - align XQueryBuilder with secure XML parsing defaults

[CAMEL-24668](https://issues.apache.org/jira/browse/CAMEL-24668)

Camel MLLP consumer discards pipelined HL7 messages that arrive in a single TCP read

[CAMEL-24651](https://issues.apache.org/jira/browse/CAMEL-24651)

Regression on Camel 4.x NPE on evaluation of a Simple expression ${exception.stacktrace}

[CAMEL-24632](https://issues.apache.org/jira/browse/CAMEL-24632)

SSLException when GET/POST to https endpoint with proxy setting using camel-http component

[CAMEL-24630](https://issues.apache.org/jira/browse/CAMEL-24630)

camel-kamelet: supervised route reload creates duplicate internal routes and causes context console NPE

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

[CAMEL-24573](https://issues.apache.org/jira/browse/CAMEL-24573)

CXF REST: UnsupportedOperationException when copying factory bean with fixed-size features list

[CAMEL-24545](https://issues.apache.org/jira/browse/CAMEL-24545)

Camel Shutdown Locked State With ZookeeprCluster Service

[CAMEL-24535](https://issues.apache.org/jira/browse/CAMEL-24535)

camel-tensorflow-serving: the Target and Credentials headers are declared but never read

[CAMEL-24534](https://issues.apache.org/jira/browse/CAMEL-24534)

camel-qdrant: the embeddings data-type transformer casts every metadata value to String

[CAMEL-24530](https://issues.apache.org/jira/browse/CAMEL-24530)

camel-djl: DJLConverter leaks the InputStream opened from File/Path bodies

[CAMEL-24529](https://issues.apache.org/jira/browse/CAMEL-24529)

camel-djl: the loaded ZooModel is never closed (native-memory leak on restart)

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

[CAMEL-24475](https://issues.apache.org/jira/browse/CAMEL-24475)

camel-xpath - documentType=InputSource evaluates the payload with an unhardened XML parser

[CAMEL-24470](https://issues.apache.org/jira/browse/CAMEL-24470)

camel-ibm-secrets-manager: IBMEventStreamReloadTriggerTask rejects Event Stream credentials provided via environment variables

[CAMEL-24468](https://issues.apache.org/jira/browse/CAMEL-24468)

camel-ibm-secrets-manager - fix defects in IBMSecretsManagerPropertiesFunction (env-var credentials rejected, secret version pin ignored, missing KV field returns "null")

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

[CAMEL-24409](https://issues.apache.org/jira/browse/CAMEL-24409)

rest-dsl - Binary data corrupted by rest client request validator

[CAMEL-24408](https://issues.apache.org/jira/browse/CAMEL-24408)

SEDA discardIfNoConsumers breaks after consumer removal when sharing the same URI

[CAMEL-24407](https://issues.apache.org/jira/browse/CAMEL-24407)

simple predicate fails for long digital strings

[CAMEL-24392](https://issues.apache.org/jira/browse/CAMEL-24392)

BacklogTracerRouteAdvice drains non-re-readable InputStream body before stream caching

[CAMEL-24382](https://issues.apache.org/jira/browse/CAMEL-24382)

camel-azure-cosmosdb: change-feed consumer checkpoints the lease before the exchange is processed, losing events on failure

[CAMEL-24380](https://issues.apache.org/jira/browse/CAMEL-24380)

camel-spring-boot - Regression in platform-http/platform-http-starter timeout handling

[CAMEL-24350](https://issues.apache.org/jira/browse/CAMEL-24350)

camel-google-pubsub: producer NPEs on non-convertible headers and drops non-Exchange list elements

[CAMEL-24349](https://issues.apache.org/jira/browse/CAMEL-24349)

camel-google-functions: createFunction fails with an opaque NPE when required headers are missing

[CAMEL-24348](https://issues.apache.org/jira/browse/CAMEL-24348)

camel-google-bigquery: NPEs on a null body or unknown job id, and insertId is ignored for List bodies

[CAMEL-24346](https://issues.apache.org/jira/browse/CAMEL-24346)

camel-google-sheets: splitResults always reports range index 1 and NPEs on an empty range

[CAMEL-24345](https://issues.apache.org/jira/browse/CAMEL-24345)

camel-google-vertexai: streamOutputMode and jsonMode options are never applied

[CAMEL-24344](https://issues.apache.org/jira/browse/CAMEL-24344)

camel-google-mail: raw option always returns a null body and non-multipart messages produce no body

[CAMEL-24342](https://issues.apache.org/jira/browse/CAMEL-24342)

camel-google-storage: producer sets wrong blob metadata and NPEs on missing objects

### Improvement (33)

[CAMEL-25225](https://issues.apache.org/jira/browse/CAMEL-25225)

camel-spring-ws: apply the HeaderFilterStrategy to producer response headers

[CAMEL-25197](https://issues.apache.org/jira/browse/CAMEL-25197)

camel-cli-connector - add a WebSocket transport so developer tools can drive running integrations

[CAMEL-25162](https://issues.apache.org/jira/browse/CAMEL-25162)

camel-oauth - confine the reconstructed post-login URL to the configured redirect URI origin

[CAMEL-25087](https://issues.apache.org/jira/browse/CAMEL-25087)

camel-coap - add a muteException consumer option

[CAMEL-24936](https://issues.apache.org/jira/browse/CAMEL-24936)

camel-netty: NettyConverter.toByteArray should copy only the readable bytes of the ByteBuf

[CAMEL-24902](https://issues.apache.org/jira/browse/CAMEL-24902)

camel-keycloak: honor token expiry (exp) when caching introspection results

[CAMEL-24901](https://issues.apache.org/jira/browse/CAMEL-24901)

camel-aws2-s3: restrict Simple expression evaluation of key/bucket to configured values

[CAMEL-24894](https://issues.apache.org/jira/browse/CAMEL-24894)

camel-docling: make output path handling consistent with input path and custom-argument handling

[CAMEL-24893](https://issues.apache.org/jira/browse/CAMEL-24893)

camel-docling: also constrain absolute paths in custom-argument path validation

[CAMEL-24677](https://issues.apache.org/jira/browse/CAMEL-24677)

camel-smooks: align XML reader configuration with the other XML components

[CAMEL-24676](https://issues.apache.org/jira/browse/CAMEL-24676)

camel-jgroups: add a configurable deserialization filter and document serialization hardening for the consumer

[CAMEL-24653](https://issues.apache.org/jira/browse/CAMEL-24653)

SSLCertTrustTest: replace external badssl.com dependency with local self-signed HTTPS endpoint

[CAMEL-24652](https://issues.apache.org/jira/browse/CAMEL-24652)

camel-servlet, camel-jetty, camel-platform-http-vertx - consolidate the fileNameExtWhitelist check and tighten the extension match

[CAMEL-24650](https://issues.apache.org/jira/browse/CAMEL-24650)

camel-http-common: lift the multipart fileNameExtWhitelist check into DefaultHttpBinding

[CAMEL-24627](https://issues.apache.org/jira/browse/CAMEL-24627)

camel-file: resolve symlinks when containing local work directory downloads (parity with camel-azure/google-storage)

[CAMEL-24605](https://issues.apache.org/jira/browse/CAMEL-24605)

camel-fop: align FopProducer XML transformation with Camel's standard secure XML processing configuration

[CAMEL-24577](https://issues.apache.org/jira/browse/CAMEL-24577)

camel-platform-http-starter - path variable headers are derived from the undecoded request URI

[CAMEL-24576](https://issues.apache.org/jira/browse/CAMEL-24576)

camel-dynamic-router: align control endpoint parameter handling with the allowTemplateFromHeader convention

[CAMEL-24574](https://issues.apache.org/jira/browse/CAMEL-24574)

camel-google-bigquery - clarify that ${name} is literal substitution and steer value parameters to @name

[CAMEL-24504](https://issues.apache.org/jira/browse/CAMEL-24504)

camel-spring-boot - extend the SpringTypeConverter String guard beyond InputStream targets

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

[CAMEL-24437](https://issues.apache.org/jira/browse/CAMEL-24437)

camel-oauth - authorization code flow sends no state, nonce or PKCE parameter

[CAMEL-24428](https://issues.apache.org/jira/browse/CAMEL-24428)

camel-knative - add a muteException consumer option

[CAMEL-24422](https://issues.apache.org/jira/browse/CAMEL-24422)

camel-docling: make message body input-source interpretation explicit and configurable

[CAMEL-24421](https://issues.apache.org/jira/browse/CAMEL-24421)

camel-spring-redis: apply a configurable ObjectInputFilter to the default JDK serializer

### Task (5)

[CAMEL-24900](https://issues.apache.org/jira/browse/CAMEL-24900)

camel-jcr - apply header filtering when mapping JCR node properties to Exchange headers

[CAMEL-24895](https://issues.apache.org/jira/browse/CAMEL-24895)

camel-mustache, camel-chunk - align Exchange header constant names with Camel naming convention

[CAMEL-24549](https://issues.apache.org/jira/browse/CAMEL-24549)

camel-google-storage: Use symlink-aware containment for local downloads

[CAMEL-24548](https://issues.apache.org/jira/browse/CAMEL-24548)

camel-azure-storage: Use symlink-aware containment for local downloads

[CAMEL-24420](https://issues.apache.org/jira/browse/CAMEL-24420)

camel-hazelcast: Apply the default JavaSerializationFilterConfig to Camel-built client configurations

### Test (1)

[CAMEL-24480](https://issues.apache.org/jira/browse/CAMEL-24480)

CliConfigITCase.setLocalMavenRepoTest is broken on 4.18.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).