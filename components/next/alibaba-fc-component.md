# Alibaba Function Compute (FC)

**Since Camel 4.23**

**Only producer is supported**

The Alibaba Cloud Function Compute (FC) component allows you to invoke functions and retrieve function metadata.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-fc</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
alibaba-fc:operation[?options]
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

The Alibaba Function Compute (FC) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Function Compute (FC) endpoint is configured using URI syntax:

alibaba-fc:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation that the producer performs. The CamelAlibabaFcOperation header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option.

Enum values:

-   invokeFunction
    
-   getFunction
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | **Required** The endpoint of Function Compute, which is a host name without http:// or https://. It contains the ID of the Alibaba Cloud account, as in 12345.cn-hangzhou.fc.aliyuncs.com. The producer sends requests to it over HTTPS. The region option does not determine the endpoint, so this option is required. Not used when the fcClient option is set or autowired. |  | String |
| **functionName** (producer) | The name of the function. The CamelAlibabaFcFunctionName header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **qualifier** (producer) | The version or alias of the service. The CamelAlibabaFcQualifier header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no version or alias to the request. |  | String |
| **region** (producer) | **Deprecated** The region ID of Function Compute, for example cn-hangzhou. The producer does not use it. Deprecation note: Use the endpoint option, which contains the region. |  | String |
| **serviceName** (producer) | The name of the service that contains the function. The CamelAlibabaFcServiceName header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **fcClient** (advanced) | **Autowired** To use a custom com.aliyun.fc\_open20210406.Client. The producer sends its requests with this client, and the endpoint, accessKey, secretKey and serviceKeys options are not used. If no client is set or autowired, the Camel endpoint creates a client from these options. It creates this client when the producer processes its first message. |  | Client |
| **accessKey** (security) | The AccessKey ID of the AccessKey pair for the requests that the producer sends to Function Compute. If not set, the accessKey of the serviceKeys option is used, and one of the two is required. Not used when the fcClient option is set or autowired. |  | String |
| **secretKey** (security) | The AccessKey secret of the AccessKey pair for the requests that the producer sends to Function Compute. If not set, the secretKey of the serviceKeys option is used, and one of the two is required. Not used when the fcClient option is set or autowired. |  | String |
| **serviceKeys** (security) | The AccessKey pair as an org.apache.camel.component.alibaba.common.models.ServiceKeys. Its accessKey is the AccessKey ID and its secretKey is the AccessKey secret. Each of the two is used when the option of the same name is not set. Not used when the fcClient option is set or autowired. |  | ServiceKeys |

## Message Headers

The Alibaba Function Compute (FC) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaFcOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#OPERATION) | The operation that the producer performs. This header replaces the operation option. If this header is not set, an exchange property of the same name replaces the operation option. |  | String |
| **CamelAlibabaFcServiceName** (producer) Constant: [`SERVICE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#SERVICE_NAME) | The name of the service that contains the function. This header replaces the serviceName option. If this header is not set, an exchange property of the same name replaces the serviceName option. |  | String |
| **CamelAlibabaFcFunctionName** (producer) Constant: [`FUNCTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#FUNCTION_NAME) | The name of the function. This header replaces the functionName option. If this header is not set, an exchange property of the same name replaces the functionName option. |  | String |
| **CamelAlibabaFcQualifier** (producer) Constant: [`QUALIFIER`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#QUALIFIER) | The version or alias of the service. This header replaces the qualifier option. If this header is not set, an exchange property of the same name replaces the qualifier option. |  | String |
| **CamelAlibabaFcRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#REQUEST_ID) | The request ID that Function Compute returns in the response to invokeFunction. The producer sets it for invokeFunction, unless the exchange fails. |  | String |
| **CamelAlibabaFcStatusCode** (producer) Constant: [`STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-fc/latest/org/apache/camel/component/alibaba/fc/constants/FCHeaders.html#STATUS_CODE) | The HTTP status code of the response to the operation. The producer sets it, unless the exchange fails. |  | Integer |

## Message Body

The message body at each side of the Alibaba Function Compute (FC) component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
invokeFunction sends the body as the payload of the function: text in UTF-8, bytes as they are, a stream or a file as its bytes, so binary data is kept, and no body as an empty payload. A Map or a POJO fails, as it does not convert to bytes, so marshal it first. getFunction does not use the body.

-   With `operation=invokeFunction`: `text`, `bytes`, `stream`, `file` or `null`
    





 |
| **Producer output** | `map` (`java.util.Map`) | A Map: for invokeFunction the statusCode, the headers and the body of the response, which holds the payload the function returns as bytes, with the status code in the CamelAlibabaFcStatusCode header too; for getFunction the fields of the function, such as functionName, runtime and handler. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Operations

The component supports the following operations:

-   `invokeFunction` - invoke a function with a payload (producer)
    
-   `getFunction` - retrieve function metadata (producer)
    

### Payload of invokeFunction

The message body is the payload of the function. A `String` is sent in UTF-8, and a `byte[]`, an `InputStream` or a file is sent as its bytes, so binary data is kept. Without a body the function is invoked with an empty payload. A `Map` or a POJO does not convert to bytes and fails with an `InvalidPayloadException`, so marshal it first, for example to JSON with `marshal().json()`.

### Endpoint of Function Compute

The `endpoint` option is the endpoint of Function Compute for your Alibaba Cloud account and region. The public endpoint has the form `<account ID>.<region ID>.fc.aliyuncs.com`, for example `12345.cn-hangzhou.fc.aliyuncs.com` for the account ID 12345 and the region cn-hangzhou. The internal endpoint has the form `<account ID>.<region ID>-internal.fc.aliyuncs.com`.

### Producer example

-   Java
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("{\"name\":\"camel\"}"))
    .to("alibaba-fc:invokeFunction?serviceName=my-service&functionName=my-function&endpoint=12345.cn-hangzhou.fc.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            expression:
              constant:
                expression: '{"name":"camel"}'
        - to:
            uri: alibaba-fc:invokeFunction
            parameters:
              serviceName: my-service
              functionName: my-function
              endpoint: 12345.cn-hangzhou.fc.aliyuncs.com
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-fc` module.