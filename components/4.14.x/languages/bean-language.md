# Bean Method

**Since Camel 1.3**

The Bean language is used for calling a method on an existing Java bean.

Camel adapts to the method being called via [Bean Binding](../../../manual/bean-binding.md). The binding process will, for example, automatically convert the message payload to the parameter of type of the first parameter in the method. The binding process has a lot more features, so it is recommended to read the [Bean Binding](../../../manual/bean-binding.md) documentation for more details.

## Bean Method options

The Bean Method language supports 7 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **ref** (common) |  | `String` | Reference to an existing bean (bean id) to lookup in the registry. |
| **method** (common) |  | `String` | Name of method to call. |
| **beanType** (common) |  | `String` | Class name (fully qualified) of the bean to use Will lookup in registry and if there is a single instance of the same type, then the existing bean is used, otherwise a new bean is created (requires a default no-arg constructor). |
| **scope** (advanced) | `Singleton` | `Enum` | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using prototype scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. So when using prototype scope then this depends on the bean registry implementation.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 |
| **validate** (advanced) | `true` | `Boolean` | Whether to validate the bean has the configured method. |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Examples

In the given route below, we call a Java Bean Method with `method`, where "myBean" is the id of the bean to use (lookup from [Registry](../../../manual/registry.md)), and "isGoldCustomer" is the name of the method to call.

-   Java
    
-   XML
    

```java
from("activemq:topic:OrdersTopic")
  .filter().method("myBean", "isGoldCustomer")
    .to("activemq:BigSpendersQueue");
```

> **Tip**
> It is also possible to omit the method name. In this case, then Camel would choose the best suitable method to use. This process is complex, so it is good practice to specify the method name.

```xml
<route>
  <from uri="activemq:topic:OrdersTopic"/>
  <filter>
    <method ref="myBean" method="isGoldCustomer"/>
    <to uri="activemq:BigSpendersQueue"/>
  </filter>
</route>
```

The bean could be implemented as follows:

```java
public class MyBean {
  public boolean isGoldCustomer(Exchange exchange) {
     // ...
  }
}
```

How this method uses `Exchange` in the method signature. You would often not do that, and use non-Camel types. For example, by using `String` then Camel will automatically convert the message body to this type when calling the method:

```java
public boolean isGoldCustomer(String body) {...}
```

### Using Annotations for bean integration

You can also use the [Bean Integration](../../../manual/bean-integration.md) annotations, such as `@Header`, `@Body`, `@Variable` etc

```java
public boolean isGoldCustomer(@Header(name = "foo") Integer fooHeader) {...}
```

So you can bind parameters of the method to the `Exchange`, the [Message](../eips/message.md) or individual headers, properties, the body or other expressions.

### Non-Registry Beans

The Bean Method Language also supports invoking beans that are not registered in the [Registry](../../../manual/registry.md).

Camel can instantiate the bean of a given type and invoke the method or invoke the method on an already existing instance.

```java
from("activemq:topic:OrdersTopic")
  .filter().method(MyBean.class, "isGoldCustomer")
  .to("activemq:BigSpendersQueue");
```

The first parameter can also be an existing instance of a Bean such as:

```java
private MyBean my = ...;

from("activemq:topic:OrdersTopic")
  .filter().method(my, "isGoldCustomer")
  .to("activemq:BigSpendersQueue");
```

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