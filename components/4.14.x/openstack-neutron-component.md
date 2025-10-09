# OpenStack Neutron

**Since Camel 2.19**

**Only producer is supported**

The Openstack Neutron component allows messages to be sent to an OpenStack network services.

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

openstack-neutron://hosturl\[?options\]

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

The OpenStack Neutron component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Neutron endpoint is configured using URI syntax:

openstack-neutron:host

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

**Required** OpenStack Neutron subsystem.

Enum values:

-   networks
    
-   subnets
    
-   ports
    
-   routers
    





 |  | String |
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Neutron component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tenantId** (network port router) Constant: [`TENANT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#TENANT_ID) | Tenant ID. |  | String |
| **networkId** (subnet port) Constant: [`NETWORK_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#NETWORK_ID) | Network ID. |  | String |
| **adminStateUp** (network) Constant: [`ADMIN_STATE_UP`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#ADMIN_STATE_UP) | AdminStateUp header. |  | Boolean |
| **networkType** (network) Constant: [`NETWORK_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#NETWORK_TYPE) | 
Network type.

Enum values:

-   LOCAL
    
-   FLAT
    
-   VLAN
    
-   VXLAN
    
-   GRE
    
-   GENEVE
    





 |  | NetworkType |
| **physicalNetwork** (network) Constant: [`PHYSICAL_NETWORK`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#PHYSICAL_NETWORK) | Physical network. |  | String |
| **segmentId** (network) Constant: [`SEGMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#SEGMENT_ID) | Segment ID. |  | String |
| **isShared** (network) Constant: [`IS_SHARED`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#IS_SHARED) | Is shared. |  | Boolean |
| **isRouterExternal** (network) Constant: [`IS_ROUTER_EXTERNAL`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#IS_ROUTER_EXTERNAL) | Is router external. |  | Boolean |
| **enableDHCP** (subnet) Constant: [`ENABLE_DHCP`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#ENABLE_DHCP) | Enable DHCP. |  | Boolean |
| **gateway** (subnet) Constant: [`GATEWAY`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#GATEWAY) | Gateway. |  | String |
| **ipVersion** (subnet) Constant: [`IP_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#IP_VERSION) | 

IP version.

Enum values:

-   V4
    
-   V6
    





 |  | IPVersionType |
| **cidr** (subnet) Constant: [`CIDR`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#CIDR) | The cidr representing the IP range for this subnet, based on IP version. |  | String |
| **subnetPools** (subnet) Constant: [`SUBNET_POOL`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#SUBNET_POOL) | The allocation pool. |  | NeutronPool |
| **deviceId** (port) Constant: [`DEVICE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#DEVICE_ID) | Device ID. |  | String |
| **macAddress** (port) Constant: [`MAC_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#MAC_ADDRESS) | MAC address. |  | String |
| **routerId** (router) Constant: [`ROUTER_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#ROUTER_ID) | Router ID. |  | String |
| **subnetId** (router subnet) Constant: [`SUBNET_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#SUBNET_ID) | Subnet ID. |  | String |
| **portId** (port router) Constant: [`PORT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#PORT_ID) | Port ID. |  | String |
| **interfaceType** (router) Constant: [`ITERFACE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/neutron/NeutronConstants.html#ITERFACE_TYPE) | 

Interface type.

Enum values:

-   PORT
    
-   SUBNET
    





 |  | AttachInterfaceType |
| **operation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **ID** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **name** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |

## Usage

You can use the following settings for each subsystem:

### Networks

#### Operations you can perform with the Network producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new network. |
| `get` | Get the network. |
| `getAll` | Get all networks. |
| `delete` | Delete the network. |

If you need more precise network settings, you can create a new object of the type `org.openstack4j.model.network.Network` and send in the message body.

### Subnets

#### Operations you can perform with the Subnet producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new subnet. |
| `get` | Get the subnet. |
| `getAll` | Get all subnets. |
| `delete` | Delete the subnet. |
| `action` | Perform an action on the subnet. |

If you need more precise subnet settings, you can create a new object of the type `org.openstack4j.model.network.Subnet` and send in the message body.

### Ports

#### Operations you can perform with the Port producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new port. |
| `get` | Get the port. |
| `getAll` | Get all ports. |
| `update` | Update the port. |
| `delete` | Delete the port. |

### Routers

#### Operations you can perform with the Router producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new router. |
| `get` | Get the router. |
| `getAll` | Get all routers. |
| `update` | Update the router. |
| `delete` | Delete the router. |
| `attachInterface` | Attach an interface. |
| `detachInterface` | Detach an interface. |

## Spring Boot Auto-Configuration

When using openstack-neutron with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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