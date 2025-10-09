# Apache camel 2.25.0 Release

## New and Noteworthy

This release is the new Camel 2.25.0 minor release.

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
      <version>2.25.0</version>
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
      <version>2.25.0</version>
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
| [apache-camel-2.25.0-src.zip](https://archive.apache.org/dist/camel/apache-camel/2.25.0/apache-camel-2.25.0-src.zip) (Sources) | [PGP Signature](https://archive.apache.org/dist/camel/apache-camel/2.25.0/apache-camel-2.25.0-src.zip.asc), [SHA512 Checksum](https://archive.apache.org/dist/camel/apache-camel/2.25.0/apache-camel-2.25.0-src.zip.sha512) |

## Git tag checkout

Release is tagged with `camel-2.25.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-2.25.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (70)

[CAMEL-14412](https://issues.apache.org/jira/browse/CAMEL-14412)

Maven central now requires HTTPS

[CAMEL-14373](https://issues.apache.org/jira/browse/CAMEL-14373)

Camel-2-x netty4 requestTimeout doesn't work as expected

[CAMEL-14372](https://issues.apache.org/jira/browse/CAMEL-14372)

Validator component fails with java.lang.IllegalArgumentException: protocol = http host = null

[CAMEL-14368](https://issues.apache.org/jira/browse/CAMEL-14368)

can't gracefully shutdown a camel-undertow consumer endpoint

[CAMEL-14333](https://issues.apache.org/jira/browse/CAMEL-14333)

Camel Jgroups Component doesn't export org.apache.camel.component.jgroups.cluster

[CAMEL-14332](https://issues.apache.org/jira/browse/CAMEL-14332)

camel-blueprint - Camel route does not consider the value of ShutdownStrategy timeout.

[CAMEL-14318](https://issues.apache.org/jira/browse/CAMEL-14318)

camel-blueprint - <proxy> in XSD is anyType

[CAMEL-14267](https://issues.apache.org/jira/browse/CAMEL-14267)

Conversion fails with NullPointerException when the body is null at the end of a route and an outputType is set

[CAMEL-14224](https://issues.apache.org/jira/browse/CAMEL-14224)

Camel-Websocket: The sendToAll method in the Producer is really slow

[CAMEL-14194](https://issues.apache.org/jira/browse/CAMEL-14194)

Invalid JID is generated for private chat in XMPP component

[CAMEL-14173](https://issues.apache.org/jira/browse/CAMEL-14173)

camel-paho - Durable subscriptions broken on client restart

[CAMEL-14172](https://issues.apache.org/jira/browse/CAMEL-14172)

setting loggingSizeLimit to -1 when using CXF components does not disable the size limit as the docs say

[CAMEL-14162](https://issues.apache.org/jira/browse/CAMEL-14162)

camel-stream - When using http url then data is not sent over the wire

[CAMEL-14156](https://issues.apache.org/jira/browse/CAMEL-14156)

JmsBinding assumes endpoint can't be null, but it can

[CAMEL-14148](https://issues.apache.org/jira/browse/CAMEL-14148)

exception during first resolve of temporary jms destination causes infinitive wait

[CAMEL-14143](https://issues.apache.org/jira/browse/CAMEL-14143)

Slack Component: Consumer does not retrieve user details on message event

[CAMEL-14139](https://issues.apache.org/jira/browse/CAMEL-14139)

Camel Undertow does not provide an option to use the producer as the "Host" header when bridging two http endpoints

[CAMEL-14137](https://issues.apache.org/jira/browse/CAMEL-14137)

Thread leak in camel-jetty component if maxThreads or minThreads property is set

[CAMEL-14129](https://issues.apache.org/jira/browse/CAMEL-14129)

kubernetesConfiguration.setNamespace is not working

[CAMEL-14127](https://issues.apache.org/jira/browse/CAMEL-14127)

The destination File gets override even if you set the option fileExist to Append

[CAMEL-14117](https://issues.apache.org/jira/browse/CAMEL-14117)

Mtom cannot be enabled in CxfEnpoint

[CAMEL-14108](https://issues.apache.org/jira/browse/CAMEL-14108)

camel-jpa - while persisting list of entity, no id returned for entity

[CAMEL-14105](https://issues.apache.org/jira/browse/CAMEL-14105)

avoid using deprecated org.eclipse.jetty.util.MultiPartInputStreamParser

[CAMEL-14098](https://issues.apache.org/jira/browse/CAMEL-14098)

netty throws exception if post does not have an empty body

[CAMEL-14097](https://issues.apache.org/jira/browse/CAMEL-14097)

Camel-gRPC: Copy headers each time we forward the exchange

[CAMEL-14082](https://issues.apache.org/jira/browse/CAMEL-14082)

docs pom.xml parent version is 3.0.0-SNAPSHOT

[CAMEL-14081](https://issues.apache.org/jira/browse/CAMEL-14081)

camel-api-component-maven-plugin fromApis throw java.lang.StringIndexOutOfBoundsException

[CAMEL-14072](https://issues.apache.org/jira/browse/CAMEL-14072)

FileInputStreamCache will not delete temporary file if file system is full

[CAMEL-14058](https://issues.apache.org/jira/browse/CAMEL-14058)

NullPointerException for failed One-Way requests with HTTP session handling

[CAMEL-14035](https://issues.apache.org/jira/browse/CAMEL-14035)

JDBC StreamList and outputClass does not work

[CAMEL-14030](https://issues.apache.org/jira/browse/CAMEL-14030)

camel-ftp - streamDownload=true and move options dont work

[CAMEL-14023](https://issues.apache.org/jira/browse/CAMEL-14023)

Camel-salesforce-maven-plugin generate fails on IBM jdk

[CAMEL-13999](https://issues.apache.org/jira/browse/CAMEL-13999)

Salesforce Component IDLE\_TIMEOUT Blocks Async Request Responses for 2.x

[CAMEL-13994](https://issues.apache.org/jira/browse/CAMEL-13994)

listPods operation of kubernetes component dont support namespace option

[CAMEL-13976](https://issues.apache.org/jira/browse/CAMEL-13976)

Allow AS2 Component to reply disposition type failed in the MDN

[CAMEL-13968](https://issues.apache.org/jira/browse/CAMEL-13968)

AS2 component treats http headers case sensitive. According to RFC this should be case insensitive

[CAMEL-13942](https://issues.apache.org/jira/browse/CAMEL-13942)

camel-undertow - UnitOfWork should be done after send back response

[CAMEL-13941](https://issues.apache.org/jira/browse/CAMEL-13941)

NullPointerException when Conduit is null

[CAMEL-13931](https://issues.apache.org/jira/browse/CAMEL-13931)

camel-file - tempFileName directory is not auto-created if it is relative before the endpoint path

[CAMEL-13924](https://issues.apache.org/jira/browse/CAMEL-13924)

Camel-DirectVM: failIfNoConsumers option not taken into account when block is enabled

[CAMEL-13886](https://issues.apache.org/jira/browse/CAMEL-13886)

camel-servlet + camel-http4 with null body causes "Stream closed" IOException

[CAMEL-13795](https://issues.apache.org/jira/browse/CAMEL-13795)

TokenXMLExpressionIterator with inheritNamespaceToken creates duplicate default namespace definition

[CAMEL-13776](https://issues.apache.org/jira/browse/CAMEL-13776)

\[MongoDB\] autoclosable cursor

[CAMEL-13770](https://issues.apache.org/jira/browse/CAMEL-13770)

Properties of class Map does not work with Spring Boot 2.x

[CAMEL-13750](https://issues.apache.org/jira/browse/CAMEL-13750)

Incoming JMSCorrelationID is passed along when useMessageIDAsCorrelationID

[CAMEL-13724](https://issues.apache.org/jira/browse/CAMEL-13724)

camel route customized id isn't correct if there are more than one Rest DSL route availble

[CAMEL-13718](https://issues.apache.org/jira/browse/CAMEL-13718)

Fix syntax for pulsar component

[CAMEL-13711](https://issues.apache.org/jira/browse/CAMEL-13711)

Files.createTempFile not equivalent to File.createTempFile

[CAMEL-13687](https://issues.apache.org/jira/browse/CAMEL-13687)

NotifyBuilder not working as expected

[CAMEL-13680](https://issues.apache.org/jira/browse/CAMEL-13680)

camel-file - From file to file with readLock=fileLock dont work on windows

[CAMEL-13667](https://issues.apache.org/jira/browse/CAMEL-13667)

Windows network UNC paths not treated correctly (File2/tempPrefix)

[CAMEL-13642](https://issues.apache.org/jira/browse/CAMEL-13642)

Testing for an expected Header in a MockEndpoint doesnt happen if there is no Exchange received

[CAMEL-13625](https://issues.apache.org/jira/browse/CAMEL-13625)

Quartz2 firenow doesn't work consistently

[CAMEL-13606](https://issues.apache.org/jira/browse/CAMEL-13606)

Olingo Consumer filtering can cause NPE

[CAMEL-13587](https://issues.apache.org/jira/browse/CAMEL-13587)

InflightRepository, InflightEntry getElapsed is 0

[CAMEL-13576](https://issues.apache.org/jira/browse/CAMEL-13576)

avoid adding cxf message context map into camel exchange

[CAMEL-13554](https://issues.apache.org/jira/browse/CAMEL-13554)

Using "route1" as a route id produces infinite loop

[CAMEL-13543](https://issues.apache.org/jira/browse/CAMEL-13543)

@PropertyInject is broken for Spring projects using CamelTestContextBootstrapper

[CAMEL-13541](https://issues.apache.org/jira/browse/CAMEL-13541)

Race condition in camel-hystrix when xecutionTimeoutInMilliseconds() and onFallback() are used

[CAMEL-13536](https://issues.apache.org/jira/browse/CAMEL-13536)

StackOverflow when using bean(this)

[CAMEL-13524](https://issues.apache.org/jira/browse/CAMEL-13524)

RuntimeCamelCatalog#asEndpointUri strips dash from url with toD and netty4-http

[CAMEL-13466](https://issues.apache.org/jira/browse/CAMEL-13466)

DefaultCamelContext not stopping all routes on doStop()

[CAMEL-13424](https://issues.apache.org/jira/browse/CAMEL-13424)

Rest Component custom routeId is not accessible in processor

[CAMEL-13407](https://issues.apache.org/jira/browse/CAMEL-13407)

CouchDbChangesetTracker fails silently on network error and does not recover

[CAMEL-13376](https://issues.apache.org/jira/browse/CAMEL-13376)

camel-cxf - failure processor for custom exception handling cannot get the original message

[CAMEL-13316](https://issues.apache.org/jira/browse/CAMEL-13316)

Olingo4 Connector split does not handle result values

[CAMEL-13121](https://issues.apache.org/jira/browse/CAMEL-13121)

Route irc->irc cycles the message because of "irc.target" header

[CAMEL-12975](https://issues.apache.org/jira/browse/CAMEL-12975)

WARN: No CamelContext defined yet so cannot inject into bean: org.apache.camel.converter.jaxb.FallbackTypeConverter

[CAMEL-12947](https://issues.apache.org/jira/browse/CAMEL-12947)

MockEndpoint.expectedHeaderReceived should fail when no exchange received

[CAMEL-12471](https://issues.apache.org/jira/browse/CAMEL-12471)

Dots in RabbitMQ-component headers do not work

### Improvement (36)

[CAMEL-14375](https://issues.apache.org/jira/browse/CAMEL-14375)

camel-kafka - The saslJaasConfig option may contain sensitive information that can be logged

[CAMEL-14307](https://issues.apache.org/jira/browse/CAMEL-14307)

camel-rabbitmq - unable to set empty routing key when declaring DLX

[CAMEL-14292](https://issues.apache.org/jira/browse/CAMEL-14292)

Remove unwanted dependency to google-http-client library

[CAMEL-14184](https://issues.apache.org/jira/browse/CAMEL-14184)

Allow setting Pulsar Message headers (properties, event time, key) when producing

[CAMEL-14163](https://issues.apache.org/jira/browse/CAMEL-14163)

Support for multiple request query parameters in Rest component

[CAMEL-14125](https://issues.apache.org/jira/browse/CAMEL-14125)

Upgrade to xstream 1.4.11.1

[CAMEL-14118](https://issues.apache.org/jira/browse/CAMEL-14118)

camel-http - Add option getWithBody

[CAMEL-14107](https://issues.apache.org/jira/browse/CAMEL-14107)

Backport MongoDB change stream feature to 2.x

[CAMEL-14070](https://issues.apache.org/jira/browse/CAMEL-14070)

netty4-http - Server Name Indication (SNI) Support

[CAMEL-14069](https://issues.apache.org/jira/browse/CAMEL-14069)

netty4-http - Add logic to handle http 100-Continue

[CAMEL-14060](https://issues.apache.org/jira/browse/CAMEL-14060)

Deprecate camel-restlet as its not active maintained

[CAMEL-14047](https://issues.apache.org/jira/browse/CAMEL-14047)

camel-pulsar: Allow Pulsar to auto-select the unique producerName

[CAMEL-14000](https://issues.apache.org/jira/browse/CAMEL-14000)

ServicePool can cause memory leak

[CAMEL-13986](https://issues.apache.org/jira/browse/CAMEL-13986)

Camel-Kubernetes: Add deleteNode operation

[CAMEL-13983](https://issues.apache.org/jira/browse/CAMEL-13983)

Provide CreateNode feature in Kubernetes Component

[CAMEL-13978](https://issues.apache.org/jira/browse/CAMEL-13978)

Create ConfigMap Watch feature in Kubernetes Component

[CAMEL-13955](https://issues.apache.org/jira/browse/CAMEL-13955)

SJMS-Batch does not support CompletionAware aggregators

[CAMEL-13951](https://issues.apache.org/jira/browse/CAMEL-13951)

JdbcAggregationRepository doesn't work with PostgreSQL

[CAMEL-13864](https://issues.apache.org/jira/browse/CAMEL-13864)

JMS Component does not support non-durable shared subscription

[CAMEL-13841](https://issues.apache.org/jira/browse/CAMEL-13841)

Pulsar: Add the ability to manually acknowledge a message consumed from Pulsar

[CAMEL-13747](https://issues.apache.org/jira/browse/CAMEL-13747)

Adding basic auth support to camel-solr

[CAMEL-13726](https://issues.apache.org/jira/browse/CAMEL-13726)

Add support for PKCS8 keys and encrypted PKCS8 keys

[CAMEL-13697](https://issues.apache.org/jira/browse/CAMEL-13697)

URISupport - Mask accessToken and clientSecret in uri logging

[CAMEL-13696](https://issues.apache.org/jira/browse/CAMEL-13696)

Upgrade to slf4j ver 1.7.26

[CAMEL-13692](https://issues.apache.org/jira/browse/CAMEL-13692)

Don't use ssh-rsa as the default keytype for client keys

[CAMEL-13644](https://issues.apache.org/jira/browse/CAMEL-13644)

CxfConsumer - Should not create server in constructor

[CAMEL-13617](https://issues.apache.org/jira/browse/CAMEL-13617)

Google sheets: Improve testability of component

[CAMEL-13605](https://issues.apache.org/jira/browse/CAMEL-13605)

Support setup proxy host and port on Telegram

[CAMEL-13593](https://issues.apache.org/jira/browse/CAMEL-13593)

avoid “expected resource not found” warnings when using camel-mail in OSGi

[CAMEL-13563](https://issues.apache.org/jira/browse/CAMEL-13563)

Update Jetty to 9.4.18 + fix client authentication issues

[CAMEL-13529](https://issues.apache.org/jira/browse/CAMEL-13529)

camel-jdbc - Improve to work with the spring Tx Manager

[CAMEL-13527](https://issues.apache.org/jira/browse/CAMEL-13527)

Implement missing optimisation for DelimiterBasedFrameDecoder

[CAMEL-13476](https://issues.apache.org/jira/browse/CAMEL-13476)

QuartzScheduledPollConsumerScheduler should not remove trigger when quartz is clustered

[CAMEL-13471](https://issues.apache.org/jira/browse/CAMEL-13471)

Support TCP + TLS in Camel CoAP

[CAMEL-13402](https://issues.apache.org/jira/browse/CAMEL-13402)

Update to Californium 2.0.x and support DTLS

[CAMEL-12957](https://issues.apache.org/jira/browse/CAMEL-12957)

camel-cxf - Swagger/OpenAPI feature should not involve the Camel route

### New Feature (3)

[CAMEL-13898](https://issues.apache.org/jira/browse/CAMEL-13898)

ensure camel-cxf consumer can propagate protocol headers from camel exchange headers when throwing a soap fault

[CAMEL-13734](https://issues.apache.org/jira/browse/CAMEL-13734)

camel-undertow - Support streaming of large data for HTTP endpoints

[CAMEL-13498](https://issues.apache.org/jira/browse/CAMEL-13498)

Add support for AS2 in Karaf

### Task (1)

[CAMEL-13719](https://issues.apache.org/jira/browse/CAMEL-13719)

Upgrade to jasypt 1.9.3

### Test (1)

[CAMEL-13693](https://issues.apache.org/jira/browse/CAMEL-13693)

avoid useOverridePropertiesWithPropertiesComponent being invoked twice when running a unit-test with OSGI Blueprint XML.

### Wish (1)

[CAMEL-14378](https://issues.apache.org/jira/browse/CAMEL-14378)

Karaf support for Camel-AS2 for Camel version 2.x

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).