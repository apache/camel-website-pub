# Google Sheets

**Since Camel 2.23**

**Both producer and consumer are supported**

The Google Sheets component provides access to [Google Sheets](http://google.com/sheets) via the [Google Sheets Web APIs](https://developers.google.com/sheets/api/reference/rest/).

Google Sheets uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/google-apps/sheets/auth). Credentials consist of a `clientId`, `clientSecret`, and a `refreshToken`. A handy resource for generating a long-lived `refreshToken` is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials consist of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [Sheets API Auth Scopes](https://developers.google.com/sheets/api/guides/authorizing).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-google-sheets</artifactId>
        <!-- use the same version as your Camel core version -->
        <version>x.x.x</version>
</dependency>
```

## URI Format

The GoogleSheets Component uses the following URI format:

google-sheets://endpoint-prefix/endpoint?\[options\]

Endpoint prefix can be one of:

-   spreadsheets
    
-   data
    

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

The Google Sheets component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **clientId** (common) | Client ID of the sheets application. |  | String |
| **configuration** (common) | To use the shared configuration. |  | GoogleSheetsConfiguration |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **splitResult** (consumer) | When consumer return an array or collection this will generate one exchange per element, and their routes will be executed once for each exchange. Set this value to false to use a single exchange for the entire list or array. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleSheetsClientFactory as factory for creating the client. Will by default use BatchGoogleSheetsClientFactory. |  | GoogleSheetsClientFactory |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the sheets application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Sheets component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Sets .json file with credentials for Service account. |  | String |

## Endpoint Options

The Google Sheets endpoint is configured using URI syntax:

google-sheets:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   SPREADSHEETS
    
-   DATA
    





 |  | GoogleSheetsApiName |
| **methodName** (common) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   create
    
-   get
    
-   update
    
-   append
    
-   batchUpdate
    
-   clear
    





 |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **clientId** (common) | Client ID of the sheets application. |  | String |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **splitResult** (consumer) | When consumer return an array or collection this will generate one exchange per element, and their routes will be executed once for each exchange. Set this value to false to use a single exchange for the entire list or array. | true | boolean |
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
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the sheets application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Sheets component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Sets .json file with credentials for Service account. |  | String |

## API Parameters (2 APIs)

The Google Sheets endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

google-sheets:apiName/methodName

There are 2 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**data**](#_api_data) | Both | The values collection of methods |
| [**spreadsheets**](#_api_spreadsheets) | Both | The spreadsheets collection of methods |

Each API is documented in the following sections to come.

### API: data

**Both producer and consumer are supported**

The data API is defined in the syntax as follows:

```none
google-sheets:data/methodName?[parameters]
```

The 10 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**append**](#_api_data_method_append) |  | Appends values to a spreadsheet |
| [**batchClear**](#_api_data_method_batchClear) |  | Clears one or more ranges of values from a spreadsheet |
| [**batchClearByDataFilter**](#_api_data_method_batchClearByDataFilter) |  | Clears one or more ranges of values from a spreadsheet |
| [**batchGet**](#_api_data_method_batchGet) |  | Returns one or more ranges of values from a spreadsheet |
| [**batchGetByDataFilter**](#_api_data_method_batchGetByDataFilter) |  | Returns one or more ranges of values that match the specified data filters |
| [**batchUpdate**](#_api_data_method_batchUpdate) |  | Sets values in one or more ranges of a spreadsheet |
| [**batchUpdateByDataFilter**](#_api_data_method_batchUpdateByDataFilter) |  | Sets values in one or more ranges of a spreadsheet |
| [**clear**](#_api_data_method_clear) |  | Clears values from a spreadsheet |
| [**get**](#_api_data_method_get) |  | Returns a range of values from a spreadsheet |
| [**update**](#_api_data_method_update) |  | Sets values in a range of a spreadsheet |

#### Method append

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.Append append(String spreadsheetId, String range, com.google.api.services.sheets.v4.model.ValueRange content);
    

The google-sheets/append API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **includeValuesInResponse** | Determines if the update response should include the values of the cells that were appended | Boolean |
| **insertDataOption** | How the input data should be inserted | String |
| **range** | The A1 notation([https://developers.google.com/workspace/sheets/api/guides/concepts#cell](https://developers.google.com/workspace/sheets/api/guides/concepts#cell)) of a range to search for a logical table of data. Values are appended after the last row of the table. | String |
| **responseDateTimeRenderOption** | Determines how dates, times, and durations in the response should be rendered | String |
| **responseValueRenderOption** | Determines how values in the response should be rendered | String |
| **spreadsheetId** | The ID of the spreadsheet to update | String |
| **valueInputOption** | How the input data should be interpreted | String |
| **values** | The com.google.api.services.sheets.v4.model.ValueRange | ValueRange |

#### Method batchClear

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchClear batchClear(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchClearValuesRequest content);
    

The google-sheets/batchClear API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchClearValuesRequest** | The com.google.api.services.sheets.v4.model.BatchClearValuesRequest | BatchClearValuesRequest |
| **spreadsheetId** | The ID of the spreadsheet to update | String |

#### Method batchClearByDataFilter

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchClearByDataFilter batchClearByDataFilter(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchClearValuesByDataFilterRequest content);
    

The google-sheets/batchClearByDataFilter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.sheets.v4.model.BatchClearValuesByDataFilterRequest | BatchClearValuesByDataFilterRequest |
| **spreadsheetId** | The ID of the spreadsheet to update | String |

#### Method batchGet

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchGet batchGet(String spreadsheetId);
    

The google-sheets/batchGet API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **dateTimeRenderOption** | How dates, times, and durations should be represented in the output | String |
| **majorDimension** | The major dimension that results should use | String |
| **ranges** | The A1 notation or R1C1 notation([https://developers](https://developers) | List |
| **spreadsheetId** | The ID of the spreadsheet to retrieve data from | String |
| **valueRenderOption** | How values should be represented in the output | String |

#### Method batchGetByDataFilter

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchGetByDataFilter batchGetByDataFilter(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchGetValuesByDataFilterRequest content);
    

The google-sheets/batchGetByDataFilter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchGetValuesByDataFilterRequest** | The com.google.api.services.sheets.v4.model.BatchGetValuesByDataFilterRequest | BatchGetValuesByDataFilterRequest |
| **spreadsheetId** | The ID of the spreadsheet to retrieve data from | String |

#### Method batchUpdate

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchUpdate batchUpdate(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchUpdateValuesRequest content);
    

The google-sheets/batchUpdate API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchUpdateValuesRequest** | The com.google.api.services.sheets.v4.model.BatchUpdateValuesRequest | BatchUpdateValuesRequest |
| **spreadsheetId** | The ID of the spreadsheet to update | String |

#### Method batchUpdateByDataFilter

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.BatchUpdateByDataFilter batchUpdateByDataFilter(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchUpdateValuesByDataFilterRequest content);
    

The google-sheets/batchUpdateByDataFilter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchUpdateValuesByDataFilterRequest** | The com.google.api.services.sheets.v4.model.BatchUpdateValuesByDataFilterRequest | BatchUpdateValuesByDataFilterRequest |
| **spreadsheetId** | The ID of the spreadsheet to update | String |

#### Method clear

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.Clear clear(String spreadsheetId, String range, com.google.api.services.sheets.v4.model.ClearValuesRequest content);
    

The google-sheets/clear API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **clearValuesRequest** | The com.google.api.services.sheets.v4.model.ClearValuesRequest | ClearValuesRequest |
| **range** | The A1 notation or R1C1 notation([https://developers.google.com/workspace/sheets/api/guides/concepts#cell](https://developers.google.com/workspace/sheets/api/guides/concepts#cell)) of the values to clear. | String |
| **spreadsheetId** | The ID of the spreadsheet to update | String |

#### Method get

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.Get get(String spreadsheetId, String range);
    

The google-sheets/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **dateTimeRenderOption** | How dates, times, and durations should be represented in the output | String |
| **majorDimension** | The major dimension that results should use | String |
| **range** | The A1 notation or R1C1 notation([https://developers.google.com/workspace/sheets/api/guides/concepts#cell](https://developers.google.com/workspace/sheets/api/guides/concepts#cell)) of the range to retrieve values from. | String |
| **spreadsheetId** | The ID of the spreadsheet to retrieve data from | String |
| **valueRenderOption** | How values should be represented in the output | String |

#### Method update

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values.Update update(String spreadsheetId, String range, com.google.api.services.sheets.v4.model.ValueRange content);
    

The google-sheets/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **includeValuesInResponse** | Determines if the update response should include the values of the cells that were updated | Boolean |
| **range** | The A1 notation([https://developers.google.com/workspace/sheets/api/guides/concepts#cell](https://developers.google.com/workspace/sheets/api/guides/concepts#cell)) of the values to update. | String |
| **responseDateTimeRenderOption** | Determines how dates, times, and durations in the response should be rendered | String |
| **responseValueRenderOption** | Determines how values in the response should be rendered | String |
| **spreadsheetId** | The ID of the spreadsheet to update | String |
| **valueInputOption** | How the input data should be interpreted | String |
| **values** | The com.google.api.services.sheets.v4.model.ValueRange | ValueRange |

In addition to the parameters above, the google-sheets API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleSheets.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleSheets.myParameterNameHere` header.

### API: spreadsheets

**Both producer and consumer are supported**

The spreadsheets API is defined in the syntax as follows:

```none
google-sheets:spreadsheets/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**batchUpdate**](#_api_spreadsheets_method_batchUpdate) |  | Applies one or more updates to the spreadsheet |
| [**create**](#_api_spreadsheets_method_create) |  | Creates a spreadsheet, returning the newly created spreadsheet |
| [**developerMetadata**](#_api_spreadsheets_method_developerMetadata) |  | An accessor for creating requests from the DeveloperMetadata collection |
| [**get**](#_api_spreadsheets_method_get) |  | Returns the spreadsheet at the given ID |
| [**getByDataFilter**](#_api_spreadsheets_method_getByDataFilter) |  | Returns the spreadsheet at the given ID |
| [**sheets**](#_api_spreadsheets_method_sheets) |  | An accessor for creating requests from the SheetsOperations collection |
| [**values**](#_api_spreadsheets_method_values) |  | An accessor for creating requests from the Values collection |

#### Method batchUpdate

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.BatchUpdate batchUpdate(String spreadsheetId, com.google.api.services.sheets.v4.model.BatchUpdateSpreadsheetRequest content);
    

The google-sheets/batchUpdate API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchUpdateSpreadsheetRequest** | The com.google.api.services.sheets.v4.model.BatchUpdateSpreadsheetRequest | BatchUpdateSpreadsheetRequest |
| **spreadsheetId** | The spreadsheet to apply the updates to | String |

#### Method create

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Create create(com.google.api.services.sheets.v4.model.Spreadsheet content);
    

The google-sheets/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.sheets.v4.model.Spreadsheet | Spreadsheet |

#### Method developerMetadata

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.DeveloperMetadata developerMetadata();
    

The google-sheets/developerMetadata API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method get

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Get get(String spreadsheetId);
    

The google-sheets/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **excludeTablesInBandedRanges** | True if tables should be excluded in the banded ranges | Boolean |
| **includeGridData** | True if grid data should be returned | Boolean |
| **ranges** | The ranges to retrieve from the spreadsheet | List |
| **spreadsheetId** | The spreadsheet to request | String |

#### Method getByDataFilter

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.GetByDataFilter getByDataFilter(String spreadsheetId, com.google.api.services.sheets.v4.model.GetSpreadsheetByDataFilterRequest content);
    

The google-sheets/getByDataFilter API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **getSpreadsheetByDataFilterRequest** | The com.google.api.services.sheets.v4.model.GetSpreadsheetByDataFilterRequest | GetSpreadsheetByDataFilterRequest |
| **spreadsheetId** | The spreadsheet to request | String |

#### Method sheets

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.SheetsOperations sheets();
    

The google-sheets/sheets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method values

Signatures:

-   com.google.api.services.sheets.v4.Sheets.Spreadsheets.Values values();
    

The google-sheets/values API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

In addition to the parameters above, the google-sheets API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleSheets.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleSheets.myParameterNameHere` header.

## ValueInputOption

Many of the APIs with Google sheets require including the following header, with one of the enum values:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Header</strong></td><td class="tableblock halign-left valign-top"><strong>Enum</strong></td><td class="tableblock halign-left valign-top"><strong>Description</strong></td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelGoogleSheets.ValueInputOption</code></td><td class="tableblock halign-left valign-top"><code>RAW</code></td><td class="tableblock halign-left valign-top">The values the user has entered will not be parsed and will be stored as-is.</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelGoogleSheets.ValueInputOption</code></td><td class="tableblock halign-left valign-top"><code>USER_ENTERED</code></td><td class="tableblock halign-left valign-top">The values will be parsed as if the user typed them into the UI. Numbers will stay as numbers, but strings may be converted to numbers, dates, etc. following the same rules that are applied when entering text into a cell via the Google Sheets UI.</td></tr></tbody></table>

## More information

For more information on the endpoints and options see API documentation at: [https://developers.google.com/sheets/api/reference/rest/](https://developers.google.com/sheets/api/reference/rest/)

## Spring Boot Auto-Configuration

When using google-sheets with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-sheets-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 36 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-sheets-stream.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-sheets-stream.application-name** | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **camel.component.google-sheets-stream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-sheets-stream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-sheets-stream.client-factory** | To use the GoogleSheetsClientFactory as factory for creating the client. Will by default use BatchGoogleSheetsClientFactory. The option is a org.apache.camel.component.google.sheets.GoogleSheetsClientFactory type. |  | GoogleSheetsClientFactory |
| **camel.component.google-sheets-stream.client-id** | Client ID of the sheets application. |  | String |
| **camel.component.google-sheets-stream.client-secret** | Client secret of the sheets application. |  | String |
| **camel.component.google-sheets-stream.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.sheets.stream.GoogleSheetsStreamConfiguration type. |  | GoogleSheetsStreamConfiguration |
| **camel.component.google-sheets-stream.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-sheets-stream.enabled** | Whether to enable auto configuration of the google-sheets-stream component. This is enabled by default. |  | Boolean |
| **camel.component.google-sheets-stream.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.google-sheets-stream.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.google-sheets-stream.include-grid-data** | True if grid data should be returned. | false | Boolean |
| **camel.component.google-sheets-stream.major-dimension** | Specifies the major dimension that results should use.. | ROWS | String |
| **camel.component.google-sheets-stream.max-results** | Specify the maximum number of returned results. This will limit the number of rows in a returned value range data set or the number of returned value ranges in a batch request. |  | Integer |
| **camel.component.google-sheets-stream.range** | Specifies the range of rows and columns in a sheet to get data from. |  | String |
| **camel.component.google-sheets-stream.refresh-token** | OAuth 2 refresh token. Using this, the Google Sheets component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-sheets-stream.scopes** | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **camel.component.google-sheets-stream.service-account-key** | Sets .json file with credentials for Service account. |  | String |
| **camel.component.google-sheets-stream.split-results** | True if value range result should be split into rows or columns to process each of them individually. When true each row or column is represented with a separate exchange in batch processing. Otherwise value range object is used as exchange junk size. | false | Boolean |
| **camel.component.google-sheets-stream.value-render-option** | Determines how values should be rendered in the output. | FORMATTED\_VALUE | String |
| **camel.component.google-sheets.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-sheets.application-name** | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **camel.component.google-sheets.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-sheets.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-sheets.client-factory** | To use the GoogleSheetsClientFactory as factory for creating the client. Will by default use BatchGoogleSheetsClientFactory. The option is a org.apache.camel.component.google.sheets.GoogleSheetsClientFactory type. |  | GoogleSheetsClientFactory |
| **camel.component.google-sheets.client-id** | Client ID of the sheets application. |  | String |
| **camel.component.google-sheets.client-secret** | Client secret of the sheets application. |  | String |
| **camel.component.google-sheets.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.sheets.GoogleSheetsConfiguration type. |  | GoogleSheetsConfiguration |
| **camel.component.google-sheets.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-sheets.enabled** | Whether to enable auto configuration of the google-sheets component. This is enabled by default. |  | Boolean |
| **camel.component.google-sheets.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-sheets.refresh-token** | OAuth 2 refresh token. Using this, the Google Sheets component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-sheets.scopes** | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **camel.component.google-sheets.service-account-key** | Sets .json file with credentials for Service account. |  | String |
| **camel.component.google-sheets.split-result** | When consumer return an array or collection this will generate one exchange per element, and their routes will be executed once for each exchange. Set this value to false to use a single exchange for the entire list or array. | true | Boolean |