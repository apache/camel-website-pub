# Apache camel 4.14.9 Release

## New and Noteworthy

This release is the new Camel 4.14.9 LTS release.

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
      <version>4.14.9</version>
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
      <version>4.14.9</version>
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
| [apache-camel-4.14.9-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-src.zip.sha512) |
| [apache-camel-4.14.9-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.xml.sha512) |
| [apache-camel-4.14.9-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.9/apache-camel-4.14.9-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.9` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.9

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (24)

[CAMEL-24360](https://issues.apache.org/jira/browse/CAMEL-24360)

camel-undertow - UndertowEndpoint discards the UndertowHeaderFilterStrategy set by DefaultUndertowHttpBinding

[CAMEL-24354](https://issues.apache.org/jira/browse/CAMEL-24354)

camel-aws2-lambda: updateFunction never sets the code source, so UpdateFunctionCode always fails

[CAMEL-24343](https://issues.apache.org/jira/browse/CAMEL-24343)

camel-google-calendar: stream consumer can skip events and only reads the first page

[CAMEL-24341](https://issues.apache.org/jira/browse/CAMEL-24341)

camel-google-secret-manager: GCP vault refresh task reads the AWS vault configuration and reloads repeatedly

[CAMEL-24251](https://issues.apache.org/jira/browse/CAMEL-24251)

camel-aws2 producer health checks can throw NPE when AwsServiceException has no error details

[CAMEL-24249](https://issues.apache.org/jira/browse/CAMEL-24249)

camel-aws2 MSK/MQ/STS producers throw copy-pasted IllegalArgumentException messages naming the wrong parameter

[CAMEL-24248](https://issues.apache.org/jira/browse/CAMEL-24248)

Concurrent pollEnrich can fail to stop in-use consumers after cache eviction

[CAMEL-24244](https://issues.apache.org/jira/browse/CAMEL-24244)

camel-base-engine: DefaultStreamCachingStrategy.updateSpool calls lock() instead of unlock() in finally, blocking other threads forever

[CAMEL-24243](https://issues.apache.org/jira/browse/CAMEL-24243)

camel-aws2-athena: a still-running query is relaunched when waitTimeout expires and maxAttempts > 1

[CAMEL-24238](https://issues.apache.org/jira/browse/CAMEL-24238)

camel-aws2-ses: a RawMessage body is sent as the SdkBytes descriptor instead of the message content

[CAMEL-24231](https://issues.apache.org/jira/browse/CAMEL-24231)

pollEnrich with dynamic fileName using exchangeProperty fails due to missing properties in dummy exchange

[CAMEL-24201](https://issues.apache.org/jira/browse/CAMEL-24201)

camel-aws2-step-functions: listExecutions never sets stateMachineArn so the operation always fails

[CAMEL-24200](https://issues.apache.org/jira/browse/CAMEL-24200)

camel-aws2-timestream: createScheduledQuery writes the time column into tableName and never sets timeColumn

[CAMEL-24194](https://issues.apache.org/jira/browse/CAMEL-24194)

camel-aws-config: removeConformancePack reads the wrong header (RULE\_NAME instead of the conformance pack name)

[CAMEL-24193](https://issues.apache.org/jira/browse/CAMEL-24193)

camel-aws-secrets-manager: SQS-notification secret-refresh NPEs on missing queue and never drains the queue

[CAMEL-24191](https://issues.apache.org/jira/browse/CAMEL-24191)

camel-aws2-kinesis: KCL consumer ignores session credentials and mishandles checkpoint/error handling

[CAMEL-24169](https://issues.apache.org/jira/browse/CAMEL-24169)

camel-jackson-avro / camel-jackson-protobuf - schema resolver latches the first resolved schema forever, breaking multi-type routes

[CAMEL-24158](https://issues.apache.org/jira/browse/CAMEL-24158)

camel-azure - Umbrella: high-severity findings from July 2026 review (storage-blob, servicebus, eventhubs, storage-queue, storage-datalake)

[CAMEL-24086](https://issues.apache.org/jira/browse/CAMEL-24086)

camel-aws2-sqs: FIFO batch send assigns the same MessageDeduplicationId to every entry

[CAMEL-24082](https://issues.apache.org/jira/browse/CAMEL-24082)

camel-aws-cloudtrail: consumer loses events (static cursor, no pagination, time-window skip)

[CAMEL-24080](https://issues.apache.org/jira/browse/CAMEL-24080)

camel-aws2-kinesis: consumer shard state is not thread-safe when consuming multiple shards

[CAMEL-23895](https://issues.apache.org/jira/browse/CAMEL-23895)

\[camel-azure-servicebus\] http 401 using connection string

[CAMEL-23844](https://issues.apache.org/jira/browse/CAMEL-23844)

Camel-PQC: extractSecretKeyFromEncapsulation uses the raw enum name instead of the mapped JCE algorithm name

[CAMEL-23843](https://issues.apache.org/jira/browse/CAMEL-23843)

Camel-PQC: sign/verify only handle String payloads and use the platform default charset

### Improvement (11)

[CAMEL-24359](https://issues.apache.org/jira/browse/CAMEL-24359)

camel-atmosphere-websocket - align Exchange header constant names with Camel naming convention

[CAMEL-24299](https://issues.apache.org/jira/browse/CAMEL-24299)

camel-core: set SUPPORT\_DTD=false in XmlStreamDetector for consistency with other XML parsers

[CAMEL-24279](https://issues.apache.org/jira/browse/CAMEL-24279)

camel-google-storage: contain downloadFileName downloads within the configured directory

[CAMEL-24240](https://issues.apache.org/jira/browse/CAMEL-24240)

camel-fhir: Align all FHIR core dependencies

[CAMEL-24085](https://issues.apache.org/jira/browse/CAMEL-24085)

camel-ironmq: apply header filter strategy when mapping message envelope headers

[CAMEL-24084](https://issues.apache.org/jira/browse/CAMEL-24084)

camel-knative: apply header filter strategy to structured-mode CloudEvent extension headers

[CAMEL-23942](https://issues.apache.org/jira/browse/CAMEL-23942)

camel-azure-storage-blob / camel-azure-storage-datalake: contain fileDir downloads within the configured directory

[CAMEL-23891](https://issues.apache.org/jira/browse/CAMEL-23891)

camel-mail: apply inbound Camel\* header filtering in MimeMultipartDataFormat unmarshal (headersInline=true), consistent with the mail consumer

[CAMEL-23868](https://issues.apache.org/jira/browse/CAMEL-23868)

camel-file: make local work directory / starting directory containment checks path-boundary aware

[CAMEL-23766](https://issues.apache.org/jira/browse/CAMEL-23766)

camel-crypto: use a constant-time comparison for HMAC verification in HMACAccumulator

[CAMEL-23525](https://issues.apache.org/jira/browse/CAMEL-23525)

camel-platform-http-main: add optional JWT issuer and audience claim validation

### Task (2)

[CAMEL-24204](https://issues.apache.org/jira/browse/CAMEL-24204)

camel-jms - exposeListenerSession catalog metadata reports wrong default value (false instead of true)

[CAMEL-21314](https://issues.apache.org/jira/browse/CAMEL-21314)

camel-aws - Fix S3CopyObjectCustomerKeyIT.sendIn which is failing on main branch

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).