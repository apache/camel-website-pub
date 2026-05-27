# DHIS2

**Since Camel 4.0**

**Both producer and consumer are supported**

The Camel DHIS2 component leverages the [DHIS2 Java SDK](https://github.com/dhis2/dhis2-java-sdk) to integrate Apache Camel with [DHIS2](https://dhis2.org/). DHIS2 is a free, open-source, fully customizable platform for collecting, analyzing, visualizing, and sharing aggregate and individual-data for district-level, national, regional, and international system and program management in health, education, and other domains.

Maven users will need to add the following dependency to their `pom.xml`.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-dhis2</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

dhis2://operation/method\[?options\]

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

The DHIS2 component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseApiUrl** (common) | DHIS2 server base API URL (e.g., [https://play.dhis2.org/2.39.1.1/api](https://play.dhis2.org/2.39.1.1/api)). |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | References a user-defined org.hisp.dhis.integration.sdk.api.Dhis2Client. This option is mutually exclusive to the baseApiUrl, username, password, and personalAccessToken options. |  | Dhis2Client |
| **configuration** (advanced) | To use the shared configuration. |  | Dhis2Configuration |
| **password** (security) | Password of the DHIS2 username. |  | String |
| **personalAccessToken** (security) | Personal access token to authenticate with DHIS2. This option is mutually exclusive to username and password. |  | String |
| **username** (security) | Username of the DHIS2 user to operate as. |  | String |

## Endpoint Options

The DHIS2 endpoint is configured using URI syntax:

dhis2:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** API operation (e.g., get).

Enum values:

-   POST
    
-   RESOURCE\_TABLES
    
-   GET
    
-   DELETE
    
-   PUT
    





 |  | Dhis2ApiName |
| **methodName** (common) | **Required** Subject of the API operation (e.g., resource). |  | String |

### Query Parameters (26 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseApiUrl** (common) | DHIS2 server base API URL (e.g., [https://play.dhis2.org/2.39.1.1/api](https://play.dhis2.org/2.39.1.1/api)). |  | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
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
| **client** (advanced) | References a user-defined org.hisp.dhis.integration.sdk.api.Dhis2Client. This option is mutually exclusive to the baseApiUrl, username, password, and personalAccessToken options. |  | Dhis2Client |
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
| **password** (security) | Password of the DHIS2 username. |  | String |
| **personalAccessToken** (security) | Personal access token to authenticate with DHIS2. This option is mutually exclusive to username and password. |  | String |
| **username** (security) | Username of the DHIS2 user to operate as. |  | String |

## API Parameters (5 APIs)

The DHIS2 endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

dhis2:apiName/methodName

There are 5 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**delete**](#_api_delete) | Both | 
 |
| [**get**](#_api_get) | Both | 

 |
| [**post**](#_api_post) | Both | 

 |
| [**put**](#_api_put) | Both | 

 |
| [**resourceTables**](#_api_resourceTables) | Both | 

 |

Each API is documented in the following sections to come.

### API: delete

**Both producer and consumer are supported**

The delete API is defined in the syntax as follows:

```none
dhis2:delete/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_delete_method_resource) |  | 
 |

#### Method resource

Signatures:

-   java.io.InputStream resource(String path, Object resource, java.util.Map<String, Object> queryParams);
    

The dhis2/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **path** | 
 | String |
| **queryParams** | 

 | Map |
| **resource** | 

 | Object |

In addition to the parameters above, the dhis2 API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelDhis2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelDhis2.myParameterNameHere` header.

### API: get

**Both producer and consumer are supported**

The get API is defined in the syntax as follows:

```none
dhis2:get/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**collection**](#_api_get_method_collection) |  | 
 |
| [**resource**](#_api_get_method_resource) |  | 

 |

#### Method collection

Signatures:

-   java.util.Iterator<org.apache.camel.component.dhis2.api.Dhis2Resource> collection(String path, String arrayName, Boolean paging, String fields, java.util.List<String> filter, org.apache.camel.component.dhis2.api.RootJunctionEnum rootJunction, java.util.Map<String, Object> queryParams);
    

The dhis2/collection API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **arrayName** | 
 | String |
| **fields** | 

 | String |
| **filter** | 

 | List |
| **paging** | 

 | Boolean |
| **path** | 

 | String |
| **queryParams** | 

 | Map |
| **rootJunction** | 

 | RootJunctionEnum |

#### Method resource

Signatures:

-   java.io.InputStream resource(String path, String fields, java.util.List<String> filter, org.apache.camel.component.dhis2.api.RootJunctionEnum rootJunction, java.util.Map<String, Object> queryParams);
    

The dhis2/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fields** | 
 | String |
| **filter** | 

 | List |
| **path** | 

 | String |
| **queryParams** | 

 | Map |
| **rootJunction** | 

 | RootJunctionEnum |

In addition to the parameters above, the dhis2 API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelDhis2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelDhis2.myParameterNameHere` header.

### API: post

**Both producer and consumer are supported**

The post API is defined in the syntax as follows:

```none
dhis2:post/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_post_method_resource) |  | 
 |

#### Method resource

Signatures:

-   java.io.InputStream resource(String path, Object resource, java.util.Map<String, Object> queryParams);
    

The dhis2/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **path** | 
 | String |
| **queryParams** | 

 | Map |
| **resource** | 

 | Object |

In addition to the parameters above, the dhis2 API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelDhis2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelDhis2.myParameterNameHere` header.

### API: put

**Both producer and consumer are supported**

The put API is defined in the syntax as follows:

```none
dhis2:put/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**resource**](#_api_put_method_resource) |  | 
 |

#### Method resource

Signatures:

-   java.io.InputStream resource(String path, Object resource, java.util.Map<String, Object> queryParams);
    

The dhis2/resource API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **path** | 
 | String |
| **queryParams** | 

 | Map |
| **resource** | 

 | Object |

In addition to the parameters above, the dhis2 API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelDhis2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelDhis2.myParameterNameHere` header.

### API: resourceTables

**Both producer and consumer are supported**

The resourceTables API is defined in the syntax as follows:

```none
dhis2:resourceTables/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**analytics**](#_api_resourceTables_method_analytics) |  | 
 |

#### Method analytics

Signatures:

-   void analytics(Boolean skipAggregate, Boolean skipEvents, Integer lastYears, Integer interval, Boolean async);
    

The dhis2/analytics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **async** | 
 | Boolean |
| **interval** | 

 | Integer |
| **lastYears** | 

 | Integer |
| **skipAggregate** | 

 | Boolean |
| **skipEvents** | 

 | Boolean |

In addition to the parameters above, the dhis2 API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelDhis2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelDhis2.myParameterNameHere` header.

## Examples

-   Fetch an organisation unit by ID:
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:getResource")
                .to("dhis2:get/resource?path=organisationUnits/O6uvpzGd5pu&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .unmarshal()
                .json(org.hisp.dhis.api.model.v40_2_2.OrganisationUnit.class);
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:getResource
        steps:
          - to:
              uri: dhis2:get/resource
              parameters:
                path: organisationUnits/O6uvpzGd5pu
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
          - unmarshal:
              json:
                unmarshalType: org.hisp.dhis.api.model.v40_2_2.OrganisationUnit
    ```
    
-   Fetch all organisation units:
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:getCollection")
                .to("dhis2:get/collection?path=organisationUnits&arrayName=organisationUnits&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .split().body()
                .convertBodyTo(org.hisp.dhis.api.model.v40_2_2.OrganisationUnit.class).log("${body}");
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:getCollection
        steps:
          - to:
              uri: dhis2:get/collection
              parameters:
                path: organisationUnits
                arrayName: organisationUnits
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
          - split:
              expression:
                simple:
                  expression: ${body}
              steps:
                - convertBodyTo:
                    type: org.hisp.dhis.api.model.v40_2_2.OrganisationUnit
                - log:
                    message: ${body}
    ```
    
-   Fetch all organisation unit codes:
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:getCollection")
                .to("dhis2:get/collection?path=organisationUnits&arrayName=organisationUnits&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .split().body()
                .convertBodyTo(org.hisp.dhis.api.model.v40_2_2.OrganisationUnit.class).log("${body}");
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:getCollection
        steps:
          - to:
              uri: dhis2:get/collection
              parameters:
                path: organisationUnits
                arrayName: organisationUnits
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
                fields: code
          - split:
              expression:
                simple:
                  expression: ${body}
              steps:
                - convertBodyTo:
                    type: org.hisp.dhis.api.model.v40_2_2.OrganisationUnit
                - log:
                    message: ${body}
    ```
    
-   Fetch users with a phone number:
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:getCollection")
                .to("dhis2://get/collection?path=users&filter=phoneNumber:!null:&arrayName=users&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .split().body()
                .convertBodyTo(org.hisp.dhis.api.model.v40_2_2.User.class)
                .log("${body}");
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:getCollection
        steps:
          - to:
              uri: dhis2:get/collection
              parameters:
                path: users
                arrayName: users
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
                filter: "phoneNumber:!null:"
          - split:
              expression:
                simple:
                  expression: ${body}
              steps:
                - convertBodyTo:
                    type: org.hisp.dhis.api.model.v40_2_2.User
                - log:
                    message: ${body}
    ```
    
-   Save a data value set
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.LoggingLevel;
    import org.apache.camel.builder.RouteBuilder;
    import org.hisp.dhis.api.model.v40_2_2.DataValueSet;
    import org.hisp.dhis.api.model.v40_2_2.DataValue;
    import org.hisp.dhis.integration.sdk.support.period.PeriodBuilder;
    
    import java.time.ZoneOffset;
    import java.time.ZonedDateTime;
    import java.time.format.DateTimeFormatter;
    import java.util.Date;
    import java.util.List;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:postResource")
                .setBody(exchange -> new DataValueSet().withCompleteDate(
                        ZonedDateTime.now(ZoneOffset.UTC).format(DateTimeFormatter.ISO_LOCAL_DATE))
                                                                       .withOrgUnit("O6uvpzGd5pu")
                                                                       .withDataSet("lyLU2wR22tC").withPeriod(PeriodBuilder.monthOf(new Date(), -1))
                                                                       .withDataValues(
                                                                           List.of(new DataValue().withDataElement("aIJZ2d2QgVV").withValue("20"))))
                .to("dhis2://post/resource?path=dataValueSets&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .unmarshal().json()
                .choice()
                .when().groovy("body.status != 'OK'")
                    .log(LoggingLevel.ERROR, "Import error from DHIS2 while saving data value set => ${body}")
                .end();
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:postResource
        steps:
          - setBody:
              groovy: |
                new org.hisp.dhis.api.model.v40_2_2.DataValueSet()
                  .withCompleteDate(java.time.ZonedDateTime.now(java.time.ZoneOffset.UTC).format(java.time.format.DateTimeFormatter.ISO_LOCAL_DATE))
                  .withOrgUnit('O6uvpzGd5pu')
                  .withDataSet('lyLU2wR22tC')
                  .withPeriod(org.hisp.dhis.integration.sdk.support.period.PeriodBuilder.monthOf(new Date(), -1))
                  .withDataValues([new org.hisp.dhis.api.model.v40_2_2.DataValue().withDataElement('aIJZ2d2QgVV').withValue('20')])
          - to:
              uri: dhis2:post/resource
              parameters:
                path: dataValueSets
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
          - unmarshal:
              json: {}
          - choice:
              when:
                - groovy: body.status != 'OK'
                  steps:
                    - log:
                        loggingLevel: ERROR
                        message: Import error from DHIS2 while saving data value set => ${body}
    ```
    
-   Update an organisation unit
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.LoggingLevel;
    import org.apache.camel.builder.RouteBuilder;
    import org.hisp.dhis.api.model.v40_2_2.OrganisationUnit;
    
    import java.util.Date;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:putResource")
                .setBody(exchange -> new OrganisationUnit().withName("Acme").withShortName("Acme").withOpeningDate(new Date()))
                .to("dhis2://put/resource?path=organisationUnits/jUb8gELQApl&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .unmarshal().json()
                .choice()
                .when().groovy("body.status != 'OK'")
                    .log(LoggingLevel.ERROR, "Import error from DHIS2 while updating org unit => ${body}")
                .end();
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:putResource
        steps:
          - setBody:
              groovy: |
                new org.hisp.dhis.api.model.v40_2_2.OrganisationUnit()
                  .withName('Acme')
                  .withShortName('Acme')
                  .withOpeningDate(new Date())
          - to:
              uri: dhis2:put/resource
              parameters:
                path: organisationUnits/jUb8gELQApl
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
          - unmarshal:
              json: {}
          - choice:
              when:
                - groovy: body.status != 'OK'
                  steps:
                    - log:
                        loggingLevel: ERROR
                        message: Import error from DHIS2 while updating org unit => ${body}
    ```
    
-   Delete an organisation unit
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.LoggingLevel;
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:deleteResource")
                .to("dhis2://delete/resource?path=organisationUnits/jUb8gELQApl&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api")
                .unmarshal().json()
                .choice()
                .when().groovy("body.status != 'OK'")
                    .log(LoggingLevel.ERROR, "Import error from DHIS2 while deleting org unit => ${body}")
                .end();
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:deleteResource
        steps:
          - to:
              uri: dhis2:delete/resource
              parameters:
                path: organisationUnits/jUb8gELQApl
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
          - unmarshal:
              json: {}
          - choice:
              when:
                - groovy: body.status != 'OK'
                  steps:
                    - log:
                        loggingLevel: ERROR
                        message: Import error from DHIS2 while deleting org unit => ${body}
    ```
    
-   Run analytics
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:resourceTablesAnalytics")
                .to("dhis2://resourceTables/analytics?skipAggregate=false&skipEvents=true&lastYears=1&username=admin&password=district&baseApiUrl=https://play.im.dhis2.org/stable-2-40-5/api");
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:resourceTablesAnalytics
        steps:
          - to:
              uri: dhis2:resourceTables/analytics
              parameters:
                skipAggregate: false
                skipEvents: true
                lastYears: 1
                username: admin
                password: district
                baseApiUrl: https://play.im.dhis2.org/stable-2-40-5/api
    ```
    
-   Reference DHIS2 client
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    import org.hisp.dhis.integration.sdk.Dhis2ClientBuilder;
    import org.hisp.dhis.integration.sdk.api.Dhis2Client;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            Dhis2Client dhis2Client = Dhis2ClientBuilder.newClient("https://play.im.dhis2.org/stable-2-40-5/api", "admin", "district").build();
            getCamelContext().getRegistry().bind("dhis2Client", dhis2Client);
    
            from("direct:resourceTablesAnalytics")
                .to("dhis2://resourceTables/analytics?skipAggregate=true&skipEvents=true&lastYears=1&client=#dhis2Client");
        }
    }
    ```
    
    ```yaml
    - beans:
      - name: dhis2Client
        type: org.hisp.dhis.integration.sdk.api.Dhis2Client
        scriptLanguage: groovy
        script: >
          org.hisp.dhis.integration.sdk.Dhis2ClientBuilder.newClient('https://play.im.dhis2.org/stable-2-40-5/api', 'admin', 'district').build()
    
    - route:
        from:
          uri: direct:resourceTablesAnalytics
        steps:
          - to:
              uri: dhis2:resourceTables/analytics
              parameters:
                skipAggregate: true
                skipEvents: true
                lastYears: 1
                client: "#dhis2Client"
    ```
    
-   Set custom query parameters
    
    -   Java
        
    -   YAML
        
    
    ```java
    package org.camel.dhis2.example;
    
    import org.apache.camel.builder.RouteBuilder;
    
    import java.util.Map;
    
    public class MyRouteBuilder extends RouteBuilder {
    
        public void configure() {
            from("direct:clearCache")
                .setHeader("CamelDhis2.queryParams", constant(Map.of("cacheClear", "true")))
                .to("dhis2://post/resource?path=maintenance&client=#dhis2Client");
        }
    }
    ```
    
    ```yaml
    - route:
        from:
          uri: direct:clearCache
        steps:
          - setHeader:
              name: CamelDhis2.queryParams
              groovy: "['cacheClear':'true']"
          - to:
              uri: dhis2:post/resource
              parameters:
                path: maintenance
                client: "#dhis2Client"
    ```