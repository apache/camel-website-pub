# Camunda

**Since Camel 4.19**

**Both producer and consumer are supported**

The **Camunda** component provides the ability to interact with [Camunda 8](https://camunda.com/) process orchestration clusters using the [Camunda Java Client](https://docs.camunda.io/docs/apis-tools/java-client/).

This component replaces the deprecated [camel-zeebe](zeebe-component.md) component, which used the older Zeebe Java Client.

> **Note**
> **Prerequisites**
>
> You must have access to a Camunda 8 cluster. This can be:
>
> -   A Camunda SaaS cluster at [Camunda SaaS](https://camunda.io/)
>     
> -   A self-managed Camunda 8 instance (e.g. via Docker Compose or Kubernetes)

To use the Camunda component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-camunda</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

camunda://\[endpoint\]?\[options\]

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

The Camunda component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **grpcAddress** (common) | gRPC address of the Camunda cluster (e.g. [http://localhost:26500](http://localhost:26500)). Used for self-managed connections when clusterId is not set. | [http://localhost:26500](http://localhost:26500) | String |
| **restAddress** (common) | REST address of the Camunda cluster (e.g. [http://localhost:8080](http://localhost:8080)). Used for self-managed connections when clusterId is not set. | [http://localhost:8080](http://localhost:8080) | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientId** (security) | Client ID for OAuth / SaaS authentication. |  | String |
| **clientSecret** (security) | Client secret for OAuth / SaaS authentication. |  | String |
| **clusterId** (security) | Camunda SaaS cluster ID. When set, the client connects via the cloud builder. |  | String |
| **oAuthAPI** (security) | OAuth authorization server URL for self-managed authentication. |  | String |
| **region** (security) | Camunda SaaS region (default: bru-2). | bru-2 | String |

## Endpoint Options

The Camunda endpoint is configured using URI syntax:

camunda:operationName

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
| **jobType** (consumer) | Job type for the job worker. |  | String |
| **timeout** (consumer) | Timeout for job worker in seconds. | 10 | int |
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

The Camunda component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCamundaJobKey** (producer) Constant: [`JOB_KEY`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#JOB_KEY) | Job key for the worker job. |  | long |
| **CamelCamundaResourceName** (producer) Constant: [`RESOURCE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#RESOURCE_NAME) | Resource name for deploy operation. |  | String |
| **CamelCamundaIsSuccess** (producer) Constant: [`IS_SUCCESS`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#IS_SUCCESS) | Indicates if the operation was successful. |  | boolean |
| **CamelCamundaErrorMessage** (producer) Constant: [`ERROR_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#ERROR_MESSAGE) | Error message if operation failed. |  | String |
| **CamelCamundaErrorCode** (producer) Constant: [`ERROR_CODE`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#ERROR_CODE) | Error code if operation failed. |  | String |
| **CamelCamundaBPMNProcessId** (producer) Constant: [`BPMN_PROCESS_ID`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#BPMN_PROCESS_ID) | The process ID of a deployed process. |  | String |
| **CamelCamundaVersion** (producer) Constant: [`VERSION`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#VERSION) | The version of a deployed process. |  | int |
| **CamelCamundaProcessDefinitionKey** (producer) Constant: [`PROCESS_DEFINITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-camunda/latest/org/apache/camel/component/camunda/CamundaConstants.html#PROCESS_DEFINITION_KEY) | The process definition key of a deployed process. |  | long |

## Connection Modes

### Camunda SaaS (Cloud)

Set the `clusterId`, `clientId`, `clientSecret`, and `region` component options.

_Java-only: programmatic component configuration_

```java
CamundaComponent camunda = context.getComponent("camunda", CamundaComponent.class);
camunda.setClusterId("your-cluster-id");
camunda.setClientId("your-client-id");
camunda.setClientSecret("your-client-secret");
camunda.setRegion("bru-2");
```

### Self-Managed

Set the `grpcAddress` and `restAddress` component options. For authenticated self-managed clusters, also set `clientId`, `clientSecret`, and `oAuthAPI`.

_Java-only: programmatic component configuration_

```java
CamundaComponent camunda = context.getComponent("camunda", CamundaComponent.class);
camunda.setGrpcAddress("http://localhost:26500");
camunda.setRestAddress("http://localhost:8080");
```

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
| `throwError` | Throws an error to indicate that a business error has occurred. |
| `deployResource` | Deploys a process resource. Currently supports process definitions. |

The endpoints accept either Java request objects as shown in the examples below or JSON. In JSON, camel case for property names is replaced with all lower case separated by underscores, e.g., processId becomes process\_id.

**Examples**

-   startProcess
    

-   Java
    
-   YAML
    
-   XML
    

```java
from("direct:start")
    .process(exchange -> {
        ProcessRequest request = new ProcessRequest();
        request.setProcessId("processId");
        request.setVariables(new HashMap<String,Object> ());
        exchange.getIn().setBody(request);
    })
    .to("camunda://startProcess")
    .process(exchange -> {
        ProcessResponse body = exchange.getIn().getBody(ProcessResponse.class);
        if (body != null) {
            boolean success = body.isSuccess();
            long processInstanceKey = body.getProcessInstanceKey();
        }
    });
```

```yaml
- route:
    from:
      uri: direct:start-process
      steps:
        - marshal:
            json: {}
        - setBody:
            simple: '{"process_id":"processId","variables":${body}}'
        - to:
            uri: camunda://startProcess
```

```xml
<route>
  <from uri="direct:start-process"/>
  <marshal>
    <json/>
  </marshal>
  <setBody>
    <simple>{"process_id":"processId","variables":${body}}</simple>
  </setBody>
  <to uri="camunda://startProcess"/>
</route>
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
    

-   Java
    
-   YAML
    
-   XML
    

```java
from("direct:cancel")
    .process(exchange -> {
        ProcessRequest request = new ProcessRequest();
        request.setProcessInstanceKey(123);
        exchange.getIn().setBody(request);
    })
    .to("camunda://cancelProcess");
```

```yaml
- route:
    from:
      uri: direct:cancel
      steps:
        - setBody:
            simple: '{"process_instance_key": 123}'
        - to:
            uri: camunda://cancelProcess
```

```xml
<route>
  <from uri="direct:cancel"/>
  <setBody>
    <simple>{"process_instance_key": 123}</simple>
  </setBody>
  <to uri="camunda://cancelProcess"/>
</route>
```

-   publishMessage
    

-   Java
    
-   YAML
    
-   XML
    

```java
from("direct:message")
    .process(exchange -> {
        MessageRequest request = new MessageRequest();
        request.setCorrelationKey("messageKey");
        request.setTimeToLive(100);
        request.setVariables(new HashMap<String,Object>());
        request.setName("MessageName");
        exchange.getIn().setBody(request);
    })
    .to("camunda://publishMessage");
```

```yaml
- route:
    from:
      uri: direct:message
      steps:
        - setBody:
            simple: '{"name":"MessageName","correlation_key":"messageKey","time_to_live":100,"variables":{}}'
        - to:
            uri: camunda://publishMessage
```

```xml
<route>
  <from uri="direct:message"/>
  <setBody>
    <simple>{"name":"MessageName","correlation_key":"messageKey","time_to_live":100,"variables":{}}</simple>
  </setBody>
  <to uri="camunda://publishMessage"/>
</route>
```

-   deployResource
    

-   Java
    
-   YAML
    
-   XML
    

```java
from("direct:deploy")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelCamundaResourceName", "process.bpmn");
        exchange.getIn().setBody(content.getBytes());
    })
    .to("camunda://deployResource");
```

```yaml
- route:
    from:
      uri: direct:deploy
      steps:
        - setHeader:
            name: CamelCamundaResourceName
            simple: "process.bpmn"
        - to:
            uri: camunda://deployResource
```

```xml
<route>
  <from uri="direct:deploy"/>
  <setHeader name="CamelCamundaResourceName">
    <simple>process.bpmn</simple>
  </setHeader>
  <to uri="camunda://deployResource"/>
</route>
```

### Consumer Endpoints

 
| Endpoint | Description |
| --- | --- |
| worker | Registers a job worker for a job type and provides messages for available jobs. |

camel-camunda creates a route exchange per job type with a job in the body. The `CamelCamundaJobKey` header is set automatically for each job.

#### Auto-Complete / Auto-Fail

The worker consumer follows the standard job worker pattern:

-   If the route completes successfully, the job is **automatically completed**. If the exchange body is a `Map`, those entries are passed as output variables.
    
-   If the route throws an exception, the job is **automatically failed** with the exception message. The retry count is decremented by one.
    
-   If the route explicitly calls `completeJob`, `failJob`, or `throwError`, the auto-complete is **skipped** (the consumer detects this via the `CamundaJobHandled` exchange property).
    

**Basic Example** — process a job (auto-completed on success):

-   Java
    
-   YAML
    
-   XML
    

```java
from("camunda://worker?jobType=myJobType&timeout=20")
    .process(exchange -> {
        JobWorkerMessage body = exchange.getIn().getBody(JobWorkerMessage.class);
        if (body != null) {
            long key = body.getKey();
            String type = body.getType();
            Map<String,String> customHeaders = body.getCustomHeaders();
            long processInstanceKey = body.getProcessInstanceKey();
            String bpmnProcessId = body.getBpmnProcessId();
            Map<String,Object> variables = body.getVariables();
        }
    });
```

```yaml
- route:
    from:
      uri: camunda://worker
      parameters:
        jobType: myJobType
        timeout: 20
      steps:
        - log:
            message: "Received job ${header.CamelCamundaJobKey}"
```

```xml
<route>
  <from uri="camunda://worker?jobType=myJobType&amp;timeout=20"/>
  <log message="Received job ${header.CamelCamundaJobKey}"/>
</route>
```

**Returning output variables** — set the body to a `Map` to pass variables back:

-   Java
    
-   XML
    
-   YAML
    

```java
from("camunda://worker?jobType=myJobType&timeout=20")
    .setBody(simple("${map('approved',true)}"))
    .to("camunda://completeJob");
```

```xml
<route>
  <from uri="camunda://worker?jobType=myJobType&amp;timeout=20"/>
  <setBody>
    <simple>${map('approved',true)}</simple>
  </setBody>
  <to uri="camunda://completeJob"/>
</route>
```

```yaml
- route:
    from:
      uri: camunda://worker
      parameters:
        jobType: myJobType
        timeout: 20
    steps:
      - setBody:
          simple: "${map('approved',true)}"
      - to:
          uri: camunda://completeJob
```

#### Advanced Worker Flow Examples

For advanced scenarios, you can explicitly call `completeJob`, `failJob`, or `throwError` in the route. When you do, the consumer skips auto-complete/auto-fail.

-   **Throw a business error** — signals a BPMN error with an error code and message:
    

-   Java
    
-   YAML
    
-   XML
    

```java
from("camunda://worker?jobType=myJobType&timeout=20")
    .setHeader("CamelCamundaErrorCode", constant("INVALID_DATA"))
    .setHeader("CamelCamundaErrorMessage", constant("Data validation failed"))
    .to("camunda://throwError");
```

```yaml
- route:
    from:
      uri: camunda://worker
      parameters:
        jobType: myJobType
        timeout: 20
      steps:
        - setHeader:
            name: CamelCamundaErrorCode
            constant: INVALID_DATA
        - setHeader:
            name: CamelCamundaErrorMessage
            constant: "Data validation failed"
        - to:
            uri: camunda://throwError
```

```xml
<route>
  <from uri="camunda://worker?jobType=myJobType&amp;timeout=20"/>
  <setHeader name="CamelCamundaErrorCode">
    <constant>INVALID_DATA</constant>
  </setHeader>
  <setHeader name="CamelCamundaErrorMessage">
    <constant>Data validation failed</constant>
  </setHeader>
  <to uri="camunda://throwError"/>
</route>
```

## Migrating from camel-zeebe

The `camel-camunda` component is the successor of `camel-zeebe`. Key differences:

-   Uses the new `io.camunda:camunda-client-java` library instead of `io.camunda:zeebe-client-java`
    
-   URI scheme changes from `zeebe:` to `camunda:`
    
-   Component options use `grpcAddress`/`restAddress` instead of `gatewayHost`/`gatewayPort`
    
-   Supports Camunda SaaS via `clusterId`, `region`, `clientId`, `clientSecret`
    
-   Consumer `jobKey` parameter is renamed to `jobType` (for clarity)
    
-   Request/response model classes are in `org.apache.camel.component.camunda.model` instead of `org.apache.camel.component.zeebe.model`