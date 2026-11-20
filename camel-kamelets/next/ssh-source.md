# ![ssh source](_images/kamelets/ssh-source.svg) SSH Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs a command on a remote server over SSH again and again, at a regular interval, and sends what the command prints as a message each time.

Use it to watch a server without installing anything on it, for example check the free disk space, the state of a service or the last lines of a log file every minute. To run a command for each incoming message instead, use `ssh-sink`.

Output: the body is what the command printed on its standard output, as text, and the `Content-Type` header is set to `text/plain`. The `CamelSshExitValue` header holds the exit code of the command, and `CamelSshStderr` what it printed on its standard error, as a stream.

Good to know: it runs `pollCommand` with the rights of `username`, so log in with an account that may do only what is needed. It runs it every half second by default; set `delay` to how often you need it. A command that fails still sends a message, with its exit code in `CamelSshExitValue`. Log in with `password`, or with a private key in `privateKeyResource` when the server does not take passwords; when a key is set, the password is not used. The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted. A server that is not listed in that file is still accepted, unless `failOnUnknownHost` is true.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SSH server, without a port. | string |  | server.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SSH server, usually 22. | string | 22 |  |
| **pollCommand** | Poll Command | **Required** The command to run each time, as you would type it in a shell on the server. It can hold several commands separated by `;`. | string |  | df -h / |
| **username** | Username | **Required** The user to log in as. The command runs with the rights of this user. | string |  |  |
| **connectTimeout** | Connect Timeout | How long to wait for the connection, for the login and for the command to start, each in milliseconds. It does not limit how long the command runs. When it is not set, it is 30000, which is 30 seconds. | integer |  | 10000 |
| **delay** | Delay | How long to wait between two runs of the command, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **failOnUnknownHost** | Fail On Unknown Host | If true, a server that is not listed in `knownHostsResource` is refused. When it is not set or false, such a server is accepted, and only a server that is listed with another key is refused. Only used when `knownHostsResource` is set. | boolean |  |  |
| **knownHostsResource** | Known Hosts Resource | A known\_hosts file that holds the key of the server, starting with `file:`, `classpath:`, `http:` or `https:`. Its lines can be made with `ssh-keyscan`. A server whose key does not match is refused. When it is not set, the key of the server is not checked, so any server is accepted. | string |  | file:/etc/ssh/known\_hosts |
| **password** | Password | The password of `username` on the SSH server. Leave it empty to log in with a private key in `privateKeyResource` instead; when a key is set, the password is not used. With neither of them set, every run fails with `No password provided`. | string |  |  |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the key in `privateKeyResource`, when the key is protected by one. | string |  |  |
| **privateKeyResource** | Private Key Resource | A private key to log in with instead of a password, starting with `file:` followed by the path of the key file, `classpath:`, `http:` or `https:`. The matching public key must be in the `authorized_keys` file of `username` on the server. OpenSSH keys, such as those made with `ssh-keygen`, and PEM keys can be read. A key that cannot be read, or a wrong passphrase, makes every run fail with `No key-pair to add`. | string |  | file:/etc/ssh-keys/id\_ed25519 |

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

The Kamelet logs in as `username`, either with `password` or with a private key in `privateKeyResource`. Use the key when the server does not take passwords. When a key is set, the password is not used. It runs the command on the server and sends what it printed.

### Configuration

The SSH Source Kamelet supports the following configurations:

-   **Connection Host** (`connectionHost`): SSH server hostname or IP address (required)
    
-   **Connection Port** (`connectionPort`): SSH server port (default: 22)
    
-   **Username** (`username`): Username for SSH authentication (required)
    
-   **Password** (`password`): Password of `username`; leave it empty to log in with a private key
    
-   **Private Key Resource** (`privateKeyResource`): private key to log in with, such as `file:/etc/ssh-keys/id_ed25519`; OpenSSH and PEM keys can be read
    
-   **Private Key Passphrase** (`privateKeyPassphrase`): passphrase of the private key, when it has one
    
-   **Poll Command** (`pollCommand`): Command to execute on the remote server (required)
    
-   **Known Hosts Resource** (`knownHostsResource`): known\_hosts file to verify the key of the server; without it, any server is accepted
    
-   **Fail On Unknown Host** (`failOnUnknownHost`): if true, a server that is not listed in `knownHostsResource` is refused; otherwise it is accepted
    
-   **Connect Timeout** (`connectTimeout`): milliseconds to wait for the connection, the login and the start of the command (default: 30000); it does not limit how long the command runs
    
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

### Example with a Private Key

For a server that does not take passwords. The key of the server must be in the known\_hosts file, which can be made with `ssh-keyscan -p 22 server.example.com > known_hosts`.

```yaml
- route:
    from:
      uri: "kamelet:ssh-source"
      parameters:
        connectionHost: "server.example.com"
        connectionPort: "22"
        username: "monitor"
        privateKeyResource: "file:/etc/ssh-keys/id_ed25519"
        privateKeyPassphrase: "{{ssh.key.passphrase}}"
        knownHostsResource: "file:/etc/ssh-keys/known_hosts"
        failOnUnknownHost: true
        pollCommand: "df -h /"
        delay: 60000
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

-   Log in with a private key, or use strong passwords
    
-   Set `knownHostsResource`, and `failOnUnknownHost` to true, so that the key of the server is checked
    
-   Limit the commands that can be executed
    
-   Consider using dedicated monitoring users with restricted permissions
    
-   Monitor SSH access logs for security purposes
    
-   Use non-standard SSH ports when possible
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ssh-source.kamelet.yaml)