# Workday

**Since Camel 3.1**

**Only producer is supported**

The **Workday**: components provides the ability to detect and parse documents with Workday.

In order to use the Workday component, Maven users will need to add the following dependency to their `pom.xml`:

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-workday</artifactId>
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

The Workday component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Workday endpoint is configured using URI syntax:

workday:entity:path

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **entity** (producer) | 
**Required** The entity to be requested or subscribed via API.

Enum values:

-   report
    
-   commonAPI
    





 |  | Entity |
| **path** (producer) | **Required** The API path to access an entity structure. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpConnectionManager** (advanced) | Pool connection manager for advanced configuration. |  | PoolingHttpClientConnectionManager |
| **reportFormat** (format) | 
Workday Report as a service output format.

Enum values:

-   json
    





 | json | String |
| **host** (host) | **Required** Workday Host name. |  | String |
| **clientId** (security) | **Required** Workday client Id generated by API client for integrations. |  | String |
| **clientSecret** (security) | **Required** Workday client Secret generated by API client for integrations. |  | String |
| **tokenRefresh** (security) | **Required** Workday token Refresh generated for integrations system user. |  | String |
| **tenant** (tenant) | **Required** Workday Tenant name. |  | String |

## Message Headers

The Workday component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWorkdayURL** (producer) Constant: [`WORKDAY_URL_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-workday/latest/org/apache/camel/component/workday/producer/WorkdayDefaultProducer.html#WORKDAY_URL_HEADER) | The workday URL. |  | String |