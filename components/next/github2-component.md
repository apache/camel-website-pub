# GitHub2

**Since Camel 4.18**

**Both producer and consumer are supported**

The GitHub2 component interacts with the GitHub API by encapsulating the [kohsuke github-api](https://github.com/hub4j/github-api) library. It currently provides polling for new pull requests, pull request comments, tags, commits, and events. It is also able to produce comments on pull requests, as well as close the pull request entirely.

This component supports GitHub Enterprise by allowing you to specify a custom API URL.

Rather than webhooks, this endpoint relies on simple polling. Reasons include:

-   Concern for reliability/stability
    
-   The types of payloads we’re polling aren’t typically large (plus, paging is available in the API)
    
-   The need to support apps running somewhere not publicly accessible where a webhook would fail
    

Note that the GitHub API is fairly expansive. Therefore, this component could be easily expanded to provide additional interactions.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-github2</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

github2://endpoint\[?options\]

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

The GitHub2 component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiUrl** (advanced) | GitHub API URL for GitHub Enterprise. Leave empty for github.com. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **oauthToken** (security) | GitHub OAuth token. Must be configured on either component or endpoint. |  | String |

## Endpoint Options

The GitHub2 endpoint is configured using URI syntax:

github2:type/branchName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** (common) | 
**Required** What git operation to execute.

Enum values:

-   CLOSEPULLREQUEST
    
-   PULLREQUESTCOMMENT
    
-   COMMIT
    
-   PULLREQUEST
    
-   TAG
    
-   PULLREQUESTSTATE
    
-   PULLREQUESTFILES
    
-   GETCOMMITFILE
    
-   CREATEISSUE
    
-   EVENT
    





 |  | GitHub2Type |
| **branchName** (consumer) | Name of branch. |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **repoName** (common) | **Required** GitHub repository name. |  | String |
| **repoOwner** (common) | **Required** GitHub repository owner (organization). |  | String |
| **commitMessageAsBody** (consumer) | Whether the commit consumer should store the commit message or the raw org.kohsuke.github.GHCommit object as the message body. | true | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **startingSha** (consumer) | The starting sha to use for polling commits with the commit consumer. The value can either be a sha for the sha to start from, or use beginning to start from the beginning, or last to start from the last commit. | last | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eventFetchStrategy** (consumer (advanced)) | To specify a custom strategy that configures how the EventsConsumer fetches events. |  | GitHub2EventFetchStrategy |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **encoding** (producer) | To use the given encoding when getting a git commit file. |  | String |
| **state** (producer) | 

To set git commit status state.

Enum values:

-   error
    
-   failure
    
-   pending
    
-   success
    





 |  | String |
| **targetUrl** (producer) | To set git commit status target url. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiUrl** (advanced) | GitHub API URL for GitHub Enterprise. Leave empty for github.com. |  | String |
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
| **oauthToken** (security) | GitHub OAuth token. Must be configured on either component or endpoint. |  | String |

## Message Headers

The GitHub2 component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGitHubPullRequest** (common) Constant: [`GITHUB_PULLREQUEST`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_PULLREQUEST) | The pull request. |  | GHPullRequest or Integer |
| **CamelGitHubInResponseTo** (producer) Constant: [`GITHUB_INRESPONSETO`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_INRESPONSETO) | The id of the comment to reply to. |  | Long |
| **CamelGitHubPullRequestHeadCommitSha** (common) Constant: [`GITHUB_PULLREQUEST_HEAD_COMMIT_SHA`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_PULLREQUEST_HEAD_COMMIT_SHA) | The sha of the head of the pull request. |  | String |
| **CamelGitHubIssueTitle** (producer) Constant: [`GITHUB_ISSUE_TITLE`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_ISSUE_TITLE) | The title of the issue. |  | String |
| **CamelGitHubCommitAuthor** (consumer) Constant: [`GITHUB_COMMIT_AUTHOR`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_COMMIT_AUTHOR) | The commit author. |  | String |
| **CamelGitHubCommitCommitter** (consumer) Constant: [`GITHUB_COMMIT_COMMITTER`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_COMMIT_COMMITTER) | The committer name. |  | String |
| **CamelGitHubCommitSha** (consumer) Constant: [`GITHUB_COMMIT_SHA`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_COMMIT_SHA) | The commit sha. |  | String |
| **CamelGitHubCommitUrl** (consumer) Constant: [`GITHUB_COMMIT_URL`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_COMMIT_URL) | The commit URL. |  | String |
| **CamelGitHubEventPayload** (consumer) Constant: [`GITHUB_EVENT_PAYLOAD`](https://javadoc.io/doc/org.apache.camel/camel-github2/latest/org/apache/camel/component/github2/GitHub2Constants.html#GITHUB_EVENT_PAYLOAD) | The event payload. |  | GHEventPayload |

## Usage

### Configuring authentication

The GitHub2 component requires to be configured with an authentication token on either the component or endpoint level.

For example, to set it on the component:

_Java-only: programmatic component configuration_

```java
GitHub2Component ghc = context.getComponent("github2", GitHub2Component.class);
ghc.setOauthToken("mytoken");
```

### GitHub Enterprise

To use with GitHub Enterprise, set the `apiUrl` parameter to your GitHub Enterprise API endpoint:

-   Java
    
-   XML
    
-   YAML
    

```java
from("github2:commit/main?repoOwner=myorg&repoName=myrepo&apiUrl=https://github.mycompany.com/api/v3")
    .to("log:commits");
```

```xml
<route>
  <from uri="github2:commit/main?repoOwner=myorg&amp;repoName=myrepo&amp;apiUrl=https://github.mycompany.com/api/v3"/>
  <to uri="log:commits"/>
</route>
```

```yaml
- route:
    from:
      uri: github2:commit/main
      parameters:
        repoOwner: myorg
        repoName: myrepo
        apiUrl: "https://github.mycompany.com/api/v3"
      steps:
        - to:
            uri: log:commits
```

### Consumer Endpoints

  
| Endpoint | Context | Body Type |
| --- | --- | --- |
| pullRequest | polling | `org.kohsuke.github.GHPullRequest` |
| pullRequestComment | polling | `org.kohsuke.github.GHPullRequestReviewComment` |
| tag | polling | `org.kohsuke.github.GHTag` |
| commit | polling | `org.kohsuke.github.GHCommit` or `String` with commit message and headers with some metadata. This can be configured by the `commitMessageAsBody` option. |
| event | polling | `org.kohsuke.github.GHEventInfo` |

### Producer Endpoints

  
| Endpoint | Body | Message Headers |
| --- | --- | --- |
| pullRequestComment | String (comment text) | \- `CamelGitHubPullRequest` (integer) (REQUIRED): Pull request number. - `CamelGitHubInResponseTo` (integer): Required if responding to another inline comment on the pull request diff. If left off, a general comment on the pull request discussion is assumed. |
| closePullRequest | none | \- `CamelGitHubPullRequest` (integer) (REQUIRED): Pull request number. |
| createIssue | String (issue body text) | \- `CamelGitHubIssueTitle` (String) (REQUIRED): Issue Title. |
| pullRequestState | none | \- `CamelGitHubPullRequest` (integer) (REQUIRED): Pull request number. Sets the commit status on a pull request. |
| pullRequestFiles | none | \- `CamelGitHubPullRequest` (integer) (REQUIRED): Pull request number. Returns the list of files changed in a pull request. |
| getCommitFile | none | \- `CamelGitHubCommitSha` (String) (REQUIRED): Commit SHA. - `CamelGitHubFilePath` (String) (REQUIRED): File path. Returns the content of a file at a specific commit. |

### Example: Consuming commits

-   Java
    
-   XML
    
-   YAML
    

```java
from("github2:commit/main?repoOwner=apache&repoName=camel&oauthToken=mytoken")
    .log("New commit: ${header.CamelGitHubCommitSha} by ${header.CamelGitHubCommitAuthor}")
    .to("direct:processCommit");
```

```xml
<route>
  <from uri="github2:commit/main?repoOwner=apache&amp;repoName=camel&amp;oauthToken=mytoken"/>
  <log message="New commit: ${header.CamelGitHubCommitSha} by ${header.CamelGitHubCommitAuthor}"/>
  <to uri="direct:processCommit"/>
</route>
```

```yaml
- route:
    from:
      uri: github2:commit/main
      parameters:
        repoOwner: apache
        repoName: camel
        oauthToken: mytoken
    steps:
      - log:
          message: "New commit: ${header.CamelGitHubCommitSha} by ${header.CamelGitHubCommitAuthor}"
      - to:
          uri: direct:processCommit
```

### Example: Creating an issue

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createIssue")
    .setHeader("CamelGitHubIssueTitle", constant("Bug Report"))
    .setBody(constant("This is the issue description"))
    .to("github2:createIssue?repoOwner=apache&repoName=camel&oauthToken=mytoken");
```

```xml
<route>
  <from uri="direct:createIssue"/>
  <setHeader name="CamelGitHubIssueTitle">
    <constant>Bug Report</constant>
  </setHeader>
  <setBody>
    <constant>This is the issue description</constant>
  </setBody>
  <to uri="github2:createIssue?repoOwner=apache&amp;repoName=camel&amp;oauthToken=mytoken"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createIssue
    steps:
      - setHeader:
          name: CamelGitHubIssueTitle
          constant: Bug Report
      - setBody:
          constant: This is the issue description
      - to:
          uri: github2:createIssue
          parameters:
            repoOwner: apache
            repoName: camel
            oauthToken: mytoken
```