# Bean Method

**Since Camel 1.3**

The Bean language is used for calling a method on an existing Java bean.

Camel adapts to the method being called via [Bean Binding](../../../manual/bean-binding.md). The binding process will, for example, automatically convert the message payload to the parameter of type of the first parameter in the method. The binding process has a lot more features, so it is recommended to read the [Bean Binding](../../../manual/bean-binding.md) documentation for more details.

## Bean Method options

The Bean Method language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **ref** (common) |  | `String` | Reference to an existing bean (bean id) to lookup in the registry. |
| **method** (common) |  | `String` | Name of method to call. |
| **beanType** (common) |  | `String` | Class name (fully qualified) of the bean to use. Will lookup in registry and if there is a single instance of the same type, then the existing bean is used, otherwise a new bean is created (requires a default no-arg constructor). |
| **scope** (advanced) | `Singleton` | `Enum` | 
Scope of bean. When using singleton scope (default) the bean is created or looked up only once and reused for the lifetime of the endpoint.

Enum values:

-   Singleton
    
-   Request
    
-   Prototype
    





 |
| **validate** (advanced) | `true` | `Boolean` | Whether to validate the bean has the configured method. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Examples

In the given route below, we call a Java Bean Method with `method`, where "myBean" is the id of the bean to use (lookup from [Registry](../../../manual/registry.md)), and "isGoldCustomer" is the name of the method to call.

-   Java
    
-   XML
    
-   YAML
    

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

```yaml
- route:
    from:
      uri: activemq:topic:OrdersTopic
      steps:
        - filter:
            expression:
              method:
                ref: myBean
                method: isGoldCustomer
            steps:
              - to:
                  uri: activemq:BigSpendersQueue
```

The bean could be implemented as follows:

_Java-only: bean class implementation with Exchange parameter_

```java
public class MyBean {
  public boolean isGoldCustomer(Exchange exchange) {
     // ...
  }
}
```

How this method uses `Exchange` in the method signature. You would often not do that, and use non-Camel types. For example, by using `String` then Camel will automatically convert the message body to this type when calling the method:

_Java-only: bean method with automatic type conversion_

```java
public boolean isGoldCustomer(String body) {...}
```

### Using Annotations for bean integration

You can also use the [Bean Integration](../../../manual/bean-integration.md) annotations, such as `@Header`, `@Body`, `@Variable` etc

_Java-only: using bean integration annotations for parameter binding_

```java
public boolean isGoldCustomer(@Header(name = "foo") Integer fooHeader) {...}
```

So you can bind parameters of the method to the `Exchange`, the [Message](../eips/message.md) or individual headers, properties, the body or other expressions.

### Non-Registry Beans

The Bean Method Language also supports invoking beans that are not registered in the [Registry](../../../manual/registry.md).

Camel can instantiate the bean of a given type and invoke the method or invoke the method on an already existing instance.

_Java-only: invoking a bean by class type_

```java
from("activemq:topic:OrdersTopic")
  .filter().method(MyBean.class, "isGoldCustomer")
  .to("activemq:BigSpendersQueue");
```

The first parameter can also be an existing instance of a Bean such as:

_Java-only: invoking a method on an existing bean instance_

```java
private MyBean my = ...;

from("activemq:topic:OrdersTopic")
  .filter().method(my, "isGoldCustomer")
  .to("activemq:BigSpendersQueue");
```