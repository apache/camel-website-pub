# OPA

**Since Camel 4.23**

**Only producer is supported**

The OPA component turns a Camel route into a Policy Enforcement Point (PEP) in front of [Open Policy Agent](https://www.openpolicyagent.org/), the CNCF policy engine whose policies are written in Rego. Camel builds an `input` document out of the Exchange, OPA evaluates the policy against it, and the resulting decision is recorded on the Exchange.

This keeps authorization **out** of the route: the rules live in Rego and can be updated, versioned and tested independently of the integration, instead of being hand-coded in a processor.

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-opa</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

opa:policyPath\[?options\]

Where `policyPath` is the path of the Rego rule head to evaluate, relative to the OPA data document. For a rule named `allow` in a policy declaring `package authz.orders`, the path is `authz/orders/allow`, which OPA serves at `/v1/data/authz/orders/allow`.

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

The OPA component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowKey** (producer) | The key to read the allow/deny verdict from when the policy returns an object rather than a plain boolean. For a policy returning \\{allow: true, reasons: } the default value of allow is what you want. A dotted path reaches a verdict nested inside the document: \\{code allowKey=result.allow} reads \\{result: \\{allow: true}}. A key with no dot is looked up directly at the top level. | allow | String |
| **configuration** (producer) | The component configuration. |  | OpaConfiguration |
| **entrypoint** (producer) | The compiled entrypoint to evaluate in wasm mode. This is not the same thing as the policy path: an entrypoint is fixed when the bundle is built, with \\{code opa build -e}. Defaults to the endpoint’s policy path, which is the name \\{code opa build} gives it. |  | String |
| **evaluationMode** (producer) | 
How the policy is evaluated. rest (the default) calls a running OPA server over its Data API. wasm evaluates a WebAssembly bundle in-process, with no server involved - so there is no network hop and no unreachable decision point, at the cost of the policy being a build-time artefact rather than something a server distributes and updates. serverUrl, bearerToken and failOpen do not apply in wasm mode.

Enum values:

-   rest
    
-   wasm
    





 | rest | String |
| **includeBody** (producer) | Whether to send the message body to OPA as part of the input document. Disabled by default: bodies can be large or streaming, and most authorization decisions only need headers. When enabled on a streaming body, enable stream caching so that the body is still readable by the rest of the route. | false | boolean |
| **includeHeaders** (producer) | Comma-separated list of message header names to send to OPA in the input document. The default of \\{code } sends every header except those that carry a caller credential verbatim - Authorization, \\{code Proxy-Authorization}, Cookie and \\{code Set-Cookie} - which are withheld because OPA’s decision logging ships the whole input document, often off the box. A policy that genuinely needs one can still have it by naming the header here. Narrow the list when the policy only needs a few headers. | \* | String |
| **includeProperties** (producer) | Comma-separated list of exchange property names to send to OPA in the input document, or \\{code } for all of them. Empty by default, so no properties are sent unless asked for. This is where the authentication components put the identity they verified: \\{code camel-keycloak} stores the access token and its subject as exchange properties and prefers them over the equivalent headers, precisely because headers can be set by the caller. List those property names here to let a policy authorize the identity an earlier step established, instead of copying it into a header first. Only custom properties are sent; Camel’s own internal exchange properties are never included. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **policyBundle** (producer) | The WebAssembly policy to evaluate in wasm mode, as produced by \\{code opa build -t wasm}. Accepts a \\{code file:}, \\{code classpath:} or \\{code http:} location holding either the bundle.tar.gz that \\{code opa build} emits or a bare .wasm module. Required when \\{code evaluationMode=wasm}. Prefer the bundle: it also carries the data document the policy reads as \\{code data.}, which a bare module does not. |  | String |
| **serverUrl** (producer) | The base URL of the OPA server, without the \\{code /v1/data} suffix. The default assumes OPA running as a sidecar on the standard port. | [http://localhost:8181](http://localhost:8181) | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **borrowTimeout** (advanced) | How long an exchange waits for a free WebAssembly policy instance in wasm mode before the evaluation fails. An exchange that cannot get an instance is not denied by a policy, so it is reported as an evaluation failure and handled like any other: failing closed, or proceeding if failOpen is set. Raise it, or poolSize, for a route whose concurrency exceeds the pool. | 30000 | long |
| **connectionTimeout** (advanced) | How long to wait for the connection to the OPA server to be established, in rest mode. The SDK’s own transport applies no timeout at all, so a server that never answers would otherwise park the calling thread indefinitely rather than letting the component fail closed. | 10000 | long |
| **opaClient** (advanced) | **Autowired** An existing OPAClient to use. When set, serverUrl and bearerToken are ignored. |  | OPAClient |
| **poolSize** (advanced) | How many WebAssembly policy instances to pool in wasm mode. An instance carries mutable state and is not thread-safe, so each exchange borrows one; this bounds how many exchanges evaluate at once. | 8 | int |
| **requestTimeout** (advanced) | How long to wait for the decision once connected, in rest mode. A request that times out is an evaluation failure rather than a deny, so it fails closed - or proceeds when failOpen is set - like any other failure to reach a verdict. | 30000 | long |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **bearerToken** (security) | Bearer token sent to the OPA server in the Authorization header, for an OPA instance that has its API authentication enabled. |  | String |
| **failOpen** (security) | Whether to allow the exchange to proceed when the policy cannot be evaluated at all, for example because the OPA server is unreachable. Disabled by default so that an unreachable policy decision point denies rather than grants access. Do not enable this in production. | false | boolean |
| **sslContextParameters** (security) | TLS configuration for the connection to the OPA server in rest mode. Needed to trust a server whose certificate comes from a private CA, and to present a client certificate to a server that requires mutual TLS - a SPIFFE X.509-SVID, for instance, so the workload authenticates to the policy decision point as itself. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The OPA endpoint is configured using URI syntax:

opa:policyPath

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **policyPath** (producer) | **Required** Path of the Rego rule head to evaluate, relative to the OPA data document. For a rule named allow in a policy declaring package authz.orders, this is authz/orders/allow. The path is taken from the endpoint only: it is deliberately not overridable by a message header, so that an inbound message cannot select which policy judges it. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowKey** (producer) | The key to read the allow/deny verdict from when the policy returns an object rather than a plain boolean. For a policy returning \\{allow: true, reasons: } the default value of allow is what you want. A dotted path reaches a verdict nested inside the document: \\{code allowKey=result.allow} reads \\{result: \\{allow: true}}. A key with no dot is looked up directly at the top level. | allow | String |
| **entrypoint** (producer) | The compiled entrypoint to evaluate in wasm mode. This is not the same thing as the policy path: an entrypoint is fixed when the bundle is built, with \\{code opa build -e}. Defaults to the endpoint’s policy path, which is the name \\{code opa build} gives it. |  | String |
| **evaluationMode** (producer) | 
How the policy is evaluated. rest (the default) calls a running OPA server over its Data API. wasm evaluates a WebAssembly bundle in-process, with no server involved - so there is no network hop and no unreachable decision point, at the cost of the policy being a build-time artefact rather than something a server distributes and updates. serverUrl, bearerToken and failOpen do not apply in wasm mode.

Enum values:

-   rest
    
-   wasm
    





 | rest | String |
| **includeBody** (producer) | Whether to send the message body to OPA as part of the input document. Disabled by default: bodies can be large or streaming, and most authorization decisions only need headers. When enabled on a streaming body, enable stream caching so that the body is still readable by the rest of the route. | false | boolean |
| **includeHeaders** (producer) | Comma-separated list of message header names to send to OPA in the input document. The default of \\{code } sends every header except those that carry a caller credential verbatim - Authorization, \\{code Proxy-Authorization}, Cookie and \\{code Set-Cookie} - which are withheld because OPA’s decision logging ships the whole input document, often off the box. A policy that genuinely needs one can still have it by naming the header here. Narrow the list when the policy only needs a few headers. | \* | String |
| **includeProperties** (producer) | Comma-separated list of exchange property names to send to OPA in the input document, or \\{code } for all of them. Empty by default, so no properties are sent unless asked for. This is where the authentication components put the identity they verified: \\{code camel-keycloak} stores the access token and its subject as exchange properties and prefers them over the equivalent headers, precisely because headers can be set by the caller. List those property names here to let a policy authorize the identity an earlier step established, instead of copying it into a header first. Only custom properties are sent; Camel’s own internal exchange properties are never included. |  | String |
| **policyBundle** (producer) | The WebAssembly policy to evaluate in wasm mode, as produced by \\{code opa build -t wasm}. Accepts a \\{code file:}, \\{code classpath:} or \\{code http:} location holding either the bundle.tar.gz that \\{code opa build} emits or a bare .wasm module. Required when \\{code evaluationMode=wasm}. Prefer the bundle: it also carries the data document the policy reads as \\{code data.}, which a bare module does not. |  | String |
| **serverUrl** (producer) | The base URL of the OPA server, without the \\{code /v1/data} suffix. The default assumes OPA running as a sidecar on the standard port. | [http://localhost:8181](http://localhost:8181) | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **borrowTimeout** (advanced) | How long an exchange waits for a free WebAssembly policy instance in wasm mode before the evaluation fails. An exchange that cannot get an instance is not denied by a policy, so it is reported as an evaluation failure and handled like any other: failing closed, or proceeding if failOpen is set. Raise it, or poolSize, for a route whose concurrency exceeds the pool. | 30000 | long |
| **connectionTimeout** (advanced) | How long to wait for the connection to the OPA server to be established, in rest mode. The SDK’s own transport applies no timeout at all, so a server that never answers would otherwise park the calling thread indefinitely rather than letting the component fail closed. | 10000 | long |
| **opaClient** (advanced) | **Autowired** An existing OPAClient to use. When set, serverUrl and bearerToken are ignored. |  | OPAClient |
| **poolSize** (advanced) | How many WebAssembly policy instances to pool in wasm mode. An instance carries mutable state and is not thread-safe, so each exchange borrows one; this bounds how many exchanges evaluate at once. | 8 | int |
| **requestTimeout** (advanced) | How long to wait for the decision once connected, in rest mode. A request that times out is an evaluation failure rather than a deny, so it fails closed - or proceeds when failOpen is set - like any other failure to reach a verdict. | 30000 | long |
| **bearerToken** (security) | Bearer token sent to the OPA server in the Authorization header, for an OPA instance that has its API authentication enabled. |  | String |
| **failOpen** (security) | Whether to allow the exchange to proceed when the policy cannot be evaluated at all, for example because the OPA server is unreachable. Disabled by default so that an unreachable policy decision point denies rather than grants access. Do not enable this in production. | false | boolean |
| **sslContextParameters** (security) | TLS configuration for the connection to the OPA server in rest mode. Needed to trust a server whose certificate comes from a private CA, and to present a client certificate to a server that requires mutual TLS - a SPIFFE X.509-SVID, for instance, so the workload authenticates to the policy decision point as itself. |  | SSLContextParameters |

## Message Headers

The OPA component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpaDecisionAllow** (producer) Constant: [`DECISION_ALLOW`](https://javadoc.io/doc/org.apache.camel/camel-opa/latest/org/apache/camel/component/opa/OpaConstants.html#DECISION_ALLOW) | The allow/deny verdict of the policy evaluation. Always overwritten by the component, so a value set by an inbound message never survives into the route. |  | Boolean |
| **CamelOpaDecision** (producer) Constant: [`DECISION`](https://javadoc.io/doc/org.apache.camel/camel-opa/latest/org/apache/camel/component/opa/OpaConstants.html#DECISION) | The raw decision document returned by OPA. Useful for policies that return more than a boolean, such as obligations, row filters or deny reasons. |  | Object |
| **CamelOpaPolicyPath** (producer) Constant: [`POLICY_PATH`](https://javadoc.io/doc/org.apache.camel/camel-opa/latest/org/apache/camel/component/opa/OpaConstants.html#POLICY_PATH) | The policy path that was evaluated. Set by the component for observability; it is not read as an input and cannot be used to select a different policy. |  | String |

## Usage

The component is used in one of two ways, depending on whether a denied message should be filtered out or should stop the route.

### As a producer, deciding with a filter

The producer evaluates the policy and records the verdict in the `CamelOpaDecisionAllow` header, leaving the message body untouched. The route then decides what to do with it:

```java
from("platform-http:/orders")
    .to("opa:authz/orders/allow")
    .filter(header(OpaConstants.DECISION_ALLOW).isEqualTo(true))
        .to("direct:handleOrder");
```

This is the right shape when a denied message is simply not routed further, or when the route wants to inspect the full decision document — a policy that returns obligations, row filters or deny reasons rather than a plain boolean puts them in the `CamelOpaDecision` header.

### As a security policy, enforcing on a route segment

`OpaSecurityPolicy` is an `AuthorizationPolicy`, so it can wrap part of a route. A deny throws a `CamelAuthorizationException` and the wrapped part never runs, which makes it composable with `onException`:

```java
OpaSecurityPolicy opaPolicy = new OpaSecurityPolicy("http://localhost:8181", "authz/orders/allow");

from("platform-http:/orders")
    .policy(opaPolicy)
        .to("direct:handleOrder");
```

The decision headers are set here too, so an `onException(CamelAuthorizationException.class)` handler can read `CamelOpaDecision` to build a meaningful error response.

## The input document

Camel sends OPA an `input` document shaped like this:

```json
{
  "headers": { "user": "alice", "CamelHttpMethod": "POST" },
  "properties": { "CamelKeycloakTokenSubject": "alice" },
  "body": "...",
  "exchangeId": "1767DC33923810E-0000000000000000",
  "routeId": "orders"
}
```

so a policy reads it as:

```rego
package authz.orders

default allow := false

allow if {
    input.headers.CamelHttpMethod == "GET"
}
```

The component’s integration test runs a real OPA server against [`authz.rego`](https://github.com/apache/camel/blob/main/components/camel-opa/src/test/resources/authz.rego), which is a worked example of both a plain boolean rule and a decision object with deny reasons; `OpaIT` alongside it shows the matching routes end to end.

`headers` carries every message header by default, with one exception: the headers that carry a caller credential verbatim — `Authorization`, `Proxy-Authorization`, `Cookie` and `Set-Cookie` — are **withheld** from the wildcard. OPA’s decision logging ships the whole `input` document, frequently to a remote collector, so the wildcard should not quietly export credentials off the box. A policy that genuinely needs one can still have it by naming the header: `includeHeaders=Authorization,user` sends it. Matching is case-insensitive, so `authorization` is withheld too. Set `includeHeaders` to a comma-separated list of names when the policy only needs a few of them.

Prefer `includeProperties` for identity: a token that an earlier step has already **verified** belongs there, as [Authorizing an identity](#authorizing-an-identity) describes, rather than handing the raw credential to the policy to re-check.

`body` is **not** sent unless `includeBody` is enabled: bodies can be large or streaming, and most authorization decisions do not need them. When you do enable it on a streaming body, enable stream caching so the body is still readable by the rest of the route.

`properties` is empty unless you ask for it — see [Authorizing an identity](#authorizing-an-identity) below.

Header and body values that are not JSON-native are converted to their string form. That conversion is shallow: a `Map` or `List` value is passed through as-is, so anything non-JSON-native nested inside it is left for the OPA SDK’s serializer to render. A policy that reads nested structures should not assume the same string conversion applies at depth.

The component’s own `CamelOpa*` decision headers are never sent back to OPA, so a policy cannot be shown a verdict that an inbound message claimed for itself.

## Reading the verdict

`CamelOpaDecision` holds the decision document exactly as OPA returned it. `CamelOpaDecisionAllow` holds the boolean verdict read out of it:

-   a decision that **is** a boolean is the verdict;
    
-   a decision that is an object is searched for the `allowKey` entry (`allow` by default), which must itself be a boolean. `allowKey` accepts a dotted path, so `allowKey=result.allow` reads a verdict nested inside the document as `{"result": {"allow": true}}`;
    
-   anything else cannot be read as a verdict and counts as a deny, with the raw document still available for the route to inspect. That case is logged at WARN rather than DEBUG: a document that arrived but could not be read is a configuration problem, and from `CamelOpaDecisionAllow` alone it is indistinguishable from a genuine denial.
    

Both headers are written on every evaluation, so a verdict set by an inbound message never survives into the route.

## Authorizing an identity

The component decides; it does not authenticate. Establish who the caller is first, then let the policy authorize the identity that step produced.

The catch is that Camel’s authentication components deliberately keep the identity they verified in **exchange properties** rather than in headers — `camel-keycloak` stores the access token and its subject that way and its `preferPropertyOverHeader` option defaults to `true`, precisely because a header can be set by the caller. So the identity you want to authorize is usually not in the header map.

Name those properties in `includeProperties` and they arrive in the input document under `properties`:

```java
from("platform-http:/orders")
    .policy(keycloakPolicy)                                  // authenticates, stores the subject as a property
    .to("opa:authz/orders/allow?includeProperties=CamelKeycloakTokenSubject")
    .filter(header(OpaConstants.DECISION_ALLOW).isEqualTo(true))
        .to("direct:handleOrder");
```

and the policy reads them the same way it reads headers:

```rego
allow if {
    input.properties.CamelKeycloakTokenSubject == "alice"
}
```

`includeProperties` takes a comma-separated list, or `*` for all of them, and matches names case-insensitively. Unlike `includeHeaders` it is **empty by default**: exchange properties are mostly used to carry state between processors, so sending them all would be noise the policy has to wade through. Only custom properties are sent — Camel’s own internal exchange properties are never included.

Prefer this over copying the identity into a header before the `opa:` endpoint. A header is exactly the channel the authentication step treated as untrusted, so moving a verified identity into one to get it past this component undoes the check that produced it.

`OpaSecurityPolicy` takes the same option through `setIncludeProperties`.

## Evaluation modes

By default the component calls a running OPA server over its Data API (`evaluationMode=rest`). It can instead evaluate a WebAssembly bundle in-process:

```java
from("platform-http:/orders")
    .to("opa:authz/orders/allow?evaluationMode=wasm&policyBundle=classpath:bundle.tar.gz")
```

Build the bundle with OPA’s compiler — note that `-e` names an **entrypoint**, which is fixed at build time and is not the same thing as a data path:

```sh
opa build -t wasm -e authz/orders/allow policy.rego
```

`policyBundle` accepts a `file:`, `classpath:` or `http:` location holding either the `bundle.tar.gz` that `opa build` emits or a bare `.wasm`. `entrypoint` defaults to the endpoint’s policy path, which is the name `opa build` gives it. `evaluationMode` accepts only `rest` and `wasm`; anything else is rejected when the endpoint is created, rather than quietly falling back to a server call that ignores `policyBundle`.

Prefer the `bundle.tar.gz`. A policy that reads `data.` **decides from the \*data document**, and `opa build` packs that beside the module as `data.json` — a bare `.wasm` carries the rules but not the data, so such a policy evaluates against an empty data document and typically denies everything. Given the bundle, the component applies its data to every evaluation, so the decision matches what a server loading the same bundle would return:

```sh
# roles.rego reads data.admins, which lives in data.json next to it
opa build -t wasm -e authz/orders/allow roles.rego data.json
```

Data that is **not** part of the bundle — what a server would receive through its Data API at runtime — has no equivalent in `wasm` mode. A policy depending on it needs `evaluationMode=rest`.

Prefer `classpath:` or `file:` for a bundle shipped with the application, which is what a build-time artefact usually is. The bundle is fetched when the endpoint starts, and Camel resolves an `http:` resource with no connect or read timeout (CAMEL-24756), so a policy server that accepts the connection and then does not answer stalls `CamelContext` startup rather than failing the one route.

Which to choose:

  
|  | `rest` | `wasm` |
| --- | --- | --- |
| Policy source | a server, centrally managed | a bundle built with your application |
| Updates | bundle polling, live | rebuild and redeploy |
| Decision logs | yes | none |
| Latency | a network round-trip per exchange | in-process |
| Unreachable decision point | a real failure mode | cannot happen |

`serverUrl` and `bearerToken` have no meaning in `wasm` mode — there is no server to address or authenticate to, and the endpoint warns at startup if either was set — and no health check is registered, because there is nothing to probe. An absent health check is not a healthy one. `failOpen` still applies: a `wasm` evaluation can fail (a busy pool, a bad bundle), and `failOpen` governs whether that failure denies the exchange or lets it through, exactly as in `rest` mode.

The decision contract is identical in both modes: the same headers, the same `allowKey` handling, and an undefined decision fails closed the same way. A route does not need to know which engine evaluated it.

Evaluation instances carry mutable state and are not thread-safe, so `wasm` mode pools them; `poolSize` (default 8) bounds how many exchanges evaluate at once. An exchange that arrives when all of them are busy waits for one, up to `borrowTimeout` (default 30s), and then fails rather than waiting indefinitely — an authorization decision that never arrives is not better than one that is denied, and it is much harder to diagnose. That failure is an evaluation failure, not a deny, so it fails closed or proceeds under `failOpen` like any other.

Size `poolSize` for the concurrency the route actually sees. A policy that takes a long time to evaluate holds its instance for that whole time, so the two options trade against each other: raise `poolSize` when many exchanges evaluate at once, and `borrowTimeout` when a single evaluation is legitimately slow. A policy that can run long enough to matter is usually better served by `evaluationMode=rest`, where the decision point is a separate process that a timeout can abandon.

## Connecting to the server

In `rest` mode the component talks to OPA over HTTP, and both waits are bounded:

-   `connectionTimeout` (default 10s) — establishing the connection.
    
-   `requestTimeout` (default 30s) — waiting for the decision once connected.
    

Neither is optional in practice. A refused connection fails immediately, but a server that **accepts** and then stops answering — wedged, mid-restart, or behind a load balancer holding the socket — would otherwise park the routing thread indefinitely. For a component that fails closed that is worse than a denial: it never reaches the point of deciding. A timeout is treated as a failure to reach a verdict, so it denies, or proceeds if `failOpen` is set, like any other such failure.

TLS is configured with `sslContextParameters`, the usual [JSSE utility](../../manual/camel-configuration-utilities.md):

```java
from("platform-http:/orders")
    .to("opa:authz/orders/allow?serverUrl=https://opa:8181&sslContextParameters=#opaTls")
```

Set `useGlobalSslContextParameters=true` on the component to pick up the context-wide configuration instead.

That is what lets a workload present a client certificate to an OPA server requiring mutual TLS — a SPIFFE X.509-SVID, for example, so the application authenticates to the policy decision point as itself rather than relying on network position:

```java
SpiffeSSLContextParameters spiffe = new SpiffeSSLContextParameters();
spiffe.setCamelContext(context);
context.getRegistry().bind("opaTls", spiffe);
```

None of this applies in `wasm` mode, where there is no server to reach.

## Failure handling

The component fails closed. If the policy cannot be evaluated at all — the OPA server is unreachable, times out, or answers with an error — the producer throws an `OpaPolicyEvaluationException` and `OpaSecurityPolicy` throws a `CamelAuthorizationException`; in neither case does the message proceed as allowed. This is deliberately different from a deny, which is a decision rather than a failure, so a route can tell "denied" from "no policy decision point available".

Setting `failOpen=true` reverses this and lets the exchange proceed when the policy cannot be evaluated. It exists for development and for non-critical policies, and should not be enabled in production.

Note that OPA reports an **undefined** decision — no rule matched and the policy declares no default — as an error rather than as a deny, so it fails closed as well. Give every decision rule a default, as in the example above, so the policy always returns a verdict.

## Health check

Because the component fails closed, an OPA server that cannot be reached fails **every** exchange through the route. The producer registers a readiness check that probes the server’s `/health` endpoint, so an unavailable policy decision point shows up in the health registry rather than only in the error logs once traffic starts failing.

Camel disables producer health checks by default; turn them on with `camel.health.producersEnabled=true`, or per component with `healthCheckProducerEnabled`. The check reports DOWN with the underlying reason — an unreachable server and a server answering its health endpoint with an error are reported differently, so a deny is never confused with an outage.

`OpaSecurityPolicy` registers an equivalent check, under an id starting `security-policy:opa-`. It is arguably the more important of the two: a denied producer merely records a verdict the route can inspect, while the policy throws `CamelAuthorizationException` and stops the exchange, so an unreachable server there fails every message outright. That is why the policy’s check is on by default rather than opt-in like the producer’s. Set `healthCheckEnabled=false` on the policy for a route that should stay ready regardless — one running `failOpen`, say — in preference to hiding the check with `camel.health.exclude-pattern`.

Neither check is registered when an `opaClient` was injected: that client may point anywhere and neither the endpoint nor the policy has a way to ask it where, so probing the configured `serverUrl` would report on a server they may never talk to. The endpoint check is also skipped when no `serverUrl` was given, and in `wasm` mode, where the policy is evaluated in-process and there is no server to probe.

## Security notes

-   The policy path comes from the endpoint only. It is deliberately not overridable by a message header, so an inbound message cannot pick which policy judges it.
    
-   OPA is a trusted component, typically running as a sidecar reachable only from the application. When it is not, put the connection on a trusted network and authenticate to it with `bearerToken`.
    
-   The component decides; it does not authenticate. Establish **who** the caller is first — with SPIFFE workload identity, a verified JWT, or the surrounding transport’s authentication — and hand the policy that identity through `includeProperties` rather than through a header, as [Authorizing an identity](#authorizing-an-identity) explains.