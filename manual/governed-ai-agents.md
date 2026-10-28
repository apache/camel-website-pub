# Governed AI Agents

An AI agent decides which tools to call, and a tool can do real work: issue a refund, read a customer record, delete a file. The model is not a security boundary. A prompt injection, a confused model or a wrong caller can all ask for the wrong tool call.

So the decision about what an agent may do sits below the model, on the tool call itself. In Camel a tool is a route, and the route that does the work also checks:

 
| Question | Building block |
| --- | --- |
| Who is calling? | [SPIFFE](../components/next/spiffe-component.md) workload identity and mutual TLS |
| May they do this? | An `authorizationPolicy` on every [AI Tool](../components/4.22.x/ai-tool-component.md) call, with [Open Policy Agent](../components/next/opa-component.md) or [OpenFGA](../components/next/openfga-component.md) |
| Does this action make sense? | A fast guard decision with the [Semantic](../components/next/languages/semantic-language.md) language and a System One model |
| What happened? | [AI Observability](../components/next/others/ai-observability.md): OpenTelemetry spans and Micrometer metrics for every LLM call |

All of it runs in-process, in the Camel application, with no extra gateway. The components are Preview, so details may still change.

## Tools are routes

A tool is a Camel route that starts with `ai-tool:`. The same route works with the LangChain4j, Spring AI and OpenAI agents, and the built-in [MCP Server](../components/4.22.x/others/mcp-server.md) exposes it to any MCP client:

-   Java
    
-   XML
    
-   YAML
    

```java
from("ai-tool:refundOrder?tags=support&description=Refund a customer order by its id"
     + "&parameter.orderId=string&parameter.amount=integer")
    .to("bean:refundLedger");
```

```xml
<route>
    <from uri="ai-tool:refundOrder?tags=support&amp;description=Refund a customer order by its id&amp;parameter.orderId=string&amp;parameter.amount=integer"/>
    <to uri="bean:refundLedger"/>
</route>
```

```yaml
- route:
    from:
      uri: ai-tool:refundOrder
      parameters:
        tags: support
        description: "Refund a customer order by its id"
        parameter.orderId: string
        parameter.amount: integer
      steps:
        - to:
            uri: bean:refundLedger
```

Because the tool is a route, everything Camel has for routes applies to tool calls: error handling, retries, circuit breakers, tracing, and the checks below.

## Who is calling: SPIFFE

[SPIFFE](https://spiffe.io/) gives every workload a cryptographic identity, issued and rotated by the local SPIRE agent, with no passwords or API keys to manage.

The [SPIFFE](../components/next/spiffe-component.md) component validates a caller’s JWT-SVID on an incoming request, fetches one for outbound calls, and backs `SSLContextParameters` with rotating mutual TLS for every component that already supports TLS:

-   Java
    
-   XML
    
-   YAML
    

```java
from("platform-http:/api")
    .to("spiffe:auth?operation=validateJwtSvid&audience=spiffe://example.org/api")
    // keep the verified caller as an exchange property
    .setProperty("subject", header(SpiffeConstants.SPIFFE_ID))
    // the token is a credential; drop it before the exchange goes further
    .removeHeaders("Authorization")
    .to("direct:handleRequest");
```

```xml
<route>
    <from uri="platform-http:/api"/>
    <to uri="spiffe:auth?operation=validateJwtSvid&amp;audience=spiffe://example.org/api"/>
    <!-- keep the verified caller as an exchange property -->
    <setProperty name="subject">
        <header>CamelSpiffeSpiffeId</header>
    </setProperty>
    <!-- the token is a credential; drop it before the exchange goes further -->
    <removeHeaders pattern="Authorization"/>
    <to uri="direct:handleRequest"/>
</route>
```

```yaml
- route:
    from:
      uri: platform-http:/api
      steps:
        - to:
            uri: "spiffe:auth?operation=validateJwtSvid&audience=spiffe://example.org/api"
        # keep the verified caller as an exchange property
        - setProperty:
            name: subject
            expression:
              header:
                expression: CamelSpiffeSpiffeId
        # the token is a credential; drop it before the exchange goes further
        - removeHeaders:
            pattern: Authorization
        - to:
            uri: direct:handleRequest
```

Keep the verified identity in an exchange property, not a header. Headers are part of the message, and on a tool route they carry the arguments the model filled in; a property is out of reach of both the sender and the model.

## May they do this: authorize every tool call

Set an `authorizationPolicy` on the `ai-tool` component and every tool route is guarded by construction. Set it on one endpoint to override:

-   Java
    
-   XML
    
-   YAML
    

```java
// one policy guarding every ai-tool route
AiToolComponent ai = context.getComponent("ai-tool", AiToolComponent.class);
ai.getConfiguration().setAuthorizationPolicy(myAuthorizationPolicy);

// ...or override on a single endpoint
from("ai-tool:transferFunds?tags=banking&description=Transfer funds&authorizationPolicy=#myAuthorizationPolicy")
    .to("bean:ledger");
```

```xml
<route>
    <from uri="ai-tool:transferFunds?tags=banking&amp;description=Transfer funds&amp;authorizationPolicy=#myAuthorizationPolicy"/>
    <to uri="bean:ledger"/>
</route>
```

```yaml
- route:
    from:
      uri: ai-tool:transferFunds
      parameters:
        tags: banking
        description: "Transfer funds"
        authorizationPolicy: "#myAuthorizationPolicy"
      steps:
        - to:
            uri: bean:ledger
```

The check runs before the route does any work. A denied call never runs the tool; the model receives a short refusal it can relay to the user, not a stack trace.

The policy can be:

-   [Open Policy Agent](../components/next/opa-component.md): rules in Rego, versioned and tested apart from the route. Evaluate a WebAssembly bundle in-process, so a tool call costs no network hop.
    
-   [OpenFGA](../components/next/openfga-component.md): relationship-based authorization ("may this user refund this order?"). It fails closed.
    
-   The policies Camel already has: SPIFFE, [Keycloak](../components/4.22.x/keycloak-component.md), [Shiro](../components/4.22.x/others/shiro.md) or [Spring Security](../components/4.22.x/others/spring-security.md).
    

Two rules make the decision trustworthy:

1.  **The tool name comes from the route**, never from model output.
    
2.  **The caller comes from an exchange property** set before the agent ran, for example by `camel-spiffe` or `camel-keycloak`. Never authorize on message headers: on a tool route they carry the arguments the model filled in.
    

See [AI Tool](../components/4.22.x/ai-tool-component.md) for which agent runtimes carry the caller identity onto the tool call, including over MCP.

## Does this action make sense: System One guard decisions

Authorization answers "may this caller use this tool". Some questions are about meaning instead: is this request actionable, which team should handle it, does this answer stay on topic.

A [System One model](https://typesafe.ai/blog/introducing-system-one-models-and-jev), such as Jev from [TypeSafe AI](../components/next/typesafe-ai-component.md), is built for exactly that: fast, structured decisions instead of generated text. Give it the state and a question, and it returns a yes/no, one category or a score.

The [Semantic](../components/next/languages/semantic-language.md) language declares the evaluations once, by name, and uses them anywhere Camel accepts a predicate or an expression. Each evaluation names its expert, a registry bean; here `decisions` is the TypeSafe AI adapter (`camel.beans.decisions=#class:org.apache.camel.component.typesafeai.TypeSafeAiSemanticAdapter`):

-   Java
    
-   YAML
    

```java
semanticEvaluations(this)
    .evaluation("actionable").expert("decisions")
        .type("boolean")
        .instructions("Does this message contain an actionable request?")
        .threshold(0.8)
        .uncertainty(0.1)
        .uncertaintyPolicy("fail")
    .end().evaluation("department").expert("decisions")
        .type("choice")
        .instructions("Which department should handle this message?")
        .criterion("billing", "Invoices, payments and refunds")
        .criterion("technical", "Bugs, outages and technical problems")
    .register();

from("direct:tickets")
    .filter().language("semantic", "ref:actionable")
        .setProperty("department").language("semantic", "ref:department")
        .to("direct:dispatch");
```

```yaml
- semantic:
    evaluation:
      actionable:
        expert: decisions
        type: boolean
        instructions: Does this message contain an actionable request?
        threshold: 0.8
        uncertainty: 0.1
        uncertaintyPolicy: fail
      department:
        expert: decisions
        type: choice
        instructions: Which department should handle this message?
        criteria:
          billing: Invoices, payments and refunds
          technical: Bugs, outages and technical problems

- route:
    from:
      uri: direct:tickets
      steps:
        - filter:
            expression:
              language:
                language: semantic
                expression: ref:actionable
            steps:
              - setProperty:
                  name: department
                  expression:
                    language:
                      language: semantic
                      expression: ref:department
              - to:
                  uri: direct:dispatch
```

The decision is a plain value, so what happens next is ordinary Camel: `filter`, `choice`, `switch`, `validate`, a dead letter channel or a human review queue. A guard decision is not authorization: it complements the policy above and never replaces it.

## What happened: GenAI observability

Add `camel-ai-observability` next to `camel-opentelemetry2` or `camel-micrometer`, and every LLM call from `langchain4j-chat`, `langchain4j-agent`, `langchain4j-embeddings`, `openai` and `spring-ai-chat` emits a child span and metrics, following the OpenTelemetry GenAI semantic conventions: operation, model, input and output tokens, duration.

The LLM spans sit inside the route’s own trace, so one trace shows the request, the agent, each tool call and each model call, in the observability stack you already run.

## In the route, or at the perimeter

Everything above runs inside the Camel application that does the work. That is the right place for decisions that depend on the business data: this customer, this order, this amount.

When many applications and teams expose tools to many agents, and you want one place where every agent call is governed, add a governed proxy in front. [Wanaku](https://wanaku.ai/) publishes Camel `ai-tool` routes through its [Integration Capability for Apache Camel](https://github.com/wanaku-ai/camel-integration-capability). The two work together: the proxy governs at the perimeter, and the route still checks the call it is about to run.

## Try it

-   [ai-tools-spiffe-opa example](https://github.com/apache/camel-examples/tree/main/ai-tools-spiffe-opa): a support assistant with three tools, two callers with SPIFFE identities and an OPA WebAssembly policy, all with Docker Compose.
    
-   [Authorizing what an AI agent may do in Apache Camel](/blog/2026/09/securing-ai-agent-tools/)
    
-   [Workload identity in Apache Camel with SPIFFE and SPIRE](/blog/2026/09/camel-spiffe-workload-identity/)
    
-   [TypeSafe Jev meets Apache Camel: semantic decisions in Camel routes](/blog/2026/09/semantic-evaluation-system-one/)
    
-   [One request, several agents: semantic routing with Apache Camel and Jev](/blog/2026/10/semantic-agent-routing/)
    
-   [Observe your Camel AI routes with GenAI OpenTelemetry](/blog/2026/09/camel-genai-observability-jbang/)
    

See also [Security Model](security-model.md) for where Camel draws its trust boundaries.