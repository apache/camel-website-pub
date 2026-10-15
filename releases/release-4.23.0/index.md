# Apache camel 4.23.0 Release

## New and Noteworthy

This release is the new Camel 4.23.0 LTS release.

## Supported Java version

This version supports Java 17, 21 and 25.

## Getting the Binaries using Maven

To use this release in your [Apache Maven](https://maven.apache.org) `pom.xml`, import the Camel Bill of Materials (BOM) and then include the `camel-core` and any other components needed without specifying the version.

Replace the `COMPONENT` with the artifact outlined in the [component documentation](../../components/next/)

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.apache.camel</groupId>
      <artifactId>camel-bom</artifactId>
      <version>4.23.0</version>
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
      <version>4.23.0</version>
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
| [apache-camel-4.23.0-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.23.0/apache-camel-4.23.0-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-src.zip.sha512) |
| [apache-camel-4.23.0-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.xml.sha512) |
| [apache-camel-4.23.0-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.23.0/apache-camel-4.23.0-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.23.0` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.23.0

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (508)

[CAMEL-25593](https://issues.apache.org/jira/browse/CAMEL-25593)

camel validate normalize for rest verbs fails

[CAMEL-25553](https://issues.apache.org/jira/browse/CAMEL-25553)

camel-aws-secrets-manager, camel-azure-key-vault, camel-google-secret-manager, camel-ibm-secrets-manager, camel-cyberark-vault - properties functions are not thread safe

[CAMEL-25551](https://issues.apache.org/jira/browse/CAMEL-25551)

camel-azure-storage-blob, camel-huaweicloud-obs, camel-alibaba-oss, camel-aws2-s3-vectors - do not consume an object again while its exchange is in flight

[CAMEL-25533](https://issues.apache.org/jira/browse/CAMEL-25533)

camel-jbang - camel run ignores camel.server.port (and the other camel.server.\* settings) for the HTTP server started for platform-http unless camel.server.enabled=true

[CAMEL-25527](https://issues.apache.org/jira/browse/CAMEL-25527)

camel-mybatis, camel-sql - the consumer runs onConsume for a failed (camel-mybatis) or rollback only (both) exchange, so the row is marked as consumed and not polled again

[CAMEL-25525](https://issues.apache.org/jira/browse/CAMEL-25525)

camel-keycloak - the consumer routes the latest events of a poll again in the next poll, although the docs promise fingerprint-based deduplication

[CAMEL-25524](https://issues.apache.org/jira/browse/CAMEL-25524)

camel-mina-sftp - the producer writes a file in the charset of the exchange instead of the charset option, and fails for a null body with allowNullBody=true

[CAMEL-25523](https://issues.apache.org/jira/browse/CAMEL-25523)

camel-slack - the consumer skips messages when more than maxResults messages are posted between two polls

[CAMEL-25522](https://issues.apache.org/jira/browse/CAMEL-25522)

camel-ibm-cos - consumer with fileName routes the object again while its exchange is in flight, and a batch cut short by a route stop leaves its objects in progress and their streams open

[CAMEL-25521](https://issues.apache.org/jira/browse/CAMEL-25521)

camel-aws2-s3 - consumer with fileName routes the object again while its exchange is in flight, and objects of a batch cut short by a route stop are never consumed after a restart

[CAMEL-25520](https://issues.apache.org/jira/browse/CAMEL-25520)

camel-google-mail - google-mail-stream consumer routes a message again while its first exchange is still in flight (asynchronous routes)

[CAMEL-25519](https://issues.apache.org/jira/browse/CAMEL-25519)

camel-google-storage - consumer routes an object again while its first exchange is still in flight (asynchronous routes)

[CAMEL-25518](https://issues.apache.org/jira/browse/CAMEL-25518)

camel-hashicorp-vault - secret refresh never detects updates of secrets outside the "secret" engine, nor updates made before its first check

[CAMEL-25512](https://issues.apache.org/jira/browse/CAMEL-25512)

camel-minio - consumer routes an object again while its first exchange is still in flight (asynchronous routes)

[CAMEL-25511](https://issues.apache.org/jira/browse/CAMEL-25511)

camel-jooq - the consumer deletes an entity whose exchange failed (consumeDelete=true, the default), so the row is lost

[CAMEL-25510](https://issues.apache.org/jira/browse/CAMEL-25510)

camel-openapi-java - the allowable values of an array parameter are generated as the enum of the array instead of its items, so the parameter accepts no value

[CAMEL-25509](https://issues.apache.org/jira/browse/CAMEL-25509)

camel-ldif - "changetype: modrdn" ignores newsuperior, and "changetype: moddn" without newsuperior moves the entry to the root

[CAMEL-25508](https://issues.apache.org/jira/browse/CAMEL-25508)

camel-mybatis - a String body with a comma runs Insert, Update and Delete once per comma-separated part

[CAMEL-25507](https://issues.apache.org/jira/browse/CAMEL-25507)

camel-lucene - with several lucene endpoints, a query searches the index of the endpoint created last

[CAMEL-25506](https://issues.apache.org/jira/browse/CAMEL-25506)

camel-lucene - concurrent queries can get another query's hits, and queries fail after the route is restarted

[CAMEL-25505](https://issues.apache.org/jira/browse/CAMEL-25505)

camel-lucene - inserts fail for good after the route is restarted, after one failed insert, and when two inserts run at the same time

[CAMEL-25504](https://issues.apache.org/jira/browse/CAMEL-25504)

camel-jta, camel-spring - a transacted exchange that completes during a graceful shutdown is rolled back instead of committed

[CAMEL-25500](https://issues.apache.org/jira/browse/CAMEL-25500)

camel-core - removeAllRoutes / stopAllRoutes stop routes one by one, so a route still sending to a direct route is cut off instead of drained

[CAMEL-25497](https://issues.apache.org/jira/browse/CAMEL-25497)

camel-jbang - camel run with --jvm-debug, --jvm-args or --open-telemetry-agent starts the default Camel version of the jbang catalog

[CAMEL-25495](https://issues.apache.org/jira/browse/CAMEL-25495)

camel-jbang - camel export --runtime=quarkus ignores --java-version in the generated Dockerfile

[CAMEL-25494](https://issues.apache.org/jira/browse/CAMEL-25494)

camel-yaml-io - YAML route dump writes routeConfiguration onException items without their onException key, which neither the schema nor the loader accept

[CAMEL-25490](https://issues.apache.org/jira/browse/CAMEL-25490)

camel-jbang - camel validate normalize writes a top-level onException into the steps of every route, which the YAML DSL schema rejects

[CAMEL-25486](https://issues.apache.org/jira/browse/CAMEL-25486)

camel-http - the OAuth2 token request with a resource indicator sends only the resource parameter

[CAMEL-25485](https://issues.apache.org/jira/browse/CAMEL-25485)

camel-jbang - the validator does not report a top-level ternary in a Simple expression that starts with resource:

[CAMEL-25483](https://issues.apache.org/jira/browse/CAMEL-25483)

camel-rest-postman - a remote collection's placeholders resolve Camel properties, JVM system properties and environment variables

[CAMEL-25470](https://issues.apache.org/jira/browse/CAMEL-25470)

camel-dataweave - $ shorthand with .@attr, .\*field or ? is mis-converted without a TODO

[CAMEL-25457](https://issues.apache.org/jira/browse/CAMEL-25457)

camel-http-common - a non-chunked text String response replaces the charset that the Content-Type declares with the exchange charset

[CAMEL-25456](https://issues.apache.org/jira/browse/CAMEL-25456)

camel-wasm - a trap in the guest function leaks its memory on the shared instance, and the cleanup releases the error buffer with the wrong size or hides the original exception

[CAMEL-25455](https://issues.apache.org/jira/browse/CAMEL-25455)

camel-wasm - the wasm predicate never matches a Boolean, String or byte\[\] result

[CAMEL-25454](https://issues.apache.org/jira/browse/CAMEL-25454)

camel-jbang - kubernetes run: --cluster-type=k3s with --output fails, and the Minikube defaults replace image options set by the user

[CAMEL-25452](https://issues.apache.org/jira/browse/CAMEL-25452)

camel-jbang - camel export ignores --resource-dir, the directories never reach the exported project

[CAMEL-25437](https://issues.apache.org/jira/browse/CAMEL-25437)

camel-jbang - camel run --prop key=value with a space is silently ignored

[CAMEL-25431](https://issues.apache.org/jira/browse/CAMEL-25431)

camel-core - backlog tracer: a route called later by the same exchange is stamped with the time the exchange was created

[CAMEL-25428](https://issues.apache.org/jira/browse/CAMEL-25428)

camel-jbang - dev mode reload keeps the old instance of a bean whose Java source changed

[CAMEL-25427](https://issues.apache.org/jira/browse/CAMEL-25427)

camel-support - on-demand route reload fails with FileNotFoundException after a route file is removed from the source dir

[CAMEL-25425](https://issues.apache.org/jira/browse/CAMEL-25425)

camel-jbang - Quitting the monitor deletes the files of examples that are still running

[CAMEL-25424](https://issues.apache.org/jira/browse/CAMEL-25424)

camel-jbang - MCP camel\_control ignores the name of the integration and acts on the selected one

[CAMEL-25423](https://issues.apache.org/jira/browse/CAMEL-25423)

camel-jbang - camel run --example with a runtime does not copy the data folders of the example

[CAMEL-25422](https://issues.apache.org/jira/browse/CAMEL-25422)

camel-jbang - camel run pom.xml runs a Quarkus project as Camel Main when the BOM coordinates are properties

[CAMEL-25419](https://issues.apache.org/jira/browse/CAMEL-25419)

Saga EIP: keep the original exception when compensation fails, and stop the in-memory saga service from reporting failed compensations as compensated

[CAMEL-25418](https://issues.apache.org/jira/browse/CAMEL-25418)

camel-jbang - camel get vault does not list the Kubernetes config map names

[CAMEL-25417](https://issues.apache.org/jira/browse/CAMEL-25417)

camel-jbang - An opened folder run with F10 stays listed as Starting next to its running app

[CAMEL-25414](https://issues.apache.org/jira/browse/CAMEL-25414)

camel-debezium-mongodb - mongodbSslInvalidHostnameAllowed is not marked insecure:ssl

[CAMEL-25413](https://issues.apache.org/jira/browse/CAMEL-25413)

camel-kubernetes: trustCerts option misannotated as security=secret instead of security=insecure:ssl

[CAMEL-25409](https://issues.apache.org/jira/browse/CAMEL-25409)

camel-mongodb, camel-aws2-transcribe, camel-twitter - security metadata of three options does not match the code

[CAMEL-25401](https://issues.apache.org/jira/browse/CAMEL-25401)

camel-jira - fugue 7.0.1 is compiled for Java 25, so camel-jira fails on Java 17 and 21

[CAMEL-25385](https://issues.apache.org/jira/browse/CAMEL-25385)

camel-jbang - the send\_message MCP tool times out and does not send the message when headers are given

[CAMEL-25384](https://issues.apache.org/jira/browse/CAMEL-25384)

camel-kubernetes - the kubernetes-secrets dev console throws NPE when no Kubernetes vault is configured, so camel ps/get do not show the integration

[CAMEL-25383](https://issues.apache.org/jira/browse/CAMEL-25383)

camel-support - EndpointUriFactorySupport removes an unset optional path option by name from inside the value of an earlier path option

[CAMEL-25376](https://issues.apache.org/jira/browse/CAMEL-25376)

camel-netty-http - match security constraint roles by exact role name

[CAMEL-25375](https://issues.apache.org/jira/browse/CAMEL-25375)

camel-undertow - Apply securityProvider, allowedRoles and handlers to WebSocket endpoints consistently with HTTP endpoints

[CAMEL-25369](https://issues.apache.org/jira/browse/CAMEL-25369)

camel-spiffe - the SpiffeSecurityPolicy doc example denies every request, and the policy has no negative tests

[CAMEL-25367](https://issues.apache.org/jira/browse/CAMEL-25367)

camel-yaml-dsl - Route dump omits doCatch and doFinally written as doTry properties

[CAMEL-25366](https://issues.apache.org/jira/browse/CAMEL-25366)

camel-core - No type converter from String or Number to BigDecimal, so simple bodyAs/convertTo/resultType BigDecimal give null

[CAMEL-25361](https://issues.apache.org/jira/browse/CAMEL-25361)

camel-couchbase - with useView=true and fullDocument=false the body is an Optional, and fullDocument is documented as default false although it defaults to true

[CAMEL-25360](https://issues.apache.org/jira/browse/CAMEL-25360)

camel-cloudevents - application-cloudevents+json ignores the datacontenttype when it writes the data: JSON of a text/plain body is nested, JSON scalars are strings, bytes that are not valid text are lost

[CAMEL-25356](https://issues.apache.org/jira/browse/CAMEL-25356)

camel-cm-sms - messages with <, >, ¤ or a form feed are sent as unicode: the GSM 03.38 regex contains HTML entities

[CAMEL-25355](https://issues.apache.org/jira/browse/CAMEL-25355)

camel-support - an empty charset parameter of the Content-Type (charset=) sets an empty CamelCharsetName, and converting the body then fails (servlet, Jetty and HTTP producer)

[CAMEL-25354](https://issues.apache.org/jira/browse/CAMEL-25354)

camel-cron - five-part schedules fail with the Spring implementation ("Cron expression must consist of 6 fields"), and Unix schedules such as \*/5 \* \* \* \* fail with the Quartz implementation

[CAMEL-25353](https://issues.apache.org/jira/browse/CAMEL-25353)

camel-sql - a :#in: parameter whose name is the start of a later :#in: name breaks the later one ("in (?,?License)"), and :#in:${...} with \[ or ( is not expanded

[CAMEL-25352](https://issues.apache.org/jira/browse/CAMEL-25352)

camel-main - CAMEL\_COMPONENT\_\*, CAMEL\_DATAFORMAT\_\* and CAMEL\_LANGUAGE\_\* environment variables are ignored, and a name that starts with another one (NETTY\_HTTP, SJMS2, JSONPATH, ...) is mapped to the shorter one

[CAMEL-25351](https://issues.apache.org/jira/browse/CAMEL-25351)

camel-reactive-streams - stopping a consumer drops the items it already received, and after a restart it may never request again

[CAMEL-25350](https://issues.apache.org/jira/browse/CAMEL-25350)

camel-reactive-streams - exchanges of a batch never complete when the subscriber cancels while the batch is sent

[CAMEL-25349](https://issues.apache.org/jira/browse/CAMEL-25349)

camel-jbang - camel run . --dev does not reload changed or new route files

[CAMEL-25347](https://issues.apache.org/jira/browse/CAMEL-25347)

camel-yaml-dsl: Validate scalar alternatives without losing required fields

[CAMEL-25346](https://issues.apache.org/jira/browse/CAMEL-25346)

camel-console - a dev console capacity set from configuration breaks the trace, receive, event and sql-trace consoles

[CAMEL-25345](https://issues.apache.org/jira/browse/CAMEL-25345)

camel-util - URISupport.normalizeUri is not idempotent when the path has # or two @ and a query value has = or #

[CAMEL-25337](https://issues.apache.org/jira/browse/CAMEL-25337)

Wrong comparison in sendAcknowledgement of camel-mllp — SEGMENT\_DELIMITER compared against loop index instead of byte value

[CAMEL-25327](https://issues.apache.org/jira/browse/CAMEL-25327)

camel-jbang - the source validator finds the project's classes under src/main/java

[CAMEL-25324](https://issues.apache.org/jira/browse/CAMEL-25324)

camel-dataweave - common DataWeave constructs are converted wrongly or dropped

[CAMEL-25323](https://issues.apache.org/jira/browse/CAMEL-25323)

camel-dataweave - unconverted DataWeave fails silently or points at the generated DataSonnet; add an executed test corpus

[CAMEL-25320](https://issues.apache.org/jira/browse/CAMEL-25320)

camel-core - the separator of @PropertyInject is used as a regular expression: with | the value is split into single characters, with . there are no values

[CAMEL-25319](https://issues.apache.org/jira/browse/CAMEL-25319)

camel-aws2-sqs - batchSeparator is used as a regular expression: with | every character is sent as a message, with . nothing is sent

[CAMEL-25318](https://issues.apache.org/jira/browse/CAMEL-25318)

camel-smpp - an 8-bit message is split by its length in characters, not bytes, and a message one segment past 255 gets the segment count 0

[CAMEL-25317](https://issues.apache.org/jira/browse/CAMEL-25317)

camel-iso8583 - unmarshal fails with "IsoType ... is not known" for every message type without an ISO header or with a binary ISO header

[CAMEL-25316](https://issues.apache.org/jira/browse/CAMEL-25316)

camel-http-common - a String response is written in the exchange charset while the Content-Type declares another charset (servlet and Jetty consumers, chunked by default)

[CAMEL-25315](https://issues.apache.org/jira/browse/CAMEL-25315)

camel-zookeeper-master - a master whose consumer failed to start never consumes, and a consumer started while the leadership is lost or the route stops keeps running

[CAMEL-25314](https://issues.apache.org/jira/browse/CAMEL-25314)

camel-cxf, camel-cxfrs - a suspended consumer keeps accepting and routing new requests (graceful shutdown, suspendRoute, route policies)

[CAMEL-25313](https://issues.apache.org/jira/browse/CAMEL-25313)

camel-kafka - a consumer resumed after a suspend may never consume again: the fetcher thread ends while the consumer is suspended, and a pause or resume request can be overwritten

[CAMEL-25312](https://issues.apache.org/jira/browse/CAMEL-25312)

camel-sjms - a suspended consumer keeps consuming (graceful shutdown, suspendRoute, route policies), and a consumer started again receives nothing

[CAMEL-25308](https://issues.apache.org/jira/browse/CAMEL-25308)

camel-smpp: the deliverSm and dataSm paths create exchanges on the endpoint instead of the consumer, so pooling never applies and fromRouteId is unset

[CAMEL-25305](https://issues.apache.org/jira/browse/CAMEL-25305)

camel-netty-http - a String body is sent in the exchange charset, not in the charset the Content-Type declares, and the request charset parameter is only recognized in lower case

[CAMEL-25304](https://issues.apache.org/jira/browse/CAMEL-25304)

camel-barcode - unmarshal fails with NoTypeConversionAvailableException unless the body is a file (byte\[\] body, image received over HTTP, marshal and unmarshal in one route)

[CAMEL-25303](https://issues.apache.org/jira/browse/CAMEL-25303)

camel-barcode - text outside ISO-8859-1 comes back as '?' (the documented default encoding UTF-8 is not used), and the hints added before the route starts are dropped

[CAMEL-25302](https://issues.apache.org/jira/browse/CAMEL-25302)

camel-google-sheets - the google-sheets:application-x-struct data type gives the custom column names to the wrong columns when the range does not start at column A (values lost or repeated), and miscomputes columns beyond ZZ

[CAMEL-25301](https://issues.apache.org/jira/browse/CAMEL-25301)

camel-cloudevents - the application-cloudevents+json data type writes invalid JSON when an attribute value or a text body contains a quote, a backslash or a line break, or when the text starts with '\[' or '{'

[CAMEL-25300](https://issues.apache.org/jira/browse/CAMEL-25300)

Throttle EIP - the clean of the total requests throttler can hand out a second set of permits, so more exchanges than allowed pass in a time period

[CAMEL-25299](https://issues.apache.org/jira/browse/CAMEL-25299)

Error handler - with asyncDelayedRedelivery, allowRedeliveryWhileStopping=false is ignored: a route stop waits for the redelivery delay and then redelivers

[CAMEL-25298](https://issues.apache.org/jira/browse/CAMEL-25298)

camel-rocketmq - an InOut exchange is completed twice when its reply arrives at the request timeout, or the reply is delivered twice

[CAMEL-25297](https://issues.apache.org/jira/browse/CAMEL-25297)

camel-direct, camel-kamelet - while one exchange waits for the consumer of a suspended or stopped route, the other exchanges of the same producer are sent to that route

[CAMEL-25295](https://issues.apache.org/jira/browse/CAMEL-25295)

camel-undertow - the charset parameter of the Content-Type is only recognized in lower case (Charset=ISO-8859-1 is read and written as UTF-8)

[CAMEL-25294](https://issues.apache.org/jira/browse/CAMEL-25294)

camel-consul - the readTimeout and writeTimeout options set the connect timeout of the Consul client, so the read and write timeouts cannot be configured

[CAMEL-25293](https://issues.apache.org/jira/browse/CAMEL-25293)

camel-hivemq - the consumer discards the messages it already acknowledged, and interrupts the ones being processed, when it stops

[CAMEL-25292](https://issues.apache.org/jira/browse/CAMEL-25292)

camel-plc4x - a stopped triggered consumer keeps its scraper running (exchanges after stop, duplicates after a restart), and the triggered consumer cannot start without jackson-databind

[CAMEL-25291](https://issues.apache.org/jira/browse/CAMEL-25291)

camel-plc4x - a write that cannot be done completes the exchange successfully, and the polling consumer answers a failed read with an empty result

[CAMEL-25290](https://issues.apache.org/jira/browse/CAMEL-25290)

camel-couchdb - the consumer ignores updates=false, and stops seeing changes for good after a page of changes that deletes=false or updates=false skips

[CAMEL-25289](https://issues.apache.org/jira/browse/CAMEL-25289)

camel-iggy - after 8 failed sends or polls the producer and the consumer wait forever for a pooled client; stopped producers and consumers leak their connections; autoCommit=false fails without startingOffset

[CAMEL-25288](https://issues.apache.org/jira/browse/CAMEL-25288)

camel-dapr - the consumers close the configured or autowired Dapr clients when they stop, and the configuration consumer fails to start in a route with a NullPointerException

[CAMEL-25287](https://issues.apache.org/jira/browse/CAMEL-25287)

camel-splunk-hec - the producer fails to start with "NullPointerException: SSL context" when no sslContextParameters is configured

[CAMEL-25286](https://issues.apache.org/jira/browse/CAMEL-25286)

camel-consul - ConsulClusterView stops taking part in the leader election after a failed query or when Consul invalidates its session, and can keep the leadership while another node takes it

[CAMEL-25281](https://issues.apache.org/jira/browse/CAMEL-25281)

camel-pubnub - an endpoint without its own PubNub client fails to start unless publishKey, secretKey and authKey are all set ("Parameter specified as non-null is null")

[CAMEL-25280](https://issues.apache.org/jira/browse/CAMEL-25280)

camel-snmp - concurrent exchanges on one endpoint share the producer's request PDU, so a GET\_NEXT walk can silently return another walk's subtree or an incomplete result

[CAMEL-25279](https://issues.apache.org/jira/browse/CAMEL-25279)

camel-knative - a consumer with reply=false answers 204 No Content when the route fails, so Knative takes the event as delivered

[CAMEL-25278](https://issues.apache.org/jira/browse/CAMEL-25278)

camel-cometd - a stopped consumer stays subscribed to its channel (each message is processed twice after a route restart), and the extensions and server listeners are added again for every producer and consumer

[CAMEL-25277](https://issues.apache.org/jira/browse/CAMEL-25277)

camel-nats - a request to an InOut consumer whose route fails gets a successful reply with the body of the failed exchange (usually its own request)

[CAMEL-25276](https://issues.apache.org/jira/browse/CAMEL-25276)

camel-pubnub - a consumer receives the messages of the other channels of a shared PubNub client, every route restart adds another listener (messages received twice), and removing a route destroys the shared client

[CAMEL-25275](https://issues.apache.org/jira/browse/CAMEL-25275)

camel-consul - the key/value and event consumers stop watching for good after one failed query, while the route stays started

[CAMEL-25274](https://issues.apache.org/jira/browse/CAMEL-25274)

camel-dapr - the pub/sub consumer acknowledges every event with SUCCESS before the route has processed it, so Dapr drops the events whose route fails

[CAMEL-25273](https://issues.apache.org/jira/browse/CAMEL-25273)

camel-kubernetes - the watch consumers stop receiving events for good when the Kubernetes client closes their watch with an error (410 Gone), while the route stays started

[CAMEL-25272](https://issues.apache.org/jira/browse/CAMEL-25272)

camel-rocketmq - the consumer acknowledges the message of a failed exchange (the message is lost), and an InOut send without replyToTopic completes successfully when the send fails

[CAMEL-25262](https://issues.apache.org/jira/browse/CAMEL-25262)

xtokenize via dynamic language: in YAML DSL NPEs

[CAMEL-25255](https://issues.apache.org/jira/browse/CAMEL-25255)

camel-yaml-io / camel-java-io - model writers: rests, route templates, interceptors and error handlers not written as their DSL loads them

[CAMEL-25253](https://issues.apache.org/jira/browse/CAMEL-25253)

camel-dynamic-router - updating a subscription is ignored when the priority is unchanged, and duplicates the subscription when the priority changes

[CAMEL-25252](https://issues.apache.org/jira/browse/CAMEL-25252)

camel-timer - stopping a timer consumer with a negative delay releases the shared java.util.Timer it never took, which cancels the timer of the other routes with the same timer name (they stay Started but never fire again)

[CAMEL-25251](https://issues.apache.org/jira/browse/CAMEL-25251)

camel-coap - the producer completes the exchange successfully when the CoAP server does not respond (timeout or rejected request), so the message is silently lost

[CAMEL-25250](https://issues.apache.org/jira/browse/CAMEL-25250)

camel-grpc - with the AGGREGATION or PROPAGATION consumer strategy a failed exchange is answered with its message body as a successful response instead of an error

[CAMEL-25249](https://issues.apache.org/jira/browse/CAMEL-25249)

camel-vertx - a request/reply over the event bus gets a successful reply (usually its own request) when the consumer route fails, and no reply at all when the route ends without a body

[CAMEL-25248](https://issues.apache.org/jira/browse/CAMEL-25248)

camel-undertow - a String body is always sent as UTF-8, even when the Content-Type declares another charset

[CAMEL-25247](https://issues.apache.org/jira/browse/CAMEL-25247)

camel-thrift - the consumer does not send a route failure to the client: the synchronous server ignores it, the asynchronous server writes both the error and a response, so the error answers the next call on the connection

[CAMEL-25246](https://issues.apache.org/jira/browse/CAMEL-25246)

camel-hazelcast - the queue consumer keeps its item listener after stop (events processed twice after a route restart), and in poll mode stops polling for good after one failed poll

[CAMEL-25245](https://issues.apache.org/jira/browse/CAMEL-25245)

camel-snmp - a GET\_NEXT walk that reaches the end of the agent's MIB view never ends, a walk can run into a neighbouring subtree, and a walk without answer returns an empty list as success

[CAMEL-25239](https://issues.apache.org/jira/browse/CAMEL-25239)

camel export: kamelet spec.dependencies missing from pom.xml when Java route builder fails to compile during silent run

[CAMEL-25238](https://issues.apache.org/jira/browse/CAMEL-25238)

camel-yaml-dsl-validator - a oneOf used twice in one file picks one winner for both, so the second place is asked for a property it does not need

[CAMEL-25230](https://issues.apache.org/jira/browse/CAMEL-25230)

camel-cli-connector - the connector thread keeps the JVM alive when the application fails to start

[CAMEL-25227](https://issues.apache.org/jira/browse/CAMEL-25227)

camel-azure-eventhubs: partition header conflict and no default header filter

[CAMEL-25224](https://issues.apache.org/jira/browse/CAMEL-25224)

camel-xslt / camel-xslt-saxon: implicitly converted DOM sources select wrong XSLT context node

[CAMEL-25222](https://issues.apache.org/jira/browse/CAMEL-25222)

Route dump - YAML with source locations loses the list dash of a choice when, and throwException given an exception instance is dumped empty

[CAMEL-25221](https://issues.apache.org/jira/browse/CAMEL-25221)

camel-couchbase: consumerProcessedStrategy=delete removes the document before the route runs, so an undelivered row is lost

[CAMEL-25218](https://issues.apache.org/jira/browse/CAMEL-25218)

camel-jsonpath - jsonpath on a file from the ftp or ftps consumer with the charset option fails with ClassCastException (FTPFile cannot be cast to java.io.File)

[CAMEL-25217](https://issues.apache.org/jira/browse/CAMEL-25217)

camel-platform-http-vertx - a String response body is always written as UTF-8, even when the response Content-Type declares another charset (for example charset=ISO-8859-1), so the client decodes it wrongly

[CAMEL-25216](https://issues.apache.org/jira/browse/CAMEL-25216)

camel-redis - RedisAggregationRepository recovers a completed exchange without the message that completed the group

[CAMEL-25215](https://issues.apache.org/jira/browse/CAMEL-25215)

camel-ehcache, camel-jcache - EhcacheKeyValueRepository and JCacheKeyValueRepository use the non-atomic default putIfAbsent, so KeyValueIdempotentRepository can add the same message id twice

[CAMEL-25214](https://issues.apache.org/jira/browse/CAMEL-25214)

camel-hl7 - HL7DataFormat decodes and encodes messages with MSH-18 = 8859/6, 8859/7, 8859/8, 8859/9 or 8859/15 in the wrong charset, and fails for GB 18030-2000 (wrong entries in HL7Charset)

[CAMEL-25213](https://issues.apache.org/jira/browse/CAMEL-25213)

camel-support - FileStateRepository can lose the stored offsets: stop rewrites the file without the lock, the rewrite truncates the file first, and an incomplete line prevents a restart

[CAMEL-25212](https://issues.apache.org/jira/browse/CAMEL-25212)

camel-infinispan - InfinispanEmbeddedClusterView and InfinispanRemoteClusterView stop refreshing the leadership after one exception, and keep the local member as leader when the view is stopped

[CAMEL-25211](https://issues.apache.org/jira/browse/CAMEL-25211)

camel-hazelcast - the aggregation repositories recover a completed exchange without the message that completed the group, and ReplicatedHazelcastAggregationRepository fails to complete any group with recovery enabled

[CAMEL-25210](https://issues.apache.org/jira/browse/CAMEL-25210)

camel-cassandraql - CassandraAggregationRepository hands aggregations that are still open to the recover task, which sends and then deletes them, and a completed exchange that failed is never recovered

[CAMEL-25209](https://issues.apache.org/jira/browse/CAMEL-25209)

camel-kubernetes - a failed Lease renewal stops the KubernetesLeadershipController for good: the leader gives up its routes and no other pod takes over

[CAMEL-25194](https://issues.apache.org/jira/browse/CAMEL-25194)

The tools cannot author a custom Kamelet: the validator checks a .kamelet.yaml against the route schema

[CAMEL-25188](https://issues.apache.org/jira/browse/CAMEL-25188)

camel-util - URISupport.normalizeUri alternates between + and %20 for a space in a query value

[CAMEL-25179](https://issues.apache.org/jira/browse/CAMEL-25179)

camel-crypto - CryptoDataFormat with the default HMAC cannot unmarshal a message larger than its buffer size (4096 bytes): ArrayIndexOutOfBoundsException in HMACAccumulator.CircularBuffer

[CAMEL-25172](https://issues.apache.org/jira/browse/CAMEL-25172)

camel-couchbase: persistTo=2 is rejected although PersistTo.TWO exists, by a message that says 0 to 4 are supported

[CAMEL-25171](https://issues.apache.org/jira/browse/CAMEL-25171)

camel-couchbase: the consumer discards route failures, and with consumerProcessedStrategy=delete the document is already gone

[CAMEL-25170](https://issues.apache.org/jira/browse/CAMEL-25170)

camel-couchbase: connectTimeout is silently ignored unless queryTimeout is also changed

[CAMEL-25169](https://issues.apache.org/jira/browse/CAMEL-25169)

camel-couchbase: the Couchbase connection is never closed - core().shutdown() returns a cold Mono that is discarded

[CAMEL-25168](https://issues.apache.org/jira/browse/CAMEL-25168)

camel-openapi-validator: a repeated request header is validated as the text of a Java collection

[CAMEL-25167](https://issues.apache.org/jira/browse/CAMEL-25167)

Large payloads - consistent body length detection and streaming charset conversion in file / object-storage producers

[CAMEL-25165](https://issues.apache.org/jira/browse/CAMEL-25165)

camel-spring-redis - SpringRedisIdempotentRepository.remove() returns true also when the key was not in the repository

[CAMEL-25164](https://issues.apache.org/jira/browse/CAMEL-25164)

camel-infinispan - the aggregation repositories recover a completed exchange without the message that completed the group

[CAMEL-25160](https://issues.apache.org/jira/browse/CAMEL-25160)

camel-mongodb - harden the persistent tail tracking manager

[CAMEL-25159](https://issues.apache.org/jira/browse/CAMEL-25159)

camel-mongodb - findAll, distinct and aggregate execute their query twice

[CAMEL-25157](https://issues.apache.org/jira/browse/CAMEL-25157)

camel-java-io - LwModelToJavaDumper writes invalid Java for some routes

[CAMEL-25156](https://issues.apache.org/jira/browse/CAMEL-25156)

camel-caffeine - CaffeineIdempotentRepository.add() is a check-then-put, so two concurrent exchanges with the same message id both pass the Idempotent Consumer

[CAMEL-25155](https://issues.apache.org/jira/browse/CAMEL-25155)

camel-spring-redis - SpringRedisIdempotentRepository.add() checks the key and adds it in two round trips and ignores the SADD result, so the same message id is processed by two consumers at the same time

[CAMEL-25154](https://issues.apache.org/jira/browse/CAMEL-25154)

camel-vertx-http - a file body that is not a local java.io.File (such as a file from ftp, sftp or smb) is never sent and the exchange never completes, so the route hangs (regression of CAMEL-22044)

[CAMEL-25153](https://issues.apache.org/jira/browse/CAMEL-25153)

camel-caffeine, camel-ehcache - the aggregation repositories hand aggregations that are still open to the recover task, so incomplete groups are sent on as redelivered exchanges, and a completed exchange that failed is never recovered

[CAMEL-25152](https://issues.apache.org/jira/browse/CAMEL-25152)

camel-bindy - fixed-length marshal pads and clips fields in UTF-16 chars while unmarshal counts code points (or graphemes), so a record with an emoji or other non-BMP character is written one pad short and read back shifted

[CAMEL-25151](https://issues.apache.org/jira/browse/CAMEL-25151)

camel-bindy - a java.util.Date field rejects a valid value that is longer than its pattern (M/d/yyyy with 12/25/2026, h:mm a, MMMM), so Bindy cannot read back dates it has written

[CAMEL-25150](https://issues.apache.org/jira/browse/CAMEL-25150)

camel-bindy - with quotingEscaped=true a CSV field whose value ends with a quote (He said "hi", 12") is not closed on unmarshal, so it swallows the next fields and the columns shift (regression of CAMEL-22068)

[CAMEL-25140](https://issues.apache.org/jira/browse/CAMEL-25140)

camel-core - interceptSendToEndpoint: the interceptor belongs to one route, so removing that route breaks the other routes, and the interception is lost on a CamelContext restart

[CAMEL-25139](https://issues.apache.org/jira/browse/CAMEL-25139)

camel-opa - failOpen allows the exchange when OPA answered (undefined decision, rejected request), not only when it is unavailable

[CAMEL-25137](https://issues.apache.org/jira/browse/CAMEL-25137)

ArrayIndexOutOfBoundsException: Index -1 when MLLP message starts with segment delimiter

[CAMEL-25135](https://issues.apache.org/jira/browse/CAMEL-25135)

camel-core - routeConfiguration onCompletion is skipped in the Java DSL

[CAMEL-25133](https://issues.apache.org/jira/browse/CAMEL-25133)

camel-http-common - a non-chunked response over 2 GiB gets a wrong Content-Length

[CAMEL-25131](https://issues.apache.org/jira/browse/CAMEL-25131)

Match header names in any case in components

[CAMEL-25130](https://issues.apache.org/jira/browse/CAMEL-25130)

camel-sql - JdbcAggregationRepository with optimistic locking: add() ignores the old exchange, so a group completed meanwhile is stored again (duplicates) and a new group can be overwritten (lost messages)

[CAMEL-25129](https://issues.apache.org/jira/browse/CAMEL-25129)

camel-resilience4j - Circuit Breaker EIP: with timeout enabled, the bulkhead permit is released when the call times out while the call keeps running, so bulkheadMaxConcurrentCalls is not enforced

[CAMEL-25128](https://issues.apache.org/jira/browse/CAMEL-25128)

camel-netty - with a TimeoutCorrelationManagerSupport correlation manager, a failed write and the request timeout both complete the exchange, so it is completed twice

[CAMEL-25127](https://issues.apache.org/jira/browse/CAMEL-25127)

camel-syslog - valid RFC 5424 messages fail or are misparsed: no MSG (RFC 5424 example 4) throws BufferUnderflowException, an escaped '\]' ends the structured data, a NILVALUE timestamp throws

[CAMEL-25126](https://issues.apache.org/jira/browse/CAMEL-25126)

camel-syslog - the syslog data format decodes every byte as ISO-8859-1, so non-ASCII text (UTF-8 MSG and structured data values) is corrupted, and the endpoint encoding option does not help

[CAMEL-25125](https://issues.apache.org/jira/browse/CAMEL-25125)

camel-mllp - automatic acknowledgement fails with ArrayIndexOutOfBoundsException when MSH-2 defines a component separator other than '^', so no ACK is sent (regression of CAMEL-22421)

[CAMEL-25124](https://issues.apache.org/jira/browse/CAMEL-25124)

camel-core - Aggregate EIP keeps bodies that stream caching spooled to disk, but their spool files are deleted when the incoming exchanges complete, so the aggregated message cannot be read (NoSuchFileException)

[CAMEL-25123](https://issues.apache.org/jira/browse/CAMEL-25123)

camel-seda - a message that is discarded (discardWhenFull) or not added to a full queue loses the on completions of its exchange, so a file consumer never commits or rolls back the file

[CAMEL-25122](https://issues.apache.org/jira/browse/CAMEL-25122)

camel-sjms - InOut: when the send fails, the request timeout completes the exchange a second time (the reply handler is registered before the send and never cancelled)

[CAMEL-25121](https://issues.apache.org/jira/browse/CAMEL-25121)

camel-util - StringQuoteHelper.splitSafeQuote trims the spaces inside a quoted value unless it is the last value

[CAMEL-25118](https://issues.apache.org/jira/browse/CAMEL-25118)

camel-catalog - Endpoint and configuration validation: fix bugs found in a deep review

[CAMEL-25117](https://issues.apache.org/jira/browse/CAMEL-25117)

camel-spring-xml - XML camelContext configuration and JAXB dumper: fix bugs found in a deep review

[CAMEL-25116](https://issues.apache.org/jira/browse/CAMEL-25116)

camel-main - /q/download?classpath=true does not list project resources

[CAMEL-25115](https://issues.apache.org/jira/browse/CAMEL-25115)

camel-core - Error handler failure paths: fix bugs found in a deep review

[CAMEL-25114](https://issues.apache.org/jira/browse/CAMEL-25114)

camel-core - doTry, doCatch and doFinally: fix bugs found in a deep review

[CAMEL-25113](https://issues.apache.org/jira/browse/CAMEL-25113)

camel-core - onException configuration: fix bugs found in a deep review

[CAMEL-25111](https://issues.apache.org/jira/browse/CAMEL-25111)

camel-core - Properties component: fix bugs found in a deep review

[CAMEL-25110](https://issues.apache.org/jira/browse/CAMEL-25110)

camel-core - Property placeholder parser: fix bugs found in a deep review

[CAMEL-25109](https://issues.apache.org/jira/browse/CAMEL-25109)

camel-core - Scheduled poll consumer: fix bugs found in a deep review

[CAMEL-25108](https://issues.apache.org/jira/browse/CAMEL-25108)

camel-core - Component, endpoint and consumer base classes: fix bugs found in a deep review

[CAMEL-25107](https://issues.apache.org/jira/browse/CAMEL-25107)

camel-core - SSLContextParameters ignores the configured named groups when the list has a duplicate or blank value

[CAMEL-25106](https://issues.apache.org/jira/browse/CAMEL-25106)

camel-kafka - sslContextParameters ignores the SSL endpoint options and does not use the SSL security protocol

[CAMEL-25105](https://issues.apache.org/jira/browse/CAMEL-25105)

camel-netty - The client authentication of sslContextParameters is overridden by needClientAuth=false

[CAMEL-25103](https://issues.apache.org/jira/browse/CAMEL-25103)

camel-vertx - Client authentication, cipher suites and protocols of SSLContextParameters are not applied

[CAMEL-25102](https://issues.apache.org/jira/browse/CAMEL-25102)

camel-core - JSSE utility and camel.ssl configuration: fix bugs found in a deep review

[CAMEL-25101](https://issues.apache.org/jira/browse/CAMEL-25101)

camel-main - The "Property not auto-configured" warnings are never logged

[CAMEL-25100](https://issues.apache.org/jira/browse/CAMEL-25100)

camel-core - OnCompletion EIP (default after-consumer mode) cannot read a body spooled to disk by stream caching, as the spool file is deleted before the onCompletion runs

[CAMEL-25099](https://issues.apache.org/jira/browse/CAMEL-25099)

camel-main - Configuration options not applied: fix bugs found in a deep review

[CAMEL-25098](https://issues.apache.org/jira/browse/CAMEL-25098)

camel-main - Bootstrap, profiles and duration options: fix bugs found in a deep review

[CAMEL-25097](https://issues.apache.org/jira/browse/CAMEL-25097)

camel-main - Route loading, route reload and startup conditions: fix bugs found in a deep review

[CAMEL-25095](https://issues.apache.org/jira/browse/CAMEL-25095)

camel-jms - InOut: a send that fails after the request timeout or the reply has completed the exchange completes it a second time

[CAMEL-25094](https://issues.apache.org/jira/browse/CAMEL-25094)

camel-seda, camel-disruptor - a message sent InOnly to seda: or disruptor: from inside a Multicast or Split loses its spooled stream cache file when the parent exchange completes

[CAMEL-25092](https://issues.apache.org/jira/browse/CAMEL-25092)

Property binding: nested list elements are appended, not created at their index, so a list of 11 or more beans or a list with gaps silently loses elements; the documented list key last fails

[CAMEL-25090](https://issues.apache.org/jira/browse/CAMEL-25090)

camel-core - Event notifiers and vault configuration: fix bugs found in a deep review

[CAMEL-25089](https://issues.apache.org/jira/browse/CAMEL-25089)

camel-cluster - Clustered route policy and file lock cluster: fix bugs found in a deep review

[CAMEL-25088](https://issues.apache.org/jira/browse/CAMEL-25088)

camel-health - Health checks: fix bugs found in a deep review

[CAMEL-25086](https://issues.apache.org/jira/browse/CAMEL-25086)

camel-platform-http-starter: fails to start outside a servlet web application (ServerProperties/WebMvcProperties)

[CAMEL-25085](https://issues.apache.org/jira/browse/CAMEL-25085)

Rest DSL: under json/xml binding a response without Content-Type ignores the verb's produces

[CAMEL-25084](https://issues.apache.org/jira/browse/CAMEL-25084)

camel-util - String, time, URI and file helpers: fix bugs found in a deep review

[CAMEL-25083](https://issues.apache.org/jira/browse/CAMEL-25083)

camel-support - ObjectHelper type coercion and iterators: fix bugs found in a deep review

[CAMEL-25082](https://issues.apache.org/jira/browse/CAMEL-25082)

camel-disruptor - a request/reply timeout marks the caller's exchange as ignored, so a redelivery or fallback to disruptor is dropped

[CAMEL-25081](https://issues.apache.org/jira/browse/CAMEL-25081)

camel-bean - a comma inside ${...} in the method parameters splits the parameter, so OGNL calls with several arguments fail (e.g. ${body.substring(0, 2)})

[CAMEL-25079](https://issues.apache.org/jira/browse/CAMEL-25079)

camel-yaml-io, camel-java-io - Route dumpers produce invalid YAML and Java: fix bugs found in a deep review

[CAMEL-25078](https://issues.apache.org/jira/browse/CAMEL-25078)

camel-xml-jaxp - XML type converters: fix bugs found in a deep review

[CAMEL-25077](https://issues.apache.org/jira/browse/CAMEL-25077)

camel-xml-io - XML DSL parser and dumper: fix bugs found in a deep review

[CAMEL-25076](https://issues.apache.org/jira/browse/CAMEL-25076)

camel-mcp-server - stdio: adding a tool fails when stdin is closed, which breaks StdioMcpServerEngineTest

[CAMEL-25073](https://issues.apache.org/jira/browse/CAMEL-25073)

camel-management - MBean registration: follow-ups from the deep review

[CAMEL-25072](https://issues.apache.org/jira/browse/CAMEL-25072)

camel-management - EIP and service MBeans: follow-ups from the deep review

[CAMEL-25071](https://issues.apache.org/jira/browse/CAMEL-25071)

camel-management - Route and CamelContext MBeans: follow-ups from the deep review

[CAMEL-25070](https://issues.apache.org/jira/browse/CAMEL-25070)

camel-core - Stream caching strategy is not stopped after a CamelContext restart

[CAMEL-25069](https://issues.apache.org/jira/browse/CAMEL-25069)

camel-core - Rest DSL: follow-ups from the deep review

[CAMEL-25067](https://issues.apache.org/jira/browse/CAMEL-25067)

camel-core - Reifiers: follow-ups from the deep review

[CAMEL-25065](https://issues.apache.org/jira/browse/CAMEL-25065)

camel-management - Processor statistics freeze after a route restart, and ContextOnly context statistics stay 0

[CAMEL-25064](https://issues.apache.org/jira/browse/CAMEL-25064)

camel-management - EIP and service MBeans: fix bugs found in a deep review

[CAMEL-25063](https://issues.apache.org/jira/browse/CAMEL-25063)

camel-management - Route and CamelContext MBeans: fix bugs found in a deep review

[CAMEL-25062](https://issues.apache.org/jira/browse/CAMEL-25062)

camel-cluster - ClusteredRoutePolicy: CamelContext stop or removeRoute can deadlock with a leadership change that is starting routes (follow-up to CAMEL-24545)

[CAMEL-25061](https://issues.apache.org/jira/browse/CAMEL-25061)

camel-file - FileLockClusterService: after the service is stopped and started again, the node can never become the leader again (cluster data tasks are rejected)

[CAMEL-25060](https://issues.apache.org/jira/browse/CAMEL-25060)

Property placeholders: an optional circular reference such as timeout={{?timeout:5000}} makes the parser loop for ever (CamelContext start hangs at 100 % CPU)

[CAMEL-25059](https://issues.apache.org/jira/browse/CAMEL-25059)

CaseInsensitiveMap (message headers) since 4.21: keySet().remove(o) and removeAll(c) are case-sensitive, so they no longer remove a header stored with another case

[CAMEL-25057](https://issues.apache.org/jira/browse/CAMEL-25057)

camel-console - Dev consoles: fix bugs found in a deep review

[CAMEL-25056](https://issues.apache.org/jira/browse/CAMEL-25056)

camel-core - Backlog debugger and tracer: fix bugs found in a deep review

[CAMEL-25055](https://issues.apache.org/jira/browse/CAMEL-25055)

camel-core - Error registry: fix bugs found in a deep review

[CAMEL-25053](https://issues.apache.org/jira/browse/CAMEL-25053)

camel-core - Stream Resequence EIP stops delivering after its route is stopped and started while a message waits for its timeout, and callers waiting for capacity are not released on stop

[CAMEL-25052](https://issues.apache.org/jira/browse/CAMEL-25052)

camel-file - FileLockClusterView: stopping the view no longer ends a leadership check that is already running (regression from CAMEL-22784), so a stopped view can take the cluster lock, and a quick restart doubles the checks

[CAMEL-25051](https://issues.apache.org/jira/browse/CAMEL-25051)

Message headers since 4.21: a header set as content-type is stored and sent on as Content-Type (CaseInsensitiveMap replaces the key with a known key of another case)

[CAMEL-25048](https://issues.apache.org/jira/browse/CAMEL-25048)

camel-core - Route templates: fix bugs found in a deep review

[CAMEL-25047](https://issues.apache.org/jira/browse/CAMEL-25047)

camel-core - Reifiers and error handler: fix bugs found in a deep review

[CAMEL-25046](https://issues.apache.org/jira/browse/CAMEL-25046)

camel-core - Rest DSL: fix bugs found in a deep review

[CAMEL-25045](https://issues.apache.org/jira/browse/CAMEL-25045)

camel-core - Java DSL builders: fix bugs found in a deep review

[CAMEL-25044](https://issues.apache.org/jira/browse/CAMEL-25044)

camel-core - ExpressionBuilder and PredicateBuilder: fix bugs found in a deep review

[CAMEL-25043](https://issues.apache.org/jira/browse/CAMEL-25043)

camel-core - Tokenize language: fix bugs found in a deep review

[CAMEL-25042](https://issues.apache.org/jira/browse/CAMEL-25042)

Dev mode reload: the scan should skip dot directories, so camel-jbang's own state file does not reload the routes

[CAMEL-25038](https://issues.apache.org/jira/browse/CAMEL-25038)

camel-disruptor - request/reply: a late reply is written into the caller's exchange after ExchangeTimedOutException, and an interrupted wait reports success (same bugs as CAMEL-24947 / CAMEL-24948 for seda)

[CAMEL-25037](https://issues.apache.org/jira/browse/CAMEL-25037)

camel-support - an interrupted EventDrivenPollingConsumer.receive() never returns: it loops at 100 % CPU and logs a WARN on every iteration (regression of CAMEL-20297, 4.4)

[CAMEL-25036](https://issues.apache.org/jira/browse/CAMEL-25036)

camel-support - EventDrivenPollingConsumer.receive() holds the service lifecycle lock while it waits, so stopping a ConsumerTemplate, a pollEnrich route or the CamelContext hangs forever (regression in 4.8)

[CAMEL-25035](https://issues.apache.org/jira/browse/CAMEL-25035)

variableReceive keeps the header variables of an earlier message when the same variable receives again

[CAMEL-25034](https://issues.apache.org/jira/browse/CAMEL-25034)

convertBodyTo(type, charset) ignores the charset when the message has a CamelCharsetName header, and leaves it on the exchange when the conversion fails

[CAMEL-25033](https://issues.apache.org/jira/browse/CAMEL-25033)

camel-bean: a parameter bound from ${body} or ${header.x} in the method name loses its surrounding quotes, and the text "null" becomes a Java null

[CAMEL-25032](https://issues.apache.org/jira/browse/CAMEL-25032)

Dev mode: a route saved together with a property it uses fails to reload and keeps running the previous version

[CAMEL-25026](https://issues.apache.org/jira/browse/CAMEL-25026)

camel-package-maven-plugin - @Metadata(security/secret) is dropped for model, dataformat and language options

[CAMEL-25025](https://issues.apache.org/jira/browse/CAMEL-25025)

camel-mongodb - a change stream event with a non-ObjectId \_id loops the consumer forever

[CAMEL-25024](https://issues.apache.org/jira/browse/CAMEL-25024)

camel-mongodb - the consumers discard a failed exchange and advance past it

[CAMEL-25023](https://issues.apache.org/jira/browse/CAMEL-25023)

camel-util - IOHelper.copy counts copied bytes in an int, so zipFile/tarFile maxDecompressedSize values of 2 GiB or more are not enforced

[CAMEL-25020](https://issues.apache.org/jira/browse/CAMEL-25020)

camel-sql - observability still reports the CamelSqlQuery header when useMessageBodyForSql=true

[CAMEL-25018](https://issues.apache.org/jira/browse/CAMEL-25018)

ThrottlingInflightRoutePolicy and ThrottlingExceptionRoutePolicy resume a consumer that the route controller suspended: suspendRoute is not honoured and a graceful stop keeps consuming until the timeout

[CAMEL-25017](https://issues.apache.org/jira/browse/CAMEL-25017)

Claim Check EIP: Split/Multicast/Recipient List/Wire Tap/SEDA copies share the parent's claim check repository, so parallel parts get each other's messages back

[CAMEL-25016](https://issues.apache.org/jira/browse/CAMEL-25016)

Remote file consumers (FTP, FTPS, SFTP, SMB, Azure Files): with noop=true or idempotent=true, a file whose download fails is never retried

[CAMEL-25014](https://issues.apache.org/jira/browse/CAMEL-25014)

ThrottlingExceptionRoutePolicy: since CAMEL-24903 the circuit stays open forever when the halfOpenHandler is not ready once, and keepOpen no longer suspends the consumer after a route restart

[CAMEL-25013](https://issues.apache.org/jira/browse/CAMEL-25013)

Simple and PredicateBuilder comparisons truncate decimals when the two numbers have different types: ${header.amount} > 100 is false for a BigDecimal 100.50, and 2.5 == 2 is true

[CAMEL-25012](https://issues.apache.org/jira/browse/CAMEL-25012)

OnCompletion EIP with parallelProcessing: a graceful shutdown drops the queued onCompletion tasks and interrupts the running ones

[CAMEL-25011](https://issues.apache.org/jira/browse/CAMEL-25011)

Saga EIP with the in-memory saga service: split, multicast, recipient list and wire tap sub-exchanges lose the saga (MANDATORY fails, REQUIRED completes independent sagas)

[CAMEL-25010](https://issues.apache.org/jira/browse/CAMEL-25010)

Supervising route controller: a restart attempt that is already running starts the route after stopRoute() cancelled it

[CAMEL-25009](https://issues.apache.org/jira/browse/CAMEL-25009)

camel-core - Bean binding: @PropertyInject hides an invalid value, and overloaded constructors are not found

[CAMEL-25008](https://issues.apache.org/jira/browse/CAMEL-25008)

Supervising route controller deadlocks when a route is stopped or started while its restart attempt completes

[CAMEL-25007](https://issues.apache.org/jira/browse/CAMEL-25007)

Supervising route controller: a cancelled restart task completes a second time and removes the route's new restart task, which then restarts the route unsupervised

[CAMEL-25006](https://issues.apache.org/jira/browse/CAMEL-25006)

In-memory Saga: after a saga timed out, a REQUIRED step on the same exchange silently starts and completes a new saga (SUPPORTS runs outside any saga)

[CAMEL-25005](https://issues.apache.org/jira/browse/CAMEL-25005)

In-memory Saga: a step that joins while the saga is being completed, compensated or timed out is reported as joined, but its compensation/completion never runs

[CAMEL-25004](https://issues.apache.org/jira/browse/CAMEL-25004)

camel-core - Producer cache and stream caching: fix lifecycle bugs found in a deep review

[CAMEL-25003](https://issues.apache.org/jira/browse/CAMEL-25003)

camel-core - ServicePool hands out a stopped non-singleton producer after LRU eviction, and stops producers in use

[CAMEL-25002](https://issues.apache.org/jira/browse/CAMEL-25002)

Loop EIP: a negative or very large loop count makes graceful shutdown stop without waiting for inflight exchanges

[CAMEL-25001](https://issues.apache.org/jira/browse/CAMEL-25001)

camel-core - Supervising route controller: an exhausted route stays unhealthy after it is started manually

[CAMEL-25000](https://issues.apache.org/jira/browse/CAMEL-25000)

camel-ai-tool / camel-ai-resource - tools and resources are missing when a route sends a request as soon as it starts

[CAMEL-24997](https://issues.apache.org/jira/browse/CAMEL-24997)

camel-core - Reactive executor: after a nested scheduleSync, scheduled tasks run inline instead of after the current task

[CAMEL-24996](https://issues.apache.org/jira/browse/CAMEL-24996)

camel-core - Changing a header value through the entry set of a copied message changes the original message

[CAMEL-24995](https://issues.apache.org/jira/browse/CAMEL-24995)

camel-core - Wire Tap EIP: a graceful shutdown does not wait for the tapped exchanges queued in the thread pool

[CAMEL-24994](https://issues.apache.org/jira/browse/CAMEL-24994)

camel-core - Enrich and Poll Enrich EIPs: the resource on completions are lost when the enrich fails

[CAMEL-24993](https://issues.apache.org/jira/browse/CAMEL-24993)

camel-core - toD, Routing Slip and producer cache: fix bugs found in a deep review

[CAMEL-24991](https://issues.apache.org/jira/browse/CAMEL-24991)

camel-core - Aggregate EIP: fix bugs found in a deep review

[CAMEL-24990](https://issues.apache.org/jira/browse/CAMEL-24990)

camel-core - Multicast, Split and Recipient List EIPs: fix bugs found in a deep review

[CAMEL-24981](https://issues.apache.org/jira/browse/CAMEL-24981)

camel-core - Error handler keeps the onException of an earlier redelivery attempt when the exception type changes

[CAMEL-24978](https://issues.apache.org/jira/browse/CAMEL-24978)

camel-core - Internal processor advices: fix bugs found in a deep review

[CAMEL-24976](https://issues.apache.org/jira/browse/CAMEL-24976)

camel-core - Type converter: fix bugs found in a deep review

[CAMEL-24973](https://issues.apache.org/jira/browse/CAMEL-24973)

camel-util - URISupport.sanitizeUri does not follow the endpoint URI parser for RAW values, userinfo, dash-case option names and additional keywords

[CAMEL-24960](https://issues.apache.org/jira/browse/CAMEL-24960)

Multicast/Split/RecipientList with parallelProcessing hangs forever when the thread pool rejects a sub-exchange task

[CAMEL-24959](https://issues.apache.org/jira/browse/CAMEL-24959)

Split with streaming and parallelProcessing completes before its parts and loses the aggregated result when the iterator returns null after hasNext()=true

[CAMEL-24958](https://issues.apache.org/jira/browse/CAMEL-24958)

Recipient List does not release the producers (and prototype endpoints) of recipients that were not sent to (stopOnException, timeout)

[CAMEL-24954](https://issues.apache.org/jira/browse/CAMEL-24954)

Stopping a route with an Idempotent Consumer stops and clears a repository that other running routes still use

[CAMEL-24953](https://issues.apache.org/jira/browse/CAMEL-24953)

Idempotent Consumer with skipDuplicate=false: a duplicate that fails removes the message id that the original exchange added

[CAMEL-24952](https://issues.apache.org/jira/browse/CAMEL-24952)

camel-seda - virtualThreadPerTask consumer: graceful stop does not wait for polled exchanges whose task has not started yet

[CAMEL-24951](https://issues.apache.org/jira/browse/CAMEL-24951)

Stopping a suspended SEDA route (or the CamelContext) with queued messages always waits for the full shutdown timeout

[CAMEL-24950](https://issues.apache.org/jira/browse/CAMEL-24950)

camel-seda - purging the queue leaves request/reply producers waiting for exchanges that were discarded (forever with timeout=0)

[CAMEL-24949](https://issues.apache.org/jira/browse/CAMEL-24949)

camel-seda - suspending a route with purgeWhenStopping=true discards all queued messages

[CAMEL-24948](https://issues.apache.org/jira/browse/CAMEL-24948)

camel-seda - SedaProducer swallows InterruptedException and reports success: message not queued, or the request returned as the reply

[CAMEL-24947](https://issues.apache.org/jira/browse/CAMEL-24947)

camel-seda - request/reply timeout race: a late reply is copied into the caller's exchange after the producer already returned ExchangeTimedOutException

[CAMEL-24946](https://issues.apache.org/jira/browse/CAMEL-24946)

KeyValueAggregationRepository stores the previous state of the group for recovery, so a recovered exchange misses the last aggregated message

[CAMEL-24945](https://issues.apache.org/jira/browse/CAMEL-24945)

Aggregate EIP: with optimistic locking a group can lose its completion timeout and never complete

[CAMEL-24944](https://issues.apache.org/jira/browse/CAMEL-24944)

Aggregate EIP: with optimistic locking and a pre-completing AggregationStrategy, a completed group can be lost

[CAMEL-24943](https://issues.apache.org/jira/browse/CAMEL-24943)

Aggregate EIP: the recover task can re-deliver an aggregated exchange that is being completed normally, which sends it twice

[CAMEL-24942](https://issues.apache.org/jira/browse/CAMEL-24942)

camel-seda - multipleConsumers=true silently load-balances instead of broadcasting when the consumer URIs differ in any other option

[CAMEL-24941](https://issues.apache.org/jira/browse/CAMEL-24941)

Aggregate EIP: with closeCorrelationKeyOnCompletion an exchange that arrives while its group is being completed starts a new group for the closed key

[CAMEL-24940](https://issues.apache.org/jira/browse/CAMEL-24940)

camel-jbang/cli - autodetection of Kubernetes property placeholder functions (configmap:, secret:) stopped working in 4.22.1

[CAMEL-24935](https://issues.apache.org/jira/browse/CAMEL-24935)

camel-pulsar - the producer replaces the message body with the MessageId

[CAMEL-24934](https://issues.apache.org/jira/browse/CAMEL-24934)

camel-pulsar - a failed acknowledgement is reported without its cause

[CAMEL-24933](https://issues.apache.org/jira/browse/CAMEL-24933)

camel-pulsar - the consumer leaks a pooled exchange for every message

[CAMEL-24932](https://issues.apache.org/jira/browse/CAMEL-24932)

camel-pulsar - the polling loop dies on a NullPointerException when a receive fails

[CAMEL-24929](https://issues.apache.org/jira/browse/CAMEL-24929)

RedeliveryPolicy javadoc shows a malformed delayPattern example

[CAMEL-24928](https://issues.apache.org/jira/browse/CAMEL-24928)

Throttle EIP with asyncDelayed fails with NullPointerException when the maximum requests is 0

[CAMEL-24927](https://issues.apache.org/jira/browse/CAMEL-24927)

Sample EIP drops every message until the machine's uptime exceeds the sample period

[CAMEL-24926](https://issues.apache.org/jira/browse/CAMEL-24926)

throttle(n).concurrentRequestsMode() lets more than n exchanges in when one of them takes longer than 10 seconds

[CAMEL-24925](https://issues.apache.org/jira/browse/CAMEL-24925)

onException redeliveryDelay("5s") fails at runtime with "Error parsing \[5s\] as a java.lang.Long"

[CAMEL-24924](https://issues.apache.org/jira/browse/CAMEL-24924)

Failover load balancer with no processors never completes the exchange, so the caller hangs

[CAMEL-24923](https://issues.apache.org/jira/browse/CAMEL-24923)

Weighted load balancer accepts negative, all-zero or overflowing distribution ratios, and the caller then hangs

[CAMEL-24922](https://issues.apache.org/jira/browse/CAMEL-24922)

Failover load balancer in sticky mode without round robin never tries the endpoints before the last known good one

[CAMEL-24910](https://issues.apache.org/jira/browse/CAMEL-24910)

rest - a path parameter and an incoming HTTP header of the same name are merged into a list, so a correct value fails

[CAMEL-24891](https://issues.apache.org/jira/browse/CAMEL-24891)

camel-debezium - generated password options are not marked as secret

[CAMEL-24890](https://issues.apache.org/jira/browse/CAMEL-24890)

camel-debezium - deprecated connector options declared as String constants are still generated

[CAMEL-24889](https://issues.apache.org/jira/browse/CAMEL-24889)

camel-debezium - the consumer is never told that the embedded engine has failed

[CAMEL-24887](https://issues.apache.org/jira/browse/CAMEL-24887)

ManagedRouteGroupMBean exchange stats changed

[CAMEL-24885](https://issues.apache.org/jira/browse/CAMEL-24885)

camel-core - Simple: a resource: text with a function but no scheme ends in a StackOverflowError

[CAMEL-24883](https://issues.apache.org/jira/browse/CAMEL-24883)

camel-jbang - the validator's Simple checks skip expressions written as YAML block scalars

[CAMEL-24878](https://issues.apache.org/jira/browse/CAMEL-24878)

camel-kamelet-main - resolving an http: resource fetches it, so rest-openapi reads its specification twice

[CAMEL-24875](https://issues.apache.org/jira/browse/CAMEL-24875)

camel-jbang - camel validate yaml skips a multi-line simple expression (expression: | block scalar)

[CAMEL-24866](https://issues.apache.org/jira/browse/CAMEL-24866)

camel-support - route reload fails with duplicate route id when a new file is added next to a file with several routes

[CAMEL-24865](https://issues.apache.org/jira/browse/CAMEL-24865)

camel-jbang - camel run --source-dir breaks the Java language and the datasource auto-configure: a missing classpath resource is replaced by a file that does not exist

[CAMEL-24864](https://issues.apache.org/jira/browse/CAMEL-24864)

camel-platform-http-vertx: response write failures are discarded, leaking exchanges and SSE subscribers when a client disconnects

[CAMEL-24853](https://issues.apache.org/jira/browse/CAMEL-24853)

camel-jbang - camel export moves a Groovy script the route references as a resource: into camel-groovy, where the reference no longer resolves

[CAMEL-24848](https://issues.apache.org/jira/browse/CAMEL-24848)

camel-mail - The useHeaderFrom and other useHeaderXXXXX options defaulted to false but the document said the default should be true

[CAMEL-24845](https://issues.apache.org/jira/browse/CAMEL-24845)

Simple: the suggestion for ${jsonpath:$.status} is the same text (did you mean ${jsonpath:$.status}?); the function is ${jsonpath($.status)}

[CAMEL-24835](https://issues.apache.org/jira/browse/CAMEL-24835)

camel-file: a consumer on the current directory (file:. or file:./) never delivers a file

[CAMEL-24825](https://issues.apache.org/jira/browse/CAMEL-24825)

REST DSL from an OpenAPI contract with no servers entry fails to start with "URI is not absolute"

[CAMEL-24816](https://issues.apache.org/jira/browse/CAMEL-24816)

camel-elasticsearch/camel-opensearch: minor robustness fixes (scroll clear NPE, id header clobber, size/from header bleed)

[CAMEL-24815](https://issues.apache.org/jira/browse/CAMEL-24815)

camel-opensearch: producer ignores socketTimeout without SSL and scopes basic auth to the first host only

[CAMEL-24814](https://issues.apache.org/jira/browse/CAMEL-24814)

camel-elasticsearch/camel-opensearch: BulkRequestAggregationStrategy returns the wrong exchange, breaking bulk aggregation

[CAMEL-24813](https://issues.apache.org/jira/browse/CAMEL-24813)

camel-core: PropertiesComponent.unescape drops trailing backslash

[CAMEL-24811](https://issues.apache.org/jira/browse/CAMEL-24811)

camel-servlet - async=true without executorRef completes the AsyncContext before a truly-asynchronous route finishes

[CAMEL-24800](https://issues.apache.org/jira/browse/CAMEL-24800)

camel-core - pooled exchange copies share the parent's clock, so Splitter children are returned to the pool without reset (properties/variables leak between messages)

[CAMEL-24799](https://issues.apache.org/jira/browse/CAMEL-24799)

camel-jbang: Installing Camel Kit by command name loses the requested plugin version

[CAMEL-24792](https://issues.apache.org/jira/browse/CAMEL-24792)

camel-aws2-ddb: setHeaderIfNotPresent in Ddb2JsonDataTypeTransformer always overwrites the header

[CAMEL-24789](https://issues.apache.org/jira/browse/CAMEL-24789)

camel-vertx-websocket: the producer completes an exchange both synchronously and asynchronously when there is no peer

[CAMEL-24788](https://issues.apache.org/jira/browse/CAMEL-24788)

camel-vertx-websocket: a shared websocket host is unregistered when the first of its consumers stops

[CAMEL-24784](https://issues.apache.org/jira/browse/CAMEL-24784)

camel-opa - the REST decision call has no timeout and builds a new HttpClient per message

[CAMEL-24783](https://issues.apache.org/jira/browse/CAMEL-24783)

camel-kafka - async batch producer: in-flight callbacks can mutate a continued/recycled exchange after a mid-batch dispatch failure

[CAMEL-24782](https://issues.apache.org/jira/browse/CAMEL-24782)

camel-kafka - transactional producer can be left permanently unusable after a transaction/commit failure (no recreation, commit failure not aborted)

[CAMEL-24780](https://issues.apache.org/jira/browse/CAMEL-24780)

camel-kafka - transactional producer leaks a half-begun transaction and skips the async callback when beginTransaction fails

[CAMEL-24778](https://issues.apache.org/jira/browse/CAMEL-24778)

camel-kafka - consumer with batching=true throws NullPointerException when maxPollRecords is not set

[CAMEL-24776](https://issues.apache.org/jira/browse/CAMEL-24776)

camel-jbang run does not auto-load camel-kubernetes for secret property functions

[CAMEL-24775](https://issues.apache.org/jira/browse/CAMEL-24775)

camel-core - BeanFactoryDefinition.type is required in the schemas but optional at runtime for scripted and builder beans

[CAMEL-24771](https://issues.apache.org/jira/browse/CAMEL-24771)

camel-core - simple predicate fails to parse a } inside a quoted literal

[CAMEL-24769](https://issues.apache.org/jira/browse/CAMEL-24769)

camel-hazelcast: leftover hazelcast-atomicvalue service files after atomicvalue removal

[CAMEL-24768](https://issues.apache.org/jira/browse/CAMEL-24768)

camel-huaweicloud-dms/-iam: ineffective int-option guards (mandatory fields, proxy port) and a fragile exchange-property cast

[CAMEL-24766](https://issues.apache.org/jira/browse/CAMEL-24766)

camel-huaweicloud-smn: empty-body guard checks the raw endpoint operation instead of the resolved one

[CAMEL-24765](https://issues.apache.org/jira/browse/CAMEL-24765)

camel-huaweicloud-functiongraph: include the region in the invoke URN when endpoint is set, and read the response body robustly

[CAMEL-24764](https://issues.apache.org/jira/browse/CAMEL-24764)

camel-huaweicloud-obs: close the downloaded object stream (connection leak) and fix putObject bucket-creation, charset and proxy-port issues

[CAMEL-24754](https://issues.apache.org/jira/browse/CAMEL-24754)

camel-opa - a verdict claimed by an inbound message survives a failed evaluation

[CAMEL-24749](https://issues.apache.org/jira/browse/CAMEL-24749)

camel-core: failover load balancer ignores inheritErrorHandler=false since 4.10

[CAMEL-24748](https://issues.apache.org/jira/browse/CAMEL-24748)

Component metadata disagrees with what seven components accept (operation enums, consumer/producer labels, options without @UriParam)

[CAMEL-24747](https://issues.apache.org/jira/browse/CAMEL-24747)

KameletComponent URL encodes kamelet parameters

[CAMEL-24746](https://issues.apache.org/jira/browse/CAMEL-24746)

KameletOptimisedComponentResolver doesn't recognize kamelets registered as beans

[CAMEL-24734](https://issues.apache.org/jira/browse/CAMEL-24734)

camel-spiffe - validateJwtSvid silently validates against only the first configured audience

[CAMEL-24730](https://issues.apache.org/jira/browse/CAMEL-24730)

camel-spiffe - do not let inbound headers choose the operation or the validated audience

[CAMEL-24729](https://issues.apache.org/jira/browse/CAMEL-24729)

camel-infinispan: a lifespan set without its time unit is silently ignored

[CAMEL-24719](https://issues.apache.org/jira/browse/CAMEL-24719)

camel-weaviate: remove the dead VECTOR\_FIELD\_NAME header

[CAMEL-24718](https://issues.apache.org/jira/browse/CAMEL-24718)

camel-sql - observability (SqlTraceDevConsole, SqlSpanDecorator) surfaces the CamelSqlQuery header even when allowQueryFromHeader is disabled

[CAMEL-24717](https://issues.apache.org/jira/browse/CAMEL-24717)

camel-opa - the producer health check publishes the bearerToken in its id

[CAMEL-24716](https://issues.apache.org/jira/browse/CAMEL-24716)

camel-xmlsecurity - the cipher algorithm values listed by the model are rejected by the data format

[CAMEL-24705](https://issues.apache.org/jira/browse/CAMEL-24705)

camel-jbang - explicit CLI flags such as --max-seconds are overridden by application.properties

[CAMEL-24701](https://issues.apache.org/jira/browse/CAMEL-24701)

camel-jbang - logging.level.root in application.properties produces a second log4j root logger and breaks the CLI log layout

[CAMEL-24700](https://issues.apache.org/jira/browse/CAMEL-24700)

camel-yaml-dsl - circuitBreaker with onFallback before steps puts the steps into the fallback (Definition has no children)

[CAMEL-24697](https://issues.apache.org/jira/browse/CAMEL-24697)

camel-yaml-dsl - JSON schema rejects EIP doc examples the runtime accepts: inheritErrorHandler, resequence expression oneOf, jaxb contextPath

[CAMEL-24694](https://issues.apache.org/jira/browse/CAMEL-24694)

YAML DSL validator rejects scalar values the runtime accepts (quoted booleans/numbers and placeholders at typed attributes)

[CAMEL-24692](https://issues.apache.org/jira/browse/CAMEL-24692)

camel-catalog: validateLanguagePredicate/Expression for simple rejects property placeholders used as operands

[CAMEL-24691](https://issues.apache.org/jira/browse/CAMEL-24691)

camel-saxon - align XQueryBuilder with secure XML parsing defaults

[CAMEL-24690](https://issues.apache.org/jira/browse/CAMEL-24690)

camel-python (Jython) - PythonExpression is not thread safe

[CAMEL-24687](https://issues.apache.org/jira/browse/CAMEL-24687)

camel-quickjs - every evaluation leaks a QuickJS module; 8 threads exhaust a 1 GB heap in 22 seconds

[CAMEL-24686](https://issues.apache.org/jira/browse/CAMEL-24686)

camel-joor - headerAs/exchangePropertyAs default-value patterns match across two calls on the same line

[CAMEL-24685](https://issues.apache.org/jira/browse/CAMEL-24685)

camel-joor - an inline expression with preCompile=false compiles on every evaluation

[CAMEL-24681](https://issues.apache.org/jira/browse/CAMEL-24681)

camel-jbang: export does not include Maven repositories from properties camel.jbang.repos and camel.extra.repos

[CAMEL-24669](https://issues.apache.org/jira/browse/CAMEL-24669)

camel-groovy - groovyJson/groovyXml: support Jackson 3 nodes and fix prettyPrint=false output

[CAMEL-24668](https://issues.apache.org/jira/browse/CAMEL-24668)

Camel MLLP consumer discards pipelined HL7 messages that arrive in a single TCP read

[CAMEL-24662](https://issues.apache.org/jira/browse/CAMEL-24662)

camel-jbang: "camel kubernetes run --cluster-type X" is silently overridden by auto cluster detection

[CAMEL-24651](https://issues.apache.org/jira/browse/CAMEL-24651)

Regression on Camel 4.x NPE on evaluation of a Simple expression ${exception.stacktrace}

[CAMEL-24632](https://issues.apache.org/jira/browse/CAMEL-24632)

SSLException when GET/POST to https endpoint with proxy setting using camel-http component

[CAMEL-24630](https://issues.apache.org/jira/browse/CAMEL-24630)

camel-kamelet: supervised route reload creates duplicate internal routes and causes context console NPE

[CAMEL-24628](https://issues.apache.org/jira/browse/CAMEL-24628)

camel-cli: dependency update silently drops route files passed as positional arguments

[CAMEL-24626](https://issues.apache.org/jira/browse/CAMEL-24626)

camel-master: follow-ups to CAMEL-24583 - leadership lock, cancelled task registry entries, backoff documentation

[CAMEL-24623](https://issues.apache.org/jira/browse/CAMEL-24623)

camel-infinispan: the QUERY operation silently returns the input when no query builder is set

[CAMEL-24622](https://issues.apache.org/jira/browse/CAMEL-24622)

camel-infinispan: the aggregation repository implements RecoverableAggregationRepository without a recovery store

[CAMEL-24614](https://issues.apache.org/jira/browse/CAMEL-24614)

camel-langchain4j-agent: validate that an agent was resolved before use

[CAMEL-24613](https://issues.apache.org/jira/browse/CAMEL-24613)

camel-langchain4j-agent-api: guardrail robustness (English false-reject with allowMixed=false, no guardrail-class interface check)

[CAMEL-24612](https://issues.apache.org/jira/browse/CAMEL-24612)

camel-langchain4j-agent: content converter charset and content-type handling issues

[CAMEL-24611](https://issues.apache.org/jira/browse/CAMEL-24611)

camel-chatscript: multiple functional bugs (resetChat no-op, chatUserName ignored, no socket timeout, non-String body NPE)

[CAMEL-24610](https://issues.apache.org/jira/browse/CAMEL-24610)

camel-langchain4j-web-search: NullPointerException unboxing maxResults when a custom WebSearchRequest omits it

[CAMEL-24609](https://issues.apache.org/jira/browse/CAMEL-24609)

camel-langchain4j-agent: the managed tool-execution executor is not recreated after a stop/start cycle

[CAMEL-24608](https://issues.apache.org/jira/browse/CAMEL-24608)

camel-langchain4j-agent-api: LanguageGuardrail minLanguageRatio option is never applied

[CAMEL-24607](https://issues.apache.org/jira/browse/CAMEL-24607)

camel-langchain4j-agent-api: CodeInjectionGuardrail blocks legitimate input by counting duplicate same-type matches

[CAMEL-24606](https://issues.apache.org/jira/browse/CAMEL-24606)

camel-google-firestore: the realtime change type header is undocumented

[CAMEL-24604](https://issues.apache.org/jira/browse/CAMEL-24604)

camel-jpa - KeyValueEntry cannot be mapped by Hibernate: isExpired() lacks @Transient

[CAMEL-24594](https://issues.apache.org/jira/browse/CAMEL-24594)

RestBindingAdvice response marshalling failure is silently swallowed

[CAMEL-24593](https://issues.apache.org/jira/browse/CAMEL-24593)

camel-platform-http-starter - accepted multipart uploads are copied to the servlet temp directory and never deleted

[CAMEL-24592](https://issues.apache.org/jira/browse/CAMEL-24592)

camel-spring-boot - health check details include the full error stack trace at the default exposure level

[CAMEL-24591](https://issues.apache.org/jira/browse/CAMEL-24591)

camel-seda - Send fails with "No queue available" after producer route restart (regression from CAMEL-24408)

[CAMEL-24590](https://issues.apache.org/jira/browse/CAMEL-24590)

ManagedRouteGroupMBean.getFailuresHandled() / getLastExchangeFailureHandledTimestamp() return 0/null even though a member route recorded a handled failure

[CAMEL-24589](https://issues.apache.org/jira/browse/CAMEL-24589)

camel-platform-http-starter: stopping the second consumer on a shared path unregisters the first consumer

[CAMEL-24585](https://issues.apache.org/jira/browse/CAMEL-24585)

The catalog validateLanguageExpression returns an invoke error when using jsonpath in a simple expression

[CAMEL-24584](https://issues.apache.org/jira/browse/CAMEL-24584)

camel-support: BackgroundTask.schedule keeps re-running a task that has completed or run out of budget

[CAMEL-24583](https://issues.apache.org/jira/browse/CAMEL-24583)

camel-master: losing leadership while a consumer start is pending leaves the delegated consumer running on a non-leader node

[CAMEL-24573](https://issues.apache.org/jira/browse/CAMEL-24573)

CXF REST: UnsupportedOperationException when copying factory bean with fixed-size features list

[CAMEL-24545](https://issues.apache.org/jira/browse/CAMEL-24545)

Camel Shutdown Locked State With ZookeeprCluster Service

[CAMEL-24544](https://issues.apache.org/jira/browse/CAMEL-24544)

camel-kserve / camel-tensorflow-serving: doStop can NPE when the gRPC channel was never created

[CAMEL-24543](https://issues.apache.org/jira/browse/CAMEL-24543)

camel-langchain4j-embeddingstore: the endpoint @UriEndpoint syntax uses the wrong scheme

[CAMEL-24542](https://issues.apache.org/jira/browse/CAMEL-24542)

camel-qdrant: the PayloadSelector header is declared and advertised but never read

[CAMEL-24541](https://issues.apache.org/jira/browse/CAMEL-24541)

camel-djl: ImageNetUtil.getSynsetName can throw ArrayIndexOutOfBoundsException on synset lines without a space

[CAMEL-24540](https://issues.apache.org/jira/browse/CAMEL-24540)

camel-huggingface: revision is ignored by two task predictors and TextToImage never sets the OUTPUT header

[CAMEL-24539](https://issues.apache.org/jira/browse/CAMEL-24539)

camel-openai: embeddings/audio store their SDK response under the chat-typed RESPONSE property

[CAMEL-24538](https://issues.apache.org/jira/browse/CAMEL-24538)

camel-openai: operator-precedence bug can discard the prompt supplied in the message body

[CAMEL-24537](https://issues.apache.org/jira/browse/CAMEL-24537)

camel-openai: the chat-completion producer does not validate that a model is set

[CAMEL-24536](https://issues.apache.org/jira/browse/CAMEL-24536)

camel-langchain4j-embeddings: OpenAiEmbeddingModelBuilder never enables response logging

[CAMEL-24535](https://issues.apache.org/jira/browse/CAMEL-24535)

camel-tensorflow-serving: the Target and Credentials headers are declared but never read

[CAMEL-24534](https://issues.apache.org/jira/browse/CAMEL-24534)

camel-qdrant: the embeddings data-type transformer casts every metadata value to String

[CAMEL-24533](https://issues.apache.org/jira/browse/CAMEL-24533)

camel-weaviate: the embeddings data-type transformer drops the document text on CREATE/UPDATE

[CAMEL-24532](https://issues.apache.org/jira/browse/CAMEL-24532)

Camel Spring Boot: Preserve property-source precedence during early vault resolution

[CAMEL-24530](https://issues.apache.org/jira/browse/CAMEL-24530)

camel-djl: DJLConverter leaks the InputStream opened from File/Path bodies

[CAMEL-24529](https://issues.apache.org/jira/browse/CAMEL-24529)

camel-djl: the loaded ZooModel is never closed (native-memory leak on restart)

[CAMEL-24528](https://issues.apache.org/jira/browse/CAMEL-24528)

camel-huggingface: four task predictors swallow Python inference errors as success

[CAMEL-24527](https://issues.apache.org/jira/browse/CAMEL-24527)

camel-huggingface: authToken/oauthProfile are honored only by the CHAT task

[CAMEL-24526](https://issues.apache.org/jira/browse/CAMEL-24526)

camel-djl: the zoo linear/softmax regression predictors are unimplemented no-ops

[CAMEL-24524](https://issues.apache.org/jira/browse/CAMEL-24524)

camel-core: URISupport.normalizeUri fast path skips value encoding when parameters are already sorted, causing duplicate endpoints

[CAMEL-24523](https://issues.apache.org/jira/browse/CAMEL-24523)

camel-paho - Consumer silently stops receiving messages when resubscribe fails and route remains in Started state

[CAMEL-24521](https://issues.apache.org/jira/browse/CAMEL-24521)

camel-google: Workload Identity Federation is documented for all components but is not wired to any of them

[CAMEL-24520](https://issues.apache.org/jira/browse/CAMEL-24520)

camel-ibm-watsonx-ai: lazy service getters on WatsonxAiEndpoint are not thread-safe

[CAMEL-24519](https://issues.apache.org/jira/browse/CAMEL-24519)

camel-ibm-watsonx-ai: the ModelId header is an output but its metadata describes it as an input

[CAMEL-24518](https://issues.apache.org/jira/browse/CAMEL-24518)

camel-ibm-watson-language: analyze with all features disabled yields an opaque Watson 400

[CAMEL-24517](https://issues.apache.org/jira/browse/CAMEL-24517)

camel-ibm-cos: headBucket does not set the BucketExists producer header

[CAMEL-24512](https://issues.apache.org/jira/browse/CAMEL-24512)

camel-spring-boot - error.message is overwritten when several health checks report DOWN

[CAMEL-24511](https://issues.apache.org/jira/browse/CAMEL-24511)

camel-paho-mqtt5 - Consumer silently stops receiving messages when resubscribe fails and route remains in Started state

[CAMEL-24509](https://issues.apache.org/jira/browse/CAMEL-24509)

camel-mina - gate the exchange-holder unmarshal on transferExchange and mark objectCodecPattern as security-relevant

[CAMEL-24495](https://issues.apache.org/jira/browse/CAMEL-24495)

Authentication-type detection is not triggered via camel-salesforce-maven-plugin. It still uses grant-type USERNAME\_PASSWORD

[CAMEL-24494](https://issues.apache.org/jira/browse/CAMEL-24494)

camel-ibm-cos: fix typo in the CacheControl producer/consumer header name

[CAMEL-24493](https://issues.apache.org/jira/browse/CAMEL-24493)

camel-ibm-cos: the producer ignores multiPartUpload, partSize, storageClass and deleteAfterWrite options

[CAMEL-24491](https://issues.apache.org/jira/browse/CAMEL-24491)

camel-ibm-cos: consumer in-progress deduplication is inert, causing duplicate delivery

[CAMEL-24490](https://issues.apache.org/jira/browse/CAMEL-24490)

camel-ibm-watsonx-ai: the timeout option is never applied to the watsonx.ai service clients

[CAMEL-24488](https://issues.apache.org/jira/browse/CAMEL-24488)

camel-ibm-watson-speech-to-text: WatsonSpeechToTextProducer leaks the audio FileInputStream

[CAMEL-24486](https://issues.apache.org/jira/browse/CAMEL-24486)

camel-core - Simple language init block custom functions ($foo ~:= ...) fail with "No custom simple function" when CamelContext profile is dev

[CAMEL-24484](https://issues.apache.org/jira/browse/CAMEL-24484)

camel-file: readLockRemoveOnCommit=false is not respected when idempotent-changed/-rename/idempotent read lock fails to acquire an existing entry

[CAMEL-24483](https://issues.apache.org/jira/browse/CAMEL-24483)

camel-jbang export: explicit --dep version is ignored for auto-detected dependencies

[CAMEL-24482](https://issues.apache.org/jira/browse/CAMEL-24482)

Camel JBang YAML validator incorrectly requires all data formats inside unmarshal step

[CAMEL-24479](https://issues.apache.org/jira/browse/CAMEL-24479)

\[camel-jbang\] YAML validation incorrectly succeeds when containing invalid properties

[CAMEL-24475](https://issues.apache.org/jira/browse/CAMEL-24475)

camel-xpath - documentType=InputSource evaluates the payload with an unhardened XML parser

[CAMEL-24472](https://issues.apache.org/jira/browse/CAMEL-24472)

camel-ibm-secrets-manager: endpoint credential validation uses && so a half-configured endpoint passes

[CAMEL-24471](https://issues.apache.org/jira/browse/CAMEL-24471)

camel-ibm-secrets-manager: SecretId producer header has a copy-pasted description

[CAMEL-24470](https://issues.apache.org/jira/browse/CAMEL-24470)

camel-ibm-secrets-manager: IBMEventStreamReloadTriggerTask rejects Event Stream credentials provided via environment variables

[CAMEL-24468](https://issues.apache.org/jira/browse/CAMEL-24468)

camel-ibm-secrets-manager - fix defects in IBMSecretsManagerPropertiesFunction (env-var credentials rejected, secret version pin ignored, missing KV field returns "null")

[CAMEL-24464](https://issues.apache.org/jira/browse/CAMEL-24464)

camel-exec ignores its documented CamelExecCommand\* headers (executable and args have no effect)

[CAMEL-24457](https://issues.apache.org/jira/browse/CAMEL-24457)

Camel Zookeeper Cluster Split brain issue when leader is isolated

[CAMEL-24456](https://issues.apache.org/jira/browse/CAMEL-24456)

camel-http - OAuth2 token cache key omits tokenEndpoint, scope and resourceIndicator

[CAMEL-24455](https://issues.apache.org/jira/browse/CAMEL-24455)

camel-platform-http - any path starting with "proxy" selects HTTP proxy mode

[CAMEL-24454](https://issues.apache.org/jira/browse/CAMEL-24454)

camel-mllp - logPhi defaults to true, so message content is written to the log at INFO/WARN

[CAMEL-24453](https://issues.apache.org/jira/browse/CAMEL-24453)

camel-platform-http - request-header echo suppression compares header names case-sensitively

[CAMEL-24452](https://issues.apache.org/jira/browse/CAMEL-24452)

camel-http - credentials are sent to redirect targets on a different host

[CAMEL-24451](https://issues.apache.org/jira/browse/CAMEL-24451)

camel-xslt - all headers are bound as stylesheet parameters and XsltUriResolver bypasses the JAXP external-access limits

[CAMEL-24450](https://issues.apache.org/jira/browse/CAMEL-24450)

camel-jetty - enableCORS installs Jetty's CrossOriginFilter with its allow-all defaults

[CAMEL-24449](https://issues.apache.org/jira/browse/CAMEL-24449)

camel-core - saga coordinator is selected from the unprefixed Long-Running-Action message header

[CAMEL-24448](https://issues.apache.org/jira/browse/CAMEL-24448)

camel-keycloak - introspection issuer validation is skipped when the iss claim is absent

[CAMEL-24447](https://issues.apache.org/jira/browse/CAMEL-24447)

camel-pqc - FileBasedKeyLifecycleManager writes private keys with default file permissions

[CAMEL-24445](https://issues.apache.org/jira/browse/CAMEL-24445)

camel-pqc - producer shares one Signature instance across concurrent exchanges without synchronization

[CAMEL-24444](https://issues.apache.org/jira/browse/CAMEL-24444)

camel-xmlsecurity - verifier output is not correlated with the validated signature References

[CAMEL-24443](https://issues.apache.org/jira/browse/CAMEL-24443)

camel-knative-http - enabling SSL without a truststore falls back to trusting all certificates

[CAMEL-24442](https://issues.apache.org/jira/browse/CAMEL-24442)

camel-thrift - unmarshal deserializes into and returns a single shared instance

[CAMEL-24441](https://issues.apache.org/jira/browse/CAMEL-24441)

camel-crypto-pgp - unmarshal accepts unsigned and non-integrity-protected messages by default

[CAMEL-24440](https://issues.apache.org/jira/browse/CAMEL-24440)

camel-crypto - CryptoDataFormat validates the MAC after decrypting, reuses the cipher key for the HMAC, and has no per-message IV

[CAMEL-24439](https://issues.apache.org/jira/browse/CAMEL-24439)

camel-shiro - presented password is not verified when the thread subject already matches the username

[CAMEL-24438](https://issues.apache.org/jira/browse/CAMEL-24438)

camel-platform-http-main - static file serving resolves against the process working directory and the classpath root

[CAMEL-24436](https://issues.apache.org/jira/browse/CAMEL-24436)

camel-platform-http-vertx - CORS handler allows any origin and always sends Access-Control-Allow-Credentials

[CAMEL-24435](https://issues.apache.org/jira/browse/CAMEL-24435)

camel-as2 - asynchronous MDN context attributes are reused across requests on the same connection

[CAMEL-24433](https://issues.apache.org/jira/browse/CAMEL-24433)

camel-mail - attachment file names are neither path-sanitised on unmarshal nor quoted on marshal

[CAMEL-24432](https://issues.apache.org/jira/browse/CAMEL-24432)

camel-mail - a single malformed message can permanently stop the consumer

[CAMEL-24429](https://issues.apache.org/jira/browse/CAMEL-24429)

camel-as2 - ResponseMDN keeps per-request signing keys in shared mutable instance fields

[CAMEL-24427](https://issues.apache.org/jira/browse/CAMEL-24427)

camel-servlet, camel-jetty - fileNameExtWhitelist is checked against the wrong value in one binding and absent in the other

[CAMEL-24425](https://issues.apache.org/jira/browse/CAMEL-24425)

camel-azure-storage-blob - sasToken is not marked as a secret

[CAMEL-24424](https://issues.apache.org/jira/browse/CAMEL-24424)

camel-vertx-http - REST header filter strategy applies the inbound rules on the outbound direction

[CAMEL-24423](https://issues.apache.org/jira/browse/CAMEL-24423)

camel-tika - parsed document metadata is copied to exchange headers without filtering

[CAMEL-24419](https://issues.apache.org/jira/browse/CAMEL-24419)

camel-mail - MimeMultipartDataFormat unmarshal does not filter the mail.smtp/mail.smtps header namespace

[CAMEL-24417](https://issues.apache.org/jira/browse/CAMEL-24417)

camel-as2 - asynchronous MDN delivery address is used without scheme validation and always over a plain socket

[CAMEL-24415](https://issues.apache.org/jira/browse/CAMEL-24415)

camel-file - normalizePathToProtocol turns a backslash in a legal POSIX file name into a path separator

[CAMEL-24413](https://issues.apache.org/jira/browse/CAMEL-24413)

camel-hazelcast - ReplicatedHazelcastAggregationRepository does not apply the default serialization filter

[CAMEL-24412](https://issues.apache.org/jira/browse/CAMEL-24412)

camel-netty-http - security constraint lookup must use the same case-insensitive path matching as dispatch

[CAMEL-24411](https://issues.apache.org/jira/browse/CAMEL-24411)

camel-oauth - stop the route when the OAuth processors do not authenticate the request

[CAMEL-24410](https://issues.apache.org/jira/browse/CAMEL-24410)

camel-jbang export fails to parse redeliveryDelay in YAML DSL (IllegalArgumentException: Error parsing as java.time.Duration)

[CAMEL-24409](https://issues.apache.org/jira/browse/CAMEL-24409)

rest-dsl - Binary data corrupted by rest client request validator

[CAMEL-24408](https://issues.apache.org/jira/browse/CAMEL-24408)

SEDA discardIfNoConsumers breaks after consumer removal when sharing the same URI

[CAMEL-24407](https://issues.apache.org/jira/browse/CAMEL-24407)

simple predicate fails for long digital strings

[CAMEL-24403](https://issues.apache.org/jira/browse/CAMEL-24403)

camel-mail: MessageRemovedException in processCommit causes null in error log

[CAMEL-24401](https://issues.apache.org/jira/browse/CAMEL-24401)

Camel-jms InOut pattern on to(...) with temporary queues can enter infinitely looping error state

[CAMEL-24398](https://issues.apache.org/jira/browse/CAMEL-24398)

\[BUG\] DefaultAttachmentMessage.hasAttachments() returns true for messages with no attachments in Camel 4.x

[CAMEL-24397](https://issues.apache.org/jira/browse/CAMEL-24397)

camel-tui: --record produces no cast file because the recording backend is never applied

[CAMEL-24392](https://issues.apache.org/jira/browse/CAMEL-24392)

BacklogTracerRouteAdvice drains non-re-readable InputStream body before stream caching

[CAMEL-24388](https://issues.apache.org/jira/browse/CAMEL-24388)

Camel JBang - PluginHelper should guard against duplicate subcommand registration

[CAMEL-24384](https://issues.apache.org/jira/browse/CAMEL-24384)

camel-azure-eventgrid: the dataVersion header is read but never applied to the published CloudEvent

[CAMEL-24383](https://issues.apache.org/jira/browse/CAMEL-24383)

camel-azure-key-vault: producer throws a copy-pasted "createSecret" validation message for every operation

[CAMEL-24382](https://issues.apache.org/jira/browse/CAMEL-24382)

camel-azure-cosmosdb: change-feed consumer checkpoints the lease before the exchange is processed, losing events on failure

[CAMEL-24379](https://issues.apache.org/jira/browse/CAMEL-24379)

AS2 client ignores custom HostnameVerifier due to JSSE-level hostname verification

[CAMEL-24376](https://issues.apache.org/jira/browse/CAMEL-24376)

boolean zen not working with logical operator

[CAMEL-24375](https://issues.apache.org/jira/browse/CAMEL-24375)

parseDuration should handle plain millis value without relying on type converter

[CAMEL-24371](https://issues.apache.org/jira/browse/CAMEL-24371)

camel-a2a - fix WebhookUrlValidator address classification and host matching

[CAMEL-24350](https://issues.apache.org/jira/browse/CAMEL-24350)

camel-google-pubsub: producer NPEs on non-convertible headers and drops non-Exchange list elements

[CAMEL-24349](https://issues.apache.org/jira/browse/CAMEL-24349)

camel-google-functions: createFunction fails with an opaque NPE when required headers are missing

[CAMEL-24348](https://issues.apache.org/jira/browse/CAMEL-24348)

camel-google-bigquery: NPEs on a null body or unknown job id, and insertId is ignored for List bodies

[CAMEL-24347](https://issues.apache.org/jira/browse/CAMEL-24347)

camel-google-firestore: listCollections ignores the configured documentId and the realtime queue is unbounded

### Dependency upgrade (4)

[CAMEL-24806](https://issues.apache.org/jira/browse/CAMEL-24806)

camel-jolt - Switch from unmaintained bazaarvoice jolt to the jolt-community fork

[CAMEL-24759](https://issues.apache.org/jira/browse/CAMEL-24759)

camel-jbang - Upgrade tamboui to 0.5.x

[CAMEL-24675](https://issues.apache.org/jira/browse/CAMEL-24675)

camel-spring-boot - Upgrade to 4.1.1

[CAMEL-24205](https://issues.apache.org/jira/browse/CAMEL-24205)

Migrate from as2lib 5.x to phase2 6.x

### Improvement (348)

[CAMEL-25530](https://issues.apache.org/jira/browse/CAMEL-25530)

camel-timer - the includeMetadata option names the exchange properties it sets, and that CamelTimerCounter starts at 1

[CAMEL-25529](https://issues.apache.org/jira/browse/CAMEL-25529)

camel-yaml-dsl-validator - an option of a step's EIP at the column of the EIP: say which key it lines up with

[CAMEL-25528](https://issues.apache.org/jira/browse/CAMEL-25528)

camel-jbang - camel run ignores camel.jbang.dependencies in a properties file given on the command line, such as camel/application.properties

[CAMEL-25517](https://issues.apache.org/jira/browse/CAMEL-25517)

camel-jbang - the shipped examples keep their values in variables, not exchange properties

[CAMEL-25516](https://issues.apache.org/jira/browse/CAMEL-25516)

camel-jbang - the validator reports a header read where the route sets an exchange property of that name, and the reverse

[CAMEL-25514](https://issues.apache.org/jira/browse/CAMEL-25514)

camel-jbang - the validator hints when an XSLT 1.0 stylesheet puts a {expression} in element text

[CAMEL-25513](https://issues.apache.org/jira/browse/CAMEL-25513)

camel-jbang-mcp - a write reports the reload and the first output of the integration running from its directory

[CAMEL-25503](https://issues.apache.org/jira/browse/CAMEL-25503)

camel-reactive-streams - Make the consumer Suspendable, so that a suspend does not stop it and wait for the drain

[CAMEL-25502](https://issues.apache.org/jira/browse/CAMEL-25502)

camel-core - RouteStoppingException for an exchange cut off by a route or CamelContext stop

[CAMEL-25501](https://issues.apache.org/jira/browse/CAMEL-25501)

camel-jbang-mcp - camel\_edit\_file can apply several edits to one file in one call

[CAMEL-25499](https://issues.apache.org/jira/browse/CAMEL-25499)

camel-semantic: Design audit SPI, TUI history and observability hooks

[CAMEL-25484](https://issues.apache.org/jira/browse/CAMEL-25484)

camel-core - a dev mode reload that cuts off an in-flight exchange logs a full ERROR, though the work is retried

[CAMEL-25471](https://issues.apache.org/jira/browse/CAMEL-25471)

camel-dataweave - convert real-world Mule DataWeave scripts faithfully

[CAMEL-25463](https://issues.apache.org/jira/browse/CAMEL-25463)

camel-langchain4j-ingest: maxDocumentSize is checked only after the whole body is read

[CAMEL-25438](https://issues.apache.org/jira/browse/CAMEL-25438)

camel-jbang - monitor tabs wait seconds behind data loads for tabs that are not shown

[CAMEL-25435](https://issues.apache.org/jira/browse/CAMEL-25435)

camel-core - backlog tracer and debugger cut node labels at 50 characters without an ellipsis

[CAMEL-25434](https://issues.apache.org/jira/browse/CAMEL-25434)

camel-jbang - camel run does not record where a property comes from, so camel get properties shows no location

[CAMEL-25433](https://issues.apache.org/jira/browse/CAMEL-25433)

camel-jbang - camel run --example and the monitor show what an example needs before it runs

[CAMEL-25432](https://issues.apache.org/jira/browse/CAMEL-25432)

camel-jbang - source editor: show the tree of the route the cursor is in; Diagram tab: levels in the title

[CAMEL-25430](https://issues.apache.org/jira/browse/CAMEL-25430)

camel-jbang - camel infra run shows the progress of pulling the container image

[CAMEL-25429](https://issues.apache.org/jira/browse/CAMEL-25429)

camel-jbang - route topology: show dead letter and onException targets as error paths from the route whose error handler acts

[CAMEL-25426](https://issues.apache.org/jira/browse/CAMEL-25426)

camel-jbang - Minor bugs and usability fixes in the monitor before 4.23

[CAMEL-25416](https://issues.apache.org/jira/browse/CAMEL-25416)

camel-jbang - Catalog view: list the Kamelets, the project's own first

[CAMEL-25412](https://issues.apache.org/jira/browse/CAMEL-25412)

camel-file - resolve symbolic links when enforcing jailStartingDirectory for the producer target and local consumer listing

[CAMEL-25411](https://issues.apache.org/jira/browse/CAMEL-25411)

camel-jbang - Source editor: run the Kamelet checks the AI tools run

[CAMEL-25407](https://issues.apache.org/jira/browse/CAMEL-25407)

Endpoint uri options keep the order they are written in

[CAMEL-25404](https://issues.apache.org/jira/browse/CAMEL-25404)

camel-ai-tool - make an authorizationPolicy denial visible to onException, tracing and metrics

[CAMEL-25403](https://issues.apache.org/jira/browse/CAMEL-25403)

camel-jbang - AI tools: note a Kamelet camel: dependency that the template does not use

[CAMEL-25402](https://issues.apache.org/jira/browse/CAMEL-25402)

camel-yaml-dsl-validator - Say how to write expression: when it is given text instead of a language

[CAMEL-25387](https://issues.apache.org/jira/browse/CAMEL-25387)

camel-kamelet - A Kamelet whose template starts from the Kamelet itself fails with a StackOverflowError instead of saying so

[CAMEL-25382](https://issues.apache.org/jira/browse/CAMEL-25382)

camel-semantic: Introduce expert-owned evaluation contracts

[CAMEL-25381](https://issues.apache.org/jira/browse/CAMEL-25381)

camel-jbang - camel validate normalize should support Kamelet files

[CAMEL-25380](https://issues.apache.org/jira/browse/CAMEL-25380)

camel-yaml-dsl - Do not log the compact notation warning for YAML inside a jar, such as the Kamelets of the Kamelet catalog

[CAMEL-25379](https://issues.apache.org/jira/browse/CAMEL-25379)

camel-jbang - AI tools: Kamelets in camel\_catalog\_doc and camel\_catalog\_find, and kamelet: endpoints checked by the validator

[CAMEL-25377](https://issues.apache.org/jira/browse/CAMEL-25377)

camel-jbang - camel\_catalog\_doc nested options: the YAML key of an element, and the options of the error handler kinds

[CAMEL-25374](https://issues.apache.org/jira/browse/CAMEL-25374)

camel-jbang - quote characters in a file include/exclude value are reported with the line to write

[CAMEL-25373](https://issues.apache.org/jira/browse/CAMEL-25373)

camel-rest - the unresolved path parameter warning comes back once a minute, and names an exchange property of that name

[CAMEL-25372](https://issues.apache.org/jira/browse/CAMEL-25372)

camel-yaml-dsl-validator - a misplaced key says where it goes: a top-level key without its - , and an option at the column of its EIP

[CAMEL-25371](https://issues.apache.org/jira/browse/CAMEL-25371)

camel-jbang-mcp - validating the same content again is a repeated call, and validating the file as it is on disk says so

[CAMEL-25370](https://issues.apache.org/jira/browse/CAMEL-25370)

camel-jbang-mcp - the catalog tools answer for the error handler: samples, where it goes, its kinds, and the redelivery options

[CAMEL-25365](https://issues.apache.org/jira/browse/CAMEL-25365)

camel-core - a dev mode reload that cuts off in-flight exchanges says where they were waiting, and does not log them as unexplained errors

[CAMEL-25364](https://issues.apache.org/jira/browse/CAMEL-25364)

camel-jbang - a failed run or restart returns its cause, and camel\_run does not start a second copy of an app that already runs from the directory

[CAMEL-25359](https://issues.apache.org/jira/browse/CAMEL-25359)

camel-barcode - getWriterHintMap() and getReaderHintMap() return the live maps, so hints changed through them are lost when the data format starts

[CAMEL-25358](https://issues.apache.org/jira/browse/CAMEL-25358)

camel-jbang - source editor: Shift+F8 (fix with AI) on a line that fails at runtime

[CAMEL-25340](https://issues.apache.org/jira/browse/CAMEL-25340)

camel-spring-ws: apply the HeaderFilterStrategy to outbound SOAP headers

[CAMEL-25338](https://issues.apache.org/jira/browse/CAMEL-25338)

camel-spring-boot - document Jackson 2 / Jackson 3 usage and migration

[CAMEL-25336](https://issues.apache.org/jira/browse/CAMEL-25336)

camel-yaml-dsl-validator - report ${...} in a constant, which is used as written and never evaluated

[CAMEL-25330](https://issues.apache.org/jira/browse/CAMEL-25330)

camel-groovy - a property read on a body that is still text says to unmarshal it first

[CAMEL-25329](https://issues.apache.org/jira/browse/CAMEL-25329)

JSON data formats - marshal json writes a body that is already JSON text (file, stream, bytes, JSON String) as-is

[CAMEL-25328](https://issues.apache.org/jira/browse/CAMEL-25328)

camel-yaml-dsl-validator - an error handler written as a route step says where it goes

[CAMEL-25322](https://issues.apache.org/jira/browse/CAMEL-25322)

camel-bean - a missing Map key says the Map has no such key and lists its keys

[CAMEL-25321](https://issues.apache.org/jira/browse/CAMEL-25321)

camel-rest-openapi - client request validation checks the path parameters too

[CAMEL-25310](https://issues.apache.org/jira/browse/CAMEL-25310)

camel-semantic: Add experts and runtime capability discovery

[CAMEL-25309](https://issues.apache.org/jira/browse/CAMEL-25309)

camel-http - a Map or List body says to marshal it to JSON first

[CAMEL-25307](https://issues.apache.org/jira/browse/CAMEL-25307)

camel-jbang-mcp - an HTTP tool group: served endpoints and a request tool for the selected integration

[CAMEL-25306](https://issues.apache.org/jira/browse/CAMEL-25306)

camel-rest-openapi - contract-first path parameter headers are not percent-decoded

[CAMEL-25296](https://issues.apache.org/jira/browse/CAMEL-25296)

camel-jbang - camel\_get\_log leaves out stack traces by default, keeping the error line

[CAMEL-25285](https://issues.apache.org/jira/browse/CAMEL-25285)

marshal/unmarshal on a null message body: say the body is null

[CAMEL-25284](https://issues.apache.org/jira/browse/CAMEL-25284)

marshal EIP: add allowNullBody, as unmarshal has

[CAMEL-25283](https://issues.apache.org/jira/browse/CAMEL-25283)

camel-kamelet - document how to write a custom Kamelet (source, sink, action) as a sub-page camel\_catalog\_doc can return

[CAMEL-25270](https://issues.apache.org/jira/browse/CAMEL-25270)

camel-jbang - Resolve Camel shorthand dependencies using catalog coordinates

[CAMEL-25265](https://issues.apache.org/jira/browse/CAMEL-25265)

docs - language pages show their examples in Java, XML and YAML tabs

[CAMEL-25264](https://issues.apache.org/jira/browse/CAMEL-25264)

docs, camel-jbang - samples for the HTTP rungs: REST status codes, JsonPath YAML, calling a rest-openapi operation, the call-service intent

[CAMEL-25261](https://issues.apache.org/jira/browse/CAMEL-25261)

camel-jbang - bundle the examples of the ladder that run offline

[CAMEL-25258](https://issues.apache.org/jira/browse/CAMEL-25258)

camel-jbang-mcp - camel\_transform\_route converts with the route DSL converter

[CAMEL-25256](https://issues.apache.org/jira/browse/CAMEL-25256)

camel-jbang - source editor: refactorings (Ctrl+R) for Java and XML routes

[CAMEL-25254](https://issues.apache.org/jira/browse/CAMEL-25254)

camel-jbang - convert a route file between YAML, XML and Java DSL without running it

[CAMEL-25244](https://issues.apache.org/jira/browse/CAMEL-25244)

camel-jbang - source editor: quick doc of the XML element or attribute at the cursor

[CAMEL-25243](https://issues.apache.org/jira/browse/CAMEL-25243)

camel-jbang - source editor: Java DSL completion inside arguments (expression builders) and for the REST DSL

[CAMEL-25242](https://issues.apache.org/jira/browse/CAMEL-25242)

camel-jbang - source editor: complete the arguments of simple functions (date commands and patterns, beans, property keys)

[CAMEL-25241](https://issues.apache.org/jira/browse/CAMEL-25241)

camel-jbang - source editor completion for the Java DSL route chain

[CAMEL-25240](https://issues.apache.org/jira/browse/CAMEL-25240)

camel-jbang - source editor completion for XML DSL elements and attributes

[CAMEL-25237](https://issues.apache.org/jira/browse/CAMEL-25237)

camel-core - Switch EIP should count the messages per case

[CAMEL-25236](https://issues.apache.org/jira/browse/CAMEL-25236)

camel-jbang - camel run --example should work from any folder for examples that read files

[CAMEL-25235](https://issues.apache.org/jira/browse/CAMEL-25235)

camel\_catalog\_doc gives a language only its generic options: the semantic language's questions, criteria and threshold are unreachable

[CAMEL-25229](https://issues.apache.org/jira/browse/CAMEL-25229)

camel-hazelcast: serialization filter docs and WARN for user-supplied configs

[CAMEL-25225](https://issues.apache.org/jira/browse/CAMEL-25225)

camel-spring-ws: apply the HeaderFilterStrategy to producer response headers

[CAMEL-25223](https://issues.apache.org/jira/browse/CAMEL-25223)

camel-jgroups: fail fast (or require explicit opt-in) when the consumer has no pre-read deserialization control on the default channel

[CAMEL-25219](https://issues.apache.org/jira/browse/CAMEL-25219)

camel-jbang - TUI Source tab completion for the simple language

[CAMEL-25208](https://issues.apache.org/jira/browse/CAMEL-25208)

camel-jbang - Camel validation and code assistance for Java and XML DSL routes (model based)

[CAMEL-25205](https://issues.apache.org/jira/browse/CAMEL-25205)

camel-jackson3xml - Add support to enable/disable features from Jackson feature enums

[CAMEL-25204](https://issues.apache.org/jira/browse/CAMEL-25204)

camel-java-io - Java DSL parser resolves the header names of the endpoint DSL

[CAMEL-25203](https://issues.apache.org/jira/browse/CAMEL-25203)

camel-java-io - Java DSL parser reads routes kept in local variables, setHeaders with plain values can be dumped

[CAMEL-25202](https://issues.apache.org/jira/browse/CAMEL-25202)

camel-jbang - camel transform route reads Java routes without compiling them

[CAMEL-25201](https://issues.apache.org/jira/browse/CAMEL-25201)

camel-typesafe-ai: Make the API path configurable

[CAMEL-25199](https://issues.apache.org/jira/browse/CAMEL-25199)

camel-jbang - read Java routes with the Java DSL parser only, retire the regex readers

[CAMEL-25198](https://issues.apache.org/jira/browse/CAMEL-25198)

camel-jbang - TUI Source tab route jump links across the folders of a project

[CAMEL-25197](https://issues.apache.org/jira/browse/CAMEL-25197)

camel-cli-connector - add a WebSocket transport so developer tools can drive running integrations

[CAMEL-25196](https://issues.apache.org/jira/browse/CAMEL-25196)

camel-jbang - TUI Source tab route jump links for XML DSL routes

[CAMEL-25195](https://issues.apache.org/jira/browse/CAMEL-25195)

camel-console - send dev console: support base64 encoded (binary) message bodies

[CAMEL-25193](https://issues.apache.org/jira/browse/CAMEL-25193)

camel-jbang - project overview and TUI diagrams miss the destinations of the Switch EIP

[CAMEL-25192](https://issues.apache.org/jira/browse/CAMEL-25192)

camel-jbang - TUI Source tab route jump links for Java DSL routes

[CAMEL-25187](https://issues.apache.org/jira/browse/CAMEL-25187)

Add suport for type/\* in RestUtil.isValidOrAcceptedContentType

[CAMEL-25184](https://issues.apache.org/jira/browse/CAMEL-25184)

camel-openfga: add the expand, readTuples and readChanges operations

[CAMEL-25183](https://issues.apache.org/jira/browse/CAMEL-25183)

camel-openfga: support contextual tuples and condition context on the check operation

[CAMEL-25182](https://issues.apache.org/jira/browse/CAMEL-25182)

Check the Java DSL examples of the documentation with the Java DSL parser

[CAMEL-25178](https://issues.apache.org/jira/browse/CAMEL-25178)

Improve Switch EIP discoverability and DSL round-trip coverage

[CAMEL-25163](https://issues.apache.org/jira/browse/CAMEL-25163)

camel-google-storage - apply the download directory containment check on the expression branch

[CAMEL-25162](https://issues.apache.org/jira/browse/CAMEL-25162)

camel-oauth - confine the reconstructed post-login URL to the configured redirect URI origin

[CAMEL-25161](https://issues.apache.org/jira/browse/CAMEL-25161)

camel-jbang - AI project overview: plain-language labels for the decision points of a route

[CAMEL-25147](https://issues.apache.org/jira/browse/CAMEL-25147)

camel-jbang - TUI: capabilities view grouping the route topology by the AI project overview's business capabilities

[CAMEL-25145](https://issues.apache.org/jira/browse/CAMEL-25145)

camel-milo - OPC Subscription parameters are not available but not handled

[CAMEL-25138](https://issues.apache.org/jira/browse/CAMEL-25138)

camel-semantic: Add question declarations to Java and XML DSLs

[CAMEL-25134](https://issues.apache.org/jira/browse/CAMEL-25134)

camel-main - security policy check matches options by name only, so one component's insecure marker applies to all

[CAMEL-25120](https://issues.apache.org/jira/browse/CAMEL-25120)

camel-core - do not reject && in endpoint uris

[CAMEL-25112](https://issues.apache.org/jira/browse/CAMEL-25112)

camel-core - The local properties of the properties component should be per thread

[CAMEL-25104](https://issues.apache.org/jira/browse/CAMEL-25104)

camel-core - SSLContextParameters should use TLSv1.2 as minimum protocol by default

[CAMEL-25096](https://issues.apache.org/jira/browse/CAMEL-25096)

camel-core - Properties component: mask the values of vault functions and sensitive keys when logging

[CAMEL-25093](https://issues.apache.org/jira/browse/CAMEL-25093)

Thread-Safety: Concurrent updateRoutes() Against a Single CamelContext Causes ConcurrentModificationException

[CAMEL-25091](https://issues.apache.org/jira/browse/CAMEL-25091)

camel-kafka: expose by\_duration as valid autoOffsetReset value (Kafka 4.0+)

[CAMEL-25087](https://issues.apache.org/jira/browse/CAMEL-25087)

camel-coap - add a muteException consumer option

[CAMEL-25075](https://issues.apache.org/jira/browse/CAMEL-25075)

camel-jbang-mcp - a repeated identical tool call should answer differently, so an agent can notice it is looping

[CAMEL-25074](https://issues.apache.org/jira/browse/CAMEL-25074)

camel-sql - say in the outputType description that a StreamList body is an Iterator with no size

[CAMEL-25068](https://issues.apache.org/jira/browse/CAMEL-25068)

camel-core - Route templates: follow-ups from the deep review

[CAMEL-25066](https://issues.apache.org/jira/browse/CAMEL-25066)

camel-core - Producer cache eviction can stop a dynamic endpoint that another producer cache still uses

[CAMEL-25058](https://issues.apache.org/jira/browse/CAMEL-25058)

camel-saga - saga:complete and saga:compensate should only consult Long-Running-Action for a saga service that uses it

[CAMEL-25054](https://issues.apache.org/jira/browse/CAMEL-25054)

camel-jackson - Add support to enable/disable features in qualified manner

[CAMEL-25049](https://issues.apache.org/jira/browse/CAMEL-25049)

camel-semantic: Support batching multiple named questions

[CAMEL-25041](https://issues.apache.org/jira/browse/CAMEL-25041)

Dev mode reload: consider a polling directory scan instead of the JDK WatchService

[CAMEL-25040](https://issues.apache.org/jira/browse/CAMEL-25040)

camel-jbang-mcp - camel\_catalog\_doc returns only the option list, not the syntax a component's documentation explains

[CAMEL-25022](https://issues.apache.org/jira/browse/CAMEL-25022)

camel-oauth: honor the JWT nbf (not before) claim when authenticating bearer tokens with the servlet backend

[CAMEL-25019](https://issues.apache.org/jira/browse/CAMEL-25019)

camel-quickfix - InOut consumer should reply on the originating session

[CAMEL-24999](https://issues.apache.org/jira/browse/CAMEL-24999)

camel-hivemq: ssl option is missing security=insecure:ssl annotation for the security policy framework

[CAMEL-24992](https://issues.apache.org/jira/browse/CAMEL-24992)

camel-yaml-dsl-validator: say when a rest-openapi call has no value for a path parameter of its operation

[CAMEL-24986](https://issues.apache.org/jira/browse/CAMEL-24986)

camel-rest: a REST producer sends the request when a path parameter has no value, with the placeholder still in the uri

[CAMEL-24984](https://issues.apache.org/jira/browse/CAMEL-24984)

camel-core: simple - support ! as a negation prefix in a predicate

[CAMEL-24975](https://issues.apache.org/jira/browse/CAMEL-24975)

camel-core: the inflight, blocked and shutdown dumps say where the node is in the source

[CAMEL-24974](https://issues.apache.org/jira/browse/CAMEL-24974)

camel-core: the failed delivery log line says where the failure is (route, node and source location)

[CAMEL-24972](https://issues.apache.org/jira/browse/CAMEL-24972)

camel-core: the error registry says where each step is in the source (foo.yaml:88), next to the body type

[CAMEL-24955](https://issues.apache.org/jira/browse/CAMEL-24955)

camel-yaml-dsl-validator: report a direct: or seda: endpoint that no route consumes

[CAMEL-24937](https://issues.apache.org/jira/browse/CAMEL-24937)

camel-pqc: confine FileBasedKeyLifecycleManager key file resolution to the configured directory

[CAMEL-24936](https://issues.apache.org/jira/browse/CAMEL-24936)

camel-netty: NettyConverter.toByteArray should copy only the readable bytes of the ByteBuf

[CAMEL-24931](https://issues.apache.org/jira/browse/CAMEL-24931)

camel-jsonpath, camel-jq: the null body hint says how to read the data, not only that it must be read

[CAMEL-24921](https://issues.apache.org/jira/browse/CAMEL-24921)

camel-core: read a predicate inside ${ } in the Simple language, as EL and Groovy do

[CAMEL-24920](https://issues.apache.org/jira/browse/CAMEL-24920)

camel-core: the ternary operator cannot take a compound condition (&& or || inside ${ })

[CAMEL-24919](https://issues.apache.org/jira/browse/CAMEL-24919)

camel-debezium - the consumer health check has no startup readiness signal

[CAMEL-24918](https://issues.apache.org/jira/browse/CAMEL-24918)

camel-core: metadata for endpoint options that are evaluated as a Simple expression per message

[CAMEL-24917](https://issues.apache.org/jira/browse/CAMEL-24917)

camel-yaml-dsl-validator: a to: uri that holds an expression says to use toD:

[CAMEL-24916](https://issues.apache.org/jira/browse/CAMEL-24916)

camel-bean: ${body.name} on a Map reads the key when there is no such method

[CAMEL-24911](https://issues.apache.org/jira/browse/CAMEL-24911)

camel-core, camel-jbang - collapse identical repeated errors in the error registry and in camel\_get\_log

[CAMEL-24909](https://issues.apache.org/jira/browse/CAMEL-24909)

camel-jbang - an edit tool for the authoring set: replace a snippet instead of rewriting the whole file

[CAMEL-24907](https://issues.apache.org/jira/browse/CAMEL-24907)

camel-jbang - camel\_eval\_expression evaluates jsonpath, jq, xpath and the other languages, not only the ones on its own classpath

[CAMEL-24906](https://issues.apache.org/jira/browse/CAMEL-24906)

camel-yaml-dsl-validator - the quote hints print the line to write, and a doubled closing quote says so

[CAMEL-24902](https://issues.apache.org/jira/browse/CAMEL-24902)

camel-keycloak: honor token expiry (exp) when caching introspection results

[CAMEL-24901](https://issues.apache.org/jira/browse/CAMEL-24901)

camel-aws2-s3: restrict Simple expression evaluation of key/bucket to configured values

[CAMEL-24899](https://issues.apache.org/jira/browse/CAMEL-24899)

camel-core - a failed reload of the only route file keeps the previous routes running (restore from the last good definitions, not from disk)

[CAMEL-24898](https://issues.apache.org/jira/browse/CAMEL-24898)

camel-jbang - camel\_catalog\_doc and camel\_catalog\_sample resolve the YAML names of data formats (json -> jackson, and the YAML shape)

[CAMEL-24897](https://issues.apache.org/jira/browse/CAMEL-24897)

camel-jbang-mcp - camel\_write\_file: drop the validate flag, an agent turns it off

[CAMEL-24894](https://issues.apache.org/jira/browse/CAMEL-24894)

camel-docling: make output path handling consistent with input path and custom-argument handling

[CAMEL-24893](https://issues.apache.org/jira/browse/CAMEL-24893)

camel-docling: also constrain absolute paths in custom-argument path validation

[CAMEL-24888](https://issues.apache.org/jira/browse/CAMEL-24888)

camel-yaml-dsl-validator, camel-jbang - say the shape for the seven mistakes of the HTTP rungs (constant null, setExchangeProperty, unclosed quote, toD options, library case, jsonPath key, rest-openapi path parameter)

[CAMEL-24884](https://issues.apache.org/jira/browse/CAMEL-24884)

camel-core - resolveResource option on expressions: a returned resource:... value is loaded and its content is the result

[CAMEL-24882](https://issues.apache.org/jira/browse/CAMEL-24882)

camel-jbang - say that a script returning 'resource:file:x' returns the text, not the file (validator hint and error diagnose)

[CAMEL-24881](https://issues.apache.org/jira/browse/CAMEL-24881)

camel-yaml-dsl-validator - say how a route-level error handler is written (errorHandler: {noErrorHandler: {}})

[CAMEL-24880](https://issues.apache.org/jira/browse/CAMEL-24880)

camel-core - GroupedBodyAggregationStrategy's list prints as List<Exchange>(n elements) although it holds bodies

[CAMEL-24879](https://issues.apache.org/jira/browse/CAMEL-24879)

camel-main - Bind @BindToRegistry and @Converter classes from compiled Groovy sources in exported projects

[CAMEL-24874](https://issues.apache.org/jira/browse/CAMEL-24874)

camel-core-languages - catalog: add the simple init block operators := and ~:= (simple.json) and fix the init block doc section

[CAMEL-24873](https://issues.apache.org/jira/browse/CAMEL-24873)

camel-jbang - Custom simple functions in Groovy: auto-add camel-groovy, honour @BindToRegistry, refresh YAML beans on --dev reload

[CAMEL-24872](https://issues.apache.org/jira/browse/CAMEL-24872)

camel-oauth: Align token caching with effective profile configuration

[CAMEL-24869](https://issues.apache.org/jira/browse/CAMEL-24869)

camel-jbang - validator hint for sql endpoint queries with :name parameters (camel-sql uses :#name)

[CAMEL-24867](https://issues.apache.org/jira/browse/CAMEL-24867)

camel-jbang-mcp - expose the sql, datasource, circuit breaker, metrics, spans, EIP stats, startup and route analysis runtime tools

[CAMEL-24863](https://issues.apache.org/jira/browse/CAMEL-24863)

camel-jbang-mcp - camel\_get\_errors counts exceptions a circuit breaker handled

[CAMEL-24862](https://issues.apache.org/jira/browse/CAMEL-24862)

camel-core - the recursive file watcher does not watch a directory created while it runs (a Java class added under src/main/java is never reloaded), and reloads on its own compile output

[CAMEL-24861](https://issues.apache.org/jira/browse/CAMEL-24861)

camel-jbang-mcp - camel\_run starts with --source-dir so files added later are part of the app, and camel\_control gets a reload action

[CAMEL-24860](https://issues.apache.org/jira/browse/CAMEL-24860)

camel-core - a failed route reload in dev mode leaves the previous route stopped: keep it running, or say that nothing runs

[CAMEL-24859](https://issues.apache.org/jira/browse/CAMEL-24859)

camel-jbang-mcp - camel\_write\_file reports the outcome of the reload in dev mode

[CAMEL-24858](https://issues.apache.org/jira/browse/CAMEL-24858)

camel-jbang - the validator reports a required endpoint path option that is missing (uri: cron without name)

[CAMEL-24857](https://issues.apache.org/jira/browse/CAMEL-24857)

camel-jbang - the validator reports a ${...} placeholder used as an endpoint option or bean property value: the syntax is {{key}}

[CAMEL-24856](https://issues.apache.org/jira/browse/CAMEL-24856)

camel-jbang - the properties validator accepts camel.resilience4j.circuitbreaker.<id>.<option>, which fails at startup

[CAMEL-24855](https://issues.apache.org/jira/browse/CAMEL-24855)

camel-jbang, camel-file - a file consumer of a directory that does not exist runs in silence: the validator names the files that are there, the consumer says it created the directory

[CAMEL-24854](https://issues.apache.org/jira/browse/CAMEL-24854)

camel-jbang - the validator reports an include/exclude regex with a doubled backslash in single quotes, which matches a literal backslash and so no file

[CAMEL-24852](https://issues.apache.org/jira/browse/CAMEL-24852)

camel-jbang - the validator reports a resource:classpath: file that sits next to the route, and a ${} placeholder in a file endpoint's directory

[CAMEL-24851](https://issues.apache.org/jira/browse/CAMEL-24851)

camel-jbang - when a YAML route fails to load, camel run prints the schema validator's report (what to write), not only the loader's message

[CAMEL-24850](https://issues.apache.org/jira/browse/CAMEL-24850)

camel-yaml-dsl-validator - say what to write for pollEnrich/enrich with a uri, a steps item inside steps, and EIPs directly under step

[CAMEL-24849](https://issues.apache.org/jira/browse/CAMEL-24849)

Make camel-http the default REST producer client (rest-openapi, rest producer) instead of vertx-http, in the rest component's default list and in the Camel CLI's dependency rule

[CAMEL-24847](https://issues.apache.org/jira/browse/CAMEL-24847)

camel validate yaml: name the data format when a step uses an alias or the artifact name (unmarshal: jackson, json-jackson, jackson-xml)

[CAMEL-24846](https://issues.apache.org/jira/browse/CAMEL-24846)

camel validate yaml: an onException (or intercept, onCompletion) placed after the routes passes validation and fails at startup with a Java DSL message

[CAMEL-24843](https://issues.apache.org/jira/browse/CAMEL-24843)

camel run / validate: a Groovy script importing a class that is not on the classpath should say how to add the dependency

[CAMEL-24842](https://issues.apache.org/jira/browse/CAMEL-24842)

YAML DSL: an endpoint with query options in the uri and a parameters block fails with 'Uri should not contains query parameters'; say what to do (and flag it in camel validate)

[CAMEL-24841](https://issues.apache.org/jira/browse/CAMEL-24841)

jsonpath: a comparison written as the path ($.status == 'paid') should say that jsonpath is a path and how to write the condition

[CAMEL-24840](https://issues.apache.org/jira/browse/CAMEL-24840)

camel validate yaml: say how a key/value property list item is written (restConfiguration dataFormatProperty and friends) instead of 'property is not defined in the schema'

[CAMEL-24839](https://issues.apache.org/jira/browse/CAMEL-24839)

camel-file: a file endpoint whose directory is an existing regular file starts and stays silent; fail with a message (and flag it in camel validate)

[CAMEL-24838](https://issues.apache.org/jira/browse/CAMEL-24838)

jsonpath and jq: say that the body is null (and how to load one) instead of 'Cannot read body as supported JSON value'

[CAMEL-24837](https://issues.apache.org/jira/browse/CAMEL-24837)

camel validate yaml: say in plain words what a YAML indentation error is, instead of the raw snakeyaml message

[CAMEL-24836](https://issues.apache.org/jira/browse/CAMEL-24836)

PropertyBindingException from camel-main configuration hides the cause: the message should carry the root cause

[CAMEL-24834](https://issues.apache.org/jira/browse/CAMEL-24834)

camel-jbang-mcp: load AI tool groups (SQL, tracing, resilience) from what the selected app has, read-only SQL for local models

[CAMEL-24833](https://issues.apache.org/jira/browse/CAMEL-24833)

camel-spiffe - validateJwtSvid should accept the token from the Authorization Bearer header

[CAMEL-24832](https://issues.apache.org/jira/browse/CAMEL-24832)

camel-openai, camel-spring-ai-chat - propagate the calling exchange into ai-tool route invocations like langchain4j-agent

[CAMEL-24831](https://issues.apache.org/jira/browse/CAMEL-24831)

camel-ai-tool - component-level authorization hook so tool routes are guarded by construction

[CAMEL-24830](https://issues.apache.org/jira/browse/CAMEL-24830)

camel-opa - OpaSecurityPolicy should support the in-process WASM evaluation mode

[CAMEL-24828](https://issues.apache.org/jira/browse/CAMEL-24828)

camel-jbang-mcp: examples tools should follow the example groups and accept optional arguments

[CAMEL-24826](https://issues.apache.org/jira/browse/CAMEL-24826)

camel validate: flag a ternary operator in a Simple expression, it is not supported and comes out as literal text

[CAMEL-24824](https://issues.apache.org/jira/browse/CAMEL-24824)

camel run --example: list the examples by group (quick-start first, then the ladder rungs, then showcase) and show what each teaches

[CAMEL-24822](https://issues.apache.org/jira/browse/CAMEL-24822)

camel run: rest-openapi producer fails with a null Vert.x unless componentName=http is set

[CAMEL-24821](https://issues.apache.org/jira/browse/CAMEL-24821)

camel infra ollama: keep pulled models in a volume, add --model, and wait for the pull

[CAMEL-24820](https://issues.apache.org/jira/browse/CAMEL-24820)

Make LangChain4j models easy to declare in YAML and properties: builder inference, component-level model, validator hints

[CAMEL-24819](https://issues.apache.org/jira/browse/CAMEL-24819)

circuitBreaker: count fallback, timed out and bulkhead rejected calls in JMX, dev console, camel get circuit-breaker and the TUI

[CAMEL-24818](https://issues.apache.org/jira/browse/CAMEL-24818)

circuitBreaker: set CamelCircuitBreakerResponseRejected when the fallback runs because the breaker is open

[CAMEL-24809](https://issues.apache.org/jira/browse/CAMEL-24809)

camel-kamelet-main - map more third-party libraries in the known dependencies, by package, and generate the list from the managed dependencies

[CAMEL-24808](https://issues.apache.org/jira/browse/CAMEL-24808)

camel-jbang-examples: revamp into a real-world ladder of examples

[CAMEL-24807](https://issues.apache.org/jira/browse/CAMEL-24807)

camel-yaml-dsl - Deprecate Pipe (aka KameletBinding) support

[CAMEL-24805](https://issues.apache.org/jira/browse/CAMEL-24805)

camel-jbang - TUI AI panel checks the simple expressions in an answer before showing it, and gives the model one turn to fix them

[CAMEL-24804](https://issues.apache.org/jira/browse/CAMEL-24804)

camel-jbang - camel\_catalog\_doc for simple: an optionsFilter that names a function group returns exactly that group, not every function whose description mentions the word

[CAMEL-24803](https://issues.apache.org/jira/browse/CAMEL-24803)

camel-knative - declare the CloudEvent message headers in the component metadata (headersClass), so the catalog, the docs and the validator know them

[CAMEL-24801](https://issues.apache.org/jira/browse/CAMEL-24801)

camel-sql - sql-stored: allow parentheses inside ${...} simple expressions in the template grammar

[CAMEL-24798](https://issues.apache.org/jira/browse/CAMEL-24798)

camel-jbang - camel\_get\_files should understand the Maven project layout: recursive listing, relative paths, and the routes' source files from the running integration

[CAMEL-24797](https://issues.apache.org/jira/browse/CAMEL-24797)

camel-core - Splitter should unwrap Exchange parts like Message parts (List<Exchange> from batching consumers)

[CAMEL-24796](https://issues.apache.org/jira/browse/CAMEL-24796)

camel-jbang - TUI AI panel with Ollama: compact on measured tokens, compact harder, and raise the 32k default context

[CAMEL-24795](https://issues.apache.org/jira/browse/CAMEL-24795)

camel-jbang - TUI add a Quit entry to the F2 actions menu

[CAMEL-24793](https://issues.apache.org/jira/browse/CAMEL-24793)

camel-jbang - TUI theme-specific syntax highlighting palettes for the built-in themes

[CAMEL-24785](https://issues.apache.org/jira/browse/CAMEL-24785)

camel-opa - support sslContextParameters for the connection to the OPA server

[CAMEL-24779](https://issues.apache.org/jira/browse/CAMEL-24779)

camel-kafka - reduce per-message allocations on the producer, consumer and transform hot paths

[CAMEL-24774](https://issues.apache.org/jira/browse/CAMEL-24774)

docs - guard the user-manual YAML examples, the XML examples against the Spring XSD, and the Java imports of the examples at build time

[CAMEL-24761](https://issues.apache.org/jira/browse/CAMEL-24761)

camel-jbang - cache the Camel version to Quarkus platform mapping so --runtime quarkus does not ask the extension registry once a day

[CAMEL-24760](https://issues.apache.org/jira/browse/CAMEL-24760)

camel-jbang - the core tool set for local models: camel\_catalog\_find in it, prefix budgets raised, prompt lines for the canonical YAML shape and file writes

[CAMEL-24756](https://issues.apache.org/jira/browse/CAMEL-24756)

camel-base-engine - http: resources are resolved with no connect or read timeout

[CAMEL-24753](https://issues.apache.org/jira/browse/CAMEL-24753)

camel-langchain4j-ingest: filter options (includeId, excludeId, minDocumentSize, documentFilter)

[CAMEL-24752](https://issues.apache.org/jira/browse/CAMEL-24752)

camel-core - generate a name to artifact table (like SensitiveUtils) so unknown component, language, data format and bean errors say which jar to add

[CAMEL-24751](https://issues.apache.org/jira/browse/CAMEL-24751)

camel-opa - unregister the OpaSecurityPolicy health check when its routes stop

[CAMEL-24745](https://issues.apache.org/jira/browse/CAMEL-24745)

camel-yaml-dsl - decide whether a top-level from: (without route:) is the compact notation: the runtime warns on it, the canonical schema accepts it

[CAMEL-24744](https://issues.apache.org/jira/browse/CAMEL-24744)

camel-jbang - the YAML the MCP scaffold tools, the camel init templates and the bundled examples generate is in the deprecated compact notation; write it in the canonical format

[CAMEL-24743](https://issues.apache.org/jira/browse/CAMEL-24743)

camel-opa - document the WASM mode and gate the server-only options and health checks

[CAMEL-24739](https://issues.apache.org/jira/browse/CAMEL-24739)

camel-spiffe - allow fetchX509Svid without placing the private key on the message

[CAMEL-24738](https://issues.apache.org/jira/browse/CAMEL-24738)

camel-opa - make a failOpen decision observable

[CAMEL-24737](https://issues.apache.org/jira/browse/CAMEL-24737)

camel-opa - allowKey cannot read a verdict nested inside the decision document

[CAMEL-24736](https://issues.apache.org/jira/browse/CAMEL-24736)

camel-opa - OpaSecurityPolicy has no health check for the OPA server

[CAMEL-24732](https://issues.apache.org/jira/browse/CAMEL-24732)

camel-opa - consider narrowing the default includeHeaders before 4.23.0 ships

[CAMEL-24731](https://issues.apache.org/jira/browse/CAMEL-24731)

camel-spiffe - acceptAnySpiffeId is invisible to the security policy framework

[CAMEL-24725](https://issues.apache.org/jira/browse/CAMEL-24725)

core: apply the shared deserialization filter in KeyValueRepositoryHelper

[CAMEL-24723](https://issues.apache.org/jira/browse/CAMEL-24723)

camel-jbang - camel validate yaml --canonical reports the deprecated compact notation as such; the runtime WARN covers implicit expressions

[CAMEL-24722](https://issues.apache.org/jira/browse/CAMEL-24722)

camel-yaml-dsl - the validator and deserializer hints recommend the classic shorthand; write them in the canonical YAML format

[CAMEL-24721](https://issues.apache.org/jira/browse/CAMEL-24721)

camel-openai: token budget and agentic observability for the Responses tool loop

[CAMEL-24720](https://issues.apache.org/jira/browse/CAMEL-24720)

camel-jbang - camel\_catalog\_sample returns samples for components, data formats and languages from their documentation, once CAMEL-24710 has their examples validating

[CAMEL-24715](https://issues.apache.org/jira/browse/CAMEL-24715)

camel-yaml-dsl-validator - table-driven hints instead of branches in four methods; drift test for the remaining hardcoded lists in the camel-jbang checks

[CAMEL-24714](https://issues.apache.org/jira/browse/CAMEL-24714)

camel-core-model - complete the @AsPredicate marking of expression properties and have tooling read asPredicate from the catalog instead of hardcoded lists

[CAMEL-24713](https://issues.apache.org/jira/browse/CAMEL-24713)

camel-jbang - generate the camel\_catalog\_sample fallback (eip-samples.json) from the user-manual YAML examples with a mojo, validated in the build

[CAMEL-24712](https://issues.apache.org/jira/browse/CAMEL-24712)

camel-jbang-mcp - retire the catalog and validation tools the shared authoring tools replace (deprecate, then remove)

[CAMEL-24711](https://issues.apache.org/jira/browse/CAMEL-24711)

camel-jbang - camel validate yaml/source --camel-version: catalog and YAML schema of that version (schema read from the camel-yaml-dsl jar)

[CAMEL-24709](https://issues.apache.org/jira/browse/CAMEL-24709)

camel-yaml-dsl - class not found hint for beans should use the bean metadata on the classpath, not a hardcoded aggregation strategy package

[CAMEL-24708](https://issues.apache.org/jira/browse/CAMEL-24708)

camel-catalog - a compact API reference of the core classes (Exchange, Message, CamelContext, Registry, AggregationStrategy...) for AI assistants, exposed as a catalog tool

[CAMEL-24707](https://issues.apache.org/jira/browse/CAMEL-24707)

camel-yaml-dsl - the JSON schema should mark the expression required on the expression nodes (split, filter, setBody, ...)

[CAMEL-24706](https://issues.apache.org/jira/browse/CAMEL-24706)

camel-main - camel.main.duration alias of durationMaxSeconds with a time unit (15s, 2m)

[CAMEL-24703](https://issues.apache.org/jira/browse/CAMEL-24703)

camel-core-languages - simple: error messages should say what to write (audit against typical mistakes)

[CAMEL-24702](https://issues.apache.org/jira/browse/CAMEL-24702)

camel-yaml-dsl - say that an expression is expected when a plain value is used for handled/continued/retryWhile/correlationExpression (handled: true)

[CAMEL-24699](https://issues.apache.org/jira/browse/CAMEL-24699)

camel-jbang - camel run on an existing Quarkus or Camel Main project does not write a log file to ~/.camel

[CAMEL-24698](https://issues.apache.org/jira/browse/CAMEL-24698)

camel-jbang: follow-ups from the AI agent benchmarks (optional MCP args, CLI validate parity, eval placeholders, validator hints)

[CAMEL-24695](https://issues.apache.org/jira/browse/CAMEL-24695)

camel-jbang: one shared, neutral set of Camel authoring MCP tools exposed by both camel-jbang-mcp and camel tui --mcp

[CAMEL-24693](https://issues.apache.org/jira/browse/CAMEL-24693)

EIP documentation YAML examples: validate at build time and ship as a per-EIP sample set in camel-catalog

[CAMEL-24689](https://issues.apache.org/jira/browse/CAMEL-24689)

camel-javascript - share one GraalJS Engine per language and cache the parsed Source; do not silence the interpreter-only warning

[CAMEL-24688](https://issues.apache.org/jira/browse/CAMEL-24688)

camel-quickjs - controlled camel API, variables/exception bindings, compile each script once per engine

[CAMEL-24684](https://issues.apache.org/jira/browse/CAMEL-24684)

camel-groovy - groovyXml creates a new XmlParser per unmarshal and writes one fragment at a time on marshal

[CAMEL-24683](https://issues.apache.org/jira/browse/CAMEL-24683)

camel-groovy - groovyJson prettyPrint=true re-lexes the generated document, 30x slower than Jackson

[CAMEL-24682](https://issues.apache.org/jira/browse/CAMEL-24682)

camel-groovy - Resolve the language and GroovyShellFactory once, keep the compiled script per expression, build the binding lazily

[CAMEL-24680](https://issues.apache.org/jira/browse/CAMEL-24680)

camel-jpa - Use field access for KeyValueEntry and cover all shipped entities in the Hibernate mapping test

[CAMEL-24679](https://issues.apache.org/jira/browse/CAMEL-24679)

Camel TUI: tui\_run\_example and tui\_infra start fail for external MCP agents

[CAMEL-24678](https://issues.apache.org/jira/browse/CAMEL-24678)

camel-jbang: infra ps shows only one instance per service alias and picks its PID non-deterministically

[CAMEL-24677](https://issues.apache.org/jira/browse/CAMEL-24677)

camel-smooks: align XML reader configuration with the other XML components

[CAMEL-24676](https://issues.apache.org/jira/browse/CAMEL-24676)

camel-jgroups: add a configurable deserialization filter and document serialization hardening for the consumer

[CAMEL-24672](https://issues.apache.org/jira/browse/CAMEL-24672)

camel-openai: moderate images with the moderation operation

[CAMEL-24671](https://issues.apache.org/jira/browse/CAMEL-24671)

camel-openai: close the remaining gaps outside the Responses API

[CAMEL-24666](https://issues.apache.org/jira/browse/CAMEL-24666)

camel-catalog: replace the Soundex suggestion strategy with an edit-distance default in camel-core-catalog

[CAMEL-24665](https://issues.apache.org/jira/browse/CAMEL-24665)

Enhance Azure Service Bus consumer to support maxConcurrentSessions

[CAMEL-24661](https://issues.apache.org/jira/browse/CAMEL-24661)

camel-jbang: feature parity for camel run CLI flags across the Camel Main, Spring Boot and Quarkus runtimes (--console, max duration, log file)

[CAMEL-24659](https://issues.apache.org/jira/browse/CAMEL-24659)

camel-jbang: add jbang as the default run runtime, and make --runtime=main export and run via Maven like Spring Boot and Quarkus

[CAMEL-24658](https://issues.apache.org/jira/browse/CAMEL-24658)

camel-catalog - find components by protocol or product name (s3 -> aws2-s3, mqtt -> paho-mqtt5)

[CAMEL-24656](https://issues.apache.org/jira/browse/CAMEL-24656)

camel-jbang TUI: reduce AI panel (F8) prompt size and make it cache friendly for local Ollama models

[CAMEL-24653](https://issues.apache.org/jira/browse/CAMEL-24653)

SSLCertTrustTest: replace external badssl.com dependency with local self-signed HTTPS endpoint

[CAMEL-24652](https://issues.apache.org/jira/browse/CAMEL-24652)

camel-servlet, camel-jetty, camel-platform-http-vertx - consolidate the fileNameExtWhitelist check and tighten the extension match

[CAMEL-24650](https://issues.apache.org/jira/browse/CAMEL-24650)

camel-http-common: lift the multipart fileNameExtWhitelist check into DefaultHttpBinding

[CAMEL-24644](https://issues.apache.org/jira/browse/CAMEL-24644)

camel-opa - add a producer health check for the OPA server

[CAMEL-24643](https://issues.apache.org/jira/browse/CAMEL-24643)

camel-opa - allow exchange properties in the OPA input document

[CAMEL-24636](https://issues.apache.org/jira/browse/CAMEL-24636)

Add SecretRotationAware SPI so components can re-authenticate on context reload

[CAMEL-24631](https://issues.apache.org/jira/browse/CAMEL-24631)

Support Ollama local models in camel doctor and TUI doctor popup

[CAMEL-24627](https://issues.apache.org/jira/browse/CAMEL-24627)

camel-file: resolve symlinks when containing local work directory downloads (parity with camel-azure/google-storage)

[CAMEL-24625](https://issues.apache.org/jira/browse/CAMEL-24625)

camel-platform-http: CamelHttpPath should optionally be relative to the consumer path (stripUriPrefix)

[CAMEL-24620](https://issues.apache.org/jira/browse/CAMEL-24620)

camel-jackson - Add support to enable/disable features from DatatypeFeature enums

[CAMEL-24605](https://issues.apache.org/jira/browse/CAMEL-24605)

camel-fop: align FopProducer XML transformation with Camel's standard secure XML processing configuration

[CAMEL-24602](https://issues.apache.org/jira/browse/CAMEL-24602)

CI test reporting should include elapsed time (duration) not just module/test counts

[CAMEL-24595](https://issues.apache.org/jira/browse/CAMEL-24595)

CassandraKeyValueRepository: implement atomic replace() and delete(key, expected) using lightweight transactions

[CAMEL-24588](https://issues.apache.org/jira/browse/CAMEL-24588)

camel-jms: disable IBM MQ tests on GitHub Actions (icr.io image not reliably pullable)

[CAMEL-24582](https://issues.apache.org/jira/browse/CAMEL-24582)

simple language - add equals/!equals operators for literal (non-numeric) string comparison

[CAMEL-24578](https://issues.apache.org/jira/browse/CAMEL-24578)

camel-avro-rpc fails with Avro 1.12.2 due to new ClassSecurityValidator rejecting HandshakeRequest

[CAMEL-24577](https://issues.apache.org/jira/browse/CAMEL-24577)

camel-platform-http-starter - path variable headers are derived from the undecoded request URI

[CAMEL-24576](https://issues.apache.org/jira/browse/CAMEL-24576)

camel-dynamic-router: align control endpoint parameter handling with the allowTemplateFromHeader convention

[CAMEL-24574](https://issues.apache.org/jira/browse/CAMEL-24574)

camel-google-bigquery - clarify that ${name} is literal substitution and steer value parameters to @name

[CAMEL-24570](https://issues.apache.org/jira/browse/CAMEL-24570)

camel-ai-observability: log when GenAI observability silently falls back to no-op

[CAMEL-24569](https://issues.apache.org/jira/browse/CAMEL-24569)

Support Salesforce Streaming API Server-Initiated Disconnect Messages

[CAMEL-24566](https://issues.apache.org/jira/browse/CAMEL-24566)

CLI GenAI Dependency Auto-Discovery

[CAMEL-24554](https://issues.apache.org/jira/browse/CAMEL-24554)

camel-jolokia-starter - agent binds all interfaces by default and the bundled restrictor gates on MBean domain only

[CAMEL-24553](https://issues.apache.org/jira/browse/CAMEL-24553)

camel-support: getMandatoryBody() OOM guard — refuse huge in-memory body conversion to String/byte\[\]

[CAMEL-24552](https://issues.apache.org/jira/browse/CAMEL-24552)

Expose phase-specific timeouts (connect/read/write/request) on camel-openai instead of a single overall timeout

[CAMEL-24551](https://issues.apache.org/jira/browse/CAMEL-24551)

Expose structured error metadata (category, retry-after) as Exchange properties when an AI producer call fails

[CAMEL-24550](https://issues.apache.org/jira/browse/CAMEL-24550)

Document how to target OpenAI/LangChain4j/Spring AI component exceptions with onException for rate-limit and retry handling

[CAMEL-24531](https://issues.apache.org/jira/browse/CAMEL-24531)

Camel Spring Boot: Extract a shared early-resolution properties parser

[CAMEL-24525](https://issues.apache.org/jira/browse/CAMEL-24525)

camel-google-firestore: the realtime change buffer is unbounded

[CAMEL-24516](https://issues.apache.org/jira/browse/CAMEL-24516)

AbstractCamelContext: keep TypeConverter non-null after stop; reset only on restart

[CAMEL-24514](https://issues.apache.org/jira/browse/CAMEL-24514)

camel-console - Generated openapi spec all are POST but lets try to use original verbs like GET

[CAMEL-24513](https://issues.apache.org/jira/browse/CAMEL-24513)

camel-core - Error registry for handlded exception should point to origin of error

[CAMEL-24508](https://issues.apache.org/jira/browse/CAMEL-24508)

Vault and secrets starters - early property resolution failures are swallowed, leaving the placeholder as the value

[CAMEL-24507](https://issues.apache.org/jira/browse/CAMEL-24507)

camel-mcp-server-starter - documentation attributes authentication to a property namespace that does not provide it

[CAMEL-24506](https://issues.apache.org/jira/browse/CAMEL-24506)

camel-jasypt-starter - modernise the default algorithm and fix the usage example's password placement

[CAMEL-24505](https://issues.apache.org/jira/browse/CAMEL-24505)

camel-micrometer-starter - uri metric tag falls back to the raw request path, giving unbounded tag cardinality

[CAMEL-24504](https://issues.apache.org/jira/browse/CAMEL-24504)

camel-spring-boot - extend the SpringTypeConverter String guard beyond InputStream targets

[CAMEL-24503](https://issues.apache.org/jira/browse/CAMEL-24503)

camel-spring-boot - security policy check does not see camel properties supplied as environment variables

[CAMEL-24502](https://issues.apache.org/jira/browse/CAMEL-24502)

Build and CI hardening - workflow token scope, job separation and Maven wrapper checksums

[CAMEL-24501](https://issues.apache.org/jira/browse/CAMEL-24501)

camel-spring-boot-generator-maven-plugin - generated configuration binding drops values silently in three places

[CAMEL-24500](https://issues.apache.org/jira/browse/CAMEL-24500)

camel-debug-starter - debugger and JMX connector are both enabled by default on classpath presence

[CAMEL-24499](https://issues.apache.org/jira/browse/CAMEL-24499)

camel-spring-boot - route detail view bypasses the route.start.exception serialization filter

[CAMEL-24498](https://issues.apache.org/jira/browse/CAMEL-24498)

camel-observability-services-starter - injected management defaults exceed the Spring Boot baseline

[CAMEL-24497](https://issues.apache.org/jira/browse/CAMEL-24497)

camel-undertow-spring-security-starter - JWT decoder is built without an issuer or audience validator

[CAMEL-24496](https://issues.apache.org/jira/browse/CAMEL-24496)

camel-platform-http-starter - align SpringBootPlatformHttpBinding multipart and path handling with the other HTTP bindings

[CAMEL-24492](https://issues.apache.org/jira/browse/CAMEL-24492)

Document that backport PRs (cherry-picks of an already-reviewed main PR) do not need reviewers and can be merged as-is

[CAMEL-24489](https://issues.apache.org/jira/browse/CAMEL-24489)

TypeConversionException prints 'from type: null' for anonymous/local classes (getCanonicalName() returns null)

[CAMEL-24487](https://issues.apache.org/jira/browse/CAMEL-24487)

camel-ftp/sftp/mina-sftp/azure-files/smb: contain remote consumer operations within the configured directory

[CAMEL-24478](https://issues.apache.org/jira/browse/CAMEL-24478)

camel-grpc - add a muteException consumer option

[CAMEL-24477](https://issues.apache.org/jira/browse/CAMEL-24477)

camel-cxf - add a muteException consumer option

[CAMEL-24476](https://issues.apache.org/jira/browse/CAMEL-24476)

camel-mina - add a muteException consumer option

[CAMEL-24474](https://issues.apache.org/jira/browse/CAMEL-24474)

camel-as2 - support TLS delivery of asynchronous MDNs via SSLContextParameters

[CAMEL-24473](https://issues.apache.org/jira/browse/CAMEL-24473)

camel-kafka: consumer/producer readiness health check does not detect a downed broker under group.protocol=consumer (AsyncKafkaConsumer)

[CAMEL-24467](https://issues.apache.org/jira/browse/CAMEL-24467)

Scripting languages (JS, MVEL, OGNL, python/python3) do not bind Exchange variables and hand-roll bindings instead of reusing ExchangeHelper.populateVariableMap

[CAMEL-24465](https://issues.apache.org/jira/browse/CAMEL-24465)

Paho MQTT consumers leak owned clients and threads after startup failures

[CAMEL-24460](https://issues.apache.org/jira/browse/CAMEL-24460)

JSpecify: Make ProducerTemplate Body Parameters Nullable

[CAMEL-24437](https://issues.apache.org/jira/browse/CAMEL-24437)

camel-oauth - authorization code flow sends no state, nonce or PKCE parameter

[CAMEL-24431](https://issues.apache.org/jira/browse/CAMEL-24431)

camel-as2 - bound the expansion of compressed entities before they are verified

[CAMEL-24428](https://issues.apache.org/jira/browse/CAMEL-24428)

camel-knative - add a muteException consumer option

[CAMEL-24422](https://issues.apache.org/jira/browse/CAMEL-24422)

camel-docling: make message body input-source interpretation explicit and configurable

[CAMEL-24421](https://issues.apache.org/jira/browse/CAMEL-24421)

camel-spring-redis: apply a configurable ObjectInputFilter to the default JDK serializer

[CAMEL-24418](https://issues.apache.org/jira/browse/CAMEL-24418)

HTTP producers - do not resolve property placeholders in message-supplied endpoint-URI override headers

[CAMEL-24416](https://issues.apache.org/jira/browse/CAMEL-24416)

camel-core - XmlConverter SAX parser factory is configured more permissively than the DOM factory in the same class

[CAMEL-24414](https://issues.apache.org/jira/browse/CAMEL-24414)

camel-core - resolve pollEnrich property placeholders at build time

[CAMEL-24406](https://issues.apache.org/jira/browse/CAMEL-24406)

camel-xml-jaxp: XmlConverter.toDOMDocument throws SAXParseException for non-XML content (Content is not allowed in prolog)

[CAMEL-24404](https://issues.apache.org/jira/browse/CAMEL-24404)

camel-base-engine: InternalRouteStartupManager re-throws consumer startup exceptions raw instead of wrapping in FailedToStartRouteException

[CAMEL-24402](https://issues.apache.org/jira/browse/CAMEL-24402)

threadNamePattern is constructed to early

[CAMEL-24399](https://issues.apache.org/jira/browse/CAMEL-24399)

camel-mcp-server: should add support for setting additional server metadata

[CAMEL-24395](https://issues.apache.org/jira/browse/CAMEL-24395)

camel-tui: Unify view and edit mode rendering to use a single TextArea-based path

[CAMEL-24394](https://issues.apache.org/jira/browse/CAMEL-24394)

camel-mcp-server: should add support for MCP resources

[CAMEL-24393](https://issues.apache.org/jira/browse/CAMEL-24393)

camel-tui: Source editor improvements for low-code editing experience

[CAMEL-24390](https://issues.apache.org/jira/browse/CAMEL-24390)

camel-mcp-server: export all tools via special tag

[CAMEL-24387](https://issues.apache.org/jira/browse/CAMEL-24387)

Add createSingletonService() to test-infra and migrate tests to singletons

[CAMEL-24386](https://issues.apache.org/jira/browse/CAMEL-24386)

Add camel.ai-observability.enabled as a first-class camel-main configuration option

[CAMEL-24374](https://issues.apache.org/jira/browse/CAMEL-24374)

Camel TUI: Add Ctrl+G Go to node popup for navigating to route nodes in Source editor

[CAMEL-24372](https://issues.apache.org/jira/browse/CAMEL-24372)

camel-tui - YAML editor: undo/redo, block-aware move/duplicate/delete for EIP nodes

[CAMEL-24370](https://issues.apache.org/jira/browse/CAMEL-24370)

camel-netty - resolve the shared deserialization filter in the object codecs and expose deserializationFilter on the endpoint

[CAMEL-24352](https://issues.apache.org/jira/browse/CAMEL-24352)

camel-jbang - Serve ai-tool routes over the MCP stdio transport

[CAMEL-24333](https://issues.apache.org/jira/browse/CAMEL-24333)

camel-ai-tool - structured tool output (outputSchema / structuredContent)

[CAMEL-24322](https://issues.apache.org/jira/browse/CAMEL-24322)

camel-openai tool-calling via AiToolRegistry

[CAMEL-24295](https://issues.apache.org/jira/browse/CAMEL-24295)

camel-core: mark the Simple nested option with security metadata

[CAMEL-24292](https://issues.apache.org/jira/browse/CAMEL-24292)

camel-sql, camel-sql-stored and camel-xslt: add opt-in gate for override headers for parity with sibling components

### New Feature (45)

[CAMEL-25491](https://issues.apache.org/jira/browse/CAMEL-25491)

camel-jbang - Add Semantic TUI inspection, evaluation and expert-aware completion

[CAMEL-25489](https://issues.apache.org/jira/browse/CAMEL-25489)

camel-jbang - add CLI commands to list and evaluate semantic definitions

[CAMEL-25333](https://issues.apache.org/jira/browse/CAMEL-25333)

Add component for feature flag evaluation using OpenFeature specification

[CAMEL-25311](https://issues.apache.org/jira/browse/CAMEL-25311)

camel-wolf-defender: Add a semantic expert for prompt-injection detection

[CAMEL-25263](https://issues.apache.org/jira/browse/CAMEL-25263)

camel-odata-starter: add the Spring Boot starter for the camel-odata component

[CAMEL-25185](https://issues.apache.org/jira/browse/CAMEL-25185)

camel-openfga-starter: add the Spring Boot starter for the camel-openfga component

[CAMEL-25148](https://issues.apache.org/jira/browse/CAMEL-25148)

camel-java-io - Lightweight Java DSL source to model parser (no compilation)

[CAMEL-25143](https://issues.apache.org/jira/browse/CAMEL-25143)

camel-jbang - TUI: AI project analysis that generates route descriptions and an integration summary, shown as AI-assisted and exposed via MCP and CLI

[CAMEL-25030](https://issues.apache.org/jira/browse/CAMEL-25030)

Supply a MQTT 3.1.1 component

[CAMEL-25029](https://issues.apache.org/jira/browse/CAMEL-25029)

camel-kafka - Add a consumer for Kafka share groups (KIP-932, Queues for Kafka)

[CAMEL-25028](https://issues.apache.org/jira/browse/CAMEL-25028)

camel-openfga: new component for relationship-based (Zanzibar/ReBAC) authorization decisions

[CAMEL-25027](https://issues.apache.org/jira/browse/CAMEL-25027)

camel-langchain4j-ingest - Add media modality to embed images, audio, video and PDF whole

[CAMEL-24988](https://issues.apache.org/jira/browse/CAMEL-24988)

camel-core: Add switch EIP for literal value-based endpoint dispatch

[CAMEL-24977](https://issues.apache.org/jira/browse/CAMEL-24977)

Add provider-agnostic semantic evaluation across Camel EIPs and error handling

[CAMEL-24913](https://issues.apache.org/jira/browse/CAMEL-24913)

camel-jev-starter: hand-craft the Spring Boot starter so the jev language can be configured

[CAMEL-24871](https://issues.apache.org/jira/browse/CAMEL-24871)

Add camel-jev component and evaluate semantic EIP integration

[CAMEL-24810](https://issues.apache.org/jira/browse/CAMEL-24810)

camel-jbang-mcp - tool that maps a class or package name to its Maven dependency, known dependencies first then Maven Central

[CAMEL-24802](https://issues.apache.org/jira/browse/CAMEL-24802)

camel-core - simple: add escape function for html/xml/json/sql/url special characters

[CAMEL-24794](https://issues.apache.org/jira/browse/CAMEL-24794)

camel-jbang - TUI Ollama tab showing local model performance (throughput, context, host, request log)

[CAMEL-24741](https://issues.apache.org/jira/browse/CAMEL-24741)

camel-opa - add an in-process WASM evaluation mode alongside the REST client

[CAMEL-24740](https://issues.apache.org/jira/browse/CAMEL-24740)

camel-opa - support batch policy evaluation

[CAMEL-24735](https://issues.apache.org/jira/browse/CAMEL-24735)

camel-spiffe - add a SpiffeSecurityPolicy to authorize on the peer SPIFFE ID

[CAMEL-24674](https://issues.apache.org/jira/browse/CAMEL-24674)

camel-openai: support the Batch API

[CAMEL-24673](https://issues.apache.org/jira/browse/CAMEL-24673)

camel-openai: verify and parse OpenAI webhook events

[CAMEL-24663](https://issues.apache.org/jira/browse/CAMEL-24663)

Camel TUI: ACP coding-agent provider for the AI panel

[CAMEL-24649](https://issues.apache.org/jira/browse/CAMEL-24649)

Customize 404/405 response body when using REST OpenApi componentc

[CAMEL-24641](https://issues.apache.org/jira/browse/CAMEL-24641)

camel-opa-starter: add the Spring Boot starter for the camel-opa component

[CAMEL-24634](https://issues.apache.org/jira/browse/CAMEL-24634)

camel-opa - new component to evaluate Open Policy Agent (Rego) policies against an Exchange

[CAMEL-24621](https://issues.apache.org/jira/browse/CAMEL-24621)

camel-langchain4j-ingest - document ingestion component: the missing ingestion half of RAG in Camel

[CAMEL-24617](https://issues.apache.org/jira/browse/CAMEL-24617)

Camel TUI: Add YAML DSL refactoring menu to Source tab editor (F5/Ctrl+R)

[CAMEL-24571](https://issues.apache.org/jira/browse/CAMEL-24571)

camel-spiffe: provide an SSLContextParameters backed by the SPIFFE Workload API (rotating mTLS)

[CAMEL-24565](https://issues.apache.org/jira/browse/CAMEL-24565)

camel-console: Authoritative typed response records so dev console OpenAPI response schemas are not empty

[CAMEL-24564](https://issues.apache.org/jira/browse/CAMEL-24564)

camel-console: Generate a static OpenAPI spec for all dev consoles and publish it in the camel-catalog

[CAMEL-24561](https://issues.apache.org/jira/browse/CAMEL-24561)

Integrate GenAI observability with Micrometer ObservationRegistry

[CAMEL-24560](https://issues.apache.org/jira/browse/CAMEL-24560)

Change GenAiUsage token fields from Integer to Long

[CAMEL-24559](https://issues.apache.org/jira/browse/CAMEL-24559)

Extend GenAI observability to additional AI producers

[CAMEL-24558](https://issues.apache.org/jira/browse/CAMEL-24558)

Add unconsumed property warning for camel.aiObservability.\* in BaseMainSupport

[CAMEL-24556](https://issues.apache.org/jira/browse/CAMEL-24556)

Add LangChain4jAgentObservabilityTest for span emission

[CAMEL-24555](https://issues.apache.org/jira/browse/CAMEL-24555)

Add GenAI observability configuration to camel-spring-boot

[CAMEL-24463](https://issues.apache.org/jira/browse/CAMEL-24463)

Introduce KeyValueRepository SPI to unify state store, idempotent, aggregation and cache repositories

[CAMEL-24377](https://issues.apache.org/jira/browse/CAMEL-24377)

Add json support to the CamelEvent

[CAMEL-24373](https://issues.apache.org/jira/browse/CAMEL-24373)

camel-alibaba - Add components for this cloud such as object storage and whatlese

[CAMEL-24367](https://issues.apache.org/jira/browse/CAMEL-24367)

Add camel-rest-postman component

[CAMEL-24337](https://issues.apache.org/jira/browse/CAMEL-24337)

Support Python 3

[CAMEL-23967](https://issues.apache.org/jira/browse/CAMEL-23967)

camel-openai: add image generation and edit operations

### Sub-task (23)

[CAMEL-25482](https://issues.apache.org/jira/browse/CAMEL-25482)

camel-dataweave - small conversion gaps (reduce without init, filter with index, fun overloads, do blocks, unless/otherwise)

[CAMEL-25481](https://issues.apache.org/jira/browse/CAMEL-25481)

camel-dataweave - XML fidelity (design spike)

[CAMEL-25480](https://issues.apache.org/jira/browse/CAMEL-25480)

camel-dataweave - match / case

[CAMEL-25479](https://issues.apache.org/jira/browse/CAMEL-25479)

camel-dataweave - number and date coercion

[CAMEL-25478](https://issues.apache.org/jira/browse/CAMEL-25478)

camel-dataweave - ranges and slicing

[CAMEL-25477](https://issues.apache.org/jira/browse/CAMEL-25477)

camel-dataweave - string interpolation and regex literals

[CAMEL-25476](https://issues.apache.org/jira/browse/CAMEL-25476)

camel-dataweave - object construction: conditional fields and object spread

[CAMEL-25475](https://issues.apache.org/jira/browse/CAMEL-25475)

camel-dataweave - use DataSonnet ds.\* library for DataWeave core functions

[CAMEL-25474](https://issues.apache.org/jira/browse/CAMEL-25474)

camel-dataweave - DataWeave null and selector semantics

[CAMEL-25473](https://issues.apache.org/jira/browse/CAMEL-25473)

camel-dataweave - DataWeave 2 lambda syntax and infix operator precedence

[CAMEL-25472](https://issues.apache.org/jira/browse/CAMEL-25472)

camel-dataweave - make fail-fast trustworthy: reject trailing tokens, unknown header lines, unknown functions and free variables

[CAMEL-25331](https://issues.apache.org/jira/browse/CAMEL-25331)

\[JDK 27\] printer component not working with JDk 27

[CAMEL-24971](https://issues.apache.org/jira/browse/CAMEL-24971)

simple - internal tidy-ups (dead code, duplication, per-exchange work)

[CAMEL-24970](https://issues.apache.org/jira/browse/CAMEL-24970)

simple - catalog, documentation and syntax hint fixes

[CAMEL-24969](https://issues.apache.org/jira/browse/CAMEL-24969)

simple - collection and misc function fixes

[CAMEL-24968](https://issues.apache.org/jira/browse/CAMEL-24968)

simple - string, math, date and file function fixes

[CAMEL-24967](https://issues.apache.org/jira/browse/CAMEL-24967)

simple - function argument parsing fixes (quotes, commas, parentheses, prefixes)

[CAMEL-24966](https://issues.apache.org/jira/browse/CAMEL-24966)

simple - operator and numeric literal fixes

[CAMEL-24965](https://issues.apache.org/jira/browse/CAMEL-24965)

simple - init block fixes (custom function leak, comments, one-liners, predicates)

[CAMEL-24964](https://issues.apache.org/jira/browse/CAMEL-24964)

simple - tokenizer and predicate parser fixes (quotes, braces, chain, ~> in text)

[CAMEL-24963](https://issues.apache.org/jira/browse/CAMEL-24963)

simple - ${properties:key:default} with a default containing an operator word is parsed as a predicate

[CAMEL-24639](https://issues.apache.org/jira/browse/CAMEL-24639)

camel-http: implement SecretRotationAware to refresh credentials on rotation

[CAMEL-24638](https://issues.apache.org/jira/browse/CAMEL-24638)

camel-jdbc/camel-sql: implement SecretRotationAware to rebuild the pool on rotation

### Task (37)

[CAMEL-25469](https://issues.apache.org/jira/browse/CAMEL-25469)

camel-openfeature - Add Spring Boot starter

[CAMEL-25266](https://issues.apache.org/jira/browse/CAMEL-25266)

Visible button to Camel Downloads on Main page and projects/

[CAMEL-25226](https://issues.apache.org/jira/browse/CAMEL-25226)

camel-fory: requireClassRegistration option missing security="insecure:serialization" annotation

[CAMEL-25119](https://issues.apache.org/jira/browse/CAMEL-25119)

camel-package-maven-plugin - prepare-catalog goal does not honour camel.prepare-catalog.skip

[CAMEL-24985](https://issues.apache.org/jira/browse/CAMEL-24985)

Dependency analysis Github wokflow is often failing with No plugin descriptor found at META-INF/maven/plugin.xml

[CAMEL-24979](https://issues.apache.org/jira/browse/CAMEL-24979)

camel-core - Deprecate exchange pooling

[CAMEL-24962](https://issues.apache.org/jira/browse/CAMEL-24962)

simple language - review findings: bugs and tidy-ups

[CAMEL-24939](https://issues.apache.org/jira/browse/CAMEL-24939)

\[build\] Fix dependency declarations in core/ and tooling/ subprojects

[CAMEL-24930](https://issues.apache.org/jira/browse/CAMEL-24930)

Resequence EIP docs say the last of duplicate messages is kept, but the first one is kept

[CAMEL-24914](https://issues.apache.org/jira/browse/CAMEL-24914)

Spring Boot starter generator: define behaviour for languages using @Language(modelName = "language")

[CAMEL-24900](https://issues.apache.org/jira/browse/CAMEL-24900)

camel-jcr - apply header filtering when mapping JCR node properties to Exchange headers

[CAMEL-24895](https://issues.apache.org/jira/browse/CAMEL-24895)

camel-mustache, camel-chunk - align Exchange header constant names with Camel naming convention

[CAMEL-24827](https://issues.apache.org/jira/browse/CAMEL-24827)

camel-jbang-core: sync the bundled examples with the revamped camel-jbang-examples (new groups and paths) and derive the bundle list from the catalog

[CAMEL-24817](https://issues.apache.org/jira/browse/CAMEL-24817)

camel-elasticsearch/camel-opensearch: fix scroll-keep-alive header description and deprecate the unused maxRetryTimeout option

[CAMEL-24791](https://issues.apache.org/jira/browse/CAMEL-24791)

camel-slack: use obvious placeholders for webhookUrl and token in the component documentation

[CAMEL-24790](https://issues.apache.org/jira/browse/CAMEL-24790)

camel-oauth: remove unused expired demo certificate and private key from helm/etc

[CAMEL-24777](https://issues.apache.org/jira/browse/CAMEL-24777)

GitHub action failure for very long jobs: 'Broken pipe'

[CAMEL-24773](https://issues.apache.org/jira/browse/CAMEL-24773)

docs - the remaining example kinds: Camel 1.x XML namespace, Camel 2 XML elements, malformed XML fragments, wrong Java imports, and user-manual YAML

[CAMEL-24770](https://issues.apache.org/jira/browse/CAMEL-24770)

docs - Java, XML and properties examples in the documentation are out of date or wrong

[CAMEL-24755](https://issues.apache.org/jira/browse/CAMEL-24755)

camel-sql-stored - align the resource schemes named in the CAMEL-24292 upgrade-guide entry

[CAMEL-24750](https://issues.apache.org/jira/browse/CAMEL-24750)

Deprecate MinIO

[CAMEL-24710](https://issues.apache.org/jira/browse/CAMEL-24710)

docs - about 375 YAML route examples in the component and data format documentation do not validate

[CAMEL-24696](https://issues.apache.org/jira/browse/CAMEL-24696)

camel-core-model: port inheritErrorHandler to a String field so property placeholders work

[CAMEL-24648](https://issues.apache.org/jira/browse/CAMEL-24648)

camel-openai: add storeFullResponse tests for audio operations and document storeFullResponse for embeddings/audio

[CAMEL-24635](https://issues.apache.org/jira/browse/CAMEL-24635)

Cleanup obsolete dependencies

[CAMEL-24624](https://issues.apache.org/jira/browse/CAMEL-24624)

camel-infinispan: catalog, lifecycle and efficiency cleanups

[CAMEL-24603](https://issues.apache.org/jira/browse/CAMEL-24603)

Document JIRA workflow transition IDs in AGENTS.md for AI agents

[CAMEL-24587](https://issues.apache.org/jira/browse/CAMEL-24587)

CI: PR incremental build tests the whole project when a core module changes (Scalpel modules bypass the 50-module threshold)

[CAMEL-24579](https://issues.apache.org/jira/browse/CAMEL-24579)

DataFormat.marshal graph parameter should be @Nullable

[CAMEL-24572](https://issues.apache.org/jira/browse/CAMEL-24572)

Use xtokenize as a language in the YAML DSL

[CAMEL-24557](https://issues.apache.org/jira/browse/CAMEL-24557)

Remove stale langchain4j-tools references from AI observability docs

[CAMEL-24549](https://issues.apache.org/jira/browse/CAMEL-24549)

camel-google-storage: Use symlink-aware containment for local downloads

[CAMEL-24548](https://issues.apache.org/jira/browse/CAMEL-24548)

camel-azure-storage: Use symlink-aware containment for local downloads

[CAMEL-24547](https://issues.apache.org/jira/browse/CAMEL-24547)

camel-jbang - Upgrade Camel Kamelets to 4.22.0

[CAMEL-24420](https://issues.apache.org/jira/browse/CAMEL-24420)

camel-hazelcast: Apply the default JavaSerializationFilterConfig to Camel-built client configurations

[CAMEL-24356](https://issues.apache.org/jira/browse/CAMEL-24356)

\[camel-micrometer\] Support logOnShutdownFormat in all runtimes

[CAMEL-24339](https://issues.apache.org/jira/browse/CAMEL-24339)

camel-openai - Can the name be updated to better hint it works for many vendor LLMs

### Test (35)

[CAMEL-25464](https://issues.apache.org/jira/browse/CAMEL-25464)

SemanticCompletionTest.completionFollowsNamedQuestionMapAndOffersVariantFields is broken

[CAMEL-25344](https://issues.apache.org/jira/browse/CAMEL-25344)

InfinispanRemoteQueryProducerIT and InfinispanRemoteQueryConsumerIT are failing with podman

[CAMEL-25343](https://issues.apache.org/jira/browse/CAMEL-25343)

Fix flaky test SshIdleTimeoutTest.testIdleTimeoutExpiresBeforeCommandCompletes

[CAMEL-25342](https://issues.apache.org/jira/browse/CAMEL-25342)

Fix flaky test NatsConsumerIT

[CAMEL-25341](https://issues.apache.org/jira/browse/CAMEL-25341)

LRA\*IT tests are failing with podman

[CAMEL-25339](https://issues.apache.org/jira/browse/CAMEL-25339)

InfinispanRemoteEmbeddingStoreIT is failing with podman

[CAMEL-25271](https://issues.apache.org/jira/browse/CAMEL-25271)

Avoid camel-jms test to create log file at the root module

[CAMEL-25228](https://issues.apache.org/jira/browse/CAMEL-25228)

IdentityRoutesTest.describesTheX509SvidWithoutRevealingTheKey is broken

[CAMEL-25206](https://issues.apache.org/jira/browse/CAMEL-25206)

camel-yaml-dsl - round-trip test of the YAML DSL writer and reader over the XML route corpus

[CAMEL-25191](https://issues.apache.org/jira/browse/CAMEL-25191)

Fix flaky test MainNotAutoConfiguredWarningTest

[CAMEL-24989](https://issues.apache.org/jira/browse/CAMEL-24989)

Overridden test methods without @Test are silently skipped in SpringSamplingThrottlerTest and an MLLP test

[CAMEL-24957](https://issues.apache.org/jira/browse/CAMEL-24957)

Fix flaky test MessageHistoryExceptionRouteTest

[CAMEL-24903](https://issues.apache.org/jira/browse/CAMEL-24903)

Fix flaky test ThrottlingExceptionRoutePolicyOpenViaConfigTest

[CAMEL-24829](https://issues.apache.org/jira/browse/CAMEL-24829)

windows-validator: each install.ps1 test launch costs ~24s, keeping the PowerShell suite near 20 minutes

[CAMEL-24787](https://issues.apache.org/jira/browse/CAMEL-24787)

Fix flaky tests Cassandra failing with Query timed out after PT5S

[CAMEL-24772](https://issues.apache.org/jira/browse/CAMEL-24772)

camel-jbang: OllamaDoctorSupportTest.detectReturnsNotRunningWhenEndpointUnreachable fails on any machine running Ollama

[CAMEL-24763](https://issues.apache.org/jira/browse/CAMEL-24763)

Fix flaky test ReactorStreamsServiceTest

[CAMEL-24762](https://issues.apache.org/jira/browse/CAMEL-24762)

Fix flaky test CoAPComponentTLSTest

[CAMEL-24742](https://issues.apache.org/jira/browse/CAMEL-24742)

camel-opa - compile Rego fixtures to WASM in test-infra for the in-process mode

[CAMEL-24733](https://issues.apache.org/jira/browse/CAMEL-24733)

camel-spiffe - add integration tests against a real SPIRE agent

[CAMEL-24660](https://issues.apache.org/jira/browse/CAMEL-24660)

3 Camel JBang InfrastructureITCase tests are failing

[CAMEL-24655](https://issues.apache.org/jira/browse/CAMEL-24655)

camel-coap: add regression test for case-insensitive Camel header filtering in the consumer

[CAMEL-24647](https://issues.apache.org/jira/browse/CAMEL-24647)

Camel JBang IT tests failing with BindException: Address already in use

[CAMEL-24645](https://issues.apache.org/jira/browse/CAMEL-24645)

camel-opa - cover the bearerToken option with an integration test

[CAMEL-24618](https://issues.apache.org/jira/browse/CAMEL-24618)

Fix flaky test SpringFileAntPathMatcherRemoteFileFilterTest.testAntPatchMatcherFilter

[CAMEL-24615](https://issues.apache.org/jira/browse/CAMEL-24615)

camel-jpa - hibernate test profile is not runnable and has failing tests

[CAMEL-24601](https://issues.apache.org/jira/browse/CAMEL-24601)

Fix flaky test SmbComponentConnectionIT.testSendReceive

[CAMEL-24597](https://issues.apache.org/jira/browse/CAMEL-24597)

Fix flaky test MailAttachmentDuplicateNamesTest.testSendAndReceiveMailWithAttachmentsWithDuplicateNames <Hello World> but was: <jakarta.mail.internet.MimeMultipart@XXXXX>

[CAMEL-24586](https://issues.apache.org/jira/browse/CAMEL-24586)

Milvus ITtests are failing very often on pp64le: ailed to initialize connection. Error: UNKNOWN: service unavailable: internal: Milvus Proxy is not ready yet. please wait

[CAMEL-24485](https://issues.apache.org/jira/browse/CAMEL-24485)

windows-validator github workflow is very unstable

[CAMEL-24481](https://issues.apache.org/jira/browse/CAMEL-24481)

Most (all?) Camel Jbang IT tests are failig with main branch on Jenkins due to docker image whcih cannot be built

[CAMEL-24469](https://issues.apache.org/jira/browse/CAMEL-24469)

Crashed tests: org.apache.camel.dsl.jbang.core.common.PluginHelperTest on 4.22.x branch

[CAMEL-24458](https://issues.apache.org/jira/browse/CAMEL-24458)

Cassandra Integration Tests are broken on s390x

[CAMEL-24038](https://issues.apache.org/jira/browse/CAMEL-24038)

Fix flaky AsyncWiretapTest in camel-telemetry and camel-telemetry-dev

[CAMEL-24029](https://issues.apache.org/jira/browse/CAMEL-24029)

Fix flaky camel-core tests using timed assertions

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).