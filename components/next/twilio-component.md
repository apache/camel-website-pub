# Twilio

**Since Camel 2.20**

**Both producer and consumer are supported**

The Twilio component provides access to Version 2010-04-01 of Twilio REST APIs accessible using [Twilio Java SDK](https://github.com/twilio/twilio-java).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-twilio</artifactId>
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

The Twilio component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the shared configuration. |  | TwilioConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **restClient** (advanced) | **Autowired** To use the shared REST client. |  | TwilioRestClient |
| **accountSid** (security) | The account SID to use. |  | String |
| **password** (security) | Auth token for the account. |  | String |
| **username** (security) | The account to use. |  | String |

## Endpoint Options

The Twilio endpoint is configured using URI syntax:

twilio:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   ACCOUNT
    
-   ADDRESS
    
-   APPLICATION
    
-   AVAILABLE\_PHONE\_NUMBER\_COUNTRY
    
-   CALL
    
-   CONFERENCE
    
-   CONNECT\_APP
    
-   INCOMING\_PHONE\_NUMBER
    
-   KEY
    
-   MESSAGE
    
-   NEW\_KEY
    
-   NEW\_SIGNING\_KEY
    
-   NOTIFICATION
    
-   OUTGOING\_CALLER\_ID
    
-   QUEUE
    
-   RECORDING
    
-   SHORT\_CODE
    
-   SIGNING\_KEY
    
-   TOKEN
    
-   TRANSCRIPTION
    
-   VALIDATION\_REQUEST
    
-   ADDRESS\_DEPENDENT\_PHONE\_NUMBER
    
-   AVAILABLE\_PHONE\_NUMBER\_COUNTRY\_LOCAL
    
-   AVAILABLE\_PHONE\_NUMBER\_COUNTRY\_MOBILE
    
-   AVAILABLE\_PHONE\_NUMBER\_COUNTRY\_TOLL\_FREE
    
-   CALL\_NOTIFICATION
    
-   CALL\_RECORDING
    
-   CONFERENCE\_PARTICIPANT
    
-   INCOMING\_PHONE\_NUMBER\_LOCAL
    
-   INCOMING\_PHONE\_NUMBER\_MOBILE
    
-   INCOMING\_PHONE\_NUMBER\_TOLL\_FREE
    
-   MESSAGE\_FEEDBACK
    
-   MESSAGE\_MEDIA
    
-   QUEUE\_MEMBER
    
-   RECORDING\_ADD\_ON\_RESULT
    
-   RECORDING\_TRANSCRIPTION
    
-   RECORDING\_ADD\_ON\_RESULT\_PAYLOAD
    
-   SIP\_CREDENTIAL\_LIST
    
-   SIP\_DOMAIN
    
-   SIP\_IP\_ACCESS\_CONTROL\_LIST
    
-   SIP\_CREDENTIAL\_LIST\_CREDENTIAL
    
-   SIP\_DOMAIN\_CREDENTIAL\_LIST\_MAPPING
    
-   SIP\_DOMAIN\_IP\_ACCESS\_CONTROL\_LIST\_MAPPING
    
-   SIP\_IP\_ACCESS\_CONTROL\_LIST\_IP\_ADDRESS
    
-   USAGE\_RECORD
    
-   USAGE\_TRIGGER
    
-   USAGE\_RECORD\_ALL\_TIME
    
-   USAGE\_RECORD\_DAILY
    
-   USAGE\_RECORD\_LAST\_MONTH
    
-   USAGE\_RECORD\_MONTHLY
    
-   USAGE\_RECORD\_THIS\_MONTH
    
-   USAGE\_RECORD\_TODAY
    
-   USAGE\_RECORD\_YEARLY
    
-   USAGE\_RECORD\_YESTERDAY
    





 |  | TwilioApiName |
| **methodName** (common) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   create
    
-   delete
    
-   fetch
    
-   read
    
-   update
    





 |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |

## API Parameters (54 APIs)

The Twilio endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

twilio:apiName/methodName

There are 54 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**account**](#_api_account) | Both | 
 |
| [**address**](#_api_address) | Both | 

 |
| [**address-dependent-phone-number**](#_api_address-dependent-phone-number) | Both | 

 |
| [**application**](#_api_application) | Both | 

 |
| [**available-phone-number-country**](#_api_available-phone-number-country) | Both | 

 |
| [**available-phone-number-country-local**](#_api_available-phone-number-country-local) | Both | 

 |
| [**available-phone-number-country-mobile**](#_api_available-phone-number-country-mobile) | Both | 

 |
| [**available-phone-number-country-toll-free**](#_api_available-phone-number-country-toll-free) | Both | 

 |
| [**call**](#_api_call) | Both | 

 |
| [**call-notification**](#_api_call-notification) | Both | 

 |
| [**call-recording**](#_api_call-recording) | Both | 

 |
| [**conference**](#_api_conference) | Both | 

 |
| [**conference-participant**](#_api_conference-participant) | Both | 

 |
| [**connect-app**](#_api_connect-app) | Both | 

 |
| [**incoming-phone-number**](#_api_incoming-phone-number) | Both | 

 |
| [**incoming-phone-number-local**](#_api_incoming-phone-number-local) | Both | 

 |
| [**incoming-phone-number-mobile**](#_api_incoming-phone-number-mobile) | Both | 

 |
| [**incoming-phone-number-toll-free**](#_api_incoming-phone-number-toll-free) | Both | 

 |
| [**key**](#_api_key) | Both | 

 |
| [**message**](#_api_message) | Both | 

 |
| [**message-feedback**](#_api_message-feedback) | Both | 

 |
| [**message-media**](#_api_message-media) | Both | 

 |
| [**new-key**](#_api_new-key) | Both | 

 |
| [**new-signing-key**](#_api_new-signing-key) | Both | 

 |
| [**notification**](#_api_notification) | Both | 

 |
| [**outgoing-caller-id**](#_api_outgoing-caller-id) | Both | 

 |
| [**queue**](#_api_queue) | Both | 

 |
| [**queue-member**](#_api_queue-member) | Both | 

 |
| [**recording**](#_api_recording) | Both | 

 |
| [**recording-add-on-result**](#_api_recording-add-on-result) | Both | 

 |
| [**recording-add-on-result-payload**](#_api_recording-add-on-result-payload) | Both | 

 |
| [**recording-transcription**](#_api_recording-transcription) | Both | 

 |
| [**short-code**](#_api_short-code) | Both | 

 |
| [**signing-key**](#_api_signing-key) | Both | 

 |
| [**sip-credential-list**](#_api_sip-credential-list) | Both | 

 |
| [**sip-credential-list-credential**](#_api_sip-credential-list-credential) | Both | 

 |
| [**sip-domain**](#_api_sip-domain) | Both | 

 |
| [**sip-domain-credential-list-mapping**](#_api_sip-domain-credential-list-mapping) | Both | 

 |
| [**sip-domain-ip-access-control-list-mapping**](#_api_sip-domain-ip-access-control-list-mapping) | Both | 

 |
| [**sip-ip-access-control-list**](#_api_sip-ip-access-control-list) | Both | 

 |
| [**sip-ip-access-control-list-ip-address**](#_api_sip-ip-access-control-list-ip-address) | Both | 

 |
| [**token**](#_api_token) | Both | 

 |
| [**transcription**](#_api_transcription) | Both | 

 |
| [**usage-record**](#_api_usage-record) | Both | 

 |
| [**usage-record-all-time**](#_api_usage-record-all-time) | Both | 

 |
| [**usage-record-daily**](#_api_usage-record-daily) | Both | 

 |
| [**usage-record-last-month**](#_api_usage-record-last-month) | Both | 

 |
| [**usage-record-monthly**](#_api_usage-record-monthly) | Both | 

 |
| [**usage-record-this-month**](#_api_usage-record-this-month) | Both | 

 |
| [**usage-record-today**](#_api_usage-record-today) | Both | 

 |
| [**usage-record-yearly**](#_api_usage-record-yearly) | Both | 

 |
| [**usage-record-yesterday**](#_api_usage-record-yesterday) | Both | 

 |
| [**usage-trigger**](#_api_usage-trigger) | Both | 

 |
| [**validation-request**](#_api_validation-request) | Both | 

 |

Each API is documented in the following sections to come.

### API: account

**Both producer and consumer are supported**

The account API is defined in the syntax as follows:

```none
twilio:account/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_account_method_creator) | create | 
 |
| [**fetcher**](#_api_account_method_fetcher) | fetch | 

 |
| [**reader**](#_api_account_method_reader) | read | 

 |
| [**updater**](#_api_account_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.AccountCreator creator();
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.AccountFetcher fetcher();
    
-   com.twilio.rest.api.v2010.AccountFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathSid** | 
 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.AccountReader reader();
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.AccountUpdater updater();
    
-   com.twilio.rest.api.v2010.AccountUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: address

**Both producer and consumer are supported**

The address API is defined in the syntax as follows:

```none
twilio:address/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_address_method_creator) | create | 
 |
| [**deleter**](#_api_address_method_deleter) | delete | 

 |
| [**fetcher**](#_api_address_method_fetcher) | fetch | 

 |
| [**reader**](#_api_address_method_reader) | read | 

 |
| [**updater**](#_api_address_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.AddressCreator creator(String customerName, String street, String city, String region, String postalCode, String isoCountry);
    
-   com.twilio.rest.api.v2010.account.AddressCreator creator(String pathAccountSid, String customerName, String street, String city, String region, String postalCode, String isoCountry);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **city** | 
 | String |
| **customerName** | 

 | String |
| **isoCountry** | 

 | String |
| **pathAccountSid** | 

 | String |
| **postalCode** | 

 | String |
| **region** | 

 | String |
| **street** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.AddressDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.AddressDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.AddressFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.AddressFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.AddressReader reader();
    
-   com.twilio.rest.api.v2010.account.AddressReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.AddressUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.AddressUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: address-dependent-phone-number

**Both producer and consumer are supported**

The address-dependent-phone-number API is defined in the syntax as follows:

```none
twilio:address-dependent-phone-number/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_address-dependent-phone-number_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.address.DependentPhoneNumberReader reader(String pathAccountSid, String pathAddressSid);
    
-   com.twilio.rest.api.v2010.account.address.DependentPhoneNumberReader reader(String pathAddressSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathAddressSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: application

**Both producer and consumer are supported**

The application API is defined in the syntax as follows:

```none
twilio:application/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_application_method_creator) | create | 
 |
| [**deleter**](#_api_application_method_deleter) | delete | 

 |
| [**fetcher**](#_api_application_method_fetcher) | fetch | 

 |
| [**reader**](#_api_application_method_reader) | read | 

 |
| [**updater**](#_api_application_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.ApplicationCreator creator();
    
-   com.twilio.rest.api.v2010.account.ApplicationCreator creator(String pathAccountSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.ApplicationDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ApplicationDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.ApplicationFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ApplicationFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.ApplicationReader reader();
    
-   com.twilio.rest.api.v2010.account.ApplicationReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.ApplicationUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ApplicationUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: available-phone-number-country

**Both producer and consumer are supported**

The available-phone-number-country API is defined in the syntax as follows:

```none
twilio:available-phone-number-country/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_available-phone-number-country_method_fetcher) | fetch | 
 |
| [**reader**](#_api_available-phone-number-country_method_reader) | read | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.AvailablePhoneNumberCountryFetcher fetcher(String pathAccountSid, String pathCountryCode);
    
-   com.twilio.rest.api.v2010.account.AvailablePhoneNumberCountryFetcher fetcher(String pathCountryCode);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCountryCode** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.AvailablePhoneNumberCountryReader reader();
    
-   com.twilio.rest.api.v2010.account.AvailablePhoneNumberCountryReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: available-phone-number-country-local

**Both producer and consumer are supported**

The available-phone-number-country-local API is defined in the syntax as follows:

```none
twilio:available-phone-number-country-local/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_available-phone-number-country-local_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.LocalReader reader(String pathAccountSid, String pathCountryCode);
    
-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.LocalReader reader(String pathCountryCode);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCountryCode** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: available-phone-number-country-mobile

**Both producer and consumer are supported**

The available-phone-number-country-mobile API is defined in the syntax as follows:

```none
twilio:available-phone-number-country-mobile/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_available-phone-number-country-mobile_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.MobileReader reader(String pathAccountSid, String pathCountryCode);
    
-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.MobileReader reader(String pathCountryCode);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCountryCode** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: available-phone-number-country-toll-free

**Both producer and consumer are supported**

The available-phone-number-country-toll-free API is defined in the syntax as follows:

```none
twilio:available-phone-number-country-toll-free/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_available-phone-number-country-toll-free_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.TollFreeReader reader(String pathAccountSid, String pathCountryCode);
    
-   com.twilio.rest.api.v2010.account.availablephonenumbercountry.TollFreeReader reader(String pathCountryCode);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCountryCode** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: call

**Both producer and consumer are supported**

The call API is defined in the syntax as follows:

```none
twilio:call/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_call_method_creator) | create | 
 |
| [**deleter**](#_api_call_method_deleter) | delete | 

 |
| [**fetcher**](#_api_call_method_fetcher) | fetch | 

 |
| [**reader**](#_api_call_method_reader) | read | 

 |
| [**updater**](#_api_call_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.CallCreator creator(String pathAccountSid, com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, String applicationSid);
    
-   com.twilio.rest.api.v2010.account.CallCreator creator(String pathAccountSid, com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, com.twilio.type.Twiml twiml);
    
-   com.twilio.rest.api.v2010.account.CallCreator creator(String pathAccountSid, com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, java.net.URI url);
    
-   com.twilio.rest.api.v2010.account.CallCreator creator(com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, String applicationSid);
    
-   com.twilio.rest.api.v2010.account.CallCreator creator(com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, com.twilio.type.Twiml twiml);
    
-   com.twilio.rest.api.v2010.account.CallCreator creator(com.twilio.type.Endpoint to, com.twilio.type.Endpoint from, java.net.URI url);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **applicationSid** | 
 | String |
| **from** | 

 | Endpoint |
| **pathAccountSid** | 

 | String |
| **to** | 

 | Endpoint |
| **twiml** | 

 | Twiml |
| **url** | 

 | URI |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.CallDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.CallDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.CallFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.CallFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.CallReader reader();
    
-   com.twilio.rest.api.v2010.account.CallReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.CallUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.CallUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: call-notification

**Both producer and consumer are supported**

The call-notification API is defined in the syntax as follows:

```none
twilio:call-notification/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_call-notification_method_fetcher) | fetch | 
 |
| [**reader**](#_api_call-notification_method_reader) | read | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.call.NotificationFetcher fetcher(String pathAccountSid, String pathCallSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.call.NotificationFetcher fetcher(String pathCallSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.call.NotificationReader reader(String pathAccountSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.call.NotificationReader reader(String pathCallSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: call-recording

**Both producer and consumer are supported**

The call-recording API is defined in the syntax as follows:

```none
twilio:call-recording/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_call-recording_method_creator) | create | 
 |
| [**deleter**](#_api_call-recording_method_deleter) | delete | 

 |
| [**fetcher**](#_api_call-recording_method_fetcher) | fetch | 

 |
| [**reader**](#_api_call-recording_method_reader) | read | 

 |
| [**updater**](#_api_call-recording_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.call.RecordingCreator creator(String pathAccountSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.call.RecordingCreator creator(String pathCallSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.call.RecordingDeleter deleter(String pathAccountSid, String pathCallSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.call.RecordingDeleter deleter(String pathCallSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.call.RecordingFetcher fetcher(String pathAccountSid, String pathCallSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.call.RecordingFetcher fetcher(String pathCallSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.call.RecordingReader reader(String pathAccountSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.call.RecordingReader reader(String pathCallSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.call.RecordingUpdater updater(String pathAccountSid, String pathCallSid, String pathSid, com.twilio.rest.api.v2010.account.call.Recording.Status status);
    
-   com.twilio.rest.api.v2010.account.call.RecordingUpdater updater(String pathCallSid, String pathSid, com.twilio.rest.api.v2010.account.call.Recording.Status status);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathSid** | 

 | String |
| **status** | 

 | Status |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: conference

**Both producer and consumer are supported**

The conference API is defined in the syntax as follows:

```none
twilio:conference/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_conference_method_fetcher) | fetch | 
 |
| [**reader**](#_api_conference_method_reader) | read | 

 |
| [**updater**](#_api_conference_method_updater) | update | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.ConferenceFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ConferenceFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.ConferenceReader reader();
    
-   com.twilio.rest.api.v2010.account.ConferenceReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.ConferenceUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ConferenceUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: conference-participant

**Both producer and consumer are supported**

The conference-participant API is defined in the syntax as follows:

```none
twilio:conference-participant/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_conference-participant_method_creator) | create | 
 |
| [**deleter**](#_api_conference-participant_method_deleter) | delete | 

 |
| [**fetcher**](#_api_conference-participant_method_fetcher) | fetch | 

 |
| [**reader**](#_api_conference-participant_method_reader) | read | 

 |
| [**updater**](#_api_conference-participant_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.conference.ParticipantCreator creator(String pathAccountSid, String pathConferenceSid, com.twilio.type.Endpoint from, com.twilio.type.Endpoint to);
    
-   com.twilio.rest.api.v2010.account.conference.ParticipantCreator creator(String pathConferenceSid, com.twilio.type.Endpoint from, com.twilio.type.Endpoint to);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **from** | 
 | Endpoint |
| **pathAccountSid** | 

 | String |
| **pathConferenceSid** | 

 | String |
| **to** | 

 | Endpoint |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.conference.ParticipantDeleter deleter(String pathAccountSid, String pathConferenceSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.conference.ParticipantDeleter deleter(String pathConferenceSid, String pathCallSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathConferenceSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.conference.ParticipantFetcher fetcher(String pathAccountSid, String pathConferenceSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.conference.ParticipantFetcher fetcher(String pathConferenceSid, String pathCallSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathConferenceSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.conference.ParticipantReader reader(String pathAccountSid, String pathConferenceSid);
    
-   com.twilio.rest.api.v2010.account.conference.ParticipantReader reader(String pathConferenceSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathConferenceSid** | 

 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.conference.ParticipantUpdater updater(String pathAccountSid, String pathConferenceSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.conference.ParticipantUpdater updater(String pathConferenceSid, String pathCallSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathConferenceSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: connect-app

**Both producer and consumer are supported**

The connect-app API is defined in the syntax as follows:

```none
twilio:connect-app/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_connect-app_method_deleter) | delete | 
 |
| [**fetcher**](#_api_connect-app_method_fetcher) | fetch | 

 |
| [**reader**](#_api_connect-app_method_reader) | read | 

 |
| [**updater**](#_api_connect-app_method_updater) | update | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.ConnectAppDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ConnectAppDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.ConnectAppFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ConnectAppFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.ConnectAppReader reader();
    
-   com.twilio.rest.api.v2010.account.ConnectAppReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.ConnectAppUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ConnectAppUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: incoming-phone-number

**Both producer and consumer are supported**

The incoming-phone-number API is defined in the syntax as follows:

```none
twilio:incoming-phone-number/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_incoming-phone-number_method_creator) | create | 
 |
| [**deleter**](#_api_incoming-phone-number_method_deleter) | delete | 

 |
| [**fetcher**](#_api_incoming-phone-number_method_fetcher) | fetch | 

 |
| [**reader**](#_api_incoming-phone-number_method_reader) | read | 

 |
| [**updater**](#_api_incoming-phone-number_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberCreator creator(String areaCode);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberCreator creator(String pathAccountSid, String areaCode);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber phoneNumber);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberCreator creator(com.twilio.type.PhoneNumber phoneNumber);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **areaCode** | 
 | String |
| **pathAccountSid** | 

 | String |
| **phoneNumber** | 

 | PhoneNumber |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberReader reader();
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.IncomingPhoneNumberUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: incoming-phone-number-local

**Both producer and consumer are supported**

The incoming-phone-number-local API is defined in the syntax as follows:

```none
twilio:incoming-phone-number-local/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_incoming-phone-number-local_method_creator) | create | 
 |
| [**reader**](#_api_incoming-phone-number-local_method_reader) | read | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.LocalCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber phoneNumber);
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.LocalCreator creator(com.twilio.type.PhoneNumber phoneNumber);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **phoneNumber** | 

 | PhoneNumber |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.LocalReader reader();
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.LocalReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: incoming-phone-number-mobile

**Both producer and consumer are supported**

The incoming-phone-number-mobile API is defined in the syntax as follows:

```none
twilio:incoming-phone-number-mobile/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_incoming-phone-number-mobile_method_creator) | create | 
 |
| [**reader**](#_api_incoming-phone-number-mobile_method_reader) | read | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.MobileCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber phoneNumber);
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.MobileCreator creator(com.twilio.type.PhoneNumber phoneNumber);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **phoneNumber** | 

 | PhoneNumber |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.MobileReader reader();
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.MobileReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: incoming-phone-number-toll-free

**Both producer and consumer are supported**

The incoming-phone-number-toll-free API is defined in the syntax as follows:

```none
twilio:incoming-phone-number-toll-free/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_incoming-phone-number-toll-free_method_creator) | create | 
 |
| [**reader**](#_api_incoming-phone-number-toll-free_method_reader) | read | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.TollFreeCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber phoneNumber);
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.TollFreeCreator creator(com.twilio.type.PhoneNumber phoneNumber);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **phoneNumber** | 

 | PhoneNumber |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.incomingphonenumber.TollFreeReader reader();
    
-   com.twilio.rest.api.v2010.account.incomingphonenumber.TollFreeReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: key

**Both producer and consumer are supported**

The key API is defined in the syntax as follows:

```none
twilio:key/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_key_method_deleter) | delete | 
 |
| [**fetcher**](#_api_key_method_fetcher) | fetch | 

 |
| [**reader**](#_api_key_method_reader) | read | 

 |
| [**updater**](#_api_key_method_updater) | update | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.KeyDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.KeyDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.KeyFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.KeyFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.KeyReader reader();
    
-   com.twilio.rest.api.v2010.account.KeyReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.KeyUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.KeyUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: message

**Both producer and consumer are supported**

The message API is defined in the syntax as follows:

```none
twilio:message/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_message_method_creator) | create | 
 |
| [**deleter**](#_api_message_method_deleter) | delete | 

 |
| [**fetcher**](#_api_message_method_fetcher) | fetch | 

 |
| [**reader**](#_api_message_method_reader) | read | 

 |
| [**updater**](#_api_message_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.MessageCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber to, String messagingServiceSid, String body);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber to, String messagingServiceSid, java.util.List<java.net.URI> mediaUrl);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber to, com.twilio.type.PhoneNumber from, String body);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber to, com.twilio.type.PhoneNumber from, java.util.List<java.net.URI> mediaUrl);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(com.twilio.type.PhoneNumber to, String messagingServiceSid, String body);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(com.twilio.type.PhoneNumber to, String messagingServiceSid, java.util.List<java.net.URI> mediaUrl);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(com.twilio.type.PhoneNumber to, com.twilio.type.PhoneNumber from, String body);
    
-   com.twilio.rest.api.v2010.account.MessageCreator creator(com.twilio.type.PhoneNumber to, com.twilio.type.PhoneNumber from, java.util.List<java.net.URI> mediaUrl);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **body** | 
 | String |
| **from** | 

 | PhoneNumber |
| **mediaUrl** | 

 | List |
| **messagingServiceSid** | 

 | String |
| **pathAccountSid** | 

 | String |
| **to** | 

 | PhoneNumber |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.MessageDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.MessageDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.MessageFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.MessageFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.MessageReader reader();
    
-   com.twilio.rest.api.v2010.account.MessageReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.MessageUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.MessageUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: message-feedback

**Both producer and consumer are supported**

The message-feedback API is defined in the syntax as follows:

```none
twilio:message-feedback/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_message-feedback_method_creator) | create | 
 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.message.FeedbackCreator creator(String pathAccountSid, String pathMessageSid);
    
-   com.twilio.rest.api.v2010.account.message.FeedbackCreator creator(String pathMessageSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathMessageSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: message-media

**Both producer and consumer are supported**

The message-media API is defined in the syntax as follows:

```none
twilio:message-media/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_message-media_method_deleter) | delete | 
 |
| [**fetcher**](#_api_message-media_method_fetcher) | fetch | 

 |
| [**reader**](#_api_message-media_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.message.MediaDeleter deleter(String pathAccountSid, String pathMessageSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.message.MediaDeleter deleter(String pathMessageSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathMessageSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.message.MediaFetcher fetcher(String pathAccountSid, String pathMessageSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.message.MediaFetcher fetcher(String pathMessageSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathMessageSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.message.MediaReader reader(String pathAccountSid, String pathMessageSid);
    
-   com.twilio.rest.api.v2010.account.message.MediaReader reader(String pathMessageSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathMessageSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: new-key

**Both producer and consumer are supported**

The new-key API is defined in the syntax as follows:

```none
twilio:new-key/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_new-key_method_creator) | create | 
 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.NewKeyCreator creator();
    
-   com.twilio.rest.api.v2010.account.NewKeyCreator creator(String pathAccountSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: new-signing-key

**Both producer and consumer are supported**

The new-signing-key API is defined in the syntax as follows:

```none
twilio:new-signing-key/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_new-signing-key_method_creator) | create | 
 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.NewSigningKeyCreator creator();
    
-   com.twilio.rest.api.v2010.account.NewSigningKeyCreator creator(String pathAccountSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: notification

**Both producer and consumer are supported**

The notification API is defined in the syntax as follows:

```none
twilio:notification/methodName?[parameters]
```

The 2 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_notification_method_fetcher) | fetch | 
 |
| [**reader**](#_api_notification_method_reader) | read | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.NotificationFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.NotificationFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.NotificationReader reader();
    
-   com.twilio.rest.api.v2010.account.NotificationReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: outgoing-caller-id

**Both producer and consumer are supported**

The outgoing-caller-id API is defined in the syntax as follows:

```none
twilio:outgoing-caller-id/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_outgoing-caller-id_method_deleter) | delete | 
 |
| [**fetcher**](#_api_outgoing-caller-id_method_fetcher) | fetch | 

 |
| [**reader**](#_api_outgoing-caller-id_method_reader) | read | 

 |
| [**updater**](#_api_outgoing-caller-id_method_updater) | update | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.OutgoingCallerIdDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.OutgoingCallerIdDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.OutgoingCallerIdFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.OutgoingCallerIdFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.OutgoingCallerIdReader reader();
    
-   com.twilio.rest.api.v2010.account.OutgoingCallerIdReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.OutgoingCallerIdUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.OutgoingCallerIdUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: queue

**Both producer and consumer are supported**

The queue API is defined in the syntax as follows:

```none
twilio:queue/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_queue_method_creator) | create | 
 |
| [**deleter**](#_api_queue_method_deleter) | delete | 

 |
| [**fetcher**](#_api_queue_method_fetcher) | fetch | 

 |
| [**reader**](#_api_queue_method_reader) | read | 

 |
| [**updater**](#_api_queue_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.QueueCreator creator(String friendlyName);
    
-   com.twilio.rest.api.v2010.account.QueueCreator creator(String pathAccountSid, String friendlyName);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **pathAccountSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.QueueDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.QueueDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.QueueFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.QueueFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.QueueReader reader();
    
-   com.twilio.rest.api.v2010.account.QueueReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.QueueUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.QueueUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: queue-member

**Both producer and consumer are supported**

The queue-member API is defined in the syntax as follows:

```none
twilio:queue-member/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_queue-member_method_fetcher) | fetch | 
 |
| [**reader**](#_api_queue-member_method_reader) | read | 

 |
| [**updater**](#_api_queue-member_method_updater) | update | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.queue.MemberFetcher fetcher(String pathAccountSid, String pathQueueSid, String pathCallSid);
    
-   com.twilio.rest.api.v2010.account.queue.MemberFetcher fetcher(String pathQueueSid, String pathCallSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathQueueSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.queue.MemberReader reader(String pathAccountSid, String pathQueueSid);
    
-   com.twilio.rest.api.v2010.account.queue.MemberReader reader(String pathQueueSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathQueueSid** | 

 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.queue.MemberUpdater updater(String pathAccountSid, String pathQueueSid, String pathCallSid, java.net.URI url);
    
-   com.twilio.rest.api.v2010.account.queue.MemberUpdater updater(String pathQueueSid, String pathCallSid, java.net.URI url);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCallSid** | 

 | String |
| **pathQueueSid** | 

 | String |
| **url** | 

 | URI |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: recording

**Both producer and consumer are supported**

The recording API is defined in the syntax as follows:

```none
twilio:recording/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_recording_method_deleter) | delete | 
 |
| [**fetcher**](#_api_recording_method_fetcher) | fetch | 

 |
| [**reader**](#_api_recording_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.RecordingDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.RecordingDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.RecordingFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.RecordingFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.RecordingReader reader();
    
-   com.twilio.rest.api.v2010.account.RecordingReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: recording-add-on-result

**Both producer and consumer are supported**

The recording-add-on-result API is defined in the syntax as follows:

```none
twilio:recording-add-on-result/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_recording-add-on-result_method_deleter) | delete | 
 |
| [**fetcher**](#_api_recording-add-on-result_method_fetcher) | fetch | 

 |
| [**reader**](#_api_recording-add-on-result_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.recording.AddOnResultDeleter deleter(String pathAccountSid, String pathReferenceSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.AddOnResultDeleter deleter(String pathReferenceSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathReferenceSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.recording.AddOnResultFetcher fetcher(String pathAccountSid, String pathReferenceSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.AddOnResultFetcher fetcher(String pathReferenceSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathReferenceSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.recording.AddOnResultReader reader(String pathAccountSid, String pathReferenceSid);
    
-   com.twilio.rest.api.v2010.account.recording.AddOnResultReader reader(String pathReferenceSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathReferenceSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: recording-add-on-result-payload

**Both producer and consumer are supported**

The recording-add-on-result-payload API is defined in the syntax as follows:

```none
twilio:recording-add-on-result-payload/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_recording-add-on-result-payload_method_deleter) | delete | 
 |
| [**fetcher**](#_api_recording-add-on-result-payload_method_fetcher) | fetch | 

 |
| [**reader**](#_api_recording-add-on-result-payload_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadDeleter deleter(String pathAccountSid, String pathReferenceSid, String pathAddOnResultSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadDeleter deleter(String pathReferenceSid, String pathAddOnResultSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathAddOnResultSid** | 

 | String |
| **pathReferenceSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadFetcher fetcher(String pathAccountSid, String pathReferenceSid, String pathAddOnResultSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadFetcher fetcher(String pathReferenceSid, String pathAddOnResultSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathAddOnResultSid** | 

 | String |
| **pathReferenceSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadReader reader(String pathAccountSid, String pathReferenceSid, String pathAddOnResultSid);
    
-   com.twilio.rest.api.v2010.account.recording.addonresult.PayloadReader reader(String pathReferenceSid, String pathAddOnResultSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathAddOnResultSid** | 

 | String |
| **pathReferenceSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: recording-transcription

**Both producer and consumer are supported**

The recording-transcription API is defined in the syntax as follows:

```none
twilio:recording-transcription/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_recording-transcription_method_deleter) | delete | 
 |
| [**fetcher**](#_api_recording-transcription_method_fetcher) | fetch | 

 |
| [**reader**](#_api_recording-transcription_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.recording.TranscriptionDeleter deleter(String pathAccountSid, String pathRecordingSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.TranscriptionDeleter deleter(String pathRecordingSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathRecordingSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.recording.TranscriptionFetcher fetcher(String pathAccountSid, String pathRecordingSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.recording.TranscriptionFetcher fetcher(String pathRecordingSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathRecordingSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.recording.TranscriptionReader reader(String pathAccountSid, String pathRecordingSid);
    
-   com.twilio.rest.api.v2010.account.recording.TranscriptionReader reader(String pathRecordingSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathRecordingSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: short-code

**Both producer and consumer are supported**

The short-code API is defined in the syntax as follows:

```none
twilio:short-code/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**fetcher**](#_api_short-code_method_fetcher) | fetch | 
 |
| [**reader**](#_api_short-code_method_reader) | read | 

 |
| [**updater**](#_api_short-code_method_updater) | update | 

 |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.ShortCodeFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ShortCodeFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.ShortCodeReader reader();
    
-   com.twilio.rest.api.v2010.account.ShortCodeReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.ShortCodeUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.ShortCodeUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: signing-key

**Both producer and consumer are supported**

The signing-key API is defined in the syntax as follows:

```none
twilio:signing-key/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_signing-key_method_deleter) | delete | 
 |
| [**fetcher**](#_api_signing-key_method_fetcher) | fetch | 

 |
| [**reader**](#_api_signing-key_method_reader) | read | 

 |
| [**updater**](#_api_signing-key_method_updater) | update | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.SigningKeyDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.SigningKeyDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.SigningKeyFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.SigningKeyFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.SigningKeyReader reader();
    
-   com.twilio.rest.api.v2010.account.SigningKeyReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.SigningKeyUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.SigningKeyUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-credential-list

**Both producer and consumer are supported**

The sip-credential-list API is defined in the syntax as follows:

```none
twilio:sip-credential-list/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-credential-list_method_creator) | create | 
 |
| [**deleter**](#_api_sip-credential-list_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-credential-list_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-credential-list_method_reader) | read | 

 |
| [**updater**](#_api_sip-credential-list_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.CredentialListCreator creator(String friendlyName);
    
-   com.twilio.rest.api.v2010.account.sip.CredentialListCreator creator(String pathAccountSid, String friendlyName);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **pathAccountSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.CredentialListDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.CredentialListDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.CredentialListFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.CredentialListFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.CredentialListReader reader();
    
-   com.twilio.rest.api.v2010.account.sip.CredentialListReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.sip.CredentialListUpdater updater(String pathAccountSid, String pathSid, String friendlyName);
    
-   com.twilio.rest.api.v2010.account.sip.CredentialListUpdater updater(String pathSid, String friendlyName);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **pathAccountSid** | 

 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-credential-list-credential

**Both producer and consumer are supported**

The sip-credential-list-credential API is defined in the syntax as follows:

```none
twilio:sip-credential-list-credential/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-credential-list-credential_method_creator) | create | 
 |
| [**deleter**](#_api_sip-credential-list-credential_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-credential-list-credential_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-credential-list-credential_method_reader) | read | 

 |
| [**updater**](#_api_sip-credential-list-credential_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialCreator creator(String pathAccountSid, String pathCredentialListSid, String username, String password);
    
-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialCreator creator(String pathCredentialListSid, String username, String password);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **password** | 
 | String |
| **pathAccountSid** | 

 | String |
| **pathCredentialListSid** | 

 | String |
| **username** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialDeleter deleter(String pathAccountSid, String pathCredentialListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialDeleter deleter(String pathCredentialListSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCredentialListSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialFetcher fetcher(String pathAccountSid, String pathCredentialListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialFetcher fetcher(String pathCredentialListSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCredentialListSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialReader reader(String pathAccountSid, String pathCredentialListSid);
    
-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialReader reader(String pathCredentialListSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCredentialListSid** | 

 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialUpdater updater(String pathAccountSid, String pathCredentialListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.credentiallist.CredentialUpdater updater(String pathCredentialListSid, String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathCredentialListSid** | 

 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-domain

**Both producer and consumer are supported**

The sip-domain API is defined in the syntax as follows:

```none
twilio:sip-domain/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-domain_method_creator) | create | 
 |
| [**deleter**](#_api_sip-domain_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-domain_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-domain_method_reader) | read | 

 |
| [**updater**](#_api_sip-domain_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.DomainCreator creator(String domainName);
    
-   com.twilio.rest.api.v2010.account.sip.DomainCreator creator(String pathAccountSid, String domainName);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **domainName** | 
 | String |
| **pathAccountSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.DomainDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.DomainDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.DomainFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.DomainFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.DomainReader reader();
    
-   com.twilio.rest.api.v2010.account.sip.DomainReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.sip.DomainUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.DomainUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-domain-credential-list-mapping

**Both producer and consumer are supported**

The sip-domain-credential-list-mapping API is defined in the syntax as follows:

```none
twilio:sip-domain-credential-list-mapping/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-domain-credential-list-mapping_method_creator) | create | 
 |
| [**deleter**](#_api_sip-domain-credential-list-mapping_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-domain-credential-list-mapping_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-domain-credential-list-mapping_method_reader) | read | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingCreator creator(String pathAccountSid, String pathDomainSid, String credentialListSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingCreator creator(String pathDomainSid, String credentialListSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **credentialListSid** | 
 | String |
| **pathAccountSid** | 

 | String |
| **pathDomainSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingDeleter deleter(String pathAccountSid, String pathDomainSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingDeleter deleter(String pathDomainSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingFetcher fetcher(String pathAccountSid, String pathDomainSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingFetcher fetcher(String pathDomainSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingReader reader(String pathAccountSid, String pathDomainSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.CredentialListMappingReader reader(String pathDomainSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-domain-ip-access-control-list-mapping

**Both producer and consumer are supported**

The sip-domain-ip-access-control-list-mapping API is defined in the syntax as follows:

```none
twilio:sip-domain-ip-access-control-list-mapping/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-domain-ip-access-control-list-mapping_method_creator) | create | 
 |
| [**deleter**](#_api_sip-domain-ip-access-control-list-mapping_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-domain-ip-access-control-list-mapping_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-domain-ip-access-control-list-mapping_method_reader) | read | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingCreator creator(String pathAccountSid, String pathDomainSid, String ipAccessControlListSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingCreator creator(String pathDomainSid, String ipAccessControlListSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ipAccessControlListSid** | 
 | String |
| **pathAccountSid** | 

 | String |
| **pathDomainSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingDeleter deleter(String pathAccountSid, String pathDomainSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingDeleter deleter(String pathDomainSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingFetcher fetcher(String pathAccountSid, String pathDomainSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingFetcher fetcher(String pathDomainSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingReader reader(String pathAccountSid, String pathDomainSid);
    
-   com.twilio.rest.api.v2010.account.sip.domain.IpAccessControlListMappingReader reader(String pathDomainSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathDomainSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-ip-access-control-list

**Both producer and consumer are supported**

The sip-ip-access-control-list API is defined in the syntax as follows:

```none
twilio:sip-ip-access-control-list/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-ip-access-control-list_method_creator) | create | 
 |
| [**deleter**](#_api_sip-ip-access-control-list_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-ip-access-control-list_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-ip-access-control-list_method_reader) | read | 

 |
| [**updater**](#_api_sip-ip-access-control-list_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListCreator creator(String friendlyName);
    
-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListCreator creator(String pathAccountSid, String friendlyName);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **pathAccountSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListReader reader();
    
-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListUpdater updater(String pathAccountSid, String pathSid, String friendlyName);
    
-   com.twilio.rest.api.v2010.account.sip.IpAccessControlListUpdater updater(String pathSid, String friendlyName);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **pathAccountSid** | 

 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: sip-ip-access-control-list-ip-address

**Both producer and consumer are supported**

The sip-ip-access-control-list-ip-address API is defined in the syntax as follows:

```none
twilio:sip-ip-access-control-list-ip-address/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_sip-ip-access-control-list-ip-address_method_creator) | create | 
 |
| [**deleter**](#_api_sip-ip-access-control-list-ip-address_method_deleter) | delete | 

 |
| [**fetcher**](#_api_sip-ip-access-control-list-ip-address_method_fetcher) | fetch | 

 |
| [**reader**](#_api_sip-ip-access-control-list-ip-address_method_reader) | read | 

 |
| [**updater**](#_api_sip-ip-access-control-list-ip-address_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressCreator creator(String pathAccountSid, String pathIpAccessControlListSid, String friendlyName, String ipAddress);
    
-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressCreator creator(String pathIpAccessControlListSid, String friendlyName, String ipAddress);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **friendlyName** | 
 | String |
| **ipAddress** | 

 | String |
| **pathAccountSid** | 

 | String |
| **pathIpAccessControlListSid** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressDeleter deleter(String pathAccountSid, String pathIpAccessControlListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressDeleter deleter(String pathIpAccessControlListSid, String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathIpAccessControlListSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressFetcher fetcher(String pathAccountSid, String pathIpAccessControlListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressFetcher fetcher(String pathIpAccessControlListSid, String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathIpAccessControlListSid** | 

 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressReader reader(String pathAccountSid, String pathIpAccessControlListSid);
    
-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressReader reader(String pathIpAccessControlListSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathIpAccessControlListSid** | 

 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressUpdater updater(String pathAccountSid, String pathIpAccessControlListSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.sip.ipaccesscontrollist.IpAddressUpdater updater(String pathIpAccessControlListSid, String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathIpAccessControlListSid** | 

 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: token

**Both producer and consumer are supported**

The token API is defined in the syntax as follows:

```none
twilio:token/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_token_method_creator) | create | 
 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.TokenCreator creator();
    
-   com.twilio.rest.api.v2010.account.TokenCreator creator(String pathAccountSid);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: transcription

**Both producer and consumer are supported**

The transcription API is defined in the syntax as follows:

```none
twilio:transcription/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**deleter**](#_api_transcription_method_deleter) | delete | 
 |
| [**fetcher**](#_api_transcription_method_fetcher) | fetch | 

 |
| [**reader**](#_api_transcription_method_reader) | read | 

 |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.TranscriptionDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.TranscriptionDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.TranscriptionFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.TranscriptionFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.TranscriptionReader reader();
    
-   com.twilio.rest.api.v2010.account.TranscriptionReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record

**Both producer and consumer are supported**

The usage-record API is defined in the syntax as follows:

```none
twilio:usage-record/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.RecordReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.RecordReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-all-time

**Both producer and consumer are supported**

The usage-record-all-time API is defined in the syntax as follows:

```none
twilio:usage-record-all-time/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-all-time_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.AllTimeReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.AllTimeReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-daily

**Both producer and consumer are supported**

The usage-record-daily API is defined in the syntax as follows:

```none
twilio:usage-record-daily/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-daily_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.DailyReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.DailyReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-last-month

**Both producer and consumer are supported**

The usage-record-last-month API is defined in the syntax as follows:

```none
twilio:usage-record-last-month/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-last-month_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.LastMonthReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.LastMonthReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-monthly

**Both producer and consumer are supported**

The usage-record-monthly API is defined in the syntax as follows:

```none
twilio:usage-record-monthly/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-monthly_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.MonthlyReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.MonthlyReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-this-month

**Both producer and consumer are supported**

The usage-record-this-month API is defined in the syntax as follows:

```none
twilio:usage-record-this-month/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-this-month_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.ThisMonthReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.ThisMonthReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-today

**Both producer and consumer are supported**

The usage-record-today API is defined in the syntax as follows:

```none
twilio:usage-record-today/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-today_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.TodayReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.TodayReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-yearly

**Both producer and consumer are supported**

The usage-record-yearly API is defined in the syntax as follows:

```none
twilio:usage-record-yearly/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-yearly_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.YearlyReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.YearlyReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-record-yesterday

**Both producer and consumer are supported**

The usage-record-yesterday API is defined in the syntax as follows:

```none
twilio:usage-record-yesterday/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**reader**](#_api_usage-record-yesterday_method_reader) | read | 
 |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.record.YesterdayReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.record.YesterdayReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: usage-trigger

**Both producer and consumer are supported**

The usage-trigger API is defined in the syntax as follows:

```none
twilio:usage-trigger/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_usage-trigger_method_creator) | create | 
 |
| [**deleter**](#_api_usage-trigger_method_deleter) | delete | 

 |
| [**fetcher**](#_api_usage-trigger_method_fetcher) | fetch | 

 |
| [**reader**](#_api_usage-trigger_method_reader) | read | 

 |
| [**updater**](#_api_usage-trigger_method_updater) | update | 

 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.usage.TriggerCreator creator(String pathAccountSid, java.net.URI callbackUrl, String triggerValue, String usageCategory);
    
-   com.twilio.rest.api.v2010.account.usage.TriggerCreator creator(java.net.URI callbackUrl, String triggerValue, String usageCategory);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **callbackUrl** | 
 | URI |
| **pathAccountSid** | 

 | String |
| **triggerValue** | 

 | String |
| **usageCategory** | 

 | String |

#### Method deleter

Signatures:

-   com.twilio.rest.api.v2010.account.usage.TriggerDeleter deleter(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.usage.TriggerDeleter deleter(String pathSid);
    

The twilio/deleter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method fetcher

Signatures:

-   com.twilio.rest.api.v2010.account.usage.TriggerFetcher fetcher(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.usage.TriggerFetcher fetcher(String pathSid);
    

The twilio/fetcher API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

#### Method reader

Signatures:

-   com.twilio.rest.api.v2010.account.usage.TriggerReader reader();
    
-   com.twilio.rest.api.v2010.account.usage.TriggerReader reader(String pathAccountSid);
    

The twilio/reader API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |

#### Method updater

Signatures:

-   com.twilio.rest.api.v2010.account.usage.TriggerUpdater updater(String pathAccountSid, String pathSid);
    
-   com.twilio.rest.api.v2010.account.usage.TriggerUpdater updater(String pathSid);
    

The twilio/updater API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **pathSid** | 

 | String |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

### API: validation-request

**Both producer and consumer are supported**

The validation-request API is defined in the syntax as follows:

```none
twilio:validation-request/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**creator**](#_api_validation-request_method_creator) | create | 
 |

#### Method creator

Signatures:

-   com.twilio.rest.api.v2010.account.ValidationRequestCreator creator(String pathAccountSid, com.twilio.type.PhoneNumber phoneNumber);
    
-   com.twilio.rest.api.v2010.account.ValidationRequestCreator creator(com.twilio.type.PhoneNumber phoneNumber);
    

The twilio/creator API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pathAccountSid** | 
 | String |
| **phoneNumber** | 

 | PhoneNumber |

In addition to the parameters above, the twilio API can also use any of the [Query Parameters (21 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelTwilio.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelTwilio.myParameterNameHere` header.

> **Note**
> This is an API-based component, so per-call parameters can be supplied through `Camel`\-prefixed exchange headers in addition to the endpoint options. If the route consumes messages from untrusted producers, strip these internal headers at the trust boundary — for example with `removeHeaders("Camel*")` — before the message reaches this component, so that a sender cannot override the API call. See [the Camel security model](../../manual/security-model.md) for details.

## Usage

### Producer Endpoints:

Producer endpoints can use endpoint prefixes followed by endpoint names and associated options described next. A shorthand alias can be used for all the endpoints. The endpoint URI MUST contain a prefix.

Any of the endpoint options can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format **`CamelTwilio.<option>`**. Note that the **`inBody`** option overrides message header, i.e., the endpoint option **`inBody=option`** would override a **`CamelTwilio.option`** header.

Endpoint can be one of:

  
| Endpoint | Shorthand Alias | Description |
| --- | --- | --- |
| **creator** | create | Make the request to the Twilio API to perform the `create` |
| **deleter** | delete | Make the request to the Twilio API to perform the `delete` |
| **fetcher** | fetch | Make the request to the Twilio API to perform the `fetch` |
| **reader** | read | Make the request to the Twilio API to perform the `read` |
| **updater** | update | Make the request to the Twilio API to perform the `update` |

Available endpoints differ depending on the endpoint prefixes.

For more information on the endpoints and options, see [Twilio API documentation](https://www.twilio.com/docs/libraries/reference/twilio-java/index.md).