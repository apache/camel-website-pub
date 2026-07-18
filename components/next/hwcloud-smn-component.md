# Huawei Simple Message Notification (SMN)

**Since Camel 3.8**

**Only producer is supported**

Huawei Cloud Simple Message Notification (SMN) component allows you to integrate with [SMN](https://www.huaweicloud.com/intl/en-us/product/smn.md) provided by Huawei Cloud.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huaweicloud-smn</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

To send a notification.

hwcloud-smn:service\[?options\]

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

The Huawei Simple Message Notification (SMN) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Huawei Simple Message Notification (SMN) endpoint is configured using URI syntax:

hwcloud-smn:smnService

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **smnService** (producer) | **Required** Name of SMN service to invoke. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessKey** (producer) | **Required** Access key for the cloud user. |  | String |
| **endpoint** (producer) | Fully qualified smn service url. Carries higher precedence than region parameter based client initialization. |  | String |
| **messageTtl** (producer) | TTL for published message. | 3600 | int |
| **operation** (producer) | **Required** Name of operation to perform. |  | String |
| **projectId** (producer) | **Required** Cloud project ID. |  | String |
| **proxyHost** (producer) | Proxy server ip/hostname. |  | String |
| **proxyPassword** (producer) | Proxy authentication password. |  | String |
| **proxyPort** (producer) | Proxy server port. |  | int |
| **proxyUser** (producer) | Proxy authentication user. |  | String |
| **region** (producer) | **Required** SMN service region. This is lower precedence than endpoint based configuration. |  | String |
| **secretKey** (producer) | **Required** Secret key for the cloud user. |  | String |
| **serviceKeys** (producer) | Configuration object for cloud service authentication. |  | ServiceKeys |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ignoreSslVerification** (security) | Ignore SSL verification. | false | boolean |

## Usage

### Message properties evaluated by the SMN producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudSmnSubject` | `String` | Subject tag for the outgoing notification |
| `CamelHwCloudSmnTopic` | `String` | Smn topic into which the message is to be posted |
| `CamelHwCloudSmnMessageTtl` | `Integer` | Validity of the posted notification message |
| `CamelHwCloudSmnTemplateTags` | `Map<String, String>` | Contains `K,V` pairs of tags and values when using operation `publishAsTemplatedMessage` |
| `CamelHwCloudSmnTemplateName` | `String` | Name of the template to use while using operation `publishAsTemplatedMessage` |

### Message properties set by the SMN producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudSmnMesssageId` | `String` | Unique message id returned by Simple Message Notification server after processing the request |
| `CamelHwCloudSmnRequestId` | `String` | Unique request id returned by Simple Message Notification server after processing the request |

### Supported list of smn services and corresponding operations

 
| Service | Operations |
| --- | --- |
| `publishMessageService` | publishAsTextMessage, publishAsTemplatedMessage |

### Inline Configuration of route

#### publishAsTextMessage

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:triggerRoute")
    .setProperty(SmnProperties.NOTIFICATION_SUBJECT, constant("Notification Subject"))
    .setProperty(SmnProperties.NOTIFICATION_TOPIC_NAME, constant("reji-test"))
    .setProperty(SmnProperties.NOTIFICATION_TTL, constant(60))
    .to("hwcloud-smn:publishMessageService?operation=publishAsTextMessage&accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4");
```

```xml
<route>
  <from uri="direct:triggerRoute"/>
  <setProperty name="CamelHwCloudSmnSubject">
    <constant>this is my subjectline</constant>
  </setProperty>
  <setProperty name="CamelHwCloudSmnTopic">
    <constant>reji-test</constant>
  </setProperty>
  <setProperty name="CamelHwCloudSmnMessageTtl">
    <constant>60</constant>
  </setProperty>
  <to uri="hwcloud-smn:publishMessageService?operation=publishAsTextMessage&amp;accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:triggerRoute
      steps:
        - setProperty:
            name: CamelHwCloudSmnSubject
            expression:
              constant:
                expression: this is my subjectline
        - setProperty:
            name: CamelHwCloudSmnTopic
            expression:
              constant:
                expression: reji-test
        - setProperty:
            name: CamelHwCloudSmnMessageTtl
            expression:
              constant:
                expression: "60"
        - to:
            uri: hwcloud-smn:publishMessageService
            parameters:
              operation: publishAsTextMessage
              accessKey: "*********"
              secretKey: "********"
              projectId: 9071a38e7f6a4ba7b7bcbeb7d4ea6efc
              region: cn-north-4
```

### publishAsTemplatedMessage

_Java-only: requires Java Map variable for template tags_

```java
from("direct:triggerRoute")
.setProperty("CamelHwCloudSmnSubject", constant("This is my subjectline"))
.setProperty("CamelHwCloudSmnTopic", constant("reji-test"))
.setProperty("CamelHwCloudSmnMessageTtl", constant(60))
.setProperty("CamelHwCloudSmnTemplateTags", constant(tags))
.setProperty("CamelHwCloudSmnTemplateName", constant("hello-template"))
.to("hwcloud-smn:publishMessageService?operation=publishAsTemplatedMessage&accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

### Using ServiceKey configuration Bean

Access key and secret keys are required to authenticate against cloud smn service. You can avoid having them being exposed and scattered over in your endpoint uri by wrapping them inside a bean of class `` `org.apache.camel.component.huaweicloud.smn.models.ServiceKeys` ``. Add it to the registry and let camel look it up by referring the object via endpoint query parameter `` `serviceKeys` ``. Check the following code snippets

```xml
<bean id="myServiceKeyConfig" class="org.apache.camel.component.huaweicloud.smn.models.ServiceKeys">
   <property name="accessKey" value="your_access_key" />
   <property name="secretKey" value="your_secret_key" />
</bean>
```

_Java-only: requires Java constants and test configuration properties_

```java
from("direct:triggerRoute")
 .setProperty(SmnProperties.NOTIFICATION_SUBJECT, constant("Notification Subject"))
 .setProperty(SmnProperties.NOTIFICATION_TOPIC_NAME, constant(testConfiguration.getProperty("topic")))
 .setProperty(SmnProperties.NOTIFICATION_TTL, constant(60))
 .to("hwcloud-smn:publishMessageService?operation=publishAsTextMessage&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4&serviceKeys=#myServiceKeyConfig")
```