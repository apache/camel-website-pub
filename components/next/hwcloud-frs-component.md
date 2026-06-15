# Huawei Cloud Face Recognition Service (FRS)

**Since Camel 3.15**

**Only producer is supported**

Huawei Cloud Face Recognition Service component allows you to integrate with [Face Recognition Service](https://support.huaweicloud.com/intl/en-us/productdesc-face/face_01_0001.md) provided by Huawei Cloud.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huaweicloud-frs</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```text
hwcloud-frs:operation[?options]
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

The Huawei Cloud Face Recognition Service (FRS) component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Huawei Cloud Face Recognition Service (FRS) endpoint is configured using URI syntax:

hwcloud-frs:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | **Required** Name of Face Recognition operation to perform, including faceDetection, faceVerification and faceLiveDetection. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessKey** (producer) | **Required** Access key for the cloud user. |  | String |
| **actions** (producer) | This param is mandatory when the operation is faceLiveDetection, indicating the action code sequence list. Actions are separated by commas (,). Currently, the following actions are supported: 1: Shake the head to the left. 2: Shake the head to the right. 3: Nod the head. 4: Mouth movement. |  | String |
| **actionTimes** (producer) | This param can be used when the operation is faceLiveDetection, indicating the action time array. The length of the array is the same as the number of actions. Each item contains the start time and end time of the action in the corresponding sequence. The unit is the milliseconds from the video start time. |  | String |
| **anotherImageBase64** (producer) | This param can be used when operation is faceVerification, indicating the Base64 character string converted from the other image. It needs to be configured if imageBase64 is set. The image size cannot exceed 10 MB. The image resolution of the narrow sides must be greater than 15 pixels, and that of the wide sides cannot exceed 4096 pixels. The supported image formats include JPG, PNG, and BMP. |  | String |
| **anotherImageFilePath** (producer) | This param can be used when operation is faceVerification, indicating the local file path of the other image. It needs to be configured if imageFilePath is set. Image size cannot exceed 8 MB, and it is recommended that the image size be less than 1 MB. |  | String |
| **anotherImageUrl** (producer) | This param can be used when operation is faceVerification, indicating the URL of the other image. It needs to be configured if imageUrl is set. The options are as follows: 1.HTTP/HTTPS URLs on the public network 2.OBS URLs. To use OBS data, authorization is required, including service authorization, temporary authorization, and anonymous public authorization. For details, see Configuring the Access Permission of OBS. |  | String |
| **endpoint** (producer) | Fully qualified Face Recognition service url. Carries higher precedence than region based configuration. |  | String |
| **imageBase64** (producer) | This param can be used when operation is faceDetection or faceVerification, indicating the Base64 character string converted from an image. Any one of imageBase64, imageUrl and imageFilePath needs to be set, and the priority is imageBase64 imageUrl imageFilePath. The Image size cannot exceed 10 MB. The image resolution of the narrow sides must be greater than 15 pixels, and that of the wide sides cannot exceed 4096 pixels. The supported image formats include JPG, PNG, and BMP. |  | String |
| **imageFilePath** (producer) | This param can be used when operation is faceDetection or faceVerification, indicating the local image file path. Any one of imageBase64, imageUrl and imageFilePath needs to be set, and the priority is imageBase64 imageUrl imageFilePath. Image size cannot exceed 8 MB, and it is recommended that the image size be less than 1 MB. |  | String |
| **imageUrl** (producer) | This param can be used when operation is faceDetection or faceVerification, indicating the URL of an image. Any one of imageBase64, imageUrl and imageFilePath needs to be set, and the priority is imageBase64 imageUrl imageFilePath. The options are as follows: 1.HTTP/HTTPS URLs on the public network 2.OBS URLs. To use OBS data, authorization is required, including service authorization, temporary authorization, and anonymous public authorization. For details, see Configuring the Access Permission of OBS. |  | String |
| **projectId** (producer) | **Required** Cloud project ID. |  | String |
| **proxyHost** (producer) | Proxy server ip/hostname. |  | String |
| **proxyPassword** (producer) | Proxy authentication password. |  | String |
| **proxyPort** (producer) | Proxy server port. |  | int |
| **proxyUser** (producer) | Proxy authentication user. |  | String |
| **region** (producer) | **Required** Face Recognition service region. Currently only cn-north-1 and cn-north-4 are supported. This is lower precedence than endpoint based configuration. |  | String |
| **secretKey** (producer) | **Required** Secret key for the cloud user. |  | String |
| **serviceKeys** (producer) | Configuration object for cloud service authentication. |  | ServiceKeys |
| **videoBase64** (producer) | This param can be used when operation is faceLiveDetection, indicating the Base64 character string converted from a video. Any one of videoBase64, videoUrl and videoFilePath needs to be set, and the priority is videoBase64 videoUrl videoFilePath. Requirements are as follows: 1.The video size after Base64 encoding cannot exceed 8 MB. It is recommended that the video file be compressed to 200 KB to 2 MB on the client. 2.The video duration must be 1 to 15 seconds. 3.The recommended frame rate is 10 fps to 30 fps. 4.The encapsulation format can be MP4, AVI, FLV, WEBM, ASF, or MOV. 5.The video encoding format can be H.261, H.263, H.264, HEVC, VC-1, VP8, VP9, or WMV3. |  | String |
| **videoFilePath** (producer) | This param can be used when operation is faceLiveDetection, indicating the local video file path. Any one of videoBase64, videoUrl and videoFilePath needs to be set, and the priority is videoBase64 videoUrl videoFilePath. The video requirements are as follows: 1.The size of a video file cannot exceed 8 MB. It is recommended that the video file be compressed to 200 KB to 2 MB on the client. 2.The video duration must be 1 to 15 seconds. 3.The recommended frame rate is 10 fps to 30 fps. 4.The encapsulation format can be MP4, AVI, FLV, WEBM, ASF, or MOV. 5.The video encoding format can be H.261, H.263, H.264, HEVC, VC-1, VP8, VP9, or WMV3. |  | String |
| **videoUrl** (producer) | This param can be used when operation is faceLiveDetection, indicating the URL of a video. Any one of videoBase64, videoUrl and videoFilePath needs to be set, and the priority is videoBase64 videoUrl videoFilePath. Currently, only the URL of an OBS bucket on HUAWEI CLOUD is supported and FRS must have the permission to read data in the OBS bucket. For details about how to enable the read permission, see Service Authorization. The video requirements are as follows: 1.The video size after Base64 encoding cannot exceed 8 MB. 2.The video duration must be 1 to 15 seconds. 3.The recommended frame rate is 10 fps to 30 fps. 4.The encapsulation format can be MP4, AVI, FLV, WEBM, ASF, or MOV. 5.The video encoding format can be H.261, H.263, H.264, HEVC, VC-1, VP8, VP9, or WMV3. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ignoreSslVerification** (security) | Ignore SSL verification. | false | boolean |
> **Note**
> When using imageBase64 or videoBase64 option, we suggest you use RAW(base64\_value) to avoid encoding issue.

## Usage

### Message properties evaluated by the Face Recognition Service producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudFrsImageBase64` | `String` | The Base64 character string converted from an image. This property can be used when the operation is faceDetection or faceVerification. |
| `CamelHwCloudFrsImageUrl` | `String` | The URL of an image. This property can be used when the operation is faceDetection or faceVerification. |
| `CamelHwCloudFrsImageFilePath` | `String` | The local file path of an image. This property can be used when the operation is faceDetection or faceVerification. |
| `CamelHwCloudFrsAnotherImageBase64` | `String` | The Base64 character string converted from another image. This property can be used when the operation is faceVerification. |
| `CamelHwCloudFrsAnotherImageUrl` | `String` | The URL of another image. This property can be used when the operation is faceVerification. |
| `CamelHwCloudFrsAnotherImageFilePath` | `String` | The local file path of another image. This property can be used when the operation is faceVerification. |
| `CamelHwCloudFrsVideoBase64` | `String` | The Base64 character string converted from a video. This property can be used when the operation is faceLiveDetection. |
| `CamelHwCloudFrsVideoUrl` | `String` | The URL of a video. This property can be used when the operation is faceLiveDetection. |
| `CamelHwCloudFrsVideoFilePath` | `String` | The local file path of a video. This property can be used when the operation is faceLiveDetection. |
| `CamelHwCloudFrsVideoActions` | `String` | The action code sequence list. This property can be used when the operation is faceLiveDetection. |
| `CamelHwCloudFrsVideoActionTimes` | `String` | The action time array. This property is used when the operation is faceLiveDetection. |

### List of Supported Operations

-   faceDetection - detect, locate, and analyze the face in an input image, and output the key facial points and attributes.
    
-   faceVerification - compare two faces to verify whether they belong to the same person and return the confidence level
    
-   faceLiveDetection - determine whether a person in a video is alive by checking whether the person’s actions in the video are consistent with those in the input action list
    

### Inline Configuration of route

#### faceDetection

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:triggerRoute")
  .setProperty(FaceRecognitionProperties.FACE_IMAGE_URL, constant("https://xxxx"))
  .to("hwcloud-frs:faceDetection?accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

```xml
<route>
  <from uri="direct:triggerRoute"/>
  <setProperty name="CamelHwCloudFrsImageUrl">
    <constant>https://xxxx</constant>
  </setProperty>
  <to uri="hwcloud-frs:faceDetection?accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:triggerRoute
      steps:
        - setProperty:
            name: CamelHwCloudFrsImageUrl
            expression:
              constant:
                expression: https://xxxx
        - to:
            uri: hwcloud-frs:faceDetection
            parameters:
              accessKey: "*********"
              secretKey: "********"
              projectId: 9071a38e7f6a4ba7b7bcbeb7d4ea6efc
              region: cn-north-4
```

#### faceVerification

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:triggerRoute")
  .setProperty(FaceRecognitionProperties.FACE_IMAGE_BASE64, constant("/9j/4AAQSkZJRgABAQEASABIAAD/..."))
  .setProperty(FaceRecognitionProperties.ANOTHER_FACE_IMAGE_BASE64, constant("/9j/4AAQSkZJRgABAQAAAQABAAD/..."))
  .to("hwcloud-frs:faceVerification?accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

```xml
<route>
  <from uri="direct:triggerRoute"/>
  <setProperty name="CamelHwCloudFrsImageBase64">
    <constant>/9j/4AAQSkZJRgABAQEASABIAAD/...</constant>
  </setProperty>
  <setProperty name="CamelHwCloudFrsAnotherImageBase64">
    <constant>/9j/4AAQSkZJRgABAQAAAQABAAD/...</constant>
  </setProperty>
  <to uri="hwcloud-frs:faceVerification?accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:triggerRoute
      steps:
        - setProperty:
            name: CamelHwCloudFrsImageBase64
            expression:
              constant:
                expression: "/9j/4AAQSkZJRgABAQEASABIAAD/..."
        - setProperty:
            name: CamelHwCloudFrsAnotherImageBase64
            expression:
              constant:
                expression: "/9j/4AAQSkZJRgABAQAAAQABAAD/..."
        - to:
            uri: hwcloud-frs:faceVerification
            parameters:
              accessKey: "*********"
              secretKey: "********"
              projectId: 9071a38e7f6a4ba7b7bcbeb7d4ea6efc
              region: cn-north-4
```

#### faceLiveDetection

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:triggerRoute")
  .setProperty(FaceRecognitionProperties.FACE_VIDEO_FILE_PATH, constant("/tmp/video.mp4"))
  .setProperty(FaceRecognitionProperties.FACE_VIDEO_ACTIONS, constant("1,3,2"))
  .to("hwcloud-frs:faceLiveDetection?accessKey=*********&secretKey=********&projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4")
```

```xml
<route>
  <from uri="direct:triggerRoute"/>
  <setProperty name="CamelHwCloudFrsVideoFilePath">
    <constant>/tmp/video.mp4</constant>
  </setProperty>
  <setProperty name="CamelHwCloudFrsVideoActions">
    <constant>1,3,2</constant>
  </setProperty>
  <to uri="hwcloud-frs:faceLiveDetection?accessKey=*********&amp;secretKey=********&amp;projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:triggerRoute
      steps:
        - setProperty:
            name: CamelHwCloudFrsVideoFilePath
            expression:
              constant:
                expression: /tmp/video.mp4
        - setProperty:
            name: CamelHwCloudFrsVideoActions
            expression:
              constant:
                expression: "1,3,2"
        - to:
            uri: hwcloud-frs:faceLiveDetection
            parameters:
              accessKey: "*********"
              secretKey: "********"
              projectId: 9071a38e7f6a4ba7b7bcbeb7d4ea6efc
              region: cn-north-4
```

## Spring Boot Auto-Configuration

When using hwcloud-frs with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-huaweicloud-frs-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hwcloud-frs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hwcloud-frs.enabled** | Whether to enable auto configuration of the hwcloud-frs component. This is enabled by default. |  | Boolean |
| **camel.component.hwcloud-frs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |