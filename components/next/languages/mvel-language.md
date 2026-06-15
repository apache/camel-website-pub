# MVEL

**Since Camel 2.0**

Camel supports [MVEL](http://mvel.documentnode.com/) to do message transformations using MVEL templates.

MVEL is powerful for templates, but can also be used for [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md)

For example, you can use MVEL in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

You can use MVEL dot notation to invoke operations. If you for instance have a body that contains a POJO that has a `getFamilyName` method then you can construct the syntax as follows:

```text
request.body.familyName
```

Or use similar syntax as in Java:

```java
getRequest().getBody().getFamilyName()
```

## MVEL Options

The MVEL language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Variables

The following Camel related variables are made available:

  
| Variable | Type | Description |
| --- | --- | --- |
| **this** | Exchange | the Exchange is the root object |
| context | CamelContext | the CamelContext |
| exchange | Exchange | the Exchange |
| exchangeId | String | the exchange id |
| exception | Throwable | the Exchange exception (if any) |
| request | Message | the message |
| message | Message | the message |
| headers | Map | the message headers |
| header(name) | Object | the message header by the given name |
| header(name, type) | Type | the message header by the given name as the given type |
| properties | Map | the exchange properties |
| property(name) | Object | the exchange property by the given name |
| property(name, type) | Type | the exchange property by the given name as the given type |

## Example

For example, you could use MVEL inside a [Message Filter](../eips/filter-eip.md)

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo")
  .filter().mvel("headers.foo == 'bar'")
    .to("seda:bar");
```

```xml
<route>
  <from uri="seda:foo"/>
  <filter>
    <mvel>headers.foo == 'bar'</mvel>
    <to uri="seda:bar"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: seda:foo
      steps:
        - filter:
            expression:
              mvel:
                expression: headers.foo == 'bar'
            steps:
              - to:
                  uri: seda:bar
```

## Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").mvel("resource:classpath:script.mvel")
```

## Dependencies

To use MVEL in your Camel routes, you need to add the dependency on **camel-mvel** which implements the MVEL language.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-mvel</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using mvel with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mvel-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mvel.allow-context-map-all** | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | Boolean |
| **camel.component.mvel.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.mvel.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mvel.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.mvel.enabled** | Whether to enable auto configuration of the mvel component. This is enabled by default. |  | Boolean |
| **camel.component.mvel.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.language.mvel.enabled** | Whether to enable auto configuration of the mvel language. This is enabled by default. |  | Boolean |
| **camel.language.mvel.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |