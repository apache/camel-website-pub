# SMPP

**Since Camel 2.2**

**Both producer and consumer are supported**

This component provides access to an SMSC (Short Message Service Center) over the [SMPP](http://smsforum.net/SMPP_v3_4_Issue1_2.zip) protocol to send and receive SMS. The [JSMPP](http://jsmpp.org) library is used for the protocol implementation.

The version of the SMPP protocol specification is 3.4 by default and can be set using the component configuration options (field "interfaceVersion").

The Camel component currently operates as an [ESME](http://en.wikipedia.org/wiki/ESME) (External Short Messaging Entity) and not as an SMSC itself.

You are also able to execute `ReplaceSm`, `QuerySm`, `SubmitMulti`, `CancelSm`, and `DataSm`.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-smpp</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## SMS limitations

SMS is neither reliable nor secure. Users who require reliable and secure delivery may want to consider using the XMPP or SIP components instead, combined with a smartphone app supporting the chosen protocol.

-   Reliability: although the SMPP standard offers a range of feedback mechanisms to indicate errors, non-delivery and confirmation of delivery, it is not uncommon for mobile networks to hide or simulate these responses. For example, some networks automatically send a delivery confirmation for every message even if the destination number is invalid or not switched on. Some networks silently drop messages if they think they are spam. Spam detection rules in the network may be very crude, sometimes more than 100 messages per day from a single sender may be considered spam.
    
-   Security: there is basic encryption for the last hop from the radio tower down to the recipient handset. SMS messages are not encrypted or authenticated in any other part of the network. Some operators allow staff in retail outlets or call centres to browse through the SMS message histories of their customers. Message sender identity can be easily forged. Regulators and even the mobile telephone industry itself have cautioned against the use of SMS in two-factor authentication schemes and other purposes where security is important.
    

While the Camel component makes it as easy as possible to send messages to the SMS network, it cannot offer an easy solution to these problems.

## Data coding, alphabet and international character sets

Data coding and alphabet can be specified on a per-message basis. Default values can be specified for the endpoint. It is important to understand the relationship between these options and the way the component acts when more than one value is set.

Data coding is an 8 bit field in the SMPP wire format.

The alphabet corresponds to bits 0–3 of the data coding field. For some types of message, where a message class is used (by setting bit 5 of the data coding field), the lower two bits of the data coding field are not interpreted as alphabet. Only bits 2 and 3 impact the alphabet.

Furthermore, the current version of the JSMPP library only seems to support bits 2 and 3, assuming that bits 0 and 1 are used for message class. This is why the Alphabet class in JSMPP doesn’t support the value 3 (binary 0011) which indicates ISO-8859-1.

Although JSMPP provides a representation of the message class parameter, the Camel component doesn’t currently provide a way to set it other than manually setting the corresponding bits in the data coding field.

When setting the data coding field in the outgoing message, the Camel component considers the following values and uses the first one it can find:

-   the data coding specified in a header
    
-   the alphabet specified in a header
    
-   the data coding specified in the endpoint configuration (URI parameter)
    

In addition to trying to send the data coding value to the SMSC, the Camel component also tries to analyze the message body, converts it to a Java String (Unicode) and converts that to a byte array in the corresponding alphabet. When deciding which alphabet to use in the byte array, the Camel SMPP component does not consider the data coding value (header or configuration), it only considers the specified alphabet (from either the header or endpoint parameter).

If some characters in the String cannot be represented in the chosen alphabet, they may be replaced by the question mark (`?`) symbol. Users of the API may want to consider checking if their message body can be converted to ISO-8859-1 before passing it to the component and if not, setting the alphabet header to request UCS-2 encoding. If the alphabet and data coding options are not specified at all, then the component may try to detect the required encoding and set the data coding for you.

The list of alphabet codes is specified in the SMPP specification v3.4, section 5.2.19. One notable limitation of the SMPP specification is that there is no alphabet code for explicitly requesting use of the GSM 3.38 (7-bit) character set. Choosing `0` for the alphabet selects the SMSC _default_ alphabet, this usually means GSM 3.38, but it is not guaranteed. The SMPP gateway Nexmo [actually allows the default to be mapped to any other character set with a control panel option](https://help.nexmo.com/hc/en-us/articles/204015813-How-to-change-the-character-encoding-in-SMPP-). It is suggested that users check with their SMSC operator to confirm exactly which character set is being used as the default.

## Message splitting and throttling

After transforming a message body from a String to a byte array, the Camel component is also responsible for splitting the message into parts (within the 140 byte SMS size limit) before passing it to JSMPP. This is completed automatically.

If the GSM 3.38 alphabet is used, the component will pack up to 160 characters into the 140-byte message body. If an 8-bit character set is used (e.g., ISO-8859-1 for Western Europe), then 140 characters will be allowed within the 140-byte message body. If 16 bit UCS-2 encoding is used, then just 70 characters fit into each 140-byte message.

Some SMSC providers implement throttling rules. Each part of a message that has been split may be counted separately by the provider’s throttling mechanism. The Camel Throttler component can be useful for throttling messages in the SMPP route before handing them to the SMSC.

## URI format

smpp://\[username@\]hostname\[:port\]\[?options\]
smpps://\[username@\]hostname\[:port\]\[?options\]

If no **username** is provided, then Camel will provide the default value `smppclient`.  
If no **port** number is provided, then Camel will provide the default value `2775`.  
If the protocol name is "smpps", camel-smpp with try to use SSLSocket to init a connection to the server.

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

The SMPP component supports 43 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **initialReconnectDelay** (common) | Defines the initial delay in milliseconds after the consumer/producer tries to reconnect to the SMSC, after the connection was lost. | 5000 | long |
| **maxReconnect** (common) | Defines the maximum number of attempts to reconnect to the SMSC, if SMSC returns a negative bind response. | 2147483647 | int |
| **reconnectDelay** (common) | Defines the interval in milliseconds between the reconnect attempts, if the connection to the SMSC was lost and the previous was not succeed. | 5000 | long |
| **splittingPolicy** (common) | 
You can specify a policy for handling long messages: ALLOW - the default, long messages are split to 140 bytes per message TRUNCATE - long messages are split and only the first fragment will be sent to the SMSC. Some carriers drop subsequent fragments so this reduces load on the SMPP connection sending parts of a message that will never be delivered. REJECT - if a message would need to be split, it is rejected with an SMPP NegativeResponseException and the reason code signifying the message is too long.

Enum values:

-   ALLOW
    
-   REJECT
    
-   TRUNCATE
    





 | ALLOW | SmppSplittingPolicy |
| **systemType** (common) | This parameter is used to categorize the type of ESME (External Short Message Entity) that is binding to the SMSC (max. 13 characters). |  | String |
| **addressRange** (consumer) | You can specify the address range for the SmppConsumer as defined in section 5.2.7 of the SMPP 3.4 specification. The SmppConsumer will receive messages only from SMSC’s which target an address (MSISDN or IP address) within this range. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **destAddr** (producer) | Defines the destination SME address. For mobile terminated messages, this is the directory number of the recipient MS. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. | 1717 | String |
| **destAddrNpi** (producer) | 

Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **destAddrTon** (producer) | 

Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **lazySessionCreation** (producer) | Sessions can be lazily created to avoid exceptions, if the SMSC is not available when the Camel producer is started. Camel will check the in message headers 'CamelSmppSystemId' and 'CamelSmppPassword' of the first exchange. If they are present, Camel will use these data to connect to the SMSC. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **messageReceiverRouteId** (producer) | Set this on producer in order to benefit from transceiver (TRX) binding type. So once set, you don’t need to define an 'SMTPP consumer' endpoint anymore. You would set this to a 'Direct consumer' endpoint instead. DISCALIMER: This feature is only tested with 'Direct consumer' endpoint. The behavior with any other consumer type is unknown and not tested. |  | String |
| **numberingPlanIndicator** (producer) | 

Defines the numeric plan indicator (NPI) to be used in the SME. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **priorityFlag** (producer) | 

Allows the originating SME to assign a priority level to the short message. Only for SubmitSm and SubmitMulti. Four Priority Levels are supported: 0: Level 0 (lowest) priority 1: Level 1 priority 2: Level 2 priority 3: Level 3 (highest) priority.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    





 |  | byte |
| **protocolId** (producer) | The protocol id. |  | byte |
| **registeredDelivery** (producer) | 

Is used to request an SMSC delivery receipt and/or SME originated acknowledgements. The following values are defined: 0: No SMSC delivery receipt requested. 1: SMSC delivery receipt requested where final delivery outcome is success or failure. 2: SMSC delivery receipt requested where the final delivery outcome is delivery failure.

Enum values:

-   0
    
-   1
    
-   2
    





 |  | byte |
| **replaceIfPresentFlag** (producer) | 

Used to request the SMSC to replace a previously submitted message, that is still pending delivery. The SMSC will replace an existing message provided that the source address, destination address and service type match the same fields in the new message. The following replace if present flag values are defined: 0: Don’t replace 1: Replace.

Enum values:

-   0
    
-   1
    





 |  | byte |
| **serviceType** (producer) | 

The service type parameter can be used to indicate the SMS Application service associated with the message. The following generic service\_types are defined: CMT: Cellular Messaging CPT: Cellular Paging VMN: Voice Mail Notification VMA: Voice Mail Alerting WAP: Wireless Application Protocol USSD: Unstructured Supplementary Services Data.

Enum values:

-   CMT
    
-   CPT
    
-   VMN
    
-   VMA
    
-   WAP
    
-   USSD
    





 |  | String |
| **sourceAddr** (producer) | Defines the address of SME (Short Message Entity) which originated this message. | 1616 | String |
| **sourceAddrNpi** (producer) | 

Defines the numeric plan indicator (NPI) to be used in the SME originator address parameters. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **sourceAddrTon** (producer) | 

Defines the type of number (TON) to be used in the SME originator address parameters. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **typeOfNumber** (producer) | 

Defines the type of number (TON) to be used in the SME. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use the shared SmppConfiguration as configuration. |  | SmppConfiguration |
| **enquireLinkTimer** (advanced) | Defines the interval in milliseconds between the confidence checks. The confidence check is used to test the communication path between an ESME and an SMSC. | 60000 | Integer |
| **interfaceVersion** (advanced) | 

Defines the interface version to be used in the binding request with the SMSC. The following values are allowed, as defined in the SMPP protocol (and the underlying implementation using the jSMPP library, respectively): legacy (0x00), 3.3 (0x33), 3.4 (0x34), and 5.0 (0x50). The default (fallback) value is version 3.4.

Enum values:

-   legacy
    
-   3.3
    
-   3.4
    
-   5.0
    





 | 3.4 | String |
| **pduProcessorDegree** (advanced) | Sets the number of threads which can read PDU and process them in parallel. | 3 | Integer |
| **pduProcessorQueueCapacity** (advanced) | Sets the capacity of the working queue for PDU processing. | 100 | Integer |
| **sessionStateListener** (advanced) | You can refer to a org.jsmpp.session.SessionStateListener in the Registry to receive callbacks when the session state changed. |  | SessionStateListener |
| **singleDLR** (advanced) | When true, the SMSC delivery receipt would be requested only for the last segment of a multi-segment (long) message. For short messages, with only 1 segment the behaviour is unchanged. | false | boolean |
| **transactionTimer** (advanced) | Defines the maximum period of inactivity allowed after a transaction, after which an SMPP entity may assume that the session is no longer active. This timer may be active on either communicating SMPP entity (i.e. SMSC or ESME). | 10000 | Integer |
| **alphabet** (codec) | 

Defines encoding of data according the SMPP 3.4 specification, section 5.2.19. 0: SMSC Default Alphabet 4: 8 bit Alphabet 8: UCS2 Alphabet.

Enum values:

-   0
    
-   4
    
-   8
    





 |  | byte |
| **dataCoding** (codec) | Defines the data coding according the SMPP 3.4 specification, section 5.2.19. Example data encodings are: 0: SMSC Default Alphabet 3: Latin 1 (ISO-8859-1) 4: Octet unspecified (8-bit binary) 8: UCS2 (ISO/IEC-10646) 13: Extended Kanji JIS(X 0212-1990). |  | byte |
| **encoding** (codec) | Defines the encoding scheme of the short message user data. Only for SubmitSm, ReplaceSm and SubmitMulti. | ISO-8859-1 | String |
| **httpProxyHost** (proxy) | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the hostname or ip address of your HTTP proxy. |  | String |
| **httpProxyPassword** (proxy) | If your HTTP proxy requires basic authentication, set this attribute to the password required for your HTTP proxy. |  | String |
| **httpProxyPort** (proxy) | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the port of your HTTP proxy. | 3128 | Integer |
| **httpProxyUsername** (proxy) | If your HTTP proxy requires basic authentication, set this attribute to the username required for your HTTP proxy. |  | String |
| **proxyHeaders** (proxy) | These headers will be passed to the proxy server while establishing the connection. |  | Map |
| **password** (security) | The password for connecting to SMSC server. |  | String |
| **systemId** (security) | The system id (username) for connecting to SMSC server. | smppclient | String |
| **usingSSL** (security) | Whether using SSL with the smpps protocol. | false | boolean |

## Endpoint Options

The SMPP endpoint is configured using URI syntax:

smpp:host:port

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | Hostname for the SMSC server to use. | localhost | String |
| **port** (common) | Port number for the SMSC server to use. | 2775 | Integer |

### Query Parameters (43 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **initialReconnectDelay** (common) | Defines the initial delay in milliseconds after the consumer/producer tries to reconnect to the SMSC, after the connection was lost. | 5000 | long |
| **maxReconnect** (common) | Defines the maximum number of attempts to reconnect to the SMSC, if SMSC returns a negative bind response. | 2147483647 | int |
| **reconnectDelay** (common) | Defines the interval in milliseconds between the reconnect attempts, if the connection to the SMSC was lost and the previous was not succeed. | 5000 | long |
| **splittingPolicy** (common) | 
You can specify a policy for handling long messages: ALLOW - the default, long messages are split to 140 bytes per message TRUNCATE - long messages are split and only the first fragment will be sent to the SMSC. Some carriers drop subsequent fragments so this reduces load on the SMPP connection sending parts of a message that will never be delivered. REJECT - if a message would need to be split, it is rejected with an SMPP NegativeResponseException and the reason code signifying the message is too long.

Enum values:

-   ALLOW
    
-   REJECT
    
-   TRUNCATE
    





 | ALLOW | SmppSplittingPolicy |
| **systemType** (common) | This parameter is used to categorize the type of ESME (External Short Message Entity) that is binding to the SMSC (max. 13 characters). |  | String |
| **addressRange** (consumer) | You can specify the address range for the SmppConsumer as defined in section 5.2.7 of the SMPP 3.4 specification. The SmppConsumer will receive messages only from SMSC’s which target an address (MSISDN or IP address) within this range. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **destAddr** (producer) | Defines the destination SME address. For mobile terminated messages, this is the directory number of the recipient MS. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. | 1717 | String |
| **destAddrNpi** (producer) | 

Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **destAddrTon** (producer) | 

Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **lazySessionCreation** (producer) | Sessions can be lazily created to avoid exceptions, if the SMSC is not available when the Camel producer is started. Camel will check the in message headers 'CamelSmppSystemId' and 'CamelSmppPassword' of the first exchange. If they are present, Camel will use these data to connect to the SMSC. | false | boolean |
| **messageReceiverRouteId** (producer) | Set this on producer in order to benefit from transceiver (TRX) binding type. So once set, you don’t need to define an 'SMTPP consumer' endpoint anymore. You would set this to a 'Direct consumer' endpoint instead. DISCALIMER: This feature is only tested with 'Direct consumer' endpoint. The behavior with any other consumer type is unknown and not tested. |  | String |
| **numberingPlanIndicator** (producer) | 

Defines the numeric plan indicator (NPI) to be used in the SME. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **priorityFlag** (producer) | 

Allows the originating SME to assign a priority level to the short message. Only for SubmitSm and SubmitMulti. Four Priority Levels are supported: 0: Level 0 (lowest) priority 1: Level 1 priority 2: Level 2 priority 3: Level 3 (highest) priority.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    





 |  | byte |
| **protocolId** (producer) | The protocol id. |  | byte |
| **registeredDelivery** (producer) | 

Is used to request an SMSC delivery receipt and/or SME originated acknowledgements. The following values are defined: 0: No SMSC delivery receipt requested. 1: SMSC delivery receipt requested where final delivery outcome is success or failure. 2: SMSC delivery receipt requested where the final delivery outcome is delivery failure.

Enum values:

-   0
    
-   1
    
-   2
    





 |  | byte |
| **replaceIfPresentFlag** (producer) | 

Used to request the SMSC to replace a previously submitted message, that is still pending delivery. The SMSC will replace an existing message provided that the source address, destination address and service type match the same fields in the new message. The following replace if present flag values are defined: 0: Don’t replace 1: Replace.

Enum values:

-   0
    
-   1
    





 |  | byte |
| **serviceType** (producer) | 

The service type parameter can be used to indicate the SMS Application service associated with the message. The following generic service\_types are defined: CMT: Cellular Messaging CPT: Cellular Paging VMN: Voice Mail Notification VMA: Voice Mail Alerting WAP: Wireless Application Protocol USSD: Unstructured Supplementary Services Data.

Enum values:

-   CMT
    
-   CPT
    
-   VMN
    
-   VMA
    
-   WAP
    
-   USSD
    





 |  | String |
| **sourceAddr** (producer) | Defines the address of SME (Short Message Entity) which originated this message. | 1616 | String |
| **sourceAddrNpi** (producer) | 

Defines the numeric plan indicator (NPI) to be used in the SME originator address parameters. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum).

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   6
    
-   8
    
-   9
    
-   10
    
-   13
    
-   18
    





 |  | byte |
| **sourceAddrTon** (producer) | 

Defines the type of number (TON) to be used in the SME originator address parameters. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **typeOfNumber** (producer) | 

Defines the type of number (TON) to be used in the SME. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated.

Enum values:

-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    





 |  | byte |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **enquireLinkTimer** (advanced) | Defines the interval in milliseconds between the confidence checks. The confidence check is used to test the communication path between an ESME and an SMSC. | 60000 | Integer |
| **interfaceVersion** (advanced) | 

Defines the interface version to be used in the binding request with the SMSC. The following values are allowed, as defined in the SMPP protocol (and the underlying implementation using the jSMPP library, respectively): legacy (0x00), 3.3 (0x33), 3.4 (0x34), and 5.0 (0x50). The default (fallback) value is version 3.4.

Enum values:

-   legacy
    
-   3.3
    
-   3.4
    
-   5.0
    





 | 3.4 | String |
| **pduProcessorDegree** (advanced) | Sets the number of threads which can read PDU and process them in parallel. | 3 | Integer |
| **pduProcessorQueueCapacity** (advanced) | Sets the capacity of the working queue for PDU processing. | 100 | Integer |
| **sessionStateListener** (advanced) | You can refer to a org.jsmpp.session.SessionStateListener in the Registry to receive callbacks when the session state changed. |  | SessionStateListener |
| **singleDLR** (advanced) | When true, the SMSC delivery receipt would be requested only for the last segment of a multi-segment (long) message. For short messages, with only 1 segment the behaviour is unchanged. | false | boolean |
| **transactionTimer** (advanced) | Defines the maximum period of inactivity allowed after a transaction, after which an SMPP entity may assume that the session is no longer active. This timer may be active on either communicating SMPP entity (i.e. SMSC or ESME). | 10000 | Integer |
| **alphabet** (codec) | 

Defines encoding of data according the SMPP 3.4 specification, section 5.2.19. 0: SMSC Default Alphabet 4: 8 bit Alphabet 8: UCS2 Alphabet.

Enum values:

-   0
    
-   4
    
-   8
    





 |  | byte |
| **dataCoding** (codec) | Defines the data coding according the SMPP 3.4 specification, section 5.2.19. Example data encodings are: 0: SMSC Default Alphabet 3: Latin 1 (ISO-8859-1) 4: Octet unspecified (8-bit binary) 8: UCS2 (ISO/IEC-10646) 13: Extended Kanji JIS(X 0212-1990). |  | byte |
| **encoding** (codec) | Defines the encoding scheme of the short message user data. Only for SubmitSm, ReplaceSm and SubmitMulti. | ISO-8859-1 | String |
| **httpProxyHost** (proxy) | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the hostname or ip address of your HTTP proxy. |  | String |
| **httpProxyPassword** (proxy) | If your HTTP proxy requires basic authentication, set this attribute to the password required for your HTTP proxy. |  | String |
| **httpProxyPort** (proxy) | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the port of your HTTP proxy. | 3128 | Integer |
| **httpProxyUsername** (proxy) | If your HTTP proxy requires basic authentication, set this attribute to the username required for your HTTP proxy. |  | String |
| **proxyHeaders** (proxy) | These headers will be passed to the proxy server while establishing the connection. |  | Map |
| **password** (security) | The password for connecting to SMSC server. |  | String |
| **systemId** (security) | The system id (username) for connecting to SMSC server. | smppclient | String |
| **usingSSL** (security) | Whether using SSL with the smpps protocol. | false | boolean |

## Message Headers

The SMPP component supports 42 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSmppAlphabet** (producer) Constant: [`ALPHABET`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ALPHABET) | For SubmitSm, SubmitMulti and ReplaceSm The data coding according to the SMPP 3.4 specification, section 5.2.19. Use the URI option alphabet settings above. |  | Byte |
| **CamelSmppCommand** (common) Constant: [`COMMAND`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#COMMAND) | The command. |  | String |
| **CamelSmppCommandId** (consumer) Constant: [`COMMAND_ID`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#COMMAND_ID) | only for AlertNotification, DeliverSm and DataSm The command id field identifies the particular SMPP PDU. For the complete list of defined values see chapter 5.1.2.1 in the smpp specification v3.4. |  | Integer |
| **CamelSmppCommandStatus** (consumer) Constant: [`COMMAND_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#COMMAND_STATUS) | only for DataSm The Command status of the message. |  | Integer |
| **CamelSmppDataCoding** (producer) Constant: [`DATA_CODING`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DATA_CODING) | For SubmitSm, SubmitMulti and ReplaceSm The data coding according to the SMPP 3.4 specification, section 5.2.19. Use the URI option alphabet settings above. |  | Byte |
| **CamelSmppSplitter** (producer) Constant: [`DATA_SPLITTER`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DATA_SPLITTER) | The splitter. |  | SmppSplitter |
| **CamelSmppDelivered** (consumer) Constant: [`DELIVERED`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DELIVERED) | only for smsc DeliveryReceipt Number of short messages delivered. This is only relevant where the original message was submitted to a distribution list.The value is padded with leading zeros if necessary. |  | Integer |
| **CamelSmppDestAddr** (common) Constant: [`DEST_ADDR`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DEST_ADDR) | Producer: only for SubmitSm, SubmitMulti, CancelSm and DataSm Defines the destination SME address(es). For mobile terminated messages, this is the directory number of the recipient MS. It must be a List for SubmitMulti and a String otherwise. Consumer: only for DeliverSm and DataSm: Defines the destination SME address. For mobile terminated messages, this is the directory number of the recipient MS. |  | List or String |
| **CamelSmppDestAddrNpi** (common) Constant: [`DEST_ADDR_NPI`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DEST_ADDR_NPI) | Producer: only for SubmitSm, SubmitMulti, CancelSm and DataSm Defines the numeric plan indicator (NPI) to be used in the SME destination address parameters. Use the URI option sourceAddrNpi values defined above. Consumer: only for DataSm Defines the numeric plan indicator (NPI) in the destination address parameters. Use the URI option sourceAddrNpi values defined above. |  | Byte |
| **CamelSmppDestAddrTon** (common) Constant: [`DEST_ADDR_TON`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DEST_ADDR_TON) | Producer: only for SubmitSm, SubmitMulti, CancelSm and DataSm Defines the type of number (TON) to be used in the SME destination address parameters. Use the sourceAddrTon URI option values defined above. Consumer: only for DataSm Defines the type of number (TON) in the destination address parameters. Use the sourceAddrTon URI option values defined above. |  | Byte |
| **CamelSmppDoneDate** (consumer) Constant: [`DONE_DATE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#DONE_DATE) | only for smsc DeliveryReceipt The time and date at which the short message reached it’s final state. The format is as follows: YYMMDDhhmm. |  | Date |
| **CamelSmppEncoding** (producer) Constant: [`ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ENCODING) | only for SubmitSm, SubmitMulti and DataSm. Specifies the encoding (character set name) of the bytes in the message body. If the message body is a string then this is not relevant because Java Strings are always Unicode. If the body is a byte array then this header can be used to indicate that it is ISO-8859-1 or some other value. Default value is specified by the endpoint configuration parameter _encoding_. |  | String |
| **CamelSmppError** (common) Constant: [`ERROR`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ERROR) | Producer: only for SubmitMultiSm The errors which occurred by sending the short message(s) the form Map (messageID : (destAddr : address, error : errorCode)). Consumer: only for smsc DeliveryReceipt Where appropriate this may hold a Network specific error code or an SMSC error code for the attempted delivery of the message. These errors are Network or SMSC specific and are not included here. |  | String or Map |
| **CamelSmppClass** (producer) Constant: [`ESM_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ESM_CLASS) | the ASM class. |  | ESMClass |
| **CamelSmppEsmeAddr** (consumer) Constant: [`ESME_ADDR`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ESME_ADDR) | only for AlertNotification Defines the destination ESME address. For mobile terminated messages, this is the directory number of the recipient MS. |  | String |
| **CamelSmppEsmeAddrNpi** (consumer) Constant: [`ESME_ADDR_NPI`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ESME_ADDR_NPI) | only for AlertNotification Defines the numeric plan indicator (NPI) to be used in the ESME originator address parameters. Use the URI option sourceAddrNpi values defined above. |  | Byte |
| **CamelSmppEsmeAddrTon** (consumer) Constant: [`ESME_ADDR_TON`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ESME_ADDR_TON) | only for AlertNotification Defines the type of number (TON) to be used in the ESME originator address parameters. Use the sourceAddrTon URI option values defined above. |  | Byte |
| **CamelSmppFinalDate** (producer) Constant: [`FINAL_DATE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#FINAL_DATE) | The final date. |  | Date |
| **CamelSmppStatus** (consumer) Constant: [`FINAL_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#FINAL_STATUS) | 
only for smsc DeliveryReceipt: The final status of the message.

Enum values:

-   ENROUTE
    
-   DELIVRD
    
-   EXPIRED
    
-   DELETED
    
-   UNDELIV
    
-   ACCEPTD
    
-   UNKNOWN
    
-   REJECTD
    





 |  | DeliveryReceiptState |
| **CamelSmppId** (common) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#ID) | Producer: The id to identify the submitted short message(s) for later use. In case of a ReplaceSm, QuerySm, CancelSm and DataSm this header value is a String. In case of a SubmitSm or SubmitMultiSm this header value is a List. Consumer: only for smsc DeliveryReceipt and DataSm The message ID allocated to the message by the SMSC when originally submitted. |  | String or List |
| **CamelSmppMessageState** (producer) Constant: [`MESSAGE_STATE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#MESSAGE_STATE) | The message date. |  | String |
| **CamelSmppMessageType** (consumer) Constant: [`MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#MESSAGE_TYPE) | Identifies the type of an incoming message: AlertNotification: an SMSC alert notification, DataSm: an SMSC data short message, DeliveryReceipt: an SMSC delivery receipt, DeliverSm: an SMSC deliver short message. |  | String |
| **CamelSmppPriorityFlag** (producer) Constant: [`PRIORITY_FLAG`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#PRIORITY_FLAG) | only for SubmitSm and SubmitMulti Allows the originating SME to assign a priority level to the short message. Use the URI option priorityFlag settings above. |  | Byte |
| **CamelSmppProtocolId** (producer) Constant: [`PROTOCOL_ID`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#PROTOCOL_ID) | The protocol id. |  | Byte |
| **CamelSmppRegisteredDelivery** (common) Constant: [`REGISTERED_DELIVERY`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#REGISTERED_DELIVERY) | Producer: only for SubmitSm, ReplaceSm, SubmitMulti and DataSm Is used to request an SMSC delivery receipt and/or SME originated acknowledgements. Use the URI option registeredDelivery settings above. Consumer: only for DataSm Is used to request an delivery receipt and/or SME originated acknowledgements. Same values as in Producer header list above. |  | Byte |
| **CamelSmppSingleDLR** (producer) Constant: [`SINGLE_DLR`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SINGLE_DLR) | only for SubmitSm, SubmitMulti Is used to request the SMSC delivery receipt only on the last segment of multi-segment (long) messages. Use the URI option singleDLR settings above. |  | Boolean |
| **CamelSmppReplaceIfPresentFlag** (producer) Constant: [`REPLACE_IF_PRESENT_FLAG`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#REPLACE_IF_PRESENT_FLAG) | only for SubmitSm and SubmitMulti The replace if present flag parameter is used to request the SMSC to replace a previously submitted message, that is still pending delivery. The SMSC will replace an existing message provided that the source address, destination address and service type match the same fields in the new message. The following values are defined: 0, Don’t replace and 1, Replace. |  | Boolean |
| **CamelSmppScheduleDeliveryTime** (common) Constant: [`SCHEDULE_DELIVERY_TIME`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SCHEDULE_DELIVERY_TIME) | Producer: only for SubmitSm, SubmitMulti and ReplaceSm This parameter specifies the scheduled time at which the message delivery should be first attempted. It defines either the absolute date and time or relative time from the current SMSC time at which delivery of this message will be attempted by the SMSC. It can be specified in either absolute time format or relative time format. The encoding of a time format is specified in chapter 7.1.1. in the smpp specification v3.4. Consumer: only for DeliverSm: This parameter specifies the scheduled time at which the message delivery should be first attempted. It defines either the absolute date and time or relative time from the current SMSC time at which delivery of this message will be attempted by the SMSC. It can be specified in either absolute time format or relative time format. The encoding of a time format is specified in Section 7.1.1. in the smpp specification v3.4. |  | Date |
| **CamelSmppSentMessageCount** (producer) Constant: [`SENT_MESSAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SENT_MESSAGE_COUNT) | only for SubmitSm and SubmitMultiSm The total number of messages which has been sent. |  | Integer |
| **CamelSmppSequenceNumber** (consumer) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SEQUENCE_NUMBER) | only for AlertNotification, DeliverSm and DataSm A sequence number allows a response PDU to be correlated with a request PDU. The associated SMPP response PDU must preserve this field. |  | int |
| **CamelSmppServiceType** (common) Constant: [`SERVICE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SERVICE_TYPE) | Producer: The service type parameter can be used to indicate the SMS Application service associated with the message. Use the URI option serviceType settings above. Consumer: only for DeliverSm and DataSm The service type parameter indicates the SMS Application service associated with the message. |  | String |
| **CamelSmppSourceAddr** (common) Constant: [`SOURCE_ADDR`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SOURCE_ADDR) | Producer: Defines the address of SME (Short Message Entity) which originated this message. Consumer: Only for AlertNotification, DeliverSm and DataSm Defines the address of SME (Short Message Entity) which originated this message. |  | String |
| **CamelSmppSourceAddrNpi** (common) Constant: [`SOURCE_ADDR_NPI`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SOURCE_ADDR_NPI) | Producer: Defines the numeric plan indicator (NPI) to be used in the SME originator address parameters. Use the URI option sourceAddrNpi values defined above. Consumer: only for AlertNotification and DataSm Defines the numeric plan indicator (NPI) to be used in the SME originator address parameters. Use the URI option sourceAddrNpi values defined above. |  | Byte |
| **CamelSmppSourceAddrTon** (common) Constant: [`SOURCE_ADDR_TON`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SOURCE_ADDR_TON) | Producer: Defines the type of number (TON) to be used in the SME originator address parameters. Use the sourceAddrTon URI option values defined above. Consumer: only for AlertNotification and DataSm Defines the type of number (TON) to be used in the SME originator address parameters. Use the sourceAddrTon URI option values defined above. |  | Byte |
| **CamelSmppSubmitted** (consumer) Constant: [`SUBMITTED`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SUBMITTED) | only for smsc DeliveryReceipt Number of short messages originally submitted. This is only relevant when the original message was submitted to a distribution list.The value is padded with leading zeros if necessary. |  | Integer |
| **CamelSmppSubmitDate** (consumer) Constant: [`SUBMIT_DATE`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SUBMIT_DATE) | only for smsc DeliveryReceipt The time and date at which the short message was submitted. In the case of a message which has been replaced, this is the date that the original message was replaced. The format is as follows: YYMMDDhhmm. |  | Date |
| **CamelSmppSystemId** (producer) Constant: [`SYSTEM_ID`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SYSTEM_ID) | The system id. |  | String |
| **CamelSmppPassword** (producer) Constant: [`PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#PASSWORD) | The password. |  | String |
| **CamelSmppValidityPeriod** (common) Constant: [`VALIDITY_PERIOD`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#VALIDITY_PERIOD) | Producer: only for SubmitSm, SubmitMulti and ReplaceSm The validity period parameter indicates the SMSC expiration time, after which the message should be discarded if not delivered to the destination. If it’s provided as Date, it’s interpreted as absolute time or relative time format if you provide it as String as specified in chapter 7.1.1 in the smpp specification v3.4. Consumer: only for DeliverSm The validity period parameter indicates the SMSC expiration time, after which the message should be discarded if not delivered to the destination. It can be defined in absolute time format or relative time format. The encoding of absolute and relative time format is specified in Section 7.1.1 in the smpp specification v3.4. |  | String or Date |
| **CamelSmppOptionalParameters** (consumer) Constant: [`OPTIONAL_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#OPTIONAL_PARAMETERS) | The optional parameters by name. Deprecation note: Use CamelSmppOptionalParameter instead. |  | Map |
| **CamelSmppOptionalParameter** (common) Constant: [`OPTIONAL_PARAMETER`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#OPTIONAL_PARAMETER) | Producer: only for SubmitSm, SubmitMulti and DataSm The optional parameter which are send to the SMSC. The value is converted in the following way: String - org.jsmpp.bean.OptionalParameter.COctetString, byte - org.jsmpp.bean.OptionalParameter.OctetString, Byte - org.jsmpp.bean.OptionalParameter.Byte, Integer - org.jsmpp.bean.OptionalParameter.Int, Short - org.jsmpp.bean.OptionalParameter.Short, null - org.jsmpp.bean.OptionalParameter.Null Consumer: only for DeliverSm The optional parameters send back by the SMSC. The key is the Short code for the optional parameter. The value is converted in the following way: org.jsmpp.bean.OptionalParameter.COctetString - String, org.jsmpp.bean.OptionalParameter.OctetString - byte, org.jsmpp.bean.OptionalParameter.Byte - Byte, org.jsmpp.bean.OptionalParameter.Int - Integer, org.jsmpp.bean.OptionalParameter.Short - Short, org.jsmpp.bean.OptionalParameter.Null - null. |  | Map |
| **CamelSmppSplittingPolicy** (producer) Constant: [`SPLITTING_POLICY`](https://javadoc.io/doc/org.apache.camel/camel-smpp/latest/org/apache/camel/component/smpp/SmppConstants.html#SPLITTING_POLICY) | only for SubmitSm, SubmitMulti and DataSm. Specifies the policy for message splitting for this exchange. Possible values are described in the endpoint configuration parameter _splittingPolicy_. |  | String |
> **Tip**
> **JSMPP library**
>
> See the documentation of the [JSMPP Library](http://jsmpp.org) for more details about the underlying library.

## Exception handling

This component supports the general Camel exception handling capabilities

When an error occurs sending a message with SubmitSm (the default action), the org.apache.camel.component.smpp.SmppException is thrown with a nested exception, org.jsmpp.extra.NegativeResponseException. Call NegativeResponseException.getCommandStatus() to obtain the exact SMPP negative response code, the values are explained in the SMPP specification 3.4, section 5.1.3.  
When the SMPP consumer receives a `DeliverSm` or `DataSm` short message and the processing of these messages fails, you can also throw a `ProcessRequestException` instead of handle the failure. In this case, this exception is forwarded to the underlying [JSMPP library](http://jsmpp.org) which will return the included error code to the SMSC. This feature is useful to e.g., instruct the SMSC to resend the short message at a later time. This could be done with the following lines of code:

```java
from("smpp://smppclient@localhost:2775?password=password&enquireLinkTimer=3000&transactionTimer=5000&systemType=consumer")
  .doTry()
    .to("bean:dao?method=updateSmsState")
  .doCatch(Exception.class)
    .throwException(new ProcessRequestException("update of sms state failed", 100))
  .end();
```

Please refer to the [SMPP specification](http://smsforum.net/SMPP_v3_4_Issue1_2.zip) for the complete list of error codes and their meanings.

## Examples

A route which sends an SMS using the Java DSL:

```java
from("direct:start")
  .to("smpp://smppclient@localhost:2775?
      password=password&enquireLinkTimer=3000&transactionTimer=5000&systemType=producer");
```

A route which sends an SMS using the Spring XML DSL:

```xml
<route>
  <from uri="direct:start"/>
  <to uri="smpp://smppclient@localhost:2775?
           password=password&amp;enquireLinkTimer=3000&amp;transactionTimer=5000&amp;systemType=producer"/>
</route>
```

A route which receives an SMS using the Java DSL:

```java
from("smpp://smppclient@localhost:2775?password=password&enquireLinkTimer=3000&transactionTimer=5000&systemType=consumer")
  .to("bean:foo");
```

A route which receives an SMS using the Spring XML DSL:

```xml
  <route>
     <from uri="smpp://smppclient@localhost:2775?
                password=password&amp;enquireLinkTimer=3000&amp;transactionTimer=5000&amp;systemType=consumer"/>
     <to uri="bean:foo"/>
  </route>
```

An example of using transceiver (TRX) binding type:

```java
from("direct:start")
        .to("smpp://j@localhost:8056?password=jpwd&systemType=producer" +
            "&messageReceiverRouteId=sampleMessageReceiverRouteId");

from("direct:messageReceiver").id("sampleMessageReceiverRouteId")
        .to("bean:foo");
```

Please note that with TRX binding type, you wouldn’t define a corresponding redundant SMPP consumer. Camel will use the specified route by `messageReceiverRouteId` as the corresponding consumer. Internally, it uses one and same SmppSession as producer for the provided consumer.

When the SMPP Server doesn’t support TRX, then you have to define separate producer (TX by default) and consumer (RX by default).

> **Tip**
> **SMSC simulator**
>
> If you need an SMSC simulator for your test, you can use the simulator provided by [JSMPP](https://github.com/opentelecoms-org/jsmpp/wiki/GettingStarted#running-smpp-server).

## Debug logging

This component has log level **DEBUG**, which can be helpful in debugging problems. If you use log4j, you can add the following line to your configuration:

```properties
log4j.logger.org.apache.camel.component.smpp=DEBUG
```

## Spring Boot Auto-Configuration

When using smpp with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-smpp-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 44 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.smpp.address-range** | You can specify the address range for the SmppConsumer as defined in section 5.2.7 of the SMPP 3.4 specification. The SmppConsumer will receive messages only from SMSC’s which target an address (MSISDN or IP address) within this range. |  | String |
| **camel.component.smpp.alphabet** | Defines encoding of data according the SMPP 3.4 specification, section 5.2.19. 0: SMSC Default Alphabet 4: 8 bit Alphabet 8: UCS2 Alphabet. |  | Byte |
| **camel.component.smpp.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.smpp.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.smpp.configuration** | To use the shared SmppConfiguration as configuration. The option is a org.apache.camel.component.smpp.SmppConfiguration type. |  | SmppConfiguration |
| **camel.component.smpp.data-coding** | Defines the data coding according the SMPP 3.4 specification, section 5.2.19. Example data encodings are: 0: SMSC Default Alphabet 3: Latin 1 (ISO-8859-1) 4: Octet unspecified (8-bit binary) 8: UCS2 (ISO/IEC-10646) 13: Extended Kanji JIS(X 0212-1990). |  | Byte |
| **camel.component.smpp.dest-addr** | Defines the destination SME address. For mobile terminated messages, this is the directory number of the recipient MS. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. | 1717 | String |
| **camel.component.smpp.dest-addr-npi** | Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum). |  | Byte |
| **camel.component.smpp.dest-addr-ton** | Defines the type of number (TON) to be used in the SME destination address parameters. Only for SubmitSm, SubmitMulti, CancelSm and DataSm. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated. |  | Byte |
| **camel.component.smpp.enabled** | Whether to enable auto configuration of the smpp component. This is enabled by default. |  | Boolean |
| **camel.component.smpp.encoding** | Defines the encoding scheme of the short message user data. Only for SubmitSm, ReplaceSm and SubmitMulti. | ISO-8859-1 | String |
| **camel.component.smpp.enquire-link-timer** | Defines the interval in milliseconds between the confidence checks. The confidence check is used to test the communication path between an ESME and an SMSC. | 60000 | Integer |
| **camel.component.smpp.http-proxy-host** | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the hostname or ip address of your HTTP proxy. |  | String |
| **camel.component.smpp.http-proxy-password** | If your HTTP proxy requires basic authentication, set this attribute to the password required for your HTTP proxy. |  | String |
| **camel.component.smpp.http-proxy-port** | If you need to tunnel SMPP through a HTTP proxy, set this attribute to the port of your HTTP proxy. | 3128 | Integer |
| **camel.component.smpp.http-proxy-username** | If your HTTP proxy requires basic authentication, set this attribute to the username required for your HTTP proxy. |  | String |
| **camel.component.smpp.initial-reconnect-delay** | Defines the initial delay in milliseconds after the consumer/producer tries to reconnect to the SMSC, after the connection was lost. | 5000 | Long |
| **camel.component.smpp.interface-version** | Defines the interface version to be used in the binding request with the SMSC. The following values are allowed, as defined in the SMPP protocol (and the underlying implementation using the jSMPP library, respectively): legacy (0x00), 3.3 (0x33), 3.4 (0x34), and 5.0 (0x50). The default (fallback) value is version 3.4. | 3.4 | String |
| **camel.component.smpp.lazy-session-creation** | Sessions can be lazily created to avoid exceptions, if the SMSC is not available when the Camel producer is started. Camel will check the in message headers 'CamelSmppSystemId' and 'CamelSmppPassword' of the first exchange. If they are present, Camel will use these data to connect to the SMSC. | false | Boolean |
| **camel.component.smpp.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.smpp.max-reconnect** | Defines the maximum number of attempts to reconnect to the SMSC, if SMSC returns a negative bind response. | 2147483647 | Integer |
| **camel.component.smpp.message-receiver-route-id** | Set this on producer in order to benefit from transceiver (TRX) binding type. So once set, you don’t need to define an 'SMTPP consumer' endpoint anymore. You would set this to a 'Direct consumer' endpoint instead. DISCALIMER: This feature is only tested with 'Direct consumer' endpoint. The behavior with any other consumer type is unknown and not tested. |  | String |
| **camel.component.smpp.numbering-plan-indicator** | Defines the numeric plan indicator (NPI) to be used in the SME. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum). |  | Byte |
| **camel.component.smpp.password** | The password for connecting to SMSC server. |  | String |
| **camel.component.smpp.pdu-processor-degree** | Sets the number of threads which can read PDU and process them in parallel. | 3 | Integer |
| **camel.component.smpp.pdu-processor-queue-capacity** | Sets the capacity of the working queue for PDU processing. | 100 | Integer |
| **camel.component.smpp.priority-flag** | Allows the originating SME to assign a priority level to the short message. Only for SubmitSm and SubmitMulti. Four Priority Levels are supported: 0: Level 0 (lowest) priority 1: Level 1 priority 2: Level 2 priority 3: Level 3 (highest) priority. |  | Byte |
| **camel.component.smpp.protocol-id** | The protocol id. |  | Byte |
| **camel.component.smpp.proxy-headers** | These headers will be passed to the proxy server while establishing the connection. |  | Map |
| **camel.component.smpp.reconnect-delay** | Defines the interval in milliseconds between the reconnect attempts, if the connection to the SMSC was lost and the previous was not succeed. | 5000 | Long |
| **camel.component.smpp.registered-delivery** | Is used to request an SMSC delivery receipt and/or SME originated acknowledgements. The following values are defined: 0: No SMSC delivery receipt requested. 1: SMSC delivery receipt requested where final delivery outcome is success or failure. 2: SMSC delivery receipt requested where the final delivery outcome is delivery failure. |  | Byte |
| **camel.component.smpp.replace-if-present-flag** | Used to request the SMSC to replace a previously submitted message, that is still pending delivery. The SMSC will replace an existing message provided that the source address, destination address and service type match the same fields in the new message. The following replace if present flag values are defined: 0: Don’t replace 1: Replace. |  | Byte |
| **camel.component.smpp.service-type** | The service type parameter can be used to indicate the SMS Application service associated with the message. The following generic service\_types are defined: CMT: Cellular Messaging CPT: Cellular Paging VMN: Voice Mail Notification VMA: Voice Mail Alerting WAP: Wireless Application Protocol USSD: Unstructured Supplementary Services Data. |  | String |
| **camel.component.smpp.session-state-listener** | You can refer to a org.jsmpp.session.SessionStateListener in the Registry to receive callbacks when the session state changed. The option is a org.jsmpp.session.SessionStateListener type. |  | SessionStateListener |
| **camel.component.smpp.single-d-l-r** | When true, the SMSC delivery receipt would be requested only for the last segment of a multi-segment (long) message. For short messages, with only 1 segment the behaviour is unchanged. | false | Boolean |
| **camel.component.smpp.source-addr** | Defines the address of SME (Short Message Entity) which originated this message. | 1616 | String |
| **camel.component.smpp.source-addr-npi** | Defines the numeric plan indicator (NPI) to be used in the SME originator address parameters. The following NPI values are defined: 0: Unknown 1: ISDN (E163/E164) 2: Data (X.121) 3: Telex (F.69) 6: Land Mobile (E.212) 8: National 9: Private 10: ERMES 13: Internet (IP) 18: WAP Client Id (to be defined by WAP Forum). |  | Byte |
| **camel.component.smpp.source-addr-ton** | Defines the type of number (TON) to be used in the SME originator address parameters. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated. |  | Byte |
| **camel.component.smpp.splitting-policy** | You can specify a policy for handling long messages: ALLOW - the default, long messages are split to 140 bytes per message TRUNCATE - long messages are split and only the first fragment will be sent to the SMSC. Some carriers drop subsequent fragments so this reduces load on the SMPP connection sending parts of a message that will never be delivered. REJECT - if a message would need to be split, it is rejected with an SMPP NegativeResponseException and the reason code signifying the message is too long. | allow | SmppSplittingPolicy |
| **camel.component.smpp.system-id** | The system id (username) for connecting to SMSC server. | smppclient | String |
| **camel.component.smpp.system-type** | This parameter is used to categorize the type of ESME (External Short Message Entity) that is binding to the SMSC (max. 13 characters). |  | String |
| **camel.component.smpp.transaction-timer** | Defines the maximum period of inactivity allowed after a transaction, after which an SMPP entity may assume that the session is no longer active. This timer may be active on either communicating SMPP entity (i.e. SMSC or ESME). | 10000 | Integer |
| **camel.component.smpp.type-of-number** | Defines the type of number (TON) to be used in the SME. The following TON values are defined: 0: Unknown 1: International 2: National 3: Network Specific 4: Subscriber Number 5: Alphanumeric 6: Abbreviated. |  | Byte |
| **camel.component.smpp.using-s-s-l** | Whether using SSL with the smpps protocol. | false | Boolean |