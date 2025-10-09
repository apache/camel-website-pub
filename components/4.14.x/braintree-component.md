# Braintree

**Since Camel 2.17**

**Only producer is supported**

The Braintree component provides access to [Braintree Payments](https://www.braintreepayments.com/) through their [Java SDK](https://developers.braintreepayments.com/start/hello-server/java).

All client applications need API credential to process payments. To use camel-braintree with your account, you’ll need to create a new [Sandbox](https://www.braintreepayments.com/get-started) or [Production](https://www.braintreepayments.com/signup) account.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-braintree</artifactId>
    <version>${camel-version}</version>
</dependency>
```

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

The Braintree component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Component configuration. |  | BraintreeConfiguration |

## Endpoint Options

The Braintree endpoint is configured using URI syntax:

braintree:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (producer) | 
**Required** What kind of operation to perform.

Enum values:

-   ADD\_ON
    
-   ADDRESS
    
-   CLIENT\_TOKEN
    
-   CREDIT\_CARD\_VERIFICATION
    
-   CUSTOMER
    
-   DISCOUNT
    
-   DISPUTE
    
-   DOCUMENT\_UPLOAD
    
-   MERCHANT\_ACCOUNT
    
-   PAYMENT\_METHOD
    
-   PAYMENT\_METHOD\_NONCE
    
-   OAUTH
    
-   PLAN
    
-   REPORT
    
-   SETTLEMENT\_BATCH\_SUMMARY
    
-   SUBSCRIPTION
    
-   TRANSACTION
    
-   US\_BANK\_ACCOUNT
    
-   WEBHOOK\_NOTIFICATION
    





 |  | BraintreeApiName |
| **methodName** (producer) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   accept
    
-   addFileEvidence
    
-   addTextEvidence
    
-   cancel
    
-   cancelRelease
    
-   cloneTransaction
    
-   create
    
-   createForCurrency
    
-   credit
    
-   delete
    
-   fetchMerchantAccounts
    
-   finalize
    
-   find
    
-   generate
    
-   grant
    
-   holdInEscrow
    
-   parse
    
-   refund
    
-   releaseFromEscrow
    
-   removeEvidence
    
-   retryCharge
    
-   revoke
    
-   sale
    
-   search
    
-   submitForPartialSettlement
    
-   submitForSettlement
    
-   transactionLevelFees
    
-   update
    
-   updateDetails
    
-   verify
    
-   voidTransaction
    





 |  | String |

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **environment** (producer) | The environment Either SANDBOX or PRODUCTION. |  | String |
| **inBody** (producer) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **merchantId** (producer) | The merchant id provided by Braintree. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpReadTimeout** (advanced) | Set read timeout for http calls. |  | Integer |
| **httpLogLevel** (logging) | 
Set logging level for http calls, see java.util.logging.Level.

Enum values:

-   OFF
    
-   SEVERE
    
-   WARNING
    
-   INFO
    
-   CONFIG
    
-   FINE
    
-   FINER
    
-   FINEST
    
-   ALL
    





 |  | String |
| **httpLogName** (logging) | Set log category to use to log http calls. | Braintree | String |
| **logHandlerEnabled** (logging) | Sets whether to enable the BraintreeLogHandler. It may be desirable to set this to 'false' where an existing JUL - SLF4J logger bridge is on the classpath. This option can also be configured globally on the BraintreeComponent. | true | boolean |
| **proxyHost** (proxy) | The proxy host. |  | String |
| **proxyPort** (proxy) | The proxy port. |  | Integer |
| **accessToken** (security) | The access token granted by a merchant to another in order to process transactions on their behalf. Used in place of environment, merchant id, public key and private key fields. |  | String |
| **privateKey** (security) | The private key provided by Braintree. |  | String |
| **publicKey** (security) | The public key provided by Braintree. |  | String |

## API Parameters (17 APIs)

The Braintree endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

braintree:apiName/methodName

There are 17 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**address**](#_api_address) | Producer | Provides methods to create, delete, find, and update Address objects |
| [**clientToken**](#_api_clientToken) | Producer | Generates client tokens, which are used to authenticate requests made directly on behalf of merchants This class does not need to be instantiated directly |
| [**creditCardVerification**](#_api_creditCardVerification) | Producer | To verify credit card information |
| [**customer**](#_api_customer) | Producer | Provides methods to create, delete, find, and update Customer objects |
| [**dispute**](#_api_dispute) | Producer | Provides methods to interact with Dispute objects |
| [**documentUpload**](#_api_documentUpload) | Producer | API to upload evidence documents |
| [**merchantAccount**](#_api_merchantAccount) | Producer | Provides methods to create, find, and update MerchantAccount objects |
| [**oauth**](#_api_oauth) | Producer | 
 |
| [**paymentMethod**](#_api_paymentMethod) | Producer | Provides methods to interact with payments |
| [**paymentMethodNonce**](#_api_paymentMethodNonce) | Producer | Provides methods to interact with nonce payments |
| [**plan**](#_api_plan) | Producer | 

 |
| [**report**](#_api_report) | Producer | Provides methods to interact with reports |
| [**settlementBatchSummary**](#_api_settlementBatchSummary) | Producer | Provides methods to interact wit settlement summaries |
| [**subscription**](#_api_subscription) | Producer | Provides methods to interact with Subscriptions |
| [**transaction**](#_api_transaction) | Producer | Provides methods to interact with Transactions |
| [**usBankAccount**](#_api_usBankAccount) | Producer | 

 |
| [**webhookNotification**](#_api_webhookNotification) | Producer | To retrieve notifications via webhooks |

Each API is documented in the following sections to come.

### API: address

**Only producer is supported**

The address API is defined in the syntax as follows:

```none
braintree:address/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_address_method_create) |  | Creates an Address for a Customer |
| [**delete**](#_api_address_method_delete) |  | Deletes a Customer’s Address |
| [**find**](#_api_address_method_find) |  | Finds a Customer’s Address |
| [**update**](#_api_address_method_update) |  | Updates a Customer’s Address |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Address> create(String customerId, com.braintreegateway.AddressRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **customerId** | The id of the Customer | String |
| **request** | The request object | AddressRequest |

#### Method delete

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Address> delete(String customerId, String id);
    

The braintree/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **customerId** | The id of the Customer | String |
| **id** | The id of the Address to delete | String |

#### Method find

Signatures:

-   com.braintreegateway.Address find(String customerId, String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **customerId** | The id of the Customer | String |
| **id** | The id of the Address | String |

#### Method update

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Address> update(String customerId, String id, com.braintreegateway.AddressRequest request);
    

The braintree/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **customerId** | The id of the Customer | String |
| **id** | The id of the Address | String |
| **request** | The request object containing the AddressRequest parameters | AddressRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: clientToken

**Only producer is supported**

The clientToken API is defined in the syntax as follows:

```none
braintree:clientToken/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**generate**](#_api_clientToken_method_generate) |  | 
 |

#### Method generate

Signatures:

-   String generate();
    
-   String generate(com.braintreegateway.ClientTokenRequest request);
    

The braintree/generate API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | ClientTokenRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: creditCardVerification

**Only producer is supported**

The creditCardVerification API is defined in the syntax as follows:

```none
braintree:creditCardVerification/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_creditCardVerification_method_create) |  | 
 |
| [**find**](#_api_creditCardVerification_method_find) |  | 

 |
| [**search**](#_api_creditCardVerification_method_search) |  | 

 |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.CreditCardVerification> create(com.braintreegateway.CreditCardVerificationRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | CreditCardVerificationRequest |

#### Method find

Signatures:

-   com.braintreegateway.CreditCardVerification find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | String |

#### Method search

Signatures:

-   com.braintreegateway.ResourceCollection<com.braintreegateway.CreditCardVerification> search(com.braintreegateway.CreditCardVerificationSearchRequest query);
    

The braintree/search API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **query** | 
 | CreditCardVerificationSearchRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: customer

**Only producer is supported**

The customer API is defined in the syntax as follows:

```none
braintree:customer/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**all**](#_api_customer_method_all) |  | Finds all Customers and returns a ResourceCollection |
| [**create**](#_api_customer_method_create) |  | Creates a Customer |
| [**delete**](#_api_customer_method_delete) |  | Deletes a Customer by id |
| [**find**](#_api_customer_method_find) |  | Finds a Customer by id |
| [**search**](#_api_customer_method_search) |  | Finds all Transactions that match the query and returns a ResourceCollection |
| [**update**](#_api_customer_method_update) |  | Updates a Customer |

#### Method all

Signatures:

-   com.braintreegateway.ResourceCollection<com.braintreegateway.Customer> all();
    

The braintree/all API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Customer> create(com.braintreegateway.CustomerRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | The request | CustomerRequest |

#### Method delete

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Customer> delete(String id);
    

The braintree/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The id of the Customer | String |

#### Method find

Signatures:

-   com.braintreegateway.Customer find(String id);
    
-   com.braintreegateway.Customer find(String id, String associationFilterId);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **associationFilterId** | The id of the association filter to use | String |
| **id** | The id of the Customer | String |

#### Method search

Signatures:

-   com.braintreegateway.ResourceCollection<com.braintreegateway.Customer> search(com.braintreegateway.CustomerSearchRequest query);
    

The braintree/search API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **query** | The request query to use for search | CustomerSearchRequest |

#### Method update

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Customer> update(String id, com.braintreegateway.CustomerRequest request);
    

The braintree/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The id of the Customer | String |
| **request** | The request | CustomerRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: dispute

**Only producer is supported**

The dispute API is defined in the syntax as follows:

```none
braintree:dispute/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**accept**](#_api_dispute_method_accept) |  | Accept a Dispute, given a dispute ID |
| [**addFileEvidence**](#_api_dispute_method_addFileEvidence) |  | Add File Evidence to a Dispute, given an ID and a FileEvidenceRequest File evidence request |
| [**addTextEvidence**](#_api_dispute_method_addTextEvidence) |  | Add Text Evidence to a Dispute, given an ID and content |
| [**finalize**](#_api_dispute_method_finalize) |  | Finalize a Dispute, given an ID |
| [**find**](#_api_dispute_method_find) |  | Returns a Dispute, given an ID |
| [**removeEvidence**](#_api_dispute_method_removeEvidence) |  | Remove Evidence from a Dispute, given an ID and a DisputeEvidence ID |
| [**search**](#_api_dispute_method_search) |  | Finds all Disputes that match the query |

#### Method accept

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Dispute> accept(String id);
    

The braintree/accept API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The dispute id to accept | String |

#### Method addFileEvidence

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.DisputeEvidence> addFileEvidence(String disputeId, String documentId);
    
-   com.braintreegateway.Result<com.braintreegateway.DisputeEvidence> addFileEvidence(String disputeId, com.braintreegateway.FileEvidenceRequest fileEvidenceRequest);
    

The braintree/addFileEvidence API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **disputeId** | The dispute id to add text evidence to | String |
| **documentId** | The document id of a previously uploaded document | String |
| **fileEvidenceRequest** | The file evidence request for the dispute | FileEvidenceRequest |

#### Method addTextEvidence

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.DisputeEvidence> addTextEvidence(String id, String content);
    
-   com.braintreegateway.Result<com.braintreegateway.DisputeEvidence> addTextEvidence(String id, com.braintreegateway.TextEvidenceRequest textEvidenceRequest);
    

The braintree/addTextEvidence API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The content of the text evidence for the dispute | String |
| **id** | The dispute id to add text evidence to | String |
| **textEvidenceRequest** | The text evidence request for the dispute | TextEvidenceRequest |

#### Method finalize

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Dispute> finalize(String id);
    

The braintree/finalize API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The dispute id to finalize | String |

#### Method find

Signatures:

-   com.braintreegateway.Dispute find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The dispute id to find | String |

#### Method removeEvidence

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Dispute> removeEvidence(String disputeId, String evidenceId);
    

The braintree/removeEvidence API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **disputeId** | The dispute id to remove evidence from | String |
| **evidenceId** | The evidence id to remove | String |

#### Method search

Signatures:

-   com.braintreegateway.PaginatedCollection<com.braintreegateway.Dispute> search(com.braintreegateway.DisputeSearchRequest query);
    

The braintree/search API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **query** | The query for what disputes to find | DisputeSearchRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: documentUpload

**Only producer is supported**

The documentUpload API is defined in the syntax as follows:

```none
braintree:documentUpload/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_documentUpload_method_create) |  | 
 |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.DocumentUpload> create(com.braintreegateway.DocumentUploadRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | DocumentUploadRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: merchantAccount

**Only producer is supported**

The merchantAccount API is defined in the syntax as follows:

```none
braintree:merchantAccount/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**all**](#_api_merchantAccount_method_all) |  | 
 |
| [**createForCurrency**](#_api_merchantAccount_method_createForCurrency) |  | 

 |
| [**fetchMerchantAccounts**](#_api_merchantAccount_method_fetchMerchantAccounts) |  | 

 |
| [**find**](#_api_merchantAccount_method_find) |  | 

 |

#### Method all

Signatures:

-   com.braintreegateway.PaginatedCollection<com.braintreegateway.MerchantAccount> all();
    

The braintree/all API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method createForCurrency

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.MerchantAccount> createForCurrency(com.braintreegateway.MerchantAccountCreateForCurrencyRequest request);
    

The braintree/createForCurrency API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **currencyRequest** | 
 | MerchantAccountCreateForCurrencyRequest |

#### Method fetchMerchantAccounts

Signatures:

-   com.braintreegateway.PaginatedResult<com.braintreegateway.MerchantAccount> fetchMerchantAccounts(int page);
    

The braintree/fetchMerchantAccounts API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **page** | 
 | Integer |

#### Method find

Signatures:

-   com.braintreegateway.MerchantAccount find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: oauth

**Only producer is supported**

The oauth API is defined in the syntax as follows:

```none
braintree:oauth/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**connectUrl**](#_api_oauth_method_connectUrl) |  | 
 |
| [**createTokenFromCode**](#_api_oauth_method_createTokenFromCode) |  | 

 |
| [**createTokenFromRefreshToken**](#_api_oauth_method_createTokenFromRefreshToken) |  | 

 |
| [**revokeAccessToken**](#_api_oauth_method_revokeAccessToken) |  | 

 |

#### Method connectUrl

Signatures:

-   String connectUrl(com.braintreegateway.OAuthConnectUrlRequest request);
    

The braintree/connectUrl API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **connectRequest** | 
 | OAuthConnectUrlRequest |

#### Method createTokenFromCode

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.OAuthCredentials> createTokenFromCode(com.braintreegateway.OAuthCredentialsRequest request);
    

The braintree/createTokenFromCode API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | OAuthCredentialsRequest |

#### Method createTokenFromRefreshToken

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.OAuthCredentials> createTokenFromRefreshToken(com.braintreegateway.OAuthCredentialsRequest request);
    

The braintree/createTokenFromRefreshToken API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | OAuthCredentialsRequest |

#### Method revokeAccessToken

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.OAuthResult> revokeAccessToken(String accessToken);
    

The braintree/revokeAccessToken API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **accessToken** | 
 | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: paymentMethod

**Only producer is supported**

The paymentMethod API is defined in the syntax as follows:

```none
braintree:paymentMethod/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_paymentMethod_method_create) |  | 
 |
| [**delete**](#_api_paymentMethod_method_delete) |  | 

 |
| [**find**](#_api_paymentMethod_method_find) |  | 

 |
| [**grant**](#_api_paymentMethod_method_grant) |  | 

 |
| [**revoke**](#_api_paymentMethod_method_revoke) |  | 

 |
| [**update**](#_api_paymentMethod_method_update) |  | 

 |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.? extends PaymentMethod> create(com.braintreegateway.PaymentMethodRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | PaymentMethodRequest |

#### Method delete

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.? extends PaymentMethod> delete(String token);
    
-   com.braintreegateway.Result<com.braintreegateway.? extends PaymentMethod> delete(String token, com.braintreegateway.PaymentMethodDeleteRequest request);
    

The braintree/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **deleteRequest** | 
 | PaymentMethodDeleteRequest |
| **token** | 

 | String |

#### Method find

Signatures:

-   com.braintreegateway.PaymentMethod find(String token);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **token** | 
 | String |

#### Method grant

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.PaymentMethodNonce> grant(String token);
    
-   com.braintreegateway.Result<com.braintreegateway.PaymentMethodNonce> grant(String token, com.braintreegateway.PaymentMethodGrantRequest grantRequest);
    

The braintree/grant API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **grantRequest** | 
 | PaymentMethodGrantRequest |
| **token** | 

 | String |

#### Method revoke

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.? extends PaymentMethod> revoke(String token);
    

The braintree/revoke API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **token** | 
 | String |

#### Method update

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.? extends PaymentMethod> update(String token, com.braintreegateway.PaymentMethodRequest request);
    

The braintree/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | PaymentMethodRequest |
| **token** | 

 | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: paymentMethodNonce

**Only producer is supported**

The paymentMethodNonce API is defined in the syntax as follows:

```none
braintree:paymentMethodNonce/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_paymentMethodNonce_method_create) |  | 
 |
| [**find**](#_api_paymentMethodNonce_method_find) |  | 

 |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.PaymentMethodNonce> create(String paymentMethodToken);
    
-   com.braintreegateway.Result<com.braintreegateway.PaymentMethodNonce> create(com.braintreegateway.PaymentMethodNonceRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **paymentMethodToken** | 
 | String |
| **request** | 

 | PaymentMethodNonceRequest |

#### Method find

Signatures:

-   com.braintreegateway.PaymentMethodNonce find(String paymentMethodNonce);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **paymentMethodNonce** | 
 | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: plan

**Only producer is supported**

The plan API is defined in the syntax as follows:

```none
braintree:plan/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**all**](#_api_plan_method_all) |  | 
 |
| [**create**](#_api_plan_method_create) |  | 

 |
| [**find**](#_api_plan_method_find) |  | 

 |
| [**update**](#_api_plan_method_update) |  | 

 |

#### Method all

Signatures:

-   java.util.List<com.braintreegateway.Plan> all();
    

The braintree/all API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Plan> create(com.braintreegateway.PlanRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | PlanRequest |

#### Method find

Signatures:

-   com.braintreegateway.Plan find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | String |

#### Method update

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Plan> update(String id, com.braintreegateway.PlanRequest request);
    

The braintree/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | String |
| **request** | 

 | PlanRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: report

**Only producer is supported**

The report API is defined in the syntax as follows:

```none
braintree:report/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**transactionLevelFees**](#_api_report_method_transactionLevelFees) |  | Retrieves a Transaction-Level Fee Report |

#### Method transactionLevelFees

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.TransactionLevelFeeReport> transactionLevelFees(com.braintreegateway.TransactionLevelFeeReportRequest request);
    

The braintree/transactionLevelFees API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | The request | TransactionLevelFeeReportRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: settlementBatchSummary

**Only producer is supported**

The settlementBatchSummary API is defined in the syntax as follows:

```none
braintree:settlementBatchSummary/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**generate**](#_api_settlementBatchSummary_method_generate) |  | 
 |

#### Method generate

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.SettlementBatchSummary> generate(java.util.Calendar settlementDate);
    
-   com.braintreegateway.Result<com.braintreegateway.SettlementBatchSummary> generate(java.util.Calendar settlementDate, String groupByCustomField);
    

The braintree/generate API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupByCustomField** | 
 | String |
| **settlementDate** | 

 | Calendar |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: subscription

**Only producer is supported**

The subscription API is defined in the syntax as follows:

```none
braintree:subscription/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**cancel**](#_api_subscription_method_cancel) |  | Cancels the Subscription with the given id |
| [**create**](#_api_subscription_method_create) |  | Creates a Subscription |
| [**delete**](#_api_subscription_method_delete) |  | 
 |
| [**find**](#_api_subscription_method_find) |  | Finds a Subscription by id |
| [**retryCharge**](#_api_subscription_method_retryCharge) |  | 

 |
| [**search**](#_api_subscription_method_search) |  | Search for a Subscription |
| [**update**](#_api_subscription_method_update) |  | Updates a Subscription |

#### Method cancel

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Subscription> cancel(String id);
    

The braintree/cancel API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the Subscription to cancel | String |

#### Method create

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Subscription> create(com.braintreegateway.SubscriptionRequest request);
    

The braintree/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | The request | SubscriptionRequest |

#### Method delete

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Subscription> delete(String customerId, String id);
    

The braintree/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **customerId** | 
 | String |
| **id** | 

 | String |

#### Method find

Signatures:

-   com.braintreegateway.Subscription find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The id of the Subscription | String |

#### Method retryCharge

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> retryCharge(String subscriptionId);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> retryCharge(String subscriptionId, Boolean submitForSettlement);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> retryCharge(String subscriptionId, java.math.BigDecimal amount);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> retryCharge(String subscriptionId, java.math.BigDecimal amount, Boolean submitForSettlement);
    

The braintree/retryCharge API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **amount** | 
 | BigDecimal |
| **submitForSettlement** | 

 | Boolean |
| **subscriptionId** | 

 | String |

#### Method search

Signatures:

-   com.braintreegateway.ResourceCollection<com.braintreegateway.Subscription> search(com.braintreegateway.SubscriptionSearchRequest searchRequest);
    

The braintree/search API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **searchRequest** | The SubscriptionSearchRequest | SubscriptionSearchRequest |

#### Method update

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Subscription> update(String id, com.braintreegateway.SubscriptionRequest request);
    

The braintree/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The id of the Subscription | String |
| **request** | The request | SubscriptionRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: transaction

**Only producer is supported**

The transaction API is defined in the syntax as follows:

```none
braintree:transaction/methodName?[parameters]
```

The 15 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**adjustAuthorization**](#_api_transaction_method_adjustAuthorization) |  | Submits the transaction with the given id to be adjusted for the given amount which must be less than or equal to the authorization amount |
| [**cancelRelease**](#_api_transaction_method_cancelRelease) |  | Cancels a pending release of a transaction with the given id from escrow |
| [**cloneTransaction**](#_api_transaction_method_cloneTransaction) |  | 
 |
| [**credit**](#_api_transaction_method_credit) |  | Creates a credit Transaction |
| [**find**](#_api_transaction_method_find) |  | Finds a Transaction by id |
| [**packageTracking**](#_api_transaction_method_packageTracking) |  | Supplement the transaction with package tracking details |
| [**refund**](#_api_transaction_method_refund) |  | Refunds all or part of a previous sale Transaction |
| [**releaseFromEscrow**](#_api_transaction_method_releaseFromEscrow) |  | Submits the transaction with the given id for release |
| [**sale**](#_api_transaction_method_sale) |  | Creates a sale Transaction |
| [**search**](#_api_transaction_method_search) |  | Finds all Transactions that match the query and returns a ResourceCollection |
| [**submitForPartialSettlement**](#_api_transaction_method_submitForPartialSettlement) |  | Submits a partial settlement transaction for the given id |
| [**submitForSettlement**](#_api_transaction_method_submitForSettlement) |  | Submits the transaction with the given id to be settled along with a TransactionRequest object |
| [**updateCustomFields**](#_api_transaction_method_updateCustomFields) |  | Updates custom field values for a given transaction |
| [**updateDetails**](#_api_transaction_method_updateDetails) |  | Updates details for a transaction that has been submitted for settlement |
| [**voidTransaction**](#_api_transaction_method_voidTransaction) |  | Voids the transaction with the given id |

#### Method adjustAuthorization

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> adjustAuthorization(String id, com.braintreegateway.TransactionRequest request);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> adjustAuthorization(String id, java.math.BigDecimal amount);
    

The braintree/adjustAuthorization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **amount** | To be adjusted | BigDecimal |
| **id** | Of the transaction to to be adjusted | String |
| **request** | Is the TransactionRequest object with amount details | TransactionRequest |

#### Method cancelRelease

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> cancelRelease(String id);
    

The braintree/cancelRelease API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction to cancel release from escrow of | String |

#### Method cloneTransaction

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> cloneTransaction(String id, com.braintreegateway.TransactionCloneRequest request);
    

The braintree/cloneTransaction API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **cloneRequest** | 
 | TransactionCloneRequest |
| **id** | 

 | String |

#### Method credit

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> credit(com.braintreegateway.TransactionRequest request);
    

The braintree/credit API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | The request | TransactionRequest |

#### Method find

Signatures:

-   com.braintreegateway.Transaction find(String id);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The id of the Transaction | String |

#### Method packageTracking

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> packageTracking(String id, com.braintreegateway.PackageTrackingRequest packageTrackingRequest);
    

The braintree/packageTracking API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction to supplement the package details for | String |
| **packageTrackingRequest** | The package tracking request related to the transaction | PackageTrackingRequest |

#### Method refund

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> refund(String id);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> refund(String id, com.braintreegateway.TransactionRefundRequest request);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> refund(String id, java.math.BigDecimal amount);
    

The braintree/refund API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **amount** | 
 | BigDecimal |
| **id** | 

 | String |
| **refundRequest** | 

 | TransactionRefundRequest |

#### Method releaseFromEscrow

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> releaseFromEscrow(String id);
    

The braintree/releaseFromEscrow API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction to submit for release | String |

#### Method sale

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> sale(com.braintreegateway.TransactionRequest request);
    

The braintree/sale API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | The request | TransactionRequest |

#### Method search

Signatures:

-   com.braintreegateway.ResourceCollection<com.braintreegateway.Transaction> search(com.braintreegateway.TransactionSearchRequest query);
    

The braintree/search API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **query** | The search query | TransactionSearchRequest |

#### Method submitForPartialSettlement

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> submitForPartialSettlement(String id, com.braintreegateway.TransactionRequest request);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> submitForPartialSettlement(String id, java.math.BigDecimal amount);
    

The braintree/submitForPartialSettlement API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **amount** | Of the partial settlement | BigDecimal |
| **id** | Of the transaction to add the partial settlement transaction for | String |
| **request** | The request | TransactionRequest |

#### Method submitForSettlement

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> submitForSettlement(String id);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> submitForSettlement(String id, com.braintreegateway.TransactionRequest request);
    
-   com.braintreegateway.Result<com.braintreegateway.Transaction> submitForSettlement(String id, java.math.BigDecimal amount);
    

The braintree/submitForSettlement API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **amount** | To settle. must be less than or equal to the authorization amount. | BigDecimal |
| **id** | Of the transaction to submit for settlement | String |
| **request** | The request | TransactionRequest |

#### Method updateCustomFields

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> updateCustomFields(String id, com.braintreegateway.TransactionRequest request);
    

The braintree/updateCustomFields API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction being updated | String |
| **request** | A TransactionRequest object containing custom field info.. | TransactionRequest |

#### Method updateDetails

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> updateDetails(String id, com.braintreegateway.TransactionRequest request);
    

The braintree/updateDetails API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction to update the details for | String |
| **request** | The request | TransactionRequest |

#### Method voidTransaction

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> voidTransaction(String id);
    

The braintree/voidTransaction API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | Of the transaction to void | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: usBankAccount

**Only producer is supported**

The usBankAccount API is defined in the syntax as follows:

```none
braintree:usBankAccount/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**find**](#_api_usBankAccount_method_find) |  | 
 |
| [**sale**](#_api_usBankAccount_method_sale) |  | 

 |

#### Method find

Signatures:

-   com.braintreegateway.UsBankAccount find(String token);
    

The braintree/find API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **token** | 
 | String |

#### Method sale

Signatures:

-   com.braintreegateway.Result<com.braintreegateway.Transaction> sale(String token, com.braintreegateway.TransactionRequest transactionRequest);
    

The braintree/sale API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **token** | 
 | String |
| **transactionRequest** | 

 | TransactionRequest |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

### API: webhookNotification

**Only producer is supported**

The webhookNotification API is defined in the syntax as follows:

```none
braintree:webhookNotification/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**parse**](#_api_webhookNotification_method_parse) |  | 
 |
| [**parseWithoutSignatureVerification**](#_api_webhookNotification_method_parseWithoutSignatureVerification) |  | 

 |
| [**verify**](#_api_webhookNotification_method_verify) |  | 

 |

#### Method parse

Signatures:

-   com.braintreegateway.WebhookNotification parse(String signature, String payload);
    

The braintree/parse API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **payload** | 
 | String |
| **signature** | 

 | String |

#### Method parseWithoutSignatureVerification

Signatures:

-   com.braintreegateway.WebhookNotification parseWithoutSignatureVerification(String payload);
    

The braintree/parseWithoutSignatureVerification API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **payload** | 
 | String |

#### Method verify

Signatures:

-   String verify(String challenge);
    

The braintree/verify API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **challenge** | 
 | String |

In addition to the parameters above, the braintree API can also use any of the [Query Parameters (13 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBraintree.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBraintree.myParameterNameHere` header.

## Examples

```java
from("direct://GENERATE")
    .to("braintree://sclientToken/generate");
```

## More Information

For more information on the endpoints and options see Braintree references at [https://developers.braintreepayments.com/reference/overview](https://developers.braintreepayments.com/reference/overview)

## Spring Boot Auto-Configuration

When using braintree with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-braintree-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.braintree.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.braintree.configuration** | Component configuration. The option is a org.apache.camel.component.braintree.BraintreeConfiguration type. |  | BraintreeConfiguration |
| **camel.component.braintree.enabled** | Whether to enable auto configuration of the braintree component. This is enabled by default. |  | Boolean |
| **camel.component.braintree.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |