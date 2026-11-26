# Alibaba Short Message Service (SMS)

**Since Camel 4.23**

**Only producer is supported**

The Alibaba Cloud SMS component allows you to send SMS messages using approved templates and sign names.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-sms</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
alibaba-sms:operation[?options]
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

The Alibaba Short Message Service (SMS) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Short Message Service (SMS) endpoint is configured using URI syntax:

alibaba-sms:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation that the producer performs. The CamelAlibabaSmsOperation header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option.

Enum values:

-   sendSms
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | The endpoint of Short Message Service, which is a host name without http:// or https://. The producer sends requests to it over HTTPS. If not set, the region option determines the endpoint, and one of the two is required. Not used when the smsClient option is set or autowired. |  | String |
| **outId** (producer) | The external transaction ID of the SMS message. The CamelAlibabaSmsOutId header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no external transaction ID to the request. |  | String |
| **phoneNumbers** (producer) | The phone numbers of the recipients, which are separated by commas. Short Message Service accepts at most 1000 phone numbers. The CamelAlibabaSmsPhoneNumbers header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **region** (producer) | The region ID of Short Message Service, for example cn-hangzhou. Only used when the endpoint option is not set, to determine the endpoint of Short Message Service. One of the two options is required. Not used when the smsClient option is set or autowired. |  | String |
| **signName** (producer) | The sign name of the SMS message. The value must be an approved sign name. The CamelAlibabaSmsSignName header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **templateCode** (producer) | The template code of the SMS message. The value must be the code of an approved template. The CamelAlibabaSmsTemplateCode header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required. |  | String |
| **templateParam** (producer) | The template parameters of the SMS message as a JSON string. The JSON string must provide a value for each variable of the template. The CamelAlibabaSmsTemplateParam header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no template parameters to the request. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **smsClient** (advanced) | **Autowired** To use a custom com.aliyun.dysmsapi20170525.Client. The producer sends its requests with this client, and the region, endpoint, accessKey, secretKey and serviceKeys options are not used. If no client is set or autowired, the Camel endpoint creates a client from these options. It creates this client when the producer processes its first message. |  | Client |
| **accessKey** (security) | The AccessKey ID of the AccessKey pair for the requests that the producer sends to Short Message Service. If not set, the accessKey of the serviceKeys option is used, and one of the two is required. Not used when the smsClient option is set or autowired. |  | String |
| **secretKey** (security) | The AccessKey secret of the AccessKey pair for the requests that the producer sends to Short Message Service. If not set, the secretKey of the serviceKeys option is used, and one of the two is required. Not used when the smsClient option is set or autowired. |  | String |
| **serviceKeys** (security) | The AccessKey pair as an org.apache.camel.component.alibaba.common.models.ServiceKeys. Its accessKey is the AccessKey ID and its secretKey is the AccessKey secret. Each of the two is used when the option of the same name is not set. Not used when the smsClient option is set or autowired. |  | ServiceKeys |

## Message Headers

The Alibaba Short Message Service (SMS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaSmsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#OPERATION) | 
The operation that the producer performs. This header replaces the operation option. If this header is not set, an exchange property of the same name replaces the operation option.

Enum values:

-   sendSms
    





 |  | String |
| **CamelAlibabaSmsPhoneNumbers** (producer) Constant: [`PHONE_NUMBERS`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#PHONE_NUMBERS) | The phone numbers of the recipients, which are separated by commas. Short Message Service accepts at most 1000 phone numbers. This header replaces the phoneNumbers option. If this header is not set, an exchange property of the same name replaces the phoneNumbers option. |  | String |
| **CamelAlibabaSmsSignName** (producer) Constant: [`SIGN_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#SIGN_NAME) | The sign name of the SMS message. The value must be an approved sign name. This header replaces the signName option. If this header is not set, an exchange property of the same name replaces the signName option. |  | String |
| **CamelAlibabaSmsTemplateCode** (producer) Constant: [`TEMPLATE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#TEMPLATE_CODE) | The template code of the SMS message. The value must be the code of an approved template. This header replaces the templateCode option. If this header is not set, an exchange property of the same name replaces the templateCode option. |  | String |
| **CamelAlibabaSmsTemplateParam** (producer) Constant: [`TEMPLATE_PARAM`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#TEMPLATE_PARAM) | The template parameters of the SMS message as a JSON string. The JSON string must provide a value for each variable of the template. This header replaces the templateParam option. If this header is not set, an exchange property of the same name replaces the templateParam option. |  | String |
| **CamelAlibabaSmsOutId** (producer) Constant: [`OUT_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#OUT_ID) | The external transaction ID of the SMS message. This header replaces the outId option. If this header is not set, an exchange property of the same name replaces the outId option. |  | String |
| **CamelAlibabaSmsRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-sms/latest/org/apache/camel/component/alibaba/sms/constants/SMSHeaders.html#REQUEST_ID) | The request ID that Short Message Service returns in the response to the operation. The producer sets it, unless the exchange fails. |  | String |

## Message Body

The message body at each side of the Alibaba Short Message Service (SMS) component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | Not used: sendSms takes the phone numbers, sign name, template code and template parameters from options or headers, such as CamelAlibabaSmsTemplateParam. |
| **Producer output** | `map` | A Map of the response: the statusCode, and the code, message, bizId and requestId the service returns. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Operations

The component supports the following operations:

-   `sendSms` - send an SMS message (producer)
    

### Producer example

-   Java
    
-   YAML
    

```java
from("direct:start")
    .to("alibaba-sms:sendSms?phoneNumbers=13800138000&signName=MySign&templateCode=SMS_123456&templateParam={\"code\":\"1234\"}&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: alibaba-sms:sendSms
            parameters:
              phoneNumbers: "13800138000"
              signName: MySign
              templateCode: SMS_123456
              templateParam: '{"code":"1234"}'
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-sms` module.