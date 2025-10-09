# Smooks

**Since Camel 4.7**

**Only producer is supported**

The Camel Smooks component uses [Smooks](https://www.smooks.org/) to break up the structured data (EDI, CSV, POJO, etc…​) of a Camel message body into fragments. These fragments can be processed independently of one another from within Smooks.

Common applications of Smooks include:

-   transformation: EDI to CSV, POJO to EDI, POJO to XML, and so on.
    
-   scalable processing: process huge payloads while keeping a small memory footprint.
    
-   split, transform, and route fragments to destinations such as JMS queues, file systems, and databases.
    
-   enrichment: enrich fragments with data from a database or other data sources.
    
-   Java binding: populate POJOs from a source such as CSV, EDI, XML, and other POJOs.
    

Use the [Smooks Data Format](dataformats/smooks-dataformat.md) instead of this component when you are primarily interested in transformation and binding. This should be used for other Smooks features, like routing.

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-smooks</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

smooks://smooks-config-path\[?options\]

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

The Smooks component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **smooksFactory** (advanced) | **Autowired** To use a custom factory for creating Smooks. |  | SmooksFactory |

## Endpoint Options

The Smooks endpoint is configured using URI syntax:

smooks:smooksConfig

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **smooksConfig** (producer) | **Required** Path to the Smooks configuration file. |  | String |

### Query Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **reportPath** (producer) | File path to place the generated HTML execution report. The report is a useful tool in the developers arsenal for diagnosing issues or comprehending a transformation. Do not set in production since this is a major performance drain. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowExecutionContextFromHeader** (advanced) | Allow execution context to be set from the CamelSmooksExecutionContext header. | false | Boolean |

## Message Headers

The Smooks component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSmooksExecutionContext** (advanced) Constant: [`SMOOKS_EXECUTION_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-smooks/latest/org/apache/camel/component/smooks/SmooksConstants.html#SMOOKS_EXECUTION_CONTEXT) | The Smooks execution context. |  | ExecutionContext |

## Usage

Using the Smooks component lets you leverage all the features of Smooks, such as transformation and fragment-driven routing, from within Camel. You can take an existing Smooks configuration and reference it from your Camel routes as shown below:

-   Java
    
-   YAML
    

```java
from("file:inputDir?noop=true")
    .to("smooks:smooks-config.xml")
    .to("jms:queue:order");
```

```yaml
- from:
    uri: file:inputDir?noop=true
    steps:
      - to: smooks:smooks-config.xml
      - to: jms:queue:order
```

The Smooks component is configured with a mandatory configuration file, which is `smooks-config.xml` in the example above. It is not clear what type of output the component is producing from looking at the above route. By default, the message body output is a stream but the type of output can be changed by configuring `{https://www.smooks.org/xsd/smooks/smooks-core-1.6.xsd}exports` in the Smooks configuration as shown next:

smooks-config.xml

```xml
<smooks-resource-list xmlns="https://www.smooks.org/xsd/smooks-2.0.xsd"
        xmlns:edi="https://www.smooks.org/xsd/smooks/edi-2.0.xsd"
        xmlns:core="https://www.smooks.org/xsd/smooks/smooks-core-1.6.xsd">

    <core:exports>
        <core:result type="org.smooks.io.sink.StringSink"/>
    </core:exports>

    <edi:parser schemaUri="/edi-mapping-model.dfdl.xsd" segmentTerminator="%NL;" dataElementSeparator="*"
                compositeDataElementSeparator="^"/>

</smooks-resource-list>
```

The `{https://www.smooks.org/xsd/smooks/smooks-core-1.6.xsd}exports` element in this example configures Smooks to export the execution result to Camel as a string. Keep in mind that exporting the result as string means that the whole result will be kept in-memory which could cause unexpected performance issues for large payloads.

### Bean routing

Smooks is capable of routing fragments to Camel endpoints using the `{https://www.smooks.org/xsd/smooks/camel-1.5.xsd}route` element from the Smooks configuration. As an example, you can route to an endpoint by declaring the following in your Smooks configuration:

smooks-config.xml

```xml
<smooks-resource-list xmlns="https://www.smooks.org/xsd/smooks-2.0.xsd"
                      xmlns:jb="https://www.smooks.org/xsd/smooks/javabean-1.6.xsd"
                      xmlns:camel="https://www.smooks.org/xsd/smooks/camel-1.5.xsd">

  <!-- Create some bean instances from the input source... -->
  <jb:bean beanId="orderItem"  ...>
    <!-- etc... See Smooks Java Binding docs -->
  </jb:bean>

  <!-- Route bean to camel endpoints... -->
  <camel:route beanId="orderItem">
    <camel:to endpoint="direct:slow" if="orderItem.priority == 'Normal'"/>
    <camel:to endpoint="direct:express" if="orderItem.priority == 'High'"/>
  </camel:route>

</smooks-resource-list>
```

The file above configures Smooks to route the Java bean `orderItem` in the [bean context](https://www.smooks.org/documentation/#bean_context) to the endpoints `direct:slow` and `direct:express`, depending on whether the `priority` field of the `orderItem` instance is equal to `Normal` or `High`. It is possible to route based on an event selector rather than a condition thanks to the `routeOnElement` XML attribute:

smooks-config.xml

```xml
<smooks-resource-list xmlns="https://www.smooks.org/xsd/smooks-2.0.xsd"
                      xmlns:jb="https://www.smooks.org/xsd/smooks/javabean-1.6.xsd"
                      xmlns:camel="https://www.smooks.org/xsd/smooks/camel-1.5.xsd">

  <!-- Create some bean instances from the input source... -->
  <jb:bean beanId="orderItem"  ...>
    <!-- etc... See Smooks Java Binding docs -->
  </jb:bean>

  <!-- Route bean to camel endpoints... -->
  <camel:route beanId="orderItem" routeOnElement="order">
    <camel:to endpoint="direct:all"/>
  </camel:route>

</smooks-resource-list>
```

> **Note**
> instead of routing complex objects to Camel, a [pipeline](https://www.smooks.org/documentation/#pipeline) allows you to have a template (e.g., FreeMarker) reference the beans and then route the evaluated template as string (e.g., XML, CSV, etc.) to Camel.