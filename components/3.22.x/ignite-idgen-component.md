# Ignite ID Generator

**Since Camel 2.17**

**Only producer is supported**

The Ignite ID Generator endpoint is one of camel-ignite endpoints which allows you to interact with [Ignite Atomic Sequences and ID Generators](https://apacheignite.readme.io/docs/id-generator).

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Ignite ID Generator component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationResource** (producer) | The resource from where to load the configuration. It can be a: URL, String or InputStream type. |  | Object |
| **ignite** (producer) | To use an existing Ignite instance. |  | Ignite |
| **igniteConfiguration** (producer) | Allows the user to set a programmatic ignite configuration. |  | IgniteConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Ignite ID Generator endpoint is configured using URI syntax:

ignite-idgen:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** The sequence name. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **batchSize** (producer) | The batch size. |  | Integer |
| **initialValue** (producer) | The initial value. | 0 | Long |
| **operation** (producer) | 
The operation to invoke on the Ignite ID Generator. Superseded by the IgniteConstants.IGNITE\_IDGEN\_OPERATION header in the IN message. Possible values: ADD\_AND\_GET, GET, GET\_AND\_ADD, GET\_AND\_INCREMENT, INCREMENT\_AND\_GET.

Enum values:

-   ADD\_AND\_GET
    
-   GET
    
-   GET\_AND\_ADD
    
-   GET\_AND\_INCREMENT
    
-   INCREMENT\_AND\_GET
    





 |  | IgniteIdGenOperation |
| **propagateIncomingBodyIfNoReturnValue** (producer) | Sets whether to propagate the incoming body if the return type of the underlying Ignite operation is void. | true | boolean |
| **treatCollectionsAsCacheObjects** (producer) | Sets whether to treat Collections as cache objects or as Collections of items to insert/update/compute, etc. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Ignite ID Generator component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIgniteIdGenOperation** (producer) Constant: [`IGNITE_IDGEN_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_IDGEN_OPERATION) | 
Allows you to dynamically change the ID Generator operation.

Enum values:

-   ADD\_AND\_GET
    
-   GET
    
-   GET\_AND\_ADD
    
-   GET\_AND\_INCREMENT
    
-   INCREMENT\_AND\_GET
    





 |  | IgniteIdGenOperation |

## Spring Boot Auto-Configuration

When using ignite-idgen with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ignite-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 37 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ignite-cache.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-cache.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ignite-cache.enabled** | Whether to enable auto configuration of the ignite-cache component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-cache.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-cache.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-cache.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-compute.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-compute.enabled** | Whether to enable auto configuration of the ignite-compute component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-compute.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-compute.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-compute.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-events.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-events.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ignite-events.enabled** | Whether to enable auto configuration of the ignite-events component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-events.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-events.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-idgen.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-idgen.enabled** | Whether to enable auto configuration of the ignite-idgen component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-idgen.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-idgen.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-idgen.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-messaging.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-messaging.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ignite-messaging.enabled** | Whether to enable auto configuration of the ignite-messaging component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-messaging.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-messaging.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-messaging.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-queue.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-queue.enabled** | Whether to enable auto configuration of the ignite-queue component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-queue.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-queue.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-queue.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-set.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-set.enabled** | Whether to enable auto configuration of the ignite-set component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-set.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-set.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-set.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |