# Apache camel 4.16.0 Release

## New and Noteworthy

This release is the new Camel 4.16.0 release.

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
      <version>4.16.0</version>
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
      <version>4.16.0</version>
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
| [apache-camel-4.16.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-src.zip.sha512) |
| [apache-camel-4.16.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.xml.sha512) |
| [apache-camel-4.16.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.16.0/apache-camel-4.16.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.16.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.16.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (23)

[CAMEL-22645](https://issues.apache.org/jira/browse/CAMEL-22645)

http-component - oauth2BodyAuthentication not being stipped out of URI

[CAMEL-22638](https://issues.apache.org/jira/browse/CAMEL-22638)

camel-jbang - Using jolokia should allow camel hawtio to connect

[CAMEL-22625](https://issues.apache.org/jira/browse/CAMEL-22625)

AvroDataFormat unmarshal fails for union with logicalType

[CAMEL-22612](https://issues.apache.org/jira/browse/CAMEL-22612)

camel-observation-starter + Spring Boot 3.5.7 fails to start

[CAMEL-22597](https://issues.apache.org/jira/browse/CAMEL-22597)

Jira possible error when using jira url ending with /

[CAMEL-22581](https://issues.apache.org/jira/browse/CAMEL-22581)

OAuth may validate token audience incorrectly

[CAMEL-22571](https://issues.apache.org/jira/browse/CAMEL-22571)

\[camel-beanio\] No type converter for encoding

[CAMEL-22565](https://issues.apache.org/jira/browse/CAMEL-22565)

camel-sql - DefaultSqlPrepareStatementStrategy is missing exchange in tryConverter

[CAMEL-22560](https://issues.apache.org/jira/browse/CAMEL-22560)

camel-telemetry - excludePatterns incorrectly prevents execution of excluded steps

[CAMEL-22558](https://issues.apache.org/jira/browse/CAMEL-22558)

Jira - Consumer ignores delay option

[CAMEL-22557](https://issues.apache.org/jira/browse/CAMEL-22557)

camel-as2 - Server-side DecryptingPrivateKey Conflict: Key from first route started is enforced for all subsequent routes on the same serverPortNumber

[CAMEL-22536](https://issues.apache.org/jira/browse/CAMEL-22536)

camel-spring-boot - Seems to not support and run on JDK 17

[CAMEL-22535](https://issues.apache.org/jira/browse/CAMEL-22535)

camel-jbang-container: Missing version pinning breaks container images / Further improvements

[CAMEL-22534](https://issues.apache.org/jira/browse/CAMEL-22534)

JPA: fails if used with splitter (with parallelProcessing)

[CAMEL-22533](https://issues.apache.org/jira/browse/CAMEL-22533)

ConcurrentModificationException thrown in JMX-enabled application using Split EIP w/ shared UoW

[CAMEL-22526](https://issues.apache.org/jira/browse/CAMEL-22526)

camel-core - The dfdl dataformat is missing in model

[CAMEL-22494](https://issues.apache.org/jira/browse/CAMEL-22494)

camel-as2 - AS2 consumer URI remains active after route stop/removal

[CAMEL-22493](https://issues.apache.org/jira/browse/CAMEL-22493)

camel-rest-openapi: Potential NPE in OpenApiUtils.isArrayType

[CAMEL-22491](https://issues.apache.org/jira/browse/CAMEL-22491)

camel-plc4j - NPE exception when cannot connect to remote service

[CAMEL-22458](https://issues.apache.org/jira/browse/CAMEL-22458)

flatpack converter accesses invalid column names for header and trailer record value retrieval of fixed width files

[CAMEL-22415](https://issues.apache.org/jira/browse/CAMEL-22415)

camel-http Changes Content-type while Building StringEntity

[CAMEL-22332](https://issues.apache.org/jira/browse/CAMEL-22332)

Salesforce API Calls Hang During PushTopic Event Processing

[CAMEL-21368](https://issues.apache.org/jira/browse/CAMEL-21368)

Regression in Camel JBang fails when generating REST routes from OpenAPI spec

### Dependency upgrade (8)

[CAMEL-22683](https://issues.apache.org/jira/browse/CAMEL-22683)

camel-jbang - Upgrade dist to 4.16.0

[CAMEL-22595](https://issues.apache.org/jira/browse/CAMEL-22595)

camel-spring-boot - Upgrade to 3.5.7

[CAMEL-22569](https://issues.apache.org/jira/browse/CAMEL-22569)

upgrade to jolokia 2.4.0

[CAMEL-22563](https://issues.apache.org/jira/browse/CAMEL-22563)

camel-spring - Upgrade to spring 6.2.12

[CAMEL-22559](https://issues.apache.org/jira/browse/CAMEL-22559)

camel-twilio - Upgrade to twilio 11

[CAMEL-22530](https://issues.apache.org/jira/browse/CAMEL-22530)

camel-redis - Upgrade to v7

[CAMEL-22492](https://issues.apache.org/jira/browse/CAMEL-22492)

camel-neo4j - Upgrade to neo 6

[CAMEL-22086](https://issues.apache.org/jira/browse/CAMEL-22086)

Reinstate camel-milo as milo has reached 1.0.0

### Improvement (29)

[CAMEL-22634](https://issues.apache.org/jira/browse/CAMEL-22634)

camel-console - Add uri for processors

[CAMEL-22628](https://issues.apache.org/jira/browse/CAMEL-22628)

camel-console - Add information to route dev console if route is created by template/kamelet

[CAMEL-22626](https://issues.apache.org/jira/browse/CAMEL-22626)

camel-console - Include all source lines for a given EIP in the dev consoles

[CAMEL-22623](https://issues.apache.org/jira/browse/CAMEL-22623)

Regression: CamelNettySSLClientCertSubjectName changed from readable string representation to obscure RFC2253 format

[CAMEL-22621](https://issues.apache.org/jira/browse/CAMEL-22621)

camel-yaml-dsl - YAML Schema default values for booleans

[CAMEL-22620](https://issues.apache.org/jira/browse/CAMEL-22620)

camel-core - JAXB data format - accessExternalSchemaProtocols should not have default value

[CAMEL-22615](https://issues.apache.org/jira/browse/CAMEL-22615)

camel-master - Add route policy to so routes dont have to be changed

[CAMEL-22611](https://issues.apache.org/jira/browse/CAMEL-22611)

SmbComponent: file move error if the user does not have "Full Control" permissions

[CAMEL-22608](https://issues.apache.org/jira/browse/CAMEL-22608)

camel-core - Using multiple validate EIP in Java DSL and end confusion

[CAMEL-22606](https://issues.apache.org/jira/browse/CAMEL-22606)

Camel-google-bigquery: Support stream list output type for SELECT queries

[CAMEL-22605](https://issues.apache.org/jira/browse/CAMEL-22605)

camel-jbang - Route dump to have actual source line numbers in dump

[CAMEL-22604](https://issues.apache.org/jira/browse/CAMEL-22604)

camel-jbang - Route dump in brief mode

[CAMEL-22603](https://issues.apache.org/jira/browse/CAMEL-22603)

camel-jbang - Add CSB/CEQ imports to known dependencies

[CAMEL-22596](https://issues.apache.org/jira/browse/CAMEL-22596)

camel-pqc - Add enum values for better tooling

[CAMEL-22566](https://issues.apache.org/jira/browse/CAMEL-22566)

camel-core - Backlog tracer should drain with higher capacity

[CAMEL-22564](https://issues.apache.org/jira/browse/CAMEL-22564)

camel-core - Using try converter should not record a miss

[CAMEL-22561](https://issues.apache.org/jira/browse/CAMEL-22561)

camel-graphql - Add support for sending custom headers

[CAMEL-22546](https://issues.apache.org/jira/browse/CAMEL-22546)

camel-core - Rest DSL model should have enum for dataformat choices

[CAMEL-22543](https://issues.apache.org/jira/browse/CAMEL-22543)

Camel-Keycloak: Add more operations in identity provider and resources

[CAMEL-22542](https://issues.apache.org/jira/browse/CAMEL-22542)

camel-core - Add support for using jacksonXML for XML binding

[CAMEL-22521](https://issues.apache.org/jira/browse/CAMEL-22521)

camel-jbang: Allow overriding quarkus gav using system properties

[CAMEL-22516](https://issues.apache.org/jira/browse/CAMEL-22516)

camel-core - RAW() should mask the value when printing

[CAMEL-22511](https://issues.apache.org/jira/browse/CAMEL-22511)

camel-kamelet - Secret options may not be auto RAW() substituted

[CAMEL-22507](https://issues.apache.org/jira/browse/CAMEL-22507)

camel-jbang - When using toD with dynamic parameters but static kamelet name then include kamelet spec file

[CAMEL-22500](https://issues.apache.org/jira/browse/CAMEL-22500)

camel-jms - Add option to use custom reply correlation ID selector for InOut

[CAMEL-22498](https://issues.apache.org/jira/browse/CAMEL-22498)

Camel-Keycloak: make requiredRoles and requiredPermissions comma separated string, it will make YAML life easier

[CAMEL-22496](https://issues.apache.org/jira/browse/CAMEL-22496)

camel-infinispan - Use the newer Query API instead of old deprecated

[CAMEL-22439](https://issues.apache.org/jira/browse/CAMEL-22439)

Camel-Nats: Support ConsumerConfiguration for NatsConsumer with Jetstream

[CAMEL-17348](https://issues.apache.org/jira/browse/CAMEL-17348)

camel-jira component newIssue does not work across multiple projects

### New Feature (23)

[CAMEL-22622](https://issues.apache.org/jira/browse/CAMEL-22622)

Camel-AWS-Bedrock: Support Converse API

[CAMEL-22619](https://issues.apache.org/jira/browse/CAMEL-22619)

Camel-Docling: Add Extract Metadata operation

[CAMEL-22617](https://issues.apache.org/jira/browse/CAMEL-22617)

Camel-AWS-Bedrock: Support Streaming mode while invoking models

[CAMEL-22614](https://issues.apache.org/jira/browse/CAMEL-22614)

Camel-IBM: Add Watson-Discovery Spring Boot Starter

[CAMEL-22613](https://issues.apache.org/jira/browse/CAMEL-22613)

Camel-IBM: Add Watson-Discovery Component

[CAMEL-22600](https://issues.apache.org/jira/browse/CAMEL-22600)

Camel-IBM-Cos: Create a Spring Boot starter for it

[CAMEL-22599](https://issues.apache.org/jira/browse/CAMEL-22599)

Camel-IBM Components: Create a middle folder like others

[CAMEL-22598](https://issues.apache.org/jira/browse/CAMEL-22598)

Camel-IBM-Cos: Add support for IBM Cloud Object Storage cloud service

[CAMEL-22592](https://issues.apache.org/jira/browse/CAMEL-22592)

Camel-Docling: Support Batch operations

[CAMEL-22586](https://issues.apache.org/jira/browse/CAMEL-22586)

Camel-PQC: Like Crypto support it as dataformat

[CAMEL-22582](https://issues.apache.org/jira/browse/CAMEL-22582)

Camel-Keycloak: Keycloak Introspector should provide different pluggable cache support

[CAMEL-22579](https://issues.apache.org/jira/browse/CAMEL-22579)

Camel-Docling: Support Connection Pooling

[CAMEL-22576](https://issues.apache.org/jira/browse/CAMEL-22576)

camel-core - Add note to EIP for code comments

[CAMEL-22575](https://issues.apache.org/jira/browse/CAMEL-22575)

Add OAuth 2.0 Token Introspection (RFC 7662) support to camel-keycloak component

[CAMEL-22567](https://issues.apache.org/jira/browse/CAMEL-22567)

Camel-Flink: Deprecate DataSet API in favor of DataStream API

[CAMEL-22547](https://issues.apache.org/jira/browse/CAMEL-22547)

Camel-Docling: Support Async operation in docling-server

[CAMEL-22509](https://issues.apache.org/jira/browse/CAMEL-22509)

Camel-docling: Add Authentication mechanism to docling-serve side

[CAMEL-22508](https://issues.apache.org/jira/browse/CAMEL-22508)

Camel-PQC: Add more KEM and Signature algorithms

[CAMEL-22505](https://issues.apache.org/jira/browse/CAMEL-22505)

Camel-Milo: Reintroduce starter for the component

[CAMEL-22503](https://issues.apache.org/jira/browse/CAMEL-22503)

Camel-Docling: Support Docling-serve and being able to invoke the service as API

[CAMEL-22495](https://issues.apache.org/jira/browse/CAMEL-22495)

Camel-aws2-s3: Add more bucket and object operations on the producer side

[CAMEL-22436](https://issues.apache.org/jira/browse/CAMEL-22436)

Camel-Docling: Add test-infra module for enabling tests on docling cli

[CAMEL-22302](https://issues.apache.org/jira/browse/CAMEL-22302)

camel-langchain4j-agent : add MCP Tool Pro

### Sub-task (2)

[CAMEL-22528](https://issues.apache.org/jira/browse/CAMEL-22528)

Camel-PQC: Add AWS Secrets Manager lifecycle manager

[CAMEL-22522](https://issues.apache.org/jira/browse/CAMEL-22522)

Camel-PQC: Add Hashicorp-vault lifecycle manager

### Task (18)

[CAMEL-22668](https://issues.apache.org/jira/browse/CAMEL-22668)

Camel migration guide link for 4.15 -> 4.16 shows older migration

[CAMEL-22643](https://issues.apache.org/jira/browse/CAMEL-22643)

docs: http-component - oauth2BodyAuthentication

[CAMEL-22630](https://issues.apache.org/jira/browse/CAMEL-22630)

camel-maven-plugin build is failing on main

[CAMEL-22610](https://issues.apache.org/jira/browse/CAMEL-22610)

Camel-IBM-Watson-language: Create a Spring Boot Starter

[CAMEL-22609](https://issues.apache.org/jira/browse/CAMEL-22609)

Camel-IBM-Watson-language: Create a component for NLU Service

[CAMEL-22607](https://issues.apache.org/jira/browse/CAMEL-22607)

\[build\] Clear DEBUG/TRACE/STDOUT traces

[CAMEL-22602](https://issues.apache.org/jira/browse/CAMEL-22602)

Camel-IBM-Cos: Add the spring-boot partials to adoc

[CAMEL-22589](https://issues.apache.org/jira/browse/CAMEL-22589)

Improve Jetty component documentation

[CAMEL-22552](https://issues.apache.org/jira/browse/CAMEL-22552)

\[build\] Substitute skipExec parameter

[CAMEL-22548](https://issues.apache.org/jira/browse/CAMEL-22548)

\[build\] annotation processor warning

[CAMEL-22541](https://issues.apache.org/jira/browse/CAMEL-22541)

\[camel-core\] Flaky FileLockClusteredRoutePolicyTest unit test

[CAMEL-22540](https://issues.apache.org/jira/browse/CAMEL-22540)

\[camel-lang4j\] Duplicated artifact declaration

[CAMEL-22532](https://issues.apache.org/jira/browse/CAMEL-22532)

\[camel-website\] Bring back procedure to delete old content

[CAMEL-22502](https://issues.apache.org/jira/browse/CAMEL-22502)

System.out|err.println code

[CAMEL-22501](https://issues.apache.org/jira/browse/CAMEL-22501)

Remove presence of main entrypoints

[CAMEL-22499](https://issues.apache.org/jira/browse/CAMEL-22499)

Add missing spring-boot-name in components documentation

[CAMEL-22478](https://issues.apache.org/jira/browse/CAMEL-22478)

\[camel-telemetry\] Introduce traceid/spanid exchange headers

[CAMEL-20875](https://issues.apache.org/jira/browse/CAMEL-20875)

Trigger component-test automatically on PR jobs

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).