# TypeSafe AI

**Since Camel 4.23**

**Only producer is supported**

The TypeSafe AI component evaluates explicit state against Noul (yes/no), Choice (one category), and Score (ordered rubric) questions using [TypeSafe AI’s HTTP API](https://docs.typesafe.ai/api). Jev is the default model; the `model` option can select another model supported by the API. It calls the service directly using the JDK HTTP client and Camel JSON utilities. For semantic conditions in Java, XML and YAML, use the [TypeSafe AI language](languages/typesafe-ai-language.md) supplied by this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-typesafe-ai</artifactId>
    <version>x.x.x</version>
</dependency>
```

## URI format

```text
typesafe-ai:name[?options]
```

`name` identifies an endpoint; it is not sent to the model. Producers and predicates using the same URI share its client and configuration. Each endpoint owns one HTTP client, connection pool, and default executor. Reuse the same endpoint URI when its configuration is shared. Camel manages its lifecycle and cancels in-flight requests on stop. Java 21 and later also close the HTTP client explicitly; on Java 17, the JDK reclaims its remaining resources after it becomes unreachable.

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

The TypeSafe AI component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseUrl** (common) | The API base URL. The client appends /v1/systemone. Redirects are not followed. | [https://api.typesafe.ai](https://api.typesafe.ai) | String |
| **configuration** (producer) | Default configuration shared by TypeSafe AI endpoints. |  | TypeSafeAiConfiguration |
| **maxConcurrentRequests** (common) | Maximum concurrent evaluations per endpoint, shared by producers and predicates. Excess requests fail immediately with RejectedExecutionException without being queued or sent. Must be positive. | 64 | int |
| **model** (common) | The model ID or alias. Use a versioned ID to pin decision behavior. | jev-latest | String |
| **questions** (common) | A JSON object mapping question names to Noul, Choice or Score question objects. When set, producers evaluate the selected message state; otherwise the body must contain a complete request map. |  | String |
| **questionsResource** (common) | Camel resource URI for a UTF-8 JSON object mapping question names to Noul, Choice or Score questions. Loaded and validated when the endpoint starts. Cannot be combined with questions. |  | String |
| **requestTimeout** (common) | The timeout in milliseconds for the complete HTTP request and response body. Must be positive. | 30000 | long |
| **state** (common) | The Simple expression selecting state for configured producer questions and the TypeSafe AI language. If not set, the message body is used. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **resultProperty** (producer) | Store the producer response in this exchange property, preserving the original message body. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **threshold** (advanced) | Default inclusive probability threshold for the TypeSafe AI language. Must be within 0,1. | 0.5 | double |
| **uncertainty** (advanced) | Default half-width of the inclusive uncertainty band for the TypeSafe AI language. Zero disables the band. | 0 | double |
| **uncertaintyPolicy** (advanced) | 
Default action for the TypeSafe AI language within the uncertainty band: NonMatch or Fail.

Enum values:

-   NonMatch
    
-   Fail
    





 | NonMatch | UncertaintyPolicy |
| **apiKey** (security) | **Required** The API key used for Bearer authentication. |  | String |

## Endpoint Options

The TypeSafe AI endpoint is configured using URI syntax:

typesafe-ai:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** A logical name for the evaluation endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseUrl** (common) | The API base URL. The client appends /v1/systemone. Redirects are not followed. | [https://api.typesafe.ai](https://api.typesafe.ai) | String |
| **maxConcurrentRequests** (common) | Maximum concurrent evaluations per endpoint, shared by producers and predicates. Excess requests fail immediately with RejectedExecutionException without being queued or sent. Must be positive. | 64 | int |
| **model** (common) | The model ID or alias. Use a versioned ID to pin decision behavior. | jev-latest | String |
| **questions** (common) | A JSON object mapping question names to Noul, Choice or Score question objects. When set, producers evaluate the selected message state; otherwise the body must contain a complete request map. |  | String |
| **questionsResource** (common) | Camel resource URI for a UTF-8 JSON object mapping question names to Noul, Choice or Score questions. Loaded and validated when the endpoint starts. Cannot be combined with questions. |  | String |
| **requestTimeout** (common) | The timeout in milliseconds for the complete HTTP request and response body. Must be positive. | 30000 | long |
| **state** (common) | The Simple expression selecting state for configured producer questions and the TypeSafe AI language. If not set, the message body is used. |  | String |
| **resultProperty** (producer) | Store the producer response in this exchange property, preserving the original message body. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **threshold** (advanced) | Default inclusive probability threshold for the TypeSafe AI language. Must be within 0,1. | 0.5 | double |
| **uncertainty** (advanced) | Default half-width of the inclusive uncertainty band for the TypeSafe AI language. Zero disables the band. | 0 | double |
| **uncertaintyPolicy** (advanced) | 
Default action for the TypeSafe AI language within the uncertainty band: NonMatch or Fail.

Enum values:

-   NonMatch
    
-   Fail
    





 | NonMatch | UncertaintyPolicy |
| **apiKey** (security) | **Required** The API key used for Bearer authentication. |  | String |

## Configuration

Configure credentials through property placeholders or a supported vault:

```properties
camel.component.typesafe-ai.api-key={{env:TYPESAFE_API_KEY}}
camel.component.typesafe-ai.model=jev-1.13.0
camel.component.typesafe-ai.request-timeout=30000
camel.component.typesafe-ai.max-concurrent-requests=64
```

`apiKey` is a secret option. `baseUrl` defaults to `[https://api.typesafe.ai](https://api.typesafe.ai)`; the client appends `/v1/systemone`. A base path can address a proxy. HTTP redirects are not followed. Use HTTPS for the service; HTTP is useful for local testing.

`model` defaults to `jev-latest`. Pin a version when tuning thresholds; aliases can change behavior without a route change. The request map may explicitly override the endpoint’s model for that request. The response’s `model` identifies the model that answered. See [available models](https://docs.typesafe.ai/models).

### Concurrent requests

`maxConcurrentRequests` limits concurrent evaluations to 64 per endpoint by default and must be positive. Producers and predicates using the same endpoint share this limit. A component property sets the default for each endpoint; an endpoint URI can override it, for example `typesafe-ai:refund?maxConcurrentRequests=8`. Different endpoints have independent limits.

When the limit is reached, the evaluation fails immediately with `java.util.concurrent.RejectedExecutionException` before request validation, serialization, or HTTP submission. No request is queued. The slot is released when the evaluation finishes, including on failure, timeout, interruption, or cancellation. Camel’s error handler can handle the rejection through `onException(RejectedExecutionException.class)`.

## Questions from properties

For a fixed set of questions, select state and retain the business message using properties:

```properties
camel.component.typesafe-ai.questions={"refund":{"type":"noul","instructions":"Is a refund requested?"}}
camel.component.typesafe-ai.state=${body}
camel.component.typesafe-ai.result-property=evaluation
```

```java
from("direct:route")
    .to("typesafe-ai:refund")
    .choice()
        .when(simple("${exchangeProperty.evaluation[answers][refund][noul]} >= '0.8'"))
            .to("direct:refund-handler")
        .otherwise().to("direct:general-handler");
```

No manually registered beans are needed. `state` is a Simple expression, defaulting to `${body}`. For an `InputStream`, use `${bodyAs(String)}`. Only the selected state is sent. Without `resultProperty`, the response replaces the message body. Quote fractional thresholds in Simple predicates as shown, so Camel compares them as decimals instead of first coercing both operands to integers.

### Questions from a JSON resource

Use `questionsResource` when the question set is too large for a property value. It accepts a Camel resource URI, including `classpath:` and `file:`, and contains only the named questions. The component reads and validates the UTF-8 JSON once when the endpoint starts. The resource is limited to 4 MB. `questions` and `questionsResource` cannot be used together. An invalid or missing resource prevents the endpoint from starting.

```json
{
  "department": {
    "type": "choice",
    "instructions": "Which team should handle this request?",
    "criteria": {
      "billing": "Payments and refunds",
      "technical": "Bugs and outages",
      "sales": "Pricing and new accounts"
    }
  },
  "refund_requested": {
    "type": "noul",
    "instructions": "Does the customer explicitly request a refund?"
  }
}
```

Put this file at `src/main/resources/typesafe/triage-questions.json` and configure the endpoint and state through properties:

```properties
camel.component.typesafe-ai.questions-resource=classpath:typesafe/triage-questions.json
camel.component.typesafe-ai.state=${body}
camel.component.typesafe-ai.result-property=evaluation
```

```java
from("direct:triage")
    .to("typesafe-ai:triage")
    .choice()
        .when(simple("${exchangeProperty.evaluation[answers][department][choice]} == 'billing'"))
            .to("direct:billing")
        .otherwise().to("direct:other");
```

The resource shape is the `questions` object from the TypeSafe AI System One request; it has no outer `state`, `questions`, or `model` fields. The component validates the question types, criteria and JSON values at startup using the same rules as inline `questions`. For editor validation, use the Camel-maintained JSON Schema in `schema/typesafe-ai-questions.schema.json` from this component’s JAR.

## Producer request and response

Without configured `questions`, the input body must be a `Map<String, Object>` with `state` and a nonempty `questions` map. An optional `model` overrides the endpoint default. Each named question is a map with `type` (`noul`, `choice`, or `score`), optional `instructions`, and the applicable `criteria`. Instructions may be omitted or null. Noul criteria and either yes/no description may also be omitted or null, matching the official Python SDK and OpenAPI schema. State, instructions, and descriptions can be text or structured maps/lists. Nested content supports strings, finite numbers, booleans, nulls, lists, and maps with string keys. Convert other objects explicitly before submitting them. The component does not collect exchange headers or properties automatically. Do not send an entire exchange as state.

The output is an `org.apache.camel.util.json.JsonObject`, which implements `Map<String, Object>`. It preserves the API’s JSON structure, including additional fields. Nested objects are maps, arrays are lists, and numeric values implement `Number`; use `doubleValue()` or `longValue()` rather than assuming a specific numeric class.

Missing or mismatched answers, invalid numeric ranges, unknown choices, and incomplete probability maps fail the exchange. The selected Choice must have maximal probability; ties are allowed. Probabilities and scores are preserved as returned. Like the official Python SDK, the component does not enforce a probability-sum tolerance or recompute a Score from its returned probabilities, which may have been rounded independently.

Token counts may be missing or null. Missing values remain absent and null values remain null; neither is replaced with zero. Present counts must be nonnegative integers.

```java
Map<String, Object> request = Map.of(
    "state", "Please refund the duplicate payment",
    "questions", Map.of(
        "refund", Map.of("type", "noul", "instructions", "Is a refund requested?",
            "criteria", Map.of("true", "An explicit request for money back", "false", "No refund requested")),
        "team", Map.of("type", "choice", "instructions", "Which team should handle this?",
            "criteria", Map.of("billing", "Payments and refunds", "technical", "Product failures",
                "other", "Neither team applies")),
        "urgency", Map.of("type", "score", "instructions", "How urgent is this?",
            "criteria", List.of("Routine", "Urgent", "Critical"))));

JsonObject response = template.requestBody("typesafe-ai:decisions", request, JsonObject.class);
JsonObject answers = response.getJsonObject("answers");
boolean requested = answers.getJsonObject("refund").getDouble("noul") >= 0.8;
String category = answers.getJsonObject("team").getString("choice");
double score = answers.getJsonObject("urgency").getDouble("score");
```

This mixed batch makes one HTTP request, with the same state for every question. There is no implicit batching across producer calls or predicates.

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top">Answer</td><td class="tableblock halign-left valign-top">Mapping</td></tr><tr><td class="tableblock halign-left valign-top">Noul</td><td class="tableblock halign-left valign-top"><code>noul</code> is the probability of yes, in [0,1]. There is no separate confidence value.</td></tr><tr><td class="tableblock halign-left valign-top">Choice</td><td class="tableblock halign-left valign-top"><code>choice</code>, <code>probabilities</code> and <code>confidence</code>. Exactly one supplied category is selected. Criteria may contain up to 255 options; an option’s description may be null.</td></tr><tr><td class="tableblock halign-left valign-top">Score</td><td class="tableblock halign-left valign-top"><code>score</code> is a possibly fractional position in 1 to 10 ordered levels. <code>legend</code> and <code>probabilities</code> are maps keyed by string indices starting at <code>"0"</code>; legend descriptions may be strings, objects, or arrays. <code>confidence</code> describes uncertainty.</td></tr><tr><td class="tableblock halign-left valign-top">Response</td><td class="tableblock halign-left valign-top"><code>model</code>, <code>answers</code>, and <code>usage</code>. The <code>input_tokens</code> and <code>output_tokens</code> counts may be absent or null.</td></tr></tbody></table>

With `resultProperty=evaluation`, the producer stores the response in that exchange property and preserves the input body. It clears the property before each evaluation so failures cannot leave a stale result. The input request map is not mutated.

For category routing, submit one Choice question and route on its `choice` field. Independent Noul conditions instead preserve Camel Choice’s first-matching-branch semantics.

## Timeouts and errors

Producer and language evaluations are synchronous. Each evaluation blocks the calling thread for a remote round trip and may incur token charges. There is no response cache or automatic retry. Loops and Camel redelivery can evaluate again; bound them and account for repeated calls.

`requestTimeout` bounds the HTTP request and complete response body. Connection, request and overall deadline failures all surface as `java.util.concurrent.TimeoutException`; an underlying JDK HTTP timeout is retained as the cause. Interruption and timeout cancel the HTTP future, including stalled response bodies. Cancellation cannot guarantee the service stopped processing or consumed no tokens.

An unsuccessful HTTP status raises `TypeSafeAiHttpException` with status code, request ID and `Retry-After` where available. Error bodies are omitted because they may contain submitted state. Invalid responses and network failures propagate. Language evaluations preserve the exception in Camel’s cause chain, so ordinary `onException` clauses can handle it. Failures never silently become a non-match. Endpoint stop cancels in-flight calls and rejects new evaluations until restart.

Only submit data permitted for the configured service. Test model decisions and thresholds against your application; structured output does not establish correctness.