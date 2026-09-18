# Working with Camel Core

## Context

The [Camel Context](../../manual/camelcontext.md) is the heart of Apache Camel, which holds everything together.

If you are not familiar with Apache Camel, then we recommend reading the [Camel Context](../../manual/camelcontext.md) first before coming back here.

## Routes

In Apache Camel, a _route_ is a set of processing steps that are applied to a message as it travels from a source to a destination. A route typically consists of a series of processing steps that are connected in a linear sequence.

In other words, a Camel _route_ is where the integration flow is defined. For example, you can write a Camel route to specify how two systems can be integrated. The following guide provides the fundamental knowledge of Camel routes:

-   [Routes](../../manual/routes.md): the basic guide about Camel Routes.
    

If you have basic knowledge about _routes_, you can use the following guides to learn how to write them in different languages, handle errors, and customize them.

-   Content
    
    -   [Camel Context](../../manual/camelcontext.md): the heart of Apache Camel
        
    
-   Routes (Basic + DSL)
    
    -   [Java DSL](../../manual/java-dsl.md): the default language to write _routes_.
        
    -   [DSL overview](../../manual/dsl.md): writing routes in other languages (XML, YAML, etc).
        
    -   [URIs](../../manual/uris.md)
        
    
-   Routes (Writing)
    
    -   [Expression](../../manual/expression.md)
        
    -   [Predicate](../../manual/predicate.md)
        
    
-   Routes (Error Handling)
    
    -   [Default Error Handler](../../manual/defaulterrorhandler.md)
        
    -   [Error Handler](../../manual/error-handler.md)
        
    -   [Exception Clause](../../manual/exception-clause.md)
        
    -   [Try, Catch and Finally](../../manual/try-catch-finally.md)
        
    
-   Routes (Others)
    
    -   [On Completion](../../manual/oncompletion.md)
        
    -   [Endpoint DSL](../../manual/Endpoint-dsl.md)
        
    -   [Route Template](../../manual/route-template.md)
        
    -   [Visual Route Diagrams](../../manual/route-diagram.md)
        
    -   [Using Property Placeholder](../../manual/using-propertyplaceholder.md)
        
    -   [Using Variables](../../manual/variables.md)
        
    
-   Routes (Rest DSL)
    
    -   [Rest DSL](../../manual/rest-dsl.md)
        
    -   [Rest DSL contract first with OpenAPI](../../manual/rest-dsl-openapi.md)
        
    

## Components

Components are a fundamental building block of Apache Camel and are used to connect routes to a wide variety of external systems and services.

-   [Component](../../manual/component.md): the comprehensive guide about components.
    

## Data Processing and Transformation

As you progress with creating your routes, you will often need to manipulate the data in transit so that you can collect, transform, or store it for future use. Apache Camel comes with many features to help you transform data in transit. The following guides can help you discover ways to manipulate the data:

-   Data Processing
    
    -   [Bean Integration](../../manual/bean-integration.md)
        
    -   [Processor](../../manual/processor.md)
        
    
-   Data Transformation
    
    -   [Data Format](../../manual/data-format.md)
        
    

## Exchanges

The exchange is a core concept of Apache Camel and is used to abstract different patterns of communication within Camel. Read the following guides to have a better understanding of it:

-   Exchange
    
    -   [Exchange](../../manual/exchange.md)
        
    

## Other Guides

Learn about additional ways to customize your integrations. Explore alternatives to consume and produce data as well as writing and defining routes.

-   Context
    
    -   [Camel Context Auto Configuration](../../manual/camelcontext-autoconfigure.md)
        
    -   [Advanced Configuration of Camel Context](../../manual/advanced-configuration-of-camelcontext-using-spring.md)
        
    
-   Running Camel Applications and Other Runtime Guides
    
    -   [Camel Lifecycle](../../manual/lifecycle.md)
        
    -   [Camel Console](../../manual/camel-console.md)
        
    -   [Camel Maven Plugin](../../manual/camel-maven-plugin.md)
        
    -   [Camel Report Maven Plugin](../../manual/camel-report-maven-plugin.md)
        
    -   [Security](../../manual/security.md)
        
    
-   Other
    
    -   [Language DSL](../../manual/language-dsl.md)
        
    -   [Camel Maven Archetypes](../../manual/camel-maven-archetypes.md)
        
    -   [Stream caching](../../manual/stream-caching.md)
        
    -   [Advice With](../../manual/advice-with.md)
        
    -   [POJO Consuming](../../manual/pojo-consuming.md)
        
    -   [POJO Producing](../../manual/pojo-producing.md)
        
    -   [Delayer](../../manual/delay-interceptor.md)
        
    -   [Configuring Route Startup Ordering](../../manual/configuring-route-startup-ordering-and-autostartup.md)
        
    -   [Endpoint](../../manual/endpoint.md)
        
    -   [Examples](../../manual/examples.md)
        
    -   [JSON Data Format](../../manual/json.md)
        
    -   [Languages](../../manual/languages.md)
        
    -   [Parameter-Binding Annotations](../../manual/parameter-binding-annotations.md)
        
    -   [Property Binding](../../manual/property-binding.md)
        
    -   [Registry](../../manual/registry.md)
        
    -   [Route Configuration](../../manual/route-configuration.md)
        
    -   [Spring](../../manual/spring.md)
        
    -   [Spring XML Extensions](../../manual/spring-xml-extensions.md)
        
    -   [Validator](../../manual/validator.md)
        
    -   [Camel Requirements](../../manual/what-are-the-dependencies.md)
        
    -   [Testing](../../manual/testing.md)
        
    

You can find additional documentation in the [architecture documentation](../../manual/architecture.md) in the user manual.