# Grape

> **Warning**
> **Deprecated:** This grape is deprecated and may be removed in a future release.

**Since Camel 2.16**

**Only producer is supported**

> **Note**
> This component is deprecated since Camel 4.1 and will be removed in a future release.

[Grape](http://docs.groovy-lang.org/latest/html/documentation/grape.md) component allows you to fetch, load and manage additional jars when `CamelContext` is running. In practice with the Camel Grape component you can add new components, data formats and beans to your `CamelContext` without the restart of the router.

## Grape options

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

The Grape component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **patchesRepository** (advanced) | Implementation of org.apache.camel.component.grape.PatchesRepository, by default: FilePatchesRepository. |  | PatchesRepository |

## Endpoint Options

The Grape endpoint is configured using URI syntax:

grape:defaultCoordinates

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultCoordinates** (producer) | **Required** Maven coordinates to use as default to grab if the message body is empty. |  | String |

### Query Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Grape component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGrapeCommand** (producer) Constant: [`GRAPE_COMMAND`](https://javadoc.io/doc/org.apache.camel/camel-grape/latest/org/apache/camel/component/grape/GrapeConstants.html#GRAPE_COMMAND) | 
The command to be performed by the Grape endpoint.

Enum values:

-   grab
    
-   listPatches
    
-   clearPatches
    





 | grab | GrapeCommand |

## Setting up class loader

Grape requires using Groovy class loader with the `CamelContext`. You can enable Groovy class loading on the existing Camel Context using the `GrapeComponent#grapeCamelContext()` method:

```java
import static org.apache.camel.component.grape.GrapeComponent.grapeCamelContext;
...
CamelContext camelContext = grapeCamelContext(new DefaultCamelContext());
```

You can also set up the Groovy class loader used by the Camel context by yourself:

```java
camelContext.setApplicationContextClassLoader(new GroovyClassLoader(myClassLoader));
```

For example, the following snippet loads Camel FTP component:

```java
from("direct:loadCamelFTP").
  to("grape:org.apache.camel/camel-ftp/2.15.2");
```

You can also specify the Maven coordinates by sending them to the endpoint as the exchange body:

```java
from("direct:loadCamelFTP").
  setBody().constant("org.apache.camel/camel-ftp/2.15.2").
  to("grape:defaultMavenCoordinates");
```

## Adding the Grape component to the project

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-grape</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Default payload type

By default, the Camel Grape component operates on the String payloads:

```java
producerTemplate.sendBody("grape:defaultMavenCoordinates", "org.apache.camel/camel-ftp/2.15.2");
```

Of course, Camel build-in [type conversion API](../../manual/type-converter.md) can perform the automatic data type transformations for you. In the example below, Camel automatically converts binary payload into the String:

```java
producerTemplate.sendBody("grape:defaultMavenCoordinates", "org.apache.camel/camel-ftp/2.15.2".getBytes());
```

## Loading components at runtime

To load the new component at the router runtime, just grab the jar containing the given component:

```java
ProducerTemplate template = camelContext.createProducerTemplate();
template.sendBody("grape:grape", "org.apache.camel/camel-stream/2.15.2");
template.sendBody("stream:out", "msg");
```

## Loading processors bean at runtime

To load the new processor bean with your custom business login at the router runtime, just grab the jar containing the required bean:

```java
ProducerTemplate template = camelContext.createProducerTemplate();
template.sendBody("grape:grape", "com.example/my-business-processors/1.0");
int productId = 1;
int price = template.requestBody("bean:com.example.PricingBean?method=currentProductPrice", productId, int.class)
```

## Loading deployed jars after Camel context restart

After you download new jar, you usually would like to have it loaded by the Camel again after the restart of the `CamelContext`. It is certainly possible, as Grape component keeps track of the jar files you have installed. To load again the installed jars on the context startup, use the `GrapeEndpoint.loadPatches()` method in your route:

```java
import static org.apache.camel.component.grape.GrapeEndpoint.loadPatches;

...
camelContext.addRoutes(
  new RouteBuilder() {
    @Override
    public void configure() throws Exception {
      loadPatches(camelContext);

      from("direct:loadCamelFTP").
        to("grape:org.apache.camel/camel-ftp/2.15.2");
    }
  });
```

## Managing the installed jars

If you would like to check what jars have been installed into the given `CamelContext`, send a message to the grape endpoint with the `CamelGrapeCommand` header set to `GrapeCommand.listPatches`:

```java
from("netty-http:http://0.0.0.0:80/patches").
    setHeader(GrapeConstats.GRAPE_COMMAND, constant(CamelGrapeCommand.listPatches)).
    to("grape:list");
```

Connecting to the route defined above using the HTTP client returns the list of the jars installed by Grape component:

```bash
$ curl http://my-router.com/patches
grape:org.apache.camel/camel-ftp/2.15.2
grape:org.apache.camel/camel-jms/2.15.2
```

If you would like to remove the installed jars, so these won’t be loaded again after the context restart, use the `GrapeCommand.``clearPatches` command:

```java
from("netty-http:http://0.0.0.0:80/patches").
    setHeader(GrapeConstats.GRAPE_COMMAND, constant(CamelGrapeCommand.clearPatches)).
    setBody().constant("Installed patches have been deleted.");
```

## Spring Boot Auto-Configuration

When using grape with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-grape-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.grape.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.grape.enabled** | Whether to enable auto configuration of the grape component. This is enabled by default. |  | Boolean |
| **camel.component.grape.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.grape.patches-repository** | Implementation of org.apache.camel.component.grape.PatchesRepository, by default: FilePatchesRepository. The option is a org.apache.camel.component.grape.PatchesRepository type. |  | PatchesRepository |