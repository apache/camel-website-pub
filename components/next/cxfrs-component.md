# CXF-RS

**Since Camel 2.0**

**Both producer and consumer are supported**

The CXFRS component provides integration with [Apache CXF](http://cxf.apache.org) for connecting to JAX-RS 1.1 and 2.0 services hosted in CXF.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
   <groupId>org.apache.camel</groupId>
   <artifactId>camel-cxf-rest</artifactId>
   <version>x.x.x</version>  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

cxfrs://address?options

Where **address** represents the CXF endpoint’s address

cxfrs:bean:rsEndpoint

Where **rsEndpoint** represents the spring bean’s name, which presents the CXFRS client or server

For either style above, you can append options to the URI as follows:

cxfrs:bean:cxfEndpoint?resourceClasses=org.apache.camel.rs.Example

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

The CXF-RS component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **synchronous** (producer (advanced)) | Whether to always process the exchange synchronously. If true, the producer sends each request without an InvocationCallback and waits for the response, and the consumer runs the route without a CXF continuation. The component sets the value on each endpoint that it creates, including a bean: endpoint, unless the endpoint URI sets synchronous. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **useGlobalSslContextParameters** (security) | Whether to use the global SSL context parameters of the CamelContext for each endpoint that the component creates and that has no sslContextParameters. The producer uses them for the HTTPS requests that it sends. The consumer does not use them. | false | boolean |

## Endpoint Options

The CXF-RS endpoint is configured using URI syntax:

cxfrs:beanId:address

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **beanId** (common) | The id of the registry bean that defines this endpoint. Written in the path of the endpoint URI in place of the service address, with the prefix bean:, for example bean:rsEndpoint. The bean is a CxfRsEndpoint, or, with camel-cxf-spring-rest, a CXF JAXRSServerFactoryBean for the consumer or a JAXRSClientFactoryBean for the producer, for example from a cxf:rsServer or cxf:rsClient element in Spring XML. The options of the endpoint URI are applied after the settings of the bean. On a CxfRsEndpoint bean, they are applied to the bean itself, so endpoint URIs with different options must not share one CxfRsEndpoint bean. |  | String |
| **address** (common) | The service address, for example [http://localhost:9000/rest](http://localhost:9000/rest). The consumer receives requests at this address, and the producer sends requests to it. The CamelDestinationOverrideUrl header replaces this address for a request that the producer sends. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **features** (common) | The CXF features to add to the server that the consumer creates and to each client that the producer creates, as a List of org.apache.cxf.feature.Feature. Written in the endpoint URI as bean ids with the prefix #, separated by commas, for example #gzipFeature, or as the id of one List bean, for example #myFeatures. |  | List |
| **modelRef** (common) | The location of a CXF user model, for example classpath:/model/customers.xml. The model is an XML document that describes resources and their operations in place of JAX-RS annotations, and the name attribute of each resource names its resource class. On the consumer, one resource of the model can be without a name attribute: the consumer gives it the interface org.apache.camel.component.cxf.jaxrs.DefaultModelResource, which works only when performInvocation is false. The producer builds requests from the model only with the proxy-based API. |  | String |
| **providers** (common) | The JAX-RS providers to add to the server that the consumer creates and to each client that the producer creates, for example a MessageBodyReader and MessageBodyWriter for JSON. Written in the endpoint URI as bean ids with the prefix #, separated by commas, for example #jsonProvider,#xmlProvider. The built-in CXF providers stay registered. |  | String |
| **resourceClasses** (common) | The JAX-RS resource classes. Written in the endpoint URI as fully qualified class names, separated by commas. The consumer serves them as root resources, and a resource class can be an interface only when performInvocation is false. Without resource classes, the consumer needs other resources, for example from serviceBeans or modelRef. With the proxy-based API, the producer calls the resource method named by the CamelCxfOperationName header on a proxy of the first resource class. With the WebClient API, the producer does not need resource classes. |  | List |
| **schemaLocations** (common) | Sets the locations of the schema(s) which can be used to validate the incoming XML or JAXB-driven JSON. |  | List |
| **skipFaultLogging** (common) | Whether to skip the log entry that the PhaseInterceptorChain writes when an interceptor throws an exception. Sets the CXF property org.apache.cxf.logging.FaultListener to a FaultListener that skips this log entry. Other log entries that CXF writes while it handles the fault are not affected. | false | boolean |
| **bindingStyle** (consumer) | 
How the consumer maps the request to the Camel message and the reply to the response. Default: the message body is a MessageContentsList of the parameters of the resource method. SimpleConsumer: the path, query, header, cookie, form and matrix parameters become Camel headers named as in their annotations, and the first other parameter, normally the request entity, becomes the message body. The component documentation describes SimpleConsumer in detail. Custom: the CxfRsBinding of the binding option maps the request and the reply. Setting the binding option sets bindingStyle to Custom. The producer uses the binding that Default or Custom selects, and cannot be created with SimpleConsumer.

Enum values:

-   SimpleConsumer
    
-   Default
    
-   Custom
    





 | Default | BindingStyle |
| **publishedEndpointUrl** (consumer) | The address to publish in the WADL that the consumer serves at the service address followed by ?\_wadl. It replaces the base attribute of the resources element. Use it when clients reach the service through another address, for example when the service is behind a proxy. CXF serves the WADL only when the module cxf-rt-rs-service-description is on the classpath. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **serviceBeans** (consumer (advanced)) | The beans to serve as JAX-RS root resources of the consumer, in addition to resourceClasses. Written in the endpoint URI as bean ids with the prefix #, separated by commas, for example #customerService, or as the id of one List bean, for example #myServiceBeans. The consumer calls the resource methods of the beans only when performInvocation is true, but always calls their sub-resource locators. |  | String |
| **cookieHandler** (producer) | To use a custom org.apache.camel.http.base.cookie.CookieHandler to keep the cookies of an HTTP session between the requests that the producer sends. An InstanceCookieHandler keeps the cookies in the handler itself, and an ExchangeCookieHandler keeps them in an exchange property. The consumer does not use it. |  | CookieHandler |
| **hostnameVerifier** (producer) | To use a custom javax.net.ssl.HostnameVerifier for the HTTPS requests that the producer sends. The consumer does not use it. |  | HostnameVerifier |
| **sslContextParameters** (producer) | To use a custom org.apache.camel.support.jsse.SSLContextParameters for the HTTPS requests that the producer sends. If not set, the component sets it to the global SSL context parameters when it creates the endpoint and its own useGlobalSslContextParameters option is true. The consumer does not use it. |  | SSLContextParameters |
| **throwExceptionOnFailure** (producer) | Whether to fail the exchange with an org.apache.camel.component.cxf.common.CxfOperationException when the HTTP status code of the response is greater than 207. The exception holds the status code, the response headers and the response entity. When synchronous is true, the producer does this only when it reads the response as a jakarta.ws.rs.core.Response. CXF itself can also fail the exchange for a status code of 300 or more, for example with the proxy-based API when the resource method does not return a Response. | true | boolean |
| **httpClientAPI** (producer (advanced)) | Whether to use the CXF WebClient API instead of the proxy-based API. With the WebClient API, the producer builds the request from the CamelHttpMethod and CamelHttpPath headers and, for methods such as POST and PUT, takes the request entity from the message body. With the proxy-based API, the producer calls the resource method named by the CamelCxfOperationName header on a proxy of the first resource class, with the message body as its parameters. The CamelCxfRsUsingHttpAPI header replaces this option for a request that the producer sends. | true | boolean |
| **ignoreDeleteMethodMessageBody** (producer (advanced)) | Whether to ignore the message body for a DELETE request and send the request without an entity. If false, the producer takes the request entity of a DELETE request from the message body, as for POST and PUT. The producer uses this option only with the WebClient API. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxClientCacheSize** (producer (advanced)) | The maximum number of CXF JAXRSClientFactoryBean instances that the producer keeps in its cache, one for each address that it sends requests to: the service address, or the address in the CamelDestinationOverrideUrl header. When the cache is full, the producer drops the least recently used factory bean. The producer creates a new client from the factory bean for each request. The value must be greater than 0. | 10 | int |
| **synchronous** (producer (advanced)) | Whether to always process the exchange synchronously. If true, the producer sends each request without an InvocationCallback and waits for the response, and the consumer runs the route without a CXF continuation. The component sets it to the value of its own synchronous option when it creates the endpoint, including a bean: endpoint, unless the endpoint URI sets it. | false | boolean |
| **binding** (advanced) | To use a custom org.apache.camel.component.cxf.jaxrs.CxfRsBinding to map between the Camel message and the JAX-RS request and response, on the consumer and on the producer. Setting this option sets bindingStyle to Custom. |  | CxfRsBinding |
| **bus** (advanced) | To use a custom configured CXF Bus. |  | Bus |
| **continuationTimeout** (advanced) | The timeout in milliseconds of the CXF continuation that the consumer uses to process the exchange asynchronously. If it expires before the route has completed, the consumer sets an ExchangeTimedOutException on the exchange and fails the request with this exception, which a JAX-RS ExceptionMapper can turn into a response. Use 0 for no timeout. Not used when synchronous is true or when the consumer gets no continuation from the transport. | 30000 | long |
| **cxfRsConfigurer** (advanced) | To use a custom org.apache.camel.component.cxf.jaxrs.CxfRsConfigurer to configure CXF in Java code. Its configure method receives the CXF factory bean before a client or the server is created, and configureClient receives each client that the producer creates. The consumer does not call configureServer. |  | CxfRsConfigurer |
| **defaultBus** (advanced) | Whether to set the Bus of the bus option as the CXF default bus by calling BusFactory.setDefaultBus. The endpoint makes this call when the bus option is set, so this option must be set before the bus option, which is the order in which an endpoint URI sets them. Without the bus option, this option has no effect, because the endpoint does not create a Bus. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **performInvocation** (advanced) | Whether to call the resource method, on an instance of the resource class or on a bean of serviceBeans, before the consumer runs the route. If true, the consumer does not serve resource classes that are interfaces. If the method throws an exception, the route does not run. If the method returns a value other than null, the route gets that value as the message body, without the Camel headers that the binding sets from the request. | false | boolean |
| **propagateContexts** (advanced) | Whether to set the JAX-RS contexts of the request as exchange properties, so that the route can use the JAX-RS API on them. The consumer sets the UriInfo, Request, HttpHeaders and SecurityContext of the request, each under the fully qualified name of its interface, for example jakarta.ws.rs.core.UriInfo. | false | boolean |
| **loggingFeatureEnabled** (logging) | Whether to add a LoggingFeature, which writes the requests and responses of the endpoint to the log. The LoggingFeature writes them with SLF4J at INFO level to loggers whose names start with org.apache.cxf.services. | false | boolean |
| **loggingSizeLimit** (logging) | The size limit at which CXF truncates the payload of a request or response in the log. Sets the limit of the LoggingFeature that the endpoint adds when loggingFeatureEnabled is true. Use -1 for no limit. | 49152 | int |

## Message Headers

The CXF-RS component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCxfOperationName** (common) Constant: [`OPERATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#OPERATION_NAME) | The name of the operation. |  | String |
| **CamelDestinationOverrideUrl** (common) Constant: [`DESTINATION_OVERRIDE_URL`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#DESTINATION_OVERRIDE_URL) | The address that the producer sends the request to, in place of the service address. With the cxf component, the HTTP transport of CXF uses it, and the Camel transport does not. |  | String |
| **CamelAuthentication** (common) Constant: [`AUTHENTICATION`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#AUTHENTICATION) | The authenticated user of the request, as a Subject. The consumer sets it from the SecurityContext of the CXF request message: the Subject of a LoginSecurityContext, or else a new Subject with the user Principal. |  | Subject |
| **CamelHttpMethod** (common) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#HTTP_METHOD) | The HTTP method of the request, for example GET. The consumer sets it to the method of the request. With the WebClient API, the producer sends its request with this method, and without an entity for GET. |  | String |
| **CamelHttpPath** (common) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#HTTP_PATH) | The path of the request below the service address, for example /customers/123. The consumer sets it to the path of the request below the service address. With the WebClient API, the producer appends it to the service address or to the address in the CamelDestinationOverrideUrl header, and fills template variables such as {id} in this path with the values of the CamelCxfRsVarValues header. |  | String |
| **Content-Type** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CONTENT_TYPE) | The Content-Type of the message body. The consumer sets it to the Content-Type of the request, and uses it as the Content-Type of the response when the message body of the reply is not a jakarta.ws.rs.core.Response. The consumer does not use this header for the response when synchronous is true or when it gets no continuation from the transport. The producer sends it as the Content-Type of its request. When synchronous is false, or when the producer reads the response as a Response, it copies the response headers to the reply, and a Content-Type of the response replaces this header. |  | String |
| **CamelHttpQuery** (common) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#HTTP_QUERY) | The query string of the request, without the question mark, for example id=1&name=a%20b. The consumer sets it when the request has a query string. With the WebClient API, the producer sends the parameters of this query string in place of the query parameters of the endpoint URI that are not options, unless the CamelCxfRsQueryMap header is set. |  | String |
| **CamelHttpResponseCode** (common) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#HTTP_RESPONSE_CODE) | The HTTP status code of the response. The producer sets it to the status code of the response, unless the exchange pattern is InOnly or the exchange fails, which with the default settings happens for a status code greater than 207. On the consumer, the route sets it to choose the status code of the response when the message body of the reply is not a jakarta.ws.rs.core.Response. If not set, the status code of the response is 200 for a successful reply, or 204 for a reply without a message body when bindingStyle is Default. |  | Integer |
| **Content-Encoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CONTENT_ENCODING) | The Content-Encoding of the message body, for example gzip. The consumer sets it to the Content-Encoding of the request, unless CXF has already decompressed the request, for example with a GZIPFeature. The producer sends it as the Content-Encoding of its request. When synchronous is false, or when the producer reads the response as a jakarta.ws.rs.core.Response, it copies the response headers to the reply, and a Content-Encoding of the response replaces this header, unless CXF has already decompressed the response. The consumer and the producer do not compress or decompress the message body because of this header. |  | String |
| **org.apache.cxf.message.Message.PROTOCOL\_HEADERS** (common) Constant: [`PROTOCOL_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#PROTOCOL_HEADERS) | The HTTP headers to add to the response of the consumer, as a Map from the header name to a List of values or to one value. The consumer adds them when the message body of the reply is not a jakarta.ws.rs.core.Response, and the Content-Type header replaces the Content-Type entry of the Map. The consumer ignores the entries of the Map when synchronous is true or when it gets no continuation from the transport. The consumer does not put the HTTP headers of the request into this Map: each HTTP header of the request that the header filter strategy keeps becomes a separate Camel header. |  | Map |
| **CamelCxfMessage** (common) Constant: [`CAMEL_CXF_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_MESSAGE) | The CXF request message, as an org.apache.cxf.message.Message. The consumer sets it for each request. With the WebClient API, the producer adds the matrix parameters in the request URI of this message to the end of the path of its own request. |  | Message |
| **CamelCxfRsUsingHttpAPI** (common) Constant: [`CAMEL_CXF_RS_USING_HTTP_API`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_USING_HTTP_API) | Whether to use the CXF WebClient API instead of the proxy-based API for this message. This header replaces the httpClientAPI option. |  | Boolean |
| **CamelCxfRsVarValues** (common) Constant: [`CAMEL_CXF_RS_VAR_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_VAR_VALUES) | The values of the template variables in the path of the request, as an Object\[\], in the order in which the variables appear. With the WebClient API, the producer fills the variables such as {id} in the CamelHttpPath header with them. With the proxy-based API, the producer passes them to CXF for the variables in the Path annotation of the first resource class, and a PathParam or BeanParam parameter of the resource method can take precedence for one of these variables. |  | Object\[\] |
| **CamelCxfRsResponseClass** (common) Constant: [`CAMEL_CXF_RS_RESPONSE_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_RESPONSE_CLASS) | The class to read the response entity as, for example String. The consumer sets it to the return type of the resource method. The producer uses it only with the WebClient API, where the message body of the reply is the jakarta.ws.rs.core.Response if this header is not set or is Response. |  | Class |
| **CamelCxfRsResponseGenericType** (common) Constant: [`CAMEL_CXF_RS_RESPONSE_GENERIC_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_RESPONSE_GENERIC_TYPE) | The generic type to read the response entity as, given as a java.lang.reflect.Type. The consumer sets it to the generic return type of the resource method. The producer uses it only with the WebClient API, and only when the CamelCxfRsResponseClass header is a class other than jakarta.ws.rs.core.Response. When synchronous is true, the producer uses it only for a Collection response class, and this header must then be a ParameterizedType whose first type argument is the class of the elements. |  | Type |
| **CamelCxfRsQueryMap** (common) Constant: [`CAMEL_CXF_RS_QUERY_MAP`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_QUERY_MAP) | The query parameters of the request, as a Map from the parameter name to the value. With the WebClient API, the producer sends them in place of the CamelHttpQuery header and of the query parameters of the endpoint URI that are not options, even when the Map is empty. |  | Map |
| **CamelCxfRsOperationResourceInfoStack** (common) Constant: [`CAMEL_CXF_RS_OPERATION_RESOURCE_INFO_STACK`](https://javadoc.io/doc/org.apache.camel/camel-cxf-rest/latest/org/apache/camel/component/cxf/common/message/CxfConstants.html#CAMEL_CXF_RS_OPERATION_RESOURCE_INFO_STACK) | The resource methods and sub-resource locators that CXF matched for the request, as a copy of the org.apache.cxf.jaxrs.model.OperationResourceInfoStack, which holds one MethodInvocationInfo for each of them, with the root resource at the bottom of the stack. The consumer sets it for each request. The producer does not use it. |  | OperationResourceInfoStack |

## Message Body

The message body at each side of the CXF-RS component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `list` (`org.apache.cxf.message.MessageContentsList`) | Default: a MessageContentsList of the parameters of the resource method, with its name in the CamelCxfOperationName header. SimpleConsumer: the request entity as the method declares it (a String, an InputStream, a JAXB bean), with the path, query and header parameters in headers; the MessageContentsList when the method has no entity, such as a GET.
-   With `bindingStyle=SimpleConsumer`: `unknown`
    
-   With `bindingStyle=Custom`: `unknown`
    

Not known when `performInvocation` is set.

 |
| **Consumer reply** | `null`, `text`, `bytes`, `stream`, `file` or `pojo` | 

The response entity: a jakarta.ws.rs.core.Response, or text, bytes, a stream, a file, or an object a JAX-RS provider writes for the Content-Type (a JAXB bean as XML); a Map or a List fails without a provider for it. With the Default binding an unchanged request MessageContentsList replies with its single element, or no content when empty (unless the method returns a collection); one of several parameters fails: set the reply body.

-   With `bindingStyle=Custom`: `any`
    





 |
| **Producer input** | `null`, `text`, `bytes`, `stream`, `file` or `pojo` | 

The request entity, written for the Content-Type header: text, bytes, a stream, a file or an object a JAX-RS provider writes, such as a List as a whole (of a MessageContentsList or an Object\[\] only the first element is sent); a Map fails. A GET sends no body. With httpClientAPI=false: the parameters of the resource method named by the CamelCxfOperationName header, as a List or the one parameter.

-   With `httpClientAPI=false`: `list`, `text`, `value`, `pojo` or `null`
    





 |
| **Producer output** | `pojo` | 

A jakarta.ws.rs.core.Response whose entity is the response stream, read once (it converts to a String or an InputStream); the entity read as the class in the CamelCxfRsResponseClass header when that is set. With httpClientAPI=false: the return value of the resource method, null for a void one.

-   With `httpClientAPI=false`: `unknown`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

You can also configure the CXF REST endpoint through the spring configuration.

> **Note**
> Since there are lots of differences between the CXF REST client and CXF REST Server, we provide different configuration for them.
>
> Please check the following files for more details:
>
> -   the [schema file](https://github.com/apache/camel/blob/main/components/camel-cxf/camel-cxf-spring-rest/src/main/resources/schema/cxfJaxrsEndpoint.xsd).
>     
> -   [CXF JAX-RS documentation](http://cxf.apache.org/docs/jax-rs.md).

## Examples

### How to configure the REST endpoint in Camel

In the [camel-cxf schema file](https://github.com/apache/camel/blob/main/components/camel-cxf/camel-cxf-spring-rest/src/main/resources/schema/cxfJaxrsEndpoint.xsd), there are two elements for the REST endpoint definition:

-   `cxf:rsServer` for REST consumer
    
-   `cxf:rsClient` for REST producer.
    

You can find a Camel REST service route configuration example there.

### How to override the CXF producer address from message header

The `camel-cxfrs` producer supports overriding the service address by setting the message with the key of `CamelDestinationOverrideUrl`.

_Java-only: inline exchange header manipulation_

```java
 // set up the service address from the message header to override the setting of CXF endpoint
 exchange.getIn().setHeader(Exchange.DESTINATION_OVERRIDE_URL, constant(getServiceAddress()));
```

### Consuming a REST Request - Simple Binding Style

**Since Camel 2.11**

The `Default` binding style is rather low-level, requiring the user to manually process the `MessageContentsList` object coming into the route. Thus, it tightly couples the route logic with the method signature and parameter indices of the JAX-RS operation. Somewhat inelegant, difficult and error-prone. When a route with the `Default` binding style does not set a reply body, the request `MessageContentsList` of one parameter is the response entity, and one without parameters replies with no content (204), unless the resource method returns a collection. A `MessageContentsList` of several parameters fails with HTTP 500, so set the reply body in the route.

In contrast, the `SimpleConsumer` binding style performs the following mappings, to **make the request data more accessible** to you within the Camel Message:

-   JAX-RS Parameters (`@HeaderParam`, `@QueryParam`, etc.) are injected as _IN_ message headers. The header name matches the value of the annotation.
    
-   The request entity (POJO or another type) becomes the _IN_ message body. If a single entity cannot be identified in the JAX-RS method signature, it falls back to the original `MessageContentsList`.
    
-   Binary `@Multipart` body parts become _IN_ message attachments, supporting `DataHandler`, `InputStream`, `DataSource` and CXF’s `Attachment` class.
    
-   Non-binary `@Multipart` body parts are mapped as _IN_ message headers. The header name matches the Body Part name.
    

Additionally, the following rules apply to the **Response mapping**:

-   If the message body type is different to `jakarta.ws.rs.core.Response` (user-built response), a new `Response` is created and the message body is set as the entity (so long it’s not null). The response status code is taken from the `Exchange.HTTP_RESPONSE_CODE` header, or defaults to 200 OK if not present.
    
-   If the message body type is equal to `jakarta.ws.rs.core.Response`, it means that the user has built a custom response, and therefore it is respected, and it becomes the final response.
    
-   In all cases, Camel headers permitted by custom or default `HeaderFilterStrategy` are added to the HTTP response.
    

### Enabling the Simple Binding Style

This binding style can be activated by setting the `bindingStyle` parameter in the consumer endpoint to value `SimpleConsumer`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("cxfrs:bean:rsServer?bindingStyle=SimpleConsumer")
    .to("log:TEST?showAll=true");
```

```xml
<route>
  <from uri="cxfrs:bean:rsServer?bindingStyle=SimpleConsumer"/>
  <to uri="log:TEST?showAll=true"/>
</route>
```

```yaml
- route:
    from:
      uri: "cxfrs:bean:rsServer?bindingStyle=SimpleConsumer"
      steps:
        - to:
            uri: "log:TEST?showAll=true"
```

### Examples of request binding with different method signatures

Below is a list of method signatures along with the expected result from the simple binding:

-   `public Response doAction(BusinessObject request);`: the request payload is placed in tbe _IN_ message body, replacing the original MessageContentsList.
    
-   `public Response doAction(BusinessObject request, @HeaderParam("abcd") String abcd, @QueryParam("defg") String defg);`: the request payload is placed in the _IN_ message body, replacing the original `MessageContentsList`. Both request parameters are mapped as IN message headers with names _"abcd"_ and _"defg"_.
    
-   `public Response doAction(@HeaderParam("abcd") String abcd, @QueryParam("defg") String defg);`: both request parameters are mapped as the _IN_ message headers with names _"abcd"_ and _"defg"_. The original `MessageContentsList` is preserved, even though it only contains the two parameters.
    
-   `public Response doAction(@Multipart(value="body1") BusinessObject request, @Multipart(value="body2") BusinessObject request2);`: the first parameter is transferred as a header with name _"body1"_, and the second one is mapped as header _"body2"_. The original `MessageContentsList` is preserved as the _IN_ message body.
    
-   `public Response doAction(InputStream abcd);`: the `InputStream` is unwrapped from the `MessageContentsList` and preserved as the _IN_ message body.
    
-   `public Response doAction(DataHandler abcd);`: the _DataHandler_ is unwrapped from the `MessageContentsList` and preserved as the _IN_ message body.
    

### More examples of the Simple Binding Style

Given a JAX-RS resource class with this method:

_Java-only: Java JAX-RS annotation_

```java
@POST @Path("/customers/{type}")
public Response newCustomer(Customer customer, @PathParam("type") String type, @QueryParam("active") @DefaultValue("true") boolean active) {
    return null;
}
```

Serviced by the following route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("cxfrs:bean:rsServer?bindingStyle=SimpleConsumer")
    .recipientList(simple("direct:${header.CamelCxfOperationName}"));

from("direct:newCustomer")
    .log("Request: type=${header.type}, active=${header.active}, customerData=${body}");
```

```xml
<route>
  <from uri="cxfrs:bean:rsServer?bindingStyle=SimpleConsumer"/>
  <recipientList>
    <simple>direct:${header.CamelCxfOperationName}</simple>
  </recipientList>
</route>
<route>
  <from uri="direct:newCustomer"/>
  <log message="Request: type=${header.type}, active=${header.active}, customerData=${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: "cxfrs:bean:rsServer?bindingStyle=SimpleConsumer"
      steps:
        - recipientList:
            simple: "direct:${header.CamelCxfOperationName}"
- route:
    from:
      uri: direct:newCustomer
      steps:
        - log:
            message: "Request: type=${header.type}, active=${header.active}, customerData=${body}"
```

The following HTTP request with XML payload (given that the Customer DTO is JAXB-annotated):

POST /customers/gold?active=true

Payload:
<Customer>
  <fullName>Raul Kripalani</fullName>
  <country>Spain</country>
  <project>Apache Camel</project>
</Customer>

Will print the message:

Request: type=gold, active=true, customerData=<Customer.toString() representation>

> **Note**
> More examples on how to process requests and write responses can be found [here](https://github.com/apache/camel/tree/main/components/camel-cxf/camel-cxf-rest/src/test/java/org/apache/camel/component/cxf/jaxrs/simplebinding).

### Consuming a REST Request - Default Binding Style

The [CXF JAXRS front end](http://cxf.apache.org/docs/jax-rs.md) implements the [JAX-RS (JSR-311) API](https://javaee.github.io/jsr311/), so we can export the resource classes as a REST service. And we leverage the [CXF Invoker API](http://cxf.apache.org/docs/invokers.md) to turn a REST request into a normal Java object method invocation. You don’t need to specify the URI template within your endpoint, CXF takes care of the REST request URI to resource class method mapping according to the JSR-311 specification. All you need to do in Camel is delegate this method request to the right processor or endpoint.

Here is an example of a CXFRS route…​

_Java-only: Java RouteBuilder with constants and Processors_

```java
private static final String CXF_RS_ENDPOINT_URI =
        "cxfrs://http://localhost:" + CXT + "/rest?resourceClasses=org.apache.camel.component.cxf.jaxrs.testbean.CustomerServiceResource";
private static final String CXF_RS_ENDPOINT_URI2 =
        "cxfrs://http://localhost:" + CXT + "/rest2?resourceClasses=org.apache.camel.component.cxf.jaxrs.testbean.CustomerService";
private static final String CXF_RS_ENDPOINT_URI3 =
        "cxfrs://http://localhost:" + CXT + "/rest3?"
        + "resourceClasses=org.apache.camel.component.cxf.jaxrs.testbean.CustomerServiceNoAnnotations&"
        + "modelRef=classpath:/org/apache/camel/component/cxf/jaxrs/CustomerServiceModel.xml";
private static final String CXF_RS_ENDPOINT_URI4 =
        "cxfrs://http://localhost:" + CXT + "/rest4?"
        + "modelRef=classpath:/org/apache/camel/component/cxf/jaxrs/CustomerServiceDefaultHandlerModel.xml";
private static final String CXF_RS_ENDPOINT_URI5 =
        "cxfrs://http://localhost:" + CXT + "/rest5?"
        + "propagateContexts=true&"
        + "modelRef=classpath:/org/apache/camel/component/cxf/jaxrs/CustomerServiceDefaultHandlerModel.xml";
protected RouteBuilder createRouteBuilder() throws Exception {
    final Processor testProcessor = new TestProcessor();
    final Processor testProcessor2 = new TestProcessor2();
    final Processor testProcessor3 = new TestProcessor3();
    return new RouteBuilder() {
        public void configure() {
            errorHandler(new NoErrorHandlerBuilder());
            from(CXF_RS_ENDPOINT_URI).process(testProcessor);
            from(CXF_RS_ENDPOINT_URI2).process(testProcessor);
            from(CXF_RS_ENDPOINT_URI3).process(testProcessor);
            from(CXF_RS_ENDPOINT_URI4).process(testProcessor2);
            from(CXF_RS_ENDPOINT_URI5).process(testProcessor3);
        }
    };
}
```

And the corresponding resource class used to configure the endpoint…​

> **Note**
> **Note about resource classes**
>
> By default, JAX-RS resource classes are **only** used to configure JAX-RS properties. Methods will **not** be executed during routing of messages to the endpoint. Instead, it is the responsibility of the route to do all processing.

It is sufficient to provide an interface only as opposed to a no-op service implementation class for the default mode.

If a **performInvocation** option is enabled, the service implementation will be invoked first, the response will be set on the Camel exchange, and the route execution will continue as usual. This can be useful for integrating the existing JAX-RS implementations into Camel routes and for post-processing JAX-RS Responses in custom processors.

_Java-only: Java JAX-RS interface definition_

```java
@Path("/customerservice/")
public interface CustomerServiceResource {

    @GET
    @Path("/customers/{id}/")
    Customer getCustomer(@PathParam("id") String id);

    @PUT
    @Path("/customers/")
    Response updateCustomer(Customer customer);

    @Path("/{id}")
    @PUT()
    @Consumes({ "application/xml", "text/plain",
                    "application/json" })
    @Produces({ "application/xml", "text/plain",
                    "application/json" })
    Object invoke(@PathParam("id") String id,
                    String payload);
}
```

### How to invoke the REST service through camel-cxfrs producer

The [CXF JAXRS front end](http://cxf.apache.org/docs/jax-rs.md) implements [a proxy-based client API](http://cxf.apache.org/docs/jax-rs-client-api.html#JAX-RSClientAPI-Proxy-basedAPI), with this API you can invoke the remote REST service through a proxy. The `camel-cxfrs` producer is based on this [proxy API](http://cxf.apache.org/docs/jax-rs-client-api.html#JAX-RSClientAPI-Proxy-basedAPI). You need to specify the operation name in the message header and prepare the parameter in the message body, the camel-cxfrs producer will generate the right REST request for you.

Here is an example:

_Java-only: Java test API (ProducerTemplate with inline Processor)_

```java
Exchange exchange = template.send("direct://proxy", ex -> {
    ex.setPattern(ExchangePattern.InOut);
    Message inMessage = ex.getIn();
    inMessage.setHeader("CamelCxfOperationName", "getCustomer");
    inMessage.setHeader("CamelCxfRsUsingHttpAPI", Boolean.FALSE);
    inMessage.setHeader("key", "value");
    inMessage.setHeader("Accept", "application/json");
    inMessage.setBody("123");
});

// get the response message
Customer response = (Customer) exchange.getMessage().getBody();

assertNotNull(response, "The response should not be null");
assertEquals(123, response.getId(), "Get a wrong customer id");
assertEquals("John", response.getName(), "Get a wrong customer name");
assertEquals(200, exchange.getMessage().getHeader(Exchange.HTTP_RESPONSE_CODE), "Get a wrong response code");
assertEquals("value", exchange.getMessage().getHeader("key"), "Get a wrong header value");
```

The [CXF JAXRS front end](http://cxf.apache.org/docs/jax-rs.md) also provides [an HTTP centric client API](http://cxf.apache.org/docs/jax-rs-client-api.html#JAX-RSClientAPI-CXFWebClientAPI). You can also invoke this API from `camel-cxfrs` producer. You need to specify the [HTTP\_PATH](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Exchange.html#HTTP_PATH) and the [HTTP\_METHOD](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Exchange.html#HTTP_METHOD) and let the producer use the http centric client API by using the URI option **httpClientAPI** or by setting the message header `CamelCxfRsUsingHttpAPI`. You can turn the response object to the type class specified with the message header `CamelCxfRsResponseClass`. The message body is the request entity (a GET sends none): a `List` or an array of primitives (such as `byte[]` or `int[]`) is sent as a whole, and of a `MessageContentsList` (such as the body from a `cxfrs` consumer with the `Default` binding style) or an `Object[]` only the first element is sent, as they carry the parameters of a method call.

_Java-only: Java test API (ProducerTemplate with inline Processor)_

```java
Exchange exchange = template.send("direct://http", ex -> {
    ex.setPattern(ExchangePattern.InOut);
    Message inMessage = ex.getIn();
    inMessage.setHeader("CamelCxfRsUsingHttpAPI", Boolean.TRUE);
    inMessage.setHeader(Exchange.HTTP_METHOD, "GET");
    inMessage.setHeader(Exchange.HTTP_PATH, "/customerservice/customers/123");
    inMessage.setHeader("CamelCxfRsResponseClass", Customer.class);
    inMessage.setHeader("key", "value");
    inMessage.setBody(null);
});
```

We also support to specify the query parameters from cxfrs URI for the CXFRS http centric client.

_Java-only: Java test API (ProducerTemplate)_

```java
Exchange exchange = template.send("cxfrs://http://localhost:9003/testQuery?httpClientAPI=true&q1=12&q2=13"
```

To support the Dynamical routing, you can override the URI’s query parameters by using the `CamelCxfRsQueryMap` header to set the parameter map for it.

_Java-only: Java collection API_

```java
Map<String, String> queryMap = new LinkedHashMap<>();
queryMap.put("q1", "new");
queryMap.put("q2", "world");
inMessage.setHeader("CamelCxfRsQueryMap", queryMap);
```