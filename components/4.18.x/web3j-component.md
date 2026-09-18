# Web3j Ethereum Blockchain

**Since Camel 2.22**

**Both producer and consumer are supported**

The Ethereum blockchain component uses the [web3j](https://github.com/web3j/web3j) client API and allows you to interact with Ethereum compatible nodes such as:

-   [Geth](https://github.com/ethereum/go-ethereum/wiki/geth)
    
-   [Parity](https://github.com/paritytech/parity)
    
-   [Quorum](https://github.com/jpmorganchase/quorum/wiki)
    
-   [Infura](https://infura.io)
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-web3j</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

web3j://<local/remote host:port or local IPC path>\[?options\]

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

The Web3j Ethereum Blockchain component supports 38 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **addresses** (common) | Contract address or a comma separated list of addresses. |  | String |
| **configuration** (common) | Default configuration. |  | Web3jConfiguration |
| **fromAddress** (common) | The address the transaction is send from. |  | String |
| **fromBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **fullTransactionObjects** (common) | If true it returns the full transaction objects, if false only the hashes of the transactions. | false | boolean |
| **gasLimit** (common) | The maximum gas allowed in this block. |  | BigInteger |
| **privateFor** (common) | A comma separated transaction privateFor nodes with public keys in a Quorum network. |  | String |
| **quorumAPI** (common) | If true, this will support Quorum API. | false | boolean |
| **toAddress** (common) | The address the transaction is directed to. |  | String |
| **toBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **topics** (common) | Topics are order-dependent. Each topic can also be a list of topics. Specify multiple topics separated by comma. |  | String |
| **web3j** (common) | The preconfigured Web3j object. |  | Web3j |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **address** (producer) | Contract address. |  | String |
| **atBlock** (producer) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **blockHash** (producer) | Hash of the block where this transaction was in. |  | String |
| **clientId** (producer) | A random hexadecimal(32 bytes) ID identifying the client. |  | String |
| **data** (producer) | The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. |  | String |
| **databaseName** (producer) | The local database name. |  | String |
| **filterId** (producer) | The filter id to use. |  | BigInteger |
| **gasPrice** (producer) | Gas price used for each paid gas. |  | BigInteger |
| **hashrate** (producer) | A hexadecimal string representation (32 bytes) of the hash rate. |  | String |
| **headerPowHash** (producer) | The header’s pow-hash (256 bits) used for submitting a proof-of-work solution. |  | String |
| **index** (producer) | The transactions/uncle index position in the block. |  | BigInteger |
| **keyName** (producer) | The key name in the database. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mixDigest** (producer) | The mix digest (256 bits) used for submitting a proof-of-work solution. |  | String |
| **nonce** (producer) | The nonce found (64 bits) used for submitting a proof-of-work solution. |  | String |
| **operation** (producer) | Operation to use. | transaction | String |
| **position** (producer) | The transaction index position withing a block. |  | BigInteger |
| **priority** (producer) | The priority of a whisper message. |  | BigInteger |
| **sha3HashOfDataToSign** (producer) | Message to sign by calculating an Ethereum specific signature. |  | String |
| **signedTransactionData** (producer) | The signed transaction data for a new message call transaction or a contract creation for signed transactions. |  | String |
| **sourceCode** (producer) | The source code to compile. |  | String |
| **transactionHash** (producer) | The information about a transaction requested by transaction hash. |  | String |
| **ttl** (producer) | The time to live in seconds of a whisper message. |  | BigInteger |
| **value** (producer) | The value sent within a transaction. |  | BigInteger |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Web3j Ethereum Blockchain endpoint is configured using URI syntax:

web3j:nodeAddress

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **nodeAddress** (common) | **Required** Sets the node address used to communicate. |  | String |

### Query Parameters (38 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **addresses** (common) | Contract address or a comma separated list of addresses. |  | String |
| **fromAddress** (common) | The address the transaction is send from. |  | String |
| **fromBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **fullTransactionObjects** (common) | If true it returns the full transaction objects, if false only the hashes of the transactions. | false | boolean |
| **gasLimit** (common) | The maximum gas allowed in this block. |  | BigInteger |
| **privateFor** (common) | A comma separated transaction privateFor nodes with public keys in a Quorum network. |  | String |
| **quorumAPI** (common) | If true, this will support Quorum API. | false | boolean |
| **toAddress** (common) | The address the transaction is directed to. |  | String |
| **toBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **topics** (common) | Topics are order-dependent. Each topic can also be a list of topics. Specify multiple topics separated by comma. |  | String |
| **web3j** (common) | The preconfigured Web3j object. |  | Web3j |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **address** (producer) | Contract address. |  | String |
| **atBlock** (producer) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **blockHash** (producer) | Hash of the block where this transaction was in. |  | String |
| **clientId** (producer) | A random hexadecimal(32 bytes) ID identifying the client. |  | String |
| **data** (producer) | The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. |  | String |
| **databaseName** (producer) | The local database name. |  | String |
| **filterId** (producer) | The filter id to use. |  | BigInteger |
| **gasPrice** (producer) | Gas price used for each paid gas. |  | BigInteger |
| **hashrate** (producer) | A hexadecimal string representation (32 bytes) of the hash rate. |  | String |
| **headerPowHash** (producer) | The header’s pow-hash (256 bits) used for submitting a proof-of-work solution. |  | String |
| **index** (producer) | The transactions/uncle index position in the block. |  | BigInteger |
| **keyName** (producer) | The key name in the database. |  | String |
| **mixDigest** (producer) | The mix digest (256 bits) used for submitting a proof-of-work solution. |  | String |
| **nonce** (producer) | The nonce found (64 bits) used for submitting a proof-of-work solution. |  | String |
| **operation** (producer) | Operation to use. | transaction | String |
| **position** (producer) | The transaction index position withing a block. |  | BigInteger |
| **priority** (producer) | The priority of a whisper message. |  | BigInteger |
| **sha3HashOfDataToSign** (producer) | Message to sign by calculating an Ethereum specific signature. |  | String |
| **signedTransactionData** (producer) | The signed transaction data for a new message call transaction or a contract creation for signed transactions. |  | String |
| **sourceCode** (producer) | The source code to compile. |  | String |
| **transactionHash** (producer) | The information about a transaction requested by transaction hash. |  | String |
| **ttl** (producer) | The time to live in seconds of a whisper message. |  | BigInteger |
| **value** (producer) | The value sent within a transaction. |  | BigInteger |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Web3j Ethereum Blockchain component supports 39 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWeb3jEthHashrate** (producer) Constant: [`ETH_HASHRATE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ETH_HASHRATE) | A hexadecimal string representation (32 bytes) of the hash rate. |  | String |
| **CamelWeb3jId** (producer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ID) | The id. |  | Long |
| **CamelWeb3jOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelWeb3jAtBlock** (producer) Constant: [`AT_BLOCK`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#AT_BLOCK) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. |  | String |
| **CamelWeb3jAddress** (producer) Constant: [`ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ADDRESS) | Contract address. |  | String |
| **CamelWeb3jAddresses** (producer) Constant: [`ADDRESSES`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ADDRESSES) | Contract address or a list of addresses. |  | List |
| **CamelWeb3jFromAddress** (producer) Constant: [`FROM_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#FROM_ADDRESS) | The address the transaction is send from. |  | String |
| **CamelWeb3jToAddress** (producer) Constant: [`TO_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#TO_ADDRESS) | The address the transaction is directed to. |  | String |
| **CamelWeb3jPosition** (producer) Constant: [`POSITION`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#POSITION) | The transaction index position withing a block. |  | String |
| **CamelWeb3jBlockHash** (producer) Constant: [`BLOCK_HASH`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#BLOCK_HASH) | Hash of the block where this transaction was in. |  | String |
| **CamelWeb3jTransactionHash** (producer) Constant: [`TRANSACTION_HASH`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#TRANSACTION_HASH) | The information about a transaction requested by transaction hash. |  | String |
| **CamelWeb3jSha3HashOfDataToSign** (producer) Constant: [`SHA3_HASH_OF_DATA_TO_SIGN`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#SHA3_HASH_OF_DATA_TO_SIGN) | Message to sign by calculating an Ethereum specific signature. |  | String |
| **CamelWeb3jSignedTransactionData** (producer) Constant: [`SIGNED_TRANSACTION_DATA`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#SIGNED_TRANSACTION_DATA) | The signed transaction data for a new message call transaction or a contract creation for signed transactions. |  | String |
| **CamelWeb3jFullTransactionObjects** (producer) Constant: [`FULL_TRANSACTION_OBJECTS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#FULL_TRANSACTION_OBJECTS) | If true it returns the full transaction objects, if false only the hashes of the transactions. |  | Boolean |
| **CamelWeb3jIndex** (producer) Constant: [`INDEX`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#INDEX) | The transactions/uncle index position in the block. |  | String |
| **CamelWeb3jSourceCode** (producer) Constant: [`SOURCE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#SOURCE_CODE) | The source code to compile. |  | String |
| **CamelWeb3jFilterId** (producer) Constant: [`FILTER_ID`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#FILTER_ID) | The filter id to use. |  | BigInteger |
| **CamelWeb3jDatabaseName** (producer) Constant: [`DATABASE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#DATABASE_NAME) | The local database name. |  | String |
| **CamelWeb3jKeyName** (producer) Constant: [`KEY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#KEY_NAME) | The key name in the database. |  | String |
| **CamelWeb3jNonce** (producer) Constant: [`NONCE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#NONCE) | The nonce found (64 bits) used for submitting a proof-of-work solution. |  | BigInteger |
| **CamelWeb3jHeaderPowHash** (producer) Constant: [`HEADER_POW_HASH`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#HEADER_POW_HASH) | The header’s pow-hash (256 bits) used for submitting a proof-of-work solution. |  | String |
| **CamelWeb3jMixDigest** (producer) Constant: [`MIX_DIGEST`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#MIX_DIGEST) | The mix digest (256 bits) used for submitting a proof-of-work solution. |  | String |
| **CamelWeb3jClientId** (producer) Constant: [`CLIENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#CLIENT_ID) | A random hexadecimal(32 bytes) ID identifying the client. |  | String |
| **CamelWeb3jGasPrice** (producer) Constant: [`GAS_PRICE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#GAS_PRICE) | Gas price used for each paid gas. |  | BigInteger |
| **CamelWeb3jGasLimit** (producer) Constant: [`GAS_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#GAS_LIMIT) | The maximum gas allowed in this block. |  | BigInteger |
| **CamelWeb3jValue** (producer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#VALUE) | The value sent within a transaction. |  | BigInteger |
| **CamelWeb3jData** (producer) Constant: [`DATA`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#DATA) | The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. |  | String |
| **CamelWeb3jFromBlock** (producer) Constant: [`FROM_BLOCK`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#FROM_BLOCK) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. |  | String |
| **CamelWeb3jToBlock** (producer) Constant: [`TO_BLOCK`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#TO_BLOCK) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. |  | String |
| **CamelWeb3jTopics** (producer) Constant: [`TOPICS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#TOPICS) | Topics are order-dependent. Each topic can also be a list of topics. Specify multiple topics separated by comma. |  | List |
| **CamelWeb3jPriority** (producer) Constant: [`PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#PRIORITY) | The priority of a whisper message. |  | BigInteger |
| **CamelWeb3jTtl** (producer) Constant: [`TTL`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#TTL) | The time to live in seconds of a whisper message. |  | BigInteger |
| **CamelWeb3jPrivateFor** (producer) Constant: [`PRIVATE_FOR`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#PRIVATE_FOR) | A transaction privateFor nodes with public keys in a Quorum network. |  | List |
| **CamelWeb3jPrivateFrom** (producer) Constant: [`PRIVATE_FROM`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#PRIVATE_FROM) | A transaction privateFrom. |  | String |
| **CamelWeb3jErrorCode** (producer) Constant: [`ERROR_CODE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ERROR_CODE) | The error code. |  | int |
| **CamelWeb3jErrorData** (producer) Constant: [`ERROR_DATA`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ERROR_DATA) | The error data. |  | String |
| **CamelWeb3jErrorMessage** (producer) Constant: [`ERROR_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#ERROR_MESSAGE) | The error message. |  | String |
| **CamelWeb3jStatus** (consumer) Constant: [`HEADER_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#HEADER_STATUS) | The status of the operation. |  | String |
| **CamelWeb3jHeaderOperation** (consumer) Constant: [`HEADER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-web3j/latest/org/apache/camel/component/web3j/Web3jConstants.html#HEADER_OPERATION) | The operation. |  | String |

All URI options can also be set as exchange headers.

## Examples

Listen for new mined blocks and send the block hash to a jms queue:

```java
from("web3j://http://127.0.0.1:7545?operation=ETH_BLOCK_HASH_OBSERVABLE")
    .to("jms:queue:blocks");
```

Use the block hash code to retrieve the block and full transaction details:

```java
from("jms:queue:blocks")
    .setHeader(BLOCK_HASH, body())
    .to("web3j://http://127.0.0.1:7545?operation=ETH_GET_BLOCK_BY_HASH&fullTransactionObjects=true");
```

Read the balance of an address at a specific block number:

```java
from("direct:start")
    .to("web3j://http://127.0.0.1:7545?operation=ETH_GET_BALANCE&address=0xc8CDceCE5d006dAB638029EBCf6Dd666efF5A952&atBlock=10");
```

## Spring Boot Auto-Configuration

When using web3j with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-web3j-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 39 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.web3j.address** | Contract address. |  | String |
| **camel.component.web3j.addresses** | Contract address or a comma separated list of addresses. |  | String |
| **camel.component.web3j.at-block** | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **camel.component.web3j.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.web3j.block-hash** | Hash of the block where this transaction was in. |  | String |
| **camel.component.web3j.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.web3j.client-id** | A random hexadecimal(32 bytes) ID identifying the client. |  | String |
| **camel.component.web3j.configuration** | Default configuration. The option is a org.apache.camel.component.web3j.Web3jConfiguration type. |  | Web3jConfiguration |
| **camel.component.web3j.data** | The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. |  | String |
| **camel.component.web3j.database-name** | The local database name. |  | String |
| **camel.component.web3j.enabled** | Whether to enable auto configuration of the web3j component. This is enabled by default. |  | Boolean |
| **camel.component.web3j.filter-id** | The filter id to use. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.from-address** | The address the transaction is send from. |  | String |
| **camel.component.web3j.from-block** | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **camel.component.web3j.full-transaction-objects** | If true it returns the full transaction objects, if false only the hashes of the transactions. | false | Boolean |
| **camel.component.web3j.gas-limit** | The maximum gas allowed in this block. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.gas-price** | Gas price used for each paid gas. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.hashrate** | A hexadecimal string representation (32 bytes) of the hash rate. |  | String |
| **camel.component.web3j.header-pow-hash** | The header’s pow-hash (256 bits) used for submitting a proof-of-work solution. |  | String |
| **camel.component.web3j.index** | The transactions/uncle index position in the block. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.key-name** | The key name in the database. |  | String |
| **camel.component.web3j.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.web3j.mix-digest** | The mix digest (256 bits) used for submitting a proof-of-work solution. |  | String |
| **camel.component.web3j.nonce** | The nonce found (64 bits) used for submitting a proof-of-work solution. |  | String |
| **camel.component.web3j.operation** | Operation to use. | transaction | String |
| **camel.component.web3j.position** | The transaction index position withing a block. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.priority** | The priority of a whisper message. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.private-for** | A comma separated transaction privateFor nodes with public keys in a Quorum network. |  | String |
| **camel.component.web3j.quorum-a-p-i** | If true, this will support Quorum API. | false | Boolean |
| **camel.component.web3j.sha3-hash-of-data-to-sign** | Message to sign by calculating an Ethereum specific signature. |  | String |
| **camel.component.web3j.signed-transaction-data** | The signed transaction data for a new message call transaction or a contract creation for signed transactions. |  | String |
| **camel.component.web3j.source-code** | The source code to compile. |  | String |
| **camel.component.web3j.to-address** | The address the transaction is directed to. |  | String |
| **camel.component.web3j.to-block** | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **camel.component.web3j.topics** | Topics are order-dependent. Each topic can also be a list of topics. Specify multiple topics separated by comma. |  | String |
| **camel.component.web3j.transaction-hash** | The information about a transaction requested by transaction hash. |  | String |
| **camel.component.web3j.ttl** | The time to live in seconds of a whisper message. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.value** | The value sent within a transaction. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.web3j.web3j** | The preconfigured Web3j object. The option is a org.web3j.protocol.Web3j type. |  | Web3j |