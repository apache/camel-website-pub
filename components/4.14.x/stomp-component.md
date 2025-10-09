# Stomp

**Since Camel 2.12**

**Both producer and consumer are supported**

The Stomp component is used for communicating with [Stomp](http://stomp.github.io/) compliant message brokers, like [Apache ActiveMQ](http://activemq.apache.org) or [ActiveMQ Artemis](https://activemq.apache.org/components/artemis/)

> **Note**
> Since STOMP specification is not actively maintained, please note [STOMP JMS client](https://github.com/fusesource/stompjms/tree/master/stompjms-client) is not as well actively maintained. However, we hope for the community to step up to help in maintaining the STOMP JMS project in the near future.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stomp</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

stomp:queue:destination\[?options\]

Where **destination** is the name of the queue.

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

The Stomp component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **brokerURL** (common) | **Required** The URI of the Stomp broker to connect to. | tcp://localhost:61613 | String |
| **customHeaders** (common) | To set custom headers. |  | Properties |
| **host** (common) | The virtual host name. |  | String |
| **version** (common) | The stomp version (1.1, or 1.2). |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Component configuration. |  | StompConfiguration |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **login** (security) | The username. |  | String |
| **passcode** (security) | The password. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Stomp endpoint is configured using URI syntax:

stomp:destination

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **destination** (common) | **Required** Name of the queue. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **brokerURL** (common) | **Required** The URI of the Stomp broker to connect to. | tcp://localhost:61613 | String |
| **customHeaders** (common) | To set custom headers. |  | Properties |
| **host** (common) | The virtual host name. |  | String |
| **version** (common) | The stomp version (1.1, or 1.2). |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **login** (security) | The username. |  | String |
| **passcode** (security) | The password. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Examples

Sending messages:

```java
from("direct:foo").to("stomp:queue:test");
```

Consuming messages:

```java
from("stomp:queue:test").transform(body().convertToString()).to("mock:result")
```

## Endpoints

Camel supports the Message Endpoint pattern using the [Endpoint](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.md) interface. Endpoints are usually created by a Component, and Endpoints are usually referred to in the DSL via their URIs.

From an Endpoint you can use the following methods

-   [`createProducer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createProducer--) will create a [Producer](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Producer.md) for sending message exchanges to the endpoint
    
-   [`createConsumer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createConsumer-org.apache.camel.Processor-) implements the Event Driven Consumer pattern for consuming message exchanges from the endpoint via a [`Processor`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Processor.md) when creating a [`Consumer`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Consumer.md)
    
-   [`createPollingConsumer()`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Endpoint.html#createPollingConsumer--) implements the Polling Consumer pattern for consuming message exchanges from the endpoint via a [`PollingConsumer`](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/PollingConsumer.md)
    

## Spring Boot Auto-Configuration

When using stomp with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-stomp-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.stomp.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.stomp.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.stomp.broker-url** | The URI of the Stomp broker to connect to. | tcp://localhost:61613 | String |
| **camel.component.stomp.configuration** | Component configuration. The option is a org.apache.camel.component.stomp.StompConfiguration type. |  | StompConfiguration |
| **camel.component.stomp.custom-headers** | To set custom headers. The option is a java.util.Properties type. |  | Properties |
| **camel.component.stomp.enabled** | Whether to enable auto configuration of the stomp component. This is enabled by default. |  | Boolean |
| **camel.component.stomp.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.stomp.host** | The virtual host name. |  | String |
| **camel.component.stomp.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.stomp.login** | The username. |  | String |
| **camel.component.stomp.passcode** | The password. |  | String |
| **camel.component.stomp.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.stomp.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.stomp.version** | The stomp version (1.1, or 1.2). |  | String |