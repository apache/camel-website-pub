Camel Components

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
| **allowKey** (producer) | The key to read the allow/deny verdict from when the policy returns an object rather than a plain boolean. For a policy returning \\{allow: true, reasons: } the default value of allow is what you want. | allow | String |
| **configuration** (producer) | The component configuration. |  | OpaConfiguration |
| **includeBody** (producer) | Whether to send the message body to OPA as part of the input document. Disabled by default: bodies can be large or streaming, and most authorization decisions only need headers. When enabled on a streaming body, enable stream caching so that the body is still readable by the rest of the route. | false | boolean |
| **includeHeaders** (producer) | Comma-separated list of message header names to send to OPA in the input document. The default of \\{code } sends every header. Narrow it when the policy only needs a few headers, or when the message carries headers that should not leave the JVM. | \* | String |
| **includeProperties** (producer) | Comma-separated list of exchange property names to send to OPA in the input document, or \\{code } for all of them. Empty by default, so no properties are sent unless asked for. This is where the authentication components put the identity they verified: \\{code camel-keycloak} stores the access token and its subject as exchange properties and prefers them over the equivalent headers, precisely because headers can be set by the caller. List those property names here to let a policy authorize the identity an earlier step established, instead of copying it into a header first. Only custom properties are sent; Camel’s own internal exchange properties are never included. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **serverUrl** (producer) | The base URL of the OPA server, without the \\{code /v1/data} suffix. The default assumes OPA running as a sidecar on the standard port. | [http://localhost:8181](http://localhost:8181) | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **opaClient** (advanced) | **Autowired** An existing OPAClient to use. When set, serverUrl and bearerToken are ignored. |  | OPAClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **bearerToken** (security) | Bearer token sent to the OPA server in the Authorization header, for an OPA instance that has its API authentication enabled. |  | String |
| **failOpen** (security) | Whether to allow the exchange to proceed when the policy cannot be evaluated at all, for example because the OPA server is unreachable. Disabled by default so that an unreachable policy decision point denies rather than grants access. Do not enable this in production. | false | boolean |

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
| **allowKey** (producer) | The key to read the allow/deny verdict from when the policy returns an object rather than a plain boolean. For a policy returning \\{allow: true, reasons: } the default value of allow is what you want. | allow | String |
| **includeBody** (producer) | Whether to send the message body to OPA as part of the input document. Disabled by default: bodies can be large or streaming, and most authorization decisions only need headers. When enabled on a streaming body, enable stream caching so that the body is still readable by the rest of the route. | false | boolean |
| **includeHeaders** (producer) | Comma-separated list of message header names to send to OPA in the input document. The default of \\{code } sends every header. Narrow it when the policy only needs a few headers, or when the message carries headers that should not leave the JVM. | \* | String |
| **includeProperties** (producer) | Comma-separated list of exchange property names to send to OPA in the input document, or \\{code } for all of them. Empty by default, so no properties are sent unless asked for. This is where the authentication components put the identity they verified: \\{code camel-keycloak} stores the access token and its subject as exchange properties and prefers them over the equivalent headers, precisely because headers can be set by the caller. List those property names here to let a policy authorize the identity an earlier step established, instead of copying it into a header first. Only custom properties are sent; Camel’s own internal exchange properties are never included. |  | String |
| **serverUrl** (producer) | The base URL of the OPA server, without the \\{code /v1/data} suffix. The default assumes OPA running as a sidecar on the standard port. | [http://localhost:8181](http://localhost:8181) | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **opaClient** (advanced) | **Autowired** An existing OPAClient to use. When set, serverUrl and bearerToken are ignored. |  | OPAClient |
| **bearerToken** (security) | Bearer token sent to the OPA server in the Authorization header, for an OPA instance that has its API authentication enabled. |  | String |
| **failOpen** (security) | Whether to allow the exchange to proceed when the policy cannot be evaluated at all, for example because the OPA server is unreachable. Disabled by default so that an unreachable policy decision point denies rather than grants access. Do not enable this in production. | false | boolean |

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

`headers` carries every message header by default. Set `includeHeaders` to a comma-separated list of names (matched case-insensitively) when the policy only needs a few of them. `body` is **not** sent unless `includeBody` is enabled: bodies can be large or streaming, and most authorization decisions do not need them. When you do enable it on a streaming body, enable stream caching so the body is still readable by the rest of the route.

`properties` is empty unless you ask for it — see [Authorizing an identity](#authorizing-an-identity) below.

Header and body values that are not JSON-native are converted to their string form. That conversion is shallow: a `Map` or `List` value is passed through as-is, so anything non-JSON-native nested inside it is left for the OPA SDK’s serializer to render. A policy that reads nested structures should not assume the same string conversion applies at depth.

The component’s own `CamelOpa*` decision headers are never sent back to OPA, so a policy cannot be shown a verdict that an inbound message claimed for itself.

## Reading the verdict

`CamelOpaDecision` holds the decision document exactly as OPA returned it. `CamelOpaDecisionAllow` holds the boolean verdict read out of it:

-   a decision that **is** a boolean is the verdict;
    
-   a decision that is an object is searched for the `allowKey` entry (`allow` by default), which must itself be a boolean;
    
-   anything else cannot be read as a verdict and counts as a deny, with the raw document still available for the route to inspect.
    

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

## Failure handling

The component fails closed. If the policy cannot be evaluated at all — the OPA server is unreachable, times out, or answers with an error — the producer throws an `OpaPolicyEvaluationException` and `OpaSecurityPolicy` throws a `CamelAuthorizationException`; in neither case does the message proceed as allowed. This is deliberately different from a deny, which is a decision rather than a failure, so a route can tell "denied" from "no policy decision point available".

Setting `failOpen=true` reverses this and lets the exchange proceed when the policy cannot be evaluated. It exists for development and for non-critical policies, and should not be enabled in production.

Note that OPA reports an **undefined** decision — no rule matched and the policy declares no default — as an error rather than as a deny, so it fails closed as well. Give every decision rule a default, as in the example above, so the policy always returns a verdict.

## Health check

Because the component fails closed, an OPA server that cannot be reached fails **every** exchange through the route. The producer registers a readiness check that probes the server’s `/health` endpoint, so an unavailable policy decision point shows up in the health registry rather than only in the error logs once traffic starts failing.

Camel disables producer health checks by default; turn them on with `camel.health.producersEnabled=true`, or per component with `healthCheckProducerEnabled`. The check reports DOWN with the underlying reason — an unreachable server and a server answering its health endpoint with an error are reported differently, so a deny is never confused with an outage.

The check is only registered when the endpoint was given a `serverUrl`. An injected `opaClient` may point anywhere and the endpoint has no way to ask it where, so no probe is registered in that case.

## Security notes

-   The policy path comes from the endpoint only. It is deliberately not overridable by a message header, so an inbound message cannot pick which policy judges it.
    
-   OPA is a trusted component, typically running as a sidecar reachable only from the application. When it is not, put the connection on a trusted network and authenticate to it with `bearerToken`.
    
-   The component decides; it does not authenticate. Establish **who** the caller is first — with SPIFFE workload identity, a verified JWT, or the surrounding transport’s authentication — and hand the policy that identity through `includeProperties` rather than through a header, as [Authorizing an identity](#authorizing-an-identity) explains.