# ![exec sink](_images/kamelets/exec-sink.svg) Exec Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Execute system commands

## Configuration Options

The following table summarizes the configuration options available for the `exec-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **executable** | Executable Command | **Required** The command to execute. | string |  |  |

## Dependencies

At runtime, the `exec-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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

### Optional Headers

The Kamelet supports the following optional headers: - `args` / `ce-args`: Command line arguments to pass to the executable

### Output

The Kamelet returns the standard output (stdout) of the executed command as the response body.

### Security Considerations

Use this Kamelet with caution as it executes system commands. Ensure proper validation and security measures are in place when using dynamic command execution.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/exec-sink.kamelet.yaml)