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
    <!-- use the same version as your Camel version -->
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

The Knative component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ceOverride** (common) | CloudEvent headers to override. |  | Map |
| **cloudEventsSpecVersion** (common) | 
Set the version of the cloudevents spec.

Enum values:

-   1.0
    
-   1.0.1
    
-   1.0.2
    





 | 1.0 | String |
| **cloudEventsType** (common) | Set the event-type information of the produced events. | org.apache.camel.event | String |
| **configuration** (common) | Set the configuration. |  | KnativeConfiguration |
| **consumerFactory** (common) | The protocol consumer factory. |  | KnativeConsumerFactory |
| **environment** (common) | The environment. |  | KnativeEnvironment |
| **environmentPath** (common) | The path ot the environment definition. |  | String |
| **filters** (common) | Set the filters. |  | Map |
| **producerFactory** (common) | The protocol producer factory. |  | KnativeProducerFactory |
| **sinkBinding** (common) | The SinkBinding configuration. |  | KnativeSinkBinding |
| **transportOptions** (common) | Set the transport options. |  | Map |
| **typeId** (common) | The name of the service to lookup from the KnativeEnvironment. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **replyWithCloudEvent** (consumer) | Transforms the reply into a cloud event that will be processed by the caller. When listening to events from a Knative Broker, if this flag is enabled, replies will be published to the same Broker where the request comes from (beware that if you don’t change the type of the received message, you may create a loop and receive your same reply). When this flag is disabled, CloudEvent headers are removed from the reply. | false | boolean |
| **reply** (consumer (advanced)) | If the consumer should construct a full reply to knative request. | true | Boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | The version of the k8s resource referenced by the endpoint. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **kind** (advanced) | The type of the k8s resource referenced by the endpoint. |  | String |
| **name** (advanced) | The name of the k8s resource referenced by the endpoint. |  | String |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Knative endpoint is configured using URI syntax:

knative:type/typeId

With the following _path_ and _query_ parameters:

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

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ceOverride** (common) | CloudEvent headers to override. |  | Map |
| **cloudEventsSpecVersion** (common) | 
Set the version of the cloudevents spec.

Enum values:

-   1.0
    
-   1.0.1
    
-   1.0.2
    





 | 1.0 | String |
| **cloudEventsType** (common) | Set the event-type information of the produced events. | org.apache.camel.event | String |
| **environment** (common) | The environment. |  | KnativeEnvironment |
| **filters** (common) | Set the filters. |  | Map |
| **sinkBinding** (common) | The SinkBinding configuration. |  | KnativeSinkBinding |
| **transportOptions** (common) | Set the transport options. |  | Map |
| **replyWithCloudEvent** (consumer) | Transforms the reply into a cloud event that will be processed by the caller. When listening to events from a Knative Broker, if this flag is enabled, replies will be published to the same Broker where the request comes from (beware that if you don’t change the type of the received message, you may create a loop and receive your same reply). When this flag is disabled, CloudEvent headers are removed from the reply. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **reply** (consumer (advanced)) | If the consumer should construct a full reply to knative request. | true | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | The version of the k8s resource referenced by the endpoint. |  | String |
| **kind** (advanced) | The type of the k8s resource referenced by the endpoint. |  | String |
| **name** (advanced) | The name of the k8s resource referenced by the endpoint. |  | String |

## Usage

### Supported Knative resources

The component support the following Knative resources you can target or exposes using the `type` path parameter:

-   `channel`: allow producing or consuming events to or from a [**Knative Channel**](https://knative.dev/docs/eventing/channels/)
    
-   `endpoint`: allow exposing or targeting serverless workloads using [**Knative Services**](https://knative.dev/docs/serving/spec/knative-api-specification-1.0/#service)
    
-   `event`: allow producing or consuming events to or from a [**Knative Broker**](https://knative.dev/docs/eventing/broker)
    

### Knative Environment

As the Knative component hides the technical details of how to communicate with Knative services to the user (protocols, addresses, etc.), it needs some metadata that describes the Knative environment to set up the low-level transport details. To do so, the component needs a so called `Knative Environment`, which is essence is a Json document made by a number of `service` elements which looks like the below example:

Example

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

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>the type of the Knative resource</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>the name of the resource</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>the url of the service to invoke (for producer only)</td></tr><tr><td><i class="conum" data-value="4"></i><b>4</b></td><td>the Knative event type received or produced by the component</td></tr><tr><td><i class="conum" data-value="5"></i><b>5</b></td><td>the type of the Camel Endpoint associated with this Knative resource (source=consumer, sink=producer)</td></tr></tbody></table>

The `metadata` fields has some additional advanced fields:

  
| Name | Description | Example |
| --- | --- | --- |
| **filter.** | The prefix to define filters to be applied to the incoming message headers. | `` `filter.ce.source=my-source` `` |
| **knative.kind** | The type of the k8s resource referenced by the endpoint. | `` `knative.kind=InMemoryChannel` `` |
| **knative.apiVersion** | The version of the k8s resource referenced by the endpoint | `` `knative.apiVersion=messaging.knative.dev/v1beta1` `` |
| **knative.reply** | If the consumer should construct a full reply to knative request. | `` `knative.reply=false` `` |
| **ce.override.** | The prefix to define CloudEvents values that have to be overridden. | `` `ce.override.ce-type=MyType` `` |

Example

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

You can also use property based component configuration to set the `Knative Environment` configuration file.

application.properties

```properties
camel.component.knative.environmentPath=classpath:knative.json
```

### Using custom Knative transports

As today the Knative component only supports `http` as transport as this is the only supported protocol on Knative side. The transport implementation is pluggable though by implementing the following interface:

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

## Knative eventing

With [Knative eventing](https://knative.dev/docs/eventing/) you have the opportunity to produce/consume events on the Knative broker.

### Producing events

The Apache Camel route is able to produce events by sending requests to the Knative broker. In the Camel route you need to use the `event` resource for this kind of interaction with the Knative eventing broker. Configure the Knative component with following `Knative Environment` configuration.

knative.json

```json
{
  "resources": [
    {
      "name": "default",
      "type": "event",
      "endpointKind": "sink",
      "url": "http://default-broker.some-namespace.svc.cluster.local",
      "objectApiVersion": "eventing.knative.dev/v1",
      "objectKind": "Broker",
      "objectName": "default"
    }
  ]
}
```

The `Knative Environment` configuration is set on the Knative component and specifies the Knative broker URL. You can then use the `event` resource type in your Camel route to send data to the Knative broker.

Example

```java
CamelContext context = new DefaultCamelContext();

KnativeComponent component = context.getComponent("knative", KnativeComponent.class);
component.getConfiguration().setEnvironmentPath("classpath:knative.json"); (1)

RouteBuilder.addRoutes(context, b -> {
    b.from("timer:tick")
        .setBody()
            .simple("Hello Knative!")
        .transform(new DataType("http:application-cloudevents")) (2)
        .to("knative:event/default?kind=Broker&name=default"); (3)
});
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>configure the Knative component to use the <code>Knative Environment</code> file</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>transform data to proper Http CloudEvents format</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>push event to the broker that gets resolved via the <code>Knative Environment</code></td></tr></tbody></table>

The Knative eventing broker uses CloudEvents data format by default. This is why we transform the data with the given data type before sending the request to the broker. The data type will set proper CloudEvent attributes like event type, id, source, subject and so on.

You can customize the CloudEvent attributes by setting specific message headers (e.g. `CamelCloudEventID=myEventId` or `CamelCloudEventType=myEventType`).

Also, you may set the CloudEvent attributes via property based configuration on the Knative component.

application.properties

```properties
camel.component.knative.ceOverride[ce-type]=dev.knative.connector.event.timer
camel.component.knative.ceOverride[ce-source]=dev.knative.eventing.timer-source
camel.component.knative.ceOverride[ce-subject]=timer
```

### SinkBinding

As an alternative to specifying the Knative broker URL statically in the `Knative Environment` configuration you can leverage the concept of a `SinkBinding` resource that is able to inject the broker URL as an environment variable named `K_SINK`.

The SinkBinding is a Kubernetes resource that makes Knative eventing automatically inject the resource URL into your Camel application on startup. The real Knative broker URL will be available in the form of the environment varoable `K_SINK`.

You can use property binding support to resolve this environment variable in the Knative component configuration:

knative.json

```json
{
  "resources": [
    {
      "name": "default",
      "type": "event",
      "endpointKind": "sink",
      "url": "{{k.sink}}",
      "objectApiVersion": "eventing.knative.dev/v1",
      "objectKind": "Broker",
      "objectName": "default"
    }
  ]
}
```

As you can see the `Knative Environment` configuration now uses the expression `{{k.sink}}` as a broker URL. On startup the `SinkBinding` will inject this environment variable.

The SinkBinding is created as a Kubernetes resource and looks like this:

Example SinkBinding

```yaml
apiVersion: sources.knative.dev/v1
kind: SinkBinding
metadata:
  labels:
    app.kubernetes.io/name: my-camel-app
  name: my-camel-app-binding
spec:
  sink:
    ref:
      apiVersion: eventing.knative.dev/v1
      kind: Broker
      name: default
  subject:
    apiVersion: apps/v1
    kind: Deployment
    name: my-camel-app
```

The binding resource specifies the reference to the Knative broker and a subject which usually is the Deployment resource that represents your Camel application running on Kubernetes.

> **Tip**
> It may take some time for the SinkBinding to inject the `K_SINK` environment variable into the Deployment resource. The Camel application may run into errors because of the missing variable when starting the Camel context. As a result you may want to wait for the environment variable to be present before starting the Camel context. You can do this with a Camel startup condition, for instance by setting `CAMEL_STARTUPCONDITION_ENVIRONMENT_VARIABLE_EXISTS=K_SINK`.

### Using ProducerTemplate

When using Knative producer with a ProducerTemplate, it is necessary to specify a value for the CloudEvent source, simply by setting a value for the header 'CamelCloudEventSource'.

Example

```java
producerTemplate.sendBodyAndHeader("knative:event/broker-test", body, CloudEvent.CAMEL_CLOUD_EVENT_SOURCE, "my-source-name");
```

### Consuming events

The Knative event consumption is based on starting a Http service as part of the Camel application. The Knative broker will invoke the service then with the event data. The concept uses a so called `Trigger` resource that connects the application with the Knative broker event stream. The trigger specifies which events should be sent to the Http service that is part of the Camel application.

As sample trigger resource looks like this:

Trigger resource

```yaml
apiVersion: eventing.knative.dev/v1
kind: Trigger
metadata:
  labels:
    app.kubernetes.io/name: my-camel-app
    eventing.knative.dev/broker: default
  name: my-camel-app-trigger
spec:
  broker: default
  subscriber:
    ref:
      apiVersion: v1
      kind: Service
      name: my-camel-app
```

The trigger resource references a Knative broker by its name (`default`) and specifies the subscriber which is an arbitrary Kubernetes Service. The trigger will invoke the service subscriber for each event on the broker. The trigger may specify filters on event attributes to select the events that should be sent to the subscriber.

The Service resource is part of the Camel application running on the Kubernetes cluster and points to an exposed Http service and port. The Knative Camel component will automatically configure this Http service when consuming events in a Camel route.

Just use the `event` resource type in your Camel route like this:

Example

```java
RouteBuilder.addRoutes(context, b -> {
    b.from("knative:event/default?kind=Broker&name=default")
        .to("log:info");
});
```

The according `Knative Environment` configuration that specifies the Http service looks like this:

knative.json

```json
{
  "resources": [
    {
      "name": "default",
      "type": "event",
      "endpointKind": "source",
      "path": "/",
      "objectApiVersion": "eventing.knative.dev/v1",
      "objectKind": "Broker",
      "objectName": "default",
      "reply": false
    }
  ]
}
```

This will create a proper Http service with the right resource path routing so that all incoming event requests will be consumed by the Camel route. Once again the Knative broker will use CloudEvent data format by default, so you can access the CloudEvent attributes such as event type, id, source, subject in the Camel route.