# DigitalOcean

**Since Camel 2.19**

**Only producer is supported**

The DigitalOcean component allows you to manage Droplets and resources within the DigitalOcean cloud with **Camel** by encapsulating [digitalocean-api-java](https://www.digitalocean.com/community/projects/api-client-in-java). All of the functionality that you are familiar with in the DigitalOcean control panel is also available through this Camel component.

## Prerequisites

You must have a valid DigitalOcean account and a valid OAuth token. You can generate an OAuth token by visiting the \[Apps & API\] section of the DigitalOcean control panel for your account.

## URI format

The **DigitalOcean Component** uses the following URI format:

digitalocean://endpoint?\[options\]

where `endpoint` is a DigitalOcean resource type.

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

The DigitalOcean component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The DigitalOcean endpoint is configured using URI syntax:

digitalocean:operation

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
The operation to perform to the given resource.

Enum values:

-   create
    
-   update
    
-   delete
    
-   list
    
-   ownList
    
-   get
    
-   listBackups
    
-   listActions
    
-   listNeighbors
    
-   listSnapshots
    
-   listKernels
    
-   listAllNeighbors
    
-   enableBackups
    
-   disableBackups
    
-   reboot
    
-   powerCycle
    
-   shutdown
    
-   powerOn
    
-   powerOff
    
-   restore
    
-   resetPassword
    
-   resize
    
-   rebuild
    
-   rename
    
-   changeKernel
    
-   enableIpv6
    
-   enablePrivateNetworking
    
-   takeSnapshot
    
-   transfer
    
-   convert
    
-   attach
    
-   detach
    
-   assign
    
-   unassign
    
-   tag
    
-   untag
    





 |  | DigitalOceanOperations |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **page** (producer) | Use for pagination. Force the page number. | 1 | Integer |
| **perPage** (producer) | Use for pagination. Set the number of item per request. The maximum number of results per page is 200. | 25 | Integer |
| **resource** (producer) | 
**Required** The DigitalOcean resource type on which perform the operation.

Enum values:

-   account
    
-   actions
    
-   blockStorages
    
-   droplets
    
-   mages
    
-   snapshots
    
-   keys
    
-   regions
    
-   sizes
    
-   floatingIPs
    
-   tags
    





 |  | DigitalOceanResources |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **digitalOceanClient** (advanced) | To use a existing configured DigitalOceanClient as client. |  | DigitalOceanClient |
| **httpProxyHost** (proxy) | Set a proxy host if needed. |  | String |
| **httpProxyPassword** (proxy) | Set a proxy password if needed. |  | String |
| **httpProxyPort** (proxy) | Set a proxy port if needed. |  | Integer |
| **httpProxyUser** (proxy) | Set a proxy host if needed. |  | String |
| **oAuthToken** (security) | DigitalOcean OAuth Token. |  | String |

## Message Headers

The DigitalOcean component supports 24 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDigitalOceanOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#OPERATION) | 
The operation to perform.

Enum values:

-   create
    
-   update
    
-   delete
    
-   list
    
-   ownList
    
-   get
    
-   listBackups
    
-   listActions
    
-   listNeighbors
    
-   listSnapshots
    
-   listKernels
    
-   listAllNeighbors
    
-   enableBackups
    
-   disableBackups
    
-   reboot
    
-   powerCycle
    
-   shutdown
    
-   powerOn
    
-   powerOff
    
-   restore
    
-   resetPassword
    
-   resize
    
-   rebuild
    
-   rename
    
-   changeKernel
    
-   enableIpv6
    
-   enablePrivateNetworking
    
-   takeSnapshot
    
-   transfer
    
-   convert
    
-   attach
    
-   detach
    
-   assign
    
-   unassign
    
-   tag
    
-   untag
    





 |  | DigitalOceanOperations |
| **CamelDigitalOceanId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#ID) | The id. |  | Integer or String |
| **CamelDigitalOceanType** (producer) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#TYPE) | 

The type.

Enum values:

-   distribution
    
-   application
    





 |  | DigitalOceanImageTypes |
| **CamelDigitalOceanName** (producer) Constant: [`NAME`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#NAME) | The name. |  | String |
| **CamelDigitalOceanNames** (producer) Constant: [`NAMES`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#NAMES) | The names of the droplet. |  | List |
| **CamelDigitalOceanRegion** (producer) Constant: [`REGION`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#REGION) | The code name of the region aka DigitalOcean data centers. |  | String |
| **CamelDigitalOceanDescription** (producer) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DESCRIPTION) | The description. |  | String |
| **CamelDigitalOceanDropletSize** (producer) Constant: [`DROPLET_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_SIZE) | The size of the droplet. |  | String |
| **CamelDigitalOceanDropletImage** (producer) Constant: [`DROPLET_IMAGE`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_IMAGE) | The image of the droplet. |  | String |
| **CamelDigitalOceanDropletSSHKeys** (producer) Constant: [`DROPLET_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_KEYS) | The keys of the droplet. |  | List |
| **CamelDigitalOceanDropletEnableBackups** (producer) Constant: [`DROPLET_ENABLE_BACKUPS`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_ENABLE_BACKUPS) | The flag to enable backups. |  | Boolean |
| **CamelDigitalOceanDropletEnableIpv6** (producer) Constant: [`DROPLET_ENABLE_IPV6`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_ENABLE_IPV6) | The flag to enable ipv6. |  | Boolean |
| **CamelDigitalOceanDropletEnablePrivateNetworking** (producer) Constant: [`DROPLET_ENABLE_PRIVATE_NETWORKING`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_ENABLE_PRIVATE_NETWORKING) | The flag to enable private networking. |  | Boolean |
| **CamelDigitalOceanDropletUserData** (producer) Constant: [`DROPLET_USER_DATA`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_USER_DATA) | The user data of the droplet. |  | String |
| **CamelDigitalOceanDropletVolumes** (producer) Constant: [`DROPLET_VOLUMES`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_VOLUMES) | The volumes' identifier of the droplet. |  | List |
| **CamelDigitalOceanDropletTags** (producer) Constant: [`DROPLET_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_TAGS) | The tags of the droplet. |  | List |
| **CamelDigitalOceanDropletId** (producer) Constant: [`DROPLET_ID`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#DROPLET_ID) | The droplet identifier. |  | Integer |
| **CamelDigitalOceanImageId** (producer) Constant: [`IMAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#IMAGE_ID) | The id of the DigitalOcean public image or your private image. |  | Integer |
| **CamelDigitalOceanKernelId** (producer) Constant: [`KERNEL_ID`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#KERNEL_ID) | The kernel id to be changed for droplet. |  | Integer |
| **CamelDigitalOceanVolumeName** (producer) Constant: [`VOLUME_NAME`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#VOLUME_NAME) | The name of the volume. |  | String |
| **CamelDigitalOceanVolumeSizeGigabytes** (producer) Constant: [`VOLUME_SIZE_GIGABYTES`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#VOLUME_SIZE_GIGABYTES) | The size value in GB. |  | Integer or Double |
| **CamelDigitalOceanFloatingIPAddress** (producer) Constant: [`FLOATING_IP_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#FLOATING_IP_ADDRESS) | The floating IP address. |  | String |
| **CamelDigitalOceanKeyFingerprint** (producer) Constant: [`KEY_FINGERPRINT`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#KEY_FINGERPRINT) | The SSH key fingerprint. |  | String |
| **CamelDigitalOceanKeyPublicKey** (producer) Constant: [`KEY_PUBLIC_KEY`](https://javadoc.io/doc/org.apache.camel/camel-digitalocean/latest/org/apache/camel/component/digitalocean/constants/DigitalOceanHeaders.html#KEY_PUBLIC_KEY) | The public key. |  | String |

You have to provide an **operation** value for each endpoint, with the `operation` URI option or the `CamelDigitalOceanOperation` message header.

All **operation** values are defined in `DigitalOceanOperations` enumeration.

All **header** names used by the component are defined in `DigitalOceanHeaders` enumeration.

## Message body result

All message bodies returned are using objects provided by the **digitalocean-api-java** library.

## API Rate Limits

DigitalOcean REST API encapsulated by camel-digitalocean component is subjected to API Rate Limiting. You can find the per method limits in the [API Rate Limits documentation](https://developers.digitalocean.com/documentation/v2/#rate-limit).

## Account endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `get` | get account info |  | `com.myjeeva.digitalocean.pojo.Account` |

## BlockStorages endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the Block Storage volumes available on your account | 
 | `List<com.myjeeva.digitalocean.pojo.Volume>` |
| `get` | show information about a Block Storage volume | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Volume` |
| `get` | show information about a Block Storage volume by name | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanRegion` _String_ | `com.myjeeva.digitalocean.pojo.Volume` |
| `listSnapshots` | retrieve the snapshots that have been created from a volume | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Snapshot>` |
| `create` | create a new volume | `CamelDigitalOceanVolumeSizeGigabytes` _Integer_,  
`CamelDigitalOceanName` _String_,  
`CamelDigitalOceanDescription`\* _String_,  
`CamelDigitalOceanRegion`\* _String_ | `com.myjeeva.digitalocean.pojo.Volume` |
| `delete` | delete a Block Storage volume, destroying all data and removing it from your account | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `delete` | delete a Block Storage volume by name | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanRegion` _String_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `attach` | attach a Block Storage volume to a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanDropletId` _Integer_,  
`CamelDigitalOceanDropletRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `attach` | attach a Block Storage volume to a Droplet by name | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanDropletId` _Integer_,  
`CamelDigitalOceanDropletRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `detach` | detach a Block Storage volume from a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanDropletId` _Integer_,  
`CamelDigitalOceanDropletRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `attach` | detach a Block Storage volume from a Droplet by name | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanDropletId` _Integer_,  
`CamelDigitalOceanDropletRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `resize` | resize a Block Storage volume | `CamelDigitalOceanVolumeSizeGigabytes` _Integer_,  
`CamelDigitalOceanRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `listActions` | retrieve all actions that have been executed on a volume | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Action>` |

## Droplets endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all Droplets in your account |  | `List<com.myjeeva.digitalocean.pojo.Droplet>` |
| `get` | show an individual droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Droplet` |
| `create` | create a new Droplet | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanDropletImage` _String_,  
`CamelDigitalOceanRegion` _String_,  
`CamelDigitalOceanDropletSize` _String_,  
`CamelDigitalOceanDropletSSHKeys`\* _List<String>_,  
`CamelDigitalOceanDropletEnableBackups`\* _Boolean_,  
`CamelDigitalOceanDropletEnableIpv6`\* _Boolean_,  
`CamelDigitalOceanDropletEnablePrivateNetworking`\* _Boolean_,  
`CamelDigitalOceanDropletUserData`\* _String_,  
`CamelDigitalOceanDropletVolumes`\* _List<String>_,  
`CamelDigitalOceanDropletTags` _List<String>_ | `com.myjeeva.digitalocean.pojo.Droplet` |
| `create` | create multiple Droplets | `CamelDigitalOceanNames` _List<String>_,  
`CamelDigitalOceanDropletImage` _String_,  
`CamelDigitalOceanRegion` _String_,  
`CamelDigitalOceanDropletSize` _String_,  
`CamelDigitalOceanDropletSSHKeys`\* _List<String>_,  
`CamelDigitalOceanDropletEnableBackups`\* _Boolean_,  
`CamelDigitalOceanDropletEnableIpv6`\* _Boolean_,  
`CamelDigitalOceanDropletEnablePrivateNetworking`\* _Boolean_,  
`CamelDigitalOceanDropletUserData`\* _String_,  
`CamelDigitalOceanDropletVolumes`\* _List<String>_,  
`CamelDigitalOceanDropletTags` _List<String>_ | `com.myjeeva.digitalocean.pojo.Droplet` |
| `delete` | delete a Droplet, | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `enableBackups` | enable backups on an existing Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `disableBackups` | disable backups on an existing Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `enableIpv6` | enable IPv6 networking on an existing Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `enablePrivateNetworking` | enable private networking on an existing Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `reboot` | reboot a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `powerCycle` | power cycle a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `shutdown` | shutdown a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `powerOff` | power off a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `powerOn` | power on a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `restore` | shutdown a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanImageId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `passwordReset` | reset the password for a Droplet | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `resize` | resize a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanDropletSize` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `rebuild` | rebuild a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanImageId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `rename` | rename a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `changeKernel` | change the kernel of a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanKernelId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `takeSnapshot` | snapshot a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName`\* _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `tag` | tag a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Response` |
| `untag` | untag a Droplet | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Response` |
| `listKernels` | retrieve a list of all kernels available to a Droplet | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Kernel>` |
| `listSnapshots` | retrieve the snapshots that have been created from a Droplet | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Snapshot>` |
| `listBackups` | retrieve any backups associated with a Droplet | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Backup>` |
| `listActions` | retrieve all actions that have been executed on a Droplet | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Action>` |
| `listNeighbors` | retrieve a list of droplets that are running on the same physical server | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Droplet>` |
| `listAllNeighbors` | retrieve a list of any droplets that are running on the same physical hardware |  | `List<com.myjeeva.digitalocean.pojo.Droplet>` |

## Images endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list images available on your account | `CamelDigitalOceanType`\* _DigitalOceanImageTypes_ | `List<com.myjeeva.digitalocean.pojo.Image>` |
| `ownList` | retrieve only the private images of a user |  | `List<com.myjeeva.digitalocean.pojo.Image>` |
| `listActions` | retrieve all actions that have been executed on a Image | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.Action>` |
| `get` | retrieve information about an image (public or private) by id | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Image` |
| `get` | retrieve information about an public image by slug | `CamelDigitalOceanDropletImage` _String_ | `com.myjeeva.digitalocean.pojo.Image` |
| `update` | update an image | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Image` |
| `delete` | delete an image | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `transfer` | transfer an image to another region | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanRegion` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `convert` | convert an image, for example, a backup to a snapshot | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |

## Snapshots endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the snapshots available on your account | `CamelDigitalOceanType`\* _DigitalOceanSnapshotTypes_ | `List<com.myjeeva.digitalocean.pojo.Snapshot>` |
| `get` | retrieve information about a snapshot | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Snapshot` |
| `delete` | delete an snapshot | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Delete` |

## Keys endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the keys in your account |  | `List<com.myjeeva.digitalocean.pojo.Key>` |
| `get` | retrieve information about a key by id | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Key` |
| `get` | retrieve information about a key by fingerprint | `CamelDigitalOceanKeyFingerprint` _String_ | `com.myjeeva.digitalocean.pojo.Key` |
| `update` | update a key by id | `CamelDigitalOceanId` _Integer_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Key` |
| `update` | update a key by fingerprint | `CamelDigitalOceanKeyFingerprint` _String_,  
`CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Key` |
| `delete` | delete a key by id | `CamelDigitalOceanId` _Integer_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `delete` | delete a key by fingerprint | `CamelDigitalOceanKeyFingerprint` _String_ | `com.myjeeva.digitalocean.pojo.Delete` |

## Regions endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the regions that are available |  | `List<com.myjeeva.digitalocean.pojo.Region>` |

## Sizes endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the sizes that are available |  | `List<com.myjeeva.digitalocean.pojo.Size>` |

## Floating IPs endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of the Floating IPs available on your account |  | `List<com.myjeeva.digitalocean.pojo.FloatingIP>` |
| `create` | create a new Floating IP assigned to a Droplet | `CamelDigitalOceanId` _Integer_ | `List<com.myjeeva.digitalocean.pojo.FloatingIP>` |
| `create` | create a new Floating IP assigned to a Region | `CamelDigitalOceanRegion` _String_ | `List<com.myjeeva.digitalocean.pojo.FloatingIP>` |
| `get` | retrieve information about a Floating IP | `CamelDigitalOceanFloatingIPAddress` _String_ | `com.myjeeva.digitalocean.pojo.Key` |
| `delete` | delete a Floating IP and remove it from your account | `CamelDigitalOceanFloatingIPAddress` _String_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `assign` | assign a Floating IP to a Droplet | `CamelDigitalOceanFloatingIPAddress` _String_,  
`CamelDigitalOceanDropletId` _Integer_ | `com.myjeeva.digitalocean.pojo.Action` |
| `unassign` | unassign a Floating IP | `CamelDigitalOceanFloatingIPAddress` _String_ | `com.myjeeva.digitalocean.pojo.Action` |
| `listActions` | retrieve all actions that have been executed on a Floating IP | `CamelDigitalOceanFloatingIPAddress` _String_ | `List<com.myjeeva.digitalocean.pojo.Action>` |

## Tags endpoint

   
| operation | Description | Headers | Result |
| --- | --- | --- | --- |
| `list` | list all of your tags |  | `List<com.myjeeva.digitalocean.pojo.Tag>` |
| `create` | create a Tag | `CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Tag` |
| `get` | retrieve an individual tag | `CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Tag` |
| `delete` | delete a tag | `CamelDigitalOceanName` _String_ | `com.myjeeva.digitalocean.pojo.Delete` |
| `update` | update a tag | `CamelDigitalOceanName` _String_,  
`CamelDigitalOceanNewName` _String_ | `com.myjeeva.digitalocean.pojo.Tag` |

## Examples

Get your account info

```java
from("direct:getAccountInfo")
    .setHeader(DigitalOceanConstants.OPERATION, constant(DigitalOceanOperations.get))
    .to("digitalocean:account?oAuthToken=XXXXXX")
```

Create a droplet

```java
from("direct:createDroplet")
    .setHeader(DigitalOceanConstants.OPERATION, constant("create"))
    .setHeader(DigitalOceanHeaders.NAME, constant("myDroplet"))
    .setHeader(DigitalOceanHeaders.REGION, constant("fra1"))
    .setHeader(DigitalOceanHeaders.DROPLET_IMAGE, constant("ubuntu-14-04-x64"))
    .setHeader(DigitalOceanHeaders.DROPLET_SIZE, constant("512mb"))
    .to("digitalocean:droplet?oAuthToken=XXXXXX")
```

List all your droplets

```java
from("direct:getDroplets")
    .setHeader(DigitalOceanConstants.OPERATION, constant("list"))
    .to("digitalocean:droplets?oAuthToken=XXXXXX")
```

Retrieve information for the Droplet (dropletId = 34772987)

```java
from("direct:getDroplet")
    .setHeader(DigitalOceanConstants.OPERATION, constant("get"))
    .setHeader(DigitalOceanConstants.ID, 34772987)
    .to("digitalocean:droplet?oAuthToken=XXXXXX")
```

Shutdown information for the Droplet (dropletId = 34772987)

```java
from("direct:shutdown")
    .setHeader(DigitalOceanConstants.ID, 34772987)
    .to("digitalocean:droplet?operation=shutdown&oAuthToken=XXXXXX")
```

## Spring Boot Auto-Configuration

When using digitalocean with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-digitalocean-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.digitalocean.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.digitalocean.enabled** | Whether to enable auto configuration of the digitalocean component. This is enabled by default. |  | Boolean |
| **camel.component.digitalocean.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |