# JBPM

**Since Camel 2.6**

**Both producer and consumer are supported**

The JBPM component provides integration with Business Process Management [jBPM](http://www.jbpm.org/). It uses kie-server-client API to interact with jBPM instance over REST. The component supports both producer and consumer.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jbpm</artifactId>
    <version>x.x.x</version><!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jbpm::events:type:\[classifier\]\[?options\]

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

The JBPM component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JBPM endpoint is configured using URI syntax:

jbpm:connectionURL

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectionURL** (common) | **Required** The URL to the jBPM server. |  | URL |
| **eventListenerType** (common) | Sets the event listener type to attach to. |  | String |

### Query Parameters (31 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **attachmentId** (common) | attachId to use when retrieving attachments. |  | Long |
| **contentId** (common) | contentId to use when retrieving attachments. |  | Long |
| **deploymentId** (common) | **Required** The id of the deployment. |  | String |
| **emitterSendItems** (common) | Sets if event produced by emitter should be sent as single items or complete collection. |  | Boolean |
| **event** (common) | the data associated with this event when signalEvent operation is performed. |  | Object |
| **eventType** (common) | the type of event to use when signalEvent operation is performed. |  | String |
| **identifier** (common) | identifier the global identifier. |  | String |
| **maxNumber** (common) | the maximum number of rules that should be fired. |  | Integer |
| **page** (common) | The page to use when retrieving user tasks. |  | Integer |
| **pageSize** (common) | The page size to use when retrieving user tasks. |  | Integer |
| **processId** (common) | the id of the process that should be acted upon. |  | String |
| **processInstanceId** (common) | the id of the process instance. |  | Long |
| **targetUserId** (common) | The targetUserId used when delegating a task. |  | String |
| **task** (common) | The task instance to use with task operations. |  | Task |
| **taskId** (common) | the id of the task. |  | Long |
| **timeout** (common) | A timeout value. |  | Integer |
| **userId** (common) | userId to use with task operations. |  | String |
| **value** (common) | the value to assign to the global identifier. |  | Object |
| **workItemId** (common) | the id of the work item. |  | Long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **synchronous** (consumer (advanced)) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **operation** (producer) | The operation to perform. | startProcess | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **entities** (advanced) | The potentialOwners when nominateTask operation is performed. |  | List |
| **extraJaxbClasses** (advanced) | To load additional classes when working with XML. |  | Class\[\] |
| **parameters** (advanced) | the variables that should be set for various operations. |  | Map |
| **statuses** (filter) | The list of status to use when filtering tasks. |  | List |
| **password** (security) | Password for authentication. |  | String |
| **userName** (security) | Username for authentication. |  | String |

## Consumer

jBPM Consumer allows to attach routes to

-   ProcessEventListeners
    
-   TaskEventListeners
    
-   CaseEventListeners
    

### Path Parameters (3 parameters):

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **events** | Classifier for the consumer to know which type of data it should attach to |  | URL |
| **type** | Type of event listener - supports: process, task, case |  | String |
| **classifier** | Used to distinguish routes for same event type |  | String |

Each route would then receive events when they are being produced by jBPM engine.

Routes can be defined either in global way - on application level or deployed together with business assets projects also knows as KJARs.

Consumers are configured via KieServerExtension that is a pluggable interface to enhance jBPM with additional capabilities. It reacts to different life cycle phases of the KIE Server and by that is able to configure individual endpoints properly.

## KJAR routes

Create file named `camel-routes.xml` in the root folder of your KJAR (src/main/resources) so it will be automatically discovered and Camel Context for given KJAR will be created.

## Global routes

Create file name `global-camel-routes` in the root of the class path of KIE Server. It will be automatically found and registered on every KJAR deployed to KIE Server.

Example `camel-routes.xml` file that can be placed in the KJAR

```xml
<routes xmlns="http://camel.apache.org/schema/spring">

    <route id="processes">
        <from uri="jbpm:events:process:test"/>
        <filter>
          <simple>${in.header.EventType} == 'beforeProcessStarted'</simple>
          <to uri="log:kjar.processes?level=INFO&amp;showBody=true&amp;showHeaders=true"/>
        </filter>
    </route>

    <route id="tasks">
        <from uri="jbpm:events:task:test"/>
        <filter>
          <simple>${in.header.EventType} starts with 'before'</simple>
          <to uri="log:kjar.tasks?level=INFO&amp;showBody=true&amp;showHeaders=true"/>
        </filter>
    </route>
</routes>
```

## Use of jBPM Component in KIE Server

To make use of camel-jbpm component in a KIE Server it is as simple as just adding two jars into KIE Server application

-   camel-core
    
-   camel-jbpm
    

then start KIE Server and you will see once booted following information in logs

Camel KIE Server extension has been successfully registered as server extension
....
Route: tasks started and consuming from: jbpm://events:task:test?deploymentId=form-rendering\_1.0.0
Total 2 routes, of which 2 are started
Apache Camel 2.23.0-SNAPSHOT (CamelContext: KIE Server Camel context for container evaluation\_1.0.0) started in 0.378 seconds
o.k.server.services.impl.KieServerImpl   : Container evaluation\_1.0.0 (for release id evaluation:evaluation:1.0.0) successfully started

To make use of jBPM Consumer jBPM deployment descriptor must also define camel specific event listeners of following types

-   `new org.apache.camel.component.jbpm.listeners.CamelProcessEventListener()`
    
-   `new org.apache.camel.component.jbpm.listeners.CamelTaskEventListener()`
    
-   `new org.apache.camel.component.jbpm.listeners.CamelCaseEventListener()`
    

These must be set in either server level of kjar deployment descriptor (use MVEL as resolver type) - see jbpm docs for more details about deployment descriptors.

## Producer

Producer is dedicated to interact with jBPM via kie-server-client that uses exposed REST api of jBPM (KIE Server).

## URI format

jbpm::hostName\[:port\]\[/resourceUri\]\[?options\]

## Message Headers

The JBPM component supports 20 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJBPMValue** (producer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#VALUE) | The value to assign to the global identifier. |  | Object |
| **CamelJBPMOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#OPERATION) | The operation to perform. The operation name must be prefixed with CamelJBPMOperation and the name of the operation. See the full list above. It is case-insensitive. | PUT | String |
| **CamelJBPMProcessId** (producer) Constant: [`PROCESS_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#PROCESS_ID) | The id of the process that should be acted upon. |  | String |
| **CamelJBPMProcessInstanceId** (producer) Constant: [`PROCESS_INSTANCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#PROCESS_INSTANCE_ID) | The id of the process instance. |  | Long |
| **CamelJBPMParameters** (producer) Constant: [`PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#PARAMETERS) | The variables that should be set for various operations. |  | Map |
| **CamelJBPMEventType** (producer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#EVENT_TYPE) | The type of event to use when signalEvent operation is performed. |  | String |
| **CamelJBPMEvent** (producer) Constant: [`EVENT`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#EVENT) | The type of the received event. Possible values defined here org.infinispan.notifications.cachelistener.event.Event.Type. |  | Object |
| **CamelJBPMMaxNumber** (producer) Constant: [`MAX_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#MAX_NUMBER) | The maximum number of rules that should be fired. |  | Integer |
| **CamelJBPMIdentifier** (producer) Constant: [`IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#IDENTIFIER) | The global identifier. |  | String |
| **CamelJBPMWorkItemId** (producer) Constant: [`WORK_ITEM_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#WORK_ITEM_ID) | The id of the work item. |  | Long |
| **CamelJBPMTaskId** (producer) Constant: [`TASK_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#TASK_ID) | The id of the task. |  | Long |
| **CamelJBPMTask** (producer) Constant: [`TASK`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#TASK) | The task instance to use with task operations. |  | Task |
| **CamelJBPMUserId** (producer) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#USER_ID) | The userId to use with task operations. |  | String |
| **CamelJBPMTargetUserId** (producer) Constant: [`TARGET_USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#TARGET_USER_ID) | The targetUserId used when delegating a task. |  | String |
| **CamelJBPMAttachmentId** (producer) Constant: [`ATTACHMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#ATTACHMENT_ID) | The attachId to use when retrieving attachments. |  | Long |
| **CamelJBPMContentId** (producer) Constant: [`CONTENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#CONTENT_ID) | The contentId to use when retrieving attachments. |  | Long |
| **CamelJBPMEntityList** (producer) Constant: [`ENTITY_LIST`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#ENTITY_LIST) | The potentialOwners when nominateTask operation is performed. |  | List |
| **CamelJBPMStatusList** (producer) Constant: [`STATUS_LIST`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#STATUS_LIST) | The list of status to use when filtering tasks. |  | List |
| **CamelJBPMResultPage** (producer) Constant: [`RESULT_PAGE`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#RESULT_PAGE) | The page to use when retrieving user tasks. |  | Integer |
| **CamelJBPMResultPageSize** (producer) Constant: [`RESULT_PAGE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-jbpm/latest/org/apache/camel/component/jbpm/JBPMConstants.html#RESULT_PAGE_SIZE) | The page size to use when retrieving user tasks. |  | Integer |

## Example

Below is an example route that starts a business process with id evaluation. To run this example you need jBPM to run locally, easiest is to use single zip distribution - downloaded from jbpm.org. Next, start it and import Evaluation sample project, build and deploy. Once done this test can be run out of the box.

```java
Map<String, Object> params = new HashMap<>();
params.put("employee", "wbadmin");
params.put("reason", "Camel asks for it");

from("direct:start")
        .setHeader(JBPMConstants.PROCESS_ID, constant("evaluation"))
        .setHeader((JBPMConstants.PARAMETERS, params))
        .to("jbpm:http://localhost:8080/kie-server/services/rest/server?userName=wbadmin&password=wbadmin
        &deploymentId=evaluation");
```

## Spring Boot Auto-Configuration

When using jbpm with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jbpm-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jbpm.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jbpm.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jbpm.enabled** | Whether to enable auto configuration of the jbpm component. This is enabled by default. |  | Boolean |
| **camel.component.jbpm.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |