# CM SMS Gateway

**Since Camel 2.18**

**Only producer is supported**

**Camel-Cm-Sms** is an [Apache Camel](http://camel.apache.org/) component for the [CM SMS Gateway](https://www.cmtelecom.com)

It allows integrating [CM SMS API](https://dashboard.onlinesmsgateway.com/docs) in an application as a camel component.

You must have a valid account. More information is available at [CM Telecom](https://www.cmtelecom.com/support).

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

The CM SMS Gateway component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The CM SMS Gateway endpoint is configured using URI syntax:

cm-sms:host

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** SMS Provider HOST with scheme. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultFrom** (producer) | **Required** This is the sender name. The maximum length is 11 characters. |  | String |
| **defaultMaxNumberOfParts** (producer) | If it is a multipart message forces the max number. Message can be truncated. Technically the gateway will first check if a message is larger than 160 characters, if so, the message will be cut into multiple 153 characters parts limited by these parameters. | 8 | int |
| **productToken** (producer) | **Required** The unique token to use. |  | String |
| **testConnectionOnStartup** (producer) | Whether to test the connection to the SMS Gateway on startup. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Example

cm-sms://sgw01.cm.nl/gateway.ashx?defaultFrom=DefaultSender&defaultMaxNumberOfParts=8&productToken=xxxxx

You can try [this project](https://github.com/oalles/camel-cm-sample) to see how camel-cm-sms can be integrated in a camel route.