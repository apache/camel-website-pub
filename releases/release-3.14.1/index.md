# Apache camel 3.14.1 Release

## New and Noteworthy

This release is the new Camel 3.14.1 LTS patch release.

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
      <version>3.14.1</version>
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
      <version>3.14.1</version>
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
| [apache-camel-3.14.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.14.1/apache-camel-3.14.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.14.1/apache-camel-3.14.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.14.1/apache-camel-3.14.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.14.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.14.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (34)

[CAMEL-17536](https://issues.apache.org/jira/browse/CAMEL-17536)

ServicePool.doStop hangs during shutdown

[CAMEL-17524](https://issues.apache.org/jira/browse/CAMEL-17524)

Camel loading of resources using ClassResolver API doesn't work in OSGi enviroments

[CAMEL-17521](https://issues.apache.org/jira/browse/CAMEL-17521)

camel-http - httpClient parameters are not filtered out

[CAMEL-17520](https://issues.apache.org/jira/browse/CAMEL-17520)

Cannot use square brackets in HTTP parameters

[CAMEL-17514](https://issues.apache.org/jira/browse/CAMEL-17514)

BreadcrumbId MDC Value not set even MDCLogging is true during ErrorHandling Processor

[CAMEL-17511](https://issues.apache.org/jira/browse/CAMEL-17511)

Spring boot actuator endpoint parameters issues

[CAMEL-17506](https://issues.apache.org/jira/browse/CAMEL-17506)

olingo4 should always look for a single entity when a predicate key is used

[CAMEL-17504](https://issues.apache.org/jira/browse/CAMEL-17504)

BridgeExceptionHandlerToErrorHandler broken with DefaultErrorHandler

[CAMEL-17503](https://issues.apache.org/jira/browse/CAMEL-17503)

camel-ahc-ws - Unable to reconnect to Server after server reboot

[CAMEL-17501](https://issues.apache.org/jira/browse/CAMEL-17501)

camel-core - FailedToCreateRouteException issue if route is very long and complex uris that cannot be sanitized

[CAMEL-17493](https://issues.apache.org/jira/browse/CAMEL-17493)

camel-kafka: safe unsubscription should ignore safe exceptions

[CAMEL-17492](https://issues.apache.org/jira/browse/CAMEL-17492)

CamelBeanPostProcessor fails if @Producer is used in EventNotifier

[CAMEL-17489](https://issues.apache.org/jira/browse/CAMEL-17489)

camel-kafka - Unsubscribing fails due to already closed consumer

[CAMEL-17486](https://issues.apache.org/jira/browse/CAMEL-17486)

camel-core - ThrottlePermit compareTo cast to int causes issues

[CAMEL-17485](https://issues.apache.org/jira/browse/CAMEL-17485)

Camel-JSLT: Currently it could only load resources from classpath

[CAMEL-17477](https://issues.apache.org/jira/browse/CAMEL-17477)

camel-smpp: reconnection logic is not respecting the reconnectDelay

[CAMEL-17473](https://issues.apache.org/jira/browse/CAMEL-17473)

camel-github: startingSha=last doesn't work properly

[CAMEL-17472](https://issues.apache.org/jira/browse/CAMEL-17472)

camel-smpp: Consumer reconnect no longer works after updating to 3.14.0

[CAMEL-17471](https://issues.apache.org/jira/browse/CAMEL-17471)

Snakeyaml: Use safe constructor where the default one has been used

[CAMEL-17457](https://issues.apache.org/jira/browse/CAMEL-17457)

camel-openapi-java - Incorrect tags in openapi

[CAMEL-17454](https://issues.apache.org/jira/browse/CAMEL-17454)

camel-undertow - Adds duplicate content-type

[CAMEL-17452](https://issues.apache.org/jira/browse/CAMEL-17452)

camel-util - URISupport#sanitizeUri sanitizes passwords incorrectly if remaining uri contains expression ${<expr>}

[CAMEL-17441](https://issues.apache.org/jira/browse/CAMEL-17441)

camel-health - Loading custom health-check from classpath scanning is not added to registry

[CAMEL-17437](https://issues.apache.org/jira/browse/CAMEL-17437)

Camel-aws2-sqs: Deadletter fails with sqs client from registry (could impact more components)

[CAMEL-17436](https://issues.apache.org/jira/browse/CAMEL-17436)

camel-spring-boot - Disabling health check for single route or consumer is not possible

[CAMEL-17430](https://issues.apache.org/jira/browse/CAMEL-17430)

Rest endpoint query parameters not set on underlying endpoint

[CAMEL-17425](https://issues.apache.org/jira/browse/CAMEL-17425)

camel-quartz - OSGi compatibility is broken for loading resources from classloader

[CAMEL-17390](https://issues.apache.org/jira/browse/CAMEL-17390)

camel-core - Cannot set tracer on a started CamelContext

[CAMEL-17372](https://issues.apache.org/jira/browse/CAMEL-17372)

Camel-Azure-Servicebus is missing in Camel catalog

[CAMEL-17367](https://issues.apache.org/jira/browse/CAMEL-17367)

Kafka endpoint DSL for producer doesn't strip //

[CAMEL-17358](https://issues.apache.org/jira/browse/CAMEL-17358)

AWS SDK2 Producer does not set the Content Type at all

[CAMEL-17336](https://issues.apache.org/jira/browse/CAMEL-17336)

camel-jackson: Can't operate in \`List\` mode and use a custom ObjectMapper

[CAMEL-17137](https://issues.apache.org/jira/browse/CAMEL-17137)

camel-karaf - Error while adding camel-cxf

[CAMEL-17118](https://issues.apache.org/jira/browse/CAMEL-17118)

mapHttpMessageFormUrlEncodedBody does not work - it will always map the POST parameters to headers

### Dependency upgrade (6)

[CAMEL-17529](https://issues.apache.org/jira/browse/CAMEL-17529)

camel-spring-boot - Upgrade to 2.6.3

[CAMEL-17395](https://issues.apache.org/jira/browse/CAMEL-17395)

upgrade to log4j 2.17.1

[CAMEL-17360](https://issues.apache.org/jira/browse/CAMEL-17360)

upgrade to bouncycastle 1.70

[CAMEL-17353](https://issues.apache.org/jira/browse/CAMEL-17353)

Upgrade to log4j 2.17.0

[CAMEL-17335](https://issues.apache.org/jira/browse/CAMEL-17335)

upgrade to logback 1.2.8

[CAMEL-17327](https://issues.apache.org/jira/browse/CAMEL-17327)

Upgrade to log4j 2.16.0

### Improvement (4)

[CAMEL-17519](https://issues.apache.org/jira/browse/CAMEL-17519)

Make Camel MainSupport internalBeforeStart method protected

[CAMEL-17509](https://issues.apache.org/jira/browse/CAMEL-17509)

camel-kafka: invalid topic info displayed when using topic patterns

[CAMEL-17479](https://issues.apache.org/jira/browse/CAMEL-17479)

camel-core - Configuring properties with optional syntax in value on beans also

[CAMEL-17389](https://issues.apache.org/jira/browse/CAMEL-17389)

toD (Dynamic To URI) doesn't work with Windows paths with file component

### Task (3)

[CAMEL-17679](https://issues.apache.org/jira/browse/CAMEL-17679)

camel-micrometer: gauge is reported as invalid

[CAMEL-17464](https://issues.apache.org/jira/browse/CAMEL-17464)

Avoid duplication of API Mapping link for ServiceNow

[CAMEL-17463](https://issues.apache.org/jira/browse/CAMEL-17463)

Little issues in twitter attributes description

### Test (1)

[CAMEL-17453](https://issues.apache.org/jira/browse/CAMEL-17453)

MTOM/XOP tests in camel-cxf are broken

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).