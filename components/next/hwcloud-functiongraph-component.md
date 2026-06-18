# Huawei FunctionGraph

**Since Camel 3.11**

**Only producer is supported**

Huawei Cloud FunctionGraph component allows you to integrate with [FunctionGraph](https://www.huaweicloud.com/intl/en-us/product/functiongraph.md) provided by Huawei Cloud.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huaweicloud-functiongraph</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

hwcloud-functiongraph:operation\[?options\]

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

The Huawei FunctionGraph component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Huawei FunctionGraph endpoint is configured using URI syntax:

hwcloud-functiongraph:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | **Required** Operation to be performed. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | FunctionGraph url. Carries higher precedence than region parameter based client initialization. |  | String |
| **functionName** (producer) | Name of the function to invoke. |  | String |
| **functionPackage** (producer) | Functions that can be logically grouped together. | default | String |
| **projectId** (producer) | **Required** Cloud project ID. |  | String |
| **region** (producer) | **Required** FunctionGraph service region. This is lower precedence than endpoint based configuration. |  | String |
| **serviceKeys** (producer) | Configuration object for cloud service authentication. |  | ServiceKeys |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (proxy) | Proxy server ip/hostname. |  | String |
| **proxyPassword** (proxy) | Proxy authentication password. |  | String |
| **proxyPort** (proxy) | Proxy server port. |  | int |
| **proxyUser** (proxy) | Proxy authentication user. |  | String |
| **accessKey** (security) | **Required** Access key for the cloud user. |  | String |
| **ignoreSslVerification** (security) | Ignore SSL verification. | false | boolean |
| **secretKey** (security) | **Required** Secret key for the cloud user. |  | String |

## Usage

### Message properties evaluated by the FunctionGraph producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudFgOperation` | `String` | Name of operation to invoke |
| `CamelHwCloudFgFunction` | `String` | Name of function to invoke operation on |
| `CamelHwCloudFgPackage` | `String` | Name of the function package |
| `CamelHwCloudFgXCffLogType` | `String` | Type of log to be returned by FunctionGraph operation |

If the operation, function name, or function package are set, they will override their corresponding query parameter.

### Message properties set by the FunctionGraph producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudFgXCffLogs` | `String` | Unique log returned by FunctionGraph after processing the request if `CamelHwCloudFgXCffLogType` is set |

### List of Supported FunctionGraph Operations

-   invokeFunction - to invoke a serverless function
    

### Using ServiceKey Configuration Bean

Access key and secret keys are required to authenticate against cloud FunctionGraph service. You can avoid having them being exposed and scattered over in your endpoint uri by wrapping them inside a bean of class `org.apache.camel.component.huaweicloud.functiongraph.models.ServiceKeys`. Add it to the registry and let Camel look it up by referring the object via endpoint query parameter `serviceKeys`.

Check the following code snippets:

```xml
<bean id="myServiceKeyConfig" class="org.apache.camel.component.huaweicloud.functiongraph.models.ServiceKeys">
   <property name="accessKey" value="your_access_key" />
   <property name="secretKey" value="your_secret_key" />
</bean>
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:triggerRoute")
 .setProperty("CamelHwCloudFgOperation", constant("invokeFunction"))
 .setProperty("CamelHwCloudFgFunction", constant("your_function_name"))
 .setProperty("CamelHwCloudFgPackage", constant("your_function_package"))
 .to("hwcloud-functiongraph:invokeFunction?projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&region=cn-north-4&serviceKeys=#myServiceKeyConfig")
```

```xml
<route>
  <from uri="direct:triggerRoute"/>
  <setProperty name="CamelHwCloudFgOperation">
    <constant>invokeFunction</constant>
  </setProperty>
  <setProperty name="CamelHwCloudFgFunction">
    <constant>your_function_name</constant>
  </setProperty>
  <setProperty name="CamelHwCloudFgPackage">
    <constant>your_function_package</constant>
  </setProperty>
  <to uri="hwcloud-functiongraph:invokeFunction?projectId=9071a38e7f6a4ba7b7bcbeb7d4ea6efc&amp;region=cn-north-4&amp;serviceKeys=#myServiceKeyConfig"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:triggerRoute
      steps:
        - setProperty:
            name: CamelHwCloudFgOperation
            constant: invokeFunction
        - setProperty:
            name: CamelHwCloudFgFunction
            constant: your_function_name
        - setProperty:
            name: CamelHwCloudFgPackage
            constant: your_function_package
        - to:
            uri: hwcloud-functiongraph:invokeFunction
            parameters:
              projectId: 9071a38e7f6a4ba7b7bcbeb7d4ea6efc
              region: cn-north-4
              serviceKeys: "#myServiceKeyConfig"
```

## Spring Boot Auto-Configuration

When using hwcloud-functiongraph with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-huaweicloud-functiongraph-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hwcloud-functiongraph.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hwcloud-functiongraph.enabled** | Whether to enable auto configuration of the hwcloud-functiongraph component. This is enabled by default. |  | Boolean |
| **camel.component.hwcloud-functiongraph.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |