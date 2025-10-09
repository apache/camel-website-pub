# Endpoints

Camel supports the [Message Endpoint](../components/4.18.x/eips/message-endpoint.md) pattern using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface.

Endpoints are created by a [Component](component.md) and these endpoints are referred to in the [DSL](dsl.md) via their endpoint [URIs](uris.md).

## Example

The following example route demonstrates the use of a [File](../components/4.18.x/file-component.md) consumer endpoint and a \* [JMS](../components/4.18.x/jms-component.md) producer endpoint, by their [URIs](uris.md):

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:messages/foo")
    .to("jms:queue:foo");
```

```xml
<route>
    <from uri="file:messages/foo"/>
    <to uri="jms:queue:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: file:messages/foo
      steps:
        - to:
            uri: jms:queue:foo
```

### Referring beans from endpoints

When configuring endpoints using the URI syntax you can refer to beans in the [Registry](registry.md) using the `#bean:id` notation.

> **Note**
> The older syntax with just `#id` has been deprecated due to ambiguity as Camel supports a number of additional functions that start with the # notation.

If the URI parameter value starts with `#bean:` then Camel will lookup in the [Registry](registry.md) for a bean of the given type by id. For instance:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:messages/foo?sorter=#bean:mySpecialFileSorter")
    .to("jms:queue:foo");
```

```xml
<route>
    <from uri="file:messages/foo?sorter=#bean:mySpecialFileSorter"/>
    <to uri="jms:queue:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: file:messages/foo?sorter=#bean:mySpecialFileSorter
      steps:
        - to:
            uri: jms:queue:foo
```

Will lookup a bean with the id `mySpecialFileSorter` in the Registry.

#### Referring beans by class

Camel also supports to refer to beans by their class type, such as `#class:com.foo.MySpecialSorter`, which then will create a new bean instance of the given class name.

If you need to provide parameters to the constructor, then this is also possible (limited to numbers, boolean, literal, and null values)

```text
file://inbox?sorter=#class:com.foo.MySpecialSorter(10, 'Hello world', true)
```

> **Tip**
> Inlining constructor arguments is only recommended for beans with a few options so the code is easy to understand and maintain. Also beware that if the bean constructor is refactored then the string text would need to be updated accordingly.

#### Referring beans by type

When configuring endpoints using URI syntax you can now refer to bean by its type which are used to lookup the bean by the given type from the [Registry](registry.md).

If there is one bean found in the registry of the given type, then that bean instance will be used; otherwise an exception is thrown.

For example below we expect there is a single bean of the `org.apache.camel.spi.IdempotentRepository` type in the [Registry](registry.md) that the file endpoint should use.

```text
file://inbox?idempontentRepository=#type:org.apache.camel.spi.IdempotentRepository
```

### Configuring endpoint URIs in XML escaping & sign

If you try and use one of the Camel [URIs](uris.md) in an XML DSL using the URI query parameter notation, such as:

```xml
<route>
  <from uri="direct:start?paramA=1&paramB=2"/>
  <to uri="mock:result"/>
</route>
```

you might get errors such as…​

Caused by: org.xml.sax.SAXParseException: The reference to entity "paramB" must end with the ';' delimiter.
  at com.sun.org.apache.xerces.internal.util.ErrorHandlerWrapper.createSAXParseException(ErrorHandlerWrapper.java:236)
  at

This is because in XML you need to escape some special XML characters like these:

 
| Special Character | How to escape it in XML |
| --- | --- |
| `&` | `&amp;` |
| `<` | `&lt;` |
| `>` | `&gt;` |

So if you write the following XML it should work…​

```xml
<route>
  <from uri="direct:start?paramA=1&amp;paramB=2"/>
  <to uri="mock:result"/>
</route>
```

If you do not escape the & sign, then you can `org.xml.sax.SAXParseException` or other kind of XML parsing errors.

In the URIs used for specifying Camel endpoints, the `&` is used to separate the parameters. However, `&` also is a reserved character in XML.

Because of this, you have to replace all `&` in your URIs by `&amp;` when using the XML DSL to configure Camel routes.

An example: this snippet of code in Java DSL:

```java
from("timer://myTimer?fixedRate=true&delay=0&period=2000")
```

1.  matches this example in the XML syntax where `&` has been replaced with `&amp;`
    

```xml
<from uri="timer://myTimer?fixedRate=true&amp;delay=0&amp;period=2000"/>
```

### Configuring parameter values using raw values, such as passwords

When configuring endpoint options using URI syntax, then the values is by default URI encoded. This can be a problem if you want to configure passwords and just use the value _as is_ without any encoding. For example, you may have a plus sign in the password, which would be decimal encoded by default.

You can define parameter value to be **raw** using the following syntax `RAW(value)`, e.g. the value starts with `RAW(` and then ends with the parenthesis `)`.

Here is a little example with the password: `se+re?t&23`:

-   Java
    
-   XML
    
-   YAML
    
-   YAML expanded
    

```java
from("file:inbox")
  .to("ftp:joe@myftpserver.com?password=RAW(se+re?t&23)&binary=true");
```

```xml
<route>
    <from uri="file:inbox"/>
    <to uri="ftp:joe@myftpserver.com?password=RAW(se+re?t&amp;23)&amp;binary=true"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - to:
            uri: ftp:joe@myftpserver.com?password=RAW(se+re?t&23)&binary=true
```

```yaml
- route:
    from:
      uri: file
      parameters:
        directoryName: inbox
      steps:
        - to:
            uri: ftp
            parameters:
              host: joe@myftpserver.com
              password: "RAW(se+re?t&23)"
              binary: true
```

In the above example, we have declared the password value as raw, and the actual password would be as typed, eg `se+re?t&23`.

> **Note**
> you may find a corner case when you use both `)` and `&` character as part of your password (ie, `se+re)t&23`). The parser will interpret the `)` as closing the `RAW` function and having a parameter started by `&`. In such case, you can instead use the `RAW{}` notation to let you include the `)` character and have it decoded as part of the password (ie, `RAW{se+re)t&23}`). As a safe alternative you can also use `password=#property:myPass` and then have `myPass` a [property placeholder value](property-binding.md).

#### Using ENV variables with raw values

If you need to use environment variables, for example as username or passwords then this is now possible by inlining the [Simple](../components/4.18.x/languages/simple-language.md) language using `$simple{xxx}` syntax in `RAW(…​)` as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .to("ftp:joe@myftpserver.com?password=RAW($simple{env:MY_FTP_PASSWORD})&binary=true");
```

```xml
<route>
    <from uri="file:inbox"/>
    <to uri="ftp:joe@myftpserver.com?password=RAW($simple{env:MY_FTP_PASSWORD})&amp;binary=true"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - to:
            uri: "ftp:joe@myftpserver.com?password=RAW($simple{env:MY_FTP_PASSWORD})&binary=true"
```

### Endpoint URIs with property placeholders

Camel has extensive support for using [Property placeholders](using-propertyplaceholder.md).

For example in the ftp example above we can externalize the password to the `application.properties` file.

```properties
myFtpPassword=RAW(se+re?t&23)
```

And the Camel routes can then refer to this placeholder using `{{key}}` style.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:inbox")
  .to("ftp:joe@myftpserver.com?password={{myFtpPassword}}&binary=true");
```

```xml
<route>
    <from uri="file:inbox"/>
    <to uri="ftp:joe@myftpserver.com?password={{myFtpPassword}}&amp;binary=true"/>
</route>
```

```yaml
- route:
    from:
      uri: file:inbox
      steps:
        - to:
            uri: "ftp:joe@myftpserver.com?password={{myFtpPassword}}&binary=true"
```

And have a `application.properties` file with password. Notice we still define the `RAW(value)` style to ensure the password is used _as is_:

```properties
myFtpPassword=RAW(se+re?t&23)
```

We could still have used the `RAW(value)` in the Camel route instead:

```java
.to("ftp:joe@myftpserver.com?password=RAW({{myFtpPassword}})&binary=true")
```

And then we would need to remove the `RAW` from the properties file:

```properties
myFtpPassword=se+re?t&23
```

## Configuring CamelContext default cache size

The [CamelContext](camelcontext.md) will by default cache the last 1000 used endpoints (based on a LRUCache).

This must be done on the `CamelContext` as a global option as shown in the following Java code:

```java
getCamelContext().getGlobalOptions().put(Exchange.MAXIMUM_ENDPOINT_CACHE_SIZE, "500");
```

The default maximum cache size is 1000.

You need to configure this before [CamelContext](camelcontext.md) is started.

## Configuring time duration using hours, minutes syntax

Some of the Camel [components](component.md) offers options to specify a time period, which must be entered in millisecond as unit.

This may be unfriendly to read as a human when the value is large such as `2700000` millis (45 minutes).

In Camel you can configure this in a more readable syntax as explained:

 
| Syntax | Unit |
| --- | --- |
| h | hour |
| m | minute |
| s | second |

So for example the [Timer](../components/4.18.x/timer-component.md) endpoint can be configured as follows:

```java
from("timer:foo?period=45m").to("log:foo");
```

You can mix and match the units so you can do this as well:

```java
from("timer:foo?period=1h15m").to("log:foo");
from("timer:bar?period=2h30s").to("log:bar");
from("timer:bar?period=3h45m58s").to("log:bar");
```

However, you can also use long syntax:

 
| Syntax | Unit |
| --- | --- |
| hour _or_ hours | hour |
| minute _or_ minutes | minute |
| second _or_ seconds | second |

```java
from("timer:foo?period=45minutes").to("log:foo");
```

## Java Endpoint API

You will almost never have the need for creating endpoints manually via Java API.

From an `Endpoint` you can use the following Java API methods to create producers or consumers to the endpoint:

-   [`createProducer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createProducer--) will create a [Producer](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Producer.md) for sending message exchanges to the endpoint.
    
-   [`createConsumer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createConsumer-org.apache.camel.Processor) implements the [Event Driven Consumer](../components/4.18.x/eips/eventDrivenConsumer-eip.md) pattern for consuming message exchanges from the endpoint via a [Processor](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Processor.md) when creating a [Consumer](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Consumer.md).
    
-   [`createPollingConsumer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createPollingConsumer) implements the [Polling Consumer](../components/4.18.x/eips/polling-consumer.md) pattern for consuming message exchanges from the endpoint via a [PollingConsumer](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/PollingConsumer.md).