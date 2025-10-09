# Apache camel 3.7.1 Release

## New and Noteworthy

This release is the new Camel 3.7.1 LTS release.

## Supported Java version

This version supports Java 8 and 11.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.7.1</version>
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
      <version>3.7.1</version>
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
| [apache-camel-3.7.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.1/apache-camel-3.7.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.1/apache-camel-3.7.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.1/apache-camel-3.7.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (22)

[CAMEL-16045](https://issues.apache.org/jira/browse/CAMEL-16045)

rest-dsl - xml or json binding should create new instance of data formats

[CAMEL-16043](https://issues.apache.org/jira/browse/CAMEL-16043)

\[camel-kafka\] additionalProperties option on endpoint level is broken

[CAMEL-16040](https://issues.apache.org/jira/browse/CAMEL-16040)

JAXB error Generating Swagger in Karaf

[CAMEL-16032](https://issues.apache.org/jira/browse/CAMEL-16032)

\[camel-main\] autoconfiguration does not bind dataformat in the registry

[CAMEL-16014](https://issues.apache.org/jira/browse/CAMEL-16014)

camel-test-infra-artemis: Invalid AMQP endpoint

[CAMEL-16009](https://issues.apache.org/jira/browse/CAMEL-16009)

OPC/UA Tree contains two nodes "Camel" that is incorrect

[CAMEL-16005](https://issues.apache.org/jira/browse/CAMEL-16005)

Route built from template with parallel processing recipient list fails to start because of duplicate node id.

[CAMEL-16000](https://issues.apache.org/jira/browse/CAMEL-16000)

Type converter regression in Camel 3.7.0

[CAMEL-15999](https://issues.apache.org/jira/browse/CAMEL-15999)

Camel-spring-boot: Property not found after upgrading to 3.7.0 when using camel-caffeine-starter

[CAMEL-15983](https://issues.apache.org/jira/browse/CAMEL-15983)

URISupport have an bug in method doFastNormalizeUri for normalize EndpointKey

[CAMEL-15974](https://issues.apache.org/jira/browse/CAMEL-15974)

HttpSendDynamicAware doesn't resolve RAW properties

[CAMEL-15971](https://issues.apache.org/jira/browse/CAMEL-15971)

SimpleFileLanguage always null due to DummyExchange

[CAMEL-15949](https://issues.apache.org/jira/browse/CAMEL-15949)

Incorrect value getSupportExtendedInformation for ManagedPollEnricher

[CAMEL-15947](https://issues.apache.org/jira/browse/CAMEL-15947)

Hazelcast : client mode : search hazelcast client by name doesn't work

[CAMEL-15945](https://issues.apache.org/jira/browse/CAMEL-15945)

Don't require sObjectName or sObjectClass when streaming with raw payload

[CAMEL-15942](https://issues.apache.org/jira/browse/CAMEL-15942)

spring xml on camel-spring-boot may add route policy factory twice

[CAMEL-15937](https://issues.apache.org/jira/browse/CAMEL-15937)

camel-netty - WARN logging with disconnect=true

[CAMEL-15930](https://issues.apache.org/jira/browse/CAMEL-15930)

ClusteredRouteController cannot start clustered routes

[CAMEL-15928](https://issues.apache.org/jira/browse/CAMEL-15928)

TimeoutException does not trigger Resilience4j circuit breaker

[CAMEL-15290](https://issues.apache.org/jira/browse/CAMEL-15290)

camel-cxfrs - CxfRsProducer leaks Header when Exchange.HTTP\_METHOD is set

[CAMEL-13553](https://issues.apache.org/jira/browse/CAMEL-13553)

OnCompletion behaves strange in combination with direct subroutes

[CAMEL-12871](https://issues.apache.org/jira/browse/CAMEL-12871)

Camel-salesforce component drops the streaming topic

### Improvement (2)

[CAMEL-16042](https://issues.apache.org/jira/browse/CAMEL-16042)

Upgrade to Spring Boot 2.4.2

[CAMEL-15938](https://issues.apache.org/jira/browse/CAMEL-15938)

Catalog contains wrong "required" for aws2-iam "operation"

### New Feature (1)

[CAMEL-15428](https://issues.apache.org/jira/browse/CAMEL-15428)

Create a proper camel BOM (for camel-spring-boot)

### Task (4)

[CAMEL-16047](https://issues.apache.org/jira/browse/CAMEL-16047)

Error building camel 3.7.0 with jdk11

[CAMEL-16033](https://issues.apache.org/jira/browse/CAMEL-16033)

camel-core-languages should move out of generated list components in parent/pom.xml

[CAMEL-16027](https://issues.apache.org/jira/browse/CAMEL-16027)

camel-xml-jaxp should be put above the marker of camel components: START in parent/pom.xml

[CAMEL-15946](https://issues.apache.org/jira/browse/CAMEL-15946)

camel-endpointdsl - Generate valid javadoc

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).