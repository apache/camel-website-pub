# Apache camel 4.0.0-RC2 Release

## New and Noteworthy

This release is the second release candidate towards the Camel 4.0.0 release.

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
      <version>4.0.0-RC2</version>
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
      <version>4.0.0-RC2</version>
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
| [apache-camel-4.0.0-RC2-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC2/apache-camel-4.0.0-RC2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC2/apache-camel-4.0.0-RC2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.0.0-RC2/apache-camel-4.0.0-RC2-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-4.0.0-RC2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.0.0-RC2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (8)

[CAMEL-19607](https://issues.apache.org/jira/browse/CAMEL-19607)

camel-core - Checking redelivery reference while error handler creation

[CAMEL-19603](https://issues.apache.org/jira/browse/CAMEL-19603)

Spring Boot and Quarkus runtimes: @PeriodicTask annotated task are not running even if scheduled

[CAMEL-19570](https://issues.apache.org/jira/browse/CAMEL-19570)

Kafka max.poll.interval.ms declared in Long and not Integer

[CAMEL-19569](https://issues.apache.org/jira/browse/CAMEL-19569)

\[observability|opentelemetry\].CurrentSpanTest.testContextDoesNotLeak() fail on Github Actions

[CAMEL-19568](https://issues.apache.org/jira/browse/CAMEL-19568)

camel-mail - HTTP/2 Multipart boundary

[CAMEL-19566](https://issues.apache.org/jira/browse/CAMEL-19566)

Camel micrometer documentation shows wrong parameter value name for summary

[CAMEL-19511](https://issues.apache.org/jira/browse/CAMEL-19511)

camel-spring-boot - Register properly auto-configurations

[CAMEL-19343](https://issues.apache.org/jira/browse/CAMEL-19343)

Predicates are shared between templated routes in Java DSL with simple predicate builder

### Dependency upgrade (13)

[CAMEL-19625](https://issues.apache.org/jira/browse/CAMEL-19625)

maven - Upgrade to plexus-utils 4.x

[CAMEL-19624](https://issues.apache.org/jira/browse/CAMEL-19624)

Upgrade Derby used for testing

[CAMEL-19614](https://issues.apache.org/jira/browse/CAMEL-19614)

camel-openapi-rest-dsl-generator - Upgrade apicurio-data-models

[CAMEL-19612](https://issues.apache.org/jira/browse/CAMEL-19612)

camel-arangodb - Upgrade to 7.x

[CAMEL-19610](https://issues.apache.org/jira/browse/CAMEL-19610)

camel-rocketmq - Upgrade to rocket v5

[CAMEL-19606](https://issues.apache.org/jira/browse/CAMEL-19606)

camel-spring-boot - Upgrade to 3.1.2

[CAMEL-19605](https://issues.apache.org/jira/browse/CAMEL-19605)

camel-xchange - Upgrade to xchange 5.1.0

[CAMEL-19596](https://issues.apache.org/jira/browse/CAMEL-19596)

camel-javascript - Upgrade to graalvm 23.0

[CAMEL-19595](https://issues.apache.org/jira/browse/CAMEL-19595)

camel-kotlin - Upgrade to 1.9

[CAMEL-19594](https://issues.apache.org/jira/browse/CAMEL-19594)

camel-jbang - Upgrade to hawtio 2.17.5

[CAMEL-19589](https://issues.apache.org/jira/browse/CAMEL-19589)

camel-test - Upgrade testcontainers to 1.18.x

[CAMEL-19581](https://issues.apache.org/jira/browse/CAMEL-19581)

camel-jbang - Upgrade to picocli 4.7.4

[CAMEL-19442](https://issues.apache.org/jira/browse/CAMEL-19442)

Manage Gson to build and test with a single deterministic version

### Improvement (21)

[CAMEL-19616](https://issues.apache.org/jira/browse/CAMEL-19616)

camel-restdsl-openapi-plugin - Do not use servlet as component by default

[CAMEL-19615](https://issues.apache.org/jira/browse/CAMEL-19615)

camel-ftp: chmodDirectory option try for each junk to change the directory permission and fails

[CAMEL-19602](https://issues.apache.org/jira/browse/CAMEL-19602)

components - Add metadata for an option that refers to a file resource for tooling

[CAMEL-19592](https://issues.apache.org/jira/browse/CAMEL-19592)

camel-jbang - Export to camel-main should include platform-http for rest-dsl

[CAMEL-19587](https://issues.apache.org/jira/browse/CAMEL-19587)

camel-jira: optional header field IssueAssignee doesn't work

[CAMEL-19586](https://issues.apache.org/jira/browse/CAMEL-19586)

camel-parquet-avro - Allow users to unmarshal Parquet file into Avro's GenericRecords

[CAMEL-19585](https://issues.apache.org/jira/browse/CAMEL-19585)

camel-jbang - Report if dependency was downloaded or resolved

[CAMEL-19583](https://issues.apache.org/jira/browse/CAMEL-19583)

Lack of multiple shards consumption of Camel aws2 Kinesis

[CAMEL-19580](https://issues.apache.org/jira/browse/CAMEL-19580)

camel-catalog-maven - Add getClassLoader API

[CAMEL-19573](https://issues.apache.org/jira/browse/CAMEL-19573)

Stop syncing version properties in git, generate the effective camel-dependencies during the build

[CAMEL-19560](https://issues.apache.org/jira/browse/CAMEL-19560)

Manage micrometer artifacts to build and test with a single deterministic set of versions

[CAMEL-19559](https://issues.apache.org/jira/browse/CAMEL-19559)

Manage commons-codec to build and test with a single deterministic version

[CAMEL-19558](https://issues.apache.org/jira/browse/CAMEL-19558)

Manage protobuf to build and test with a single deterministic version

[CAMEL-19496](https://issues.apache.org/jira/browse/CAMEL-19496)

Manage single version of Guava

[CAMEL-19466](https://issues.apache.org/jira/browse/CAMEL-19466)

Skip Maven mojos in the fast profile properly

[CAMEL-19121](https://issues.apache.org/jira/browse/CAMEL-19121)

camel-jbang - Adapt to Camel v4

[CAMEL-19063](https://issues.apache.org/jira/browse/CAMEL-19063)

Find a replacement library for abdera & axiom in camel-atom & camel-rss

[CAMEL-18261](https://issues.apache.org/jira/browse/CAMEL-18261)

Add connection parameters to MongoDB component

[CAMEL-15978](https://issues.apache.org/jira/browse/CAMEL-15978)

camel-xmpp - Upgrade to 1.0.x

[CAMEL-14104](https://issues.apache.org/jira/browse/CAMEL-14104)

Update FHIR to latest version

[CAMEL-13611](https://issues.apache.org/jira/browse/CAMEL-13611)

Camel Web3j - Upgrade to Web3j 4.3.1

### New Feature (7)

[CAMEL-19601](https://issues.apache.org/jira/browse/CAMEL-19601)

camel-core - Limit auto conversion when stream caching is enabled

[CAMEL-19599](https://issues.apache.org/jira/browse/CAMEL-19599)

camel-jbang - Export to camel-main - Add support for Kubernetes

[CAMEL-19593](https://issues.apache.org/jira/browse/CAMEL-19593)

camel-main - Standalone web console

[CAMEL-19584](https://issues.apache.org/jira/browse/CAMEL-19584)

Camel aws2 Kinesis Asynchronous Client

[CAMEL-18916](https://issues.apache.org/jira/browse/CAMEL-18916)

camel-xslt-saxon: allow logger injection

[CAMEL-18837](https://issues.apache.org/jira/browse/CAMEL-18837)

Component for Opensearch

[CAMEL-16479](https://issues.apache.org/jira/browse/CAMEL-16479)

Camel-AWS-Kinesis: The consumer should be able to consume from multiple shards at the same time

### Task (19)

[CAMEL-19643](https://issues.apache.org/jira/browse/CAMEL-19643)

apache-camel - RC2 should include source tarball

[CAMEL-19634](https://issues.apache.org/jira/browse/CAMEL-19634)

camel-zeebe - Only download from Maven central

[CAMEL-19632](https://issues.apache.org/jira/browse/CAMEL-19632)

camel-xml-jaxp: Split package warning

[CAMEL-19630](https://issues.apache.org/jira/browse/CAMEL-19630)

camel-hyperledger-aries - Remove

[CAMEL-19629](https://issues.apache.org/jira/browse/CAMEL-19629)

camel-weka - Remove this component

[CAMEL-19628](https://issues.apache.org/jira/browse/CAMEL-19628)

Restrict downloading JARs from Atlassian Maven

[CAMEL-19621](https://issues.apache.org/jira/browse/CAMEL-19621)

camel-elytron - Deprecate this component

[CAMEL-19600](https://issues.apache.org/jira/browse/CAMEL-19600)

camel-atom: investigate potential test cleanups

[CAMEL-19563](https://issues.apache.org/jira/browse/CAMEL-19563)

Investigate usages of raw types

[CAMEL-19510](https://issues.apache.org/jira/browse/CAMEL-19510)

camel-spring-boot-examples - Fix the reactive-streams

[CAMEL-19465](https://issues.apache.org/jira/browse/CAMEL-19465)

Move Apache snapshots repository to a separate Maven profile for better build reproducibility

[CAMEL-19446](https://issues.apache.org/jira/browse/CAMEL-19446)

camel-caffeine: investigate potential test cleanups

[CAMEL-19445](https://issues.apache.org/jira/browse/CAMEL-19445)

camel-caffeine: cleanup assertions

[CAMEL-19444](https://issues.apache.org/jira/browse/CAMEL-19444)

camel-kafka: fix grammar errors on the documentation

[CAMEL-19438](https://issues.apache.org/jira/browse/CAMEL-19438)

camel-sftp: tests cause entry pollution on user's known hosts file

[CAMEL-19355](https://issues.apache.org/jira/browse/CAMEL-19355)

maven wrapper - Upgrade to 3.9.2

[CAMEL-18876](https://issues.apache.org/jira/browse/CAMEL-18876)

ErrorHandlerDefinition properties missing in camel-catalog

[CAMEL-18540](https://issues.apache.org/jira/browse/CAMEL-18540)

camel-atom: component depends on deprecated artifacts

[CAMEL-17328](https://issues.apache.org/jira/browse/CAMEL-17328)

Avoid 3rd party maven repository - jboss

### Test (2)

[CAMEL-19609](https://issues.apache.org/jira/browse/CAMEL-19609)

camel-test-infra-hdfs: infra is not container-based

[CAMEL-19604](https://issues.apache.org/jira/browse/CAMEL-19604)

camel-knative: component is likely broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).