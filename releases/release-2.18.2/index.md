# Apache camel 2.18.2 Release

## New and Noteworthy

This release is a minor update of the 2.18.x branch.

## Supported Java version

This version supports Java 8.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>2.18.2</version>
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
      <version>2.18.2</version>
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
| [apache-camel-2.18.2-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.2/apache-camel-2.18.2-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.2/apache-camel-2.18.2-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.2/apache-camel-2.18.2-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (40)

[CAMEL-10771](https://issues.apache.org/jira/browse/CAMEL-10771)

CxfEndpoint shows WARNING altough endpoint-/port name is configured

[CAMEL-10732](https://issues.apache.org/jira/browse/CAMEL-10732)

Remove from all caches when Groovy script is removed from Camel script cache

[CAMEL-10727](https://issues.apache.org/jira/browse/CAMEL-10727)

camel-ftp: knownHostsUri configuration with camel 2.18.1

[CAMEL-10713](https://issues.apache.org/jira/browse/CAMEL-10713)

SCP not handling errors for failed transfers correctly

[CAMEL-10712](https://issues.apache.org/jira/browse/CAMEL-10712)

Camel-SFTP endpoints will silently not delete file on disconnect

[CAMEL-10709](https://issues.apache.org/jira/browse/CAMEL-10709)

camel-etcd: etcd stats endpoint fails because of a class cast exception

[CAMEL-10708](https://issues.apache.org/jira/browse/CAMEL-10708)

org.apache.camel.component.cxf.CxfEndpoint -- Lines 554 -558 should be Nullsafe

[CAMEL-10704](https://issues.apache.org/jira/browse/CAMEL-10704)

XSLT will fail if the XML document contains a default namespace

[CAMEL-10701](https://issues.apache.org/jira/browse/CAMEL-10701)

Classloader issue prevents from loading kafka authentication in OSGi environments

[CAMEL-10695](https://issues.apache.org/jira/browse/CAMEL-10695)

camel-mqtt: TimeoutException thrown on MQTTEndpoint stop

[CAMEL-10692](https://issues.apache.org/jira/browse/CAMEL-10692)

OptaPlanner cannot load config from deployment

[CAMEL-10689](https://issues.apache.org/jira/browse/CAMEL-10689)

NoFactoryAvailableException when invoking component-list ssh command

[CAMEL-10677](https://issues.apache.org/jira/browse/CAMEL-10677)

SJMSBatchConsumer does not respect the consumerCount parameter

[CAMEL-10675](https://issues.apache.org/jira/browse/CAMEL-10675)

Swagger is not generating schema ref for body parameter

[CAMEL-10664](https://issues.apache.org/jira/browse/CAMEL-10664)

SimpleIllegalSyntaxException in nested expression

[CAMEL-10663](https://issues.apache.org/jira/browse/CAMEL-10663)

Basic authentication information not sent on versions post 2.14.1

[CAMEL-10653](https://issues.apache.org/jira/browse/CAMEL-10653)

XQuery support broken in Camel 2.18.x

[CAMEL-10644](https://issues.apache.org/jira/browse/CAMEL-10644)

Camel-MongoDB: component should not store state

[CAMEL-10640](https://issues.apache.org/jira/browse/CAMEL-10640)

Custom AsyncHttpClientConfig not used in WsEndpoint

[CAMEL-10635](https://issues.apache.org/jira/browse/CAMEL-10635)

camel-mongodb-gridfs - The component should not store state

[CAMEL-10634](https://issues.apache.org/jira/browse/CAMEL-10634)

Camel Catalog contains some invalid entries for Spring-boot in 2.18.x

[CAMEL-10628](https://issues.apache.org/jira/browse/CAMEL-10628)

camel jetty9 endpoint configured with sslContextParametersRef and jetty handlers causes SSL handshake failure

[CAMEL-10616](https://issues.apache.org/jira/browse/CAMEL-10616)

shutdown timeout override not working in unit tests

[CAMEL-10603](https://issues.apache.org/jira/browse/CAMEL-10603)

Realm parameter cause Exception

[CAMEL-10602](https://issues.apache.org/jira/browse/CAMEL-10602)

camel:run with simple blueprint project failed "waiting for BlueprintContainer" although the route is active

[CAMEL-10597](https://issues.apache.org/jira/browse/CAMEL-10597)

Swagger prints child object types as string parameters rather than refs

[CAMEL-10594](https://issues.apache.org/jira/browse/CAMEL-10594)

Kafka consumer stays alive when camel context is shut down

[CAMEL-10582](https://issues.apache.org/jira/browse/CAMEL-10582)

Spring Message headers are immutable

[CAMEL-10581](https://issues.apache.org/jira/browse/CAMEL-10581)

toD (ToDynamicDefinition) does not honor RAW( ) contract - 'removes + from password'

[CAMEL-10579](https://issues.apache.org/jira/browse/CAMEL-10579)

SOAP 1.1 unmarshalling fails for faults that lack a detail element

[CAMEL-10578](https://issues.apache.org/jira/browse/CAMEL-10578)

Default namespaces defined on SOAPEnvelope cause problems with CXF PAYLOAD mode

[CAMEL-10573](https://issues.apache.org/jira/browse/CAMEL-10573)

Align FallbackTypeConverter loading in OSGI environments

[CAMEL-10568](https://issues.apache.org/jira/browse/CAMEL-10568)

SftpChangedExclusiveReadLockStrategy integer overflow

[CAMEL-10562](https://issues.apache.org/jira/browse/CAMEL-10562)

UnsupportedOperationException in DefaultCamelContext#safelyStartRouteServices

[CAMEL-10557](https://issues.apache.org/jira/browse/CAMEL-10557)

Salesforce bulk API getBatchRequest uses wrong URL pattern

[CAMEL-10548](https://issues.apache.org/jira/browse/CAMEL-10548)

Converter from List to String is not found when @EnableAutoConfiguration is used

[CAMEL-10539](https://issues.apache.org/jira/browse/CAMEL-10539)

When bridging http endpoints and end users do not enable the bridgeEndpoint option they may get a NPE exception

[CAMEL-10511](https://issues.apache.org/jira/browse/CAMEL-10511)

MllpTcpClientProducer should read all available bytes in TCP buffer for acknowledgment

[CAMEL-10490](https://issues.apache.org/jira/browse/CAMEL-10490)

JpaPollingConsumer does not support consumeLockEntity and others

[CAMEL-10461](https://issues.apache.org/jira/browse/CAMEL-10461)

camel-cmis - Parameters not taking in account

### Improvement (22)

[CAMEL-10729](https://issues.apache.org/jira/browse/CAMEL-10729)

Camel-AWS: S3 autocloseBody option

[CAMEL-10700](https://issues.apache.org/jira/browse/CAMEL-10700)

camel-maven - validate simple predicates and property placeholders

[CAMEL-10699](https://issues.apache.org/jira/browse/CAMEL-10699)

Simple - Add short error message

[CAMEL-10697](https://issues.apache.org/jira/browse/CAMEL-10697)

Infinite loop sometimes happen at the shutdown of the Kafka consumer

[CAMEL-10684](https://issues.apache.org/jira/browse/CAMEL-10684)

camel-catalog - Simple validator should provide location index of the error

[CAMEL-10680](https://issues.apache.org/jira/browse/CAMEL-10680)

Camel catalog - validate endpoint properties - consumer vs producer

[CAMEL-10679](https://issues.apache.org/jira/browse/CAMEL-10679)

Producer does not populate attachments from response

[CAMEL-10667](https://issues.apache.org/jira/browse/CAMEL-10667)

Add tarFile data format to Java DSL

[CAMEL-10662](https://issues.apache.org/jira/browse/CAMEL-10662)

camel-hystrix - If hystrix timeout occurs then the hystrix timeout exception should be cause

[CAMEL-10661](https://issues.apache.org/jira/browse/CAMEL-10661)

camel-hystrix - Fallback should route exchange if it was marked as stop due delay timeout

[CAMEL-10619](https://issues.apache.org/jira/browse/CAMEL-10619)

Add spring boot configuration for configuring shutdown options

[CAMEL-10606](https://issues.apache.org/jira/browse/CAMEL-10606)

Modify quartz2 endpoint to be a singleton

[CAMEL-10604](https://issues.apache.org/jira/browse/CAMEL-10604)

Camel-JacksonXML: Add an option to allow the UnmarshallType header use

[CAMEL-10592](https://issues.apache.org/jira/browse/CAMEL-10592)

Improve naming and description for sip components

[CAMEL-10589](https://issues.apache.org/jira/browse/CAMEL-10589)

ServiceNow: add an option to convigure SSL/TLS

[CAMEL-10577](https://issues.apache.org/jira/browse/CAMEL-10577)

Jetty9 producer only supports payloads up hardcoded limit (2MB)

[CAMEL-10575](https://issues.apache.org/jira/browse/CAMEL-10575)

snakeyaml: add an option to filter classes the yaml parser can construct

[CAMEL-10567](https://issues.apache.org/jira/browse/CAMEL-10567)

Camel-Jackson: Add an option to allow the UnmarshallType header use

[CAMEL-10552](https://issues.apache.org/jira/browse/CAMEL-10552)

spring-boot: make component lazy loading

[CAMEL-10551](https://issues.apache.org/jira/browse/CAMEL-10551)

spring-boot: make auto configured dataformats and languages prototype

[CAMEL-10550](https://issues.apache.org/jira/browse/CAMEL-10550)

spring-boot: add a global option to disable data-format, language and components auto configuration

[CAMEL-10509](https://issues.apache.org/jira/browse/CAMEL-10509)

ManagedCamelContextMBean - additional namespaces are removed

### New Feature (1)

[CAMEL-10588](https://issues.apache.org/jira/browse/CAMEL-10588)

Add HTTP proxy config params to camel-servicenow

### Task (6)

[CAMEL-10723](https://issues.apache.org/jira/browse/CAMEL-10723)

Errors in documentation for camel-kinesis

[CAMEL-10673](https://issues.apache.org/jira/browse/CAMEL-10673)

Expose activemq-mqtt through parent POM

[CAMEL-10647](https://issues.apache.org/jira/browse/CAMEL-10647)

camel-test-karaf - Cause wrong build order

[CAMEL-10637](https://issues.apache.org/jira/browse/CAMEL-10637)

IllegalStateException that is not thrown in IgniteMessagingEndpoint

[CAMEL-10623](https://issues.apache.org/jira/browse/CAMEL-10623)

Camel CXF version not compatible with WildFly CXF

[CAMEL-10605](https://issues.apache.org/jira/browse/CAMEL-10605)

add camel-tar doc as wiki

### Wish (1)

[CAMEL-11622](https://issues.apache.org/jira/browse/CAMEL-11622)

Rest-dsl doesn't support post() endpoints with different request body types

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).