# FHIR

**Since Camel 2.23**

**Both producer and consumer are supported**

The FHIR component integrates with the [HAPI-FHIR](http://hapifhir.io/) library, which is an open-source implementation of the [FHIR](http://hl7.org/implement/standards/fhir/) (Fast Healthcare Interoperability Resources) specification in Java.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-fhir</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI Format

The FHIR Component uses the following URI format:

fhir://endpoint-prefix/endpoint?\[options\]

Endpoint prefix can be one of:

-   capabilities
    
-   create
    
-   delete
    
-   history
    
-   load-page
    
-   meta
    
-   operation
    
-   patch
    
-   read
    
-   search
    
-   transaction
    
-   update
    
-   validate
    

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

The FHIR component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **encoding** (common) | 
Encoding to use for all request.

Enum values:

-   JSON
    
-   XML
    





 |  | String |
| **fhirVersion** (common) | 

The FHIR Version to use.

Enum values:

-   DSTU2
    
-   DSTU2\_HL7ORG
    
-   DSTU2\_1
    
-   DSTU3
    
-   R4
    
-   R4B
    
-   R5
    





 | R4 | String |
| **log** (common) | Will log every requests and responses. | false | boolean |
| **prettyPrint** (common) | Pretty print all request. | false | boolean |
| **serverUrl** (common) | The FHIR server base URL. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | To use the custom client. |  | IGenericClient |
| **clientFactory** (advanced) | To use the custom client factory. |  | IRestfulClientFactory |
| **compress** (advanced) | Compresses outgoing (POST/PUT) contents to the GZIP format. | false | boolean |
| **configuration** (advanced) | To use the shared configuration. |  | FhirConfiguration |
| **connectionTimeout** (advanced) | How long to try and establish the initial TCP connection (in ms). | 10000 | Integer |
| **deferModelScanning** (advanced) | When this option is set, model classes will not be scanned for children until the child list for the given type is actually accessed. | false | boolean |
| **fhirContext** (advanced) | FhirContext is an expensive object to create. To avoid creating multiple instances, it can be set directly. |  | FhirContext |
| **forceConformanceCheck** (advanced) | Force conformance check. | false | boolean |
| **sessionCookie** (advanced) | HTTP session cookie to add to every request. |  | String |
| **socketTimeout** (advanced) | How long to block for individual read/write operations (in ms). | 10000 | Integer |
| **summary** (advanced) | 

Request that the server modify the response using the \_summary param.

Enum values:

-   COUNT
    
-   TEXT
    
-   DATA
    
-   TRUE
    
-   FALSE
    





 |  | String |
| **validationMode** (advanced) | 

When should Camel validate the FHIR Server’s conformance statement.

Enum values:

-   NEVER
    
-   ONCE
    





 | ONCE | String |
| **proxyHost** (proxy) | The proxy host. |  | String |
| **proxyPassword** (proxy) | The proxy password. |  | String |
| **proxyPort** (proxy) | The proxy port. |  | Integer |
| **proxyUser** (proxy) | The proxy username. |  | String |
| **accessToken** (security) | OAuth access token. |  | String |
| **password** (security) | Password to use for basic authentication. |  | String |
| **username** (security) | Username to use for basic authentication. |  | String |

## Endpoint Options

The FHIR endpoint is configured using URI syntax:

fhir:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   CAPABILITIES
    
-   CREATE
    
-   DELETE
    
-   HISTORY
    
-   LOAD\_PAGE
    
-   META
    
-   OPERATION
    
-   PATCH
    
-   READ
    
-   SEARCH
    
-   TRANSACTION
    
-   UPDATE
    
-   VALIDATE
    





 |  | FhirApiName |
| **methodName** (common) | **Required** What sub operation to use for the selected operation. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **encoding** (common) | 
Encoding to use for all request.

Enum values:

-   JSON
    
-   XML
    





 |  | String |
| **fhirVersion** (common) | 

The FHIR Version to use.

Enum values:

-   DSTU2
    
-   DSTU2\_HL7ORG
    
-   DSTU2\_1
    
-   DSTU3
    
-   R4
    
-   R4B
    
-   R5
    





 | R4 | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **log** (common) | Will log every requests and responses. | false | boolean |
| **prettyPrint** (common) | Pretty print all request. | false | boolean |
| **serverUrl** (common) | The FHIR server base URL. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | To use the custom client. |  | IGenericClient |
| **clientFactory** (advanced) | To use the custom client factory. |  | IRestfulClientFactory |
| **compress** (advanced) | Compresses outgoing (POST/PUT) contents to the GZIP format. | false | boolean |
| **connectionTimeout** (advanced) | How long to try and establish the initial TCP connection (in ms). | 10000 | Integer |
| **deferModelScanning** (advanced) | When this option is set, model classes will not be scanned for children until the child list for the given type is actually accessed. | false | boolean |
| **fhirContext** (advanced) | FhirContext is an expensive object to create. To avoid creating multiple instances, it can be set directly. |  | FhirContext |
| **forceConformanceCheck** (advanced) | Force conformance check. | false | boolean |
| **sessionCookie** (advanced) | HTTP session cookie to add to every request. |  | String |
| **socketTimeout** (advanced) | How long to block for individual read/write operations (in ms). | 10000 | Integer |
| **summary** (advanced) | 

Request that the server modify the response using the \_summary param.

Enum values:

-   COUNT
    
-   TEXT
    
-   DATA
    
-   TRUE
    
-   FALSE
    





 |  | String |
| **validationMode** (advanced) | 

When should Camel validate the FHIR Server’s conformance statement.

Enum values:

-   NEVER
    
-   ONCE
    





 | ONCE | String |
| **proxyHost** (proxy) | The proxy host. |  | String |
| **proxyPassword** (proxy) | The proxy password. |  | String |
| **proxyPort** (proxy) | The proxy port. |  | Integer |
| **proxyUser** (proxy) | The proxy username. |  | String |
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
| **accessToken** (security) | OAuth access token. |  | String |
| **password** (security) | Password to use for basic authentication. |  | String |
| **username** (security) | Username to use for basic authentication. |  | String |

## API Parameters (13 APIs)

The FHIR endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

fhir:apiName/methodName

There are 13 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**capabilities**](#_api_capabilities) | Both | API to Fetch the capability statement for the server |
| [**create**](#_api_create) | Both | API for the create operation, which creates a new resource instance on the server |
| [**delete**](#_api_delete) | Both | API for the delete operation, which performs a logical delete on a server resource |
| [**history**](#_api_history) | Both | API for the history method |
| [**load-page**](#_api_load-page) | Both | API that Loads the previous/next bundle of resources from a paged set, using the link specified in the link type=next tag within the atom bundle |
| [**meta**](#_api_meta) | Both | API for the meta operations, which can be used to get, add and remove tags and other Meta elements from a resource or across the server |
| [**operation**](#_api_operation) | Both | API for extended FHIR operations |
| [**patch**](#_api_patch) | Both | API for the patch operation, which performs a logical patch on a server resource |
| [**read**](#_api_read) | Both | API method for read operations |
| [**search**](#_api_search) | Both | API to search for resources matching a given set of criteria |
| [**transaction**](#_api_transaction) | Both | API for sending a transaction (collection of resources) to the server to be executed as a single unit |
| [**update**](#_api_update) | Both | API for the update operation, which performs a logical delete on a server resource |
| [**validate**](#_api_validate) | Both | API for validating resources |

Each API is documented in the following sections to come.

### API: capabilities

**Both producer and consumer are supported**

The capabilities API is defined in the syntax as follows:

```none
fhir:capabilities/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**ofType**](#_api_capabilities_method_ofType) |  | Retrieve the conformance statement using the given model type |

#### Method ofType

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseConformance ofType(Class<org.hl7.fhir.instance.model.api.IBaseConformance> type, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/ofType API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **type** | The model type | Class |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: create

**Both producer and consumer are supported**

The create API is defined in the syntax as follows:

```none
fhir:create/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_create_method_resource) |  | Creates a IBaseResource on the server |

#### Method resource

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resource(String resourceAsString, String url, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resource(org.hl7.fhir.instance.model.api.IBaseResource resource, String url, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **preferReturn** | Add a Prefer header to the request, which requests that the server include or suppress the resource body as a part of the result. If a resource is returned by the server it will be parsed an accessible to the client via MethodOutcome#getResource() , may be null | PreferReturnEnum |
| **resource** | The resource to create | IBaseResource |
| **resourceAsString** | The resource to create | String |
| **url** | The search URL to use. The format of this URL should be of the form ResourceTypeParameters, for example: Patientname=Smith&identifier=13.2.4.11.4%7C847366, may be null | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: delete

**Both producer and consumer are supported**

The delete API is defined in the syntax as follows:

```none
fhir:delete/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_delete_method_resource) |  | Deletes the given resource |
| [**resourceById**](#_api_delete_method_resourceById) |  | Deletes the resource by resource type e |
| [**resourceConditionalByUrl**](#_api_delete_method_resourceConditionalByUrl) |  | Specifies deleting should be performed as a conditional delete against a given search URL |

#### Method resource

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resource(org.hl7.fhir.instance.model.api.IBaseResource resource, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **resource** | The IBaseResource to delete | IBaseResource |

#### Method resourceById

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resourceById(String type, String stringId, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resourceById(org.hl7.fhir.instance.model.api.IIdType id, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resourceById API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The IIdType referencing the resource | IIdType |
| **stringId** | It’s id | String |
| **type** | The resource type e.g Patient | String |

#### Method resourceConditionalByUrl

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resourceConditionalByUrl(String url, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resourceConditionalByUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **url** | The search URL to use. The format of this URL should be of the form ResourceTypeParameters, for example: Patientname=Smith&identifier=13.2.4.11.4%7C847366 | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: history

**Both producer and consumer are supported**

The history API is defined in the syntax as follows:

```none
fhir:history/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**onInstance**](#_api_history_method_onInstance) |  | Perform the operation across all versions of a specific resource (by ID and type) on the server |
| [**onServer**](#_api_history_method_onServer) |  | Perform the operation across all versions of all resources of all types on the server |
| [**onType**](#_api_history_method_onType) |  | Perform the operation across all versions of all resources of the given type on the server |

#### Method onInstance

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle onInstance(org.hl7.fhir.instance.model.api.IIdType id, Class<org.hl7.fhir.instance.model.api.IBaseBundle> returnType, Integer count, java.util.Date cutoff, org.hl7.fhir.instance.model.api.IPrimitiveType<java.util.Date> iCutoff, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onInstance API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **count** | Request that the server return only up to theCount number of resources, may be NULL | Integer |
| **cutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | Date |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **iCutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | IPrimitiveType |
| **id** | The IIdType which must be populated with both a resource type and a resource ID at | IIdType |
| **returnType** | Request that the method return a Bundle resource (such as ca.uhn.fhir.model.dstu2.resource.Bundle). Use this method if you are accessing a DSTU2 server. | Class |

#### Method onServer

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle onServer(Class<org.hl7.fhir.instance.model.api.IBaseBundle> returnType, Integer count, java.util.Date cutoff, org.hl7.fhir.instance.model.api.IPrimitiveType<java.util.Date> iCutoff, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onServer API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **count** | Request that the server return only up to theCount number of resources, may be NULL | Integer |
| **cutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | Date |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **iCutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | IPrimitiveType |
| **returnType** | Request that the method return a Bundle resource (such as ca.uhn.fhir.model.dstu2.resource.Bundle). Use this method if you are accessing a DSTU2 server. | Class |

#### Method onType

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle onType(Class<org.hl7.fhir.instance.model.api.IBaseResource> resourceType, Class<org.hl7.fhir.instance.model.api.IBaseBundle> returnType, Integer count, java.util.Date cutoff, org.hl7.fhir.instance.model.api.IPrimitiveType<java.util.Date> iCutoff, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onType API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **count** | Request that the server return only up to theCount number of resources, may be NULL | Integer |
| **cutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | Date |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **iCutoff** | Request that the server return only resource versions that were created at or after the given time (inclusive), may be NULL | IPrimitiveType |
| **resourceType** | The resource type to search for | Class |
| **returnType** | Request that the method return a Bundle resource (such as ca.uhn.fhir.model.dstu2.resource.Bundle). Use this method if you are accessing a DSTU2 server. | Class |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: load-page

**Both producer and consumer are supported**

The load-page API is defined in the syntax as follows:

```none
fhir:load-page/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**byUrl**](#_api_load-page_method_byUrl) |  | Load a page of results using the given URL and bundle type and return a DSTU1 Atom bundle |
| [**next**](#_api_load-page_method_next) |  | Load the next page of results using the link with relation next in the bundle |
| [**previous**](#_api_load-page_method_previous) |  | Load the previous page of results using the link with relation prev in the bundle |

#### Method byUrl

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle byUrl(String url, Class<org.hl7.fhir.instance.model.api.IBaseBundle> returnType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/byUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **returnType** | The return type | Class |
| **url** | The search url | String |

#### Method next

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle next(org.hl7.fhir.instance.model.api.IBaseBundle bundle, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/next API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **bundle** | The IBaseBundle | IBaseBundle |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |

#### Method previous

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle previous(org.hl7.fhir.instance.model.api.IBaseBundle bundle, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/previous API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **bundle** | The IBaseBundle | IBaseBundle |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: meta

**Both producer and consumer are supported**

The meta API is defined in the syntax as follows:

```none
fhir:meta/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**add**](#_api_meta_method_add) |  | Add the elements in the given metadata to the already existing set (do not remove any) |
| [**delete**](#_api_meta_method_delete) |  | Delete the elements in the given metadata from the given id |
| [**getFromResource**](#_api_meta_method_getFromResource) |  | Fetch the current metadata from a specific resource |
| [**getFromServer**](#_api_meta_method_getFromServer) |  | Fetch the current metadata from the whole Server |
| [**getFromType**](#_api_meta_method_getFromType) |  | Fetch the current metadata from a specific type |

#### Method add

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseMetaType add(org.hl7.fhir.instance.model.api.IBaseMetaType meta, org.hl7.fhir.instance.model.api.IIdType id, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/add API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The id | IIdType |
| **meta** | The IBaseMetaType class | IBaseMetaType |

#### Method delete

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseMetaType delete(org.hl7.fhir.instance.model.api.IBaseMetaType meta, org.hl7.fhir.instance.model.api.IIdType id, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The id | IIdType |
| **meta** | The IBaseMetaType class | IBaseMetaType |

#### Method getFromResource

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseMetaType getFromResource(Class<org.hl7.fhir.instance.model.api.IBaseMetaType> metaType, org.hl7.fhir.instance.model.api.IIdType id, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/getFromResource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The id | IIdType |
| **metaType** | The IBaseMetaType class | Class |

#### Method getFromServer

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseMetaType getFromServer(Class<org.hl7.fhir.instance.model.api.IBaseMetaType> metaType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/getFromServer API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **metaType** | The type of the meta datatype for the given FHIR model version (should be MetaDt.class or MetaType.class) | Class |

#### Method getFromType

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseMetaType getFromType(Class<org.hl7.fhir.instance.model.api.IBaseMetaType> metaType, String resourceType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/getFromType API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **metaType** | The IBaseMetaType class | Class |
| **resourceType** | The resource type e.g Patient | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: operation

**Both producer and consumer are supported**

The operation API is defined in the syntax as follows:

```none
fhir:operation/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**onInstance**](#_api_operation_method_onInstance) |  | Perform the operation across all versions of a specific resource (by ID and type) on the server |
| [**onInstanceVersion**](#_api_operation_method_onInstanceVersion) |  | This operation operates on a specific version of a resource |
| [**onServer**](#_api_operation_method_onServer) |  | Perform the operation across all versions of all resources of all types on the server |
| [**onType**](#_api_operation_method_onType) |  | Perform the operation across all versions of all resources of the given type on the server |
| [**processMessage**](#_api_operation_method_processMessage) |  | This operation is called $process-message as defined by the FHIR specification |

#### Method onInstance

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource onInstance(org.hl7.fhir.instance.model.api.IIdType id, String name, org.hl7.fhir.instance.model.api.IBaseParameters parameters, Class<org.hl7.fhir.instance.model.api.IBaseParameters> outputParameterType, boolean useHttpGet, Class<org.hl7.fhir.instance.model.api.IBaseResource> returnType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onInstance API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | Resource (version will be stripped) | IIdType |
| **name** | Operation name | String |
| **outputParameterType** | The type to use for the output parameters (this should be set to Parameters.class drawn from the version of the FHIR structures you are using), may be NULL | Class |
| **parameters** | The parameters to use as input. May also be null if the operation does not require any input parameters. | IBaseParameters |
| **returnType** | If this operation returns a single resource body as its return type instead of a Parameters resource, use this method to specify that resource type. This is useful for certain operations (e.g. Patient/NNN/$everything) which return a bundle instead of a Parameters resource, may be NULL | Class |
| **useHttpGet** | Use HTTP GET verb | Boolean |

#### Method onInstanceVersion

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource onInstanceVersion(org.hl7.fhir.instance.model.api.IIdType id, String name, org.hl7.fhir.instance.model.api.IBaseParameters parameters, Class<org.hl7.fhir.instance.model.api.IBaseParameters> outputParameterType, boolean useHttpGet, Class<org.hl7.fhir.instance.model.api.IBaseResource> returnType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onInstanceVersion API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | Resource version | IIdType |
| **name** | Operation name | String |
| **outputParameterType** | The type to use for the output parameters (this should be set to Parameters.class drawn from the version of the FHIR structures you are using), may be NULL | Class |
| **parameters** | The parameters to use as input. May also be null if the operation does not require any input parameters. | IBaseParameters |
| **returnType** | If this operation returns a single resource body as its return type instead of a Parameters resource, use this method to specify that resource type. This is useful for certain operations (e.g. Patient/NNN/$everything) which return a bundle instead of a Parameters resource, may be NULL | Class |
| **useHttpGet** | Use HTTP GET verb | Boolean |

#### Method onServer

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource onServer(String name, org.hl7.fhir.instance.model.api.IBaseParameters parameters, Class<org.hl7.fhir.instance.model.api.IBaseParameters> outputParameterType, boolean useHttpGet, Class<org.hl7.fhir.instance.model.api.IBaseResource> returnType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onServer API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **name** | Operation name | String |
| **outputParameterType** | The type to use for the output parameters (this should be set to Parameters.class drawn from the version of the FHIR structures you are using), may be NULL | Class |
| **parameters** | The parameters to use as input. May also be null if the operation does not require any input parameters. | IBaseParameters |
| **returnType** | If this operation returns a single resource body as its return type instead of a Parameters resource, use this method to specify that resource type. This is useful for certain operations (e.g. Patient/NNN/$everything) which return a bundle instead of a Parameters resource, may be NULL | Class |
| **useHttpGet** | Use HTTP GET verb | Boolean |

#### Method onType

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource onType(Class<org.hl7.fhir.instance.model.api.IBaseResource> resourceType, String name, org.hl7.fhir.instance.model.api.IBaseParameters parameters, Class<org.hl7.fhir.instance.model.api.IBaseParameters> outputParameterType, boolean useHttpGet, Class<org.hl7.fhir.instance.model.api.IBaseResource> returnType, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/onType API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **name** | Operation name | String |
| **outputParameterType** | The type to use for the output parameters (this should be set to Parameters.class drawn from the version of the FHIR structures you are using), may be NULL | Class |
| **parameters** | The parameters to use as input. May also be null if the operation does not require any input parameters. | IBaseParameters |
| **resourceType** | The resource type to operate on | Class |
| **returnType** | If this operation returns a single resource body as its return type instead of a Parameters resource, use this method to specify that resource type. This is useful for certain operations (e.g. Patient/NNN/$everything) which return a bundle instead of a Parameters resource, may be NULL | Class |
| **useHttpGet** | Use HTTP GET verb | Boolean |

#### Method processMessage

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle processMessage(String respondToUri, org.hl7.fhir.instance.model.api.IBaseBundle msgBundle, boolean asynchronous, Class<org.hl7.fhir.instance.model.api.IBaseBundle> responseClass, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/processMessage API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **asynchronous** | Whether to process the message asynchronously or synchronously, defaults to synchronous. | Boolean |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **msgBundle** | Set the Message Bundle to POST to the messaging server | IBaseBundle |
| **respondToUri** | An optional query parameter indicating that responses from the receiving server should be sent to this URI, may be NULL | String |
| **responseClass** | The response class | Class |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: patch

**Both producer and consumer are supported**

The patch API is defined in the syntax as follows:

```none
fhir:patch/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**patchById**](#_api_patch_method_patchById) |  | Applies the patch to the given resource ID |
| [**patchByUrl**](#_api_patch_method_patchByUrl) |  | Specifies that the update should be performed as a conditional create against a given search URL |

#### Method patchById

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome patchById(String patchBody, String stringId, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome patchById(String patchBody, org.hl7.fhir.instance.model.api.IIdType id, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/patchById API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The resource ID to patch | IIdType |
| **patchBody** | The body of the patch document serialized in either XML or JSON which conforms to [http://jsonpatch.com/](http://jsonpatch.com/) or [http://tools.ietf.org/html/rfc5261](http://tools.ietf.org/html/rfc5261) | String |
| **preferReturn** | Add a Prefer header to the request, which requests that the server include or suppress the resource body as a part of the result. If a resource is returned by the server it will be parsed an accessible to the client via MethodOutcome#getResource() | PreferReturnEnum |
| **stringId** | The resource ID to patch | String |

#### Method patchByUrl

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome patchByUrl(String patchBody, String url, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/patchByUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **patchBody** | The body of the patch document serialized in either XML or JSON which conforms to [http://jsonpatch.com/](http://jsonpatch.com/) or [http://tools.ietf.org/html/rfc5261](http://tools.ietf.org/html/rfc5261) | String |
| **preferReturn** | Add a Prefer header to the request, which requests that the server include or suppress the resource body as a part of the result. If a resource is returned by the server it will be parsed an accessible to the client via MethodOutcome#getResource() | PreferReturnEnum |
| **url** | The search URL to use. The format of this URL should be of the form ResourceTypeParameters, for example: Patientname=Smith&identifier=13.2.4.11.4%7C847366 | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: read

**Both producer and consumer are supported**

The read API is defined in the syntax as follows:

```none
fhir:read/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resourceById**](#_api_read_method_resourceById) |  | Reads a IBaseResource on the server by id |
| [**resourceByUrl**](#_api_read_method_resourceByUrl) |  | Reads a IBaseResource on the server by url |

#### Method resourceById

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(Class<org.hl7.fhir.instance.model.api.IBaseResource> resource, Long longId, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(Class<org.hl7.fhir.instance.model.api.IBaseResource> resource, String stringId, String version, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(Class<org.hl7.fhir.instance.model.api.IBaseResource> resource, org.hl7.fhir.instance.model.api.IIdType id, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(String resourceClass, Long longId, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(String resourceClass, String stringId, String ifVersionMatches, String version, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceById(String resourceClass, org.hl7.fhir.instance.model.api.IIdType id, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resourceById API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The IIdType referencing the resource | IIdType |
| **ifVersionMatches** | A version to match against the newest version on the server | String |
| **longId** | The resource ID | Long |
| **resource** | The resource to read (e.g. Patient) | Class |
| **resourceClass** | The resource to read (e.g. Patient) | String |
| **returnNull** | Return null if version matches | Boolean |
| **returnResource** | Return the resource if version matches | IBaseResource |
| **stringId** | The resource ID | String |
| **throwError** | Throw error if the version matches | Boolean |
| **version** | The resource version | String |

#### Method resourceByUrl

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseResource resourceByUrl(Class<org.hl7.fhir.instance.model.api.IBaseResource> resource, String url, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceByUrl(Class<org.hl7.fhir.instance.model.api.IBaseResource> resource, org.hl7.fhir.instance.model.api.IIdType iUrl, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceByUrl(String resourceClass, String url, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseResource resourceByUrl(String resourceClass, org.hl7.fhir.instance.model.api.IIdType iUrl, String ifVersionMatches, Boolean returnNull, org.hl7.fhir.instance.model.api.IBaseResource returnResource, Boolean throwError, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resourceByUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **iUrl** | The IIdType referencing the resource by absolute url | IIdType |
| **ifVersionMatches** | A version to match against the newest version on the server | String |
| **resource** | The resource to read (e.g. Patient) | Class |
| **resourceClass** | The resource to read (e.g. Patient.class) | String |
| **returnNull** | Return null if version matches | Boolean |
| **returnResource** | Return the resource if version matches | IBaseResource |
| **throwError** | Throw error if the version matches | Boolean |
| **url** | Referencing the resource by absolute url | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: search

**Both producer and consumer are supported**

The search API is defined in the syntax as follows:

```none
fhir:search/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**searchByResource**](#_api_search_method_searchByResource) |  | Perform a search by resource name |
| [**searchByUrl**](#_api_search_method_searchByUrl) |  | Perform a search directly by URL |

#### Method searchByResource

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle searchByResource(String resourceName, java.util.Map<String, java.util.List<String>> searchParameters, ca.uhn.fhir.rest.api.SearchStyleEnum searchStyle, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/searchByResource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **resourceName** | The resource to search for | String |
| **searchParameters** | A set of search parameters to the query | Map |
| **searchStyle** | Forces the query to perform the search using the given method (allowable methods are described in the FHIR Search Specification). The default search style is HTTP POST. | SearchStyleEnum |

#### Method searchByUrl

Signatures:

-   org.hl7.fhir.instance.model.api.IBaseBundle searchByUrl(String url, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/searchByUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **url** | The URL to search for. Note that this URL may be complete (e.g. [http://example.com/base/Patientname=foo](http://example.com/base/Patientname=foo)) in which case the client’s base URL will be ignored. Or it can be relative (e.g. Patientname=foo) in which case the client’s base URL will be used. | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: transaction

**Both producer and consumer are supported**

The transaction API is defined in the syntax as follows:

```none
fhir:transaction/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**withBundle**](#_api_transaction_method_withBundle) |  | Use the given raw text (should be a Bundle resource) as the transaction input |
| [**withResources**](#_api_transaction_method_withResources) |  | Use a list of resources as the transaction input |

#### Method withBundle

Signatures:

-   String withBundle(String stringBundle, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   org.hl7.fhir.instance.model.api.IBaseBundle withBundle(org.hl7.fhir.instance.model.api.IBaseBundle bundle, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/withBundle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **bundle** | Bundle to use in the transaction | IBaseBundle |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **stringBundle** | Bundle to use in the transaction | String |

#### Method withResources

Signatures:

-   java.util.List<org.hl7.fhir.instance.model.api.IBaseResource> withResources(java.util.List<org.hl7.fhir.instance.model.api.IBaseResource> resources, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/withResources API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **resources** | Resources to use in the transaction | List |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: update

**Both producer and consumer are supported**

The update API is defined in the syntax as follows:

```none
fhir:update/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_update_method_resource) |  | Updates a IBaseResource on the server by id |
| [**resourceBySearchUrl**](#_api_update_method_resourceBySearchUrl) |  | Updates a IBaseResource on the server by search url |

#### Method resource

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resource(String resourceAsString, String stringId, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resource(String resourceAsString, org.hl7.fhir.instance.model.api.IIdType id, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resource(org.hl7.fhir.instance.model.api.IBaseResource resource, String stringId, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resource(org.hl7.fhir.instance.model.api.IBaseResource resource, org.hl7.fhir.instance.model.api.IIdType id, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **id** | The IIdType referencing the resource | IIdType |
| **preferReturn** | Whether the server include or suppress the resource body as a part of the result | PreferReturnEnum |
| **resource** | The resource to update (e.g. Patient) | IBaseResource |
| **resourceAsString** | The resource body to update | String |
| **stringId** | The ID referencing the resource | String |

#### Method resourceBySearchUrl

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resourceBySearchUrl(String resourceAsString, String url, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resourceBySearchUrl(org.hl7.fhir.instance.model.api.IBaseResource resource, String url, ca.uhn.fhir.rest.api.PreferReturnEnum preferReturn, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resourceBySearchUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **preferReturn** | Whether the server include or suppress the resource body as a part of the result | PreferReturnEnum |
| **resource** | The resource to update (e.g. Patient) | IBaseResource |
| **resourceAsString** | The resource body to update | String |
| **url** | Specifies that the update should be performed as a conditional create against a given search URL | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

### API: validate

**Both producer and consumer are supported**

The validate API is defined in the syntax as follows:

```none
fhir:validate/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_validate_method_resource) |  | Validates the resource |

#### Method resource

Signatures:

-   ca.uhn.fhir.rest.api.MethodOutcome resource(String resourceAsString, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    
-   ca.uhn.fhir.rest.api.MethodOutcome resource(org.hl7.fhir.instance.model.api.IBaseResource resource, java.util.Map<org.apache.camel.component.fhir.api.ExtraParameters, Object> extraParameters);
    

The fhir/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **extraParameters** | See ExtraParameters for a full list of parameters that can be passed, may be NULL | Map |
| **resource** | The IBaseResource to validate | IBaseResource |
| **resourceAsString** | Raw resource to validate | String |

In addition to the parameters above, the fhir API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelFhir.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelFhir.myParameterNameHere` header.

> **Note**
> This is an API-based component, so per-call parameters can be supplied through `Camel`\-prefixed exchange headers in addition to the endpoint options. If the route consumes messages from untrusted producers, strip these internal headers at the trust boundary — for example with `removeHeaders("Camel*")` — before the message reaches this component, so that a sender cannot override the API call. See [the Camel security model](../../manual/security-model.md) for details.