# JMX

**Since Camel 2.6**

**Only consumer is supported**

Apache Camel has extensive support for JMX to allow you to monitor and control the Camel managed objects with a JMX client.

Camel also provides a [JMX](#) component that allows you to subscribe to MBean notifications. This page is about how to manage and monitor Camel using JMX.

> **Note**
> If you run Camel standalone with just `camel-core` as a dependency, and you want JMX to enable out of the box, then you need to add `camel-management` as a dependency.

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

The JMX component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JMX endpoint is configured using URI syntax:

jmx:serverURL

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serverURL** (consumer) | Server url comes from the remaining endpoint. Use platform to connect to local JVM. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **format** (consumer) | 
Format for the message body. Either xml or raw. If xml, the notification is serialized to xml. If raw, then the raw java object is set as the body.

Enum values:

-   xml
    
-   raw
    





 | xml | String |
| **granularityPeriod** (consumer) | The frequency to poll the bean to check the monitor (monitor types only). | 10000 | long |
| **monitorType** (consumer) | 

The type of monitor to create. One of string, gauge, counter (monitor types only).

Enum values:

-   counter
    
-   gauge
    
-   string
    





 |  | String |
| **objectDomain** (consumer) | **Required** The domain for the mbean you’re connecting to. |  | String |
| **objectName** (consumer) | The name key for the mbean you’re connecting to. This value is mutually exclusive with the object properties that get passed. |  | String |
| **observedAttribute** (consumer) | The attribute to observe for the monitor bean or consumer. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **executorService** (advanced) | To use a custom shared thread pool for the consumers. By default each consume has their own thread-pool to process and route notifications. |  | ExecutorService |
| **handback** (advanced) | Value to handback to the listener when a notification is received. This value will be put in the message header with the key JMXConstants#JMX\_HANDBACK. |  | Object |
| **notificationFilter** (advanced) | Reference to a bean that implements the NotificationFilter. |  | NotificationFilter |
| **objectProperties** (advanced) | Properties for the object name. These values will be used if the objectName param is not set. This is a multi-value option with prefix: key. |  | Map |
| **reconnectDelay** (advanced) | The number of seconds to wait before attempting to retry establishment of the initial connection or attempt to reconnect a lost connection. | 10 | int |
| **reconnectOnConnectionFailure** (advanced) | If true the consumer will attempt to reconnect to the JMX server when any connection failure occurs. The consumer will attempt to re-establish the JMX connection every 'x' seconds until the connection is made-- where 'x' is the configured reconnectionDelay. | false | boolean |
| **testConnectionOnStartup** (advanced) | If true the consumer will throw an exception if unable to establish the JMX connection upon startup. If false, the consumer will attempt to establish the JMX connection every 'x' seconds until the connection is made — where 'x' is the configured reconnectionDelay. | true | boolean |
| **initThreshold** (counter) | Initial threshold for the monitor. The value must exceed this before notifications are fired (counter monitor only). |  | int |
| **modulus** (counter) | The value at which the counter is reset to zero (counter monitor only). |  | int |
| **offset** (counter) | The amount to increment the threshold after it’s been exceeded (counter monitor only). |  | int |
| **differenceMode** (gauge) | If true, then the value reported in the notification is the difference from the threshold as opposed to the value itself (counter and gauge monitor only). | false | boolean |
| **notifyHigh** (gauge) | If true, the gauge will fire a notification when the high threshold is exceeded (gauge monitor only). | false | boolean |
| **notifyLow** (gauge) | If true, the gauge will fire a notification when the low threshold is exceeded (gauge monitor only). | false | boolean |
| **thresholdHigh** (gauge) | Value for the gauge’s high threshold (gauge monitor only). |  | Double |
| **thresholdLow** (gauge) | Value for the gauge’s low threshold (gauge monitor only). |  | Double |
| **password** (security) | Credentials for making a remote connection. |  | String |
| **user** (security) | Credentials for making a remote connection. |  | String |
| **notifyDiffer** (string) | If true, will fire a notification when the string attribute differs from the string to compare (string monitor or consumer). By default the consumer will notify match if observed attribute and string to compare has been configured. | false | boolean |
| **notifyMatch** (string) | If true, will fire a notification when the string attribute matches the string to compare (string monitor or consumer). By default the consumer will notify match if observed attribute and string to compare has been configured. | false | boolean |
| **stringToCompare** (string) | Value for attribute to compare (string monitor or consumer). By default the consumer will notify match if observed attribute and string to compare has been configured. |  | String |

## Message Headers

The JMX component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **jmx.handback** (consumer) Constant: [`JMX_HANDBACK`](https://javadoc.io/doc/org.apache.camel/camel-jmx/latest/org/apache/camel/component/jmx/JMXConstants.html#JMX_HANDBACK) | The handback. |  | Object |