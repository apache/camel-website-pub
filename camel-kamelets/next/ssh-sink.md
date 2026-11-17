# ![ssh sink](_images/kamelets/ssh-sink.svg) SSH Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the text of each message as a command on a remote server over SSH, and returns what the command prints.

Use it to run a script or a maintenance command on a server when something happens, for example restart a service after a deployment or clear a cache when data changes. To run a fixed command on a schedule and read its output, use `ssh-source`; to run a command on the machine of the integration, use `exec-sink`.

Input: the body is the command to run, as text, such as `systemctl restart myapp`. It runs in the shell of `username`, so it can hold several commands separated by `;`.

Output: the body afterwards is what the command printed on its standard output, as a stream. The `CamelSshExitValue` header holds the exit code of the command, and `CamelSshStderr` what it printed on its standard error, as a stream.

Good to know: it runs whatever command it receives, with the rights of `username`. Never send it messages from an untrusted source, and log in with an account that may do only what is needed. A command that ends with an exit code other than 0 does not fail the message: check `CamelSshExitValue`. The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SSH server, without a port. | string |  | server.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SSH server, usually 22. | string | 22 |  |
| **password** | Password | **Required** The password of `username` on the SSH server. | string |  |  |
| **username** | Username | **Required** The user to log in as. The commands run with the rights of this user. | string |  |  |
| **knownHostsResource** | Known Hosts Resource | A known\_hosts file that holds the key of the server, starting with `file:`, `classpath:`, `http:` or `https:`. Its lines can be made with `ssh-keyscan`. A server whose key does not match is refused. When it is not set, the key of the server is not checked, so any server is accepted. | string |  | file:/etc/ssh/known\_hosts |

## Dependencies

At runtime, the `ssh-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ssh
    
-   camel:gson
    
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
            uri: "kamelet:ssh-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SSH Sink Kamelet Description

### Secure Shell Integration

This Kamelet provides integration with SSH (Secure Shell) for executing remote commands and operations on remote systems over encrypted connections.

### Remote Command Execution

The body of each message is run as a command in the shell of `username`, and the body afterwards is what the command printed on its standard output. The exit code is in the `CamelSshExitValue` header and the standard error in `CamelSshStderr`; an exit code other than 0 does not fail the message. The Kamelet runs whatever command it receives, so never place it after messages from an untrusted source.

### Authentication Methods

The Kamelet logs in with a username and a password. The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted.

### Security Features

SSH provides comprehensive security features:

-   Strong encryption for all communications
    
-   Host key verification, when `knownHostsResource` is set
    
-   User authentication and authorization
    
-   Session integrity and confidentiality
    

### Remote Administration

Common use cases include:

-   System administration and maintenance
    
-   Automated deployment and configuration
    
-   Remote monitoring and diagnostics
    
-   File operations and transfers
    
-   Service management and control
    

### Cross-Platform Support

Works across different operating systems and platforms, providing consistent secure remote access capabilities for heterogeneous environments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-sink.kamelet.yaml)