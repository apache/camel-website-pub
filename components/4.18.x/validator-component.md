# Validator

**Since Camel 1.1**

**Only producer is supported**

The Validation component performs XML validation of the message body using the JAXP Validation API and based on any of the supported XML schema languages, which defaults to [XML Schema](http://www.w3.org/XML/Schema).

## URI format

validator:someLocalOrRemoteResource

Where **someLocalOrRemoteResource** is some URL to a local resource on the classpath or a full URL to a remote resource or resource on the file system which contains the XSD to validate against. For example:

-   `validator:com/mypackage/myschema.xsd`
    

The Validation component is provided directly in the camel-core.

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

The Validator component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **resourceResolverFactory** (advanced) | To use a custom LSResourceResolver which depends on a dynamic endpoint resource URI. |  | ValidatorResourceResolverFactory |

## Endpoint Options

The Validator endpoint is configured using URI syntax:

validator:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** URL to a local resource on the classpath, or a reference to lookup a bean in the Registry, or a full URL to a remote resource or resource on the file system which contains the XSD to validate against. |  | String |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **failOnNullBody** (producer) | Whether to fail if no body exists. | true | boolean |
| **failOnNullHeader** (producer) | Whether to fail if no header exists when validating against a header. | true | boolean |
| **headerName** (producer) | To validate against a header instead of the message body. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **errorHandler** (advanced) | To use a custom org.apache.camel.processor.validation.ValidatorErrorHandler. The default error handler captures the errors and throws an exception. |  | ValidatorErrorHandler |
| **resourceResolver** (advanced) | To use a custom LSResourceResolver. Do not use together with resourceResolverFactory. |  | LSResourceResolver |
| **resourceResolverFactory** (advanced) | To use a custom LSResourceResolver which depends on a dynamic endpoint resource URI. The default resource resolver factory returns a resource resolver which can read files from the class path and file system. Do not use together with resourceResolver. |  | ValidatorResourceResolverFactory |
| **schemaFactory** (advanced) | To use a custom javax.xml.validation.SchemaFactory. |  | SchemaFactory |
| **schemaLanguage** (advanced) | Configures the W3C XML Schema Namespace URI. | [http://www.w3.org/2001/XMLSchema](http://www.w3.org/2001/XMLSchema) | String |
| **useSharedSchema** (advanced) | Whether the Schema instance should be shared or not. This option is introduced to work around a JDK 1.6.x bug. Xerces should not have this issue. | true | boolean |

## Example

The following [example](https://github.com/apache/camel/blob/main/components/camel-spring-xml/src/test/resources/org/apache/camel/component/validator/camelContext.xml) shows how to configure a route from endpoint **direct:start** which then goes to one of two endpoints, either **mock:valid** or **mock:invalid** based on whether the XML matches the given schema (which is supplied on the classpath).

## Advanced: JMX method `clearCachedSchema`

You can force that the cached schema in the validator endpoint is cleared and reread with the next process call with the JMX operation `clearCachedSchema`. You can also use this method to programmatically clear the cache. This method is available on the `ValidatorEndpoint` class.

## Spring Boot Auto-Configuration

When using validator with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-validator-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.validator.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.validator.enabled** | Whether to enable auto configuration of the validator component. This is enabled by default. |  | Boolean |
| **camel.component.validator.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.validator.resource-resolver-factory** | To use a custom LSResourceResolver which depends on a dynamic endpoint resource URI. The option is a org.apache.camel.component.validator.ValidatorResourceResolverFactory type. |  | ValidatorResourceResolverFactory |