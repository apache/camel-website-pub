# XQuery

**Since Camel 1.0**

Camel supports [XQuery](http://www.w3.org/TR/xquery/) to allow an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) to be used in the [DSL](../../../manual/dsl.md).

For example, you could use XQuery to create a predicate in a [Message Filter](../eips/filter-eip.md) or as an expression for a [Recipient List](../eips/recipientList-eip.md).

## XQuery Language options

The XQuery language supports 6 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** |  | `String` | Sets the class of the result type (type from output). |
| **type** |  | `String` | Sets the class name of the result type (type from output) The default result type is NodeSet. |
| **configurationRef** |  | `String` | Reference to a saxon configuration instance in the registry to use for xquery (requires camel-saxon). This may be needed to add custom functions to a saxon configuration, so these custom functions can be used in xquery expressions. |
| **headerName** |  | `String` | Name of header to use as input, instead of the message body It has as higher precedent than the propertyName if both are set. |
| **propertyName** |  | `String` | Name of property to use as input, instead of the message body. It has a lower precedent than the headerName if both are set. |
| **trim** | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Variables

The message body will be set as the `contextItem`. And the following variables are available as well:

  
| Variable | Type | Description |
| --- | --- | --- |
| exchange | Exchange | The current Exchange |
| in.body | Object | The message body |
| out.body | Object | **deprecated** The OUT message body (if any) |
| in.headers.\* | Object | You can access the value of exchange.in.headers with key **foo** by using the variable which name is in.headers.foo |
| out.headers.\* | Object | **deprecated** You can access the value of exchange.out.headers with key **foo** by using the variable which name is out.headers.foo variable |
| **key name** | Object | Any exchange.properties and exchange.in.headers and any additional parameters set using `setParameters(Map)`. These parameters are added with they own key name, for instance if there is an IN header with the key name **foo** then its added as **foo**. |

## Example

```java
from("queue:foo")
  .filter().xquery("//foo")
  .to("queue:bar")
```

You can also use functions inside your query, in which case you need an explicit type conversion, or you will get an `org.w3c.dom.DOMException: HIERARCHY_REQUEST_ERR`). You need to pass in the expected output type of the function. For example the concat function returns a `String` which is done as shown:

```java
from("direct:start")
  .recipientList().xquery("concat('mock:foo.', /person/@city)", String.class);
```

And in XML DSL:

```xml
<route>
  <from uri="direct:start"/>
  <recipientList>
    <xquery type="java.lang.String">concat('mock:foo.', /person/@city</xquery>
  </recipientList>
</route>
```

### Using namespaces

If you have a standard set of namespaces you wish to work with and wish to share them across many XQuery expressions you can use the `org.apache.camel.support.builder.Namespaces` when using Java DSL as shown:

```java
Namespaces ns = new Namespaces("c", "http://acme.com/cheese");

from("direct:start")
  .filter().xquery("/c:person[@name='James']", ns)
  .to("mock:result");
```

Notice how the namespaces are provided to `xquery` with the `ns` variable that are passed in as the 2nd parameter.

Each namespace is a key=value pair, where the prefix is the key. In the XQuery expression then the namespace is used by its prefix, eg:

```text
/c:person[@name='James']
```

The namespace builder supports adding multiple namespaces as shown:

```java
Namespaces ns = new Namespaces("c", "http://acme.com/cheese")
                     .add("w", "http://acme.com/wine")
                     .add("b", "http://acme.com/beer");
```

When using namespaces in XML DSL then its different, as you setup the namespaces in the XML root tag (or one of the `camelContext`, `routes`, `route` tags).

In the XML example below we use Spring XML where the namespace is declared in the root tag `beans`, in the line with `xmlns:foo="http://example.com/person"`:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:foo="http://example.com/person"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

  <camelContext id="camel" xmlns="http://activemq.apache.org/camel/schema/spring">
    <route>
      <from uri="activemq:MyQueue"/>
      <filter>
        <xquery>/foo:person[@name='James']</xquery>
        <to uri="mqseries:SomeOtherQueue"/>
      </filter>
    </route>
  </camelContext>
</beans>
```

This namespace uses `foo` as prefix, so the `<xquery>` expression uses `foo:` to use this namespace.

## Using XQuery as transformation

We can do a message translation using transform or setBody in the route, as shown below:

```java
from("direct:start").
   transform().xquery("/people/person");
```

Notice that xquery will use DOMResult by default, so if we want to grab the value of the person node, using `text()` we need to tell XQuery to use String as result type, as shown:

```java
from("direct:start").
   transform().xquery("/people/person/text()", String.class);
```

If you want to use Camel variables like headers, you have to explicitly declare them in the XQuery expression.

```xml
<transform>
    <xquery>
        declare variable $in.headers.foo external;
        element item {$in.headers.foo}
    </xquery>
</transform>
```

## Loading script from external resource

You can externalize the script and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g. to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").xquery("resource:classpath:myxquery.txt", String.class)
```

## Learning XQuery

XQuery is a very powerful language for querying, searching, sorting and returning XML. For help learning XQuery try these tutorials

-   Mike Kay’s [XQuery Primer](http://www.stylusstudio.com/xquery_primer.md)
    
-   The W3Schools [XQuery Tutorial](http://www.w3schools.com/xml/xquery_intro.asp)
    

## Dependencies

To use XQuery in your camel routes you need to add the a dependency on **camel-saxon** which implements the XQuery language.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-saxon</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using xquery with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-saxon-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.xquery.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.xquery.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.xquery.configuration** | To use a custom Saxon configuration. The option is a net.sf.saxon.Configuration type. |  | Configuration |
| **camel.component.xquery.configuration-properties** | To set custom Saxon configuration properties. |  | Map |
| **camel.component.xquery.enabled** | Whether to enable auto configuration of the xquery component. This is enabled by default. |  | Boolean |
| **camel.component.xquery.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.xquery.module-u-r-i-resolver** | To use the custom ModuleURIResolver. The option is a net.sf.saxon.lib.ModuleURIResolver type. |  | ModuleURIResolver |
| **camel.language.xquery.configuration-ref** | Reference to a saxon configuration instance in the registry to use for xquery (requires camel-saxon). This may be needed to add custom functions to a saxon configuration, so these custom functions can be used in xquery expressions. |  | String |
| **camel.language.xquery.enabled** | Whether to enable auto configuration of the xquery language. This is enabled by default. |  | Boolean |
| **camel.language.xquery.namespace** | Injects the XML Namespaces of prefix - uri mappings. |  | List |
| **camel.language.xquery.property-name** | Name of property to use as input, instead of the message body. It has a lower precedent than the headerName if both are set. |  | String |
| **camel.language.xquery.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.xquery.type** | Sets the class name of the result type (type from output) The default result type is NodeSet. |  | String |