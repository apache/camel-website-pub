# OpenStack Swift

**Since Camel 2.19**

**Only producer is supported**

The Openstack Swift component allows messages to be sent to an OpenStack object storage services.

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

pom.xml

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openstack</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.

## URI Format

openstack-swift://hosturl\[?options\]

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

The OpenStack Swift component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Swift endpoint is configured using URI syntax:

openstack-swift:host

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** OpenStack host url. |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiVersion** (producer) | 
OpenStack API version.

Enum values:

-   V2
    
-   V3
    





 | V3 | String |
| **config** (producer) | OpenStack configuration. |  | Config |
| **domain** (producer) | Authentication domain. | default | String |
| **operation** (producer) | The operation to do. |  | String |
| **password** (producer) | **Required** OpenStack password. |  | String |
| **project** (producer) | **Required** The project ID. |  | String |
| **subsystem** (producer) | 

**Required** OpenStack Swift subsystem.

Enum values:

-   objects
    
-   containers
    





 |  | String |
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Swift component supports 14 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenstackSwiftContainerName** (object container) Constant: [`CONTAINER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#CONTAINER_NAME) | The container name. |  | String |
| **CamelOpenstackSwiftObjectName** (object) Constant: [`OBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#OBJECT_NAME) | The object name. |  | String |
| xref:#\_endpoint\_header\_X-Container-Meta-**X-Container-Meta-** (container) Constant: [`CONTAINER_METADATA_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#CONTAINER_METADATA_PREFIX) | Container metadata prefix. |  | Map |
| **X-Versions-Location** (container) Constant: [`VERSIONS_LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#VERSIONS_LOCATION) | Versions location. |  | String |
| **X-Container-Read** (container) Constant: [`CONTAINER_READ`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#CONTAINER_READ) | ACL - container read. |  | String |
| **X-Container-Write** (container) Constant: [`CONTAINER_WRITE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#CONTAINER_WRITE) | ACL - container write. |  | String |
| **CamelOpenstackSwiftLimit** (container) Constant: [`LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#LIMIT) | List options - limit. |  | Integer |
| **CamelOpenstackSwiftMarker** (container) Constant: [`MARKER`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#MARKER) | List options - marker. |  | String |
| **CamelOpenstackSwiftEndMarker** (container) Constant: [`END_MARKER`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#END_MARKER) | List options - end marker. |  | String |
| **CamelOpenstackSwiftDelimiter** (container) Constant: [`DELIMITER`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#DELIMITER) | List options - delimiter. |  | Character |
| **CamelOpenstackSwiftPath** (container object) Constant: [`PATH`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/swift/SwiftConstants.html#PATH) | The path. |  | String |
| **CamelOpenstackOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelOpenstackId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **CamelOpenstackName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |

## Usage

You can use the following settings for each subsystem:

### Containers

#### Operations you can perform with the Container producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new container. |
| `get` | Get the container. |
| `getAll` | Get all containers. |
| `update` | Update the container. |
| `delete` | Delete the container. |
| `getMetadata` | Get metadata. |
| `createUpdateMetadata` | Create/update metadata. |
| `deleteMetadata` | Delete metadata. |

If you need more precise container settings, you can create a new object of the type `org.openstack4j.model.storage.object.options.CreateUpdateContainerOptions` (in case of create or update operation) or `org.openstack4j.model.storage.object.options.ContainerListOptions` for listing containers and send in the message body.

### Objects

#### Operations you can perform with the Object producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new object. |
| `get` | Get the object. |
| `getAll` | Get all objects. |
| `update` | Get update the object. |
| `delete` | Delete the object. |
| `getMetadata` | Get metadata. |
| `createUpdateMetadata` | Create/update metadata. |

## Spring Boot Auto-Configuration

When using openstack-swift with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-openstack-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.openstack-cinder.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-cinder.enabled** | Whether to enable auto configuration of the openstack-cinder component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-cinder.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openstack-glance.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-glance.enabled** | Whether to enable auto configuration of the openstack-glance component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-glance.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openstack-keystone.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-keystone.enabled** | Whether to enable auto configuration of the openstack-keystone component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-keystone.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openstack-neutron.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-neutron.enabled** | Whether to enable auto configuration of the openstack-neutron component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-neutron.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openstack-nova.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-nova.enabled** | Whether to enable auto configuration of the openstack-nova component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-nova.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openstack-swift.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openstack-swift.enabled** | Whether to enable auto configuration of the openstack-swift component. This is enabled by default. |  | Boolean |
| **camel.component.openstack-swift.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |