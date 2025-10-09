# Apache camel 4.8.1 Release

## New and Noteworthy

This release is the new Camel 4.8.1 release.

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
      <version>4.8.1</version>
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
      <version>4.8.1</version>
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
| [apache-camel-4.8.1-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-src.zip.sha512) |
| [apache-camel-4.8.1-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.xml.sha512) |
| [apache-camel-4.8.1-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.8.1/apache-camel-4.8.1-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.8.1` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.8.1

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (36)

[CAMEL-21363](https://issues.apache.org/jira/browse/CAMEL-21363)

camel-whatsapp - Serialization error in MessageResponse when the Message object returns "message\_status" from the endpoint.

[CAMEL-21362](https://issues.apache.org/jira/browse/CAMEL-21362)

camel k8s run cannot find pod on openshift

[CAMEL-21345](https://issues.apache.org/jira/browse/CAMEL-21345)

Invalid manifest with jbang camel k8s --cluster-type openshift

[CAMEL-21340](https://issues.apache.org/jira/browse/CAMEL-21340)

camel-spring-boot - JSON validator object mapper and standalone tomcat

[CAMEL-21339](https://issues.apache.org/jira/browse/CAMEL-21339)

camel-rest - Client request validation and empty body

[CAMEL-21337](https://issues.apache.org/jira/browse/CAMEL-21337)

Camel-Jbang: Camel run with runtime=quarkus doesn't use group-id from config

[CAMEL-21329](https://issues.apache.org/jira/browse/CAMEL-21329)

camel-zipfile (and camel-tarfile) - Null body is not supported by ZipAggregationStrategy

[CAMEL-21328](https://issues.apache.org/jira/browse/CAMEL-21328)

Camel-AS2 signing MDN message with SHA1 and MD5 not sha-256

[CAMEL-21318](https://issues.apache.org/jira/browse/CAMEL-21318)

camel-platform-http-starter executed on multiple async threads

[CAMEL-21316](https://issues.apache.org/jira/browse/CAMEL-21316)

camel-jbang - Export with k8s secret does not include camel-kubernetes

[CAMEL-21306](https://issues.apache.org/jira/browse/CAMEL-21306)

camel-jsonpath - Null should be accepted return value

[CAMEL-21305](https://issues.apache.org/jira/browse/CAMEL-21305)

camel-pdf: type converter doesn't work with stream cache

[CAMEL-21301](https://issues.apache.org/jira/browse/CAMEL-21301)

\[camel-jbang\] Error when running openapi contract first with Q or SB

[CAMEL-21293](https://issues.apache.org/jira/browse/CAMEL-21293)

camel-core - Unmarshal processor should close InputStream after processing

[CAMEL-21291](https://issues.apache.org/jira/browse/CAMEL-21291)

Camel-smb: Producer requires "FileExist" parameter and "Exchange.FILE\_NAME" header to work

[CAMEL-21290](https://issues.apache.org/jira/browse/CAMEL-21290)

camel-jbang - Export activemq should include connection pool

[CAMEL-21289](https://issues.apache.org/jira/browse/CAMEL-21289)

camel-jbang - Export with --local-kamelet-dir

[CAMEL-21287](https://issues.apache.org/jira/browse/CAMEL-21287)

Camel-Azure-Files: missing header for AZURE\_IDENTITY

[CAMEL-21283](https://issues.apache.org/jira/browse/CAMEL-21283)

Regression: cannot use camel-version in combination of maven repositories in Camel Jbang cli

[CAMEL-21280](https://issues.apache.org/jira/browse/CAMEL-21280)

azure-files: Only CredentialType.SHARED\_ACCOUNT\_KEY is handled

[CAMEL-21271](https://issues.apache.org/jira/browse/CAMEL-21271)

camel-jbang - Export @PropertyInject should support ENV variables

[CAMEL-21269](https://issues.apache.org/jira/browse/CAMEL-21269)

camel-langchain4j-tokenizer: tokenizer are unusable in YAML

[CAMEL-21267](https://issues.apache.org/jira/browse/CAMEL-21267)

camel-jbang k8s delete command may not see k8s run dir

[CAMEL-21263](https://issues.apache.org/jira/browse/CAMEL-21263)

camel-smb: unable to read files after connection has closed

[CAMEL-21256](https://issues.apache.org/jira/browse/CAMEL-21256)

camel-github startingSha=last does not work with large history

[CAMEL-21243](https://issues.apache.org/jira/browse/CAMEL-21243)

camel-braintree-starter tries to use org.osgi:org.osgi.core:8.0.0

[CAMEL-21240](https://issues.apache.org/jira/browse/CAMEL-21240)

camel-jbang - Download does not work with --source-dir option

[CAMEL-21239](https://issues.apache.org/jira/browse/CAMEL-21239)

camel-report-maven-plugin - NPE if route does not have id

[CAMEL-21238](https://issues.apache.org/jira/browse/CAMEL-21238)

camel-jbang - k8s run - Reloading project does not change route behaviour

[CAMEL-21235](https://issues.apache.org/jira/browse/CAMEL-21235)

Cannot run k8s app in namespace other than default

[CAMEL-21227](https://issues.apache.org/jira/browse/CAMEL-21227)

camel k8s run ignores output format

[CAMEL-21219](https://issues.apache.org/jira/browse/CAMEL-21219)

camel-jms - Sending request/reply should not include temporary CamelJmsDeliveryMode header

[CAMEL-21216](https://issues.apache.org/jira/browse/CAMEL-21216)

Apache Camel LRA does not work with Oracle MicroTX LRA coordinator

[CAMEL-21211](https://issues.apache.org/jira/browse/CAMEL-21211)

camel-azure-servicebus - Default header filter strategy can try to propagate headers of types not supported by the Service Bus protocol

[CAMEL-21210](https://issues.apache.org/jira/browse/CAMEL-21210)

camel-jbang - Optimized backlog tracer may miss information about which endpoint sent to

[CAMEL-21209](https://issues.apache.org/jira/browse/CAMEL-21209)

camel-langchain4j-tools: incorrect metadata prevents usage for tooling

### Dependency upgrade (3)

[CAMEL-21344](https://issues.apache.org/jira/browse/CAMEL-21344)

Update OpenTelemetry dependencies to use out of the box thread-pool functionality

[CAMEL-21231](https://issues.apache.org/jira/browse/CAMEL-21231)

camel-jq - The JQ library is not as active maintaned

[CAMEL-21229](https://issues.apache.org/jira/browse/CAMEL-21229)

camel-spring-boot - Upgrade to 3.3.4

### Improvement (23)

[CAMEL-21357](https://issues.apache.org/jira/browse/CAMEL-21357)

camel-jq: Add ability to resolve the root scope from the registry

[CAMEL-21349](https://issues.apache.org/jira/browse/CAMEL-21349)

Add support for camel spring-boot on OpenShift

[CAMEL-21336](https://issues.apache.org/jira/browse/CAMEL-21336)

camel-kamelet - Allow Kamelets configured by EnvVars only

[CAMEL-21321](https://issues.apache.org/jira/browse/CAMEL-21321)

camel-main - Allow configuring long ENV names using more human readable

[CAMEL-21320](https://issues.apache.org/jira/browse/CAMEL-21320)

camel-main - Configuring camel.server should allow ENV variables

[CAMEL-21309](https://issues.apache.org/jira/browse/CAMEL-21309)

camel-cxf - When Exchange is using otel then run synchronous to avoid leaking spans

[CAMEL-21307](https://issues.apache.org/jira/browse/CAMEL-21307)

camel-smb: should provide the file name via header

[CAMEL-21303](https://issues.apache.org/jira/browse/CAMEL-21303)

camel-core - Tone down logging noise for IOHelper close

[CAMEL-21300](https://issues.apache.org/jira/browse/CAMEL-21300)

camel-platform-http - Consumer should have option to control if writing response failing should cause Exchange to fail

[CAMEL-21298](https://issues.apache.org/jira/browse/CAMEL-21298)

camel-jbang - VersionList to output in json

[CAMEL-21286](https://issues.apache.org/jira/browse/CAMEL-21286)

Add a cache to JAXB object factories on JAXB Marshalling/Fallback converter

[CAMEL-21282](https://issues.apache.org/jira/browse/CAMEL-21282)

camel-file: allow creating folders one by one

[CAMEL-21279](https://issues.apache.org/jira/browse/CAMEL-21279)

camel-jbang - Export using custom kamelets should not add not needed kamelet JARs

[CAMEL-21276](https://issues.apache.org/jira/browse/CAMEL-21276)

camel-kamelet - ENV variable name configuration - Can we support underscore for long names

[CAMEL-21273](https://issues.apache.org/jira/browse/CAMEL-21273)

camel-jbang can not run with the saga() dsl

[CAMEL-21264](https://issues.apache.org/jira/browse/CAMEL-21264)

camel-smb: should use avoid leaking implementation details

[CAMEL-21261](https://issues.apache.org/jira/browse/CAMEL-21261)

camel-opentelemetry does not use it's context propagators

[CAMEL-21260](https://issues.apache.org/jira/browse/CAMEL-21260)

camel-cxf - Allow to configure synchronous on component level

[CAMEL-21255](https://issues.apache.org/jira/browse/CAMEL-21255)

camel-core - Add listener for creating ThreadFactory in ExecutorServiceManager

[CAMEL-21253](https://issues.apache.org/jira/browse/CAMEL-21253)

Camel AWS Kinesis: KCL Consumers, make the ConfigsBuilder for metrics of the Scheduler enable/disable

[CAMEL-21246](https://issues.apache.org/jira/browse/CAMEL-21246)

camel-jbang - Export should include console & management if dev console is enabled

[CAMEL-21068](https://issues.apache.org/jira/browse/CAMEL-21068)

Add support for \`camel kubernetes run\` for all runtimes

[CAMEL-21063](https://issues.apache.org/jira/browse/CAMEL-21063)

Provide health endpoint for k8s export main

### New Feature (2)

[CAMEL-21242](https://issues.apache.org/jira/browse/CAMEL-21242)

camel-jolokia-starter - a new starter to easily expose Jolokia endpoint

[CAMEL-21202](https://issues.apache.org/jira/browse/CAMEL-21202)

Add a ThreadPoolFactory to propagate OpenTelemetry contexts

### Task (5)

[CAMEL-21343](https://issues.apache.org/jira/browse/CAMEL-21343)

No longer possible to recreate camel-vm

[CAMEL-21317](https://issues.apache.org/jira/browse/CAMEL-21317)

camel-jbang: Kubernetes plugin: Service exposure as Route/Ingress documentation

[CAMEL-21252](https://issues.apache.org/jira/browse/CAMEL-21252)

Add checking for non .\*-versions to sync-properties-maven-plugin

[CAMEL-21236](https://issues.apache.org/jira/browse/CAMEL-21236)

Explicitly enable/disable quarkus image push

[CAMEL-20923](https://issues.apache.org/jira/browse/CAMEL-20923)

camel-jbang: Camel JBang is unable to load langchain4j embeddings

### Test (1)

[CAMEL-21297](https://issues.apache.org/jira/browse/CAMEL-21297)

camel-test-infra-dispatch-router not working due to SEGFAULT in running qdrouterd

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).