# OpenFGA

**Since Camel 4.23**

**Only producer is supported**

The OpenFGA component turns a Camel route into a Policy Enforcement Point (PEP) in front of [OpenFGA](https://openfga.dev), the CNCF authorization engine that implements Google’s Zanzibar model. Where a policy engine asks **what do the rules say**, OpenFGA answers a different question: **what is this subject’s relationship to this resource**.

That distinction is the reason the component exists. Expressing "anne may read `document:budget` because she owns the folder it lives in" as policy-as-code means shipping the relationship graph into the policy input on every message, which does not scale past a handful of relationships. OpenFGA keeps the graph — a set of `(user, relation, object)` tuples — in the decision point, and the route asks it a question instead of handing it data.

The component is a companion to `camel-opa` and `camel-spiffe`, and deliberately shares camel-opa’s shape and its security posture, so that an operator who knows one knows the other:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><code>camel-spiffe</code></td><td class="tableblock halign-left valign-top">establishes <strong>who the caller is</strong> (workload identity, X.509-SVID / JWT-SVID)</td></tr><tr><td class="tableblock halign-left valign-top"><code>camel-opa</code></td><td class="tableblock halign-left valign-top">evaluates <strong>what the rules say</strong> (policy-as-code, Rego)</td></tr><tr><td class="tableblock halign-left valign-top">camel-openfga</td><td class="tableblock halign-left valign-top">answers <strong>what the caller’s relationship to the resource is</strong> (ReBAC, relationship tuples)</td></tr></tbody></table>

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openfga</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

openfga:operation\[?options\]

Where `operation` is one of `check`, `batchCheck`, `listObjects`, `listRelations`, `listUsers`, `writeTuples` or `deleteTuples`.

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

The OpenFGA component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiUrl** (producer) | The base URL of the OpenFGA HTTP API, without a trailing path. The default assumes OpenFGA running as a sidecar on its standard HTTP port. | [http://localhost:8080](http://localhost:8080) | String |
| **authorizationModelId** (producer) | The identifier of the authorization model revision to evaluate against. Leave it empty to use whichever model the store considers latest. Pin it in production. A store keeps every model it was ever given and latest moves the moment somebody writes a new one, so an unpinned endpoint can start answering a different question than the one it was reviewed with - without any change to the route. Pinning also makes a model rollout a deliberate, reviewable configuration change. |  | String |
| **configuration** (producer) | The component configuration. |  | OpenFgaConfiguration |
| **consistency** (producer) | 
The consistency the query is answered with. OpenFGA’s default, MINIMIZE\_LATENCY, may answer from a replica that has not caught up yet, which right after a revoke means a tuple that was deleted can still grant access for a moment. Set HIGHER\_CONSISTENCY on the paths where that window matters, at the cost of latency. Left unset, OpenFGA’s own default applies.

Enum values:

-   UNSPECIFIED
    
-   MINIMIZE\_LATENCY
    
-   HIGHER\_CONSISTENCY
    





 |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **object** (producer) | The object being accessed, as an OpenFGA object identifier such as \\{code document:budget}. Evaluated as a Simple expression against each exchange, so document:$\\{header.documentId} names the resource the message is about. Unlike the subject, taking the object from a header is normal and safe: the caller is entitled to say which resource it wants, and the check is what decides whether it may have it. |  | String |
| **relation** (producer) | The relation to demand, such as reader or owner. Evaluated as a Simple expression against each exchange, though a literal is what you usually want. The relation is the permission being demanded, so resolving it from an inbound header lets the caller pick the weakest one the model defines. Keep it literal, or derive it from something the route controls such as $\\{header.CamelHttpMethod}. |  | String |
| **relations** (producer) | Comma-separated list of relations the listRelations operation asks about, for example reader,writer,owner. Only the ones the subject actually holds come back. |  | String |
| **storeId** (producer) | **Required** The identifier of the OpenFGA store holding the relationship tuples and the authorization model, as returned by \\{code fga store create}. The store is the relationship graph that judges the exchange, so it comes from the endpoint only and is never taken from a message header. |  | String |
| **type** (producer) | The object type to enumerate for the listObjects operation, for example document. This is a type name from the authorization model, so it is taken literally rather than evaluated. |  | String |
| **user** (producer) | The subject to authorize, as an OpenFGA user identifier such as \\{code user:anne}. Evaluated as a Simple expression against each exchange, so a literal is used as-is and user:$\\{exchangeProperty.CamelKeycloakTokenSubject} resolves whatever an earlier step established. Read it from an exchange property rather than a header wherever you can. An exchange property is set by the route itself - by the step that verified the caller - and nothing outside the route can set one. A header, by contrast, is often whatever the caller sent, and an endpoint configured as user:$\\{header.userId} lets the caller choose who to be. \\{code camel-keycloak}'s KeycloakSecurityPolicy already follows that reasoning: it reads the subject from the CamelKeycloakTokenSubject exchange property in preference to the header of the same name, its preferPropertyOverHeader option defaulting to true. Nothing in Camel sets the property for you, so the step that validates the token has to record it - but recording it under that name lets one identity serve both. An expression that resolves to blank, or to a bare \\{code user:} prefix, denies the exchange: an exchange carrying no identity is not authorized, and failOpen does not apply to it. |  | String |
| **userFilters** (producer) | Comma-separated list of user filters for the listUsers operation, naming which kinds of subject to return. An entry is either a type, user, or a type and a relation, team#member, to return the usersets holding the relation rather than the individual subjects. Defaults to user. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectTimeout** (advanced) | How long to wait for the connection to OpenFGA to be established. The component applies this itself rather than through the SDK’s own connectTimeout setting, which as of openfga-sdk 0.10.1 is accepted and then never read, leaving the connect phase bounded only by the operating system. | 10000 | long |
| **maxParallelRequests** (advanced) | How many of a batchCheck’s checks may be in flight at once. The batch is issued as one request per object, so this bounds the load one exchange puts on the server. | 10 | int |
| **maxRetries** (advanced) | How many times the SDK retries a request that failed in a way worth retrying, such as a rate limit or a 5xx. Set it to 0 to disable retries; the overall wait a routing thread can spend on one exchange grows with it. | 3 | int |
| **openFgaClient** (advanced) | **Autowired** An existing OpenFgaClient to use. When set, every option describing how to reach the server - apiUrl, storeId, the credentials, the timeouts and sslContextParameters - is ignored, because they are baked into the client that was handed over. |  | OpenFgaClient |
| **readTimeout** (advanced) | How long to wait for one request to OpenFGA to complete once connected. A request that times out is a failure to obtain a verdict rather than a deny, so it fails closed - or proceeds when failOpen is set. | 10000 | long |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **apiAudience** (security) | The audience to request the access token for in the client-credentials flow. |  | String |
| **apiToken** (security) | Pre-shared token sent to OpenFGA in the Authorization header, for a server started with \\{code --authn-method preshared}. |  | String |
| **apiTokenIssuer** (security) | The token endpoint the client-credentials flow exchanges its credentials at. |  | String |
| **clientId** (security) | Client identifier for the OAuth 2.0 client-credentials flow, for a server that authenticates through an OIDC provider. Setting it selects that flow, so clientSecret, apiTokenIssuer and apiAudience are then required too. |  | String |
| **clientSecret** (security) | Client secret for the OAuth 2.0 client-credentials flow. |  | String |
| **failOpen** (security) | Whether to let the exchange proceed when OpenFGA could not be asked at all, for example because the server is unreachable. Disabled by default so that an unavailable decision point denies rather than grants access. Do not enable this in production. It applies to the check operation and to OpenFgaSecurityPolicy, the two places where proceed has a meaning, and it covers only a failure to obtain a verdict. An exchange that was denied, and an exchange that carried no usable subject or object, are decisions rather than failures and are never turned into an allow by this flag. The other operations ignore it. A batchCheck or listObjects that failed has no safe way to proceed - returning the objects it never managed to filter would be the leak the filtering was there to prevent - so a failure there is reported as an error for the route’s own error handling to deal with. | false | boolean |
| **scopes** (security) | Space-separated scopes to request in the client-credentials flow. |  | String |
| **sslContextParameters** (security) | TLS configuration for the connection to OpenFGA. Needed to trust a server whose certificate comes from a private CA, and to present a client certificate to a server that requires mutual TLS - a SPIFFE X.509-SVID obtained with \\{code camel-spiffe}, for instance, so the workload authenticates to the decision point as itself. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The OpenFGA endpoint is configured using URI syntax:

openfga:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform. The operation is taken from the endpoint only: it is deliberately not overridable by a message header, so that an inbound message cannot turn a check into a tuple write, nor a check for one relation into a check for a weaker one.

Enum values:

-   check
    
-   batchCheck
    
-   listObjects
    
-   listRelations
    
-   listUsers
    
-   writeTuples
    
-   deleteTuples
    





 |  | OpenFgaOperation |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiUrl** (producer) | The base URL of the OpenFGA HTTP API, without a trailing path. The default assumes OpenFGA running as a sidecar on its standard HTTP port. | [http://localhost:8080](http://localhost:8080) | String |
| **authorizationModelId** (producer) | The identifier of the authorization model revision to evaluate against. Leave it empty to use whichever model the store considers latest. Pin it in production. A store keeps every model it was ever given and latest moves the moment somebody writes a new one, so an unpinned endpoint can start answering a different question than the one it was reviewed with - without any change to the route. Pinning also makes a model rollout a deliberate, reviewable configuration change. |  | String |
| **consistency** (producer) | 
The consistency the query is answered with. OpenFGA’s default, MINIMIZE\_LATENCY, may answer from a replica that has not caught up yet, which right after a revoke means a tuple that was deleted can still grant access for a moment. Set HIGHER\_CONSISTENCY on the paths where that window matters, at the cost of latency. Left unset, OpenFGA’s own default applies.

Enum values:

-   UNSPECIFIED
    
-   MINIMIZE\_LATENCY
    
-   HIGHER\_CONSISTENCY
    





 |  | String |
| **object** (producer) | The object being accessed, as an OpenFGA object identifier such as \\{code document:budget}. Evaluated as a Simple expression against each exchange, so document:$\\{header.documentId} names the resource the message is about. Unlike the subject, taking the object from a header is normal and safe: the caller is entitled to say which resource it wants, and the check is what decides whether it may have it. |  | String |
| **relation** (producer) | The relation to demand, such as reader or owner. Evaluated as a Simple expression against each exchange, though a literal is what you usually want. The relation is the permission being demanded, so resolving it from an inbound header lets the caller pick the weakest one the model defines. Keep it literal, or derive it from something the route controls such as $\\{header.CamelHttpMethod}. |  | String |
| **relations** (producer) | Comma-separated list of relations the listRelations operation asks about, for example reader,writer,owner. Only the ones the subject actually holds come back. |  | String |
| **storeId** (producer) | **Required** The identifier of the OpenFGA store holding the relationship tuples and the authorization model, as returned by \\{code fga store create}. The store is the relationship graph that judges the exchange, so it comes from the endpoint only and is never taken from a message header. |  | String |
| **type** (producer) | The object type to enumerate for the listObjects operation, for example document. This is a type name from the authorization model, so it is taken literally rather than evaluated. |  | String |
| **user** (producer) | The subject to authorize, as an OpenFGA user identifier such as \\{code user:anne}. Evaluated as a Simple expression against each exchange, so a literal is used as-is and user:$\\{exchangeProperty.CamelKeycloakTokenSubject} resolves whatever an earlier step established. Read it from an exchange property rather than a header wherever you can. An exchange property is set by the route itself - by the step that verified the caller - and nothing outside the route can set one. A header, by contrast, is often whatever the caller sent, and an endpoint configured as user:$\\{header.userId} lets the caller choose who to be. \\{code camel-keycloak}'s KeycloakSecurityPolicy already follows that reasoning: it reads the subject from the CamelKeycloakTokenSubject exchange property in preference to the header of the same name, its preferPropertyOverHeader option defaulting to true. Nothing in Camel sets the property for you, so the step that validates the token has to record it - but recording it under that name lets one identity serve both. An expression that resolves to blank, or to a bare \\{code user:} prefix, denies the exchange: an exchange carrying no identity is not authorized, and failOpen does not apply to it. |  | String |
| **userFilters** (producer) | Comma-separated list of user filters for the listUsers operation, naming which kinds of subject to return. An entry is either a type, user, or a type and a relation, team#member, to return the usersets holding the relation rather than the individual subjects. Defaults to user. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectTimeout** (advanced) | How long to wait for the connection to OpenFGA to be established. The component applies this itself rather than through the SDK’s own connectTimeout setting, which as of openfga-sdk 0.10.1 is accepted and then never read, leaving the connect phase bounded only by the operating system. | 10000 | long |
| **maxParallelRequests** (advanced) | How many of a batchCheck’s checks may be in flight at once. The batch is issued as one request per object, so this bounds the load one exchange puts on the server. | 10 | int |
| **maxRetries** (advanced) | How many times the SDK retries a request that failed in a way worth retrying, such as a rate limit or a 5xx. Set it to 0 to disable retries; the overall wait a routing thread can spend on one exchange grows with it. | 3 | int |
| **openFgaClient** (advanced) | **Autowired** An existing OpenFgaClient to use. When set, every option describing how to reach the server - apiUrl, storeId, the credentials, the timeouts and sslContextParameters - is ignored, because they are baked into the client that was handed over. |  | OpenFgaClient |
| **readTimeout** (advanced) | How long to wait for one request to OpenFGA to complete once connected. A request that times out is a failure to obtain a verdict rather than a deny, so it fails closed - or proceeds when failOpen is set. | 10000 | long |
| **apiAudience** (security) | The audience to request the access token for in the client-credentials flow. |  | String |
| **apiToken** (security) | Pre-shared token sent to OpenFGA in the Authorization header, for a server started with \\{code --authn-method preshared}. |  | String |
| **apiTokenIssuer** (security) | The token endpoint the client-credentials flow exchanges its credentials at. |  | String |
| **clientId** (security) | Client identifier for the OAuth 2.0 client-credentials flow, for a server that authenticates through an OIDC provider. Setting it selects that flow, so clientSecret, apiTokenIssuer and apiAudience are then required too. |  | String |
| **clientSecret** (security) | Client secret for the OAuth 2.0 client-credentials flow. |  | String |
| **failOpen** (security) | Whether to let the exchange proceed when OpenFGA could not be asked at all, for example because the server is unreachable. Disabled by default so that an unavailable decision point denies rather than grants access. Do not enable this in production. It applies to the check operation and to OpenFgaSecurityPolicy, the two places where proceed has a meaning, and it covers only a failure to obtain a verdict. An exchange that was denied, and an exchange that carried no usable subject or object, are decisions rather than failures and are never turned into an allow by this flag. The other operations ignore it. A batchCheck or listObjects that failed has no safe way to proceed - returning the objects it never managed to filter would be the leak the filtering was there to prevent - so a failure there is reported as an error for the route’s own error handling to deal with. | false | boolean |
| **scopes** (security) | Space-separated scopes to request in the client-credentials flow. |  | String |
| **sslContextParameters** (security) | TLS configuration for the connection to OpenFGA. Needed to trust a server whose certificate comes from a private CA, and to present a client certificate to a server that requires mutual TLS - a SPIFFE X.509-SVID obtained with \\{code camel-spiffe}, for instance, so the workload authenticates to the decision point as itself. |  | SSLContextParameters |

## Message Headers

The OpenFGA component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenFgaAllowed** (producer) Constant: [`ALLOWED`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#ALLOWED) | The allow/deny verdict of the authorization check. Always overwritten by the component, so a value set by an inbound message never survives into the route. |  | Boolean |
| **CamelOpenFgaDenyReason** (producer) Constant: [`DENY_REASON`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#DENY_REASON) | Why the exchange was denied, set only on a deny. denied when OpenFGA evaluated the relationship and answered no; missing-user, missing-object, missing-relation, wildcard-subject or invalid-identifier when the exchange never reached OpenFGA because what it carried could not be used as a subject or an object. |  | String |
| **CamelOpenFgaFailedOpen** (producer) Constant: [`FAILED_OPEN`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#FAILED_OPEN) | Set to true only when the exchange proceeded because failOpen is enabled and OpenFGA could not be asked - nothing authorized it. Absent on every verdict OpenFGA actually gave, so a route or an audit trail can tell the two apart rather than seeing the same CamelOpenFgaAllowed=true for both. |  | Boolean |
| **CamelOpenFgaUser** (producer) Constant: [`USER`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#USER) | The subject the check was made for, as resolved from the endpoint’s user expression. Set for observability; it is not read as an input. |  | String |
| **CamelOpenFgaObject** (producer) Constant: [`OBJECT`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#OBJECT) | The object the check was made against, as resolved from the endpoint’s object expression. Set for observability; it is not read as an input. |  | String |
| **CamelOpenFgaRelation** (producer) Constant: [`RELATION`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#RELATION) | The relation that was checked. Set for observability; it is not read as an input and cannot be used to demand a weaker permission than the endpoint configured. |  | String |
| **CamelOpenFgaStoreId** (producer) Constant: [`STORE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#STORE_ID) | The identifier of the OpenFGA store that was consulted, so an audit trail records which relationship graph produced the verdict. |  | String |
| **CamelOpenFgaWrittenTuples** (producer) Constant: [`WRITTEN_TUPLES`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#WRITTEN_TUPLES) | How many relationship tuples the writeTuples operation wrote. |  | Integer |
| **CamelOpenFgaDeletedTuples** (producer) Constant: [`DELETED_TUPLES`](https://javadoc.io/doc/org.apache.camel/camel-openfga/latest/org/apache/camel/component/openfga/OpenFgaConstants.html#DELETED_TUPLES) | How many relationship tuples the deleteTuples operation deleted. |  | Integer |

## Resolving the subject and the object

`user`, `object` and `relation` are evaluated as [Simple](languages/simple-language.md) expressions against each Exchange, so a literal is used as written and an expression resolves per message:

```java
to("openfga:check"
        + "?storeId=01HQMVAJ..."
        + "&relation=reader"
        + "&user=user:${exchangeProperty.CamelKeycloakTokenSubject}"
        + "&object=document:${header.documentId}");
```

The component evaluates these itself, per Exchange, so a plain `to()` is enough — there is no need for `toD()` and the endpoint cache it churns.

> **Important**
> Read the subject from an exchange property, not a header
>
> An endpoint configured as `user=user:${header.userId}` lets the caller choose who to be — it is the authorization-bypass equivalent of trusting a client-supplied username.
>
> Put the subject where the caller cannot reach it. An exchange property set by the step in your route that **verified** the caller cannot be set from outside the route, and a header usually can. Name that property here, and let authentication decide who the caller is.
>
> There is a convention worth following rather than inventing one: ``camel-keycloak’s `KeycloakSecurityPolicy`` reads the subject from the `CamelKeycloakTokenSubject` exchange property in preference to the header of the same name — its `preferPropertyOverHeader` option defaults to `true`, for exactly the reason above. Nothing in Camel sets that property for you, so the step in your route that validates the token is what has to record it; but recording it under that name means the same identity serves both components.
>
> Taking the **object** from a header is a different matter and is entirely normal: the caller is entitled to say **which** resource it wants, and the check is what decides whether it may have it.

## Usage

### As a producer, deciding with a filter

The `check` operation records the verdict in the `CamelOpenFgaAllowed` header and leaves the message body untouched, so the route decides what to do with it:

```java
from("platform-http:/documents")
        .to("openfga:check?storeId={{fga.store}}&authorizationModelId={{fga.model}}"
            + "&relation=reader&user=user:${exchangeProperty.CamelKeycloakTokenSubject}"
            + "&object=document:${header.documentId}")
        .choice()
            .when(header("CamelOpenFgaAllowed").isEqualTo(true))
                .to("direct:serveDocument")
            .otherwise()
                .setHeader(Exchange.HTTP_RESPONSE_CODE, constant(403));
```

### As a security policy, stopping the route

`OpenFgaSecurityPolicy` is an `AuthorizationPolicy`, so the check guards a section of the route and a denial throws `CamelAuthorizationException` for the usual `onException` machinery to handle:

```java
OpenFgaSecurityPolicy policy = new OpenFgaSecurityPolicy();
policy.setApiUrl("http://openfga:8080");
policy.setStoreId("01HQMVAJ...");
policy.setAuthorizationModelId("01HQMVAK...");
policy.setRelation("writer");
policy.setUser("user:${exchangeProperty.CamelKeycloakTokenSubject}");
policy.setObject("document:${header.documentId}");

from("platform-http:/documents")
        .policy(policy)
        .to("direct:updateDocument");
```

### Filtering a collection

`batchCheck` takes the object identifiers from the body and replaces it with the ones the check allowed, in the order the body asked in:

```java
from("direct:listDocuments")
        .to("sql:SELECT id FROM documents")
        // sql: answers with a List<Map>, one entry per row, so turn it into the object identifiers first - a Map
        // would stringify to {ID=budget}, which is not an identifier and would simply be skipped
        .process(exchange -> {
            List<Map<String, Object>> rows = exchange.getMessage().getBody(List.class);
            exchange.getMessage().setBody(rows.stream().map(row -> "document:" + row.get("id")).toList());
        })
        .to("openfga:batchCheck?storeId={{fga.store}}&relation=reader"
            + "&user=user:${exchangeProperty.CamelKeycloakTokenSubject}")
        .to("direct:render");
```

The body comes back holding only the identifiers the check allowed, in the order it was given them.

`listObjects` answers the same question from the other end — ask OpenFGA which objects the subject can reach, rather than filtering a list you already have:

```java
to("openfga:listObjects?storeId={{fga.store}}&relation=reader"
   + "&user=user:${exchangeProperty.CamelKeycloakTokenSubject}&type=document");
// body becomes [document:budget, document:roadmap]
```

`listRelations` and `listUsers` round this out: what a subject may do with one object, and who may do something with it. Both replace the body with a `List<String>`.

### Granting and revoking access

A route that creates a resource usually has to grant access to it too. `writeTuples` takes its tuples from the body, and falls back to the endpoint’s `user`/`relation`/`object` when the body carries none — which is the shape that reads best right after a resource was created:

```java
from("direct:createDocument")
        .to("sql:INSERT INTO documents ...")
        .to("openfga:writeTuples?storeId={{fga.store}}"
            + "&user=user:${exchangeProperty.CamelKeycloakTokenSubject}&relation=owner"
            + "&object=document:${header.documentId}");
```

For several tuples at once, leave `user`/`relation`/`object` unset and put them in the body instead — a collection of ``Map`s with `user``, `relation` and `object` entries, or of `ClientTupleKey` objects. `deleteTuples` accepts the same shapes and revokes instead.

> **Important**
> The endpoint wins over the body
>
> If the endpoint configures any of `user`, `relation` or `object`, that is the tuple written and the body is not consulted. The body is read only when the endpoint names none of them.
>
> The same rule that governs a check governs a write: the configuration decides and the message does not. Were the body preferred, a route that unmarshals an untrusted payload before writing would hand the caller the choice of which relationship to grant — and `{"user": "user:attacker", "relation": "owner", "object": "document:secret"}` is a perfectly well-formed tuple.
>
> A partly configured triple is treated as a mistake rather than an invitation to fill the rest in from the message: the producer fails and names the part that is missing.

A typed wildcard — `user:*`, OpenFGA’s "everyone" — is accepted here, because writing that tuple is how a resource is shared publicly and is a deliberate act by the route. It is **refused** as the subject of a check; see below.

## Security

### It fails closed

An OpenFGA server that cannot be reached, or that answers with an error, denies. The `failOpen` option reverses that and is off by default; it is marked `insecure:dev` and should not be enabled in production.

`failOpen` covers only a **failure to obtain an answer**, and only for `check` and for `OpenFgaSecurityPolicy` — the two places where "proceed" means something. It never turns a denial into an allow, and it never applies to an Exchange that carried no usable subject (see below).

When `failOpen` does let an exchange through, it carries `CamelOpenFgaFailedOpen=true`. The verdict header alone cannot distinguish "OpenFGA allowed this" from "OpenFGA was never reached and we were told to proceed", and an audit asking which exchanges went through unauthorized needs something it can filter on. The marker is set only on that deliberate path, and it is cleared on entry like the other decision headers so a sender cannot preload it.

It also does not apply when OpenFGA answers with an HTTP 4xx. A 400 means the question was malformed, a 401 or 403 that this client may not ask it, a 404 that what was asked about does not exist — none of which is a decision point that has gone away. This matters concretely: an object identifier can get past the component’s own guards and still be rejected by the server (`document:a:b` and `document:x#y` are both HTTP 400 on OpenFGA 1.21.0), and if `failOpen` covered that, any caller able to influence the identifier could turn a check into an allow. Those fail closed, and the component logs why it did not fail open. A 429 is the one 4xx that does count as unavailable — it means "not right now" — as do transport errors, timeouts and 5xx.

The rule is an allowlist rather than a list of exclusions: `failOpen` applies to a rate limit, a 5xx, a transport error and a timeout, and to nothing else. A failure the component does not recognise — a request the SDK refused to build, input it could not serialise, an interrupt during shutdown — is not evidence that OpenFGA was unreachable, so it denies. Anything unfamiliar therefore fails closed rather than being waved through for being unfamiliar.

The query operations ignore `failOpen` entirely: a `batchCheck` or `listObjects` that failed has no safe way to proceed, since handing back the objects it never managed to filter would be exactly the leak the filtering was there to prevent.

### What is asked is not up to the message

`storeId`, `authorizationModelId`, `relation` and the `operation` all come from the endpoint. An inbound message cannot point the check at a different store, pin an older model revision, downgrade the relation demanded from `owner` to `reader`, or turn a check into a tuple write.

The `CamelOpenFga*` headers are outputs only. They are cleared on entry — before the expressions are evaluated — written on every evaluation, and never read back as inputs, so a verdict a message arrived with never survives into the route, including down the paths that throw.

### A missing identity is a denial, not a failure

If the `user` or `object` expression resolves to blank — or to a bare `user:` prefix, which is what a configured prefix plus an unresolved expression leaves behind — the Exchange is denied with `CamelOpenFgaDenyReason` set to `missing-user` or `missing-object`, and OpenFGA is never asked.

This split matters. OpenFGA would reject a blank subject with an HTTP 400, which is a **failure** to obtain a verdict — and with `failOpen` set a failure becomes an allow. An Exchange that carried no identity has not been authorized by anything, so it is denied, and `failOpen` does not reach it.

### A wildcard subject is refused

`user:*` is a legitimate thing to write a tuple for. It is not a legitimate thing to **check**: asking "may everyone read this" is not asking whether the caller may, and OpenFGA answers `true` for it wherever a public-access tuple exists. A `user` expression that resolved to a typed wildcard would therefore hand out every publicly shared object, so it is denied with `CamelOpenFgaDenyReason` set to `wildcard-subject`.

### Pin the authorization model

`authorizationModelId` is optional, and leaving it out means "whichever model the store considers latest". A store keeps every model it was ever given and "latest" moves the moment somebody writes a new one, so an unpinned endpoint can start answering a different question than the one it was reviewed with — with no change to the route. The component logs a warning at startup when it is unset. Pin it in production, so that a model rollout is a deliberate, reviewable configuration change.

### Consistency

OpenFGA’s default read consistency may answer from a replica that has not caught up, which right after a revoke means a deleted tuple can still grant access for a moment. Set `consistency=HIGHER_CONSISTENCY` on the paths where that window matters, at the cost of latency.

The value is checked when the endpoint starts, and an unrecognised one — `higher_consistency`, say — is refused rather than accepted and quietly sent as `unknown_default_open_api` on every request.

### Authentication and TLS

For a server started with `--authn-method preshared`, set `apiToken`. For one behind an OIDC provider, set `clientId`, `clientSecret`, `apiTokenIssuer` and `apiAudience` for the OAuth 2.0 client-credentials flow. Both `apiToken` and `clientSecret` are marked secret and are masked wherever Camel prints an endpoint URI.

`sslContextParameters` configures TLS, including presenting a client certificate to a server that requires mutual TLS. A SPIFFE X.509-SVID obtained through `camel-spiffe` works here, which closes the loop: the workload authenticates to the authorization decision point as itself.

> **Note**
> `useGlobalSslContextParameters` on the component has no effect on `OpenFgaSecurityPolicy`. The policy is a standalone bean and is not bound to a component instance, so set `sslContextParameters` on it explicitly.

### Timeouts

`connectTimeout` and `readTimeout` bound the call, and `maxRetries` bounds how often a retryable failure is re-attempted. The component supplies the SDK’s HTTP client itself so that `connectTimeout` actually takes effect; the SDK’s own `connectTimeout` setting is accepted and then never read, and the client it builds by default sets none, leaving the connect phase bounded only by the operating system.

## Health checks

Both the producer and `OpenFgaSecurityPolicy` register a readiness check that probes OpenFGA’s `/healthz` endpoint. Because the component fails closed, a route that is up but cannot reach OpenFGA fails every message, so it is not ready — and this makes that visible before traffic arrives rather than only in the error logs afterwards.

The check requires the server to report `SERVING`, not merely to answer with HTTP 200: the HTTP gateway can answer 200 while the health service behind it reports `NOT_SERVING`.

No check is registered for an injected `openFgaClient`, which can point anywhere the component has no way to ask about. Set `healthCheckProducerEnabled=false` on the component, or `healthCheckEnabled=false` on the policy, to turn them off.

## What this component does not do yet

-   **Contextual tuples and condition context on a check.** A contextual tuple derived from a message is a self-authorization primitive — `(user:me, owner, document:secret)` — so rather than ship a gate for it that has not been reviewed, the first release leaves it out entirely.
    
-   The `expand`, `readTuples` and `readChanges` operations, and store or authorization-model management.
    

## Examples

Guarding an HTTP endpoint, with the identity coming from an authentication step earlier in the route:

```java
from("platform-http:/orders/{orderId}")
        // whatever verifies the caller, ending in a processor that records the verified subject as a property
        .to("direct:authenticate")
        .to("openfga:check?storeId={{fga.store}}&authorizationModelId={{fga.model}}"
            + "&relation=can_view&user=user:${exchangeProperty.CamelKeycloakTokenSubject}"
            + "&object=order:${header.orderId}")
        .filter(header("CamelOpenFgaAllowed").isEqualTo(true))
            .to("direct:serveOrder");
```