# Bean

**Since Camel 1.0**

**Only producer is supported**

The Bean component binds beans to Camel message exchanges.

## URI format

bean:beanName\[?options\]

Where `beanName` can be any string used to look up the bean in the Registry

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

The Bean component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **scope** (producer) | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using delegate scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. so when using prototype then this depends on the delegated registry.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 | Singleton | BeanScope |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **beanInfoCacheSize** (advanced) | Maximum cache size of internal cache for bean introspection. Setting a value of 0 or negative will disable the cache. | 1000 | int |

## Endpoint Options

The Bean endpoint is configured using URI syntax:

bean:beanName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **beanName** (common) | **Required** Sets the name of the bean to invoke. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **method** (common) | Sets the name of the method to invoke on the bean. |  | String |
| **scope** (common) | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using prototype scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. so when using prototype then this depends on the delegated registry.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 | Singleton | BeanScope |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **parameters** (advanced) | Used for configuring additional properties on the bean. This is a multi-value option with prefix: bean. |  | Map |

## Examples

A **bean:** endpoint cannot be defined as the input to the route; i.e., you cannot consume from it, you can only route from some inbound message Endpoint to the bean endpoint as output, such as the **direct** endpoint as input.

Suppose you have the following POJO class to be used by Camel

```java
package com.foo;

public class MyBean {

    public String saySomething(String input) {
        return "Hello " + input;
    }
}
```

Then the bean can be called in a Camel route by the fully qualified class name:

-   Java
    
-   XML
    

```java
from("direct:hello")
   .to("bean:com.foo.MyBean");
```

```xml
<route>
   <from uri="direct:hello"/>
   <to uri="bean:com.foo.MyBean"/>
</route>
```

What happens is that when the exchange is routed to the MyBean, then Camel will use the Bean Binding to invoke the bean, in this case the _saySomething_ method, by converting the `Exchange` in body to the `String` type and storing the output of the method back to the Exchange again.

> **Tip**
> The bean component can also call a bean by _bean id_ by looking up the bean in the [Registry](../../manual/registry.md) instead of using the class name.

### Java DSL specific bean syntax

Java DSL comes with syntactic sugar for the [Bean](#) component. Instead of specifying the bean explicitly as the endpoint (i.e., `to("bean:beanName")`) you can use the following syntax:

```java
// Send a message to the bean endpoint
// and invoke method using Bean Binding.
from("direct:start").bean("beanName");

// Send a message to the bean endpoint
// and invoke given method.
from("direct:start").bean("beanName", "methodName");
```

Instead of passing the name of the reference to the bean (so that Camel will look up for it in the [Registry](../../manual/registry.md)), you can specify the bean itself:

```java
// Send a message to the given bean instance.
from("direct:start").bean(new ExampleBean());

// Explicit selection of bean method to be invoked.
from("direct:start").bean(new ExampleBean(), "methodName");

// Camel will create the instance of bean and cache it for you.
from("direct:start").bean(ExampleBean.class);
```

This bean could be a lambda if you cast the lambda to a `@FunctionalInterface`

```java
@FunctionalInterface
public interface ExampleInterface() {
    @Handler String methodName();
}

from("direct:start")
    .bean((ExampleInterface) () -> ""))
```

## Bean Binding

The [Bean Binding](../../manual/bean-binding.md) mechanism defines how methods to be invoked are chosen (if they are not specified explicitly through the **method** parameter) and how parameter values are constructed from the Message. These are used throughout all the various [Bean Integration](../../manual/bean-integration.md) mechanisms in Camel.

See also related [Bean Language](languages/bean-language.md).

## Spring Boot Auto-Configuration

When using bean with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-bean-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.bean.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.bean.bean-info-cache-size** | Maximum cache size of internal cache for bean introspection. Setting a value of 0 or negative will disable the cache. | 1000 | Integer |
| **camel.component.bean.enabled** | Whether to enable auto configuration of the bean component. This is enabled by default. |  | Boolean |
| **camel.component.bean.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.bean.scope** | Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using delegate scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. so when using prototype then this depends on the delegated registry. | singleton | BeanScope |
| **camel.component.class.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.class.bean-info-cache-size** | Maximum cache size of internal cache for bean introspection. Setting a value of 0 or negative will disable the cache. | 1000 | Integer |
| **camel.component.class.enabled** | Whether to enable auto configuration of the class component. This is enabled by default. |  | Boolean |
| **camel.component.class.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.class.scope** | Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using delegate scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. so when using prototype then this depends on the delegated registry. | singleton | BeanScope |
| **camel.language.bean.enabled** | Whether to enable auto configuration of the bean language. This is enabled by default. |  | Boolean |
| **camel.language.bean.scope** | Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using prototype scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. So when using prototype scope then this depends on the bean registry implementation. | Singleton | String |
| **camel.language.bean.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.bean.validate** | Whether to validate the bean has the configured method. | true | Boolean |