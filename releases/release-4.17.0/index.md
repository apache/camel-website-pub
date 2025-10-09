# Apache camel 4.17.0 Release

## New and Noteworthy

This release is the new Camel 4.17.0 release.

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
      <version>4.17.0</version>
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
      <version>4.17.0</version>
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
| [apache-camel-4.17.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-src.zip.sha512) |
| [apache-camel-4.17.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.xml.sha512) |
| [apache-camel-4.17.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.17.0/apache-camel-4.17.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.17.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.17.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (35)

[CAMEL-22798](https://issues.apache.org/jira/browse/CAMEL-22798)

camel-jbang: Tests fail on Windows

[CAMEL-22790](https://issues.apache.org/jira/browse/CAMEL-22790)

RestOpenApiReader does not build an ApiResponse correctly for multiple produces content types

[CAMEL-22789](https://issues.apache.org/jira/browse/CAMEL-22789)

camel-core - Using bridgeErrorHandler=true can cause endless loop if triggered from onCompletion (such as camel-aws-s3)

[CAMEL-22787](https://issues.apache.org/jira/browse/CAMEL-22787)

Camel-bean: CAMEL-22775 introduced an wrong method detection if Exchange is an arg

[CAMEL-22784](https://issues.apache.org/jira/browse/CAMEL-22784)

Failover in FileLockClusterService is unreliable when running multiple JVMs

[CAMEL-22776](https://issues.apache.org/jira/browse/CAMEL-22776)

camel-jbang-kubernetes: Unable to export project on Windows

[CAMEL-22772](https://issues.apache.org/jira/browse/CAMEL-22772)

Freemarker shared variables not respected when using dynamic templates

[CAMEL-22769](https://issues.apache.org/jira/browse/CAMEL-22769)

\[camel-cxf\] Possible jakarta/javax class mismatch

[CAMEL-22762](https://issues.apache.org/jira/browse/CAMEL-22762)

aws2-sqs: queue URL stays null if the queue is created after the application has already started

[CAMEL-22759](https://issues.apache.org/jira/browse/CAMEL-22759)

camel-caffeine - Camel context null during test execution

[CAMEL-22758](https://issues.apache.org/jira/browse/CAMEL-22758)

camel-jbang - Debug inside choice may not correlate to source location

[CAMEL-22754](https://issues.apache.org/jira/browse/CAMEL-22754)

Additional route step after a body is set to Response may alter the HTTP code in the Response

[CAMEL-22753](https://issues.apache.org/jira/browse/CAMEL-22753)

camel-jbang-kubernetes: remove the podman build strategy

[CAMEL-22749](https://issues.apache.org/jira/browse/CAMEL-22749)

\[camel-kafka/camel-observation\] tracing fails for Kafka consumer with multiple topics

[CAMEL-22743](https://issues.apache.org/jira/browse/CAMEL-22743)

camel-jbang - get platfomr-http with --all does not show management

[CAMEL-22741](https://issues.apache.org/jira/browse/CAMEL-22741)

pollEnrich EIP doesn't preserve the original headers

[CAMEL-22738](https://issues.apache.org/jira/browse/CAMEL-22738)

\[camel-core-reifier\] No language could be found for: simple-no-file

[CAMEL-22717](https://issues.apache.org/jira/browse/CAMEL-22717)

camel-mdc - MDC values get lost at interceptedSendTo Endpoint

[CAMEL-22716](https://issues.apache.org/jira/browse/CAMEL-22716)

SpringBootAzureKeyVaultPropertiesParser uses environment variable with dot

[CAMEL-22707](https://issues.apache.org/jira/browse/CAMEL-22707)

File consumer move option misbehaves when used in pollEnrich

[CAMEL-22699](https://issues.apache.org/jira/browse/CAMEL-22699)

Camel JBang run --stub affects all endpoints

[CAMEL-22696](https://issues.apache.org/jira/browse/CAMEL-22696)

camel-jbang: export for quarkus runtime causes camel-dsl-modeline error

[CAMEL-22695](https://issues.apache.org/jira/browse/CAMEL-22695)

camel-jbang: --observe flag being ignored

[CAMEL-22691](https://issues.apache.org/jira/browse/CAMEL-22691)

camel-cxf - Memory leak in CXF producer

[CAMEL-22675](https://issues.apache.org/jira/browse/CAMEL-22675)

Camel JBang Run with --source-dir always loads http server

[CAMEL-22667](https://issues.apache.org/jira/browse/CAMEL-22667)

camel-jbang - Using --stub with none existing may cause timer to not trigger

[CAMEL-22660](https://issues.apache.org/jira/browse/CAMEL-22660)

camel-jbang - Use --stub=all should only stub components

[CAMEL-22659](https://issues.apache.org/jira/browse/CAMEL-22659)

Aggregator completionInterval not working during shutdown

[CAMEL-22658](https://issues.apache.org/jira/browse/CAMEL-22658)

\[camel-google-pubsub\] GooglePubsubProducer fails with INVALID\_ARGUMENT

[CAMEL-22657](https://issues.apache.org/jira/browse/CAMEL-22657)

camel-jbang - NPE in row clone

[CAMEL-22656](https://issues.apache.org/jira/browse/CAMEL-22656)

camel-jbang - Using --prompt ask for location of some internal main property

[CAMEL-22653](https://issues.apache.org/jira/browse/CAMEL-22653)

\[camel-api-component-maven-plugin\] Circumvent wildcard import issue

[CAMEL-22651](https://issues.apache.org/jira/browse/CAMEL-22651)

camel-jbang - Using --stub does not work correct with multiple patterns

[CAMEL-22627](https://issues.apache.org/jira/browse/CAMEL-22627)

Camel fails graceful shutdown with wiretap/kamelet

[CAMEL-22529](https://issues.apache.org/jira/browse/CAMEL-22529)

route configuration in Java DSL with multiple onException does not work

### Dependency upgrade (12)

[CAMEL-22795](https://issues.apache.org/jira/browse/CAMEL-22795)

camel-debezium - Upgrade to 3.4.x

[CAMEL-22792](https://issues.apache.org/jira/browse/CAMEL-22792)

camel-spring-boot - Upgrade to 3.5.9

[CAMEL-22788](https://issues.apache.org/jira/browse/CAMEL-22788)

Investigate upgrading to at.yawk.lz4:lz4-java 1.10.1

[CAMEL-22757](https://issues.apache.org/jira/browse/CAMEL-22757)

camel-tika - Upgrade to tika 3.x

[CAMEL-22735](https://issues.apache.org/jira/browse/CAMEL-22735)

camel-infinispan-starter - Update unit test after v16 upgrade

[CAMEL-22720](https://issues.apache.org/jira/browse/CAMEL-22720)

Update testcontainer to 2.0.2

[CAMEL-22701](https://issues.apache.org/jira/browse/CAMEL-22701)

camel-spring-boot - Upgrade to 3.5.8

[CAMEL-22692](https://issues.apache.org/jira/browse/CAMEL-22692)

camel-infinispan: Upgrade to Infinispan 16.x

[CAMEL-22679](https://issues.apache.org/jira/browse/CAMEL-22679)

camel-microprofile-health - Upgrade smallrye health 4.3

[CAMEL-22593](https://issues.apache.org/jira/browse/CAMEL-22593)

camel-infinispan JDK25 compilation issues

[CAMEL-22578](https://issues.apache.org/jira/browse/CAMEL-22578)

Upgrade Artemis to 2.43+

[CAMEL-22574](https://issues.apache.org/jira/browse/CAMEL-22574)

Remove lombok from camel-milvius

### Improvement (45)

[CAMEL-22807](https://issues.apache.org/jira/browse/CAMEL-22807)

camel-cluster - Add bean metadata for tooling

[CAMEL-22800](https://issues.apache.org/jira/browse/CAMEL-22800)

camel-jbang - Sort list of commands A..Z

[CAMEL-22796](https://issues.apache.org/jira/browse/CAMEL-22796)

camel-platform-http-vertx - VertX has hardcoded content-type validation

[CAMEL-22791](https://issues.apache.org/jira/browse/CAMEL-22791)

Camel-docling: Move docling-serve to docling-java

[CAMEL-22785](https://issues.apache.org/jira/browse/CAMEL-22785)

The master customer does not start the consumers asynchronously.

[CAMEL-22783](https://issues.apache.org/jira/browse/CAMEL-22783)

camel-xslt - Add option to set xpathTotalOpLimit

[CAMEL-22782](https://issues.apache.org/jira/browse/CAMEL-22782)

camel-salesforce: Modernize integration test setup with Salesforce CLI

[CAMEL-22775](https://issues.apache.org/jira/browse/CAMEL-22775)

camel-bean - Avoid caching Exchange bean

[CAMEL-22770](https://issues.apache.org/jira/browse/CAMEL-22770)

camel-sql - Stored producer should lookup named parameters like regular producer do

[CAMEL-22768](https://issues.apache.org/jira/browse/CAMEL-22768)

camel-http: useSystemProperties property defined at component level is ignored

[CAMEL-22765](https://issues.apache.org/jira/browse/CAMEL-22765)

camel-jbang - Pick Maven repositories configured to search for Camel JBang plugin

[CAMEL-22763](https://issues.apache.org/jira/browse/CAMEL-22763)

Support of exchange variables in XPath

[CAMEL-22761](https://issues.apache.org/jira/browse/CAMEL-22761)

camel-jbang - Pick Maven repositories provided on Camel JBang for actions related to Kamelet

[CAMEL-22748](https://issues.apache.org/jira/browse/CAMEL-22748)

camel-jbang - camel debug to do remote attach to existing running Camel

[CAMEL-22744](https://issues.apache.org/jira/browse/CAMEL-22744)

camel-core - Transform EIP is expression based but can ignore it

[CAMEL-22742](https://issues.apache.org/jira/browse/CAMEL-22742)

camel-core - Rest DSL contract first should have jmx statistics

[CAMEL-22740](https://issues.apache.org/jira/browse/CAMEL-22740)

camel-smb - Simplify SMB file move operation to use atomic rename instead of copy-then-delete strategy

[CAMEL-22739](https://issues.apache.org/jira/browse/CAMEL-22739)

camel-main: Avoid potential duplicate route resources in DefaultRoutesCollector.findRouteResourcesFromDirectory

[CAMEL-22737](https://issues.apache.org/jira/browse/CAMEL-22737)

camel-as2: MimeEntity::parseEntityBody causes NPE for unsupported mime types

[CAMEL-22736](https://issues.apache.org/jira/browse/CAMEL-22736)

camel-jbang - Allow to run with dynamic assigned management port

[CAMEL-22734](https://issues.apache.org/jira/browse/CAMEL-22734)

camel-jbang - Add both repo/repos and prop/property as option names

[CAMEL-22732](https://issues.apache.org/jira/browse/CAMEL-22732)

camel-jbang - Add DTO classes to represent json output

[CAMEL-22731](https://issues.apache.org/jira/browse/CAMEL-22731)

Enhance routeTemplate documentation for null values and not operator

[CAMEL-22727](https://issues.apache.org/jira/browse/CAMEL-22727)

Several aws region are missing for AWS Bedrock

[CAMEL-22725](https://issues.apache.org/jira/browse/CAMEL-22725)

camel-core - Backlog tracer for Aggregate EIP should have first|last markers

[CAMEL-22719](https://issues.apache.org/jira/browse/CAMEL-22719)

camel-neo4j - Improve detection of message body

[CAMEL-22715](https://issues.apache.org/jira/browse/CAMEL-22715)

camel-jbang - Receive command to be able to load properties

[CAMEL-22712](https://issues.apache.org/jira/browse/CAMEL-22712)

Add UNICODE -> UTF-8 to MllpProtocolConstants.MSH18\_VALUES and also values

[CAMEL-22705](https://issues.apache.org/jira/browse/CAMEL-22705)

Camel-Nats: Reuse existing stream for consumers

[CAMEL-22703](https://issues.apache.org/jira/browse/CAMEL-22703)

camel-jbang - history to have it mode to show message data like debugger

[CAMEL-22702](https://issues.apache.org/jira/browse/CAMEL-22702)

Add structured output option for Camel JBang cmd receive

[CAMEL-22689](https://issues.apache.org/jira/browse/CAMEL-22689)

camel-http - Add nonProxyHosts option to exclude hosts/domains from proxy

[CAMEL-22688](https://issues.apache.org/jira/browse/CAMEL-22688)

Add support for Client Secret Credentials in Azure Identity authentication for camel-azure-storage-blob component

[CAMEL-22686](https://issues.apache.org/jira/browse/CAMEL-22686)

Add GenericFile case to camel-docling

[CAMEL-22685](https://issues.apache.org/jira/browse/CAMEL-22685)

camel-jbang - Use --repos as the option name

[CAMEL-22684](https://issues.apache.org/jira/browse/CAMEL-22684)

camel-jbang - The doc command should filter headers when using filter

[CAMEL-22682](https://issues.apache.org/jira/browse/CAMEL-22682)

camel-jbang - Make load command able to detect existing source

[CAMEL-22671](https://issues.apache.org/jira/browse/CAMEL-22671)

camel-jbang - Refer to third party JAR versions from camel-dependencies POM

[CAMEL-22670](https://issues.apache.org/jira/browse/CAMEL-22670)

camel-jbang - Running CXF should automatic include needed JARs to run out of the box

[CAMEL-22629](https://issues.apache.org/jira/browse/CAMEL-22629)

camel-console - Add producer dev console

[CAMEL-22408](https://issues.apache.org/jira/browse/CAMEL-22408)

OpenAPI Description showing wrong allowable dates depending on system timezone

[CAMEL-22353](https://issues.apache.org/jira/browse/CAMEL-22353)

Undertow "null header error" on response if there is an invalid character in the request header name

[CAMEL-22272](https://issues.apache.org/jira/browse/CAMEL-22272)

camel-jbang - Make it easier to export and have hawtio ready to use

[CAMEL-20455](https://issues.apache.org/jira/browse/CAMEL-20455)

camel-jbang - Kamelets should be downloaded by Camel instead of jbang

[CAMEL-12941](https://issues.apache.org/jira/browse/CAMEL-12941)

camel-bindy - Null as default value for string

### New Feature (41)

[CAMEL-22803](https://issues.apache.org/jira/browse/CAMEL-22803)

Camel-Keycloak: Add EvaluatePermission operation

[CAMEL-22793](https://issues.apache.org/jira/browse/CAMEL-22793)

Camel-Langchain4j-Agent: Provide pre-defined guardrails for input/output

[CAMEL-22786](https://issues.apache.org/jira/browse/CAMEL-22786)

Camel-AWS: Extract common logic for clients instantiation in a separated module

[CAMEL-22778](https://issues.apache.org/jira/browse/CAMEL-22778)

Camel-Google-VertexAI: Create Spring Boot starter

[CAMEL-22777](https://issues.apache.org/jira/browse/CAMEL-22777)

Camel-Google: Add a VertexAI component

[CAMEL-22773](https://issues.apache.org/jira/browse/CAMEL-22773)

Camel AWS S3 Vectors: Add Spring Boot Starter

[CAMEL-22756](https://issues.apache.org/jira/browse/CAMEL-22756)

Create a Camel Stripe Starter for Spring Boot

[CAMEL-22755](https://issues.apache.org/jira/browse/CAMEL-22755)

Create a Camel Stripe component

[CAMEL-22747](https://issues.apache.org/jira/browse/CAMEL-22747)

camel-test-main-junit6 - JUnit 6 module for main test

[CAMEL-22746](https://issues.apache.org/jira/browse/CAMEL-22746)

camel-test-spring-junit6 - JUnit 6 module for spring test

[CAMEL-22724](https://issues.apache.org/jira/browse/CAMEL-22724)

Camel-Keycloak: Enhance component with configurable token source priority and binding validation

[CAMEL-22722](https://issues.apache.org/jira/browse/CAMEL-22722)

Camel-Shiro: Improve Authentication Error logging

[CAMEL-22713](https://issues.apache.org/jira/browse/CAMEL-22713)

Camel-IBM-Secrets-Manager: Add more producer operations

[CAMEL-22711](https://issues.apache.org/jira/browse/CAMEL-22711)

Spring AI integration components for Apache Camel (Chat, Embeddings, Tools, Vector Store)

[CAMEL-22710](https://issues.apache.org/jira/browse/CAMEL-22710)

Camel-IBM: Add Speech To Text Starter for CSB

[CAMEL-22709](https://issues.apache.org/jira/browse/CAMEL-22709)

Camel-IBM: Add Speech To Text component

[CAMEL-22708](https://issues.apache.org/jira/browse/CAMEL-22708)

Camel-IBM: Add Watson text-to-speech starter for CSB

[CAMEL-22706](https://issues.apache.org/jira/browse/CAMEL-22706)

Camel-IBM: Add Watson text-to-speech component

[CAMEL-22694](https://issues.apache.org/jira/browse/CAMEL-22694)

Camel-Spring-Boot: Create Azure Eventgrid starter

[CAMEL-22693](https://issues.apache.org/jira/browse/CAMEL-22693)

camel-core - Mark up EIP and component header that are more widespread in use for tooling assistance

[CAMEL-22690](https://issues.apache.org/jira/browse/CAMEL-22690)

Camel-AWS-Bedrock: Support Guardrails

[CAMEL-22687](https://issues.apache.org/jira/browse/CAMEL-22687)

camel-jbang - Always trace last message

[CAMEL-22678](https://issues.apache.org/jira/browse/CAMEL-22678)

camel-jbang - Add a dirty command

[CAMEL-22677](https://issues.apache.org/jira/browse/CAMEL-22677)

Camel-Hashicorp-Vault starter: Support Secret Refresh

[CAMEL-22676](https://issues.apache.org/jira/browse/CAMEL-22676)

Camel-Hashicorp-Vault: Support Secret Refresh

[CAMEL-22674](https://issues.apache.org/jira/browse/CAMEL-22674)

Camel-Keycloak: Support Bulk Operations

[CAMEL-22665](https://issues.apache.org/jira/browse/CAMEL-22665)

Camel-Cyberark-Vault: Support more producer operation

[CAMEL-22664](https://issues.apache.org/jira/browse/CAMEL-22664)

Camel-Cyberark-vault Spring Boot: Support Properties function in Spring Boot

[CAMEL-22663](https://issues.apache.org/jira/browse/CAMEL-22663)

Camel-Cyberark-vault: Create SB starter

[CAMEL-22661](https://issues.apache.org/jira/browse/CAMEL-22661)

Create a native OpenAI component

[CAMEL-22655](https://issues.apache.org/jira/browse/CAMEL-22655)

Create a Camel-Cyberark Conjur Vault component

[CAMEL-22654](https://issues.apache.org/jira/browse/CAMEL-22654)

camel-jbang - Add command for loading and adding new routes from source files

[CAMEL-22644](https://issues.apache.org/jira/browse/CAMEL-22644)

camel-jbang-kubernetes: add support to generate a CronJob instead a Deployment

[CAMEL-22637](https://issues.apache.org/jira/browse/CAMEL-22637)

camel-sql - Allow to specify DataSource dynamic in producer

[CAMEL-22431](https://issues.apache.org/jira/browse/CAMEL-22431)

camel-once - A component for development to trigger only once

[CAMEL-22249](https://issues.apache.org/jira/browse/CAMEL-22249)

Create a Camel AWS S3 Vectors component

[CAMEL-22222](https://issues.apache.org/jira/browse/CAMEL-22222)

camel-iggy - Add component for Apache Iggy

[CAMEL-22000](https://issues.apache.org/jira/browse/CAMEL-22000)

Expose mTLS headers for camel-mllp

[CAMEL-20919](https://issues.apache.org/jira/browse/CAMEL-20919)

Introduce Producer based Health for any SFTPs

[CAMEL-20552](https://issues.apache.org/jira/browse/CAMEL-20552)

Create an Azure Event Grid component

[CAMEL-16866](https://issues.apache.org/jira/browse/CAMEL-16866)

camel-opentelemetry - Add metrics support

### Sub-task (1)

[CAMEL-22806](https://issues.apache.org/jira/browse/CAMEL-22806)

Camel-AWS components: Avoid duplicated code and add pagination to producer operation where it makes sense - AWS IAM

### Task (20)

[CAMEL-22799](https://issues.apache.org/jira/browse/CAMEL-22799)

camel-route-parser - Remove camell-cdi parsing

[CAMEL-22781](https://issues.apache.org/jira/browse/CAMEL-22781)

camel-spring-boot - Virtual threads test is failing

[CAMEL-22771](https://issues.apache.org/jira/browse/CAMEL-22771)

camel-jbang - camel-test-infra uses old 4.8.3 jbang for testing

[CAMEL-22764](https://issues.apache.org/jira/browse/CAMEL-22764)

OAuth doc should be probably placed in Others (not components)

[CAMEL-22728](https://issues.apache.org/jira/browse/CAMEL-22728)

Create a new module for junit 6 (camel-test-junit6)

[CAMEL-22669](https://issues.apache.org/jira/browse/CAMEL-22669)

Documentation issue on user-manual/security and CyberArk Vault component link

[CAMEL-22662](https://issues.apache.org/jira/browse/CAMEL-22662)

docs: camel-cxf - add info on http transport dependency

[CAMEL-22652](https://issues.apache.org/jira/browse/CAMEL-22652)

Camel-PQC: misses pqc-dataformat.adoc

[CAMEL-22649](https://issues.apache.org/jira/browse/CAMEL-22649)

Camel-IBM: Add Group label to IBM Secrets Manager otherwise is not present in summary

[CAMEL-22647](https://issues.apache.org/jira/browse/CAMEL-22647)

\[build\] Enhance parent pom properties detector

[CAMEL-22641](https://issues.apache.org/jira/browse/CAMEL-22641)

jsonpath / XML DSL example code should not use headerName attribute

[CAMEL-22633](https://issues.apache.org/jira/browse/CAMEL-22633)

\[camel-robot-framework\] \[ WARN \] Command line option --xunitskipnoncritical has been deprecated and has no effect.

[CAMEL-22631](https://issues.apache.org/jira/browse/CAMEL-22631)

camel-aws - Deprecate camel-aws-xray

[CAMEL-22591](https://issues.apache.org/jira/browse/CAMEL-22591)

\[build\] SLF4J(W): No SLF4J providers were found.

[CAMEL-22585](https://issues.apache.org/jira/browse/CAMEL-22585)

Reactivate JMS component tests on JDK 25

[CAMEL-22584](https://issues.apache.org/jira/browse/CAMEL-22584)

\[build\] Review native calls

[CAMEL-22550](https://issues.apache.org/jira/browse/CAMEL-22550)

\[build\] Generated class is missing @Generated

[CAMEL-22460](https://issues.apache.org/jira/browse/CAMEL-22460)

documentation: Non-existent SPIs referenced in documentation

[CAMEL-22243](https://issues.apache.org/jira/browse/CAMEL-22243)

camel-jbang - Add documentation about camel launcher

[CAMEL-20809](https://issues.apache.org/jira/browse/CAMEL-20809)

camel-core: potential to reduce allocations

### Test (5)

[CAMEL-22779](https://issues.apache.org/jira/browse/CAMEL-22779)

All tests related to Iggy are failing

[CAMEL-22766](https://issues.apache.org/jira/browse/CAMEL-22766)

Fix issue related to failing test LangChain4jEmbeddingsComponentQdrantTargetIT.rag\_similarity\_search

[CAMEL-22650](https://issues.apache.org/jira/browse/CAMEL-22650)

camel-jbang - Kubernetes export test are failing

[CAMEL-22182](https://issues.apache.org/jira/browse/CAMEL-22182)

Fix issue related to falky test IssueWithWrongEncodingTest.testOkEncoding()

[CAMEL-22109](https://issues.apache.org/jira/browse/CAMEL-22109)

Fix issue related to flaky test MinaUdpNoCamelTest.testMinaUDPWithNoCamel

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).