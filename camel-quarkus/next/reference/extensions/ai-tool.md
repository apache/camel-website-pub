# AI Tool

JVM since3.39.0 Native since3.39.0

Framework-agnostic consumer endpoint that registers a Camel route as an LLM tool in the shared AiToolRegistry.

## What’s inside

-   [AI Tool component](../../../../components/next/ai-tool-component.md), URI syntax: `ai-tool:toolName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ai-tool)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ai-tool</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The `ai-tool` component is a framework-agnostic consumer endpoint that registers Camel routes as LLM-callable tools in a shared `AiToolRegistry`. Framework-specific extensions (such as `camel-quarkus-langchain4j-tools`, `camel-quarkus-openai`) discover and invoke these tools at runtime.

### Defining a tool

Use the `ai-tool` consumer endpoint to register a route as an AI tool. Tool parameters are declared via URI options.

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("ai-tool:getWeather?tags=weather"
                + "&description=Get the current weather for a city"
                + "&parameter.city=string"
                + "&parameter.city.description=The city name"
                + "&parameter.city.required=true"
                + "&parameter.unit=string"
                + "&parameter.unit.enum=celsius,fahrenheit")
            .setBody(simple("Sunny in ${header.city}, temperature in ${header.unit}"));
    }
}
```

Arguments passed by the LLM are set as exchange headers (e.g. `${header.city}`).

### Tag-based grouping

Tools can be grouped by tags. AI producer endpoints use tags to discover a subset of available tools.

A tool with no tags is placed in a default pool and is available to all tag queries.

```java
// Tagged tool — only visible to producers querying the "support" tag
from("ai-tool:lookupOrder?tags=support&description=Look up order status"
        + "&parameter.orderId=string&parameter.orderId.required=true")
    .to("sql:SELECT status FROM orders WHERE id = :#${header.orderId}");

// Untagged tool — available to all producers
from("ai-tool:greet?description=Greet a user"
        + "&parameter.name=string&parameter.name.required=true")
    .setBody(simple("Hello, ${header.name}!"));
```