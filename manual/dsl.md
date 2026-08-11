# DSL

Camel uses a Java _Domain Specific Language_ or DSL for creating [Enterprise Integration Patterns](../components/4.22.x/eips/enterprise-integration-patterns.md) or [Routes](routes.md) in a variety of domain-specific languages (DSL) as listed below:

-   [Java DSL](java-dsl.md): a Java-based DSL using the fluent builder style.
    
-   [XML DSL](../components/4.22.x/others/java-xml-io-dsl.md): an XML-based DSL in Camel XML files only.
    
-   [Spring XML](../components/4.22.x/spring-summary.md): an XML-based DSL in classic Spring XML files.
    
-   [YAML DSL](../components/4.22.x/others/yaml-dsl.md): for creating routes using YAML format.
    
-   [Rest DSL](rest-dsl.md): a DSL to define REST services using REST verbs.
    
    -   [Rest DSL contract first](rest-dsl-openapi.md): rest DSL using _contract-first_ when OpenAPI specs.
        
    
-   [Annotation DSL](bean-integration.md): Use annotations in Java beans.
    

## See Also

-   [CamelContext](camelcontext.md) the main entry for Camel is the `CamelContext`
    
-   [Routes](routes.md) for general information about a Camel route
    
-   [RouteBuilder](route-builder.md) for creating routes using the Java DSL style.
    
-   [LambdaRouteBuilder](lambda-route-builder.md) for creating routes using Java lambda style.
    
-   [Endpoint DSL](Endpoint-dsl.md) for creating routes using type-safe Camel endpoints in Java.
    
-   [DataFormat DSL](dataformat-dsl.md) for type-safe Camel data formats in Java.
    
-   [Route Template](route-template.md) for creating reusable route templates.
    
-   [Route Diagram](route-diagram.md) for generating visual route diagrams for documentation purposes.
    
-   [Route Reload](route-reload.md) for hot-reloading routes in a running Camel application.