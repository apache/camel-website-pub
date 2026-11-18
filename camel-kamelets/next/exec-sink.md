# ![exec sink](_images/kamelets/exec-sink.svg) Exec Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a program or command on the machine where the integration runs, once for each message, with the body as its standard input.

Use it to hand each message to an existing script or command-line tool, for example a script that imports a file or a tool that converts data, and to use what the program prints in the next step.

Input: the body is written to the standard input of the program, when it is text, bytes, a stream or a file. Another body, or no body, runs the program without input.

Output: when it is used inside a route, the body afterwards is what the program printed on its standard output, as a stream, or no body when it printed nothing. The `CamelExecExitValue` header is the exit code of the program, and `CamelExecStderr` what it printed on its standard error.

Good to know: this Kamelet runs programs by design, with the rights of the integration, so never place it after a source of untrusted messages. `executable` is only the name or path of the program, and its arguments go in `args`. Only the options decide what runs: `CamelExecCommand*` headers on the message are ignored. The program is started directly, not through a shell, so `*`, `$HOME`, `|`, `>` and `;` in the arguments are passed on as they are. A program that ends with an error exit code does not fail the message; check `CamelExecExitValue`, or list the exit codes that mean success in `exitValues`. A program that is not found, or a `workingDir` that does not exist, fails the message. A program that runs longer than `commandTimeout` is stopped.

## Configuration Options

The following table summarizes the configuration options available for the `exec-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **executable** | Executable Command | **Required** The name of the program to run, found on the `PATH` of the machine, or its full path, without arguments. A value with a space, such as `ls -l`, fails, because no program has that name; put the arguments in `args`. | string |  | /opt/scripts/import-order.sh |
| **args** | Arguments | The arguments to give to the program, separated by spaces, such as `-l /data`. Put an argument that contains a space in double or single quotes, such as `--name "John Doe"`; the program gets the text inside the quotes as one argument, without the quotes. To pass a quote character, put the argument in the other kind of quotes, such as `"it’s"`. When not set, the program runs without arguments. | string |  | \--input /data/orders.csv --name "John Doe" |
| **commandTimeout** | Timeout | How long the program may run, in milliseconds, such as 60000 for one minute. A program that runs longer is stopped. The message then carries on, with what the program printed so far as the body and the exit code of the stopped program, such as 143, in `CamelExecExitValue`; set `exitValues` to fail the message instead. When not set, the Kamelet waits until the program ends. | integer |  | 60000 |
| **exitValues** | Exit Values | The exit codes that mean the program succeeded, separated by commas without spaces, such as `0` or `0,1`. The message fails when the program ends with another exit code, or is stopped by `commandTimeout`. When not set, any exit code is accepted and the message carries on. | string |  | 0 |
| **workingDir** | Working Directory | The directory to run the program in, as a full path. A directory that does not exist fails the message. When not set, the program runs in the working directory of the integration. | string |  | /opt/scripts |

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

### Arguments

The arguments of the program go in **Arguments**, separated by spaces. An argument that contains a space goes in double or single quotes. The program is started directly, not through a shell, so `*`, `$HOME`, `|`, `>` and `;` are passed to it as they are.

For example, to run a script with two options in `/opt/scripts`, stop it after one minute, and fail the message when it does not end with exit code 0:

```yaml
executable: /opt/scripts/import-order.sh
args: '--input /data/orders.csv --name "John Doe"'
workingDir: /opt/scripts
commandTimeout: 60000
exitValues: "0"
```

The script gets four arguments: `--input`, `/data/orders.csv`, `--name` and `John Doe`.

### Output

The Kamelet returns the standard output (stdout) of the executed command as the response body.

### Security Considerations

Use this Kamelet with caution as it executes system commands. Ensure proper validation and security measures are in place when using dynamic command execution.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml)