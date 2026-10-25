# OpenStack Nova

**Since Camel 2.19**

**Only producer is supported**

The Openstack Nova component allows messages to be sent to an OpenStack compute services.

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

openstack-nova://hosturl\[?options\]

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

The OpenStack Nova component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Nova endpoint is configured using URI syntax:

openstack-nova:host

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

**Required** OpenStack Nova subsystem.

Enum values:

-   flavors
    
-   servers
    
-   keypairs
    





 |  | String |
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Nova component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenstackNovaFlavorId** (flavor server) Constant: [`FLAVOR_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#FLAVOR_ID) | ID of the flavor. |  | String |
| **CamelOpenstackNovaRam** (flavor) Constant: [`RAM`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#RAM) | Size of RAM. |  | Integer |
| **CamelOpenstackNovaVcpu** (flavor) Constant: [`VCPU`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#VCPU) | The number of flavor VCPU. |  | Integer |
| **CamelOpenstackNovaDisk** (flavor) Constant: [`DISK`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#DISK) | Size of disk. |  | Integer |
| **CamelOpenstackNovaSwap** (flavor) Constant: [`SWAP`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#SWAP) | Size of swap. |  | Integer |
| **CamelOpenstackNovaRxtxFactor** (flavor) Constant: [`RXTXFACTOR`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#RXTXFACTOR) | Rxtx Factor. |  | Integer |
| **CamelOpenstackNovaAdminPassword** (server) Constant: [`ADMIN_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#ADMIN_PASSWORD) | Admin password of the new server. |  | String |
| **CamelOpenstackNovaImageId** (server) Constant: [`IMAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#IMAGE_ID) | The Image ID. |  | String |
| **CamelOpenstackNovaKeypairName** (server) Constant: [`KEYPAIR_NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#KEYPAIR_NAME) | The Keypair name. |  | String |
| **CamelOpenstackNovaNetworkId** (server) Constant: [`NETWORK`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#NETWORK) | The list of networks (by id). |  | List |
| **CamelOpenstackNovaAction** (server) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/nova/NovaConstants.html#ACTION) | 
An action to perform.

Enum values:

-   PAUSE
    
-   UNPAUSE
    
-   STOP
    
-   START
    
-   LOCK
    
-   UNLOCK
    
-   SUSPEND
    
-   RESUME
    
-   RESCUE
    
-   UNRESCUE
    
-   SHELVE
    
-   SHELVE\_OFFLOAD
    
-   UNSHELVE
    
-   FORCEDELETE
    





 |  | Action |
| **CamelOpenstackOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelOpenstackId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **CamelOpenstackName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |

## Message Body

The message body at each side of the OpenStack Nova component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | Read by create only: a Flavor or ServerCreate of openstack4j, or else the fields from headers such as CamelOpenstackName; for keypairs the public key as text, or no body to have the key pair generated. The other operations take the id or name from headers. |
| **Producer output** | `pojo`, `list`, `text`, `null` or `unchanged` | 
The Flavor, Server or Keypair of openstack4j created or read (null when get finds none), a List of them for getAll, the id of the image as text for createSnapshot; delete and a server action keep the body.

-   With `operation=create`: `pojo`
    
-   With `operation=get`: `pojo` or `null`
    
-   With `operation=getAll`: `list`
    
-   With `operation=createSnapshot`: `text` (`java.lang.String`)
    
-   With `operation=delete`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Usage

You can use the following settings for each subsystem:

### Flavors

#### Operations you can perform with the Flavor producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new flavor. |
| `get` | Get the flavor. |
| `getAll` | Get all flavors. |
| `delete` | Delete the flavor. |

If you need more precise flavor settings, you can create a new object of the type `org.openstack4j.model.compute.Flavor` and send in the message body.

### Servers

#### Operations you can perform with the Server producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new server. |
| `createSnapshot` | Create snapshot of the server. |
| `get` | Get the server. |
| `getAll` | Get all servers. |
| `delete` | Delete the server. |
| `action` | Perform an action on the server. |

If you need more precise server settings, you can create a new object of the type `org.openstack4j.model.compute.ServerCreate` and send in the message body.

### Key/Pairs

#### Operations you can perform with the Keypair producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new keypair. |
| `get` | Get the keypair. |
| `getAll` | Get all keypairs. |
| `delete` | Delete the keypair. |

### Example

The following route lists the servers. The endpoint is the address of the identity service (Keystone), and the credentials are property placeholders:

```yaml
- route:
    from:
      uri: direct:listServers
      steps:
        - to:
            uri: openstack-nova:http://controller:5000/v3
            parameters:
              username: "{{openstack.username}}"
              password: "{{openstack.password}}"
              project: "{{openstack.project}}"
              subsystem: servers
              operation: getAll
        - log:
            message: "Found ${body.size()} servers"
```