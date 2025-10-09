# Bean

The Bean EIP is used for invoking a method on a bean, and the returned value is the new message body.

The Bean EIP is similar to the [Bean](../bean-component.md) component which also is used for invoking beans, but in the form as a Camel component.

## URI Format

```none
bean:beanID[?options]
```

Where **beanID** can be any string which is used to look up the bean in the [Registry](../../../manual/registry.md).

## EIP options

The Bean eip supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ref** | Sets a reference to an exiting bean to use, which is looked up from the registry. |  | String |
| **method** | Sets the method name on the bean to use. |  | String |
| **beanType** | Sets the class name (fully qualified) of the bean to use. |  | String |
| **scope** | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time. When using request scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request. When using prototype scope, then the bean will be looked up or created per call. However in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. So when using prototype scope then this depends on the bean registry implementation.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 | Singleton | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

### Bean scope

When using `singleton` scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads is calling the bean at the same time.

When using `request` scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request, and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request.

When using `prototype` scope, then the bean will be looked up or created per call. However, in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. However, when using `prototype` then behaviour is dependent on the delegated registry (such as Spring, Quarkus or CDI).

## Example

The Bean EIP can be used directly in the routes as shown below:

```java
// lookup bean from registry and invoke the given method by the name
from("direct:foo").bean("myBean", "myMethod");

// lookup bean from registry and invoke best matching method
from("direct:bar").bean("myBean");
```

And with Spring XML you can declare the bean using `<bean>` as shown:

```xml
<bean id="myBean" class="com.foo.ExampleBean"/>
```

And in XML DSL you can call this bean:

```xml
<routes>
    <route>
      <from uri="direct:foo"/>
      <bean ref="myBean" method="myMethod"/>
    </route>
    <route>
      <from uri="direct:bar"/>
      <bean ref="myBean"/>
    </route>
</routes>
```

Instead of passing name of the reference to the bean (so that Camel will lookup for it in the registry), you can provide the bean:

```java
// Send message to the given bean instance.
from("direct:foo").bean(new ExampleBean());

// Explicit selection of bean method to be invoked.
from("direct:bar").bean(new ExampleBean(), "myMethod");

// Camel will create a singleton instance of the bean, and reuse the instance for following calls (see scope)
from("direct:cheese").bean(ExampleBean.class);
```

In XML DSL this is also possible using `beanType`:

```xml
<routes>
    <route>
      <from uri="direct:foo"/>
      <bean beanType="com.foo.ExampleBean" method="myMethod"/>
    </route>
    <route>
      <from uri="direct:bar"/>
      <bean beanType="com.foo.ExampleBean"/>
    </route>
    <route>
      <from uri="direct:cheese"/>
      <bean beanType="com.foo.ExampleBean"/>
    </route>
</routes>
```

## Bean binding

How bean methods to be invoked are chosen (if they are not specified explicitly through the **method** parameter) and how parameter values are constructed from the [Message](message.md) are all defined by the [Bean Binding](../../../manual/bean-binding.md) mechanism which is used throughout all the various [Bean Integration](../../../manual/bean-integration.md) mechanisms in Camel.