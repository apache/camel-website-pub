# Apache camel 2.20.1 Release

## New and Noteworthy

This release is a minor update of the 2.20.x branch.

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
      <version>2.20.1</version>
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
      <version>2.20.1</version>
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
| [apache-camel-2.20.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.20.1/apache-camel-2.20.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.20.1/apache-camel-2.20.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.20.1/apache-camel-2.20.1-src.zip.sha1) |

## Git tag checkout

Release is tagged with `camel-2.20.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.20.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (43)

[CAMEL-12001](https://issues.apache.org/jira/browse/CAMEL-12001)

Cannot create a component based on the SqlComponent

[CAMEL-11999](https://issues.apache.org/jira/browse/CAMEL-11999)

Cannot create queue/message for Azure

[CAMEL-11992](https://issues.apache.org/jira/browse/CAMEL-11992)

connectors : alias scheme is not used by the connector component

[CAMEL-11988](https://issues.apache.org/jira/browse/CAMEL-11988)

camel-jetty - Problem with latest Spring Boot 1.5.8

[CAMEL-11986](https://issues.apache.org/jira/browse/CAMEL-11986)

HTTP4 Producer for TLS schemes transforms endpoint URI to \`http4s\`

[CAMEL-11983](https://issues.apache.org/jira/browse/CAMEL-11983)

XsltAggregationStrategy thread safety during initialization

[CAMEL-11980](https://issues.apache.org/jira/browse/CAMEL-11980)

PushTopic client doesn't clear refresh token after a long disconnected period

[CAMEL-11967](https://issues.apache.org/jira/browse/CAMEL-11967)

Restlet binding should not create jaxb marshaller when binding mode is set to json

[CAMEL-11963](https://issues.apache.org/jira/browse/CAMEL-11963)

camel-spring-boot - Actuator endpoints for MVC should only trigger if web application

[CAMEL-11962](https://issues.apache.org/jira/browse/CAMEL-11962)

AdviceWith weaveAddFirst using onCompletion issue

[CAMEL-11961](https://issues.apache.org/jira/browse/CAMEL-11961)

ClassCastException in HttpMessage

[CAMEL-11955](https://issues.apache.org/jira/browse/CAMEL-11955)

Using @AdviceWith and testing camel-spring-boot startup CamelContext eager

[CAMEL-11953](https://issues.apache.org/jira/browse/CAMEL-11953)

maven connector plugin: connector only properties are ignored in spring boot code generation

[CAMEL-11952](https://issues.apache.org/jira/browse/CAMEL-11952)

XSLT options not set when resource URI is http

[CAMEL-11951](https://issues.apache.org/jira/browse/CAMEL-11951)

Uri matching does not match request type

[CAMEL-11950](https://issues.apache.org/jira/browse/CAMEL-11950)

Inconsistent jar versions with apache curator

[CAMEL-11945](https://issues.apache.org/jira/browse/CAMEL-11945)

camel-spring-boot - CamelContextConfiguration afterApplicationStart should trigger later

[CAMEL-11939](https://issues.apache.org/jira/browse/CAMEL-11939)

asn1 dataformat is not part of xsd for global dataformat

[CAMEL-11938](https://issues.apache.org/jira/browse/CAMEL-11938)

Thrift data format is not part of the xsd for dataformats

[CAMEL-11937](https://issues.apache.org/jira/browse/CAMEL-11937)

Fix syntax for iec60870 component

[CAMEL-11936](https://issues.apache.org/jira/browse/CAMEL-11936)

Fix syntax for Atomix component

[CAMEL-11926](https://issues.apache.org/jira/browse/CAMEL-11926)

close JMXConnector on shutdown of JMXConsumer in camel-jmx

[CAMEL-11925](https://issues.apache.org/jira/browse/CAMEL-11925)

Atmos component fails to load atmos.properties in a modular class loading environment

[CAMEL-11922](https://issues.apache.org/jira/browse/CAMEL-11922)

Persistent tail tracking picks random tail tracker from mongoDB collection

[CAMEL-11920](https://issues.apache.org/jira/browse/CAMEL-11920)

camel-hdfs2 not working in osgi using documented HdfsOsgiHelper

[CAMEL-11917](https://issues.apache.org/jira/browse/CAMEL-11917)

camel-jgroups-starter : JGroupsLockClusterService auto configuration lacks enable flag

[CAMEL-11916](https://issues.apache.org/jira/browse/CAMEL-11916)

camel-jgroups-starter : JGroupsLockClusterServiceConfiguration lacks getter/setters

[CAMEL-11912](https://issues.apache.org/jira/browse/CAMEL-11912)

Camel Dropbox validator regex is too restrictive and fails for common paths

[CAMEL-11910](https://issues.apache.org/jira/browse/CAMEL-11910)

camel-maven-plugin - validate should not include route ids as consumer urls

[CAMEL-11909](https://issues.apache.org/jira/browse/CAMEL-11909)

camel-catalog-maven - Cannot load out of the box components

[CAMEL-11906](https://issues.apache.org/jira/browse/CAMEL-11906)

Missing compile scope dependencies in camel-pgevent

[CAMEL-11902](https://issues.apache.org/jira/browse/CAMEL-11902)

cluster-service : FileLockClusterView should not always return local member as leader

[CAMEL-11900](https://issues.apache.org/jira/browse/CAMEL-11900)

cluster-service : only the first event listener is notified about cluster events

[CAMEL-11898](https://issues.apache.org/jira/browse/CAMEL-11898)

camel-spring-ws - Attachments are lost

[CAMEL-11897](https://issues.apache.org/jira/browse/CAMEL-11897)

camel-kubernetes: cannot use the same cluster view to start a master route and a custom service

[CAMEL-11896](https://issues.apache.org/jira/browse/CAMEL-11896)

camel-spring-boot - set CamelLogDebugBodyMaxChars when 0 or negative

[CAMEL-11894](https://issues.apache.org/jira/browse/CAMEL-11894)

camel-karaf-commands deployment failed on karaf 4.0

[CAMEL-11892](https://issues.apache.org/jira/browse/CAMEL-11892)

SpringWebserviceConsumer and class cast exception

[CAMEL-11889](https://issues.apache.org/jira/browse/CAMEL-11889)

Kie assumes that the TCCL can load its services

[CAMEL-11628](https://issues.apache.org/jira/browse/CAMEL-11628)

MQTT Connection loop

[CAMEL-11387](https://issues.apache.org/jira/browse/CAMEL-11387)

SFTP is delivered into incorrect location, without exception (file in subfolder + temp file is created + Camel running on Window & SFTP server running on LINUX)

[CAMEL-11286](https://issues.apache.org/jira/browse/CAMEL-11286)

Imported Xquery modules will not resolve using classpath - Regression

[CAMEL-11045](https://issues.apache.org/jira/browse/CAMEL-11045)

onCompletion does not trigger on failure if split is in route

### Improvement (18)

[CAMEL-11997](https://issues.apache.org/jira/browse/CAMEL-11997)

camel-archetype-component - Should generate DefaultComponent

[CAMEL-11991](https://issues.apache.org/jira/browse/CAMEL-11991)

camel-swagger-java - Allow to specify type as date format

[CAMEL-11984](https://issues.apache.org/jira/browse/CAMEL-11984)

AggregationStrategy - Let EIPs support lifecycle of custom aggregation strategy to allow custom start/stop logic

[CAMEL-11979](https://issues.apache.org/jira/browse/CAMEL-11979)

camel-undertow - swagger api should match on uri prefix

[CAMEL-11978](https://issues.apache.org/jira/browse/CAMEL-11978)

camel-swagger-java - Include 200 status response as default in generated api-doc

[CAMEL-11975](https://issues.apache.org/jira/browse/CAMEL-11975)

camel-connector - Allow to set before/after consumer/producer processors per endpoint

[CAMEL-11960](https://issues.apache.org/jira/browse/CAMEL-11960)

camel-swagger-java - Generated swagger doc should use primitive types

[CAMEL-11958](https://issues.apache.org/jira/browse/CAMEL-11958)

rest-dsl - Disable vendor extension by default

[CAMEL-11957](https://issues.apache.org/jira/browse/CAMEL-11957)

rest-dsl - Allow to turn off vendor extension in generated api docs

[CAMEL-11948](https://issues.apache.org/jira/browse/CAMEL-11948)

NPE on DefaultMessage setBody if deprecated constructor was used

[CAMEL-11944](https://issues.apache.org/jira/browse/CAMEL-11944)

Ensure HBaseConfiguration ClassLoader is set correctly

[CAMEL-11932](https://issues.apache.org/jira/browse/CAMEL-11932)

For fixed length records crlf field is not honored during un-marshaling

[CAMEL-11929](https://issues.apache.org/jira/browse/CAMEL-11929)

camel-castor - Add more configuration

[CAMEL-11927](https://issues.apache.org/jira/browse/CAMEL-11927)

camel-spring-ws - Support for header transformation

[CAMEL-11904](https://issues.apache.org/jira/browse/CAMEL-11904)

Increase dependency java-util-version to min. 1.26.1

[CAMEL-11895](https://issues.apache.org/jira/browse/CAMEL-11895)

camel-hystrix - Expose state of circuit breaker on JMX / processor

[CAMEL-11891](https://issues.apache.org/jira/browse/CAMEL-11891)

XML2JSON Data Format and empty requests

[CAMEL-11890](https://issues.apache.org/jira/browse/CAMEL-11890)

camel-connector - Use JSon parser to parse the camel-connector-schema.json

### New Feature (1)

[CAMEL-11923](https://issues.apache.org/jira/browse/CAMEL-11923)

Camel-Hessian: Add Whitelisting feature

### Task (4)

[CAMEL-11993](https://issues.apache.org/jira/browse/CAMEL-11993)

Upgrade to CXF 3.2.1

[CAMEL-11965](https://issues.apache.org/jira/browse/CAMEL-11965)

camel BOM (and camel-hl7) lack the optional dependency to hapi-structures-v251

[CAMEL-11946](https://issues.apache.org/jira/browse/CAMEL-11946)

Invalid artifactId in docs for camel-json-validator

[CAMEL-11911](https://issues.apache.org/jira/browse/CAMEL-11911)

Setup CI server to build 2.20.x SNAPSHOT builds

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).