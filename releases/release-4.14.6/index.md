# Apache camel 4.14.6 Release

## New and Noteworthy

This release is the new Camel 4.14.6 LTS release.

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
      <version>4.14.6</version>
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
      <version>4.14.6</version>
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
| [apache-camel-4.14.6-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-src.zip.sha512) |
| [apache-camel-4.14.6-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.xml.sha512) |
| [apache-camel-4.14.6-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.6/apache-camel-4.14.6-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.6` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.6

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (16)

[CAMEL-23310](https://issues.apache.org/jira/browse/CAMEL-23310)

camel-core - Suspend/resume on CamelContext should reset prepare shutdown flag

[CAMEL-23294](https://issues.apache.org/jira/browse/CAMEL-23294)

\[camel-sql\] JDBC-based Idempotent repository strategy fails in racing conditions.

[CAMEL-23282](https://issues.apache.org/jira/browse/CAMEL-23282)

Simple OGNL ${body.xxx} causes unbounded BeanInfo cache growth for ephemeral message bodies

[CAMEL-23279](https://issues.apache.org/jira/browse/CAMEL-23279)

SamplingDefinition.description() fails with NumberFormatException when samplePeriod uses property placeholders

[CAMEL-23267](https://issues.apache.org/jira/browse/CAMEL-23267)

File consumer does not release items in SimpleLRUCache

[CAMEL-23249](https://issues.apache.org/jira/browse/CAMEL-23249)

CXF RS Rest service loses content-type with stream caching enabled

[CAMEL-23122](https://issues.apache.org/jira/browse/CAMEL-23122)

camel-core - DefaultErrorHandler with logExhausted(false) still logs

[CAMEL-23061](https://issues.apache.org/jira/browse/CAMEL-23061)

camel-sql - SqlConsumer NPE if using exchange factory statistics

[CAMEL-23036](https://issues.apache.org/jira/browse/CAMEL-23036)

camel-core - NPE when pooled exchange in split at UoW done

[CAMEL-23030](https://issues.apache.org/jira/browse/CAMEL-23030)

Streaming splitter with aggregation using synchronous executor results in StackOverflowError

[CAMEL-23023](https://issues.apache.org/jira/browse/CAMEL-23023)

camel-kafka - Kafka consumers are started to eager before CamelContext is fully started

[CAMEL-23018](https://issues.apache.org/jira/browse/CAMEL-23018)

camel-rest-openapi - Response operation with content-type by no schema causes NPE

[CAMEL-22998](https://issues.apache.org/jira/browse/CAMEL-22998)

camel-kamelet - Kamelet should inherit route configuration so error handler can take affect

[CAMEL-22978](https://issues.apache.org/jira/browse/CAMEL-22978)

Camel Bean Constructor Fails to Resolve String Parameters with Quotes in Overloaded Factory Method

[CAMEL-22973](https://issues.apache.org/jira/browse/CAMEL-22973)

camel-core - ClassCastException in Splitter with exchange pooling

[CAMEL-22972](https://issues.apache.org/jira/browse/CAMEL-22972)

camel-as2 - AS2ClientConnection leaks HTTP connections on error paths

### Dependency upgrade (1)

[CAMEL-23027](https://issues.apache.org/jira/browse/CAMEL-23027)

camel-spring-boot - Upgrade to SB 3.5.11

### Improvement (6)

[CAMEL-23319](https://issues.apache.org/jira/browse/CAMEL-23319)

Improve error handling and add input validation in camel-mina converters

[CAMEL-23313](https://issues.apache.org/jira/browse/CAMEL-23313)

HeaderFilter Strategies: add lowerCase where it's not present - JMS, SJMS, CoAP, Google PubSub

[CAMEL-23224](https://issues.apache.org/jira/browse/CAMEL-23224)

camel-mail - MailHeaderFilterStrategy should also filter inbound headers

[CAMEL-23222](https://issues.apache.org/jira/browse/CAMEL-23222)

camel-coap: Integrate HeaderFilterStrategy for CoAP query parameter to header mapping

[CAMEL-23111](https://issues.apache.org/jira/browse/CAMEL-23111)

camel-jbang - camel run - YAML parsing errors not published to OTEL

[CAMEL-23029](https://issues.apache.org/jira/browse/CAMEL-23029)

Camel-Consul: Add ObjectInputFilter String pattern parameter in ConsulRegistry to be used in deserialize operations

### Task (1)

[CAMEL-22983](https://issues.apache.org/jira/browse/CAMEL-22983)

Several tests are failing with propertyDatabinding errors

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).