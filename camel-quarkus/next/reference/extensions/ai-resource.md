# AI Resource

JVM since4.0.0 Native since4.0.0

Framework-agnostic consumer endpoint that registers a Camel route as a read-only AI resource in the shared AiResourceRegistry.

## What’s inside

-   [AI Resource component](../../../../components/next/ai-resource-component.md), URI syntax: `ai-resource:resourceName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ai-resource)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ai-resource</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The `ai-resource` component registers Camel routes as read-only resources in a shared `AiResourceRegistry`. To serve the tagged routes as MCP resources, add the `camel-quarkus-mcp-server` extension, see [MCP Server resources](mcp-server.html#extensions-mcp-server-usage-resources).