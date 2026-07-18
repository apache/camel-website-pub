# CoAP

**Since Camel 2.16**

**Both producer and consumer are supported**

Camel-CoAP is an [Apache Camel](http://camel.apache.org/) component that allows you to work with CoAP, a lightweight REST-type protocol for machine-to-machine operation. [CoAP](http://coap.technology/), Constrained Application Protocol is a specialized web transfer protocol for use with constrained nodes and constrained networks, and it is based on RFC 7252.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
 <groupId>org.apache.camel</groupId>
 <artifactId>camel-coap</artifactId>
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

The CoAP component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationFile** (common) | Name of COAP configuration file to load and use. Will by default load from classpath, so use file: as prefix to load from file system. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (producer (advanced)) | To use a shared client for the producers. |  | CoapClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The CoAP endpoint is configured using URI syntax:

coap:uri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uri** (common) | The URI for the CoAP endpoint. |  | URI |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **coapMethodRestrict** (consumer) | 
Comma separated list of methods that the CoAP consumer will bind to. The default is to bind to all methods (DELETE, GET, POST, PUT).

Enum values:

-   DELETE
    
-   GET
    
-   POST
    
-   PUT
    





 |  | String |
| **observable** (consumer) | Make CoAP resource observable for source endpoint, based on RFC 7641. | false | boolean |
| **observe** (consumer) | Send an observe request from a source endpoint, based on RFC 7641. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **notify** (producer) | Notify observers that the resource of this URI has changed, based on RFC 7641. Use this flag on a destination endpoint, with a URI that matches an existing source endpoint URI. | false | boolean |
| **client** (producer (advanced)) | To use a shared client for the producers. |  | CoapClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **advancedCertificateVerifier** (security) | Set the AdvancedCertificateVerifier to use to determine trust in raw public keys. |  | NewAdvancedCertificateVerifier |
| **advancedPskStore** (security) | Set the AdvancedPskStore to use for pre-shared key. |  | AdvancedPskStore |
| **alias** (security) | 

Sets the alias used to query the KeyStore for the private key and certificate. This parameter is used when we are enabling TLS with certificates on the service side, and similarly on the client side when TLS is used with certificates and client authentication. If the parameter is not specified then the default behavior is to use the first alias in the keystore that contains a key entry. This configuration parameter does not apply to configuring TLS via a Raw Public Key or a Pre-Shared Key.

Enum values:

-   NONE
    
-   WANT
    
-   REQUIRE
    





 |  | String |
| **cipherSuites** (security) | Sets the cipherSuites String. This is a comma separated String of ciphersuites to configure. If it is not specified, then it falls back to getting the ciphersuites from the sslContextParameters object. |  | String |
| **clientAuthentication** (security) | 

Sets the configuration options for server-side client-authentication requirements. The value must be one of NONE, WANT, REQUIRE. If this value is not specified, then it falls back to checking the sslContextParameters.getServerParameters().getClientAuthentication() value.

Enum values:

-   NONE
    
-   WANTED
    
-   NEEDED
    





 |  | CertificateAuthenticationMode |
| **privateKey** (security) | Set the configured private key for use with Raw Public Key. |  | PrivateKey |
| **publicKey** (security) | Set the configured public key for use with Raw Public Key. |  | PublicKey |
| **recommendedCipherSuitesOnly** (security) | The CBC cipher suites are not recommended. If you want to use them, you first need to set the recommendedCipherSuitesOnly option to false. | true | boolean |
| **sslContextParameters** (security) | Set the SSLContextParameters object for setting up TLS. This is required for coapstcp, and for coaps when we are using certificates for TLS (as opposed to RPK or PKS). |  | SSLContextParameters |

## Message Headers

The CoAP component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCoapETag** (common) Constant: [`COAP_ETAG`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_ETAG) | The CoAP ETag for the response. |  | byte\[\] |
| **CamelCoapMaxAge** (common) Constant: [`COAP_MAX_AGE`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_MAX_AGE) | The CoAP Max-Age for the response body. |  | Long |
| **CamelCoapMethod** (common) Constant: [`COAP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_METHOD) | The request method that the CoAP producer should use when calling the target CoAP server URI. Valid options are DELETE, GET, PING, POST & PUT. |  | String |
| **CamelCoapResponseCode** (common) Constant: [`COAP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#COAP_RESPONSE_CODE) | The CoAP response code sent by the external server. See RFC 7252 for details of what each code means. |  | String |
| **Content-Type** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-coap/latest/org/apache/camel/coap/CoAPConstants.html#CONTENT_TYPE) | The content type. |  | String |

## Usage

Camel supports the DTLS, TCP and TLS protocols via the following URI schemes:

 
| Scheme | Protocol |
| --- | --- |
| coap | UDP |
| coaps | UDP + DTLS |
| coap+tcp | TCP |
| coaps+tcp | TCP + TLS |

There are a number of different configuration options to configure TLS. For both DTLS (the "coaps" uri scheme) and TCP + TLS (the "coaps+tcp" uri scheme), it is possible to use a "sslContextParameters" parameter, from which the camel-coap component will extract the required truststore / keystores etc. to set up TLS. In addition, the DTLS protocol supports two alternative configuration mechanisms. To use a pre-shared key, configure a pskStore, and to work with raw public keys, configure privateKey + publicKey objects.

### Configuring the CoAP producer request method

The following rules determine which request method the CoAP producer will use to invoke the target URI:

1.  The value of the `CamelCoapMethod` header
    
2.  `GE` if a query string is provided on the target CoAP server URI.
    
3.  `POST` if the message exchange body is not null.
    
4.  `GET` otherwise.
    

## Configuring COAP Server

The COAP server has many configuration options, and this can be configured from a properties file such as `Californium3.properties`. You can specfiy the location of this configuration file on the Camel CoAPComponent, such as:

_Java-only: configuring the CoAP component programmatically_

```java
CoAPComponent coap = context.getComponent("coap", CoAPComponent.class);
coap.setCconfigurationFile("/etc/myapp/Californium3.properties");
```

The configuration file has many options, here is a sample from CoAP 3.13 release from the [cf-simplefile-server](https://github.com/eclipse-californium/californium/blob/main/demo-apps/cf-simplefile-server/README.md) example:

```properties
# Californium CoAP Properties file for Fileserver
# Thu Feb 27 21:43:28 CET 2025
#
# Maximum payload size with coap/UDP using an external network interface.
# Default: 64
EXTERNAL_UDP_MAX_MESSAGE_SIZE=64
# Preferred blocksize for blockwise transfer with coap/UDP using an
# external network interface.
# Default: 64
EXTERNAL_UDP_PREFERRED_BLOCK_SIZE=64
# Random factor for initial CoAP acknowledge timeout.
# Default: 1.5
COAP.ACK_INIT_RANDOM=1.5
# Initial CoAP acknowledge timeout.
# Default: 2[s]
COAP.ACK_TIMEOUT=2[s]
# Scale factor for CoAP acknowledge backoff-timeout.
# Default: 2.0
COAP.ACK_TIMEOUT_SCALE=2.0
# Enable automatic failover on "entity too large" response.
# Default: true
COAP.BLOCKWISE_ENTITY_TOO_LARGE_AUTO_FAILOVER=true
# Reuse token for blockwise requests. Ease traceability but may introduce
# vulnerability.
# Default: false
COAP.BLOCKWISE_REUSE_TOKEN=false
# Interval to validate lifetime of blockwise status.
# Default: 5[s]
COAP.BLOCKWISE_STATUS_INTERVAL=5[s]
# Lifetime of blockwise status.
# Default: 5[min]
COAP.BLOCKWISE_STATUS_LIFETIME=5[min]
# Use block1 option strictly, even for error-responses.
# Default: false
COAP.BLOCKWISE_STRICT_BLOCK1_OPTION=false
# Use block2 option strictly, even if block2 is not required.
# Default: false
COAP.BLOCKWISE_STRICT_BLOCK2_OPTION=false
# CoAP port.
# Default: 5683
COAP.COAP_PORT=5683
# CoAP DTLS port.
# Default: 5684
COAP.COAP_SECURE_PORT=5684
# Congestion-Control algorithm (still experimental).
# [NULL, COCOA, COCOA_STRONG, BASIC_RTO, LINUX_RTO, PEAKHOPPER_RTO].
# Default: NULL
COAP.CONGESTION_CONTROL_ALGORITHM=NULL
# Use inet-address for congestion control, even if an other peer identity
# is used. Enable, if NAT changes are also changing the quality of the
# ip-route.
# Default: false
COAP.CONGESTION_CONTROL_USE_INET_ADDRESS=false
# Crop rotation period.
# Default: 247[s]
COAP.CROP_ROTATION_PERIOD=247[s]
# Deduplicator algorithm.
# [MARK_AND_SWEEP, PEERS_MARK_AND_SWEEP, CROP_ROTATION, NO_DEDUPLICATOR].
# Default: MARK_AND_SWEEP
COAP.DEDUPLICATOR=MARK_AND_SWEEP
# Automatic replace entries in deduplicator.
# Default: true
COAP.DEDUPLICATOR_AUTO_REPLACE=true
# CoAP maximum exchange lifetime for CON requests.
# Default: 247[s]
COAP.EXCHANGE_LIFETIME=247[s]
# Timespan a multicast server may spread the response.
# Default: 5[s]
COAP.LEISURE=5[s]
# Mark and sweep interval.
# Default: 10[s]
COAP.MARK_AND_SWEEP_INTERVAL=10[s]
# Maximum CoAP acknowledge timeout.
# Default: 1[min]
COAP.MAX_ACK_TIMEOUT=1[min]
# Maximum number of active peers.
# Default: 150000
COAP.MAX_ACTIVE_PEERS=150000
# Maximum transmission latency for messages.
# Default: 100[s]
COAP.MAX_LATENCY=100[s]
# Maximum payload size.
# Default: 1024
COAP.MAX_MESSAGE_SIZE=512
# Maximum inactive period of peer.
# Default: 10[min]
COAP.MAX_PEER_INACTIVITY_PERIOD=10[min]
# Maximum size of resource body. 0 to disable transparent blockwise
# mode.
# Default: 8192
COAP.MAX_RESOURCE_BODY_SIZE=2097152
# Maximum number of CoAP retransmissions.
# Default: 4
COAP.MAX_RETRANSMIT=4
# Maximum number of observes on server-side. 0 to disable this limitation.
# Default: 50000
COAP.MAX_SERVER_OBSERVES=50000
# Maximum server response delay.
# Default: 250[s]
COAP.MAX_SERVER_RESPONSE_DELAY=250[s]
# Maximum time to wait for ACK or RST after the first transmission of
# a CON message.
# Default: 93[s]
COAP.MAX_TRANSMIT_WAIT=93[s]
# MID tracker.
# [NULL, GROUPED, MAPBASED].
# Default: GROUPED
COAP.MID_TACKER=GROUPED
# Number of MID tracker groups.
# Default: 16
COAP.MID_TRACKER_GROUPS=16
# Base MID for multicast requests.
# Default: 65000
COAP.MULTICAST_BASE_MID=65000
# CoAP maximum lifetime for NON requests.
# Default: 145[s]
COAP.NON_LIFETIME=145[s]
# Interval time to check notifications receiver using a CON message.
# Default: 2[min]
COAP.NOTIFICATION_CHECK_INTERVAL=2[min]
# Interval counter to check notifications receiver using a CON message.
# Default: 100
COAP.NOTIFICATION_CHECK_INTERVAL_COUNT=100
# Additional time (backoff) to the max-age option
# for waiting for the next notification before reregister.
# Default: 2[s]
COAP.NOTIFICATION_REREGISTRATION_BACKOFF=2[s]
# Maximum concurrent transmissions.
# Default: 1
COAP.NSTART=1
# Maximum messages kept per peer for PEERS_MARK_AND_SWEEP.
# Default: 64
COAP.PEERS_MARK_AND_SWEEP_MESSAGES=64
# Preferred blocksize for blockwise transfer.
# Default: 512
COAP.PREFERRED_BLOCK_SIZE=512
# Probing rate to peers, which didn't response before. Currently not
# used.
# Default: 1.0
COAP.PROBING_RATE=1.0
# Protocol stage thread count.
# Default: 1
COAP.PROTOCOL_STAGE_THREAD_COUNT=14
# Response matching mode.
# [STRICT, RELAXED, PRINCIPAL, PRINCIPAL_IDENTITY].
# Default: STRICT
COAP.RESPONSE_MATCHING=STRICT
# Process empty messages strictly according RFC7252, 4.1 as format error.
# Disable to ignore additional data as tokens or options.
# Default: true
COAP.STRICT_EMPTY_MESSAGE_FORMAT=true
# Number of block per TCP-blockwise bulk transfer.
# Default: 1
COAP.TCP_NUMBER_OF_BULK_BLOCKS=4
# Limit of token size.
# Default: 8
COAP.TOKEN_SIZE_LIMIT=8
# Use message off-loading, when data is not longer required.
# Default: false
COAP.USE_MESSAGE_OFFLOADING=false
# Use initially a random value for MID.
# Default: true
COAP.USE_RANDOM_MID_START=true
# DTLS additional initial timeout for ECC related flights.
# Default: 0[ms]
DTLS.ADDITIONAL_ECC_TIMEOUT=0[ms]
# DTLS auto-handshake timeout. After that period without exchanging
# messages, a new message will initiate a handshake. Must not be used
# with SERVER_ONLY! Common value will be "30[s]" in order to compensate
# assumed NAT timeouts. <blank>, disabled.
DTLS.AUTO_HANDSHAKE_TIMEOUT=
# List of DTLS certificate key algorithms.
# On the client side used to select the default cipher-suites, on the
# server side to negotiate the client's certificate.
# List of [EC, RSA].
DTLS.CERTIFICATE_KEY_ALGORITHMS=
# DTLS supported certificate types ordered by preference.
# List of [RAW_PUBLIC_KEY, X_509].
# Default: RAW_PUBLIC_KEY, X_509
DTLS.CERTIFICATE_TYPES=RAW_PUBLIC_KEY, X_509
# List of DTLS cipher-suites.
# If not recommended cipher suites are intended to be used, switch off
# DTLS_RECOMMENDED_CIPHER_SUITES_ONLY.
# The supported cipher suites are evaluated at runtime and may differ
# from the ones when creating this properties file.
# List of [TLS_ECDHE_PSK_WITH_AES_128_GCM_SHA256, TLS_ECDHE_PSK_WITH_AES_256_GCM_SHA378,
# TLS_ECDHE_PSK_WITH_AES_128_CCM_8_SHA256, TLS_ECDHE_PSK_WITH_AES_128_CCM_SHA256,
# TLS_PSK_WITH_AES_128_GCM_SHA256, TLS_PSK_WITH_AES_256_GCM_SHA378,
# TLS_PSK_WITH_AES_128_CCM_8, TLS_PSK_WITH_AES_256_CCM_8, TLS_PSK_WITH_AES_128_CCM,
# TLS_PSK_WITH_AES_256_CCM, TLS_ECDHE_PSK_WITH_AES_128_CBC_SHA256, TLS_PSK_WITH_AES_128_CBC_SHA256,
# TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256, TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384,
# TLS_ECDHE_ECDSA_WITH_AES_128_CCM_8, TLS_ECDHE_ECDSA_WITH_AES_256_CCM_8,
# TLS_ECDHE_ECDSA_WITH_AES_128_CCM, TLS_ECDHE_ECDSA_WITH_AES_256_CCM,
# TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256, TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384,
# TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA, TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,
# TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384, TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,
# TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA].
DTLS.CIPHER_SUITES=
# DTLS connection ID length. <blank> disabled, 0 enables support without
# active use of CID.
DTLS.CONNECTION_ID_LENGTH=
# DTLS cluster-node ID used for connection ID. <blank> not used.
DTLS.CONNECTION_ID_NODE_ID=
# Number of DTLS connector threads.
# Default: 1
DTLS.CONNECTOR_THREAD_COUNT=14
# List of DTLS curves (supported groups).
# Defaults to all supported curves of the JCE at runtime.
# List of [secp256r1, secp384r1, secp521r1, X25519, X448].
DTLS.CURVES=
# DTLS default handshake mode.
# [none, auto].
# Default: auto
DTLS.DEFAULT_HANDSHAKE_MODE=
# DTLS extended master secret mode.
# [NONE, OPTIONAL, ENABLED, REQUIRED].
# Default: ENABLED
DTLS.EXTENDED_MASTER_SECRET_MODE=ENABLED
# Quiet time to reset MAC error filter.
# The MAC error filter blocks all traffic for an endpoint, if since
# the last quiet period the number of new MAC errors exceeds a threshold.
# 0 to disable the MAC error filter.
# Default: 0[ms]
DTLS.MAC_ERROR_FILTER_QUIET_TIME=0[ms]
# Threshold of current MAC errors to block all traffic for an endpoint.
# 0 to disable the MAC error filter.
# Default: 0
DTLS.MAC_ERROR_FILTER_THRESHOLD=0
# DTLS maximum connections.
# Default: 150000
DTLS.MAX_CONNECTIONS=150000
# DTLS maximum size of all deferred inbound messages.
# Default: 8192
DTLS.MAX_DEFERRED_INBOUND_RECORDS=8192
# DTLS maximum deferred outbound application messages.
# Default: 10
DTLS.MAX_DEFERRED_OUTBOUND_APPLICATION_MESSAGES=10
# DTLS maximum length of reassembled fragmented handshake message.
# Must be large enough for used certificates.
# Default: 8192
DTLS.MAX_FRAGMENTED_HANDSHAKE_MESSAGE_LENGTH=8192
# DTLS maximum fragment length (RFC 6066).
# [BYTES_512, BYTES_1024, BYTES_2048, BYTES_4096].
DTLS.MAX_FRAGMENT_SIZE=
# Maximum number of jobs for DTLS handshake results.
# Default: 5000
DTLS.MAX_PENDING_HANDSHAKE_RESULT_JOBS=5000
# Maximum number of jobs for inbound DTLS messages.
# Default: 50000
DTLS.MAX_PENDING_INBOUND_JOBS=50000
# Maximum number of jobs for outbound DTLS messages.
# Default: 50000
DTLS.MAX_PENDING_OUTBOUND_JOBS=50000
# DTLS maximum number of flight retransmissions.
# Default: 4
DTLS.MAX_RETRANSMISSIONS=4
# DTLS maximum retransmission timeout.
# Default: 1[min]
DTLS.MAX_RETRANSMISSION_TIMEOUT=1[min]
# DTLS MTU (Maximum Transmission Unit).
# Must be used, if the MTU of the local network doesn't apply, e.g.
# if ip-tunnels are used.
DTLS.MAX_TRANSMISSION_UNIT=
# DTLS MTU (Maximum Transmission Unit) limit for local auto detection.
DTLS.MAX_TRANSMISSION_UNIT_LIMIT=1500
# List of preselected DTLS cipher-suites.
# If not recommended cipher suites are intended to be used, switch off
# DTLS_RECOMMENDED_CIPHER_SUITES_ONLY.
# The supported cipher suites are evaluated at runtime and may differ
# from the ones when creating this properties file.
# List of [TLS_ECDHE_PSK_WITH_AES_128_GCM_SHA256, TLS_ECDHE_PSK_WITH_AES_256_GCM_SHA378,
# TLS_ECDHE_PSK_WITH_AES_128_CCM_8_SHA256, TLS_ECDHE_PSK_WITH_AES_128_CCM_SHA256,
# TLS_PSK_WITH_AES_128_GCM_SHA256, TLS_PSK_WITH_AES_256_GCM_SHA378,
# TLS_PSK_WITH_AES_128_CCM_8, TLS_PSK_WITH_AES_256_CCM_8, TLS_PSK_WITH_AES_128_CCM,
# TLS_PSK_WITH_AES_256_CCM, TLS_PSK_WITH_ARIA_128_GCM_SHA256, TLS_PSK_WITH_ARIA_256_GCM_SHA384,
# TLS_ECDHE_PSK_WITH_AES_128_CBC_SHA256, TLS_PSK_WITH_AES_128_CBC_SHA256,
# TLS_ECDHE_PSK_WITH_ARIA_128_CBC_SHA256, TLS_PSK_WITH_ARIA_128_CBC_SHA256,
# TLS_PSK_WITH_ARIA_256_CBC_SHA384, TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,
# TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384, TLS_ECDHE_ECDSA_WITH_AES_128_CCM_8,
# TLS_ECDHE_ECDSA_WITH_AES_256_CCM_8, TLS_ECDHE_ECDSA_WITH_AES_128_CCM,
# TLS_ECDHE_ECDSA_WITH_AES_256_CCM, TLS_ECDHE_ECDSA_WITH_ARIA_128_GCM_SHA256,
# TLS_ECDHE_ECDSA_WITH_ARIA_256_GCM_SHA384, TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256,
# TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384, TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA,
# TLS_ECDHE_ECDSA_WITH_ARIA_128_CBC_SHA256, TLS_ECDHE_ECDSA_WITH_ARIA_256_CBC_SHA384,
# TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256, TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,
# TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,
# TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA, TLS_ECDHE_RSA_WITH_ARIA_128_GCM_SHA256,
# TLS_ECDHE_RSA_WITH_ARIA_256_GCM_SHA384].
DTLS.PRESELECTED_CIPHER_SUITES=
# Use read-write-lock connection store.
# Default: true
DTLS.READ_WRITE_LOCK_CONNECTION_STORE=true
# Number of DTLS receiver threads.
# Default: 1
DTLS.RECEIVER_THREAD_COUNT=2
# DTLS receive-buffer size. Empty or 0 to use the OS default.
DTLS.RECEIVE_BUFFER_SIZE=
# DTLS recommended cipher-suites only.
# Default: true
DTLS.RECOMMENDED_CIPHER_SUITES_ONLY=true
# DTLS recommended ECC curves/groups only.
# Default: true
DTLS.RECOMMENDED_CURVES_ONLY=true
# DTLS recommended signature- and hash-algorithms only.
# Default: true
DTLS.RECOMMENDED_SIGNATURE_AND_HASH_ALGORITHMS_ONLY=true
# DTLS record size limit (RFC 8449). Between 64 and 16K.
DTLS.RECORD_SIZE_LIMIT=
# Remove stale double principals.
# Requires unique principals and a read-write-lock connection store.
# Default: false
DTLS.REMOVE_STALE_DOUBLE_PRINCIPALS=false
# Number of flight-retransmissions before switching to backoff mode
# using single handshake messages in single record datagrams.
DTLS.RETRANSMISSION_BACKOFF=
# DTLS random factor for initial retransmission timeout.
# Default: 1.0
DTLS.RETRANSMISSION_INIT_RANDOM=1.0
# DTLS initial retransmission timeout.
# Default: 2[s]
DTLS.RETRANSMISSION_TIMEOUT=2[s]
# DTLS scale factor for retransmission backoff-timeout.
# Default: 2.0
DTLS.RETRANSMISSION_TIMEOUT_SCALE=2.0
# DTLS role.
# [CLIENT_ONLY, SERVER_ONLY, BOTH].
# Default: BOTH
DTLS.ROLE=BOTH
# Use minimal version of RFC5746 to indicate secure renegotiation on
# initial handshake.
# Renegotation handshakes are always rejected by Californium.
# [NONE, WANTED, NEEDED].
# Default: WANTED
DTLS.SECURE_RENEGOTIATION_MODE=WANTED
# DTLS send-buffer size. Empty or 0 to use the OS default.
DTLS.SEND_BUFFER_SIZE=
# Enable server to use a session ID in order to support session resumption.
# Default: true
DTLS.SERVER_USE_SESSION_ID=true
# DTLS session timeout. Currently not supported.
# Default: 1[h]
DTLS.SESSION_TIMEOUT=1[d]
# List of DTLS signature- and hash-algorithms.
# Values e.g SHA256withECDSA or ED25519.
DTLS.SIGNATURE_AND_HASH_ALGORITHMS=
# DTLS threshold for stale connections. Connections will only get removed
# for new ones, if at least for that threshold no messages are exchanged
# using that connection.
# Default: 30[min]
DTLS.STALE_CONNECTION_THRESHOLD=30[min]
# DTLS support deprecated CID for server (before version 9).
# Default: false
DTLS.SUPPORT_DEPRECATED_CID=false
# Support key material export according RFC5705.
# Default: false
DTLS.SUPPORT_KEY_MATERIAL_EXPORT=false
# DTLS certificate path for validation.
# Default: true
DTLS.TRUNCATE_CERTIFICATE_PATH_FOR_VALIDATION=true
# DTLS truncate client certificate path.
# Default: true
DTLS.TRUNCATE_CLIENT_CERTIFICATE_PATH=true
# DTLS update address using CID on newer records.
# Default: true
DTLS.UPDATE_ADDRESS_USING_CID_ON_NEWER_RECORDS=true
# DTLS use the anti-replay-filter.
# Default: true
DTLS.USE_ANTI_REPLAY_FILTER=true
# Use default DTLS record filter.
# Default: true
DTLS.USE_DEFAULT_RECORD_FILTER=true
# DTLS use deprecated CID extension code point for client (before version
# 09 of RFC-CID).
DTLS.USE_DEPRECATED_CID=
# DTLS use a disabled window for the anti-replay-filter. -1 := extend
# the disabled window to start of session, 0 := normal window, <n> :=
# disabled window of size <n>.
# Default: 0
DTLS.USE_DISABLED_WINDOW_FOR_ANTI_REPLAY_FILTER=0
# Stop retransmission on receiving the first message of the next flight,
# not waiting for the last message.
# Default: true
DTLS.USE_EARLY_STOP_RETRANSMISSION=true
# DTLS use a HELLO_VERIFY_REQUEST to protect against spoofing.
# Default: true
DTLS.USE_HELLO_VERIFY_REQUEST=true
# DTLS use a HELLO_VERIFY_REQUEST for PSK cipher suites to protect against
# spoofing.
# Default: true
DTLS.USE_HELLO_VERIFY_REQUEST_FOR_PSK=true
# Use multiple handshake messages in DTLS records.
# Not all libraries may have implemented this!
DTLS.USE_MULTI_HANDSHAKE_MESSAGE_RECORDS=
# Use multiple DTLS records in UDP messages.
DTLS.USE_MULTI_RECORD_MESSAGES=
# DTLS use newer record filter.
# Drop reordered records in order to protect from delay attacks,
# if no other means, maybe on application level, are available.
# Default: false
DTLS.USE_NEWER_FILTER=false
# DTLS use server name indication.
# Default: false
DTLS.USE_SERVER_NAME_INDICATION=false
# DTLS verify peers on resumption threshold in percent.
# Default: 30
DTLS.VERIFY_PEERS_ON_RESUMPTION_THRESHOLD=30
# DTLS verifies the server certificate's subjects.
# Default: true
DTLS.VERIFY_SERVER_CERTIFICATES_SUBJECT=true
# Health status interval. 0 to disable the health status.
# Default: 0[ms]
SYS.HEALTH_STATUS_INTERVAL=0[ms]
# TCP connection idle timeout.
# Default: 10[s]
TCP.CONNECTION_IDLE_TIMEOUT=10[s]
# TCP connect timeout.
# Default: 10[s]
TCP.CONNECT_TIMEOUT=10[s]
# TLS handshake timeout.
# Default: 10[s]
TCP.HANDSHAKE_TIMEOUT=10[s]
# TLS session timeout.
# Default: 1[h]
TCP.SESSION_TIMEOUT=1[h]
# TLS verifies the server certificate's subjects.
# Default: true
TCP.VERIFY_SERVER_CERTIFICATES_SUBJECT=true
# Number of TCP worker threads. 0 to use default of TCP implementation.
# Default: 0
TCP.WORKER_THREADS=0
# Maximum number of pending outgoing messages.
# Default: 2147483647
UDP.CONNECTOR_OUT_CAPACITY=2147483647
# Maxium size of UDP datagram.
# Default: 2048
UDP.DATAGRAM_SIZE=2048
# Number of UDP receiver threads.
# Default: 1
UDP.RECEIVER_THREAD_COUNT=2
# UDP receive-buffer size. Empty or 0 to use the OS default.
UDP.RECEIVE_BUFFER_SIZE=
# Number of UDP sender threads.
# Default: 1
UDP.SENDER_THREAD_COUNT=2
# UDP send-buffer size. Empty or 0 to use the OS default.
UDP.SEND_BUFFER_SIZE=
```