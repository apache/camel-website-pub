# jOOR

> **Warning**
> **Deprecated:** This joor is deprecated and may be removed in a future release.

**Since Camel 3.7**

The jOOR language allows using Java code in your Camel expression, with some limitations.

The jOOR library integrates with the Java compiler and performs runtime compilation of Java code.

> **Note**
> The jOOR language is actually Java code and therefore `joor` has been deprecated in favour of using `java` as the language name in Camel.

> **Note**
> Java 8 is not supported. Java 11 is required.

## jOOR Options

The jOOR language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **preCompile** (advanced) | `true` | `Boolean` | Whether the expression should be pre compiled once during initialization phase. If this is turned off, then the expression is reloaded and compiled on each evaluation. |
| **singleQuotes** (advanced) | `true` | `Boolean` | Whether single quotes can be used as replacement for double quotes. This is convenient when you need to work with strings inside strings. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Usage

### Variables

The jOOR language allows the following variables to be used in the script:

  
| Variable | Java Type | Description |
| --- | --- | --- |
| `context` | `Context` | The CamelContext |
| `exchange` | `Exchange` | The Camel Exchange |
| `message` | `Message` | The Camel message |
| `body` | `Object` | The message body |

### Functions

The jOOR language allows the following functions to be used in the script:

 
| Function | Description |
| --- | --- |
| bodyAs(type) | To convert the body to the given type. |
| headerAs(name, type) | To convert the header with the name to the given type. |
| headerAs(name, defaultValue, type) | To convert the header with the name to the given type. If no header exists, then use the given default value. |
| exchangePropertyAs(name, type) | To convert the exchange property with the name to the given type. |
| exchangePropertyAs(name, defaultValue, type) | To convert the exchange property with the name to the given type. If no exchange property exists, then use the given default value. |
| optionalBodyAs(type) | To convert the body to the given type, returned wrapped in `java.util.Optional`. |
| optionalHeaderAs(name, type) | To convert the header with the name to the given type, returned wrapped in `java.util.Optional`. |
| optionalExchangePropertyAs(name, type) | To convert the exchange property with the name to the given type, returned wrapped in `java.util.Optional`. |

These functions are convenient for getting the message body, header or exchange properties as a specific Java type.

Here we want to get the message body as a `com.foo.MyUser` type we can do as follows:

_Java-only: jOOR type conversion function_

```java
var user = bodyAs(com.foo.MyUser.class);
```

You can omit _.class_ to make the function a little smaller:

_Java-only: jOOR shorthand type conversion_

```java
var user = bodyAs(com.foo.MyUser);
```

The type must be a fully qualified class type, but that can be inconvenient to type all the time. In such a situation, you can configure an import in the `camel-joor.properties` file as shown below:

```properties
import com.foo.MyUser;
```

And then the function can be shortened:

_Java-only: jOOR type conversion with imported class_

```java
var user = bodyAs(MyUser);
```

### Dependency Injection

The Camel jOOR language allows dependency injection by referring to beans by their id from the Camel registry. For optimization purposes, then the beans are injected once in the constructor and the scopes are _singleton_. This requires the injected beans to be _thread safe_ as they will be reused for all processing.

In the jOOR script you declare the injected beans using the syntax `#bean:beanId`.

For example, suppose we have the following bean

_Java-only: bean class used for dependency injection_

```java
public class MyEchoBean {

    public String echo(String str) {
        return str + str;
    }

    public String greet() {
        return "Hello ";
    }
}
```

And this bean is registered with the name `myEcho` in the Camel registry.

The jOOR script can then inject this bean directly in the script where the bean is in use:

_Java-only: jOOR bean injection in route_

```java
from("direct:start")
    .transform().joor("'Hello ' + #bean:myEcho.echo(bodyAs(String))")
    .to("mock:result");
```

Now this code may seem a bit magic, but what happens is that the `myEcho` bean is injected via a constructor, and then called directly in the script, so it is as fast as possible.

Under the hood, Camel jOOR generates the following source code compiled once:

_Java-only: generated compiled jOOR script class_

```java
public class JoorScript1 implements org.apache.camel.language.joor.JoorMethod {

    private MyEchoBean myEcho;

    public JoorScript1(CamelContext context) throws Exception {
        myEcho = context.getRegistry().lookupByNameAndType("myEcho", MyEchoBean.class);
    }

    @Override
    public Object evaluate(CamelContext context, Exchange exchange, Message message, Object body, Optional optionalBody) throws Exception {
        return "Hello " + myEcho.echo(bodyAs(exchange, String.class));
    }
}
```

You can also store a reference to the bean in a variable which would more resemble how you would code in Java

_Java-only: jOOR bean variable reference in route_

```java
from("direct:start")
    .transform().joor("var bean = #bean:myEcho; return 'Hello ' + bean.echo(bodyAs(String))")
    .to("mock:result");
```

Notice how we declare the bean as if it is a local variable via `var bean = #bean:myEcho`. When doing this, we must use a different name as `myEcho` is the variable used by the dependency injection. Therefore, we use _bean_ as name in the script.

### Auto imports

The jOOR language will automatically import from:

_Java-only: jOOR auto-imported packages_

```java
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;
import org.apache.camel.*;
import org.apache.camel.util.*;
```

### Configuration file

You can configure the jOOR language in the `camel-joor.properties` file which by default is loaded from the root classpath. You can specify a different location with the `configResource` option on the jOOR language.

For example, you can add additional imports in the `camel-joor.properties` file by adding:

```properties
import com.foo.MyUser;
import com.bar.*;
import static com.foo.MyHelper.*;
```

You can also add aliases (`key=value`) where an alias will be used as a shorthand replacement in the code.

```properties
echo()=bodyAs(String) + bodyAs(String)
```

Which allows using `echo()` in the jOOR language script such as:

_Java-only: jOOR alias usage in route_

```java
from("direct:hello")
    .transform(joor("'Hello ' + echo()"))
    .log("You said ${body}");
```

The `echo()` alias will be replaced with its value resulting in a script as:

_Java-only: jOOR alias expansion result_

```java
.transform(joor("'Hello ' + bodyAs(String) + bodyAs(String)"))
```

You can configure a custom configuration location for the `camel-joor.properties` file or reference to a bean in the registry:

_Java-only: programmatic language configuration_

```java
JoorLanguage joor = (JoorLanguage) context.resolveLanguage("joor");
joor.setConfigResource("ref:MyJoorConfig");
```

And then register a bean in the registry with id `MyJoorConfig` that is a String value with the content.

_Java-only: programmatic bean registration_

```java
String config = "....";
camelContext.getRegistry().put("MyJoorConfig", config);
```

## Example

For example, to transform the message using jOOR language to the upper case

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:orders")
  .transform().joor("message.getBody(String.class).toUpperCase()")
  .to("seda:upper");
```

```xml
<route>
   <from uri="seda:orders"/>
   <transform>
     <joor>message.getBody(String.class).toUpperCase()</joor>
   </transform>
   <to uri="seda:upper"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:orders
      steps:
        - transform:
            expression:
              joor:
                expression: "message.getBody(String.class).toUpperCase()"
        - to:
            uri: seda:upper
```

### Multi statements

It is possible to include multiple statements. The code below shows an example where the `user` header is retrieved in a first statement. And then, in a second statement we return a value whether the user is `null` or not.

_Java-only: jOOR multi-statement expression in route_

```java
from("seda:orders")
  .transform().joor("var user = message.getHeader(\"user\"); return user != null ? \"User: \" + user : \"No user exists\";")
  .to("seda:user");
```

Notice how we have to quote strings in strings, and that is annoying, so instead we can use single quotes:

_Java-only: jOOR single-quoted string syntax_

```java
from("seda:orders")
  .transform().joor("var user = message.getHeader('user'); return user != null ? 'User: ' + user : 'No user exists';")
  .to("seda:user");
```

### Hot re-load

You can turn off pre-compilation for the jOOR language and then Camel will recompile the script for each message. You can externalize the code into a resource file, which will be reloaded on each message as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
JoorLanguage joor = (JoorLanguage) context.resolveLanguage("joor");
joor.setPreCompile(false);

from("jms:incoming")
    .transform().joor("resource:file:src/main/resources/orders.joor")
    .to("jms:orders");
```

Here the jOOR script is externalized into the file `src/main/resources/orders.joor` which allows you to edit this source file while running the Camel application and try the changes with hot-reloading.

In XML DSL it’s easier because you can turn off pre-compilation in the `<joor>` XML element:

```xml
<route>
    <from uri="jms:incoming"/>
    <transform>
      <joor preCompile="false">resource:file:src/main/resources/orders.joor</joor>
    </transform>
    <to uri="jms:orders"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:incoming
      steps:
        - transform:
            expression:
              joor:
                expression: "resource:file:src/main/resources/orders.joor"
                preCompile: false
        - to:
            uri: jms:orders
```

### Lambda-based AggregationStrategy

The jOOR language has special support for defining an `org.apache.camel.AggregationStrategy` as a lambda expression. This is useful when using EIP patterns that use aggregation such as the Aggregator, Splitter, Recipient List, Enrich, and others.

To use this then the jOOR language script must be in the following syntax:

(e1, e2) -> { }

Where `e1` and `e2` are the _old_ Exchange and _new_ Exchange from the `aggregate` method in the `AggregationStrategy`. The returned value is used as the aggregated message body, or use `null` to skip this.

The lambda syntax is representing a Java util `BiFunction<Exchange, Exchange, Object>` type.

For example, to aggregate message bodies together, we can do this as shown:

_Java-only: jOOR lambda-based aggregation strategy_

```java
(e1, e2) -> {
  String b1 = e1.getMessage().getBody(String.class);
  String b2 = e2.getMessage().getBody(String.class);
  return b1 + ',' + b2;
}
```

### Limitations

The jOOR Camel language is only supported as a block of Java code that gets compiled into a Java class with a single method. The code that you can write is therefore limited to a number of Java statements.

The supported runtime is intended for Java standalone, Spring Boot, Camel Quarkus and other microservices runtimes. It is not supported on any kind of Java Application Server runtime.

## Dependencies

To use scripting languages in your camel routes, you need to add a dependency on **camel-joor**.

If you use Maven you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-joor</artifactId>
  <version>x.x.x</version>
</dependency>
```