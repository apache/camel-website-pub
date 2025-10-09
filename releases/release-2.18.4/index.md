# Apache camel 2.18.4 Release

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
      <version>2.18.4</version>
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
      <version>2.18.4</version>
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
| [apache-camel-2.18.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.18.4/apache-camel-2.18.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.18.4/apache-camel-2.18.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.18.4/apache-camel-2.18.4-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.18.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.18.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (34)

[CAMEL-11287](https://issues.apache.org/jira/browse/CAMEL-11287)

MDC routeId value is lost after calling a direct route from a transacted route

[CAMEL-11281](https://issues.apache.org/jira/browse/CAMEL-11281)

camel-spring is not usable in an osgi-context

[CAMEL-11279](https://issues.apache.org/jira/browse/CAMEL-11279)

Camel hystrix does not handle exceptions properly

[CAMEL-11269](https://issues.apache.org/jira/browse/CAMEL-11269)

URISupport sanitizeUri partial support for RAW()

[CAMEL-11264](https://issues.apache.org/jira/browse/CAMEL-11264)

Potential NPE in DefaultUndertowHttpBinding

[CAMEL-11255](https://issues.apache.org/jira/browse/CAMEL-11255)

Error handler may be called twice if routing from onException to direct with global scoped error handler

[CAMEL-11234](https://issues.apache.org/jira/browse/CAMEL-11234)

NullPointerException while trying to get the Route Status on startup

[CAMEL-11229](https://issues.apache.org/jira/browse/CAMEL-11229)

Infinite recursion if exception happens inside exception handler

[CAMEL-11227](https://issues.apache.org/jira/browse/CAMEL-11227)

Simple expression colon in sql-stored component

[CAMEL-11225](https://issues.apache.org/jira/browse/CAMEL-11225)

Deadlock in component creation

[CAMEL-11221](https://issues.apache.org/jira/browse/CAMEL-11221)

camel-netty4-http cannot have a URL larger than 409 bytes by default, rather than the assumed 4096 byte limit

[CAMEL-11197](https://issues.apache.org/jira/browse/CAMEL-11197)

camel-jpa consumer fails to poll after database connection is lost

[CAMEL-11139](https://issues.apache.org/jira/browse/CAMEL-11139)

ClassNotFoundException may silently be ignored in InProducer

[CAMEL-11138](https://issues.apache.org/jira/browse/CAMEL-11138)

ConsumerTemplate - If cache is full then polling consumer should be stopped to not leak resources

[CAMEL-11131](https://issues.apache.org/jira/browse/CAMEL-11131)

Timer consumer - Should call start/stop of the processor

[CAMEL-11117](https://issues.apache.org/jira/browse/CAMEL-11117)

The searchTerm subjectOrBody breaks the searchTerm unseen

[CAMEL-11106](https://issues.apache.org/jira/browse/CAMEL-11106)

camel-sql - allow using the $simple{} syntax for query arguments

[CAMEL-11074](https://issues.apache.org/jira/browse/CAMEL-11074)

Unable to load Schematron XSLT templates on windows

[CAMEL-11065](https://issues.apache.org/jira/browse/CAMEL-11065)

Cannot parse CSV record starting with separator character

[CAMEL-11063](https://issues.apache.org/jira/browse/CAMEL-11063)

PGP Decryptor does not make Integrity check

[CAMEL-11048](https://issues.apache.org/jira/browse/CAMEL-11048)

Jetty Producer always uses "Transfer-Encoding: chunked" header

[CAMEL-11047](https://issues.apache.org/jira/browse/CAMEL-11047)

STARTTLS broken with camel-mail

[CAMEL-11031](https://issues.apache.org/jira/browse/CAMEL-11031)

Use default ("") exchange for reply-to messages

[CAMEL-11028](https://issues.apache.org/jira/browse/CAMEL-11028)

camel-spark-rest - Adds duplicate content-type

[CAMEL-11020](https://issues.apache.org/jira/browse/CAMEL-11020)

Camel Kubernetes consumers do not close watchers

[CAMEL-11012](https://issues.apache.org/jira/browse/CAMEL-11012)

bindy csv doesn't populate with defaultValue on marshal

[CAMEL-11009](https://issues.apache.org/jira/browse/CAMEL-11009)

Camel spring - spring.schemas file contains unexpaned maven properties in release artefact

[CAMEL-11008](https://issues.apache.org/jira/browse/CAMEL-11008)

Consumer/Producer templates are not stopped when auto-configured in Spring Boot

[CAMEL-11002](https://issues.apache.org/jira/browse/CAMEL-11002)

Camel-Blueprint - failed container fails to remove JMX object

[CAMEL-11000](https://issues.apache.org/jira/browse/CAMEL-11000)

Property 'accessExternalDTD' is not recognized by (all) Xerces

[CAMEL-10961](https://issues.apache.org/jira/browse/CAMEL-10961)

ZookeeperRoutingPolicy - Error setting up election node

[CAMEL-10949](https://issues.apache.org/jira/browse/CAMEL-10949)

Websocket clients get message from all resources on one port

[CAMEL-10948](https://issues.apache.org/jira/browse/CAMEL-10948)

Camel-hdfs2: initialDelay option is overwritten with default value

[CAMEL-10820](https://issues.apache.org/jira/browse/CAMEL-10820)

DefaultFluentProducerTemplate mixes up data when sending asynchronously

### Improvement (6)

[CAMEL-11263](https://issues.apache.org/jira/browse/CAMEL-11263)

set HeaderFilterStrategy before setting properties

[CAMEL-11206](https://issues.apache.org/jira/browse/CAMEL-11206)

camel-twitter - The default delay is not used

[CAMEL-11182](https://issues.apache.org/jira/browse/CAMEL-11182)

SolrParams are not honored when sending SolrInputDocument.

[CAMEL-11141](https://issues.apache.org/jira/browse/CAMEL-11141)

Add support for VPC instances

[CAMEL-10983](https://issues.apache.org/jira/browse/CAMEL-10983)

Fail early and show meaningful log for invalid endpoint URI in Blueprint

[CAMEL-7809](https://issues.apache.org/jira/browse/CAMEL-7809)

Quartz PollConsumerScheduler in a cluster tries to create duplicate triggers, fails

### Sub-task (1)

[CAMEL-7933](https://issues.apache.org/jira/browse/CAMEL-7933)

Camel-apns should create https connections using SSLContextParameters

### Task (2)

[CAMEL-11101](https://issues.apache.org/jira/browse/CAMEL-11101)

Update CXF dependency to latest version > 3.1.10

[CAMEL-11064](https://issues.apache.org/jira/browse/CAMEL-11064)

Add activemq-amqp to parent POM

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).