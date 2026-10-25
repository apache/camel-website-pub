# Jira

**Since Camel 3.0**

**Both producer and consumer are supported**

The JIRA component interacts with the JIRA API by encapsulating Atlassian’s [REST Java Client for JIRA](https://bitbucket.org/atlassian/jira-rest-java-client/src/master/). It currently provides polling for new issues and new comments. It is also able to create new issues, add comments, change issues, add/remove watchers, add attachment and transition the state of an issue.

Rather than webhooks, this endpoint relies on simple polling. Reasons include:

-   Concern for reliability/stability
    
-   The types of payloads we’re polling aren’t typically large (plus, paging is available in the API)
    
-   The need to support apps running somewhere not publicly accessible where a webhook would fail
    

Note that the JIRA API is fairly expansive. Therefore, this component could be easily expanded to provide additional interactions.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jira</artifactId>
    <version>${camel-version}</version>
</dependency>
```

> **Note**
> Atlassian does not release their JIRA Java client to Maven Central. Therefore, when using `camel-jira` then the `pom.xml` has included Maven repository to the following URL: `[https://packages.atlassian.com/maven-external](https://packages.atlassian.com/maven-external)`.
>
> Keep this in mind as Maven will then use this repository to download the JIRA client (and potentially other JARs). Which allows Atlassian to track these downloads by their servers.

## URI format

jira://type\[?options\]

The Jira type accepts the following operations:

For consumers:

-   newIssues: retrieve only new issues after the route is started
    
-   newComments: retrieve only new comments after the route is started
    
-   watchUpdates: retrieve only updated fields/issues based on provided jql
    

For producers:

-   addIssue: add an issue
    
-   addComment: add a comment on a given issue
    
-   attach: add an attachment on a given issue
    
-   deleteIssue: delete a given issue
    
-   updateIssue: update fields of a given issue
    
-   transitionIssue: transition a status of a given issue
    
-   watchers: add/remove watchers of a given issue
    

As Jira is fully customizable, you must ensure the field IDs exist for the project and workflow, as they can change between different Jira servers.

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

The Jira component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **delay** (common) | Time in milliseconds to elapse for the next poll. | 6000 | Integer |
| **jiraUrl** (common) | **Required** The Jira server url, for example [http://my\_jira.com:8081](http://my_jira.com:8081). |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a shared base jira configuration. |  | JiraConfiguration |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **accessToken** (security) | (OAuth or Personal Access Token authentication) The access token generated by the Jira server. |  | String |
| **consumerKey** (security) | (OAuth only) The consumer key from Jira settings. |  | String |
| **password** (security) | (Basic authentication only) The password or the API Token to authenticate to the Jira server. Use only if username basic authentication is used. |  | String |
| **privateKey** (security) | (OAuth only) The private key generated by the client to encrypt the conversation to the server. |  | String |
| **username** (security) | (Basic authentication only) The username to authenticate to the Jira server. Use only if OAuth is not enabled on the Jira server. Do not set the username and OAuth token parameter, if they are both set, the username basic authentication takes precedence. |  | String |
| **verificationCode** (security) | (OAuth only) The verification code from Jira generated in the first step of the authorization proccess. |  | String |

## Endpoint Options

The Jira endpoint is configured using URI syntax:

jira:type

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** (common) | 
**Required** Operation to perform. Consumers: NewIssues, NewComments. Producers: AddIssue, AttachFile, DeleteIssue, TransitionIssue, UpdateIssue, Watchers. See this class javadoc description for more information.

Enum values:

-   ADDCOMMENT
    
-   ADDISSUE
    
-   ATTACH
    
-   DELETEISSUE
    
-   NEWISSUES
    
-   NEWCOMMENTS
    
-   WATCHUPDATES
    
-   UPDATEISSUE
    
-   TRANSITIONISSUE
    
-   WATCHERS
    
-   ADDISSUELINK
    
-   ADDWORKLOG
    
-   FETCHISSUE
    
-   FETCHCOMMENTS
    





 |  | JiraType |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **delay** (common) | Time in milliseconds to elapse for the next poll. | 6000 | Integer |
| **jiraUrl** (common) | **Required** The Jira server url, for example [http://my\_jira.com:8081](http://my_jira.com:8081). |  | String |
| **jql** (consumer) | JQL is the query language from JIRA which allows you to retrieve the data you want. For example jql=project=MyProject Where MyProject is the product key in Jira. It is important to use the RAW() and set the JQL inside it to prevent camel parsing it, example: RAW(project in (MYP, COM) AND resolution = Unresolved). |  | String |
| **maxResults** (consumer) | Max number of issues to search for. The newIssues consumer reads every issue created since its previous poll, page by page, with this as the page size (at most 50). | 50 | Integer |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **sendOnlyUpdatedField** (consumer) | Indicator for sending only changed fields in exchange body or issue object. By default consumer sends only changed fields. | true | boolean |
| **watchedFields** (consumer) | Comma separated list of fields to watch for changes. Status,Priority are the defaults. | Status,Priority | String |
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
| **accessToken** (security) | (OAuth or Personal Access Token authentication) The access token generated by the Jira server. |  | String |
| **consumerKey** (security) | (OAuth only) The consumer key from Jira settings. |  | String |
| **password** (security) | (Basic authentication only) The password or the API Token to authenticate to the Jira server. Use only if username basic authentication is used. |  | String |
| **privateKey** (security) | (OAuth only) The private key generated by the client to encrypt the conversation to the server. |  | String |
| **username** (security) | (Basic authentication only) The username to authenticate to the Jira server. Use only if OAuth is not enabled on the Jira server. Do not set the username and OAuth token parameter, if they are both set, the username basic authentication takes precedence. |  | String |
| **verificationCode** (security) | (OAuth only) The verification code from Jira generated in the first step of the authorization proccess. |  | String |

## Message Headers

The Jira component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJiraIssueAssigneeId** (producer) Constant: [`ISSUE_ASSIGNEE_ID`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_ASSIGNEE_ID) | The assignee’s id of the issue. |  | String |
| **CamelJiraIssueAssignee** (producer) Constant: [`ISSUE_ASSIGNEE`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_ASSIGNEE) | The assignee’s name of the issue. |  | String |
| **CamelJiraIssueComponents** (producer) Constant: [`ISSUE_COMPONENTS`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_COMPONENTS) | The comma separated list of the issue’s components. |  | String |
| **CamelJiraIssueChanged** (consumer) Constant: [`ISSUE_CHANGED`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_CHANGED) | The name of the updated field (i.e Status). |  | String |
| **CamelJiraIssueKey** (common) Constant: [`ISSUE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_KEY) | The id of the issue. |  | String |
| **CamelJiraIssuePriorityId** (producer) Constant: [`ISSUE_PRIORITY_ID`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_PRIORITY_ID) | The priority’s id of the issue. |  | Long |
| **CamelJiraIssuePriorityName** (producer) Constant: [`ISSUE_PRIORITY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_PRIORITY_NAME) | The priority’s name of the issue. |  | String |
| **CamelJiraIssueProjectKey** (producer) Constant: [`ISSUE_PROJECT_KEY`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_PROJECT_KEY) | The project’s id of the issue. |  | String |
| **CamelJiraIssueSummary** (producer) Constant: [`ISSUE_SUMMARY`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_SUMMARY) | The summary of the issue. |  | String |
| **CamelJiraIssueTransitionId** (producer) Constant: [`ISSUE_TRANSITION_ID`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_TRANSITION_ID) | The transition id. |  | Integer |
| **CamelJiraIssueTypeId** (producer) Constant: [`ISSUE_TYPE_ID`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_TYPE_ID) | The type’s id of the issue. |  | Long |
| **CamelJiraIssueTypeName** (producer) Constant: [`ISSUE_TYPE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_TYPE_NAME) | The type’s name of the issue. |  | String |
| **CamelJiraIssueWatchedIssues** (consumer) Constant: [`ISSUE_WATCHED_ISSUES`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_WATCHED_ISSUES) | The list of all issue keys that are watched in the time of update. |  | String |
| **CamelJiraIssueWatchersAdd** (producer) Constant: [`ISSUE_WATCHERS_ADD`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_WATCHERS_ADD) | The comma separated list of watchers to add to the issue. |  | String |
| **CamelJiraIssueWatchersRemove** (producer) Constant: [`ISSUE_WATCHERS_REMOVE`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#ISSUE_WATCHERS_REMOVE) | The watchers of the issue to remove. |  | String |
| **CamelJiraParentIssueKey** (producer) Constant: [`PARENT_ISSUE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#PARENT_ISSUE_KEY) | The id of the parent issue. |  | String |
| **CamelJiraChildIssueKey** (producer) Constant: [`CHILD_ISSUE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#CHILD_ISSUE_KEY) | The id of the child issue. |  | String |
| **CamelJiraLinkType** (producer) Constant: [`LINK_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#LINK_TYPE) | The type of link. |  | String |
| **CamelJiraMinutesSpent** (producer) Constant: [`MINUTES_SPENT`](https://javadoc.io/doc/org.apache.camel/camel-jira/latest/org/apache/camel/component/jira/JiraConstants.html#MINUTES_SPENT) | The minutes spent. | \-1 | int |

## Message Body

The message body at each side of the Jira component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `pojo` or `null` | One message per new Issue (newIssues) or new Comment (newComments). watchUpdates sends one per watched field that changed, with its new value, such as the Status or the BasicPriority (null when cleared), or the Issue with sendOnlyUpdatedField=false.
-   With `sendOnlyUpdatedField=false`: `pojo` (`com.atlassian.jira.rest.client.api.domain.Issue`)
    
-   With `type=NEWISSUES`: `pojo` (`com.atlassian.jira.rest.client.api.domain.Issue`)
    
-   With `type=NEWCOMMENTS`: `pojo` (`com.atlassian.jira.rest.client.api.domain.Comment`)
    

Not known when `watchedFields` is set.

 |
| **Producer input** | `any` | 

Read as text: the description for addIssue and updateIssue, the comment for addComment and addWorkLog, which fail without a body, and an optional comment for transitionIssue and addIssueLink; a Map or a POJO is sent as its toString(), so marshal it first. attach uploads a file, or text, bytes or a stream named by the CamelFileName header. The other types read only headers.

-   With `type=ADDISSUE`: `null`, `text`, `bytes`, `stream` or `file`
    
-   With `type=UPDATEISSUE`: `null`, `text`, `bytes`, `stream` or `file`
    
-   With `type=TRANSITIONISSUE`: `null`, `text`, `bytes`, `stream` or `file`
    
-   With `type=ADDISSUELINK`: `null`, `text`, `bytes`, `stream` or `file`
    
-   With `type=ADDCOMMENT`: `text`, `bytes`, `stream` or `file`
    
-   With `type=ADDWORKLOG`: `text`, `bytes`, `stream` or `file`
    
-   With `type=ATTACH`: `text`, `bytes`, `stream` or `file`
    





 |
| **Producer output** | `unchanged` | 

The Issue created for addIssue, the Issue for fetchIssue and the List of its Comments for fetchComments. The other types leave the body unchanged.

-   With `type=ADDISSUE`: `pojo` (`com.atlassian.jira.rest.client.api.domain.Issue`)
    
-   With `type=FETCHISSUE`: `pojo` (`com.atlassian.jira.rest.client.api.domain.Issue`)
    
-   With `type=FETCHCOMMENTS`: `list` (`java.util.List<com.atlassian.jira.rest.client.api.domain.Comment>`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Client Factory

You can bind the `JiraRestClientFactory` with name **JiraRestClientFactory** in the registry to have it automatically set in the Jira endpoint.

### Authentication

Camel-jira supports the following forms of authentication:

-   [Basic Authentication](https://developer.atlassian.com/cloud/jira/platform/jira-rest-api-basic-authentication/)
    
-   [OAuth 3 legged authentication](https://developer.atlassian.com/cloud/jira/platform/jira-rest-api-oauth-authentication/)
    
-   [Personal Token](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.md)\*
    

We recommend using OAuth or Personal token whenever possible, as it provides the best security for your users and system.

#### Basic authentication requirements:

-   A username and a password.
    

#### OAuth authentication requirements:

Follow the tutorial in [Jira OAuth documentation](https://developer.atlassian.com/cloud/jira/platform/jira-rest-api-oauth-authentication/) to generate the client private key, consumer key, verification code and access token.

-   a private key, generated locally on your system.
    
-   A verification code, generated by Jira server.
    
-   The consumer key, set in the Jira server settings.
    
-   An access token, generated by Jira server.
    

#### Personal access token authentication requirements:

Follow the tutorial to generate the [Personal Token](https://confluence.atlassian.com/enterprise/using-personal-access-tokens-1026032365.md).

-   You have to set only the personal token in the `access-token` parameter.
    

### JQL

The JQL URI option is used by both consumer endpoints. Theoretically, items like the "project key", etc. could be URI options themselves. However, by requiring the use of JQL, the consumers become much more flexible and powerful.

At the bare minimum, the consumers will require the following:

jira://\[type\]?\[required options\]&jql=project=\[project key\]

One important thing to note is that the newIssues consumer will automatically set the JQL as:

-   append `ORDER BY created DESC` to your JQL
    
-   prepend `created > latestIssueCreationDate` to retrieve issues added after the camel route was started.
    

This is in order to optimize startup processing, rather than having to index every single issue in the project.

Each poll reads every page of that search, so the issues created since the previous poll are consumed also when there are more than `maxResults` of them (for example after Jira was unreachable for a while); `maxResults` is then the page size of the search (at most 50). There is no upper bound: after a long outage or a large import, one poll reads all the new issues, one search request per page, keeps them in memory and routes them as one batch. On Jira Cloud the pages are read with the next page token of the search, as Jira Cloud cannot page by start index. The search of Jira Cloud is eventually consistent, so a new issue can become searchable only after a newer one: when a poll has already consumed the newer one, the late issue is not consumed.

Another note is that, similarly, the newComments consumer will have to index every single issue **and** comment on the project. Therefore, for large projects, it’s **vital** to optimize the JQL expression as much as possible. For example, the JIRA Toolkit Plugin includes a `"Number of comments"` custom field use `'"Number of comments" > 0'` in your query. Also try to minimize based on state (`status=Open`), increase the polling delay, etc. Example:

jira://\[type\]?\[required options\]&jql=RAW(project=\[project key\] AND status in (Open, \\"Coding In Progress\\") AND \\"Number of comments\\">0)"

### Examples

The Jira server and the credentials are component options, for example in `application.properties`:

```properties
camel.component.jira.jira-url = https://jira.example.com
camel.component.jira.username = {{env:JIRA_USERNAME}}
camel.component.jira.password = {{env:JIRA_PASSWORD}}
```

The following route polls the new open issues of a project every minute. The body is the `Issue`:

```yaml
- route:
    from:
      uri: jira:newIssues
      parameters:
        jql: "RAW(project=CAMEL AND status=Open)"
        delay: 60000
      steps:
        - log:
            message: "New issue ${body.key}: ${body.summary}"
```

The following route creates an issue. The message body is the description, and the body after the call is the created `Issue`:

```yaml
- route:
    from:
      uri: direct:report
      steps:
        - setHeader:
            name: CamelJiraIssueProjectKey
            expression:
              constant:
                expression: CAMEL
        - setHeader:
            name: CamelJiraIssueTypeName
            expression:
              constant:
                expression: Bug
        - setHeader:
            name: CamelJiraIssueSummary
            expression:
              simple:
                expression: "Order ${header.orderId} failed"
        - to:
            uri: jira:addIssue
        - log:
            message: "Created ${body.key}"
```

### Operations

See a list of required headers to set when using the Jira operations. The author field for the producers is automatically set to the authenticated user on the Jira side.

If any required field is not set, then an IllegalArgumentException is throw.

There are operations that requires `id` for fields such as the issue type, priority, transition. Check the valid `id` on your jira project as they may differ on a jira installation and project workflow.

### AddIssue

Required:

-   `CamelJiraIssueProjectKey`: The project key, example: CAMEL, HHH, MYP.
    
-   `CamelJiraIssueTypeId` or `CamelJiraIssueTypeName`: The `id` of the issue type or the name of the issue type, you can see the valid list in `http://jira_server/rest/api/2/issue/createmeta?projectKeys=SAMPLE_KEY`.
    
-   `CamelJiraIssueSummary`: The summary of the issue.
    

Optional:

-   `CamelJiraIssueAssignee`: the assignee user
    
-   `CamelJiraIssueAssigneeId`: the assignee user id
    
-   `CamelJiraIssuePriorityId` or `CamelJiraIssuePriorityName`: The priority of the issue, you can see the valid list in `http://jira_server/rest/api/2/priority`.
    
-   `CamelJiraIssueComponents`: A list of string with the valid component names.
    
-   `CamelJiraIssueWatchersAdd`: A list of strings with the usernames (or id) to add to the watcher list.
    
-   The exchange body is used as the issue description.
    

### AddComment

Required:

-   `CamelJiraIssueKey`: The issue key identifier.
    
-   the body of the exchange is the text of the comment.
    

### Attach

Only one file should attach per invocation.

Required:

-   `CamelJiraIssueKey`: The issue key identifier.
    
-   the body of the exchange is the file to attach: a `File`, the file of the file consumer, or text, bytes or a stream, named by the `CamelFileName` header
    

### DeleteIssue

Required:

-   `CamelJiraIssueKey`: The issue key identifier.
    

### TransitionIssue

Required:

-   `CamelJiraIssueKey`: The issue key identifier.
    
-   `CamelJiraIssueTransitionId`: The issue transition `id`.
    

Optional:

-   the body of the exchange is a comment to add to the issue after the transition.
    

### UpdateIssue

-   `CamelJiraIssueKey`: The issue key identifier.
    
-   `CamelJiraIssueTypeId` or `CamelJiraIssueTypeName`: The `id` of the issue type or the name of the issue type, you can see the valid list in `http://jira_server/rest/api/2/issue/createmeta?projectKeys=SAMPLE_KEY`.
    
-   `CamelJiraIssueSummary`: The summary of the issue.
    
-   `CamelJiraIssueAssignee`: the assignee user
    
-   `CamelJiraIssueAssigneeId`: the assignee user id
    
-   `CamelJiraIssuePriorityId` or `CamelJiraIssuePriorityName`: The priority of the issue, you can see the valid list in `http://jira_server/rest/api/2/priority`.
    
-   `CamelJiraIssueComponents`: A list of string with the valid component names.
    
-   The exchange body is used as the issue description.
    

### Watcher

-   `CamelJiraIssueKey`: The issue key identifier.
    
-   `CamelJiraIssueWatchersAdd`: A list of strings with the usernames (or id) to add to the watcher list.
    
-   `CamelJiraIssueWatchersRemove`: A list of strings with the usernames to remove from the watcher list.
    

### WatchUpdates (consumer)

-   `watchedFields` Comma separated list of fields to watch for changes i.e. `Status,Priority,Assignee,Components` etc.
    
-   `sendOnlyUpdatedField` By default, only the changed field is sent as the body.
    

All messages also contain the following headers that add additional info about the change:

-   `issueKey`: Key of the updated issue
    
-   `changed`: name of the updated field (i.e., Status)
    
-   `watchedIssues`: list of all issue keys that are watched in the time of update