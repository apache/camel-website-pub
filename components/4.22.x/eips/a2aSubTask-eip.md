# A2A Sub Task

The A2A Sub Task EIP groups route steps and emits [A2A protocol](https://a2a-protocol.org/latest/specification/) progress events before, after, or when the grouped work fails.

This is useful for [A2A](../a2a-component.md) consumer routes where you want to report scoped progress updates to the calling agent as the route processes different stages of work.

The `emitBefore`, `emitAfter`, and `emitOnError` fields are optional and are evaluated as [Simple](../languages/simple-language.md) expressions against the current Exchange.

## EIP options

The A2A Sub Task eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **emitBefore** | Simple expression template to emit before the nested steps run. |  | String |
| **emitAfter** | Simple expression template to emit after the nested steps complete successfully. |  | String |
| **emitOnError** | Simple expression template to emit when the nested steps fail. |  | String |
| **failIfNoTaskContext** | Whether to fail if the current Exchange does not have an active A2A task context. | false | Boolean |
| **outputs** | **Required** |  | List |

## Example

In this example, the route groups two stages of work and emits progress events for each:

-   YAML
    
-   Java
    

```yaml
- route:
    from:
      uri: a2a:classpath:agent-card.json
      steps:
        - a2aSubTask:
            id: search-docs-progress
            emitBefore: "Searching docs..."
            emitAfter: "Docs found: ${body.size()}"
            emitOnError: "Error searching docs: ${exception.message}"
            steps:
              - to:
                  uri: "elasticsearch:docs?operation=Search"
        - a2aSubTask:
            id: draft-answer-progress
            emitBefore: "Drafting answer..."
            emitAfter: "Answer drafted: ${body}"
            emitOnError: "Error drafting answer: ${exception.message}"
            steps:
              - bean:
                  ref: answerDraftingService
                  method: draft
        - setBody:
            simple: "Final answer: ${body}"
```

```java
from("a2a:classpath:agent-card.json")
    .a2aSubTask()
        .id("search-docs-progress")
        .emitBefore("Searching docs...")
        .emitAfter("Docs found: ${body.size()}")
        .emitOnError("Error searching docs: ${exception.message}")
        .to("elasticsearch:docs?operation=Search")
    .end()
    .a2aSubTask()
        .id("draft-answer-progress")
        .emitBefore("Drafting answer...")
        .emitAfter("Answer drafted: ${body}")
        .emitOnError("Error drafting answer: ${exception.message}")
        .bean(answerDraftingService, "draft")
    .end()
    .setBody(simple("Final answer: ${body}"));
```

## Behavior

-   The nested `steps` behave like normal Camel route steps.
    
-   If the nested steps fail, `emitOnError` can access the original exception via `${exception.message}`, and the original exception continues to propagate through the route.
    
-   Failures while evaluating the `emitBefore`, `emitAfter`, or `emitOnError` expressions are route failures.
    
-   Failures while storing or notifying the resulting A2A progress event are best-effort: they are logged at debug level and do not stop nested work, fail an otherwise successful exchange, or replace the original nested-step exception.
    
-   By default, emitting progress outside an active A2A task context is a no-op. Set `failIfNoTaskContext=true` when a route should fail if the current Exchange does not carry an active A2A task.
    
-   Use stable `id` values on long-lived sub-tasks so route tracing and route-structure views keep stable node names.
    

## See Also

-   [A2A Component](../a2a-component.md)
    
-   [A2A Consumer Guide](../others/a2a-consumer.md)