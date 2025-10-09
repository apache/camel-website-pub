# Spring

Apache Camel is designed to work first class with Spring in a number of ways, such as:

-   Camel runs on Spring Boot with the Camel Spring Boot project
    
-   Camel works with Spring XML files (classic Spring XML)
    
-   Camel works with Spring dependency injection
    
-   Camel works with Spring configuration and property placeholders
    
-   Camel works with Spring transactions
    
-   Camel works with Spring testing
    

## Using Camel on Spring Boot

See the Camel Spring Boot documentation.

## Using Camel with Spring XML files

Using Camel with Spring XML files, is a classic way, of using XML DSL with Camel. Camel has historically been using Spring XML for a long time. The Spring framework started with XML files as a popular and common configuration for building Spring applications.

To use Camel with Spring XML files see the [Spring XML](spring-xml-extensions.md) documentation.

## Using Spring dependency injection

Spring dependency injection is integrated first-class when using Camel and Spring together.

For example when using Camel on Spring Boot, then you can use any kind of Spring dependency and be able to inject Camel resources such as 'CamelContext', [Endpoint](endpoint.md) and many more.

## Using Camel with Spring configuration and property placeholders

See [Using Property Placeholder](using-propertyplaceholder.md) documentation.

## Using Camel with Spring transactions

See [Transactional Client](../components/4.18.x/eips/transactional-client.md) EIP.

## Using Camel with Spring testing

See [camel-test-spring-junit5](../components/4.18.x/others/test-spring-junit5.md) and [camel-test-spring-junit6](../components/4.18.x/others/test-spring-junit6.md) documentation.