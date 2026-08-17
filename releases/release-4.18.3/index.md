# Apache camel 4.18.3 Release

## New and Noteworthy

This release is the new Camel 4.18.3 LTS release.

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
      <version>4.18.3</version>
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
      <version>4.18.3</version>
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
| [apache-camel-4.18.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-src.zip.sha512) |
| [apache-camel-4.18.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.xml.sha512) |
| [apache-camel-4.18.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.18.3/apache-camel-4.18.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (33)

[CAMEL-23834](https://issues.apache.org/jira/browse/CAMEL-23834)

camel-smb forward slashes rejected on Windows System STATUS\_OBJECT\_NAME\_INVALID

[CAMEL-23828](https://issues.apache.org/jira/browse/CAMEL-23828)

camel export --quarkus-version is ignored — registry resolution overwrites the user-specified version

[CAMEL-23821](https://issues.apache.org/jira/browse/CAMEL-23821)

camel-jbang: camel validate plugin doesn't find any files

[CAMEL-23814](https://issues.apache.org/jira/browse/CAMEL-23814)

camel-core - Optional secret property placeholders in YAML DSL parameters not stripped due to RAW() wrapping

[CAMEL-23811](https://issues.apache.org/jira/browse/CAMEL-23811)

camel-micrometer: app.info gauge value uses weak reference causing NaN values

[CAMEL-23805](https://issues.apache.org/jira/browse/CAMEL-23805)

HTTP endpoint summary not logged on startup when supervised route controller is enabled

[CAMEL-23740](https://issues.apache.org/jira/browse/CAMEL-23740)

LangChain4jAgentConverter WrappedFile converter fails for FTP/SFTP GenericFile — requires manual convertBodyTo workaround

[CAMEL-23739](https://issues.apache.org/jira/browse/CAMEL-23739)

camel-openai: support WrappedFile, byte\[\], and InputStream bodies for vision models

[CAMEL-23730](https://issues.apache.org/jira/browse/CAMEL-23730)

AggregateReifier.mandatoryLookup fails during export dry-run even with lazyBean=true

[CAMEL-23729](https://issues.apache.org/jira/browse/CAMEL-23729)

camel-google-secret-manager: NoClassDefFoundError due to protobuf 3.x/4.x version mismatch

[CAMEL-23698](https://issues.apache.org/jira/browse/CAMEL-23698)

camel-rest-openapi - Producer appends trailing ? to URL when no query parameters are set

[CAMEL-23646](https://issues.apache.org/jira/browse/CAMEL-23646)

BackgroundTask callbacks return inverted boolean in sjms, pgevent, and master causing infinite retry loops after successful recovery

[CAMEL-23627](https://issues.apache.org/jira/browse/CAMEL-23627)

Exception not caught when Slack returns a response code > 299

[CAMEL-23571](https://issues.apache.org/jira/browse/CAMEL-23571)

Google PubSub component leaves orphaned channels when using PubSub emulator

[CAMEL-23547](https://issues.apache.org/jira/browse/CAMEL-23547)

camel-core - Properties component should eager start custom functions resolver

[CAMEL-23523](https://issues.apache.org/jira/browse/CAMEL-23523)

camel-kafka: batchingIntervalMs timer not reset on new accumulation cycle, causing premature single-message batches after idle periods

[CAMEL-23513](https://issues.apache.org/jira/browse/CAMEL-23513)

completeAllOnStop() does not complete aggregations when used with completionInterval()

[CAMEL-23505](https://issues.apache.org/jira/browse/CAMEL-23505)

camel-splunk-hec: align hostname verification with system default in SplunkHECProducer

[CAMEL-23504](https://issues.apache.org/jira/browse/CAMEL-23504)

camel-keycloak: KeycloakSecurityHelper.parseAndVerifyAccessToken should include the IS\_ACTIVE predicate on TokenVerifier

[CAMEL-23494](https://issues.apache.org/jira/browse/CAMEL-23494)

preparingShutdown flag not reset on error handlers after suspend/resume — causes silent transaction rollback and redelivery suppression

[CAMEL-23469](https://issues.apache.org/jira/browse/CAMEL-23469)

Infinite redelivery loop when child route with NoErrorHandler uses removeHeaders("\*")

[CAMEL-23461](https://issues.apache.org/jira/browse/CAMEL-23461)

Camel-AWS-Bedrock: applyGuardrail reads guardrail identifier from wrong header

[CAMEL-23448](https://issues.apache.org/jira/browse/CAMEL-23448)

camel-launcher jolokia fails to attach agent — JAR path unresolvable from nested Spring Boot JAR

[CAMEL-23422](https://issues.apache.org/jira/browse/CAMEL-23422)

camel-spring-rabbitmq - Exported camel-jbang project with RabbitMQ consumer not consuming messages anymore on runtime main

[CAMEL-23419](https://issues.apache.org/jira/browse/CAMEL-23419)

camel-nats - Consumer does not work in pull mode

[CAMEL-23384](https://issues.apache.org/jira/browse/CAMEL-23384)

camel-kamelet-main: camel export fails with IllegalArgumentException on kamelets using transformDataType EIP

[CAMEL-23378](https://issues.apache.org/jira/browse/CAMEL-23378)

camel-spring-boot - Block String to InputStream conversion in SpringTypeConverter

[CAMEL-23355](https://issues.apache.org/jira/browse/CAMEL-23355)

camel-jbang: export with kamelet aws-ddb-sink - transformer aws2-ddb is not working

[CAMEL-23334](https://issues.apache.org/jira/browse/CAMEL-23334)

JBang plugin resolution checks remote repositories on every CLI invocation even when artifacts are cached locally

[CAMEL-23291](https://issues.apache.org/jira/browse/CAMEL-23291)

EventHubs and Google PubSub consumers lack ShutdownAware support, causing potential message loss during graceful shutdown

[CAMEL-23192](https://issues.apache.org/jira/browse/CAMEL-23192)

jbang export to quarkus generates wrong dockerfiles

[CAMEL-23124](https://issues.apache.org/jira/browse/CAMEL-23124)

camel-docling - Fix CLI mode ProcessBuilder deadlock with sequential stream reading

[CAMEL-23120](https://issues.apache.org/jira/browse/CAMEL-23120)

camel-docling - Implement batchSize sub-batch partitioning in batch processing

### Dependency upgrade (2)

[CAMEL-23731](https://issues.apache.org/jira/browse/CAMEL-23731)

camel-spring-boot - Upgrade to SB 3.5.15

[CAMEL-23401](https://issues.apache.org/jira/browse/CAMEL-23401)

Upgrade JSch to 2.28.2 (RSA certificate authentication fix)

### Improvement (46)

[CAMEL-23803](https://issues.apache.org/jira/browse/CAMEL-23803)

camel-jackson-avro / camel-jackson-protobuf: block unsafe polymorphic base types by default in the data format ObjectMapper

[CAMEL-23787](https://issues.apache.org/jira/browse/CAMEL-23787)

camel-jacksonxml: block unsafe polymorphic base types by default in the XmlMapper

[CAMEL-23786](https://issues.apache.org/jira/browse/CAMEL-23786)

camel-jackson: block unsafe polymorphic base types by default in the data format ObjectMapper

[CAMEL-23783](https://issues.apache.org/jira/browse/CAMEL-23783)

camel-schematron: harden the rules TransformerFactory against external entities (XXE)

[CAMEL-23782](https://issues.apache.org/jira/browse/CAMEL-23782)

camel-leveldb: apply an ObjectInputFilter to aggregation-repository key deserialization

[CAMEL-23765](https://issues.apache.org/jira/browse/CAMEL-23765)

camel-ftp/sftp/mina-sftp/azure-files/smb: contain localWorkDirectory downloads within the work directory

[CAMEL-23762](https://issues.apache.org/jira/browse/CAMEL-23762)

camel-whatsapp: support X-Hub-Signature-256 verification of inbound webhook payloads

[CAMEL-23760](https://issues.apache.org/jira/browse/CAMEL-23760)

camel-oauth: require a JWK set to verify token signatures in UserProfile

[CAMEL-23759](https://issues.apache.org/jira/browse/CAMEL-23759)

camel-spring-ws: apply a HeaderFilterStrategy to inbound SOAP headers

[CAMEL-23738](https://issues.apache.org/jira/browse/CAMEL-23738)

camel-keycloak: always verify the access token in KeycloakSecurityPolicy regardless of configured roles/permissions

[CAMEL-23726](https://issues.apache.org/jira/browse/CAMEL-23726)

camel-pqc: Use JSON instead of Java serialization for key metadata in AWS and HashiCorp Vault lifecycle managers

[CAMEL-23716](https://issues.apache.org/jira/browse/CAMEL-23716)

camel-salesforce - align Exchange header constant names with Camel naming convention

[CAMEL-23651](https://issues.apache.org/jira/browse/CAMEL-23651)

camel-netty-http and camel-undertow: align muteException default with the other HTTP components

[CAMEL-23630](https://issues.apache.org/jira/browse/CAMEL-23630)

camel-dapr - add HeaderFilterStrategy and avoid copying routing-relevant CloudEvent fields into Camel exchange headers

[CAMEL-23629](https://issues.apache.org/jira/browse/CAMEL-23629)

camel-irc - align Exchange header constant names with Camel naming convention

[CAMEL-23621](https://issues.apache.org/jira/browse/CAMEL-23621)

camel-langchain4j-tools / camel-langchain4j-agent / camel-spring-ai-tools: tool argument headers should be filtered against declared parameters

[CAMEL-23597](https://issues.apache.org/jira/browse/CAMEL-23597)

camel-solr - align Exchange header prefix constants with Camel naming convention

[CAMEL-23588](https://issues.apache.org/jira/browse/CAMEL-23588)

camel-undertow - align websocket header names with Camel naming convention (CAMEL-23532 follow-on)

[CAMEL-23584](https://issues.apache.org/jira/browse/CAMEL-23584)

camel-kafka - align Exchange header constant names with Camel naming convention

[CAMEL-23576](https://issues.apache.org/jira/browse/CAMEL-23576)

camel-jira - align Exchange header constant names with Camel naming convention

[CAMEL-23575](https://issues.apache.org/jira/browse/CAMEL-23575)

camel-mongodb-gridfs: align Exchange header constant names with Camel naming convention

[CAMEL-23574](https://issues.apache.org/jira/browse/CAMEL-23574)

camel-dns - align Exchange header constant names with Camel naming convention

[CAMEL-23532](https://issues.apache.org/jira/browse/CAMEL-23532)

camel-vertx-websocket / camel-atmosphere-websocket / camel-iggy - use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23528](https://issues.apache.org/jira/browse/CAMEL-23528)

camel-neo4j: validate property names when building MATCH/DELETE WHERE clause

[CAMEL-23526](https://issues.apache.org/jira/browse/CAMEL-23526)

camel-cxf: align Exchange header constant names with Camel naming convention

[CAMEL-23524](https://issues.apache.org/jira/browse/CAMEL-23524)

camel-couchdb / camel-couchbase - align Exchange header constant values with Camel naming convention

[CAMEL-23522](https://issues.apache.org/jira/browse/CAMEL-23522)

camel-mail: filter mail.smtp.\* / mail.smtps.\* namespace from producer headers

[CAMEL-23516](https://issues.apache.org/jira/browse/CAMEL-23516)

camel-xmpp - Use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23515](https://issues.apache.org/jira/browse/CAMEL-23515)

camel-nats - Use dedicated HeaderFilterStrategy aligned with sibling components

[CAMEL-23511](https://issues.apache.org/jira/browse/CAMEL-23511)

camel-jgroups-raft: align Exchange header constant names with Camel naming convention

[CAMEL-23510](https://issues.apache.org/jira/browse/CAMEL-23510)

camel-jgroups: align Exchange header constant names with Camel naming convention

[CAMEL-23509](https://issues.apache.org/jira/browse/CAMEL-23509)

camel-lucene: align Exchange header constant names with Camel naming convention

[CAMEL-23508](https://issues.apache.org/jira/browse/CAMEL-23508)

camel-elasticsearch-rest-client: align Exchange header constant names with Camel naming convention

[CAMEL-23507](https://issues.apache.org/jira/browse/CAMEL-23507)

camel-cometd: Integrate HeaderFilterStrategy for inbound header mapping

[CAMEL-23506](https://issues.apache.org/jira/browse/CAMEL-23506)

camel-aws2-sqs / camel-aws2-sns - align HeaderFilterStrategy with sibling components

[CAMEL-23409](https://issues.apache.org/jira/browse/CAMEL-23409)

camel-sjms - Disable ObjectMessage by default

[CAMEL-23399](https://issues.apache.org/jira/browse/CAMEL-23399)

camel-mina - Upgrade to 2.2.7

[CAMEL-23379](https://issues.apache.org/jira/browse/CAMEL-23379)

camel-core - DefaultHeaderFilterStrategy should be lower-case by default

[CAMEL-23373](https://issues.apache.org/jira/browse/CAMEL-23373)

camel-jms - Disable ObjectMessage by default

[CAMEL-23372](https://issues.apache.org/jira/browse/CAMEL-23372)

Tighten default ObjectInputFilter to deny java.net.\*\* before java.\*\*

[CAMEL-23363](https://issues.apache.org/jira/browse/CAMEL-23363)

camel-platform-http-main - NPE if you enable healt-check but lack JAR

[CAMEL-23353](https://issues.apache.org/jira/browse/CAMEL-23353)

camel-jbang: Support configurable default Maven repositories and dynamic Quarkus platform version resolution from registry

[CAMEL-23324](https://issues.apache.org/jira/browse/CAMEL-23324)

camel-vertx-http, camel-netty-http - Add deserialization filtering in helper utilities

[CAMEL-23320](https://issues.apache.org/jira/browse/CAMEL-23320)

camel-platform-http-starter - Fix binary data corruption due to Spring Boot's default UTF-8 charset

[CAMEL-23312](https://issues.apache.org/jira/browse/CAMEL-23312)

Opentelemetry2: SpanLifecycleManager.create() missing SpanKind parameter causing incorrect span types

[CAMEL-23212](https://issues.apache.org/jira/browse/CAMEL-23212)

Camel-Docling: Harden CLI argument injection validation in camel-docling

### Task (1)

[CAMEL-23414](https://issues.apache.org/jira/browse/CAMEL-23414)

camel-hazelcast: Allow customization of SerializationConfig on managed Hazelcast instances

### Test (2)

[CAMEL-23754](https://issues.apache.org/jira/browse/CAMEL-23754)

CustomJarsITCase.testCustomJars is broken on 4.18.x

[CAMEL-23725](https://issues.apache.org/jira/browse/CAMEL-23725)

CI sometimes stay blocked on InOutQueueProducerAsyncLoadTest for 4.18.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).