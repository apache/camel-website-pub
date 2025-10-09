# OpenStack Keystone

**Since Camel 2.19**

**Only producer is supported**

The Openstack Keystone component allows messages to be sent to an OpenStack identity services.

> **Note**
> The openstack-keystone component supports only Identity API v3

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openstack</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version`} must be replaced by the actual version of Camel.

## URI Format

openstack-keystone://hosturl\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The OpenStack Keystone component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Keystone endpoint is configured using URI syntax:

openstack-keystone:host

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** OpenStack host url. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **config** (producer) | OpenStack configuration. |  | Config |
| **domain** (producer) | Authentication domain. | default | String |
| **operation** (producer) | The operation to do. |  | String |
| **password** (producer) | **Required** OpenStack password. |  | String |
| **project** (producer) | **Required** The project ID. |  | String |
| **subsystem** (producer) | 
**Required** OpenStack Keystone subsystem.

Enum values:

-   regions
    
-   domains
    
-   projects
    
-   users
    
-   groups
    





 |  | String |
| **username** (producer) | **Required** OpenStack username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenStack Keystone component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** (producer) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#DESCRIPTION) | The description. |  | String |
| **domainId** (group project user) Constant: [`DOMAIN_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#DOMAIN_ID) | ID of the domain. |  | String |
| **parentId** (project) Constant: [`PARENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#PARENT_ID) | The parent project ID. |  | String |
| **password** (user) Constant: [`PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#PASSWORD) | User’s password. |  | String |
| **email** (user) Constant: [`EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#EMAIL) | User’s email. |  | String |
| **userId** (group) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#USER_ID) | ID of the user. |  | String |
| **groupId** (group) Constant: [`GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#GROUP_ID) | ID of the group. |  | String |
| **operation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **ID** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **name** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |

## Usage

You can use following settings for each subsystem:

## domains

### Operations you can perform with the Domain producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new domain. |
| `get` | Get the domain. |
| `getAll` | Get all domains. |
| `update` | Update the domain. |
| `delete` | Delete the domain. |

If you need more precise domain settings you can create new object of the type **org.openstack4j.model.identity.v3.Domain** and send in the message body.

## groups

### Operations you can perform with the Group producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new group. |
| `get` | Get the group. |
| `getAll` | Get all groups. |
| `update` | Update the group. |
| `delete` | Delete the group. |
| `addUserToGroup` | Add the user to the group. |
| `checkUserGroup` | Check whether is the user in the group. |
| `removeUserFromGroup` | Remove the user from the group. |

If you need more precise group settings you can create new object of the type **org.openstack4j.model.identity.v3.Group** and send in the message body.

## projects

### Operations you can perform with the Project producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new project. |
| `get` | Get the project. |
| `getAll` | Get all projects. |
| `update` | Update the project. |
| `delete` | Delete the project. |

If you need more precise project settings you can create new object of the type **org.openstack4j.model.identity.v3.Project** and send in the message body.

## regions

### Operations you can perform with the Region producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new region. |
| `get` | Get the region. |
| `getAll` | Get all regions. |
| `update` | Update the region. |
| `delete` | Delete the region. |

If you need more precise region settings you can create new object of the type **org.openstack4j.model.identity.v3.Region** and send in the message body.

## users

### Operations you can perform with the User producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new user. |
| `get` | Get the user. |
| `getAll` | Get all users. |
| `update` | Update the user. |
| `delete` | Delete the user. |

If you need more precise user settings you can create new object of the type **org.openstack4j.model.identity.v3.User** and send in the message body.

## Spring Boot Auto-Configuration

When using openstack-keystone with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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