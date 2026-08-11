# Apache camel 4.14.8 Release

## New and Noteworthy

This release is the new Camel 4.14.8 LTS release.

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
      <version>4.14.8</version>
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
      <version>4.14.8</version>
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
| [apache-camel-4.14.8-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-src.zip.sha512) |
| [apache-camel-4.14.8-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.xml.sha512) |
| [apache-camel-4.14.8-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.8/apache-camel-4.14.8-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.8` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.8

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (3)

[CAMEL-23523](https://issues.apache.org/jira/browse/CAMEL-23523)

camel-kafka: batchingIntervalMs timer not reset on new accumulation cycle, causing premature single-message batches after idle periods

[CAMEL-23513](https://issues.apache.org/jira/browse/CAMEL-23513)

completeAllOnStop() does not complete aggregations when used with completionInterval()

[CAMEL-23505](https://issues.apache.org/jira/browse/CAMEL-23505)

camel-splunk-hec: align hostname verification with system default in SplunkHECProducer

### Dependency upgrade (1)

[CAMEL-23748](https://issues.apache.org/jira/browse/CAMEL-23748)

camel-spring-boot - Upgrade to 3.5.15

### Improvement (38)

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

[CAMEL-23716](https://issues.apache.org/jira/browse/CAMEL-23716)

camel-salesforce - align Exchange header constant names with Camel naming convention

[CAMEL-23651](https://issues.apache.org/jira/browse/CAMEL-23651)

camel-netty-http and camel-undertow: align muteException default with the other HTTP components

[CAMEL-23630](https://issues.apache.org/jira/browse/CAMEL-23630)

camel-dapr - add HeaderFilterStrategy and avoid copying routing-relevant CloudEvent fields into Camel exchange headers

[CAMEL-23629](https://issues.apache.org/jira/browse/CAMEL-23629)

camel-irc - align Exchange header constant names with Camel naming convention

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

[CAMEL-23324](https://issues.apache.org/jira/browse/CAMEL-23324)

camel-vertx-http, camel-netty-http - Add deserialization filtering in helper utilities

### Task (1)

[CAMEL-23414](https://issues.apache.org/jira/browse/CAMEL-23414)

camel-hazelcast: Allow customization of SerializationConfig on managed Hazelcast instances

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).