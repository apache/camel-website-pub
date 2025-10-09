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

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The PubNub component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The component configurations. |  | PubNubConfiguration |
| **uuid** (common) | UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **withPresence** (consumer) | Also subscribe to related presence information. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. WHERENOW: Obtain information about the current list of channels to which a uuid is subscribed to. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel.

Enum values:

-   HERENOW
    
-   WHERENOW
    
-   GETSTATE
    
-   SETSTATE
    
-   GETHISTORY
    
-   PUBLISH
    
-   FIRE
    





 |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **authKey** (security) | If Access Manager is utilized, client will use this authKey in all restricted requests. |  | String |
| **cipherKey** (security) | If cipher is passed, all communications to/from PubNub will be encrypted. |  | String |
| **publishKey** (security) | The publish key obtained from your PubNub account. Required when publishing messages. |  | String |
| **secretKey** (security) | The secret key used for message signing. |  | String |
| **secure** (security) | Use SSL for secure transmission. | true | boolean |
| **subscribeKey** (security) | The subscribe key obtained from your PubNub account. Required when subscribing to channels or listening for presence events. |  | String |

## Endpoint Options

The PubNub endpoint is configured using URI syntax:

pubnub:channel

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channel** (common) | **Required** The channel used for subscribing/publishing events. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uuid** (common) | UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **withPresence** (consumer) | Also subscribe to related presence information. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **operation** (producer) | 

The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. WHERENOW: Obtain information about the current list of channels to which a uuid is subscribed to. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel.

Enum values:

-   HERENOW
    
-   WHERENOW
    
-   GETSTATE
    
-   SETSTATE
    
-   GETHISTORY
    
-   PUBLISH
    
-   FIRE
    





 |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **pubnub** (advanced) | **Autowired** Reference to a Pubnub client in the registry. |  | PubNub |
| **authKey** (security) | If Access Manager is utilized, client will use this authKey in all restricted requests. |  | String |
| **cipherKey** (security) | If cipher is passed, all communications to/from PubNub will be encrypted. |  | String |
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

## Message body

The message body can contain any JSON serializable data, including: Objects, Arrays, Ints and Strings. Message data should not contain special Java V4 classes or functions as these will not serialize. String content can include any single-byte or multi-byte UTF-8

Object serialization when sending is done automatically. Just pass the full object as the message payload. PubNub will takes care of object serialization.

When receiving the message body utilize objects provided by the PubNub API.

## Examples

### Publishing events

Default operation when producing. The following snippet publish the event generated by PojoBean to the channel iot.

```java
from("timer:mytimer")
    // generate some data as POJO.
    .bean(PojoBean.class)
    .to("pubnub:iot?publishKey=mypublishKey");
```

### Fire events aka BLOCKS Event Handlers

See [https://www.pubnub.com/blocks-catalog/](https://www.pubnub.com/blocks-catalog/) for all kind of serverless functions that can be invoked. Example of geolocation lookup

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

```java
from("pubnub:iot?subscribeKey=mySubscribeKey")
    .log("${body}")
    .to("mock:result");
```

### Performing operations

herenow : Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count of the channel

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=herenow")
    .to("mock:result");
```

wherenow : Obtain information about the current list of channels to which a uuid is subscribed

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=wherenow&uuid=spyonme")
    .to("mock:result");
```

setstate : Used to set key/value pairs specific to a subscriber uuid.

```java
from("direct:control")
    .bean(StateGenerator.class)
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=setstate&uuid=myuuid");
```

gethistory : Fetches historical messages of a channel.

```java
from("direct:control")
    .to("pubnub:myChannel?publishKey=mypublishKey&subscribeKey=mySubscribeKey&operation=gethistory");
```

There is a couple of examples in test directory that shows some of the PubNub features. They require a PubNub account, from where you can obtain a publish- and subscribe key.

The example PubNubSensorExample already contains a subscribe key provided by PubNub, so this is ready to run without a account. The example illustrates the PubNub component subscribing to a infinite stream of sensor data.

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

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.pubnub.auth-key** | If Access Manager is utilized, client will use this authKey in all restricted requests. |  | String |
| **camel.component.pubnub.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.pubnub.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.pubnub.cipher-key** | If cipher is passed, all communications to/from PubNub will be encrypted. |  | String |
| **camel.component.pubnub.configuration** | The component configurations. The option is a org.apache.camel.component.pubnub.PubNubConfiguration type. |  | PubNubConfiguration |
| **camel.component.pubnub.enabled** | Whether to enable auto configuration of the pubnub component. This is enabled by default. |  | Boolean |
| **camel.component.pubnub.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.pubnub.operation** | The operation to perform. PUBLISH: Default. Send a message to all subscribers of a channel. FIRE: allows the client to send a message to BLOCKS Event Handlers. These messages will go directly to any Event Handlers registered on the channel. HERENOW: Obtain information about the current state of a channel including a list of unique user-ids currently subscribed to the channel and the total occupancy count. WHERENOW: Obtain information about the current list of channels to which a uuid is subscribed to. GETSTATE: Used to get key/value pairs specific to a subscriber uuid. State information is supplied as a JSON object of key/value pairs SETSTATE: Used to set key/value pairs specific to a subscriber uuid GETHISTORY: Fetches historical messages of a channel. |  | String |
| **camel.component.pubnub.publish-key** | The publish key obtained from your PubNub account. Required when publishing messages. |  | String |
| **camel.component.pubnub.secret-key** | The secret key used for message signing. |  | String |
| **camel.component.pubnub.secure** | Use SSL for secure transmission. | true | Boolean |
| **camel.component.pubnub.subscribe-key** | The subscribe key obtained from your PubNub account. Required when subscribing to channels or listening for presence events. |  | String |
| **camel.component.pubnub.uuid** | UUID to be used as a device identifier, a default UUID is generated if not passed. |  | String |
| **camel.component.pubnub.with-presence** | Also subscribe to related presence information. | false | Boolean |