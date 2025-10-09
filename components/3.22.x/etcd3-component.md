# Etcd v3

**Since Camel 3.19**

**Both producer and consumer are supported**

The camel Etcd component allows you to work with Etcd, a distributed reliable key-value store.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-etcd3</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

etcd3:path\[?options\]

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

The Etcd v3 component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration. |  | Etcd3Configuration |
| **endpoints** (common) | Configure etcd server endpoints using the IPNameResolver. | Etcd3Constants.ETCD\_DEFAULT\_ENDPOINTS | String\[\] |
| **keyCharset** (common) | Configure the charset to use for the keys. | UTF-8 | String |
| **namespace** (common) | Configure the namespace of keys used. / will be treated as no namespace. |  | String |
| **prefix** (common) | To apply an action on all the key-value pairs whose key that starts with the target path. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **fromIndex** (consumer (advanced)) | The index to watch from. | 0 | long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **valueCharset** (producer) | Configure the charset to use for the values. | UTF-8 | String |
| **authHeaders** (advanced) | Configure the headers to be added to auth request headers. |  | Map |
| **authority** (advanced) | Configure the authority used to authenticate connections to servers. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionTimeout** (advanced) | Configure the connection timeout. |  | Duration |
| **headers** (advanced) | Configure the headers to be added to http request headers. |  | Map |
| **keepAliveTime** (advanced) | Configure the interval for gRPC keepalives. The current minimum allowed by gRPC is 10 seconds. | 30 seconds | Duration |
| **keepAliveTimeout** (advanced) | Configure the timeout for gRPC keepalives. | 10 seconds | Duration |
| **loadBalancerPolicy** (advanced) | Configure etcd load balancer policy. |  | String |
| **maxInboundMessageSize** (advanced) | Configure the maximum message size allowed for a single gRPC frame. |  | Integer |
| **retryDelay** (advanced) | Configure the delay between retries in milliseconds. | 500 | long |
| **retryMaxDelay** (advanced) | Configure the max backing off delay between retries in milliseconds. | 2500 | long |
| **retryMaxDuration** (advanced) | Configure the retries max duration. |  | Duration |
| **servicePath** (cloud) | The path to look for service discovery. | /services/ | String |
| **password** (security) | Configure etcd auth password. |  | String |
| **sslContext** (security) | Configure SSL/TLS context to use instead of the system default. |  | SslContext |
| **userName** (security) | Configure etcd auth user. |  | String |

## Endpoint Options

The Etcd v3 endpoint is configured using URI syntax:

etcd3:path

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **path** (common) | The path the endpoint refers to. |  | String |

### Query Parameters (25 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoints** (common) | Configure etcd server endpoints using the IPNameResolver. | Etcd3Constants.ETCD\_DEFAULT\_ENDPOINTS | String\[\] |
| **keyCharset** (common) | Configure the charset to use for the keys. | UTF-8 | String |
| **namespace** (common) | Configure the namespace of keys used. / will be treated as no namespace. |  | String |
| **prefix** (common) | To apply an action on all the key-value pairs whose key that starts with the target path. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **fromIndex** (consumer (advanced)) | The index to watch from. | 0 | long |
| **valueCharset** (producer) | Configure the charset to use for the values. | UTF-8 | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **authHeaders** (advanced) | Configure the headers to be added to auth request headers. |  | Map |
| **authority** (advanced) | Configure the authority used to authenticate connections to servers. |  | String |
| **connectionTimeout** (advanced) | Configure the connection timeout. |  | Duration |
| **headers** (advanced) | Configure the headers to be added to http request headers. |  | Map |
| **keepAliveTime** (advanced) | Configure the interval for gRPC keepalives. The current minimum allowed by gRPC is 10 seconds. | 30 seconds | Duration |
| **keepAliveTimeout** (advanced) | Configure the timeout for gRPC keepalives. | 10 seconds | Duration |
| **loadBalancerPolicy** (advanced) | Configure etcd load balancer policy. |  | String |
| **maxInboundMessageSize** (advanced) | Configure the maximum message size allowed for a single gRPC frame. |  | Integer |
| **retryDelay** (advanced) | Configure the delay between retries in milliseconds. | 500 | long |
| **retryMaxDelay** (advanced) | Configure the max backing off delay between retries in milliseconds. | 2500 | long |
| **retryMaxDuration** (advanced) | Configure the retries max duration. |  | Duration |
| **servicePath** (cloud) | The path to look for service discovery. | /services/ | String |
| **password** (security) | Configure etcd auth password. |  | String |
| **sslContext** (security) | Configure SSL/TLS context to use instead of the system default. |  | SslContext |
| **userName** (security) | Configure etcd auth user. |  | String |

## Message Headers

The Etcd v3 component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelEtcdAction** (producer) Constant: [`ETCD_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-etcd3/latest/org/apache/camel/component/etcd3/Etcd3Constants.html#ETCD_ACTION) | The action to perform. Supported values: set get delete. |  | String |
| **CamelEtcdPath** (common) Constant: [`ETCD_PATH`](https://javadoc.io/doc/org.apache.camel/camel-etcd3/latest/org/apache/camel/component/etcd3/Etcd3Constants.html#ETCD_PATH) | The target path. |  | String |
| **CamelEtcdIsPrefix** (producer) Constant: [`ETCD_IS_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-etcd3/latest/org/apache/camel/component/etcd3/Etcd3Constants.html#ETCD_IS_PREFIX) | To apply an action on all the key-value pairs whose key that starts with the target path. |  | Boolean |
| **CamelEtcdKeyCharset** (producer) Constant: [`ETCD_KEY_CHARSET`](https://javadoc.io/doc/org.apache.camel/camel-etcd3/latest/org/apache/camel/component/etcd3/Etcd3Constants.html#ETCD_KEY_CHARSET) | The charset to use for the keys. |  | String |
| **CamelEtcdValueCharset** (producer) Constant: [`ETCD_VALUE_CHARSET`](https://javadoc.io/doc/org.apache.camel/camel-etcd3/latest/org/apache/camel/component/etcd3/Etcd3Constants.html#ETCD_VALUE_CHARSET) | The charset to use for the values. |  | String |

## Producer Operations (Since 3.20)

The following ETCD operations are currently supported. Simply set the exchange header with a key of "CamelEtcdAction" and a value set to one of the following.

   
| operation | input message body | output message body | description |
| --- | --- | --- | --- |
| set | **String** value of the key-value pair to put | **PutResponse** result of a put operation | Puts a new key-value pair into etcd where the option "path" or the exchange header "CamelEtcdPath" is the key. You can set the key charset by setting the exchange header with the key "CamelEtcdKeyCharset". You can set the value charset by setting the exchange header with the key "CamelEtcdValueCharset". |
| get | None | **GetResponse** result of the get operation | Retrieves the key-value pair(s) that match with the key corresponding to the option "path" or the exchange header "CamelEtcdPath". You can set the key charset by setting the exchange header with the key "CamelEtcdKeyCharset". You indicate if the key is a prefix by setting the exchange header with the key "CamelEtcdIsPrefix" to true. |
| delete | None | **DeleteResponse** result of the delete operation | Deletes the key-value pair(s) that match with the key corresponding to the option "path" or the exchange header "CamelEtcdPath". You can set the key charset by setting the exchange header with the key "CamelEtcdKeyCharset". You indicate if the key is a prefix by setting the exchange header with the key "CamelEtcdIsPrefix" to true. == Consumer (Since 3.20) The consumer of the etcd components allows to watch changes on the matching key-value pair(s). One exchange is created per event with the header "CamelEtcdPath" set to the path of the corresponding key-value pair and the body of type **WatchEvent**. You can set the key charset by setting the exchange header with the key "CamelEtcdKeyCharset". You indicate if the key is a prefix by setting the exchange header with the key "CamelEtcdIsPrefix" to true. By default, the consumer receives only the latest changes, but it is also possible to start watching events from a specific revision by setting the option "fromIndex" to the expected starting index. == AggregationRepository The Etcd3 component provides an `AggregationStrategy` to use Etcd as the backend datastore. == RoutePolicy (Since 3.20) The Etcd3 component provides a `RoutePolicy` to use Etcd as clustered lock. |

## Spring Boot Auto-Configuration

When using etcd3 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-etcd3-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.etcd3.auth-headers** | Configure the headers to be added to auth request headers. |  | Map |
| **camel.component.etcd3.authority** | Configure the authority used to authenticate connections to servers. |  | String |
| **camel.component.etcd3.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.etcd3.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.etcd3.configuration** | Component configuration. The option is a org.apache.camel.component.etcd3.Etcd3Configuration type. |  | Etcd3Configuration |
| **camel.component.etcd3.connection-timeout** | Configure the connection timeout. The option is a java.time.Duration type. |  | Duration |
| **camel.component.etcd3.enabled** | Whether to enable auto configuration of the etcd3 component. This is enabled by default. |  | Boolean |
| **camel.component.etcd3.endpoints** | Configure etcd server endpoints using the IPNameResolver. |  | String\[\] |
| **camel.component.etcd3.from-index** | The index to watch from. | 0 | Long |
| **camel.component.etcd3.headers** | Configure the headers to be added to http request headers. |  | Map |
| **camel.component.etcd3.keep-alive-time** | Configure the interval for gRPC keepalives. The current minimum allowed by gRPC is 10 seconds. The option is a java.time.Duration type. |  | Duration |
| **camel.component.etcd3.keep-alive-timeout** | Configure the timeout for gRPC keepalives. The option is a java.time.Duration type. |  | Duration |
| **camel.component.etcd3.key-charset** | Configure the charset to use for the keys. | UTF-8 | String |
| **camel.component.etcd3.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.etcd3.load-balancer-policy** | Configure etcd load balancer policy. |  | String |
| **camel.component.etcd3.max-inbound-message-size** | Configure the maximum message size allowed for a single gRPC frame. |  | Integer |
| **camel.component.etcd3.namespace** | Configure the namespace of keys used. / will be treated as no namespace. |  | String |
| **camel.component.etcd3.password** | Configure etcd auth password. |  | String |
| **camel.component.etcd3.prefix** | To apply an action on all the key-value pairs whose key that starts with the target path. | false | Boolean |
| **camel.component.etcd3.retry-delay** | Configure the delay between retries in milliseconds. | 500 | Long |
| **camel.component.etcd3.retry-max-delay** | Configure the max backing off delay between retries in milliseconds. | 2500 | Long |
| **camel.component.etcd3.retry-max-duration** | Configure the retries max duration. The option is a java.time.Duration type. |  | Duration |
| **camel.component.etcd3.service-path** | The path to look for service discovery. | /services/ | String |
| **camel.component.etcd3.ssl-context** | Configure SSL/TLS context to use instead of the system default. The option is a io.netty.handler.ssl.SslContext type. |  | SslContext |
| **camel.component.etcd3.user-name** | Configure etcd auth user. |  | String |
| **camel.component.etcd3.value-charset** | Configure the charset to use for the values. | UTF-8 | String |