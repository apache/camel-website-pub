# Huawei Cloud Image Recognition

**Since Camel 3.12**

**Only producer is supported**

Huawei Cloud Image Recognition component allows you to integrate with [Image Recognition](https://www.huaweicloud.com/intl/en-us/product/image.md) provided by Huawei Cloud.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huaweicloud-imagerecognition</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```text
hwcloud-imagerecognition:operation[?options]
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

The Huawei Cloud Image Recognition component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Huawei Cloud Image Recognition endpoint is configured using URI syntax:

hwcloud-imagerecognition:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | **Required** Name of Image Recognition operation to perform, including celebrityRecognition and tagRecognition. |  | String |

### Query Parameters (17 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessKey** (producer) | **Required** Access key for the cloud user. |  | String |
| **endpoint** (producer) | Fully qualified Image Recognition service url. Carries higher precedence than region based configuration. |  | String |
| **imageContent** (producer) | Indicates the Base64 character string converted from the image. The size cannot exceed 10 MB. The image resolution of the narrow sides must be greater than 15 pixels, and that of the wide sides cannot exceed 4096 pixels.The supported image formats include JPG, PNG, and BMP. Configure either this parameter or imageUrl, and this one carries higher precedence than imageUrl. |  | String |
| **imageUrl** (producer) | Indicates the URL of an image. The options are as follows: HTTP/HTTPS URLs on the public network OBS URLs. To use OBS data, authorization is required, including service authorization, temporary authorization, and anonymous public authorization. For details, see Configuring the Access Permission of OBS. Configure either this parameter or imageContent, and this one carries lower precedence than imageContent. |  | String |
| **projectId** (producer) | **Required** Cloud project ID. |  | String |
| **proxyHost** (producer) | Proxy server ip/hostname. |  | String |
| **proxyPassword** (producer) | Proxy authentication password. |  | String |
| **proxyPort** (producer) | Proxy server port. |  | int |
| **proxyUser** (producer) | Proxy authentication user. |  | String |
| **region** (producer) | **Required** Image Recognition service region. Currently only cn-north-1 and cn-north-4 are supported. This is lower precedence than endpoint based configuration. |  | String |
| **secretKey** (producer) | **Required** Secret key for the cloud user. |  | String |
| **serviceKeys** (producer) | Configuration object for cloud service authentication. |  | ServiceKeys |
| **tagLanguage** (producer) | Indicates the language of the returned tags when the operation is tagRecognition, including zh and en. | zh | String |
| **tagLimit** (producer) | Indicates the maximum number of the returned tags when the operation is tagRecognition. | 50 | int |
| **threshold** (producer) | Indicates the threshold of confidence. When the operation is tagRecognition, this parameter ranges from 0 to 100. Tags whose confidence score is lower than the threshold will not be returned. The default value is 60. When the operation is celebrityRecognition, this parameter ranges from 0 to 1. Labels whose confidence score is lower than the threshold will not be returned. The default value is 0.48. |  | float |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ignoreSslVerification** (security) | Ignore SSL verification. | false | boolean |
> **Note**
> When using imageContent option, we suggest you use RAW(image\_base64\_value) to avoid encoding issue.

## Usage

### Message properties evaluated by the Image Recognition producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudImageContent` | `String` | The Base64 character string converted from the image |
| `CamelHwCloudImageUrl` | `String` | The URL of an image |
| `CamelHwCloudImageTagLimit` | `Integer` | The maximum number of the returned tags when the operation is tagRecognition |
| `CamelHwCloudImageTagLanguage` | `String` | The language of the returned tags when the operation is tagRecognition |
| `CamelHwCloudImageThreshold` | `Integer` | The threshold of confidence. |

### List of Supported Image Recognition Operations

-   celebrityRecognition - to analyze and identify the political figures, stars and online celebrities contained in the picture, and return the person information and face coordinates
    
-   tagRecognition - to recognize hundreds of scenes and thousands of objects and their properties in natural images
    

### Inline Configuration of route

#### celebrityRecognition

Java DSL

```java
from("direct:triggerRoute")
  .setProperty(ImageRecognitionProperties.IMAGE_URL, constant("https://xxxx"))
  .setProperty(ImageRecognitionProperties.THRESHOLD,constant(0.5))
  .to("hwcloud-imagerecognition:celebrityRecognition?accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

XML DSL

```xml
<route>
   <from uri="direct:triggerRoute" />
   <setProperty name="CamelHwCloudImageUrl">
      <constant>https://xxxx</constant>
   </setProperty>
   <setProperty name="CamelHwCloudImageThreshold">
      <constant>0.5</constant>
   </setProperty>
   <to uri="hwcloud-imagerecognition:celebrityRecognition?accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4" />
</route>
```

### tagRecognition

Java DSL

```java
from("direct:triggerRoute")
  .setProperty(ImageRecognitionProperties.IMAGE_CONTENT, constant("/9j/4AAQSkZJRgABAQEASABIAAD/2wBDAA0JCgsKCA0LCgsODg0PEyAVExISEyccHhcgLikxMC4pLSwzOko+MzZGNywtQFdBRkxOUlNSMj5aYVpQYEpRUk//..."))
  .setProperty(ImageRecognitionProperties.THRESHOLD,constant(60))
  .setProperty(ImageRecognitionProperties.TAG_LANGUAGE,constant("en"))
  .setProperty(ImageRecognitionProperties.TAG_LIMIT,constant(50))
  .to("hwcloud-imagerecognition:tagRecognition?accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

XML DSL

```xml
<route>
    <from uri="direct:triggerRoute" />
    <setProperty name="CamelHwCloudImageContent">
        <constant>/9j/4AAQSkZJRgABAQEASABIAAD/2wBDAA0JCgsKCA0LCgsODg0PEyAVExISEyccHhcgLikxMC4pLSwzOko+MzZGNywtQFdBRkxOUlNSMj5aYVpQYEpRUk//...</constant>
    </setProperty>
    <setProperty name="CamelHwCloudImageThreshold">
        <constant>60</constant>
    </setProperty>
    <setProperty name="CamelHwCloudImageTagLanguage">
        <constant>en</constant>
    </setProperty>
    <setProperty name="CamelHwCloudImageTagLimit">
        <constant>50</constant>
    </setProperty>
    <to uri="hwcloud-imagerecognition:tagRecognition?accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4" />
</route>
```

## Spring Boot Auto-Configuration

When using hwcloud-imagerecognition with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-huaweicloud-imagerecognition-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hwcloud-imagerecognition.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hwcloud-imagerecognition.enabled** | Whether to enable auto configuration of the hwcloud-imagerecognition component. This is enabled by default. |  | Boolean |
| **camel.component.hwcloud-imagerecognition.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |