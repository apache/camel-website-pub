# SPIFFE

**Since Camel 4.23**

**Only producer is supported**

The SPIFFE component integrates with the [SPIFFE](https://spiffe.io/) (Secure Production Identity Framework For Everyone) Workload API to provide cryptographic workload identity to Camel routes. It talks to a local SPIFFE Workload API endpoint — for example the one exposed by a [SPIRE](https://spiffe.io/docs/latest/spire-about/) agent — to fetch and validate SVIDs (SPIFFE Verifiable Identity Documents):

-   **X.509-SVID**: an X.509 certificate whose SPIFFE ID is encoded as a URI SAN, used for mutual TLS.
    
-   **JWT-SVID**: a JWT whose subject is the SPIFFE ID, used as a bearer token for workload-to-workload authentication.
    

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spiffe</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

spiffe:label\[?options\]

Where `label` is a logical name for the endpoint.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The SPIFFE component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **audience** (producer) | The comma-separated audience(s) to request for a JWT-SVID (fetchJwtSvid) or to validate against (validateJwtSvid). fetchJwtSvid requests all of them and can be overridden per-message with the CamelSpiffeAudience header; validateJwtSvid ignores that header and uses this configuration only, accepting the token if it matches any of the configured audiences, trying each in turn. |  | String |
| **configuration** (producer) | The component configuration. |  | SpiffeConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform on the SPIFFE Workload API.

Enum values:

-   fetchX509Svid
    
-   fetchJwtSvid
    
-   validateJwtSvid
    





 | fetchX509Svid | SpiffeOperation |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **workloadApiClient** (advanced) | **Autowired** An existing WorkloadApiClient to use. When set, the component does not create or close its own client and spiffeSocketPath is ignored. |  | WorkloadApiClient |
| **allowOperationHeader** (security) | Whether the CamelSpiffeOperation header may override the configured operation. Disabled by default: the operation decides whether this endpoint validates a token or mints one, so a message that can set it can turn a validator into an endpoint that hands out this workload’s own JWT-SVID. Enable it only on routes whose input is trusted. | false | boolean |
| **spiffeSocketPath** (security) | The address of the SPIFFE Workload API endpoint (for example \\{code unix:///tmp/agent.sock} or \\{code tcp://127.0.0.1:8082}). When not set, the SPIFFE\_ENDPOINT\_SOCKET environment variable is used. |  | String |
| **x509Response** (security) | 

What the fetchX509Svid operation returns in the message body. Defaults to chain: the X.509 certificate chain without the private key, so a route never handles key material unless it asks for it. Choose svid to get the whole X509Svid including the private key (needed for programmatic mTLS), or id to leave the body untouched. The SPIFFE ID and expiry are exposed through the CamelSpiffeSpiffeId and CamelSpiffeExpiry headers in every case.

Enum values:

-   svid
    
-   chain
    
-   id
    





 | chain | SpiffeX509Response |

## Endpoint Options

The SPIFFE endpoint is configured using URI syntax:

spiffe:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | Logical name of the endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **audience** (producer) | The comma-separated audience(s) to request for a JWT-SVID (fetchJwtSvid) or to validate against (validateJwtSvid). fetchJwtSvid requests all of them and can be overridden per-message with the CamelSpiffeAudience header; validateJwtSvid ignores that header and uses this configuration only, accepting the token if it matches any of the configured audiences, trying each in turn. |  | String |
| **operation** (producer) | 
The operation to perform on the SPIFFE Workload API.

Enum values:

-   fetchX509Svid
    
-   fetchJwtSvid
    
-   validateJwtSvid
    





 | fetchX509Svid | SpiffeOperation |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **workloadApiClient** (advanced) | **Autowired** An existing WorkloadApiClient to use. When set, the component does not create or close its own client and spiffeSocketPath is ignored. |  | WorkloadApiClient |
| **allowOperationHeader** (security) | Whether the CamelSpiffeOperation header may override the configured operation. Disabled by default: the operation decides whether this endpoint validates a token or mints one, so a message that can set it can turn a validator into an endpoint that hands out this workload’s own JWT-SVID. Enable it only on routes whose input is trusted. | false | boolean |
| **spiffeSocketPath** (security) | The address of the SPIFFE Workload API endpoint (for example \\{code unix:///tmp/agent.sock} or \\{code tcp://127.0.0.1:8082}). When not set, the SPIFFE\_ENDPOINT\_SOCKET environment variable is used. |  | String |
| **x509Response** (security) | 

What the fetchX509Svid operation returns in the message body. Defaults to chain: the X.509 certificate chain without the private key, so a route never handles key material unless it asks for it. Choose svid to get the whole X509Svid including the private key (needed for programmatic mTLS), or id to leave the body untouched. The SPIFFE ID and expiry are exposed through the CamelSpiffeSpiffeId and CamelSpiffeExpiry headers in every case.

Enum values:

-   svid
    
-   chain
    
-   id
    





 | chain | SpiffeX509Response |

## Message Headers

The SPIFFE component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpiffeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#OPERATION) | Overrides the operation to be used by the producer. Ignored unless the endpoint sets allowOperationHeader=true, because the operation decides whether the endpoint validates a token or mints one. |  | SpiffeOperation or String |
| **CamelSpiffeAudience** (producer) Constant: [`AUDIENCE`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#AUDIENCE) | The comma-separated audience(s) for the fetchJwtSvid operation. Ignored by validateJwtSvid, which always validates against the configured audience: there the audience is the check that binds the token to this workload, not a parameter. |  | String |
| **CamelSpiffeToken** (producer) Constant: [`TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#TOKEN) | The JWT-SVID token to validate, for the validateJwtSvid operation. |  | String |
| **CamelSpiffeSpiffeId** (producer) Constant: [`SPIFFE_ID`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#SPIFFE_ID) | The SPIFFE ID of the returned SVID. |  | String |
| **CamelSpiffeExpiry** (producer) Constant: [`EXPIRY`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#EXPIRY) | The expiry of the returned SVID: the token expiry for fetchJwtSvid, or the leaf certificate’s notAfter for fetchX509Svid. |  | Date |

## Workload API endpoint

The address of the SPIFFE Workload API is taken from the `spiffeSocketPath` option, or, when that is not set, from the standard `SPIFFE_ENDPOINT_SOCKET` environment variable — for example `unix:///tmp/spire-agent/public/api.sock`. For advanced scenarios an already-configured `io.spiffe.workloadapi.WorkloadApiClient` can be supplied through the `workloadApiClient` option; in that case the component neither creates nor closes the client.

## Operations

The component supports the following producer operations:

-   `fetchX509Svid` — fetches the default X.509-SVID from the Workload API. By default (`x509Response=chain`) the message body is set to the certificate chain only (a `List<java.security.cert.X509Certificate>`, without the private key), so a route never handles key material unless it asks for it. Set `x509Response=svid` to get the whole `io.spiffe.svid.x509svid.X509Svid` including the private key (needed for programmatic mTLS), or `x509Response=id` to leave the body untouched. In every case the `CamelSpiffeSpiffeId` and `CamelSpiffeExpiry` (the leaf certificate’s expiry) headers carry the identity.
    
-   `fetchJwtSvid` — fetches a JWT-SVID for the configured `audience` (or the `CamelSpiffeAudience` header). The message body is set to the JWT token string, with the `CamelSpiffeSpiffeId` and `CamelSpiffeExpiry` headers.
    
-   `validateJwtSvid` — validates a JWT-SVID against the `audience`. The token is taken from the first of: the `CamelSpiffeToken` header, an `Authorization: Bearer <token>` header (the scheme matched case-insensitively), or the message body. The `Authorization` header is tried **before** the body so a request payload on a `POST`/`PUT` is not mistaken for the token; this lets a `platform-http` route validate an incoming bearer token without a bean to strip the scheme. On success the message body is set to the validated `io.spiffe.svid.jwtsvid.JwtSvid`, so a route that needs the original request payload afterwards must keep a copy before validating (or validate a bodiless request). When several audiences are configured the token is accepted if it matches **any** of them — the Workload API validates one audience at a time, so each is tried in turn.
    

> **Note**
> The `fetchX509Svid` and `fetchJwtSvid` operations place sensitive key material on the message: the `X509Svid` carries the workload’s private key, and the JWT-SVID is a bearer token. Route authors are trusted with Exchange contents, but you should avoid logging or tracing the message body for these operations — for example via the `log`/`trace` components or the message-history / breadcrumb EIPs — to prevent accidental disclosure of the key or token. `fetchX509Svid` only puts the private key on the body when `x509Response=svid` is set explicitly; the default (`chain`) and `id` keep the key off the message entirely.

## Example

Fetch a JWT-SVID for an outbound call:

```java
from("direct:start")
    .to("spiffe:identity?operation=fetchJwtSvid&audience=spiffe://example.org/backend")
    .setHeader("Authorization", simple("Bearer ${body}"))
    .to("http://backend.example.org/api");
```

Validate an incoming bearer token on a `platform-http` route, without a bean to strip the scheme:

```yaml
- route:
    from:
      uri: "platform-http:/api"
      steps:
        # the Authorization: Bearer <token> header is picked up automatically; validation replaces the body with the
        # JwtSvid, so this fits a request whose payload is not needed afterwards
        - to:
            uri: "spiffe:auth?operation=validateJwtSvid&audience=spiffe://example.org/api"
        # the token is a credential; drop it before the exchange goes further
        - removeHeaders:
            pattern: "Authorization"
        - to:
            uri: "direct:handleRequest"
```

A missing token fails with `IllegalArgumentException`; a rejected one (invalid, expired, or a wrong audience) fails with `io.spiffe.exception.JwtSvidException`. Catch both — `onException(io.spiffe.exception.JwtSvidException.class, IllegalArgumentException.class)` — to answer `401`.

## Mutual TLS with SPIFFE (SSLContextParameters)

For X.509-based zero-trust mTLS, the component provides `org.apache.camel.component.spiffe.SpiffeSSLContextParameters`, an `SSLContextParameters` whose `SSLContext` is backed by the SPIFFE Workload API. The X.509-SVID and trust bundles are fetched live and rotated automatically, so any Camel component that accepts an `sslContextParameters` reference (camel-http, camel-netty-http, camel-jetty, camel-vertx-http, …​) can obtain SPIFFE mTLS.

Peer authentication must be constrained explicitly: set `acceptedSpiffeIds` to an allow-list of peer SPIFFE IDs, or `acceptAnySpiffeId=true` to accept any SVID that validates against the trust bundle. The two are mutually exclusive, and setting neither fails closed.

Because it extends `SSLContextParameters`, the inherited configuration is still honoured: set `serverParameters.clientAuthentication` (for a server that must require client certificates), `cipherSuites` and `secureSocketProtocols` as usual, and the base handshake protocol comes from `secureSocketProtocol` (default `TLSv1.3`). The underlying `X509Source` is created lazily (bounded by `initTimeout`, default 30s), closed on `CamelContext` shutdown, and the cached context is invalidated at the same time so a restarted context rebuilds a fresh source.

```java
SpiffeSSLContextParameters ssl = new SpiffeSSLContextParameters();
// ssl.setSpiffeSocketPath("unix:///tmp/spire-agent/public/api.sock"); // or SPIFFE_ENDPOINT_SOCKET
ssl.setAcceptedSpiffeIds("spiffe://example.org/backend");
getCamelContext().getRegistry().bind("spiffeSsl", ssl);

from("direct:start")
    .to("https://backend.example.org/api?sslContextParameters=#spiffeSsl");
```

## Authorizing a route on the peer SPIFFE ID (SpiffeSecurityPolicy)

`SpiffeSSLContextParameters` decides **which peers may connect**; `org.apache.camel.component.spiffe.SpiffeSecurityPolicy` decides **what a given peer may reach**. It is an `AuthorizationPolicy` - the SPIFFE sibling of `ShiroSecurityPolicy`, `KeycloakSecurityPolicy` and `OpaSecurityPolicy` - that wraps a route segment and authorizes it on the caller’s verified SPIFFE ID:

```java
// the server must REQUIRE a client certificate, or the policy has no verified peer to authorize
SpiffeSSLContextParameters serverSsl = new SpiffeSSLContextParameters();
serverSsl.setAcceptedSpiffeIds("spiffe://example.org/frontend");
SSLContextServerParameters serverParameters = new SSLContextServerParameters();
serverParameters.setClientAuthentication(ClientAuthentication.REQUIRE.name());
serverSsl.setServerParameters(serverParameters);
getCamelContext().getRegistry().bind("spiffeSsl", serverSsl);

SpiffeSecurityPolicy spiffePolicy = new SpiffeSecurityPolicy("spiffe://example.org/frontend");
getCamelContext().getRegistry().bind("spiffePolicy", spiffePolicy);

from("netty-http:https://0.0.0.0:8443?sslContextParameters=#spiffeSsl")
    .policy(spiffePolicy)
    .to("direct:handleOrder");
```

> **Important**
> A few things about the server side decide whether, and for which peers, this policy can work.
>
> -   **The server must request a client certificate.** `serverParameters.clientAuthentication` defaults to unset, which leaves the JSSE default: the server never asks. `SSLSession.getPeerCertificates()` then throws and the policy fails closed, so **every** request is denied. Set it to `REQUIRE`, as above.
>     
> -   **The server must use `SpiffeSSLContextParameters`**, not a plain truststore that happens to trust the SPIFFE CA. Such a truststore accepts any SVID that CA issued, which is a weaker check than the allow-list this policy appears to give you.
>     
> -   **The handshake allow-list gates every policy.** `SpiffeSSLContextParameters.acceptedSpiffeIds` decides who may connect at all, so a peer it rejects never reaches any route’s policy. When several routes with different `SpiffeSecurityPolicy` allow-lists share one server, this TLS-level list must contain every ID those policies accept (or use `acceptAnySpiffeId` and let each policy narrow it), otherwise the handshake turns a peer away before its route could have authorized it.
>     
>
> Only camel-netty and camel-netty-http put the `SSLSession` on the message today, as the `CamelNettySSLSession` header. Behind platform-http, jetty, undertow or servlet there is no session on the exchange, so the policy has no verified peer certificate to read and denies everything.

The peer SPIFFE ID is taken from the **verified** TLS peer certificate the consumer put on the exchange - the `CamelNettySSLSession` header for camel-netty-http - and never from a message header a sender could set (see the Security notes below). A peer that is not on the `acceptedSpiffeIds` allow-list, or that presents no verified SVID at all, is denied with a `CamelAuthorizationException`, so the route stops and the regular `onException` machinery applies.

Set exactly one of:

-   `acceptedSpiffeIds` - a comma-separated allow-list of the peer SPIFFE IDs this segment authorizes;
    
-   `acceptAnySpiffeId=true` - authorize any peer that presents a verified SVID, leaving the which-peer decision to a downstream policy. It still fails closed when no verified peer certificate is present.
    

Setting both is rejected and setting neither fails closed, mirroring `SpiffeSSLContextParameters`.

The policy answers "is the peer who they claim to be"; it is designed to **compose** with `camel-opa` ("may they do this") rather than duplicate it. On a successful authorization the verified SPIFFE ID is stored as the `CamelSpiffePeerId` exchange property, so an OPA policy downstream can forward it to a Rego rule through its `includeProperties` option:

```java
from("netty-http:https://0.0.0.0:8443?sslContextParameters=#spiffeSsl")
    .policy(spiffePolicy)   // authenticates the peer, sets CamelSpiffePeerId
    .policy(opaPolicy)      // opaPolicy.setIncludeProperties("CamelSpiffePeerId")
    .to("direct:handleOrder");
```

For a TLS consumer that exposes the `SSLSession` under a different header name, set `sslSessionHeader` accordingly. The identity is always read from the verified `SSLSession`, never from a certificate object placed on a message header - nothing would prove the TLS layer had verified such a certificate.

## Security notes

-   **The operation comes from the endpoint.** `CamelSpiffeOperation` is ignored unless the endpoint sets `allowOperationHeader=true`. The operation decides whether this endpoint **validates** a token or **mints** one, so a message able to set it could turn a validator into an endpoint that hands out this workload’s own JWT-SVID.
    
-   **A validation always uses the configured audience.** `CamelSpiffeAudience` is honoured by `fetchJwtSvid`, where the audience is a genuine per-message parameter ("mint me a token for X"), and ignored by `validateJwtSvid`, where the audience is the check that binds the token to this workload. Letting a message choose it would allow a JWT-SVID minted for a different service to validate successfully.
    
-   **Strip the component’s headers on untrusted ingress.** As with any Camel component, a consumer that does not apply a `HeaderFilterStrategy` blocking `Camel*` lets a sender populate the header map. Call `removeHeaders("CamelSpiffe*")` before the `spiffe:` endpoint when the message comes from an untrusted producer.
    
-   **Key material reaches the message.** `fetchX509Svid` places an `X509Svid` - which carries the private key - on the body, and `fetchJwtSvid` places the bearer token. Do not log or trace the body for those operations.
    
-   **Constrain the peer.** `SpiffeSSLContextParameters` requires either an `acceptedSpiffeIds` allow-list or `acceptAnySpiffeId=true`; it fails closed when neither is given. Prefer the allow-list - `acceptAnySpiffeId` accepts any SVID that chains to the trust bundle, which authenticates the trust domain but not the peer.
    
-   **The authorization decision is made on the certificate, not a header.** `SpiffeSecurityPolicy` reads the peer SPIFFE ID from the verified TLS peer certificate (the `CamelNettySSLSession` header for camel-netty-http), so a sender cannot assert an identity by setting a header - and it requires mutual TLS, failing closed when the peer presented no verified certificate. The verified id it publishes is the `CamelSpiffePeerId` exchange **property**, never a header, so it likewise cannot be injected by an inbound message.