# MTConnect

**Since Camel 4.24**

**Both producer and consumer are supported**

The MTConnect component reads machine tools and other shop-floor equipment through the agent their vendor ships for the [MTConnect](https://www.mtconnect.org/) standard (ANSI/MTC1.4-2018, Part 1). An MTConnect agent is a read-only HTTP server that answers four requests with XML documents: `probe` (the device model), `current` (the latest value of every data item), `sample` (a range of observations, or an open stream of them) and `assets` (cutting tools, NC programs and other assets).

The consumer runs that protocol against one agent and delivers every observation as its own message, the value as the body and the MTConnect metadata as `CamelMTConnect*` headers. It keeps the sequence cursor across outages, resynchronises when the agent’s buffer no longer holds the next observation, re-reads the device model when the agent restarts, and reports an unreachable agent once per data item with quality `Bad`. The producer sends one request per exchange and sets the answer as the body. Nothing is installed on the plant side: the vendor’s own agent is the source.

The component uses the JDK’s HTTP client and has no third-party dependency.

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mtconnect</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

mtconnect:agentUrl\[?options\]

The `agentUrl` is the agent address: `http` or `https`, host, port and an optional base path, such as `[http://agent:5000](http://agent:5000)`. The `device` option selects one device by name or uuid; without it the consumer receives every device the agent serves.

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

The MTConnect component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The MTConnect endpoint is configured using URI syntax:

mtconnect:agentUrl

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agentUrl** (common) | **Required** The agent address: http or https, host, port and an optional base path, such as [http://agent:5000](http://agent:5000). |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **assetType** (common) | The asset type to read, such as CuttingTool or File: the standard’s type parameter of the assets request, for the producer’s assets operation and the consumer’s asset messages. Without it assets of every type are read. |  | String |
| **connectTimeout** (common) | The time in milliseconds to establish the connection to the agent. | 5000 | long |
| **count** (common) | The maximum number of observations in one part of the consumer’s stream, in each sample request of the polling consumer and in the producer’s sample reply, lowered to the agent’s buffer size from the probe; also the maximum number of assets in the producer’s assets reply. | 1000 | int |
| **device** (common) | The device name or uuid. Without it the consumer receives every device the agent serves. |  | String |
| **readTimeout** (common) | The time in milliseconds within which the agent’s response headers must arrive after a request, and the longest silence while the rest of a document arrives. The parts of the streaming consumer’s sample stream are bounded by two heartbeats instead. | 5000 | long |
| **path** (common (advanced)) | An MTConnect XPath filter the agent applies to the current and sample requests, passed unchanged, such as //Axes//Linear to receive the linear axes only. |  | String |
| **assets** (consumer) | Whether the consumer also sends asset messages: every asset the agent holds, removed ones included, after the current values and after each resynchronisation or agent restart, and the asset of each AssetChanged or AssetRemoved observation. The body is the asset element as a standalone XML document. | false | boolean |
| **heartbeat** (consumer) | Streaming only: the time in milliseconds after which the agent sends an empty part when nothing changed. A stream without a part for two heartbeats counts as a failure. | 10000 | long |
| **interval** (consumer) | Streaming only: the minimum time in milliseconds between two parts of the agent’s sample stream. | 500 | long |
| **reconnectDelay** (consumer) | Streaming only: the time in milliseconds to wait after a failed request, a failed or ended stream or an agent error before the next attempt. | 10000 | long |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streaming** (consumer) | Whether the consumer reads the agent’s streaming sample request. When false, it polls the agent on Camel’s scheduler with one probe, current or sample request per poll, for agents behind a proxy or firewall that cuts long-lived responses; the scheduler options such as delay, initialDelay and greedy apply only then, and the delay is also the wait after a failure. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **at** (producer) | The sequence at which the current request reads the values, one the agent still buffers. Without it the agent answers with its latest values. |  | Long |
| **from** (producer) | The first sequence of the sample request. Without it the agent starts at the oldest sequence it buffers. |  | Long |
| **operation** (producer) | 

The request the producer sends: probe returns the agent’s device model document, current the latest observations, sample a range of observations, assets the agent’s asset document. The CamelMTConnectOperation header overrides it; with neither, the exchange fails.

Enum values:

-   probe
    
-   current
    
-   sample
    
-   assets
    





 |  | MTConnectOperation |
| **removed** (producer) | Whether the assets request also reads assets the agent marked removed. | false | boolean |
| **to** (producer) | The last sequence the sample request includes. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **sslContextParameters** (security) | The TLS configuration for an https agent, such as a trust store with a private certificate authority. Without it, and without the component’s global SSL context parameters, the runtime’s default trust applies. |  | SSLContextParameters |

## Message Headers

The MTConnect component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMTConnectAgent** (consumer) Constant: [`AGENT`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#AGENT) | The agent address of the endpoint, which tells apart agents that serve the same device uuid. |  | String |
| **CamelMTConnectDeviceUuid** (consumer) Constant: [`DEVICE_UUID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DEVICE_UUID) | The uuid of the device. |  | String |
| **CamelMTConnectDeviceName** (consumer) Constant: [`DEVICE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DEVICE_NAME) | The name of the device. |  | String |
| **CamelMTConnectComponentId** (consumer) Constant: [`COMPONENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#COMPONENT_ID) | The id of the component that owns the data item. |  | String |
| **CamelMTConnectComponentType** (consumer) Constant: [`COMPONENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#COMPONENT_TYPE) | The type of the component that owns the data item, such as Linear, Controller or Device. |  | String |
| **CamelMTConnectComponentName** (consumer) Constant: [`COMPONENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#COMPONENT_NAME) | The name of the component that owns the data item. |  | String |
| **CamelMTConnectDataItemId** (consumer) Constant: [`DATA_ITEM_ID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DATA_ITEM_ID) | The data item id, unique within the agent. |  | String |
| **CamelMTConnectDataItemName** (consumer) Constant: [`DATA_ITEM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DATA_ITEM_NAME) | The data item name. |  | String |
| **CamelMTConnectCategory** (consumer) Constant: [`CATEGORY`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#CATEGORY) | 
The data item category from the probe.

Enum values:

-   SAMPLE
    
-   EVENT
    
-   CONDITION
    





 |  | String |
| **CamelMTConnectType** (consumer) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#TYPE) | The data item type from the probe, such as POSITION or EXECUTION. |  | String |
| **CamelMTConnectSubType** (consumer) Constant: [`SUB_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#SUB_TYPE) | The data item subtype, such as ACTUAL. |  | String |
| **CamelMTConnectUnits** (consumer) Constant: [`UNITS`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#UNITS) | The units of the value from the probe. |  | String |
| **CamelMTConnectNativeUnits** (consumer) Constant: [`NATIVE_UNITS`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#NATIVE_UNITS) | The native units of the data item from the probe. |  | String |
| **CamelMTConnectRepresentation** (consumer) Constant: [`REPRESENTATION`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#REPRESENTATION) | 

The data item representation from the probe; VALUE when the probe names none.

Enum values:

-   VALUE
    
-   DATA\_SET
    
-   TABLE
    
-   TIME\_SERIES
    
-   DISCRETE
    





 |  | String |
| **CamelMTConnectSequence** (consumer) Constant: [`SEQUENCE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#SEQUENCE) | The sequence number the agent gave the observation. |  | Long |
| **CamelMTConnectTimestamp** (consumer) Constant: [`TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#TIMESTAMP) | The observation timestamp, the time the failure was detected for a Bad message without an observation, or on asset messages the asset’s timestamp: that of its AssetRemoved observation when the agent no longer holds it. |  | Instant |
| **CamelMTConnectInstanceId** (common) Constant: [`INSTANCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#INSTANCE_ID) | The instance id of the agent; it changes when the agent restarts. Set on consumer messages and producer replies. |  | Long |
| **CamelMTConnectQuality** (consumer) Constant: [`QUALITY`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#QUALITY) | 

Good, or Bad when the agent reports the value UNAVAILABLE or cannot be read.

Enum values:

-   Good
    
-   Bad
    





 |  | String |
| **CamelMTConnectReason** (consumer) Constant: [`REASON`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#REASON) | 

Why the quality is Bad: the agent reports UNAVAILABLE, the agent is unreachable, or the agent answered with an error.

Enum values:

-   UNAVAILABLE
    
-   UNREACHABLE
    
-   ERROR
    





 |  | String |
| **CamelMTConnectError** (consumer) Constant: [`ERROR`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#ERROR) | The failure behind a Bad message without an observation: the HTTP status, the parser message or the transport error. |  | String |
| **CamelMTConnectLevel** (consumer) Constant: [`LEVEL`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#LEVEL) | 

The level of a condition.

Enum values:

-   Normal
    
-   Warning
    
-   Fault
    
-   Unavailable
    





 |  | String |
| **CamelMTConnectNativeCode** (consumer) Constant: [`NATIVE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#NATIVE_CODE) | The native code of a condition. |  | String |
| **CamelMTConnectNativeSeverity** (consumer) Constant: [`NATIVE_SEVERITY`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#NATIVE_SEVERITY) | The native severity of a condition. |  | String |
| **CamelMTConnectQualifier** (consumer) Constant: [`QUALIFIER`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#QUALIFIER) | The qualifier of a condition, such as HIGH or LOW. |  | String |
| **CamelMTConnectDocument** (consumer) Constant: [`DOCUMENT`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DOCUMENT) | 

The agent document the message came from: Current or Sample for an observation, Asset for an asset message.

Enum values:

-   Current
    
-   Sample
    
-   Asset
    





 |  | String |
| **CamelMTConnectResync** (consumer) Constant: [`RESYNC`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#RESYNC) | 

Set on the Current messages that follow a resynchronisation: the agent’s buffer no longer held the next observation, or the agent restarted.

Enum values:

-   OUT\_OF\_RANGE
    
-   INSTANCE\_CHANGED
    





 |  | String |
| **CamelMTConnectCompositionId** (consumer) Constant: [`COMPOSITION_ID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#COMPOSITION_ID) | The compositionId attribute of the observation: the id of the component composition the data item belongs to. |  | String |
| **CamelMTConnectResetTriggered** (consumer) Constant: [`RESET_TRIGGERED`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#RESET_TRIGGERED) | The resetTriggered attribute of the observation, such as MANUAL or DAY: the value was reset, so it does not continue the previous one. A data set or table observation with it is the whole set, not a change. |  | String |
| **CamelMTConnectStatistic** (consumer) Constant: [`STATISTIC`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#STATISTIC) | The statistic attribute of the observation, such as AVERAGE or MAXIMUM. |  | String |
| **CamelMTConnectDuration** (consumer) Constant: [`DURATION`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#DURATION) | The duration attribute of the observation: the time in seconds the statistic covers. |  | BigDecimal |
| **CamelMTConnectSampleRate** (consumer) Constant: [`SAMPLE_RATE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#SAMPLE_RATE) | The sampleRate attribute of a time series observation: samples per second. |  | BigDecimal |
| **CamelMTConnectAssetType** (common) Constant: [`ASSET_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#ASSET_TYPE) | The asset type, such as CuttingTool: on the consumer the type of an asset message, or the assetType attribute of an AssetChanged or AssetRemoved observation; on the producer the type of the assets request, overriding the assetType option for one message. |  | String |
| **CamelMTConnectAssetId** (common) Constant: [`ASSET_ID`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#ASSET_ID) | The asset id: on the consumer the id of an asset message; on the producer the asset the assets request reads, or several ids separated by a semicolon, with which assetType, count and removed do not apply. |  | String |
| **CamelMTConnectAssetRemoved** (consumer) Constant: [`ASSET_REMOVED`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#ASSET_REMOVED) | Whether the asset message reports a removed asset: the agent marked it removed, or reported AssetRemoved for it. The body is null when the agent no longer holds the asset. |  | Boolean |
| **CamelMTConnectOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#OPERATION) | 

The request to send, overriding the operation option for one message.

Enum values:

-   probe
    
-   current
    
-   sample
    
-   assets
    





 |  | String |
| **CamelMTConnectAt** (producer) Constant: [`AT`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#AT) | The sequence at which the current request reads the values, overriding the at option for one message. |  | Long |
| **CamelMTConnectFrom** (producer) Constant: [`FROM`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#FROM) | The first sequence of the sample request, overriding the from option for one message. |  | Long |
| **CamelMTConnectTo** (producer) Constant: [`TO`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#TO) | The last sequence the sample request includes, overriding the to option for one message. |  | Long |
| **CamelMTConnectCount** (producer) Constant: [`COUNT`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#COUNT) | The maximum number of observations of the sample request or of assets of the assets request, overriding the count option for one message. |  | Integer |
| **CamelMTConnectFirstSequence** (producer) Constant: [`FIRST_SEQUENCE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#FIRST_SEQUENCE) | The oldest sequence the agent still buffers, from the reply’s header. |  | Long |
| **CamelMTConnectLastSequence** (producer) Constant: [`LAST_SEQUENCE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#LAST_SEQUENCE) | The newest sequence the agent holds, from the reply’s header. |  | Long |
| **CamelMTConnectNextSequence** (producer) Constant: [`NEXT_SEQUENCE`](https://javadoc.io/doc/org.apache.camel/camel-mtconnect/latest/org/apache/camel/component/mtconnect/MTConnectConstants.html#NEXT_SEQUENCE) | The sequence that follows the reply: the from of the next sample request that continues it. |  | Long |

## Usage

### Consumer

The consumer runs the MTConnect HTTP binding against the agent, by default on one thread per endpoint with the streaming sample request:

1.  **Probe** (`/<device>/probe`) keeps per data item its name, category, type, subtype, units, native units, representation and owning component, the device uuid and name, the agent’s instance id and its buffer size. The `count` option is lowered to the buffer size.
    
2.  **Current** (`/<device>/current`) delivers one message per observation with document `Current`; the header’s `nextSequence` becomes the cursor.
    
3.  **Stream** (`/<device>/sample?from&count&interval&heartbeat`): the response stays open and each multipart part is a complete streams document. Observations are delivered in sequence order, the part’s `nextSequence` becomes the cursor, and a part without observations is a heartbeat.
    

Documents are parsed by local element name, so the 1.x and 2.x schema namespaces and vendor namespaces read the same way. External entities and DTDs are disabled. The stream is `multipart/mixed` on 2.x agents and `multipart/x-mixed-replace` on 1.x agents.

 
| Event | What the consumer does |
| --- | --- |
| A document carries another instance id than the stored one (the agent restarted) | probe again, then current with resync `INSTANCE_CHANGED`, then stream |
| An `MTConnectError` with `OUT_OF_RANGE`, whatever the HTTP status (1.x agents send 200) | current with resync `OUT_OF_RANGE`, then stream from its `nextSequence` |
| Any other `MTConnectError`, such as `NO_DEVICE` | an outage with reason `ERROR` and the agent’s error code and text, the exception handler once per outage, then probe again after `reconnectDelay` |
| The agent ends the stream without an error | stream again from the cursor after `reconnectDelay`; nothing is delivered |
| Connection refused or not established within `connectTimeout`, no response headers within `readTimeout`, no part within two heartbeats, a broken transfer | an outage with reason `UNREACHABLE`, then the same step again after `reconnectDelay` |
| An HTTP error status without an MTConnect error document, or a body that is not an MTConnect document | an outage with reason `ERROR` naming the status or the parser message, then the same step again after `reconnectDelay` |

#### Polling instead of streaming

With `streaming=false` the consumer is a scheduled poll consumer around the same protocol, for agents behind a proxy or firewall that cuts long-lived responses. Each poll performs the next step: the probe, the current, or one `/<device>/sample?from=<cursor>&count` request without `interval`, which the agent answers with one document. Cursor, outages, `Bad` messages, the `OUT_OF_RANGE` resynchronisation and the re-probe on a new instance id are those of streaming. Silence is detected by `readTimeout`; the scheduler’s `delay` is also the wait after a failure; `interval`, `heartbeat` and `reconnectDelay` apply to streaming only. A poll returns the number of messages it delivered, so `greedy=true` polls again at once while a backlog drains. There is no automatic fallback: an agent that answers the streaming request with one document instead of a stream is reported as an outage with reason `ERROR` and the text `The agent answered the sample request without streaming; read it with streaming=false`.

#### Outages

The first failure after a healthy period sends one message per known data item with a null body, quality `Bad`, reason `UNREACHABLE` or `ERROR` and the failure text in `CamelMTConnectError`. Retries during the same outage send nothing more. Known items are every probe item, or with `path` the items the agent has returned since the probe.

On recovery the stream resumes from the cursor, so the observations the agent still buffers arrive first, in order. Once the stream has caught up, the consumer reads current once and sends a `Current` message for every item that was reported `Bad` and that the catch-up did not touch. Every item turns `Good` again and no observation is delivered twice. An agent that reports `UNAVAILABLE` sends an observation, not a failure: it arrives with quality `Bad`, reason `UNAVAILABLE` and a null body.

A route that wants good values only filters on the quality header:

```java
from("mtconnect:http://agent:5000?device=Mill-1")
    .filter(simple("${header.CamelMTConnectQuality} == 'Good'"))
    .to("kafka:observations");
```

Stopping the route does not wait for an agent that sends nothing: the request in flight is cancelled and the stream closed, so a stop during an outage returns at once.

#### Message body

 
| Observation | Body |
| --- | --- |
| Sample | `BigDecimal`; a time series as `List<BigDecimal>`; the text when the value is not a number |
| Event | the text as the agent sent it |
| Data set, table | `Map` of entry key to value (a table entry is a `Map` of cell key to value); a removed entry maps to null |
| Condition | the condition text, or null; the level, native code, native severity and qualifier are headers |
| `UNAVAILABLE`, outage | null |

The metadata of the observation and of its data item from the probe are the `CamelMTConnect*` headers listed above. The data set and table `count` and the time series `sampleCount` attributes have no header: they equal the size of the body.

#### Assets

With `assets=true` the consumer also sends asset messages; `AssetChanged` and `AssetRemoved` arrive as observations either way.

-   After each current (the first one, and after every resynchronisation or agent restart) it reads `/assets?device=<device>&type=<assetType>&count=<assetBufferSize>&removed=true` and sends one message per asset, removed assets with `CamelMTConnectAssetRemoved=true`. A removal whose `AssetRemoved` event an overrun or an agent restart lost therefore still reaches the route.
    
-   For each `AssetChanged` observation it reads `/asset/<id>` after the observations of that document and sends the asset; for each `AssetRemoved` observation it sends the asset with `CamelMTConnectAssetRemoved=true`, or, when the agent answers `ASSET_NOT_FOUND`, a message with a null body, the removed flag and the observation’s asset id, type, device and time.
    
-   An asset is not sent again when its timestamp and removed flag equal those last sent for its id.
    
-   Asset reads fail like any other request. Asset messages never carry a quality.
    

The body is the asset element as a standalone XML document (`String`) with the namespace declarations of the agent’s document root, so vendor extensions survive. Routes read it with `xpath`, `xslt` or a data format; there is no typed asset model.

### Producer

A `to` endpoint sends one request per exchange and sets the answer as the body. The request is the `operation` option or the `CamelMTConnectOperation` header; with neither, the exchange fails.

  
| Operation | Request | Body |
| --- | --- | --- |
| `probe` | `/<device>/probe` | the agent’s `MTConnectDevices` document as received, as a `String` |
| `current` | `/<device>/current?at&path` | `List<Map<String, Object>>`, one map per observation |
| `sample` | `/<device>/sample?from&to&count&path`, answered with one document | `List<Map<String, Object>>` |
| `assets` | `/assets?device&type&count&removed`, or `/asset/<id>[;<id>…​]` with `CamelMTConnectAssetId` | the agent’s `MTConnectAssets` document as received, as a `String` |

An observation map holds the consumer’s headers without the `CamelMTConnect` prefix (`DataItemId`, `Category`, `Units`, `Sequence`, `Quality`, `Document`, …​) and the value under `value`; one mapping fills both. The maps carry the probe’s metadata, so the producer reads the probe on first use and again when a reply carries another instance id. `count` is lowered to the agent’s buffer size, because agents reject a larger one. The reply headers are `CamelMTConnectInstanceId` and, for `current` and `sample`, `CamelMTConnectFirstSequence`, `CamelMTConnectLastSequence` and `CamelMTConnectNextSequence`; a route pages through a range by sending the next `sample` from `CamelMTConnectNextSequence`. Start a range at a sequence the route has received, such as that header: on a busy agent the `firstSequence` of one reply can already have left the buffer by the next request, which the agent answers with `OUT_OF_RANGE`.

 
| Answer | Exchange |
| --- | --- |
| An `MTConnectError` document, whatever the HTTP status, `OUT_OF_RANGE` included | fails with `MTConnectErrorException`, whose `getErrorCodes()` and `getErrorTexts()` hold the agent’s codes and texts |
| An HTTP error status without one, a body that is not an MTConnect document, another document than expected | fails with `CamelExchangeException` naming the status, the parser message or the document the agent answered with |
| Connection refused, no response headers within `readTimeout`, nothing for `readTimeout` while the body arrives | fails with `CamelExchangeException` whose cause is the transport exception |

The producer has no outage state and sends no `Bad` messages; the route’s error handling applies.

### TLS and compression

An `https` agent is read with the SSL context of the endpoint’s `sslContextParameters` or, when the component’s `useGlobalSslContextParameters` is set, with the global SSL context parameters of the CamelContext. Without either, the runtime’s default trust applies. An untrusted certificate is an outage with reason `UNREACHABLE` for the consumer and fails the producer’s exchange with the handshake exception as the cause.

Requests whose answer is one document send `Accept-Encoding: gzip` and decode a compressed answer. The streaming sample request asks for no encoding, because the stream is read part by part.

## Examples

Receive every observation of one device and keep the good values:

-   Java
    
-   YAML
    

```java
from("mtconnect:http://agent:5000?device=Mill-1&heartbeat=5000")
    .filter(simple("${header.CamelMTConnectQuality} == 'Good'"))
    .log("${header.CamelMTConnectDataItemId} = ${body} ${header.CamelMTConnectUnits}");
```

```yaml
- route:
    from:
      uri: "mtconnect:http://agent:5000"
      parameters:
        device: Mill-1
        heartbeat: 5000
      steps:
        - filter:
            expression:
              simple:
                expression: "${header.CamelMTConnectQuality} == 'Good'"
            steps:
              - log:
                  message: "${header.CamelMTConnectDataItemId} = ${body} ${header.CamelMTConnectUnits}"
```

Poll an agent behind a proxy that cuts long-lived responses, and receive its cutting tools as well:

```java
from("mtconnect:http://agent:5000?device=Mill-1&streaming=false&delay=1000&assets=true&assetType=CuttingTool")
    .choice()
        .when(header("CamelMTConnectDocument").isEqualTo("Asset"))
            .to("file:tools?fileName=${header.CamelMTConnectAssetId}.xml")
        .otherwise()
            .to("seda:observations");
```

Read the device model on demand, and the observations of a sequence range:

```java
from("direct:probe")
    .to("mtconnect:http://agent:5000?device=Mill-1&operation=probe");

from("direct:range")
    .setHeader("CamelMTConnectFrom", constant(4017657L))
    .setHeader("CamelMTConnectCount", constant(500))
    .to("mtconnect:http://agent:5000?device=Mill-1&operation=sample")
    .split(body())
        .log("${body[DataItemId]} at ${body[Sequence]} = ${body[value]}");
```

Read an `https` agent whose certificate a private authority signed:

```java
KeyStoreParameters trust = new KeyStoreParameters();
trust.setResource("file:/etc/mtconnect/truststore.p12");
trust.setPassword("changeit");
TrustManagersParameters trustManagers = new TrustManagersParameters();
trustManagers.setKeyStore(trust);
SSLContextParameters ssl = new SSLContextParameters();
ssl.setTrustManagers(trustManagers);
context.getRegistry().bind("agentTls", ssl);

from("mtconnect:https://agent:5443?device=Mill-1&sslContextParameters=#agentTls")
    .to("log:observations");
```

## Notes

-   The producer holds the whole answer in memory; `count`, at most the agent’s buffer size, bounds the sample and assets answers.
    
-   The polling consumer reports failures itself, as an outage with `Bad` messages, and the poll returns 0 instead of throwing, so the scheduler’s `pollStrategy` never sees a failure.
    
-   The component requests and reads XML. The JSON documents and the MQTT binding of MTConnect 2.x are not supported.