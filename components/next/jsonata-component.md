# JSONata

**Since Camel 3.5**

**Only producer is supported**

The Jsonata component allows you to process JSON messages using the [JSONATA](https://jsonata.org/) specification. This can be ideal when doing JSON to JSON transformation and other transformations from JSON.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jsonata</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jsonata:specName\[?options\]

Where **specName** is the classpath-local URI of the specification to invoke; or the complete URL of the remote specification (e.g.: `file://folder/myfile.vm`).

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

The JSONata component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **frameBinding** (advanced) | To configure custom frame bindings and inject user functions. |  | JsonataFrameBinding |

## Endpoint Options

The JSONata endpoint is configured using URI syntax:

jsonata:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **inputType** (producer) | 
Specifies if the input should be Jackson JsonNode or a JSON String.

Enum values:

-   Jackson
    
-   JsonString
    





 | Jackson | JsonataInputOutputType |
| **outputType** (producer) | 

Specifies if the output should be Jackson JsonNode or a JSON String.

Enum values:

-   Jackson
    
-   JsonString
    





 | Jackson | JsonataInputOutputType |
| **prettyPrint** (producer) | Whether to pretty print JSon output when using string as output type. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **frameBinding** (advanced) | To configure the Jsonata frame binding. Allows custom functions to be added. |  | JsonataFrameBinding |

## Examples

### Basic

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("jsonata:com/acme/MyResponse.json");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="jsonata:com/acme/MyResponse.json"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: jsonata:com/acme/MyResponse.json
```

And a file-based resource:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("jsonata:file://myfolder/MyResponse.json?contentCache=true")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="jsonata:file://myfolder/MyResponse.json?contentCache=true"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: jsonata:file://myfolder/MyResponse.json
            parameters:
              contentCache: true
        - to:
            uri: activemq:Another.Queue
```

### Frame bindings

It is possible to configure custom functions that can be called from Jsonata. For example you might want to be able to inject environment variables:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("jsonata:file://myfolder/MyResponse.json?contentCache=true&frameBinding=#customBindings")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="jsonata:file://myfolder/MyResponse.json?contentCache=true&amp;frameBinding=#customBindings"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: jsonata:file://myfolder/MyResponse.json
            parameters:
              contentCache: true
              frameBinding: "#customBindings"
        - to:
            uri: activemq:Another.Queue
```

A custom binding might look like the following:

_Java-only: implementing a custom JsonataFrameBinding_

```java
@NoArgsConstructor
public class CustomJsonataFrameBinding implements JsonataFrameBinding {
  @Override
  public void bindToFrame(Jsonata.Frame frame) {
    frame.bind("env", (String s) -> System.getenv(s));
  }
}
```

## Spring Boot Auto-Configuration

When using jsonata with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jsonata-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jsonata.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.jsonata.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jsonata.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.jsonata.enabled** | Whether to enable auto configuration of the jsonata component. This is enabled by default. |  | Boolean |
| **camel.component.jsonata.frame-binding** | To configure custom frame bindings and inject user functions. The option is a org.apache.camel.component.jsonata.JsonataFrameBinding type. |  | JsonataFrameBinding |
| **camel.component.jsonata.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |