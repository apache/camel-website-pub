# Spring Boot

Spring Boot component provides auto-configuration for Apache Camel. Our opinionated auto-configuration of the Camel context auto-detects Camel routes available in the Spring context and registers the key Camel utilities (like producer template, consumer template and the type converter) as beans.

Maven users will need to add the following dependency to their `pom.xml` in order to use this component:

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-boot</artifactId>
    <version>${camel.version}</version> <!-- use the same version as your Camel core version -->
</dependency>
```

`camel-spring-boot` jar comes with the `org.springframework.boot.autoconfigure.AutoConfiguration.imports` file, so as soon as you add that dependency into your classpath, Spring Boot will automatically auto-configure Camel for you.

## Camel Spring Boot Starter

Apache Camel ships a [Spring Boot Starter](https://github.com/spring-projects/spring-boot/tree/main/spring-boot-project/spring-boot-starters) module that allows you to develop Spring Boot applications using starters. There is a [sample application](https://github.com/apache/camel-spring-boot-examples/tree/main/spring-boot) in the source code also.

To use the starter, add the following to your spring boot pom.xml file:

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>${camel.version}</version> <!-- use the same version as your Camel core version -->
</dependency>
```

Then you can just add classes with your Camel routes such as:

```java
package com.example;

import org.apache.camel.builder.RouteBuilder;
import org.springframework.stereotype.Component;

@Component
public class MyRoute extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        from("timer:foo").to("log:bar");
    }
}
```

Then these routes will be started automatically.

You can customize the Camel application in the `application.properties` or `application.yml` file.

## Spring Boot Auto-Configuration

When using spring-boot with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-spring-boot-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 296 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.clustered.controller.cluster-service** | The cluster service. |  | CamelClusterService |
| **camel.clustered.controller.enabled** | Global option to enable/disable Camel clustered route controller, default is false. | false | Boolean |
| **camel.clustered.controller.initial-delay** | Set the amount of time (in millis) the route controller should wait before to start the routes after the camel context is started or after the route is initialized if the route is created after the camel context is started. |  | String |
| **camel.clustered.controller.namespace** | The default namespace. |  | String |
| **camel.clustered.controller.routes** | Routes configuration. |  | Map |
| **camel.component.enabled** | Global option to enable/disable component auto-configuration, default is true. | true | Boolean |
| **camel.component.properties.auto-discover-properties-sources** | Whether to automatically discovery instances of PropertiesSource from registry and service factory. | true | Boolean |
| **camel.component.properties.default-fallback-enabled** | If false, the component does not attempt to find a default for the key by looking after the colon separator. | true | Boolean |
| **camel.component.properties.encoding** | Encoding to use when loading properties file from the file system or classpath. If no encoding has been set, then the properties files is loaded using ISO-8859-1 encoding (latin-1) as documented by java.util.Properties#load(java.io.InputStream). |  | String |
| **camel.component.properties.environment-variable-mode** | Sets the OS environment variables mode (0 = never, 1 = fallback, 2 = override). The default mode (override) is to use OS environment variables if present, and override any existing properties. OS environment variable mode is checked before JVM system property mode. |  | Integer |
| **camel.component.properties.ignore-missing-location** | Whether to silently ignore if a location cannot be located, such as a properties file not found. | false | Boolean |
| **camel.component.properties.initial-properties** | Sets initial properties which will be used before any locations are resolved. The option is a java.util.Properties type. |  | String |
| **camel.component.properties.location** | A list of locations to load properties. You can use comma to separate multiple locations. This option will override any default locations and only use the locations from this option. |  | String |
| **camel.component.properties.nested-placeholder** | Whether to support nested property placeholders. A nested placeholder, means that a placeholder, has also a placeholder, that should be resolved (recursively). | true | Boolean |
| **camel.component.properties.override-properties** | Sets a special list of override properties that take precedence and will use first, if a property exist. The option is a java.util.Properties type. |  | String |
| **camel.component.properties.properties-parser** | To use a custom PropertiesParser. The option is a org.apache.camel.component.properties.PropertiesParser type. |  | String |
| **camel.component.properties.system-properties-mode** | Sets the JVM system property mode (0 = never, 1 = fallback, 2 = override). The default mode (override) is to use system properties if present, and override any existing properties. OS environment variable mode is checked before JVM system property mode. |  | Integer |
| **camel.dataformat.enabled** | Global option to enable/disable dataformat auto-configuration, default is true. | true | Boolean |
| **camel.health.async-camel-health-check** | Whether Camel Health Checks are executed asynchronously <p> disabled by default. | false | Boolean |
| **camel.health.consumers-enabled** | Whether consumers health check is enabled. <p> Is default enabled. |  | Boolean |
| **camel.health.enabled** | Whether health check is enabled globally. <p> Is default enabled. |  | Boolean |
| **camel.health.exclude-pattern** | Pattern to exclude health checks from being invoked by Camel when checking healths. Multiple patterns can be separated by comma. |  | String |
| **camel.health.exposure-level** | Sets the level of details to exposure as result of invoking health checks. There are the following levels: full, default, oneline The full level will include all details and status from all the invoked health checks. The default level will report UP if everything is okay, and only include detailed information for health checks that was DOWN. The oneline level will only report either UP or DOWN. | default | String |
| **camel.health.health-check-frequency** | Camel’s HealthCheck frequency in seconds. | 10 | Integer |
| **camel.health.health-check-pool-size** | Camel HealthCheck pool size. | 5 | Integer |
| **camel.health.health-check-thread-name-prefix** | Camel HealthCheck thread name prefix. | CamelHealthTaskScheduler | String |
| **camel.health.initial-state** | The initial state of health-checks (readiness). There are the following states: UP, DOWN, UNKNOWN. By default, the state is DOWN, is regarded as being pessimistic/careful. This means that the overall health checks may report as DOWN during startup and then only if everything is up and running flip to being UP. Setting the initial state to UP, is regarded as being optimistic. This means that the overall health checks may report as UP during startup and then if a consumer or other service is in fact un-healthy, then the health-checks can flip being DOWN. Setting the state to UNKNOWN means that some health-check would be reported in unknown state, especially during early bootstrap where a consumer may not be fully initialized or validated a connection to a remote system. This option allows to pre-configure the state for different modes. | down | String |
| **camel.health.producers-enabled** | Whether producers health check is enabled. <p> Is default disabled. |  | Boolean |
| **camel.health.registry-enabled** | Whether registry health check is enabled. <p> Is default enabled. |  | Boolean |
| **camel.health.routes-enabled** | Whether routes health check is enabled. <p> Is default enabled. |  | Boolean |
| **camel.language.enabled** | Global option to enable/disable language auto-configuration, default is true. | true | Boolean |
| **camel.main.additional-sensitive-keywords** | Camel comes with a default set of sensitive keywords which are automatically masked. This option allows to add additional custom keywords to be masked as well. Multiple keywords can be separated by comma. |  | String |
| **camel.main.allow-use-original-message** | Sets whether to allow access to the original message from Camel’s error handler, or from org.apache.camel.spi.UnitOfWork.getOriginalInMessage(). Turning this off can optimize performance, as defensive copy of the original message is not needed. Default is false. | false | Boolean |
| **camel.main.auto-startup** | Sets whether the object should automatically start when Camel starts. Important: Currently only routes can be disabled, as CamelContext’s are always started. Note: When setting auto startup false on CamelContext then that takes precedence and no routes are started. You would need to start CamelContext explicit using the org.apache.camel.CamelContext.start() method, to start the context, and then you would need to start the routes manually using CamelContext.getRouteController().startRoute(String). Default is true to always start up. | true | Boolean |
| **camel.main.auto-startup-exclude-pattern** | Used for exclusive filtering of routes to not automatically start with Camel starts. The pattern support matching by route id or endpoint urls. Multiple patterns can be specified separated by comma, as example, to exclude all the routes starting from kafka or jms use: kafka,jms. |  | String |
| **camel.main.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. Default is true. | true | Boolean |
| **camel.main.bean-introspection-extended-statistics** | Sets whether bean introspection uses extended statistics. The default is false. | false | Boolean |
| **camel.main.bean-introspection-logging-level** | Sets the logging level used by bean introspection, logging activity of its usage. The default is TRACE. |  | LoggingLevel |
| **camel.main.bean-post-processor-enabled** | Can be used to turn off bean post processing. Be careful to turn this off, as this means that beans that use Camel annotations such as \\{@link org.apache.camel.EndpointInject}, \\{@link org.apache.camel.ProducerTemplate}, \\{@link org.apache.camel.Produce}, \\{@link org.apache.camel.Consume} etc will not be injected and in use. Turning this off should only be done if you are sure you do not use any of these Camel features. Not all runtimes allow turning this off. The default value is true (enabled). | true | Boolean |
| **camel.main.camel-events-timestamp-enabled** | Whether to include timestamps for all emitted Camel Events. Enabling this allows to know fine-grained at what time each event was emitted, which can be used for reporting to report exactly the time of the events. This is by default false to avoid the overhead of including this information. | false | Boolean |
| **camel.main.case-insensitive-headers** | Whether to use case sensitive or insensitive headers. Important: When using case sensitive (this is set to false). Then the map is case sensitive which means headers such as content-type and Content-Type are two different keys which can be a problem for some protocols such as HTTP based, which rely on case insensitive headers. However case sensitive implementations can yield faster performance. Therefore use case sensitive implementation with care. Default is true. | true | Boolean |
| **camel.main.cloud-properties-location** | Sets the locations (comma separated values) where to find properties configuration as defined for cloud native environments such as Kubernetes. You should only scan text based mounted configuration. |  | String |
| **camel.main.compile-work-dir** | Work directory for compiler. Can be used to write compiled classes or other resources. |  | String |
| **camel.main.consumer-template-cache-size** | Consumer template endpoints cache size. | 1000 | Integer |
| **camel.main.context-reload-enabled** | Used for enabling context reloading. If enabled then Camel allow external systems such as security vaults (AWS secrets manager, etc.) to trigger refreshing Camel by updating property placeholders and reload all existing routes to take changes into effect. | false | Boolean |
| **camel.main.description** | Sets the description (intended for humans) of the Camel application. |  | String |
| **camel.main.dev-console-enabled** | Whether to enable developer console (requires camel-console on classpath). The developer console is only for assisting during development. This is NOT for production usage. | false | Boolean |
| **camel.main.dump-routes** | If dumping is enabled then Camel will during startup dump all loaded routes (incl rests and route templates) represented as XML/YAML DSL into the log. This is intended for trouble shooting or to assist during development. Sensitive information that may be configured in the route endpoints could potentially be included in the dump output and is therefore not recommended being used for production usage. This requires to have camel-xml-io/camel-yaml-io on the classpath to be able to dump the routes as XML/YAML. |  | String |
| **camel.main.dump-routes-generated-ids** | Whether to include auto generated IDs in the dumped output. Default is false. | false | Boolean |
| **camel.main.dump-routes-include** | Controls what to include in output for route dumping. Possible values: all, routes, rests, routeConfigurations, routeTemplates, beans, dataFormats. Multiple values can be separated by comma. Default is routes. | routes | String |
| **camel.main.dump-routes-log** | Whether to log route dumps to Logger. | true | Boolean |
| **camel.main.dump-routes-output** | Whether to save route dumps to an output file. If the output is a filename, then all content is saved to this file. If the output is a directory name, then one or more files are saved to the directory, where the names are based on the original source file names, or auto generated names. |  | String |
| **camel.main.dump-routes-resolve-placeholders** | Whether to resolve property placeholders in the dumped output. Default is true. | true | Boolean |
| **camel.main.dump-routes-uri-as-parameters** | When dumping routes to YAML format, then this option controls whether endpoint URIs should be expanded into a key/value parameters. | false | Boolean |
| **camel.main.duration-max-action** | Controls whether the Camel application should shutdown the JVM, or stop all routes, when duration max is triggered. | shutdown | String |
| **camel.main.duration-max-idle-seconds** | To specify for how long time in seconds Camel can be idle before automatic terminating the JVM. You can use this to run Camel for a short while. | 0 | Integer |
| **camel.main.duration-max-messages** | To specify how many messages to process by Camel before automatic terminating the JVM. You can use this to run Camel for a short while. | 0 | Integer |
| **camel.main.duration-max-seconds** | To specify for how long time in seconds to keep running the JVM before automatic terminating the JVM. You can use this to run Camel for a short while. | 0 | Integer |
| **camel.main.endpoint-bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. <p/> By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN/ERROR level and ignored. The default value is false. | false | Boolean |
| **camel.main.endpoint-lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. The default value is false. | false | Boolean |
| **camel.main.endpoint-runtime-statistics-enabled** | Sets whether endpoint runtime statistics is enabled (gathers runtime usage of each incoming and outgoing endpoints). The default value is false. | false | Boolean |
| **camel.main.error-registry-enabled** | Sets whether the error registry is enabled to capture errors during message routing. This is by default disabled. | false | Boolean |
| **camel.main.error-registry-maximum-entries** | Sets the maximum number of error entries to keep in the error registry. When the limit is exceeded, the oldest entries are evicted. The default value is 100. | 100 | Integer |
| **camel.main.error-registry-stack-trace-enabled** | Sets whether to capture stack traces in the error registry. This is enabled by default. | true | Boolean |
| **camel.main.error-registry-time-to-live-seconds** | Sets the time-to-live in seconds for error entries in the error registry. Entries older than this are evicted. The default value is 3600 (1 hour). | 3600 | Integer |
| **camel.main.exchange-factory** | Controls whether to pool (reuse) exchanges or create new exchanges (prototype). Using pooled will reduce JVM garbage collection overhead by avoiding to re-create Exchange instances per message each consumer receives. The default is prototype mode. | default | String |
| **camel.main.exchange-factory-capacity** | The capacity the pool (for each consumer) uses for storing exchanges. The default capacity is 100. | 100 | Integer |
| **camel.main.exchange-factory-statistics-enabled** | Configures whether statistics is enabled on exchange factory. | false | Boolean |
| **camel.main.file-configurations** | Directory to load additional properties files that contains configurations that takes precedence (except for camel.main.xxx configurations). This can be used to refer to files that may have secret configuration that has been mounted on the file system for containers. You can specify a pattern to load from file-system (not classpath) and a name pattern such as /var/app/secret/\*.properties, multiple directories can be separated by comma. |  | String |
| **camel.main.global-options** | Sets global options that can be referenced in the camel context <p/> <b>Important:</b> This has nothing to do with property placeholders, and is just a plain set of key/value pairs which are used to configure global options on CamelContext, such as a maximum debug logging length etc. |  | Map |
| **camel.main.groovy-preload-compiled** | Whether to preload existing compiled Groovy sources from the compileWorkDir option on startup. This can be enabled to avoid compiling sources that already has been compiled during a build phase. | false | Boolean |
| **camel.main.groovy-script-pattern** | Directories to scan for groovy source to be pre-compiled. For example: scripts/\*.groovy will scan inside the classpath folder scripts for all groovy source files. By default, sources are scanned from the classpath, but you can prefix with file: to use file system. The directories are using Ant-path style pattern, and multiple directories can be specified separated by comma. This requires having camel-groovy JAR on the classpath. | classpath:camel-groovy/**,classpath:camel-groovy-compiled/** | String |
| **camel.main.include-non-singletons** | Whether to include non-singleton beans (prototypes) when scanning for RouteBuilder instances. By default only singleton beans is included in the context scan. | false | Boolean |
| **camel.main.inflight-repository-browse-enabled** | Sets whether the inflight repository should allow browsing each inflight exchange. This is by default disabled as there is a very slight performance overhead when enabled. | false | Boolean |
| **camel.main.java-routes-exclude-pattern** | Used for exclusive filtering RouteBuilder classes which are collected from the registry or via classpath scanning. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. For example to exclude all classes starting with Bar use: \*\*/Bar\* To exclude all routes form a specific package use: com/mycompany/bar/\* To exclude all routes form a specific package and its sub-packages use double wildcards: com/mycompany/bar/\*\* And to exclude all routes from two specific packages use: com/mycompany/bar/\*,com/mycompany/stuff/\*. |  | String |
| **camel.main.java-routes-include-pattern** | Used for inclusive filtering RouteBuilder classes which are collected from the registry or via classpath scanning. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. Multiple patterns can be specified separated by comma. For example to include all classes starting with Foo use: \*\*/Foo\* To include all routes form a specific package use: com/mycompany/foo/\* To include all routes form a specific package and its sub-packages use double wildcards: com/mycompany/foo/\*\* And to include all routes from two specific packages use: com/mycompany/foo/\*,com/mycompany/stuff/\*. |  | String |
| **camel.main.jmx-enabled** | Enable JMX in your Camel application. | true | Boolean |
| **camel.main.jmx-management-m-beans-level** | Sets the mbeans registration level. The default value is Default. |  | ManagementMBeansLevel |
| **camel.main.jmx-management-name-pattern** | The naming pattern for creating the CamelContext JMX management name. The default pattern is name. | name | String |
| **camel.main.jmx-management-register-routes-create-by-kamelet** | Whether routes created by Kamelets should be registered for JMX management. Enabling this allows to have fine-grained monitoring and management of every route created via Kamelets. This is default disabled as a Kamelet is intended as a component (black-box) and its implementation details as Camel route makes the overall management and monitoring of Camel applications more verbose. During development of Kamelets then enabling this will make it possible for developers to do fine-grained performance inspection and identify potential bottlenecks in the Kamelet routes. However, for production usage then keeping this disabled is recommended. | false | Boolean |
| **camel.main.jmx-management-register-routes-create-by-template** | Whether routes created by route templates (not Kamelets) should be registered for JMX management. Enabling this allows to have fine-grained monitoring and management of every route created via route templates. This is default enabled (unlike Kamelets) as routes created via templates is regarded as standard routes, and should be available for management and monitoring. | true | Boolean |
| **camel.main.jmx-management-statistics-level** | Sets the JMX statistics level, the level can be set to Extended to gather additional information The default value is Default. |  | ManagementStatisticsLevel |
| **camel.main.jmx-update-route-enabled** | Whether to allow updating routes at runtime via JMX using the ManagedRouteMBean. This is disabled by default, but can be enabled for development and troubleshooting purposes, such as updating routes in an existing running Camel via JMX and other tools. | false | Boolean |
| **camel.main.load-health-checks** | Whether to load custom health checks by scanning classpath. | false | Boolean |
| **camel.main.load-statistics-enabled** | Sets whether Camel load (inflight messages, not cpu) statistics is enabled (something like the unix load average). The statistics requires to have camel-management on the classpath as JMX is required. The default value is false. | false | Boolean |
| **camel.main.load-type-converters** | Whether to load custom type converters by scanning classpath. This is used for backwards compatibility with Camel 2.x. Its recommended to migrate to use fast type converter loading by setting <tt>@Converter(loader = true)</tt> on your custom type converter classes. | false | Boolean |
| **camel.main.log-debug-max-chars** | Is used to limit the maximum length of the logging Camel message bodies. If the message body is longer than the limit, the log message is clipped. Use -1 to have unlimited length. Use for example 1000 to log at most 1000 characters. | 0 | Integer |
| **camel.main.log-exhausted-message-body** | Sets whether to log exhausted message body with message history. Default is false. | false | Boolean |
| **camel.main.log-language** | To configure the language to use for Log EIP. By default, the simple language is used. However, Camel also supports other languages such as groovy. |  | String |
| **camel.main.log-mask** | Sets whether log mask is enabled or not. Default is false. | false | Boolean |
| **camel.main.log-name** | The global name to use for Log EIP The name is default the routeId or the source:line if source location is enabled. You can also specify the name using tokens: <br/> ${class} - the logger class name (org.apache.camel.processor.LogProcessor) <br/> ${contextId} - the camel context id <br/> ${routeId} - the route id <br/> ${groupId} - the route group id <br/> ${nodeId} - the node id <br/> ${nodePrefixId} - the node prefix id <br/> ${source} - the source:line (source location must be enabled) <br/> $\\{source.name} - the source filename (source location must be enabled) <br/> $\\{source.line} - the source line number (source location must be enabled) For example to use the route and node id you can specify the name as: ${routeId}/${nodeId}. |  | String |
| **camel.main.message-history** | Sets whether message history is enabled or not. Default is false. | false | Boolean |
| **camel.main.modeline** | Whether to support JBang style //DEPS to specify additional dependencies when running Camel JBang. | false | Boolean |
| **camel.main.name** | Sets the name of the CamelContext. |  | String |
| **camel.main.producer-template-cache-size** | Producer template endpoints cache size. | 1000 | Integer |
| **camel.main.route-filter-exclude-pattern** | Used for filtering routes routes matching the given pattern, which follows the following rules: - Match by route id - Match by route input endpoint uri The matching is using exact match, by wildcard and regular expression as documented by \\{@link PatternHelper#matchPattern(String, String)}. For example to only include routes which starts with foo in their route id’s, use: include=foo\* And to exclude routes which starts from JMS endpoints, use: exclude=jms:\* Multiple patterns can be separated by comma, for example to exclude both foo and bar routes, use: exclude=foo\*,bar\* Exclude takes precedence over include. |  | String |
| **camel.main.route-filter-include-pattern** | Used for filtering routes matching the given pattern, which follows the following rules: - Match by route id - Match by route input endpoint uri The matching is using exact match, by wildcard and regular expression as documented by \\{@link PatternHelper#matchPattern(String, String)}. For example to only include routes which starts with foo in their route id’s, use: include=foo\* And to exclude routes which starts from JMS endpoints, use: exclude=jms:\* Multiple patterns can be separated by comma, for example to exclude both foo and bar routes, use: exclude=foo\*,bar\* Exclude takes precedence over include. |  | String |
| **camel.main.routes-collector-enabled** | Whether the routes collector is enabled or not. When enabled Camel will auto-discover routes (RouteBuilder instances from the registry and also load additional routes from the file system). The routes collector is default enabled. | true | Boolean |
| **camel.main.routes-collector-ignore-loading-error** | Whether the routes collector should ignore any errors during loading and compiling routes. This is only intended for development or tooling. | false | Boolean |
| **camel.main.routes-exclude-pattern** | Used for exclusive filtering of routes from directories. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma, as example, to exclude all the routes from a directory whose name contains foo use: \*\*/**foo**. |  | String |
| **camel.main.routes-include-pattern** | Used for inclusive filtering of routes from directories. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma, as example, to include all the routes from a directory whose name contains foo use: \*\*/**foo**. | classpath:camel/**,classpath:camel-template/**,classpath:camel-rest/\* | String |
| **camel.main.routes-reload-directory** | Directory to scan for route changes. Camel cannot scan the classpath, so this must be configured to a file directory. Development with Maven as build tool, you can configure the directory to be src/main/resources to scan for Camel routes in XML or YAML files. | src/main/resources/camel | String |
| **camel.main.routes-reload-directory-recursive** | Whether the directory to scan should include sub directories. Depending on the number of sub directories, then this can cause the JVM to startup slower as Camel uses the JDK file-watch service to scan for file changes. | false | Boolean |
| **camel.main.routes-reload-enabled** | Used for enabling automatic routes reloading. If enabled then Camel will watch for file changes in the given reload directory, and trigger reloading routes if files are changed. | false | Boolean |
| **camel.main.routes-reload-pattern** | Used for inclusive filtering of routes from directories. Typical used for specifying to accept routes in XML or YAML files, such as <tt>\*.yaml,\*.xml</tt>. Multiple patterns can be specified separated by comma. |  | String |
| **camel.main.routes-reload-remove-all-routes** | When reloading routes should all existing routes be stopped and removed. By default, Camel will stop and remove all existing routes before reloading routes. This ensures that only the reloaded routes will be active. If disabled then only routes with the same route id is updated, and any existing routes are continued to run. | true | Boolean |
| **camel.main.routes-reload-restart-duration** | Whether to restart max duration when routes are reloaded. For example if max duration is 60 seconds, and a route is reloaded after 25 seconds, then this will restart the count and wait 60 seconds again. | false | Boolean |
| **camel.main.run-controller** | Whether to use the main run controller to ensure the Spring-Boot application keeps running until being stopped or the JVM terminated. You typically only need this if you run Spring-Boot standalone. If you run Spring-Boot with spring-boot-starter-web then the web container keeps the JVM running. | false | Boolean |
| **camel.main.shutdown-log-inflight-exchanges-on-timeout** | Sets whether to log information about the inflight Exchanges which are still running during a shutdown which didn’t complete without the given timeout. This requires to enable the option inflightRepositoryBrowseEnabled. | true | Boolean |
| **camel.main.shutdown-now-on-timeout** | Sets whether to force shutdown of all consumers when a timeout occurred and thus not all consumers was shutdown within that period. You should have good reasons to set this option to false as it means that the routes keep running and is halted abruptly when CamelContext has been shutdown. | true | Boolean |
| **camel.main.shutdown-routes-in-reverse-order** | Sets whether routes should be shutdown in reverse or the same order as they were started. | true | Boolean |
| **camel.main.shutdown-suppress-logging-on-timeout** | Whether Camel should try to suppress logging during shutdown and timeout was triggered, meaning forced shutdown is happening. And during forced shutdown we want to avoid logging errors/warnings et all in the logs as a side-effect of the forced timeout. Notice the suppress is a best effort as there may still be some logs coming from 3rd party libraries and whatnot, which Camel cannot control. This option is default false. | false | Boolean |
| **camel.main.shutdown-timeout** | Timeout in seconds to graceful shutdown all the Camel routes. | 45 | Integer |
| **camel.main.source-location-enabled** | Whether to capture precise source location:line-number for all EIPs in Camel routes. Enabling this will impact parsing Java based routes (also Groovy etc.) on startup as this uses JDK StackTraceElement to calculate the location from the Camel route, which comes with a performance cost. This only impact startup, not the performance of the routes at runtime. | false | Boolean |
| **camel.main.startup-recorder** | To use startup recorder for capturing execution time during starting Camel. The recorder can be one of: false (or off), logging, backlog, java-flight-recorder (or jfr). |  | String |
| **camel.main.startup-recorder-dir** | Directory to store the recording. By default the current directory will be used. Use false to turn off saving recording to disk. |  | String |
| **camel.main.startup-recorder-duration** | How long time to run the startup recorder. Use 0 (default) to keep the recorder running until the JVM is exited. Use -1 to stop the recorder right after Camel has been started (to only focus on potential Camel startup performance bottlenecks) Use a positive value to keep recording for N seconds. When the recorder is stopped then the recording is auto saved to disk (note: save to disk can be disabled by setting startupRecorderDir to false). | 0 | Long |
| **camel.main.startup-recorder-max-depth** | To filter our sub steps at a maximum depth. Use -1 for no maximum. Use 0 for no sub steps. Use 1 for max 1 sub step, and so forth. The default is -1. | \-1 | Integer |
| **camel.main.startup-recorder-profile** | To use a specific Java Flight Recorder profile configuration, such as default or profile. The default is default. | default | String |
| **camel.main.startup-recorder-recording** | To enable Java Flight Recorder to start a recording and automatic dump the recording to disk after startup is complete. This requires that camel-jfr is on the classpath, and to enable this option. | false | Boolean |
| **camel.main.startup-summary-level** | Controls the level of information logged during startup (and shutdown) of CamelContext. |  | StartupSummaryLevel |
| **camel.main.stream-caching-allow-classes** | To filter stream caching of a given set of allowed/denied classes. By default, all classes that are \\{@link java.io.InputStream} is allowed. Multiple class names can be separated by comma. |  | String |
| **camel.main.stream-caching-any-spool-rules** | Sets whether if just any of the org.apache.camel.spi.StreamCachingStrategy.SpoolRule rules returns true then shouldSpoolCache(long) returns true, to allow spooling to disk. If this option is false, then all the org.apache.camel.spi.StreamCachingStrategy.SpoolRule must return true. The default value is false which means that all the rules must return true. | false | Boolean |
| **camel.main.stream-caching-buffer-size** | Sets the stream caching buffer size to use when allocating in-memory buffers used for in-memory stream caches. The default size is 4096. | 0 | Integer |
| **camel.main.stream-caching-deny-classes** | To filter stream caching of a given set of allowed/denied classes. By default, all classes that are \\{@link java.io.InputStream} is allowed. Multiple class names can be separated by comma. |  | String |
| **camel.main.stream-caching-enabled** | Sets whether stream caching is enabled or not. While stream types (like StreamSource, InputStream and Reader) are commonly used in messaging for performance reasons, they also have an important drawback: they can only be read once. In order to be able to work with message content multiple times, the stream needs to be cached. Streams are cached in memory only (by default). If streamCachingSpoolEnabled=true, then, for large stream messages (over 128 KB by default) will be cached in a temporary file instead, and Camel will handle deleting the temporary file once the cached stream is no longer necessary. Default is true. | true | Boolean |
| **camel.main.stream-caching-remove-spool-directory-when-stopping** | Whether to remove stream caching temporary directory when stopping. This option is default true. | true | Boolean |
| **camel.main.stream-caching-spool-cipher** | Sets a stream caching cipher name to use when spooling to disk to write with encryption. By default the data is not encrypted. |  | String |
| **camel.main.stream-caching-spool-directory** | Sets the stream caching spool (temporary) directory to use for overflow and spooling to disk. If no spool directory has been explicit configured, then a temporary directory is created in the java.io.tmpdir directory. |  | String |
| **camel.main.stream-caching-spool-enabled** | To enable stream caching spooling to disk. This means, for large stream messages (over 128 KB by default) will be cached in a temporary file instead, and Camel will handle deleting the temporary file once the cached stream is no longer necessary. Default is false. | false | Boolean |
| **camel.main.stream-caching-spool-rules** | Sets custom rules (org.apache.camel.spi.StreamCachingStrategy.SpoolRule) for deciding when to spool to disk. Multiple rules can be separated by comma. |  | String |
| **camel.main.stream-caching-spool-threshold** | Stream caching threshold in bytes when overflow to disk is activated. The default threshold is 128kb. Use -1 to disable overflow to disk. | 0 | Long |
| **camel.main.stream-caching-spool-used-heap-memory-limit** | Sets what the upper bounds should be when streamCachingSpoolUsedHeapMemoryThreshold is in use. |  | String |
| **camel.main.stream-caching-spool-used-heap-memory-threshold** | Sets a percentage (1-99) of used heap memory threshold to activate stream caching spooling to disk. | 0 | Integer |
| **camel.main.stream-caching-statistics-enabled** | Sets whether stream caching statistics is enabled. | false | Boolean |
| **camel.main.thread-name-pattern** | Sets the thread name pattern used for creating the full thread name. The default pattern is: Camel (camelId) thread #counter - name Where camelId is the name of the CamelContext. and counter is a unique incrementing counter. and name is the regular thread name. You can also use longName which is the long thread name which can includes endpoint parameters etc. |  | String |
| **camel.main.tracing** | Sets whether tracing is enabled or not. Default is false. | false | Boolean |
| **camel.main.tracing-logging-format** | To use a custom tracing logging format. The default format (arrow, routeId, label) is: %-4.4s \[%-12.12s\] \[%-33.33s\]. |  | String |
| **camel.main.tracing-pattern** | Tracing pattern to match which node EIPs to trace. For example to match all To EIP nodes, use to\*. The pattern matches by node and route id’s Multiple patterns can be separated by comma. |  | String |
| **camel.main.tracing-standby** | Whether to set tracing on standby. If on standby then the tracer is installed and made available. Then the tracer can be enabled later at runtime via JMX or via \\{@link Tracer#setEnabled(boolean)}. | false | Boolean |
| **camel.main.tracing-templates** | Whether tracing should trace inner details from route templates (or kamelets). Turning this on increases the verbosity of tracing by including events from internal routes in the templates or kamelets. Default is false. | false | Boolean |
| **camel.main.type-converter-statistics-enabled** | Sets whether type converter statistics is enabled. By default the type converter utilization statistics is disabled. Notice: If enabled then there is a slight performance impact under very heavy load. | false | Boolean |
| **camel.main.use-breadcrumb** | Set whether breadcrumb is enabled. The default value is false. | false | Boolean |
| **camel.main.use-data-type** | Whether to enable using data type on Camel messages. Data type are automatic turned on if one ore more routes has been explicit configured with input and output types. Otherwise data type is default off. | false | Boolean |
| **camel.main.uuid-generator** | UUID generator to use. default (32 bytes), short (16 bytes), classic (32 bytes or longer), simple (long incrementing counter), off (turned off for exchanges - only intended for performance profiling). | default | String |
| **camel.main.warn-on-early-shutdown** | Whether to log a WARN if Camel on Spring Boot was immediately shutdown after starting which very likely is because there is no JVM thread to keep the application running. | true | Boolean |
| **camel.routecontroller.back-off-delay** | Backoff delay in millis when restarting a route that failed to startup. | 2000 | Long |
| **camel.routecontroller.back-off-max-attempts** | Backoff maximum number of attempts to restart a route that failed to startup. When this threshold has been exceeded then the controller will give up attempting to restart the route, and the route will remain as stopped. | 0 | Long |
| **camel.routecontroller.back-off-max-delay** | Backoff maximum delay in millis when restarting a route that failed to startup. | 0 | Long |
| **camel.routecontroller.back-off-max-elapsed-time** | Backoff maximum elapsed time in millis, after which the backoff should be considered exhausted and no more attempts should be made. | 0 | Long |
| **camel.routecontroller.back-off-multiplier** | Backoff multiplier to use for exponential backoff. This is used to extend the delay between restart attempts. | 1 | Double |
| **camel.routecontroller.enabled** | To enable using supervising route controller which allows Camel to startup and then the controller takes care of starting the routes in a safe manner. This can be used when you want to startup Camel despite a route may otherwise fail fast during startup and cause Camel to fail to startup as well. By delegating the route startup to the supervising route controller then it manages the startup using a background thread. The controller allows to be configured with various settings to attempt to restart failing routes. | false | Boolean |
| **camel.routecontroller.exclude-routes** | Pattern for filtering routes to be included as supervised. The pattern is matching on route id, and endpoint uri for the route. Multiple patterns can be separated by comma. For example to include all kafka routes, you can say <tt>kafka:\*</tt>. And to include routes with specific route ids <tt>myRoute,myOtherRoute</tt>. The pattern supports wildcards and uses the matcher from org.apache.camel.support.PatternHelper#matchPattern. |  | String |
| **camel.routecontroller.include-routes** | Pattern for filtering routes to be excluded as supervised. The pattern is matching on route id, and endpoint uri for the route. Multiple patterns can be separated by comma. For example to exclude all JMS routes, you can say <tt>jms:\*</tt>. And to exclude routes with specific route ids <tt>mySpecialRoute,myOtherSpecialRoute</tt>. The pattern supports wildcards and uses the matcher from org.apache.camel.support.PatternHelper#matchPattern. |  | String |
| **camel.routecontroller.initial-delay** | Initial delay in milli seconds before the route controller starts, after CamelContext has been started. | 0 | Long |
| **camel.routecontroller.thread-pool-size** | The number of threads used by the route controller scheduled thread pool that are used for restarting routes. The pool uses 1 thread by default, but you can increase this to allow the controller to concurrently attempt to restart multiple routes in case more than one route has problems starting. | 1 | Integer |
| **camel.routecontroller.unhealthy-on-exhausted** | Whether to mark the route as unhealthy (down) when all restarting attempts (backoff) have failed and the route is not successfully started and the route manager is giving up. If setting this to false will make health checks ignore this problem and allow to report the Camel application as UP. | true | Boolean |
| **camel.routecontroller.unhealthy-on-restarting** | Whether to mark the route as unhealthy (down) when the route failed to initially start, and is being controlled for restarting (backoff). If setting this to false will make health checks ignore this problem and allow to report the Camel application as UP. | true | Boolean |
| **camel.routetemplate.config** | Route template configurations. |  | List |
| **camel.security.allowed-properties** | Comma-separated list of property keys to exclude from security policy checks. Use full property paths (e.g., camel.component.aws2-s3.trustAllCertificates) to allow specific properties regardless of the configured policy. |  | String |
| **camel.security.insecure-dev-policy** | Security policy for development-only features. When set, overrides the global policy for options intended only for development environments. |  | String |
| **camel.security.insecure-serialization-policy** | Security policy for insecure deserialization configuration. When set, overrides the global policy for options that enable dangerous deserialization of untrusted data. |  | String |
| **camel.security.insecure-ssl-policy** | Security policy for insecure SSL/TLS configuration. When set, overrides the global policy for options that disable certificate validation or hostname verification. |  | String |
| **camel.security.policy** | Global security policy applied to all categories unless overridden. Controls how Camel reacts when insecure configuration is detected at startup. | warn | String |
| **camel.security.secret-policy** | Security policy for plain-text secrets. When set, overrides the global policy for properties that contain sensitive values configured as plain text. |  | String |
| **camel.ssl.cert-alias** | An optional certificate alias to use. This is useful when the keystore has multiple certificates. |  | String |
| **camel.ssl.cipher-suites** | The optional explicitly configured cipher suites for this configuration. |  | CipherSuitesParameters |
| **camel.ssl.cipher-suites-filter** | The optional cipher suite filter configuration for this configuration. |  | FilterParameters |
| **camel.ssl.client-parameters** | The optional configuration options to be applied purely to the client side settings of the SSLContext. Settings specified here override any duplicate settings provided at the overall level by this class. These parameters apply to SSLSocketFactory and SSLEngine produced by the SSLContext produced from this class as well as to the SSLContext itself. |  | SSLContextClientParameters |
| **camel.ssl.config** | Global Camel security configuration. |  | SSLContextParameters |
| **camel.ssl.key-managers** | The optional key manager configuration for creating the KeyManager used in constructing an SSLContext. |  | KeyManagersParameters |
| **camel.ssl.named-groups** | The optional explicitly configured named groups (key exchange groups) for this configuration. Named groups control which key exchange algorithms are available during the TLS handshake, including post-quantum hybrid groups such as X25519MLKEM768. |  | NamedGroupsParameters |
| **camel.ssl.named-groups-filter** | The optional named groups filter configuration for this configuration. |  | FilterParameters |
| **camel.ssl.provider** | The optional provider identifier for the JSSE implementation to use when constructing an SSLContext. |  | String |
| **camel.ssl.secure-random** | The optional secure random configuration options to use for constructing the SecureRandom used in the creation of an SSLContext. |  | SecureRandomParameters |
| **camel.ssl.secure-socket-protocol** | The optional protocol for the secure sockets created by the SSLContext represented by this instance’s configuration. See Appendix A in the Java Secure Socket Extension Reference Guide for information about standard protocol names. |  | String |
| **camel.ssl.secure-socket-protocols** | The optional explicitly configured secure socket protocol names for this configuration. |  | SecureSocketProtocolsParameters |
| **camel.ssl.secure-socket-protocols-filter** | The option secure socket protocol name filter configuration for this configuration. |  | FilterParameters |
| **camel.ssl.server-parameters** | The optional configuration options to be applied purely to the server side settings of the SSLContext. Settings specified here override any duplicate settings provided at the overall level by this class. These parameters apply to SSLServerSocketFactory and SSLEngine produced by the SSLContext produced from this class as well as to the SSLContext itself. |  | SSLContextServerParameters |
| **camel.ssl.session-timeout** | The optional SSLSessionContext timeout time for javax.net.ssl.SSLSession in seconds. |  | String |
| **camel.ssl.signature-schemes** | The optional explicitly configured signature schemes for this configuration. Signature schemes control which signature algorithms are available during the TLS handshake, including post-quantum signature algorithms such as ML-DSA. |  | SignatureSchemesParameters |
| **camel.ssl.signature-schemes-filter** | The optional signature schemes filter configuration for this configuration. |  | FilterParameters |
| **camel.ssl.trust-all-certificates** | Allows to trust all SSL certificates without performing certificate validation. This can be used in development environment but may expose the system to security risks. Notice that if the trustAllCertificates option is set to true then the trustStore/trustStorePassword options are not in use. | false | Boolean |
| **camel.ssl.trust-managers** | The optional trust manager configuration for creating the TrustManager used in constructing an SSLContext. |  | TrustManagersParameters |
| **camel.startupcondition.custom-class-names** | A list of custom class names (FQN). Multiple classes can be separated by comma. |  | String |
| **camel.startupcondition.enabled** | To enable using startup conditions. | false | Boolean |
| **camel.startupcondition.environment-variable-exists** | Wait for an environment variable with the given name to exists before continuing. |  | String |
| **camel.startupcondition.file-exists** | Wait for a file with the given name to exists before continuing. |  | String |
| **camel.startupcondition.interval** | Interval in millis between checking conditions. | 500 | Integer |
| **camel.startupcondition.on-timeout** | What action, to do on timeout. fail = do not startup, and throw an exception causing camel to fail stop = do not startup, and stop camel ignore = log a WARN and continue to startup. | stop | String |
| **camel.startupcondition.timeout** | Total timeout (in millis) for all startup conditions. | 20000 | Integer |
| **camel.threadpool.allow-core-thread-time-out** | Sets default whether to allow core threads to timeout. |  | Boolean |
| **camel.threadpool.config** | Adds a configuration for a specific thread pool profile (inherits default values). |  | Map |
| **camel.threadpool.config.allow-core-thread-time-out** | Sets whether to allow core threads to timeout. |  | Boolean |
| **camel.threadpool.config.id** | Sets the id of this thread pool. |  | String |
| **camel.threadpool.config.keep-alive-time** | Sets the keep alive time for inactive threads. |  | Long |
| **camel.threadpool.config.max-pool-size** | Sets the maximum pool size. |  | Integer |
| **camel.threadpool.config.max-queue-size** | Sets the maximum number of tasks in the work queue. Use -1 or an unbounded queue. |  | Integer |
| **camel.threadpool.config.pool-size** | Sets the core pool size (threads to keep minimum in pool). |  | Integer |
| **camel.threadpool.config.rejected-policy** | Sets the handler for tasks which cannot be executed by the thread pool. |  | ThreadPoolRejectedPolicy |
| **camel.threadpool.config.time-unit** | Sets the time unit used for keep alive time. |  | TimeUnit |
| **camel.threadpool.keep-alive-time** | Sets the default keep alive time for inactive threads. |  | Long |
| **camel.threadpool.max-pool-size** | Sets the default maximum pool size. |  | Integer |
| **camel.threadpool.max-queue-size** | Sets the default maximum number of tasks in the work queue. Use -1 or an unbounded queue. |  | Integer |
| **camel.threadpool.pool-size** | Sets the default core pool size (threads to keep minimum in pool). |  | Integer |
| **camel.threadpool.rejected-policy** | Sets the default handler for tasks which cannot be executed by the thread pool. |  | ThreadPoolRejectedPolicy |
| **camel.threadpool.time-unit** | Sets the default time unit used for keep alive time. |  | TimeUnit |
| **camel.trace.backlog-size** | Defines how many of the last messages to keep in the tracer. | 1000 | Integer |
| **camel.trace.body-include-files** | Whether to include the message body of file based messages. The overhead is that the file content has to be read from the file. | true | Boolean |
| **camel.trace.body-include-streams** | Whether to include the message body of stream based messages. If enabled then beware the stream may not be re-readable later. See more about Stream Caching. | false | Boolean |
| **camel.trace.body-max-chars** | To limit the message body to a maximum size in the traced message. Use 0 or negative value to use unlimited size. |  | Integer |
| **camel.trace.enabled** | Enables tracer in your Camel application. | false | Boolean |
| **camel.trace.include-exception** | Trace messages to include exception if the message failed. | true | Boolean |
| **camel.trace.include-exchange-properties** | Whether to include the exchange properties in the traced message. | true | Boolean |
| **camel.trace.include-exchange-variables** | Whether to include the exchange variables in the traced message. | true | Boolean |
| **camel.trace.remove-on-dump** | Whether all traced messages should be removed when the tracer is dumping. By default, the messages are removed, which means that dumping will not contain previous dumped messages. | true | Boolean |
| **camel.trace.standby** | To set the tracer in standby mode, where the tracer will be installed by not automatic enabled. The tracer can then later be enabled explicit from Java, JMX or tooling. | false | Boolean |
| **camel.trace.trace-filter** | Filter for tracing messages. |  | String |
| **camel.trace.trace-pattern** | Filter for tracing by route or node id. |  | String |
| **camel.trace.trace-rests** | Whether to trace routes that is created from Rest DSL. | false | Boolean |
| **camel.trace.trace-templates** | Whether to trace routes that is created from route templates or kamelets. | false | Boolean |
| **camel.vault.aws.access-key** | The AWS access key. |  | String |
| **camel.vault.aws.default-credentials-provider** | Define if we want to use the AWS Default Credentials Provider or not. | false | Boolean |
| **camel.vault.aws.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.vault.aws.profile-credentials-provider** | Define if we want to use the AWS Profile Credentials Provider or not. | false | Boolean |
| **camel.vault.aws.profile-name** | Define the profile name in case we are using profile credentials provider. |  | String |
| **camel.vault.aws.refresh-enabled** | Define if we want to refresh the secrets on update. | false | Boolean |
| **camel.vault.aws.refresh-period** | Define the refresh period. | 30000 | Long |
| **camel.vault.aws.region** | The AWS region. |  | String |
| **camel.vault.aws.secret-key** | The AWS secret key. |  | String |
| **camel.vault.aws.secrets** | Define the secrets to look at. |  | String |
| **camel.vault.aws.sqs-queue-url** | In case of usage of SQS notification this field will specified the Queue URL to use. |  | String |
| **camel.vault.aws.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.vault.aws.use-sqs-notification** | Whether to use AWS SQS for secrets updates notification, this will require setting up Eventbridge/Cloudtrail/SQS communication. | false | Boolean |
| **camel.vault.azure.azure-identity-enabled** | Whether the Azure Identity Authentication should be used or not. | false | Boolean |
| **camel.vault.azure.blob-access-key** | The Eventhubs Blob Access Key for CheckpointStore purpose. |  | String |
| **camel.vault.azure.blob-account-name** | The Eventhubs Blob Account Name for CheckpointStore purpose. |  | String |
| **camel.vault.azure.blob-container-name** | The Eventhubs Blob Container Name for CheckpointStore purpose. |  | String |
| **camel.vault.azure.client-id** | The Client Id. |  | String |
| **camel.vault.azure.client-secret** | The Client secret. |  | String |
| **camel.vault.azure.eventhub-connection-string** | The Eventhubs connection String for Key Vault Secret events notifications. |  | String |
| **camel.vault.azure.refresh-enabled** | Whether to automatically reload Camel upon secrets being updated in Azure. | false | Boolean |
| **camel.vault.azure.refresh-period** | The period (millis) between checking Azure for updated secrets. | 30000 | Long |
| **camel.vault.azure.secrets** | Specify the secret names (or pattern) to check for updates. Multiple secrets can be separated by comma. |  | String |
| **camel.vault.azure.tenant-id** | The tenant Id. |  | String |
| **camel.vault.azure.vault-name** | The Vault Name. |  | String |
| **camel.vault.cyberark.account** | The CyberArk Conjur account name. |  | String |
| **camel.vault.cyberark.api-key** | The API key for authentication. |  | String |
| **camel.vault.cyberark.auth-token** | Pre-authenticated token to use. |  | String |
| **camel.vault.cyberark.certificate-path** | Path to the SSL certificate for verification. |  | String |
| **camel.vault.cyberark.password** | The password for authentication. |  | String |
| **camel.vault.cyberark.secrets** | Specify the secret names (or pattern) to check for updates. Multiple secrets can be separated by comma. |  | String |
| **camel.vault.cyberark.url** | The CyberArk Conjur instance URL. |  | String |
| **camel.vault.cyberark.username** | The username for authentication. |  | String |
| **camel.vault.cyberark.verify-ssl** | Whether to verify SSL certificates. | true | Boolean |
| **camel.vault.gcp.project-id** | The GCP Project ID. |  | String |
| **camel.vault.gcp.refresh-enabled** | Define if we want to refresh the secrets on update. | false | Boolean |
| **camel.vault.gcp.refresh-period** | Define the refresh period. | 30000 | Long |
| **camel.vault.gcp.secrets** | Define the secrets to look at. |  | String |
| **camel.vault.gcp.service-account-key** | The Service Account Key location. |  | String |
| **camel.vault.gcp.subscription-name** | Define the Google Pubsub subscription Name to be used when checking for updates. |  | String |
| **camel.vault.gcp.use-default-instance** | Define if we want to use the GCP Client Default Instance or not. | false | Boolean |
| **camel.vault.hashicorp.cloud** | Determine if the Hashicorp Vault is deployed on Hashicorp Cloud or not. | false | Boolean |
| **camel.vault.hashicorp.host** | The Hashicorp Vault Host for accessing the service. |  | String |
| **camel.vault.hashicorp.namespace** | If the Hashicorp Vault instance is deployed on Hashicorp Cloud, this field will determine the namespace. |  | String |
| **camel.vault.hashicorp.port** | The Hashicorp Vault port for accessing the service. |  | String |
| **camel.vault.hashicorp.refresh-enabled** | Whether to automatically reload Camel upon secrets being updated in Hashicorp Vault. | false | Boolean |
| **camel.vault.hashicorp.refresh-period** | The period (millis) between checking Hashicorp Vault for updated secrets. | 60000 | Long |
| **camel.vault.hashicorp.scheme** | The Hashicorp Vault Scheme for accessing the service. |  | String |
| **camel.vault.hashicorp.secrets** | Specify the secret names (or pattern) to check for updates. Multiple secrets can be separated by comma. |  | String |
| **camel.vault.hashicorp.token** | The Hashicorp Vault Token for accessing the service. |  | String |
| **camel.vault.ibm.event-stream-bootstrap-servers** | Specify the Bootstrap servers for consuming notification on IBM Event Stream. Multiple servers can be separated by comma. |  | String |
| **camel.vault.ibm.event-stream-consumer-poll-timeout** | Specify the Consumer Poll Timeout while consuming from IBM Event Stream Topic. | 3000 | Long |
| **camel.vault.ibm.event-stream-group-id** | Specify the Consumer Group ID to access IBM Event Stream. |  | String |
| **camel.vault.ibm.event-stream-password** | Specify the password to access IBM Event Stream. |  | String |
| **camel.vault.ibm.event-stream-topic** | Specify the topic name for consuming notification on IBM Event Stream. |  | String |
| **camel.vault.ibm.event-stream-username** | Specify the username to access IBM Event Stream. |  | String |
| **camel.vault.ibm.service-url** | The IBM Secrets Manager Service URL. |  | String |
| **camel.vault.ibm.token** | The IBM Secrets Manager Token. |  | String |
| **camel.vault.kubernetes.refresh-enabled** | Define if we want to refresh the secrets on update. | false | Boolean |
| **camel.vault.kubernetes.secrets** | Define the secrets to look at. |  | String |
| **camel.vault.kubernetescm.configmaps** | Define the configmaps to look at. |  | String |
| **camel.vault.kubernetescm.refresh-enabled** | Define if we want to refresh the configmaps on update. | false | Boolean |
| **management.endpoint.camel.access** | Permitted level of access for the camel endpoint. | unrestricted | Access |
| **management.endpoint.camel.cache.time-to-live** | Maximum time that a response can be cached. | 0ms | Duration |
| **management.endpoint.camelroutecontroller.access** | Permitted level of access for the camelroutecontroller endpoint. | unrestricted | Access |
| **management.endpoint.camelroutecontroller.cache.time-to-live** | Maximum time that a response can be cached. | 0ms | Duration |
| **management.endpoint.camelroutes.access** | Permitted level of access for the camelroutes endpoint. | unrestricted | Access |
| **management.endpoint.camelroutes.cache.time-to-live** | Maximum time that a response can be cached. | 0ms | Duration |
| **management.endpoint.camelroutes.read-only** | Whether Camel Routes actuator is in read-only mode. If not in read-only mode then operations to start/stop routes would be enabled. | true | Boolean |
| **management.info.camel.enabled** | Whether to enable Camel info. | true | Boolean |
| **management.server.accesslog.enabled** | Whether access logging is enabled for the management server. When false and using a separate management port, access logs are disabled for actuator endpoints. | true | Boolean |
| **management.server.accesslog.pattern** |  | common | String |
| **camel.main.main-run-controller** | **Deprecated** Whether to use the main run controller to ensure the Spring-Boot application keeps running until being stopped or the JVM terminated. You typically only need this if you run Spring-Boot standalone. If you run Spring-Boot with spring-boot-starter-web then the web container keeps the JVM running. | false | Boolean |
| **camel.main.mdc-logging-keys-pattern** | **Deprecated** Sets the pattern used for determine which custom MDC keys to propagate during message routing when the routing engine continues routing asynchronously for the given message. Setting this pattern to \* will propagate all custom keys. Or setting the pattern to foo\*,bar\* will propagate any keys starting with either foo or bar. Notice that a set of standard Camel MDC keys are always propagated which starts with camel. as key name. The match rules are applied in this order (case insensitive): 1. exact match, returns true 2. wildcard match (pattern ends with a \* and the name starts with the pattern), returns true 3. regular expression match, returns true 4. otherwise returns false Deprecated, use camel-mdc component instead. |  | String |
| **camel.main.use-mdc-logging** | **Deprecated** To turn on MDC logging (deprecated, use camel-mdc component instead). | false | Boolean |

## Auto-configured Camel context

The most important piece of functionality provided by the Camel auto-configuration is `CamelContext` instance. Camel auto-configuration creates a `SpringCamelContext` for you and takes care of the proper initialization and shutdown of that context. The created Camel context is also registered in the Spring application context (under `camelContext` bean name), so you can access it just as any other Spring bean.

```java
@Configuration
public class MyAppConfig {

  @Autowired
  CamelContext camelContext;

  @Bean
  MyService myService() {
    return new DefaultMyService(camelContext);
  }

}
```

## Auto-detecting Camel routes

Camel auto-configuration collects all the `RouteBuilder` instances from the Spring context and automatically injects them into the provided `CamelContext`. That means that creating new Camel routes with the Spring Boot starter is as simple as adding the `@Component` annotated class to your classpath:

```java
@Component
public class MyRouter extends RouteBuilder {

  @Override
  public void configure() throws Exception {
    from("jms:invoices").to("file:/invoices");
  }

}
```

Or creating a new route `RouteBuilder` bean in your `@Configuration` class:

```java
@Configuration
public class MyRouterConfiguration {

  @Bean
  RoutesBuilder myRouter() {
    return new RouteBuilder() {

      @Override
      public void configure() throws Exception {
        from("jms:invoices").to("file:/invoices");
      }

    };
  }

}
```

## Camel properties

Spring Boot auto-configuration automatically connects to [Spring Boot external configuration](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config) (like properties placeholders, OS environment variables or system properties) with the Camel properties support. It basically means that any property defined in `application.properties` file:

```properties
route.from = jms:invoices
```

Or set via system property:

```properties
java -Droute.to=jms:processed.invoices -jar mySpringApp.jar
```

…​can be used as placeholders in Camel route:

```java
@Component
public class MyRouter extends RouteBuilder {

  @Override
  public void configure() throws Exception {
    from("{{route.from}}").to("{{route.to}}");
  }

}
```

## Custom Camel context configuration

If you would like to perform some operations on `CamelContext` bean created by Camel auto-configuration, register `CamelContextConfiguration` instance in your Spring context:

```java
@Configuration
public class MyAppConfig {

  @Bean
  CamelContextConfiguration contextConfiguration() {
    return new CamelContextConfiguration() {
      @Override
      void beforeApplicationStart(CamelContext context) {
        // your custom configuration goes here
      }
    };
  }

}
```

Method beforeApplicationStart\` will be called just before the Spring context is started, so the `CamelContext` instance passed to this callback is fully auto-configured. You can add many instances of `CamelContextConfiguration` into your Spring context - all of them will be executed.

## Auto-configured consumer and producer templates

Camel auto-configuration provides pre-configured `ConsumerTemplate` and `ProducerTemplate` instances. You can simply inject them into your Spring-managed beans:

```java
@Component
public class InvoiceProcessor {

  @Autowired
  private ProducerTemplate producerTemplate;

  @Autowired
  private ConsumerTemplate consumerTemplate;

  public void processNextInvoice() {
    Invoice invoice = consumerTemplate.receiveBody("jms:invoices", Invoice.class);
    ...
    producerTemplate.sendBody("netty-http:http://invoicing.com/received/" + invoice.id());
  }

}
```

By default, consumer templates and producer templates come with the endpoint cache sizes set to 1000. You can change those values via the following Spring properties:

```properties
camel.main.consumer-template-cache-size = 100
camel.main.producer-template-cache-size = 200
```

## Auto-configured TypeConverter

Camel auto-configuration registers a `TypeConverter` instance named `typeConverter` in the Spring context.

```java
@Component
public class InvoiceProcessor {

  @Autowired
  private TypeConverter typeConverter;

  public long parseInvoiceValue(Invoice invoice) {
    String invoiceValue = invoice.grossValue();
    return typeConverter.convertTo(Long.class, invoiceValue);
  }

}
```

### Spring type conversion API bridge

Spring comes with the powerful [type conversion API](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/validation.html#core-convert). Spring API happens to be very similar to the Camel type converter API. As those APIs are so similar, Camel Spring Boot automatically registers a bridge converter (`SpringTypeConverter`) that delegates to the Spring conversion API.That means that out-of-the-box Camel will treat Spring Converters like Camel ones. With this approach you can enjoy both Camel and Spring converters accessed via Camel `TypeConverter` API:

```java
@Component
public class InvoiceProcessor {

  @Autowired
  private TypeConverter typeConverter;

  public UUID parseInvoiceId(Invoice invoice) {
    // Using Spring's StringToUUIDConverter
    UUID id = invoice.typeConverter.convertTo(UUID.class, invoice.getId());
  }

}
```

Under the hood Camel Spring Boot delegates conversion to the Spring’s `ConversionService` instances available in the application context. If no `ConversionService` instance is available, Camel Spring Boot auto-configuration will create one for you.

## Keeping the application alive

Camel applications having this feature enabled launch a new thread on startup for the sole purpose of keeping the application alive by preventing JVM termination. It means that after you start a Camel application with Spring Boot, your application waits for a `Ctrl+C` signal and does not exit immediately.

The controller thread can be activated using the `camel.main.run-controller` to `true`.

```properties
camel.main.run-controller = true
```

Applications using web modules (e.g. importing the `org.springframework.boot:spring-boot-web-starter` module), usually don’t need to use this feature because the application is kept alive by the presence of other non-daemon threads.

## Adding XML routes

By default, you can put Camel XML routes in the classpath under the directory camel, which camel-spring-boot will auto-detect and include. You can configure the directory name or turn this off using the configuration option

```properties
# turn off
camel.main.routes-include-pattern = false
# scan only in the com/foo/routes classpath
camel.main.routes-include-pattern = classpath:com/foo/routes/*.xml
```

The XML files should be Camel XML routes (**not** `<CamelContext>`) such as

```xml
<routes xmlns="http://camel.apache.org/schema/spring">
    <route id="test">
        <from uri="timer://trigger"/>
        <transform>
            <simple>ref:myBean</simple>
        </transform>
        <to uri="log:out"/>
    </route>
</routes>
```

## Testing the JUnit 6 way

For testing, Maven users will need to add the following dependencies to their `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <version>${spring-boot.version}</version> <!-- Use the same version as your Spring Boot version -->
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-test-spring-junit6</artifactId>
    <version>${camel.version}</version> <!-- use the same version as your Camel core version -->
    <scope>test</scope>
</dependency>
```

To test a Camel Spring Boot application, annotate your test class(es) with `@CamelSpringBootTest`. This brings Camel’s Spring Test support to your application, so that you can write tests using [Spring Boot test conventions](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-testing.md).

To get the `CamelContext` or `ProducerTemplate`, you can inject them into the class in the normal Spring manner, using `@Autowired`.

You can also use [camel-test-spring-junit6](../../components/4.18.x/others/test-spring-junit6.md) to configure tests declaratively. This example uses the `@MockEndpoints` annotation to auto-mock an endpoint:

```java
@CamelSpringBootTest
@SpringBootApplication
@MockEndpoints("direct:end")
public class MyApplicationTest {

    @Autowired
    private ProducerTemplate template;

    @EndpointInject("mock:direct:end")
    private MockEndpoint mock;

    @Test
    public void testReceive() throws Exception {
        mock.expectedBodiesReceived("Hello");
        template.sendBody("direct:start", "Hello");
        mock.assertIsSatisfied();
    }

}
```

## Camel Spring Boot Native

One of the most interesting features added to Spring Boot 3 is the support of GraalVM Native Image which allows you to reduce significantly the memory footprint and the startup time of your application. Those improvements are only possible thanks to the Ahead-Of-Time (AOT) compilation that relies on a closed-world assumption which means that everything needs to be known at build type, all dynamic aspects included such as reflection, JNI, Proxy, and resources loading from a ClassLoader.

For now, only Camel routes written using the Java, XML, and/or YAML DSL with basic components that don’t rely on dynamic aspects to work are covered out of the box. For other components, you will need to provide GraalVM some hints to let it know all the dynamic aspects needed by your application either by implementing your custom [`RuntimeHintsRegistrar`](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html#native-image.advanced.custom-hints) or by providing GraalVM JSON hint files that can be generated by the [Tracing Agent](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html#native-image.advanced.using-the-tracing-agent).

For more details about `GraalVM Native Image Support` in Spring Boot please refer to [https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.md)

## Camel Asynchronous Health Checks

Camel health checks can be executed asynchronously via a Task Scheduler so that the result can be cached and the actual health check is executed in background every few seconds. Asynchronous Camel health checks are disabled by default but can be enabled with the following property:

```properties
camel.health.async-camel-health-check=true
```

moreover the Camel health check task scheduler can be customized with the following properties:

```properties
camel.health.healthCheckPoolSize=5
camel.health.healthCheckFrequency=10
camel.health.healthCheckThreadNamePrefix=CamelHealthTaskScheduler
```

## Camel Readiness and Liveness State Indicators

Camel specific Readiness and Liveness checks can be added to a Spring Boot 3 application including respectively in the readiness and livenss groups camelLivenessStateHealthIndicator and camelReadinessStateHealthIndicator. In particular:

```properties
management.endpoint.health.group.liveness.include=livenessState,camelLivenessState
management.endpoint.health.group.readiness.include=readinessState,camelReadinessState
```

Using Camel specific readiness and liveness health indicators, the probes will be augmented with camel components health checks that support this feature. In enable the probes locally, they need to be enabled

```properties
management.endpoint.health.probes.enabled=true
```

Finally, [http://localhost:8080/actuator/health/liveness](http://localhost:8080/actuator/health/liveness) will show the updated probe.

## Management Access Log Control

When running actuator endpoints on a separate management port, you can disable access logging for the management context while keeping access logs for the main application. This is useful to avoid cluttering access logs with health check requests.

> **Note**
> This feature requires `management.server.port` to be different from the main application port.

### Tomcat

```properties
server.tomcat.accesslog.enabled=true
server.tomcat.accesslog.directory=logs
server.tomcat.basedir=./target
management.server.port=9090
management.server.accesslog.enabled=false
```

Result: Main app logs to `./target/logs/access_log.<date>.log`, actuator has no access logs.

### Undertow

```properties
server.undertow.accesslog.enabled=true
server.undertow.accesslog.dir=logs
management.server.port=9090
management.server.accesslog.enabled=false
```

Result: Main app logs to `logs/access_log.log`, actuator has no access logs.

#### Camel Logging to Control Management Access Log

This is valid only when using `spring-boot-starter-undertow`.

If you want to defer the http access log control to whatever camel logging mechanism, you have to set `management.server.undertow.accesslog.use-camel-logging=true`. Optionally you can set a message pattern with `management.server.accesslog.pattern=combined`.

Example:

```properties
management.server.undertow.accesslog.use-camel-logging=true
management.server.accesslog.pattern=combined
```

## Security Policy

Camel Spring Boot automatically enforces security policies at startup, detecting insecure configuration such as disabled SSL verification, plain-text secrets, enabled Java deserialization, or development-only features.

The global policy controls how Camel reacts when insecure configuration is detected:

```properties
# allow  — no warnings, allow the configuration
# warn   — log a warning at startup (default)
# fail   — throw an exception and prevent startup
camel.security.policy=warn
```

### Category Overrides

Each security category can override the global policy independently:

```properties
camel.security.policy=fail
camel.security.insecure-ssl-policy=warn
camel.security.insecure-serialization-policy=warn
camel.security.insecure-dev-policy=allow
camel.security.secret-policy=fail
```

To exclude specific properties from all checks, use `allowed-properties`:

```properties
camel.security.allowed-properties=camel.component.http.trustAllCertificates,camel.component.netty.allowJavaSerializedObject
```

### Per-Environment Policies with Spring Profiles

Spring profiles allow you to enforce strict security in production while keeping a relaxed policy during development.

In `application-prod.properties`:

```properties
camel.security.policy=fail
```

In `application-dev.properties`:

```properties
camel.security.policy=allow
```

Activate the profile via `spring.profiles.active`:

```properties
# application.properties
spring.profiles.active=dev
```

Or at runtime:

```bash
java -Dspring.profiles.active=prod -jar myApp.jar
```

This way, developers can freely use options like `trustAllCertificates=true` locally, while production deployments will fail fast if any insecure configuration is detected.

## Virtual Threads Support

Camel Spring Boot provides comprehensive support for JDK 21+ Virtual Threads, offering significant performance improvements for I/O-intensive applications. Virtual threads are lightweight threads that can dramatically reduce memory overhead and improve scalability compared to traditional platform threads.

### Enabling Virtual Threads

To enable virtual threads in your Camel Spring Boot application, simply set the Spring Boot virtual threads property:

```properties
spring.threads.virtual.enabled=true
```

When this property is set to `true`, Camel Spring Boot automatically:

1.  **Enables Camel Virtual Threads**: Automatically sets `camel.threads.virtual.enabled=true`
    
2.  **Optimizes Executors**: Configures components to use `SimpleAsyncTaskExecutor` which is optimized for virtual threads
    
3.  **Updates Component Configurations**: Automatically configures supported components for optimal virtual thread performance
    

### Automatic Configuration

When virtual threads are enabled, Camel Spring Boot provides automatic configuration for several components:

#### Platform HTTP Component

The Platform HTTP component automatically uses `SimpleAsyncTaskExecutor` when virtual threads are enabled, providing better performance for HTTP endpoints:

```java
@Component
public class MyRoute extends RouteBuilder {
    @Override
    public void configure() {
        from("platform-http:/api/data")
            .to("http://external-service/api")  // Benefits from virtual threads
            .setBody(constant("Response processed"));
    }
}
```

##### Undertow Metrics

When using the Platform HTTP component with Undertow as the underlying web server, comprehensive metrics are automatically available through Spring Boot Actuator. To enable Undertow metrics:

1.  Exclude Tomcat from Spring Boot Web starter in your `pom.xml`:
    
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    ```
    
2.  Add Spring Boot Undertow starter:
    
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-undertow</artifactId>
    </dependency>
    ```
    
3.  Include Spring Boot Actuator:
    
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    ```
    
4.  Expose actuator metrics and enable Undertow session statistics
    
    ```properties
    server.undertow.options.server.ENABLE_STATISTICS=true
    management.endpoints.web.exposure.include=metrics,health,info
    ```
    

With this configuration, Undertow-specific metrics will be automatically exposed under `/actuator/metrics`, providing detailed insights into HTTP server including: session management, connection pools and thread usage These metrics help monitor the health and performance of your Platform HTTP endpoints running on Undertow.

#### JMS and AMQP Components

JMS and AMQP components benefit from virtual threads through the global virtual thread configuration. When `spring.threads.virtual.enabled=true` is set, these components will use virtual threads for message processing through the standard Spring Boot virtual thread integration:

```properties
spring.threads.virtual.enabled=true
# JMS and AMQP components will automatically benefit from virtual threads
```

### Manual Configuration

If you need to manually configure specific components for virtual threads, you can use the `VirtualThreadAwareExecutorFactory`:

```java
@Configuration
public class VirtualThreadConfig {

    @Bean
    @ConditionalOnProperty(name = "spring.threads.virtual.enabled", havingValue = "true")
    public TaskExecutor customTaskExecutor() {
        return VirtualThreadAwareExecutorFactory.createOptimalExecutor();
    }
}
```

### Performance Benefits

Virtual threads provide several performance advantages:

-   **Reduced Memory Overhead**: Virtual threads use significantly less memory than platform threads
    
-   **Higher Concurrency**: Support for millions of concurrent virtual threads
    
-   **Better Resource Utilization**: Reduced thread pool contention and context switching
    
-   **Simplified Programming Model**: No need for complex async/reactive programming patterns
    

### Best Practices

When using virtual threads with Camel Spring Boot:

1.  **Avoid Thread Pinning**: Minimize use of `synchronized` blocks in route processing
    
2.  **Use Simple Async Executors**: Let Camel Spring Boot auto-configure optimal executors
    
3.  **Monitor Performance**: Use Spring Boot Actuator to monitor virtual thread usage
    
4.  **Test Thoroughly**: Validate behavior under load with virtual threads enabled
    

### Example Application

Here’s a complete example of a Camel Spring Boot application optimized for virtual threads:

```properties
# application.properties
spring.threads.virtual.enabled=true
camel.main.routes-include-pattern=classpath:routes/*
```

```java
@SpringBootApplication
public class VirtualThreadsApplication {

    public static void main(String[] args) {
        SpringApplication.run(VirtualThreadsApplication.class, args);
    }

    @Component
    public static class ApiRoutes extends RouteBuilder {
        @Override
        public void configure() {
            from("platform-http:/api/process")
                .log("Processing request with virtual thread: ${threadName}")
                .to("http://external-api/data")
                .transform(body().prepend("Processed: "))
                .setHeader("X-Thread-Type", constant("virtual"));
        }
    }
}
```

### Compatibility

Virtual threads support requires:

-   **JDK 21+**: Virtual threads are a JDK 21+ feature
    
-   **Spring Boot 3.2+**: Spring Boot virtual thread support
    
-   **Camel 4.0+**: Camel virtual thread integration
    

### Troubleshooting

If you encounter issues with virtual threads:

1.  **Check JDK Version**: Ensure you’re running JDK 21 or later
    
2.  **Verify Property Setting**: Confirm `spring.threads.virtual.enabled=true` is set
    
3.  **Review Logs**: Check for virtual thread configuration messages in startup logs
    
4.  **Monitor Thread Usage**: Use JVM monitoring tools to observe virtual thread behavior