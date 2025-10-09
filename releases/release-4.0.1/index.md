# Apache camel 4.0.1 Release

## New and Noteworthy

This release is the new Camel 4.0.1 LTS patch release.

## Supported Java version

This version supports Java 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.0.1</version>
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
      <version>4.0.1</version>
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
| [apache-camel-4.0.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.1/apache-camel-4.0.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.1/apache-camel-4.0.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.1/apache-camel-4.0.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (32)

[CAMEL-19895](https://issues.apache.org/jira/browse/CAMEL-19895)

Camel JBang dependency copy --output-directory doesn't respect absolute path

[CAMEL-19885](https://issues.apache.org/jira/browse/CAMEL-19885)

Default auth scope on google-sheets-streams not working

[CAMEL-19878](https://issues.apache.org/jira/browse/CAMEL-19878)

camel-main - Using Camel- as context name causes ENV name clash running on Kubernetes

[CAMEL-19875](https://issues.apache.org/jira/browse/CAMEL-19875)

HealthCheck is broken for KafkaConsumer

[CAMEL-19870](https://issues.apache.org/jira/browse/CAMEL-19870)

Camel AS2: Should accept MDN field name Disposition as case insensitive

[CAMEL-19859](https://issues.apache.org/jira/browse/CAMEL-19859)

camel-spring-rabbitmq set headerfilter not effective

[CAMEL-19857](https://issues.apache.org/jira/browse/CAMEL-19857)

Cannot run Kotlin DSL 1.8 in a fatjar

[CAMEL-19843](https://issues.apache.org/jira/browse/CAMEL-19843)

HTTP/2 pseudo-headers such as :status should not be propagated from CXF message to Camel message

[CAMEL-19842](https://issues.apache.org/jira/browse/CAMEL-19842)

camel-zookeeper-master: fix MasterEndpointFailoverIT

[CAMEL-19822](https://issues.apache.org/jira/browse/CAMEL-19822)

camel-azure-files - assert failure in the implementation of move=

[CAMEL-19818](https://issues.apache.org/jira/browse/CAMEL-19818)

camel-openapi-java - A response type containing an array generates incorrect schema reference

[CAMEL-19815](https://issues.apache.org/jira/browse/CAMEL-19815)

camel-seda: cached queue reference can become invalid

[CAMEL-19814](https://issues.apache.org/jira/browse/CAMEL-19814)

camel-rest - Should filter out query parameters that are for the producer endpoint

[CAMEL-19811](https://issues.apache.org/jira/browse/CAMEL-19811)

camel-aws - Restore multi-shard handling in Kinesis

[CAMEL-19798](https://issues.apache.org/jira/browse/CAMEL-19798)

Inconsistent camel-kamelets version in Camel JBang

[CAMEL-19789](https://issues.apache.org/jira/browse/CAMEL-19789)

Kinesis2Consumer repeatedly reads first record in stream

[CAMEL-19785](https://issues.apache.org/jira/browse/CAMEL-19785)

camel-yaml-dsl - Order of beans should not matter

[CAMEL-19784](https://issues.apache.org/jira/browse/CAMEL-19784)

camel-core - PropertyBindingSupport - mandatory reference should fail if cannot resolve bean

[CAMEL-19783](https://issues.apache.org/jira/browse/CAMEL-19783)

camel-salesforce - grpc will not resubscribe on connection failure if no messages have been received

[CAMEL-19780](https://issues.apache.org/jira/browse/CAMEL-19780)

Camel JBang does not support relative paths

[CAMEL-19777](https://issues.apache.org/jira/browse/CAMEL-19777)

camel-jms: toD endpoint with FQQN

[CAMEL-19775](https://issues.apache.org/jira/browse/CAMEL-19775)

camel-main: main duration event is not enabled for exchange completed

[CAMEL-19768](https://issues.apache.org/jira/browse/CAMEL-19768)

camel-http - HTTP message body encoded with wrong charset

[CAMEL-19766](https://issues.apache.org/jira/browse/CAMEL-19766)

Routes loaded with xml-io-dsl don't find associated routeConfiguration

[CAMEL-19764](https://issues.apache.org/jira/browse/CAMEL-19764)

camel-openapi - basic and bearer token

[CAMEL-19758](https://issues.apache.org/jira/browse/CAMEL-19758)

netty-http in proxy mode generates IllegalReferenceCountException for every success request.

[CAMEL-19756](https://issues.apache.org/jira/browse/CAMEL-19756)

camel-zeebe - ThrowError operation does not set Processor

[CAMEL-19738](https://issues.apache.org/jira/browse/CAMEL-19738)

camel-core - Loop EIP can have wrong pending inflight in case of early loop exit due to exception

[CAMEL-19737](https://issues.apache.org/jira/browse/CAMEL-19737)

camel-aws - SNS component subscription to SQS error

[CAMEL-19731](https://issues.apache.org/jira/browse/CAMEL-19731)

Camel-AS2: exception on empty response

[CAMEL-19729](https://issues.apache.org/jira/browse/CAMEL-19729)

camel-jbang - camel get route-dump should handle 2+ routes in the source files

[CAMEL-18759](https://issues.apache.org/jira/browse/CAMEL-18759)

camel-kafka - When Kafka pausable consumer is resumed, it reads all the messages from the earliest offset

### Dependency upgrade (3)

[CAMEL-19884](https://issues.apache.org/jira/browse/CAMEL-19884)

pooled-jms - Upgrade to 3.1.3

[CAMEL-19881](https://issues.apache.org/jira/browse/CAMEL-19881)

camel-spring-boot - Upgrade to 3.1.4

[CAMEL-19791](https://issues.apache.org/jira/browse/CAMEL-19791)

camel-spring-boot - Upgrade to 3.1.3

### Improvement (12)

[CAMEL-19890](https://issues.apache.org/jira/browse/CAMEL-19890)

camel-jbang - Downloading dependencies from a list with white spaces

[CAMEL-19888](https://issues.apache.org/jira/browse/CAMEL-19888)

Preserve openapi tags order while generating api-doc

[CAMEL-19852](https://issues.apache.org/jira/browse/CAMEL-19852)

Camel-platform-http-vertx: Always use normalized path from context

[CAMEL-19851](https://issues.apache.org/jira/browse/CAMEL-19851)

spring-boot Allow to configure timeouts natively

[CAMEL-19823](https://issues.apache.org/jira/browse/CAMEL-19823)

camel-spring-rabbitmq - Add allowNullBody as endpoint option

[CAMEL-19816](https://issues.apache.org/jira/browse/CAMEL-19816)

camel-platform-http-vertx: Add headers for local address & remote address

[CAMEL-19810](https://issues.apache.org/jira/browse/CAMEL-19810)

\[test-infra\] Inifinispan test container using podman

[CAMEL-19805](https://issues.apache.org/jira/browse/CAMEL-19805)

Support IntegrationSpec as part of Pipe/KameletBinding

[CAMEL-19776](https://issues.apache.org/jira/browse/CAMEL-19776)

Provide tracing strategy to trace each processor for OpenTelemetry

[CAMEL-19760](https://issues.apache.org/jira/browse/CAMEL-19760)

netty-http:prevent the usage of proxy protocol in producer endpoint

[CAMEL-19752](https://issues.apache.org/jira/browse/CAMEL-19752)

Usage of "doc" prefix in some elasticsearch operations are regression to camel-elasticsearch-rest

[CAMEL-19736](https://issues.apache.org/jira/browse/CAMEL-19736)

Environment variables with the name 'secret' aren't masked in logs

### New Feature (1)

[CAMEL-19876](https://issues.apache.org/jira/browse/CAMEL-19876)

Add maven-settings to camel-jbang export command

### Task (8)

[CAMEL-19871](https://issues.apache.org/jira/browse/CAMEL-19871)

camel-jooq - Set the proper scope to all test dependencies

[CAMEL-19867](https://issues.apache.org/jira/browse/CAMEL-19867)

spring-boot - Fix the integration test FhirUpdateIT

[CAMEL-19854](https://issues.apache.org/jira/browse/CAMEL-19854)

spring-boot - Fix the test KafkaConsumerHealthCheckIT

[CAMEL-19840](https://issues.apache.org/jira/browse/CAMEL-19840)

camel-core-api - Add a warning when the key store file cannot be found

[CAMEL-19782](https://issues.apache.org/jira/browse/CAMEL-19782)

\[DOCS\] Camel JPA wrong transaction manager documentation

[CAMEL-19751](https://issues.apache.org/jira/browse/CAMEL-19751)

camel-xchange: tests keep hitting the binance API

[CAMEL-19733](https://issues.apache.org/jira/browse/CAMEL-19733)

Migrate CRDs used from camel.apache.org/v1alpha1 to camel.apache.org/v1

[CAMEL-19732](https://issues.apache.org/jira/browse/CAMEL-19732)

KameletBinding renamed to Pipe

### Test (1)

[CAMEL-19669](https://issues.apache.org/jira/browse/CAMEL-19669)

camel-jms: fix flaky tests

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).