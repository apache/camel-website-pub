# Kamelet

**Since Camel 3.8**

**Both producer and consumer are supported**

The Kamelet Component provides support for interacting with the [Camel Route Template](../../manual/route-template.md) engine using Endpoint semantic.

## URI format

kamelet:templateId/routeId\[?options\]

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

The Kamelet component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **location** (common) | The location(s) of the Kamelets on the file system. Multiple locations can be set separated by comma. | classpath:kamelets | String |
| **routeProperties** (common) | Set route local parameters. |  | Map |
| **templateProperties** (common) | Set template local parameters. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **block** (producer) | If sending a message to a kamelet endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer) | The timeout value to use if block is enabled. | 30000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **noErrorHandler** (advanced) | Whether kamelets should use error handling or not. By default, the Kamelet uses the same error handler as from the calling route. This means that if the calling route has error handling that performs retries, or routing to a dead letter channel, then the kamelet route will use this also. This can be turned off by setting this option to true. If off then the kamelet route is not using error handling, and any exception thrown will for source kamelets be logged by the consumer, and the sink/action kamelets will fail processing. | false | boolean |
| **routeTemplateLoaderListener** (advanced) | **Autowired** To plugin a custom listener for when the Kamelet component is loading Kamelets from external resources. |  | RouteTemplateLoaderListener |

## Endpoint Options

The Kamelet endpoint is configured using URI syntax:

kamelet:templateId/routeId

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **templateId** (common) | **Required** The Route Template ID. |  | String |
| **routeId** (advanced) | The Route ID. Default value notice: The ID will be auto-generated if not provided. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **block** (producer (advanced)) | If sending a message to a direct endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **failIfNoConsumers** (producer (advanced)) | Whether the producer should fail by throwing an exception, when sending to a kamelet endpoint with no active consumers. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer (advanced)) | The timeout value to use if block is enabled. | 30000 | long |
| **location** (advanced) | Location of the Kamelet to use which can be specified as a resource from file system, classpath etc. The location cannot use wildcards, and must refer to a file including extension, for example file:/etc/foo-kamelet.xml. |  | String |
| **noErrorHandler** (advanced) | Whether kamelets should use error handling or not. By default, the Kamelet uses the same error handler as from the calling route. This means that if the calling route has error handling that performs retries, or routing to a dead letter channel, then the kamelet route will use this also. This can be turned off by setting this option to true. If off then the kamelet route is not using error handling, and any exception thrown will for source kamelets be logged by the consumer, and the sink/action kamelets will fail processing. | false | boolean |
> **Note**
> The **kamelet** endpoint is **lenient**, which means that the endpoint accepts additional parameters that are passed to the [Route Template](../../manual/route-template.md) engine and consumed upon route materialization.

## Usage

### Discovery

If a [Route Template](../../manual/route-template.md) is not found, the **kamelet** endpoint tries to load the related **kamelet** definition from the file system (by default `classpath:kamelets`). The default resolution mechanism expects _Kamelets_ files to have the extension `.kamelet.yaml`.

### Error Handling

The error handling when using kamelets are using the same error handling that are from the route where the kamelets are being used.

Suppose you have kamelets that would cause an exception during processing, such as the source below. Now because the route has been configured with a _dead letter channel_ as the error handler, then the exception from the kamelet will be handled by the route error handler. Which means you will se a WARN being logged.

```yaml
- route:
    errorHandler:
      deadLetterChannel:
        deadLetterUri: log:dead?level=WARN
    id: myRoute
    from:
      uri: kamelet:my-error-source/source
      steps:
        - log:
            message: "${body}"
```

For sink kamelets then error handling also allows to perform retries.

So suppose you have the following route:

```yaml
- route:
    errorHandler:
      deadLetterChannel:
        deadLetterUri: log:dead?level=WARN
        redeliveryPolicy:
          maximumRedeliveries: 5
          redeliveryDelay: "5000"
    id: myRoute
    from:
      uri: direct:start
      steps:
        - to:
            uri: kamelet:my-error-sink/sink
        - log:
            message: "${body}"
```

Then notice the error handler has been configured to do redeliveries up till 5 times with 5 sec delay between. Suppose the sink kamelet is throwing an exception, then Camel will now perform the redelivery attempt at the point of origin, which means inside the Kamelet.

### Calling a Kamelet from another Kamelet

> **Note**
> this feature is available since version 4.10.0 onward

As a Kamelet behave as any other regular component, you will be able to use it in a nested way. The definition of a Kamelet can contains the reference to another Kamelet which will give you a high level of flexibility when constructing your abstraction.

In the following example, we are creating a Kamelet which is calling a bundled catalog Kamelet `log-sink`:

```yaml
apiVersion: camel.apache.org/v1
kind: Kamelet
metadata:
  name: nested-sink
spec:
  definition:
    title: "Kamelet in a Kamelet"
    description: A Kamelet calling another Kamelet
    required:
      - log-level
    properties:
      log-level:
        title: The Kamelet log-sink log level
        description: The Kamelet log-sink log level
        type: string
        example: DEBUG
  dependencies:
  - "camel:core"
  - "camel:kamelet"
  template:
    from:
      uri: kamelet:source
      steps:
      - to:
          uri: kamelet:log-sink
          parameters:
            level: "{{log-level}}"
```

According to the specification, this Kamelet expects a parameter, _log-level_ which we will use as a further parameter for the downstream call to the `log-sink` Kamelet.

The usage of this Kamelet into a Camel route is going to be the same as any other Kamelet:

```yaml
- route:
    from:
      uri: timer:yaml
      parameters:
        period: "5000"
    steps:
      - setBody:
          simple: "Hello Camel from ${routeId}"
      - to:
          uri: kamelet:nested-sink
          parameters:
            log-level: INFO
```

> **Warning**
> beware of any potential circular reference you may introduce when using chain of Kamelets, in which case, the runtime will likely be idle consuming a high amount of resources.

## Examples

_Kamelets_ can be used as if they were standard Camel components. For example, suppose that we have created a Route Template as follows:

_Java-only: programmatic route template definition_

```java
routeTemplate("setMyBody")
    .templateParameter("bodyValue")
    .from("kamelet:source")
        .setBody().constant("{{bodyValue}}");
```

> **Important**
> To let the **Kamelet** component wiring the materialized route to the caller processor, we need to be able to identify the input and output endpoint of the route and this is done by using `kamelet:source` to mark the input endpoint and `kamelet:sink` for the output endpoint.

Then the template can be instantiated and invoked as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:setMyBody")
    .to("kamelet:setMyBody?bodyValue=myKamelet");
```

```xml
<route>
  <from uri="direct:setMyBody"/>
  <to uri="kamelet:setMyBody?bodyValue=myKamelet"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:setMyBody
      steps:
        - to:
            uri: kamelet:setMyBody
            parameters:
              bodyValue: myKamelet
```

Behind the scenes, the **Kamelet** component does the following things:

1.  it instantiates a route out of the Route Template identified by the given `templateId` path parameter (in this case `setMyBody`)
    
2.  it will act like the `direct` component and connect the current route to the materialized one.
    

If you had to do it programmatically, it would have been something like:

_Java-only: programmatic TemplatedRouteBuilder usage_

```java
routeTemplate("setMyBody")
    .templateParameter("bodyValue")
    .from("direct:{{foo}}")
        .setBody().constant("{{bodyValue}}");

TemplatedRouteBuilder.builder(context, "setMyBody")
    .parameter("foo", "bar")
    .parameter("bodyValue", "myKamelet")
    .add();

from("direct:template")
    .to("direct:bar");
```