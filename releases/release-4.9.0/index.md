# Apache camel 4.9.0 Release

## New and Noteworthy

This release is the new Camel 4.9.0 release.

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
      <version>4.9.0</version>
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
      <version>4.9.0</version>
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
| [apache-camel-4.9.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-src.zip.sha512) |
| [apache-camel-4.9.0-sbom.xml](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.xml.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.xml.sha512) |
| [apache-camel-4.9.0-sbom.json](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.json.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/4.9.0/apache-camel-4.9.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.9.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.9.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (72)

[CAMEL-21493](https://issues.apache.org/jira/browse/CAMEL-21493)

camel-ref: should use CamelContext.hasEndpoint but not CamelContext.getEndpoint to check existence of an endpoint

[CAMEL-21488](https://issues.apache.org/jira/browse/CAMEL-21488)

camel-jbang - Export with multiple customer kamelets

[CAMEL-21487](https://issues.apache.org/jira/browse/CAMEL-21487)

camel-jbang - Should be able to load route template files

[CAMEL-21471](https://issues.apache.org/jira/browse/CAMEL-21471)

camel-quartz ignores ignoreExpiredNextFireTime when endAt is expired

[CAMEL-21467](https://issues.apache.org/jira/browse/CAMEL-21467)

Simple expressions execute forever. Thread is RUNNABLE for ever. Issue appears with bean expressions inside simple expressions on SimpleLRUCache

[CAMEL-21460](https://issues.apache.org/jira/browse/CAMEL-21460)

\[camel-opentelemetry\] Cannot run with Camel Springboot runtime

[CAMEL-21446](https://issues.apache.org/jira/browse/CAMEL-21446)

configmap/secret - default takes precedence

[CAMEL-21444](https://issues.apache.org/jira/browse/CAMEL-21444)

camel-jbang - catalog using since-after can do NPE if version is single digit

[CAMEL-21436](https://issues.apache.org/jira/browse/CAMEL-21436)

camel-jbang - Export beans with secret function should work even if k8s is not configured

[CAMEL-21435](https://issues.apache.org/jira/browse/CAMEL-21435)

Commons-pool2: When Camel Netty configured with producerPoolMaxTotal=1 and retry, the application hangs

[CAMEL-21432](https://issues.apache.org/jira/browse/CAMEL-21432)

multicast function executes for ever. Thread is RUNNABLE for ever. Issue appears with multicast operating on SimpleLRUCache

[CAMEL-21430](https://issues.apache.org/jira/browse/CAMEL-21430)

camel-rest-openapi - Generated produces string is missing media types

[CAMEL-21423](https://issues.apache.org/jira/browse/CAMEL-21423)

camel-crypto - It is not possible to use "inline" with "AES/GCM/NoPadding"

[CAMEL-21420](https://issues.apache.org/jira/browse/CAMEL-21420)

camel-yaml-io - YAML model serializer is not serializing XPath expression namespaces

[CAMEL-21419](https://issues.apache.org/jira/browse/CAMEL-21419)

Camel Spring Boot v. 4.8.1: Multiple Task Executor Beans Detected

[CAMEL-21407](https://issues.apache.org/jira/browse/CAMEL-21407)

camel-dynamic-router component: unsubscribe by control message does not work

[CAMEL-21406](https://issues.apache.org/jira/browse/CAMEL-21406)

camel-sql - RowMapperFactory should be configurable to refer a bean by id

[CAMEL-21404](https://issues.apache.org/jira/browse/CAMEL-21404)

camel-jbang - Skip files without extension when using --source-dir

[CAMEL-21403](https://issues.apache.org/jira/browse/CAMEL-21403)

AS2 Component - Incorrect message length calculation when generating MIC for EDI messages with multi-byte characters

[CAMEL-21401](https://issues.apache.org/jira/browse/CAMEL-21401)

camel-core - Custom bean in DSL using factory method should avoid ClassCastException

[CAMEL-21399](https://issues.apache.org/jira/browse/CAMEL-21399)

Kubernetes plugin regression. Fails on OCP deployments

[CAMEL-21397](https://issues.apache.org/jira/browse/CAMEL-21397)

camel-file: autoCreateStepwise not working in Windows

[CAMEL-21386](https://issues.apache.org/jira/browse/CAMEL-21386)

camel k8s run --dev does not work on openshift

[CAMEL-21382](https://issues.apache.org/jira/browse/CAMEL-21382)

camel-core - Tracing with headers that are Map type can cause ClassCastException when dumping as XML

[CAMEL-21381](https://issues.apache.org/jira/browse/CAMEL-21381)

camel k8s cannot run spring-boot on openshift

[CAMEL-21379](https://issues.apache.org/jira/browse/CAMEL-21379)

camel-salesforce: introduce delay in pub/sub reconnect attempts

[CAMEL-21376](https://issues.apache.org/jira/browse/CAMEL-21376)

UseOriginalAggregationStrategy - null pointer

[CAMEL-21374](https://issues.apache.org/jira/browse/CAMEL-21374)

camel-jbang - Export pipe with local kamelets seems to fail

[CAMEL-21372](https://issues.apache.org/jira/browse/CAMEL-21372)

Camel JBang Export/Run are not working based on external camel-version setting

[CAMEL-21363](https://issues.apache.org/jira/browse/CAMEL-21363)

camel-whatsapp - Serialization error in MessageResponse when the Message object returns "message\_status" from the endpoint.

[CAMEL-21362](https://issues.apache.org/jira/browse/CAMEL-21362)

camel k8s run cannot find pod on openshift

[CAMEL-21361](https://issues.apache.org/jira/browse/CAMEL-21361)

fabric8 kubernetes-client fails to connect to openshift

[CAMEL-21355](https://issues.apache.org/jira/browse/CAMEL-21355)

LangChain4j Tools fails with direct LLM response

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

[CAMEL-21302](https://issues.apache.org/jira/browse/CAMEL-21302)

camel-opentelemetry context leak with direct async producer

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

[CAMEL-21285](https://issues.apache.org/jira/browse/CAMEL-21285)

\[camel-jbang\] Error exporting from different directory

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

[CAMEL-21215](https://issues.apache.org/jira/browse/CAMEL-21215)

camel-jbang: unreliable export to Quarkus without lazy binding

[CAMEL-21211](https://issues.apache.org/jira/browse/CAMEL-21211)

camel-azure-servicebus - Default header filter strategy can try to propagate headers of types not supported by the Service Bus protocol

[CAMEL-21210](https://issues.apache.org/jira/browse/CAMEL-21210)

camel-jbang - Optimized backlog tracer may miss information about which endpoint sent to

[CAMEL-21209](https://issues.apache.org/jira/browse/CAMEL-21209)

camel-langchain4j-tools: incorrect metadata prevents usage for tooling

[CAMEL-21199](https://issues.apache.org/jira/browse/CAMEL-21199)

Camel-jackson not properly marshalling 4-byte characters

[CAMEL-21188](https://issues.apache.org/jira/browse/CAMEL-21188)

No EndpointBuilder for camel-activemq6

[CAMEL-21133](https://issues.apache.org/jira/browse/CAMEL-21133)

camel-jbang: export a project using langchain4j-chat does not compile

### Dependency upgrade (13)

[CAMEL-21470](https://issues.apache.org/jira/browse/CAMEL-21470)

camel-datasonnet - Upgrade to 3.0.0

[CAMEL-21455](https://issues.apache.org/jira/browse/CAMEL-21455)

camel-beanio - Upgrade to 3.2.0

[CAMEL-21447](https://issues.apache.org/jira/browse/CAMEL-21447)

camel-spring-boot - Upgrade to 3.4.0

[CAMEL-21393](https://issues.apache.org/jira/browse/CAMEL-21393)

Upgrade to Jackson 2.18.1

[CAMEL-21367](https://issues.apache.org/jira/browse/CAMEL-21367)

camel-smooks - Upgrade to 2.0.1

[CAMEL-21366](https://issues.apache.org/jira/browse/CAMEL-21366)

camel-spring-boot - Upgrade to 3.3.5

[CAMEL-21344](https://issues.apache.org/jira/browse/CAMEL-21344)

Update OpenTelemetry dependencies to use out of the box thread-pool functionality

[CAMEL-21312](https://issues.apache.org/jira/browse/CAMEL-21312)

camel-debezium - Upgrade to 3.0

[CAMEL-21310](https://issues.apache.org/jira/browse/CAMEL-21310)

camel-jackson - Upgrade to 2.18

[CAMEL-21232](https://issues.apache.org/jira/browse/CAMEL-21232)

camel-http - Upgrade to 5.3 causes test failures

[CAMEL-21231](https://issues.apache.org/jira/browse/CAMEL-21231)

camel-jq - The JQ library is not as active maintaned

[CAMEL-21229](https://issues.apache.org/jira/browse/CAMEL-21229)

camel-spring-boot - Upgrade to 3.3.4

[CAMEL-20593](https://issues.apache.org/jira/browse/CAMEL-20593)

camel-kafka - Use official ASF docker images instead of confluent

### Improvement (94)

[CAMEL-21492](https://issues.apache.org/jira/browse/CAMEL-21492)

Doc: it would be nice to have a list of components usable for payload security

[CAMEL-21489](https://issues.apache.org/jira/browse/CAMEL-21489)

camel-micrometer - Make it possible to skip routes

[CAMEL-21482](https://issues.apache.org/jira/browse/CAMEL-21482)

camel-jaxb - JaxbDataFormat ignoreJAXBElement is default true

[CAMEL-21481](https://issues.apache.org/jira/browse/CAMEL-21481)

camel-jbang - Capture reload error when doing route reloads

[CAMEL-21477](https://issues.apache.org/jira/browse/CAMEL-21477)

Camel-Google-Storage: Add prefix option to consumer

[CAMEL-21475](https://issues.apache.org/jira/browse/CAMEL-21475)

camel-yaml-dsl - Using route templates with hardcoded ids problem

[CAMEL-21474](https://issues.apache.org/jira/browse/CAMEL-21474)

Camel-SMBProducer is never disconnecting

[CAMEL-21462](https://issues.apache.org/jira/browse/CAMEL-21462)

\[camel-observability-services\] Include more components

[CAMEL-21459](https://issues.apache.org/jira/browse/CAMEL-21459)

camel-jbang - Version list to include old releases

[CAMEL-21454](https://issues.apache.org/jira/browse/CAMEL-21454)

camel-main - Do not trigger JVM shutdown hook if already shutting down

[CAMEL-21445](https://issues.apache.org/jira/browse/CAMEL-21445)

camel-core - Vault with secret refresh should be disabled as default

[CAMEL-21434](https://issues.apache.org/jira/browse/CAMEL-21434)

camel-kamelet-main: decouple from Camel JBang

[CAMEL-21431](https://issues.apache.org/jira/browse/CAMEL-21431)

camel-jbang - camel export using dot instead of star

[CAMEL-21427](https://issues.apache.org/jira/browse/CAMEL-21427)

camel-xml-io - XML model serializer is serializing default values

[CAMEL-21422](https://issues.apache.org/jira/browse/CAMEL-21422)

CPU Load sometimes returns empty String

[CAMEL-21421](https://issues.apache.org/jira/browse/CAMEL-21421)

Move assertj version to parent

[CAMEL-21415](https://issues.apache.org/jira/browse/CAMEL-21415)

\[camel-micrometer-prometheus\] Make endpoint metrics configurable

[CAMEL-21414](https://issues.apache.org/jira/browse/CAMEL-21414)

\[camel-micrometer-prometheus\] Make endpoint metrics configurable

[CAMEL-21412](https://issues.apache.org/jira/browse/CAMEL-21412)

camel-test - Make it easy to use expression outside route builder

[CAMEL-21411](https://issues.apache.org/jira/browse/CAMEL-21411)

camel-openapi-rest - Should default load specification from classpath

[CAMEL-21402](https://issues.apache.org/jira/browse/CAMEL-21402)

Enhance Camel's testing capabilities of MockEndpoint with Expressions

[CAMEL-21387](https://issues.apache.org/jira/browse/CAMEL-21387)

Let's add some default dependencies to camel-opentelemetry-starter

[CAMEL-21384](https://issues.apache.org/jira/browse/CAMEL-21384)

\[camel-micrometer\] Analyse the possibility to harmonize the metrics endpoint

[CAMEL-21383](https://issues.apache.org/jira/browse/CAMEL-21383)

Add OIDC support for Knative Http client

[CAMEL-21380](https://issues.apache.org/jira/browse/CAMEL-21380)

camel-salesforce: pub/sub: add ability to opt out of proxy

[CAMEL-21378](https://issues.apache.org/jira/browse/CAMEL-21378)

Enable camel-opentelemetry-starter by default

[CAMEL-21377](https://issues.apache.org/jira/browse/CAMEL-21377)

camel-jbang - Add default values to --help

[CAMEL-21375](https://issues.apache.org/jira/browse/CAMEL-21375)

Camel-AWS-Secrets-Manager: Support Properties Function with Localstack in Spring Boot

[CAMEL-21373](https://issues.apache.org/jira/browse/CAMEL-21373)

Camel-AWS-Secrets-Manager: Delete operation add an header for forcing the deletion

[CAMEL-21371](https://issues.apache.org/jira/browse/CAMEL-21371)

camel-core - Add converter for Reader to InputStream

[CAMEL-21369](https://issues.apache.org/jira/browse/CAMEL-21369)

camel-jbang - Kubernetes plugin - Use quarkus extensions for Route trait

[CAMEL-21358](https://issues.apache.org/jira/browse/CAMEL-21358)

Add Knative Http client SSL support

[CAMEL-21357](https://issues.apache.org/jira/browse/CAMEL-21357)

camel-jq: Add ability to resolve the root scope from the registry

[CAMEL-21353](https://issues.apache.org/jira/browse/CAMEL-21353)

camel-core - Add possibility to set some condition for Camel to wait during startup before continuing

[CAMEL-21351](https://issues.apache.org/jira/browse/CAMEL-21351)

camel-core - AllowAllHeaderFilterStrategy

[CAMEL-21349](https://issues.apache.org/jira/browse/CAMEL-21349)

Add support for camel spring-boot on OpenShift

[CAMEL-21348](https://issues.apache.org/jira/browse/CAMEL-21348)

camel-spring-boot-examples : add an example how to use jolokia-starter

[CAMEL-21347](https://issues.apache.org/jira/browse/CAMEL-21347)

camel-aws - Head bucket should have option to return true|false instead of throwing exception

[CAMEL-21342](https://issues.apache.org/jira/browse/CAMEL-21342)

camel-kamelet-main - openapi generator should be optional and downloaded dynamically

[CAMEL-21336](https://issues.apache.org/jira/browse/CAMEL-21336)

camel-kamelet - Allow Kamelets configured by EnvVars only

[CAMEL-21335](https://issues.apache.org/jira/browse/CAMEL-21335)

camel-jbang - Command to start route should log start summary

[CAMEL-21333](https://issues.apache.org/jira/browse/CAMEL-21333)

camel-core - RemoveHeaders should default to remove all

[CAMEL-21331](https://issues.apache.org/jira/browse/CAMEL-21331)

camel-jbang - Kubernetes run/export - Remove trait-profile option

[CAMEL-21326](https://issues.apache.org/jira/browse/CAMEL-21326)

camel-jbang - Kubernetes run --verbose

[CAMEL-21322](https://issues.apache.org/jira/browse/CAMEL-21322)

camel-core - CamelRestartRouteEvent as event for supervised controller restarting a route

[CAMEL-21321](https://issues.apache.org/jira/browse/CAMEL-21321)

camel-main - Allow configuring long ENV names using more human readable

[CAMEL-21320](https://issues.apache.org/jira/browse/CAMEL-21320)

camel-main - Configuring camel.server should allow ENV variables

[CAMEL-21315](https://issues.apache.org/jira/browse/CAMEL-21315)

Throw an exception or add a warning when multiple ToDefinitions are defined in Rest DSL

[CAMEL-21311](https://issues.apache.org/jira/browse/CAMEL-21311)

NATS: Automatically added nats:// prefix in servers-parameter blocks the usage of NATS' built-in Websocket support

[CAMEL-21309](https://issues.apache.org/jira/browse/CAMEL-21309)

camel-cxf - When Exchange is using otel then run synchronous to avoid leaking spans

[CAMEL-21307](https://issues.apache.org/jira/browse/CAMEL-21307)

camel-smb: should provide the file name via header

[CAMEL-21304](https://issues.apache.org/jira/browse/CAMEL-21304)

Avoid "Invalid AnsiLogger Stream -> Swapping to default sdt out logger." with Camel JBang kubernetes run

[CAMEL-21303](https://issues.apache.org/jira/browse/CAMEL-21303)

camel-core - Tone down logging noise for IOHelper close

[CAMEL-21300](https://issues.apache.org/jira/browse/CAMEL-21300)

camel-platform-http - Consumer should have option to control if writing response failing should cause Exchange to fail

[CAMEL-21298](https://issues.apache.org/jira/browse/CAMEL-21298)

camel-jbang - VersionList to output in json

[CAMEL-21294](https://issues.apache.org/jira/browse/CAMEL-21294)

\[Camel JBang\] Run/Export hardcoded platform-http

[CAMEL-21292](https://issues.apache.org/jira/browse/CAMEL-21292)

camel-jbang - Export to quarkus should map JARs to quarkiverse JARs

[CAMEL-21286](https://issues.apache.org/jira/browse/CAMEL-21286)

Add a cache to JAXB object factories on JAXB Marshalling/Fallback converter

[CAMEL-21282](https://issues.apache.org/jira/browse/CAMEL-21282)

camel-file: allow creating folders one by one

[CAMEL-21279](https://issues.apache.org/jira/browse/CAMEL-21279)

camel-jbang - Export using custom kamelets should not add not needed kamelet JARs

[CAMEL-21277](https://issues.apache.org/jira/browse/CAMEL-21277)

camel-smb: should use WrappedFile for consistency

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

[CAMEL-21259](https://issues.apache.org/jira/browse/CAMEL-21259)

\[Camel JBang\] Missing dockerfile in springboot and main runtime

[CAMEL-21258](https://issues.apache.org/jira/browse/CAMEL-21258)

camel-core - Add SPI for before/afterExecute on Camel thread pools

[CAMEL-21255](https://issues.apache.org/jira/browse/CAMEL-21255)

camel-core - Add listener for creating ThreadFactory in ExecutorServiceManager

[CAMEL-21253](https://issues.apache.org/jira/browse/CAMEL-21253)

Camel AWS Kinesis: KCL Consumers, make the ConfigsBuilder for metrics of the Scheduler enable/disable

[CAMEL-21247](https://issues.apache.org/jira/browse/CAMEL-21247)

camel-core - CamelThreadFactory should create thread via newer JDK api

[CAMEL-21246](https://issues.apache.org/jira/browse/CAMEL-21246)

camel-jbang - Export should include console & management if dev console is enabled

[CAMEL-21241](https://issues.apache.org/jira/browse/CAMEL-21241)

camel-core - Properties dev console to capture actual values

[CAMEL-21237](https://issues.apache.org/jira/browse/CAMEL-21237)

Allow Endpoint DSL in Rest DSL 'to'

[CAMEL-21234](https://issues.apache.org/jira/browse/CAMEL-21234)

camel-core - Log EIP to use exchange formatter for ${exchange}

[CAMEL-21224](https://issues.apache.org/jira/browse/CAMEL-21224)

camel-jbang - Total counter should have option to show total as remote only

[CAMEL-21221](https://issues.apache.org/jira/browse/CAMEL-21221)

camel-jms - Should default filter out Camel headers like other components

[CAMEL-21217](https://issues.apache.org/jira/browse/CAMEL-21217)

camel-rest-openapi consumer: request and response types

[CAMEL-21214](https://issues.apache.org/jira/browse/CAMEL-21214)

camel-core - BrowsableEndpoint - Optimize for a get size only

[CAMEL-21213](https://issues.apache.org/jira/browse/CAMEL-21213)

camel-groovy - Align variables to use same naming as simple

[CAMEL-21212](https://issues.apache.org/jira/browse/CAMEL-21212)

camel-groovy - Add log as a variable to make it easy to write to log in a script

[CAMEL-21201](https://issues.apache.org/jira/browse/CAMEL-21201)

camel-ftp - Enrich exception with FTP client error codes if failing to upload file

[CAMEL-21189](https://issues.apache.org/jira/browse/CAMEL-21189)

camel-jms: Add idleReceivesPerTaskLimit

[CAMEL-21183](https://issues.apache.org/jira/browse/CAMEL-21183)

camel-core - BrowseEndpoint should have limit parameter

[CAMEL-21174](https://issues.apache.org/jira/browse/CAMEL-21174)

camel-core - Allow to use groovy in the log EIP

[CAMEL-21152](https://issues.apache.org/jira/browse/CAMEL-21152)

Camel-Jbang Kubernetes Plugin: remove dependency to camel k

[CAMEL-21138](https://issues.apache.org/jira/browse/CAMEL-21138)

camel-jbang - Export should use lazy beans

[CAMEL-21128](https://issues.apache.org/jira/browse/CAMEL-21128)

camel-core - Add trust all certificate for easier TLS/SSL development

[CAMEL-21104](https://issues.apache.org/jira/browse/CAMEL-21104)

camel-jbang - Delete used files when creating a Camel project "in-place" with Camel JBang

[CAMEL-21085](https://issues.apache.org/jira/browse/CAMEL-21085)

camel-jbang - Init - Support providing absolute path for camel file creation using Camel JBang

[CAMEL-21068](https://issues.apache.org/jira/browse/CAMEL-21068)

Add support for \`camel kubernetes run\` for all runtimes

[CAMEL-21063](https://issues.apache.org/jira/browse/CAMEL-21063)

Provide health endpoint for k8s export main

[CAMEL-16209](https://issues.apache.org/jira/browse/CAMEL-16209)

aws kinesis: re-processing Kinesis records

[CAMEL-11780](https://issues.apache.org/jira/browse/CAMEL-11780)

camel-amqp - SSL Transport configuration

### New Feature (29)

[CAMEL-21443](https://issues.apache.org/jira/browse/CAMEL-21443)

Read-Eval-Print loop for Camel JBang

[CAMEL-21398](https://issues.apache.org/jira/browse/CAMEL-21398)

Smooks Data Format

[CAMEL-21396](https://issues.apache.org/jira/browse/CAMEL-21396)

Introduce a fury format

[CAMEL-21392](https://issues.apache.org/jira/browse/CAMEL-21392)

camel-jbang - Add support for --cluster-type=k3s

[CAMEL-21391](https://issues.apache.org/jira/browse/CAMEL-21391)

camel-core - Add configuring dataFormats into model DSL

[CAMEL-21389](https://issues.apache.org/jira/browse/CAMEL-21389)

camel-flowable - Add component for flowable

[CAMEL-21330](https://issues.apache.org/jira/browse/CAMEL-21330)

Camel-AWS-Secrets-Manager: Support Properties Function with Localstack

[CAMEL-21324](https://issues.apache.org/jira/browse/CAMEL-21324)

Camel-AWS-Secret-Manager: for context reloading on secret refresh we should check also UpdateSecret Event

[CAMEL-21323](https://issues.apache.org/jira/browse/CAMEL-21323)

Camel-AWS-Secrets-Manager: Add a PutSecretValue operation to producer

[CAMEL-21275](https://issues.apache.org/jira/browse/CAMEL-21275)

Camel-Clickup Spring Boot Starter

[CAMEL-21265](https://issues.apache.org/jira/browse/CAMEL-21265)

Create ApplicationEnvironmentPreparedEvent for Vault components

[CAMEL-21262](https://issues.apache.org/jira/browse/CAMEL-21262)

Camel-AWS2-S3: Explicitly add Producer operations HeadObject and HeadBucket

[CAMEL-21251](https://issues.apache.org/jira/browse/CAMEL-21251)

Camel-AWS2-S3: Support Conditional Reads on producer operations

[CAMEL-21249](https://issues.apache.org/jira/browse/CAMEL-21249)

Camel-Kamelets: Move Kamelets utils in Camel Kamelets component

[CAMEL-21248](https://issues.apache.org/jira/browse/CAMEL-21248)

Camel-Aws2-S3: Support Conditional Writes

[CAMEL-21244](https://issues.apache.org/jira/browse/CAMEL-21244)

camel-clickup component

[CAMEL-21242](https://issues.apache.org/jira/browse/CAMEL-21242)

camel-jolokia-starter - a new starter to easily expose Jolokia endpoint

[CAMEL-21226](https://issues.apache.org/jira/browse/CAMEL-21226)

camel-jasypt-starter: Support early properties' decryption on properties files

[CAMEL-21207](https://issues.apache.org/jira/browse/CAMEL-21207)

Camel-Opensearch: Provide a parameter to set HostNameVerifier on client

[CAMEL-21206](https://issues.apache.org/jira/browse/CAMEL-21206)

Camel-Google-Storage: Support prefix in ListObjects operation

[CAMEL-21202](https://issues.apache.org/jira/browse/CAMEL-21202)

Add a ThreadPoolFactory to propagate OpenTelemetry contexts

[CAMEL-21193](https://issues.apache.org/jira/browse/CAMEL-21193)

camel-jbang - Add receive command

[CAMEL-21186](https://issues.apache.org/jira/browse/CAMEL-21186)

AWS Secrets Manager: Support Batch Retrieval for Secrets

[CAMEL-21179](https://issues.apache.org/jira/browse/CAMEL-21179)

Secret Properties Functions: Supporting secret name containing "/"

[CAMEL-21166](https://issues.apache.org/jira/browse/CAMEL-21166)

Kubernetes Configmaps: Trigger context reloading on update

[CAMEL-21018](https://issues.apache.org/jira/browse/CAMEL-21018)

Add a component for PyTorch TorchServe

[CAMEL-20968](https://issues.apache.org/jira/browse/CAMEL-20968)

camel-langchain4j: Add RAG option

[CAMEL-20503](https://issues.apache.org/jira/browse/CAMEL-20503)

camel-http OAuth2 support for caching / refreshing tokens

[CAMEL-6070](https://issues.apache.org/jira/browse/CAMEL-6070)

camel-test - Add annotations to configure test class instead of using methods

### Sub-task (2)

[CAMEL-21458](https://issues.apache.org/jira/browse/CAMEL-21458)

Kubernetes Configmaps: Trigger context reloading on update - Documentation

[CAMEL-21360](https://issues.apache.org/jira/browse/CAMEL-21360)

Camel Spring Boot: Vault early resolving properties documentation

### Task (24)

[CAMEL-21485](https://issues.apache.org/jira/browse/CAMEL-21485)

camel-spring-boot - The dynamic-router-eip example is failing

[CAMEL-21483](https://issues.apache.org/jira/browse/CAMEL-21483)

Camel-upgrade-recipes: cover upgrading camel 4.8 to 4.9

[CAMEL-21464](https://issues.apache.org/jira/browse/CAMEL-21464)

camel k8s run ... may lead to exec format error

[CAMEL-21453](https://issues.apache.org/jira/browse/CAMEL-21453)

Camel-Spring-Boot: Kubernetes Configmaps Trigger context reloading on update

[CAMEL-21448](https://issues.apache.org/jira/browse/CAMEL-21448)

camel-etcd3: deprecate component etcd3

[CAMEL-21410](https://issues.apache.org/jira/browse/CAMEL-21410)

Replace usage of STRICT\_VALIDATOR with UTF\_VALIDATOR

[CAMEL-21395](https://issues.apache.org/jira/browse/CAMEL-21395)

camel-debezium - Avoid split packages

[CAMEL-21343](https://issues.apache.org/jira/browse/CAMEL-21343)

No longer possible to recreate camel-vm

[CAMEL-21338](https://issues.apache.org/jira/browse/CAMEL-21338)

camel-jbang - Running java route seems to be slow at resolving java-dsl

[CAMEL-21334](https://issues.apache.org/jira/browse/CAMEL-21334)

Camel-opensearch - Provide ppc64le arch support

[CAMEL-21272](https://issues.apache.org/jira/browse/CAMEL-21272)

Move jbang camel-k plugin to camel-k git repo

[CAMEL-21252](https://issues.apache.org/jira/browse/CAMEL-21252)

Add checking for non .\*-versions to sync-properties-maven-plugin

[CAMEL-21236](https://issues.apache.org/jira/browse/CAMEL-21236)

Explicitly enable/disable quarkus image push

[CAMEL-21205](https://issues.apache.org/jira/browse/CAMEL-21205)

Remove Groovy DSL

[CAMEL-21204](https://issues.apache.org/jira/browse/CAMEL-21204)

Remove JavaScript DSL

[CAMEL-21203](https://issues.apache.org/jira/browse/CAMEL-21203)

Remove JavaShell DSL

[CAMEL-21131](https://issues.apache.org/jira/browse/CAMEL-21131)

Camel-upgrade-recipes: 4.0 recipe does ignore one of its sub-recipes

[CAMEL-21127](https://issues.apache.org/jira/browse/CAMEL-21127)

Migrate from Deprecated o.a.maven.plugins.annotations.Component

[CAMEL-20923](https://issues.apache.org/jira/browse/CAMEL-20923)

camel-jbang: Camel JBang is unable to load langchain4j embeddings

[CAMEL-20888](https://issues.apache.org/jira/browse/CAMEL-20888)

Remove Kotlin DSL and API

[CAMEL-20837](https://issues.apache.org/jira/browse/CAMEL-20837)

camel-test: implement extensions for CamelTestSupport

[CAMEL-20138](https://issues.apache.org/jira/browse/CAMEL-20138)

Avoid time out during dependabot Check Update job

[CAMEL-19767](https://issues.apache.org/jira/browse/CAMEL-19767)

camel-core: test should not catch AssertionError

[CAMEL-19538](https://issues.apache.org/jira/browse/CAMEL-19538)

camel-mllp: replace Thread.sleep in tests

### Test (5)

[CAMEL-21439](https://issues.apache.org/jira/browse/CAMEL-21439)

camel-etcd3: all tests are broken

[CAMEL-21417](https://issues.apache.org/jira/browse/CAMEL-21417)

Broken tests in various components

[CAMEL-21332](https://issues.apache.org/jira/browse/CAMEL-21332)

Smpp tests broken on main branch

[CAMEL-21297](https://issues.apache.org/jira/browse/CAMEL-21297)

camel-test-infra-dispatch-router not working due to SEGFAULT in running qdrouterd

[CAMEL-21195](https://issues.apache.org/jira/browse/CAMEL-21195)

tests: resolve flaky tests

### Wish (1)

[CAMEL-21158](https://issues.apache.org/jira/browse/CAMEL-21158)

Add exception as variable to expression languages

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).