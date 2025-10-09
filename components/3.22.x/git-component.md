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

The producer allows to do operations on a specific repository.  
The consumer allows consuming commits, tags and branches on a specific repository.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Git component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Git endpoint is configured using URI syntax:

git:localPath

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **localPath** (common) | **Required** Local repository path. |  | String |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **branchName** (common) | The branch name to work on. |  | String |
| **type** (consumer) | 
The consumer type.

Enum values:

-   commit
    
-   tag
    
-   branch
    





 |  | GitType |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **allowEmpty** (producer) | The flag to manage empty git commits. | true | boolean |
| **operation** (producer) | 

The operation to do on the repository.

Enum values:

-   clone
    
-   init
    
-   add
    
-   remove
    
-   commit
    
-   commitAll
    
-   createBranch
    
-   deleteBranch
    
-   createTag
    
-   deleteTag
    
-   status
    
-   log
    
-   push
    
-   pull
    
-   showBranches
    
-   cherryPick
    
-   remoteAdd
    
-   remoteList
    





 |  | String |
| **password** (producer) | Remote repository password. |  | String |
| **remoteName** (producer) | The remote repository name to use in particular operation like pull. |  | String |
| **remotePath** (producer) | The remote repository path. |  | String |
| **tagName** (producer) | The tag name to work on. |  | String |
| **targetBranchName** (producer) | Name of target branch in merge operation. If not supplied will try to use init.defaultBranch git configs. If not configured will use default value. | master | String |
| **username** (producer) | Remote repository username. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **gitConfigFile** (advanced) | A String with path to a .gitconfig file. |  | String |

## Message Headers

The Git component supports 12 message header(s), which is/are listed below:

   
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
| **CamelGitBranchLeaf** (consumer) Constant: [`GIT_BRANCH_LEAF`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_BRANCH_LEAF) | The leaf. |  | String |
| **CamelGitBranchObjectId** (consumer) Constant: [`GIT_BRANCH_OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-git/latest/org/apache/camel/component/git/GitConstants.html#GIT_BRANCH_OBJECT_ID) | The object id. |  | String |

## Producer Example

Below is an example route of a producer that add a file test.java to a local repository, commit it with a specific message on master branch and then push it to remote repository.

```java
from("direct:start")
    .setHeader(GitConstants.GIT_FILE_NAME, constant("test.java"))
    .to("git:///tmp/testRepo?operation=add")
    .setHeader(GitConstants.GIT_COMMIT_MESSAGE, constant("first commit"))
    .to("git:///tmp/testRepo?operation=commit")
    .to("git:///tmp/testRepo?operation=push&remotePath=https://foo.com/test/test.git&username=xxx&password=xxx")
    .to("git:///tmp/testRepo?operation=createTag&tagName=myTag")
    .to("git:///tmp/testRepo?operation=pushTag&tagName=myTag&remoteName=origin")
```

## Consumer Example

Below is an example route of a consumer that consumes commit:

```java
from("git:///tmp/testRepo?type=commit")
    .to(....)
```

## Custom config file

By default camel-git will load `.gitconfig` file from user home folder. You can override this by providing your own `.gitconfig` file.

```java
from("git:///tmp/testRepo?type=commit&gitConfigFile=file:/tmp/configfile")
    .to(....) //will load from os dirs

from("git:///tmp/testRepo?type=commit&gitConfigFile=classpath:configfile")
    .to(....) //will load from resources dir

from("git:///tmp/testRepo?type=commit&gitConfigFile=http://somedomain.xyz/gitconfigfile")
    .to(....) //will load from http. You could also use https
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

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.git.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.git.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.git.enabled** | Whether to enable auto configuration of the git component. This is enabled by default. |  | Boolean |
| **camel.component.git.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |