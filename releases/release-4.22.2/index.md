# Apache camel 4.22.2 Release

## New and Noteworthy

This release is the new Camel 4.22.2 LTS release.

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
      <version>4.22.2</version>
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
      <version>4.22.2</version>
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
| [apache-camel-4.22.2-src.zip](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.2/apache-camel-4.22.2-src.zip) (Sources) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-src.zip.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-src.zip.sha512) |
| [apache-camel-4.22.2-sbom.xml](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.xml) (SBOM, CycloneDX XML) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.xml.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.xml.sha512) |
| [apache-camel-4.22.2-sbom.json](https://www.apache.org/dyn/closer.lua/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.json) (SBOM, CycloneDX JSON) | [PGP Signature](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.json.asc), [SHA512 Checksum](https://downloads.apache.org/camel/apache-camel/4.22.2/apache-camel-4.22.2-sbom.json.sha512) |

## Git tag checkout

Release is tagged with `camel-4.22.2` in the Git, to fetch it use:

git clone https://git-wip-us.apache.org/repos/asf/camel.git
cd camel
git checkout camel-4.22.2

## Resolved issues

Here is a list of all the issues that have been resolved for this release

### Bug (49)

[CAMEL-25715](https://issues.apache.org/jira/browse/CAMEL-25715)

camel-jbang - camel cmd eval breaks an expression with a double quote or a slash

[CAMEL-25638](https://issues.apache.org/jira/browse/CAMEL-25638)

camel-graphql - bind accessToken and basic credentials to the configured httpUri authority

[CAMEL-25629](https://issues.apache.org/jira/browse/CAMEL-25629)

camel-jbang - java version enum should include 25

[CAMEL-25620](https://issues.apache.org/jira/browse/CAMEL-25620)

camel-console: ConcurrentModificationException in DefaultDevConsoleRegistry.doStart when camel-cli-connector is enabled

[CAMEL-25603](https://issues.apache.org/jira/browse/CAMEL-25603)

camel-pqc - key encapsulation operations share one KeyGenerator and KeyAgreement instance across concurrent exchanges without synchronization

[CAMEL-25601](https://issues.apache.org/jira/browse/CAMEL-25601)

camel-vertx-websocket - a client consumer started while the WebSocket is already open registers no handlers

[CAMEL-25582](https://issues.apache.org/jira/browse/CAMEL-25582)

camel-vertx-websocket - a consumeAsClient consumer starts overlapping reconnect attempts: after a slow handshake it holds up to 20 WebSockets and routes every message once per WebSocket; it also keeps reconnecting after its route is stopped

[CAMEL-25559](https://issues.apache.org/jira/browse/CAMEL-25559)

camel-core - with the pooled exchange factory, an exchange that a consumer gives back without routing it is put into the pool twice, and the next two messages share one exchange

[CAMEL-25558](https://issues.apache.org/jira/browse/CAMEL-25558)

camel-aws2-s3 - a listed object that cannot be got (deleted meanwhile, or a failed get) fails the poll and stays in the in-progress repository, so it is never consumed until a restart

[CAMEL-25534](https://issues.apache.org/jira/browse/CAMEL-25534)

camel-mail - subject option description still says the Subject header takes precedence, but useHeaderSubject defaults to false

[CAMEL-25533](https://issues.apache.org/jira/browse/CAMEL-25533)

camel-jbang - camel run ignores camel.server.port (and the other camel.server.\* settings) for the HTTP server started for platform-http unless camel.server.enabled=true

[CAMEL-25494](https://issues.apache.org/jira/browse/CAMEL-25494)

camel-yaml-io - YAML route dump writes routeConfiguration onException items without their onException key, which neither the schema nor the loader accept

[CAMEL-25490](https://issues.apache.org/jira/browse/CAMEL-25490)

camel-jbang - camel validate normalize writes a top-level onException into the steps of every route, which the YAML DSL schema rejects

[CAMEL-25486](https://issues.apache.org/jira/browse/CAMEL-25486)

camel-http - the OAuth2 token request with a resource indicator sends only the resource parameter

[CAMEL-25452](https://issues.apache.org/jira/browse/CAMEL-25452)

camel-jbang - camel export ignores --resource-dir, the directories never reach the exported project

[CAMEL-25437](https://issues.apache.org/jira/browse/CAMEL-25437)

camel-jbang - camel run --prop key=value with a space is silently ignored

[CAMEL-25427](https://issues.apache.org/jira/browse/CAMEL-25427)

camel-support - on-demand route reload fails with FileNotFoundException after a route file is removed from the source dir

[CAMEL-25418](https://issues.apache.org/jira/browse/CAMEL-25418)

camel-jbang - camel get vault does not list the Kubernetes config map names

[CAMEL-25376](https://issues.apache.org/jira/browse/CAMEL-25376)

camel-netty-http - match security constraint roles by exact role name

[CAMEL-25375](https://issues.apache.org/jira/browse/CAMEL-25375)

camel-undertow - Apply securityProvider, allowedRoles and handlers to WebSocket endpoints consistently with HTTP endpoints

[CAMEL-25227](https://issues.apache.org/jira/browse/CAMEL-25227)

camel-azure-eventhubs: partition header conflict and no default header filter

[CAMEL-25224](https://issues.apache.org/jira/browse/CAMEL-25224)

camel-xslt / camel-xslt-saxon: implicitly converted DOM sources select wrong XSLT context node

[CAMEL-25222](https://issues.apache.org/jira/browse/CAMEL-25222)

Route dump - YAML with source locations loses the list dash of a choice when, and throwException given an exception instance is dumped empty

[CAMEL-25164](https://issues.apache.org/jira/browse/CAMEL-25164)

camel-infinispan - the aggregation repositories recover a completed exchange without the message that completed the group

[CAMEL-25116](https://issues.apache.org/jira/browse/CAMEL-25116)

camel-main - /q/download?classpath=true does not list project resources

[CAMEL-25103](https://issues.apache.org/jira/browse/CAMEL-25103)

camel-vertx - Client authentication, cipher suites and protocols of SSLContextParameters are not applied

[CAMEL-25086](https://issues.apache.org/jira/browse/CAMEL-25086)

camel-platform-http-starter: fails to start outside a servlet web application (ServerProperties/WebMvcProperties)

[CAMEL-25085](https://issues.apache.org/jira/browse/CAMEL-25085)

Rest DSL: under json/xml binding a response without Content-Type ignores the verb's produces

[CAMEL-25023](https://issues.apache.org/jira/browse/CAMEL-25023)

camel-util - IOHelper.copy counts copied bytes in an int, so zipFile/tarFile maxDecompressedSize values of 2 GiB or more are not enforced

[CAMEL-25001](https://issues.apache.org/jira/browse/CAMEL-25001)

camel-core - Supervising route controller: an exhausted route stays unhealthy after it is started manually

[CAMEL-25000](https://issues.apache.org/jira/browse/CAMEL-25000)

camel-ai-tool / camel-ai-resource - tools and resources are missing when a route sends a request as soon as it starts

[CAMEL-24973](https://issues.apache.org/jira/browse/CAMEL-24973)

camel-util - URISupport.sanitizeUri does not follow the endpoint URI parser for RAW values, userinfo, dash-case option names and additional keywords

[CAMEL-24940](https://issues.apache.org/jira/browse/CAMEL-24940)

camel-jbang/cli - autodetection of Kubernetes property placeholder functions (configmap:, secret:) stopped working in 4.22.1

[CAMEL-24935](https://issues.apache.org/jira/browse/CAMEL-24935)

camel-pulsar - the producer replaces the message body with the MessageId

[CAMEL-24932](https://issues.apache.org/jira/browse/CAMEL-24932)

camel-pulsar - the polling loop dies on a NullPointerException when a receive fails

[CAMEL-24889](https://issues.apache.org/jira/browse/CAMEL-24889)

camel-debezium - the consumer is never told that the embedded engine has failed

[CAMEL-24887](https://issues.apache.org/jira/browse/CAMEL-24887)

ManagedRouteGroupMBean exchange stats changed

[CAMEL-24848](https://issues.apache.org/jira/browse/CAMEL-24848)

camel-mail - The useHeaderFrom and other useHeaderXXXXX options defaulted to false but the document said the default should be true

[CAMEL-24816](https://issues.apache.org/jira/browse/CAMEL-24816)

camel-elasticsearch/camel-opensearch: minor robustness fixes (scroll clear NPE, id header clobber, size/from header bleed)

[CAMEL-24814](https://issues.apache.org/jira/browse/CAMEL-24814)

camel-elasticsearch/camel-opensearch: BulkRequestAggregationStrategy returns the wrong exchange, breaking bulk aggregation

[CAMEL-24811](https://issues.apache.org/jira/browse/CAMEL-24811)

camel-servlet - async=true without executorRef completes the AsyncContext before a truly-asynchronous route finishes

[CAMEL-24799](https://issues.apache.org/jira/browse/CAMEL-24799)

camel-jbang: Installing Camel Kit by command name loses the requested plugin version

[CAMEL-24776](https://issues.apache.org/jira/browse/CAMEL-24776)

camel-jbang run does not auto-load camel-kubernetes for secret property functions

[CAMEL-24766](https://issues.apache.org/jira/browse/CAMEL-24766)

camel-huaweicloud-smn: empty-body guard checks the raw endpoint operation instead of the resolved one

[CAMEL-24691](https://issues.apache.org/jira/browse/CAMEL-24691)

camel-saxon - align XQueryBuilder with secure XML parsing defaults

[CAMEL-24594](https://issues.apache.org/jira/browse/CAMEL-24594)

RestBindingAdvice response marshalling failure is silently swallowed

[CAMEL-24590](https://issues.apache.org/jira/browse/CAMEL-24590)

ManagedRouteGroupMBean.getFailuresHandled() / getLastExchangeFailureHandledTimestamp() return 0/null even though a member route recorded a handled failure

[CAMEL-24440](https://issues.apache.org/jira/browse/CAMEL-24440)

camel-crypto - CryptoDataFormat validates the MAC after decrypting, reuses the cipher key for the HMAC, and has no per-message IV

[CAMEL-24371](https://issues.apache.org/jira/browse/CAMEL-24371)

camel-a2a - fix WebhookUrlValidator address classification and host matching

### Dependency upgrade (1)

[CAMEL-25468](https://issues.apache.org/jira/browse/CAMEL-25468)

Upgrade Bouncy Castle to 1.86 on Camel 4.22.x

### Improvement (28)

[CAMEL-25622](https://issues.apache.org/jira/browse/CAMEL-25622)

camel-smpp - Add hostname verification for SSL connections

[CAMEL-25605](https://issues.apache.org/jira/browse/CAMEL-25605)

camel-mina - Add hostname verification for TLS producer connections

[CAMEL-25604](https://issues.apache.org/jira/browse/CAMEL-25604)

camel-mllp - Add hostname verification for TLS producer connections

[CAMEL-25590](https://issues.apache.org/jira/browse/CAMEL-25590)

camel-lra-starter - expose the callbackSecret and allowedCoordinatorUrls options

[CAMEL-25585](https://issues.apache.org/jira/browse/CAMEL-25585)

camel-chunk - message body and header values are expanded as Chunk template code instead of printed literally

[CAMEL-25584](https://issues.apache.org/jira/browse/CAMEL-25584)

camel-lra - only join LRAs hosted by the configured LRA coordinator

[CAMEL-25578](https://issues.apache.org/jira/browse/CAMEL-25578)

camel-lra - verify participant callbacks with an optional shared secret

[CAMEL-25568](https://issues.apache.org/jira/browse/CAMEL-25568)

camel-oauth - make OAuthBearerTokenProcessor stateless and read credentials from HTTP request headers

[CAMEL-25564](https://issues.apache.org/jira/browse/CAMEL-25564)

camel-telegram - verify the Bot API secret token on webhook updates

[CAMEL-25528](https://issues.apache.org/jira/browse/CAMEL-25528)

camel-jbang - camel run ignores camel.jbang.dependencies in a properties file given on the command line, such as camel/application.properties

[CAMEL-25445](https://issues.apache.org/jira/browse/CAMEL-25445)

camel-jbang-plugin-tui - sanitize 8-bit C1 control characters in displayed integration text

[CAMEL-25412](https://issues.apache.org/jira/browse/CAMEL-25412)

camel-file - resolve symbolic links when enforcing jailStartingDirectory for the producer target and local consumer listing

[CAMEL-25340](https://issues.apache.org/jira/browse/CAMEL-25340)

camel-spring-ws: apply the HeaderFilterStrategy to outbound SOAP headers

[CAMEL-25225](https://issues.apache.org/jira/browse/CAMEL-25225)

camel-spring-ws: apply the HeaderFilterStrategy to producer response headers

[CAMEL-25205](https://issues.apache.org/jira/browse/CAMEL-25205)

camel-jackson3xml - Add support to enable/disable features from Jackson feature enums

[CAMEL-25197](https://issues.apache.org/jira/browse/CAMEL-25197)

camel-cli-connector - add a WebSocket transport so developer tools can drive running integrations

[CAMEL-25162](https://issues.apache.org/jira/browse/CAMEL-25162)

camel-oauth - confine the reconstructed post-login URL to the configured redirect URI origin

[CAMEL-25091](https://issues.apache.org/jira/browse/CAMEL-25091)

camel-kafka: expose by\_duration as valid autoOffsetReset value (Kafka 4.0+)

[CAMEL-25087](https://issues.apache.org/jira/browse/CAMEL-25087)

camel-coap - add a muteException consumer option

[CAMEL-25054](https://issues.apache.org/jira/browse/CAMEL-25054)

camel-jackson - Add support to enable/disable features in qualified manner

[CAMEL-24936](https://issues.apache.org/jira/browse/CAMEL-24936)

camel-netty: NettyConverter.toByteArray should copy only the readable bytes of the ByteBuf

[CAMEL-24902](https://issues.apache.org/jira/browse/CAMEL-24902)

camel-keycloak: honor token expiry (exp) when caching introspection results

[CAMEL-24901](https://issues.apache.org/jira/browse/CAMEL-24901)

camel-aws2-s3: restrict Simple expression evaluation of key/bucket to configured values

[CAMEL-24894](https://issues.apache.org/jira/browse/CAMEL-24894)

camel-docling: make output path handling consistent with input path and custom-argument handling

[CAMEL-24893](https://issues.apache.org/jira/browse/CAMEL-24893)

camel-docling: also constrain absolute paths in custom-argument path validation

[CAMEL-24872](https://issues.apache.org/jira/browse/CAMEL-24872)

camel-oauth: Align token caching with effective profile configuration

[CAMEL-24652](https://issues.apache.org/jira/browse/CAMEL-24652)

camel-servlet, camel-jetty, camel-platform-http-vertx - consolidate the fileNameExtWhitelist check and tighten the extension match

[CAMEL-24650](https://issues.apache.org/jira/browse/CAMEL-24650)

camel-http-common: lift the multipart fileNameExtWhitelist check into DefaultHttpBinding

### Task (2)

[CAMEL-24900](https://issues.apache.org/jira/browse/CAMEL-24900)

camel-jcr - apply header filtering when mapping JCR node properties to Exchange headers

[CAMEL-24895](https://issues.apache.org/jira/browse/CAMEL-24895)

camel-mustache, camel-chunk - align Exchange header constant names with Camel naming convention

### Test (1)

[CAMEL-24957](https://issues.apache.org/jira/browse/CAMEL-24957)

Fix flaky test MessageHistoryExceptionRouteTest

## Keys

You can verify your download by following these [procedures](http://www.apache.org/info/verification.md) and using these [KEYS](https://www.apache.org/dist/camel/KEYS).