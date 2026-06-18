# Exec

**Since Camel 2.3**

**Only producer is supported**

The Exec component can be used to execute system commands.

## Dependencies

Maven users need to add the following dependency to their `pom.xml`

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-exec</artifactId>
  <version>${camel-version}</version>
</dependency>
```

Where `${camel-version`} must be replaced by the actual version of Camel.

## URI format

exec://executable\[?options\]

Where `executable` is the name, or file path, of the system command that will be executed. If executable name is used (e.g. `exec:java`), the executable must in the system path.

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

The Exec component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer) | The timeout, in milliseconds, after which the executable should be terminated. If execution has not completed within the timeout, the component will send a termination request. |  | long |
| **workingDir** (producer) | The directory in which the command should be executed. If null, the working directory of the current process will be used. |  | String |
| **allowControlHeaders** (advanced) | Whether to allow to use Camel headers or not (default false). Enabling this allows to specify dynamic command line arguments via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **binding** (advanced) | To use a custom org.apache.commons.exec.ExecBinding for advanced use-cases. |  | ExecBinding |
| **commandExecutor** (advanced) | To use a custom org.apache.commons.exec.ExecCommandExecutor that customizes the command execution. The default command executor utilizes the commons-exec library, which adds a shutdown hook for every executed command. |  | ExecCommandExecutor |

## Endpoint Options

The Exec endpoint is configured using URI syntax:

exec:executable

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **executable** (producer) | **Required** Sets the executable to be executed. The executable must not be empty or null. |  | String |

### Query Parameters (11 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **args** (producer) | The arguments may be one or many whitespace-separated tokens. |  | String |
| **commandLogLevel** (producer) | 
Logging level to be used for commands during execution. The default value is DEBUG. Possible values are TRACE, DEBUG, INFO, WARN, ERROR or OFF. (Values of ExecCommandLogLevelType enum).

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | DEBUG | LoggingLevel |
| **exitValues** (producer) | The exit values of successful executions. If the process exits with another value, an exception is raised. Comma-separated list of exit values. And empty list (the default) sets no expected exit values and disables the check. |  | String |
| **outFile** (producer) | The name of a file, created by the executable, that should be considered as its output. If no outFile is set, the standard output (stdout) of the executable will be used instead. |  | String |
| **timeout** (producer) | The timeout, in milliseconds, after which the executable should be terminated. If execution has not completed within the timeout, the component will send a termination request. |  | long |
| **useStderrOnEmptyStdout** (producer) | A boolean indicating that when stdout is empty, this component will populate the Camel Message Body with stderr. This behavior is disabled (false) by default. | false | boolean |
| **workingDir** (producer) | The directory in which the command should be executed. If null, the working directory of the current process will be used. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowControlHeaders** (advanced) | Whether to allow to use Camel headers or not (default false). Enabling this allows to specify dynamic command line arguments via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **binding** (advanced) | To use a custom org.apache.commons.exec.ExecBinding for advanced use-cases. |  | ExecBinding |
| **commandExecutor** (advanced) | To use a custom org.apache.commons.exec.ExecCommandExecutor that customizes the command execution. The default command executor utilizes the commons-exec library, which adds a shutdown hook for every executed command. |  | ExecCommandExecutor |

## Message Headers

The Exec component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelExecCommandExecutable** (in) Constant: [`EXEC_COMMAND_EXECUTABLE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_EXECUTABLE) | The name of the system command that will be executed. Overrides executable in the URI. |  | String |
| **CamelExecCommandArgs** (in) Constant: [`EXEC_COMMAND_ARGS`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_ARGS) | Command-line argument(s) to pass to the executed process. The argument(s) is/are used literally - no quoting is applied. Overrides any existing args in the URI. |  | List or String |
| **CamelExecCommandOutFile** (in) Constant: [`EXEC_COMMAND_OUT_FILE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_OUT_FILE) | The name of a file, created by the executable, that should be considered as its output. Overrides any existing outFile in the URI. |  | String |
| **CamelExecCommandWorkingDir** (in) Constant: [`EXEC_COMMAND_WORKING_DIR`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_WORKING_DIR) | The directory in which the command should be executed. Overrides any existing workingDir in the URI. |  | String |
| **CamelExecCommandTimeout** (in) Constant: [`EXEC_COMMAND_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_TIMEOUT) | The timeout, in milliseconds, after which the executable should be terminated. Overrides any existing timeout in the URI. |  | long |
| **CamelExecExitValues** (in) Constant: [`EXEC_COMMAND_EXIT_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_EXIT_VALUES) | The exit values for successful execution of the process. Overrides any existing exitValues in the URI. |  | String |
| **CamelExecStderr** (out) Constant: [`EXEC_STDERR`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_STDERR) | The value of this header points to the standard error stream (stderr) of the executable. If no stderr is written, the value is null. |  | InputStream |
| **CamelExecExitValue** (out) Constant: [`EXEC_EXIT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_EXIT_VALUE) | The value of this header is the _exit value_ of the executable. Non-zero exit values typically indicate abnormal termination. Note that the exit value is OS-dependent. |  | int |
| **CamelExecUseStderrOnEmptyStdout** (in) Constant: [`EXEC_USE_STDERR_ON_EMPTY_STDOUT`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_USE_STDERR_ON_EMPTY_STDOUT) | Indicates that when stdout is empty, this component will populate the Camel Message Body with stderr. This behavior is disabled (false) by default. |  | boolean |
| **CamelExecCommandLogLevel** (in) Constant: [`EXEC_COMMAND_LOG_LEVEL`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_LOG_LEVEL) | Logging level to be used for commands during execution. The default value is DEBUG. Possible values are TRACE, DEBUG, INFO, WARN, ERROR or OFF (Values of LoggingLevel enum). |  | String |

## Usage

### Message body

If the component receives an `in` message body that is convertible to `java.io.InputStream`, it is used to feed input to the executable via its standard input (`stdin`). After execution, [the message body](http://camel.apache.org/exchange.md) is the result of the execution. That is, an `org.apache.camel.components.exec.ExecResult` instance containing the `stdout`, `stderr`, _exit value_, and the _out file_.

This component supports the following `ExecResult` [type converters](http://camel.apache.org/type-converter.md) for convenience:

 
| From | To |
| --- | --- |
| `ExecResult` | `java.io.InputStream` |
| `ExecResult` | `String` |
| `ExecResult` | `byte []` |
| `ExecResult` | `org.w3c.dom.Document` |

If an _out file_ is specified (in the endpoint via `outFile` or the message headers via `ExecBinding.EXEC_COMMAND_OUT_FILE`), the converters will return the content of the _out file_. If no _out file_ is used, then this component will convert the `stdout` of the process to the target type. For more details, please refer to the [usage examples](#) below.

## Examples

### Executing word count (Linux)

The example below executes `wc` (word count, Linux) to count the words in file `/usr/share/dict/words`. The word count (_output_) is written to the standard output stream of `wc`:

_Java-only: route with inline Processor to handle ExecResult_

```java
from("direct:exec")
.to("exec:wc?args=--words /usr/share/dict/words")
.process(new Processor() {
     public void process(Exchange exchange) throws Exception {
       // By default, the body is ExecResult instance
       assertIsInstanceOf(ExecResult.class, exchange.getIn().getBody());
       // Use the Camel Exec String type converter to convert the ExecResult to String
       // In this case, the stdout is considered as output
       String wordCountOutput = exchange.getIn().getBody(String.class);
       // do something with the word count
     }
});
```

### Executing `java`

The example below executes `java` with two arguments: `-server` and `-version`, if `java` is in the system path.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:exec")
    .to("exec:java?args=-server -version");
```

```xml
<route>
  <from uri="direct:exec"/>
  <to uri="exec:java?args=-server -version"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: exec:java
            parameters:
              args: "-server -version"
```

The example below executes `java` in `c:\temp` with three arguments: `-server`, `-version` and the system property `user.name`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:exec")
    .to("exec:c:/program files/jdk/bin/java?args=-server -version -Duser.name=Camel&workingDir=c:/temp");
```

```xml
<route>
  <from uri="direct:exec"/>
  <to uri="exec:c:/program files/jdk/bin/java?args=-server -version -Duser.name=Camel&amp;workingDir=c:/temp"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: "exec:c:/program files/jdk/bin/java"
            parameters:
              args: "-server -version -Duser.name=Camel"
              workingDir: "c:/temp"
```

### Executing Ant scripts

The following example executes [Apache Ant](http://ant.apache.org/) (Windows only) with the build file `CamelExecBuildFile.xml`, provided that `ant.bat` is in the system path, and that `CamelExecBuildFile.xml` is in the current directory.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:exec")
    .to("exec:ant.bat?args=-f CamelExecBuildFile.xml");
```

```xml
<route>
  <from uri="direct:exec"/>
  <to uri="exec:ant.bat?args=-f CamelExecBuildFile.xml"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: exec:ant.bat
            parameters:
              args: "-f CamelExecBuildFile.xml"
```

In the next example, the `ant.bat` command redirects its output to `CamelExecOutFile.txt` with `-l`. The file `CamelExecOutFile.txt` is used as the _out file_ with `outFile=CamelExecOutFile.txt`. The example assumes that `ant.bat` is in the system path, and that `CamelExecBuildFile.xml` is in the current directory.

_Java-only: route with inline Processor to handle output file_

```java
from("direct:exec")
.to("exec:ant.bat?args=-f CamelExecBuildFile.xml -l CamelExecOutFile.txt&outFile=CamelExecOutFile.txt")
.process(new Processor() {
     public void process(Exchange exchange) throws Exception {
        InputStream outFile = exchange.getIn().getBody(InputStream.class);
        assertIsInstanceOf(InputStream.class, outFile);
        // do something with the out file here
     }
  });
```

### Executing `echo` (Windows)

Commands such as `echo` and `dir` can be executed only with the command interpreter of the operating system. This example shows how to execute such a command - `echo` - in Windows.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:exec")
    .to("exec:cmd?args=/C echo echoString");
```

```xml
<route>
  <from uri="direct:exec"/>
  <to uri="exec:cmd?args=/C echo echoString"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: exec:cmd
            parameters:
              args: "/C echo echoString"
```

## Spring Boot Auto-Configuration

When using exec with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-exec-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.exec.allow-control-headers** | Whether to allow to use Camel headers or not (default false). Enabling this allows to specify dynamic command line arguments via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.exec.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.exec.binding** | To use a custom org.apache.commons.exec.ExecBinding for advanced use-cases. The option is a org.apache.camel.component.exec.ExecBinding type. |  | ExecBinding |
| **camel.component.exec.command-executor** | To use a custom org.apache.commons.exec.ExecCommandExecutor that customizes the command execution. The default command executor utilizes the commons-exec library, which adds a shutdown hook for every executed command. The option is a org.apache.camel.component.exec.ExecCommandExecutor type. |  | ExecCommandExecutor |
| **camel.component.exec.enabled** | Whether to enable auto configuration of the exec component. This is enabled by default. |  | Boolean |
| **camel.component.exec.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.exec.timeout** | The timeout, in milliseconds, after which the executable should be terminated. If execution has not completed within the timeout, the component will send a termination request. |  | Long |
| **camel.component.exec.working-dir** | The directory in which the command should be executed. If null, the working directory of the current process will be used. |  | String |