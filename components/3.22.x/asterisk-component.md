# Asterisk

**Since Camel 2.18**

**Both producer and consumer are supported**

The Asterisk component allows you to work easily with an Asterisk PBX Server [http://www.asterisk.org/](http://www.asterisk.org/) using [asterisk-java](https://asterisk-java.org/)

This component help to interface with [Asterisk Manager Interface](http://www.voip-info.org/wiki-Asterisk+manager+API)

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-asterisk</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

asterisk:name\[?options\]

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

The Asterisk component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Asterisk endpoint is configured using URI syntax:

asterisk:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of component. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (common) | **Required** The hostname of the asterisk server. |  | String |
| **password** (common) | **Required** Login password. |  | String |
| **username** (common) | **Required** Login username. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **action** (producer) | 

What action to perform such as getting queue status, sip peers or extension state.

Enum values:

-   QUEUE\_STATUS
    
-   SIP\_PEERS
    
-   EXTENSION\_STATE
    





 |  | AsteriskAction |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Asterisk component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAsteriskEventName** (consumer) Constant: [`EVENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-asterisk/latest/org/apache/camel/component/asterisk/AsteriskConstants.html#EVENT_NAME) | The name of the Asterisk event. | Simple name of the event | String |
| **CamelAsteriskExtension** (producer) Constant: [`EXTENSION`](https://javadoc.io/doc/org.apache.camel/camel-asterisk/latest/org/apache/camel/component/asterisk/AsteriskConstants.html#EXTENSION) | The extension to query in case of an ExtensionStateAction. |  | String |
| **CamelAsteriskContext** (producer) Constant: [`CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-asterisk/latest/org/apache/camel/component/asterisk/AsteriskConstants.html#CONTEXT) | The name of the context that contains the extension to query in case of an ExtensionStateAction. |  | String |
| **CamelAsteriskAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-asterisk/latest/org/apache/camel/component/asterisk/AsteriskConstants.html#ACTION) | 
The Asterisk action to do.

Enum values:

-   QUEUE\_STATUS
    
-   SIP\_PEERS
    
-   EXTENSION\_STATE
    





 |  | AsteriskAction |

## Action

Supported actions are:

-   QUEUE\_STATUS: Queue status
    
-   SIP\_PEERS: List SIP peers
    
-   EXTENSION\_STATE: Check extension status
    

## Examples

### Producer Example

```java
from("direct:in")
  .to("asterisk://myVoIP?hostname=hostname&username=username&password=password&action=EXTENSION_STATE")
```

### Consumer Example

```java
from("asterisk:myVoIP?hostname=hostname&username=username&password=password")
  .log("Received a message - ${body}");
```

## Spring Boot Auto-Configuration

When using asterisk with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-asterisk-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.asterisk.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.asterisk.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.asterisk.enabled** | Whether to enable auto configuration of the asterisk component. This is enabled by default. |  | Boolean |
| **camel.component.asterisk.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |