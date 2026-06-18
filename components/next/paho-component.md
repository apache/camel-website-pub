# Paho

> **Warning**
> **Deprecated:** This paho is deprecated and may be removed in a future release.

**Since Camel 2.16**

**Both producer and consumer are supported**

Paho component provides a connector for the [MQTT](https://en.wikipedia.org/wiki/MQTT) messaging protocol using the [Eclipse Paho](https://eclipse.org/paho/) library. Paho is one of the most popular MQTT libraries, so if you would like to integrate it with your Java project - Camel Paho connector is a way to go.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-paho</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

paho:topic\[?options\]

Where `topic` is the name of the topic.

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

The Paho component supports 32 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **automaticReconnect** (common) | Sets whether the client will automatically attempt to reconnect to the server if the connection is lost. If set to false, the client will not attempt to automatically reconnect to the server in the event that the connection is lost. If set to true, in the event that the connection is lost, the client will attempt to reconnect to the server. It will initially wait 1 second before it attempts to reconnect, for every failed reconnect attempt, the delay will double until it is at 2 minutes at which point the delay will stay at 2 minutes. | true | boolean |
| **brokerUrl** (common) | The URL of the MQTT broker. | tcp://localhost:1883 | String |
| **cleanSession** (common) | Sets whether the client and server should remember state across restarts and reconnects. If set to false both the client and server will maintain state across restarts of the client, the server and the connection. As state is maintained: Message delivery will be reliable meeting the specified QOS even if the client, server or connection are restarted. The server will treat a subscription as durable. If set to true the client and server will not maintain state across restarts of the client, the server or the connection. This means Message delivery to the specified QOS cannot be maintained if the client, server or connection are restarted The server will treat a subscription as non-durable. | true | boolean |
| **clientId** (common) | MQTT client identifier. The identifier must be unique. |  | String |
| **configuration** (common) | To use the shared Paho configuration. |  | PahoConfiguration |
| **connectionTimeout** (common) | Sets the connection timeout value. This value, measured in seconds, defines the maximum time interval the client will wait for the network connection to the MQTT server to be established. The default timeout is 30 seconds. A value of 0 disables timeout processing meaning the client will wait until the network connection is made successfully or fails. | 30 | int |
| **filePersistenceDirectory** (common) | Base directory used by file persistence. Will by default use user directory. |  | String |
| **keepAliveInterval** (common) | Sets the keep alive interval. This value, measured in seconds, defines the maximum time interval between messages sent or received. It enables the client to detect if the server is no longer available, without having to wait for the TCP/IP timeout. The client will ensure that at least one message travels across the network within each keep alive period. In the absence of a data-related message during the time period, the client sends a very small ping message, which the server will acknowledge. A value of 0 disables keepalive processing in the client. The default value is 60 seconds. | 60 | int |
| **maxInflight** (common) | Sets the max inflight. please increase this value in a high traffic environment. The default value is 10. | 10 | int |
| **maxReconnectDelay** (common) | Get the maximum time (in millis) to wait between reconnects. | 128000 | int |
| **mqttVersion** (common) | Sets the MQTT version. The default action is to connect with version 3.1.1, and to fall back to 3.1 if that fails. Version 3.1.1 or 3.1 can be selected specifically, with no fall back, by using the MQTT\_VERSION\_3\_1\_1 or MQTT\_VERSION\_3\_1 options respectively. |  | int |
| **persistence** (common) | 
Client persistence to be used - memory or file.

Enum values:

-   FILE
    
-   MEMORY
    





 | MEMORY | PahoPersistence |
| **qos** (common) | Client quality of service level (0-2). | 2 | int |
| **retained** (common) | Retain option. | false | boolean |
| **serverURIs** (common) | Set a list of one or more serverURIs the client may connect to. Multiple servers can be separated by comma. Each serverURI specifies the address of a server that the client may connect to. Two types of connection are supported tcp:// for a TCP connection and ssl:// for a TCP connection secured by SSL/TLS. For example: tcp://localhost:1883 ssl://localhost:8883 If the port is not specified, it will default to 1883 for tcp:// URIs, and 8883 for ssl:// URIs. If serverURIs is set then it overrides the serverURI parameter passed in on the constructor of the MQTT client. When an attempt to connect is initiated the client will start with the first serverURI in the list and work through the list until a connection is established with a server. If a connection cannot be made to any of the servers then the connect attempt fails. Specifying a list of servers that a client may connect to has several uses: High Availability and reliable message delivery Some MQTT servers support a high availability feature where two or more equal MQTT servers share state. An MQTT client can connect to any of the equal servers and be assured that messages are reliably delivered and durable subscriptions are maintained no matter which server the client connects to. The cleansession flag must be set to false if durable subscriptions and/or reliable message delivery is required. Hunt List A set of servers may be specified that are not equal (as in the high availability option). As no state is shared across the servers reliable message delivery and durable subscriptions are not valid. The cleansession flag must be set to true if the hunt list mode is used. |  | String |
| **willPayload** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the message for the LWT. |  | String |
| **willQos** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the quality of service to publish the message at (0, 1 or 2). |  | int |
| **willRetained** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets whether or not the message should be retained. | false | boolean |
| **willTopic** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the topic that the willPayload will be published to. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **manualAcksEnabled** (consumer) | Sets whether to use manual acknowledgements for the client. By default, this is false and message will be automatically acknowledged. If set to true, the acknowledgement is added in the exchange’s completion callback. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | To use a shared Paho client. |  | MqttClient |
| **customWebSocketHeaders** (advanced) | Sets the Custom WebSocket Headers for the WebSocket Connection. |  | Properties |
| **executorServiceTimeout** (advanced) | Set the time in seconds that the executor service should wait when terminating before forcefully terminating. It is not recommended to change this value unless you are absolutely sure that you need to. | 1 | int |
| **httpsHostnameVerificationEnabled** (security) | Whether SSL HostnameVerifier is enabled or not. The default value is true. | true | boolean |
| **password** (security) | Password to be used for authentication against the MQTT broker. |  | String |
| **socketFactory** (security) | Sets the SocketFactory to use. This allows an application to apply its own policies around the creation of network sockets. If using an SSL connection, an SSLSocketFactory can be used to supply application-specific security settings. |  | SocketFactory |
| **sslClientProps** (security) | Sets the SSL properties for the connection. Note that these properties are only valid if an implementation of the Java Secure Socket Extensions (JSSE) is available. These properties are not used if a custom SocketFactory has been set. The following properties can be used: com.ibm.ssl.protocol One of: SSL, SSLv3, TLS, TLSv1, SSL\_TLS. com.ibm.ssl.contextProvider Underlying JSSE provider. For example IBMJSSE2 or SunJSSE com.ibm.ssl.keyStore The name of the file that contains the KeyStore object that you want the KeyManager to use. For example /mydir/etc/key.p12 com.ibm.ssl.keyStorePassword The password for the KeyStore object that you want the KeyManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.keyStoreType Type of key store, for example PKCS12, JKS, or JCEKS. com.ibm.ssl.keyStoreProvider Key store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.trustStore The name of the file that contains the KeyStore object that you want the TrustManager to use. com.ibm.ssl.trustStorePassword The password for the TrustStore object that you want the TrustManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.trustStoreType The type of KeyStore object that you want the default TrustManager to use. Same possible values as keyStoreType. com.ibm.ssl.trustStoreProvider Trust store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.enabledCipherSuites A list of which ciphers are enabled. Values are dependent on the provider, for example: SSL\_RSA\_WITH\_AES\_128\_CBC\_SHA;SSL\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA. com.ibm.ssl.keyManager Sets the algorithm that will be used to instantiate a KeyManagerFactory object instead of using the default algorithm available in the platform. Example values: IbmX509 or IBMJ9X509. com.ibm.ssl.trustManager Sets the algorithm that will be used to instantiate a TrustManagerFactory object instead of using the default algorithm available in the platform. Example values: PKIX or IBMJ9X509. |  | Properties |
| **sslHostnameVerifier** (security) | Sets the HostnameVerifier for the SSL connection. Note that it will be used after handshake on a connection and you should do actions by yourself when hostname is verified error. There is no default HostnameVerifier. |  | HostnameVerifier |
| **userName** (security) | Username to be used for authentication against the MQTT broker. |  | String |

## Endpoint Options

The Paho endpoint is configured using URI syntax:

paho:topic

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** Name of the topic. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **automaticReconnect** (common) | Sets whether the client will automatically attempt to reconnect to the server if the connection is lost. If set to false, the client will not attempt to automatically reconnect to the server in the event that the connection is lost. If set to true, in the event that the connection is lost, the client will attempt to reconnect to the server. It will initially wait 1 second before it attempts to reconnect, for every failed reconnect attempt, the delay will double until it is at 2 minutes at which point the delay will stay at 2 minutes. | true | boolean |
| **brokerUrl** (common) | The URL of the MQTT broker. | tcp://localhost:1883 | String |
| **cleanSession** (common) | Sets whether the client and server should remember state across restarts and reconnects. If set to false both the client and server will maintain state across restarts of the client, the server and the connection. As state is maintained: Message delivery will be reliable meeting the specified QOS even if the client, server or connection are restarted. The server will treat a subscription as durable. If set to true the client and server will not maintain state across restarts of the client, the server or the connection. This means Message delivery to the specified QOS cannot be maintained if the client, server or connection are restarted The server will treat a subscription as non-durable. | true | boolean |
| **clientId** (common) | MQTT client identifier. The identifier must be unique. |  | String |
| **connectionTimeout** (common) | Sets the connection timeout value. This value, measured in seconds, defines the maximum time interval the client will wait for the network connection to the MQTT server to be established. The default timeout is 30 seconds. A value of 0 disables timeout processing meaning the client will wait until the network connection is made successfully or fails. | 30 | int |
| **filePersistenceDirectory** (common) | Base directory used by file persistence. Will by default use user directory. |  | String |
| **keepAliveInterval** (common) | Sets the keep alive interval. This value, measured in seconds, defines the maximum time interval between messages sent or received. It enables the client to detect if the server is no longer available, without having to wait for the TCP/IP timeout. The client will ensure that at least one message travels across the network within each keep alive period. In the absence of a data-related message during the time period, the client sends a very small ping message, which the server will acknowledge. A value of 0 disables keepalive processing in the client. The default value is 60 seconds. | 60 | int |
| **maxInflight** (common) | Sets the max inflight. please increase this value in a high traffic environment. The default value is 10. | 10 | int |
| **maxReconnectDelay** (common) | Get the maximum time (in millis) to wait between reconnects. | 128000 | int |
| **mqttVersion** (common) | Sets the MQTT version. The default action is to connect with version 3.1.1, and to fall back to 3.1 if that fails. Version 3.1.1 or 3.1 can be selected specifically, with no fall back, by using the MQTT\_VERSION\_3\_1\_1 or MQTT\_VERSION\_3\_1 options respectively. |  | int |
| **persistence** (common) | 
Client persistence to be used - memory or file.

Enum values:

-   FILE
    
-   MEMORY
    





 | MEMORY | PahoPersistence |
| **qos** (common) | Client quality of service level (0-2). | 2 | int |
| **retained** (common) | Retain option. | false | boolean |
| **serverURIs** (common) | Set a list of one or more serverURIs the client may connect to. Multiple servers can be separated by comma. Each serverURI specifies the address of a server that the client may connect to. Two types of connection are supported tcp:// for a TCP connection and ssl:// for a TCP connection secured by SSL/TLS. For example: tcp://localhost:1883 ssl://localhost:8883 If the port is not specified, it will default to 1883 for tcp:// URIs, and 8883 for ssl:// URIs. If serverURIs is set then it overrides the serverURI parameter passed in on the constructor of the MQTT client. When an attempt to connect is initiated the client will start with the first serverURI in the list and work through the list until a connection is established with a server. If a connection cannot be made to any of the servers then the connect attempt fails. Specifying a list of servers that a client may connect to has several uses: High Availability and reliable message delivery Some MQTT servers support a high availability feature where two or more equal MQTT servers share state. An MQTT client can connect to any of the equal servers and be assured that messages are reliably delivered and durable subscriptions are maintained no matter which server the client connects to. The cleansession flag must be set to false if durable subscriptions and/or reliable message delivery is required. Hunt List A set of servers may be specified that are not equal (as in the high availability option). As no state is shared across the servers reliable message delivery and durable subscriptions are not valid. The cleansession flag must be set to true if the hunt list mode is used. |  | String |
| **willPayload** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the message for the LWT. |  | String |
| **willQos** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the quality of service to publish the message at (0, 1 or 2). |  | int |
| **willRetained** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets whether or not the message should be retained. | false | boolean |
| **willTopic** (common) | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the topic that the willPayload will be published to. |  | String |
| **manualAcksEnabled** (consumer) | Sets whether to use manual acknowledgements for the client. By default, this is false and message will be automatically acknowledged. If set to true, the acknowledgement is added in the exchange’s completion callback. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | To use an existing mqtt client. |  | MqttClient |
| **customWebSocketHeaders** (advanced) | Sets the Custom WebSocket Headers for the WebSocket Connection. |  | Properties |
| **executorServiceTimeout** (advanced) | Set the time in seconds that the executor service should wait when terminating before forcefully terminating. It is not recommended to change this value unless you are absolutely sure that you need to. | 1 | int |
| **httpsHostnameVerificationEnabled** (security) | Whether SSL HostnameVerifier is enabled or not. The default value is true. | true | boolean |
| **password** (security) | Password to be used for authentication against the MQTT broker. |  | String |
| **socketFactory** (security) | Sets the SocketFactory to use. This allows an application to apply its own policies around the creation of network sockets. If using an SSL connection, an SSLSocketFactory can be used to supply application-specific security settings. |  | SocketFactory |
| **sslClientProps** (security) | Sets the SSL properties for the connection. Note that these properties are only valid if an implementation of the Java Secure Socket Extensions (JSSE) is available. These properties are not used if a custom SocketFactory has been set. The following properties can be used: com.ibm.ssl.protocol One of: SSL, SSLv3, TLS, TLSv1, SSL\_TLS. com.ibm.ssl.contextProvider Underlying JSSE provider. For example IBMJSSE2 or SunJSSE com.ibm.ssl.keyStore The name of the file that contains the KeyStore object that you want the KeyManager to use. For example /mydir/etc/key.p12 com.ibm.ssl.keyStorePassword The password for the KeyStore object that you want the KeyManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.keyStoreType Type of key store, for example PKCS12, JKS, or JCEKS. com.ibm.ssl.keyStoreProvider Key store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.trustStore The name of the file that contains the KeyStore object that you want the TrustManager to use. com.ibm.ssl.trustStorePassword The password for the TrustStore object that you want the TrustManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.trustStoreType The type of KeyStore object that you want the default TrustManager to use. Same possible values as keyStoreType. com.ibm.ssl.trustStoreProvider Trust store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.enabledCipherSuites A list of which ciphers are enabled. Values are dependent on the provider, for example: SSL\_RSA\_WITH\_AES\_128\_CBC\_SHA;SSL\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA. com.ibm.ssl.keyManager Sets the algorithm that will be used to instantiate a KeyManagerFactory object instead of using the default algorithm available in the platform. Example values: IbmX509 or IBMJ9X509. com.ibm.ssl.trustManager Sets the algorithm that will be used to instantiate a TrustManagerFactory object instead of using the default algorithm available in the platform. Example values: PKIX or IBMJ9X509. |  | Properties |
| **sslHostnameVerifier** (security) | Sets the HostnameVerifier for the SSL connection. Note that it will be used after handshake on a connection and you should do actions by yourself when hostname is verified error. There is no default HostnameVerifier. |  | HostnameVerifier |
| **userName** (security) | Username to be used for authentication against the MQTT broker. |  | String |

## Message Headers

The Paho component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMqttTopic** (consumer) Constant: [`MQTT_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-paho/latest/org/apache/camel/component/paho/PahoConstants.html#MQTT_TOPIC) | The name of the topic. |  | String |
| **CamelMqttQoS** (consumer) Constant: [`MQTT_QOS`](https://javadoc.io/doc/org.apache.camel/camel-paho/latest/org/apache/camel/component/paho/PahoConstants.html#MQTT_QOS) | The quality of service of the incoming message. |  | Integer |
| **CamelPahoQos** (producer) Constant: [`CAMEL_PAHO_MSG_QOS`](https://javadoc.io/doc/org.apache.camel/camel-paho/latest/org/apache/camel/component/paho/PahoConstants.html#CAMEL_PAHO_MSG_QOS) | The client quality of service level (0-2). |  | Integer |
| **CamelPahoRetained** (producer) Constant: [`CAMEL_PAHO_MSG_RETAINED`](https://javadoc.io/doc/org.apache.camel/camel-paho/latest/org/apache/camel/component/paho/PahoConstants.html#CAMEL_PAHO_MSG_RETAINED) | Retain option. |  | Boolean |
| **CamelPahoOverrideTopic** (producer) Constant: [`CAMEL_PAHO_OVERRIDE_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-paho/latest/org/apache/camel/component/paho/PahoConstants.html#CAMEL_PAHO_OVERRIDE_TOPIC) | The name of topic to override and send to instead of topic specified on endpoint. |  | String |

## Usage

### Default payload type

By default, the Camel Paho component operates on the binary payloads extracted out of (or put into) the MQTT message:

_Java-only: receiving and sending binary payloads using the Paho component_

```java
// Receive payload
byte[] payload = (byte[]) consumerTemplate.receiveBody("paho:topic");

// Send payload
byte[] payload = "message".getBytes();
producerTemplate.sendBody("paho:topic", payload);
```

Of course, Camel build-in [type conversion API](../../manual/type-converter.md) can perform the automatic data type transformations for you. In the example below Camel automatically converts binary payload into `String` (and conversely):

_Java-only: automatic type conversion of payloads_

```java
// Receive payload
String payload = consumerTemplate.receiveBody("paho:topic", String.class);

// Send payload
String payload = "message";
producerTemplate.sendBody("paho:topic", payload);
```

## Examples

For example, the following snippet reads messages from the MQTT broker installed on the same host as the Camel router:

-   Java
    
-   XML
    
-   YAML
    

```java
from("paho:some/queue")
    .to("mock:test");
```

```xml
<route>
  <from uri="paho:some/queue"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    from:
      uri: paho:some/queue
      steps:
        - to:
            uri: mock:test
```

While the snippet below sends a message to the MQTT broker:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:test")
    .to("paho:some/target/queue");
```

```xml
<route>
  <from uri="direct:test"/>
  <to uri="paho:some/target/queue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:test
      steps:
        - to:
            uri: paho:some/target/queue
```

For example, this is how to read messages from the remote MQTT broker:

-   Java
    
-   XML
    
-   YAML
    

```java
from("paho:some/queue?brokerUrl=tcp://iot.eclipse.org:1883")
    .to("mock:test");
```

```xml
<route>
  <from uri="paho:some/queue?brokerUrl=tcp://iot.eclipse.org:1883"/>
  <to uri="mock:test"/>
</route>
```

```yaml
- route:
    from:
      uri: paho:some/queue
      parameters:
        brokerUrl: "tcp://iot.eclipse.org:1883"
      steps:
        - to:
            uri: mock:test
```

And here we override the default topic and set to a dynamic topic

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:test")
    .setHeader(PahoConstants.CAMEL_PAHO_OVERRIDE_TOPIC, simple("${header.customerId}"))
    .to("paho:some/target/queue");
```

```xml
<route>
    <from uri="direct:test"/>
    <setHeader name="CamelPahoOverrideTopic">
        <simple>${header.customerId}</simple>
    </setHeader>
    <to uri="paho:some/target/queue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:test
    steps:
      - setHeader:
          name: CamelPahoOverrideTopic
          simple: "${header.customerId}"
      - to:
          uri: paho:some/target/queue
```

## Spring Boot Auto-Configuration

When using paho with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-paho-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 33 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.paho.automatic-reconnect** | Sets whether the client will automatically attempt to reconnect to the server if the connection is lost. If set to false, the client will not attempt to automatically reconnect to the server in the event that the connection is lost. If set to true, in the event that the connection is lost, the client will attempt to reconnect to the server. It will initially wait 1 second before it attempts to reconnect, for every failed reconnect attempt, the delay will double until it is at 2 minutes at which point the delay will stay at 2 minutes. | true | Boolean |
| **camel.component.paho.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.paho.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.paho.broker-url** | The URL of the MQTT broker. | tcp://localhost:1883 | String |
| **camel.component.paho.clean-session** | Sets whether the client and server should remember state across restarts and reconnects. If set to false both the client and server will maintain state across restarts of the client, the server and the connection. As state is maintained: Message delivery will be reliable meeting the specified QOS even if the client, server or connection are restarted. The server will treat a subscription as durable. If set to true the client and server will not maintain state across restarts of the client, the server or the connection. This means Message delivery to the specified QOS cannot be maintained if the client, server or connection are restarted The server will treat a subscription as non-durable. | true | Boolean |
| **camel.component.paho.client** | To use a shared Paho client. The option is a org.eclipse.paho.client.mqttv3.MqttClient type. |  | MqttClient |
| **camel.component.paho.client-id** | MQTT client identifier. The identifier must be unique. |  | String |
| **camel.component.paho.configuration** | To use the shared Paho configuration. The option is a org.apache.camel.component.paho.PahoConfiguration type. |  | PahoConfiguration |
| **camel.component.paho.connection-timeout** | Sets the connection timeout value. This value, measured in seconds, defines the maximum time interval the client will wait for the network connection to the MQTT server to be established. The default timeout is 30 seconds. A value of 0 disables timeout processing meaning the client will wait until the network connection is made successfully or fails. | 30 | Integer |
| **camel.component.paho.custom-web-socket-headers** | Sets the Custom WebSocket Headers for the WebSocket Connection. The option is a java.util.Properties type. |  | Properties |
| **camel.component.paho.enabled** | Whether to enable auto configuration of the paho component. This is enabled by default. |  | Boolean |
| **camel.component.paho.executor-service-timeout** | Set the time in seconds that the executor service should wait when terminating before forcefully terminating. It is not recommended to change this value unless you are absolutely sure that you need to. | 1 | Integer |
| **camel.component.paho.file-persistence-directory** | Base directory used by file persistence. Will by default use user directory. |  | String |
| **camel.component.paho.https-hostname-verification-enabled** | Whether SSL HostnameVerifier is enabled or not. The default value is true. | true | Boolean |
| **camel.component.paho.keep-alive-interval** | Sets the keep alive interval. This value, measured in seconds, defines the maximum time interval between messages sent or received. It enables the client to detect if the server is no longer available, without having to wait for the TCP/IP timeout. The client will ensure that at least one message travels across the network within each keep alive period. In the absence of a data-related message during the time period, the client sends a very small ping message, which the server will acknowledge. A value of 0 disables keepalive processing in the client. The default value is 60 seconds. | 60 | Integer |
| **camel.component.paho.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.paho.manual-acks-enabled** | Sets whether to use manual acknowledgements for the client. By default, this is false and message will be automatically acknowledged. If set to true, the acknowledgement is added in the exchange’s completion callback. | false | Boolean |
| **camel.component.paho.max-inflight** | Sets the max inflight. please increase this value in a high traffic environment. The default value is 10. | 10 | Integer |
| **camel.component.paho.max-reconnect-delay** | Get the maximum time (in millis) to wait between reconnects. | 128000 | Integer |
| **camel.component.paho.mqtt-version** | Sets the MQTT version. The default action is to connect with version 3.1.1, and to fall back to 3.1 if that fails. Version 3.1.1 or 3.1 can be selected specifically, with no fall back, by using the MQTT\_VERSION\_3\_1\_1 or MQTT\_VERSION\_3\_1 options respectively. |  | Integer |
| **camel.component.paho.password** | Password to be used for authentication against the MQTT broker. |  | String |
| **camel.component.paho.persistence** | Client persistence to be used - memory or file. | memory | PahoPersistence |
| **camel.component.paho.qos** | Client quality of service level (0-2). | 2 | Integer |
| **camel.component.paho.retained** | Retain option. | false | Boolean |
| **camel.component.paho.server-u-r-is** | Set a list of one or more serverURIs the client may connect to. Multiple servers can be separated by comma. Each serverURI specifies the address of a server that the client may connect to. Two types of connection are supported tcp:// for a TCP connection and ssl:// for a TCP connection secured by SSL/TLS. For example: tcp://localhost:1883 ssl://localhost:8883 If the port is not specified, it will default to 1883 for tcp:// URIs, and 8883 for ssl:// URIs. If serverURIs is set then it overrides the serverURI parameter passed in on the constructor of the MQTT client. When an attempt to connect is initiated the client will start with the first serverURI in the list and work through the list until a connection is established with a server. If a connection cannot be made to any of the servers then the connect attempt fails. Specifying a list of servers that a client may connect to has several uses: High Availability and reliable message delivery Some MQTT servers support a high availability feature where two or more equal MQTT servers share state. An MQTT client can connect to any of the equal servers and be assured that messages are reliably delivered and durable subscriptions are maintained no matter which server the client connects to. The cleansession flag must be set to false if durable subscriptions and/or reliable message delivery is required. Hunt List A set of servers may be specified that are not equal (as in the high availability option). As no state is shared across the servers reliable message delivery and durable subscriptions are not valid. The cleansession flag must be set to true if the hunt list mode is used. |  | String |
| **camel.component.paho.socket-factory** | Sets the SocketFactory to use. This allows an application to apply its own policies around the creation of network sockets. If using an SSL connection, an SSLSocketFactory can be used to supply application-specific security settings. The option is a javax.net.SocketFactory type. |  | SocketFactory |
| **camel.component.paho.ssl-client-props** | Sets the SSL properties for the connection. Note that these properties are only valid if an implementation of the Java Secure Socket Extensions (JSSE) is available. These properties are not used if a custom SocketFactory has been set. The following properties can be used: com.ibm.ssl.protocol One of: SSL, SSLv3, TLS, TLSv1, SSL\_TLS. com.ibm.ssl.contextProvider Underlying JSSE provider. For example IBMJSSE2 or SunJSSE com.ibm.ssl.keyStore The name of the file that contains the KeyStore object that you want the KeyManager to use. For example /mydir/etc/key.p12 com.ibm.ssl.keyStorePassword The password for the KeyStore object that you want the KeyManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.keyStoreType Type of key store, for example PKCS12, JKS, or JCEKS. com.ibm.ssl.keyStoreProvider Key store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.trustStore The name of the file that contains the KeyStore object that you want the TrustManager to use. com.ibm.ssl.trustStorePassword The password for the TrustStore object that you want the TrustManager to use. The password can either be in plain-text, or may be obfuscated using the static method: com.ibm.micro.security.Password.obfuscate(char password). This obfuscates the password using a simple and insecure XOR and Base64 encoding mechanism. Note that this is only a simple scrambler to obfuscate clear-text passwords. com.ibm.ssl.trustStoreType The type of KeyStore object that you want the default TrustManager to use. Same possible values as keyStoreType. com.ibm.ssl.trustStoreProvider Trust store provider, for example IBMJCE or IBMJCEFIPS. com.ibm.ssl.enabledCipherSuites A list of which ciphers are enabled. Values are dependent on the provider, for example: SSL\_RSA\_WITH\_AES\_128\_CBC\_SHA;SSL\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA. com.ibm.ssl.keyManager Sets the algorithm that will be used to instantiate a KeyManagerFactory object instead of using the default algorithm available in the platform. Example values: IbmX509 or IBMJ9X509. com.ibm.ssl.trustManager Sets the algorithm that will be used to instantiate a TrustManagerFactory object instead of using the default algorithm available in the platform. Example values: PKIX or IBMJ9X509. The option is a java.util.Properties type. |  | Properties |
| **camel.component.paho.ssl-hostname-verifier** | Sets the HostnameVerifier for the SSL connection. Note that it will be used after handshake on a connection and you should do actions by yourself when hostname is verified error. There is no default HostnameVerifier. The option is a javax.net.ssl.HostnameVerifier type. |  | HostnameVerifier |
| **camel.component.paho.user-name** | Username to be used for authentication against the MQTT broker. |  | String |
| **camel.component.paho.will-payload** | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the message for the LWT. |  | String |
| **camel.component.paho.will-qos** | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the quality of service to publish the message at (0, 1 or 2). |  | Integer |
| **camel.component.paho.will-retained** | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets whether or not the message should be retained. | false | Boolean |
| **camel.component.paho.will-topic** | Sets the Last Will and Testament (LWT) for the connection. In the event that this client unexpectedly loses its connection to the server, the server will publish a message to itself using the supplied details. Sets the topic that the willPayload will be published to. |  | String |