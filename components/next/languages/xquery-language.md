# XQuery

**Since Camel 1.0**

Camel supports [XQuery](http://www.w3.org/TR/xquery/) to allow an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) to be used in the [DSL](../../../manual/dsl.md).

For example, you could use XQuery to create a predicate in a [Message Filter](../eips/filter-eip.md) or as an expression for a [Recipient List](../eips/recipientList-eip.md).

## XQuery Language options

The XQuery language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **configurationRef** (advanced) |  | `String` | Reference to a saxon configuration instance in the registry to use for xquery (requires camel-saxon). |
| **namespacesRef** (advanced) |  | `String` | Reference to a org.apache.camel.support.builder.Namespaces bean in the registry to use for the XML Namespaces of prefix to uri mappings. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Variables

The message body will be set as the `contextItem`. And the following variables are available as well:

  
| Variable | Type | Description |
| --- | --- | --- |
| `exchange` | Exchange | The current Exchange |
| `in.body` | Object | The message body |
| `out.body` | Object | **deprecated** The OUT message body (if any) |
| `in.headers.*` | Object | You can access the value of exchange.in.headers with key **foo** by using the variable which name is in.headers.foo |
| `out.headers.*` | Object | **deprecated** You can access the value of `exchange.out.headers` with key **foo** by using the variable which name is `out.headers.foo` variable |
| `**key name**` | Object | Any `exchange.properties` and `exchange.in.headers` and any additional parameters set using `setParameters(Map)`. These parameters are added with their own key name, for instance, if there is an IN header with the key name **foo** then it is added as **foo**. |

## Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("queue:foo")
  .filter().xquery("//foo")
  .to("queue:bar");
```

```xml
<route>
  <from uri="queue:foo"/>
  <filter>
    <xquery>//foo</xquery>
    <to uri="queue:bar"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: queue:foo
      steps:
        - filter:
            expression:
              xquery:
                expression: //foo
            steps:
              - to:
                  uri: queue:bar
```

You can also use functions inside your query, in which case you need an explicit type conversion, or you will get an `org.w3c.dom.DOMException: HIERARCHY_REQUEST_ERR`). You need to pass in the expected output type of the function. For example, the concat function returns a `String` which is done as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .recipientList().xquery("concat('mock:foo.', /person/@city)", String.class);
```

```xml
<route>
  <from uri="direct:start"/>
  <recipientList>
    <xquery resultType="java.lang.String">concat('mock:foo.', /person/@city)</xquery>
  </recipientList>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - recipientList:
            expression:
              xquery:
                expression: "concat('mock:foo.', /person/@city)"
                resultType: java.lang.String
```

### Using namespaces

If you have a standard set of namespaces you wish to work with and wish to share them across many XQuery expressions, you can use the `org.apache.camel.support.builder.Namespaces` when using Java DSL as shown:

_Java-only: programmatic namespace configuration with Namespaces builder_

```java
Namespaces ns = new Namespaces("c", "http://acme.com/cheese");

from("direct:start")
  .filter().xquery("/c:person[@name='James']", ns)
  .to("mock:result");
```

Notice how the namespaces are provided to `xquery` with the `ns` variable that are passed in as the second parameter.

Each namespace is a key=value pair, where the prefix is the key. In the XQuery expression then the namespace is used by its prefix, e.g.:

```text
/c:person[@name='James']
```

The namespace builder supports adding multiple namespaces as shown:

_Java-only: adding multiple namespaces with the Namespaces builder_

```java
Namespaces ns = new Namespaces("c", "http://acme.com/cheese")
                     .add("w", "http://acme.com/wine")
                     .add("b", "http://acme.com/beer");
```

When using namespaces in XML DSL then it is different, as you set up the namespaces in the XML root tag (or one of the `camelContext`, `routes`, `route` tags).

In the XML example below we use Spring XML where the namespace is declared in the root tag `beans`, in the line with `xmlns:foo="http://example.com/person"`:

_XML-only:_

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

### Sharing namespaces via a registry bean

Declaring the prefixes on the XML root tag only works when the route itself is written in XML. To share one set of prefix to URI mappings across several expressions, register a `org.apache.camel.support.builder.Namespaces` bean and refer to it with the `namespacesRef` option:

-   XML
    
-   YAML
    

```xml
<camel xmlns="http://camel.apache.org/schema/xml-io">

  <bean name="myNamespaces" type="org.apache.camel.support.builder.Namespaces">
    <properties>
      <property key="namespaces[c]" value="http://acme.com/cheese"/>
      <property key="namespaces[w]" value="http://acme.com/wine"/>
    </properties>
  </bean>

  <route>
    <from uri="direct:start"/>
    <filter>
      <xquery namespacesRef="myNamespaces">/c:person[@name='James']</xquery>
      <to uri="mock:result"/>
    </filter>
  </route>

</camel>
```

```yaml
- beans:
    - name: myNamespaces
      type: org.apache.camel.support.builder.Namespaces
      properties:
        namespaces[c]: "http://acme.com/cheese"
        namespaces[w]: "http://acme.com/wine"
- route:
    from:
      uri: "direct:start"
      steps:
        - filter:
            expression:
              xquery:
                expression: "/c:person[@name='James']"
                namespacesRef: "myNamespaces"
            steps:
              - to: "mock:result"
```

Each prefix is configured as a `namespaces[prefix]` property on the bean, with the namespace URI as the value. In Java DSL there is no need for this, as the `Namespaces` builder is passed to the expression directly, as shown above.

If an expression declares namespaces inline as well, then the inline namespaces win and `namespacesRef` is ignored.

## Using XQuery as transformation

We can do a message translation using transform or setBody in the route, as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start").
   transform().xquery("/people/person");
```

```xml
<route>
  <from uri="direct:start"/>
  <transform>
    <xquery>/people/person</xquery>
  </transform>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - transform:
            expression:
              xquery:
                expression: /people/person
```

Notice that xquery will use DOMResult by default, so if we want to grab the value of the person node, using `text()` we need to tell XQuery to use String as the result type, as shown:

_Java-only: specifying result type with String.class parameter_

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

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

_Java-only: loading XQuery script from classpath with class literal_

```java
.setHeader("myHeader").xquery("resource:classpath:myxquery.txt", String.class)
```

## Learning XQuery

XQuery is a very powerful language for querying, searching, sorting and returning XML. For help learning XQuery, try these tutorials

-   Mike Kay’s [XQuery Primer](http://www.stylusstudio.com/xquery_primer.md)
    
-   The W3Schools [XQuery Tutorial](http://www.w3schools.com/xml/xquery_intro.asp)
    

## Dependencies

To use XQuery in your Camel routes, you need to add the dependency on **camel-saxon**, which implements the XQuery language.

If you use Maven you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-saxon</artifactId>
  <version>x.x.x</version>
</dependency>
```