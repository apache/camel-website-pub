# OpenStack Cinder

**Since Camel 2.19**

**Only producer is supported**

The Openstack Cinder component allows messages to be sent to an OpenStack block storage services.

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

openstack-cinder://hosturl\[?options\]

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

The OpenStack Cinder component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Cinder endpoint is configured using URI syntax:

openstack-cinder:host

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** OpenStack host url. |  | String |

### Query Parameters

   
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

**Required** OpenStack Cinder subsystem.

Enum values:

-   snapshots
    
-   volumes
    





 |  | String |
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Cinder component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenstackCinderSize** (volume) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#SIZE) | Size of volume. |  | Integer |
| **CamelOpenstackCinderVolumeType** (volume) Constant: [`VOLUME_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#VOLUME_TYPE) | Volume type. |  | String |
| **CamelOpenstackCinderImageRef** (volume) Constant: [`IMAGE_REF`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#IMAGE_REF) | ID of image. |  | String |
| **CamelOpenstackCinderSnapshotId** (volume) Constant: [`SNAPSHOT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#SNAPSHOT_ID) | ID of snapshot. |  | String |
| **CamelOpenstackCinderIsBootable** (volume) Constant: [`IS_BOOTABLE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#IS_BOOTABLE) | Is bootable. |  | Boolean |
| **CamelOpenstackCinderVolumeId** (snapshot) Constant: [`VOLUME_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#VOLUME_ID) | The Volume ID. |  | String |
| **CamelOpenstackCinderForce** (snapshot) Constant: [`FORCE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/cinder/CinderConstants.html#FORCE) | Force. |  | Boolean |
| **CamelOpenstackOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelOpenstackId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **CamelOpenstackName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |
| **CamelOpenstackDescription** (producer) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#DESCRIPTION) | The description. |  | String |

## Usage

You can use the following settings for each subsystem:

### Volumes

#### Operations you can perform with the Volume producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new volume. |
| `get` | Get the volume. |
| `getAll` | Get all volumes. |
| `getAllTypes` | Get volume types. |
| `update` | Update the volume. |
| `delete` | Delete the volume. |

If you need more precise volume settings, you can create a new object of the type `org.openstack4j.model.storage.block.Volume` and send in the message body.

### Snapshots

#### Operations you can perform with the Snapshot producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new snapshot. |
| `get` | Get the snapshot. |
| `getAll` | Get all snapshots. |
| `update` | Get update the snapshot. |
| `delete` | Delete the snapshot. |

If you need more precise server settings, you can create a new object of the type `org.openstack4j.model.storage.block.VolumeSnapshot` and send in the message body.