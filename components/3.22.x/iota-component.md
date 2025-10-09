# IOTA

> **Warning**
> **Deprecated:** This iota is deprecated and may be removed in a future release.

**Since Camel 2.23**

**Only producer is supported**

According to IOTA Official site: "IOTA is the first open-source distributed ledger that is being built to power the future of the Internet of Things with feeless microtransactions and data integrity for machines."

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-iota</artifactId>
    <version>x.y.z</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

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

The IOTA component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The IOTA endpoint is configured using URI syntax:

iota:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** Component name. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **depth** (producer) | The depth determines how deep the tangle is analysed for getting Tips. | 9 | Integer |
| **minWeightMagnitude** (producer) | The minWeightMagnitude is the minimum number of zeroes that a proof-of-work output/transaction hash must end with to be considered valid by full nodes. | 14 | Integer |
| **operation** (producer) | 
**Required** Which operation to perform, one of: sendTransfer, getNewAddress, getTransfers.

Enum values:

-   sendTransfer
    
-   getNewAddress
    
-   getTransfers
    





 |  | String |
| **tag** (producer) | TAG. |  | String |
| **url** (producer) | **Required** Node url. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **securityLevel** (security) | Security level to be used for the private key / address. Can be 1, 2 or 3. | 1 | Integer |

## Message Headers

The IOTA component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIOTASeed** (producer) Constant: [`SEED_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#SEED_HEADER) | The tryte-encoded seed. |  | String |
| **CamelIOTAValue** (producer) Constant: [`VALUE_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#VALUE_HEADER) | The value to transfer. |  | Integer |
| **CamelIOTAToAddress** (producer) Constant: [`TO_ADDRESS_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#TO_ADDRESS_HEADER) | The address of the recipient. |  | String |
| **CamelIOTAAddressIndex** (producer) Constant: [`ADDRESS_INDEX_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#ADDRESS_INDEX_HEADER) | The key index to start search from. |  | Integer |
| **CamelIOTAAddressStartIndex** (producer) Constant: [`ADDRESS_START_INDEX_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#ADDRESS_START_INDEX_HEADER) | The starting key index, must be at least 0. |  | Integer |
| **CamelIOTAAddressEndIndex** (producer) Constant: [`ADDRESS_END_INDEX_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-iota/latest/org/apache/camel/component/iota/IOTAConstants.html#ADDRESS_END_INDEX_HEADER) | The ending key index, must be bigger then start. |  | Integer |

## Examples

The following route defined in Spring XML send a message to tangle

**Send message to tangle**

```xml
<route>
  <from uri="direct:start" />
  <setMessage>
  	<constant>Hello world!</constant>
  </setMessage>
  <setHeader name="CamelIOTASeed">
  	<constant>MYSEEDHERE</constant>
  </setHeader>
  <setHeader name="CamelIOTAValue">
  	<constant>1</constant>
  </setHeader>
  <setHeader name="CamelIOTAToAddress">
  	<constant>RECIPIENTADDRESS</constant>
  </setHeader>
  <setHeader name="CamelIOTAToAddress">
  	<constant>RECIPIENTADDRESS</constant>
  </setHeader>
  <to uri="iota:good?url=https://node.iota.org:443&amp;operation=sendTransfer" />
  <to uri="direct:result" />
</route>
```

The following route defined in Spring XML create a new address

**Create a new address**

```xml
<route>
  <from uri="direct:start" />
  <setHeader name="CamelIOTASeed">
  	<constant>MYSEEDHERE</constant>
  </setHeader>
  <setHeader name="CamelIOTAAddressIndex">
  	<constant>1</constant>
  </setHeader>
  <to uri="iota:good?url=https://node.iota.org:443&amp;operation=getNewAddress" />
  <to uri="direct:result" />
</route>
```

The following route defined in Spring XML retrieve transfers data

**Retrieve transfers**

```xml
<route>
  <from uri="direct:start" />
  <setHeader name="CamelIOTASeed">
  	<constant>MYSEEDHERE</constant>
  </setHeader>
  <setHeader name="CamelIOTAAddressStartIndex">
  	<constant>1</constant>
  </setHeader>
  <setHeader name="CamelIOTAAddressEndIndex">
  	<constant>10</constant>
  </setHeader>
  <to uri="iota:good?url=https://node.iota.org:443&amp;operation=getTransfers" />
  <to uri="direct:result" />
</route>
```

## Spring Boot Auto-Configuration

When using iota with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-iota-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.iota.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.iota.enabled** | Whether to enable auto configuration of the iota component. This is enabled by default. |  | Boolean |
| **camel.component.iota.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |