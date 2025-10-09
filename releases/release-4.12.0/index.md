# Apache camel 4.12.0 Release

## New and Noteworthy

This release is the new Camel 4.12.0 release.

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
      <version>4.12.0</version>
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
      <version>4.12.0</version>
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
| [apache-camel-4.12.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-src.zip.sha512) |
| [apache-camel-4.12.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.xml.sha512) |
| [apache-camel-4.12.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.12.0/apache-camel-4.12.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.12.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.12.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (55)

[CAMEL-22191](https://issues.apache.org/jira/browse/CAMEL-22191)

camel-resilience4j - The option recordExceptions is configured as ignored

[CAMEL-22103](https://issues.apache.org/jira/browse/CAMEL-22103)

camel-cxf: CXF RS Rest service with optional query parameter fails

[CAMEL-22100](https://issues.apache.org/jira/browse/CAMEL-22100)

camel-jbang - Transitive dependencies on plugins should use the parent artifact to manage versions

[CAMEL-22097](https://issues.apache.org/jira/browse/CAMEL-22097)

camel-observability-starter - Cannot change port 9876

[CAMEL-22095](https://issues.apache.org/jira/browse/CAMEL-22095)

camel-core - Rest DSL with inlined routes does not work with AdviceWith testing

[CAMEL-22092](https://issues.apache.org/jira/browse/CAMEL-22092)

\[camel-jbang\] Adding dependency camel:management duplicate the camel-observability-services in the pom.xml

[CAMEL-22082](https://issues.apache.org/jira/browse/CAMEL-22082)

camel-stream - NPE if charset is not specified

[CAMEL-22081](https://issues.apache.org/jira/browse/CAMEL-22081)

Http component oauth2ResourceIndicator not present

[CAMEL-22078](https://issues.apache.org/jira/browse/CAMEL-22078)

camel-jbang - Resolving DEPS may not work if using profile option

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

[CAMEL-22032](https://issues.apache.org/jira/browse/CAMEL-22032)

camel-jbang - Regression with k8s pod logs

[CAMEL-22028](https://issues.apache.org/jira/browse/CAMEL-22028)

camel-jbang - Regression with missing routes file

[CAMEL-22026](https://issues.apache.org/jira/browse/CAMEL-22026)

Camel SJMS & SJMS2 component cause thread leak when the route is stopped.

[CAMEL-22020](https://issues.apache.org/jira/browse/CAMEL-22020)

platform-http - Error in clientRequestValidation consumes & produces when plus sign in content-type

[CAMEL-22015](https://issues.apache.org/jira/browse/CAMEL-22015)

camel-jbang - Export with language component should resolve dependency

[CAMEL-22014](https://issues.apache.org/jira/browse/CAMEL-22014)

camel-jbang - Should be able to include groovy files on classpath

[CAMEL-22004](https://issues.apache.org/jira/browse/CAMEL-22004)

Kafka component shutdown may get stuck when rebalancing occurs

[CAMEL-21990](https://issues.apache.org/jira/browse/CAMEL-21990)

camel-jbang - Stop integration by name may not work

[CAMEL-21988](https://issues.apache.org/jira/browse/CAMEL-21988)

Missing @UriParam with entityManagerFactory in JpaEndpoint

[CAMEL-21987](https://issues.apache.org/jira/browse/CAMEL-21987)

camel-jbang - Run with --source-dir may not load content for static HTTP server

[CAMEL-21986](https://issues.apache.org/jira/browse/CAMEL-21986)

camel-oauth - spring-boot does not maintain post login url

[CAMEL-21983](https://issues.apache.org/jira/browse/CAMEL-21983)

camel-jbang - Export to quarkus produces an incorrect application.properties file when referring kamelet files

[CAMEL-21979](https://issues.apache.org/jira/browse/CAMEL-21979)

camel-core - DefaultSourceLoader fails to load sb route

[CAMEL-21978](https://issues.apache.org/jira/browse/CAMEL-21978)

camel-jbang - k8s examples should serve ingress cert

[CAMEL-21967](https://issues.apache.org/jira/browse/CAMEL-21967)

camel-jbang - Transform route to yaml with CBR cannot load into Karavan

[CAMEL-21964](https://issues.apache.org/jira/browse/CAMEL-21964)

camel-salesforce: bulk api 2.0 error responses fail to deserialize

[CAMEL-21963](https://issues.apache.org/jira/browse/CAMEL-21963)

camel-infinispan - query parameters not working

[CAMEL-21958](https://issues.apache.org/jira/browse/CAMEL-21958)

camel-core - Java DSL wrong "otherwise" is triggered when having nested choice

[CAMEL-21957](https://issues.apache.org/jira/browse/CAMEL-21957)

camel-core - Error handler should store failure route id eager so onRedelivery/onExceptionOccurred processors have access

[CAMEL-21956](https://issues.apache.org/jira/browse/CAMEL-21956)

camel-jbang - k8s plugin does not delete the ingress

[CAMEL-21954](https://issues.apache.org/jira/browse/CAMEL-21954)

camel-core - Route templates with onException does not work

[CAMEL-21953](https://issues.apache.org/jira/browse/CAMEL-21953)

camel-groovy: GroovyLanguage.stop may throw UnsupportedOperationException

[CAMEL-21947](https://issues.apache.org/jira/browse/CAMEL-21947)

GenericFileConsumer with eager idempotence and read lock stop processing file

[CAMEL-21942](https://issues.apache.org/jira/browse/CAMEL-21942)

camel-jbang - Export kamelet with custom bean should not create bean when being used as part of stubbing

[CAMEL-21940](https://issues.apache.org/jira/browse/CAMEL-21940)

camel-kafka - KafkaProducerCallBack can execute the continuation twice

[CAMEL-21938](https://issues.apache.org/jira/browse/CAMEL-21938)

camel-jolt - inputType & outputType can't be set for http uris

[CAMEL-21926](https://issues.apache.org/jira/browse/CAMEL-21926)

camel-attachment: inconsistent behaviour

[CAMEL-21923](https://issues.apache.org/jira/browse/CAMEL-21923)

camel-langchain4j-tools: LLM call should include all tools at the end of the flow

[CAMEL-21912](https://issues.apache.org/jira/browse/CAMEL-21912)

camel-cxf - Caching of ToStringTypeConverter breaks CXF RS Rest service

[CAMEL-21908](https://issues.apache.org/jira/browse/CAMEL-21908)

camel-jms - Property 'idleReceivesPerTaskLimit' is not populated to spring-jms

[CAMEL-21901](https://issues.apache.org/jira/browse/CAMEL-21901)

Salesforce consumer endpoint query parameter fallBackReplayId not working

[CAMEL-21899](https://issues.apache.org/jira/browse/CAMEL-21899)

camel-oauth - openshift does not maintain http session

[CAMEL-21897](https://issues.apache.org/jira/browse/CAMEL-21897)

camel-opentelemetry - Failed to capture tracing data

[CAMEL-21891](https://issues.apache.org/jira/browse/CAMEL-21891)

camel-ftp - Consumer and antInclude regression

[CAMEL-21816](https://issues.apache.org/jira/browse/CAMEL-21816)

camel-ai - Missing tool information when returning function call response

[CAMEL-21490](https://issues.apache.org/jira/browse/CAMEL-21490)

camel-jbang - Transform route to yaml with choice

### Dependency upgrade (16)

[CAMEL-22091](https://issues.apache.org/jira/browse/CAMEL-22091)

Rest-openapi: swagger-openapi3-version has to be upgraded with swagger-openapi3-java-parser-version

[CAMEL-22060](https://issues.apache.org/jira/browse/CAMEL-22060)

camel-micrometer - Upgrade to 1.5.0

[CAMEL-22058](https://issues.apache.org/jira/browse/CAMEL-22058)

camel-spring-boot - Upgrade to SB 3.5

[CAMEL-22052](https://issues.apache.org/jira/browse/CAMEL-22052)

Camel-opensearch: Upgrade to 3.x

[CAMEL-22036](https://issues.apache.org/jira/browse/CAMEL-22036)

camel-jackson-avro: Align avro version with Camel

[CAMEL-22035](https://issues.apache.org/jira/browse/CAMEL-22035)

camel-as2 - Upgrade to as2-lib 5.1.5

[CAMEL-22034](https://issues.apache.org/jira/browse/CAMEL-22034)

upgrade to bouncycastle 1.80

[CAMEL-22024](https://issues.apache.org/jira/browse/CAMEL-22024)

camel-jackson - Upgrade to 2.19.x

[CAMEL-22023](https://issues.apache.org/jira/browse/CAMEL-22023)

camel-debezium - Upgrade to 3.1.x

[CAMEL-22003](https://issues.apache.org/jira/browse/CAMEL-22003)

camel-spring-boot - Upgrade to 3.4.5

[CAMEL-21999](https://issues.apache.org/jira/browse/CAMEL-21999)

camel-netty - Downgrade to 4.1.x

[CAMEL-21980](https://issues.apache.org/jira/browse/CAMEL-21980)

camel-jbang - Transform route dump YAML in tooling friendly format

[CAMEL-21976](https://issues.apache.org/jira/browse/CAMEL-21976)

camel-elasticsearch - Upgrade to v9

[CAMEL-21951](https://issues.apache.org/jira/browse/CAMEL-21951)

Bump Pulsar to 4.x

[CAMEL-21914](https://issues.apache.org/jira/browse/CAMEL-21914)

camel-infinispan - Building CSB fails

[CAMEL-21815](https://issues.apache.org/jira/browse/CAMEL-21815)

camel-pulsar - Upgrade to 4

### Improvement (61)

[CAMEL-22087](https://issues.apache.org/jira/browse/CAMEL-22087)

\[JBang\] Unable to execute multithreading under different ports and process name

[CAMEL-22085](https://issues.apache.org/jira/browse/CAMEL-22085)

camel-jbang - Receive and Browse command should embed local Camel if no existing running

[CAMEL-22084](https://issues.apache.org/jira/browse/CAMEL-22084)

Camel-PQC: Support KeyStore and Alias for KeyPair for signing and verifying

[CAMEL-22079](https://issues.apache.org/jira/browse/CAMEL-22079)

camel-jbang - Allow modeline parsing for //DEPS

[CAMEL-22077](https://issues.apache.org/jira/browse/CAMEL-22077)

Provide syntax highlighting for came-jbang shell commands

[CAMEL-22076](https://issues.apache.org/jira/browse/CAMEL-22076)

camel-jbang - Do not show remote counters by default

[CAMEL-22075](https://issues.apache.org/jira/browse/CAMEL-22075)

camel-http - Add support for bearer authentication

[CAMEL-22074](https://issues.apache.org/jira/browse/CAMEL-22074)

camel-jbang - camel cmd send to be able to send to remote instance

[CAMEL-22069](https://issues.apache.org/jira/browse/CAMEL-22069)

camel-core-model - Transformer and Validator are not include correctly in model

[CAMEL-22061](https://issues.apache.org/jira/browse/CAMEL-22061)

camel-test-junit - Make it easy to include more than 1 route builder in Java

[CAMEL-22054](https://issues.apache.org/jira/browse/CAMEL-22054)

camel-jbang - Allow @Inject/@Produce bean methods to not be public

[CAMEL-22053](https://issues.apache.org/jira/browse/CAMEL-22053)

camel-jbang - Add support for @Inject on bean method that produces a bean

[CAMEL-22051](https://issues.apache.org/jira/browse/CAMEL-22051)

rest-dsl - Rest configuration context-path should be favoured as base-path instead of from spec file

[CAMEL-22049](https://issues.apache.org/jira/browse/CAMEL-22049)

camel-aws2-kinesis: use created async client for KCL consumer

[CAMEL-22048](https://issues.apache.org/jira/browse/CAMEL-22048)

camel-platform-http-main - HTTP summary align verbx

[CAMEL-22047](https://issues.apache.org/jira/browse/CAMEL-22047)

camel-jbang - Send command to allow including exchange properties and variables in response

[CAMEL-22045](https://issues.apache.org/jira/browse/CAMEL-22045)

camel-tracer - The legacy tracer should trace rests by default

[CAMEL-22044](https://issues.apache.org/jira/browse/CAMEL-22044)

camel-vertx-http - Make it easier to do file upload as Multipart-Form

[CAMEL-22043](https://issues.apache.org/jira/browse/CAMEL-22043)

camel-smb - Configure path in context-path to be more similar to other file based components

[CAMEL-22042](https://issues.apache.org/jira/browse/CAMEL-22042)

camel-http - Make it easier to do file upload as MultiPart-Form

[CAMEL-22033](https://issues.apache.org/jira/browse/CAMEL-22033)

camel-salesforce - For the Pub/Sub API, add the original ConsumerEvent as an exchange property

[CAMEL-22029](https://issues.apache.org/jira/browse/CAMEL-22029)

aws dynamodb scan and query not implemented with attributes-to-get

[CAMEL-22022](https://issues.apache.org/jira/browse/CAMEL-22022)

camel-jacksonxml - Transform from XML to JSon can we preserve order of elements

[CAMEL-22019](https://issues.apache.org/jira/browse/CAMEL-22019)

camel-smb - Add header for UNCPath for backwards compatability

[CAMEL-22018](https://issues.apache.org/jira/browse/CAMEL-22018)

camel-core - Exchange.getVariables should include message headers

[CAMEL-22017](https://issues.apache.org/jira/browse/CAMEL-22017)

\[camel-jbang\] Add management-port flag

[CAMEL-22016](https://issues.apache.org/jira/browse/CAMEL-22016)

Camel-PQC: Check if BC and BCPQC Bouncycastle Providers are installed before installing or removing

[CAMEL-22008](https://issues.apache.org/jira/browse/CAMEL-22008)

camel-sjms - Add option to set jmsMessageType to force a given type

[CAMEL-22007](https://issues.apache.org/jira/browse/CAMEL-22007)

camel-micrometer - Configuring tags is not tooling friendly

[CAMEL-22006](https://issues.apache.org/jira/browse/CAMEL-22006)

camel-jbang - Detect rest-openapi need rest producer component to function

[CAMEL-22005](https://issues.apache.org/jira/browse/CAMEL-22005)

Camel-PQC: Provide default for KEM and Signature/Verify even for non-standardized algorithms

[CAMEL-22001](https://issues.apache.org/jira/browse/CAMEL-22001)

camel-core - Kamelet and EIPs should propagate exchange variables

[CAMEL-21996](https://issues.apache.org/jira/browse/CAMEL-21996)

camel-jbang: use new Files java API instead of Input/Output Streams

[CAMEL-21991](https://issues.apache.org/jira/browse/CAMEL-21991)

camel-jpa - Make entityManagerFactory as an autowired option

[CAMEL-21989](https://issues.apache.org/jira/browse/CAMEL-21989)

camel-jpa - Lookup of EntityManagerFactory in component can be autowired

[CAMEL-21985](https://issues.apache.org/jira/browse/CAMEL-21985)

camel-jbang refactor the edit plugin's CamelNanoLspEditor class

[CAMEL-21982](https://issues.apache.org/jira/browse/CAMEL-21982)

camel-core - LW XML dumper should output inlined Java DSL expressions

[CAMEL-21981](https://issues.apache.org/jira/browse/CAMEL-21981)

camel-jbang: when running in shell mode, plugins cannot be used

[CAMEL-21971](https://issues.apache.org/jira/browse/CAMEL-21971)

camel-pqc - Provide default KeyPair and Signature

[CAMEL-21950](https://issues.apache.org/jira/browse/CAMEL-21950)

\[camel-observability-services\] Use a different port to expose the services

[CAMEL-21949](https://issues.apache.org/jira/browse/CAMEL-21949)

camel-core - Type converter with allowNull should be a valid response for ConvertBodyTo

[CAMEL-21948](https://issues.apache.org/jira/browse/CAMEL-21948)

camel-console - BeanDevConsole should ignore lazy bean that cannot be loaded

[CAMEL-21939](https://issues.apache.org/jira/browse/CAMEL-21939)

camel-jbang - Export to have --verbose option

[CAMEL-21934](https://issues.apache.org/jira/browse/CAMEL-21934)

Additional Information Needed in ContextHealthCheck message

[CAMEL-21931](https://issues.apache.org/jira/browse/CAMEL-21931)

Add bridgeEndponit option in camel-vertx-http producer

[CAMEL-21928](https://issues.apache.org/jira/browse/CAMEL-21928)

camel-jq - include variable() and body() as new functions to access in-process data

[CAMEL-21927](https://issues.apache.org/jira/browse/CAMEL-21927)

Camel Vault Properties Function: Harmonize error messages and cause

[CAMEL-21921](https://issues.apache.org/jira/browse/CAMEL-21921)

camel-jbang - using stop with name will terminate all integrations with same root

[CAMEL-21907](https://issues.apache.org/jira/browse/CAMEL-21907)

camel-http - Add oauth2 scope to request body

[CAMEL-21902](https://issues.apache.org/jira/browse/CAMEL-21902)

camel-core - Remove Camel v1 header prefix in header filter strategies

[CAMEL-21898](https://issues.apache.org/jira/browse/CAMEL-21898)

camel-jbang - camel kubernetes --quiet=false seems to be ignored

[CAMEL-21884](https://issues.apache.org/jira/browse/CAMEL-21884)

Introduce the useBodyHandler option in camel-platform-http

[CAMEL-21875](https://issues.apache.org/jira/browse/CAMEL-21875)

camel-as2 - Add config for Authentication Header

[CAMEL-21871](https://issues.apache.org/jira/browse/CAMEL-21871)

camel-azure-servicebus - default endpoint option credentialType overrides component option if it is set to something else than the default value

[CAMEL-21859](https://issues.apache.org/jira/browse/CAMEL-21859)

camel-xslt - Add source option to allow using header/variable as input instead of message body

[CAMEL-21857](https://issues.apache.org/jira/browse/CAMEL-21857)

camel-microprofile-fault-tolerance: Refactor component to avoid internal API usage

[CAMEL-21736](https://issues.apache.org/jira/browse/CAMEL-21736)

camel-google - Ability to fetch data from Google BigQuery tables

[CAMEL-21424](https://issues.apache.org/jira/browse/CAMEL-21424)

camel-jbang - Add --verbose to export output a lot more fine grained details of what is happening

[CAMEL-18392](https://issues.apache.org/jira/browse/CAMEL-18392)

camel-jt400 - UTF-8 improvement for data queues

[CAMEL-17025](https://issues.apache.org/jira/browse/CAMEL-17025)

camel-aws-s3 - Allow moveAfterRead in same bucket for AWS S3 consumer

[CAMEL-5576](https://issues.apache.org/jira/browse/CAMEL-5576)

create an XML and namespace without spring in it

### New Feature (23)

[CAMEL-22188](https://issues.apache.org/jira/browse/CAMEL-22188)

camel-jq to support variables

[CAMEL-22098](https://issues.apache.org/jira/browse/CAMEL-22098)

camel-jbang - camel dependency runtime

[CAMEL-22064](https://issues.apache.org/jira/browse/CAMEL-22064)

camel-xml-io - Generate XSD schema

[CAMEL-22010](https://issues.apache.org/jira/browse/CAMEL-22010)

Camel-PQC: Define an option to store result of extractSecretKeyFromEncapsulation as header or in body

[CAMEL-22002](https://issues.apache.org/jira/browse/CAMEL-22002)

Camel-PQC: Document Encapsulation/Decapsulation of Secret and show different algorithm

[CAMEL-21995](https://issues.apache.org/jira/browse/CAMEL-21995)

Camel-PQC: Add an extractSecretKeyFromEncapsulation producer operation

[CAMEL-21994](https://issues.apache.org/jira/browse/CAMEL-21994)

Camel-PQC: Add more Symmetric Algorithms

[CAMEL-21993](https://issues.apache.org/jira/browse/CAMEL-21993)

Camel-PQC - Provide default KeyGenerator for KEM operations

[CAMEL-21992](https://issues.apache.org/jira/browse/CAMEL-21992)

Camel-PQC: Support more KEM Algorithms

[CAMEL-21970](https://issues.apache.org/jira/browse/CAMEL-21970)

Create a Camel-PQC Spring Boot Starter

[CAMEL-21961](https://issues.apache.org/jira/browse/CAMEL-21961)

Create a Camel PQC component

[CAMEL-21945](https://issues.apache.org/jira/browse/CAMEL-21945)

camel-jbang add camel-lsp to Nano editor

[CAMEL-21944](https://issues.apache.org/jira/browse/CAMEL-21944)

camel-jbang - Classpath scan custom JARs for beans and processors with dependency injection annotations

[CAMEL-21943](https://issues.apache.org/jira/browse/CAMEL-21943)

Add a weaviate component

[CAMEL-21911](https://issues.apache.org/jira/browse/CAMEL-21911)

camel-bang: kubernetes add support for ingress class

[CAMEL-21905](https://issues.apache.org/jira/browse/CAMEL-21905)

Camel-IBM-Secrets-Manager: Implement secret refresh by using IBM Event Streams as destination of notifications

[CAMEL-21896](https://issues.apache.org/jira/browse/CAMEL-21896)

camel-jbang - Allow configuration preset per directory

[CAMEL-21801](https://issues.apache.org/jira/browse/CAMEL-21801)

spring-cloud-config - Vault for spring config server to lookup property values

[CAMEL-21760](https://issues.apache.org/jira/browse/CAMEL-21760)

camel-oauth - OpenID Connect & OAuth for Camel Kafka, Web and Rest

[CAMEL-21087](https://issues.apache.org/jira/browse/CAMEL-21087)

camel-jbang: Kubernetes plugin: Add jolokia trait

[CAMEL-17530](https://issues.apache.org/jira/browse/CAMEL-17530)

Support for Azure Lease Blob options in Camel component

[CAMEL-16360](https://issues.apache.org/jira/browse/CAMEL-16360)

Add Pulsar Support for Scheduled/Delayed MEssages

[CAMEL-15088](https://issues.apache.org/jira/browse/CAMEL-15088)

Create a dapr component

### Sub-task (1)

[CAMEL-21918](https://issues.apache.org/jira/browse/CAMEL-21918)

Camel-IBM-Secret-Manager: Document Refresh feature

### Task (27)

[CAMEL-22123](https://issues.apache.org/jira/browse/CAMEL-22123)

Camel-upgrade-recipes: cover upgrade of camel 4.11 to 4.12

[CAMEL-22101](https://issues.apache.org/jira/browse/CAMEL-22101)

camel-http - Remove Digest authMethod

[CAMEL-22088](https://issues.apache.org/jira/browse/CAMEL-22088)

Camel-HTTP: Document httpClient.\* possible values

[CAMEL-22071](https://issues.apache.org/jira/browse/CAMEL-22071)

camel-spring - Add missing docs to Spring XML XSD

[CAMEL-22063](https://issues.apache.org/jira/browse/CAMEL-22063)

camel-spring-boot-generator-maven-plugin: prioritize deprecated field from csb catalog

[CAMEL-22046](https://issues.apache.org/jira/browse/CAMEL-22046)

Add test-infra for pinecone

[CAMEL-22040](https://issues.apache.org/jira/browse/CAMEL-22040)

AWS-DDB: Support projection and filter expressions in scan and query operation

[CAMEL-22031](https://issues.apache.org/jira/browse/CAMEL-22031)

Camel-PQC: Document usage of secret key extraction from encapsulation

[CAMEL-22025](https://issues.apache.org/jira/browse/CAMEL-22025)

camel-platform-http-main - Add startup summary back

[CAMEL-22013](https://issues.apache.org/jira/browse/CAMEL-22013)

camel-api - Remove all usage of component.extension and the component.extension package content itself

[CAMEL-22012](https://issues.apache.org/jira/browse/CAMEL-22012)

Add test-infra for camel-weaviate

[CAMEL-21997](https://issues.apache.org/jira/browse/CAMEL-21997)

Fix camel-weaviate integration test

[CAMEL-21984](https://issues.apache.org/jira/browse/CAMEL-21984)

camel-smb File type is wrong in documentation

[CAMEL-21977](https://issues.apache.org/jira/browse/CAMEL-21977)

Remove CamelBeanMethodName constants

[CAMEL-21973](https://issues.apache.org/jira/browse/CAMEL-21973)

Add try with resources to reported errors in coverity

[CAMEL-21972](https://issues.apache.org/jira/browse/CAMEL-21972)

ComponentArtifactHelper.java add try with resources

[CAMEL-21969](https://issues.apache.org/jira/browse/CAMEL-21969)

Camel-PQC: Support KEM operations

[CAMEL-21968](https://issues.apache.org/jira/browse/CAMEL-21968)

Camel-PQC: Add Documentation and show algorithms

[CAMEL-21965](https://issues.apache.org/jira/browse/CAMEL-21965)

rest-dsl - Add docs about configuring base-path for OpenAPI

[CAMEL-21962](https://issues.apache.org/jira/browse/CAMEL-21962)

CSimpleTest is failing in camel-examples repository

[CAMEL-21941](https://issues.apache.org/jira/browse/CAMEL-21941)

Camel-Jbang: Upgrade to Camel-Kamelets 4.11.0

[CAMEL-21930](https://issues.apache.org/jira/browse/CAMEL-21930)

Camel-test-infra-aws: Move to Localstack v4

[CAMEL-21920](https://issues.apache.org/jira/browse/CAMEL-21920)

Camel-IBM-Secrets-Manager: Support Secret Refresh in Camel-Spring-Boot

[CAMEL-21910](https://issues.apache.org/jira/browse/CAMEL-21910)

\[Camel Spring Boot Examples\] Add Salesforce example

[CAMEL-21879](https://issues.apache.org/jira/browse/CAMEL-21879)

Run camel-oauth examples on openshift

[CAMEL-21878](https://issues.apache.org/jira/browse/CAMEL-21878)

Run camel-oauth examples on remote k8s cluster

[CAMEL-21573](https://issues.apache.org/jira/browse/CAMEL-21573)

camel-spring-boot - Deprecate camel-jetty-starter

### Test (2)

[CAMEL-21959](https://issues.apache.org/jira/browse/CAMEL-21959)

camel-knative - Cannot run CI tests due to SSL issue

[CAMEL-21952](https://issues.apache.org/jira/browse/CAMEL-21952)

camel-telegram - Test failures due to Port already in use

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).