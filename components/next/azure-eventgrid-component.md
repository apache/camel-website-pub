# Azure Event Grid

**Since Camel 4.17**

**Only producer is supported**

The Azure Event Grid component provides the capability to publish events to [Azure Event Grid](https://learn.microsoft.com/en-us/azure/event-grid/overview) topics using [CloudEvents](https://learn.microsoft.com/en-us/azure/event-grid/cloud-event-schema).

Azure Event Grid is an eventing service for the cloud that enables event-driven architectures. It provides event routing from any source to any destination with rich filtering capabilities.

**Prerequisites**

You must have a valid Microsoft Azure account and an Event Grid topic. More information is available at the [Azure Event Grid documentation](https://learn.microsoft.com/en-us/azure/event-grid/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-eventgrid</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-eventgrid:topicEndpoint
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

The Azure Event Grid component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The component configurations. |  | EventGridConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **publisherClient** (producer) | **Autowired** The EventGrid publisher client. If provided, it will be used instead of creating a new one. |  | EventGridPublisherClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | The access key for the Event Grid topic. Required when using ACCESS\_KEY credential type. |  | String |
| **azureKeyCredential** (security) | **Autowired** The Azure Key Credential for authentication. This is automatically created from the accessKey if not provided. |  | AzureKeyCredential |
| **credentialType** (security) | 
Determines the credential strategy to adopt.

Enum values:

-   ACCESS\_KEY
    
-   AZURE\_IDENTITY
    
-   TOKEN\_CREDENTIAL
    





 | ACCESS\_KEY | CredentialType |
| **tokenCredential** (security) | **Autowired** Provide custom authentication credentials using an implementation of TokenCredential. |  | TokenCredential |

## Endpoint Options

The Azure Event Grid endpoint is configured using URI syntax:

azure-eventgrid:topicEndpoint

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicEndpoint** (producer) | **Required** The topic endpoint URL where events will be published. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **publisherClient** (producer) | **Autowired** The EventGrid publisher client. If provided, it will be used instead of creating a new one. |  | EventGridPublisherClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | The access key for the Event Grid topic. Required when using ACCESS\_KEY credential type. |  | String |
| **azureKeyCredential** (security) | **Autowired** The Azure Key Credential for authentication. This is automatically created from the accessKey if not provided. |  | AzureKeyCredential |
| **credentialType** (security) | 
Determines the credential strategy to adopt.

Enum values:

-   ACCESS\_KEY
    
-   AZURE\_IDENTITY
    
-   TOKEN\_CREDENTIAL
    





 | ACCESS\_KEY | CredentialType |
| **tokenCredential** (security) | **Autowired** Provide custom authentication credentials using an implementation of TokenCredential. |  | TokenCredential |

## Message Headers

The Azure Event Grid component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureEventGridEventType** (producer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventgrid/latest/org/apache/camel/component/azure/eventgrid/EventGridConstants.html#EVENT_TYPE) | The event type of the event. |  | String |
| **CamelAzureEventGridSubject** (producer) Constant: [`SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventgrid/latest/org/apache/camel/component/azure/eventgrid/EventGridConstants.html#SUBJECT) | The subject of the event. |  | String |
| **CamelAzureEventGridEventTime** (producer) Constant: [`EVENT_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventgrid/latest/org/apache/camel/component/azure/eventgrid/EventGridConstants.html#EVENT_TIME) | The time the event was generated. |  | OffsetDateTime |
| **CamelAzureEventGridId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventgrid/latest/org/apache/camel/component/azure/eventgrid/EventGridConstants.html#ID) | The unique identifier for the event. |  | String |
| **CamelAzureEventGridDataVersion** (producer) Constant: [`DATA_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventgrid/latest/org/apache/camel/component/azure/eventgrid/EventGridConstants.html#DATA_VERSION) | The schema version of the data object. |  | String |

## Authentication

The component supports the following credential types via the `credentialType` option:

ACCESS\_KEY

Uses the Event Grid topic access key for authentication (default). Set the `accessKey` option with your topic key.

TOKEN\_CREDENTIAL

Uses a `TokenCredential` implementation (e.g., Azure Identity `DefaultAzureCredential`). Set the `tokenCredential` option.

AZURE\_IDENTITY

Uses Azure Identity default credential chain automatically.

## Usage

### Sending events

The producer publishes events as CloudEvents to the configured Event Grid topic endpoint:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-eventgrid:https://my-topic.eastus-1.eventgrid.azure.net/api/events?accessKey=RAW(myKey)");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="azure-eventgrid:https://my-topic.eastus-1.eventgrid.azure.net/api/events?accessKey=RAW(myKey)"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - to:
          uri: azure-eventgrid:https://my-topic.eastus-1.eventgrid.azure.net/api/events
          parameters:
            accessKey: "RAW(myKey)"
```