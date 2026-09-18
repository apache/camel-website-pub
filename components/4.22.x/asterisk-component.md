# Asterisk

**Since Camel 2.18**

**Both producer and consumer are supported**

The Asterisk component allows you to work easily with an Asterisk PBX Server [http://www.asterisk.org/](http://www.asterisk.org/) using [asterisk-java](https://asterisk-java.org/)

This component helps to interface with [Asterisk Manager Interface](http://www.voip-info.org/wiki-Asterisk+manager+API)

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

The Asterisk component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Asterisk endpoint is configured using URI syntax:

asterisk:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of component. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (common) | **Required** The hostname of the asterisk server. |  | String |
| **password** (common) | **Required** Login password. |  | String |
| **username** (common) | **Required** Login username. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





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

The Asterisk component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAsteriskEventName** (consumer) Constant: [`EVENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-asterisk/latest/org/apache/camel/component/asterisk/AsteriskConstants.html#EVENT_NAME) | The name of the Asterisk event. |  | String |
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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
  .to("asterisk://myVoIP?hostname=hostname&username=username&password=password&action=EXTENSION_STATE");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="asterisk://myVoIP?hostname=hostname&amp;username=username&amp;password=password&amp;action=EXTENSION_STATE"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: asterisk://myVoIP
            parameters:
              hostname: hostname
              username: username
              password: password
              action: EXTENSION_STATE
```

### Consumer Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("asterisk:myVoIP?hostname=hostname&username=username&password=password")
  .log("Received a message - ${body}");
```

```xml
<route>
  <from uri="asterisk:myVoIP?hostname=hostname&amp;username=username&amp;password=password"/>
  <log message="Received a message - ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: asterisk:myVoIP
      parameters:
        hostname: hostname
        username: username
        password: password
      steps:
        - log:
            message: "Received a message - ${body}"
```