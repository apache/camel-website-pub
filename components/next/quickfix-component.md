# QuickFix

**Since Camel 2.1**

**Both producer and consumer are supported**

The Quickfix component adapts the [QuickFIX/J](http://www.quickfixj.org/) FIX engine for using in Camel. This component uses the standard [Financial Interchange (FIX) protocol](http://www.fixprotocol.org/) for message transport.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-quickfix</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

quickfix:configFile\[?sessionID=sessionID&lazyCreateEngine=true|false\]

The `configFile` is the name of the QuickFIX/J configuration to use for the FIX engine (located as a resource found in your classpath). The optional `sessionID` identifies a specific FIX session. The format of the sessionID is:

(BeginString):(SenderCompID)\[/(SenderSubID)\[/(SenderLocationID)\]\]->(TargetCompID)\[/(TargetSubID)\[/(TargetLocationID)\]\]

The optional `lazyCreateEngine` parameter allows creating QuickFIX/J engine on demand:

-   The value `true` means the engine is started when the first message is sent or there’s consumer configured in route definition.
    
-   When the value `false` is used, the engine is started at the endpoint creation.
    

When this parameter is missing, the value of component’s property `lazyCreateEngines` is being used.

Example URIs:

quickfix:config.cfg

quickfix:config.cfg?sessionID=FIX.4.2:MyTradingCompany->SomeExchange

quickfix:config.cfg?sessionID=FIX.4.2:MyTradingCompany->SomeExchange&lazyCreateEngine=true

## Endpoints

FIX sessions are endpoints for the quickfix component. An endpoint URI may specify a single session or all sessions managed by a specific QuickFIX/J engine. Typical applications will use only one FIX engine, but advanced users may create multiple FIX engines by referencing different configuration files in quickfix component endpoint URIs.

When a consumer does not include a session ID in the endpoint URI, it will receive exchanges for all sessions managed by the FIX engine associated with the configuration file specified in the URI. If a producer does not specify a session in the endpoint URI, then it must include the session-related fields in the FIX message being sent. If a session is specified in the URI, then the component will automatically inject the session-related fields into the FIX message.

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

The QuickFix component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eagerStopEngines** (common) | Whether to eager stop engines when there are no active consumer or producers using the engine. For example when stopping a route, then the engine can be stopped as well. And when the route is started, then the engine is started again. This can be turned off to only stop the engines when Camel is shutdown. | true | boolean |
| **lazyCreateEngines** (common) | If set to true, the engines will be created and started when needed (when first message is send). | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **logFactory** (advanced) | To use the given LogFactory. |  | LogFactory |
| **messageFactory** (advanced) | To use the given MessageFactory. |  | MessageFactory |
| **messageStoreFactory** (advanced) | To use the given MessageStoreFactory. |  | MessageStoreFactory |

## Endpoint Options

The QuickFix endpoint is configured using URI syntax:

quickfix:configurationName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationName** (common) | **Required** Path to the quickfix configuration file. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the configuration file using these protocols (classpath is default). ref will lookup the configuration file in the registry. bean will call a method on a bean to be used as the configuration. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyCreateEngine** (common) | This option allows creating QuickFIX/J engine on demand. Value true means the engine is started when first message is send or there’s consumer configured in route definition. When false value is used, the engine is started at the endpoint creation. When this parameter is missing, the value of component’s property lazyCreateEngines is being used. | false | boolean |
| **sessionID** (common) | The optional sessionID identifies a specific FIX session. The format of the sessionID is: (BeginString):(SenderCompID)/(SenderSubID)/(SenderLocationID)-(TargetCompID)/(TargetSubID)/(TargetLocationID). |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The QuickFix component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **EventCategory** (common) Constant: [`EVENT_CATEGORY_KEY`](https://javadoc.io/doc/org.apache.camel/camel-quickfix/latest/org/apache/camel/component/quickfixj/QuickfixjEndpoint.html#EVENT_CATEGORY_KEY) | 
The event category.

Enum values:

-   AppMessageReceived
    
-   AppMessageSent
    
-   AdminMessageReceived
    
-   AdminMessageSent
    
-   SessionCreated
    
-   SessionLogon
    
-   SessionLogoff
    





 |  | QuickfixjEventCategory |
| **SessionID** (common) Constant: [`SESSION_ID_KEY`](https://javadoc.io/doc/org.apache.camel/camel-quickfix/latest/org/apache/camel/component/quickfixj/QuickfixjEndpoint.html#SESSION_ID_KEY) | The FIX message SessionID. |  | SessionID |
| **MessageType** (common) Constant: [`MESSAGE_TYPE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-quickfix/latest/org/apache/camel/component/quickfixj/QuickfixjEndpoint.html#MESSAGE_TYPE_KEY) | The FIX MsgType tag value. |  | String |

## Usage

The DataDictionary header is useful if string messages are being received and need to be parsed in a route. QuickFIX/J requires a data dictionary to parse certain types of messages (with repeating groups, for example). By injecting a DataDictionary header in the route after receiving a message string, the FIX engine can properly parse the data.

### QuickFIX/J Configuration Extensions

When using QuickFIX/J directly, one typically writes code to create instances of logging adapters, message stores, and communication connectors. The quickfix component will automatically create instances of these classes based on information in the configuration file. It also provides defaults for many of the commonly required settings and adds additional capabilities (like the ability to activate JMX support).

The following sections describe how the quickfix component processes the QuickFIX/J configuration. For comprehensive information about QuickFIX/J configuration, see the [user manual](http://www.quickfixj.org/quickfixj/usermanual/usage/configuration.md).

#### Communication Connectors

When the component detects an initiator or acceptor session setting in the QuickFIX/J configuration file, it will automatically create the corresponding initiator and/or acceptor connector. These settings can be in the default or in a specific session section of the configuration file.

 
| Session Setting | Component Action |
| --- | --- |
| `ConnectionType=initiator` | Create an initiator connector |
| `ConnectionType=acceptor` | Create an acceptor connector |

The threading model for the QuickFIX/J session connectors can also be specified. These settings affect all sessions in the configuration file and must be placed in the settings default section.

 
| Default/Global Setting | Component Action |
| --- | --- |
| `ThreadModel=ThreadPerConnector` | Use `SocketInitiator` or `SocketAcceptor` (default) |
| `ThreadModel=ThreadPerSession` | Use `ThreadedSocketInitiator` or `ThreadedSocketAcceptor` |

#### Logging

The QuickFIX/J logger implementation can be specified by including the following settings in the default section of the configuration file. The `ScreenLog` is the default if none of the following settings are present in the configuration. It’s an error to include settings that imply more than one log implementation. The log factory implementation can also be set directly on the Quickfix component. This will override any related values in the QuickFIX/J settings file.

 
| Default/Global Setting | Component Action |
| --- | --- |
| `ScreenLogShowEvents` | Use a `ScreenLog` |
| `ScreenLogShowIncoming` | Use a `ScreenLog` |
| `ScreenLogShowOutgoing` | Use a `ScreenLog` |
| `SLF4J*` | Use a `SLF4JLog`. Any of the SLF4J settings will cause this log to be used. |
| `FileLogPath` | Use a `FileLog` |
| `JdbcDriver` | Use a `JdbcLog` |

#### Message Store

The QuickFIX/J message store implementation can be specified by including the following settings in the default section of the configuration file. The `MemoryStore` is the default if none of the following settings are present in the configuration. It’s an error to include settings that imply more than one message store implementation. The message store factory implementation can also be set directly on the Quickfix component. This will override any related values in the QuickFIX/J settings file.

 
| Default/Global Setting | Component Action |
| --- | --- |
| `JdbcDriver` | Use a `JdbcStore` |
| `FileStorePath` | Use a `FileStore` |
| `SleepycatDatabaseDir` | Use a `SleepcatStore` |

#### Message Factory

A message factory is used to construct domain objects from raw FIX messages. The default message factory is `DefaultMessageFactory`. However, advanced applications may require a custom message factory. This can be set on the QuickFIX/J component.

#### JMX

 
| Default/Global Setting | Component Action |
| --- | --- |
| `UseJmx` | if `Y`, then enable QuickFIX/J JMX |

#### Other Defaults

The component provides some default settings for what are normally required settings in QuickFIX/J configuration files. `SessionStartTime` and `SessionEndTime` default to "00:00:00", meaning the session will not be automatically started and stopped. The `HeartBtInt` (heartbeat interval) defaults to 30 seconds.

#### Minimal Initiator Configuration Example

\[SESSION\]
ConnectionType=initiator
BeginString=FIX.4.4
SenderCompID=YOUR\_SENDER
TargetCompID=YOUR\_TARGET

### Using the InOut Message Exchange Pattern

Although the FIX protocol is event-driven and asynchronous, there are specific pairs of messages that represent a request-reply message exchange. To use an InOut exchange pattern, there should be a single request message and single reply message to the request. Examples include an OrderStatusRequest message and UserRequest.

#### Implementing InOut Exchanges for Consumers

Add `exchangePattern=InOut` to the QuickFIX/J endpoint URI. The `MessageOrderStatusService` in the example below is a bean with a synchronous service method. The method returns the response to the request (an ExecutionReport in this case) which is then sent back to the requestor session.

_Java-only: route definition using Java DSL for InOut consumer exchange_

```java
    from("quickfix:examples/inprocess.qf.cfg?sessionID=FIX.4.2:MARKET->TRADER&exchangePattern=InOut")
        .filter(header(QuickfixjEndpoint.MESSAGE_TYPE_KEY).isEqualTo(MsgType.ORDER_STATUS_REQUEST))
        .bean(new MarketOrderStatusService());
```

#### Implementing InOut Exchanges for Producers

For producers, sending a message will block until a reply is received or a timeout occurs. There is no standard way to correlate reply messages in FIX. Therefore, a correlation criteria must be defined for each type of InOut exchange. The correlation criteria and timeout can be specified using `Exchange` properties.

   
| Description | Key String | Key Constant | Default |
| --- | --- | --- | --- |
| Correlation Criteria | `CorrelationCriteria` | `QuickfixjProducer.CORRELATION_CRITERIA_KEY` | None |
| Correlation Timeout in Milliseconds | `CorrelationTimeout` | `QuickfixjProducer.CORRELATION_TIMEOUT_KEY` | 1000 |

The correlation criteria is defined with a `MessagePredicate` object. The following example will treat a FIX `ExecutionReport` from the specified session where the transaction type is STATUS and the Order ID matches our request. The session ID should be for the _requestor_, the sender and target CompID fields will be reversed when looking for the reply.

_Java-only: programmatic correlation criteria setup using QuickFIX/J API_

```java
exchange.setProperty(QuickfixjProducer.CORRELATION_CRITERIA_KEY,
    new MessagePredicate(new SessionID(sessionID), MsgType.EXECUTION_REPORT)
        .withField(ExecTransType.FIELD, Integer.toString(ExecTransType.STATUS))
        .withField(OrderID.FIELD, request.getString(OrderID.FIELD)));
```

### Spring Configuration

The QuickFIX/J component includes a Spring `FactoryBean` for configuring the session settings within a Spring context. A type converter for QuickFIX/J session ID strings is also included. The following example shows a simple configuration of an acceptor and initiator session with default settings for both sessions.

```xml
<!--  camel route  -->
<camelContext xmlns="http://camel.apache.org/schema/spring" id="quickfixjContext">
    <route>
        <from uri="quickfix:example"/>
        <filter>
            <simple>${in.header.EventCategory} == 'AppMessageReceived'</simple>
            <to uri="log:test"/>
        </filter>
    </route>
</camelContext>
        <!--  quickfix component  -->
<bean id="quickfix" class="org.apache.camel.component.quickfixj.QuickfixjComponent">
<property name="engineSettings">
    <util:map>
        <entry key="quickfix:example" value-ref="quickfixjSettings"/>
    </util:map>
</property>
<property name="messageFactory">
    <bean class="org.apache.camel.component.quickfixj.QuickfixjSpringTest.CustomMessageFactory"/>
</property>
</bean>
        <!--  quickfix settings  -->
<bean id="quickfixjSettings" class="org.apache.camel.component.quickfixj.QuickfixjSettingsFactory">
<property name="defaultSettings">
    <util:map>
        <entry key="SocketConnectProtocol" value="VM_PIPE"/>
        <entry key="SocketAcceptProtocol" value="VM_PIPE"/>
        <entry key="UseDataDictionary" value="N"/>
    </util:map>
</property>
<property name="sessionSettings">
    <util:map>
        <entry key="FIX.4.2:INITIATOR->ACCEPTOR">
            <util:map>
                <entry key="ConnectionType" value="initiator"/>
                <entry key="SocketConnectHost" value="localhost"/>
                <entry key="SocketConnectPort" value="5000"/>
            </util:map>
        </entry>
        <entry key="FIX.4.2:ACCEPTOR->INITIATOR">
            <util:map>
                <entry key="ConnectionType" value="acceptor"/>
                <entry key="SocketAcceptPort" value="5000"/>
            </util:map>
        </entry>
    </util:map>
</property>
</bean>
```

The QuickFIX/J component includes a `QuickfixjConfiguration` class for configuring the session settings. A type converter for QuickFIX/J session ID strings is also included. The following example shows a simple configuration of an acceptor and initiator session with default settings for both sessions.

```xml
    <!-- camel route -->
    <camelContext id="quickfixjContext" xmlns="http://camel.apache.org/schema/spring">
        <route>
            <from uri="quickfix:example"/>
            <filter>
                <simple>${in.header.EventCategory} == 'AppMessageReceived'</simple>
                <to uri="log:test"/>
            </filter>
        </route>
        <route>
            <from uri="seda:test"/>
            <to uri="lazyQuickfix:example"/>
        </route>
    </camelContext>

    <!-- quickfix component -->
    <bean id="quickfix" class="org.apache.camel.component.quickfixj.QuickfixjComponent">
        <property name="configurations">
            <util:map>
                <entry key="example" value-ref="quickfixjConfiguration"/>
            </util:map>
        </property>
        <property name="messageFactory">
            <bean class="org.apache.camel.component.quickfixj.QuickfixjSpringTest.CustomMessageFactory"/>
        </property>
    </bean>

    <!-- lazy quickfix component -->
    <bean id="lazyQuickfix" class="org.apache.camel.component.quickfixj.QuickfixjComponent">
        <property name="lazyCreateEngines" value="true" />
        <property name="configurations">
            <util:map>
                <entry key="example" value-ref="lazyQuickfixjConfiguration"/>
            </util:map>
        </property>
        <property name="messageFactory">
            <bean class="org.apache.camel.component.quickfixj.QuickfixjSpringTest.CustomMessageFactory"/>
        </property>
    </bean>

    <!-- quickfix settings -->
    <bean id="quickfixjConfiguration" class="org.apache.camel.component.quickfixj.QuickfixjConfiguration">
        <property name="defaultSettings">
            <util:map>
                <entry key="SocketConnectProtocol" value="VM_PIPE"/>
                <entry key="SocketAcceptProtocol" value="VM_PIPE"/>
                <entry key="UseDataDictionary" value="N"/>
            </util:map>
        </property>
        <property name="sessionSettings">
            <util:map>
                <entry key="FIX.4.2:INITIATOR->ACCEPTOR">
                    <util:map>
                        <entry key="ConnectionType" value="initiator"/>
                        <entry key="SocketConnectHost" value="localhost"/>
                        <entry key="SocketConnectPort" value="5000"/>
                    </util:map>
                </entry>
                <entry key="FIX.4.2:ACCEPTOR->INITIATOR">
                    <util:map>
                        <entry key="ConnectionType" value="acceptor"/>
                        <entry key="SocketAcceptPort" value="5000"/>
                    </util:map>
                </entry>
            </util:map>
        </property>
    </bean>
```

### Exception handling

QuickFIX/J behavior can be modified if certain exceptions are thrown during processing of a message. If a `RejectLogon` exception is thrown while processing an incoming logon administrative message, then the logon will be rejected.

Normally, QuickFIX/J handles the logon process automatically. However, sometimes an outgoing logon message must be modified to include credentials required by a FIX counterparty. If the FIX logon message body is modified when sending a logon message (`EventCategory=AdminMessageSent` the modified message will be sent to the counterparty. It is important that the outgoing logon message is being processed _synchronously_. If it is processed asynchronously (on another thread), the FIX engine will immediately send the unmodified outgoing message when its callback method returns.

### FIX Sequence Number Management

If an application exception is thrown during _synchronous_ exchange processing, this will cause QuickFIX/J to not increment incoming FIX message sequence numbers and will cause a resend of the counterparty message. This FIX protocol behavior is primarily intended to handle _transport_ errors rather than application errors. There are risks associated with using this mechanism to handle application errors. The primary risk is that the message will repeatedly cause application errors each time it’s re-received. A better solution is to persist the incoming message (database, JMS queue) immediately before processing it. This also allows the application to process messages asynchronously without losing messages when errors occur.

Although it’s possible to send messages to a FIX session before it’s logged on (the messages will be sent at logon time), it is usually a better practice to wait until the session is logged on. This eliminates the required sequence number resynchronization steps at logon. Waiting for session logon can be done by setting up a route that processes the `SessionLogon` event category and signals the application to start sending messages.

See the FIX protocol specifications and the QuickFIX/J documentation for more details about FIX sequence number management.

## Examples

### Route Examples

Several examples are included in the QuickFIX/J component source code (test subdirectories). One of these examples implements a trivial trade execution simulation. The example defines an application component that uses the URI scheme "trade-executor".

The following route receives messages for the trade executor session and passes application messages to the trade executor component.

_Java-only: route definition using Java DSL to filter and forward FIX messages_

```java
from("quickfix:examples/inprocess.qf.cfg?sessionID=FIX.4.2:MARKET->TRADER").
    filter(header(QuickfixjEndpoint.EVENT_CATEGORY_KEY).isEqualTo(QuickfixjEventCategory.AppMessageReceived)).
    to("trade-executor:market");
```

The trade executor component generates messages that are routed back to the trade session. The session ID must be set in the FIX message itself since no session ID is specified in the endpoint URI.

_Java-only: route definition using Java DSL to send messages back to FIX session_

```java
from("trade-executor:market").to("quickfix:examples/inprocess.qf.cfg");
```

The trader session consumes execution report messages from the market and processes them.

_Java-only: route definition using Java DSL to consume and process execution reports_

```java
from("quickfix:examples/inprocess.qf.cfg?sessionID=FIX.4.2:TRADER->MARKET").
    filter(header(QuickfixjEndpoint.MESSAGE_TYPE_KEY).isEqualTo(MsgType.EXECUTION_REPORT)).
    bean(new MyTradeExecutionProcessor());
```

### Additional Examples

The source code contains an example called `RequestReplyExample` that demonstrates the InOut exchanges for a consumer and producer. This example creates a simple HTTP server endpoint that accepts order status requests. The HTTP request is converted to a FIX `OrderStatusRequestMessage`, is augmented with a correlation criteria, and is then routed to a quickfix endpoint. The response is then converted to a JSON-formatted string and sent back to the HTTP server endpoint to be provided as the web response.

## Spring Boot Auto-Configuration

When using quickfix with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-quickfix-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.quickfix.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.quickfix.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.quickfix.eager-stop-engines** | Whether to eager stop engines when there are no active consumer or producers using the engine. For example when stopping a route, then the engine can be stopped as well. And when the route is started, then the engine is started again. This can be turned off to only stop the engines when Camel is shutdown. | true | Boolean |
| **camel.component.quickfix.enabled** | Whether to enable auto configuration of the quickfix component. This is enabled by default. |  | Boolean |
| **camel.component.quickfix.lazy-create-engines** | If set to true, the engines will be created and started when needed (when first message is send). | false | Boolean |
| **camel.component.quickfix.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.quickfix.log-factory** | To use the given LogFactory. The option is a quickfix.LogFactory type. |  | LogFactory |
| **camel.component.quickfix.message-factory** | To use the given MessageFactory. The option is a quickfix.MessageFactory type. |  | MessageFactory |
| **camel.component.quickfix.message-store-factory** | To use the given MessageStoreFactory. The option is a quickfix.MessageStoreFactory type. |  | MessageStoreFactory |