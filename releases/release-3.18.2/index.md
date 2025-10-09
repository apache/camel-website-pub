# Apache camel 3.18.2 Release

## New and Noteworthy

This release is the new Camel 3.18.2 LTS patch release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.18.2</version>
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
      <version>3.18.2</version>
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
| [apache-camel-3.18.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.18.2/apache-camel-3.18.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.18.2/apache-camel-3.18.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.18.2/apache-camel-3.18.2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.18.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.18.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (31)

[CAMEL-18444](https://issues.apache.org/jira/browse/CAMEL-18444)

camel-caffeine - Caffeine-cache query parameter action does not work

[CAMEL-18443](https://issues.apache.org/jira/browse/CAMEL-18443)

Problem using AdviceWith on routes with try-catch-finally

[CAMEL-18442](https://issues.apache.org/jira/browse/CAMEL-18442)

camel-github - Github commit consumer does not work

[CAMEL-18439](https://issues.apache.org/jira/browse/CAMEL-18439)

camel-github - Consumer that polls commits crashed when repository has more than 100 commits

[CAMEL-18435](https://issues.apache.org/jira/browse/CAMEL-18435)

camel-core - RAW values should be kept as-s

[CAMEL-18433](https://issues.apache.org/jira/browse/CAMEL-18433)

camel-yaml-dsl - Unsupported field: routeConfigurationId

[CAMEL-18432](https://issues.apache.org/jira/browse/CAMEL-18432)

DockerConfiguration malformerd UriPath for variable operation

[CAMEL-18424](https://issues.apache.org/jira/browse/CAMEL-18424)

camel-jbang - Dependency downloaded issue with camel-aws-s3

[CAMEL-18421](https://issues.apache.org/jira/browse/CAMEL-18421)

camel-core - Adding route dynamic leak bootstraps

[CAMEL-18418](https://issues.apache.org/jira/browse/CAMEL-18418)

aws-s3-sink Kamelet returns 403

[CAMEL-18405](https://issues.apache.org/jira/browse/CAMEL-18405)

camel-karaf - Camel-file ResumeAware

[CAMEL-18400](https://issues.apache.org/jira/browse/CAMEL-18400)

jbang does not use correct camel version

[CAMEL-18399](https://issues.apache.org/jira/browse/CAMEL-18399)

camel-sql - NullPointer exception for DBMaker PreparedStatement

[CAMEL-18396](https://issues.apache.org/jira/browse/CAMEL-18396)

NotifyBuilder.matches returns always true in conjunction with NotifyBuilderMatcher usage

[CAMEL-18394](https://issues.apache.org/jira/browse/CAMEL-18394)

CXF-Consumer does not start

[CAMEL-18393](https://issues.apache.org/jira/browse/CAMEL-18393)

Camel-bigquery: NPE if select \* is requested

[CAMEL-18391](https://issues.apache.org/jira/browse/CAMEL-18391)

camel-http - HttpSendDynamicAware not optimizing for url without slashes

[CAMEL-18387](https://issues.apache.org/jira/browse/CAMEL-18387)

camel-tarfile: TarAggregationStrategy throws error when first message is empty

[CAMEL-18379](https://issues.apache.org/jira/browse/CAMEL-18379)

camel-mail: attachments with empty fileName

[CAMEL-18377](https://issues.apache.org/jira/browse/CAMEL-18377)

camel-jpa producer does not reuse existing EntityManager in transaction and create its own one

[CAMEL-18375](https://issues.apache.org/jira/browse/CAMEL-18375)

Property description for FromDefinition is missing in camelYamlDsl.json

[CAMEL-18371](https://issues.apache.org/jira/browse/CAMEL-18371)

camel-resume-api: file component is not loading the cache

[CAMEL-18370](https://issues.apache.org/jira/browse/CAMEL-18370)

Bidning properties to route template local beans do not honor RAW()

[CAMEL-18362](https://issues.apache.org/jira/browse/CAMEL-18362)

camel-resume-api: kafka resume strategy fails to fetch the first batch

[CAMEL-18360](https://issues.apache.org/jira/browse/CAMEL-18360)

camel-jbang - Export --fresh with property placeholder using dash may fail

[CAMEL-18357](https://issues.apache.org/jira/browse/CAMEL-18357)

camel-core - Splitter issue with tokenizer with hashNext/next

[CAMEL-18355](https://issues.apache.org/jira/browse/CAMEL-18355)

HTTP component overwrites basic authentication credentials with proxy authentication

[CAMEL-18351](https://issues.apache.org/jira/browse/CAMEL-18351)

ExchangePropertyKey.SPLIT\_COMPLETE not set to true after zip splitting completed

[CAMEL-18347](https://issues.apache.org/jira/browse/CAMEL-18347)

camel-test-infra: instances are not properly singleton

[CAMEL-18328](https://issues.apache.org/jira/browse/CAMEL-18328)

RouteConfiguration with RouteTemplate doesn't work

[CAMEL-18049](https://issues.apache.org/jira/browse/CAMEL-18049)

Camel Webhook - error to set Webhook URL

### Dependency upgrade (5)

[CAMEL-18407](https://issues.apache.org/jira/browse/CAMEL-18407)

Align to spring-boot 2.7.3

[CAMEL-18365](https://issues.apache.org/jira/browse/CAMEL-18365)

camel-jsonpath - Upgrade to 2.7

[CAMEL-18361](https://issues.apache.org/jira/browse/CAMEL-18361)

camel-grpc: Upgrade gRPC to 1.48.1

[CAMEL-18344](https://issues.apache.org/jira/browse/CAMEL-18344)

Supporting camel "camel-google-pubsub" and "camel-grpc" OSGi deployment

[CAMEL-18179](https://issues.apache.org/jira/browse/CAMEL-18179)

Supporting camel-jira OSGi deployment

### Improvement (9)

[CAMEL-18450](https://issues.apache.org/jira/browse/CAMEL-18450)

camel-jpa: improve to use transaction strategy in JpaMessageIdRepository

[CAMEL-18429](https://issues.apache.org/jira/browse/CAMEL-18429)

camel-jbang - Shutdown timeout 10 sec by default

[CAMEL-18423](https://issues.apache.org/jira/browse/CAMEL-18423)

camel-microprofile-config: Handle NoSuchElementException in CamelMicroProfilePropertiesSource. loadProperties(Predicate<String> filter)

[CAMEL-18388](https://issues.apache.org/jira/browse/CAMEL-18388)

camel-jbang - add directory option to init to save to this folder

[CAMEL-18374](https://issues.apache.org/jira/browse/CAMEL-18374)

camel-core - Route template should be able to specify stream-caching option

[CAMEL-18373](https://issues.apache.org/jira/browse/CAMEL-18373)

camel-salesforce - Camel 3.18.x should support the new subscribe operation

[CAMEL-18368](https://issues.apache.org/jira/browse/CAMEL-18368)

Kamelet jslt-action not handling byte\[\] input

[CAMEL-18366](https://issues.apache.org/jira/browse/CAMEL-18366)

allow for per-route configuration of streamCaching in YAML

[CAMEL-18358](https://issues.apache.org/jira/browse/CAMEL-18358)

Support for mail attachments for camel freemarker

### New Feature (1)

[CAMEL-18426](https://issues.apache.org/jira/browse/CAMEL-18426)

camel-jbang - Export - Add support for local-kamelets-dir

### Task (5)

[CAMEL-18460](https://issues.apache.org/jira/browse/CAMEL-18460)

Duplicate dependency in camel-spring-boot-bom

[CAMEL-18428](https://issues.apache.org/jira/browse/CAMEL-18428)

Fhir component documentation describes the option password as the Username

[CAMEL-18422](https://issues.apache.org/jira/browse/CAMEL-18422)

Camel-AWS Component: Explicitly add AWS SDK Utils dependency

[CAMEL-18404](https://issues.apache.org/jira/browse/CAMEL-18404)

No documentation in camel-stax for XML DSL example

[CAMEL-18403](https://issues.apache.org/jira/browse/CAMEL-18403)

Improve controlbus docs

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).