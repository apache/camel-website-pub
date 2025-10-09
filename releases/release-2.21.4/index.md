# Apache camel 2.21.4 Release

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
      <version>2.21.4</version>
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
      <version>2.21.4</version>
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
| [apache-camel-2.21.4-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.21.4/apache-camel-2.21.4-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.21.4/apache-camel-2.21.4-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.21.4/apache-camel-2.21.4-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.21.4` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.21.4

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (21)

[CAMEL-13028](https://issues.apache.org/jira/browse/CAMEL-13028)

camel-undertow - When using SSL with rest-dsl and api-doc then you can get a port already bound exception

[CAMEL-13016](https://issues.apache.org/jira/browse/CAMEL-13016)

camel-jetty - If multiple bundles uses the same context-path (pathspec) then Jetty should fail

[CAMEL-13014](https://issues.apache.org/jira/browse/CAMEL-13014)

camel mqtt crash using high volume traffic

[CAMEL-13008](https://issues.apache.org/jira/browse/CAMEL-13008)

Odata-connector assumes '/' at end of URI

[CAMEL-13006](https://issues.apache.org/jira/browse/CAMEL-13006)

Missing properties on Olingo4 consumer initialisation

[CAMEL-13005](https://issues.apache.org/jira/browse/CAMEL-13005)

olingo4 component serviceUri not set

[CAMEL-12974](https://issues.apache.org/jira/browse/CAMEL-12974)

Route coverage: When and otherwise are not marked as covered

[CAMEL-12969](https://issues.apache.org/jira/browse/CAMEL-12969)

camel-core-osgi: Slow Memory Leak in OsgiServiceRegistry

[CAMEL-12942](https://issues.apache.org/jira/browse/CAMEL-12942)

camel-dropbox: upload file does not work

[CAMEL-12940](https://issues.apache.org/jira/browse/CAMEL-12940)

Dynamic doneFileName is not working with filename containing 2 dots

[CAMEL-12933](https://issues.apache.org/jira/browse/CAMEL-12933)

Camel FTP regression: RemoteFile does not override populateHeaders method

[CAMEL-12932](https://issues.apache.org/jira/browse/CAMEL-12932)

Camel-AHC-WS: Consumer parameters are not set

[CAMEL-12916](https://issues.apache.org/jira/browse/CAMEL-12916)

camel-http4 - The sslContextParameters option should be documented on endpoint as well

[CAMEL-12911](https://issues.apache.org/jira/browse/CAMEL-12911)

gzip Content-Encoding problems after upgrading to Jetty 9.4.12

[CAMEL-12900](https://issues.apache.org/jira/browse/CAMEL-12900)

Route contract validate does not throw validation exception when validation fails

[CAMEL-12897](https://issues.apache.org/jira/browse/CAMEL-12897)

PGP Decryption in XML DSL not working

[CAMEL-12891](https://issues.apache.org/jira/browse/CAMEL-12891)

camel-kubernetes getConfigMap does not use Namespace Header

[CAMEL-12890](https://issues.apache.org/jira/browse/CAMEL-12890)

Camel Printer unable to print to the network printer

[CAMEL-12835](https://issues.apache.org/jira/browse/CAMEL-12835)

camel-json-validator - Potential issue with reading from streams

[CAMEL-12774](https://issues.apache.org/jira/browse/CAMEL-12774)

Error during type conversion from type: java.lang.String to the required type: org.elasticsearch.action.update.UpdateRequest

[CAMEL-12626](https://issues.apache.org/jira/browse/CAMEL-12626)

Camel Tracing is not working for route with redelivery strategy

### Improvement (3)

[CAMEL-13029](https://issues.apache.org/jira/browse/CAMEL-13029)

camel-swagger-java - Should default use scheme from rest-dsl configuration in swagger doc

[CAMEL-13025](https://issues.apache.org/jira/browse/CAMEL-13025)

camel-core - File read lock changed - If file gets deleted then break out loop

[CAMEL-12631](https://issues.apache.org/jira/browse/CAMEL-12631)

SFTP: Socket timeout overwrites Server Alive Interval

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).