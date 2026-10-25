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

The Web3j Ethereum Blockchain component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **addresses** (common) | Contract address or a comma separated list of addresses. |  | String |
| **configuration** (common) | Default configuration. |  | Web3jConfiguration |
| **fromAddress** (common) | The address the transaction is send from. |  | String |
| **fromBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **fullTransactionObjects** (common) | If true it returns the full transaction objects, if false only the hashes of the transactions. | false | boolean |
| **gasLimit** (common) | The maximum gas allowed in this block. |  | BigInteger |
| **operation** (common) | Operation to use. | transaction | String |
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

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **nodeAddress** (common) | **Required** Sets the node address used to communicate. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **addresses** (common) | Contract address or a comma separated list of addresses. |  | String |
| **fromAddress** (common) | The address the transaction is send from. |  | String |
| **fromBlock** (common) | The block number, or the string latest for the last mined block or pending, earliest for not yet mined transactions. | latest | String |
| **fullTransactionObjects** (common) | If true it returns the full transaction objects, if false only the hashes of the transactions. | false | boolean |
| **gasLimit** (common) | The maximum gas allowed in this block. |  | BigInteger |
| **operation** (common) | Operation to use. | transaction | String |
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

The Web3j Ethereum Blockchain component supports the following message header(s), which is/are listed below:

   
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

## Message Body

The message body at each side of the Web3j Ethereum Blockchain component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `text`, `pojo` or `null` | One message per item of the subscription of the operation: the hash of a block or a pending transaction as a String, an EthBlock.Block, a Transaction or a Log of web3j. No body on the message that ends the subscription (header CamelWeb3jStatus=done) or carries its error.
-   With `operation=ETH_BLOCK_HASH_OBSERVABLE`: `text` or `null` (`java.lang.String`)
    
-   With `operation=ETH_PENDING_TRANSACTION_HASH_OBSERVABLE`: `text` or `null` (`java.lang.String`)
    
-   With `operation=BLOCK_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=REPLAY_BLOCKS_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=TRANSACTION_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=PENDING_TRANSACTION_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=REPLAY_TRANSACTIONS_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=ETH_LOG_OBSERVABLE`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Log`)
    

Not known when `operation` is set.

 |
| **Producer input** | `any` | The operations take their input from headers and options, except WEB3\_SHA3, DB\_PUT\_STRING, DB\_PUT\_HEX and QUORUM\_GET\_PRIVATE\_PAYLOAD, which send the body converted to a String: a Map or a POJO is sent as its toString. |
| **Producer output** | `unchanged` | 

The result of the JSON-RPC call of the operation, selected by the CamelWeb3jOperation header or the operation option: a String for a hash, an address or hex data, a BigInteger for a quantity, a Boolean, a List, or a web3j object such as an EthBlock.Block, a Transaction (null when not found) or an Optional of a TransactionReceipt. On a JSON-RPC error the body is unchanged and the exchange fails, with the CamelWeb3jErrorCode, CamelWeb3jErrorData and CamelWeb3jErrorMessage headers.

-   With `operation=WEB3_CLIENT_VERSION`: `text` (`java.lang.String`)
    
-   With `operation=WEB3_SHA3`: `text` (`java.lang.String`)
    
-   With `operation=NET_VERSION`: `text` (`java.lang.String`)
    
-   With `operation=ETH_PROTOCOL_VERSION`: `text` (`java.lang.String`)
    
-   With `operation=ETH_COINBASE`: `text` (`java.lang.String`)
    
-   With `operation=ETH_GET_STORAGE_AT`: `text` (`java.lang.String`)
    
-   With `operation=ETH_GET_CODE`: `text` (`java.lang.String`)
    
-   With `operation=ETH_SIGN`: `text` (`java.lang.String`)
    
-   With `operation=ETH_SEND_TRANSACTION`: `text` (`java.lang.String`)
    
-   With `operation=ETH_SEND_RAW_TRANSACTION`: `text` (`java.lang.String`)
    
-   With `operation=ETH_CALL`: `text` (`java.lang.String`)
    
-   With `operation=ETH_COMPILE_LLL`: `text` (`java.lang.String`)
    
-   With `operation=ETH_COMPILE_SERPENT`: `text` (`java.lang.String`)
    
-   With `operation=DB_GET_STRING`: `text` (`java.lang.String`)
    
-   With `operation=DB_GET_HEX`: `text` (`java.lang.String`)
    
-   With `operation=SHH_VERSION`: `text` (`java.lang.String`)
    
-   With `operation=SHH_NEW_IDENTITY`: `text` (`java.lang.String`)
    
-   With `operation=SHH_NEW_GROUP`: `text` (`java.lang.String`)
    
-   With `operation=QUORUM_ETH_SEND_TRANSACTION`: `text` (`java.lang.String`)
    
-   With `operation=QUORUM_GET_PRIVATE_PAYLOAD`: `text` (`java.lang.String`)
    
-   With `operation=NET_PEER_COUNT`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_HASHRATE`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GAS_PRICE`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_BLOCK_NUMBER`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_BALANCE`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_TRANSACTION_COUNT`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_BLOCK_TRANSACTION_COUNT_BY_HASH`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_BLOCK_TRANSACTION_COUNT_BY_NUMBER`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_UNCLE_COUNT_BY_BLOCK_HASH`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_GET_UNCLE_COUNT_BY_BLOCK_NUMBER`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_ESTIMATE_GAS`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_NEW_FILTER`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_NEW_BLOCK_FILTER`: `value` (`java.math.BigInteger`)
    
-   With `operation=ETH_NEW_PENDING_TRANSACTION_FILTER`: `value` (`java.math.BigInteger`)
    
-   With `operation=SHH_NEW_FILTER`: `value` (`java.math.BigInteger`)
    
-   With `operation=NET_LISTENING`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_SYNCING`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_MINING`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_UNINSTALL_FILTER`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_SUBMIT_WORK`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_SUBMIT_HASHRATE`: `value` (`java.lang.Boolean`)
    
-   With `operation=DB_PUT_STRING`: `value` (`java.lang.Boolean`)
    
-   With `operation=DB_PUT_HEX`: `value` (`java.lang.Boolean`)
    
-   With `operation=SHH_POST`: `value` (`java.lang.Boolean`)
    
-   With `operation=SHH_HAS_IDENTITY`: `value` (`java.lang.Boolean`)
    
-   With `operation=SHH_ADD_TO_GROUP`: `value` (`java.lang.Boolean`)
    
-   With `operation=SHH_UNINSTALL_FILTER`: `value` (`java.lang.Boolean`)
    
-   With `operation=ETH_ACCOUNTS`: `list` (`java.util.List<java.lang.String>`)
    
-   With `operation=ETH_GET_COMPILERS`: `list` (`java.util.List<java.lang.String>`)
    
-   With `operation=ETH_GET_WORK`: `list` (`java.util.List<java.lang.String>`)
    
-   With `operation=ETH_GET_FILTER_CHANGES`: `list` (`java.util.List<org.web3j.protocol.core.methods.response.EthLog.LogResult<?>>`)
    
-   With `operation=ETH_GET_FILTER_LOGS`: `list` (`java.util.List<org.web3j.protocol.core.methods.response.EthLog.LogResult<?>>`)
    
-   With `operation=ETH_GET_LOGS`: `list` (`java.util.List<org.web3j.protocol.core.methods.response.EthLog.LogResult<?>>`)
    
-   With `operation=SHH_GET_FILTER_CHANGES`: `list` (`java.util.List<org.web3j.protocol.core.methods.response.ShhMessages.SshMessage>`)
    
-   With `operation=SHH_GET_MESSAGES`: `list` (`java.util.List<org.web3j.protocol.core.methods.response.ShhMessages.SshMessage>`)
    
-   With `operation=ETH_COMPILE_SOLIDITY`: `map` (`java.util.Map<java.lang.String, org.web3j.protocol.core.methods.response.EthCompileSolidity.Code>`)
    
-   With `operation=ETH_GET_BLOCK_BY_HASH`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=ETH_GET_BLOCK_BY_NUMBER`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=ETH_GET_UNCLE_BY_BLOCK_HASH_AND_INDEX`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=ETH_GET_UNCLE_BY_BLOCK_NUMBER_AND_INDEX`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.EthBlock.Block`)
    
-   With `operation=ETH_GET_TRANSACTION_BY_HASH`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=ETH_GET_TRANSACTION_BY_BLOCK_HASH_AND_INDEX`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=ETH_GET_TRANSACTION_BY_BLOCK_NUMBER_AND_INDEX`: `pojo` or `null` (`org.web3j.protocol.core.methods.response.Transaction`)
    
-   With `operation=ETH_GET_TRANSACTION_RECEIPT`: `pojo` (`java.util.Optional<org.web3j.protocol.core.methods.response.TransactionReceipt>`)
    
-   With `operation=QUORUM_NODE_INFO`: `pojo` (`org.web3j.protocol.core.methods.response.admin.AdminNodeInfo.NodeInfo`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

All URI options can also be set as exchange headers.

## Examples

Listen for new mined blocks and send the block hash to a jms queue:

-   Java
    
-   XML
    
-   YAML
    

```java
from("web3j://http://127.0.0.1:7545?operation=ETH_BLOCK_HASH_OBSERVABLE")
    .to("jms:queue:blocks");
```

```xml
<route>
  <from uri="web3j://http://127.0.0.1:7545?operation=ETH_BLOCK_HASH_OBSERVABLE"/>
  <to uri="jms:queue:blocks"/>
</route>
```

```yaml
- route:
    from:
      uri: "web3j://http://127.0.0.1:7545"
      parameters:
        operation: ETH_BLOCK_HASH_OBSERVABLE
      steps:
        - to:
            uri: jms:queue:blocks
```

Use the block hash code to retrieve the block and full transaction details:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:queue:blocks")
    .setHeader(BLOCK_HASH, body())
    .to("web3j://http://127.0.0.1:7545?operation=ETH_GET_BLOCK_BY_HASH&fullTransactionObjects=true");
```

```xml
<route>
  <from uri="jms:queue:blocks"/>
  <setHeader name="BLOCK_HASH">
    <simple>${body}</simple>
  </setHeader>
  <to uri="web3j://http://127.0.0.1:7545?operation=ETH_GET_BLOCK_BY_HASH&amp;fullTransactionObjects=true"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:queue:blocks
      steps:
        - setHeader:
            name: BLOCK_HASH
            simple: "${body}"
        - to:
            uri: "web3j://http://127.0.0.1:7545"
            parameters:
              operation: ETH_GET_BLOCK_BY_HASH
              fullTransactionObjects: true
```

Read the balance of an address at a specific block number:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("web3j://http://127.0.0.1:7545?operation=ETH_GET_BALANCE&address=0xc8CDceCE5d006dAB638029EBCf6Dd666efF5A952&atBlock=10");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="web3j://http://127.0.0.1:7545?operation=ETH_GET_BALANCE&amp;address=0xc8CDceCE5d006dAB638029EBCf6Dd666efF5A952&amp;atBlock=10"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "web3j://http://127.0.0.1:7545"
            parameters:
              operation: ETH_GET_BALANCE
              address: "0xc8CDceCE5d006dAB638029EBCf6Dd666efF5A952"
              atBlock: 10
```