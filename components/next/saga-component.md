# Saga

**Since Camel 2.21**

**Only producer is supported**

The Saga component provides a bridge to execute custom actions within a route using the Saga EIP.

The component should be used for advanced tasks, such as deciding to complete or compensate a Saga with completionMode set to **MANUAL**.

Refer to the [Saga EIP](eips/saga-eip.md) documentation for help on using sagas in common scenarios.

## URI format

saga:action

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

The Saga component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Saga endpoint is configured using URI syntax:

saga:action

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
**Required** Action to execute (complete or compensate).

Enum values:

-   COMPLETE
    
-   COMPENSATE
    





 |  | SagaEndpointAction |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Saga component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **Long-Running-Action** (producer) Constant: [`SAGA_LONG_RUNNING_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-saga/latest/org/apache/camel/component/saga/SagaConstants.html#SAGA_LONG_RUNNING_ACTION) | The long running action. |  | String |

## Message Body

The message body at each side of the Saga component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
 |
| **Producer output** | `unchanged` | Unchanged: the saga service calls the completion or compensation endpoints with messages of its own. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

The two endpoints are `saga:complete` and `saga:compensate`. A route that is part of a saga with the completion mode `MANUAL` sends to one of them to end the saga. Camel then calls the completion or the compensation endpoint of the saga.

The example below uses the in-memory saga service, which is not meant for production. The first route starts a saga for an order and asks for the payment. The second route gets the payment result, in the same saga: it completes the saga when the order is paid, and compensates it otherwise. The `orderId` option is a header in the completion and compensation routes.

```yaml
- beans:
    - name: sagaService
      type: org.apache.camel.saga.InMemorySagaService
- route:
    from:
      uri: direct:order
      steps:
        - saga:
            completionMode: MANUAL
            timeout: 1m
            completion: direct:orderCompleted
            compensation: direct:orderCancelled
            option:
              - key: orderId
                expression:
                  simple:
                    expression: "${header.orderId}"
        - to:
            uri: seda:payment
- route:
    from:
      uri: seda:paymentResult
      steps:
        - saga:
            propagation: MANDATORY
        - choice:
            when:
              - expression:
                  simple:
                    expression: "${body} == 'paid'"
                steps:
                  - to:
                      uri: saga:complete
            otherwise:
              steps:
                - to:
                    uri: saga:compensate
```