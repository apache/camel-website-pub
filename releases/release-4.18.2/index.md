# Apache camel 4.18.2 Release

## New and Noteworthy

This release is the new Camel 4.18.2 LTS release.

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
      <version>4.18.2</version>
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
      <version>4.18.2</version>
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
| [apache-camel-4.18.2-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.2/apache-camel-4.18.2-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-src.zip.sha512) |
| [apache-camel-4.18.2-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.xml.sha512) |
| [apache-camel-4.18.2-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.18.2/apache-camel-4.18.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.18.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.18.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (13)

[CAMEL-23310](https://issues.apache.org/jira/browse/CAMEL-23310)

camel-core - Suspend/resume on CamelContext should reset prepare shutdown flag

[CAMEL-23299](https://issues.apache.org/jira/browse/CAMEL-23299)

Aggregated exchange does not preserve the transacted flag from the original exchange

[CAMEL-23294](https://issues.apache.org/jira/browse/CAMEL-23294)

\[camel-sql\] JDBC-based Idempotent repository strategy fails in racing conditions.

[CAMEL-23284](https://issues.apache.org/jira/browse/CAMEL-23284)

Pipe YAML Kamelet properties with {{placeholder}} get URL-encoded, preventing property resolution

[CAMEL-23283](https://issues.apache.org/jira/browse/CAMEL-23283)

OpenTelemetry/Micrometer traces are not correctly structured for JMS-initiated routes

[CAMEL-23282](https://issues.apache.org/jira/browse/CAMEL-23282)

Simple OGNL ${body.xxx} causes unbounded BeanInfo cache growth for ephemeral message bodies

[CAMEL-23281](https://issues.apache.org/jira/browse/CAMEL-23281)

\[camel-core\] split/aggregator stuck in tx

[CAMEL-23279](https://issues.apache.org/jira/browse/CAMEL-23279)

SamplingDefinition.description() fails with NumberFormatException when samplePeriod uses property placeholders

[CAMEL-23272](https://issues.apache.org/jira/browse/CAMEL-23272)

\`--management-port\` is overriding \`restConfiguration > port\`

[CAMEL-23267](https://issues.apache.org/jira/browse/CAMEL-23267)

File consumer does not release items in SimpleLRUCache

[CAMEL-23260](https://issues.apache.org/jira/browse/CAMEL-23260)

ServiceBusComponent: RejectedExecutionException during graceful shutdown after successful exchange completion

[CAMEL-23249](https://issues.apache.org/jira/browse/CAMEL-23249)

CXF RS Rest service loses content-type with stream caching enabled

[CAMEL-23193](https://issues.apache.org/jira/browse/CAMEL-23193)

JmsMessage does not copy attachments to new instance

### Improvement (7)

[CAMEL-23322](https://issues.apache.org/jira/browse/CAMEL-23322)

camel-infinispan: align remote aggregation repository options with sibling repos

[CAMEL-23321](https://issues.apache.org/jira/browse/CAMEL-23321)

camel-jms, camel-sjms, camel-amqp - Add deserialization filtering for ObjectMessage handling

[CAMEL-23319](https://issues.apache.org/jira/browse/CAMEL-23319)

Improve error handling and add input validation in camel-mina converters

[CAMEL-23313](https://issues.apache.org/jira/browse/CAMEL-23313)

HeaderFilter Strategies: add lowerCase where it's not present - JMS, SJMS, CoAP, Google PubSub

[CAMEL-23277](https://issues.apache.org/jira/browse/CAMEL-23277)

camel-jsch: Add OpenSSH certificate support to jsch based components

[CAMEL-23254](https://issues.apache.org/jira/browse/CAMEL-23254)

Add Milvus helper beans for YAML DSL usage

[CAMEL-23243](https://issues.apache.org/jira/browse/CAMEL-23243)

Enhance the OpenAI operation property

### New Feature (2)

[CAMEL-23276](https://issues.apache.org/jira/browse/CAMEL-23276)

Allow JBang plugins to customize Run command before CamelContext is built

[CAMEL-23252](https://issues.apache.org/jira/browse/CAMEL-23252)

Add onReload SPI method to ContextServicePlugin for dev-mode hot-reload hooks

### Task (3)

[CAMEL-23309](https://issues.apache.org/jira/browse/CAMEL-23309)

Camel-Jbang: Upgrade to Camel-Kamelets 4.18.1

[CAMEL-23298](https://issues.apache.org/jira/browse/CAMEL-23298)

camel-core - PGC and ODCF dataformats are missing in model

[CAMEL-23200](https://issues.apache.org/jira/browse/CAMEL-23200)

Camel-PQC: Replace Java serialization with PKCS#8/X.509 in FileBasedKeyLifecycleManager

### Test (1)

[CAMEL-23217](https://issues.apache.org/jira/browse/CAMEL-23217)

CamelSalesforceIT is failing on SpringBoot with NoClassDefFoundError: com/google/protobuf/RuntimeVersion$RuntimeDomain

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).