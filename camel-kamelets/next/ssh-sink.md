# ![ssh sink](_images/kamelets/ssh-sink.svg) SSH Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the text of each message as a command on a remote server over SSH, and returns what the command prints.

Use it to run a script or a maintenance command on a server when something happens, for example restart a service after a deployment or clear a cache when data changes. To run a fixed command on a schedule and read its output, use `ssh-source`; to run a command on the machine of the integration, use `exec-sink`.

Input: the body is the command to run, as text, such as `systemctl restart myapp`. It runs in the shell of `username`, so it can hold several commands separated by `;`.

Output: the body afterwards is what the command printed on its standard output, as a stream. The `CamelSshExitValue` header holds the exit code of the command, and `CamelSshStderr` what it printed on its standard error, as a stream.

Good to know: it runs whatever command it receives, with the rights of `username`. Never send it messages from an untrusted source, and log in with an account that may do only what is needed. A command that ends with an exit code other than 0 does not fail the message: check `CamelSshExitValue`. Log in with `password`, or with a private key in `privateKeyResource` when the server does not take passwords; when a key is set, the password is not used. The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted. A server that is not listed in that file is still accepted, unless `failOnUnknownHost` is true.

## Configuration Options

The following table summarizes the configuration options available for the `ssh-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SSH server, without a port. | string |  | server.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SSH server, usually 22. | string | 22 |  |
| **username** | Username | **Required** The user to log in as. The commands run with the rights of this user. | string |  |  |
| **connectTimeout** | Connect Timeout | How long to wait for the connection, for the login and for the command to start, each in milliseconds. It does not limit how long the command runs. When it is not set, it is 30000, which is 30 seconds. | integer |  | 10000 |
| **failOnUnknownHost** | Fail On Unknown Host | If true, a server that is not listed in `knownHostsResource` is refused. When it is not set or false, such a server is accepted, and only a server that is listed with another key is refused. Only used when `knownHostsResource` is set. | boolean |  |  |
| **knownHostsResource** | Known Hosts Resource | A known\_hosts file that holds the key of the server, starting with `file:`, `classpath:`, `http:` or `https:`. Its lines can be made with `ssh-keyscan`. A server whose key does not match is refused. When it is not set, the key of the server is not checked, so any server is accepted. | string |  | file:/etc/ssh/known\_hosts |
| **password** | Password | The password of `username` on the SSH server. Leave it empty to log in with a private key in `privateKeyResource` instead; when a key is set, the password is not used. With neither of them set, every command fails with `No password provided`. | string |  |  |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the key in `privateKeyResource`, when the key is protected by one. | string |  |  |
| **privateKeyResource** | Private Key Resource | A private key to log in with instead of a password, starting with `file:` followed by the path of the key file, `classpath:`, `http:` or `https:`. The matching public key must be in the `authorized_keys` file of `username` on the server. OpenSSH keys, such as those made with `ssh-keygen`, and PEM keys can be read. A key that cannot be read, or a wrong passphrase, makes every command fail with `No key-pair to add`. | string |  | file:/etc/ssh-keys/id\_ed25519 |

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

The Kamelet logs in as `username`, either with `password` or with a private key in `privateKeyResource`. Use the key when the server does not take passwords. When a key is set, the password is not used.

-   `privateKeyResource` is where to read the key from: `file:` followed by the path of the key file, `classpath:`, `http:` or `https:`. OpenSSH keys, such as those made with `ssh-keygen`, and PEM keys can be read. The matching public key must be in the `authorized_keys` file of `username` on the server.
    
-   `privateKeyPassphrase` is the passphrase of the key, when it has one.
    

The key of the server is checked only when `knownHostsResource` is set; without it, any server is accepted. A server that is not listed in that file is still accepted, unless `failOnUnknownHost` is true. A server that is listed with another key is always refused. The lines of the file can be made with `ssh-keyscan`, such as `ssh-keyscan -p 22 server.example.com > known_hosts`.

`connectTimeout` is how long to wait for the connection, for the login and for the command to start, in milliseconds (30000 when it is not set). It does not limit how long the command runs.

### Example with a Private Key

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      parameters:
        subpath: "restart"
      steps:
        - setBody:
            constant: "systemctl restart myapp"
        - to:
            uri: "kamelet:ssh-sink"
            parameters:
              connectionHost: "server.example.com"
              connectionPort: "22"
              username: "deploy"
              privateKeyResource: "file:/etc/ssh-keys/id_ed25519"
              privateKeyPassphrase: "{{ssh.key.passphrase}}"
              knownHostsResource: "file:/etc/ssh-keys/known_hosts"
              failOnUnknownHost: true
```

The command is fixed in the route, not taken from the request, so that callers of the webhook cannot choose what runs on the server.

### Security Features

SSH provides comprehensive security features:

-   Strong encryption for all communications
    
-   Host key verification, when `knownHostsResource` is set
    
-   Login with a private key, when `privateKeyResource` is set
    
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