# MLLP

**Since Camel 2.17**

**Both producer and consumer are supported**

The MLLP component is specifically designed to handle the nuances of the MLLP protocol and provide the functionality required by Healthcare providers to communicate with other systems using the MLLP protocol.

The MLLP component provides a simple configuration URI, automated HL7 acknowledgment generation, and automatic acknowledgment interrogation.

The MLLP protocol does not typically use a large number of concurrent TCP connections - a single active TCP connection is the normal case. Therefore, the MLLP component uses a simple thread-per-connection model based on standard Java Sockets. This keeps the implementation simple and eliminates the dependencies on only Camel itself.

The component supports the following:

-   A Camel consumer using a TCP Server
    
-   A Camel producer using a TCP Client
    

The MLLP component use `byte[]` payloads, and relies on Camel type conversion to convert `byte[]` to other types.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mllp</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The MLLP component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoAck** (common) | Enable/Disable the automatic generation of a MLLP Acknowledgement MLLP Consumers only. | true | boolean |
| **charsetName** (common) | Sets the default charset to use. |  | String |
| **configuration** (common) | Sets the default configuration to use when creating MLLP endpoints. |  | MllpConfiguration |
| **hl7Headers** (common) | Enable/Disable the automatic generation of message headers from the HL7 Message MLLP Consumers only. | true | boolean |
| **requireEndOfData** (common) | Enable/Disable strict compliance to the MLLP standard. The MLLP standard specifies START\_OF\_BLOCKhl7 payloadEND\_OF\_BLOCKEND\_OF\_DATA, however, some systems do not send the final END\_OF\_DATA byte. This setting controls whether or not the final END\_OF\_DATA byte is required or optional. | true | boolean |
| **stringPayload** (common) | Enable/Disable converting the payload to a String. If enabled, HL7 Payloads received from external systems will be validated converted to a String. If the charsetName property is set, that character set will be used for the conversion. If the charsetName property is not set, the value of MSH-18 will be used to determine th appropriate character set. If MSH-18 is not set, then the default ISO-8859-1 character set will be use. | true | boolean |
| **validatePayload** (common) | Enable/Disable the validation of HL7 Payloads If enabled, HL7 Payloads received from external systems will be validated (see Hl7Util.generateInvalidPayloadExceptionMessage for details on the validation). If and invalid payload is detected, a MllpInvalidMessageException (for consumers) or a MllpInvalidAcknowledgementException will be thrown. | false | boolean |
| **acceptTimeout** (consumer) | Timeout (in milliseconds) while waiting for a TCP connection TCP Server Only. | 60000 | int |
| **backlog** (consumer) | The maximum queue length for incoming connection indications (a request to connect) is set to the backlog parameter. If a connection indication arrives when the queue is full, the connection is refused. | 5 | Integer |
| **bindRetryInterval** (consumer) | TCP Server Only - The number of milliseconds to wait between bind attempts. | 5000 | int |
| **bindTimeout** (consumer) | TCP Server Only - The number of milliseconds to retry binding to a server port. | 30000 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to receive incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. If disabled, the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions by logging them at WARN or ERROR level and ignored. | true | boolean |
| **lenientBind** (consumer) | TCP Server Only - Allow the endpoint to start before the TCP ServerSocket is bound. In some environments, it may be desirable to allow the endpoint to start before the TCP ServerSocket is bound. | false | boolean |
| **maxConcurrentConsumers** (consumer) | The maximum number of concurrent MLLP Consumer connections that will be allowed. If a new connection is received and the maximum is number are already established, the new connection will be reset immediately. | 5 | int |
| **reuseAddress** (consumer) | Enable/disable the SO\_REUSEADDR socket option. | false | Boolean |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 | InOut | ExchangePattern |
| **connectTimeout** (producer) | Timeout (in milliseconds) for establishing for a TCP connection TCP Client only. | 30000 | int |
| **idleTimeoutStrategy** (producer) | 

decide what action to take when idle timeout occurs. Possible values are : RESET: set SO\_LINGER to 0 and reset the socket CLOSE: close the socket gracefully default is RESET.

Enum values:

-   RESET
    
-   CLOSE
    





 | RESET | MllpIdleTimeoutStrategy |
| **keepAlive** (producer) | Enable/disable the SO\_KEEPALIVE socket option. | true | Boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **tcpNoDelay** (producer) | Enable/disable the TCP\_NODELAY socket option. | true | Boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **defaultCharset** (advanced) | Set the default character set to use for byte to/from String conversions. | ISO-8859-1 | String |
| **logPhi** (advanced) | Whether to log PHI. | false | Boolean |
| **logPhiMaxBytes** (advanced) | Set the maximum number of bytes of PHI that will be logged in a log entry. | 5120 | Integer |
| **maxBufferSize** (advanced) | Maximum buffer size used when receiving or sending data over the wire. | 1073741824 | int |
| **minBufferSize** (advanced) | Minimum buffer size used when receiving or sending data over the wire. | 2048 | int |
| **readTimeout** (advanced) | The SO\_TIMEOUT value (in milliseconds) used after the start of an MLLP frame has been received. | 5000 | int |
| **receiveBufferSize** (advanced) | Sets the SO\_RCVBUF option to the specified value (in bytes). | 8192 | Integer |
| **receiveTimeout** (advanced) | The SO\_TIMEOUT value (in milliseconds) used when waiting for the start of an MLLP frame. | 15000 | int |
| **sendBufferSize** (advanced) | Sets the SO\_SNDBUF option to the specified value (in bytes). | 8192 | Integer |
| **sslContextParameters** (security) | Sets the SSLContextParameters for securing TCP connections. If set, the MLLP component will use SSL/TLS for securing both producer and consumer TCP connections. This allows the configuration of trust stores, key stores, protocols, and other SSL/TLS settings. If not set, the MLLP component will use plain TCP communication. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **idleTimeout** (tcp) | The approximate idle time allowed before the Client TCP Connection will be reset. A null value or a value less than or equal to zero will disable the idle timeout. |  | Integer |

## Endpoint Options

The MLLP endpoint is configured using URI syntax:

mllp:hostname:port

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (common) | **Required** Hostname or IP for connection for the TCP connection. The default value is null, which means any local IP address. |  | String |
| **port** (common) | **Required** Port number for the TCP connection. |  | int |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoAck** (common) | Enable/Disable the automatic generation of a MLLP Acknowledgement MLLP Consumers only. | true | boolean |
| **charsetName** (common) | Sets the default charset to use. |  | String |
| **hl7Headers** (common) | Enable/Disable the automatic generation of message headers from the HL7 Message MLLP Consumers only. | true | boolean |
| **requireEndOfData** (common) | Enable/Disable strict compliance to the MLLP standard. The MLLP standard specifies START\_OF\_BLOCKhl7 payloadEND\_OF\_BLOCKEND\_OF\_DATA, however, some systems do not send the final END\_OF\_DATA byte. This setting controls whether or not the final END\_OF\_DATA byte is required or optional. | true | boolean |
| **stringPayload** (common) | Enable/Disable converting the payload to a String. If enabled, HL7 Payloads received from external systems will be validated converted to a String. If the charsetName property is set, that character set will be used for the conversion. If the charsetName property is not set, the value of MSH-18 will be used to determine th appropriate character set. If MSH-18 is not set, then the default ISO-8859-1 character set will be use. | true | boolean |
| **validatePayload** (common) | Enable/Disable the validation of HL7 Payloads If enabled, HL7 Payloads received from external systems will be validated (see Hl7Util.generateInvalidPayloadExceptionMessage for details on the validation). If and invalid payload is detected, a MllpInvalidMessageException (for consumers) or a MllpInvalidAcknowledgementException will be thrown. | false | boolean |
| **acceptTimeout** (consumer) | Timeout (in milliseconds) while waiting for a TCP connection TCP Server Only. | 60000 | int |
| **backlog** (consumer) | The maximum queue length for incoming connection indications (a request to connect) is set to the backlog parameter. If a connection indication arrives when the queue is full, the connection is refused. | 5 | Integer |
| **bindRetryInterval** (consumer) | TCP Server Only - The number of milliseconds to wait between bind attempts. | 5000 | int |
| **bindTimeout** (consumer) | TCP Server Only - The number of milliseconds to retry binding to a server port. | 30000 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to receive incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. If disabled, the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions by logging them at WARN or ERROR level and ignored. | true | boolean |
| **lenientBind** (consumer) | TCP Server Only - Allow the endpoint to start before the TCP ServerSocket is bound. In some environments, it may be desirable to allow the endpoint to start before the TCP ServerSocket is bound. | false | boolean |
| **maxConcurrentConsumers** (consumer) | The maximum number of concurrent MLLP Consumer connections that will be allowed. If a new connection is received and the maximum is number are already established, the new connection will be reset immediately. | 5 | int |
| **reuseAddress** (consumer) | Enable/disable the SO\_REUSEADDR socket option. | false | Boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 | InOut | ExchangePattern |
| **connectTimeout** (producer) | Timeout (in milliseconds) for establishing for a TCP connection TCP Client only. | 30000 | int |
| **idleTimeoutStrategy** (producer) | 

decide what action to take when idle timeout occurs. Possible values are : RESET: set SO\_LINGER to 0 and reset the socket CLOSE: close the socket gracefully default is RESET.

Enum values:

-   RESET
    
-   CLOSE
    





 | RESET | MllpIdleTimeoutStrategy |
| **keepAlive** (producer) | Enable/disable the SO\_KEEPALIVE socket option. | true | Boolean |
| **tcpNoDelay** (producer) | Enable/disable the TCP\_NODELAY socket option. | true | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxBufferSize** (advanced) | Maximum buffer size used when receiving or sending data over the wire. | 1073741824 | int |
| **minBufferSize** (advanced) | Minimum buffer size used when receiving or sending data over the wire. | 2048 | int |
| **readTimeout** (advanced) | The SO\_TIMEOUT value (in milliseconds) used after the start of an MLLP frame has been received. | 5000 | int |
| **receiveBufferSize** (advanced) | Sets the SO\_RCVBUF option to the specified value (in bytes). | 8192 | Integer |
| **receiveTimeout** (advanced) | The SO\_TIMEOUT value (in milliseconds) used when waiting for the start of an MLLP frame. | 15000 | int |
| **sendBufferSize** (advanced) | Sets the SO\_SNDBUF option to the specified value (in bytes). | 8192 | Integer |
| **sslContextParameters** (security) | Sets the SSLContextParameters for securing TCP connections. If set, the MLLP component will use SSL/TLS for securing both producer and consumer TCP connections. This allows the configuration of trust stores, key stores, protocols, and other SSL/TLS settings. If not set, the MLLP component will use plain TCP communication. |  | SSLContextParameters |
| **idleTimeout** (tcp) | The approximate idle time allowed before the Client TCP Connection will be reset. A null value or a value less than or equal to zero will disable the idle timeout. |  | Integer |

## Message Headers

The MLLP component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMllpLocalAddress** (common) Constant: [`MLLP_LOCAL_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_LOCAL_ADDRESS) | The local TCP Address of the Socket. |  | String |
| **CamelMllpRemoteAddress** (common) Constant: [`MLLP_REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_REMOTE_ADDRESS) | The remote TCP Address of the Socket. |  | String |
| **CamelMllpSslClientCertSubjectName** (consumer) Constant: [`MLLP_SSL_CLIENT_CERT_SUBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SSL_CLIENT_CERT_SUBJECT_NAME) | The SSL client certificate subject name. |  | String |
| **CamelMllpSslClientCertIssuerName** (consumer) Constant: [`MLLP_SSL_CLIENT_CERT_ISSUER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SSL_CLIENT_CERT_ISSUER_NAME) | The SSL client certificate issuer name. |  | String |
| **CamelMllpSslClientCertSerialNo** (consumer) Constant: [`MLLP_SSL_CLIENT_CERT_SERIAL_NO`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SSL_CLIENT_CERT_SERIAL_NO) | The SSL client certificate serial number. |  | String |
| **CamelMllpSslClientCertNotBefore** (consumer) Constant: [`MLLP_SSL_CLIENT_CERT_NOT_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SSL_CLIENT_CERT_NOT_BEFORE) | The SSL client certificate not before. |  | Date |
| **CamelMllpSslClientCertNotAfter** (consumer) Constant: [`MLLP_SSL_CLIENT_CERT_NOT_AFTER`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SSL_CLIENT_CERT_NOT_AFTER) | The SSL client certificate not after. |  | Date |
| **CamelMllpAcknowledgement** (common) Constant: [`MLLP_ACKNOWLEDGEMENT`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_ACKNOWLEDGEMENT) | The HL7 Acknowledgment received in bytes. |  | byte\[\] |
| **CamelMllpAcknowledgementString** (common) Constant: [`MLLP_ACKNOWLEDGEMENT_STRING`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_ACKNOWLEDGEMENT_STRING) | The HL7 Acknowledgment received, converted to a String. |  | String |
| **CamelMllpAcknowledgementType** (common) Constant: [`MLLP_ACKNOWLEDGEMENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_ACKNOWLEDGEMENT_TYPE) | The HL7 acknowledgement type (AA, AE, AR, etc). |  | String |
| **CamelMllpSendingApplication** (consumer) Constant: [`MLLP_SENDING_APPLICATION`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SENDING_APPLICATION) | MSH-3 value. |  | String |
| **CamelMllpSendingFacility** (consumer) Constant: [`MLLP_SENDING_FACILITY`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SENDING_FACILITY) | MSH-4 value. |  | String |
| **CamelMllpReceivingApplication** (consumer) Constant: [`MLLP_RECEIVING_APPLICATION`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_RECEIVING_APPLICATION) | MSH-5 value. |  | String |
| **CamelMllpReceivingFacility** (consumer) Constant: [`MLLP_RECEIVING_FACILITY`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_RECEIVING_FACILITY) | MSH-6 value. |  | String |
| **CamelMllpTimestamp** (consumer) Constant: [`MLLP_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_TIMESTAMP) | MSH-7 value. |  | String |
| **CamelMllpSecurity** (consumer) Constant: [`MLLP_SECURITY`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_SECURITY) | MSH-8 value. |  | String |
| **CamelMllpMessageType** (consumer) Constant: [`MLLP_MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_MESSAGE_TYPE) | MSH-9 value. |  | String |
| **CamelMllpEventType** (consumer) Constant: [`MLLP_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_EVENT_TYPE) | MSH-9.1 value. |  | String |
| **CamelMllpTriggerEvent** (consumer) Constant: [`MLLP_TRIGGER_EVENT`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_TRIGGER_EVENT) | MSH-9.2 value. |  | String |
| **CamelMllpMessageControlId** (consumer) Constant: [`MLLP_MESSAGE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_MESSAGE_CONTROL) | MSH-10 value. |  | String |
| **CamelMllpProcessingId** (consumer) Constant: [`MLLP_PROCESSING_ID`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_PROCESSING_ID) | MSH-11 value. |  | String |
| **CamelMllpVersionId** (consumer) Constant: [`MLLP_VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_VERSION_ID) | MSH-12 value. |  | String |
| **CamelMllpCharset** (consumer) Constant: [`MLLP_CHARSET`](https://javadoc.io/doc/org.apache.camel/camel-mllp/latest/org/apache/camel/component/mllp/MllpConstants.html#MLLP_CHARSET) | MSH-18 value. |  | String |

## Usage

### MLLP Consumer

The MLLP Consumer supports receiving MLLP-framed messages and sending HL7 Acknowledgements. The MLLP Consumer can automatically generate the HL7 Acknowledgement (HL7 Application Acknowledgements only - AA, AE and AR), or the acknowledgement can be specified using the `CamelMllpAcknowledgement` exchange property. Additionally, the type of acknowledgement that will be generated can be controlled by setting the `CamelMllpAcknowledgementType` exchange property. The MLLP Consumer can read messages without sending any HL7 Acknowledgement if the automatic acknowledgement is disabled and the exchange pattern is `InOnly`.

#### Exchange Properties

The type of acknowledgment the MLLP Consumer generates, and the state of the TCP Socket can be controlled by these properties on the Camel exchange:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Key</strong></td><td class="tableblock halign-left valign-top"><strong>Type</strong></td><td class="tableblock halign-left valign-top"><strong>Description</strong></td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpAcknowledgement</code></td><td class="tableblock halign-left valign-top"><code>byte[]</code></td><td class="tableblock halign-left valign-top">If present, this property will be sent to the client as the MLLP Acknowledgement</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpAcknowledgementString</code></td><td class="tableblock halign-left valign-top"><code>String</code></td><td class="tableblock halign-left valign-top">If present and <code>CamelMllpAcknowledgement</code> is not present, this property will we sent to the client as the MLLP Acknowledgement</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpAcknowledgementMsaText</code></td><td class="tableblock halign-left valign-top"><code>String</code></td><td class="tableblock halign-left valign-top">If neither <code>CamelMllpAcknowledgement</code> or <code>CamelMllpAcknowledgementString</code> are present and autoAck is true, this property can be used to specify the contents of MSA-3 in the generated HL7 acknowledgement</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpAcknowledgementType</code></td><td class="tableblock halign-left valign-top"><code>String</code></td><td class="tableblock halign-left valign-top">If neither <code>CamelMllpAcknowledgement</code> or <code>CamelMllpAcknowledgementString</code> are present and autoAck is true, this property can be used to specify the HL7 acknowledgement type (i.e. AA, AE, AR)</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpAutoAcknowledge</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">Overrides the autoAck query parameter</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpCloseConnectionBeforeSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be closed before sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpResetConnectionBeforeSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be reset before sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpCloseConnectionAfterSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be closed immediately after sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpResetConnectionAfterSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be reset immediately after sending any data</td></tr></tbody></table>

### MLLP Producer

The MLLP Producer supports sending MLLP-framed messages and receiving HL7 Acknowledgements. The MLLP Producer interrogates the HL7 Acknowledgements and raises exceptions if a negative acknowledgement is received. The received acknowledgement is interrogated and an exception is raised in the event of a negative acknowledgement. The MLLP Producer can ignore acknowledgements when configured with InOnly exchange pattern.

#### Exchange Properties

The state of the TCP Socket can be controlled by these properties on the Camel exchange:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Key</strong></td><td class="tableblock halign-left valign-top"><strong>Type</strong></td><td class="tableblock halign-left valign-top"><strong>Description</strong></td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpCloseConnectionBeforeSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be closed before sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpResetConnectionBeforeSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be reset before sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpCloseConnectionAfterSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be closed immediately after sending data</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelMllpResetConnectionAfterSend</code></td><td class="tableblock halign-left valign-top"><code>Boolean</code></td><td class="tableblock halign-left valign-top">If true, the Socket will be reset immediately after sending any data</td></tr></tbody></table>