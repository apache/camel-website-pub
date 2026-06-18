# IEC 60870 Client

> **Warning**
> **Deprecated:** This iec60870-client is deprecated and may be removed in a future release.

**Since Camel 2.20**

**Both producer and consumer are supported**

The IEC 60870-5-104 Client component provides access to IEC 60870 servers using the [Eclipse NeoSCADA](http://eclipse.org/eclipsescada) implementation.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-iec60870</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI syntax of the endpoint is:

iec60870-client:host:port/00-01-02-03-04

The information object address is encoded in the path in the syntax above. Please note that always the full, 5-octet address format is being used. Unused octets have to be filled with zero.

A connection instance if identified by the host and port part of the URI, plus all parameters in the _"id"_ group. If a new connection id is encountered, the connection options will be evaluated and the connection instance is created with those options.

> **Note**
> If two URIs specify the same connection (host, port, …​) but different connection options, then it is undefined which of those connection options will be used.

The final connection options will be evaluated in the following order:

-   If present, the `connectionOptions` parameter will be used
    
-   Otherwise, the `defaultConnectionOptions` instance is copied and customized in the following steps
    
-   Apply `protocolOptions` if present
    
-   Apply `dataModuleOptions` if present
    
-   Apply all explicit connection parameters (e.g. `timeZone`)
    

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

The IEC 60870 Client component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultConnectionOptions** (common) | Default connection options. |  | ClientOptions |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The IEC 60870 Client endpoint is configured using URI syntax:

iec60870-client:uriPath

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uriPath** (common) | **Required** The object information address. |  | ObjectAddress |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataModuleOptions** (common) | Data module options. |  | DataModuleOptions |
| **protocolOptions** (common) | Protocol options. |  | ProtocolOptions |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **acknowledgeWindow** (connection) | Parameter W - Acknowledgment window. | 10 | short |
| **adsuAddressType** (connection) | 

The common ASDU address size. May be either SIZE\_1 or SIZE\_2.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    





 |  | ASDUAddressType |
| **causeOfTransmissionType** (connection) | 

The cause of transmission type. May be either SIZE\_1 or SIZE\_2.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    





 |  | CauseOfTransmissionType |
| **informationObjectAddressType** (connection) | 

The information address size. May be either SIZE\_1, SIZE\_2 or SIZE\_3.

Enum values:

-   SIZE\_1
    
-   SIZE\_2
    
-   SIZE\_3
    





 |  | InformationObjectAddressType |
| **maxUnacknowledged** (connection) | Parameter K - Maximum number of un-acknowledged messages. | 15 | short |
| **timeout1** (connection) | Timeout T1 in milliseconds. | 15000 | int |
| **timeout2** (connection) | Timeout T2 in milliseconds. | 10000 | int |
| **timeout3** (connection) | Timeout T3 in milliseconds. | 20000 | int |
| **causeSourceAddress** (data) | Whether to include the source address. |  | byte |
| **connectionTimeout** (data) | Timeout in millis to wait for client to establish a connected connection. | 10000 | int |
| **ignoreBackgroundScan** (data) | Whether background scan transmissions should be ignored. | true | boolean |
| **ignoreDaylightSavingTime** (data) | Whether to ignore or respect DST. | false | boolean |
| **timeZone** (data) | The timezone to use. May be any Java time zone string. | UTC | TimeZone |
| **connectionId** (id) | An identifier grouping connection instances. |  | String |

## Message Headers

The IEC 60870 Client component supports 15 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIec60870Value** (consumer) Constant: [`IEC60870_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_VALUE) | The value. |  | Object |
| **CamelIec60870Timestamp** (consumer) Constant: [`IEC60870_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_TIMESTAMP) | The timestamp of the value. |  | long |
| **CamelIec60870Quality** (consumer) Constant: [`IEC60870_QUALITY`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QUALITY) | The quality information of the value. |  | QualityInformation |
| **CamelIec60870Overflow** (consumer) Constant: [`IEC60870_OVERFLOW`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_OVERFLOW) | Is overflow. |  | boolean |
| **CamelIec60870ConnectionState** (consumer) Constant: [`IEC60870_CONNECTION_STATE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_CONNECTION_STATE) | 
The connection state (CONNECTED, DISCONNECTED, etc.).

Enum values:

-   SLEEPING
    
-   DISCONNECTED
    
-   LOOKUP
    
-   CONNECTING
    
-   CONNECTED
    





 |  | State |
| **CamelIec60870ConnectionError** (consumer) Constant: [`IEC60870_CONNECTION_ERROR`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_CONNECTION_ERROR) | The connection state error if any. |  | Throwable |
| **CamelIec60870ConnectionUptime** (consumer) Constant: [`IEC60870_CONNECTION_UPTIME`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_CONNECTION_UPTIME) | Connection uptime in milliseconds since last connected. |  | long |
| **CamelIec60870CommandType** (producer) Constant: [`IEC60870_COMMAND_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_COMMAND_TYPE) | The command type: 'value' (default), 'interrogation', 'read', or 'status'. |  | String |
| **CamelIec60870AsduAddress** (producer) Constant: [`IEC60870_ASDU_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_ASDU_ADDRESS) | The ASDU address for interrogation (optional, defaults to broadcast). |  | ASDUAddress |
| **CamelIec60870Qoi** (producer) Constant: [`IEC60870_QOI`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QOI) | The qualifier of interrogation: 20 (global) or 21-36 (groups 1-16). |  | short |
| **CamelIec60870QualityBlocked** (consumer) Constant: [`IEC60870_QUALITY_BLOCKED`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QUALITY_BLOCKED) | Quality flag: Blocked (BL). |  | boolean |
| **CamelIec60870QualitySubstituted** (consumer) Constant: [`IEC60870_QUALITY_SUBSTITUTED`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QUALITY_SUBSTITUTED) | Quality flag: Substituted (SB). |  | boolean |
| **CamelIec60870QualityNotTopical** (consumer) Constant: [`IEC60870_QUALITY_NOT_TOPICAL`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QUALITY_NOT_TOPICAL) | Quality flag: Not topical (NT). |  | boolean |
| **CamelIec60870QualityValid** (consumer) Constant: [`IEC60870_QUALITY_VALID`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_QUALITY_VALID) | Quality flag: Invalid (IV). |  | boolean |
| **CamelIec60870CauseOfTransmission** (consumer) Constant: [`IEC60870_CAUSE_OF_TRANSMISSION`](https://javadoc.io/doc/org.apache.camel/camel-iec60870/latest/org/apache/camel/component/iec60870/Constants.html#IEC60870_CAUSE_OF_TRANSMISSION) | The cause of transmission. |  | CauseOfTransmission |

## Producer Command Types

The producer supports different command types via the `CamelIec60870CommandType` header:

 
| Command Type | Description |
| --- | --- |
| `value` | Send value command (default). Body type determines command: Boolean→Single, Integer→Scaled, Float→Float setpoint. |
| `interrogation` | Trigger interrogation (C\_IC\_NA\_1). Use `CamelIec60870Qoi` header for group interrogation (21-36). |
| `read` | Read single data point (C\_RD\_NA\_1). |
| `status` | Get connection state only. No protocol command sent. |

### Getting Connection Status (Producer)

_Java-only: using ProducerTemplate to send and inspect connection state headers_

```java
from("direct:status")
    .setHeader("CamelIec60870CommandType", constant("status"))
    .to("iec60870-client:localhost:2404/00-01-00-00-01");

// Usage
Exchange result = producerTemplate.send("direct:status", e -> {});
State state = result.getMessage().getHeader("CamelIec60870ConnectionState", State.class);
Long uptime = result.getMessage().getHeader("CamelIec60870ConnectionUptime", Long.class);
```

### Triggering Interrogation

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:interrogate")
    .setHeader("CamelIec60870CommandType", constant("interrogation"))
    .to("iec60870-client:localhost:2404/00-01-00-00-01");

from("direct:interrogateGroup")
    .setHeader("CamelIec60870CommandType", constant("interrogation"))
    .setHeader("CamelIec60870Qoi", constant((short) 21))
    .to("iec60870-client:localhost:2404/00-01-00-00-01");
```

```xml
<route>
  <from uri="direct:interrogate"/>
  <setHeader name="CamelIec60870CommandType">
    <constant>interrogation</constant>
  </setHeader>
  <to uri="iec60870-client:localhost:2404/00-01-00-00-01"/>
</route>

<route>
  <from uri="direct:interrogateGroup"/>
  <setHeader name="CamelIec60870CommandType">
    <constant>interrogation</constant>
  </setHeader>
  <setHeader name="CamelIec60870Qoi">
    <constant>21</constant>
  </setHeader>
  <to uri="iec60870-client:localhost:2404/00-01-00-00-01"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:interrogate
      steps:
        - setHeader:
            name: CamelIec60870CommandType
            constant: interrogation
        - to:
            uri: iec60870-client:localhost:2404/00-01-00-00-01

- route:
    from:
      uri: direct:interrogateGroup
      steps:
        - setHeader:
            name: CamelIec60870CommandType
            constant: interrogation
        - setHeader:
            name: CamelIec60870Qoi
            constant: 21
        - to:
            uri: iec60870-client:localhost:2404/00-01-00-00-01
```

### Sending Value Commands

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:bool").setBody(constant(true))
    .to("iec60870-client:localhost:2404/00-01-00-00-01");

from("direct:float").setBody(constant(42.5f))
    .to("iec60870-client:localhost:2404/00-01-00-00-01");
```

```xml
<route>
  <from uri="direct:bool"/>
  <setBody>
    <constant>true</constant>
  </setBody>
  <to uri="iec60870-client:localhost:2404/00-01-00-00-01"/>
</route>

<route>
  <from uri="direct:float"/>
  <setBody>
    <constant>42.5</constant>
  </setBody>
  <to uri="iec60870-client:localhost:2404/00-01-00-00-01"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:bool
      steps:
        - setBody:
            constant: true
        - to:
            uri: iec60870-client:localhost:2404/00-01-00-00-01

- route:
    from:
      uri: direct:float
      steps:
        - setBody:
            constant: 42.5
        - to:
            uri: iec60870-client:localhost:2404/00-01-00-00-01
```

## Consumer Examples

Each message received by the consumer includes connection state and quality headers.

### Getting Connection Status (Consumer)

_Java-only: using a Processor lambda to access typed connection state and quality headers_

```java
from("iec60870-client:localhost:2404/00-01-00-00-01")
    .process(exchange -> {
        // Connection state is included in every message
        State state = exchange.getIn().getHeader("CamelIec60870ConnectionState", State.class);
        Long uptime = exchange.getIn().getHeader("CamelIec60870ConnectionUptime", Long.class);

        // Get the value and quality
        Object value = exchange.getIn().getHeader("CamelIec60870Value");
        Boolean valid = exchange.getIn().getHeader("CamelIec60870QualityValid", Boolean.class);

        log.info("State: {}, Uptime: {} ms, Value: {}, Valid: {}", state, uptime, value, valid);
    })
    .to("log:values");
```

### Filtering by Quality

-   Java
    
-   XML
    
-   YAML
    

```java
from("iec60870-client:localhost:2404/00-01-00-00-01")
    .filter(header("CamelIec60870QualityValid").isEqualTo(true))
    .log("Good value: ${header.CamelIec60870Value}")
    .to("seda:process");
```

```xml
<route>
  <from uri="iec60870-client:localhost:2404/00-01-00-00-01"/>
  <filter>
    <simple>${header.CamelIec60870QualityValid} == true</simple>
    <log message="Good value: ${header.CamelIec60870Value}"/>
    <to uri="seda:process"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: iec60870-client:localhost:2404/00-01-00-00-01
      steps:
        - filter:
            simple: "${header.CamelIec60870QualityValid} == true"
            steps:
              - log: "Good value: ${header.CamelIec60870Value}"
              - to:
                  uri: seda:process
```

## Spring Boot Auto-Configuration

When using iec60870-client with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-iec60870-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.iec60870-client.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.iec60870-client.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.iec60870-client.default-connection-options** | Default connection options. The option is a org.apache.camel.component.iec60870.client.ClientOptions type. |  | ClientOptions |
| **camel.component.iec60870-client.enabled** | Whether to enable auto configuration of the iec60870-client component. This is enabled by default. |  | Boolean |
| **camel.component.iec60870-client.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.iec60870-server.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.iec60870-server.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.iec60870-server.default-connection-options** | Default connection options. The option is a org.apache.camel.component.iec60870.server.ServerOptions type. |  | ServerOptions |
| **camel.component.iec60870-server.enabled** | Whether to enable auto configuration of the iec60870-server component. This is enabled by default. |  | Boolean |
| **camel.component.iec60870-server.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |