# Apache camel 3.11.1 Release

## New and Noteworthy

This release is the new Camel 3.11.1 LTS patch release.

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
      <version>3.11.1</version>
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
      <version>3.11.1</version>
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
| [apache-camel-3.11.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.1/apache-camel-3.11.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.1/apache-camel-3.11.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.1/apache-camel-3.11.1-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (21)

[CAMEL-16821](https://issues.apache.org/jira/browse/CAMEL-16821)

camel-bean - BeanProcessor with Process bean does not handle Throwable

[CAMEL-16820](https://issues.apache.org/jira/browse/CAMEL-16820)

camel-core - CircuitBreaker - java.lang.UnsupportedOperationException: Is this really correct

[CAMEL-16818](https://issues.apache.org/jira/browse/CAMEL-16818)

camel-core - route dump dose not print correct route with kamelet eip

[CAMEL-16815](https://issues.apache.org/jira/browse/CAMEL-16815)

OpenTracing with Avro keys causes warning

[CAMEL-16811](https://issues.apache.org/jira/browse/CAMEL-16811)

Cannot consume messages from sjms2 endpoint with deliveryMode set

[CAMEL-16807](https://issues.apache.org/jira/browse/CAMEL-16807)

camel-kafka - problem using two kafka connections in the same application

[CAMEL-16806](https://issues.apache.org/jira/browse/CAMEL-16806)

AWS2 S3 Documentation contains references to obsolete AWS 1 API

[CAMEL-16804](https://issues.apache.org/jira/browse/CAMEL-16804)

NullPointerException when using try-with-resources and MainConfigurationProperties

[CAMEL-16802](https://issues.apache.org/jira/browse/CAMEL-16802)

camel-core - Split / Aggregate with parallelprocessing aggregates in random order

[CAMEL-16796](https://issues.apache.org/jira/browse/CAMEL-16796)

camel-cxf - Problem with inflight message count being -1

[CAMEL-16795](https://issues.apache.org/jira/browse/CAMEL-16795)

camel-file - read-lock fails for minimum length files

[CAMEL-16794](https://issues.apache.org/jira/browse/CAMEL-16794)

camel-core - race condition in LoopProcessor

[CAMEL-16782](https://issues.apache.org/jira/browse/CAMEL-16782)

Getting FailedToCreateProducerException with reason java.util.ConcurrentModificationException randomly when using huge split

[CAMEL-16776](https://issues.apache.org/jira/browse/CAMEL-16776)

camel-test - Dependency injected Endpoint via @EndpointInject should have components autowired eager

[CAMEL-16772](https://issues.apache.org/jira/browse/CAMEL-16772)

camel-sjms - Messages not filing to amq if using onCompletion() and transacted=true.

[CAMEL-16767](https://issues.apache.org/jira/browse/CAMEL-16767)

camel-core - Stoping route failed with NPE when route contains loopDoWhile

[CAMEL-16764](https://issues.apache.org/jira/browse/CAMEL-16764)

Box component does not reuse BoxAPIConnection when configured at the component level

[CAMEL-16763](https://issues.apache.org/jira/browse/CAMEL-16763)

camel-sjms - Null JMS Correlation ID using Camel-SJMS Request/Reply with Artemis JMS Client

[CAMEL-16762](https://issues.apache.org/jira/browse/CAMEL-16762)

camel-jms - Only the first payload chunk will be read when using jmsMessageType=Stream

[CAMEL-16704](https://issues.apache.org/jira/browse/CAMEL-16704)

camel-ahc - Requests getting timed out because the threads assigned to channels are busy

[CAMEL-16692](https://issues.apache.org/jira/browse/CAMEL-16692)

SFTP sometimes doesn't receive all files

### Dependency upgrade (3)

[CAMEL-16827](https://issues.apache.org/jira/browse/CAMEL-16827)

camel 3.11.x - Upgrade spring boot to 2.5.3

[CAMEL-16778](https://issues.apache.org/jira/browse/CAMEL-16778)

upgrade to vertx 4.1.1

[CAMEL-16771](https://issues.apache.org/jira/browse/CAMEL-16771)

camel-spring-boot - Upgrade to 2.5.2

### Improvement (5)

[CAMEL-16824](https://issues.apache.org/jira/browse/CAMEL-16824)

camel-jpa - Do not lose headers

[CAMEL-16792](https://issues.apache.org/jira/browse/CAMEL-16792)

camel-core - OGNL \`properties\` variable should use \`allProperties\`

[CAMEL-16759](https://issues.apache.org/jira/browse/CAMEL-16759)

camel-core - Kamelet add support for factory method in #class local bean

[CAMEL-16756](https://issues.apache.org/jira/browse/CAMEL-16756)

Improve handling of Vert.x Buffer payloads in platform-http-vertx

[CAMEL-16750](https://issues.apache.org/jira/browse/CAMEL-16750)

Do not propagate exception when concurrent FILE component consumers try to acquire lock in JdbcMessageIdRepository

### Task (3)

[CAMEL-16817](https://issues.apache.org/jira/browse/CAMEL-16817)

camel-karaf - Error building with maven 3.8.1

[CAMEL-16803](https://issues.apache.org/jira/browse/CAMEL-16803)

remove unnecessary dependency from JDK9+ profile

[CAMEL-16752](https://issues.apache.org/jira/browse/CAMEL-16752)

camel-spring feature should install camel-spring-xml bundle

### Test (1)

[CAMEL-16814](https://issues.apache.org/jira/browse/CAMEL-16814)

camel-jms - a testcase to demonstrate that Messages filing to amq if using onCompletion() and transacted=true.

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).