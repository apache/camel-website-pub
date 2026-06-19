# Class

**Since Camel 2.4**

**Only producer is supported**

The Class component binds beans to Camel message exchanges. It works in the same way as the [Bean](bean-component.md) component, but instead of looking up beans from a Registry, it creates the bean based on the class name.

## URI format

class:className\[?options\]

Where `className` is the fully qualified class name to create and use as bean.

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

The Class component supports 4 options, which are listed below.

   
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

The Class endpoint is configured using URI syntax:

class:beanName

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

## Usage

You simply use the **class** component just as the [Bean](bean-component.md) component but by specifying the fully qualified class name instead. For example to use the `MyFooBean` you have to do as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("class:org.apache.camel.component.bean.MyFooBean")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="class:org.apache.camel.component.bean.MyFooBean"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: class:org.apache.camel.component.bean.MyFooBean
        - to:
            uri: mock:result
```

You can also specify which method to invoke on the `MyFooBean`, for example `hello`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("class:org.apache.camel.component.bean.MyFooBean?method=hello")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="class:org.apache.camel.component.bean.MyFooBean?method=hello"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: class:org.apache.camel.component.bean.MyFooBean
            parameters:
              method: hello
        - to:
            uri: mock:result
```

## Examples

### Setting properties on the created instance

In the endpoint uri you can specify properties to set on the created instance, for example, if it has a `setPrefix` method:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("class:org.apache.camel.component.bean.MyPrefixBean?bean.prefix=Bye")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="class:org.apache.camel.component.bean.MyPrefixBean?bean.prefix=Bye"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: class:org.apache.camel.component.bean.MyPrefixBean
            parameters:
              bean.prefix: Bye
        - to:
            uri: mock:result
```

And you can also use the `#` syntax to refer to properties to be looked up in the Registry.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("class:org.apache.camel.component.bean.MyPrefixBean?bean.cool=#foo")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="class:org.apache.camel.component.bean.MyPrefixBean?bean.cool=#foo"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: class:org.apache.camel.component.bean.MyPrefixBean
            parameters:
              bean.cool: "#foo"
        - to:
            uri: mock:result
```

Which will look up a bean from the Registry with the id `foo` and invoke the `setCool` method on the created instance of the `MyPrefixBean` class.

> **Tip**
> See more details on the [Bean](bean-component.md) component as the **class** component works in much the same way.