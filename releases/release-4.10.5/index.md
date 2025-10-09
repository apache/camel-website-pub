# Apache camel 4.10.5 Release

## New and Noteworthy

This release is the new Camel 4.10.5 release.

## Supported Java version

This version supports Java 17 and 21.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.10.5</version>
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
      <version>4.10.5</version>
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
| [apache-camel-4.10.5-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-src.zip.sha512) |
| [apache-camel-4.10.5-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.xml.sha512) |
| [apache-camel-4.10.5-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.10.5/apache-camel-4.10.5-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.10.5` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.10.5

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (18)

[CAMEL-22103](https://issues.apache.org/jira/browse/CAMEL-22103)

camel-cxf: CXF RS Rest service with optional query parameter fails

[CAMEL-22100](https://issues.apache.org/jira/browse/CAMEL-22100)

camel-jbang - Transitive dependencies on plugins should use the parent artifact to manage versions

[CAMEL-22095](https://issues.apache.org/jira/browse/CAMEL-22095)

camel-core - Rest DSL with inlined routes does not work with AdviceWith testing

[CAMEL-22082](https://issues.apache.org/jira/browse/CAMEL-22082)

camel-stream - NPE if charset is not specified

[CAMEL-22073](https://issues.apache.org/jira/browse/CAMEL-22073)

camel-http - NTLM authentication doesn't work over http

[CAMEL-22068](https://issues.apache.org/jira/browse/CAMEL-22068)

Camel-bindy does not treat escaped double quotes in CSV data

[CAMEL-22065](https://issues.apache.org/jira/browse/CAMEL-22065)

camel-rest-openapi: OpenApi specification in the rest configuration will be ignored in Camel Spring Boot

[CAMEL-22062](https://issues.apache.org/jira/browse/CAMEL-22062)

camel-jsonata: outputType: Jackson does not output Jackson body

[CAMEL-22059](https://issues.apache.org/jira/browse/CAMEL-22059)

camel-ssh - Calling 2nd time does not keep correct exit value header

[CAMEL-22057](https://issues.apache.org/jira/browse/CAMEL-22057)

camel-jbang - Dependency command does not handle version

[CAMEL-22056](https://issues.apache.org/jira/browse/CAMEL-22056)

camel-jbang - Annotation based dependency injection with lazy-bean should should be registered as supplier based

[CAMEL-22055](https://issues.apache.org/jira/browse/CAMEL-22055)

camel-main - Loaded Java routes may be dependency injected twice

[CAMEL-22050](https://issues.apache.org/jira/browse/CAMEL-22050)

camel-rest-openapi - Component configuration should be used in endpoint

[CAMEL-22038](https://issues.apache.org/jira/browse/CAMEL-22038)

aws-ddb: float/doubles are being set as ddb attribute type=S while using transformer - Ddb2JsonDataTypeTransformer

[CAMEL-22037](https://issues.apache.org/jira/browse/CAMEL-22037)

camel-as2 - In AS2Receiver, line feeds are replaced by CRLF

[CAMEL-22026](https://issues.apache.org/jira/browse/CAMEL-22026)

Camel SJMS & SJMS2 component cause thread leak when the route is stopped.

[CAMEL-22020](https://issues.apache.org/jira/browse/CAMEL-22020)

platform-http - Error in clientRequestValidation consumes & produces when plus sign in content-type

[CAMEL-21963](https://issues.apache.org/jira/browse/CAMEL-21963)

camel-infinispan - query parameters not working

### Dependency upgrade (1)

[CAMEL-22036](https://issues.apache.org/jira/browse/CAMEL-22036)

camel-jackson-avro: Align avro version with Camel

### Improvement (5)

[CAMEL-22122](https://issues.apache.org/jira/browse/CAMEL-22122)

camel-stub - No INFO about duplicates in use

[CAMEL-22087](https://issues.apache.org/jira/browse/CAMEL-22087)

\[JBang\] Unable to execute multithreading under different ports and process name

[CAMEL-22061](https://issues.apache.org/jira/browse/CAMEL-22061)

camel-test-junit - Make it easy to include more than 1 route builder in Java

[CAMEL-22049](https://issues.apache.org/jira/browse/CAMEL-22049)

camel-aws2-kinesis: use created async client for KCL consumer

[CAMEL-22029](https://issues.apache.org/jira/browse/CAMEL-22029)

aws dynamodb scan and query not implemented with attributes-to-get

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).