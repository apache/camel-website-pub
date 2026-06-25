# Bean

The Bean EIP is used for invoking a method on a bean, and the returned value is the new message body.

The Bean EIP is similar to the [Bean](../bean-component.md) component which also is used for invoking beans, but in the form as a Camel component.

## URI Format

bean:beanID\[?options\]

Where **beanID** can be any string used to look up the bean in the [Registry](../../../manual/registry.md).

## EIP options

The Bean eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **ref** | A reference to an existing bean to use, which is looked up from the registry. |  | String |
| **method** | The method name on the bean to invoke. |  | String |
| **beanType** | The class name (fully qualified) of the bean to use. |  | String |
| **scope** | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 | Singleton | String |

## Exchange properties

The Bean eip has no exchange properties.

### Bean scope

When using `singleton` scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint. The bean should be thread-safe in case concurrent threads are calling the bean at the same time.

When using `request` scope the bean is created or looked up once per request (exchange). This can be used if you want to store state on a bean while processing a request, and you want to call the same bean instance multiple times while processing the request. The bean does not have to be thread-safe as the instance is only called from the same request.

When using `prototype` scope, then the bean will be looked up or created per call. However, in case of lookup then this is delegated to the bean registry such as Spring or CDI (if in use), which depends on their configuration can act as either singleton or prototype scope. However, when using `prototype` then behaviour is dependent on the delegated registry (such as Spring, Quarkus or CDI).

## Example

The Bean EIP can be used directly in the routes as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
// lookup bean from registry and invoke the given method by the name
from("direct:foo").bean("myBean", "myMethod");

// lookup bean from registry and invoke best matching method
from("direct:bar").bean("myBean");
```

With Spring XML you can declare the bean using `<bean>` as shown:

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

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - bean:
            ref: myBean
            method: myMethod
- route:
    from:
      uri: direct:start
      steps:
        - bean:
            ref: myBean
- beans:
    - name: myBean
      type: com.foo.ExampleBean
```

Instead of passing the name of the reference to the bean (so that Camel will look up for it in the registry), you can provide the bean:

-   Java
    
-   XML
    
-   YAML
    

```java
// Send a message to the given bean instance.
from("direct:foo").bean(new ExampleBean());

// Explicit selection of bean method to be invoked.
from("direct:bar").bean(new ExampleBean(), "myMethod");

// Camel will create a singleton instance of the bean, and reuse the instance for the following calls (see scope)
from("direct:cheese").bean(ExampleBean.class);
```

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

```yaml
- route:
    from:
      uri: direct:foo
      steps:
        - bean:
            beanType: com.foo.ExampleBean
            method: myMethod
- route:
    from:
      uri: direct:bar
      steps:
        - bean:
            beanType: com.foo.ExampleBean
- route:
    from:
      uri: direct:cheese
      steps:
        - bean:
            beanType: com.foo.ExampleBean
```

## Bean binding

How bean methods to be invoked are chosen (if they are not specified explicitly through the **method** parameter) and how parameter values are constructed from the [Message](message.md) are all defined by the [Bean Binding](../../../manual/bean-binding.md) mechanism. This is used throughout all the various [Bean Integration](../../../manual/bean-integration.md) mechanisms in Camel.