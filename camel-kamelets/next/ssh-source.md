# ![ssh source](_images/kamelets/ssh-source.svg) SSH Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a command on a remote server over SSH again and again, at a regular interval, and sends what the command prints as a message each time.

Use it to watch a server without installing anything on it, for example check the free disk space, the state of a service or the last lines of a log file every minute. To run a command for each incoming message instead, use `ssh-sink`.

Output: the body is what the command printed on its standard output, as text. The `CamelSshExitValue` header holds the exit code of the command, and `CamelSshStderr` what it printed on its standard error, as a stream.

Good to know: it runs `pollCommand` with the rights of `username`, so log in with an account that may do only what is needed. It runs it every half second by default; set `delay` to how often you need it. A command that fails still sends a message, with its exit code in `CamelSshExitValue`. The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SSH server, without a port. | string |  | server.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SSH server, usually 22. | string | 22 |  |
| **password** | Password | **Required** The password of `username` on the SSH server. | string |  |  |
| **pollCommand** | Poll Command | **Required** The command to run each time, as you would type it in a shell on the server. It can hold several commands separated by `;`. | string |  | df -h / |
| **username** | Username | **Required** The user to log in as. The command runs with the rights of this user. | string |  |  |
| **delay** | Delay | How long to wait between two runs of the command, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **knownHostsResource** | Known Hosts Resource | A known\_hosts file that holds the key of the server, starting with `file:`, `classpath:`, `http:` or `https:`. Its lines can be made with `ssh-keyscan`. A server whose key does not match is refused. When it is not set, the key of the server is not checked, so any server is accepted. | string |  | file:/etc/ssh/known\_hosts |

## Dependencies

At runtime, the `ssh-source` Kamelet relies upon the presence of the following dependencies:

-   camel:ssh
    
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
      uri: "kamelet:ssh-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SSH Source Kamelet Description

### Authentication

This Kamelet supports SSH authentication using username and password credentials. It can execute commands on remote SSH servers and retrieve the output.

### Configuration

The SSH Source Kamelet supports the following configurations:

-   **Connection Host** (`connectionHost`): SSH server hostname or IP address (required)
    
-   **Connection Port** (`connectionPort`): SSH server port (default: 22)
    
-   **Username** (`username`): Username for SSH authentication (required)
    
-   **Password** (`password`): Password for SSH authentication (required)
    
-   **Poll Command** (`pollCommand`): Command to execute on the remote server (required)
    
-   **Known Hosts Resource** (`knownHostsResource`): known\_hosts file to verify the key of the server; without it, any server is accepted
    
-   **Delay** (`delay`): Milliseconds between two runs of the command (default: 500)
    

### Output Format

The body is what the command printed on its standard output, as text. The exit code is in the `CamelSshExitValue` header and the standard error, as a stream, in `CamelSshStderr`. A command that fails still sends a message.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        connectionHost: "server.example.com"
        connectionPort: "22"
        username: "sshuser"
        password: "sshpass"
        pollCommand: "tail -n 10 /var/log/application.log"
        delay: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with System Monitoring

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        connectionHost: "server.example.com"
        username: "monitor"
        password: "monitorpass"
        pollCommand: "df -h | grep -E '(Filesystem|/dev/)'  && free -m"
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Longer Delay

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        connectionHost: "server.example.com"
        username: "operator"
        password: "operatorpass"
        pollCommand: "ps aux | grep java | grep -v grep"
        delay: 120000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security Considerations

-   Use strong passwords
    
-   Set `knownHostsResource` so that the key of the server is checked
    
-   Limit the commands that can be executed
    
-   Consider using dedicated monitoring users with restricted permissions
    
-   Monitor SSH access logs for security purposes
    
-   Use non-standard SSH ports when possible
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml)