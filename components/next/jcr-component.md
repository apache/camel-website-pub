# JCR

**Since Camel 1.3**

**Both producer and consumer are supported**

The JCR component allows you to add/read nodes to/from a JCR compliant content repository, for example, [Apache Jackrabbit](http://jackrabbit.apache.org/), with its producer, or register an EventListener with the consumer.

You can use consumer as an EventListener in JCR or a producer to read a node by identifier.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jcr</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jcr://user:password@repository/path/to/node

The `repository` element of the URI is used to look up the JCR `Repository` object in the Camel context registry.

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

The JCR component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JCR endpoint is configured using URI syntax:

jcr:host/base

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Name of the javax.jcr.Repository to lookup from the Camel registry to be used. |  | String |
| **base** (common) | Get the base node when accessing the repository. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **deep** (common) | When isDeep is true, events whose associated parent node is at absPath or within its subgraph are received. | false | boolean |
| **eventTypes** (common) | eventTypes (a combination of one or more event types encoded as a bit mask value such as javax.jcr.observation.Event.NODE\_ADDED, javax.jcr.observation.Event.NODE\_REMOVED, etc.). |  | int |
| **nodeTypeNames** (common) | When a comma separated nodeTypeName list string is set, only events whose associated parent node has one of the node types (or a subtype of one of the node types) in this list will be received. |  | String |
| **noLocal** (common) | If noLocal is true, then events generated by the session through which the listener was registered are ignored. Otherwise, they are not ignored. | false | boolean |
| **sessionLiveCheckInterval** (common) | Interval in milliseconds to wait before each session live checking The default value is 60000 ms. | 60000 | long |
| **sessionLiveCheckIntervalOnStart** (common) | Interval in milliseconds to wait before the first session live checking. The default value is 3000 ms. | 3000 | long |
| **username** (common) | Username for login. |  | String |
| **uuids** (common) | When a comma separated uuid list string is set, only events whose associated parent node has one of the identifiers in the comma separated uuid list will be received. |  | String |
| **workspaceName** (common) | The workspace to access. If it’s not specified then the default one will be used. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **password** (security) | Password for login. |  | String |

## Message Headers

The JCR component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJcrNodeName** (producer) Constant: [`JCR_NODE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-jcr/latest/org/apache/camel/component/jcr/JcrConstants.html#JCR_NODE_NAME) | The name of the target node. | The exchange id | String |
| **CamelJcrOperation** (producer) Constant: [`JCR_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-jcr/latest/org/apache/camel/component/jcr/JcrConstants.html#JCR_OPERATION) | The operation to perform. Possible values: CamelJcrInsert or CamelJcrGetById. | CamelJcrInsert | String |
| **CamelJcrNodeType** (producer) Constant: [`JCR_NODE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jcr/latest/org/apache/camel/component/jcr/JcrConstants.html#JCR_NODE_TYPE) | The node type of the target node. |  | String |

## Example

The snippet below creates a node named `node` under the `/home/test` node in the content repository. One additional property is added to the node as well: `my.contents.property` which will contain the body of the message being sent.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a").setHeader("CamelJcrNodeName", constant("node"))
    .setHeader("my.contents.property", body())
    .to("jcr://user:pass@repository/home/test");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeader name="CamelJcrNodeName">
        <constant>node</constant>
    </setHeader>
    <setHeader name="my.contents.property">
        <simple>${body}</simple>
    </setHeader>
    <to uri="jcr://user:pass@repository/home/test"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setHeader:
            name: CamelJcrNodeName
            expression:
              constant:
                expression: node
        - setHeader:
            name: my.contents.property
            expression:
              simple:
                expression: "${body}"
        - to:
            uri: jcr://user:pass@repository/home/test
```

The following code will register an EventListener under the path import-application/inbox for `Event.NODE_ADDED` and `Event.NODE_REMOVED` events (event types 1 and 2, both masked as 3) and listening deep for all the children.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jcr://user:pass@repository/import-application/inbox?eventTypes=3&deep=true")
    .to("direct:execute-import-application");
```

```xml
<route>
    <from uri="jcr://user:pass@repository/import-application/inbox?eventTypes=3&amp;deep=true"/>
    <to uri="direct:execute-import-application"/>
</route>
```

```yaml
- route:
    from:
      uri: jcr://user:pass@repository/import-application/inbox
      parameters:
        eventTypes: 3
        deep: true
      steps:
        - to:
            uri: direct:execute-import-application
```