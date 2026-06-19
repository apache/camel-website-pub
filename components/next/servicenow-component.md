# ServiceNow

**Since Camel 2.18**

**Only producer is supported**

The ServiceNow component provides access to ServiceNow platform through their REST API.

The component supports multiple versions of ServiceNow platform with default to Helsinki.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-servicenow</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

servicenow://instanceName?\[options\]

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

The ServiceNow component supports 48 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | ServiceNowConfiguration |
| **display** (producer) | 
Set this parameter to true to return only scorecards where the indicator Display field is selected. Set this parameter to all to return scorecards with any Display field value. This parameter is true by default.

Enum values:

-   false
    
-   true
    
-   all
    





 | true | String |
| **displayValue** (producer) | 

Return the display value (true), actual value (false), or both (all) for reference fields (default: false).

Enum values:

-   false
    
-   true
    
-   all
    





 | false | String |
| **excludeReferenceLink** (producer) | True to exclude Table API links for reference fields (default: false). | false | Boolean |
| **favorites** (producer) | Set this parameter to true to return only scorecards that are favorites of the querying user. | false | Boolean |
| **includeAggregates** (producer) | Set this parameter to true to always return all available aggregates for an indicator, including when an aggregate has already been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. | false | Boolean |
| **includeAvailableAggregates** (producer) | Set this parameter to true to return all available aggregates for an indicator when no aggregate has been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. | false | Boolean |
| **includeAvailableBreakdowns** (producer) | Set this parameter to true to return all available breakdowns for an indicator. If a value is not specified, this parameter defaults to false and returns no breakdowns. | false | Boolean |
| **includeScoreNotes** (producer) | Set this parameter to true to return all notes associated with the score. The note element contains the note text as well as the author and timestamp when the note was added. | false | Boolean |
| **includeScores** (producer) | Set this parameter to true to return all scores for a scorecard. If a value is not specified, this parameter defaults to false and returns only the most recent score value. | false | Boolean |
| **inputDisplayValue** (producer) | True to set raw value of input fields (default: false). | false | Boolean |
| **key** (producer) | Set this parameter to true to return only scorecards for key indicators. | false | Boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **models** (producer) | Defines both request and response models. This is a multi-value option with prefix: model. |  | Map |
| **perPage** (producer) | Enter the maximum number of scorecards each query can return. By default this value is 10, and the maximum is 100. | 10 | Integer |
| **release** (producer) | 

The ServiceNow release to target, default to Helsinki See [https://docs.servicenow.com](https://docs.servicenow.com).

Enum values:

-   FUJI
    
-   GENEVA
    
-   HELSINKI
    





 | HELSINKI | ServiceNowRelease |
| **requestModels** (producer) | Defines the request model. This is a multi-value option with prefix: request-model. |  | Map |
| **resource** (producer) | The default resource, can be overridden by header CamelServiceNowResource. |  | String |
| **responseModels** (producer) | Defines the response model. This is a multi-value option with prefix: response-model. |  | Map |
| **sortBy** (producer) | 

Specify the value to use when sorting results. By default, queries sort records by value.

Enum values:

-   value
    
-   change
    
-   changeperc
    
-   gap
    
-   gapperc
    
-   duedate
    
-   name
    
-   order
    
-   default
    
-   group
    
-   indicator\_group
    
-   frequency
    
-   target
    
-   date
    
-   trend
    
-   bullet
    
-   direction
    





 |  | String |
| **sortDir** (producer) | 

Specify the sort direction, ascending or descending. By default, queries sort records in descending order. Use sysparm\_sortdir=asc to sort in ascending order.

Enum values:

-   asc
    
-   desc
    





 |  | String |
| **suppressAutoSysField** (producer) | True to suppress auto generation of system fields (default: false). | false | Boolean |
| **suppressPaginationHeader** (producer) | Set this value to true to remove the Link header from the response. The Link header allows you to request additional pages of data when the number of records matching your query exceeds the query limit. | false | Boolean |
| **table** (producer) | The default table, can be overridden by header CamelServiceNowTable. |  | String |
| **target** (producer) | Set this parameter to true to return only scorecards that have a target. | false | Boolean |
| **topLevelOnly** (producer) | Gets only those categories whose parent is a catalog. | false | Boolean |
| **apiVersion** (advanced) | The ServiceNow REST API version, default latest. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **dateFormat** (advanced) | The date format used for Json serialization/deserialization. | yyyy-MM-dd | String |
| **dateTimeFormat** (advanced) | The date-time format used for Json serialization/deserialization. | yyyy-MM-dd HH:mm:ss | String |
| **httpClientPolicy** (advanced) | To configure http-client. |  | HTTPClientPolicy |
| **instanceName** (advanced) | The ServiceNow instance name. |  | String |
| **mapper** (advanced) | Sets Jackson’s ObjectMapper to use for request/reply. |  | ObjectMapper |
| **proxyAuthorizationPolicy** (advanced) | To configure proxy authentication. |  | ProxyAuthorizationPolicy |
| **retrieveTargetRecordOnImport** (advanced) | Set this parameter to true to retrieve the target record when using import set api. The import set result is then replaced by the target record. | false | Boolean |
| **timeFormat** (advanced) | The time format used for Json serialization/deserialization. | HH:mm:ss | String |
| **proxyHost** (proxy) | The proxy host name. |  | String |
| **proxyPort** (proxy) | The proxy port number. |  | Integer |
| **apiUrl** (security) | The ServiceNow REST API url. |  | String |
| **oauthClientId** (security) | OAuth2 ClientID. |  | String |
| **oauthClientSecret** (security) | OAuth2 ClientSecret. |  | String |
| **oauthTokenUrl** (security) | OAuth token Url. |  | String |
| **password** (security) | **Required** ServiceNow account password, MUST be provided. |  | String |
| **proxyPassword** (security) | Password for proxy authentication. |  | String |
| **proxyUserName** (security) | Username for proxy authentication. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. See [http://camel.apache.org/camel-configuration-utilities.html](http://camel.apache.org/camel-configuration-utilities.md). |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **userName** (security) | **Required** ServiceNow user account name, MUST be provided. |  | String |

## Endpoint Options

The ServiceNow endpoint is configured using URI syntax:

servicenow:instanceName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **instanceName** (producer) | **Required** The ServiceNow instance name. |  | String |

### Query Parameters (44 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **display** (producer) | 
Set this parameter to true to return only scorecards where the indicator Display field is selected. Set this parameter to all to return scorecards with any Display field value. This parameter is true by default.

Enum values:

-   false
    
-   true
    
-   all
    





 | true | String |
| **displayValue** (producer) | 

Return the display value (true), actual value (false), or both (all) for reference fields (default: false).

Enum values:

-   false
    
-   true
    
-   all
    





 | false | String |
| **excludeReferenceLink** (producer) | True to exclude Table API links for reference fields (default: false). | false | Boolean |
| **favorites** (producer) | Set this parameter to true to return only scorecards that are favorites of the querying user. | false | Boolean |
| **includeAggregates** (producer) | Set this parameter to true to always return all available aggregates for an indicator, including when an aggregate has already been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. | false | Boolean |
| **includeAvailableAggregates** (producer) | Set this parameter to true to return all available aggregates for an indicator when no aggregate has been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. | false | Boolean |
| **includeAvailableBreakdowns** (producer) | Set this parameter to true to return all available breakdowns for an indicator. If a value is not specified, this parameter defaults to false and returns no breakdowns. | false | Boolean |
| **includeScoreNotes** (producer) | Set this parameter to true to return all notes associated with the score. The note element contains the note text as well as the author and timestamp when the note was added. | false | Boolean |
| **includeScores** (producer) | Set this parameter to true to return all scores for a scorecard. If a value is not specified, this parameter defaults to false and returns only the most recent score value. | false | Boolean |
| **inputDisplayValue** (producer) | True to set raw value of input fields (default: false). | false | Boolean |
| **key** (producer) | Set this parameter to true to return only scorecards for key indicators. | false | Boolean |
| **models** (producer) | Defines both request and response models. This is a multi-value option with prefix: model. |  | Map |
| **perPage** (producer) | Enter the maximum number of scorecards each query can return. By default this value is 10, and the maximum is 100. | 10 | Integer |
| **release** (producer) | 

The ServiceNow release to target, default to Helsinki See [https://docs.servicenow.com](https://docs.servicenow.com).

Enum values:

-   FUJI
    
-   GENEVA
    
-   HELSINKI
    





 | HELSINKI | ServiceNowRelease |
| **requestModels** (producer) | Defines the request model. This is a multi-value option with prefix: request-model. |  | Map |
| **resource** (producer) | The default resource, can be overridden by header CamelServiceNowResource. |  | String |
| **responseModels** (producer) | Defines the response model. This is a multi-value option with prefix: response-model. |  | Map |
| **sortBy** (producer) | 

Specify the value to use when sorting results. By default, queries sort records by value.

Enum values:

-   value
    
-   change
    
-   changeperc
    
-   gap
    
-   gapperc
    
-   duedate
    
-   name
    
-   order
    
-   default
    
-   group
    
-   indicator\_group
    
-   frequency
    
-   target
    
-   date
    
-   trend
    
-   bullet
    
-   direction
    





 |  | String |
| **sortDir** (producer) | 

Specify the sort direction, ascending or descending. By default, queries sort records in descending order. Use sysparm\_sortdir=asc to sort in ascending order.

Enum values:

-   asc
    
-   desc
    





 |  | String |
| **suppressAutoSysField** (producer) | True to suppress auto generation of system fields (default: false). | false | Boolean |
| **suppressPaginationHeader** (producer) | Set this value to true to remove the Link header from the response. The Link header allows you to request additional pages of data when the number of records matching your query exceeds the query limit. | false | Boolean |
| **table** (producer) | The default table, can be overridden by header CamelServiceNowTable. |  | String |
| **target** (producer) | Set this parameter to true to return only scorecards that have a target. | false | Boolean |
| **topLevelOnly** (producer) | Gets only those categories whose parent is a catalog. | false | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiVersion** (advanced) | The ServiceNow REST API version, default latest. |  | String |
| **dateFormat** (advanced) | The date format used for Json serialization/deserialization. | yyyy-MM-dd | String |
| **dateTimeFormat** (advanced) | The date-time format used for Json serialization/deserialization. | yyyy-MM-dd HH:mm:ss | String |
| **httpClientPolicy** (advanced) | To configure http-client. |  | HTTPClientPolicy |
| **mapper** (advanced) | Sets Jackson’s ObjectMapper to use for request/reply. |  | ObjectMapper |
| **proxyAuthorizationPolicy** (advanced) | To configure proxy authentication. |  | ProxyAuthorizationPolicy |
| **retrieveTargetRecordOnImport** (advanced) | Set this parameter to true to retrieve the target record when using import set api. The import set result is then replaced by the target record. | false | Boolean |
| **timeFormat** (advanced) | The time format used for Json serialization/deserialization. | HH:mm:ss | String |
| **proxyHost** (proxy) | The proxy host name. |  | String |
| **proxyPort** (proxy) | The proxy port number. |  | Integer |
| **apiUrl** (security) | The ServiceNow REST API url. |  | String |
| **oauthClientId** (security) | OAuth2 ClientID. |  | String |
| **oauthClientSecret** (security) | OAuth2 ClientSecret. |  | String |
| **oauthTokenUrl** (security) | OAuth token Url. |  | String |
| **password** (security) | **Required** ServiceNow account password, MUST be provided. |  | String |
| **proxyPassword** (security) | Password for proxy authentication. |  | String |
| **proxyUserName** (security) | Username for proxy authentication. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. See [http://camel.apache.org/camel-configuration-utilities.html](http://camel.apache.org/camel-configuration-utilities.md). |  | SSLContextParameters |
| **userName** (security) | **Required** ServiceNow user account name, MUST be provided. |  | String |

## Message Headers

The ServiceNow component supports 63 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelServiceNowResource** (producer) Constant: [`RESOURCE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#RESOURCE) | The resource to access. |  | String |
| **CamelServiceNowAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#ACTION) | The action to perform. |  | String |
| **CamelServiceNowActionSubject** (producer) Constant: [`ACTION_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#ACTION_SUBJECT) | The action subject. |  | String |
| **CamelServiceNowModel** (producer) Constant: [`MODEL`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#MODEL) | The data model. |  | Class |
| **CamelServiceNowRequestModel** (producer) Constant: [`REQUEST_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#REQUEST_MODEL) | The request data model. |  | Class |
| **CamelServiceNowResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#RESPONSE_MODEL) | The response data model. |  | Class |
| **CamelServiceNowContentType** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#CONTENT_TYPE) | The content type. |  | String |
| **CamelServiceNowContentMeta** (producer) Constant: [`CONTENT_META`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#CONTENT_META) | The content meta. |  | Map |
| **CamelServiceNowResponseMeta** (producer) Constant: [`RESPONSE_META`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#RESPONSE_META) | The response meta. |  | Map |
| **CamelServiceNowApiVersion** (producer) Constant: [`API_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#API_VERSION) | The REST API version. |  | String |
| **CamelServiceNowResponseType** (producer) Constant: [`RESPONSE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#RESPONSE_TYPE) | The type of the response. |  | Class |
| **CamelServiceNowRetrieveTargetRecord** (producer) Constant: [`RETRIEVE_TARGET_RECORD`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#RETRIEVE_TARGET_RECORD) | Set this parameter to true to retrieve the target record. |  | Boolean |
| **CamelServiceNowTable** (producer) Constant: [`PARAM_TABLE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_TABLE_NAME) | The default table. |  | String |
| **CamelServiceNowSysId** (producer) Constant: [`PARAM_SYS_ID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_SYS_ID) | The sys id. |  | String |
| **CamelServiceNowUserSysId** (producer) Constant: [`PARAM_USER_SYS_ID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_USER_SYS_ID) | The user sys id. |  | String |
| **CamelServiceNowUserId** (producer) Constant: [`PARAM_USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_USER_ID) | The user id. |  | String |
| **CamelServiceNowCartItemId** (producer) Constant: [`PARAM_CART_ITEM_ID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_CART_ITEM_ID) | The cart item id. |  | String |
| **CamelServiceNowFileName** (producer) Constant: [`PARAM_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_FILE_NAME) | The file name. |  | String |
| **CamelServiceNowTableSysId** (producer) Constant: [`PARAM_TABLE_SYS_ID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_TABLE_SYS_ID) | The table sys id. |  | String |
| **CamelServiceNowEncryptionContext** (producer) Constant: [`PARAM_ENCRYPTION_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#PARAM_ENCRYPTION_CONTEXT) | The encryption context. |  | String |
| **CamelServiceNowCategory** (producer) Constant: [`SYSPARM_CATEGORY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_CATEGORY) | The sys param category. |  | String |
| **CamelServiceNowType** (producer) Constant: [`SYSPARM_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_TYPE) | The sys param type. |  | String |
| **CamelServiceNowCatalog** (producer) Constant: [`SYSPARM_CATALOG`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_CATALOG) | The sys param catalog. |  | String |
| **CamelServiceNowQuery** (producer) Constant: [`SYSPARM_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_QUERY) | The sys param query. |  | String |
| **CamelServiceNowDisplayValue** (producer) Constant: [`SYSPARM_DISPLAY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_DISPLAY_VALUE) | Return the display value (true), actual value (false), or both (all) for reference fields. | false | String |
| **CamelServiceNowInputDisplayValue** (producer) Constant: [`SYSPARM_INPUT_DISPLAY_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INPUT_DISPLAY_VALUE) | True to set raw value of input fields. | false | Boolean |
| **CamelServiceNowExcludeReferenceLink** (producer) Constant: [`SYSPARM_EXCLUDE_REFERENCE_LINK`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_EXCLUDE_REFERENCE_LINK) | True to exclude Table API links for reference fields. | false | Boolean |
| **CamelServiceNowFields** (producer) Constant: [`SYSPARM_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_FIELDS) | The sys param fields. |  | String |
| **CamelServiceNowLimit** (producer) Constant: [`SYSPARM_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_LIMIT) | The sys param limit. |  | Integer |
| **CamelServiceNowText** (producer) Constant: [`SYSPARM_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_TEXT) | The sys param text. |  | String |
| **CamelServiceNowOffset** (producer) Constant: [`SYSPARM_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_OFFSET) | The sys param offset. |  | Integer |
| **CamelServiceNowView** (producer) Constant: [`SYSPARM_VIEW`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_VIEW) | The sys param view. |  | String |
| **CamelServiceNowSuppressAutoSysField** (producer) Constant: [`SYSPARM_SUPPRESS_AUTO_SYS_FIELD`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_SUPPRESS_AUTO_SYS_FIELD) | True to suppress auto generation of system fields. | false | Boolean |
| **CamelServiceNowSuppressPaginationHeader** (producer) Constant: [`SYSPARM_SUPPRESS_PAGINATION_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_SUPPRESS_PAGINATION_HEADER) | Set this value to true to remove the Link header from the response. The Link header allows you to request additional pages of data when the number of records matching your query exceeds the query limit. |  | Boolean |
| **CamelServiceNowMinFields** (producer) Constant: [`SYSPARM_MIN_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_MIN_FIELDS) | The sys param min fields. |  | String |
| **CamelServiceNowMaxFields** (producer) Constant: [`SYSPARM_MAX_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_MAX_FIELDS) | The sys param max fields. |  | String |
| **CamelServiceNowSumFields** (producer) Constant: [`SYSPARM_SUM_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_SUM_FIELDS) | The sys param sum fields. |  | String |
| **CamelServiceNowAvgFields** (producer) Constant: [`SYSPARM_AVG_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_AVG_FIELDS) | The sys param avg fields. |  | String |
| **CamelServiceNowCount** (producer) Constant: [`SYSPARM_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_COUNT) | The sys param count. |  | Boolean |
| **CamelServiceNowGroupBy** (producer) Constant: [`SYSPARM_GROUP_BY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_GROUP_BY) | The sys param group by. |  | String |
| **CamelServiceNowOrderBy** (producer) Constant: [`SYSPARM_ORDER_BY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_ORDER_BY) | The sys param order by. |  | String |
| **CamelServiceNowHaving** (producer) Constant: [`SYSPARM_HAVING`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_HAVING) | The sys param having. |  | String |
| **CamelServiceNowUUID** (producer) Constant: [`SYSPARM_UUID`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_UUID) | The sys param UUID. |  | String |
| **CamelServiceNowBreakdown** (producer) Constant: [`SYSPARM_BREAKDOWN`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_BREAKDOWN) | The sys param breakdown. |  | String |
| **CamelServiceNowIncludeScores** (producer) Constant: [`SYSPARM_INCLUDE_SCORES`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INCLUDE_SCORES) | Set this parameter to true to return all scores for a scorecard. If a value is not specified, this parameter defaults to false and returns only the most recent score value. |  | Boolean |
| **CamelServiceNowIncludeScoreNotes** (producer) Constant: [`SYSPARM_INCLUDE_SCORE_NOTES`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INCLUDE_SCORE_NOTES) | Set this parameter to true to return all notes associated with the score. The note element contains the note text as well as the author and timestamp when the note was added. |  | Boolean |
| **CamelServiceNowIncludeAggregates** (producer) Constant: [`SYSPARM_INCLUDE_AGGREGATES`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INCLUDE_AGGREGATES) | Set this parameter to true to always return all available aggregates for an indicator, including when an aggregate has already been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. |  | Boolean |
| **CamelServiceNowIncludeAvailableBreakdowns** (producer) Constant: [`SYSPARM_INCLUDE_AVAILABLE_BREAKDOWNS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INCLUDE_AVAILABLE_BREAKDOWNS) | Set this parameter to true to return all available breakdowns for an indicator. If a value is not specified, this parameter defaults to false and returns no breakdowns. |  | Boolean |
| **CamelServiceNowIncludeAvailableAggregates** (producer) Constant: [`SYSPARM_INCLUDE_AVAILABLE_AGGREGATES`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_INCLUDE_AVAILABLE_AGGREGATES) | Set this parameter to true to return all available aggregates for an indicator when no aggregate has been applied. If a value is not specified, this parameter defaults to false and returns no aggregates. |  | Boolean |
| **CamelServiceNowFavorites** (producer) Constant: [`SYSPARM_FAVORITES`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_FAVORITES) | Set this parameter to true to return only scorecards that are favorites of the querying user. |  | Boolean |
| **CamelServiceNowKey** (producer) Constant: [`SYSPARM_KEY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_KEY) | Set this parameter to true to return only scorecards for key indicators. |  | Boolean |
| **CamelServiceNowTarget** (producer) Constant: [`SYSPARM_TARGET`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_TARGET) | Set this parameter to true to return only scorecards that have a target. |  | Boolean |
| **CamelServiceNowDisplay** (producer) Constant: [`SYSPARM_DISPLAY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_DISPLAY) | Set this parameter to true to return only scorecards where the indicator Display field is selected. Set this parameter to all to return scorecards with any Display field value. | true | String |
| **CamelServiceNowPerPage** (producer) Constant: [`SYSPARM_PER_PAGE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_PER_PAGE) | Enter the maximum number of scorecards each query can return. By default this value is 10, and the maximum is 100. | 10 | Integer |
| **CamelServiceNowSortBy** (producer) Constant: [`SYSPARM_SORT_BY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_SORT_BY) | Specify the value to use when sorting results. By default, queries sort records by value. |  | String |
| **CamelServiceNowSortDir** (producer) Constant: [`SYSPARM_SORT_DIR`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_SORT_DIR) | Specify the sort direction, ascending or descending. By default, queries sort records in descending order. Use sysparm\_sortdir=asc to sort in ascending order. |  | String |
| **CamelServiceNowContains** (producer) Constant: [`SYSPARM_CONTAINS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_CONTAINS) | The sys param contains. |  | String |
| **CamelServiceNowTags** (producer) Constant: [`SYSPARM_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_TAGS) | The sys param tags. |  | String |
| **CamelServiceNowPage** (producer) Constant: [`SYSPARM_PAGE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_PAGE) | The sys param page. |  | String |
| **CamelServiceNowElementsFilter** (producer) Constant: [`SYSPARM_ELEMENTS_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_ELEMENTS_FILTER) | The sys param elements filter. |  | String |
| **CamelServiceNowBreakdownRelation** (producer) Constant: [`SYSPARM_BREAKDOWN_RELATION`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_BREAKDOWN_RELATION) | The sys param breakdown relation. |  | String |
| **CamelServiceNowDataSource** (producer) Constant: [`SYSPARM_DATA_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_DATA_SOURCE) | The sys param data source. |  | String |
| **CamelServiceNowTopLevelOnly** (producer) Constant: [`SYSPARM_TOP_LEVEL_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-servicenow/latest/org/apache/camel/component/servicenow/ServiceNowConstants.html#SYSPARM_TOP_LEVEL_ONLY) | Gets only those categories whose parent is a catalog. |  | Boolean |Table 1. API Mapping    
| CamelServiceNowResource | CamelServiceNowAction | Method | API URI |
| --- | --- | --- | --- |
| TABLE | RETRIEVE | GET | /api/now/v1/table/{table\_name}/{sys\_id} |
| CREATE | POST | /api/now/v1/table/{table\_name} |
| MODIFY | PUT | /api/now/v1/table/{table\_name}/{sys\_id} |
| DELETE | DELETE | /api/now/v1/table/{table\_name}/{sys\_id} |
| UPDATE | PATCH | /api/now/v1/table/{table\_name}/{sys\_id} |
| AGGREGATE | RETRIEVE | GET | /api/now/v1/stats/{table\_name} |
| IMPORT | RETRIEVE | GET | /api/now/import/{table\_name}/{sys\_id} |
| CREATE | POST | /api/now/import/{table\_name} |
> **Note**
> [Fuji REST API Documentation](http://wiki.servicenow.com/index.php?title=REST_API#Available_APIs)

Table 2. API Mapping     
| CamelServiceNowResource | CamelServiceNowAction | CamelServiceNowActionSubject | Method | API URI |
| --- | --- | --- | --- | --- |
| TABLE | RETRIEVE | 
 | GET | /api/now/v1/table/{table\_name}/{sys\_id} |
| CREATE | 

 | POST | /api/now/v1/table/{table\_name} |
| MODIFY | 

 | PUT | /api/now/v1/table/{table\_name}/{sys\_id} |
| DELETE | 

 | DELETE | /api/now/v1/table/{table\_name}/{sys\_id} |
| UPDATE | 

 | PATCH | /api/now/v1/table/{table\_name}/{sys\_id} |
| AGGREGATE | RETRIEVE | 

 | GET | /api/now/v1/stats/{table\_name} |
| IMPORT | RETRIEVE | 

 | GET | /api/now/import/{table\_name}/{sys\_id} |
| CREATE | 

 | POST | /api/now/import/{table\_name} |
| ATTACHMENT | RETRIEVE | 

 | GET | /api/now/api/now/attachment/{sys\_id} |
| CONTENT | 

 | GET | /api/now/attachment/{sys\_id}/file |
| UPLOAD | 

 | POST | /api/now/api/now/attachment/file |
| DELETE | 

 | DELETE | /api/now/attachment/{sys\_id} |
| SCORECARDS | RETRIEVE | PERFORMANCE\_ANALYTICS | GET | /api/now/pa/scorecards |
| MISC | RETRIEVE | USER\_ROLE\_INHERITANCE | GET | /api/global/user\_role\_inheritance |
| CREATE | IDENTIFY\_RECONCILE | POST | /api/now/identifyreconcile |
| SERVICE\_CATALOG | RETRIEVE | 

 | GET | /sn\_sc/servicecatalog/catalogs/{sys\_id} |
| RETRIEVE | CATEGORIES | GET | /sn\_sc/servicecatalog/catalogs/{sys\_id}/categories |
| SERVICE\_CATALOG\_ITEMS | RETRIEVE | 

 | GET | /sn\_sc/servicecatalog/items/{sys\_id} |
| RETRIEVE | SUBMIT\_GUIDE | POST | /sn\_sc/servicecatalog/items/{sys\_id}/submit\_guide |
| RETRIEVE | CHECKOUT\_GUIDE | POST | /sn\_sc/servicecatalog/items/{sys\_id}/checkout\_guide |
| CREATE | SUBJECT\_CART | POST | /sn\_sc/servicecatalog/items/{sys\_id}/add\_to\_cart |
| CREATE | SUBJECT\_PRODUCER | POST | /sn\_sc/servicecatalog/items/{sys\_id}/submit\_producer |
| SERVICE\_CATALOG\_CARTS | RETRIEVE | 

 | GET | /sn\_sc/servicecatalog/cart |
| RETRIEVE | DELIVERY\_ADDRESS | GET | /sn\_sc/servicecatalog/cart/delivery\_address/{user\_id} |
| RETRIEVE | CHECKOUT | POST | /sn\_sc/servicecatalog/cart/checkout |
| UPDATE | 

 | POST | /sn\_sc/servicecatalog/cart/{cart\_item\_id} |
| UPDATE | CHECKOUT | POST | /sn\_sc/servicecatalog/cart/submit\_order |
| DELETE | 

 | DELETE | /sn\_sc/servicecatalog/cart/{sys\_id}/empty |
| SERVICE\_CATALOG\_CATEGORIES | RETRIEVE | 

 | GET | /sn\_sc/servicecatalog/categories/{sys\_id} |
> **Note**
> [Helsinki REST API Documentation](https://docs.servicenow.com/bundle/helsinki-servicenow-platform/page/integrate/inbound-rest/reference/r_RESTResources.md)

## Examples:

Retrieve 10 Incidents

```java
context.addRoutes(new RouteBuilder() {
    public void configure() {
       from("direct:servicenow")
           .to("servicenow:{{env:SERVICENOW_INSTANCE}}"
               + "?userName={{env:SERVICENOW_USERNAME}}"
               + "&password={{env:SERVICENOW_PASSWORD}}"
               + "&oauthClientId={{env:SERVICENOW_OAUTH2_CLIENT_ID}}"
               + "&oauthClientSecret={{env:SERVICENOW_OAUTH2_CLIENT_SECRET}}"
           .to("mock:servicenow");
    }
});

FluentProducerTemplate.on(context)
    .withHeader(ServiceNowConstants.RESOURCE, "table")
    .withHeader(ServiceNowConstants.ACTION, ServiceNowConstants.ACTION_RETRIEVE)
    .withHeader(ServiceNowConstants.SYSPARM_LIMIT.getId(), "10")
    .withHeader(ServiceNowConstants.TABLE, "incident")
    .withHeader(ServiceNowConstants.MODEL, Incident.class)
    .to("direct:servicenow")
    .send();
```