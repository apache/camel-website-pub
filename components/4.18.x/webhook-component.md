# Webhook

**Since Camel 3.0**

**Only consumer is supported**

The Webhook meta-component allows other Camel components to configure webhooks on a remote webhook provider and listen for them.

The following components currently provide webhook endpoints:

-   [Camel Telegram](telegram-component.md)
    
-   [Camel WhatsApp](whatsapp-component.md)
    

Maven users can add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-webhook</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Typically, other components that support webhook will bring this dependency transitively.

## URI Format

webhook:endpoint\[?options\]

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

The Webhook component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **webhookAutoRegister** (consumer) | Automatically register the webhook at startup and unregister it on shutdown. | true | boolean |
| **webhookBasePath** (consumer) | The first (base) path element where the webhook will be exposed. It’s a good practice to set it to a random string, so that it cannot be guessed by unauthorized parties. |  | String |
| **webhookComponentName** (consumer) | The Camel Rest component to use for the REST transport, such as netty-http. |  | String |
| **webhookExternalUrl** (consumer) | The URL of the current service as seen by the webhook provider. |  | String |
| **webhookPath** (consumer) | The path where the webhook endpoint will be exposed (relative to basePath, if any). |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Set the default configuration for the webhook meta-component. |  | WebhookConfiguration |

## Endpoint Options

The Webhook endpoint is configured using URI syntax:

webhook:endpointUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointUri** (consumer) | **Required** The delegate uri. Must belong to a component that supports webhooks. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **webhookAutoRegister** (consumer) | Automatically register the webhook at startup and unregister it on shutdown. | true | boolean |
| **webhookBasePath** (consumer) | The first (base) path element where the webhook will be exposed. It’s a good practice to set it to a random string, so that it cannot be guessed by unauthorized parties. |  | String |
| **webhookComponentName** (consumer) | The Camel Rest component to use for the REST transport, such as netty-http. |  | String |
| **webhookExternalUrl** (consumer) | The URL of the current service as seen by the webhook provider. |  | String |
| **webhookPath** (consumer) | The path where the webhook endpoint will be exposed (relative to basePath, if any). |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Examples

Examples of the webhook component are provided in the documentation of the delegate components that support it.

## Spring Boot Auto-Configuration

When using webhook with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-webhook-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.webhook.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.webhook.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.webhook.configuration** | Set the default configuration for the webhook meta-component. The option is a org.apache.camel.component.webhook.WebhookConfiguration type. |  | WebhookConfiguration |
| **camel.component.webhook.enabled** | Whether to enable auto configuration of the webhook component. This is enabled by default. |  | Boolean |
| **camel.component.webhook.webhook-auto-register** | Automatically register the webhook at startup and unregister it on shutdown. | true | Boolean |
| **camel.component.webhook.webhook-base-path** | The first (base) path element where the webhook will be exposed. It’s a good practice to set it to a random string, so that it cannot be guessed by unauthorized parties. |  | String |
| **camel.component.webhook.webhook-component-name** | The Camel Rest component to use for the REST transport, such as netty-http. |  | String |
| **camel.component.webhook.webhook-external-url** | The URL of the current service as seen by the webhook provider. |  | String |
| **camel.component.webhook.webhook-path** | The path where the webhook endpoint will be exposed (relative to basePath, if any). |  | String |