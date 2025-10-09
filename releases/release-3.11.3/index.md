# Apache camel 3.11.3 Release

## New and Noteworthy

This release is the new Camel 3.11.3 LTS patch release.

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
      <version>3.11.3</version>
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
      <version>3.11.3</version>
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
| [apache-camel-3.11.3-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.11.3/apache-camel-3.11.3-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.11.3/apache-camel-3.11.3-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.11.3/apache-camel-3.11.3-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.11.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.11.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (17)

[CAMEL-17043](https://issues.apache.org/jira/browse/CAMEL-17043)

camel-rest-openapi - Endpoint query parameters not forwarded to underlaying component endpoint

[CAMEL-17039](https://issues.apache.org/jira/browse/CAMEL-17039)

Camel-AWS2-S3: When includeBody is false, the message Body should not be set

[CAMEL-17034](https://issues.apache.org/jira/browse/CAMEL-17034)

Camel-Github: StartingSha should be an URI param and not an URI path

[CAMEL-17017](https://issues.apache.org/jira/browse/CAMEL-17017)

camel-metrics - Cannot be used out of the box due to mixed jackson JARs

[CAMEL-17015](https://issues.apache.org/jira/browse/CAMEL-17015)

camel-servlet - Issue with REST Service after Camel update - custom servletName does not work

[CAMEL-17011](https://issues.apache.org/jira/browse/CAMEL-17011)

camel-ssh - The producer should not be singleton

[CAMEL-17008](https://issues.apache.org/jira/browse/CAMEL-17008)

okStatusCodeRange does not permit single status code

[CAMEL-17007](https://issues.apache.org/jira/browse/CAMEL-17007)

camel-aws2-lambda: GetAlias is not working

[CAMEL-17004](https://issues.apache.org/jira/browse/CAMEL-17004)

camel-servlet - Should not close HttpServletInputStream when reading body into stream caching

[CAMEL-16990](https://issues.apache.org/jira/browse/CAMEL-16990)

camel-core - Stream caching checking for caused exception can lead to converter problem

[CAMEL-16957](https://issues.apache.org/jira/browse/CAMEL-16957)

NettyHttpHelper appends slash to an URI in case of empty CamelHttpPath

[CAMEL-16936](https://issues.apache.org/jira/browse/CAMEL-16936)

camel-aws2-s3: Not setting CONTENT-MD5 header which breaks putObject with object locks

[CAMEL-16924](https://issues.apache.org/jira/browse/CAMEL-16924)

After upgrade to Camel 3.11.0. Cannot write to HttpServletResponse when aggregator is used.

[CAMEL-16916](https://issues.apache.org/jira/browse/CAMEL-16916)

camel split with parallel processing true consumes lots of heap space when using camel-ftp

[CAMEL-16892](https://issues.apache.org/jira/browse/CAMEL-16892)

Camel-InfluxDB: Don't check database existence each time we perform a producer operation

[CAMEL-16877](https://issues.apache.org/jira/browse/CAMEL-16877)

camel-salesforce: any salesforce operation inside transaction times out

[CAMEL-14823](https://issues.apache.org/jira/browse/CAMEL-14823)

Support to disable the stream caching in camel-servlet from the camel context - once more

### Dependency upgrade (2)

[CAMEL-17047](https://issues.apache.org/jira/browse/CAMEL-17047)

camel-karaf - upgrade aries proxy version to 1.1.11 to support JDK11+

[CAMEL-16999](https://issues.apache.org/jira/browse/CAMEL-16999)

camel-spring-boot - Update to 2.5.5

### Improvement (5)

[CAMEL-17031](https://issues.apache.org/jira/browse/CAMEL-17031)

Performances/Profiling: Avoid boolean allocation in EventHelper

[CAMEL-17030](https://issues.apache.org/jira/browse/CAMEL-17030)

camel-ftp - Disconnect should ignore any kind of exception

[CAMEL-17023](https://issues.apache.org/jira/browse/CAMEL-17023)

Do not bundle Atlasmap DFDL module

[CAMEL-17022](https://issues.apache.org/jira/browse/CAMEL-17022)

camel-mina - MinaProducer does not disconnect on timeouts

[CAMEL-17020](https://issues.apache.org/jira/browse/CAMEL-17020)

camel-restdsl plugins doesn't implement all documented parameters for xml and yaml

### Task (1)

[CAMEL-16914](https://issues.apache.org/jira/browse/CAMEL-16914)

camel-kafka: possible corruption of idempotency messages when using KafkaIdempotentRepository

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).