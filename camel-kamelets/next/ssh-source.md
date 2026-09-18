# ![ssh source](_images/kamelets/ssh-source.svg) SSH Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from SSH session.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The SSH Host. | string |  |  |
| **connectionPort** | Connection Port | **Required** The SSH Port. | string | 22 |  |
| **password** | Password | **Required** The SSH password to use. | string |  |  |
| **pollCommand** | Poll Command | **Required** The command to run while polling the SSH session. | string |  | date |
| **username** | Username | **Required** The SSH username to use. | string |  |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **knownHostsResource** | Known Hosts Resource | The resource path of a known\_hosts file used to verify the SSH server host key. When not set, the client does not verify the server host key against a known\_hosts file. | string |  |  |

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

-   **Host**: SSH server hostname or IP address (required)
    
-   **Port**: SSH server port (default: 22)
    
-   **Username**: Username for SSH authentication (required)
    
-   **Password**: Password for SSH authentication (required)
    
-   **Poll Command**: Command to execute on the remote server (required)
    
-   **Cert Resource**: SSH certificate resource for key-based authentication
    
-   **Timeout**: Command execution timeout in milliseconds
    
-   **Poll Interval**: Interval between command executions
    

### Output Format

The Kamelet outputs the result of SSH command execution as text, including both stdout and stderr streams from the remote command.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        host: "server.example.com"
        port: "22"
        username: "sshuser"
        password: "sshpass"
        pollCommand: "tail -n 10 /var/log/application.log"
        pollInterval: 30000
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
        host: "server.example.com"
        username: "monitor"
        password: "monitorpass"
        pollCommand: "df -h | grep -E '(Filesystem|/dev/)'  && free -m"
        pollInterval: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Custom Timeout

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        host: "server.example.com"
        username: "operator"
        password: "operatorpass"
        pollCommand: "ps aux | grep java | grep -v grep"
        timeout: 10000
        pollInterval: 120000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security Considerations

-   Use strong passwords or preferably SSH key authentication
    
-   Limit the commands that can be executed
    
-   Consider using dedicated monitoring users with restricted permissions
    
-   Monitor SSH access logs for security purposes
    
-   Use non-standard SSH ports when possible
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml)