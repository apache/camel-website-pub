# Language

**Since Camel 2.5**

**Only producer is supported**

The Language component allows you to send `Exchange` to an endpoint which executes a script by any of the supported Languages in Camel.

By having a component to execute language scripts, it allows more dynamic routing capabilities. For example, by using the Routing Slip or [Dynamic Router](eips/dynamicRouter-eip.md) EIPs you can send messages to `language` endpoints where the script is dynamically defined as well.

You only have to include additional Camel components if the language of choice mandates it, such as using [Groovy](languages/groovy-language.md) or [JavaScript](languages/groovy-language.md) languages.

## URI format

language://languageName\[:script\]\[?options\]

You can refer to an external resource for the script using the same notation as supported by the other [Language](#)s in Camel

language://languageName:resource:scheme:location\]\[?options\]

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

The Language component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Language endpoint is configured using URI syntax:

language:languageName:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **languageName** (producer) | 
**Required** Sets the name of the language to use.

Enum values:

-   bean
    
-   constant
    
-   csimple
    
-   datasonnet
    
-   exchangeProperty
    
-   file
    
-   groovy
    
-   header
    
-   hl7terser
    
-   java
    
-   joor
    
-   jq
    
-   js
    
-   jsonpath
    
-   mvel
    
-   ognl
    
-   python
    
-   ref
    
-   simple
    
-   spel
    
-   tokenize
    
-   variable
    
-   wasm
    
-   xpath
    
-   xquery
    
-   xtokenize
    





 |  | String |
| **resourceUri** (producer) | Path to the resource, or a reference to lookup a bean in the Registry to use as the resource. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **resultType** (producer) | Sets the class of the result type (type from output). |  | String |
| **script** (producer) | Sets the script to execute. |  | String |
| **transform** (producer) | Whether or not the result of the script should be used as message body. This options is default true. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **binary** (advanced) | Whether the script is binary content or text content. By default the script is read as text content (eg java.lang.String). | false | boolean |
| **cacheScript** (advanced) | Whether to cache the compiled script and reuse Notice reusing the script can cause side effects from processing one Camel org.apache.camel.Exchange to the next org.apache.camel.Exchange. | false | boolean |

## Message Headers

The Language component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLanguageScript** (producer) Constant: [`LANGUAGE_SCRIPT`](https://javadoc.io/doc/org.apache.camel/camel-language/latest/org/apache/camel/component/language/LanguageConstants.html#LANGUAGE_SCRIPT) | The script to execute provided in the header. Takes precedence over script configured on the endpoint. |  | String or Expression |

## Examples

For example, you can use the [Simple](languages/simple-language.md) language as [Message Translator](eips/message-translator.md) EIP:

```java
from("direct:hello")
    .to("language:simple:Hello ${body}")
```

In case you want to convert the message body type, you can do this as well. However, it is better to use [Convert Body To](eips/convertBodyTo-eip.md):

```java
from("direct:toString")
    .to("language:simple:${bodyAs(String.class)}")
```

You can also use the [Groovy](languages/groovy-language.md) language, such as this example where the input message will be multiplied with 2:

```groovy
from("direct:double")
    .to("language:groovy:${body} * 2}")
```

You can also provide the script as a header as shown below. Here we use [XPath](languages/xpath-language.md) language to extract the text from the `<foo>` tag.

```java
Object out = producer.requestBodyAndHeader("language:xpath", "<foo>Hello World</foo>", Exchange.LANGUAGE_SCRIPT, "/foo/text()");
assertEquals("Hello World", out);
```

## Loading scripts from resources

You can specify a resource uri for a script to load in either the endpoint uri, or in the `Exchange.LANGUAGE_SCRIPT` header. The uri must start with one of the following schemes: `file:`, `classpath:`, or `http:`

```java
from("direct:start")
        // load the script from the classpath
        .to("language:simple:resource:classpath:org/apache/camel/component/language/mysimplescript.txt")
        .to("mock:result");
```

By default, the script is loaded once and cached. However, you can disable the `contentCache` option and have the script loaded on each evaluation. For example, if the file `myscript.txt` is changed on disk, then the updated script is used:

```java
from("direct:start")
        // the script will be loaded on each message, as we disabled cache
        .to("language:simple:myscript.txt?contentCache=false")
        .to("mock:result");
```

You can also refer to the script as a resource similar to how all the other [Language](#)s in Camel functions, by prefixing with `resource:` as shown below:

```java
from("direct:start")
    .to("language:constant:resource:classpath:org/apache/camel/component/language/hello.txt")
    .to("mock:result");
```

## Spring Boot Auto-Configuration

When using language with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-language-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.language.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.language.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.language.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.language.enabled** | Whether to enable auto configuration of the language component. This is enabled by default. |  | Boolean |
| **camel.component.language.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |