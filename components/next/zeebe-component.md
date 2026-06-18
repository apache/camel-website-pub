# Zeebe

> **Warning**
> **Deprecated:** This zeebe is deprecated and may be removed in a future release.

**Since Camel 3.21**

**Both producer and consumer are supported**

> **Note**
> This component is deprecated since Camel 4.19 and will be removed in a future release. Please use the [Camunda](camunda-component.md) component instead, which uses the new Camunda Java Client (`io.camunda:camunda-client-java`).

The **Zeebe**: components provides the ability to interact with business processes in [Zeebe](https://github.com/camunda/zeebe).

To use the Zeebe component, Maven users will need to add the following dependency to their `pom.xml`:

> **Note**
> **Prerequisites**
>
> You must have access to a local zeebe instance. More information is available at [Camunda Zeebe](https://camunda.com/platform/zeebe/).

## URI format

zeebe://\[endpoint\]?\[options\]

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

The Zeebe component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **oAuthAPI** (common) | The authorization server’s URL, from which the access token will be requested. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientId** (security) | Client id to be used when requesting access token from OAuth authorization server. |  | String |
| **clientSecret** (security) | Client secret to be used when requesting access token from OAuth authorization server. |  | String |
| **gatewayHost** (security) | The gateway server hostname to connect to the Zeebe cluster. | localhost | String |
| **gatewayPort** (security) | The gateway server port to connect to the Zeebe cluster. | 26500 | int |

## Endpoint Options

The Zeebe endpoint is configured using URI syntax:

zeebe:operationName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operationName** (common) | 
**Required** The operation to use.

Enum values:

-   startProcess
    
-   cancelProcess
    
-   publishMessage
    
-   completeJob
    
-   failJob
    
-   updateJobRetries
    
-   worker
    
-   throwError
    
-   deployResource
    





 |  | OperationName |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **formatJSON** (common) | Format the result in the body as JSON. | false | boolean |
| **jobKey** (consumer) | JobKey for the job worker. |  | String |
| **timeout** (consumer) | Timeout for job worker. | 10 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Zeebe component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelZeebeResourceName** (producer) Constant: [`RESOURCE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#RESOURCE_NAME) | The name of the resource. |  | String |
| **CamelZeebeIsSuccess** (producer) Constant: [`IS_SUCCESS`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#IS_SUCCESS) | True if the operation was successful. |  | boolean |
| **CamelZeebeErrorMessage** (producer) Constant: [`ERROR_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#ERROR_MESSAGE) | In case of an error, the error message. |  | String |
| **CamelZeebeErrorCode** (producer) Constant: [`ERROR_CODE`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#ERROR_CODE) | In case of an error, the error code if available. |  | String |
| **CamelZeebeBPMNProcessId** (producer) Constant: [`BPMN_PROCESS_ID`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#BPMN_PROCESS_ID) | The process ID of a deployed process. |  | String |
| **CamelZeebeVersion** (producer) Constant: [`VERSION`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#VERSION) | The version of a deployed process. |  | int |
| **CamelZeebeProcessDefinitionKey** (producer) Constant: [`PROCESS_DEFINITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#PROCESS_DEFINITION_KEY) | The process definition key of a deployed process. |  | long |
| **CamelZeebeJobKey** (common) Constant: [`JOB_KEY`](https://javadoc.io/doc/org.apache.camel/camel-zeebe/latest/org/apache/camel/component/zeebe/ZeebeConstants.html#JOB_KEY) | The key of a job. The worker consumer adds the job key to the headers and the operations completeJob and failJob accept the job key in the header if no JobRequest is provided in the body. |  | long |

## Usage

### Producer Endpoints

 
| Endpoint | Description |
| --- | --- |
| `startProcess` | Creates and starts an instance of the specified process. |
| `cancelProcess` | Cancels a running process instance. |
| `publishMessage` | Publishes a message. |
| `completeJob` | Completes a job for a service task. |
| `failJob` | Fails a job. |
| `updateJobRetries` | Updates the number of retries for a job. |
| `throwError` | Throw an error to indicate that a business error has occurred. |
| `deployResource` | Deploy a process resource. Currently only supports process definitions. |

The endpoints accept either Java request objects as shown in the examples below or JSON. In JSON camel case for property names is replaced with all lower case separated by underscores, e.g., processId becomes process\_id.

**Examples**

-   startProcess
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            ProcessRequest request = new ProcessRequest();
            request.setProcessId("processId");
            request.setVariables(new HashMap<String,Object> ());
            exchange.getIn().setBody(request);
        })
        .to("zeebe://startProcess")
        .process(exchange -> {
            ProcessResponse body = exchange.getIn().getBody(ProcessResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
                long processInstanceKey = body.getProcessInstanceKey();
            }
        });
```

**JSON Request Example**

```json
    {
        "process_id" : "Process_0e3ldfm",
        "variables" : { "v1": "a", "v2": 10 }
    }
```

**JSON Response Example**

```json
    {
        "success": true,
        "process_id": "Process_0e3ldfm",
        "process_instance_key": 2251799813688297,
        "process_version": 4,
        "process_key": 2251799813685906
    }
```

-   cancelProcess
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            ProcessRequest request = new ProcessRequest();
            request.setProcessInstanceKey(123);
            exchange.getIn().setBody(request);
        })
        .to("zeebe://cancelProcess")
        .process(exchange -> {
            ProcessResponse body = exchange.getIn().getBody(ProcessResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
            }
        });
```

-   publishMessage
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            MessageRequest request = new MessageRequest();
            request.setCorrelationKey("messageKey");
            request.setTimeToLive(100);
            request.setVariables(new HashMap<String,Object>());
            request.setName("MessageName");
            exchange.getIn().setBody(request);
        })
        .to("zeebe://publishMessage")
        .process(exchange -> {
            MessageResponse body = exchange.getIn().getBody(MessageResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
                String messageKey = body.getMessageKey();
            }
        });
```

**JSON Request Example**

```json
    {
        "correlation_key" : "messageKey",
        "time-to-live" : 100,
        "variables" : { "v1": "a", "v2": 10 },
        "name" : "MessageName"
    }
```

**JSON Response Example**

```json
    {
        "success": true,
        "correlation_key": "messageKey",
        "message_key": 2251799813688336
    }
```

-   completeJob
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            JobRequest request = new JobRequest();
            request.setJobKey("jobKey");
            request.setVariables(new HashMap<String,Object>());
            exchange.getIn().setBody(request);
        })
        .to("zeebe://completeJob")
        .process(exchange -> {
            JobResponse body = exchange.getIn().getBody(JobResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
            }
        });
```

-   failJob
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            JobRequest request = new JobRequest();
            request.setJobKey("jobKey");
            request.setRetries(3);
            request.setErrorMessage("Error");
            exchange.getIn().setBody(request);
        })
        .to("zeebe://failJob")
        .process(exchange -> {
            JobResponse body = exchange.getIn().getBody(JobResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
            }
        });
```

-   updateJobRetries
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            JobRequest request = new JobRequest();
            request.setJobKey("jobKey");
            request.setRetries(3);
            exchange.getIn().setBody(request);
        })
        .to("zeebe://updateJobRetries")
        .process(exchange -> {
            JobResponse body = exchange.getIn().getBody(JobResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
            }
        });
```

-   throwError
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            JobRequest request = new JobRequest();
            request.setJobKey("jobKey");
            request.setErrorMessage("Error Message");
            request.setErrorCode("Error Code")
            exchange.getIn().setBody(request);
        })
        .to("zeebe://throwError")
        .process(exchange -> {
            JobResponse body = exchange.getIn().getBody(JobResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
            }
        });
```

-   deployResource
    

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("direct:start")
        .process(exchange -> {
            DeploymentRequest request = new DeploymentRequest();
            request.setName("process.bpmn");
            request.setContent(content.getBytes());
            exchange.getIn().setBody(request);
        })
        .to("zeebe://deployResource")
        .process(exchange -> {
            ProcessDeploymentResponse body = exchange.getIn().getBody(ProcessDeploymentResponse.class);
            if (body != null) {
                bool success = body.getSuccess();
                String bpmnProcessId = body.getBpmnProcessId();
                int version = body.getVersion();
                long processDefinitionKey = body.getProcessDefinitionKey();
                String resourceName = body.getResourceName();
            }
        });
```

### Consumer Endpoints:

 
| Endpoint | Description |
| --- | --- |
| worker | Registers a job worker for a job type and provides messages for available jobs. |

**Example**

_Java-only: inline Processor with Zeebe SDK types_

```java
    from("zeebe://worker?jobKey=job1&timeout=20")
        .process(exchange -> {
            JobWorkerMessage body = exchange.getIn().getBody(JobWorkerMessage.class);
            if (body != null) {
                long key = body.getKey();
                String type = body.getType();
                Map<String,String> customHeaders = body.getCustomHeaders();
                long processInstanceKey = body.getProcessInstanceKey();
                String bpmnProcessId = body.getBpmnProcessId();
                int processDefinitionVersion = body.getProcessDefinitionVersion();
                long processDefinitionKey = body.getProcessDefinitionKey();
                String elementId = body.getElementId();
                long elementInstanceKey = body.getElementInstanceKey();
                String worker = body.getWorker();
                int retries = body.getRetries();
                long deadline = body.getDeadline();
                Map<String,Object> variables = body.getVariables();
            }
        })
```

camel-zeebe creates a route exchange per job type with a job in the body.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-zeebe</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using zeebe with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-zeebe-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.zeebe.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.zeebe.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.zeebe.client-id** | Client id to be used when requesting access token from OAuth authorization server. |  | String |
| **camel.component.zeebe.client-secret** | Client secret to be used when requesting access token from OAuth authorization server. |  | String |
| **camel.component.zeebe.enabled** | Whether to enable auto configuration of the zeebe component. This is enabled by default. |  | Boolean |
| **camel.component.zeebe.gateway-host** | The gateway server hostname to connect to the Zeebe cluster. | localhost | String |
| **camel.component.zeebe.gateway-port** | The gateway server port to connect to the Zeebe cluster. | 26500 | Integer |
| **camel.component.zeebe.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.zeebe.o-auth-a-p-i** | The authorization server’s URL, from which the access token will be requested. |  | String |