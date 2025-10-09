# Apache camel 4.14.0 Release

## New and Noteworthy

This release is the new Camel 4.14.0 LTS release.

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
      <version>4.14.0</version>
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
      <version>4.14.0</version>
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
| [apache-camel-4.14.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-src.zip.sha512) |
| [apache-camel-4.14.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.xml.sha512) |
| [apache-camel-4.14.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.14.0/apache-camel-4.14.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.14.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.14.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (30)

[CAMEL-22417](https://issues.apache.org/jira/browse/CAMEL-22417)

ErrorHandlerReifier fails with Unsupported definition: null

[CAMEL-22342](https://issues.apache.org/jira/browse/CAMEL-22342)

camel-jbang - Export using Maven GAV that has number can cause java compilation error

[CAMEL-22339](https://issues.apache.org/jira/browse/CAMEL-22339)

CloudEvents Json DataTypeTransformer not handling Json payloads

[CAMEL-22331](https://issues.apache.org/jira/browse/CAMEL-22331)

camel-jbang-plugin-kubernetes: wrong container probes port

[CAMEL-22314](https://issues.apache.org/jira/browse/CAMEL-22314)

Configuration camel.main.fileConfigurations not taken into account

[CAMEL-22294](https://issues.apache.org/jira/browse/CAMEL-22294)

camel-zipfile - decompression of multi-member archive

[CAMEL-22293](https://issues.apache.org/jira/browse/CAMEL-22293)

camel-core - Endpoint DSL with option using a object instance does not work with pollEnrich

[CAMEL-22282](https://issues.apache.org/jira/browse/CAMEL-22282)

platform-http using spring boot won't create the producer URL correctly in case of bridged url

[CAMEL-22273](https://issues.apache.org/jira/browse/CAMEL-22273)

Google Storage Component: Content disposition header is not set correctly

[CAMEL-22268](https://issues.apache.org/jira/browse/CAMEL-22268)

camel-jbang - camel infra get can return old data

[CAMEL-22267](https://issues.apache.org/jira/browse/CAMEL-22267)

camel-jbang - camel infra run xxx should create log dir if missing

[CAMEL-22264](https://issues.apache.org/jira/browse/CAMEL-22264)

camel-catalog - XPath language doesn't seem to validate

[CAMEL-22262](https://issues.apache.org/jira/browse/CAMEL-22262)

Wrong handling SftpConsumer.getRelativeFilePath and FtpConsumer.getRelativeFilePath

[CAMEL-22261](https://issues.apache.org/jira/browse/CAMEL-22261)

camel-kafka - Kafka producer should reuse existing transaction if already transacted

[CAMEL-22253](https://issues.apache.org/jira/browse/CAMEL-22253)

camel-sjms - Setting JMS delivery mode should not set via property

[CAMEL-22251](https://issues.apache.org/jira/browse/CAMEL-22251)

Incorrect Exchange status when using camel-rest

[CAMEL-22248](https://issues.apache.org/jira/browse/CAMEL-22248)

camel-jbang - Export http endpoint issue with http://@@CamelMagicValue@@

[CAMEL-22247](https://issues.apache.org/jira/browse/CAMEL-22247)

Camel Google Components: Make the scopes parameter a string in all the components

[CAMEL-22241](https://issues.apache.org/jira/browse/CAMEL-22241)

camel-kudu: AsyncKuduClient.build throws ClassNotFoundException: com/stumbleupon/async/Callback

[CAMEL-22239](https://issues.apache.org/jira/browse/CAMEL-22239)

camel-catalog - Language model does not include functions

[CAMEL-22235](https://issues.apache.org/jira/browse/CAMEL-22235)

camel-smb - SmbOperations may swallow exception and can cause NPE with camel-file

[CAMEL-22229](https://issues.apache.org/jira/browse/CAMEL-22229)

camel-core - Inlined anonymous DataFormat in java based route template is not supported

[CAMEL-22228](https://issues.apache.org/jira/browse/CAMEL-22228)

Camel jbang export for SpringBoot and Main generates invalid CamelApplication.java file when gav is not specified and use of \`.\` as target to export

[CAMEL-22227](https://issues.apache.org/jira/browse/CAMEL-22227)

Camel JBang update dependency is generating wrong dependencies in the pom.xml for quarkus

[CAMEL-22226](https://issues.apache.org/jira/browse/CAMEL-22226)

Camel JBang dependency update is not working when called from a different folder than the target pom.xml

[CAMEL-22220](https://issues.apache.org/jira/browse/CAMEL-22220)

camel-jbang - Nullpointer when using get variable command

[CAMEL-22219](https://issues.apache.org/jira/browse/CAMEL-22219)

Missing method list, emptyTrash and GenerateIds for Google Drive files

[CAMEL-22216](https://issues.apache.org/jira/browse/CAMEL-22216)

camel-zipfile - ZipIterator in split streamning mode does not trigger last element as completed

[CAMEL-22174](https://issues.apache.org/jira/browse/CAMEL-22174)

camel-smb : doesn't recover from TransportException if smb share disappears from network

[CAMEL-22144](https://issues.apache.org/jira/browse/CAMEL-22144)

camel-jbang: Kubernetes plugin management port for liveness/readiness

### Dependency upgrade (4)

[CAMEL-22298](https://issues.apache.org/jira/browse/CAMEL-22298)

camel-debezium - Upgrade to 3.2.x

[CAMEL-22270](https://issues.apache.org/jira/browse/CAMEL-22270)

camel-spring-boot - Upgrade to 3.5.4

[CAMEL-22258](https://issues.apache.org/jira/browse/CAMEL-22258)

Upgrade apache directory to 2.0.0.AM27

[CAMEL-22236](https://issues.apache.org/jira/browse/CAMEL-22236)

Camel-Jbang: Bump Camel Kamelets to version 4.13.0

### Improvement (55)

[CAMEL-22350](https://issues.apache.org/jira/browse/CAMEL-22350)

camel-main - The spring-cloud vault lacks documentation for each option

[CAMEL-22346](https://issues.apache.org/jira/browse/CAMEL-22346)

camel-core - Deprecate global options for http.proxy

[CAMEL-22345](https://issues.apache.org/jira/browse/CAMEL-22345)

camel-http - The proxy options are named auth which is a bit confusing

[CAMEL-22338](https://issues.apache.org/jira/browse/CAMEL-22338)

camel-core - Message history elapsed time should exclude debug wait time

[CAMEL-22336](https://issues.apache.org/jira/browse/CAMEL-22336)

Migrate Olingo4 tests to WireMock for better stability

[CAMEL-22333](https://issues.apache.org/jira/browse/CAMEL-22333)

camel-netty - The options are not in use for the producer

[CAMEL-22328](https://issues.apache.org/jira/browse/CAMEL-22328)

camel-langchain4j-tools: Avoid using JsonNode for parameter header values

[CAMEL-22327](https://issues.apache.org/jira/browse/CAMEL-22327)

camel-langchain4j-agent: separate API interface from implementation

[CAMEL-22326](https://issues.apache.org/jira/browse/CAMEL-22326)

camel-langchain4j-agent: implement support for any type of agent

[CAMEL-22321](https://issues.apache.org/jira/browse/CAMEL-22321)

OpenSearch SSL Fallback Issue

[CAMEL-22320](https://issues.apache.org/jira/browse/CAMEL-22320)

camel-jbang - camel debug to step N so user can fast forward

[CAMEL-22317](https://issues.apache.org/jira/browse/CAMEL-22317)

camel-jbang - Speedup camel debug

[CAMEL-22315](https://issues.apache.org/jira/browse/CAMEL-22315)

camel-core - Debug skip over

[CAMEL-22313](https://issues.apache.org/jira/browse/CAMEL-22313)

camel-core - Disable and Enable EIPs at runtime

[CAMEL-22312](https://issues.apache.org/jira/browse/CAMEL-22312)

camel-core - Stopping route removes managed processors in JMX

[CAMEL-22311](https://issues.apache.org/jira/browse/CAMEL-22311)

Add camel-langchain4j-embedding support for weaviate

[CAMEL-22309](https://issues.apache.org/jira/browse/CAMEL-22309)

camel-spring-batch - Should auto wire job launcher and registry

[CAMEL-22307](https://issues.apache.org/jira/browse/CAMEL-22307)

camel-core - Add dumpRouteStatAsJson

[CAMEL-22304](https://issues.apache.org/jira/browse/CAMEL-22304)

camel-core - Add exchangesTotal to dumpRouteStatsAsXml

[CAMEL-22299](https://issues.apache.org/jira/browse/CAMEL-22299)

camel-platform-http-main - Use camel-json-util for building json response

[CAMEL-22297](https://issues.apache.org/jira/browse/CAMEL-22297)

camel-jsonata does not support json array as input

[CAMEL-22295](https://issues.apache.org/jira/browse/CAMEL-22295)

camel-core - Consumer can setup MDC with route id during internal processing

[CAMEL-22291](https://issues.apache.org/jira/browse/CAMEL-22291)

camel-aws-s3 - Consumer can use nextMarker if file listening is truncated

[CAMEL-22287](https://issues.apache.org/jira/browse/CAMEL-22287)

camel-main - Max wait duration seconds - allow to use -1 to be really fast

[CAMEL-22285](https://issues.apache.org/jira/browse/CAMEL-22285)

platform-http-main - Dev consoles should be registered as management endpoints

[CAMEL-22283](https://issues.apache.org/jira/browse/CAMEL-22283)

camel-jbang - infra stop to stop by pid also

[CAMEL-22279](https://issues.apache.org/jira/browse/CAMEL-22279)

camel-jbang - infra run to have --background option

[CAMEL-22278](https://issues.apache.org/jira/browse/CAMEL-22278)

spring-rabbitmq - producer performance

[CAMEL-22276](https://issues.apache.org/jira/browse/CAMEL-22276)

Camel HTTP OAuth2 request doesn't support body authentication

[CAMEL-22269](https://issues.apache.org/jira/browse/CAMEL-22269)

camel-jbang - test infra better shutdown message

[CAMEL-22266](https://issues.apache.org/jira/browse/CAMEL-22266)

camel-jbang - Should use java 21 as default java version

[CAMEL-22265](https://issues.apache.org/jira/browse/CAMEL-22265)

camel-jbang infra run: Set the container name to a fixed name

[CAMEL-22263](https://issues.apache.org/jira/browse/CAMEL-22263)

camel-core - Deprecate PARENT\_UNIT\_OF\_WORK

[CAMEL-22260](https://issues.apache.org/jira/browse/CAMEL-22260)

\[camel-langchain4j-tools\] Support for defining the tool names

[CAMEL-22259](https://issues.apache.org/jira/browse/CAMEL-22259)

camel-core - Splitter with shareUnitOfWork should use single uow

[CAMEL-22257](https://issues.apache.org/jira/browse/CAMEL-22257)

Support for Java 25 - Fix deprecations and removals

[CAMEL-22256](https://issues.apache.org/jira/browse/CAMEL-22256)

camel-http - Configuring tineout options should be tooling friendly

[CAMEL-22255](https://issues.apache.org/jira/browse/CAMEL-22255)

camel-jbang - Only include camel-groovy if there are groovy source files

[CAMEL-22254](https://issues.apache.org/jira/browse/CAMEL-22254)

Generate Camel Quarkus project without \`quarkus.native.resources.includes\` for \`src/main/resources/camel\` when Camel Quarkus version is 3.22+

[CAMEL-22250](https://issues.apache.org/jira/browse/CAMEL-22250)

camel-jackson - Allow to configure stream reader constraints

[CAMEL-22245](https://issues.apache.org/jira/browse/CAMEL-22245)

camel-core - EventNotifier should allow Ordered

[CAMEL-22238](https://issues.apache.org/jira/browse/CAMEL-22238)

Camel JBang automated test plugin

[CAMEL-22237](https://issues.apache.org/jira/browse/CAMEL-22237)

camel-jbang - Loading expression scripts from file vs classpath

[CAMEL-22233](https://issues.apache.org/jira/browse/CAMEL-22233)

camel-spring-boot - Properties component should eager be configured

[CAMEL-22232](https://issues.apache.org/jira/browse/CAMEL-22232)

camel-micrometer: Add filter option to Micrometer Dev Console

[CAMEL-22231](https://issues.apache.org/jira/browse/CAMEL-22231)

camel-ai: camel langchain4j-tools should have strict description policy

[CAMEL-22230](https://issues.apache.org/jira/browse/CAMEL-22230)

Camel-PQC: Support more signature and KEM algorithms

[CAMEL-22225](https://issues.apache.org/jira/browse/CAMEL-22225)

Support "generic" parameters for Google component

[CAMEL-22224](https://issues.apache.org/jira/browse/CAMEL-22224)

camel-jbang - get group

[CAMEL-22223](https://issues.apache.org/jira/browse/CAMEL-22223)

Add group to a templatedRoute

[CAMEL-22215](https://issues.apache.org/jira/browse/CAMEL-22215)

camel-core - Interceptor EIPs should include more information where the interception happened

[CAMEL-22187](https://issues.apache.org/jira/browse/CAMEL-22187)

camel-jbang - Camel export should only include observability if --observe

[CAMEL-22089](https://issues.apache.org/jira/browse/CAMEL-22089)

camel-observability-services - Port 9876 should be optional

[CAMEL-21917](https://issues.apache.org/jira/browse/CAMEL-21917)

\[camel-telemetry\] Load decorators dynamically

[CAMEL-16871](https://issues.apache.org/jira/browse/CAMEL-16871)

Support camel-aws2-s3 multipart with remote files

### New Feature (9)

[CAMEL-22330](https://issues.apache.org/jira/browse/CAMEL-22330)

camel-vertx-websocket: Add dev console for vertx-websocket consumers

[CAMEL-22322](https://issues.apache.org/jira/browse/CAMEL-22322)

camel-jbang : camel debug a spring-boot app

[CAMEL-22310](https://issues.apache.org/jira/browse/CAMEL-22310)

camel-core - Add RouteGroupMBean

[CAMEL-22288](https://issues.apache.org/jira/browse/CAMEL-22288)

camel-jbang: Kubernetes plugin: add --source-dir option

[CAMEL-22244](https://issues.apache.org/jira/browse/CAMEL-22244)

camel-salesforce: support multipart blob uploads

[CAMEL-22214](https://issues.apache.org/jira/browse/CAMEL-22214)

camel-groovy - Allow to pre-load groovy source files for shared functions and DTOs

[CAMEL-22205](https://issues.apache.org/jira/browse/CAMEL-22205)

Provide Camel JBang properties in Camel catalog

[CAMEL-22196](https://issues.apache.org/jira/browse/CAMEL-22196)

Create an AI agent component

[CAMEL-21974](https://issues.apache.org/jira/browse/CAMEL-21974)

camel-j8583 - dataformat for ISO-8583 standard

### Task (7)

[CAMEL-22308](https://issues.apache.org/jira/browse/CAMEL-22308)

ca.uhn.fhir.rest.client.api.IGenericClient.fetchConformance deprecated

[CAMEL-22303](https://issues.apache.org/jira/browse/CAMEL-22303)

camel-torchserve: deprecate component

[CAMEL-22301](https://issues.apache.org/jira/browse/CAMEL-22301)

Align support level for AI components

[CAMEL-22286](https://issues.apache.org/jira/browse/CAMEL-22286)

\[doc\] Mail-microsoft-oauth: make component requirements easier to understand

[CAMEL-22246](https://issues.apache.org/jira/browse/CAMEL-22246)

camel-run-plugin - WARN about unknown option

[CAMEL-22240](https://issues.apache.org/jira/browse/CAMEL-22240)

camel-kafka - Remove camel-console dependency

[CAMEL-21408](https://issues.apache.org/jira/browse/CAMEL-21408)

camel-jbang - export is not working when specifying a Camel route with a path

### Test (3)

[CAMEL-22316](https://issues.apache.org/jira/browse/CAMEL-22316)

camel-azure - Upgrade Azurite

[CAMEL-22252](https://issues.apache.org/jira/browse/CAMEL-22252)

Regression CreateEndpointManualIssueTest.testCreateEndpoint is now failing

[CAMEL-21523](https://issues.apache.org/jira/browse/CAMEL-21523)

camel-jbang - Improve assertions when checking for a Maven dependency

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).