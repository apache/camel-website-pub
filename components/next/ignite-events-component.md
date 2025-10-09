# Ignite Events

**Since Camel 2.17**

**Only consumer is supported**

The Ignite Events endpoint is one of camel-ignite endpoints which allows you to [receive events](https://apacheignite.readme.io/docs/events) from the Ignite cluster by creating a local event listener.

The Exchanges created by this consumer put the received Event object into the body of the _IN_ message.

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

The Ignite Events component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configurationResource** (consumer) | The resource from where to load the configuration. It can be a: URL, String or InputStream type. |  | Object |
| **ignite** (consumer) | To use an existing Ignite instance. |  | Ignite |
| **igniteConfiguration** (consumer) | Allows the user to set a programmatic ignite configuration. |  | IgniteConfiguration |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Ignite Events endpoint is configured using URI syntax:

ignite-events:endpointId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointId** (consumer) | The endpoint ID (not used). |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterGroupExpression** (consumer) | The cluster group expression. |  | ClusterGroupExpression |
| **events** (consumer) | The event types to subscribe to as a comma-separated string of event constants as defined in EventType. For example: EVT\_CACHE\_ENTRY\_CREATED,EVT\_CACHE\_OBJECT\_REMOVED,EVT\_IGFS\_DIR\_CREATED. | EVTS\_ALL | String |
| **propagateIncomingBodyIfNoReturnValue** (consumer) | Sets whether to propagate the incoming body if the return type of the underlying Ignite operation is void. | true | boolean |
| **treatCollectionsAsCacheObjects** (consumer) | Sets whether to treat Collections as cache objects or as Collections of items to insert/update/compute, etc. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Spring Boot Auto-Configuration

When using ignite-events with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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
| **camel.component.ignite-cache.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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
| **camel.component.ignite-events.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ignite-events.enabled** | Whether to enable auto configuration of the ignite-events component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-events.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-events.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-idgen.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-idgen.enabled** | Whether to enable auto configuration of the ignite-idgen component. This is enabled by default. |  | Boolean |
| **camel.component.ignite-idgen.ignite** | To use an existing Ignite instance. The option is a org.apache.ignite.Ignite type. |  | Ignite |
| **camel.component.ignite-idgen.ignite-configuration** | Allows the user to set a programmatic ignite configuration. The option is a org.apache.ignite.configuration.IgniteConfiguration type. |  | IgniteConfiguration |
| **camel.component.ignite-idgen.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.ignite-messaging.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ignite-messaging.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
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