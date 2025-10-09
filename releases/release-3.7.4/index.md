# Apache camel 3.7.4 Release

## New and Noteworthy

This release is the new Camel 3.7.4 LTS release.

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
      <version>3.7.4</version>
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
      <version>3.7.4</version>
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
| [apache-camel-3.7.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.7.4/apache-camel-3.7.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.7.4/apache-camel-3.7.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.7.4/apache-camel-3.7.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.7.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.7.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-16550](https://issues.apache.org/jira/browse/CAMEL-16550)

camel-core - Split and Aggregate with Transacted may cause thread to stuck

[CAMEL-16530](https://issues.apache.org/jira/browse/CAMEL-16530)

AWS2-S3 component does not recognize or use proxy-host and proxy-port from application.properties

[CAMEL-16480](https://issues.apache.org/jira/browse/CAMEL-16480)

Simple expression behavior change after 3.4->3.7 migration

[CAMEL-16453](https://issues.apache.org/jira/browse/CAMEL-16453)

camel-zipkin - Incorrect spans created when using parallelProcessing with recipientList or multicast

[CAMEL-16423](https://issues.apache.org/jira/browse/CAMEL-16423)

Camel-Minio converts any body consumed to String

[CAMEL-16418](https://issues.apache.org/jira/browse/CAMEL-16418)

LEAK: ByteBuf.release() results when using circuit breaker with netty http producer

[CAMEL-16412](https://issues.apache.org/jira/browse/CAMEL-16412)

camel-core - Environment Variables in Properties Source location no longer works

[CAMEL-16393](https://issues.apache.org/jira/browse/CAMEL-16393)

camel-jsonpath - results from $.concat(...) seems to be cached on following calls

[CAMEL-16377](https://issues.apache.org/jira/browse/CAMEL-16377)

camel-core - Recipient List EIP - Failed to create Producer for endpoint - NPE in ServicePool

[CAMEL-16318](https://issues.apache.org/jira/browse/CAMEL-16318)

camel-kafka - LoginCallbackHandler causes ClassNotFoudException on OSGi

[CAMEL-16317](https://issues.apache.org/jira/browse/CAMEL-16317)

NPE on SFTP component query parameter for options that are duration

[CAMEL-16309](https://issues.apache.org/jira/browse/CAMEL-16309)

The Rest Openapi schema generator has a typo; "sting" instead of "string"

[CAMEL-16295](https://issues.apache.org/jira/browse/CAMEL-16295)

split with AggregationStrategy is ignored when using transacted

[CAMEL-16173](https://issues.apache.org/jira/browse/CAMEL-16173)

Camel Resilience4j Bulkhead seems to not limit concurrent requests

### Dependency upgrade (1)

[CAMEL-16376](https://issues.apache.org/jira/browse/CAMEL-16376)

camel-spring-boot - Upgrade to Spring Boot 2.4.4

### Improvement (3)

[CAMEL-16552](https://issues.apache.org/jira/browse/CAMEL-16552)

camel-spring-boot - Configuring route templates trouble setting route id when using spring yaml configuration

[CAMEL-16470](https://issues.apache.org/jira/browse/CAMEL-16470)

Problem when using multiple EntityManagerFactories for different datasources in the same route

[CAMEL-16315](https://issues.apache.org/jira/browse/CAMEL-16315)

Camel-Netty: Support Hostname verification even though we are on Netty 4.1.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).