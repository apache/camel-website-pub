# PubNub

**Since Camel 2.19**

**Both producer and consumer are supported**

Camel PubNub component can be used to communicate with the [PubNub](https://www.pubnub.com/) data stream network for connected devices. This component uses pubnub [java library](https://github.com/pubnub/java).

Use cases include:

-   Chat rooms: Sending and receiving messages
    
-   Locations and Connected cars: dispatching taxi cabs
    
-   Smart sensors: Receiving data from a sensor for data visualizations
    
-   Health: Monitoring heart rate from a patient’s wearable device
    
-   Multiplayer games
    
-   Interactive media: audience-participating voting system
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-pubnub</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

pubnub:channel\[?options\]

Where **channel** is the PubNub channel to publish or subscribe to.

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

The PubNub component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The component configurations. |  | PubNubConfiguration |
| **uuid** (common) | **Required** UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **withPresence** (consumer) | Also subscribe to related presence information. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel.

Enum values:

-   HERENOW
    
-   GETSTATE
    
-   SETSTATE
    
-   GETHISTORY
    
-   PUBLISH
    
-   FIRE
    





 |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **authKey** (security) | **Deprecated** If Access Manager is utilized, client will use this authKey in all restricted requests. Default value notice: This setting is deprecated because it relates to deprecated Access Manager (PAM V2) and will be removed in the future. Please, migrate to new Access Manager (PAM V3) [https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration](https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration). |  | String |
| **publishKey** (security) | The publish key obtained from your PubNub account. Required when publishing messages. |  | String |
| **secretKey** (security) | The secret key used for message signing. |  | String |
| **secure** (security) | Use SSL for secure transmission. | true | boolean |
| **subscribeKey** (security) | The subscribe key obtained from your PubNub account. Required when subscribing to channels or listening for presence events. |  | String |

## Endpoint Options

The PubNub endpoint is configured using URI syntax:

pubnub:channel

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channel** (common) | **Required** The channel used for subscribing/publishing events. |  | String |

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uuid** (common) | **Required** UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **withPresence** (consumer) | Also subscribe to related presence information. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **operation** (producer) | 

The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel.

Enum values:

-   HERENOW
    
-   GETSTATE
    
-   SETSTATE
    
-   GETHISTORY
    
-   PUBLISH
    
-   FIRE
    





 |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **pubnub** (advanced) | **Autowired** Reference to a Pubnub client in the registry. |  | PubNub |
| **authKey** (security) | **Deprecated** If Access Manager is utilized, client will use this authKey in all restricted requests. Default value notice: This setting is deprecated because it relates to deprecated Access Manager (PAM V2) and will be removed in the future. Please, migrate to new Access Manager (PAM V3) [https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration](https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration). |  | String |
| **publishKey** (security) | The publish key obtained from your PubNub account. Required when publishing messages. |  | String |
| **secretKey** (security) | The secret key used for message signing. |  | String |
| **secure** (security) | Use SSL for secure transmission. | true | boolean |
| **subscribeKey** (security) | The subscribe key obtained from your PubNub account. Required when subscribing to channels or listening for presence events. |  | String |

## Message Headers

The PubNub component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelPubNubOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-pubnub/latest/org/apache/camel/component/pubnub/PubNubConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelPubNubTimeToken** (common) Constant: [`TIMETOKEN`](https://javadoc.io/doc/org.apache.camel/camel-pubnub/latest/org/apache/camel/component/pubnub/PubNubConstants.html#TIMETOKEN) | The Timestamp for the event. |  | Long |
| **CamelPubNubChannel** (consumer) Constant: [`CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-pubnub/latest/org/apache/camel/component/pubnub/PubNubConstants.html#CHANNEL) | The channel for which the message belongs. |  | String |
| **CamelPubNubUUID** (producer) Constant: [`UUID`](https://javadoc.io/doc/org.apache.camel/camel-pubnub/latest/org/apache/camel/component/pubnub/PubNubConstants.html#UUID) | UUID to be used as a device identifier. |  | String |

## Usage

### Message body

The message body can contain any JSON serializable data, including Objects, Arrays, Integers, and Strings. Message data should not contain special Java V4 classes or functions as these will not serialize. String content can include any single-byte or multibyte UTF-8.

Object serialization when sending is done automatically. Pass the full object as the message payload. PubNub will take care of object serialization.

When receiving the message body uses objects provided by the PubNub API.

## Examples

### Publishing events

Default operation when producing. The following snippet publishes the event generated by PojoBean to the channel iot.

_Java-only: publishing events with a bean processor_

```java
from("timer:mytimer")
    // generate some data as POJO.
    .bean(PojoBean.class)
    .to("pubnub:iot?publishKey=mypublishKey");
```

### Fire events aka BLOCKS Event Handlers

See [blocks catalog](https://www.pubnub.com/blocks-catalog/) for all kinds of serverless functions that can be invoked. Example of geolocation lookup

_Java-only: fire events with geolocation lookup_

```java
from("timer:geotimer")
    .process(exchange -> exchange.getIn().setBody(new Foo("bar", "TEXT")))
    .to("pubnub:eon-maps-geolocation-input?operation=fire&publishKey=mypubkey&subscribeKey=mysubkey");

from("pubnub:eon-map-geolocation-output?subscribeKey=mysubkey)
    // geolocation output will be logged here
    .log("${body}");
```

### Subscribing to events

The following snippet listens for events on the iot channel. If you can add the option withPresence, you will also receive channel Join, Leave asf events.

-   Java
    
-   XML
    
-   YAML
    

```java
from("pubnub:iot?subscribeKey=mySubscribeKey")
    .log("${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="pubnub:iot?subscribeKey=mySubscribeKey"/>
  <log message="${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: pubnub:iot
      parameters:
        subscribeKey: mySubscribeKey
      steps:
        - log:
            message: "${body}"
        - to:
            uri: mock:result
```

### Performing operations

-   `herenow`: obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count of the channel:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=herenow")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:control"/>
  <to uri="pubnub:myChannel?publishKey=mypublishKey&amp;subscribeKey=mySubscribeKey&amp;operation=herenow"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:control
      steps:
        - to:
            uri: pubnub:myChannel
            parameters:
              publishKey: mypublishKey
              subscribeKey: mySubscribeKey
              operation: herenow
        - to:
            uri: mock:result
```

-   `wherenow`: obtain information about the current list of channels to which a uuid is subscribed:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=wherenow&uuid=spyonme")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:control"/>
  <to uri="pubnub:myChannel?publishKey=mypublishKey&amp;subscribeKey=mySubscribeKey&amp;operation=wherenow&amp;uuid=spyonme"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:control
      steps:
        - to:
            uri: pubnub:myChannel
            parameters:
              publishKey: mypublishKey
              subscribeKey: mySubscribeKey
              operation: wherenow
              uuid: spyonme
        - to:
            uri: mock:result
```

-   `setstate`: used to set key/value pairs specific to a subscriber uuid:
    

_Java-only: setting state with a bean processor_

```java
from("direct:control")
    .bean(StateGenerator.class)
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=setstate&uuid=myuuid");
```

-   `gethistory`: Fetches historical messages of a channel:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=gethistory");
```

```xml
<route>
  <from uri="direct:control"/>
  <to uri="pubnub:myChannel?publishKey=mypublishKey&amp;subscribeKey=mySubscribeKey&amp;operation=gethistory"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:control
      steps:
        - to:
            uri: pubnub:myChannel
            parameters:
              publishKey: mypublishKey
              subscribeKey: mySubscribeKey
              operation: gethistory
```

There are a couple of examples in the test directory that show some of the PubNub features. They require a PubNub account, from where you can obtain a publish/subscribe key.

The example PubNubSensorExample already contains a subscription key provided by PubNub, so this is ready to run without an account. The example illustrates the PubNub component subscribing to an infinite stream of sensor data.

## Spring Boot Auto-Configuration

When using pubnub with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-pubnub-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.pubnub.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.pubnub.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.pubnub.configuration** | The component configurations. The option is a org.apache.camel.component.pubnub.PubNubConfiguration type. |  | PubNubConfiguration |
| **camel.component.pubnub.enabled** | Whether to enable auto configuration of the pubnub component. This is enabled by default. |  | Boolean |
| **camel.component.pubnub.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.pubnub.operation** | The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel. |  | String |
| **camel.component.pubnub.publish-key** | The publish key obtained from your PubNub account. Required when publishing messages. |  | String |
| **camel.component.pubnub.secret-key** | The secret key used for message signing. |  | String |
| **camel.component.pubnub.secure** | Use SSL for secure transmission. | true | Boolean |
| **camel.component.pubnub.subscribe-key** | The subscribe key obtained from your PubNub account. Required when subscribing to channels or listening for presence events. |  | String |
| **camel.component.pubnub.uuid** | UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **camel.component.pubnub.with-presence** | Also subscribe to related presence information. | false | Boolean |
| **camel.component.pubnub.auth-key** | **Deprecated** If Access Manager is utilized, client will use this authKey in all restricted requests. Default value notice: This setting is deprecated because it relates to deprecated Access Manager (PAM V2) and will be removed in the future. Please, migrate to new Access Manager (PAM V3) [https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration](https://www.pubnub.com/docs/general/resources/migration-guides/pam-v3-migration). |  | String |