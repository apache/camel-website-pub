# CometD

**Since Camel 2.0**

**Both producer and consumer are supported**

The Cometd component is a transport for working with the [jetty](http://www.mortbay.org/jetty) implementation of the [cometd/bayeux protocol](http://docs.codehaus.org/display/JETTY/Cometd+%28aka+Bayeux%29).  
Using this component in combination with the dojo toolkit library it’s possible to push Camel messages directly into the browser using an AJAX based mechanism.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-cometd</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

cometd://host:port/channelName\[?options\]

The **channelName** represents a topic that can be subscribed to by the Camel endpoints.

cometd://localhost:8080/service/mychannel
cometds://localhost:8443/service/mychannel

where `cometds:` represents an SSL configured endpoint.

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

The CometD component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **extensions** (advanced) | To use a list of custom BayeuxServer.Extension that allows modifying incoming and outgoing requests. |  | List |
| **securityPolicy** (security) | To use a custom configured SecurityPolicy to control authorization. |  | SecurityPolicy |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslKeyPassword** (security) | The password for the keystore when using SSL. |  | String |
| **sslKeystore** (security) | The path to the keystore. |  | String |
| **sslPassword** (security) | The password when using SSL. |  | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The CometD endpoint is configured using URI syntax:

cometd:host:port/channelName

with the following path and query parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Hostname. |  | String |
| **port** (common) | **Required** Host port number. |  | int |
| **channelName** (common) | **Required** The channelName represents a topic that can be subscribed to by the Camel endpoints. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowedOrigins** (common) | The origins domain that support to cross, if the crosssOriginFilterOn is true. | \* | String |
| **baseResource** (common) | The root directory for the web resources or classpath. Use the protocol file: or classpath: depending if you want that the component loads the resource from file system or classpath. Classpath is required for OSGI deployment where the resources are packaged in the jar. |  | String |
| **crossOriginFilterOn** (common) | If true, the server will support for cross-domain filtering. | false | boolean |
| **filterPath** (common) | The filterPath will be used by the CrossOriginFilter, if the crosssOriginFilterOn is true. |  | String |
| **interval** (common) | The client side poll timeout in milliseconds. How long a client will wait between reconnects. |  | int |
| **jsonCommented** (common) | If true, the server will accept JSON wrapped in a comment and will generate JSON wrapped in a comment. This is a defence against Ajax Hijacking. | true | boolean |
| **logLevel** (common) | 
Logging level. 0=none, 1=info, 2=debug.

Enum values:

-   0
    
-   1
    
-   2
    





 | 1 | int |
| **maxInterval** (common) | The max client side poll timeout in milliseconds. A client will be removed if a connection is not received in this time. | 30000 | int |
| **multiFrameInterval** (common) | The client side poll timeout, if multiple connections are detected from the same browser. | 1500 | int |
| **timeout** (common) | The server side poll timeout in milliseconds. This is how long the server will hold a reconnect request before responding. | 240000 | int |
| **sessionHeadersEnabled** (consumer) | Whether to include the server session headers in the Camel message when creating a Camel Message for incoming requests. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **disconnectLocalSession** (producer) | Whether to disconnect local sessions after publishing a message to its channel. Disconnecting local session is needed as they are not swept by default by CometD, and therefore you can run out of memory. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The CometD component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CometdClientId** (common) Constant: [`COMETD_CLIENT_ID_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-cometd/latest/org/apache/camel/component/cometd/CometdBinding.html#COMETD_CLIENT_ID_HEADER_NAME) | The clientId of the session. |  | String |
| **subscription** (common) Constant: [`COMETD_SUBSCRIPTION_HEADER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-cometd/latest/org/apache/camel/component/cometd/CometdBinding.html#COMETD_SUBSCRIPTION_HEADER_NAME) | The subscription. |  | String |

## Sample

Here is some examples on How to pass the parameters

For file (for webapp resources located in the Web Application directory -→ cometd://localhost:8080?resourceBase=file./webapp  
For classpath (when by example the web resources are packaged inside the webapp folder -→ cometd://localhost:8080?resourceBase=classpath:webapp

## Authentication

You can configure custom `SecurityPolicy` and ``Extension’s to the `CometdComponent`` which allows you to use authentication as [documented here](http://cometd.org/documentation/howtos/authentication)

## Setting up SSL for Cometd Component

### Using the JSSE Configuration Utility

The Cometd component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the Cometd component. You need to configure SSL on the CometdComponent.

Programmatic configuration of the component

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/users/home/server/keystore.jks");
ksp.setPassword("keystorePassword");

KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("keyPassword");

TrustManagersParameters tmp = new TrustManagersParameters();
tmp.setKeyStore(ksp);

SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);
scp.setTrustManagers(tmp);

CometdComponent commetdComponent = getContext().getComponent("cometds", CometdComponent.class);
commetdComponent.setSslContextParameters(scp);
```

Spring DSL based configuration of endpoint

```xml
  <camel:sslContextParameters
      id="sslContextParameters">
    <camel:keyManagers
        keyPassword="keyPassword">
      <camel:keyStore
          resource="/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
    <camel:trustManagers>
      <camel:keyStore
          resource="/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
  </camel:sslContextParameters>

  <bean id="cometd" class="org.apache.camel.component.cometd.CometdComponent">
    <property name="sslContextParameters" ref="sslContextParameters"/>
  </bean>

  <to uri="cometds://127.0.0.1:443/service/test?baseResource=file:./target/test-classes/webapp&timeout=240000&interval=0&maxInterval=30000&multiFrameInterval=1500&jsonCommented=true&logLevel=2"/>...
```

## Spring Boot Auto-Configuration

When using cometd with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-cometd-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.cometd.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.cometd.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.cometd.enabled** | Whether to enable auto configuration of the cometd component. This is enabled by default. |  | Boolean |
| **camel.component.cometd.extensions** | To use a list of custom BayeuxServer.Extension that allows modifying incoming and outgoing requests. |  | List |
| **camel.component.cometd.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.cometd.security-policy** | To use a custom configured SecurityPolicy to control authorization. The option is a org.cometd.bayeux.server.SecurityPolicy type. |  | SecurityPolicy |
| **camel.component.cometd.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.cometd.ssl-key-password** | The password for the keystore when using SSL. |  | String |
| **camel.component.cometd.ssl-keystore** | The path to the keystore. |  | String |
| **camel.component.cometd.ssl-password** | The password when using SSL. |  | String |
| **camel.component.cometd.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |