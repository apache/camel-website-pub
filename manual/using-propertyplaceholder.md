# Property placeholders

Camel has extensive support for property placeholders, which can be used _almost anywhere_ in your Camel [routes](routes.md), [endpoints](endpoint.md), [DSL](dsl.md), and [route configuration](route-configuration.md), [bean integration](bean-integration.md) and elsewhere.

Property placeholders are used to define a _placeholder_ instead of the actual value. This is important as you would want to be able to make your applications external configurable, such as values for network addresses, port numbers, authentication credentials, login tokens, and configuration in general.

## Properties component

Camel provides the [Properties](../components/4.18.x/properties-component.md) out of the box from the core, which is responsible for handling and resolving the property placeholders.

See the [Properties](../components/4.18.x/properties-component.md) documentation for how to configure Camel to known from which location(a) to load properties.

## Property placeholder syntax

The value of a Camel property can be obtained by specifying its key name within a property placeholder, using the following syntax: `{{key}}`

For example:

```text
{{file.uri}}
```

where `file.uri` is the property key.

Property placeholders can for example be used to specify parts, or all, of an [endpoint uri](uris.md) by embedding one or more placeholders in the URI’s string definition.

For example as shown in the route below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("{{file.uri}}")
  .to("kafka:{{orderTopic}}");
```

```xml
    <route>
        <from uri="{{file.uri}}"/>
        <to uri="kafka:{{orderTopic}}"/>
    </route>
```

```yaml
- route:
    from:
      uri: "{{file.uri}}"
      steps:
        - to:
            uri: "kafka:{{orderTopic}}"
```

Then the placeholder can be declared in `application.properties`:

```properties
file.uri = file:/var/orders/inbox?recursive=true
```

### Using property placeholder with default value

You can specify a default value to use if a property with the key does not exist, where the default value is the text after the colon:

```text
{{file.url:/some/path}}
```

In this case the default value is `/some/path`.

### Using optional property placeholders

Camel’s elaborate property placeholder feature supports optional placeholders, which is declared with the `?` (question mark) as prefix in the key name, as shown:

```text
{{?myBufferSize}}
```

If a value for the key exists then the value is used, however if the key does not exist, then Camel understands how to handle this. For example when used in [Endpoints](endpoint.md):

```text
file:foo?bufferSize={{?myBufferSize}}
```

Then the `bufferSize` option will only be configured in the endpoint, if a placeholder exists. Otherwise, the option will not be set on the endpoint, meaning the endpoint would be _restructured_ as:

```text
file:foo
```

Then the option `bufferSize` is not declared, and this would allow Camel to use the standard default value for `bufferSize` (if any exists).

### Reverse a boolean value

If a property placeholder is a boolean value, then it is possible to negate (reverse) the value by using `!` as prefix in the key.

For example given we have this property:

```properties
integration.ftpEnabled=true
```

Then this can be used to control which routes should be auto started.

-   Java
    
-   XML
    
-   YAML
    

```java
from("ftp:....").autoStartup("{{integration.ftpEnabled}}")
    .to("kafka:cheese");

from("jms:....").autoStartup("{{!integration.ftpEnabled}}")
    .to("kafka:cheese");
```

```xml
<route autoStartup="{{integration.ftpEnabled}}">
    <from uri="ftp:...."/>
    <to uri="kafka:cheese"/>
</route>

<route autoStartup="{{!integration.ftpEnabled}}">
    <from uri="jms:...."/>
    <to uri="kafka:cheese"/>
</route>
```

```yaml
- route:
    autoStartup: "{{integration.ftpEnabled}}"
    from:
      uri: ftp:....
      steps:
        - to:
            uri: kafka:cheese
- route:
    autoStartup: "{{!integration.ftpEnabled}}"
    from:
      uri: jms:....
      steps:
        - to:
            uri: kafka:cheese
```

In the example above then the FTP route or the JMS route should only be started. So if the FTP is enabled then JMS should be disabled, and vice versa. We can do this be negating the `autoStartup` in the JMS route, by using `!integration.ftpEnabled` as the key.

## Using property placeholders

When using property placeholders in the endpoint [URIs](uris.md) you should use this with the syntax `{{key}}` as shown in this example:

```properties
cool.end = mock:result
where = cheese
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{cool.end}}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="{{cool.end}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{cool.end}}"
```

A property placeholder may also just be a one part in the endpoint URI.

A common use-case is to use a placeholder for an endpoint option such as the size of the write buffer in the file endpoint:

```properties
buf = 8192
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("file:outbox?bufferSize={{buf}}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="file:outbox?bufferSize={{buf}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: file:outbox
            parameters:
              bufferSize: "{{buf}}"
```

However, the placeholder can be anywhere, so it could also be the name of a mock endpoint

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("mock:{{where}}");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="mock:{{where}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "mock:{{where}}"
```

In the example above the mock endpoint, is already hardcoded to start with `mock:`, and the `where` placeholder has the value `cheese` so the resolved uri becomes `mock:cheese`.

### Property placeholders referring to other properties (nested placeholders)

You can also have properties with refer to each other such as:

```properties
cool.foo=result
cool.concat=mock:{{cool.foo}}
```

Notice how `cool.concat` refer to another property (above).

You can then use the `cool.concat` placeholder in the Camel routes:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("{{cool.concat}}");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="{{cool.concat}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "{{cool.concat}}"
```

#### Turning off nested placeholders (advanced)

If the placeholder value contains data that interfere with the property placeholder syntax `{{` and `}}` (such as JSon data), you can be then explicit turn off nested placeholder by `?nested=false` in the key name, such as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("elasticsearch:foo?query={{myQuery?nested=false}}");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="elasticsearch:foo?query={{myQuery?nested=false}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: elasticsearch:foo
            parameters:
              query: "{{myQuery?nested=false}}"
```

In the example above the placeholder _myQuery_ placeholder value is as follows

```properties
myQuery = {"query":{"match_all":{}}}
```

Notice how the JSon query ends with `}}` which interfere with the Camel property placeholder syntax.

Nested placeholders can also be turned off globally on the [Properties](../components/4.18.x/properties-component.md) component, such as:

```java
CamelContext context = ...
context.getPropertiesComponent().setNestedPlaceholder(false);
```

In the situation with the JSon query ending with `}}` which clashes with Camels property placeholder syntax, then its also possible to use escaping as explained in the following section.

#### Escaping a property placeholder

The property placeholder can be problematic if the double curly brackets are used by a third party library like for example a query in ElasticSearch of type `{"query":{"match_all":{}}}`.

To work around that it is possible to escape the double curly brackets with a backslash character like for example `\{{ property-name \}}`. This way, it won’t be interpreted as a property placeholder to resolve and will be resolved as `{{ property-name }}`.

The previous example can then use escaping (see how the value ends with `\\}}`)

```properties
myQuery = {"query":{"match_all":{}\\}}
```

If for some reason, the backslash character before the double curly brackets must not be interpreted as an escape character, it is possible to add another backslash in front of it to escape it, it will then be seen as a backslash.

### Using property placeholders multiple times

You can of course also use placeholders several times:

```properties
cool.start=direct:start
cool.showid=true
cool.result=result
```

And in this route we use `cool.start` two times:

-   Java
    
-   XML
    
-   YAML
    

```java
from("{{cool.start}}")
    .to("log:{{cool.start}}?showBodyType=false&showExchangeId={{cool.showid}}")
    .to("mock:{{cool.result}}");
```

```xml
<route>
    <from uri="{{cool.start}}"/>
    <to uri="log:{{cool.start}}?showBodyType=false&amp;showExchangeId={{cool.showid}}"/>
    <to uri="mock:{{cool.result}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "log:{{cool.start}}"
            parameters:
              showBodyType: "false"
              showExchangeId: "{{cool.showid}}"
        - to:
            uri: "mock:{{cool.result}}"
```

### Using property placeholders with consumer and producer templates

You can also your property placeholders when using [ProducerTemplate](producertemplate.md) for example:

```java
template.sendBody("{{cool.start}}", "Hello World");
```

This can also be done when using [ConsumerTemplate](consumertemplate.md), such as:

```java
Object body = template.receiveBody("{{cool.start}}");
```

## Resolving property placeholders from Java code

If you need to resolve property placeholder(s) from some Java code, then Camel has two APIs for this:

-   You can use the method `resolveProperty` on the `PropertiesComponent` to resolve a single property from Java code.
    
-   Use the method `resolvePropertyPlaceholders` on the `CamelContext` to resolve (one or more) property placeholder(s) in a String.
    

For example to resolve a placeholder with key foo, you can do:

```java
Optional<String> prop = camelContext.getPropertiesComponent().resolveProperty("foo");
if (prop.isPresent()) {
    String value = prop.get();
    ....
}
```

This API is to lookup a single property and returns a `java.util.Optional` type.

The `CamelContext` have another API which is capable of resolving multiple placeholders, and interpolate placeholders from an input String. Let’s try with an example to explain this:

```java
String msg = camelContext.resolvePropertyPlaceholders("{{greeting}} Camel user, Camel is {{cool}} dont you think?");
```

The input string is a text statement which have two placeholders that will be resolved, for example:

```properties
greeting = Hi
cool = awesome
```

Will be resolved to:

```text
Hi Camel user, Camel is awesome dont you think?
```

## Resolving property placeholders on cloud

When you are running your Camel application on the cloud you may want to automatically scan any Configmap or Secret as it was an application properties. Given the following Secret:

```yaml
apiVersion: v1
data:
  my-property: Q2FtZWwgNC44
kind: Secret
metadata:
  name: my-secret
type: Opaque
```

You can mount it in your Pod container, for instance, under `/etc/camel/conf.d/_secrets/my-secret`. Now, just make your Camel application be aware where to scan your configuration via `camel.main.cloud-properties-location = /etc/camel/conf.d/_secrets/my-secret` application properties. It’s a comma separated value, so, you can add as many Secrets/Configmaps you need.

At runtime, you will be able to read the configuration transparently as `` `{{ my-property }}` `` as you’re doing with the rest of properties.

> **Note**
> the same configuration works with Configmap.

## Special features for legacy Spring XML files

Apache Camel started decade(s) ago when Spring Framework was heavily used with Spring XML files. This means Camel has special features that apply only to Spring XML.

### Using property placeholders for any kind of attribute in Spring XML files

Previously it was only the `xs:string` type attributes in the XML DSL that support placeholders. For example often a timeout attribute would be a `xs:int` type, and thus you cannot set a string value as the placeholder key. This is now possible using a special placeholder namespace.

In the example below we use the `prop` prefix for the namespace `http://camel.apache.org/schema/placeholder`. Now we can use `prop:` as prefix to configure any kind of XML attributes in Spring XML files.

In the example below we want to use a placeholder for the `stopOnException` option in the [Multicast](../components/4.18.x/eips/multicast-eip.md) EIP. The `stopOnException` is a `xs:boolean` type, so we cannot configure this as:

```xml
<multicast stopOnException="{{stop}}">
   ...
</multicast>
```

Instead, we must use the `prop:` namespace, so we must add this namespace in the top of the XML file in the `<beans>` tag.

To configure the option we must then use the `prop:optionName` as shown below:

```xml
<multicast prop:stopOnException="stop">
  ...
</multicast>
```

The complete example is below:

Spring XML

```xml
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:prop="http://camel.apache.org/schema/placeholder"
       xsi:schemaLocation="
           http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
           http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

    <bean id="damn" class="java.lang.IllegalArgumentException">
        <constructor-arg index="0" value="Damn"/>
    </bean>

    <camelContext xmlns="http://camel.apache.org/schema/spring">
        <propertyPlaceholder id="properties" location="classpath:myprop.properties"/>
        <route>
            <from uri="direct:start"/>
            <!-- use prop namespace, to define a property placeholder, which maps to option stopOnException={{stop}} -->
            <multicast prop:stopOnException="stop">
                <to uri="mock:a"/>
                <throwException ref="damn"/>
                <to uri="mock:b"/>
            </multicast>
        </route>
    </camelContext>
</beans>
```

In our properties file we have the value defined as:

```properties
stop = true
```

### Bridging Camel property placeholders with Spring XML files

> **Note**
> If you are using Spring Boot then this does not apply. This is only for legacy Camel and Spring applications which are using Spring XML files.

The Spring Framework does not allow third-party frameworks such as Apache Camel to seamless hook into the Spring property placeholder mechanism. However, you can bridge Spring and Camel by declaring a Spring bean with the type `org.apache.camel.spring.spi.BridgePropertyPlaceholderConfigurer`, which is a Spring `org.springframework.beans.factory.config.PropertyPlaceholderConfigurer` type.

To bridge Spring and Camel you must define a single bean as shown below:

Spring XML

```xml
<!-- bridge spring property placeholder with Camel -->
<!-- you must NOT use the <context:property-placeholder at the same time, only this bridge bean -->
<bean id="bridgePropertyPlaceholder" class="org.apache.camel.spring.spi.BridgePropertyPlaceholderConfigurer">
  <property name="location" value="classpath:org/apache/camel/component/properties/cheese.properties"/>
</bean>
```

You **must not** use the spring `<context:property-placeholder>` namespace at the same time; this is not possible.

After declaring this bean, you can define property placeholders using both the Spring style, and the Camel style within the `<camelContext>` tag as shown below:

Spring XML

```xml
<!-- a bean that uses Spring property placeholder -->
<!-- the ${hi} is a spring property placeholder -->
<bean id="hello" class="org.apache.camel.component.properties.HelloBean">
  <property name="greeting" value="${hi}"/>
</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">
  <!-- in this route we use Camels property placeholder {{ }} style -->
  <route>
    <from uri="direct:{{cool.bar}}"/>
    <bean ref="hello"/>
    <to uri="{{cool.end}}"/>
  </route>
</camelContext>
```

Notice how the hello bean is using pure Spring property placeholders using the `${}` notation. And in the Camel routes we use the Camel placeholder notation with `{{key}}`.

## Property Placeholder Functions

Camel supports built-in functions for looking up properties from environment variables, system properties, Kubernetes, and custom sources.

See [Property Placeholder Functions](property-placeholder-functions.md) for details.

## Using third party property sources

The properties component allows to plugin 3rd party sources to load and lookup properties via the `PropertySource` API from camel-api.

The regular `PropertySource` will lookup the property on-demand, for example to lookup values from a backend source such as a database or HashiCorp Vault etc.

A `PropertySource` can define that it supports loading all its properties (by implementing `LoadablePropertiesSource`) from the source at once, for example from file system. This allows Camel properties component to load these properties at once during startup.

For example the `camel-microprofile-config` component is implemented using this. The 3rd-party `PropertySource` can automatically be discovered from classpath when Camel is starting up. This is done by including the file `META-INF/services/org/apache/camel/property-source-factory` which refers to the fully qualified class name of the `PropertySource` implementation.

See [MicroProfile Config](../components/4.18.x/others/microprofile-config.md) component as an example.

You can also register 3rd-party property sources via Java API on the `PropertiesComponent` as shown:

```java
PropertiesComponent pc = context.getPropertiesComponent();
pc.addPropertiesSource(myPropertySource);
```