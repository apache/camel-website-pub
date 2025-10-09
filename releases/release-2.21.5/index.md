# Apache camel 2.21.5 Release

## New and Noteworthy

This release is a minor update of the 2.21.x branch.

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
      <version>2.21.5</version>
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
      <version>2.21.5</version>
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
| [apache-camel-2.21.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.21.5/apache-camel-2.21.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.21.5/apache-camel-2.21.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.21.5/apache-camel-2.21.5-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.21.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.21.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (14)

[CAMEL-13132](https://issues.apache.org/jira/browse/CAMEL-13132)

uploadBlobBlocks and commitBlobBlockList operations does not work with List

[CAMEL-13123](https://issues.apache.org/jira/browse/CAMEL-13123)

Endpoint shutdown closes mongo connection, killing the connection for everyone

[CAMEL-13093](https://issues.apache.org/jira/browse/CAMEL-13093)

Output of route-profile is empty if there are same route-id for multiple camel-contexts.

[CAMEL-13077](https://issues.apache.org/jira/browse/CAMEL-13077)

Olingo4 Consumer appears to not work with backoffIdleThreshold

[CAMEL-13063](https://issues.apache.org/jira/browse/CAMEL-13063)

Olingo2Endpoint swallowing consumer. options

[CAMEL-13062](https://issues.apache.org/jira/browse/CAMEL-13062)

olingo2 component serviceUri not set

[CAMEL-13061](https://issues.apache.org/jira/browse/CAMEL-13061)

Missing properties on Olingo2 consumer initialisation

[CAMEL-13059](https://issues.apache.org/jira/browse/CAMEL-13059)

camel-olingo2 assumes '/' at end of URI

[CAMEL-13058](https://issues.apache.org/jira/browse/CAMEL-13058)

AbstractFutureCallback generates NPE when response is a 401

[CAMEL-13054](https://issues.apache.org/jira/browse/CAMEL-13054)

Olingo4Endpoint swallowing consumer. options

[CAMEL-13049](https://issues.apache.org/jira/browse/CAMEL-13049)

Karaf commands that start/resume contexts and routes should use proper TCCL

[CAMEL-13044](https://issues.apache.org/jira/browse/CAMEL-13044)

Camel-AWS MQ: it is not possible to set Broker "Public accessibility" parameter using createBroker command

[CAMEL-13012](https://issues.apache.org/jira/browse/CAMEL-13012)

camel-olingo4 - AbstractFutureCallback generates NPE when response is a 401

[CAMEL-12980](https://issues.apache.org/jira/browse/CAMEL-12980)

Bundle in 'Active' State but Camel Context not initialized

### Improvement (4)

[CAMEL-13150](https://issues.apache.org/jira/browse/CAMEL-13150)

Add command "exchangeProperty" for dateExpression in ExpressionBuilder

[CAMEL-13072](https://issues.apache.org/jira/browse/CAMEL-13072)

In DefaultUnitOfWork:popRouteContext() avoid exception thrown

[CAMEL-13066](https://issues.apache.org/jira/browse/CAMEL-13066)

camel-hystrix - Do not fallback on HystrixBadRequestException

[CAMEL-13042](https://issues.apache.org/jira/browse/CAMEL-13042)

camel-core - File producer should by default not allow writing files to directories outside its starting directory

### Task (1)

[CAMEL-13041](https://issues.apache.org/jira/browse/CAMEL-13041)

Camel-AWS MQ: Create Broker operation is not working

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).