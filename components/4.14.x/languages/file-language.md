# File

**Since Camel 1.1**

The File Expression Language is an extension to the [Simple](simple-language.md) language, adding file related capabilities. These capabilities are related to common use cases working with file path and names. The goal is to allow expressions to be used with the [File](../../4.18.x/file-component.md) and [FTP](../../4.18.x/ftp-component.md) components for setting dynamic file patterns for both consumer and producer.

> **Note**
> The file language is merged with [Simple](simple-language.md) language, which means you can use all the file syntax directly within the simple language.

## File Language options

The File language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Syntax

This language is an **extension** to the [Simple](simple-language.md) language, so the [Simple](simple-language.md) syntax applies also. So the table below only lists the additional file related functions.

All the file tokens use the same expression name as the method on the `java.io.File` object, for instance `file:absolute` refers to the `java.io.File.getAbsolute()` method. Notice that not all expressions are supported by the current Exchange. For instance, the [FTP](../../4.18.x/ftp-component.md) component supports some options, whereas the File component supports all of them.

      
| Expression | Type | File Consumer | File Producer | FTP Consumer | FTP Producer | Description |
| --- | --- | --- | --- | --- | --- | --- |
| file:name | String | yes | no | yes | no | refers to the file name (is relative to the starting directory, see note below) |
| file:name.ext | String | yes | no | yes | no | refers to the file extension only |
| file:name.ext.single | String | yes | no | yes | no | refers to the file extension. If the file extension has multiple dots, then this expression strips and only returns the last part. |
| file:name.noext | String | yes | no | yes | no | refers to the file name with no extension (is relative to the starting directory, see note below) |
| file:name.noext.single | String | yes | no | yes | no | refers to the file name with no extension (is relative to the starting directory, see note below). If the file name has multiple dots, then this expression strips only the last part, and keeps the others. |
| file:onlyname | String | yes | no | yes | no | refers to the file name only with no leading paths. |
| file:onlyname.noext | String | yes | no | yes | no | refers to the file name only with no extension and with no leading paths. |
| file:onlyname.noext.single | String | yes | no | yes | no | refers to the file name only with no extension and with no leading paths. If the file extension has multiple dots, then this expression strips only the last part, and keeps the others. |
| file:ext | String | yes | no | yes | no | refers to the file extension only |
| file:parent | String | yes | no | yes | no | refers to the file parent |
| file:path | String | yes | no | yes | no | refers to the file path |
| file:absolute | Boolean | yes | no | no | no | refers to whether the file is regarded as absolute or relative |
| file:absolute.path | String | yes | no | no | no | refers to the absolute file path |
| file:length | Long | yes | no | yes | no | refers to the file length returned as a Long type |
| file:size | Long | yes | no | yes | no | refers to the file length returned as a Long type |
| file:modified | Date | yes | no | yes | no | Refers to the file last modified returned as a Date type |
| date:\_command:pattern\_ | String | yes | yes | yes | yes | for date formatting using the `java.text.SimpleDateFormat` patterns. Is an **extension** to the [Simple](simple-language.md) language. Additional command is: **file** (consumers only) for the last modified timestamp of the file. Notice: all the commands from the [Simple](simple-language.md) language can also be used. |

## File token example

### Relative paths

We have a `java.io.File` handle for the file `hello.txt` in the following **relative** directory: `./filelanguage/test`. And we configure our endpoint to use this starting directory `./filelanguage`. The file tokens will return as:

 
| Expression | Returns |
| --- | --- |
| file:name | test/hello.txt |
| file:name.ext | txt |
| file:name.noext | test/hello |
| file:onlyname | hello.txt |
| file:onlyname.noext | hello |
| file:ext | txt |
| file:parent | filelanguage/test |
| file:path | filelanguage/test/hello.txt |
| file:absolute | false |
| file:absolute.path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |

### Absolute paths

We have a `java.io.File` handle for the file `hello.txt` in the following **absolute** directory: `/workspace/camel/camel-core/target/filelanguage/test`. And we configure the out endpoint to use the absolute starting directory `/workspace/camel/camel-core/target/filelanguage`. The file tokens will return as:

 
| Expression | Returns |
| --- | --- |
| file:name | test/hello.txt |
| file:name.ext | txt |
| file:name.noext | test/hello |
| file:onlyname | hello.txt |
| file:onlyname.noext | hello |
| file:ext | txt |
| file:parent | /workspace/camel/camel-core/target/filelanguage/test |
| file:path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |
| file:absolute | true |
| file:absolute.path | /workspace/camel/camel-core/target/filelanguage/test/hello.txt |

## Examples

You can enter a fixed file name such as `myfile.txt`:

```properties
fileName="myfile.txt"
```

Let’s assume we use the file consumer to read files and want to move the read files to back up folder with the current date as a subfolder. This can be done using an expression like:

```properties
fileName="backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"
```

relative folder names are also supported so suppose the backup folder should be a sibling folder then you can append `..` as shown:

```properties
fileName="../backup/${date:now:yyyyMMdd}/${file:name.noext}.bak"
```

As this is an extension to the [Simple](simple-language.md) language, we have access to all the goodies from this language also, so in this use case we want to use the in.header.type as a parameter in the dynamic expression:

```properties
fileName="../backup/${date:now:yyyyMMdd}/type-${in.header.type}/backup-of-${file:name.noext}.bak"
```

If you have a custom date you want to use in the expression, then Camel supports retrieving dates from the message header:

```properties
fileName="orders/order-${in.header.customerId}-${date:in.header.orderDate:yyyyMMdd}.xml"
```

And finally, we can also use a bean expression to invoke a POJO class that generates some String output (or convertible to String) to be used:

```properties
fileName="uniquefile-${bean:myguidgenerator.generateid}.txt"
```

Of course, all this can be combined in one expression where you can use the [File Language](#), [Simple](#) and the [Bean](../../4.18.x/bean-component.md) language in one combined expression. This is pretty powerful for those common file path patterns.

## Dependencies

The File language is part of **camel-core**.

## Spring Boot Auto-Configuration

When using file with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-core-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 114 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.cloud.consul.service-discovery.acl-token** | Sets the ACL token to be used with Consul. |  | String |
| **camel.cloud.consul.service-discovery.block-seconds** | The seconds to wait for a watch event, default 10 seconds. | 10 | Integer |
| **camel.cloud.consul.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.consul.service-discovery.connect-timeout-millis** | Connect timeout for OkHttpClient. |  | Long |
| **camel.cloud.consul.service-discovery.datacenter** | The data center. |  | String |
| **camel.cloud.consul.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.consul.service-discovery.password** | Sets the password to be used for basic authentication. |  | String |
| **camel.cloud.consul.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.consul.service-discovery.read-timeout-millis** | Read timeout for OkHttpClient. |  | Long |
| **camel.cloud.consul.service-discovery.url** | The Consul agent URL. |  | String |
| **camel.cloud.consul.service-discovery.user-name** | Sets the username to be used for basic authentication. |  | String |
| **camel.cloud.consul.service-discovery.write-timeout-millis** | Write timeout for OkHttpClient. |  | Long |
| **camel.cloud.dns.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.dns.service-discovery.domain** | The domain name;. |  | String |
| **camel.cloud.dns.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.dns.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.dns.service-discovery.proto** | The transport protocol of the desired service. | \_tcp | String |
| **camel.cloud.kubernetes.service-discovery.api-version** | Sets the API version when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.ca-cert-data** | Sets the Certificate Authority data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.ca-cert-file** | Sets the Certificate Authority data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-cert-data** | Sets the Client Certificate data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-cert-file** | Sets the Client Certificate data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-algo** | Sets the Client Keystore algorithm, such as RSA when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-data** | Sets the Client Keystore data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-file** | Sets the Client Keystore data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-passphrase** | Sets the Client Keystore passphrase when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.kubernetes.service-discovery.dns-domain** | Sets the DNS domain to use for DNS lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.kubernetes.service-discovery.lookup** | How to perform service lookup. Possible values: client, dns, environment. When using client, then the client queries the kubernetes master to obtain a list of active pods that provides the service, and then random (or round robin) select a pod. When using dns the service name is resolved as name.namespace.svc.dnsDomain. When using dnssrv the service name is resolved with SRV query for _._…​svc…​ When using environment then environment variables are used to lookup the service. By default environment is used. | environment | String |
| **camel.cloud.kubernetes.service-discovery.master-url** | Sets the URL to the master when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.namespace** | Sets the namespace to use. Will by default use namespace from the ENV variable KUBERNETES\_MASTER. |  | String |
| **camel.cloud.kubernetes.service-discovery.oauth-token** | Sets the OAUTH token for authentication (instead of username/password) when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.password** | Sets the password for authentication when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.port-name** | Sets the Port Name to use for DNS/DNSSRV lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.port-protocol** | Sets the Port Protocol to use for DNS/DNSSRV lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.kubernetes.service-discovery.trust-certs** | Sets whether to turn on trust certificate check when using client lookup. | false | Boolean |
| **camel.cloud.kubernetes.service-discovery.username** | Sets the username for authentication when using client lookup. |  | String |
| **camel.language.constant.enabled** | Whether to enable auto configuration of the constant language. This is enabled by default. |  | Boolean |
| **camel.language.constant.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.csimple.enabled** | Whether to enable auto configuration of the csimple language. This is enabled by default. |  | Boolean |
| **camel.language.csimple.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.exchange-property.enabled** | Whether to enable auto configuration of the exchangeProperty language. This is enabled by default. |  | Boolean |
| **camel.language.exchange-property.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.file.enabled** | Whether to enable auto configuration of the file language. This is enabled by default. |  | Boolean |
| **camel.language.file.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.header.enabled** | Whether to enable auto configuration of the header language. This is enabled by default. |  | Boolean |
| **camel.language.header.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.ref.enabled** | Whether to enable auto configuration of the ref language. This is enabled by default. |  | Boolean |
| **camel.language.ref.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.simple.enabled** | Whether to enable auto configuration of the simple language. This is enabled by default. |  | Boolean |
| **camel.language.simple.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.tokenize.enabled** | Whether to enable auto configuration of the tokenize language. This is enabled by default. |  | Boolean |
| **camel.language.tokenize.group-delimiter** | Sets the delimiter to use when grouping. If this has not been set then token will be used as the delimiter. |  | String |
| **camel.language.tokenize.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.tokenize.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.variable.enabled** | Whether to enable auto configuration of the variable language. This is enabled by default. |  | Boolean |
| **camel.language.variable.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.resilience4j.automatic-transition-from-open-to-half-open-enabled** | Enables automatic transition from OPEN to HALF\_OPEN state once the waitDurationInOpenState has passed. | false | Boolean |
| **camel.resilience4j.bulkhead-enabled** | Whether bulkhead is enabled or not on the circuit breaker. Default is false. | false | Boolean |
| **camel.resilience4j.bulkhead-max-concurrent-calls** | Configures the max amount of concurrent calls the bulkhead will support. | 25 | Integer |
| **camel.resilience4j.bulkhead-max-wait-duration** | Configures a maximum amount of time which the calling thread will wait to enter the bulkhead. If bulkhead has space available, entry is guaranteed and immediate. If bulkhead is full, calling threads will contest for space, if it becomes available. maxWaitDuration can be set to 0. Note: for threads running on an event-loop or equivalent (rx computation pool, etc), setting maxWaitDuration to 0 is highly recommended. Blocking an event-loop thread will most likely have a negative effect on application throughput. | 0 | Integer |
| **camel.resilience4j.circuit-breaker** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreaker instance to lookup and use from the registry. When using this, then any other circuit breaker options are not in use. |  | String |
| **camel.resilience4j.config** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreakerConfig instance to lookup and use from the registry. |  | String |
| **camel.resilience4j.configurations** | Define additional configuration definitions. |  | Map |
| **camel.resilience4j.enabled** | Enable the component. | true | Boolean |
| **camel.resilience4j.failure-rate-threshold** | Configures the failure rate threshold in percentage. If the failure rate is equal or greater than the threshold the CircuitBreaker transitions to open and starts short-circuiting calls. The threshold must be greater than 0 and not greater than 100. Default value is 50 percentage. |  | Float |
| **camel.resilience4j.ignore-exception** | Configure a list of exceptions that are ignored and neither count as a failure nor success. Any exception matching or inheriting from one of the list will not count as a failure nor success, even if the exceptions is part of recordExceptions. |  | List |
| **camel.resilience4j.minimum-number-of-calls** | Configures the minimum number of calls which are required (per sliding window period) before the CircuitBreaker can calculate the error rate. For example, if minimumNumberOfCalls is 10, then at least 10 calls must be recorded, before the failure rate can be calculated. If only 9 calls have been recorded the CircuitBreaker will not transition to open even if all 9 calls have failed. Default minimumNumberOfCalls is 100. | 100 | Integer |
| **camel.resilience4j.permitted-number-of-calls-in-half-open-state** | Configures the number of permitted calls when the CircuitBreaker is half open. The size must be greater than 0. Default size is 10. | 10 | Integer |
| **camel.resilience4j.record-exception** | Configure a list of exceptions that are recorded as a failure and thus increase the failure rate. Any exception matching or inheriting from one of the list counts as a failure, unless explicitly ignored via ignoreExceptions. |  | List |
| **camel.resilience4j.sliding-window-size** | Configures the size of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. slidingWindowSize configures the size of the sliding window. Sliding window can either be count-based or time-based. If slidingWindowType is COUNT\_BASED, the last slidingWindowSize calls are recorded and aggregated. If slidingWindowType is TIME\_BASED, the calls of the last slidingWindowSize seconds are recorded and aggregated. The slidingWindowSize must be greater than 0. The minimumNumberOfCalls must be greater than 0. If the slidingWindowType is COUNT\_BASED, the minimumNumberOfCalls cannot be greater than slidingWindowSize . If the slidingWindowType is TIME\_BASED, you can pick whatever you want. Default slidingWindowSize is 100. | 100 | Integer |
| **camel.resilience4j.sliding-window-type** | Configures the type of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. Sliding window can either be count-based or time-based. If slidingWindowType is COUNT\_BASED, the last slidingWindowSize calls are recorded and aggregated. If slidingWindowType is TIME\_BASED, the calls of the last slidingWindowSize seconds are recorded and aggregated. Default slidingWindowType is COUNT\_BASED. | COUNT\_BASED | String |
| **camel.resilience4j.slow-call-duration-threshold** | Configures the duration threshold (seconds) above which calls are considered as slow and increase the slow calls percentage. Default value is 60 seconds. | 60 | Integer |
| **camel.resilience4j.slow-call-rate-threshold** | Configures a threshold in percentage. The CircuitBreaker considers a call as slow when the call duration is greater than slowCallDurationThreshold Duration. When the percentage of slow calls is equal or greater the threshold, the CircuitBreaker transitions to open and starts short-circuiting calls. The threshold must be greater than 0 and not greater than 100. Default value is 100 percentage which means that all recorded calls must be slower than slowCallDurationThreshold. |  | Float |
| **camel.resilience4j.throw-exception-when-half-open-or-open-state** | Whether to throw io.github.resilience4j.circuitbreaker.CallNotPermittedException when the call is rejected due circuit breaker is half open (and was not attempted but rejected immediately) or open (always rejected). This option is only in use when there is NOT a fallback configured on the circuit breaker. When there is a fallback then the fallback is always executed and CallNotPermittedException is not thrown. | false | Boolean |
| **camel.resilience4j.timeout-cancel-running-future** | Configures whether cancel is called on the running future. Defaults to true. | true | Boolean |
| **camel.resilience4j.timeout-duration** | Configures the thread execution timeout. Default value is 1 second. | 1000 | Integer |
| **camel.resilience4j.timeout-enabled** | Whether timeout is enabled or not on the circuit breaker. Default is false. | false | Boolean |
| **camel.resilience4j.timeout-executor-service** | References to a custom thread pool to use when timeout is enabled (uses ForkJoinPool#commonPool() by default). |  | ExecutorService |
| **camel.resilience4j.wait-duration-in-open-state** | Configures the wait duration (in seconds) which specifies how long the CircuitBreaker should stay open, before it switches to half open. Default value is 60 seconds. | 60 | Integer |
| **camel.resilience4j.writable-stack-trace-enabled** | Enables writable stack traces. When set to false, Exception.getStackTrace returns a zero length array. This may be used to reduce log spam when the circuit breaker is open as the cause of the exceptions is already known (the circuit breaker is short-circuiting calls). | true | Boolean |
| **camel.rest.api-component** | The name of the Camel component to use as the REST API. If no API Component has been explicit configured, then Camel will lookup if there is a Camel component responsible for servicing and generating the REST API documentation, or if a org.apache.camel.spi.RestApiProcessorFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.rest.api-context-path** | Sets a leading context-path the REST API will be using. This can be used when using components such as camel-servlet where the deployed web application is deployed using a context-path. |  | String |
| **camel.rest.api-context-route-id** | Sets the route id to use for the route that services the REST API. The route will by default use an auto assigned route id. |  | String |
| **camel.rest.api-host** | To use a specific hostname for the API documentation (such as swagger or openapi) This can be used to override the generated host with this configured hostname. |  | String |
| **camel.rest.api-property** | Allows to configure as many additional properties for the api documentation. For example set property api.title to my cool stuff. |  | Map |
| **camel.rest.api-vendor-extension** | Whether vendor extension is enabled in the Rest APIs. If enabled then Camel will include additional information as vendor extension (eg keys starting with x-) such as route ids, class names etc. Not all 3rd party API gateways and tools supports vendor-extensions when importing your API docs. | false | Boolean |
| **camel.rest.binding-mode** | Sets the binding mode to use. The default value is off. | off | RestBindingMode |
| **camel.rest.binding-package-scan** | Package name to use as base (offset) for classpath scanning of POJO classes are located when using binding mode is enabled for JSon or XML. Multiple package names can be separated by comma. |  | String |
| **camel.rest.client-request-validation** | Whether to enable validation of the client request to check: 1) Content-Type header matches what the Rest DSL consumes; returns HTTP Status 415 if validation error. 2) Accept header matches what the Rest DSL produces; returns HTTP Status 406 if validation error. 3) Missing required data (query parameters, HTTP headers, body); returns HTTP Status 400 if validation error. 4) Parsing error of the message body (JSon, XML or Auto binding mode must be enabled); returns HTTP Status 400 if validation error. | false | Boolean |
| **camel.rest.client-response-validation** | Whether to check what Camel is returning as response to the client: 1) Status-code and Content-Type matches Rest DSL response messages. 2) Check whether expected headers is included according to the Rest DSL repose message headers. 3) If the response body is JSon then check whether its valid JSon. Returns 500 if validation error detected. | false | Boolean |
| **camel.rest.component** | The Camel Rest component to use for the REST transport (consumer), such as netty-http, jetty, servlet, undertow. If no component has been explicit configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.rest.component-property** | Allows to configure as many additional properties for the rest component in use. |  | Map |
| **camel.rest.consumer-property** | Allows to configure as many additional properties for the rest consumer in use. |  | Map |
| **camel.rest.context-path** | Sets a leading context-path the REST services will be using. This can be used when using components such as camel-servlet where the deployed web application is deployed using a context-path. Or for components such as camel-jetty or camel-netty-http that includes a HTTP server. |  | String |
| **camel.rest.cors-headers** | Allows to configure custom CORS headers. |  | Map |
| **camel.rest.data-format-property** | Allows to configure as many additional properties for the data formats in use. For example set property prettyPrint to true to have json outputted in pretty mode. The properties can be prefixed to denote the option is only for either JSON or XML and for either the IN or the OUT. The prefixes are: json.in. json.out. xml.in. xml.out. For example a key with value xml.out.mustBeJAXBElement is only for the XML data format for the outgoing. A key without a prefix is a common key for all situations. |  | Map |
| **camel.rest.enable-cors** | Whether to enable CORS headers in the HTTP response. The default value is false. | false | Boolean |
| **camel.rest.enable-no-content-response** | Whether to return HTTP 204 with an empty body when a response contains an empty JSON object or XML root object. The default value is false. | false | Boolean |
| **camel.rest.endpoint-property** | Allows to configure as many additional properties for the rest endpoint in use. |  | Map |
| **camel.rest.host** | The hostname to use for exposing the REST service. |  | String |
| **camel.rest.host-name-resolver** | If no hostname has been explicit configured, then this resolver is used to compute the hostname the REST service will be using. | alllocalip | RestHostNameResolver |
| **camel.rest.inline-routes** | Inline routes in rest-dsl which are linked using direct endpoints. Each service in Rest DSL is an individual route, meaning that you would have at least two routes per service (rest-dsl, and the route linked from rest-dsl). By inlining (default) allows Camel to optimize and inline this as a single route, however this requires to use direct endpoints, which must be unique per service. If a route is not using direct endpoint then the rest-dsl is not inlined, and will become an individual route. This option is default true. | true | Boolean |
| **camel.rest.json-data-format** | Name of specific json data format to use. By default jackson will be used. Important: This option is only for setting a custom name of the data format, not to refer to an existing data format instance. |  | String |
| **camel.rest.port** | The port number to use for exposing the REST service. Notice if you use servlet component then the port number configured here does not apply, as the port number in use is the actual port number the servlet component is using. eg if using Apache Tomcat its the tomcat http port, if using Apache Karaf its the HTTP service in Karaf that uses port 8181 by default etc. Though in those situations setting the port number here, allows tooling and JMX to know the port number, so its recommended to set the port number to the number that the servlet engine uses. |  | String |
| **camel.rest.producer-api-doc** | Sets the location of the api document the REST producer will use to validate the REST uri and query parameters are valid accordingly to the api document. The location of the api document is loaded from classpath by default, but you can use file: or http: to refer to resources to load from file or http url. |  | String |
| **camel.rest.producer-component** | Sets the name of the Camel component to use as the REST producer. |  | String |
| **camel.rest.scheme** | The scheme to use for exposing the REST service. Usually http or https is supported. The default value is http. |  | String |
| **camel.rest.skip-binding-on-error-code** | Whether to skip binding on output if there is a custom HTTP error code header. This allows to build custom error messages that do not bind to json / xml etc, as success messages otherwise will do. | false | Boolean |
| **camel.rest.use-x-forward-headers** | Whether to use X-Forward headers to set host etc. for OpenApi. This may be needed in special cases involving reverse-proxy and networking going from HTTP to HTTPS etc. Then the proxy can send X-Forward headers (X-Forwarded-Proto) that influences the host names in the OpenAPI schema that camel-openapi-java generates from Rest DSL routes. | false | Boolean |
| **camel.rest.validation-levels** | Allows to configure custom validation levels when using camel-openapi-validator with client request/response validator. |  | Map |
| **camel.rest.xml-data-format** | Name of specific XML data format to use. By default jaxb will be used. Important: This option is only for setting a custom name of the data format, not to refer to an existing data format instance. |  | String |