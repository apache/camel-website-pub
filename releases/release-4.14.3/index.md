# Apache camel 4.14.3 Release

## New and Noteworthy

This release is the new Camel 4.14.3 LTS release.

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
      <version>4.14.3</version>
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
      <version>4.14.3</version>
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
| [apache-camel-4.14.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-src.zip.sha512) |
| [apache-camel-4.14.3-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.xml.sha512) |
| [apache-camel-4.14.3-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.3/apache-camel-4.14.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (21)

[CAMEL-22772](https://issues.apache.org/jira/browse/CAMEL-22772)

Freemarker shared variables not respected when using dynamic templates

[CAMEL-22762](https://issues.apache.org/jira/browse/CAMEL-22762)

aws2-sqs: queue URL stays null if the queue is created after the application has already started

[CAMEL-22754](https://issues.apache.org/jira/browse/CAMEL-22754)

Additional route step after a body is set to Response may alter the HTTP code in the Response

[CAMEL-22749](https://issues.apache.org/jira/browse/CAMEL-22749)

\[camel-kafka/camel-observation\] tracing fails for Kafka consumer with multiple topics

[CAMEL-22743](https://issues.apache.org/jira/browse/CAMEL-22743)

camel-jbang - get platfomr-http with --all does not show management

[CAMEL-22741](https://issues.apache.org/jira/browse/CAMEL-22741)

pollEnrich EIP doesn't preserve the original headers

[CAMEL-22695](https://issues.apache.org/jira/browse/CAMEL-22695)

camel-jbang: --observe flag being ignored

[CAMEL-22691](https://issues.apache.org/jira/browse/CAMEL-22691)

camel-cxf - Memory leak in CXF producer

[CAMEL-22667](https://issues.apache.org/jira/browse/CAMEL-22667)

camel-jbang - Using --stub with none existing may cause timer to not trigger

[CAMEL-22660](https://issues.apache.org/jira/browse/CAMEL-22660)

camel-jbang - Use --stub=all should only stub components

[CAMEL-22659](https://issues.apache.org/jira/browse/CAMEL-22659)

Aggregator completionInterval not working during shutdown

[CAMEL-22658](https://issues.apache.org/jira/browse/CAMEL-22658)

\[camel-google-pubsub\] GooglePubsubProducer fails with INVALID\_ARGUMENT

[CAMEL-22657](https://issues.apache.org/jira/browse/CAMEL-22657)

camel-jbang - NPE in row clone

[CAMEL-22656](https://issues.apache.org/jira/browse/CAMEL-22656)

camel-jbang - Using --prompt ask for location of some internal main property

[CAMEL-22651](https://issues.apache.org/jira/browse/CAMEL-22651)

camel-jbang - Using --stub does not work correct with multiple patterns

[CAMEL-22645](https://issues.apache.org/jira/browse/CAMEL-22645)

http-component - oauth2BodyAuthentication not being stipped out of URI

[CAMEL-22638](https://issues.apache.org/jira/browse/CAMEL-22638)

camel-jbang - Using jolokia should allow camel hawtio to connect

[CAMEL-22627](https://issues.apache.org/jira/browse/CAMEL-22627)

Camel fails graceful shutdown with wiretap/kamelet

[CAMEL-22625](https://issues.apache.org/jira/browse/CAMEL-22625)

AvroDataFormat unmarshal fails for union with logicalType

[CAMEL-22557](https://issues.apache.org/jira/browse/CAMEL-22557)

camel-as2 - Server-side DecryptingPrivateKey Conflict: Key from first route started is enforced for all subsequent routes on the same serverPortNumber

[CAMEL-22529](https://issues.apache.org/jira/browse/CAMEL-22529)

route configuration in Java DSL with multiple onException does not work

### Dependency upgrade (2)

[CAMEL-22757](https://issues.apache.org/jira/browse/CAMEL-22757)

camel-tika - Upgrade to tika 3.x

[CAMEL-22701](https://issues.apache.org/jira/browse/CAMEL-22701)

camel-spring-boot - Upgrade to 3.5.8

### Improvement (5)

[CAMEL-22761](https://issues.apache.org/jira/browse/CAMEL-22761)

camel-jbang - Pick Maven repositories provided on Camel JBang for actions related to Kamelet

[CAMEL-22742](https://issues.apache.org/jira/browse/CAMEL-22742)

camel-core - Rest DSL contract first should have jmx statistics

[CAMEL-22719](https://issues.apache.org/jira/browse/CAMEL-22719)

camel-neo4j - Improve detection of message body

[CAMEL-22628](https://issues.apache.org/jira/browse/CAMEL-22628)

camel-console - Add information to route dev console if route is created by template/kamelet

[CAMEL-22623](https://issues.apache.org/jira/browse/CAMEL-22623)

Regression: CamelNettySSLClientCertSubjectName changed from readable string representation to obscure RFC2253 format

### Task (1)

[CAMEL-22643](https://issues.apache.org/jira/browse/CAMEL-22643)

docs: http-component - oauth2BodyAuthentication

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).