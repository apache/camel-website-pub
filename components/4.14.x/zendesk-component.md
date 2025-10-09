# Zendesk

**Since Camel 2.19**

**Both producer and consumer are supported**

The Zendesk component provides access to all the zendesk.com APIs accessible using [zendesk-java-client](https://github.com/cloudbees/zendesk-java-client). It allows producing messages to manage Zendesk ticket, user, organization, etc.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-zendesk</artifactId>
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

The Zendesk component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serverUrl** (common) | The server URL to connect. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Component configuration. |  | ZendeskConfiguration |
| **zendesk** (advanced) | To use a shared Zendesk instance. |  | Zendesk |
| **oauthToken** (security) | The OAuth token. |  | String |
| **password** (security) | The password. |  | String |
| **token** (security) | The security token. |  | String |
| **username** (security) | The user name. |  | String |

## Endpoint Options

The Zendesk endpoint is configured using URI syntax:

zendesk:methodName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **methodName** (common) | 
**Required** What operation to use.

Enum values:

-   ADD\_TAG\_TO\_ORGANISATIONS
    
-   ADD\_TAG\_TO\_TICKET
    
-   ADD\_TAG\_TO\_TOPICS
    
-   ASSOCIATE\_ATTACHMENTS\_TO\_ARTICLE
    
-   CHANGE\_USER\_PASSWORD
    
-   CREATE\_ARTICLE
    
-   CREATE\_ARTICLE\_1
    
-   CREATE\_ARTICLE\_TRANSLATION
    
-   CREATE\_AUTOMATION
    
-   CREATE\_CATEGORY
    
-   CREATE\_CATEGORY\_TRANSLATION
    
-   CREATE\_COMMENT
    
-   CREATE\_CONTENT\_TAG
    
-   CREATE\_DYNAMIC\_CONTENT\_ITEM
    
-   CREATE\_DYNAMIC\_CONTENT\_ITEM\_VARIANT
    
-   CREATE\_FORUM
    
-   CREATE\_GROUP
    
-   CREATE\_GROUP\_MEMBERSHIP
    
-   CREATE\_GROUP\_MEMBERSHIP\_1
    
-   CREATE\_MACRO
    
-   CREATE\_OR\_UPDATE\_ORGANIZATION
    
-   CREATE\_OR\_UPDATE\_USER
    
-   CREATE\_OR\_UPDATE\_USERS
    
-   CREATE\_OR\_UPDATE\_USERS\_1
    
-   CREATE\_OR\_UPDATE\_USERS\_ASYNC
    
-   CREATE\_ORGANIZATION
    
-   CREATE\_ORGANIZATION\_MEMBERSHIP
    
-   CREATE\_ORGANIZATION\_MEMBERSHIP\_1
    
-   CREATE\_ORGANIZATION\_MEMBERSHIPS
    
-   CREATE\_ORGANIZATION\_MEMBERSHIPS\_1
    
-   CREATE\_ORGANIZATION\_MEMBERSHIPS\_ASYNC
    
-   CREATE\_ORGANIZATIONS
    
-   CREATE\_ORGANIZATIONS\_1
    
-   CREATE\_ORGANIZATIONS\_ASYNC
    
-   CREATE\_PERMISSION\_GROUP
    
-   CREATE\_REQUEST
    
-   CREATE\_SATISFACTION\_RATING
    
-   CREATE\_SATISFACTION\_RATING\_1
    
-   CREATE\_SECTION
    
-   CREATE\_SECTION\_TRANSLATION
    
-   CREATE\_TARGET
    
-   CREATE\_TICKET
    
-   CREATE\_TICKET\_ASYNC
    
-   CREATE\_TICKET\_FIELD
    
-   CREATE\_TICKET\_FORM
    
-   CREATE\_TICKET\_FROM\_TWEET
    
-   CREATE\_TICKETS
    
-   CREATE\_TICKETS\_1
    
-   CREATE\_TICKETS\_ASYNC
    
-   CREATE\_TOPIC
    
-   CREATE\_TRIGGER
    
-   CREATE\_UPLOAD
    
-   CREATE\_UPLOAD\_1
    
-   CREATE\_UPLOAD\_2
    
-   CREATE\_UPLOAD\_ARTICLE
    
-   CREATE\_UPLOAD\_ARTICLE\_1
    
-   CREATE\_USER
    
-   CREATE\_USER\_IDENTITY
    
-   CREATE\_USER\_IDENTITY\_1
    
-   CREATE\_USER\_SEGMENT
    
-   CREATE\_USERS
    
-   CREATE\_USERS\_1
    
-   CREATE\_USERS\_ASYNC
    
-   DELETE\_ARTICLE
    
-   DELETE\_ARTICLE\_ATTACHMENT
    
-   DELETE\_ARTICLE\_ATTACHMENT\_1
    
-   DELETE\_ATTACHMENT
    
-   DELETE\_ATTACHMENT\_1
    
-   DELETE\_AUTOMATION
    
-   DELETE\_CATEGORY
    
-   DELETE\_CONTENT\_TAG
    
-   DELETE\_DYNAMIC\_CONTENT\_ITEM
    
-   DELETE\_DYNAMIC\_CONTENT\_ITEM\_VARIANT
    
-   DELETE\_FORUM
    
-   DELETE\_GROUP
    
-   DELETE\_GROUP\_1
    
-   DELETE\_GROUP\_MEMBERSHIP
    
-   DELETE\_GROUP\_MEMBERSHIP\_1
    
-   DELETE\_GROUP\_MEMBERSHIP\_2
    
-   DELETE\_GROUP\_MEMBERSHIP\_3
    
-   DELETE\_ORGANIZATION
    
-   DELETE\_ORGANIZATION\_1
    
-   DELETE\_ORGANIZATION\_MEMBERSHIP
    
-   DELETE\_ORGANIZATION\_MEMBERSHIP\_1
    
-   DELETE\_ORGANIZATION\_MEMBERSHIP\_2
    
-   DELETE\_ORGANIZATION\_MEMBERSHIPS
    
-   DELETE\_ORGANIZATIONS
    
-   DELETE\_PERMISSION\_GROUP
    
-   DELETE\_PERMISSION\_GROUP\_1
    
-   DELETE\_SECTION
    
-   DELETE\_SUSPENDED\_TICKET
    
-   DELETE\_SUSPENDED\_TICKET\_1
    
-   DELETE\_TARGET
    
-   DELETE\_TICKET
    
-   DELETE\_TICKET\_1
    
-   DELETE\_TICKET\_FIELD
    
-   DELETE\_TICKET\_FIELD\_1
    
-   DELETE\_TICKET\_FORM
    
-   DELETE\_TICKET\_FORM\_1
    
-   DELETE\_TICKETS
    
-   DELETE\_TOPIC
    
-   DELETE\_TRANSLATION
    
-   DELETE\_TRANSLATION\_1
    
-   DELETE\_TRIGGER
    
-   DELETE\_UPLOAD
    
-   DELETE\_UPLOAD\_1
    
-   DELETE\_USER
    
-   DELETE\_USER\_1
    
-   DELETE\_USER\_IDENTITY
    
-   DELETE\_USER\_IDENTITY\_1
    
-   DELETE\_USER\_IDENTITY\_2
    
-   DELETE\_USER\_SEGMENT
    
-   DELETE\_USER\_SEGMENT\_1
    
-   DELETE\_USERS
    
-   EXECUTE\_VIEW
    
-   GET\_ACTIVE\_TRIGGERS
    
-   GET\_ARTICLE
    
-   GET\_ARTICLE\_FROM\_SEARCH
    
-   GET\_ARTICLE\_FROM\_SEARCH\_1
    
-   GET\_ARTICLE\_SUBSCRIPTIONS
    
-   GET\_ARTICLE\_SUBSCRIPTIONS\_1
    
-   GET\_ARTICLE\_TRANSLATIONS
    
-   GET\_ARTICLES
    
-   GET\_ARTICLES\_1
    
-   GET\_ARTICLES\_2
    
-   GET\_ARTICLES\_3
    
-   GET\_ARTICLES\_4
    
-   GET\_ARTICLES\_5
    
-   GET\_ARTICLES\_FROM\_ALL\_LABELS
    
-   GET\_ARTICLES\_FROM\_ANY\_LABELS
    
-   GET\_ARTICLES\_FROM\_PAGE
    
-   GET\_ARTICLES\_INCREMENTALLY
    
-   GET\_ASSIGNABLE\_GROUP\_MEMBERSHIPS
    
-   GET\_ASSIGNABLE\_GROUP\_MEMBERSHIPS\_1
    
-   GET\_ASSIGNABLE\_GROUPS
    
-   GET\_ASSIGNED\_TICKETS\_COUNT\_FOR\_USER
    
-   GET\_ATTACHMENT
    
-   GET\_ATTACHMENT\_1
    
-   GET\_ATTACHMENTS\_FROM\_ARTICLE
    
-   GET\_AUTHENTICATED\_USER
    
-   GET\_AUTO\_COMPLETE\_ORGANIZATIONS
    
-   GET\_AUTOMATION
    
-   GET\_AUTOMATIONS
    
-   GET\_BRANDS
    
-   GET\_CC\_REQUESTS
    
-   GET\_CATEGORIES
    
-   GET\_CATEGORY
    
-   GET\_CATEGORY\_TRANSLATIONS
    
-   GET\_CCD\_TICKETS\_COUNT\_FOR\_USER
    
-   GET\_COMPLIANCE\_DELETION\_STATUSES
    
-   GET\_CONTENT\_TAG
    
-   GET\_CONTENT\_TAGS
    
-   GET\_CONTENT\_TAGS\_1
    
-   GET\_CONTENT\_TAGS\_2
    
-   GET\_CURRENT\_USER
    
-   GET\_CUSTOM\_AGENT\_ROLES
    
-   GET\_CUSTOM\_TICKET\_STATUSES
    
-   GET\_DELETED\_TICKETS
    
-   GET\_DELETED\_TICKETS\_1
    
-   GET\_DYNAMIC\_CONTENT\_ITEM
    
-   GET\_DYNAMIC\_CONTENT\_ITEM\_VARIANT
    
-   GET\_DYNAMIC\_CONTENT\_ITEM\_VARIANTS
    
-   GET\_DYNAMIC\_CONTENT\_ITEMS
    
-   GET\_FORUM
    
-   GET\_FORUMS
    
-   GET\_FORUMS\_1
    
-   GET\_GROUP
    
-   GET\_GROUP\_MEMBERSHIP
    
-   GET\_GROUP\_MEMBERSHIP\_1
    
-   GET\_GROUP\_MEMBERSHIP\_BY\_USER
    
-   GET\_GROUP\_MEMBERSHIPS
    
-   GET\_GROUP\_MEMBERSHIPS\_1
    
-   GET\_GROUP\_ORGANIZATION
    
-   GET\_GROUP\_USERS
    
-   GET\_GROUPS
    
-   GET\_HELP\_CENTER\_LOCALES
    
-   GET\_HOLIDAYS\_FOR\_SCHEDULE
    
-   GET\_HOLIDAYS\_FOR\_SCHEDULE\_1
    
-   GET\_INCREMENTAL\_TICKETS\_RESULT
    
-   GET\_JIRA\_LINKS
    
-   GET\_JOB\_STATUS
    
-   GET\_JOB\_STATUS\_ASYNC
    
-   GET\_JOB\_STATUSES
    
-   GET\_JOB\_STATUSES\_ASYNC
    
-   GET\_LOCALES
    
-   GET\_MACRO
    
-   GET\_MACROS
    
-   GET\_OPEN\_REQUESTS
    
-   GET\_ORGANIZATION
    
-   GET\_ORGANIZATION\_FIELDS
    
-   GET\_ORGANIZATION\_MEMBERSHIP
    
-   GET\_ORGANIZATION\_MEMBERSHIP\_BY\_USER
    
-   GET\_ORGANIZATION\_MEMBERSHIP\_FOR\_USER
    
-   GET\_ORGANIZATION\_MEMBERSHIPS
    
-   GET\_ORGANIZATION\_MEMBERSHIPS\_FOR\_ORG
    
-   GET\_ORGANIZATION\_MEMBERSHIPS\_FOR\_USER
    
-   GET\_ORGANIZATION\_REQUESTS
    
-   GET\_ORGANIZATION\_TICKETS
    
-   GET\_ORGANIZATION\_USERS
    
-   GET\_ORGANIZATIONS
    
-   GET\_ORGANIZATIONS\_1
    
-   GET\_ORGANIZATIONS\_INCREMENTALLY
    
-   GET\_PERMISSION\_GROUP
    
-   GET\_PERMISSION\_GROUPS
    
-   GET\_RECENT\_TICKETS
    
-   GET\_REQUEST
    
-   GET\_REQUEST\_COMMENT
    
-   GET\_REQUEST\_COMMENT\_1
    
-   GET\_REQUEST\_COMMENT\_2
    
-   GET\_REQUEST\_COMMENTS
    
-   GET\_REQUEST\_COMMENTS\_1
    
-   GET\_REQUESTS
    
-   GET\_SATISFACTION\_RATING
    
-   GET\_SATISFACTION\_RATINGS
    
-   GET\_SCHEDULE
    
-   GET\_SCHEDULE\_1
    
-   GET\_SCHEDULES
    
-   GET\_SEARCH\_TICKET\_RESULTS
    
-   GET\_SECTION
    
-   GET\_SECTION\_SUBSCRIPTIONS
    
-   GET\_SECTION\_SUBSCRIPTIONS\_1
    
-   GET\_SECTION\_TRANSLATIONS
    
-   GET\_SECTIONS
    
-   GET\_SECTIONS\_1
    
-   GET\_SECTIONS\_2
    
-   GET\_SOLVED\_REQUESTS
    
-   GET\_SUSPENDED\_TICKETS
    
-   GET\_TARGET
    
-   GET\_TARGETS
    
-   GET\_TICKET
    
-   GET\_TICKET\_AUDIT
    
-   GET\_TICKET\_AUDIT\_1
    
-   GET\_TICKET\_AUDIT\_2
    
-   GET\_TICKET\_AUDITS
    
-   GET\_TICKET\_AUDITS\_1
    
-   GET\_TICKET\_COLLABORATORS
    
-   GET\_TICKET\_COMMENTS
    
-   GET\_TICKET\_COMMENTS\_1
    
-   GET\_TICKET\_FIELD
    
-   GET\_TICKET\_FIELDS
    
-   GET\_TICKET\_FORM
    
-   GET\_TICKET\_FORMS
    
-   GET\_TICKET\_INCIDENTS
    
-   GET\_TICKET\_METRIC
    
-   GET\_TICKET\_METRIC\_BY\_TICKET
    
-   GET\_TICKET\_METRICS
    
-   GET\_TICKETS
    
-   GET\_TICKETS\_1
    
-   GET\_TICKETS\_BY\_EXTERNAL\_ID
    
-   GET\_TICKETS\_BY\_EXTERNAL\_ID\_1
    
-   GET\_TICKETS\_COUNT
    
-   GET\_TICKETS\_COUNT\_FOR\_ORGANIZATION
    
-   GET\_TICKETS\_FROM\_SEARCH
    
-   GET\_TICKETS\_INCREMENTALLY
    
-   GET\_TICKETS\_INCREMENTALLY\_1
    
-   GET\_TIME\_ZONES
    
-   GET\_TOPIC
    
-   GET\_TOPICS
    
-   GET\_TOPICS\_1
    
-   GET\_TOPICS\_2
    
-   GET\_TOPICS\_3
    
-   GET\_TOPICS\_BY\_USER
    
-   GET\_TRIGGER
    
-   GET\_TRIGGERS
    
-   GET\_TRIGGERS\_1
    
-   GET\_TWITTER\_MONITORS
    
-   GET\_USER
    
-   GET\_USER\_CCD\_TICKETS
    
-   GET\_USER\_FIELDS
    
-   GET\_USER\_IDENTITIES
    
-   GET\_USER\_IDENTITIES\_1
    
-   GET\_USER\_IDENTITY
    
-   GET\_USER\_IDENTITY\_1
    
-   GET\_USER\_IDENTITY\_2
    
-   GET\_USER\_RELATED\_INFO
    
-   GET\_USER\_REQUESTED\_TICKETS
    
-   GET\_USER\_REQUESTS
    
-   GET\_USER\_REQUESTS\_1
    
-   GET\_USER\_SEGMENT
    
-   GET\_USER\_SEGMENTS
    
-   GET\_USER\_SEGMENTS\_1
    
-   GET\_USER\_SEGMENTS\_APPLICABLE
    
-   GET\_USER\_SUBSCRIPTIONS
    
-   GET\_USER\_SUBSCRIPTIONS\_1
    
-   GET\_USERS
    
-   GET\_USERS\_1
    
-   GET\_USERS\_BY\_EXTERNAL\_IDS
    
-   GET\_USERS\_BY\_EXTERNAL\_IDS\_1
    
-   GET\_USERS\_BY\_ROLE
    
-   GET\_USERS\_INCREMENTALLY
    
-   GET\_VIEW
    
-   GET\_VIEWS
    
-   IMPORT\_TICKET
    
-   IMPORT\_TOPIC
    
-   LIST\_HELP\_CENTER\_LOCALES
    
-   LOOKUP\_ORGANIZATIONS\_BY\_EXTERNAL\_ID
    
-   LOOKUP\_USER\_BY\_EMAIL
    
-   LOOKUP\_USER\_BY\_EXTERNAL\_ID
    
-   MACROS\_SHOW\_CHANGES\_TO\_TICKET
    
-   MACROS\_SHOW\_TICKET\_AFTER\_CHANGES
    
-   MAKE\_PRIVATE\_TICKET\_AUDIT
    
-   MAKE\_PRIVATE\_TICKET\_AUDIT\_1
    
-   MAKE\_PRIVATE\_TICKET\_AUDIT\_2
    
-   MARK\_TICKET\_AS\_SPAM
    
-   MARK\_TICKET\_AS\_SPAM\_1
    
-   MERGE\_USERS
    
-   NOTIFY\_APP
    
-   PERMANENTLY\_DELETE\_TICKET
    
-   PERMANENTLY\_DELETE\_TICKET\_1
    
-   PERMANENTLY\_DELETE\_TICKETS
    
-   PERMANENTLY\_DELETE\_USER
    
-   PERMANENTLY\_DELETE\_USER\_1
    
-   QUEUE\_CREATE\_TICKET\_ASYNC
    
-   REMOVE\_TAG\_FROM\_ORGANISATIONS
    
-   REMOVE\_TAG\_FROM\_TICKET
    
-   REMOVE\_TAG\_FROM\_TOPICS
    
-   REQUEST\_VERIFY\_USER\_IDENTITY
    
-   REQUEST\_VERIFY\_USER\_IDENTITY\_1
    
-   REQUEST\_VERIFY\_USER\_IDENTITY\_2
    
-   RESET\_USER\_PASSWORD
    
-   RESET\_USER\_PASSWORD\_1
    
-   SEARCH\_TRIGGERS
    
-   SEARCH\_TRIGGERS\_1
    
-   SET\_GROUP\_MEMBERSHIP\_AS\_DEFAULT
    
-   SET\_ORGANIZATION\_MEMBERSHIP\_AS\_DEFAULT
    
-   SET\_TAG\_ON\_ORGANISATIONS
    
-   SET\_TAG\_ON\_TICKET
    
-   SET\_TAG\_ON\_TOPICS
    
-   SET\_USER\_PRIMARY\_IDENTITY
    
-   SET\_USER\_PRIMARY\_IDENTITY\_1
    
-   SET\_USER\_PRIMARY\_IDENTITY\_2
    
-   SHOW\_ARTICLE\_TRANSLATION
    
-   SHOW\_CATEGORY\_TRANSLATION
    
-   SHOW\_SECTION\_TRANSLATION
    
-   SUSPEND\_USER
    
-   TRUST\_TICKET\_AUDIT
    
-   TRUST\_TICKET\_AUDIT\_1
    
-   TRUST\_TICKET\_AUDIT\_2
    
-   UNASSIGN\_ORGANIZATION\_MEMBERSHIP
    
-   UNSUSPEND\_USER
    
-   UPDATE\_ARTICLE
    
-   UPDATE\_ARTICLE\_TRANSLATION
    
-   UPDATE\_AUTOMATION
    
-   UPDATE\_CATEGORY
    
-   UPDATE\_CATEGORY\_TRANSLATION
    
-   UPDATE\_CONTENT\_TAG
    
-   UPDATE\_DYNAMIC\_CONTENT\_ITEM
    
-   UPDATE\_DYNAMIC\_CONTENT\_ITEM\_VARIANT
    
-   UPDATE\_FORUM
    
-   UPDATE\_GROUP
    
-   UPDATE\_INSTALLATION
    
-   UPDATE\_MACRO
    
-   UPDATE\_ORGANIZATION
    
-   UPDATE\_ORGANIZATIONS
    
-   UPDATE\_ORGANIZATIONS\_1
    
-   UPDATE\_ORGANIZATIONS\_ASYNC
    
-   UPDATE\_PERMISSION\_GROUP
    
-   UPDATE\_REQUEST
    
-   UPDATE\_SECTION
    
-   UPDATE\_SECTION\_TRANSLATION
    
-   UPDATE\_TICKET
    
-   UPDATE\_TICKET\_FIELD
    
-   UPDATE\_TICKET\_FORM
    
-   UPDATE\_TICKETS
    
-   UPDATE\_TICKETS\_1
    
-   UPDATE\_TICKETS\_ASYNC
    
-   UPDATE\_TOPIC
    
-   UPDATE\_TRIGGER
    
-   UPDATE\_USER
    
-   UPDATE\_USER\_IDENTITY
    
-   UPDATE\_USER\_IDENTITY\_1
    
-   UPDATE\_USER\_SEGMENT
    
-   UPDATE\_USERS
    
-   UPDATE\_USERS\_1
    
-   UPDATE\_USERS\_ASYNC
    
-   VERIFY\_USER\_IDENTITY
    
-   VERIFY\_USER\_IDENTITY\_1
    
-   VERIFY\_USER\_IDENTITY\_2
    





 |  | ZendeskApiMethod |

### Query Parameters (26 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **serverUrl** (common) | The server URL to connect. |  | String |
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
| **oauthToken** (security) | The OAuth token. |  | String |
| **password** (security) | The password. |  | String |
| **token** (security) | The security token. |  | String |
| **username** (security) | The user name. |  | String |

## API Parameters (1 APIs)

The Zendesk endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `methodName` path parameters:

zendesk:methodName

There are 1 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**DEFAULT**](#_api_DEFAULT) | Both | 
 |

Each API is documented in the following sections to come.

### API: DEFAULT

**Both producer and consumer are supported**

The DEFAULT API is defined in the syntax as follows:

```none
zendesk:DEFAULT/methodName?[parameters]
```

The 283 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addTagToOrganisations**](#_api_DEFAULT_method_addTagToOrganisations) |  | 
 |
| [**addTagToTicket**](#_api_DEFAULT_method_addTagToTicket) |  | 

 |
| [**addTagToTopics**](#_api_DEFAULT_method_addTagToTopics) |  | 

 |
| [**associateAttachmentsToArticle**](#_api_DEFAULT_method_associateAttachmentsToArticle) |  | 

 |
| [**changeUserPassword**](#_api_DEFAULT_method_changeUserPassword) |  | 

 |
| [**createArticle**](#_api_DEFAULT_method_createArticle) |  | 

 |
| [**createArticleTranslation**](#_api_DEFAULT_method_createArticleTranslation) |  | 

 |
| [**createAutomation**](#_api_DEFAULT_method_createAutomation) |  | 

 |
| [**createCategory**](#_api_DEFAULT_method_createCategory) |  | 

 |
| [**createCategoryTranslation**](#_api_DEFAULT_method_createCategoryTranslation) |  | 

 |
| [**createComment**](#_api_DEFAULT_method_createComment) |  | 

 |
| [**createContentTag**](#_api_DEFAULT_method_createContentTag) |  | 

 |
| [**createDynamicContentItem**](#_api_DEFAULT_method_createDynamicContentItem) |  | 

 |
| [**createDynamicContentItemVariant**](#_api_DEFAULT_method_createDynamicContentItemVariant) |  | 

 |
| [**createForum**](#_api_DEFAULT_method_createForum) |  | 

 |
| [**createGroup**](#_api_DEFAULT_method_createGroup) |  | 

 |
| [**createGroupMembership**](#_api_DEFAULT_method_createGroupMembership) |  | 

 |
| [**createMacro**](#_api_DEFAULT_method_createMacro) |  | 

 |
| [**createOrUpdateOrganization**](#_api_DEFAULT_method_createOrUpdateOrganization) |  | 

 |
| [**createOrUpdateUser**](#_api_DEFAULT_method_createOrUpdateUser) |  | 

 |
| [**createOrUpdateUsers**](#_api_DEFAULT_method_createOrUpdateUsers) |  | 

 |
| [**createOrUpdateUsersAsync**](#_api_DEFAULT_method_createOrUpdateUsersAsync) |  | 

 |
| [**createOrganization**](#_api_DEFAULT_method_createOrganization) |  | 

 |
| [**createOrganizationMembership**](#_api_DEFAULT_method_createOrganizationMembership) |  | 

 |
| [**createOrganizationMemberships**](#_api_DEFAULT_method_createOrganizationMemberships) |  | 

 |
| [**createOrganizationMembershipsAsync**](#_api_DEFAULT_method_createOrganizationMembershipsAsync) |  | 

 |
| [**createOrganizations**](#_api_DEFAULT_method_createOrganizations) |  | 

 |
| [**createOrganizationsAsync**](#_api_DEFAULT_method_createOrganizationsAsync) |  | 

 |
| [**createPermissionGroup**](#_api_DEFAULT_method_createPermissionGroup) |  | Create permission group |
| [**createRequest**](#_api_DEFAULT_method_createRequest) |  | 

 |
| [**createSatisfactionRating**](#_api_DEFAULT_method_createSatisfactionRating) |  | 

 |
| [**createSection**](#_api_DEFAULT_method_createSection) |  | 

 |
| [**createSectionTranslation**](#_api_DEFAULT_method_createSectionTranslation) |  | 

 |
| [**createTarget**](#_api_DEFAULT_method_createTarget) |  | 

 |
| [**createTicket**](#_api_DEFAULT_method_createTicket) |  | 

 |
| [**createTicketAsync**](#_api_DEFAULT_method_createTicketAsync) |  | 

 |
| [**createTicketField**](#_api_DEFAULT_method_createTicketField) |  | 

 |
| [**createTicketForm**](#_api_DEFAULT_method_createTicketForm) |  | 

 |
| [**createTicketFromTweet**](#_api_DEFAULT_method_createTicketFromTweet) |  | 

 |
| [**createTickets**](#_api_DEFAULT_method_createTickets) |  | 

 |
| [**createTicketsAsync**](#_api_DEFAULT_method_createTicketsAsync) |  | 

 |
| [**createTopic**](#_api_DEFAULT_method_createTopic) |  | 

 |
| [**createTrigger**](#_api_DEFAULT_method_createTrigger) |  | 

 |
| [**createUpload**](#_api_DEFAULT_method_createUpload) |  | 

 |
| [**createUploadArticle**](#_api_DEFAULT_method_createUploadArticle) |  | 

 |
| [**createUser**](#_api_DEFAULT_method_createUser) |  | 

 |
| [**createUserIdentity**](#_api_DEFAULT_method_createUserIdentity) |  | 

 |
| [**createUserSegment**](#_api_DEFAULT_method_createUserSegment) |  | Create User Segment |
| [**createUsers**](#_api_DEFAULT_method_createUsers) |  | 

 |
| [**createUsersAsync**](#_api_DEFAULT_method_createUsersAsync) |  | 

 |
| [**deleteArticle**](#_api_DEFAULT_method_deleteArticle) |  | 

 |
| [**deleteArticleAttachment**](#_api_DEFAULT_method_deleteArticleAttachment) |  | Delete attachment from article |
| [**deleteAttachment**](#_api_DEFAULT_method_deleteAttachment) |  | 

 |
| [**deleteAutomation**](#_api_DEFAULT_method_deleteAutomation) |  | 

 |
| [**deleteCategory**](#_api_DEFAULT_method_deleteCategory) |  | 

 |
| [**deleteContentTag**](#_api_DEFAULT_method_deleteContentTag) |  | 

 |
| [**deleteDynamicContentItem**](#_api_DEFAULT_method_deleteDynamicContentItem) |  | 

 |
| [**deleteDynamicContentItemVariant**](#_api_DEFAULT_method_deleteDynamicContentItemVariant) |  | 

 |
| [**deleteForum**](#_api_DEFAULT_method_deleteForum) |  | 

 |
| [**deleteGroup**](#_api_DEFAULT_method_deleteGroup) |  | 

 |
| [**deleteGroupMembership**](#_api_DEFAULT_method_deleteGroupMembership) |  | 

 |
| [**deleteOrganization**](#_api_DEFAULT_method_deleteOrganization) |  | 

 |
| [**deleteOrganizationMembership**](#_api_DEFAULT_method_deleteOrganizationMembership) |  | 

 |
| [**deleteOrganizationMemberships**](#_api_DEFAULT_method_deleteOrganizationMemberships) |  | 

 |
| [**deleteOrganizations**](#_api_DEFAULT_method_deleteOrganizations) |  | 

 |
| [**deletePermissionGroup**](#_api_DEFAULT_method_deletePermissionGroup) |  | Delete permission group |
| [**deleteSection**](#_api_DEFAULT_method_deleteSection) |  | 

 |
| [**deleteSuspendedTicket**](#_api_DEFAULT_method_deleteSuspendedTicket) |  | 

 |
| [**deleteTarget**](#_api_DEFAULT_method_deleteTarget) |  | 

 |
| [**deleteTicket**](#_api_DEFAULT_method_deleteTicket) |  | 

 |
| [**deleteTicketField**](#_api_DEFAULT_method_deleteTicketField) |  | 

 |
| [**deleteTicketForm**](#_api_DEFAULT_method_deleteTicketForm) |  | 

 |
| [**deleteTickets**](#_api_DEFAULT_method_deleteTickets) |  | 

 |
| [**deleteTopic**](#_api_DEFAULT_method_deleteTopic) |  | 

 |
| [**deleteTranslation**](#_api_DEFAULT_method_deleteTranslation) |  | Delete translation |
| [**deleteTrigger**](#_api_DEFAULT_method_deleteTrigger) |  | 

 |
| [**deleteUpload**](#_api_DEFAULT_method_deleteUpload) |  | 

 |
| [**deleteUser**](#_api_DEFAULT_method_deleteUser) |  | 

 |
| [**deleteUserIdentity**](#_api_DEFAULT_method_deleteUserIdentity) |  | 

 |
| [**deleteUserSegment**](#_api_DEFAULT_method_deleteUserSegment) |  | Delete User Segment |
| [**deleteUsers**](#_api_DEFAULT_method_deleteUsers) |  | 

 |
| [**executeView**](#_api_DEFAULT_method_executeView) |  | 

 |
| [**getActiveTriggers**](#_api_DEFAULT_method_getActiveTriggers) |  | 

 |
| [**getArticle**](#_api_DEFAULT_method_getArticle) |  | 

 |
| [**getArticleFromSearch**](#_api_DEFAULT_method_getArticleFromSearch) |  | 

 |
| [**getArticleSubscriptions**](#_api_DEFAULT_method_getArticleSubscriptions) |  | 

 |
| [**getArticleTranslations**](#_api_DEFAULT_method_getArticleTranslations) |  | 

 |
| [**getArticles**](#_api_DEFAULT_method_getArticles) |  | Get all articles from help center |
| [**getArticlesFromAllLabels**](#_api_DEFAULT_method_getArticlesFromAllLabels) |  | 

 |
| [**getArticlesFromAnyLabels**](#_api_DEFAULT_method_getArticlesFromAnyLabels) |  | 

 |
| [**getArticlesFromPage**](#_api_DEFAULT_method_getArticlesFromPage) |  | 

 |
| [**getArticlesIncrementally**](#_api_DEFAULT_method_getArticlesIncrementally) |  | 

 |
| [**getAssignableGroupMemberships**](#_api_DEFAULT_method_getAssignableGroupMemberships) |  | 

 |
| [**getAssignableGroups**](#_api_DEFAULT_method_getAssignableGroups) |  | 

 |
| [**getAssignedTicketsCountForUser**](#_api_DEFAULT_method_getAssignedTicketsCountForUser) |  | 

 |
| [**getAttachment**](#_api_DEFAULT_method_getAttachment) |  | 

 |
| [**getAttachmentsFromArticle**](#_api_DEFAULT_method_getAttachmentsFromArticle) |  | 

 |
| [**getAuthenticatedUser**](#_api_DEFAULT_method_getAuthenticatedUser) |  | 

 |
| [**getAutoCompleteOrganizations**](#_api_DEFAULT_method_getAutoCompleteOrganizations) |  | 

 |
| [**getAutomation**](#_api_DEFAULT_method_getAutomation) |  | 

 |
| [**getAutomations**](#_api_DEFAULT_method_getAutomations) |  | 

 |
| [**getBrands**](#_api_DEFAULT_method_getBrands) |  | 

 |
| [**getCCRequests**](#_api_DEFAULT_method_getCCRequests) |  | 

 |
| [**getCategories**](#_api_DEFAULT_method_getCategories) |  | 

 |
| [**getCategory**](#_api_DEFAULT_method_getCategory) |  | 

 |
| [**getCategoryTranslations**](#_api_DEFAULT_method_getCategoryTranslations) |  | 

 |
| [**getCcdTicketsCountForUser**](#_api_DEFAULT_method_getCcdTicketsCountForUser) |  | 

 |
| [**getComplianceDeletionStatuses**](#_api_DEFAULT_method_getComplianceDeletionStatuses) |  | 

 |
| [**getContentTag**](#_api_DEFAULT_method_getContentTag) |  | 

 |
| [**getContentTags**](#_api_DEFAULT_method_getContentTags) |  | 

 |
| [**getCurrentUser**](#_api_DEFAULT_method_getCurrentUser) |  | 

 |
| [**getCustomAgentRoles**](#_api_DEFAULT_method_getCustomAgentRoles) |  | 

 |
| [**getCustomTicketStatuses**](#_api_DEFAULT_method_getCustomTicketStatuses) |  | 

 |
| [**getDeletedTickets**](#_api_DEFAULT_method_getDeletedTickets) |  | 

 |
| [**getDynamicContentItem**](#_api_DEFAULT_method_getDynamicContentItem) |  | 

 |
| [**getDynamicContentItemVariant**](#_api_DEFAULT_method_getDynamicContentItemVariant) |  | 

 |
| [**getDynamicContentItemVariants**](#_api_DEFAULT_method_getDynamicContentItemVariants) |  | 

 |
| [**getDynamicContentItems**](#_api_DEFAULT_method_getDynamicContentItems) |  | 

 |
| [**getForum**](#_api_DEFAULT_method_getForum) |  | 

 |
| [**getForums**](#_api_DEFAULT_method_getForums) |  | 

 |
| [**getGroup**](#_api_DEFAULT_method_getGroup) |  | 

 |
| [**getGroupMembership**](#_api_DEFAULT_method_getGroupMembership) |  | 

 |
| [**getGroupMembershipByUser**](#_api_DEFAULT_method_getGroupMembershipByUser) |  | 

 |
| [**getGroupMemberships**](#_api_DEFAULT_method_getGroupMemberships) |  | 

 |
| [**getGroupOrganization**](#_api_DEFAULT_method_getGroupOrganization) |  | 

 |
| [**getGroupUsers**](#_api_DEFAULT_method_getGroupUsers) |  | 

 |
| [**getGroups**](#_api_DEFAULT_method_getGroups) |  | 

 |
| [**getHelpCenterLocales**](#_api_DEFAULT_method_getHelpCenterLocales) |  | 

 |
| [**getHolidaysForSchedule**](#_api_DEFAULT_method_getHolidaysForSchedule) |  | 

 |
| [**getIncrementalTicketsResult**](#_api_DEFAULT_method_getIncrementalTicketsResult) |  | 

 |
| [**getJiraLinks**](#_api_DEFAULT_method_getJiraLinks) |  | 

 |
| [**getJobStatus**](#_api_DEFAULT_method_getJobStatus) |  | 

 |
| [**getJobStatusAsync**](#_api_DEFAULT_method_getJobStatusAsync) |  | 

 |
| [**getJobStatuses**](#_api_DEFAULT_method_getJobStatuses) |  | 

 |
| [**getJobStatusesAsync**](#_api_DEFAULT_method_getJobStatusesAsync) |  | 

 |
| [**getLocales**](#_api_DEFAULT_method_getLocales) |  | 

 |
| [**getMacro**](#_api_DEFAULT_method_getMacro) |  | 

 |
| [**getMacros**](#_api_DEFAULT_method_getMacros) |  | 

 |
| [**getOpenRequests**](#_api_DEFAULT_method_getOpenRequests) |  | 

 |
| [**getOrganization**](#_api_DEFAULT_method_getOrganization) |  | 

 |
| [**getOrganizationFields**](#_api_DEFAULT_method_getOrganizationFields) |  | 

 |
| [**getOrganizationMembership**](#_api_DEFAULT_method_getOrganizationMembership) |  | 

 |
| [**getOrganizationMembershipByUser**](#_api_DEFAULT_method_getOrganizationMembershipByUser) |  | 

 |
| [**getOrganizationMembershipForUser**](#_api_DEFAULT_method_getOrganizationMembershipForUser) |  | 

 |
| [**getOrganizationMemberships**](#_api_DEFAULT_method_getOrganizationMemberships) |  | 

 |
| [**getOrganizationMembershipsForOrg**](#_api_DEFAULT_method_getOrganizationMembershipsForOrg) |  | 

 |
| [**getOrganizationMembershipsForUser**](#_api_DEFAULT_method_getOrganizationMembershipsForUser) |  | 

 |
| [**getOrganizationRequests**](#_api_DEFAULT_method_getOrganizationRequests) |  | 

 |
| [**getOrganizationTickets**](#_api_DEFAULT_method_getOrganizationTickets) |  | 

 |
| [**getOrganizationUsers**](#_api_DEFAULT_method_getOrganizationUsers) |  | 

 |
| [**getOrganizations**](#_api_DEFAULT_method_getOrganizations) |  | 

 |
| [**getOrganizationsIncrementally**](#_api_DEFAULT_method_getOrganizationsIncrementally) |  | 

 |
| [**getPermissionGroup**](#_api_DEFAULT_method_getPermissionGroup) |  | Get permission group by id |
| [**getPermissionGroups**](#_api_DEFAULT_method_getPermissionGroups) |  | Get all permission groups |
| [**getRecentTickets**](#_api_DEFAULT_method_getRecentTickets) |  | 

 |
| [**getRequest**](#_api_DEFAULT_method_getRequest) |  | 

 |
| [**getRequestComment**](#_api_DEFAULT_method_getRequestComment) |  | 

 |
| [**getRequestComments**](#_api_DEFAULT_method_getRequestComments) |  | 

 |
| [**getRequests**](#_api_DEFAULT_method_getRequests) |  | 

 |
| [**getSatisfactionRating**](#_api_DEFAULT_method_getSatisfactionRating) |  | 

 |
| [**getSatisfactionRatings**](#_api_DEFAULT_method_getSatisfactionRatings) |  | 

 |
| [**getSchedule**](#_api_DEFAULT_method_getSchedule) |  | 

 |
| [**getSchedules**](#_api_DEFAULT_method_getSchedules) |  | Get a list of the current business hours schedules |
| [**getSearchTicketResults**](#_api_DEFAULT_method_getSearchTicketResults) |  | Ticket Search API implementation with pagination support |
| [**getSection**](#_api_DEFAULT_method_getSection) |  | 

 |
| [**getSectionSubscriptions**](#_api_DEFAULT_method_getSectionSubscriptions) |  | 

 |
| [**getSectionTranslations**](#_api_DEFAULT_method_getSectionTranslations) |  | 

 |
| [**getSections**](#_api_DEFAULT_method_getSections) |  | List Sections using a User Segment |
| [**getSolvedRequests**](#_api_DEFAULT_method_getSolvedRequests) |  | 

 |
| [**getSuspendedTickets**](#_api_DEFAULT_method_getSuspendedTickets) |  | 

 |
| [**getTarget**](#_api_DEFAULT_method_getTarget) |  | 

 |
| [**getTargets**](#_api_DEFAULT_method_getTargets) |  | 

 |
| [**getTicket**](#_api_DEFAULT_method_getTicket) |  | 

 |
| [**getTicketAudit**](#_api_DEFAULT_method_getTicketAudit) |  | 

 |
| [**getTicketAudits**](#_api_DEFAULT_method_getTicketAudits) |  | 

 |
| [**getTicketCollaborators**](#_api_DEFAULT_method_getTicketCollaborators) |  | 

 |
| [**getTicketComments**](#_api_DEFAULT_method_getTicketComments) |  | 

 |
| [**getTicketField**](#_api_DEFAULT_method_getTicketField) |  | 

 |
| [**getTicketFields**](#_api_DEFAULT_method_getTicketFields) |  | 

 |
| [**getTicketForm**](#_api_DEFAULT_method_getTicketForm) |  | 

 |
| [**getTicketForms**](#_api_DEFAULT_method_getTicketForms) |  | 

 |
| [**getTicketIncidents**](#_api_DEFAULT_method_getTicketIncidents) |  | 

 |
| [**getTicketMetric**](#_api_DEFAULT_method_getTicketMetric) |  | 

 |
| [**getTicketMetricByTicket**](#_api_DEFAULT_method_getTicketMetricByTicket) |  | 

 |
| [**getTicketMetrics**](#_api_DEFAULT_method_getTicketMetrics) |  | 

 |
| [**getTickets**](#_api_DEFAULT_method_getTickets) |  | 

 |
| [**getTicketsByExternalId**](#_api_DEFAULT_method_getTicketsByExternalId) |  | 

 |
| [**getTicketsCount**](#_api_DEFAULT_method_getTicketsCount) |  | 

 |
| [**getTicketsCountForOrganization**](#_api_DEFAULT_method_getTicketsCountForOrganization) |  | 

 |
| [**getTicketsFromSearch**](#_api_DEFAULT_method_getTicketsFromSearch) |  | 

 |
| [**getTicketsIncrementally**](#_api_DEFAULT_method_getTicketsIncrementally) |  | 

 |
| [**getTimeZones**](#_api_DEFAULT_method_getTimeZones) |  | 

 |
| [**getTopic**](#_api_DEFAULT_method_getTopic) |  | 

 |
| [**getTopics**](#_api_DEFAULT_method_getTopics) |  | List Topics using a User Segment |
| [**getTopicsByUser**](#_api_DEFAULT_method_getTopicsByUser) |  | 

 |
| [**getTrigger**](#_api_DEFAULT_method_getTrigger) |  | 

 |
| [**getTriggers**](#_api_DEFAULT_method_getTriggers) |  | 

 |
| [**getTwitterMonitors**](#_api_DEFAULT_method_getTwitterMonitors) |  | 

 |
| [**getUser**](#_api_DEFAULT_method_getUser) |  | 

 |
| [**getUserCCDTickets**](#_api_DEFAULT_method_getUserCCDTickets) |  | 

 |
| [**getUserFields**](#_api_DEFAULT_method_getUserFields) |  | 

 |
| [**getUserIdentities**](#_api_DEFAULT_method_getUserIdentities) |  | 

 |
| [**getUserIdentity**](#_api_DEFAULT_method_getUserIdentity) |  | 

 |
| [**getUserRelatedInfo**](#_api_DEFAULT_method_getUserRelatedInfo) |  | 

 |
| [**getUserRequestedTickets**](#_api_DEFAULT_method_getUserRequestedTickets) |  | 

 |
| [**getUserRequests**](#_api_DEFAULT_method_getUserRequests) |  | 

 |
| [**getUserSegment**](#_api_DEFAULT_method_getUserSegment) |  | Get user segment by id |
| [**getUserSegments**](#_api_DEFAULT_method_getUserSegments) |  | Returns the list of user segments that a particular user belongs to |
| [**getUserSegmentsApplicable**](#_api_DEFAULT_method_getUserSegmentsApplicable) |  | Request only user segments applicable on the account’s current Guide plan |
| [**getUserSubscriptions**](#_api_DEFAULT_method_getUserSubscriptions) |  | 

 |
| [**getUsers**](#_api_DEFAULT_method_getUsers) |  | 

 |
| [**getUsersByExternalIds**](#_api_DEFAULT_method_getUsersByExternalIds) |  | 

 |
| [**getUsersByRole**](#_api_DEFAULT_method_getUsersByRole) |  | 

 |
| [**getUsersIncrementally**](#_api_DEFAULT_method_getUsersIncrementally) |  | 

 |
| [**getView**](#_api_DEFAULT_method_getView) |  | 

 |
| [**getViews**](#_api_DEFAULT_method_getViews) |  | 

 |
| [**importTicket**](#_api_DEFAULT_method_importTicket) |  | 

 |
| [**importTopic**](#_api_DEFAULT_method_importTopic) |  | 

 |
| [**listHelpCenterLocales**](#_api_DEFAULT_method_listHelpCenterLocales) |  | 

 |
| [**lookupOrganizationsByExternalId**](#_api_DEFAULT_method_lookupOrganizationsByExternalId) |  | 

 |
| [**lookupUserByEmail**](#_api_DEFAULT_method_lookupUserByEmail) |  | 

 |
| [**lookupUserByExternalId**](#_api_DEFAULT_method_lookupUserByExternalId) |  | 

 |
| [**macrosShowChangesToTicket**](#_api_DEFAULT_method_macrosShowChangesToTicket) |  | 

 |
| [**macrosShowTicketAfterChanges**](#_api_DEFAULT_method_macrosShowTicketAfterChanges) |  | 

 |
| [**makePrivateTicketAudit**](#_api_DEFAULT_method_makePrivateTicketAudit) |  | 

 |
| [**markTicketAsSpam**](#_api_DEFAULT_method_markTicketAsSpam) |  | 

 |
| [**mergeUsers**](#_api_DEFAULT_method_mergeUsers) |  | 

 |
| [**notifyApp**](#_api_DEFAULT_method_notifyApp) |  | 

 |
| [**permanentlyDeleteTicket**](#_api_DEFAULT_method_permanentlyDeleteTicket) |  | 

 |
| [**permanentlyDeleteTickets**](#_api_DEFAULT_method_permanentlyDeleteTickets) |  | 

 |
| [**permanentlyDeleteUser**](#_api_DEFAULT_method_permanentlyDeleteUser) |  | 

 |
| [**queueCreateTicketAsync**](#_api_DEFAULT_method_queueCreateTicketAsync) |  | 

 |
| [**removeTagFromOrganisations**](#_api_DEFAULT_method_removeTagFromOrganisations) |  | 

 |
| [**removeTagFromTicket**](#_api_DEFAULT_method_removeTagFromTicket) |  | 

 |
| [**removeTagFromTopics**](#_api_DEFAULT_method_removeTagFromTopics) |  | 

 |
| [**requestVerifyUserIdentity**](#_api_DEFAULT_method_requestVerifyUserIdentity) |  | 

 |
| [**resetUserPassword**](#_api_DEFAULT_method_resetUserPassword) |  | 

 |
| [**searchTriggers**](#_api_DEFAULT_method_searchTriggers) |  | 

 |
| [**setGroupMembershipAsDefault**](#_api_DEFAULT_method_setGroupMembershipAsDefault) |  | 

 |
| [**setOrganizationMembershipAsDefault**](#_api_DEFAULT_method_setOrganizationMembershipAsDefault) |  | 

 |
| [**setTagOnOrganisations**](#_api_DEFAULT_method_setTagOnOrganisations) |  | 

 |
| [**setTagOnTicket**](#_api_DEFAULT_method_setTagOnTicket) |  | 

 |
| [**setTagOnTopics**](#_api_DEFAULT_method_setTagOnTopics) |  | 

 |
| [**setUserPrimaryIdentity**](#_api_DEFAULT_method_setUserPrimaryIdentity) |  | 

 |
| [**showArticleTranslation**](#_api_DEFAULT_method_showArticleTranslation) |  | 

 |
| [**showCategoryTranslation**](#_api_DEFAULT_method_showCategoryTranslation) |  | 

 |
| [**showSectionTranslation**](#_api_DEFAULT_method_showSectionTranslation) |  | 

 |
| [**suspendUser**](#_api_DEFAULT_method_suspendUser) |  | 

 |
| [**trustTicketAudit**](#_api_DEFAULT_method_trustTicketAudit) |  | 

 |
| [**unassignOrganizationMembership**](#_api_DEFAULT_method_unassignOrganizationMembership) |  | 

 |
| [**unsuspendUser**](#_api_DEFAULT_method_unsuspendUser) |  | 

 |
| [**updateArticle**](#_api_DEFAULT_method_updateArticle) |  | 

 |
| [**updateArticleTranslation**](#_api_DEFAULT_method_updateArticleTranslation) |  | 

 |
| [**updateAutomation**](#_api_DEFAULT_method_updateAutomation) |  | 

 |
| [**updateCategory**](#_api_DEFAULT_method_updateCategory) |  | 

 |
| [**updateCategoryTranslation**](#_api_DEFAULT_method_updateCategoryTranslation) |  | 

 |
| [**updateContentTag**](#_api_DEFAULT_method_updateContentTag) |  | 

 |
| [**updateDynamicContentItem**](#_api_DEFAULT_method_updateDynamicContentItem) |  | 

 |
| [**updateDynamicContentItemVariant**](#_api_DEFAULT_method_updateDynamicContentItemVariant) |  | 

 |
| [**updateForum**](#_api_DEFAULT_method_updateForum) |  | 

 |
| [**updateGroup**](#_api_DEFAULT_method_updateGroup) |  | 

 |
| [**updateInstallation**](#_api_DEFAULT_method_updateInstallation) |  | 

 |
| [**updateMacro**](#_api_DEFAULT_method_updateMacro) |  | 

 |
| [**updateOrganization**](#_api_DEFAULT_method_updateOrganization) |  | 

 |
| [**updateOrganizations**](#_api_DEFAULT_method_updateOrganizations) |  | 

 |
| [**updateOrganizationsAsync**](#_api_DEFAULT_method_updateOrganizationsAsync) |  | 

 |
| [**updatePermissionGroup**](#_api_DEFAULT_method_updatePermissionGroup) |  | Update permission group |
| [**updateRequest**](#_api_DEFAULT_method_updateRequest) |  | 

 |
| [**updateSection**](#_api_DEFAULT_method_updateSection) |  | 

 |
| [**updateSectionTranslation**](#_api_DEFAULT_method_updateSectionTranslation) |  | 

 |
| [**updateTicket**](#_api_DEFAULT_method_updateTicket) |  | 

 |
| [**updateTicketField**](#_api_DEFAULT_method_updateTicketField) |  | 

 |
| [**updateTicketForm**](#_api_DEFAULT_method_updateTicketForm) |  | 

 |
| [**updateTickets**](#_api_DEFAULT_method_updateTickets) |  | 

 |
| [**updateTicketsAsync**](#_api_DEFAULT_method_updateTicketsAsync) |  | 

 |
| [**updateTopic**](#_api_DEFAULT_method_updateTopic) |  | 

 |
| [**updateTrigger**](#_api_DEFAULT_method_updateTrigger) |  | 

 |
| [**updateUser**](#_api_DEFAULT_method_updateUser) |  | 

 |
| [**updateUserIdentity**](#_api_DEFAULT_method_updateUserIdentity) |  | 

 |
| [**updateUserSegment**](#_api_DEFAULT_method_updateUserSegment) |  | Update User Segment |
| [**updateUsers**](#_api_DEFAULT_method_updateUsers) |  | 

 |
| [**updateUsersAsync**](#_api_DEFAULT_method_updateUsersAsync) |  | 

 |
| [**verifyUserIdentity**](#_api_DEFAULT_method_verifyUserIdentity) |  | 

 |

#### Method addTagToOrganisations

Signatures:

-   java.util.List<String> addTagToOrganisations(long id, String\[\] tags);
    

The zendesk/addTagToOrganisations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method addTagToTicket

Signatures:

-   java.util.List<String> addTagToTicket(long id, String\[\] tags);
    

The zendesk/addTagToTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method addTagToTopics

Signatures:

-   java.util.List<String> addTagToTopics(long id, String\[\] tags);
    

The zendesk/addTagToTopics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method associateAttachmentsToArticle

Signatures:

-   void associateAttachmentsToArticle(String idArticle, java.util.List<org.zendesk.client.v2.model.Attachment> attachments);
    

The zendesk/associateAttachmentsToArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **attachments** | 
 | List |
| **idArticle** | 

 | String |

#### Method changeUserPassword

Signatures:

-   void changeUserPassword(org.zendesk.client.v2.model.User user, String oldPassword, String newPassword);
    

The zendesk/changeUserPassword API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **newPassword** | 
 | String |
| **oldPassword** | 

 | String |
| **user** | 

 | User |

#### Method createArticle

Signatures:

-   org.zendesk.client.v2.model.hc.Article createArticle(org.zendesk.client.v2.model.hc.Article article);
    
-   org.zendesk.client.v2.model.hc.Article createArticle(org.zendesk.client.v2.model.hc.Article article, boolean notifySubscribers);
    

The zendesk/createArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **article** | 
 | Article |
| **notifySubscribers** | 

 | Boolean |

#### Method createArticleTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation createArticleTranslation(Long articleId, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/createArticleTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId** | 
 | Long |
| **translation** | 

 | Translation |

#### Method createAutomation

Signatures:

-   org.zendesk.client.v2.model.Automation createAutomation(org.zendesk.client.v2.model.Automation automation);
    

The zendesk/createAutomation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **automation** | 
 | Automation |

#### Method createCategory

Signatures:

-   org.zendesk.client.v2.model.hc.Category createCategory(org.zendesk.client.v2.model.hc.Category category);
    

The zendesk/createCategory API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category** | 
 | Category |

#### Method createCategoryTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation createCategoryTranslation(Long categoryId, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/createCategoryTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **categoryId** | 
 | Long |
| **translation** | 

 | Translation |

#### Method createComment

Signatures:

-   org.zendesk.client.v2.model.Ticket createComment(long ticketId, org.zendesk.client.v2.model.Comment comment);
    

The zendesk/createComment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **comment** | 
 | Comment |
| **ticketId** | 

 | Long |

#### Method createContentTag

Signatures:

-   org.zendesk.client.v2.model.hc.ContentTag createContentTag(org.zendesk.client.v2.model.hc.ContentTag contentTag);
    

The zendesk/createContentTag API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentTag** | 
 | ContentTag |

#### Method createDynamicContentItem

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItem createDynamicContentItem(org.zendesk.client.v2.model.dynamic.DynamicContentItem item);
    

The zendesk/createDynamicContentItem API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **item** | 
 | DynamicContentItem |

#### Method createDynamicContentItemVariant

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant createDynamicContentItemVariant(Long itemId, org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant variant);
    

The zendesk/createDynamicContentItemVariant API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **itemId** | 
 | Long |
| **variant** | 

 | DynamicContentItemVariant |

#### Method createForum

Signatures:

-   org.zendesk.client.v2.model.Forum createForum(org.zendesk.client.v2.model.Forum forum);
    

The zendesk/createForum API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **forum** | 
 | Forum |

#### Method createGroup

Signatures:

-   org.zendesk.client.v2.model.Group createGroup(org.zendesk.client.v2.model.Group group);
    

The zendesk/createGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group** | 
 | Group |

#### Method createGroupMembership

Signatures:

-   org.zendesk.client.v2.model.GroupMembership createGroupMembership(long user\_id, org.zendesk.client.v2.model.GroupMembership groupMembership);
    
-   org.zendesk.client.v2.model.GroupMembership createGroupMembership(org.zendesk.client.v2.model.GroupMembership groupMembership);
    

The zendesk/createGroupMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembership** | 
 | GroupMembership |
| **user\_id** | 

 | Long |

#### Method createMacro

Signatures:

-   org.zendesk.client.v2.model.Macro createMacro(org.zendesk.client.v2.model.Macro macro);
    

The zendesk/createMacro API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **macro** | 
 | Macro |

#### Method createOrUpdateOrganization

Signatures:

-   org.zendesk.client.v2.model.Organization createOrUpdateOrganization(org.zendesk.client.v2.model.Organization organization);
    

The zendesk/createOrUpdateOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization** | 
 | Organization |

#### Method createOrUpdateUser

Signatures:

-   org.zendesk.client.v2.model.User createOrUpdateUser(org.zendesk.client.v2.model.User user);
    

The zendesk/createOrUpdateUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user** | 
 | User |

#### Method createOrUpdateUsers

Signatures:

-   org.zendesk.client.v2.model.JobStatus createOrUpdateUsers(java.util.List<org.zendesk.client.v2.model.User> users);
    
-   org.zendesk.client.v2.model.JobStatus createOrUpdateUsers(org.zendesk.client.v2.model.User\[\] users);
    

The zendesk/createOrUpdateUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **users** | 
 | User\[\] |
| **usersList** | 

 | List |

#### Method createOrUpdateUsersAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> createOrUpdateUsersAsync(java.util.List<org.zendesk.client.v2.model.User> users);
    

The zendesk/createOrUpdateUsersAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **usersList** | 
 | List |

#### Method createOrganization

Signatures:

-   org.zendesk.client.v2.model.Organization createOrganization(org.zendesk.client.v2.model.Organization organization);
    

The zendesk/createOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization** | 
 | Organization |

#### Method createOrganizationMembership

Signatures:

-   org.zendesk.client.v2.model.OrganizationMembership createOrganizationMembership(long user\_id, org.zendesk.client.v2.model.OrganizationMembership organizationMembership);
    
-   org.zendesk.client.v2.model.OrganizationMembership createOrganizationMembership(org.zendesk.client.v2.model.OrganizationMembership organizationMembership);
    

The zendesk/createOrganizationMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationMembership** | 
 | OrganizationMembership |
| **user\_id** | 

 | Long |

#### Method createOrganizationMemberships

Signatures:

-   org.zendesk.client.v2.model.JobStatus createOrganizationMemberships(java.util.List<org.zendesk.client.v2.model.OrganizationMembership> organizationMemberships);
    
-   org.zendesk.client.v2.model.JobStatus createOrganizationMemberships(org.zendesk.client.v2.model.OrganizationMembership\[\] organizationMemberships);
    

The zendesk/createOrganizationMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationMembershipList** | 
 | List |
| **organizationMemberships** | 

 | OrganizationMembership\[\] |

#### Method createOrganizationMembershipsAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> createOrganizationMembershipsAsync(java.util.List<org.zendesk.client.v2.model.OrganizationMembership> organizationMemberships);
    

The zendesk/createOrganizationMembershipsAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationMembershipList** | 
 | List |

#### Method createOrganizations

Signatures:

-   org.zendesk.client.v2.model.JobStatus createOrganizations(java.util.List<org.zendesk.client.v2.model.Organization> organizations);
    
-   org.zendesk.client.v2.model.JobStatus createOrganizations(org.zendesk.client.v2.model.Organization\[\] organizations);
    

The zendesk/createOrganizations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationList** | 
 | List |
| **organizations** | 

 | Organization\[\] |

#### Method createOrganizationsAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> createOrganizationsAsync(java.util.List<org.zendesk.client.v2.model.Organization> organizations);
    

The zendesk/createOrganizationsAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationList** | 
 | List |

#### Method createPermissionGroup

Signatures:

-   org.zendesk.client.v2.model.hc.PermissionGroup createPermissionGroup(org.zendesk.client.v2.model.hc.PermissionGroup permissionGroup);
    

The zendesk/createPermissionGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **permissionGroup** | 
 | PermissionGroup |

#### Method createRequest

Signatures:

-   org.zendesk.client.v2.model.Request createRequest(org.zendesk.client.v2.model.Request request);
    

The zendesk/createRequest API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | Request |

#### Method createSatisfactionRating

Signatures:

-   org.zendesk.client.v2.model.SatisfactionRating createSatisfactionRating(long ticketId, org.zendesk.client.v2.model.SatisfactionRating satisfactionRating);
    
-   org.zendesk.client.v2.model.SatisfactionRating createSatisfactionRating(org.zendesk.client.v2.model.Ticket ticket, org.zendesk.client.v2.model.SatisfactionRating satisfactionRating);
    

The zendesk/createSatisfactionRating API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **satisfactionRating** | 
 | SatisfactionRating |
| **ticket** | 

 | Ticket |
| **ticketId** | 

 | Long |

#### Method createSection

Signatures:

-   org.zendesk.client.v2.model.hc.Section createSection(org.zendesk.client.v2.model.hc.Section section);
    

The zendesk/createSection API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **section** | 
 | Section |

#### Method createSectionTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation createSectionTranslation(Long sectionId, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/createSectionTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **sectionId** | 
 | Long |
| **translation** | 

 | Translation |

#### Method createTarget

Signatures:

-   org.zendesk.client.v2.model.targets.Target createTarget(org.zendesk.client.v2.model.targets.Target target);
    

The zendesk/createTarget API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **target** | 
 | Target |

#### Method createTicket

Signatures:

-   org.zendesk.client.v2.model.Ticket createTicket(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/createTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticket** | 
 | Ticket |

#### Method createTicketAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.Ticket> createTicketAsync(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/createTicketAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticket** | 
 | Ticket |

#### Method createTicketField

Signatures:

-   org.zendesk.client.v2.model.Field createTicketField(org.zendesk.client.v2.model.Field field);
    

The zendesk/createTicketField API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **field** | 
 | Field |

#### Method createTicketForm

Signatures:

-   org.zendesk.client.v2.model.TicketForm createTicketForm(org.zendesk.client.v2.model.TicketForm ticketForm);
    

The zendesk/createTicketForm API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketForm** | 
 | TicketForm |

#### Method createTicketFromTweet

Signatures:

-   org.zendesk.client.v2.model.Ticket createTicketFromTweet(long tweetId, long monitorId);
    

The zendesk/createTicketFromTweet API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **monitorId** | 
 | Long |
| **tweetId** | 

 | Long |

#### Method createTickets

Signatures:

-   org.zendesk.client.v2.model.JobStatus createTickets(java.util.List<org.zendesk.client.v2.model.Ticket> tickets);
    
-   org.zendesk.client.v2.model.JobStatus createTickets(org.zendesk.client.v2.model.Ticket\[\] tickets);
    

The zendesk/createTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketList** | 
 | List |
| **tickets** | 

 | Ticket\[\] |

#### Method createTicketsAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> createTicketsAsync(java.util.List<org.zendesk.client.v2.model.Ticket> tickets);
    

The zendesk/createTicketsAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketList** | 
 | List |

#### Method createTopic

Signatures:

-   org.zendesk.client.v2.model.Topic createTopic(org.zendesk.client.v2.model.Topic topic);
    

The zendesk/createTopic API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **topic** | 
 | Topic |

#### Method createTrigger

Signatures:

-   org.zendesk.client.v2.model.Trigger createTrigger(org.zendesk.client.v2.model.Trigger trigger);
    

The zendesk/createTrigger API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **trigger** | 
 | Trigger |

#### Method createUpload

Signatures:

-   org.zendesk.client.v2.model.Attachment.Upload createUpload(String fileName, String contentType, byte\[\] content);
    
-   org.zendesk.client.v2.model.Attachment.Upload createUpload(String fileName, byte\[\] content);
    
-   org.zendesk.client.v2.model.Attachment.Upload createUpload(String token, String fileName, String contentType, byte\[\] content);
    

The zendesk/createUpload API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | 
 | byte\[\] |
| **contentType** | 

 | String |
| **fileName** | 

 | String |
| **token** | 

 | String |

#### Method createUploadArticle

Signatures:

-   org.zendesk.client.v2.model.hc.ArticleAttachments createUploadArticle(long articleId, java.io.File file);
    
-   org.zendesk.client.v2.model.hc.ArticleAttachments createUploadArticle(long articleId, java.io.File file, boolean inline);
    

The zendesk/createUploadArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId0** | 
 | Long |
| **file** | 

 | File |
| **inline** | 

 | Boolean |

#### Method createUser

Signatures:

-   org.zendesk.client.v2.model.User createUser(org.zendesk.client.v2.model.User user);
    

The zendesk/createUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user** | 
 | User |

#### Method createUserIdentity

Signatures:

-   org.zendesk.client.v2.model.Identity createUserIdentity(long userId, org.zendesk.client.v2.model.Identity identity);
    
-   org.zendesk.client.v2.model.Identity createUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/createUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method createUserSegment

Signatures:

-   org.zendesk.client.v2.model.hc.UserSegment createUserSegment(org.zendesk.client.v2.model.hc.UserSegment userSegment);
    

The zendesk/createUserSegment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userSegment** | 
 | UserSegment |

#### Method createUsers

Signatures:

-   org.zendesk.client.v2.model.JobStatus createUsers(java.util.List<org.zendesk.client.v2.model.User> users);
    
-   org.zendesk.client.v2.model.JobStatus createUsers(org.zendesk.client.v2.model.User\[\] users);
    

The zendesk/createUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userList** | 
 | List |
| **users** | 

 | User\[\] |

#### Method createUsersAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> createUsersAsync(java.util.List<org.zendesk.client.v2.model.User> users);
    

The zendesk/createUsersAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userList** | 
 | List |

#### Method deleteArticle

Signatures:

-   void deleteArticle(org.zendesk.client.v2.model.hc.Article article);
    

The zendesk/deleteArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **article** | 
 | Article |

#### Method deleteArticleAttachment

Signatures:

-   void deleteArticleAttachment(long id);
    
-   void deleteArticleAttachment(org.zendesk.client.v2.model.hc.ArticleAttachments attachment);
    

The zendesk/deleteArticleAttachment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleAttachments** | 
 | ArticleAttachments |
| **id** | Attachment identifier | Long |

#### Method deleteAttachment

Signatures:

-   void deleteAttachment(long id);
    
-   void deleteAttachment(org.zendesk.client.v2.model.Attachment attachment);
    

The zendesk/deleteAttachment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **attachment** | 
 | Attachment |
| **id** | 

 | Long |

#### Method deleteAutomation

Signatures:

-   void deleteAutomation(long automationId);
    

The zendesk/deleteAutomation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **automationId0** | 
 | Long |

#### Method deleteCategory

Signatures:

-   void deleteCategory(org.zendesk.client.v2.model.hc.Category category);
    

The zendesk/deleteCategory API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category** | 
 | Category |

#### Method deleteContentTag

Signatures:

-   void deleteContentTag(org.zendesk.client.v2.model.hc.ContentTag contentTag);
    

The zendesk/deleteContentTag API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentTag** | 
 | ContentTag |

#### Method deleteDynamicContentItem

Signatures:

-   void deleteDynamicContentItem(org.zendesk.client.v2.model.dynamic.DynamicContentItem item);
    

The zendesk/deleteDynamicContentItem API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **item** | 
 | DynamicContentItem |

#### Method deleteDynamicContentItemVariant

Signatures:

-   void deleteDynamicContentItemVariant(Long itemId, org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant variant);
    

The zendesk/deleteDynamicContentItemVariant API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **itemId** | 
 | Long |
| **variant** | 

 | DynamicContentItemVariant |

#### Method deleteForum

Signatures:

-   void deleteForum(org.zendesk.client.v2.model.Forum forum);
    

The zendesk/deleteForum API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **forum** | 
 | Forum |

#### Method deleteGroup

Signatures:

-   void deleteGroup(long id);
    
-   void deleteGroup(org.zendesk.client.v2.model.Group group);
    

The zendesk/deleteGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group** | 
 | Group |
| **id** | 

 | Long |

#### Method deleteGroupMembership

Signatures:

-   void deleteGroupMembership(long id);
    
-   void deleteGroupMembership(long user\_id, long group\_membership\_id);
    
-   void deleteGroupMembership(long user\_id, org.zendesk.client.v2.model.GroupMembership groupMembership);
    
-   void deleteGroupMembership(org.zendesk.client.v2.model.GroupMembership groupMembership);
    

The zendesk/deleteGroupMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembership** | 
 | GroupMembership |
| **group\_membership\_id** | 

 | Long |
| **id** | 

 | Long |
| **user\_id** | 

 | Long |

#### Method deleteOrganization

Signatures:

-   void deleteOrganization(long id);
    
-   void deleteOrganization(org.zendesk.client.v2.model.Organization organization);
    

The zendesk/deleteOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **organization** | 

 | Organization |

#### Method deleteOrganizationMembership

Signatures:

-   void deleteOrganizationMembership(long id);
    
-   void deleteOrganizationMembership(long user\_id, long organization\_membership\_id);
    
-   void deleteOrganizationMembership(long user\_id, org.zendesk.client.v2.model.OrganizationMembership organizationMembership);
    

The zendesk/deleteOrganizationMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **organizationMembership** | 

 | OrganizationMembership |
| **organization\_membership\_id** | 

 | Long |
| **user\_id** | 

 | Long |

#### Method deleteOrganizationMemberships

Signatures:

-   void deleteOrganizationMemberships(long id, long\[\] ids);
    

The zendesk/deleteOrganizationMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method deleteOrganizations

Signatures:

-   org.zendesk.client.v2.model.JobStatus deleteOrganizations(long\[\] ids);
    

The zendesk/deleteOrganizations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ids** | 
 | long\[\] |

#### Method deletePermissionGroup

Signatures:

-   void deletePermissionGroup(long id);
    
-   void deletePermissionGroup(org.zendesk.client.v2.model.hc.PermissionGroup permissionGroup);
    

The zendesk/deletePermissionGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **permissionGroup** | 

 | PermissionGroup |

#### Method deleteSection

Signatures:

-   void deleteSection(org.zendesk.client.v2.model.hc.Section section);
    

The zendesk/deleteSection API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **section** | 
 | Section |

#### Method deleteSuspendedTicket

Signatures:

-   void deleteSuspendedTicket(long id);
    
-   void deleteSuspendedTicket(org.zendesk.client.v2.model.SuspendedTicket ticket);
    

The zendesk/deleteSuspendedTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **suspendedTicket** | 

 | SuspendedTicket |

#### Method deleteTarget

Signatures:

-   void deleteTarget(long targetId);
    

The zendesk/deleteTarget API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **targetId** | 
 | Long |

#### Method deleteTicket

Signatures:

-   void deleteTicket(long id);
    
-   void deleteTicket(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/deleteTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ticket** | 

 | Ticket |

#### Method deleteTicketField

Signatures:

-   void deleteTicketField(long id);
    
-   void deleteTicketField(org.zendesk.client.v2.model.Field field);
    

The zendesk/deleteTicketField API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **field** | 
 | Field |
| **id** | 

 | Long |

#### Method deleteTicketForm

Signatures:

-   void deleteTicketForm(long id);
    
-   void deleteTicketForm(org.zendesk.client.v2.model.TicketForm ticketForm);
    

The zendesk/deleteTicketForm API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ticketForm** | 

 | TicketForm |

#### Method deleteTickets

Signatures:

-   org.zendesk.client.v2.model.JobStatus deleteTickets(long id, long\[\] ids);
    

The zendesk/deleteTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method deleteTopic

Signatures:

-   void deleteTopic(org.zendesk.client.v2.model.Topic topic);
    

The zendesk/deleteTopic API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **topic** | 
 | Topic |

#### Method deleteTranslation

Signatures:

-   void deleteTranslation(Long translationId);
    
-   void deleteTranslation(org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/deleteTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **translation** | 
 | Translation |
| **translationId** | 

 | Long |

#### Method deleteTrigger

Signatures:

-   void deleteTrigger(long triggerId);
    

The zendesk/deleteTrigger API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **triggerId** | 
 | Long |

#### Method deleteUpload

Signatures:

-   void deleteUpload(String token);
    
-   void deleteUpload(org.zendesk.client.v2.model.Attachment.Upload upload);
    

The zendesk/deleteUpload API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **token** | 
 | String |
| **upload** | 

 | Upload |

#### Method deleteUser

Signatures:

-   void deleteUser(long id);
    
-   void deleteUser(org.zendesk.client.v2.model.User user);
    

The zendesk/deleteUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **user** | 

 | User |

#### Method deleteUserIdentity

Signatures:

-   void deleteUserIdentity(long userId, long identityId);
    
-   void deleteUserIdentity(org.zendesk.client.v2.model.User user, long identityId);
    
-   void deleteUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/deleteUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **identityId** | 

 | Long |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method deleteUserSegment

Signatures:

-   void deleteUserSegment(long id);
    
-   void deleteUserSegment(org.zendesk.client.v2.model.hc.UserSegment userSegment);
    

The zendesk/deleteUserSegment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **userSegment** | 

 | UserSegment |

#### Method deleteUsers

Signatures:

-   org.zendesk.client.v2.model.JobStatus deleteUsers(long\[\] ids);
    

The zendesk/deleteUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ids** | 
 | long\[\] |

#### Method executeView

Signatures:

-   java.util.Optional<org.zendesk.client.v2.model.views.ExecutedViewPage<V>> executeView(long id, Class<org.zendesk.client.v2.model.views.ViewRow> clazz);
    

The zendesk/executeView API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **clazz** | 
 | Class |
| **id** | 

 | Long |

#### Method getActiveTriggers

Signatures:

-   Iterable<org.zendesk.client.v2.model.Trigger> getActiveTriggers();
    

The zendesk/getActiveTriggers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getArticle

Signatures:

-   org.zendesk.client.v2.model.hc.Article getArticle(long id);
    

The zendesk/getArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getArticleFromSearch

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticleFromSearch(String searchTerm);
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticleFromSearch(String searchTerm, Long sectionId);
    

The zendesk/getArticleFromSearch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **searchTerm** | 
 | String |
| **sectionId** | 

 | Long |

#### Method getArticleSubscriptions

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getArticleSubscriptions(Long articleId);
    
-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getArticleSubscriptions(Long articleId, String locale);
    

The zendesk/getArticleSubscriptions API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId** | 
 | Long |
| **locale** | 

 | String |

#### Method getArticleTranslations

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Translation> getArticleTranslations(Long articleId);
    

The zendesk/getArticleTranslations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId** | 
 | Long |

#### Method getArticles

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles();
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles(String locale);
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles(org.zendesk.client.v2.model.hc.Category category);
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles(org.zendesk.client.v2.model.hc.Category category, String locale);
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles(org.zendesk.client.v2.model.hc.Section section);
    
-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticles(org.zendesk.client.v2.model.hc.Section section, String locale);
    

The zendesk/getArticles API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category** | 
 | Category |
| **locale** | 

 | String |
| **section** | 

 | Section |

#### Method getArticlesFromAllLabels

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticlesFromAllLabels(java.util.List<String> labels);
    

The zendesk/getArticlesFromAllLabels API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **labels** | 
 | List |

#### Method getArticlesFromAnyLabels

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticlesFromAnyLabels(java.util.List<String> labels);
    

The zendesk/getArticlesFromAnyLabels API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **labels** | 
 | List |

#### Method getArticlesFromPage

Signatures:

-   java.util.List<org.zendesk.client.v2.model.hc.Article> getArticlesFromPage(int page);
    

The zendesk/getArticlesFromPage API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **page** | 
 | Integer |

#### Method getArticlesIncrementally

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Article> getArticlesIncrementally(java.util.Date startTime);
    

The zendesk/getArticlesIncrementally API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **startTime** | 
 | Date |

#### Method getAssignableGroupMemberships

Signatures:

-   Iterable<org.zendesk.client.v2.model.GroupMembership> getAssignableGroupMemberships();
    
-   Iterable<org.zendesk.client.v2.model.GroupMembership> getAssignableGroupMemberships(long group\_id);
    

The zendesk/getAssignableGroupMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group\_id** | 
 | Long |

#### Method getAssignableGroups

Signatures:

-   Iterable<org.zendesk.client.v2.model.Group> getAssignableGroups();
    

The zendesk/getAssignableGroups API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getAssignedTicketsCountForUser

Signatures:

-   org.zendesk.client.v2.model.TicketCount getAssignedTicketsCountForUser(long id);
    

The zendesk/getAssignedTicketsCountForUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getAttachment

Signatures:

-   org.zendesk.client.v2.model.Attachment getAttachment(long id);
    
-   org.zendesk.client.v2.model.Attachment getAttachment(org.zendesk.client.v2.model.Attachment attachment);
    

The zendesk/getAttachment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **attachment** | 
 | Attachment |
| **id** | 

 | Long |

#### Method getAttachmentsFromArticle

Signatures:

-   java.util.List<org.zendesk.client.v2.model.hc.ArticleAttachments> getAttachmentsFromArticle(Long articleID);
    

The zendesk/getAttachmentsFromArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId** | 
 | Long |

#### Method getAuthenticatedUser

Signatures:

-   org.zendesk.client.v2.model.User getAuthenticatedUser();
    

The zendesk/getAuthenticatedUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getAutoCompleteOrganizations

Signatures:

-   Iterable<org.zendesk.client.v2.model.Organization> getAutoCompleteOrganizations(String name);
    

The zendesk/getAutoCompleteOrganizations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **name** | 
 | String |

#### Method getAutomation

Signatures:

-   org.zendesk.client.v2.model.Automation getAutomation(long id);
    

The zendesk/getAutomation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getAutomations

Signatures:

-   Iterable<org.zendesk.client.v2.model.Automation> getAutomations();
    

The zendesk/getAutomations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getBrands

Signatures:

-   Iterable<org.zendesk.client.v2.model.Brand> getBrands();
    

The zendesk/getBrands API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getCCRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getCCRequests();
    

The zendesk/getCCRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getCategories

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Category> getCategories();
    

The zendesk/getCategories API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getCategory

Signatures:

-   org.zendesk.client.v2.model.hc.Category getCategory(long id);
    

The zendesk/getCategory API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getCategoryTranslations

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Translation> getCategoryTranslations(Long categoryId);
    

The zendesk/getCategoryTranslations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **categoryId** | 
 | Long |

#### Method getCcdTicketsCountForUser

Signatures:

-   org.zendesk.client.v2.model.TicketCount getCcdTicketsCountForUser(long id);
    

The zendesk/getCcdTicketsCountForUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getComplianceDeletionStatuses

Signatures:

-   Iterable<org.zendesk.client.v2.model.ComplianceDeletionStatus> getComplianceDeletionStatuses(long userId);
    

The zendesk/getComplianceDeletionStatuses API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | 
 | Long |

#### Method getContentTag

Signatures:

-   org.zendesk.client.v2.model.hc.ContentTag getContentTag(String contentTagId);
    

The zendesk/getContentTag API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentTagId** | 
 | String |

#### Method getContentTags

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.ContentTag> getContentTags();
    
-   Iterable<org.zendesk.client.v2.model.hc.ContentTag> getContentTags(int pageSize);
    
-   Iterable<org.zendesk.client.v2.model.hc.ContentTag> getContentTags(int pageSize, String namePrefix);
    

The zendesk/getContentTags API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **namePrefix** | 
 | String |
| **pageSize** | 

 | Integer |

#### Method getCurrentUser

Signatures:

-   org.zendesk.client.v2.model.User getCurrentUser();
    

The zendesk/getCurrentUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getCustomAgentRoles

Signatures:

-   Iterable<org.zendesk.client.v2.model.AgentRole> getCustomAgentRoles();
    

The zendesk/getCustomAgentRoles API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getCustomTicketStatuses

Signatures:

-   Iterable<org.zendesk.client.v2.model.CustomTicketStatus> getCustomTicketStatuses();
    

The zendesk/getCustomTicketStatuses API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getDeletedTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.DeletedTicket> getDeletedTickets();
    
-   Iterable<org.zendesk.client.v2.model.DeletedTicket> getDeletedTickets(String sortBy, org.zendesk.client.v2.model.SortOrder sortOrder);
    

The zendesk/getDeletedTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **sortBy** | 
 | String |
| **sortOrder** | 

 | SortOrder |

#### Method getDynamicContentItem

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItem getDynamicContentItem(long id);
    

The zendesk/getDynamicContentItem API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getDynamicContentItemVariant

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant getDynamicContentItemVariant(Long itemId, long id);
    

The zendesk/getDynamicContentItemVariant API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **itemId** | 

 | Long |

#### Method getDynamicContentItemVariants

Signatures:

-   Iterable<org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant> getDynamicContentItemVariants(org.zendesk.client.v2.model.dynamic.DynamicContentItem item);
    

The zendesk/getDynamicContentItemVariants API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **item** | 
 | DynamicContentItem |

#### Method getDynamicContentItems

Signatures:

-   Iterable<org.zendesk.client.v2.model.dynamic.DynamicContentItem> getDynamicContentItems();
    

The zendesk/getDynamicContentItems API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getForum

Signatures:

-   org.zendesk.client.v2.model.Forum getForum(long id);
    

The zendesk/getForum API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getForums

Signatures:

-   Iterable<org.zendesk.client.v2.model.Forum> getForums();
    
-   java.util.List<org.zendesk.client.v2.model.Forum> getForums(long category\_id);
    

The zendesk/getForums API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category\_id** | 
 | Long |

#### Method getGroup

Signatures:

-   org.zendesk.client.v2.model.Group getGroup(long id);
    

The zendesk/getGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getGroupMembership

Signatures:

-   org.zendesk.client.v2.model.GroupMembership getGroupMembership(long id);
    
-   org.zendesk.client.v2.model.GroupMembership getGroupMembership(long user\_id, long group\_membership\_id);
    

The zendesk/getGroupMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group\_membership\_id** | 
 | Long |
| **id** | 

 | Long |
| **user\_id** | 

 | Long |

#### Method getGroupMembershipByUser

Signatures:

-   Iterable<org.zendesk.client.v2.model.GroupMembership> getGroupMembershipByUser(long user\_id);
    

The zendesk/getGroupMembershipByUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user\_id** | 
 | Long |

#### Method getGroupMemberships

Signatures:

-   Iterable<org.zendesk.client.v2.model.GroupMembership> getGroupMemberships();
    
-   Iterable<org.zendesk.client.v2.model.GroupMembership> getGroupMemberships(long group\_id);
    

The zendesk/getGroupMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group\_id** | 
 | Long |

#### Method getGroupOrganization

Signatures:

-   org.zendesk.client.v2.model.OrganizationMembership getGroupOrganization(long user\_id, long organization\_membership\_id);
    

The zendesk/getGroupOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization\_membership\_id** | 
 | Long |
| **user\_id** | 

 | Long |

#### Method getGroupUsers

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> getGroupUsers(long id);
    

The zendesk/getGroupUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getGroups

Signatures:

-   Iterable<org.zendesk.client.v2.model.Group> getGroups();
    

The zendesk/getGroups API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getHelpCenterLocales

Signatures:

-   java.util.List<String> getHelpCenterLocales();
    

The zendesk/getHelpCenterLocales API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getHolidaysForSchedule

Signatures:

-   Iterable<org.zendesk.client.v2.model.schedules.Holiday> getHolidaysForSchedule(Long scheduleId);
    
-   Iterable<org.zendesk.client.v2.model.schedules.Holiday> getHolidaysForSchedule(org.zendesk.client.v2.model.schedules.Schedule schedule);
    

The zendesk/getHolidaysForSchedule API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **schedule** | 
 | Schedule |
| **scheduleId** | 

 | Long |

#### Method getIncrementalTicketsResult

Signatures:

-   java.util.Map getIncrementalTicketsResult(long unixEpochTime);
    

The zendesk/getIncrementalTicketsResult API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **unixEpochTime** | 
 | Long |

#### Method getJiraLinks

Signatures:

-   Iterable<org.zendesk.client.v2.model.JiraLink> getJiraLinks();
    

The zendesk/getJiraLinks API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getJobStatus

Signatures:

-   org.zendesk.client.v2.model.JobStatus getJobStatus(org.zendesk.client.v2.model.JobStatus status);
    

The zendesk/getJobStatus API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **status** | 
 | JobStatus |

#### Method getJobStatusAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> getJobStatusAsync(org.zendesk.client.v2.model.JobStatus status);
    

The zendesk/getJobStatusAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **status** | 
 | JobStatus |

#### Method getJobStatuses

Signatures:

-   java.util.List<org.zendesk.client.v2.model.JobStatus> getJobStatuses(java.util.List<org.zendesk.client.v2.model.JobStatus> statuses);
    

The zendesk/getJobStatuses API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **statuses** | 
 | List |

#### Method getJobStatusesAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<java.util.List<org.zendesk.client.v2.model.JobStatus>> getJobStatusesAsync(java.util.List<org.zendesk.client.v2.model.JobStatus> statuses);
    

The zendesk/getJobStatusesAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **statuses** | 
 | List |

#### Method getLocales

Signatures:

-   Iterable<org.zendesk.client.v2.model.Locale> getLocales();
    

The zendesk/getLocales API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getMacro

Signatures:

-   org.zendesk.client.v2.model.Macro getMacro(long macroId);
    

The zendesk/getMacro API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **macroId** | 
 | Long |

#### Method getMacros

Signatures:

-   Iterable<org.zendesk.client.v2.model.Macro> getMacros();
    

The zendesk/getMacros API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getOpenRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getOpenRequests();
    

The zendesk/getOpenRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getOrganization

Signatures:

-   org.zendesk.client.v2.model.Organization getOrganization(long id);
    

The zendesk/getOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getOrganizationFields

Signatures:

-   Iterable<org.zendesk.client.v2.model.OrganizationField> getOrganizationFields();
    

The zendesk/getOrganizationFields API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getOrganizationMembership

Signatures:

-   org.zendesk.client.v2.model.OrganizationMembership getOrganizationMembership(long id);
    

The zendesk/getOrganizationMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getOrganizationMembershipByUser

Signatures:

-   Iterable<org.zendesk.client.v2.model.OrganizationMembership> getOrganizationMembershipByUser(long user\_id);
    

The zendesk/getOrganizationMembershipByUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user\_id** | 
 | Long |

#### Method getOrganizationMembershipForUser

Signatures:

-   org.zendesk.client.v2.model.OrganizationMembership getOrganizationMembershipForUser(long user\_id, long id);
    

The zendesk/getOrganizationMembershipForUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **user\_id** | 

 | Long |

#### Method getOrganizationMemberships

Signatures:

-   Iterable<org.zendesk.client.v2.model.OrganizationMembership> getOrganizationMemberships();
    

The zendesk/getOrganizationMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getOrganizationMembershipsForOrg

Signatures:

-   Iterable<org.zendesk.client.v2.model.OrganizationMembership> getOrganizationMembershipsForOrg(long organization\_id);
    

The zendesk/getOrganizationMembershipsForOrg API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization\_id** | 
 | Long |

#### Method getOrganizationMembershipsForUser

Signatures:

-   Iterable<org.zendesk.client.v2.model.OrganizationMembership> getOrganizationMembershipsForUser(long user\_id);
    

The zendesk/getOrganizationMembershipsForUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user\_id** | 
 | Long |

#### Method getOrganizationRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getOrganizationRequests(long organizationId);
    

The zendesk/getOrganizationRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationId** | 
 | Long |

#### Method getOrganizationTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getOrganizationTickets(long organizationId);
    

The zendesk/getOrganizationTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationId** | 
 | Long |

#### Method getOrganizationUsers

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> getOrganizationUsers(long id);
    

The zendesk/getOrganizationUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getOrganizations

Signatures:

-   Iterable<org.zendesk.client.v2.model.Organization> getOrganizations();
    
-   java.util.List<org.zendesk.client.v2.model.Organization> getOrganizations(long id, long\[\] ids);
    

The zendesk/getOrganizations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method getOrganizationsIncrementally

Signatures:

-   Iterable<org.zendesk.client.v2.model.Organization> getOrganizationsIncrementally(java.util.Date startTime);
    

The zendesk/getOrganizationsIncrementally API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **startTime** | 
 | Date |

#### Method getPermissionGroup

Signatures:

-   org.zendesk.client.v2.model.hc.PermissionGroup getPermissionGroup(long id);
    

The zendesk/getPermissionGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getPermissionGroups

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.PermissionGroup> getPermissionGroups();
    

The zendesk/getPermissionGroups API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getRecentTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getRecentTickets();
    

The zendesk/getRecentTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getRequest

Signatures:

-   org.zendesk.client.v2.model.Request getRequest(long id);
    

The zendesk/getRequest API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getRequestComment

Signatures:

-   org.zendesk.client.v2.model.Comment getRequestComment(long requestId, long commentId);
    
-   org.zendesk.client.v2.model.Comment getRequestComment(org.zendesk.client.v2.model.Request request, long commentId);
    
-   org.zendesk.client.v2.model.Comment getRequestComment(org.zendesk.client.v2.model.Request request, org.zendesk.client.v2.model.Comment comment);
    

The zendesk/getRequestComment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **comment** | 
 | Comment |
| **commentId** | 

 | Long |
| **request** | 

 | Request |
| **requestId** | 

 | Long |

#### Method getRequestComments

Signatures:

-   Iterable<org.zendesk.client.v2.model.Comment> getRequestComments(long id);
    
-   Iterable<org.zendesk.client.v2.model.Comment> getRequestComments(org.zendesk.client.v2.model.Request request);
    

The zendesk/getRequestComments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **request** | 

 | Request |

#### Method getRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getRequests();
    

The zendesk/getRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getSatisfactionRating

Signatures:

-   org.zendesk.client.v2.model.SatisfactionRating getSatisfactionRating(long id);
    

The zendesk/getSatisfactionRating API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getSatisfactionRatings

Signatures:

-   Iterable<org.zendesk.client.v2.model.SatisfactionRating> getSatisfactionRatings();
    

The zendesk/getSatisfactionRatings API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getSchedule

Signatures:

-   org.zendesk.client.v2.model.schedules.Schedule getSchedule(Long scheduleId);
    
-   org.zendesk.client.v2.model.schedules.Schedule getSchedule(org.zendesk.client.v2.model.schedules.Schedule schedule);
    

The zendesk/getSchedule API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **schedule** | 
 | Schedule |
| **scheduleId** | 

 | Long |

#### Method getSchedules

Signatures:

-   Iterable<org.zendesk.client.v2.model.schedules.Schedule> getSchedules();
    

The zendesk/getSchedules API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getSearchTicketResults

Signatures:

-   java.util.Optional<org.zendesk.client.v2.model.TicketPage> getSearchTicketResults(String query, java.util.Map<String, Object> queryParams, String sortBy, org.zendesk.client.v2.model.SortOrder sortOrder);
    

The zendesk/getSearchTicketResults API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **query** | String used filter a type given by searchType | String |
| **queryParams** | Additional parameters other than filter string like per\_page, page etc | Map |
| **sortBy** | Name of any field of the searchType | String |
| **sortOrder** | Sort order | SortOrder |

#### Method getSection

Signatures:

-   org.zendesk.client.v2.model.hc.Section getSection(long id);
    

The zendesk/getSection API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getSectionSubscriptions

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getSectionSubscriptions(Long sectionId);
    
-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getSectionSubscriptions(Long sectionId, String locale);
    

The zendesk/getSectionSubscriptions API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **locale** | 
 | String |
| **sectionId** | 

 | Long |

#### Method getSectionTranslations

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Translation> getSectionTranslations(Long sectionId);
    

The zendesk/getSectionTranslations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **sectionId** | 
 | Long |

#### Method getSections

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Section> getSections();
    
-   Iterable<org.zendesk.client.v2.model.hc.Section> getSections(org.zendesk.client.v2.model.hc.Category category);
    
-   Iterable<org.zendesk.client.v2.model.hc.Section> getSections(org.zendesk.client.v2.model.hc.UserSegment userSegment);
    

The zendesk/getSections API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category** | 
 | Category |
| **userSegment** | 

 | UserSegment |

#### Method getSolvedRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getSolvedRequests();
    

The zendesk/getSolvedRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getSuspendedTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.SuspendedTicket> getSuspendedTickets();
    

The zendesk/getSuspendedTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTarget

Signatures:

-   org.zendesk.client.v2.model.targets.Target getTarget(long id);
    

The zendesk/getTarget API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTargets

Signatures:

-   Iterable<org.zendesk.client.v2.model.targets.Target> getTargets();
    

The zendesk/getTargets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTicket

Signatures:

-   org.zendesk.client.v2.model.Ticket getTicket(long id);
    

The zendesk/getTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketAudit

Signatures:

-   org.zendesk.client.v2.model.Audit getTicketAudit(long ticketId, long auditId);
    
-   org.zendesk.client.v2.model.Audit getTicketAudit(org.zendesk.client.v2.model.Ticket ticket, long id);
    
-   org.zendesk.client.v2.model.Audit getTicketAudit(org.zendesk.client.v2.model.Ticket ticket, org.zendesk.client.v2.model.Audit audit);
    

The zendesk/getTicketAudit API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **audit** | 
 | Audit |
| **auditId** | 

 | Long |
| **id** | 

 | Long |
| **ticket** | 

 | Ticket |
| **ticketId** | 

 | Long |

#### Method getTicketAudits

Signatures:

-   Iterable<org.zendesk.client.v2.model.Audit> getTicketAudits(Long id);
    
-   Iterable<org.zendesk.client.v2.model.Audit> getTicketAudits(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/getTicketAudits API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticket** | 
 | Ticket |
| **ticketId0** | 

 | Long |

#### Method getTicketCollaborators

Signatures:

-   java.util.List<org.zendesk.client.v2.model.User> getTicketCollaborators(long id);
    

The zendesk/getTicketCollaborators API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketComments

Signatures:

-   Iterable<org.zendesk.client.v2.model.Comment> getTicketComments(long id);
    
-   Iterable<org.zendesk.client.v2.model.Comment> getTicketComments(long id, org.zendesk.client.v2.model.SortOrder order);
    

The zendesk/getTicketComments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **order** | 

 | SortOrder |

#### Method getTicketField

Signatures:

-   org.zendesk.client.v2.model.Field getTicketField(long id);
    

The zendesk/getTicketField API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketFields

Signatures:

-   Iterable<org.zendesk.client.v2.model.Field> getTicketFields();
    

The zendesk/getTicketFields API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTicketForm

Signatures:

-   org.zendesk.client.v2.model.TicketForm getTicketForm(long id);
    

The zendesk/getTicketForm API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketForms

Signatures:

-   java.util.List<org.zendesk.client.v2.model.TicketForm> getTicketForms();
    

The zendesk/getTicketForms API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTicketIncidents

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketIncidents(long id);
    

The zendesk/getTicketIncidents API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketMetric

Signatures:

-   org.zendesk.client.v2.model.Metric getTicketMetric(long id);
    

The zendesk/getTicketMetric API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketMetricByTicket

Signatures:

-   org.zendesk.client.v2.model.Metric getTicketMetricByTicket(long id);
    

The zendesk/getTicketMetricByTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketMetrics

Signatures:

-   Iterable<org.zendesk.client.v2.model.Metric> getTicketMetrics();
    

The zendesk/getTicketMetrics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getTickets();
    
-   java.util.List<org.zendesk.client.v2.model.Ticket> getTickets(long id, long\[\] ids);
    

The zendesk/getTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method getTicketsByExternalId

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketsByExternalId(String externalId);
    
-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketsByExternalId(String externalId, boolean includeArchived);
    

The zendesk/getTicketsByExternalId API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **externalId** | 
 | String |
| **includeArchived** | 

 | Boolean |

#### Method getTicketsCount

Signatures:

-   org.zendesk.client.v2.model.TicketCount getTicketsCount();
    

The zendesk/getTicketsCount API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTicketsCountForOrganization

Signatures:

-   org.zendesk.client.v2.model.TicketCount getTicketsCountForOrganization(long id);
    

The zendesk/getTicketsCountForOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTicketsFromSearch

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketsFromSearch(String searchTerm);
    

The zendesk/getTicketsFromSearch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **searchTerm** | 
 | String |

#### Method getTicketsIncrementally

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketsIncrementally(java.util.Date startTime);
    
-   Iterable<org.zendesk.client.v2.model.Ticket> getTicketsIncrementally(java.util.Date startTime, java.util.Date endTime);
    

The zendesk/getTicketsIncrementally API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **endTime** | 
 | Date |
| **startTime** | 

 | Date |

#### Method getTimeZones

Signatures:

-   java.util.List<org.zendesk.client.v2.model.TimeZone> getTimeZones();
    

The zendesk/getTimeZones API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getTopic

Signatures:

-   org.zendesk.client.v2.model.Topic getTopic(long id);
    

The zendesk/getTopic API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTopics

Signatures:

-   Iterable<org.zendesk.client.v2.model.Topic> getTopics();
    
-   Iterable<org.zendesk.client.v2.model.Topic> getTopics(org.zendesk.client.v2.model.hc.UserSegment userSegment);
    
-   java.util.List<org.zendesk.client.v2.model.Topic> getTopics(long forum\_id);
    
-   java.util.List<org.zendesk.client.v2.model.Topic> getTopics(long id, long\[\] ids);
    

The zendesk/getTopics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **forum\_id** | 
 | Long |
| **id** | 

 | Long |
| **ids** | 

 | long\[\] |
| **userSegment** | 

 | UserSegment |

#### Method getTopicsByUser

Signatures:

-   java.util.List<org.zendesk.client.v2.model.Topic> getTopicsByUser(long user\_id);
    

The zendesk/getTopicsByUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user\_id** | 
 | Long |

#### Method getTrigger

Signatures:

-   org.zendesk.client.v2.model.Trigger getTrigger(long id);
    

The zendesk/getTrigger API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getTriggers

Signatures:

-   Iterable<org.zendesk.client.v2.model.Trigger> getTriggers();
    
-   Iterable<org.zendesk.client.v2.model.Trigger> getTriggers(String categoryId, boolean active, String sortBy, org.zendesk.client.v2.model.SortOrder sortOrder);
    

The zendesk/getTriggers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **active** | 
 | Boolean |
| **categoryId0** | 

 | String |
| **sortBy** | 

 | String |
| **sortOrder** | 

 | SortOrder |

#### Method getTwitterMonitors

Signatures:

-   Iterable<org.zendesk.client.v2.model.TwitterMonitor> getTwitterMonitors();
    

The zendesk/getTwitterMonitors API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getUser

Signatures:

-   org.zendesk.client.v2.model.User getUser(long id);
    

The zendesk/getUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getUserCCDTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getUserCCDTickets(long userId);
    

The zendesk/getUserCCDTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | 
 | Long |

#### Method getUserFields

Signatures:

-   Iterable<org.zendesk.client.v2.model.UserField> getUserFields();
    

The zendesk/getUserFields API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getUserIdentities

Signatures:

-   java.util.List<org.zendesk.client.v2.model.Identity> getUserIdentities(long userId);
    
-   java.util.List<org.zendesk.client.v2.model.Identity> getUserIdentities(org.zendesk.client.v2.model.User user);
    

The zendesk/getUserIdentities API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user** | 
 | User |
| **userId** | 

 | Long |

#### Method getUserIdentity

Signatures:

-   org.zendesk.client.v2.model.Identity getUserIdentity(long userId, long identityId);
    
-   org.zendesk.client.v2.model.Identity getUserIdentity(org.zendesk.client.v2.model.User user, long identityId);
    
-   org.zendesk.client.v2.model.Identity getUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/getUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **identityId** | 

 | Long |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method getUserRelatedInfo

Signatures:

-   org.zendesk.client.v2.model.UserRelatedInfo getUserRelatedInfo(long userId);
    

The zendesk/getUserRelatedInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | 
 | Long |

#### Method getUserRequestedTickets

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getUserRequestedTickets(long userId);
    

The zendesk/getUserRequestedTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | 
 | Long |

#### Method getUserRequests

Signatures:

-   Iterable<org.zendesk.client.v2.model.Request> getUserRequests(long id);
    
-   Iterable<org.zendesk.client.v2.model.Request> getUserRequests(org.zendesk.client.v2.model.User user);
    

The zendesk/getUserRequests API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **user** | 

 | User |

#### Method getUserSegment

Signatures:

-   org.zendesk.client.v2.model.hc.UserSegment getUserSegment(long id);
    

The zendesk/getUserSegment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getUserSegments

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.UserSegment> getUserSegments();
    
-   Iterable<org.zendesk.client.v2.model.hc.UserSegment> getUserSegments(long id);
    

The zendesk/getUserSegments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getUserSegmentsApplicable

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.UserSegment> getUserSegmentsApplicable();
    

The zendesk/getUserSegmentsApplicable API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getUserSubscriptions

Signatures:

-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getUserSubscriptions(Long userId);
    
-   Iterable<org.zendesk.client.v2.model.hc.Subscription> getUserSubscriptions(org.zendesk.client.v2.model.User user);
    

The zendesk/getUserSubscriptions API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user** | 
 | User |
| **userId0** | 

 | Long |

#### Method getUsers

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> getUsers();
    
-   java.util.List<org.zendesk.client.v2.model.User> getUsers(long id, long\[\] ids);
    

The zendesk/getUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method getUsersByExternalIds

Signatures:

-   java.util.List<org.zendesk.client.v2.model.User> getUsersByExternalIds(String externalId, String\[\] externalIds);
    
-   java.util.List<org.zendesk.client.v2.model.User> getUsersByExternalIds(long externalId, long\[\] externalIds);
    

The zendesk/getUsersByExternalIds API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **externalId** | 
 | String |
| **externalId0** | 

 | Long |
| **externalId0s** | 

 | long\[\] |
| **externalIds** | 

 | String\[\] |

#### Method getUsersByRole

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> getUsersByRole(String role, String\[\] roles);
    

The zendesk/getUsersByRole API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **role** | 
 | String |
| **roles** | 

 | String\[\] |

#### Method getUsersIncrementally

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> getUsersIncrementally(java.util.Date startTime);
    

The zendesk/getUsersIncrementally API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **startTime** | 
 | Date |

#### Method getView

Signatures:

-   Iterable<org.zendesk.client.v2.model.Ticket> getView(long id);
    

The zendesk/getView API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method getViews

Signatures:

-   Iterable<org.zendesk.client.v2.model.View> getViews();
    

The zendesk/getViews API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method importTicket

Signatures:

-   org.zendesk.client.v2.model.Ticket importTicket(org.zendesk.client.v2.model.TicketImport ticketImport);
    

The zendesk/importTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketImport** | 
 | TicketImport |

#### Method importTopic

Signatures:

-   org.zendesk.client.v2.model.Topic importTopic(org.zendesk.client.v2.model.Topic topic);
    

The zendesk/importTopic API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **topic** | 
 | Topic |

#### Method listHelpCenterLocales

Signatures:

-   org.zendesk.client.v2.model.hc.Locales listHelpCenterLocales();
    

The zendesk/listHelpCenterLocales API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method lookupOrganizationsByExternalId

Signatures:

-   Iterable<org.zendesk.client.v2.model.Organization> lookupOrganizationsByExternalId(String externalId);
    

The zendesk/lookupOrganizationsByExternalId API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **externalId** | 
 | String |

#### Method lookupUserByEmail

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> lookupUserByEmail(String email);
    

The zendesk/lookupUserByEmail API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **email** | 
 | String |

#### Method lookupUserByExternalId

Signatures:

-   Iterable<org.zendesk.client.v2.model.User> lookupUserByExternalId(String externalId);
    

The zendesk/lookupUserByExternalId API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **externalId** | 
 | String |

#### Method macrosShowChangesToTicket

Signatures:

-   org.zendesk.client.v2.model.Ticket macrosShowChangesToTicket(long macroId);
    

The zendesk/macrosShowChangesToTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **macroId** | 
 | Long |

#### Method macrosShowTicketAfterChanges

Signatures:

-   org.zendesk.client.v2.model.Ticket macrosShowTicketAfterChanges(long ticketId, long macroId);
    

The zendesk/macrosShowTicketAfterChanges API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **macroId** | 
 | Long |
| **ticketId** | 

 | Long |

#### Method makePrivateTicketAudit

Signatures:

-   void makePrivateTicketAudit(long ticketId, long auditId);
    
-   void makePrivateTicketAudit(org.zendesk.client.v2.model.Ticket ticket, long id);
    
-   void makePrivateTicketAudit(org.zendesk.client.v2.model.Ticket ticket, org.zendesk.client.v2.model.Audit audit);
    

The zendesk/makePrivateTicketAudit API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **audit** | 
 | Audit |
| **auditId** | 

 | Long |
| **id** | 

 | Long |
| **ticket** | 

 | Ticket |
| **ticketId** | 

 | Long |

#### Method markTicketAsSpam

Signatures:

-   void markTicketAsSpam(long id);
    
-   void markTicketAsSpam(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/markTicketAsSpam API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ticket** | 

 | Ticket |

#### Method mergeUsers

Signatures:

-   org.zendesk.client.v2.model.User mergeUsers(long userIdThatWillRemain, long userIdThatWillBeMerged);
    

The zendesk/mergeUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userIdThatWillBeMerged** | 
 | Long |
| **userIdThatWillRemain** | 

 | Long |

#### Method notifyApp

Signatures:

-   void notifyApp(String json);
    

The zendesk/notifyApp API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **json** | 
 | String |

#### Method permanentlyDeleteTicket

Signatures:

-   org.zendesk.client.v2.model.JobStatus permanentlyDeleteTicket(long id);
    
-   org.zendesk.client.v2.model.JobStatus permanentlyDeleteTicket(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/permanentlyDeleteTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ticket** | 

 | Ticket |

#### Method permanentlyDeleteTickets

Signatures:

-   org.zendesk.client.v2.model.JobStatus permanentlyDeleteTickets(long id, long\[\] ids);
    

The zendesk/permanentlyDeleteTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **ids** | 

 | long\[\] |

#### Method permanentlyDeleteUser

Signatures:

-   org.zendesk.client.v2.model.User permanentlyDeleteUser(long id);
    
-   org.zendesk.client.v2.model.User permanentlyDeleteUser(org.zendesk.client.v2.model.User user);
    

The zendesk/permanentlyDeleteUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **user** | 

 | User |

#### Method queueCreateTicketAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> queueCreateTicketAsync(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/queueCreateTicketAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticket** | 
 | Ticket |

#### Method removeTagFromOrganisations

Signatures:

-   java.util.List<String> removeTagFromOrganisations(long id, String\[\] tags);
    

The zendesk/removeTagFromOrganisations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method removeTagFromTicket

Signatures:

-   java.util.List<String> removeTagFromTicket(long id, String\[\] tags);
    

The zendesk/removeTagFromTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method removeTagFromTopics

Signatures:

-   java.util.List<String> removeTagFromTopics(long id, String\[\] tags);
    

The zendesk/removeTagFromTopics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method requestVerifyUserIdentity

Signatures:

-   org.zendesk.client.v2.model.Identity requestVerifyUserIdentity(long userId, long identityId);
    
-   org.zendesk.client.v2.model.Identity requestVerifyUserIdentity(org.zendesk.client.v2.model.User user, long identityId);
    
-   org.zendesk.client.v2.model.Identity requestVerifyUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/requestVerifyUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **identityId** | 

 | Long |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method resetUserPassword

Signatures:

-   void resetUserPassword(long id, String password);
    
-   void resetUserPassword(org.zendesk.client.v2.model.User user, String password);
    

The zendesk/resetUserPassword API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **password** | 

 | String |
| **user** | 

 | User |

#### Method searchTriggers

Signatures:

-   Iterable<org.zendesk.client.v2.model.Trigger> searchTriggers(String query);
    
-   Iterable<org.zendesk.client.v2.model.Trigger> searchTriggers(String query, boolean active, String sortBy, org.zendesk.client.v2.model.SortOrder sortOrder);
    

The zendesk/searchTriggers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **active** | 
 | Boolean |
| **query** | 

 | String |
| **sortBy** | 

 | String |
| **sortOrder** | 

 | SortOrder |

#### Method setGroupMembershipAsDefault

Signatures:

-   java.util.List<org.zendesk.client.v2.model.GroupMembership> setGroupMembershipAsDefault(long user\_id, org.zendesk.client.v2.model.GroupMembership groupMembership);
    

The zendesk/setGroupMembershipAsDefault API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembership** | 
 | GroupMembership |
| **user\_id** | 

 | Long |

#### Method setOrganizationMembershipAsDefault

Signatures:

-   java.util.List<org.zendesk.client.v2.model.OrganizationMembership> setOrganizationMembershipAsDefault(long user\_id, org.zendesk.client.v2.model.OrganizationMembership organizationMembership);
    

The zendesk/setOrganizationMembershipAsDefault API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationMembership** | 
 | OrganizationMembership |
| **user\_id** | 

 | Long |

#### Method setTagOnOrganisations

Signatures:

-   java.util.List<String> setTagOnOrganisations(long id, String\[\] tags);
    

The zendesk/setTagOnOrganisations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method setTagOnTicket

Signatures:

-   java.util.List<String> setTagOnTicket(long id, String\[\] tags);
    

The zendesk/setTagOnTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method setTagOnTopics

Signatures:

-   java.util.List<String> setTagOnTopics(long id, String\[\] tags);
    

The zendesk/setTagOnTopics API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |
| **tags** | 

 | String\[\] |

#### Method setUserPrimaryIdentity

Signatures:

-   java.util.List<org.zendesk.client.v2.model.Identity> setUserPrimaryIdentity(long userId, long identityId);
    
-   java.util.List<org.zendesk.client.v2.model.Identity> setUserPrimaryIdentity(org.zendesk.client.v2.model.User user, long identityId);
    
-   java.util.List<org.zendesk.client.v2.model.Identity> setUserPrimaryIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/setUserPrimaryIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **identityId** | 

 | Long |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method showArticleTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation showArticleTranslation(long articleId, String locale);
    

The zendesk/showArticleTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId0** | 
 | Long |
| **locale** | 

 | String |

#### Method showCategoryTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation showCategoryTranslation(long categoryId, String locale);
    

The zendesk/showCategoryTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **categoryId1** | 
 | Long |
| **locale** | 

 | String |

#### Method showSectionTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation showSectionTranslation(long sectionId, String locale);
    

The zendesk/showSectionTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **locale** | 
 | String |
| **sectionId0** | 

 | Long |

#### Method suspendUser

Signatures:

-   org.zendesk.client.v2.model.User suspendUser(long id);
    

The zendesk/suspendUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method trustTicketAudit

Signatures:

-   void trustTicketAudit(long ticketId, long auditId);
    
-   void trustTicketAudit(org.zendesk.client.v2.model.Ticket ticket, long id);
    
-   void trustTicketAudit(org.zendesk.client.v2.model.Ticket ticket, org.zendesk.client.v2.model.Audit audit);
    

The zendesk/trustTicketAudit API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **audit** | 
 | Audit |
| **auditId** | 

 | Long |
| **id** | 

 | Long |
| **ticket** | 

 | Ticket |
| **ticketId** | 

 | Long |

#### Method unassignOrganizationMembership

Signatures:

-   void unassignOrganizationMembership(long user\_id, long organization\_id);
    

The zendesk/unassignOrganizationMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization\_id** | 
 | Long |
| **user\_id** | 

 | Long |

#### Method unsuspendUser

Signatures:

-   org.zendesk.client.v2.model.User unsuspendUser(long id);
    

The zendesk/unsuspendUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | 
 | Long |

#### Method updateArticle

Signatures:

-   org.zendesk.client.v2.model.hc.Article updateArticle(org.zendesk.client.v2.model.hc.Article article);
    

The zendesk/updateArticle API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **article** | 
 | Article |

#### Method updateArticleTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation updateArticleTranslation(Long articleId, String locale, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/updateArticleTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **articleId** | 
 | Long |
| **locale** | 

 | String |
| **translation** | 

 | Translation |

#### Method updateAutomation

Signatures:

-   org.zendesk.client.v2.model.Automation updateAutomation(Long automationId, org.zendesk.client.v2.model.Automation automation);
    

The zendesk/updateAutomation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **automation** | 
 | Automation |
| **automationId** | 

 | Long |

#### Method updateCategory

Signatures:

-   org.zendesk.client.v2.model.hc.Category updateCategory(org.zendesk.client.v2.model.hc.Category category);
    

The zendesk/updateCategory API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **category** | 
 | Category |

#### Method updateCategoryTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation updateCategoryTranslation(Long categoryId, String locale, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/updateCategoryTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **categoryId** | 
 | Long |
| **locale** | 

 | String |
| **translation** | 

 | Translation |

#### Method updateContentTag

Signatures:

-   org.zendesk.client.v2.model.hc.ContentTag updateContentTag(org.zendesk.client.v2.model.hc.ContentTag contentTag);
    

The zendesk/updateContentTag API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentTag** | 
 | ContentTag |

#### Method updateDynamicContentItem

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItem updateDynamicContentItem(org.zendesk.client.v2.model.dynamic.DynamicContentItem item);
    

The zendesk/updateDynamicContentItem API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **item** | 
 | DynamicContentItem |

#### Method updateDynamicContentItemVariant

Signatures:

-   org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant updateDynamicContentItemVariant(Long itemId, org.zendesk.client.v2.model.dynamic.DynamicContentItemVariant variant);
    

The zendesk/updateDynamicContentItemVariant API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **itemId** | 
 | Long |
| **variant** | 

 | DynamicContentItemVariant |

#### Method updateForum

Signatures:

-   org.zendesk.client.v2.model.Forum updateForum(org.zendesk.client.v2.model.Forum forum);
    

The zendesk/updateForum API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **forum** | 
 | Forum |

#### Method updateGroup

Signatures:

-   org.zendesk.client.v2.model.Group updateGroup(org.zendesk.client.v2.model.Group group);
    

The zendesk/updateGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **group** | 
 | Group |

#### Method updateInstallation

Signatures:

-   void updateInstallation(int id, String json);
    

The zendesk/updateInstallation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **installationId** | 
 | Integer |
| **json** | 

 | String |

#### Method updateMacro

Signatures:

-   org.zendesk.client.v2.model.Macro updateMacro(Long macroId, org.zendesk.client.v2.model.Macro macro);
    

The zendesk/updateMacro API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **macro** | 
 | Macro |
| **macroId0** | 

 | Long |

#### Method updateOrganization

Signatures:

-   org.zendesk.client.v2.model.Organization updateOrganization(org.zendesk.client.v2.model.Organization organization);
    

The zendesk/updateOrganization API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organization** | 
 | Organization |

#### Method updateOrganizations

Signatures:

-   org.zendesk.client.v2.model.JobStatus updateOrganizations(java.util.List<org.zendesk.client.v2.model.Organization> organizations);
    
-   org.zendesk.client.v2.model.JobStatus updateOrganizations(org.zendesk.client.v2.model.Organization\[\] organizations);
    

The zendesk/updateOrganizations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationList** | 
 | List |
| **organizations** | 

 | Organization\[\] |

#### Method updateOrganizationsAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> updateOrganizationsAsync(java.util.List<org.zendesk.client.v2.model.Organization> organizations);
    

The zendesk/updateOrganizationsAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **organizationList** | 
 | List |

#### Method updatePermissionGroup

Signatures:

-   org.zendesk.client.v2.model.hc.PermissionGroup updatePermissionGroup(org.zendesk.client.v2.model.hc.PermissionGroup permissionGroup);
    

The zendesk/updatePermissionGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **permissionGroup** | 
 | PermissionGroup |

#### Method updateRequest

Signatures:

-   org.zendesk.client.v2.model.Request updateRequest(org.zendesk.client.v2.model.Request request);
    

The zendesk/updateRequest API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **request** | 
 | Request |

#### Method updateSection

Signatures:

-   org.zendesk.client.v2.model.hc.Section updateSection(org.zendesk.client.v2.model.hc.Section section);
    

The zendesk/updateSection API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **section** | 
 | Section |

#### Method updateSectionTranslation

Signatures:

-   org.zendesk.client.v2.model.hc.Translation updateSectionTranslation(Long sectionId, String locale, org.zendesk.client.v2.model.hc.Translation translation);
    

The zendesk/updateSectionTranslation API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **locale** | 
 | String |
| **sectionId** | 

 | Long |
| **translation** | 

 | Translation |

#### Method updateTicket

Signatures:

-   org.zendesk.client.v2.model.Ticket updateTicket(org.zendesk.client.v2.model.Ticket ticket);
    

The zendesk/updateTicket API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticket** | 
 | Ticket |

#### Method updateTicketField

Signatures:

-   org.zendesk.client.v2.model.Field updateTicketField(org.zendesk.client.v2.model.Field field);
    

The zendesk/updateTicketField API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **field** | 
 | Field |

#### Method updateTicketForm

Signatures:

-   org.zendesk.client.v2.model.TicketForm updateTicketForm(org.zendesk.client.v2.model.TicketForm ticketForm);
    

The zendesk/updateTicketForm API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketForm** | 
 | TicketForm |

#### Method updateTickets

Signatures:

-   org.zendesk.client.v2.model.JobStatus updateTickets(java.util.List<org.zendesk.client.v2.model.Ticket> tickets);
    
-   org.zendesk.client.v2.model.JobStatus updateTickets(org.zendesk.client.v2.model.Ticket\[\] tickets);
    

The zendesk/updateTickets API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketList** | 
 | List |
| **tickets** | 

 | Ticket\[\] |

#### Method updateTicketsAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> updateTicketsAsync(java.util.List<org.zendesk.client.v2.model.Ticket> tickets);
    

The zendesk/updateTicketsAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **ticketList** | 
 | List |

#### Method updateTopic

Signatures:

-   org.zendesk.client.v2.model.Topic updateTopic(org.zendesk.client.v2.model.Topic topic);
    

The zendesk/updateTopic API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **topic** | 
 | Topic |

#### Method updateTrigger

Signatures:

-   org.zendesk.client.v2.model.Trigger updateTrigger(Long triggerId, org.zendesk.client.v2.model.Trigger trigger);
    

The zendesk/updateTrigger API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **trigger** | 
 | Trigger |
| **triggerId0** | 

 | Long |

#### Method updateUser

Signatures:

-   org.zendesk.client.v2.model.User updateUser(org.zendesk.client.v2.model.User user);
    

The zendesk/updateUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **user** | 
 | User |

#### Method updateUserIdentity

Signatures:

-   org.zendesk.client.v2.model.Identity updateUserIdentity(long userId, org.zendesk.client.v2.model.Identity identity);
    
-   org.zendesk.client.v2.model.Identity updateUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/updateUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **user** | 

 | User |
| **userId** | 

 | Long |

#### Method updateUserSegment

Signatures:

-   org.zendesk.client.v2.model.hc.UserSegment updateUserSegment(org.zendesk.client.v2.model.hc.UserSegment userSegment);
    

The zendesk/updateUserSegment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userSegment** | 
 | UserSegment |

#### Method updateUsers

Signatures:

-   org.zendesk.client.v2.model.JobStatus updateUsers(java.util.List<org.zendesk.client.v2.model.User> users);
    
-   org.zendesk.client.v2.model.JobStatus updateUsers(org.zendesk.client.v2.model.User\[\] users);
    

The zendesk/updateUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **users** | 
 | User\[\] |
| **usersList** | 

 | List |

#### Method updateUsersAsync

Signatures:

-   org.asynchttpclient.ListenableFuture<org.zendesk.client.v2.model.JobStatus> updateUsersAsync(java.util.List<org.zendesk.client.v2.model.User> users);
    

The zendesk/updateUsersAsync API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **usersList** | 
 | List |

#### Method verifyUserIdentity

Signatures:

-   org.zendesk.client.v2.model.Identity verifyUserIdentity(long userId, long identityId);
    
-   org.zendesk.client.v2.model.Identity verifyUserIdentity(org.zendesk.client.v2.model.User user, long identityId);
    
-   org.zendesk.client.v2.model.Identity verifyUserIdentity(org.zendesk.client.v2.model.User user, org.zendesk.client.v2.model.Identity identity);
    

The zendesk/verifyUserIdentity API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **identity** | 
 | Identity |
| **identityId** | 

 | Long |
| **user** | 

 | User |
| **userId** | 

 | Long |

In addition to the parameters above, the zendesk API can also use any of the [Query Parameters (26 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelZendesk.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelZendesk.myParameterNameHere` header.

## Spring Boot Auto-Configuration

When using zendesk with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-zendesk-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.zendesk.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.zendesk.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.zendesk.configuration** | Component configuration. The option is a org.apache.camel.component.zendesk.ZendeskConfiguration type. |  | ZendeskConfiguration |
| **camel.component.zendesk.enabled** | Whether to enable auto configuration of the zendesk component. This is enabled by default. |  | Boolean |
| **camel.component.zendesk.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.zendesk.oauth-token** | The OAuth token. |  | String |
| **camel.component.zendesk.password** | The password. |  | String |
| **camel.component.zendesk.server-url** | The server URL to connect. |  | String |
| **camel.component.zendesk.token** | The security token. |  | String |
| **camel.component.zendesk.username** | The user name. |  | String |
| **camel.component.zendesk.zendesk** | To use a shared Zendesk instance. The option is a org.zendesk.client.v2.Zendesk type. |  | Zendesk |