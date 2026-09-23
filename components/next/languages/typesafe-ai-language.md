# TypeSafe AI

**Since Camel 4.23**

The TypeSafe AI language evaluates a plain-text question against selected exchange state using the [TypeSafe AI component](../typesafe-ai-component.md). It returns a Boolean from the Noul probability and a configured threshold. Each evaluation makes a synchronous remote request, may incur token charges, and preserves the message body. Use the component producer for structured questions, Choice classification, Score rubrics, or batching multiple questions in one request.

## Configuration

```properties
camel.component.typesafe-ai.api-key={{env:TYPESAFE_API_KEY}}
camel.component.typesafe-ai.model=jev-1.13.0
camel.language.typesafe-ai.endpoint=typesafe-ai:refund
camel.language.typesafe-ai.threshold=0.8
camel.language.typesafe-ai.state=${body}
```

With Camel Main, all settings are configurable from properties; no predicate beans are needed. The expression text is only the question, never an endpoint URI or configuration. Credentials and transport settings belong to the component or selected endpoint.

  
| Language property | Default | Meaning |
| --- | --- | --- |
| `endpoint` | `typesafe-ai:default` | URI of the managed TypeSafe AI endpoint. |
| `threshold` | Endpoint `threshold` (`0.5`) | Probability at or above this value matches outside the uncertainty band. |
| `uncertainty` | Endpoint `uncertainty` (`0`) | Half-width of the inclusive band around the threshold; zero disables it. |
| `uncertainty-policy` | Endpoint `uncertaintyPolicy` (`NonMatch`) | `NonMatch` returns false within the band; `Fail` raises `TypeSafeAiUncertainResultException`. |
| `state` | Endpoint `state` (`${body}`) | Simple expression selecting the state to send. For streams, use `${bodyAs(String)}`. |

Prefix these properties with `camel.language.typesafe-ai.`. Unset language properties fall back to the selected endpoint’s configuration, which inherits `camel.component.typesafe-ai.*` defaults. Threshold and both uncertainty-band boundaries must lie in \[0,1\]. For example, threshold `0.5` and uncertainty `0.125` make \[0.375, 0.625\] uncertain, including both boundaries.

The catalog entry describes the generic expression model. Spring Boot’s starter generator currently derives language configuration from those model options, so it needs separate support for TypeSafe AI’s `camel.language.typesafe-ai.*` settings. For property configuration through the default `typesafe-ai:default` endpoint, use `camel.component.typesafe-ai.threshold`, `camel.component.typesafe-ai.uncertainty`, `camel.component.typesafe-ai.uncertainty-policy`, and `camel.component.typesafe-ai.state`, alongside the component credentials and transport settings.

## Java, XML and YAML

Use Camel’s generic language expression. The same condition works in Filter, Choice, Validate and other EIPs accepting a predicate. A non-match retains that EIP’s normal behavior.

```java
from("direct:filter")
    .filter().language("typesafe-ai", "Does this message request a refund?")
    .to("direct:refund-handler");

from("direct:route").choice()
    .when().language("typesafe-ai", "Does this message request a refund?")
        .to("direct:refund-handler")
    .otherwise().to("direct:general-handler");
```

```xml
<filter>
  <language language="typesafe-ai">Does this message request a refund?</language>
  <to uri="direct:refund-handler"/>
</filter>
```

```yaml
- from:
    uri: direct:filter
    steps:
      - filter:
          expression:
            language:
              language: typesafe-ai
              expression: "Does this message request a refund?"
          steps:
            - to: direct:refund-handler
```

XML and YAML use the configured language defaults. Java callers needing per-use settings can use the Language SPI. The optional array positions are endpoint, threshold, uncertainty, uncertainty policy, and state. Null entries inherit the language settings; state can be a Simple string or a thread-safe Camel `Expression`.

```java
Predicate refund = context.resolveLanguage("typesafe-ai").createPredicate(
    "Does this message request a refund?",
    new Object[] { "typesafe-ai:refund", 0.8, 0.05, "Fail", "${header.customerText}" });

from("direct:filter").filter(refund).to("direct:refund-handler");
```

Per-use settings take precedence over language properties and endpoint defaults. Camel initializes route predicates and manages their endpoints. Programmatic callers should call `init(context)` before evaluation. Evaluation does not restart a stopped endpoint.

## Results and failures

Each invocation selects fresh state and replaces `CamelTypeSafeAiResult` with the full response `JsonObject`. It clears the property before evaluation, preventing stale results after a failure. An uncertain result remains available when `TypeSafeAiUncertainResultException` is raised. HTTP, timeout and invalid-response failures propagate through Camel’s normal exception handling. They are distinct from a valid non-match. Repeated conditions, loops and redelivery can each make another request; bound them and account for latency and cost.

The TypeSafe AI language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **language** (common) |  | `String` | **Required** The name of the language to use. |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |
| **resolveResource** (advanced) | `false` | `Boolean` | Whether a result of the expression that is a String starting with resource: is loaded as a resource and its content becomes the result, e.g. a script that returns resource:file:order.json or resource:classpath:templates/order.json (a name without a scheme is a classpath resource). Off by default; the resource: prefix on the expression text itself is always resolved. Applies to the expression used as a value, not as a predicate. |