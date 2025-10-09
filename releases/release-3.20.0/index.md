# Apache camel 3.20.0 Release

## New and Noteworthy

This release is the new Camel 3.20.0 LTS release.

## Supported Java version

This version supports Java 11 and 17.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>3.20.0</version>
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
      <version>3.20.0</version>
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
| [apache-camel-3.20.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/3.20.0/apache-camel-3.20.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/3.20.0/apache-camel-3.20.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/3.20.0/apache-camel-3.20.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-3.20.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-3.20.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (58)

[CAMEL-18811](https://issues.apache.org/jira/browse/CAMEL-18811)

camel-ldap - InvalidSearchFilterException: invalid attribute description

[CAMEL-18809](https://issues.apache.org/jira/browse/CAMEL-18809)

camel-core-model: RouteDefinitionHelper should resolve the intercepted from URI which is configured with property placeholder

[CAMEL-18807](https://issues.apache.org/jira/browse/CAMEL-18807)

camel-yaml-dsl - Using method call in filter EIP not working

[CAMEL-18805](https://issues.apache.org/jira/browse/CAMEL-18805)

Camel-telegram: bug while unregistreing webhook with autoregister=true

[CAMEL-18796](https://issues.apache.org/jira/browse/CAMEL-18796)

camel-kafka: kafka consumer stops in case of an authentication issue

[CAMEL-18795](https://issues.apache.org/jira/browse/CAMEL-18795)

camel-kafka: consumer not being closed during shutdown

[CAMEL-18782](https://issues.apache.org/jira/browse/CAMEL-18782)

Apache camel http component HTTP\_PATH header not working with toD

[CAMEL-18778](https://issues.apache.org/jira/browse/CAMEL-18778)

camel-jbang - Export to quarkus on windows generate wrong GAVs in pom.xml

[CAMEL-18776](https://issues.apache.org/jira/browse/CAMEL-18776)

camel-hdfs - Fix HdfsNormalFileHandler to handle temporary file path correctly

[CAMEL-18772](https://issues.apache.org/jira/browse/CAMEL-18772)

camel-jbang - Run from gist can lead to JMX ObjectName issue

[CAMEL-18766](https://issues.apache.org/jira/browse/CAMEL-18766)

camel-support: background tasks without maxDuration are reeschedulable

[CAMEL-18764](https://issues.apache.org/jira/browse/CAMEL-18764)

camel-core - templatedRoute builder from Java cannot use templates from other DSLs

[CAMEL-18755](https://issues.apache.org/jira/browse/CAMEL-18755)

camel-yaml-dsl - Intercept is not added in the route definition.

[CAMEL-18753](https://issues.apache.org/jira/browse/CAMEL-18753)

camel-yaml-dsl - OnCompletion is not added in the route definition.

[CAMEL-18750](https://issues.apache.org/jira/browse/CAMEL-18750)

camel-elastisearch-starter - Spring Boot clash with json-api dependency

[CAMEL-18739](https://issues.apache.org/jira/browse/CAMEL-18739)

ZipAggregationStrategy loses onCompletion

[CAMEL-18737](https://issues.apache.org/jira/browse/CAMEL-18737)

\[camel-kamelet\] parameter substitution does not work in bean instantiation when constructor or factory method is used

[CAMEL-18736](https://issues.apache.org/jira/browse/CAMEL-18736)

Duplicate schema/cxfEndpoint.xsd resource in camel-cxf-spring-rest and camel-cxf-spring-soap jars

[CAMEL-18733](https://issues.apache.org/jira/browse/CAMEL-18733)

camel-micrometer - Route policy should use unique names

[CAMEL-18730](https://issues.apache.org/jira/browse/CAMEL-18730)

camel-report-maven-plugin - Class missing when generating the route coverage report

[CAMEL-18728](https://issues.apache.org/jira/browse/CAMEL-18728)

Elasticsearch rest and Elasticsearch Java component name clash

[CAMEL-18722](https://issues.apache.org/jira/browse/CAMEL-18722)

Camel AWS2 S3 doesn't handle metadata correctly

[CAMEL-18719](https://issues.apache.org/jira/browse/CAMEL-18719)

camel-jbang - Adding the dependency of camel-quarkus-core creates two entries in exported POM.xml

[CAMEL-18717](https://issues.apache.org/jira/browse/CAMEL-18717)

camel-kafka: investigate offset not increasing

[CAMEL-18713](https://issues.apache.org/jira/browse/CAMEL-18713)

Loop processor interrupted when Camel engine shutdown

[CAMEL-18711](https://issues.apache.org/jira/browse/CAMEL-18711)

OpenAPI Schema references not generating correctly

[CAMEL-18704](https://issues.apache.org/jira/browse/CAMEL-18704)

components - Headers metadata is not included for components extending another component

[CAMEL-18703](https://issues.apache.org/jira/browse/CAMEL-18703)

camel-jbang - doc command with --header does not show headers

[CAMEL-18690](https://issues.apache.org/jira/browse/CAMEL-18690)

camel-jbang generates package name with special symbols

[CAMEL-18689](https://issues.apache.org/jira/browse/CAMEL-18689)

Context reload doesn't update properties when using EndpointDSL

[CAMEL-18688](https://issues.apache.org/jira/browse/CAMEL-18688)

camel-kafka: kafka component is not fully resumable

[CAMEL-18676](https://issues.apache.org/jira/browse/CAMEL-18676)

Camel-Jbang does not add camel-openapi-java component when required

[CAMEL-18661](https://issues.apache.org/jira/browse/CAMEL-18661)

Camel OpenTelemtery instrumentation does not make spans current

[CAMEL-18657](https://issues.apache.org/jira/browse/CAMEL-18657)

camel-jbang - Loading dynamic JARs should load EndpointUriFactory

[CAMEL-18656](https://issues.apache.org/jira/browse/CAMEL-18656)

Camel-git always merge at master branch

[CAMEL-18648](https://issues.apache.org/jira/browse/CAMEL-18648)

Google-bigquery: ResolveEndpointFailedException because of the bug in configuration class

[CAMEL-18642](https://issues.apache.org/jira/browse/CAMEL-18642)

camel-jbang change class packag when export

[CAMEL-18641](https://issues.apache.org/jira/browse/CAMEL-18641)

Python not available in the Java DSL

[CAMEL-18634](https://issues.apache.org/jira/browse/CAMEL-18634)

camel-health - Custom health check may get registered twice

[CAMEL-18627](https://issues.apache.org/jira/browse/CAMEL-18627)

camel-kafka: Kafka resume throws null pointer exception if no partition offset exists

[CAMEL-18624](https://issues.apache.org/jira/browse/CAMEL-18624)

camel-jbang - Should load custom type converters when adding new JARs

[CAMEL-18617](https://issues.apache.org/jira/browse/CAMEL-18617)

Some health checks are hidden when running withg supervised controller enabled

[CAMEL-18614](https://issues.apache.org/jira/browse/CAMEL-18614)

Getting Route for a RouteConfiguration is null when doing manual route loading

[CAMEL-18612](https://issues.apache.org/jira/browse/CAMEL-18612)

Inconsistency in JsonPath component causes problems with databinding

[CAMEL-18611](https://issues.apache.org/jira/browse/CAMEL-18611)

camel-karaf - CNFE when using camel-blueprint

[CAMEL-18603](https://issues.apache.org/jira/browse/CAMEL-18603)

Camel-Jbang: When using aws-ddb-sink Kamelet dependency are not resolved

[CAMEL-18594](https://issues.apache.org/jira/browse/CAMEL-18594)

camel-master: NPE when taking the leadership

[CAMEL-18589](https://issues.apache.org/jira/browse/CAMEL-18589)

Bug in org.apache.camel.http.common.DefaultHttpBinding.java

[CAMEL-18588](https://issues.apache.org/jira/browse/CAMEL-18588)

Kafka consumer on any exception should repoll records after the committed offset

[CAMEL-18587](https://issues.apache.org/jira/browse/CAMEL-18587)

Kafka Consumer closes on any exception if breakOnFirstError is set to TRUE

[CAMEL-18586](https://issues.apache.org/jira/browse/CAMEL-18586)

Spinning JVM through interception using interceptFrom interceptSendToEndpoint

[CAMEL-18585](https://issues.apache.org/jira/browse/CAMEL-18585)

Validator: investigate strange validator behavior

[CAMEL-18583](https://issues.apache.org/jira/browse/CAMEL-18583)

\[camel-minio\] deleteObjects operation does not delete multiple objects

[CAMEL-18579](https://issues.apache.org/jira/browse/CAMEL-18579)

Missing osgi import for CxfUtils in camel-cxf-rest

[CAMEL-18576](https://issues.apache.org/jira/browse/CAMEL-18576)

kamelets - JSon Property value can't finish with }}

[CAMEL-18563](https://issues.apache.org/jira/browse/CAMEL-18563)

camel-karaf - ClassNotDefFoundError when an exception thrown from a cxfrs route

[CAMEL-18447](https://issues.apache.org/jira/browse/CAMEL-18447)

Camel-pubsub: com.google.api.gax.rpc.AsyncTaskException: Asynchronous task failed with real account

[CAMEL-18350](https://issues.apache.org/jira/browse/CAMEL-18350)

camel-kafka: enabling "breakOnFirstError" causes camel to reconsume all records on error

### Dependency upgrade (14)

[CAMEL-18819](https://issues.apache.org/jira/browse/CAMEL-18819)

hbase: different version of audience-annotations brought by zookeeper

[CAMEL-18810](https://issues.apache.org/jira/browse/CAMEL-18810)

camel-kubernetes - Upgrade to 6.3.x

[CAMEL-18758](https://issues.apache.org/jira/browse/CAMEL-18758)

camel-spring-boot - Upgrade to 2.7.6

[CAMEL-18707](https://issues.apache.org/jira/browse/CAMEL-18707)

upgrade to Jandex 3

[CAMEL-18668](https://issues.apache.org/jira/browse/CAMEL-18668)

Upgrade SmallRye Fault Tolerance to 5.6.x

[CAMEL-18644](https://issues.apache.org/jira/browse/CAMEL-18644)

Camel - Upgrade hsqldb 2.7.1

[CAMEL-18631](https://issues.apache.org/jira/browse/CAMEL-18631)

spring boot - upgrade to 2.7.5

[CAMEL-18629](https://issues.apache.org/jira/browse/CAMEL-18629)

camel-kubernetes - Upgrade to 6.2.x

[CAMEL-18621](https://issues.apache.org/jira/browse/CAMEL-18621)

Vulnerabilities identified with jackson-databind dependency

[CAMEL-18573](https://issues.apache.org/jira/browse/CAMEL-18573)

upgrade to spring boot 2.7.4

[CAMEL-18571](https://issues.apache.org/jira/browse/CAMEL-18571)

Upgrade to Infinispan 14.0.0.Final

[CAMEL-17856](https://issues.apache.org/jira/browse/CAMEL-17856)

camel-jackson - Upgrade to 2.14.x

[CAMEL-16484](https://issues.apache.org/jira/browse/CAMEL-16484)

Camel-Dropbox: Bump to Dropbox-core 5.x

[CAMEL-15616](https://issues.apache.org/jira/browse/CAMEL-15616)

camel-saxon - Upgrade to Saxon 11.x

### Improvement (80)

[CAMEL-18817](https://issues.apache.org/jira/browse/CAMEL-18817)

camel-hbase - Support append and increment operations in the producer

[CAMEL-18813](https://issues.apache.org/jira/browse/CAMEL-18813)

\[Hyperledger-Aries\] Add support for service=present-proof/send-proposal

[CAMEL-18812](https://issues.apache.org/jira/browse/CAMEL-18812)

REST DSL configuration placeholder for .id() doesn't work

[CAMEL-18808](https://issues.apache.org/jira/browse/CAMEL-18808)

camel-azure-storage-blob producer doesn't use CamelAzureStorageBlobBlobSize-header

[CAMEL-18803](https://issues.apache.org/jira/browse/CAMEL-18803)

\[Hyperledger-Aries\] Add support for service=didexchange

[CAMEL-18802](https://issues.apache.org/jira/browse/CAMEL-18802)

camel-base64 - Optional properties: if encoded the optional doesn't have any effect

[CAMEL-18800](https://issues.apache.org/jira/browse/CAMEL-18800)

Support Camel K integration in JBang run command

[CAMEL-18797](https://issues.apache.org/jira/browse/CAMEL-18797)

camel-sql - Conditionally execute ps.getParameterMetaData() in SqlProducer populateStatement

[CAMEL-18790](https://issues.apache.org/jira/browse/CAMEL-18790)

camel-log - Do not show MEP by default

[CAMEL-18789](https://issues.apache.org/jira/browse/CAMEL-18789)

camel-log - Add option to allowCachedStreams

[CAMEL-18788](https://issues.apache.org/jira/browse/CAMEL-18788)

camel-jbang - run myfolder/foo.yaml --dev will have live reload in current folder

[CAMEL-18784](https://issues.apache.org/jira/browse/CAMEL-18784)

camel-jbang - Run example with csimple should compile on startup

[CAMEL-18783](https://issues.apache.org/jira/browse/CAMEL-18783)

camel-cxf - avoid referring Singleton bean instance(CxfEndpoint) while changing its state in different URIs

[CAMEL-18777](https://issues.apache.org/jira/browse/CAMEL-18777)

Camel-Google-Storage: getObject Producer operation should place the object content in the body and populating headers with other info

[CAMEL-18773](https://issues.apache.org/jira/browse/CAMEL-18773)

camel-google-pubsub - Do not use dot in header keys

[CAMEL-18767](https://issues.apache.org/jira/browse/CAMEL-18767)

camel-jbang - Make --trace output message body

[CAMEL-18763](https://issues.apache.org/jira/browse/CAMEL-18763)

camel-jbang - camel doc main should should main options

[CAMEL-18762](https://issues.apache.org/jira/browse/CAMEL-18762)

camel-hdfs - Add LZ4 and Zstd compression support

[CAMEL-18761](https://issues.apache.org/jira/browse/CAMEL-18761)

camel-open-api - Warning log when using boolean type.

[CAMEL-18754](https://issues.apache.org/jira/browse/CAMEL-18754)

Camel Rest Monitoring Metrics UNKNOWN URI

[CAMEL-18749](https://issues.apache.org/jira/browse/CAMEL-18749)

camel-hdfs: Add Snappy compression support

[CAMEL-18748](https://issues.apache.org/jira/browse/CAMEL-18748)

camel-catalog - Missing properties for ErrorHandler in catalog for yaml DSL

[CAMEL-18735](https://issues.apache.org/jira/browse/CAMEL-18735)

camel-rest - Add option back to set route id for api-route

[CAMEL-18732](https://issues.apache.org/jira/browse/CAMEL-18732)

camel-micrometer - Include description of metrics

[CAMEL-18731](https://issues.apache.org/jira/browse/CAMEL-18731)

camel-core - Languages should have a way to set result type / and input from header instead of body

[CAMEL-18727](https://issues.apache.org/jira/browse/CAMEL-18727)

camel-jbang - get micrometer to filter out Camel route metrics

[CAMEL-18724](https://issues.apache.org/jira/browse/CAMEL-18724)

Add defaults for options for the EIPs in the documentation

[CAMEL-18715](https://issues.apache.org/jira/browse/CAMEL-18715)

camel-jbang - Make --local-kamelet-dir point to a github link for loading kamelets there

[CAMEL-18714](https://issues.apache.org/jira/browse/CAMEL-18714)

camel-jbang - Remove command aliases

[CAMEL-18712](https://issues.apache.org/jira/browse/CAMEL-18712)

camel-jbang - export dsl-modeline should only be included in needed

[CAMEL-18710](https://issues.apache.org/jira/browse/CAMEL-18710)

camel-jbang - Only include kamelets JARs if kamelets are in use

[CAMEL-18706](https://issues.apache.org/jira/browse/CAMEL-18706)

camel-jbang - Automatic include ASF snapshot repo if using SNAPSHOT jars

[CAMEL-18702](https://issues.apache.org/jira/browse/CAMEL-18702)

camel-mail-microsoft-oauth: Add a Spring Boot starter

[CAMEL-18700](https://issues.apache.org/jira/browse/CAMEL-18700)

camel-main - Unable to declare map bean with dotted keys

[CAMEL-18699](https://issues.apache.org/jira/browse/CAMEL-18699)

camel-jbang - Export to Spring Boot - Allow to specify a Camel version

[CAMEL-18697](https://issues.apache.org/jira/browse/CAMEL-18697)

camel-core - Propose a DSL for languages

[CAMEL-18696](https://issues.apache.org/jira/browse/CAMEL-18696)

camel-ldap - Make filter a bit easier to use

[CAMEL-18684](https://issues.apache.org/jira/browse/CAMEL-18684)

Add Microsoft Exchange Online OAuth2 Mail Authenticator

[CAMEL-18683](https://issues.apache.org/jira/browse/CAMEL-18683)

Priorize RouteTemplate initialization

[CAMEL-18679](https://issues.apache.org/jira/browse/CAMEL-18679)

camel-docker - Bind mount support

[CAMEL-18677](https://issues.apache.org/jira/browse/CAMEL-18677)

camel-resume-api: allow setting the cache on the configuration builder

[CAMEL-18675](https://issues.apache.org/jira/browse/CAMEL-18675)

camel-resume-api: implement resume strategy auto-instantiation

[CAMEL-18669](https://issues.apache.org/jira/browse/CAMEL-18669)

camel-jbang - Using resilience4j as CB should include include dependency

[CAMEL-18665](https://issues.apache.org/jira/browse/CAMEL-18665)

JsseParameters should use the camel provided resource loader instead of its own

[CAMEL-18663](https://issues.apache.org/jira/browse/CAMEL-18663)

camel-vertx-http: allow to configure WebClientOptions at component level

[CAMEL-18658](https://issues.apache.org/jira/browse/CAMEL-18658)

camel-jbang - Live reload of Camel K CRD with embedded source code

[CAMEL-18653](https://issues.apache.org/jira/browse/CAMEL-18653)

camel-resume-api: reliability improvements

[CAMEL-18652](https://issues.apache.org/jira/browse/CAMEL-18652)

camel-micrometer - Add more supported types

[CAMEL-18650](https://issues.apache.org/jira/browse/CAMEL-18650)

camel-jbang - Auto create micrometer registry

[CAMEL-18649](https://issues.apache.org/jira/browse/CAMEL-18649)

camel-resume-api: file resume for directory entries performs badly

[CAMEL-18646](https://issues.apache.org/jira/browse/CAMEL-18646)

camel-git - Provide custom configuration

[CAMEL-18645](https://issues.apache.org/jira/browse/CAMEL-18645)

camel-health - Details metadata is mixed between custom and standard details

[CAMEL-18643](https://issues.apache.org/jira/browse/CAMEL-18643)

AWS Health Check: Use AwsServiceException instead of SdkClientException for health check

[CAMEL-18640](https://issues.apache.org/jira/browse/CAMEL-18640)

camel-console - Stacktraces in json response should be as array

[CAMEL-18639](https://issues.apache.org/jira/browse/CAMEL-18639)

camel-health - Add detail for last time there was a failure

[CAMEL-18630](https://issues.apache.org/jira/browse/CAMEL-18630)

camel-jbang - Add get health command

[CAMEL-18626](https://issues.apache.org/jira/browse/CAMEL-18626)

Set the ExchangePattern with a routeTemplate

[CAMEL-18622](https://issues.apache.org/jira/browse/CAMEL-18622)

camel-yaml-dsl - Add support for xxx.camel.yaml extension

[CAMEL-18618](https://issues.apache.org/jira/browse/CAMEL-18618)

Came milo client does not return response code on write

[CAMEL-18613](https://issues.apache.org/jira/browse/CAMEL-18613)

camel-cxf - Add option on endpoint to configure schema validation

[CAMEL-18609](https://issues.apache.org/jira/browse/CAMEL-18609)

camel-jbang - Export should sort dependencies in pom.xml

[CAMEL-18604](https://issues.apache.org/jira/browse/CAMEL-18604)

XpathRouteBuilder in Route Templates

[CAMEL-18601](https://issues.apache.org/jira/browse/CAMEL-18601)

Replace assertMockEndpointsSatisfied() in doc

[CAMEL-18596](https://issues.apache.org/jira/browse/CAMEL-18596)

camel-azure-eventhubs consumer is invoking a blocking method

[CAMEL-18584](https://issues.apache.org/jira/browse/CAMEL-18584)

Regression: MailBinding Contructor has been extended instead of creating a new contructor

[CAMEL-18580](https://issues.apache.org/jira/browse/CAMEL-18580)

camel-elasticsearch - Propose an async producer

[CAMEL-18578](https://issues.apache.org/jira/browse/CAMEL-18578)

camel-lra refactor LRAClient to use jdk11 HttpClient

[CAMEL-18575](https://issues.apache.org/jira/browse/CAMEL-18575)

Replace temporary dir logic in test code

[CAMEL-18568](https://issues.apache.org/jira/browse/CAMEL-18568)

Extend handleDuplicateAttachmentNames handling to suffix filename with UUID

[CAMEL-18565](https://issues.apache.org/jira/browse/CAMEL-18565)

Camel fails to start routes without failure message when routes-include-pattern has an invalid entry

[CAMEL-18558](https://issues.apache.org/jira/browse/CAMEL-18558)

camel-jbang - get inflight and blocked exchanges

[CAMEL-18555](https://issues.apache.org/jira/browse/CAMEL-18555)

camel-jbang - Use standard Maven for download instead of ShrinkWrap

[CAMEL-18549](https://issues.apache.org/jira/browse/CAMEL-18549)

Dynamic router component should add filters to a map (by filter id) instead of a list to prevent multiple additions of the same filter.

[CAMEL-18363](https://issues.apache.org/jira/browse/CAMEL-18363)

camel-couchdb - improve the documentation for updates

[CAMEL-18254](https://issues.apache.org/jira/browse/CAMEL-18254)

camel-jbang - Kamelets should only log explicit configured options on startup

[CAMEL-18205](https://issues.apache.org/jira/browse/CAMEL-18205)

camel-jbang - Export to Quarkus and Spring Boot support Gradle

[CAMEL-17929](https://issues.apache.org/jira/browse/CAMEL-17929)

camel-yaml-dsl - KameletBinding style error-handler is not Camel standard

[CAMEL-17505](https://issues.apache.org/jira/browse/CAMEL-17505)

camel-core - Propose a DSL for data formats

[CAMEL-17438](https://issues.apache.org/jira/browse/CAMEL-17438)

Camel-Kubernetes: Add the ability to replace a resource by producers operations

[CAMEL-16354](https://issues.apache.org/jira/browse/CAMEL-16354)

camel-core - Optimize Splitters using Scanner

### New Feature (25)

[CAMEL-18798](https://issues.apache.org/jira/browse/CAMEL-18798)

camel-core - Add prefixId to route model so generated IDs of the route is prefixed

[CAMEL-18794](https://issues.apache.org/jira/browse/CAMEL-18794)

camel-jbang - Add run --code

[CAMEL-18771](https://issues.apache.org/jira/browse/CAMEL-18771)

camel-core - Route template with hardcoded node IDs - Allow to specify prefix

[CAMEL-18745](https://issues.apache.org/jira/browse/CAMEL-18745)

camel-core - Simple language ${originalBody}

[CAMEL-18743](https://issues.apache.org/jira/browse/CAMEL-18743)

camel-jbang - Command to see only if everything is okay or there has been a failure

[CAMEL-18725](https://issues.apache.org/jira/browse/CAMEL-18725)

camel-jbang - Route profile command

[CAMEL-18718](https://issues.apache.org/jira/browse/CAMEL-18718)

camel-javascript - Language based on graalvm sdk

[CAMEL-18716](https://issues.apache.org/jira/browse/CAMEL-18716)

camel-jbang - Provide completion for positional file path parameters

[CAMEL-18692](https://issues.apache.org/jira/browse/CAMEL-18692)

camel-jbang - Export - Add option to choose gradle as build system

[CAMEL-18682](https://issues.apache.org/jira/browse/CAMEL-18682)

Camel-Plc4x: Add a Spring Boot starter

[CAMEL-18673](https://issues.apache.org/jira/browse/CAMEL-18673)

camel-jbang - Provide shell completions for camel CLI

[CAMEL-18655](https://issues.apache.org/jira/browse/CAMEL-18655)

Integrate the Apache PLC4X Camel Integration module into the Apache Camel Project

[CAMEL-18651](https://issues.apache.org/jira/browse/CAMEL-18651)

camel-jbang - CLI command to get micrometer metrics

[CAMEL-18647](https://issues.apache.org/jira/browse/CAMEL-18647)

Java DSL - Set delay options from route templates in Delay EIP

[CAMEL-18628](https://issues.apache.org/jira/browse/CAMEL-18628)

rest-dsl to support autoStartup

[CAMEL-18616](https://issues.apache.org/jira/browse/CAMEL-18616)

camel-file - Add option to jail starting directory

[CAMEL-18615](https://issues.apache.org/jira/browse/CAMEL-18615)

Using CSVDataformat in a Route Template

[CAMEL-18600](https://issues.apache.org/jira/browse/CAMEL-18600)

properties component - Allow to turn off nested placeholders

[CAMEL-18593](https://issues.apache.org/jira/browse/CAMEL-18593)

Platform-http : add reverse proxy feature

[CAMEL-18574](https://issues.apache.org/jira/browse/CAMEL-18574)

camel-core - Add disabled option to EIPs

[CAMEL-16909](https://issues.apache.org/jira/browse/CAMEL-16909)

Camel-Kubernetes: Added support for Event Resources

[CAMEL-16030](https://issues.apache.org/jira/browse/CAMEL-16030)

camel-pulsar - Add async send to producer

[CAMEL-14832](https://issues.apache.org/jira/browse/CAMEL-14832)

Data format for SWIFT financial message conversion support

[CAMEL-14831](https://issues.apache.org/jira/browse/CAMEL-14831)

Create a Camel-rocketmq component

[CAMEL-10173](https://issues.apache.org/jira/browse/CAMEL-10173)

Create a camel component for etcd v3

### Task (26)

[CAMEL-18804](https://issues.apache.org/jira/browse/CAMEL-18804)

Camel-SFTP: Host key type ED25519 not supported

[CAMEL-18787](https://issues.apache.org/jira/browse/CAMEL-18787)

Add camel-elasticsearch to Camel-Karaf

[CAMEL-18781](https://issues.apache.org/jira/browse/CAMEL-18781)

Re-add camel-mongodb to Camel-Karaf

[CAMEL-18775](https://issues.apache.org/jira/browse/CAMEL-18775)

Re-add camel-spring-redis to Camel-Karaf

[CAMEL-18774](https://issues.apache.org/jira/browse/CAMEL-18774)

camel-bom - Do not include test-jar

[CAMEL-18757](https://issues.apache.org/jira/browse/CAMEL-18757)

camel-bom should specify <type>pom</type> for pom-only artifacts like camel-\*-parent

[CAMEL-18756](https://issues.apache.org/jira/browse/CAMEL-18756)

camel-spark: deprecate the component

[CAMEL-18751](https://issues.apache.org/jira/browse/CAMEL-18751)

camel-hbase: deprecate the component

[CAMEL-18746](https://issues.apache.org/jira/browse/CAMEL-18746)

camel-spring-boot 3.18.3 release missing debezium-db2-starter / debezium-oracle-starter

[CAMEL-18734](https://issues.apache.org/jira/browse/CAMEL-18734)

camel-microprofile - Deprecate mp-metrics

[CAMEL-18672](https://issues.apache.org/jira/browse/CAMEL-18672)

\[DOCS\] Dataset component - incorrect link

[CAMEL-18671](https://issues.apache.org/jira/browse/CAMEL-18671)

\[DOCS\] Dataset component - unclear parameter description

[CAMEL-18670](https://issues.apache.org/jira/browse/CAMEL-18670)

\[DOCS\] Dataset component - unclear parameter name

[CAMEL-18664](https://issues.apache.org/jira/browse/CAMEL-18664)

Fix camel-karaf-examples with features.xml

[CAMEL-18660](https://issues.apache.org/jira/browse/CAMEL-18660)

Kinesis tests fail due to an API rate limit exceeded

[CAMEL-18633](https://issues.apache.org/jira/browse/CAMEL-18633)

Wrong debug log output when using MockEndpoint

[CAMEL-18607](https://issues.apache.org/jira/browse/CAMEL-18607)

camel-yaml-dsl - bannedDefinition partially fails to exclude expression definition

[CAMEL-18602](https://issues.apache.org/jira/browse/CAMEL-18602)

Adjust sync-properties-maven-plugin to generate apache parent version 25

[CAMEL-18564](https://issues.apache.org/jira/browse/CAMEL-18564)

Use Jkube kubernetes-maven-plugin instead of deprecated fabric8-maven-plugin in camel-spring-boot-example

[CAMEL-18554](https://issues.apache.org/jira/browse/CAMEL-18554)

The example kamelet-chucknorris fails

[CAMEL-18516](https://issues.apache.org/jira/browse/CAMEL-18516)

camel-yaml-dsl - bannedDefinitions doesn't work for generate-yaml-schema

[CAMEL-18327](https://issues.apache.org/jira/browse/CAMEL-18327)

camel-kafka: Kafka consumer closes when it is paused

[CAMEL-18148](https://issues.apache.org/jira/browse/CAMEL-18148)

camel-resume-api: improve key/offset data serialization

[CAMEL-17448](https://issues.apache.org/jira/browse/CAMEL-17448)

build: review and remove unused dependencies in components

[CAMEL-17447](https://issues.apache.org/jira/browse/CAMEL-17447)

build: review and remove unused dependencies in core

[CAMEL-16273](https://issues.apache.org/jira/browse/CAMEL-16273)

Camel-google-\* cloud components: Make the serviceAccountKey explicitly configurable

### Test (5)

[CAMEL-18792](https://issues.apache.org/jira/browse/CAMEL-18792)

camel-hdfs - Make integration tests runnable without a real cluster

[CAMEL-18741](https://issues.apache.org/jira/browse/CAMEL-18741)

js-dsl fails on GraalVM 22.3 on camel-quarkus

[CAMEL-18729](https://issues.apache.org/jira/browse/CAMEL-18729)

add more tests for camel-cxf-soap-starter

[CAMEL-18694](https://issues.apache.org/jira/browse/CAMEL-18694)

Documentation using uri attribute for rest dsl in xml examples

[CAMEL-18680](https://issues.apache.org/jira/browse/CAMEL-18680)

Wrong initialization of KeyStoreParameters causes java.lang.IllegalArgumentException

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).