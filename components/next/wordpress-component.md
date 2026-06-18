# WordPress

**Since Camel 2.21**

**Both producer and consumer are supported**

Camel component for the [WordPress API](https://developer.wordpress.org/rest-api/reference/).

Currently only the **Posts** and **Users** operations are supported.

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

The WordPress component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (common) | The Wordpress REST API version. | 2 | String |
| **configuration** (common) | Wordpress configuration. |  | WordpressConfiguration |
| **criteria** (common) | The criteria to use with complex searches. This is a multi-value option with prefix: criteria. |  | Map |
| **force** (common) | Whether to bypass trash and force deletion. | false | boolean |
| **id** (common) | The entity ID. Should be passed when the operation performed requires a specific entity, e.g. deleting a post. |  | Integer |
| **password** (common) | Password from authorized user. |  | String |
| **searchCriteria** (common) | Search criteria. |  | SearchCriteria |
| **url** (common) | **Required** The Wordpress API URL from your site, e.g. [http://myblog.com/wp-json/](http://myblog.com/wp-json/). |  | String |
| **user** (common) | Authorized user to perform writing operations. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The WordPress endpoint is configured using URI syntax:

wordpress:operation

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (common) | 
**Required** The endpoint operation.

Enum values:

-   post
    
-   user
    





 |  | String |
| **operationDetail** (common) | 

The second part of an endpoint operation. Needed only when endpoint semantic is not enough, like wordpress:post:delete.

Enum values:

-   delete
    





 |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (common) | The Wordpress REST API version. | 2 | String |
| **criteria** (common) | The criteria to use with complex searches. This is a multi-value option with prefix: criteria. |  | Map |
| **force** (common) | Whether to bypass trash and force deletion. | false | boolean |
| **id** (common) | The entity ID. Should be passed when the operation performed requires a specific entity, e.g. deleting a post. |  | Integer |
| **password** (common) | Password from authorized user. |  | String |
| **searchCriteria** (common) | Search criteria. |  | SearchCriteria |
| **url** (common) | **Required** The Wordpress API URL from your site, e.g. [http://myblog.com/wp-json/](http://myblog.com/wp-json/). |  | String |
| **user** (common) | Authorized user to perform writing operations. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

Most of the parameters needed when performing a read operation mirrors from the official [API](https://developer.wordpress.org/rest-api/reference/). When performing searches operations, the `criteria.` suffix is needed. Take the following `Consumer` as example:

wordpress:post?criteria.perPage=10&criteria.orderBy=author&criteria.categories=camel,dozer,json

## Usage

### Configuring WordPress component

The `WordpressConfiguration` class can be used to set initial properties configuration to the component instead of passing it as query parameter. The following listing shows how to set the component to be used in your routes.

_Java-only: configuring the WordPress component programmatically_

```java
public void configure() {
    final WordpressConfiguration configuration = new WordpressConfiguration();
    final WordpressComponent component = new WordpressComponent();
    configuration.setApiVersion("2");
    configuration.setUrl("http://yoursite.com/wp-json/");
    component.setConfiguration(configuration);
    getContext().addComponent("wordpress", component);

    from("wordpress:post?id=1")
      .to("mock:result");
}
```

## Examples

### Consumer Example

Consumer polls from the API from time to time domain objects from WordPress. Following, an example using the `Post` operation:

-   `wordpress:post` retrieves posts (defaults to 10 posts)
    
-   `wordpress:post?id=1` search for a specific post
    

### Producer Example

Producer performs write operations on WordPress like adding a new user or update a post. To be able to write, you must have an authorized user credentials (see Authentication).

-   `wordpress:post` creates a new post from the `org.apache.camel.component.wordpress.api.model.Post` class in the message body.
    
-   `wordpress:post?id=1` updates a post based on data `org.apache.camel.component.wordpress.api.model.Post` from the message body.
    
-   `wordpress:post:delete?id=1` deletes a specific post
    

### Authentication

Producers that perform write operations, e.g., creating a new post, [must have an authenticated user](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/) to do so. The standard authentication mechanism used by WordPress is cookie. Unfortunately, this method is not supported outside WordPress environment because it relies on [nonce](https://codex.wordpress.org/WordPress_Nonces) internal function.

There are some alternatives to using the WordPress API without nonces, but require specific plugin installations.

At this time, `camel-wordpress` only supports Basic Authentication (more to come). To configure it, you must install the [Basic-Auth WordPress plugin](https://github.com/WP-API/Basic-Auth) and pass the credentials to the endpoint:

`from("direct:deletePost").to("wordpress:post:delete?id=9&user=ben&password=password123").to("mock:resultDelete");`

**It’s not recommended to use Basic Authentication in production without TLS!!**

## Spring Boot Auto-Configuration

When using wordpress with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-wordpress-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.wordpress.api-version** | The Wordpress REST API version. | 2 | String |
| **camel.component.wordpress.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.wordpress.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.wordpress.configuration** | Wordpress configuration. The option is a org.apache.camel.component.wordpress.WordpressConfiguration type. |  | WordpressConfiguration |
| **camel.component.wordpress.criteria** | The criteria to use with complex searches. This is a multi-value option with prefix: criteria. |  | Map |
| **camel.component.wordpress.enabled** | Whether to enable auto configuration of the wordpress component. This is enabled by default. |  | Boolean |
| **camel.component.wordpress.force** | Whether to bypass trash and force deletion. | false | Boolean |
| **camel.component.wordpress.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.wordpress.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.wordpress.id** | The entity ID. Should be passed when the operation performed requires a specific entity, e.g. deleting a post. |  | Integer |
| **camel.component.wordpress.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.wordpress.password** | Password from authorized user. |  | String |
| **camel.component.wordpress.search-criteria** | Search criteria. The option is a org.apache.camel.component.wordpress.api.model.SearchCriteria type. |  | SearchCriteria |
| **camel.component.wordpress.url** | The Wordpress API URL from your site, e.g. [http://myblog.com/wp-json/](http://myblog.com/wp-json/). |  | String |
| **camel.component.wordpress.user** | Authorized user to perform writing operations. |  | String |