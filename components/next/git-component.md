# Git

**Since Camel 2.16**

**Both producer and consumer are supported**

The Git component allows you to work with a generic Git repository.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-git</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

**URI Format**

git://localRepositoryPath\[?options\]

## URI Options

The producer allows doing operations on a specific repository. The consumer allows consuming commits, tags, and branches in a specific repository.

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

The Git component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Git endpoint is configured using URI syntax:

git:localPath

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **localPath** (common) | **Required** Local repository path. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **branchName** (common) | The branch name to work on. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **type** (consumer) | 
The consumer type.

Enum values:

-   commit
    
-   tag
    
-   branch
    





 |  | GitType |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **allowEmpty** (producer) | The flag to manage empty git commits. | true | boolean |
| **depth** (producer) | Clone depth for shallow clones. Must be a positive integer. A value of 1 fetches only the latest commit. When set to 0 or not specified, a full clone is performed. |  | int |
| **operation** (producer) | 

The operation to do on the repository.

Enum values:

-   add
    
-   cherryPick
    
-   clean
    
-   clone
    
-   commit
    
-   commitAll
    
-   createBranch
    
-   createTag
    
-   deleteBranch
    
-   deleteTag
    
-   gc
    
-   init
    
-   log
    
-   pull
    
-   push
    
-   remoteAdd
    
-   remoteList
    
-   remove
    
-   showBranches
    
-   showTags
    
-   status
    





 |  | String |
| **remoteName** (producer) | The remote repository name to use in particular operation like pull. |  | String |
| **remotePath** (producer) | The remote repository path. |  | String |
| **tagName** (producer) | The tag name to work on. |  | String |
| **targetBranchName** (producer) | Name of target branch in merge operation. If not supplied will try to use init.defaultBranch git configs. If not configured will use default value. | master | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **gitConfigFile** (advanced) | A String with path to a .gitconfig file. |  | String |
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
| **password** (security) | Remote repository password. |  | String |
| **username** (security) | Remote repository username. |  | String |

## Message Headers

The Git component supports 13 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGitOperation** (producer) Constant: [`GIT_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_OPERATION) | The operation to do on a repository, if not specified as endpoint option. |  | String |
| **CamelGitFilename** (producer) Constant: [`GIT_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_FILE_NAME) | The file name in an add operation. |  | String |
| **CamelGitCommitMessage** (producer) Constant: [`GIT_COMMIT_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_MESSAGE) | The commit message related in a commit operation. |  | String |
| **CamelGitCommitUsername** (producer) Constant: [`GIT_COMMIT_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_USERNAME) | The commit username in a commit operation. |  | String |
| **CamelGitCommitEmail** (producer) Constant: [`GIT_COMMIT_EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_EMAIL) | The commit email in a commit operation. |  | String |
| **CamelGitCommitId** (common) Constant: [`GIT_COMMIT_ID`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_ID) | The commit id. |  | String |
| **CamelGitAllowEmpty** (producer) Constant: [`GIT_ALLOW_EMPTY`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_ALLOW_EMPTY) | The flag to manage empty git commits. |  | Boolean |
| **CamelGitAuthorName** (consumer) Constant: [`GIT_COMMIT_AUTHOR_NAME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_AUTHOR_NAME) | The author name. |  | String |
| **CamelGitCommiterName** (consumer) Constant: [`GIT_COMMIT_COMMITTER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_COMMITTER_NAME) | The committer name. |  | String |
| **CamelGitCommitTime** (consumer) Constant: [`GIT_COMMIT_TIME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_COMMIT_TIME) | The commit time. |  | int |
| **CamelGitBranchName** (consumer) Constant: [`GIT_BRANCH_NAME`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_BRANCH_NAME) | The branch/tag name. |  | String |
| **CamelGitBranchLeaf** (consumer) Constant: [`GIT_BRANCH_LEAF`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_BRANCH_LEAF) | The leaf. |  | String |
| **CamelGitBranchObjectId** (consumer) Constant: [`GIT_BRANCH_OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_BRANCH_OBJECT_ID) | The object id. |  | String |

## Examples

### Producer Example

Below is an example route of a producer that adds a file test.java to a local repository, commits it with a specific message on the `main` branch and then pushes it to remote repository.

_Java-only: setting headers with GitConstants and chaining multiple git operations_

```java
from("direct:start")
    .setHeader(GitConstants.GIT_FILE_NAME, constant("test.java"))
    .to("git:///tmp/testRepo?operation=add")
    .setHeader(GitConstants.GIT_COMMIT_MESSAGE, constant("first commit"))
    .to("git:///tmp/testRepo?operation=commit")
    .to("git:///tmp/testRepo?operation=push&remotePath=https://foo.com/test/test.git&username=xxx&password=xxx")
    .to("git:///tmp/testRepo?operation=createTag&tagName=myTag")
    .to("git:///tmp/testRepo?operation=pushTag&tagName=myTag&remoteName=origin");
```

### Consumer Example

Below is an example route of a consumer that consumes commit:

-   Java
    
-   XML
    
-   YAML
    

```java
from("git:///tmp/testRepo?type=commit")
    .to("mock:result");
```

```xml
<route>
  <from uri="git:///tmp/testRepo?type=commit"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: git:///tmp/testRepo
      parameters:
        type: commit
      steps:
        - to:
            uri: mock:result
```

### Shallow Clone

Use the `depth` option to perform a shallow clone, fetching only a limited number of commits. This reduces clone time and disk usage for large repositories when full history is not needed.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:clone")
    .to("git:///tmp/myRepo?operation=clone&remotePath=https://github.com/example/repo.git&depth=1");
```

```xml
<route>
  <from uri="direct:clone"/>
  <to uri="git:///tmp/myRepo?operation=clone&amp;remotePath=https://github.com/example/repo.git&amp;depth=1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:clone
      steps:
        - to:
            uri: git:///tmp/myRepo
            parameters:
              operation: clone
              remotePath: "https://github.com/example/repo.git"
              depth: 1
```

A `depth` of 1 fetches only the latest commit. The value must be a positive integer. When set to 0 or omitted, a full clone is performed.

### Custom config file

By default, camel-git will load `.gitconfig` file from user home folder. You can override this by providing your own `.gitconfig` file.

_Java-only: configuring custom gitConfigFile with different resource schemes_

```java
from("git:///tmp/testRepo?type=commit&gitConfigFile=file:/tmp/configfile")
    .to(....); // will load from os dirs

from("git:///tmp/testRepo?type=commit&gitConfigFile=classpath:configfile")
    .to(....); // will load from resources dir

from("git:///tmp/testRepo?type=commit&gitConfigFile=http://somedomain.xyz/gitconfigfile")
    .to(....); // will load from http. You could also use https
```

## Spring Boot Auto-Configuration

When using git with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-git-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.git.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.git.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.git.enabled** | Whether to enable auto configuration of the git component. This is enabled by default. |  | Boolean |
| **camel.component.git.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.git.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.git.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |