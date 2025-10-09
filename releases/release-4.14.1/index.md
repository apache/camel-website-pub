# Apache camel 4.14.1 Release

## New and Noteworthy

This release is the new Camel 4.14.1 LTS release.

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
      <version>4.14.1</version>
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
      <version>4.14.1</version>
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
| [apache-camel-4.14.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-src.zip.sha512) |
| [apache-camel-4.14.1-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.xml.sha512) |
| [apache-camel-4.14.1-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.1/apache-camel-4.14.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (18)

[CAMEL-22418](https://issues.apache.org/jira/browse/CAMEL-22418)

camel run broken when --runtime quarkus|spring-boot

[CAMEL-22416](https://issues.apache.org/jira/browse/CAMEL-22416)

camel-jbang - Customize server port not working

[CAMEL-22410](https://issues.apache.org/jira/browse/CAMEL-22410)

SchedulingPollConsumer is not thread safe during graceful shutdown.

[CAMEL-22407](https://issues.apache.org/jira/browse/CAMEL-22407)

camel-jbang-plugin-kubernetes: --config and --resource fails when setting a key or destination file path

[CAMEL-22405](https://issues.apache.org/jira/browse/CAMEL-22405)

camel-ai: agent is unable to support different data types

[CAMEL-22404](https://issues.apache.org/jira/browse/CAMEL-22404)

camel-jbang-plugin-kubernetes: duplicate declaration of camel:observability-services in pom.xml

[CAMEL-22397](https://issues.apache.org/jira/browse/CAMEL-22397)

camel-ai: cannot create multiple agents due to missing route information

[CAMEL-22391](https://issues.apache.org/jira/browse/CAMEL-22391)

camel-core - Disabled does not work for inlined anonymous processors in Java DSL

[CAMEL-22385](https://issues.apache.org/jira/browse/CAMEL-22385)

OpenTelemetry: Unclosed Span Scope with Parallel Multicast

[CAMEL-22384](https://issues.apache.org/jira/browse/CAMEL-22384)

camel-catalog - The route.json for autoStartup should be boolean type

[CAMEL-22380](https://issues.apache.org/jira/browse/CAMEL-22380)

camel-platform-http-main - Authentication path does not work

[CAMEL-22373](https://issues.apache.org/jira/browse/CAMEL-22373)

camel-http - Headers may be lost when calling HTTP service fails and exception is thrown

[CAMEL-22366](https://issues.apache.org/jira/browse/CAMEL-22366)

camel-spring-boot - Nested property placeholder is turned off by mistake

[CAMEL-22364](https://issues.apache.org/jira/browse/CAMEL-22364)

camel-jms - Rare ConcurrentModificationException on message header map when using multiple camel-jms calls after each other in route

[CAMEL-22363](https://issues.apache.org/jira/browse/CAMEL-22363)

camel-azure - EventHub consumer updates checkout on every event

[CAMEL-22359](https://issues.apache.org/jira/browse/CAMEL-22359)

camel-as2: MDN multipart/report parsing issue with no Content-Type

[CAMEL-22335](https://issues.apache.org/jira/browse/CAMEL-22335)

camel jbang kubernetes manifest options not picked up from application.properties

[CAMEL-22094](https://issues.apache.org/jira/browse/CAMEL-22094)

camel-openapi-java - Rest DSL with code-first - ClassCastException in openapi v3.1 parsing complex types

### Dependency upgrade (2)

[CAMEL-22394](https://issues.apache.org/jira/browse/CAMEL-22394)

camel-vertx - Upgrade to 4.5.20

[CAMEL-22344](https://issues.apache.org/jira/browse/CAMEL-22344)

camel-spring-boot - Upgrade to SB 3.5.5

### Improvement (14)

[CAMEL-22453](https://issues.apache.org/jira/browse/CAMEL-22453)

camel-sql - SQL query should support java text blocks

[CAMEL-22441](https://issues.apache.org/jira/browse/CAMEL-22441)

components with supportFileReference should support resource: prefix

[CAMEL-22438](https://issues.apache.org/jira/browse/CAMEL-22438)

camel-catalog - Enum should be type: enum in catalog metadata

[CAMEL-22435](https://issues.apache.org/jira/browse/CAMEL-22435)

Camel CLI Infra run - use the default port for custom implementations

[CAMEL-22430](https://issues.apache.org/jira/browse/CAMEL-22430)

Make FileLockClusterView more resilient to split-brain scenarios

[CAMEL-22422](https://issues.apache.org/jira/browse/CAMEL-22422)

\[camel-telemetry\] exclude processors when added in the filter

[CAMEL-22403](https://issues.apache.org/jira/browse/CAMEL-22403)

\[camel-google-pubsub\] Extend headers with some HeaderFilterStrategy

[CAMEL-22400](https://issues.apache.org/jira/browse/CAMEL-22400)

camel-zipfile - Add support for empty zip files / entries

[CAMEL-22398](https://issues.apache.org/jira/browse/CAMEL-22398)

camel-ai: allow agents to define the specifics of the exchange body

[CAMEL-22387](https://issues.apache.org/jira/browse/CAMEL-22387)

camel-quartz graceful shutdown issue

[CAMEL-22381](https://issues.apache.org/jira/browse/CAMEL-22381)

camel-platform-http-vertx - Do not log ERROR for unauthenticated requests

[CAMEL-22368](https://issues.apache.org/jira/browse/CAMEL-22368)

camel-catalog - Add support for validating JQ language

[CAMEL-22362](https://issues.apache.org/jira/browse/CAMEL-22362)

camel-exec - Use quote safe arg parser

[CAMEL-21268](https://issues.apache.org/jira/browse/CAMEL-21268)

Google PubSub - pass headers (breadcrumb+) from publisher to subscriber

### New Feature (1)

[CAMEL-22423](https://issues.apache.org/jira/browse/CAMEL-22423)

Make Camel extensible from 3d party dependencies via ServiceLoader

### Task (9)

[CAMEL-22450](https://issues.apache.org/jira/browse/CAMEL-22450)

Camel JBang update dependency is failing when kamelet is missing some mandatory parameters in a Pipe file

[CAMEL-22448](https://issues.apache.org/jira/browse/CAMEL-22448)

Camel JBang dependency update is not adding dependency for component in Intercept/Intercept From/Intercept Send To Endpoint

[CAMEL-22447](https://issues.apache.org/jira/browse/CAMEL-22447)

Camel JBang Dependency update is not adding dependencies iif there is an OnException not configured

[CAMEL-22446](https://issues.apache.org/jira/browse/CAMEL-22446)

Camel JBang update dependency is failing for Avro Kamelet

[CAMEL-22444](https://issues.apache.org/jira/browse/CAMEL-22444)

Camel JBang update dependency is failing with NPE when Bean component is not yet configured

[CAMEL-22443](https://issues.apache.org/jira/browse/CAMEL-22443)

Camel JBang update dependency is failing when component/kamelet/processor is missing some mandatory parameters

[CAMEL-22413](https://issues.apache.org/jira/browse/CAMEL-22413)

Provide kamelet component vs. kamelet EIP info in catalog

[CAMEL-22386](https://issues.apache.org/jira/browse/CAMEL-22386)

camel-catalog - Some components with boolean option should have defaultValue as boolean type in json metadata

[CAMEL-22371](https://issues.apache.org/jira/browse/CAMEL-22371)

camel-ognl - Deprecate

### Test (1)

[CAMEL-22399](https://issues.apache.org/jira/browse/CAMEL-22399)

camel-aws-sqs - SqsBatchConsumerConcurrentConsumersIT test failure

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).