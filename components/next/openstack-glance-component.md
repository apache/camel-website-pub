# OpenStack Glance

**Since Camel 2.19**

**Only producer is supported**

The Openstack Glance component allows messages to be sent to an OpenStack image services.

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

openstack-glance://hosturl\[?options\]

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

The OpenStack Glance component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Glance endpoint is configured using URI syntax:

openstack-glance:host

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
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Glance component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenstackGlanceDiskFormat** (producer) Constant: [`DISK_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#DISK_FORMAT) | 
The number of flavor VCPU.

Enum values:

-   RAW
    
-   VHD
    
-   VMDK
    
-   VDI
    
-   ISO
    
-   QCOW2
    
-   AKI
    
-   ARI
    
-   AMI
    
-   UNRECOGNIZED
    





 |  | DiskFormat |
| **CamelOpenstackGlanceContainerFormat** (producer) Constant: [`CONTAINER_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#CONTAINER_FORMAT) | 

Size of RAM.

Enum values:

-   BARE
    
-   OVF
    
-   AKI
    
-   ARI
    
-   AMI
    
-   DOCKER
    
-   UNRECOGNIZED
    





 |  | ContainerFormat |
| **CamelOpenstackGlanceOwner** (producer) Constant: [`OWNER`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#OWNER) | Image owner. |  | String |
| **CamelOpenstackGlanceIsPublic** (producer) Constant: [`IS_PUBLIC`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#IS_PUBLIC) | Is public. |  | Boolean |
| **CamelOpenstackGlanceMinRam** (producer) Constant: [`MIN_RAM`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#MIN_RAM) | Minimum ram. |  | Long |
| **CamelOpenstackGlanceMinDisk** (producer) Constant: [`MIN_DISK`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#MIN_DISK) | Minimum disk. |  | Long |
| **CamelOpenstackGlanceSize** (producer) Constant: [`SIZE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#SIZE) | Size. |  | Long |
| **CamelOpenstackGlanceChecksum** (producer) Constant: [`CHECKSUM`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/glance/GlanceConstants.html#CHECKSUM) | Checksum. |  | String |
| **CamelOpenstackOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelOpenstackId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **CamelOpenstackName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |
| **CamelOpenstackProperties** (producer) Constant: [`PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#PROPERTIES) | The image properties. |  | Map |

## Message Body

The message body at each side of the OpenStack Glance component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
For create and upload the image data: an InputStream, a File, a URL or a Payload of openstack4j; text, bytes or the file of the file consumer fail: convert it to a File or an InputStream first. reserve and update take an Image of openstack4j, or else the fields from headers such as CamelOpenstackName.

-   With `operation=create`: `stream`, `file` or `pojo`
    
-   With `operation=upload`: `stream`, `file` or `pojo`
    





 |
| **Producer output** | `pojo`, `list`, `null` or `unchanged` | 

The Image of openstack4j reserved, created, uploaded, updated or read (null when get finds none), a List of them for getAll; delete keeps the body.

-   With `operation=reserve`: `pojo`
    
-   With `operation=create`: `pojo`
    
-   With `operation=upload`: `pojo`
    
-   With `operation=update`: `pojo`
    
-   With `operation=get`: `pojo` or `null`
    
-   With `operation=getAll`: `list`
    
-   With `operation=delete`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

 
| Operation | Description |
| --- | --- |
| `reserve` | Reserve image. |
| `create` | Create a new image. |
| `update` | Update image. |
| `upload` | Upload image. |
| `get` | Get the image. |
| `getAll` | Get all images. |
| `delete` | Delete the image. |

### Example

The following route lists the images. The endpoint is the address of the identity service (Keystone), and the credentials are property placeholders:

```yaml
- route:
    from:
      uri: direct:listImages
      steps:
        - to:
            uri: openstack-glance:http://controller:5000/v3
            parameters:
              username: "{{openstack.username}}"
              password: "{{openstack.password}}"
              project: "{{openstack.project}}"
              operation: getAll
        - log:
            message: "Found ${body.size()} images"
```