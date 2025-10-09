# Knative

**Since Camel 3.15**

**Both producer and consumer are supported**

The Knative component provides support for interacting with [Knative](https://knative.dev/).

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-knative</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel K version -->
</dependency>
```

## URI format

```text
knative:type/name[?options]
```

You can append query options to the URI in the following format:

```text
?option=value&option=value&...
```

## Options

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

The Knative component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ceOverride** (common) | CloudEvent headers to override. |  | Map |
| **cloudEventsSpecVersion** (common) | 
Set the version of the cloudevents spec.

Enum values:

-   1.0
    
-   1.0.1
    





 | 1.0 | String |
| **cloudEventsType** (common) | Set the event-type information of the produced events. | org.apache.camel.event | String |
| **configuration** (common) | Set the configuration. |  | KnativeConfiguration |
| **consumerFactory** (common) | The protocol consumer factory. |  | KnativeConsumerFactory |
| **environment** (common) | The environment. |  | KnativeEnvironment |
| **environmentPath** (common) | The path ot the environment definition. |  | String |
| **filters** (common) | Set the filters. |  | Map |
| **producerFactory** (common) | The protocol producer factory. |  | KnativeProducerFactory |
| **transportOptions** (common) | Set the transport options. |  | Map |
| **typeId** (common) | The name of the service to lookup from the KnativeEnvironment. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **replyWithCloudEvent** (consumer) | Transforms the reply into a cloud event that will be processed by the caller. When listening to events from a Knative Broker, if this flag is enabled, replies will be published to the same Broker where the request comes from (beware that if you don’t change the type of the received message, you may create a loop and receive your same reply). When this flag is disabled, CloudEvent headers are removed from the reply. | false | boolean |
| **reply** (consumer (advanced)) | If the consumer should construct a full reply to knative request. | true | Boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | The version of the k8s resource referenced by the endpoint. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **kind** (advanced) | The type of the k8s resource referenced by the endpoint. |  | String |
| **name** (advanced) | The name of the k8s resource referenced by the endpoint. |  | String |

## Endpoint Options

The Knative endpoint is configured using URI syntax:

knative:type/typeId

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** (common) | 
The Knative resource type.

Enum values:

-   endpoint
    
-   channel
    
-   event
    





 |  | Type |
| **typeId** (common) | The identifier of the Knative resource. |  | String |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ceOverride** (common) | CloudEvent headers to override. |  | Map |
| **cloudEventsSpecVersion** (common) | 
Set the version of the cloudevents spec.

Enum values:

-   1.0
    
-   1.0.1
    





 | 1.0 | String |
| **cloudEventsType** (common) | Set the event-type information of the produced events. | org.apache.camel.event | String |
| **environment** (common) | The environment. |  | KnativeEnvironment |
| **filters** (common) | Set the filters. |  | Map |
| **transportOptions** (common) | Set the transport options. |  | Map |
| **replyWithCloudEvent** (consumer) | Transforms the reply into a cloud event that will be processed by the caller. When listening to events from a Knative Broker, if this flag is enabled, replies will be published to the same Broker where the request comes from (beware that if you don’t change the type of the received message, you may create a loop and receive your same reply). When this flag is disabled, CloudEvent headers are removed from the reply. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **reply** (consumer (advanced)) | If the consumer should construct a full reply to knative request. | true | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | The version of the k8s resource referenced by the endpoint. |  | String |
| **kind** (advanced) | The type of the k8s resource referenced by the endpoint. |  | String |
| **name** (advanced) | The name of the k8s resource referenced by the endpoint. |  | String |

## Supported Knative resources

The component support the following Knative resources you can target or exposes using the `type` path parameter:

-   **channel** allow producing or consuming events to or from a [**Knative Channel**](https://knative.dev/docs/eventing/channels/)
    
-   **endpoint** allow exposing or targeting serverless workloads using [**Knative Services**](https://knative.dev/docs/serving/spec/knative-api-specification-1.0/#service)
    
-   **event** allow producing or consuming events to or from a [**Knative Broker**](https://knative.dev/docs/eventing/broker)
    

## Knative Environment

As the Knative component hides the technical details of how to communicate with Knative services to the user (protocols, addresses, etc.), it needs some metadata that describe the Knative environment to set-up the low level transport details. In order to do so, the component needs a so called `Knative Environment` which is essence is a Json document made by a number of `service` elements which looks like the below example:

```json
{
    "services": [
        {
             "type": "channel|endpoint|event", (1)
             "name": "", (2)
             "metadata": {
                 "service.url": "http://my-service.svc.cluster.local" (3)
                 "knative.event.type": "", (4)
                 "camel.endpoint.kind": "source|sink", (5)
             }
        }, {
            ...
        }
    ]
}
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>the type of the Knative resource</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>the name of the resource</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>the url of the service to invoke (for producer only)</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>the Knative event type received or produced by the component</td></tr><tr><td><i class="conum" data-value="5"></i><b>5</b></td><td>the type of the Camel Endpoint associated to this Knative resource (source=consumer, sink=producer)</td></tr></tbody></table>

The `metadata` fields has some additional advanced fields:

  
| Name | Description | Example |
| --- | --- | --- |
| **filter.** | The prefix to define filters to be applied to the incoming message headers. | `` `filter.ce.source=my-source` `` |
| **knative.kind** | The type of the k8s resource referenced by the endpoint. | `` `knative.kind=InMemoryChannel` `` |
| **knative.apiVersion** | The version of the k8s resource referenced by the endpoint | `` `knative.apiVersion=messaging.knative.dev/v1beta1` `` |
| **knative.reply** | If the consumer should construct a full reply to knative request. | `` `knative.reply=false` `` |
| **ce.override.** | The prefix to define CloudEvents values that have to be overridden. | `` `ce.override.ce-type=MyType` `` |

## Example

```java
CamelContext context = new DefaultCamelContext();

KnativeComponent component = context.getComponent("knative", KnativeComponent.class);
component.getConfiguration().setEnvironmentPath("classpath:knative.json"); (1)

RouteBuilder.addRoutes(context, b -> {
    b.from("knative:endpoint/myEndpoint") (2)
        .to("log:info");
});
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>set the location of the <code>Knative Environment</code> file</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>expose knative service</td></tr></tbody></table>

## Using custom Knative Transport

As today the component only support `http` as transport as it is the only supported protocol on Knative side but the transport is pluggable by implementing the following interface:

```java
public interface KnativeTransport extends Service {
    /**
     * Create a camel {@link org.apache.camel.Producer} in place of the original endpoint for a specific protocol.
     *
     * @param endpoint the endpoint for which the producer should be created
     * @param configuration the general transport configuration
     * @param service the service definition containing information about how make reach the target service.
     */
    Producer createProducer(
        Endpoint endpoint,
        KnativeTransportConfiguration configuration,
        KnativeEnvironment.KnativeServiceDefinition service);

    /**
     * Create a camel {@link org.apache.camel.Producer} in place of the original endpoint for a specific protocol.
     *
     * @param endpoint the endpoint for which the consumer should be created.
     * @param configuration the general transport configuration
     * @param service the service definition containing information about how make the route reachable from knative.
     */
    Consumer createConsumer(
        Endpoint endpoint,
        KnativeTransportConfiguration configuration,
        KnativeEnvironment.KnativeServiceDefinition service, Processor processor);
}
```

## Using ProducerTemplate

When using Knative producer with a ProducerTemplate, it is necessary to specify a value for the CloudEvent source, simply by setting a value for the header 'CamelCloudEventSource'.

### Example

```java
producerTemplate.sendBodyAndHeader("knative:event/broker-test", body, CloudEvent.CAMEL_CLOUD_EVENT_SOURCE, "my-source-name");
```