# XQuery

**Since Camel 1.0**

**Only producer is supported**

Camel supports [XQuery](http://www.w3.org/TR/xquery/) component for message transformation

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

The XQuery component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **configurationProperties** (advanced) | To set custom Saxon configuration properties. |  | Map |
| **moduleURIResolver** (advanced) | To use the custom ModuleURIResolver. |  | ModuleURIResolver |

## Endpoint Options

The XQuery endpoint is configured using URI syntax:

xquery:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** The name of the template to load from classpath or file system. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowStAX** (producer) | Whether to allow using StAX mode. | false | boolean |
| **namespacePrefixes** (producer) | Allows to control which namespace prefixes to use for a set of namespace mappings. |  | Map |
| **resultsFormat** (producer) | 
What output result to use.

Enum values:

-   Bytes
    
-   BytesSource
    
-   DOM
    
-   DOMSource
    
-   List
    
-   String
    
-   StringSource
    





 | DOM | ResultFormat |
| **resultType** (producer) | What output result to use defined as a class. |  | Class |
| **source** (producer) | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **stripsAllWhiteSpace** (producer) | Whether to strip all whitespaces. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **configuration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **configurationProperties** (advanced) | To set custom Saxon configuration properties. |  | Map |
| **moduleURIResolver** (advanced) | To use the custom ModuleURIResolver. |  | ModuleURIResolver |
| **parameters** (advanced) | Additional parameters. |  | Map |
| **properties** (advanced) | Properties to configure the serialization parameters. |  | Properties |
| **staticQueryContext** (advanced) | To use a custom Saxon StaticQueryContext. |  | StaticQueryContext |

## Message Body

The message body at each side of the XQuery component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream`, `file` or `pojo`, as xml | The XML to query: text, bytes, a stream, a file, a DOM or another javax.xml.transform.Source. A Map or no body fails.
Not known when `source` is set.

 |
| **Producer output** | `pojo` (`org.w3c.dom.Document`) | The result of the query as a DOM Document. A query that gives text, a number or more than one element fails with the default DOM: set resultsFormat to String or List.

-   With `resultsFormat=Bytes`: `bytes` (`byte[]`)
    
-   With `resultsFormat=BytesSource`: `pojo` (`org.apache.camel.util.xml.BytesSource`)
    
-   With `resultsFormat=DOMSource`: `text` (`java.lang.String`)
    
-   With `resultsFormat=List`: `list`
    
-   With `resultsFormat=String`: `text` (`java.lang.String`)
    
-   With `resultsFormat=StringSource`: `pojo` (`org.apache.camel.util.xml.StringSource`)
    

Not known when `resultType` is set.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Examples

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
            xquery:
              expression: //foo
            steps:
              - to:
                  uri: queue:bar
```

You can also use functions inside your query, in which case you need an explicit type conversion (otherwise you will get a `org.w3c.dom.DOMException: HIERARCHY_REQUEST_ERR`), by passing the Class as a second argument to the **xquery()** method.

_Java-only: xquery() with class literal parameter_

```java
from("direct:start")
  .recipientList().xquery("concat('mock:foo.', /person/@city)", String.class);
```

## Usage

### Variables

The IN message body will be set as the `contextItem`. Besides this, these Variables are also added as parameters:

  
| Variable | Type | Description |
| --- | --- | --- |
| `exchange` | Exchange | The current Exchange |
| `in.body` | Object | The In message’s body |
| `out.body` | Object | The OUT message’s body (if any) |
| `in.headers.*` | Object | You can access the value of exchange.in.headers with key **foo** by using the variable which name is in.headers.foo |
| `out.headers.*` | Object | You can access the value of exchange.out.headers with key **foo** by using the variable which name is out.headers.foo variable |
| `**key name**` | Object | Any exchange.properties and exchange.in.headers and any additional parameters set using `setParameters(Map)`. These parameters are added with their own key name, for instance, if there is an IN header with the key name **foo** then it is added as **foo**. |

### Using XML configuration

If you prefer to configure your routes in your Spring XML file, then you can use XPath expressions as follows

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:MyQueue")
    .filter().xquery("/foo:person[@name='James']")
        .to("mqseries:SomeOtherQueue");
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:foo="http://example.com/person"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

  <camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
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

```yaml
- route:
    from:
      uri: activemq:MyQueue
      steps:
        - filter:
            xquery:
              expression: "/foo:person[@name='James']"
            steps:
              - to:
                  uri: mqseries:SomeOtherQueue
```

Notice how we can reuse the namespace prefixes, **foo** in this case, in the XPath expression for easier namespace-based XQuery expressions!

When you use functions in your XQuery expression, you need an explicit type conversion which is done in the xml configuration via the **resultType** attribute:

```xml
<xquery resultType="java.lang.String">concat('mock:foo.', /person/@city)</xquery>
```

### Using XQuery as an endpoint

Sometimes an XQuery expression can be quite large; it can essentially be used for Templating. So you may want to use an XQuery Endpoint, so you can route using XQuery templates.

The following example shows how to take a message of an ActiveMQ queue (MyQueue) and transform it using XQuery and send it to MQSeries.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:MyQueue")
    .to("xquery:com/acme/someTransform.xquery")
    .to("mqseries:SomeOtherQueue");
```

```xml
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="activemq:MyQueue"/>
    <to uri="xquery:com/acme/someTransform.xquery"/>
    <to uri="mqseries:SomeOtherQueue"/>
  </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: activemq:MyQueue
      steps:
        - to:
            uri: xquery:com/acme/someTransform.xquery
        - to:
            uri: mqseries:SomeOtherQueue
```

### Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

_Java-only: setHeader with xquery() and class literal_

```java
.setHeader("myHeader").xquery("resource:classpath:myxquery.txt", String.class)
```

### Learning XQuery

XQuery is a very powerful language for querying, searching, sorting and returning XML. For help learning XQuery, try these tutorials

-   Mike Kay’s [XQuery Primer](http://www.stylusstudio.com/xquery_primer.md)
    
-   The W3Schools [XQuery Tutorial](https://www.w3schools.com/xml/xquery_intro.asp)
    

## Dependencies

To use XQuery in your Camel routes, you need to add the dependency on **camel-saxon**, which implements the XQuery language.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-saxon</artifactId>
  <version>x.x.x</version>
</dependency>
```