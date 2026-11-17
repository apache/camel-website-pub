# ![exec sink](_images/kamelets/exec-sink.svg) Exec Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a program or command on the machine where the integration runs, once for each message, with the body as its standard input.

Use it to hand each message to an existing script or command-line tool, for example a script that imports a file or a tool that converts data, and to use what the program prints in the next step.

Input: the body is written to the standard input of the program, when it is text, bytes, a stream or a file. Another body, or no body, runs the program without input.

Output: when it is used inside a route, the body afterwards is what the program printed on its standard output, as a stream, or no body when it printed nothing. The `CamelExecExitValue` header is the exit code of the program, and `CamelExecStderr` what it printed on its standard error.

Good to know: this Kamelet runs programs by design, with the rights of the integration, so never place it after a source of untrusted messages. `executable` is only the name or path of the program: arguments cannot be given, so to run a command with arguments, put it in a script. A program that ends with an error exit code does not fail the message; check `CamelExecExitValue`. A program that is not found fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `exec-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **executable** | Executable Command | **Required** The name of the program to run, found on the `PATH` of the machine, or its full path, without arguments. A value with a space, such as `ls -l`, fails, because no program has that name. | string |  | /opt/scripts/import-order.sh |

## Dependencies

At runtime, the `exec-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:exec
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:exec-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Exec Sink Kamelet Description

### Command Execution

This Kamelet executes system commands on the local machine. It requires an executable command to be specified.

### Output

The Kamelet returns the standard output (stdout) of the executed command as the response body.

### Security Considerations

Use this Kamelet with caution as it executes system commands. Ensure proper validation and security measures are in place when using dynamic command execution.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml)