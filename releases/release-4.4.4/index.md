# Apache camel 4.4.4 Release

## New and Noteworthy

This release is the new Camel 4.4.4 LTS patch release.

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
      <version>4.4.4</version>
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
      <version>4.4.4</version>
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
| [apache-camel-4.4.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-src.zip.sha512) |
| [apache-camel-4.4.4-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.xml.sha512) |
| [apache-camel-4.4.4-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.4.4/apache-camel-4.4.4-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.4.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.4.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (21)

[CAMEL-21329](https://issues.apache.org/jira/browse/CAMEL-21329)

camel-zipfile (and camel-tarfile) - Null body is not supported by ZipAggregationStrategy

[CAMEL-21306](https://issues.apache.org/jira/browse/CAMEL-21306)

camel-jsonpath - Null should be accepted return value

[CAMEL-21293](https://issues.apache.org/jira/browse/CAMEL-21293)

camel-core - Unmarshal processor should close InputStream after processing

[CAMEL-21239](https://issues.apache.org/jira/browse/CAMEL-21239)

camel-report-maven-plugin - NPE if route does not have id

[CAMEL-21211](https://issues.apache.org/jira/browse/CAMEL-21211)

camel-azure-servicebus - Default header filter strategy can try to propagate headers of types not supported by the Service Bus protocol

[CAMEL-21164](https://issues.apache.org/jira/browse/CAMEL-21164)

camel-rest - Code first should use actual values for property placeholders in dumped API spec

[CAMEL-21161](https://issues.apache.org/jira/browse/CAMEL-21161)

camel-aws2-s3 is uploading always files as multipart when multiPartUpload is set true

[CAMEL-21154](https://issues.apache.org/jira/browse/CAMEL-21154)

camel-hashicorp-vault: Potential NPE in getSecret operation result handling

[CAMEL-21112](https://issues.apache.org/jira/browse/CAMEL-21112)

camel-sql - Simple language to lookup parameter value is not compatible with batch mode

[CAMEL-21109](https://issues.apache.org/jira/browse/CAMEL-21109)

Choice evaluation behaves inconsistently when source is String and Value is Float.

[CAMEL-21101](https://issues.apache.org/jira/browse/CAMEL-21101)

Camel-Hashicorp-Vault: Get Secret operation doesn't take into account the secretPath configuration parameter

[CAMEL-21057](https://issues.apache.org/jira/browse/CAMEL-21057)

REST OpenApi fails to resolve host from the URL

[CAMEL-21048](https://issues.apache.org/jira/browse/CAMEL-21048)

MLLP ACK invalid timestamp

[CAMEL-21044](https://issues.apache.org/jira/browse/CAMEL-21044)

azure-servicebus: FQNS not set correctly when credentialType is AZURE\_IDENTITY

[CAMEL-21033](https://issues.apache.org/jira/browse/CAMEL-21033)

camel-jbang-plugin-k run command kebab-case parsing on uppercase

[CAMEL-20995](https://issues.apache.org/jira/browse/CAMEL-20995)

camel-azure-storage-blob uploadBlockBlob retry operation fails due to mark and reset issue / Flux

[CAMEL-20988](https://issues.apache.org/jira/browse/CAMEL-20988)

camel-test-infra: some services are unable to properly log initialization failures

[CAMEL-20954](https://issues.apache.org/jira/browse/CAMEL-20954)

Cannot share SSLContextParameters between camel-kafka and other components

[CAMEL-20938](https://issues.apache.org/jira/browse/CAMEL-20938)

camel-http - Using disableStreamCache=true cannot read body later due to stream closed

[CAMEL-20932](https://issues.apache.org/jira/browse/CAMEL-20932)

camel-core - Error handler redelivery options should support template parameters for route templates

[CAMEL-20921](https://issues.apache.org/jira/browse/CAMEL-20921)

Route configuration is not loaded on a Camel application XML file

### Dependency upgrade (5)

[CAMEL-21344](https://issues.apache.org/jira/browse/CAMEL-21344)

Update OpenTelemetry dependencies to use out of the box thread-pool functionality

[CAMEL-21299](https://issues.apache.org/jira/browse/CAMEL-21299)

camel-avro - Upgrade to 1.11.4

[CAMEL-21231](https://issues.apache.org/jira/browse/CAMEL-21231)

camel-jq - The JQ library is not as active maintaned

[CAMEL-21230](https://issues.apache.org/jira/browse/CAMEL-21230)

camel-spring-boot - Upgrade to SB 3.2.10

[CAMEL-21113](https://issues.apache.org/jira/browse/CAMEL-21113)

camel-spring-boot - Upgrade to 3.2.9

### Improvement (13)

[CAMEL-21309](https://issues.apache.org/jira/browse/CAMEL-21309)

camel-cxf - When Exchange is using otel then run synchronous to avoid leaking spans

[CAMEL-21303](https://issues.apache.org/jira/browse/CAMEL-21303)

camel-core - Tone down logging noise for IOHelper close

[CAMEL-21300](https://issues.apache.org/jira/browse/CAMEL-21300)

camel-platform-http - Consumer should have option to control if writing response failing should cause Exchange to fail

[CAMEL-21286](https://issues.apache.org/jira/browse/CAMEL-21286)

Add a cache to JAXB object factories on JAXB Marshalling/Fallback converter

[CAMEL-21261](https://issues.apache.org/jira/browse/CAMEL-21261)

camel-opentelemetry does not use it's context propagators

[CAMEL-21260](https://issues.apache.org/jira/browse/CAMEL-21260)

camel-cxf - Allow to configure synchronous on component level

[CAMEL-21255](https://issues.apache.org/jira/browse/CAMEL-21255)

camel-core - Add listener for creating ThreadFactory in ExecutorServiceManager

[CAMEL-21089](https://issues.apache.org/jira/browse/CAMEL-21089)

camel-core: CamelBaseBulkConverterLoader should handle conversion to byte primitive

[CAMEL-21064](https://issues.apache.org/jira/browse/CAMEL-21064)

camel-as2 - Be case insensitive in http header parsing

[CAMEL-21053](https://issues.apache.org/jira/browse/CAMEL-21053)

camel-xslt - All exchange properties should be avaiable

[CAMEL-20852](https://issues.apache.org/jira/browse/CAMEL-20852)

Allow empty files within ZipAggregationStrategy

[CAMEL-20821](https://issues.apache.org/jira/browse/CAMEL-20821)

camel-opentelemetry - Add traceProcessors boolean option

[CAMEL-20643](https://issues.apache.org/jira/browse/CAMEL-20643)

camel-opentelemetry - OpenTelemetryTracingStrategy does not propagate OpenTelemetry Context in some cases

### New Feature (1)

[CAMEL-21202](https://issues.apache.org/jira/browse/CAMEL-21202)

Add a ThreadPoolFactory to propagate OpenTelemetry contexts

### Test (1)

[CAMEL-21297](https://issues.apache.org/jira/browse/CAMEL-21297)

camel-test-infra-dispatch-router not working due to SEGFAULT in running qdrouterd

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).