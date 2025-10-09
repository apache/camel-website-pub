# Apache camel 4.18.1 Release

## New and Noteworthy

This release is the new Camel 4.18.1 LTS release.

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
      <version>4.18.1</version>
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
      <version>4.18.1</version>
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
| [apache-camel-4.18.1-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.1/apache-camel-4.18.1-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-src.zip.sha512) |
| [apache-camel-4.18.1-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.xml.sha512) |
| [apache-camel-4.18.1-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.1/apache-camel-4.18.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (29)

[CAMEL-23288](https://issues.apache.org/jira/browse/CAMEL-23288)

JBang - Issues with kubernetes plugin when exporting with a selected runtime

[CAMEL-23191](https://issues.apache.org/jira/browse/CAMEL-23191)

Path parameters incorrectly extracted when server.servlet.context-path is configured

[CAMEL-23174](https://issues.apache.org/jira/browse/CAMEL-23174)

Kamelet: transformer in aws-ddb-sink is not executed

[CAMEL-23123](https://issues.apache.org/jira/browse/CAMEL-23123)

S3Presigner does not honor forcePathStyle configuration in createDownloadLink/createUploadLink operations

[CAMEL-23122](https://issues.apache.org/jira/browse/CAMEL-23122)

camel-core - DefaultErrorHandler with logExhausted(false) still logs

[CAMEL-23116](https://issues.apache.org/jira/browse/CAMEL-23116)

CamelContext is never stopped when using @TestInstance(Lifecycle.PER\_CLASS) with CamelTestSupport

[CAMEL-23115](https://issues.apache.org/jira/browse/CAMEL-23115)

camel-openapi-java - base.path option will never survive if context-path is set

[CAMEL-23106](https://issues.apache.org/jira/browse/CAMEL-23106)

camel-docling - Remove temp file in DoclingProducer.getInputPath()

[CAMEL-23105](https://issues.apache.org/jira/browse/CAMEL-23105)

camel-docling - Fix broken async conversion workflow (discarded result and error masking)

[CAMEL-23101](https://issues.apache.org/jira/browse/CAMEL-23101)

camel-minio error writing to object store

[CAMEL-23100](https://issues.apache.org/jira/browse/CAMEL-23100)

camel-bom has SNAPSHOT in camel-bom 4.18.0 release

[CAMEL-23062](https://issues.apache.org/jira/browse/CAMEL-23062)

camel-openai: encodingFormat option does not take effect

[CAMEL-23061](https://issues.apache.org/jira/browse/CAMEL-23061)

camel-sql - SqlConsumer NPE if using exchange factory statistics

[CAMEL-23051](https://issues.apache.org/jira/browse/CAMEL-23051)

camel-yaml-dsl-validator - Tooling for offline validate should support property placeholders

[CAMEL-23036](https://issues.apache.org/jira/browse/CAMEL-23036)

camel-core - NPE when pooled exchange in split at UoW done

[CAMEL-23035](https://issues.apache.org/jira/browse/CAMEL-23035)

camel-core - Simple language using colon or question mark can conflict with ternary operator

[CAMEL-23033](https://issues.apache.org/jira/browse/CAMEL-23033)

camel-yaml-dsl - Setting routePolicy on route should be routePolicyRef

[CAMEL-23032](https://issues.apache.org/jira/browse/CAMEL-23032)

camel-nats consumer sends ACK regardless of the Exchange processing/delivery result

[CAMEL-23031](https://issues.apache.org/jira/browse/CAMEL-23031)

Regression from CAMEL-22354 in camel-csv

[CAMEL-23030](https://issues.apache.org/jira/browse/CAMEL-23030)

Streaming splitter with aggregation using synchronous executor results in StackOverflowError

[CAMEL-23028](https://issues.apache.org/jira/browse/CAMEL-23028)

camel-jbang - Transform route with transacted does not include following steps

[CAMEL-23024](https://issues.apache.org/jira/browse/CAMEL-23024)

camel-jbang - Route dumper for YAML with setHeaders / setVariables EIP

[CAMEL-23023](https://issues.apache.org/jira/browse/CAMEL-23023)

camel-kafka - Kafka consumers are started to eager before CamelContext is fully started

[CAMEL-23018](https://issues.apache.org/jira/browse/CAMEL-23018)

camel-rest-openapi - Response operation with content-type by no schema causes NPE

[CAMEL-23015](https://issues.apache.org/jira/browse/CAMEL-23015)

camel-jbang - YAML DSL dump of route with Saga EIP does not dump completion/compensation correctly

[CAMEL-23012](https://issues.apache.org/jira/browse/CAMEL-23012)

camel-jbang - Resequence EIP route dump to YAML is wrong for batch config

[CAMEL-23011](https://issues.apache.org/jira/browse/CAMEL-23011)

camel-mcp - camel\_catalog\_components returns Internal Server Error

[CAMEL-23002](https://issues.apache.org/jira/browse/CAMEL-23002)

camel plugin add xyz - should ignore the gav in the camel-jbang-user.properties

[CAMEL-21932](https://issues.apache.org/jira/browse/CAMEL-21932)

Kubernetes Secrets and Config maps context reloading doesn't work together

### Dependency upgrade (3)

[CAMEL-23163](https://issues.apache.org/jira/browse/CAMEL-23163)

camel-spring-boot - Upgrade to 3.5.12

[CAMEL-23027](https://issues.apache.org/jira/browse/CAMEL-23027)

camel-spring-boot - Upgrade to SB 3.5.11

[CAMEL-23026](https://issues.apache.org/jira/browse/CAMEL-23026)

camel-cxf - Upgrade to CXF 4.1.5

### Improvement (18)

[CAMEL-23224](https://issues.apache.org/jira/browse/CAMEL-23224)

camel-mail - MailHeaderFilterStrategy should also filter inbound headers

[CAMEL-23222](https://issues.apache.org/jira/browse/CAMEL-23222)

camel-coap: Integrate HeaderFilterStrategy for CoAP query parameter to header mapping

[CAMEL-23169](https://issues.apache.org/jira/browse/CAMEL-23169)

camel-jbang - Export to camel main as fat-jar should can cause overrides in META-INF services files that camel-jq needs

[CAMEL-23119](https://issues.apache.org/jira/browse/CAMEL-23119)

camel-launcher - Add validate plugin

[CAMEL-23114](https://issues.apache.org/jira/browse/CAMEL-23114)

camel-jbang - camel version list - Add --vendor flag

[CAMEL-23111](https://issues.apache.org/jira/browse/CAMEL-23111)

camel-jbang - camel run - YAML parsing errors not published to OTEL

[CAMEL-23107](https://issues.apache.org/jira/browse/CAMEL-23107)

camel-docling - Add CLI command validation in buildDoclingCommand

[CAMEL-23094](https://issues.apache.org/jira/browse/CAMEL-23094)

camel-core - Saga EIP fix model for completion and compensation

[CAMEL-23085](https://issues.apache.org/jira/browse/CAMEL-23085)

camel-nats - Make more options configurable on component level

[CAMEL-23084](https://issues.apache.org/jira/browse/CAMEL-23084)

camel-jbang - camel infra log - May log duplicate

[CAMEL-23081](https://issues.apache.org/jira/browse/CAMEL-23081)

camel-milo - Allow overriding the server reported endpoint port

[CAMEL-23048](https://issues.apache.org/jira/browse/CAMEL-23048)

camel-core - Simple init block to require using semi colon to end each variable

[CAMEL-23047](https://issues.apache.org/jira/browse/CAMEL-23047)

camel-core - Add val function to simple

[CAMEL-23046](https://issues.apache.org/jira/browse/CAMEL-23046)

camel-mail - Auto start IdempotentRepository

[CAMEL-23029](https://issues.apache.org/jira/browse/CAMEL-23029)

Camel-Consul: Add ObjectInputFilter String pattern parameter in ConsulRegistry to be used in deserialize operations

[CAMEL-23025](https://issues.apache.org/jira/browse/CAMEL-23025)

camel-core - Tokenizer language should work with \\n out of the box in XML and YAML DSL

[CAMEL-23003](https://issues.apache.org/jira/browse/CAMEL-23003)

camel-test-infra - Align Jackson JARs for testcontainers

[CAMEL-23000](https://issues.apache.org/jira/browse/CAMEL-23000)

camel-ssh - idleTimeout

### New Feature (1)

[CAMEL-23142](https://issues.apache.org/jira/browse/CAMEL-23142)

camel-google-pubsub: Add maxDeliveryAttempts enforcement to prevent infinite redelivery loops

### Task (3)

[CAMEL-23103](https://issues.apache.org/jira/browse/CAMEL-23103)

camel-json-patch - Deprecate

[CAMEL-23099](https://issues.apache.org/jira/browse/CAMEL-23099)

Remove camel-test references

[CAMEL-23055](https://issues.apache.org/jira/browse/CAMEL-23055)

Camel-Jbang: Upgrade to Camel-Kamelets 4.18.0

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).