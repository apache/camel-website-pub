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
| **audience** (producer) | The comma-separated audience(s) to request for a JWT-SVID (fetchJwtSvid) or to validate against (validateJwtSvid). Can be overridden per-message with the CamelSpiffeAudience header. Note that validateJwtSvid validates against a single audience, so when several comma-separated audiences are given only the first one is used for validation; fetchJwtSvid requests all of them. |  | String |
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
| **spiffeSocketPath** (security) | The address of the SPIFFE Workload API endpoint (for example \\{code unix:///tmp/agent.sock} or \\{code tcp://127.0.0.1:8082}). When not set, the SPIFFE\_ENDPOINT\_SOCKET environment variable is used. |  | String |

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
| **audience** (producer) | The comma-separated audience(s) to request for a JWT-SVID (fetchJwtSvid) or to validate against (validateJwtSvid). Can be overridden per-message with the CamelSpiffeAudience header. Note that validateJwtSvid validates against a single audience, so when several comma-separated audiences are given only the first one is used for validation; fetchJwtSvid requests all of them. |  | String |
| **operation** (producer) | 
The operation to perform on the SPIFFE Workload API.

Enum values:

-   fetchX509Svid
    
-   fetchJwtSvid
    
-   validateJwtSvid
    





 | fetchX509Svid | SpiffeOperation |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **workloadApiClient** (advanced) | **Autowired** An existing WorkloadApiClient to use. When set, the component does not create or close its own client and spiffeSocketPath is ignored. |  | WorkloadApiClient |
| **spiffeSocketPath** (security) | The address of the SPIFFE Workload API endpoint (for example \\{code unix:///tmp/agent.sock} or \\{code tcp://127.0.0.1:8082}). When not set, the SPIFFE\_ENDPOINT\_SOCKET environment variable is used. |  | String |

## Message Headers

The SPIFFE component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpiffeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#OPERATION) | Overrides the operation to be used by the producer. |  | SpiffeOperation or String |
| **CamelSpiffeAudience** (producer) Constant: [`AUDIENCE`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#AUDIENCE) | The comma-separated audience(s) for the fetchJwtSvid and validateJwtSvid operations. |  | String |
| **CamelSpiffeToken** (producer) Constant: [`TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#TOKEN) | The JWT-SVID token to validate, for the validateJwtSvid operation. |  | String |
| **CamelSpiffeSpiffeId** (producer) Constant: [`SPIFFE_ID`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#SPIFFE_ID) | The SPIFFE ID of the returned SVID. |  | String |
| **CamelSpiffeExpiry** (producer) Constant: [`EXPIRY`](https://javadoc.io/doc/org.apache.camel/camel-spiffe/latest/org/apache/camel/component/spiffe/SpiffeConstants.html#EXPIRY) | The expiry of the returned JWT-SVID. |  | Date |

## Workload API endpoint

The address of the SPIFFE Workload API is taken from the `spiffeSocketPath` option, or, when that is not set, from the standard `SPIFFE_ENDPOINT_SOCKET` environment variable — for example `unix:///tmp/spire-agent/public/api.sock`. For advanced scenarios an already-configured `io.spiffe.workloadapi.WorkloadApiClient` can be supplied through the `workloadApiClient` option; in that case the component neither creates nor closes the client.

## Operations

The component supports the following producer operations:

-   `fetchX509Svid` — fetches the default X.509-SVID from the Workload API. The message body is set to the `io.spiffe.svid.x509svid.X509Svid` (certificate chain, private key and SPIFFE ID) and the `CamelSpiffeSpiffeId` header to its SPIFFE ID.
    
-   `fetchJwtSvid` — fetches a JWT-SVID for the configured `audience` (or the `CamelSpiffeAudience` header). The message body is set to the JWT token string, with the `CamelSpiffeSpiffeId` and `CamelSpiffeExpiry` headers.
    
-   `validateJwtSvid` — validates the JWT-SVID passed in the `CamelSpiffeToken` header (or the body) against the `audience`. The message body is set to the validated `io.spiffe.svid.jwtsvid.JwtSvid`.
    

> **Note**
> The `fetchX509Svid` and `fetchJwtSvid` operations place sensitive key material on the message: the `X509Svid` carries the workload’s private key, and the JWT-SVID is a bearer token. Route authors are trusted with Exchange contents, but you should avoid logging or tracing the message body for these operations — for example via the `log`/`trace` components or the message-history / breadcrumb EIPs — to prevent accidental disclosure of the key or token.

## Example

Fetch a JWT-SVID for an outbound call:

```java
from("direct:start")
    .to("spiffe:identity?operation=fetchJwtSvid&audience=spiffe://example.org/backend")
    .setHeader("Authorization", simple("Bearer ${body}"))
    .to("http://backend.example.org/api");
```

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