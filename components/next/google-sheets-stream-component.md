# Google Sheets Stream

**Since Camel 2.23**

**Only consumer is supported**

The Google Sheets component provides access to [Sheets](https://sheets.google.com/) via the [Google Sheets Web APIs](https://developers.google.com/sheets/api/reference/rest/).

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

The Google Sheets Component uses the following URI format:

google-sheets-stream://apiName?\[options\]

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

The Google Sheets Stream component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientId** (consumer) | Client ID of the sheets application. |  | String |
| **configuration** (consumer) | To use the shared configuration. |  | GoogleSheetsStreamConfiguration |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **includeGridData** (consumer) | True if grid data should be returned. | false | boolean |
| **majorDimension** (consumer) | 
Specifies the major dimension that results should use..

Enum values:

-   ROWS
    
-   COLUMNS
    
-   DIMENSION\_UNSPECIFIED
    





 | ROWS | String |
| **maxResults** (consumer) | Specify the maximum number of returned results. This will limit the number of rows in a returned value range data set or the number of returned value ranges in a batch request. |  | int |
| **range** (consumer) | Specifies the range of rows and columns in a sheet to get data from. |  | String |
| **scopes** (consumer) | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **splitResults** (consumer) | True if value range result should be split into rows or columns to process each of them individually. When true each row or column is represented with a separate exchange in batch processing. Otherwise value range object is used as exchange junk size. | false | boolean |
| **valueRenderOption** (consumer) | 

Determines how values should be rendered in the output.

Enum values:

-   FORMATTED\_VALUE
    
-   UNFORMATTED\_VALUE
    
-   FORMULA
    





 | FORMATTED\_VALUE | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleSheetsClientFactory as factory for creating the client. Will by default use BatchGoogleSheetsClientFactory. |  | GoogleSheetsClientFactory |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the sheets application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Sheets component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Sets .json file with credentials for Service account. |  | String |

## Endpoint Options

The Google Sheets Stream endpoint is configured using URI syntax:

google-sheets-stream:spreadsheetId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **spreadsheetId** (consumer) | **Required** Specifies the spreadsheet identifier that is used to identify the target to obtain. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google Sheets application name. Example would be camel-google-sheets/1.0. |  | String |
| **clientId** (consumer) | Client ID of the sheets application. |  | String |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **includeGridData** (consumer) | True if grid data should be returned. | false | boolean |
| **majorDimension** (consumer) | 
Specifies the major dimension that results should use..

Enum values:

-   ROWS
    
-   COLUMNS
    
-   DIMENSION\_UNSPECIFIED
    





 | ROWS | String |
| **maxResults** (consumer) | Specify the maximum number of returned results. This will limit the number of rows in a returned value range data set or the number of returned value ranges in a batch request. |  | int |
| **range** (consumer) | Specifies the range of rows and columns in a sheet to get data from. |  | String |
| **scopes** (consumer) | Specifies the level of permissions you want a sheets application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **splitResults** (consumer) | True if value range result should be split into rows or columns to process each of them individually. When true each row or column is represented with a separate exchange in batch processing. Otherwise value range object is used as exchange junk size. | false | boolean |
| **valueRenderOption** (consumer) | 

Determines how values should be rendered in the output.

Enum values:

-   FORMATTED\_VALUE
    
-   UNFORMATTED\_VALUE
    
-   FORMULA
    





 | FORMATTED\_VALUE | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
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

## Message Headers

The Google Sheets Stream component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleSheetsSpreadsheetId** (consumer) Constant: [`SPREADSHEET_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#SPREADSHEET_ID) | Specifies the spreadsheet identifier that is used to identify the target to obtain. |  | String |
| **CamelGoogleSheetsSpreadsheetUrl** (consumer) Constant: [`SPREADSHEET_URL`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#SPREADSHEET_URL) | The URL of the spreadsheet. |  | String |
| **CamelGoogleSheetsMajorDimension** (consumer) Constant: [`MAJOR_DIMENSION`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#MAJOR_DIMENSION) | The major dimension of the values. |  | String |
| **CamelGoogleSheetsRange** (consumer) Constant: [`RANGE`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#RANGE) | The range the values cover, in A1 notation. |  | String |
| **CamelGoogleSheetsRangeIndex** (consumer) Constant: [`RANGE_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#RANGE_INDEX) | The index of the range. |  | int |
| **CamelGoogleSheetsValueIndex** (consumer) Constant: [`VALUE_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-google-sheets/latest/org/apache/camel/component/google/sheets/stream/GoogleSheetsStreamConstants.html#VALUE_INDEX) | The index of the value. |  | int |

## ValueInputOption

Many of the APIs with Google sheets require including the following header, with one of the enum values:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Header</strong></td><td class="tableblock halign-left valign-top"><strong>Enum</strong></td><td class="tableblock halign-left valign-top"><strong>Description</strong></td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelGoogleSheets.ValueInputOption</code></td><td class="tableblock halign-left valign-top"><code>RAW</code></td><td class="tableblock halign-left valign-top">The values the user has entered will not be parsed and will be stored as-is.</td></tr><tr><td class="tableblock halign-left valign-top"><code>CamelGoogleSheets.ValueInputOption</code></td><td class="tableblock halign-left valign-top"><code>USER_ENTERED</code></td><td class="tableblock halign-left valign-top">The values will be parsed as if the user typed them into the UI. Numbers will stay as numbers, but strings may be converted to numbers, dates, etc. following the same rules that are applied when entering text into a cell via the Google Sheets UI.</td></tr></tbody></table>

## More information

For more information on the endpoints and options see API documentation at: [https://developers.google.com/sheets/api/reference/rest/](https://developers.google.com/sheets/api/reference/rest/)