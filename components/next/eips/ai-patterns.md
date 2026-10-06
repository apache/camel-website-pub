# AI Patterns

If you come from an AI, data engineering, or modern distributed systems background, you may know integration patterns by different names. This page maps common terms to the corresponding Camel EIPs.

See also the full [Enterprise Integration Patterns](enterprise-integration-patterns.md) index.

## Data Flow

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Pipeline / Chain | [Pipes and Filters](pipeline-eip.md) | Process a message through a sequence of steps. |
| Fan-out / Broadcast | [Multicast](multicast-eip.md) | Send the same message to multiple destinations in parallel. |
| Fan-in / Reduce / Join | [Aggregator](aggregate-eip.md) | Combine multiple related messages into a single message. |
| Scatter-Gather | [Scatter-Gather](scatter-gather.md) | Send a message to multiple recipients and aggregate their replies. |
| Map / Transform | [Transform](transform-eip.md), [Set Body](setBody-eip.md) | Transform or replace the message content. |
| Split / Chunk | [Splitter](split-eip.md) | Break a message into smaller pieces for individual processing. |
| Merge | [Aggregator](aggregate-eip.md) | Merge multiple messages into one using a correlation key and aggregation strategy. |
| Filter | [Message Filter](filter-eip.md) | Discard messages that do not match a predicate. |
| Router / Dispatch | [Content-Based Router](choice-eip.md), [Switch](switch-eip.md), [Dynamic Router](dynamicRouter-eip.md) | Route messages to different destinations based on content or rules. |

## Enrichment and Context

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Enrich / Hydrate / Augment | [Enrich](enrich-eip.md), [Poll Enrich](pollEnrich-eip.md) | Fetch additional data from an external source and merge it into the message. |
| Validate / Guard | [Validate](validate-eip.md) | Check that a message satisfies a condition before further processing. |
| Normalize | [Normalizer](normalizer.md) | Convert messages from different formats into a single canonical format. |
| Serialize / Deserialize | [Marshal](marshal-eip.md), [Unmarshal](unmarshal-eip.md) | Convert between objects and wire formats (JSON, XML, Avro, Protobuf, etc.). |

## Resilience and Error Handling

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Retry | [Error Handler](../../../manual/error-handler.md) | Automatically retry failed message processing with configurable backoff. |
| Circuit Breaker | [Circuit Breaker](circuitBreaker-eip.md) | Stop calling a failing service and provide a fallback response. |
| Fallback | [On Exception](../../../manual/exception-clause.md), [On Fallback](onFallback-eip.md) | Handle exceptions with onException (general), or define a Circuit Breaker fallback with onFallback. |
| Dead Letter / Poison Pill | [Dead Letter Channel](dead-letter-channel.md) | Move messages that cannot be processed to a separate channel for investigation. |
| Compensate / Rollback | [Saga](saga-eip.md), [Rollback](rollback-eip.md) | Undo or compensate for completed steps when a multi-step process fails. |

## Rate Control and Scheduling

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Rate Limit / Throttle | [Throttler](throttle-eip.md) | Limit the number of messages processed per time period. |
| Debounce / Delay | [Delayer](delay-eip.md) | Introduce a delay before processing a message. |
| Poll / Pull | [Polling Consumer](polling-consumer.md), [Poll](poll-eip.md) | Consume messages on demand rather than being pushed. |
| Loop / Iterate | [Loop](loop-eip.md) | Repeat processing a message a fixed number of times or until a condition is met. |
| Sample | [Sampling](sample-eip.md) | Pick one message out of many in a time period to reduce volume. |

## Load Distribution

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Load Balance | [Load Balancer](loadBalance-eip.md) | Distribute messages across multiple endpoints. |
| Round Robin | [Round Robin Load Balancer](roundRobinLoadBalancer-eip.md) | Distribute messages evenly in rotation. |
| Failover | [Failover Load Balancer](failoverLoadBalancer-eip.md) | Try the next endpoint when the current one fails. |
| Weighted | [Weighted Load Balancer](weightedLoadBalancer-eip.md) | Distribute messages according to weighted ratios. |
| Sticky / Affinity | [Sticky Load Balancer](stickyLoadBalancer-eip.md) | Route related messages to the same endpoint based on a correlation key. |

## Deduplication and Idempotency

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Dedup / Deduplicate | [Idempotent Consumer](idempotentConsumer-eip.md) | Detect and discard duplicate messages based on a unique identifier. |
| Claim Check / Stash | [Claim Check](claimCheck-eip.md) | Temporarily store message data and retrieve it later to reduce payload size. |

## Connectivity

  
| Term | Camel EIP | Description |
| --- | --- | --- |
| Source / Ingress | [From](from-eip.md) | Define the input endpoint that feeds messages into a route. |
| Sink / Egress | [To](to-eip.md), [To D](toD-eip.md) | Send messages to a fixed or dynamically computed endpoint. |
| Connector / Adapter | [Channel Adapter](channel-adapter.md) | Connect an application to a messaging system. |
| Webhook / Event-Driven | [Event Driven Consumer](eventDrivenConsumer-eip.md) | React to messages as they arrive without polling. |
| Gateway | [Messaging Gateway](messaging-gateway.md) | Encapsulate access to the messaging system behind a clean interface. |
| Wire Tap / Tap / Observe | [Wire Tap](wireTap-eip.md) | Send a copy of the message to a secondary destination for monitoring. |

## AI and Agent Integration

  
| Term | Camel Component / EIP | Description |
| --- | --- | --- |
| Classify / Intent routing | [Semantic](../languages/semantic-language.md), [Switch](switch-eip.md) | Evaluate a Semantic choice question once and dispatch its category string through literal Switch cases. |
| Guardrail / Guard decision | [Semantic](../languages/semantic-language.md), [TypeSafe AI](../typesafe-ai-component.md), [Filter](filter-eip.md), [Validate](validate-eip.md) | Ask a yes/no question about the message (is this request actionable, does this action fit the task) and filter or validate on the answer. A System One model such as Jev answers with a fast, structured decision instead of generated text. |
| Tool / Function calling | [AI Tool](../ai-tool-component.md) | Expose a route as a tool an AI agent can call. The same route works with the LangChain4j, Spring AI and OpenAI agents. |
| MCP server | [MCP Server](../others/mcp-server.md), [AI Resource](../ai-resource-component.md) | Expose `ai-tool` routes as MCP tools and `ai-resource` routes as MCP resources to any MCP client. |
| MCP client | [LangChain4j Agent MCP](../others/langchain4j-agent-mcp.md), [OpenAI MCP](../others/openai-mcp.md) | Let an agent in a route call the tools of remote MCP servers. |
| Tool authorization / Agent permissions | [AI Tool authorization](../ai-tool-component.html#_authorizing_tool_calls), [OPA](../opa-component.md), [OpenFGA](../openfga-component.md) | Authorize every tool call before it runs, on the caller identity and the tool name, never on model output. |
| Agent identity / Workload identity | [SPIFFE](../spiffe-component.md) | Give each workload a cryptographic identity and mutual TLS, so a tool call can be authorized on who is calling. |
| LLM observability | [AI Observability](../others/ai-observability.md) | Record an OpenTelemetry span and Micrometer metrics (model, tokens, duration) for each call of the LangChain4j, OpenAI and Spring AI chat producers, inside the route’s trace. |
| RAG ingestion | [LangChain4j Ingest](../langchain4j-ingest-component.md) | Split, embed and store documents in an embedding store for retrieval-augmented generation. |
| Agent-to-Agent / A2A | [A2A](../a2a-component.md) | Google’s Agent-to-Agent protocol for communication between AI agents. |
| Tokenize / Chunk (for LLM) | [LangChain4j Tokenizer](../others/langchain4j-tokenizer.md) | Split text into tokens or chunks sized for LLM context windows, using LangChain4j tokenizer strategies. |