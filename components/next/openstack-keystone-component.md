# OpenStack Keystone

**Since Camel 2.19**

**Only producer is supported**

The Openstack Keystone component allows messages to be sent to an OpenStack identity services.

> **Note**
> The openstack-keystone component supports only Identity API v3

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

openstack-keystone://hosturl\[?options\]

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

The OpenStack Keystone component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenStack Keystone endpoint is configured using URI syntax:

openstack-keystone:host

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** OpenStack host url. |  | String |

### Query Parameters

   
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

The OpenStack Keystone component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenstackKeystoneDescription** (producer) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#DESCRIPTION) | The description. |  | String |
| **CamelOpenstackKeystoneDomainId** (group project user) Constant: [`DOMAIN_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#DOMAIN_ID) | ID of the domain. |  | String |
| **CamelOpenstackKeystoneParentId** (project) Constant: [`PARENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#PARENT_ID) | The parent project ID. |  | String |
| **CamelOpenstackKeystonePassword** (user) Constant: [`PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#PASSWORD) | User’s password. |  | String |
| **CamelOpenstackKeystoneEmail** (user) Constant: [`EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#EMAIL) | User’s email. |  | String |
| **CamelOpenstackKeystoneUserId** (group) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#USER_ID) | ID of the user. |  | String |
| **CamelOpenstackKeystoneGroupId** (group) Constant: [`GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/keystone/KeystoneConstants.html#GROUP_ID) | ID of the group. |  | String |
| **CamelOpenstackOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelOpenstackId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#ID) | The ID. |  | String |
| **CamelOpenstackName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-openstack/latest/org/apache/camel/component/openstack/common/OpenstackConstants.html#NAME) | The name. |  | String |

## Usage

You can use the following settings for each subsystem:

### Domains

#### Operations you can perform with the Domain producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new domain. |
| `get` | Get the domain. |
| `getAll` | Get all domains. |
| `update` | Update the domain. |
| `delete` | Delete the domain. |

If you need more precise domain settings, you can create a new object of the type `org.openstack4j.model.identity.v3.Domain` and send in the message body.

### Groups

#### Operations you can perform with the Group producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new group. |
| `get` | Get the group. |
| `getAll` | Get all groups. |
| `update` | Update the group. |
| `delete` | Delete the group. |
| `addUserToGroup` | Add the user to the group. |
| `checkUserGroup` | Check whether is the user in the group. |
| `removeUserFromGroup` | Remove the user from the group. |

If you need more precise group settings, you can create a new object of the type `org.openstack4j.model.identity.v3.Group` and send in the message body.

### Projects

#### Operations you can perform with the Project producer

 
| Operation | Description |
| --- | --- |
| `create` | Create a new project. |
| `get` | Get the project. |
| `getAll` | Get all projects. |
| `update` | Update the project. |
| `delete` | Delete the project. |

If you need more precise project settings, you can create a new object of the type `org.openstack4j.model.identity.v3.Project` and send in the message body.

### Regions

#### Operations you can perform with the Region producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new region. |
| `get` | Get the region. |
| `getAll` | Get all regions. |
| `update` | Update the region. |
| `delete` | Delete the region. |

If you need more precise region settings, you can create a new object of the type `org.openstack4j.model.identity.v3.Region` and send in the message body.

### Users

#### Operations you can perform with the User producer

 
| Operation | Description |
| --- | --- |
| `create` | Create new user. |
| `get` | Get the user. |
| `getAll` | Get all users. |
| `update` | Update the user. |
| `delete` | Delete the user. |

If you need more precise user settings, you can create a new object of the type `org.openstack4j.model.identity.v3.User` and send in the message body.