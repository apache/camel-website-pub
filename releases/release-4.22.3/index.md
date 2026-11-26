# Apache camel 4.22.3 Release

## New and Noteworthy

This release is the new Camel 4.22.3 LTS release.

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
      <version>4.22.3</version>
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
      <version>4.22.3</version>
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
| [apache-camel-4.22.3-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.3/apache-camel-4.22.3-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-src.zip.sha512) |
| [apache-camel-4.22.3-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.xml.sha512) |
| [apache-camel-4.22.3-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.3/apache-camel-4.22.3-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.22.3` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.22.3

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (113)

[CAMEL-27449](https://issues.apache.org/jira/browse/CAMEL-27449)

camel-crypto-pgp - decrypt OCB (AEAD) messages of current GnuPG, which are integrity protected

[CAMEL-27255](https://issues.apache.org/jira/browse/CAMEL-27255)

camel-mllp - the initial read of a connection logs the data it received although logPhi is false

[CAMEL-27229](https://issues.apache.org/jira/browse/CAMEL-27229)

camel-ftp - ftps checks the server certificate against the JVM trust store when no trust store is configured

[CAMEL-27228](https://issues.apache.org/jira/browse/CAMEL-27228)

camel-vertx-http - an https:// address is called with TLS also when no sslContextParameters is configured

[CAMEL-27226](https://issues.apache.org/jira/browse/CAMEL-27226)

camel-google-drive, camel-google-mail - the OAuth access token is sent only in the Authorization header

[CAMEL-27224](https://issues.apache.org/jira/browse/CAMEL-27224)

camel-snmp - the trap consumer should apply snmpVersion and the SNMPv3 user and security level of its endpoint

[CAMEL-27218](https://issues.apache.org/jira/browse/CAMEL-27218)

camel-mongodb - the tls and tlsAllowInvalidHostnames options are not applied to the client created from hosts or connectionUriString

[CAMEL-27208](https://issues.apache.org/jira/browse/CAMEL-27208)

camel-grpc - a producer with streamRepliesTo completes a failed call as a success, so the error is lost

[CAMEL-27160](https://issues.apache.org/jira/browse/CAMEL-27160)

camel-core - treat dynamic endpoint option values from the message as literals

[CAMEL-27110](https://issues.apache.org/jira/browse/CAMEL-27110)

camel-jbang - camel bind on camel-4.18.x fails when a property value or a Kamelet example holds ${...}

[CAMEL-27077](https://issues.apache.org/jira/browse/CAMEL-27077)

camel-quartz - a scheduler from the registry that is already running (spring-boot-starter-quartz) fails the jobs that fire before the CamelContext is fully started

[CAMEL-27072](https://issues.apache.org/jira/browse/CAMEL-27072)

camel-kamelet-main: Detect bundled Kamelets versions outside java.class.path

[CAMEL-27062](https://issues.apache.org/jira/browse/CAMEL-27062)

camel-cxf, camel-cxfrs - the producers ignore the former operationName header without a hint, and send it as an HTTP header

[CAMEL-27054](https://issues.apache.org/jira/browse/CAMEL-27054)

camel-ftp - refuse a file or directory name with a carriage return or line feed

[CAMEL-27049](https://issues.apache.org/jira/browse/CAMEL-27049)

camel-main - mask the server and vault options flagged secret

[CAMEL-26986](https://issues.apache.org/jira/browse/CAMEL-26986)

camel-jdbc - the producer does not close a connection that already reports isClosed(), so an Agroal pool loses one connection per connection error

[CAMEL-26978](https://issues.apache.org/jira/browse/CAMEL-26978)

camel-kafka: an async manual commit after an aggregator fails with ConcurrentModificationException

[CAMEL-26977](https://issues.apache.org/jira/browse/CAMEL-26977)

camel-file: idempotent=true or noop=true with readLock=idempotent never consumes a file

[CAMEL-26976](https://issues.apache.org/jira/browse/CAMEL-26976)

camel-xslt: transformerFactoryConfigurationStrategy ignored for the default factory, secureProcessing ignored with a saxonConfiguration bean

[CAMEL-26975](https://issues.apache.org/jira/browse/CAMEL-26975)

camel-csv: an empty header marshals Map rows as empty lines

[CAMEL-26967](https://issues.apache.org/jira/browse/CAMEL-26967)

camel-kafka - breakOnFirstError with synchronous manual commits: a commitSync timeout in the break skips the failed record and the rest of the poll

[CAMEL-26945](https://issues.apache.org/jira/browse/CAMEL-26945)

camel-core - the time an inflight exchange has been at its node is garbage: MessageHistory.getElapsedSinceCreated() subtracts wall clock millis from System.nanoTime()

[CAMEL-26928](https://issues.apache.org/jira/browse/CAMEL-26928)

camel-file - jailStartingDirectory also checks links in consumer move targets

[CAMEL-26927](https://issues.apache.org/jira/browse/CAMEL-26927)

camel-wordpress - each endpoint should use its own site URL and credentials

[CAMEL-26926](https://issues.apache.org/jira/browse/CAMEL-26926)

camel-jbang: Spring Boot/Quarkus catalogs mix requested and server versions

[CAMEL-26925](https://issues.apache.org/jira/browse/CAMEL-26925)

camel-sftp - use remote file names literally when calling JSch

[CAMEL-26891](https://issues.apache.org/jira/browse/CAMEL-26891)

camel-whatsapp - do not log the response body at INFO

[CAMEL-26782](https://issues.apache.org/jira/browse/CAMEL-26782)

camel-spring-boot: copyConfigurationProperties drops values assigned in Java to a starter configuration bean

[CAMEL-26779](https://issues.apache.org/jira/browse/CAMEL-26779)

camel-snmp - the consumer can run its first poll before it is started, and fails with a NullPointerException

[CAMEL-26710](https://issues.apache.org/jira/browse/CAMEL-26710)

camel-core - Split EIP with a resume strategy hangs when the watermark cannot be evaluated or stored

[CAMEL-26696](https://issues.apache.org/jira/browse/CAMEL-26696)

camel-cxf: async producer may never complete the exchange when the connection fails

[CAMEL-26647](https://issues.apache.org/jira/browse/CAMEL-26647)

camel-google-pubsub - manual ack of an aggregated exchange (synchronousPull) acks none of the grouped messages

[CAMEL-26646](https://issues.apache.org/jira/browse/CAMEL-26646)

camel-couchdb - maxMessagesPerPoll 0 or negative, documented as unlimited, is sent as the CouchDB \_changes limit

[CAMEL-26640](https://issues.apache.org/jira/browse/CAMEL-26640)

Route level StreamCachingAdvice fails exchange with "Cannot reset stream from file" when using spooled stream cache

[CAMEL-26637](https://issues.apache.org/jira/browse/CAMEL-26637)

camel-azure-cosmosdb - createContainer does not normalize the partition key path

[CAMEL-26611](https://issues.apache.org/jira/browse/CAMEL-26611)

camel-micrometer - use tags and attributes from headers as given

[CAMEL-26606](https://issues.apache.org/jira/browse/CAMEL-26606)

camel-platform-http-vertx - a failed bind of the HTTP server is only logged, so the CamelContext starts with nothing listening

[CAMEL-26603](https://issues.apache.org/jira/browse/CAMEL-26603)

camel-core - Aggregate EIP: forceCompletionOnStop loses the messages that the consumer routes during the graceful shutdown

[CAMEL-26596](https://issues.apache.org/jira/browse/CAMEL-26596)

FileConsumer calls super.doStart() twice causing duplicate scheduling

[CAMEL-26586](https://issues.apache.org/jira/browse/CAMEL-26586)

camel-google-storage - close the upload stream after a failure

[CAMEL-26585](https://issues.apache.org/jira/browse/CAMEL-26585)

camel-aws2-sns - escape string members of array attributes

[CAMEL-26584](https://issues.apache.org/jira/browse/CAMEL-26584)

camel-aws-bedrock - clear the retrieve token on the last page

[CAMEL-26581](https://issues.apache.org/jira/browse/CAMEL-26581)

camel-google-calendar - follow all pages in stream polling

[CAMEL-26565](https://issues.apache.org/jira/browse/CAMEL-26565)

\[camel-micrometer\] Regression and reduced metrics retrieval performances

[CAMEL-26550](https://issues.apache.org/jira/browse/CAMEL-26550)

camel-grpc - with consumerStrategy=PROPAGATION and routeControlledStreamObserver=true the route cannot control the reply

[CAMEL-26545](https://issues.apache.org/jira/browse/CAMEL-26545)

the post-quantum named group auto-configuration races on a shared SSLContextParameters and only looks for X25519MLKEM768

[CAMEL-26533](https://issues.apache.org/jira/browse/CAMEL-26533)

camel-jpa - bind CamelJpaParameters header values literally

[CAMEL-26490](https://issues.apache.org/jira/browse/CAMEL-26490)

camel-telemetry - the http.url, url.path and server.address span attributes should be presented like camel.uri

[CAMEL-26488](https://issues.apache.org/jira/browse/CAMEL-26488)

camel-mina - sync producer always closes a timed-out session

[CAMEL-26487](https://issues.apache.org/jira/browse/CAMEL-26487)

camel-netty-http - endpoints that differ only in their options should be distinct endpoints

[CAMEL-26485](https://issues.apache.org/jira/browse/CAMEL-26485)

camel-netty-http - endpoint options such as cookieHandler and httpMethodRestrict are sent to the server as query parameters

[CAMEL-26425](https://issues.apache.org/jira/browse/CAMEL-26425)

camel-as2 - signature verification and MDN MIC are computed over a re-serialisation of the signed part, not over the bytes received

[CAMEL-26404](https://issues.apache.org/jira/browse/CAMEL-26404)

camel-oauth: validate audience and authorized party claims for access tokens in UserProfile

[CAMEL-26370](https://issues.apache.org/jira/browse/CAMEL-26370)

{{camel export --local-kamelet-dir=<dir1>,<dir2>}} silently produces a broken export when more than one directory is supplied on the 4.22.x branch.

[CAMEL-26367](https://issues.apache.org/jira/browse/CAMEL-26367)

camel-aws: AwsClientBuilderUtil shares the DefaultCredentialsProvider singleton across clients; closing one endpoint breaks all others ("Connection pool shut down")

[CAMEL-26343](https://issues.apache.org/jira/browse/CAMEL-26343)

camel-aws - set the AWS SDK HTTP client explicitly instead of the classpath lookup

[CAMEL-26340](https://issues.apache.org/jira/browse/CAMEL-26340)

camel-lra: validate coordinator URL returned when starting a new saga against allowed coordinators

[CAMEL-26336](https://issues.apache.org/jira/browse/CAMEL-26336)

camel-minio: MinioProducer should apply configured serverSideEncryption and serverSideEncryptionCustomerKey options

[CAMEL-26335](https://issues.apache.org/jira/browse/CAMEL-26335)

camel-cometd - configure allowedTransports and disable callback-polling by default

[CAMEL-26327](https://issues.apache.org/jira/browse/CAMEL-26327)

camel-core - Routing Slip / Dynamic Router: a redelivered step hangs forever when the route it called used a routing slip or dynamic router itself

[CAMEL-26323](https://issues.apache.org/jira/browse/CAMEL-26323)

camel-shiro: ShiroSecurityProcessor should authenticate against policy security manager

[CAMEL-26319](https://issues.apache.org/jira/browse/CAMEL-26319)

camel-oauth: InMemorySessionStore should not log session identifiers and OAuthCodeFlowCallback should rotate session identifiers on login

[CAMEL-26318](https://issues.apache.org/jira/browse/CAMEL-26318)

camel-stripe: StripeProducer should use request options instead of mutating JVM-global Stripe settings

[CAMEL-26306](https://issues.apache.org/jira/browse/CAMEL-26306)

camel-as2 - a CRLF whose CR is the last byte of an 8 KB read of the line reader loses its CR: the received EDI message changes and its signature fails

[CAMEL-26301](https://issues.apache.org/jira/browse/CAMEL-26301)

tokenizer EIP: an exception of the tokenizer, such as for a null body, hangs the exchange forever

[CAMEL-26287](https://issues.apache.org/jira/browse/CAMEL-26287)

camel-jcache - stopping a jcache endpoint closes the caching provider, so removing one route breaks the caches of every other jcache endpoint

[CAMEL-26278](https://issues.apache.org/jira/browse/CAMEL-26278)

camel-hazelcast - the hazelcast-seda consumer restores the headers and properties of an exchange holder even with transferExchange=false

[CAMEL-26256](https://issues.apache.org/jira/browse/CAMEL-26256)

camel-cyberark-vault - with authToken, a 401 makes the client retry with the same token until a StackOverflowError, and no credentials gives a NullPointerException

[CAMEL-26164](https://issues.apache.org/jira/browse/CAMEL-26164)

camel-whatsapp - the webhook fails with ArrayIndexOutOfBoundsException on an empty query value and does not URL-decode query values

[CAMEL-26162](https://issues.apache.org/jira/browse/CAMEL-26162)

camel-workday - the token request sends the Basic header as Arrays.toString of the bytes, so getting an access token fails

[CAMEL-26141](https://issues.apache.org/jira/browse/CAMEL-26141)

camel-atmosphere-websocket - a query parameter without a value fails with ArrayIndexOutOfBoundsException, and useStreaming is documented for sending but only used by the consumer

[CAMEL-26130](https://issues.apache.org/jira/browse/CAMEL-26130)

camel-oaipmh - the CamelOaimphOnlyFirst header is stored on the shared endpoint, so all later requests return only the first page

[CAMEL-26118](https://issues.apache.org/jira/browse/CAMEL-26118)

camel-flowable - a producer created before its channel is deployed fails every send with a NullPointerException, and the doc gives the wrong URI scheme

[CAMEL-26105](https://issues.apache.org/jira/browse/CAMEL-26105)

camel-aws2-athena - take the SQL from the body only with useMessageBodyForSql

[CAMEL-26068](https://issues.apache.org/jira/browse/CAMEL-26068)

camel-netty-http - Ensure NettyHttpSecurityConfiguration is copied per endpoint

[CAMEL-26065](https://issues.apache.org/jira/browse/CAMEL-26065)

camel-netty-http - key multiplex channel handlers by listener address

[CAMEL-26028](https://issues.apache.org/jira/browse/CAMEL-26028)

camel-support - the error of a failed API component call shows the values of the endpoint options, passwords and tokens too

[CAMEL-26027](https://issues.apache.org/jira/browse/CAMEL-26027)

camel-telegram - concurrent sends through one endpoint mix up the parts of their requests

[CAMEL-25994](https://issues.apache.org/jira/browse/CAMEL-25994)

camel-undertow - WebSocket: keep the OAuth validation of a connection per endpoint, like the other security checks

[CAMEL-25992](https://issues.apache.org/jira/browse/CAMEL-25992)

camel-pqc - sign and verify File and Path bodies over their raw bytes

[CAMEL-25984](https://issues.apache.org/jira/browse/CAMEL-25984)

camel-cometd - CORS filter should not allow credentials for wildcard origins

[CAMEL-25983](https://issues.apache.org/jira/browse/CAMEL-25983)

camel-github2 - getCommitFile passes the commit sha to getBlob, never uses the file path, and decodes the content with the wrong base64 decoder

[CAMEL-25979](https://issues.apache.org/jira/browse/CAMEL-25979)

camel-language - compile a script from the CamelLanguageScript header once, never keep it as the script of the endpoint, and remove the header after use

[CAMEL-25964](https://issues.apache.org/jira/browse/CAMEL-25964)

camel-vertx - VertxHelper does not apply standalone TrustManager from SSLContextParameters

[CAMEL-25931](https://issues.apache.org/jira/browse/CAMEL-25931)

camel-a2a - an agent that calls another agent mixes their headers: the producer runs the operation of the consumer, and the reply takes the other agent's task

[CAMEL-25921](https://issues.apache.org/jira/browse/CAMEL-25921)

camel-jbang - plugins resolve with no dependencies (or are re-downloaded) when the local Maven repository was written by Maven 3.10

[CAMEL-25918](https://issues.apache.org/jira/browse/CAMEL-25918)

camel-as2 - consumers sharing a port use their own asynchronous MDN settings

[CAMEL-25895](https://issues.apache.org/jira/browse/CAMEL-25895)

camel-openstack - use Camel-prefixed names for the remaining Swift headers

[CAMEL-25888](https://issues.apache.org/jira/browse/CAMEL-25888)

camel-pubnub - the producer should not use the consumer's channel header

[CAMEL-25875](https://issues.apache.org/jira/browse/CAMEL-25875)

camel-milo - a sessionTimeout configured on the component does not reach its endpoints

[CAMEL-25860](https://issues.apache.org/jira/browse/CAMEL-25860)

camel-core - pollEnrich: after a timeout, a message that creates its body on demand (such as of a file consumer) brings its body back instead of null

[CAMEL-25827](https://issues.apache.org/jira/browse/CAMEL-25827)

camel-xslt-saxon - apply endpoint factory settings to the aggregation strategy

[CAMEL-25793](https://issues.apache.org/jira/browse/CAMEL-25793)

camel-paho-mqtt5 - with manualAcksEnabled a failed message is never retried, and after receiveMaximum failures the consumer receives nothing more

[CAMEL-25787](https://issues.apache.org/jira/browse/CAMEL-25787)

camel-smooks - handle Smooks Source bodies like other XML message bodies

[CAMEL-25779](https://issues.apache.org/jira/browse/CAMEL-25779)

camel-jms: JmsMessage loses attachments when the exchange is copied

[CAMEL-25778](https://issues.apache.org/jira/browse/CAMEL-25778)

camel-file - the consumer can route a file twice when the exchange is completed on another thread

[CAMEL-25734](https://issues.apache.org/jira/browse/CAMEL-25734)

camel-core - Starting Camel can fail with a ConcurrentModificationException in DefaultBeanIntrospection

[CAMEL-25708](https://issues.apache.org/jira/browse/CAMEL-25708)

camel-opensearch - bind the basic authentication credentials to the cluster nodes

[CAMEL-25707](https://issues.apache.org/jira/browse/CAMEL-25707)

camel-elasticsearch-rest-client - bind the basic authentication credentials to the cluster nodes

[CAMEL-25706](https://issues.apache.org/jira/browse/CAMEL-25706)

camel-elasticsearch - bind the basic authentication credentials to the cluster nodes

[CAMEL-25705](https://issues.apache.org/jira/browse/CAMEL-25705)

camel-netty-http - normalize dot-segments in the request path used for security constraint matching

[CAMEL-25704](https://issues.apache.org/jira/browse/CAMEL-25704)

camel-undertow - the producer refuses a request target or header value it cannot write as it is

[CAMEL-25694](https://issues.apache.org/jira/browse/CAMEL-25694)

camel-milo - awaited write/call service failures are reported as success

[CAMEL-25645](https://issues.apache.org/jira/browse/CAMEL-25645)

camel-milo - let the OPC UA client validate the server certificate against a trust list

[CAMEL-25644](https://issues.apache.org/jira/browse/CAMEL-25644)

camel-ssh - match known\_hosts entries by exact host pattern

[CAMEL-25461](https://issues.apache.org/jira/browse/CAMEL-25461)

camel-thrift - consumer: apply the client authentication of sslParameters

[CAMEL-25459](https://issues.apache.org/jira/browse/CAMEL-25459)

camel-thrift - consumer: fail at startup when negotiationType cannot be applied

[CAMEL-25458](https://issues.apache.org/jira/browse/CAMEL-25458)

camel-a2a - improve how the consumer derives the caller profile

[CAMEL-25297](https://issues.apache.org/jira/browse/CAMEL-25297)

camel-direct, camel-kamelet - while one exchange waits for the consumer of a suspended or stopped route, the other exchanges of the same producer are sent to that route

[CAMEL-25125](https://issues.apache.org/jira/browse/CAMEL-25125)

camel-mllp - automatic acknowledgement fails with ArrayIndexOutOfBoundsException when MSH-2 defines a component separator other than '^', so no ACK is sent (regression of CAMEL-22421)

[CAMEL-25105](https://issues.apache.org/jira/browse/CAMEL-25105)

camel-netty - The client authentication of sslContextParameters is overridden by needClientAuth=false

[CAMEL-24935](https://issues.apache.org/jira/browse/CAMEL-24935)

camel-pulsar - the producer replaces the message body with the MessageId

[CAMEL-24747](https://issues.apache.org/jira/browse/CAMEL-24747)

KameletComponent URL encodes kamelet parameters

### Dependency upgrade (1)

[CAMEL-27254](https://issues.apache.org/jira/browse/CAMEL-27254)

camel-spring-boot - Upgrade to SB 4.1.3

### Improvement (37)

[CAMEL-27225](https://issues.apache.org/jira/browse/CAMEL-27225)

camel-redis - RedisAggregationRepository stores exchanges in Java serialization and reads them through a deserialization filter

[CAMEL-27222](https://issues.apache.org/jira/browse/CAMEL-27222)

camel-platform-http-main, camel-netty-http, camel-undertow - remove the Authorization header after the login is checked

[CAMEL-27207](https://issues.apache.org/jira/browse/CAMEL-27207)

camel-pulsar - check the host name in the certificate of the broker with pulsar+ssl

[CAMEL-27196](https://issues.apache.org/jira/browse/CAMEL-27196)

camel-pulsar - add an option for a custom CA trust store file

[CAMEL-27116](https://issues.apache.org/jira/browse/CAMEL-27116)

camel-file, camel-ftp, camel-smb - noop with delete or move, a fileName with wildcards and a classpath: directory start silently, and include=\*.xml fails with only the regex parser message

[CAMEL-27052](https://issues.apache.org/jira/browse/CAMEL-27052)

camel-jaxb - use the part class and namespace headers only when allowed

[CAMEL-26923](https://issues.apache.org/jira/browse/CAMEL-26923)

camel-duckdb - copy loads one local file unless options allow URLs or globs

[CAMEL-26922](https://issues.apache.org/jira/browse/CAMEL-26922)

camel-atmosphere-websocket - events use their connection's query parameters

[CAMEL-26921](https://issues.apache.org/jira/browse/CAMEL-26921)

camel-oaipmh - remove the CamelOaimphIgnoreSSLWarnings producer header

[CAMEL-26766](https://issues.apache.org/jira/browse/CAMEL-26766)

camel-jbang - Support custom plugin configuration path

[CAMEL-26644](https://issues.apache.org/jira/browse/CAMEL-26644)

camel-file: getFile() and getDirectory() return inconsistent path separators on Linux/macOS

[CAMEL-26587](https://issues.apache.org/jira/browse/CAMEL-26587)

camel-netty: NettyPayloadHelper should check transferExchange before processing transferred exchange objects

[CAMEL-26508](https://issues.apache.org/jira/browse/CAMEL-26508)

camel-netty - with transferExchange the consumer keeps its own connection headers

[CAMEL-26481](https://issues.apache.org/jira/browse/CAMEL-26481)

camel-syslog: Rfc5425FrameDecoder should handle fragmented length fields

[CAMEL-26415](https://issues.apache.org/jira/browse/CAMEL-26415)

\[camel-micrometer\] Reduce the time to lookup camel\_exchanges\_last\_timestamp

[CAMEL-26344](https://issues.apache.org/jira/browse/CAMEL-26344)

camel-jbang - plugin add: select community plugin versions built for the installed CLI's minor line

[CAMEL-26284](https://issues.apache.org/jira/browse/CAMEL-26284)

camel-azure-storage-blob - validate the source account and container name in copyBlob

[CAMEL-26283](https://issues.apache.org/jira/browse/CAMEL-26283)

camel-elasticsearch-rest-client - encode document id and index name in the path

[CAMEL-26282](https://issues.apache.org/jira/browse/CAMEL-26282)

camel-flowable - xml inbound channels parse events with the Camel XML settings

[CAMEL-26281](https://issues.apache.org/jira/browse/CAMEL-26281)

camel-whatsapp - verify the webhook event signature by default

[CAMEL-26280](https://issues.apache.org/jira/browse/CAMEL-26280)

camel-azure-functions - validate the function app and name in invokeFunction

[CAMEL-26276](https://issues.apache.org/jira/browse/CAMEL-26276)

camel-clickup - compare the webhook signature in constant time, and do not log it

[CAMEL-26109](https://issues.apache.org/jira/browse/CAMEL-26109)

camel-vertx-websocket - fail to start when consumers on the same host and port use different SSLContextParameters

[CAMEL-26066](https://issues.apache.org/jira/browse/CAMEL-26066)

camel-jsch - the scp producer should refuse a file name with a line feed or a NUL character

[CAMEL-26042](https://issues.apache.org/jira/browse/CAMEL-26042)

camel-aws2-sts - do not copy the temporary secret key and session token into message headers

[CAMEL-25930](https://issues.apache.org/jira/browse/CAMEL-25930)

camel-file - GenericFilePollingConsumer should return the polled exchange directly from receive

[CAMEL-25917](https://issues.apache.org/jira/browse/CAMEL-25917)

camel-undertow - close WebSocket connections opened before the consumer starts

[CAMEL-25890](https://issues.apache.org/jira/browse/CAMEL-25890)

camel-ftp - FTPS: verify the host name of the server over TLS

[CAMEL-25889](https://issues.apache.org/jira/browse/CAMEL-25889)

camel-google-mail/drive/calendar/sheets - create the API client per endpoint credentials instead of one per component

[CAMEL-25886](https://issues.apache.org/jira/browse/CAMEL-25886)

camel-ftp/mina-sftp - resolve listed symbolic links for jailStartingDirectory

[CAMEL-25754](https://issues.apache.org/jira/browse/CAMEL-25754)

camel-test-infra-artemis - no disk usage limit, so a broker on a nearly full Docker disk does not block producers

[CAMEL-25462](https://issues.apache.org/jira/browse/CAMEL-25462)

camel-platform-http-main - management settings ignored on a shared server port

[CAMEL-25460](https://issues.apache.org/jira/browse/CAMEL-25460)

camel-thrift - add a muteException consumer option

[CAMEL-25163](https://issues.apache.org/jira/browse/CAMEL-25163)

camel-google-storage - apply the download directory containment check on the expression branch

[CAMEL-25104](https://issues.apache.org/jira/browse/CAMEL-25104)

camel-core - SSLContextParameters should use TLSv1.2 as minimum protocol by default

[CAMEL-24937](https://issues.apache.org/jira/browse/CAMEL-24937)

camel-pqc: confine FileBasedKeyLifecycleManager key file resolution to the configured directory

[CAMEL-24416](https://issues.apache.org/jira/browse/CAMEL-24416)

camel-core - XmlConverter SAX parser factory is configured more permissively than the DOM factory in the same class

### Sub-task (2)

[CAMEL-27470](https://issues.apache.org/jira/browse/CAMEL-27470)

camel-timer - a VirtualMachineError in a timer route stops every timer route with the same timer name

[CAMEL-26478](https://issues.apache.org/jira/browse/CAMEL-26478)

camel-util - BoundedExecutorService: a task must not wait for a permit it holds itself

### Task (3)

[CAMEL-26347](https://issues.apache.org/jira/browse/CAMEL-26347)

camel-wordpress: logging cleanups

[CAMEL-26346](https://issues.apache.org/jira/browse/CAMEL-26346)

camel-jbang - Document CLI release selection (latest vs LTS), pinning and community plugin compatibility

[CAMEL-26108](https://issues.apache.org/jira/browse/CAMEL-26108)

camel-avro-rpc - the http consumer should configure the host of the endpoint

### Test (1)

[CAMEL-24903](https://issues.apache.org/jira/browse/CAMEL-24903)

Fix flaky test ThrottlingExceptionRoutePolicyOpenViaConfigTest

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).