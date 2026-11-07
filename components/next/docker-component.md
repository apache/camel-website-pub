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

The Docker component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the shared docker configuration. |  | DockerConfiguration |
| **email** (common) | Email address associated with the user. |  | String |
| **host** (common) | **Required** Docker host. In socket mode (socket=true), the path of the unix socket of the Docker daemon, where the default localhost means /var/run/docker.sock. A host with a tcp:// or unix:// scheme (such as tcp://myhost:2376 or unix:///var/run/docker.sock) is used as is, and then the port and socket options are not used. | localhost | String |
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
| **socket** (advanced) | Socket connection mode. When enabled, connects to the unix socket of the Docker daemon, whose path is given by the host option (the default localhost means /var/run/docker.sock), and the port is not used. When disabled, connects over TCP to the host and port. | false | boolean |
| **allowConnectionAndCredentialsFromHeaders** (security) | Whether to allow overriding the connection and credential settings of the endpoint with the CamelDockerHost, CamelDockerPort, CamelDockerSocketEnabled, CamelDockerSecure, CamelDockerTlsVerify, CamelDockerCertPath, CamelDockerCmdExecFactory, CamelDockerUsername, CamelDockerPassword and CamelDockerServerAddress headers. Disabled by default; enable it only when the header source is trusted, since it lets a message choose the Docker daemon that the client connects to and how, and the registry that receives the username and password of the endpoint. | false | boolean |
| **certPath** (security) | Location containing the SSL certificate chain. |  | String |
| **password** (security) | Password to authenticate with. |  | String |
| **secure** (security) | Use HTTPS communication. | false | boolean |
| **tlsVerify** (security) | Check TLS. | false | boolean |
| **username** (security) | User name to authenticate with. |  | String |

## Endpoint Options

The Docker endpoint is configured using URI syntax:

docker:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
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

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **email** (common) | Email address associated with the user. |  | String |
| **host** (common) | **Required** Docker host. In socket mode (socket=true), the path of the unix socket of the Docker daemon, where the default localhost means /var/run/docker.sock. A host with a tcp:// or unix:// scheme (such as tcp://myhost:2376 or unix:///var/run/docker.sock) is used as is, and then the port and socket options are not used. | localhost | String |
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
| **socket** (advanced) | Socket connection mode. When enabled, connects to the unix socket of the Docker daemon, whose path is given by the host option (the default localhost means /var/run/docker.sock), and the port is not used. When disabled, connects over TCP to the host and port. | false | boolean |
| **allowConnectionAndCredentialsFromHeaders** (security) | Whether to allow overriding the connection and credential settings of the endpoint with the CamelDockerHost, CamelDockerPort, CamelDockerSocketEnabled, CamelDockerSecure, CamelDockerTlsVerify, CamelDockerCertPath, CamelDockerCmdExecFactory, CamelDockerUsername, CamelDockerPassword and CamelDockerServerAddress headers. Disabled by default; enable it only when the header source is trusted, since it lets a message choose the Docker daemon that the client connects to and how, and the registry that receives the username and password of the endpoint. | false | boolean |
| **certPath** (security) | Location containing the SSL certificate chain. |  | String |
| **password** (security) | Password to authenticate with. |  | String |
| **secure** (security) | Use HTTPS communication. | false | boolean |
| **tlsVerify** (security) | Check TLS. | false | boolean |
| **username** (security) | User name to authenticate with. |  | String |

## Message Headers

The Docker component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDockerRequestTimeout** (common) Constant: [`DOCKER_API_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_API_REQUEST_TIMEOUT) | The request timeout for response (in seconds). |  | Integer |
| **CamelDockerCertPath** (common) Constant: [`DOCKER_CERT_PATH`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CERT_PATH) | The location containing the SSL certificate chain. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerHost** (common) Constant: [`DOCKER_HOST`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_HOST) | The docker host. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerPort** (common) Constant: [`DOCKER_PORT`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PORT) | The docker port. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | Integer |
| **CamelDockerMaxPerRouteConnections** (common) Constant: [`DOCKER_MAX_PER_ROUTE_CONNECTIONS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MAX_PER_ROUTE_CONNECTIONS) | The maximum route connections. |  | Integer |
| **CamelDockerMaxTotalConnections** (common) Constant: [`DOCKER_MAX_TOTAL_CONNECTIONS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_MAX_TOTAL_CONNECTIONS) | The maximum total connections. |  | Integer |
| **CamelDockerSecure** (common) Constant: [`DOCKER_SECURE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SECURE) | Use HTTPS communication. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). | false | Boolean |
| **CamelDockerTlsVerify** (common) Constant: [`DOCKER_TLSVERIFY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TLSVERIFY) | Check TLS. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). | false | Boolean |
| **CamelDockerSocketEnabled** (common) Constant: [`DOCKER_SOCKET_ENABLED`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SOCKET_ENABLED) | Socket connection mode: connect to the unix socket of the Docker daemon, whose path is given by the host (the default localhost means /var/run/docker.sock). This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). | false | Boolean |
| **CamelDockerCmdExecFactory** (common) Constant: [`DOCKER_CMD_EXEC_FACTORY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CMD_EXEC_FACTORY) | The fully qualified class name of the DockerCmdExecFactory implementation to use. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerFilter** (common) Constant: [`DOCKER_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_FILTER) | With label filter. |  | String |
| **CamelDockerShowAll** (common) Constant: [`DOCKER_SHOW_ALL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SHOW_ALL) | With show all flag. |  | Boolean |
| **CamelDockerContainerId** (common) Constant: [`DOCKER_CONTAINER_ID`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_CONTAINER_ID) | The id of the container. |  | String |
| **CamelDockerImageId** (common) Constant: [`DOCKER_IMAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_IMAGE_ID) | The Image ID. |  | String |
| **CamelDockerEmail** (common) Constant: [`DOCKER_EMAIL`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_EMAIL) | The email address associated with the user. |  | String |
| **CamelDockerPassword** (common) Constant: [`DOCKER_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_PASSWORD) | The password to authenticate with. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerServerAddress** (common) Constant: [`DOCKER_SERVER_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_SERVER_ADDRESS) | The server address for docker registry. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerUsername** (common) Constant: [`DOCKER_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_USERNAME) | The user name to authenticate with. This header is ignored unless the endpoint enables allowConnectionAndCredentialsFromHeaders=true (disabled by default). |  | String |
| **CamelDockerRegistry** (common) Constant: [`DOCKER_REGISTRY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REGISTRY) | The registry. |  | String |
| **CamelDockerRepository** (common) Constant: [`DOCKER_REPOSITORY`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_REPOSITORY) | The repository. |  | String |
| **CamelDockerTag** (common) Constant: [`DOCKER_TAG`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TAG) | The tag. |  | String |
| **CamelDockerName** (common) Constant: [`DOCKER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NAME) | The image name. |  | String |
| **CamelDockerTerm** (common) Constant: [`DOCKER_TERM`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_TERM) | The term to search. |  | String |
| **CamelDockerForce** (common) Constant: [`DOCKER_FORCE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_FORCE) | With force flag. |  | Boolean |
| **CamelDockerNoPrune** (common) Constant: [`DOCKER_NO_PRUNE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_NO_PRUNE) | With no prune flag. |  | Boolean |
| **CamelDockerInitialRange** (common) Constant: [`DOCKER_INITIAL_RANGE`](https://javadoc.io/doc/org.apache.camel/camel-docker/latest/org/apache/camel/component/docker/DockerConstants.html#DOCKER_INITIAL_RANGE) | The time in milliseconds before the start of the events consumer from which it also receives the past events. |  | Long |
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

## Message Body

The message body at each side of the Docker component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `pojo` | 
The object of docker-java for each item of the stream: an Event of the daemon with events, the Statistics of the container in CamelDockerContainerId with stats.

-   With `operation=events`: `pojo` (`com.github.dockerjava.api.model.Event`)
    
-   With `operation=stats`: `pojo` (`com.github.dockerjava.api.model.Statistics`)
    





 |
| **Producer input** | `any` | 

Not used by most operations, which take their input from the options and headers, such as the container in CamelDockerContainerId. imagecreate reads the image as a stream; imagebuild needs the build context as a tar archive (an InputStream, a byte\[\] or another body that converts to an InputStream) or as a java.io.File of the Dockerfile or its directory, and fails without one.

-   With `operation=imagecreate`: `stream`, `bytes`, `text` or `file`
    
-   With `operation=imagebuild`: `stream`, `bytes` or `file`
    





 |
| **Producer output** | `pojo`, `list`, `text`, `stream`, `value` or `unchanged` | 

The response of docker-java for the operation, such as the Version of version and a List of Containers for containerlist; the operations without a response, such as ping and containerstart, keep the body. The streaming operations wait until the stream is done: containerattach, containerlog and execstart give the output of stdout and stderr as text, containerwait the exit code of the container, imagebuild the id of the built image, imagepull and imagepush the last item of the progress; a failed build, pull or push fails the exchange.

-   With `operation=auth`: `pojo` (`com.github.dockerjava.api.model.AuthResponse`)
    
-   With `operation=info`: `pojo` (`com.github.dockerjava.api.model.Info`)
    
-   With `operation=ping`: `unchanged`
    
-   With `operation=version`: `pojo` (`com.github.dockerjava.api.model.Version`)
    
-   With `operation=imagebuild`: `text` (`java.lang.String`)
    
-   With `operation=imagecreate`: `pojo` (`com.github.dockerjava.api.command.CreateImageResponse`)
    
-   With `operation=imageinspect`: `pojo` (`com.github.dockerjava.api.command.InspectImageResponse`)
    
-   With `operation=imagelist`: `list`
    
-   With `operation=imagepull`: `pojo` (`com.github.dockerjava.api.model.PullResponseItem`)
    
-   With `operation=imagepush`: `pojo` (`com.github.dockerjava.api.model.PushResponseItem`)
    
-   With `operation=imageremove`: `unchanged`
    
-   With `operation=imagesearch`: `list`
    
-   With `operation=imagetag`: `unchanged`
    
-   With `operation=containerattach`: `text` (`java.lang.String`)
    
-   With `operation=containercommit`: `text` (`java.lang.String`)
    
-   With `operation=containercopyfile`: `stream`
    
-   With `operation=containercreate`: `pojo` (`com.github.dockerjava.api.command.CreateContainerResponse`)
    
-   With `operation=containerdiff`: `list`
    
-   With `operation=inspectcontainer`: `pojo` (`com.github.dockerjava.api.command.InspectContainerResponse`)
    
-   With `operation=containerkill`: `unchanged`
    
-   With `operation=containerlist`: `list`
    
-   With `operation=containerlog`: `text` (`java.lang.String`)
    
-   With `operation=containerpause`: `unchanged`
    
-   With `operation=containerrestart`: `unchanged`
    
-   With `operation=containerremove`: `unchanged`
    
-   With `operation=containerstart`: `unchanged`
    
-   With `operation=containerstop`: `unchanged`
    
-   With `operation=containertop`: `pojo` (`com.github.dockerjava.api.command.TopContainerResponse`)
    
-   With `operation=containerunpause`: `unchanged`
    
-   With `operation=containerwait`: `value` (`java.lang.Integer`)
    
-   With `operation=execcreate`: `pojo` (`com.github.dockerjava.api.command.ExecCreateCmdResponse`)
    
-   With `operation=execstart`: `text` (`java.lang.String`)
    
-   With `operation=networkconnect`: `unchanged`
    
-   With `operation=networkcreate`: `pojo` (`com.github.dockerjava.api.command.CreateNetworkResponse`)
    
-   With `operation=networkremove`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Connecting to the Docker daemon

By default, the component connects over TCP to `host` and `port` (`tcp://localhost:2375`). Docker does not open this TCP port by default; it has to be enabled in the configuration of the daemon.

To connect to the local unix socket of the daemon instead, set `socket=true`. In socket mode `host` is the path of the socket and `port` is not used. The default host `localhost` means `/var/run/docker.sock`:

```java
from("timer:info?repeatCount=1")
    .to("docker:info?socket=true")
    .log("${body}");
```

For a socket in another place, set its path as the host, for example `docker:info?socket=true&host=/run/user/1000/docker.sock`.

The host can also be a full Docker host URL with a `tcp://` or `unix://` scheme, in the same form as the `DOCKER_HOST` environment variable, such as `tcp://myhost:2376` or `unix:///var/run/docker.sock`. Such a host is used as is, and the `port` and `socket` options are not used. Windows named pipes (`npipe://`) are not supported by the Docker client of the component.

### Header Strategy

All URI options can be passed as Header properties. Values found in a message header take precedence over URI parameters. A header property takes the form of a URI option prefixed with **CamelDocker** as shown below

 
| URI Option | Header Property |
| --- | --- |
| containerId | CamelDockerContainerId |

The headers of the connection and credential settings are the exception: `CamelDockerHost`, `CamelDockerPort`, `CamelDockerSocketEnabled`, `CamelDockerSecure`, `CamelDockerTlsVerify`, `CamelDockerCertPath`, `CamelDockerCmdExecFactory`, `CamelDockerUsername`, `CamelDockerPassword` and `CamelDockerServerAddress` are ignored unless the endpoint sets `allowConnectionAndCredentialsFromHeaders=true`. Without this option, the producer connects to the Docker daemon of the endpoint, in the way the endpoint configures, and gives the username and password of the endpoint to the registry of the endpoint, whatever the headers of the message say.

Enable `allowConnectionAndCredentialsFromHeaders` only when the headers come from a trusted source, since with it a message chooses the Docker daemon that the client connects to and how (TLS, the client certificates and the `DockerCmdExecFactory` class), and the registry that receives the username and password of the endpoint. Set on the component, the option applies to all its endpoints.

The other headers, such as `CamelDockerContainerId`, still take precedence over the options of the endpoint. When the messages come from an untrusted producer through a consumer that does not filter out `Camel*` headers, remove these headers with `removeHeaders("CamelDocker*")` before the `docker` endpoint.

### Registry authentication

The `imagepull` and `imagepush` operations send the `username`, `password` and `email` of the endpoint only for an image in the registry of `serverAddress`: the registry host and port of the image reference must match those of `serverAddress`. An image reference without a registry host, such as `ubuntu` or `team/app`, is on Docker Hub, which matches the default `serverAddress` (`[https://index.docker.io/v1/](https://index.docker.io/v1/)`). An image in another registry is pulled or pushed without authentication, and so is every image when the endpoint has no `username`. To pull or push with authentication from several registries, use one endpoint per registry.

### Streaming operations

The operations `imagebuild`, `imagepull`, `imagepush`, `containerattach`, `containerlog`, `containerwait` and `execstart` wait until Docker has finished, and set the result as the message body:

-   `imagebuild`: the id of the built image. The body is the build context: a tar archive as an `InputStream`, a `byte[]` or another body that converts to an `InputStream`, or a `java.io.File` of the Dockerfile or its directory.
    
-   `containerattach`, `containerlog` and `execstart`: the output of stdout and stderr as a `String`.
    
-   `containerwait`: the exit code of the container as an `Integer`.
    
-   `imagepull` and `imagepush`: the last `PullResponseItem` or `PushResponseItem` of the progress.
    

When the operation fails, for example a build step that fails, the exchange fails.

> **Note**
> With `followStream=true`, `containerattach` and `containerlog` wait until the container stops.

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