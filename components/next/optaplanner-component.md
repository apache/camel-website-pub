# OptaPlanner

**Since Camel 2.13**

**Both producer and consumer are supported**

The [OptaPlanner](http://www.optaplanner.org/) component solves the planning problem contained in a message with [OptaPlanner](http://www.optaplanner.org/). For example, feed it an unsolved Vehicle Routing problem and it solves it.

The component supports consumer listening for `SolverManager` results and producer for processing Solution and ProblemChange.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-optaplanner</artifactId>
    <version>x.x.x</version><!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

optaplanner:problemName\[?options\]

You can append query options to the URI in the following format, `?option=value&option=value&…​`

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

The OptaPlanner component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OptaPlanner endpoint is configured using URI syntax:

optaplanner:problemName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **problemName** (common) | **Required** Problem name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configFile** (common) | If SolverManager is absent from the header OptaPlannerConstants.SOLVER\_MANAGER then a SolverManager will be created using this Optaplanner config file. |  | String |
| **problemId** (common) | In case of using SolverManager : the problem id. | 1 | long |
| **solverId** (common) | Specifies the solverId to user for the solver instance key. | DEFAULT\_SOLVER | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **async** (producer) | Specifies to perform operations in async mode. | false | boolean |
| **threadPoolSize** (producer) | Specifies the thread pool size to use when async is true. | 10 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **solverManager** (advanced) | SolverManager. |  | SolverManager |

## Message Headers

The OptaPlanner component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOptaPlannerSolverId** (producer) Constant: [`SOLVER_ID`](https://javadoc.io/doc/org.apache.camel/camel-optaplanner/latest/org/apache/camel/component/optaplanner/OptaPlannerConstants.html#SOLVER_ID) | Specifies the solverId to use. |  | String |
| **CamelOptaPlannerIsAsync** (producer) Constant: [`IS_ASYNC`](https://javadoc.io/doc/org.apache.camel/camel-optaplanner/latest/org/apache/camel/component/optaplanner/OptaPlannerConstants.html#IS_ASYNC) | Specify whether to use another thread for submitting Solution instances rather than blocking the current thread. |  | Boolean |
| **CamelOptaPlannerBestSolution** (consumer) Constant: [`BEST_SOLUTION`](https://javadoc.io/doc/org.apache.camel/camel-optaplanner/latest/org/apache/camel/component/optaplanner/OptaPlannerConstants.html#BEST_SOLUTION) | The best planning solution. |  | Object |
| **CamelOptaPlannerIsSolving** (producer) Constant: [`IS_SOLVING`](https://javadoc.io/doc/org.apache.camel/camel-optaplanner/latest/org/apache/camel/component/optaplanner/OptaPlannerConstants.html#IS_SOLVING) | Is solving. |  | Boolean |
| **CamelOptaPlannerSolverManager** (producer) Constant: [`SOLVER_MANAGER`](https://javadoc.io/doc/org.apache.camel/camel-optaplanner/latest/org/apache/camel/component/optaplanner/OptaPlannerConstants.html#SOLVER_MANAGER) | The Solver Manager. |  | SolverManager |

## Message Body

The message body at each side of the OptaPlanner component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `null` | The body is empty: the new best solution is in the CamelOptaPlannerBestSolution header. Events come only from producers that solve asynchronously, with the same problemId. |
| **Producer input** | `pojo` | The planning problem: an instance of the PlanningSolution class of the solver configuration, or a ProblemChange to apply to the problem being solved. Any other body fails to solve, and no body fails. |
| **Producer output** | `pojo` or `unchanged` | The best solution found, a new instance of the problem class, with the CamelOptaPlannerIsSolving header false (also with async, the exchange waits for it); a ProblemChange leaves the body unchanged. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Message Body

Camel takes the planning problem from the message body, solves it and sets the best solution as the message body. The body supports the following use cases:

-   If the body is an instance of the `PlanningSolution` class of the solver configuration, then it is solved, either synchronously or asynchronously. In both cases the exchange continues with the best solution as the body.
    
-   If the body is an instance of `ProblemChange`, then it is added to the problem being solved with the same `problemId`, and the body is left unchanged.
    
-   Any other body fails the exchange, as the solver cannot solve it.
    

The consumer receives an exchange each time a producer solving asynchronously, with the same `problemId`, finds a new best solution. Its body is empty: the best solution is in the `CamelOptaPlannerBestSolution` header.

### Examples

Solve a planning problem on the ActiveMQ queue with OptaPlanner, passing the `SolverManager`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("optaplanner:problemName?solverManager=#solverManager");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="optaplanner:problemName?solverManager=#solverManager"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: optaplanner:problemName
            parameters:
              solverManager: "#solverManager"
```

Expose OptaPlanner as a REST service, passing the Solver configuration file:

-   Java
    
-   XML
    
-   YAML
    

```java
from("cxfrs:bean:rsServer?bindingStyle=SimpleConsumer")
    .to("optaplanner:problemName?configFile=/org/foo/barSolverConfig.xml");
```

```xml
<route>
  <from uri="cxfrs:bean:rsServer?bindingStyle=SimpleConsumer"/>
  <to uri="optaplanner:problemName?configFile=/org/foo/barSolverConfig.xml"/>
</route>
```

```yaml
- route:
    from:
      uri: cxfrs:bean:rsServer
      parameters:
        bindingStyle: SimpleConsumer
      steps:
        - to:
            uri: optaplanner:problemName
            parameters:
              configFile: /org/foo/barSolverConfig.xml
```