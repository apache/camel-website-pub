# MapStruct

**Since Camel 3.19**

**Only producer is supported**

The camel-mapstruct component is used for converting POJOs using [MapStruct](https://mapstruct.org/).

## URI format

mapstruct:className\[?options\]

Where `className` is the fully qualified class name of the POJO to convert to.

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

The MapStruct component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mapperPackageName** (producer) | **Required** Package name(s) where Camel should discover Mapstruct mapping classes. Multiple package names can be separated by comma. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **mapStructConverter** (advanced) | **Autowired** To use a custom MapStructConverter such as adapting to a special runtime. |  | MapStructMapperFinder |

## Endpoint Options

The MapStruct endpoint is configured using URI syntax:

mapstruct:className

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **className** (producer) | **Required** The fully qualified class name of the POJO that mapstruct should convert to (target). |  | String |

### Query Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **mandatory** (producer) | Whether there must exist a mapstruct converter to convert to the POJO. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

### Setting up MapStruct

The camel-mapstruct component must be configured with one or more package names for classpath scanning MapStruct _Mapper_ classes. This is necessary because the _Mapper_ classes are to be used for converting POJOs with MapStruct.

For example, to set up two packages, you can do the following:

```java
MapstructComponent mc = context.getComponent("mapstruct", MapstructComponent.class);
mc.setMapperPackageName("com.foo.mapper,com.bar.mapper");
```

This can also be configured in `application.properties`:

```properties
camel.component.mapstruct.mapper-package-name = com.foo.mapper,com.bar.mapper
```

Camel will on startup scan these packages for classes which names ends with _Mapper_. These classes are then introspected to discover the mapping methods. These mapping methods are then registered into the Camel [Type Converter](../../manual/type-converter.md) registry. This means that you can also use type converter to convert the POJOs with MapStruct, such as:

```java
from("direct:foo")
  .convertBodyTo(MyFooDto.class);
```

Where `MyFooDto` is a POJO that MapStruct is able to convert to/from.

> **Note**
> Camel does not support mapper methods defined with a `void` return type such as those used with `@MappingTarget`.

> **Warning**
> If you define multiple mapping methods for the same from / to types, then the implementation chosen by Camel to do its type conversion is potentially non-deterministic.

## Spring Boot Auto-Configuration

When using mapstruct with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mapstruct-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mapstruct.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mapstruct.enabled** | Whether to enable auto configuration of the mapstruct component. This is enabled by default. |  | Boolean |
| **camel.component.mapstruct.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.mapstruct.map-struct-converter** | To use a custom MapStructConverter such as adapting to a special runtime. The option is a org.apache.camel.component.mapstruct.MapStructMapperFinder type. |  | MapStructMapperFinder |
| **camel.component.mapstruct.mapper-package-name** | Package name(s) where Camel should discover Mapstruct mapping classes. Multiple package names can be separated by comma. |  | String |