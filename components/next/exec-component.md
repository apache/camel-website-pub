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

The Exec component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer) | The timeout, in milliseconds, after which the executable should be terminated. If execution has not completed within the timeout, the component will send a termination request. |  | long |
| **workingDir** (producer) | The directory in which the command should be executed. If null, the working directory of the current process will be used. |  | String |
| **allowControlHeaders** (advanced) | Whether \\{code CamelExec} in-headers may override URI options (default false since Camel 4.20). When false, CamelExecCommandExecutable, CamelExecCommandArgs, CamelExecCommandOutFile, CamelExecCommandWorkingDir, CamelExecCommandTimeout, CamelExecExitValues, CamelExecUseStderrOnEmptyStdout, and CamelExecCommandLogLevel are ignored. Enable only when those headers come from a trusted route, not from an untrusted consumer. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **binding** (advanced) | To use a custom org.apache.commons.exec.ExecBinding for advanced use-cases. |  | ExecBinding |
| **commandExecutor** (advanced) | To use a custom org.apache.commons.exec.ExecCommandExecutor that customizes the command execution. The default command executor utilizes the commons-exec library, which adds a shutdown hook for every executed command. |  | ExecCommandExecutor |

## Endpoint Options

The Exec endpoint is configured using URI syntax:

exec:executable

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **executable** (producer) | **Required** Sets the executable to be executed. The executable must not be empty or null. |  | String |

### Query Parameters

   
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
| **allowControlHeaders** (advanced) | Whether \\{code CamelExec} in-headers may override URI options (default false since Camel 4.20). When false, CamelExecCommandExecutable, CamelExecCommandArgs, CamelExecCommandOutFile, CamelExecCommandWorkingDir, CamelExecCommandTimeout, CamelExecExitValues, CamelExecUseStderrOnEmptyStdout, and CamelExecCommandLogLevel are ignored. Enable only when those headers come from a trusted route, not from an untrusted consumer. | false | boolean |
| **binding** (advanced) | To use a custom org.apache.commons.exec.ExecBinding for advanced use-cases. |  | ExecBinding |
| **commandExecutor** (advanced) | To use a custom org.apache.commons.exec.ExecCommandExecutor that customizes the command execution. The default command executor utilizes the commons-exec library, which adds a shutdown hook for every executed command. |  | ExecCommandExecutor |

## Message Headers

The Exec component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelExecCommandExecutable** (in) Constant: [`EXEC_COMMAND_EXECUTABLE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_EXECUTABLE) | The name of the system command that will be executed. Overrides executable in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | String |
| **CamelExecCommandArgs** (in) Constant: [`EXEC_COMMAND_ARGS`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_ARGS) | Command-line argument(s) to pass to the executed process. The argument(s) is/are used literally - no quoting is applied. Overrides any existing args in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | List or String |
| **CamelExecCommandOutFile** (in) Constant: [`EXEC_COMMAND_OUT_FILE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_OUT_FILE) | The name of a file, created by the executable, that should be considered as its output. Overrides any existing outFile in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | String |
| **CamelExecCommandWorkingDir** (in) Constant: [`EXEC_COMMAND_WORKING_DIR`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_WORKING_DIR) | The directory in which the command should be executed. Overrides any existing workingDir in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | String |
| **CamelExecCommandTimeout** (in) Constant: [`EXEC_COMMAND_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_TIMEOUT) | The timeout, in milliseconds, after which the executable should be terminated. Overrides any existing timeout in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | long |
| **CamelExecExitValues** (in) Constant: [`EXEC_COMMAND_EXIT_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_EXIT_VALUES) | The exit values for successful execution of the process. Overrides any existing exitValues in the URI. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | String |
| **CamelExecStderr** (out) Constant: [`EXEC_STDERR`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_STDERR) | The value of this header points to the standard error stream (stderr) of the executable. If no stderr is written, the value is null. |  | InputStream |
| **CamelExecExitValue** (out) Constant: [`EXEC_EXIT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_EXIT_VALUE) | The value of this header is the _exit value_ of the executable. Non-zero exit values typically indicate abnormal termination. Note that the exit value is OS-dependent. |  | int |
| **CamelExecUseStderrOnEmptyStdout** (in) Constant: [`EXEC_USE_STDERR_ON_EMPTY_STDOUT`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_USE_STDERR_ON_EMPTY_STDOUT) | Indicates that when stdout is empty, this component will populate the Camel Message Body with stderr. This behavior is disabled (false) by default. Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | boolean |
| **CamelExecCommandLogLevel** (in) Constant: [`EXEC_COMMAND_LOG_LEVEL`](https://javadoc.io/doc/org.apache.camel/camel-exec/latest/org/apache/camel/component/exec/ExecBinding.html#EXEC_COMMAND_LOG_LEVEL) | Logging level to be used for commands during execution. The default value is DEBUG. Possible values are TRACE, DEBUG, INFO, WARN, ERROR or OFF (Values of LoggingLevel enum). Requires allowControlHeaders=true on the exec endpoint or component (default is false since Camel 4.20). |  | String |

## Usage

### Control headers

Since Camel 4.20, the exec in-headers that override URI options (`CamelExecCommand*`, `CamelExecExitValues`, and `CamelExecUseStderrOnEmptyStdout`) are disabled by default. This prevents untrusted message sources from redirecting command execution. To use dynamic executable, arguments, working directory, or other command settings from headers, enable the opt-in flag on the endpoint or component:

-   Java
    
-   YAML
    

```java
from("direct:run")
    .setHeader("CamelExecCommandArgs", constant("ARGS-WORK"))
    .to("exec:echo?allowControlHeaders=true");
```

```yaml
- route:
    from:
      uri: direct:run
      steps:
        - setHeader:
            name: CamelExecCommandArgs
            constant: "ARGS-WORK"
        - to:
            uri: exec:echo
            parameters:
              allowControlHeaders: true
```

When `allowControlHeaders` is `false` (the default), those in-headers on the exchange are ignored (they are not removed), and a WARN is logged once per exec endpoint. URI parameters such as `args` continue to work as before.

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

-   Java
    
-   XML
    
-   YAML
    

```java
// The body is an ExecResult instance, which can be auto-converted to String (stdout output)
from("direct:exec")
    .to("exec:wc?args=--words /usr/share/dict/words")
    .to("log:result");
```

```xml
<!-- The body is an ExecResult instance, which can be auto-converted to String (stdout output) -->
<route>
  <from uri="direct:exec"/>
  <to uri="exec:wc?args=--words /usr/share/dict/words"/>
  <to uri="log:result"/>
</route>
```

```yaml
# The body is an ExecResult instance, which can be auto-converted to String (stdout output)
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: exec:wc
            parameters:
              args: "--words /usr/share/dict/words"
        - to:
            uri: log:result
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

-   Java
    
-   XML
    
-   YAML
    

```java
// When outFile is specified, the body is the content of that file (as InputStream)
from("direct:exec")
    .to("exec:ant.bat?args=-f CamelExecBuildFile.xml -l CamelExecOutFile.txt&outFile=CamelExecOutFile.txt")
    .to("log:result");
```

```xml
<!-- When outFile is specified, the body is the content of that file (as InputStream) -->
<route>
  <from uri="direct:exec"/>
  <to uri="exec:ant.bat?args=-f CamelExecBuildFile.xml -l CamelExecOutFile.txt&amp;outFile=CamelExecOutFile.txt"/>
  <to uri="log:result"/>
</route>
```

```yaml
# When outFile is specified, the body is the content of that file (as InputStream)
- route:
    from:
      uri: direct:exec
      steps:
        - to:
            uri: exec:ant.bat
            parameters:
              args: "-f CamelExecBuildFile.xml -l CamelExecOutFile.txt"
              outFile: CamelExecOutFile.txt
        - to:
            uri: log:result
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