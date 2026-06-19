# Docker

**Since Camel 2.15**

**Both producer and consumer are supported**

Camel component for communicating with Docker.

The Docker Camel component leverages the [docker-java](https://github.com/docker-java/docker-java) via the [Docker Remote API](https://docs.docker.com/reference/api/docker_remote_api).

## URI format

docker://\[operation\]?\[options\]

Where **operation** is the specific action to perform on Docker.

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

The Docker component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the shared docker configuration. |  | DockerConfiguration |
| **email** (common) | Email address associated with the user. |  | String |
| **host** (common) | **Required** Docker host. | localhost | String |
| **port** (common) | Docker port. | 2375 | Integer |
| **requestTimeout** (common) | Request timeout for response (in seconds). |  | Integer |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cmdExecFactory** (advanced) | The fully qualified class name of the DockerCmdExecFactory implementation to use. | com.github.dockerjava.netty.NettyDockerCmdExecFactory | String |
| **followRedirectFilter** (advanced) | Whether to follow redirect filter. | false | boolean |
| **loggingFilter** (advanced) | Whether to use logging filter. | false | boolean |
| **maxPerRouteConnections** (advanced) | Maximum route connections. | 100 | Integer |
| **maxTotalConnections** (advanced) | Maximum total connections. | 100 | Integer |
| **parameters** (advanced) | Additional configuration parameters as key/value pairs. |  | Map |
| **serverAddress** (advanced) | Server address for docker registry. | [https://index.docker.io/v1/](https://index.docker.io/v1/) | String |
| **socket** (advanced) | Socket connection mode. | true | boolean |
| **certPath** (security) | Location containing the SSL certificate chain. |  | String |
| **password** (security) | Password to authenticate with. |  | String |
| **secure** (security) | Use HTTPS communication. | false | boolean |
| **tlsVerify** (security) | Check TLS. | false | boolean |
| **username** (security) | User name to authenticate with. |  | String |

## Endpoint Options

The Docker endpoint is configured using URI syntax:

docker:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (common) | 
**Required** Which operation to use.

Enum values:

-   events
    
-   stats
    
-   auth
    
-   info
    
-   ping
    
-   version
    
-   imagebuild
    
-   imagecreate
    
-   imageinspect
    
-   imagelist
    
-   imagepull
    
-   imagepush
    
-   imageremove
    
-   imagesearch
    
-   imagetag
    
-   containerattach
    
-   containercommit
    
-   containercopyfile
    
-   containercreate
    
-   containerdiff
    
-   inspectcontainer
    
-   containerkill
    
-   containerlist
    
-   containerlog
    
-   containerpause
    
-   containerrestart
    
-   containerremove
    
-   containerstart
    
-   containerstop
    
-   containertop
    
-   containerunpause
    
-   containerwait
    
-   execcreate
    
-   execstart
    
-   networkconnect
    
-   networkcreate
    
-   networkremove
    





 |  | DockerOperation |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **email** (common) | Email address associated with the user. |  | String |
| **host** (common) | **Required** Docker host. | localhost | String |
| **port** (common) | Docker port. | 2375 | Integer |
| **requestTimeout** (common) | Request timeout for response (in seconds). |  | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cmdExecFactory** (advanced) | The fully qualified class name of the DockerCmdExecFactory implementation to use. | com.github.dockerjava.netty.NettyDockerCmdExecFactory | String |
| **followRedirectFilter** (advanced) | Whether to follow redirect filter. | false | boolean |
| **loggingFilter** (advanced) | Whether to use logging filter. | false | boolean |
| **maxPerRouteConnections** (advanced) | Maximum route connections. | 100 | Integer |
| **maxTotalConnections** (advanced) | Maximum total connections. | 100 | Integer |
| **parameters** (advanced) | Additional configuration parameters as key/value pairs. |  | Map |
| **serverAddress** (advanced) | Server address for docker registry. | [https://index.docker.io/v1/](https://index.docker.io/v1/) | String |
| **socket** (advanced) | Socket connection mode. | true | boolean |
| **certPath** (security) | Location containing the SSL certificate chain. |  | String |
| **password** (security) | Password to authenticate with. |  | String |
| **secure** (security) | Use HTTPS communication. | false | boolean |
| **tlsVerify** (security) | Check TLS. | false | boolean |
| **username** (security) | User name to authenticate with. |  | String |

## Message Headers

The Docker component supports 82 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDockerRequestTimeout** (common) Constant: [`DOCKER_API_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_API_REQUEST_TIMEOUT) | The request timeout for response (in seconds). |  | Integer |
| **CamelDockerCertPath** (common) Constant: [`DOCKER_CERT_PATH`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CERT_PATH) | The location containing the SSL certificate chain. |  | String |
| **CamelDockerHost** (common) Constant: [`DOCKER_HOST`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_HOST) | The docker host. |  | String |
| **CamelDockerPort** (common) Constant: [`DOCKER_PORT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PORT) | The docker port. |  | Integer |
| **CamelDockerMaxPerRouteConnections** (common) Constant: [`DOCKER_MAX_PER_ROUTE_CONNECTIONS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MAX_PER_ROUTE_CONNECTIONS) | The maximum route connections. |  | Integer |
| **CamelDockerMaxTotalConnections** (common) Constant: [`DOCKER_MAX_TOTAL_CONNECTIONS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MAX_TOTAL_CONNECTIONS) | The maximum total connections. |  | Integer |
| **CamelDockerSecure** (common) Constant: [`DOCKER_SECURE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SECURE) | Use HTTPS communication. | false | Boolean |
| **CamelDockerTlsVerify** (common) Constant: [`DOCKER_TLSVERIFY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TLSVERIFY) | Check TLS. | false | Boolean |
| **CamelDockerSocketEnabled** (common) Constant: [`DOCKER_SOCKET_ENABLED`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SOCKET_ENABLED) | Socket connection mode. | true | Boolean |
| **CamelDockerCmdExecFactory** (common) Constant: [`DOCKER_CMD_EXEC_FACTORY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CMD_EXEC_FACTORY) | The fully qualified class name of the DockerCmdExecFactory implementation to use. |  | String |
| **CamelDockerFilter** (common) Constant: [`DOCKER_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_FILTER) | With label filter. |  | String |
| **CamelDockerShowAll** (common) Constant: [`DOCKER_SHOW_ALL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SHOW_ALL) | With show all flag. |  | Boolean |
| **CamelDockerContainerId** (common) Constant: [`DOCKER_CONTAINER_ID`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CONTAINER_ID) | The id of the container. |  | String |
| **CamelDockerImageId** (common) Constant: [`DOCKER_IMAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_IMAGE_ID) | The Image ID. |  | String |
| **CamelDockerEmail** (common) Constant: [`DOCKER_EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_EMAIL) | The email address associated with the user. |  | String |
| **CamelDockerPassword** (common) Constant: [`DOCKER_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PASSWORD) | The password to authenticate with. |  | String |
| **CamelDockerServerAddress** (common) Constant: [`DOCKER_SERVER_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SERVER_ADDRESS) | The server address for docker registry. |  | String |
| **CamelDockerUsername** (common) Constant: [`DOCKER_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_USERNAME) | The user name to authenticate with. |  | String |
| **CamelDockerRegistry** (common) Constant: [`DOCKER_REGISTRY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REGISTRY) | The registry. |  | String |
| **CamelDockerRepository** (common) Constant: [`DOCKER_REPOSITORY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REPOSITORY) | The repository. |  | String |
| **CamelDockerTag** (common) Constant: [`DOCKER_TAG`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TAG) | The tag. |  | String |
| **CamelDockerName** (common) Constant: [`DOCKER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NAME) | The image name. |  | String |
| **CamelDockerTerm** (common) Constant: [`DOCKER_TERM`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TERM) | The term to search. |  | String |
| **CamelDockerForce** (common) Constant: [`DOCKER_FORCE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_FORCE) | With force flag. |  | Boolean |
| **CamelDockerNoPrune** (common) Constant: [`DOCKER_NO_PRUNE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NO_PRUNE) | With no prune flag. |  | Boolean |
| **CamelDockerInitialRange** (common) Constant: [`DOCKER_INITIAL_RANGE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_INITIAL_RANGE) | The initial range. |  | Long |
| **CamelDockerBefore** (common) Constant: [`DOCKER_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_BEFORE) | With before. |  | String |
| **CamelDockerLimit** (common) Constant: [`DOCKER_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_LIMIT) | With limit. |  | Integer |
| **CamelDockerShowSize** (common) Constant: [`DOCKER_SHOW_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SHOW_SIZE) | With show size flag. |  | Boolean |
| **CamelDockerSince** (common) Constant: [`DOCKER_SINCE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SINCE) | With since. |  | String |
| **CamelDockerRemoveVolumes** (common) Constant: [`DOCKER_REMOVE_VOLUMES`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REMOVE_VOLUMES) | With remove volumes flag. |  | Boolean |
| **CamelDockerFollowStream** (common) Constant: [`DOCKER_FOLLOW_STREAM`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_FOLLOW_STREAM) | With follow stream flag. |  | Boolean |
| **CamelDockerLogs** (common) Constant: [`DOCKER_LOGS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_LOGS) | With logs flag. |  | Boolean |
| **CamelDockerStdErr** (common) Constant: [`DOCKER_STD_ERR`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_STD_ERR) | With stdErr flag. |  | Boolean |
| **CamelDockerStdOut** (common) Constant: [`DOCKER_STD_OUT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_STD_OUT) | With stdOut flag. |  | Boolean |
| **CamelDockerTimestamps** (common) Constant: [`DOCKER_TIMESTAMPS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TIMESTAMPS) | With timestamps flag. |  | Boolean |
| **CamelDockerTail** (common) Constant: [`DOCKER_TAIL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TAIL) | With Tail. |  | Integer |
| **CamelDockerTailAll** (common) Constant: [`DOCKER_TAIL_ALL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TAIL_ALL) | With tail all flag. |  | Boolean |
| **CamelDockerHostPath** (common) Constant: [`DOCKER_HOST_PATH`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_HOST_PATH) | The host path. |  | String |
| **CamelDockerResource** (common) Constant: [`DOCKER_RESOURCE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_RESOURCE) | The resource. |  | String |
| **CamelDockerContainerIdDiff** (common) Constant: [`DOCKER_CONTAINER_ID_DIFF`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CONTAINER_ID_DIFF) | With container id for diff container request. |  | String |
| **CamelDockerTimeout** (common) Constant: [`DOCKER_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TIMEOUT) | With timeout. |  | Integer |
| **CamelDockerSignal** (common) Constant: [`DOCKER_SIGNAL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SIGNAL) | With signal. |  | String |
| **CamelDockerPsArgs** (common) Constant: [`DOCKER_PS_ARGS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PS_ARGS) | With ps args. |  | String |
| **CamelDockerNoCache** (common) Constant: [`DOCKER_NO_CACHE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NO_CACHE) | With no cache flag. |  | Boolean |
| **CamelDockerQuiet** (common) Constant: [`DOCKER_QUIET`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_QUIET) | With quiet flag. |  | Boolean |
| **CamelDockerRemove** (common) Constant: [`DOCKER_REMOVE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REMOVE) | With remove flag. |  | Boolean |
| **CamelDockerAttachStdErr** (common) Constant: [`DOCKER_ATTACH_STD_ERR`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_ATTACH_STD_ERR) | With attach StdErr flag. |  | Boolean |
| **CamelDockerAttachStdIn** (common) Constant: [`DOCKER_ATTACH_STD_IN`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_ATTACH_STD_IN) | With attach StdIn flag. |  | Boolean |
| **CamelDockerAttachStdOut** (common) Constant: [`DOCKER_ATTACH_STD_OUT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_ATTACH_STD_OUT) | With attach StdOut flag. |  | Boolean |
| **CamelDockerAuthor** (common) Constant: [`DOCKER_AUTHOR`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_AUTHOR) | The author. |  | String |
| **CamelDockerCmd** (common) Constant: [`DOCKER_CMD`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CMD) | With cmd. |  | String or String\[\] |
| **CamelDockerDisableNetwork** (common) Constant: [`DOCKER_DISABLE_NETWORK`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_DISABLE_NETWORK) | With disable network flag. |  | Boolean |
| **CamelDockerEnv** (common) Constant: [`DOCKER_ENV`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_ENV) | With env. |  | String or String\[\] |
| **CamelDockerExposedPorts** (common) Constant: [`DOCKER_EXPOSED_PORTS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_EXPOSED_PORTS) | The exposed ports. |  | ExposedPorts or ExposedPorts\[\] |
| **CamelDockerHostname** (common) Constant: [`DOCKER_HOSTNAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_HOSTNAME) | The hostname. |  | String |
| **CamelDockerMessage** (common) Constant: [`DOCKER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MESSAGE) | The message. |  | String |
| **CamelDockerMemory** (common) Constant: [`DOCKER_MEMORY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MEMORY) | With memory. |  | Integer |
| **CamelDockerMemorySwap** (common) Constant: [`DOCKER_MEMORY_SWAP`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MEMORY_SWAP) | With memory swap. |  | Long or Integer |
| **CamelDockerOpenStdIn** (common) Constant: [`DOCKER_OPEN_STD_IN`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_OPEN_STD_IN) | With open StdIn flag. |  | Boolean |
| **CamelDockerPause** (common) Constant: [`DOCKER_PAUSE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PAUSE) | With pause flag. |  | Boolean |
| **CamelDockerPortSpecs** (common) Constant: [`DOCKER_PORT_SPECS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PORT_SPECS) | With port specs. |  | String or String\[\] |
| **CamelDockerStdInOnce** (common) Constant: [`DOCKER_STD_IN_ONCE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_STD_IN_ONCE) | With StdIn in once flag. |  | Boolean |
| **CamelDockerTty** (common) Constant: [`DOCKER_TTY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TTY) | With TTY flag. |  | Boolean |
| **CamelDockerUser** (common) Constant: [`DOCKER_USER`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_USER) | With user. |  | String |
| **CamelDockerVolumes** (common) Constant: [`DOCKER_VOLUMES`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_VOLUMES) | With volumes. |  | Volume or Volume\[\] |
| **CamelDockerWorkingDir** (common) Constant: [`DOCKER_WORKING_DIR`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_WORKING_DIR) | With working directory. |  | String |
| **CamelDockerCpuShares** (common) Constant: [`DOCKER_CPU_SHARES`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CPU_SHARES) | With CPU shares. |  | Integer |
| **CamelDockerDns** (common) Constant: [`DOCKER_DNS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_DNS) | With dns. |  | String or String\[\] |
| **CamelDockerEntryPoint** (common) Constant: [`DOCKER_ENTRYPOINT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_ENTRYPOINT) | With entrypoint. |  | String or String\[\] |
| **CamelDockerHostConfig** (common) Constant: [`DOCKER_HOST_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_HOST_CONFIG) | With host config. |  | HostConfig |
| **CamelDockerImage** (common) Constant: [`DOCKER_IMAGE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_IMAGE) | The docker image. |  | String |
| **CamelDockerMemoryLimit** (common) Constant: [`DOCKER_MEMORY_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MEMORY_LIMIT) | With memory limit. |  | Long |
| **CamelDockerStdInOpen** (common) Constant: [`DOCKER_STD_IN_OPEN`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_STD_IN_OPEN) | With StdIn in open flag. |  | Boolean |
| **CamelDockerVolumesFrom** (common) Constant: [`DOCKER_VOLUMES_FROM`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_VOLUMES_FROM) | With volumes from. |  | VolumesFrom or VolumesFrom\[\] |
| **CamelDockerDomainName** (common) Constant: [`DOCKER_DOMAIN_NAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_DOMAIN_NAME) | With domain name. |  | String |
| **CamelDockerBinds** (common) Constant: [`DOCKER_BINDS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_BINDS) | With binds. |  | Bind or Bind\[\] |
| **CamelDockerCapAdd** (common) Constant: [`DOCKER_CAP_ADD`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CAP_ADD) | With cap add. |  | Capability or Capability\[\] |
| **CamelDockerCapDrop** (common) Constant: [`DOCKER_CAP_DROP`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CAP_DROP) | With cap drop. |  | Capability or Capability\[\] |
| **CamelDockerNetwork** (common) Constant: [`DOCKER_NETWORK`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NETWORK) | The network name. |  | String |
| **CamelDockerDetach** (common) Constant: [`DOCKER_DETACH`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_DETACH) | With detach flag. |  | Boolean |
| **CamelDockerExecId** (common) Constant: [`DOCKER_EXEC_ID`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_EXEC_ID) | The Exec ID. |  | String |

## Usage

### Header Strategy

All URI options can be passed as Header properties. Values found in a message header take precedence over URI parameters. A header property takes the form of a URI option prefixed with **CamelDocker** as shown below

 
| URI Option | Header Property |
| --- | --- |
| containerId | CamelDockerContainerId |

## Examples

The following example consumes events from Docker:

-   Java
    
-   XML
    
-   YAML
    

```java
from("docker://events?host=192.168.59.103&port=2375").to("log:event");
```

```xml
<route>
  <from uri="docker://events?host=192.168.59.103&amp;port=2375"/>
  <to uri="log:event"/>
</route>
```

```yaml
- route:
    from:
      uri: docker://events
      parameters:
        host: 192.168.59.103
        port: 2375
      steps:
        - to:
            uri: log:event
```

The following example queries Docker for system-wide information

-   Java
    
-   XML
    
-   YAML
    

```java
from("docker://info?host=192.168.59.103&port=2375").to("log:info");
```

```xml
<route>
  <from uri="docker://info?host=192.168.59.103&amp;port=2375"/>
  <to uri="log:info"/>
</route>
```

```yaml
- route:
    from:
      uri: docker://info
      parameters:
        host: 192.168.59.103
        port: 2375
      steps:
        - to:
            uri: log:info
```

## Dependencies

To use Docker in your Camel routes, you need to add a dependency on **camel-docker**, which implements the component.

If you use Maven, you can add the following to your pom.xml, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-docker</artifactId>
  <version>x.x.x</version>
</dependency>
```