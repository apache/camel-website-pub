# ![scp sink](_images/kamelets/scp-sink.svg) SCP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Copies each message as a file to a directory on a remote server, with SCP (secure copy) over an SSH connection.

Use it to copy files to a server you reach with SSH that does not offer SFTP, for example to drop a configuration or a report on a host. To append to or keep existing files, or to create the directory when it is missing, use `sftp-sink` instead.

Input: the body is the content of the file, as text, bytes or a stream. The name of the file comes from the `CamelFileName` header, which may hold subdirectories, such as `reports/data.csv`; without it, a unique name is generated.

Output: the message is unchanged. The `CamelFileNameProduced` header is set to the path of the file on the server.

Good to know: files are written in `directoryName`, or else in the home directory of `username`, with the rights of that user, and a file with the same name is replaced. `directoryName` must exist: when it does not, every file is written as a file with the name of the directory. A file name that points outside the directory fails the message. The key of the server is checked against the file in `knownHostsUri`, or else `~/.ssh/known_hosts` of the user that runs the integration, unless `strictHostKeyChecking` is `no`. Do not place it after messages from an untrusted source. Headers that start with `CamelFile` or `CamelOverruleFile`, except `CamelFileName`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `scp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **serverName** | Hostname | **Required** The host name or IP address of the server to copy the files to. | string |  | files.example.com |
| **serverPort** | Port | **Required** The SSH port of the server, usually 22. | string |  | 22 |
| **chmod** | File Permissions | The permissions to give each new file, as three octal digits, such as `640` for read and write by the owner and read by the group. The umask of the server can take some away, so with the usual umask 022 the `664` used when it is not set gives `644`. A file that already exists keeps its permissions, and only its content is replaced. | string |  | 640 |
| **directoryName** | Directory Name | The directory on the server to write the files to, such as `incoming/reports` or `/data/incoming`. A path without a leading `/` is relative to the home directory of `username`. It must exist, as it is not created; when it is missing, each file is written as a file with the name of the directory instead. When it is not set, the files are written in the home directory. | string |  | incoming/reports |
| **knownHostsUri** | Known Hosts URI | A known\_hosts file that holds the key of the server, such as one made with `ssh-keyscan`. A path is read as a file; `classpath:` followed by a name reads a resource of the application. Use it when the user that runs the integration has no `~/.ssh/known_hosts` with the server in it. | string |  |  |
| **password** | Password | The password of `username`. Leave it empty to log in with a private key, set in `privateKeyFile`. | string |  |  |
| **privateKeyFile** | Private Key File | The path of a private key file on the machine that runs the integration, to log in with instead of a password. The matching public key must be in the `authorized_keys` of `username` on the server. | string |  | /etc/scp/keys/id\_rsa |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the private key in `privateKeyFile`, when the key is protected by one. | string |  |  |
| **strictHostKeyChecking** | Strict Host Checking | Whether the key of the server must be found in `~/.ssh/known_hosts` of the user that runs the integration. With `yes`, a server that is not in it is refused. With `no`, any server is accepted without checking its key, so someone in between could read the files and the password. `ask` is meant for interactive use. Enum values: \* yes \* no \* ask | string | yes |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If true, the key of the server is looked up in `~/.ssh/known_hosts` of the user that runs the integration. | boolean | true |  |
| **username** | Username | The user to log in as. The files are written in the home directory of this user. | string |  |  |

## Dependencies

At runtime, the `scp-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jsch
    
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
            uri: "kamelet:scp-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SCP Sink Kamelet Description

### Secure File Transfer

This Kamelet provides secure file transfer capabilities using SCP (Secure Copy Protocol). SCP enables encrypted file transfers over SSH connections, ensuring data security during transmission.

### SSH-Based Security

Uses SSH protocol for authentication and encryption, providing strong security for file transfers across networks. Supports both password and key-based authentication methods.

### Remote File Placement

Transfers files to `directoryName` on the remote server, or to the home directory of `username` when it is not set. A path without a leading `/` is relative to the home directory. The directory must exist: when it does not, each file is written as a file with the name of the directory. The file name comes from the `CamelFileName` header, which may include subdirectories, which are created; without it, a unique name is generated. A file with the same name is replaced. To create a missing directory, or to keep or append to existing files, use the SFTP Sink Kamelet.

### Network Efficiency

SCP provides efficient file transfer capabilities suitable for:

-   Automated file deployments
    
-   Backup operations
    
-   Data distribution across systems
    
-   Secure file archiving
    

### Authentication Methods

Supports multiple authentication methods:

-   Username and password authentication
    
-   Private key authentication (`privateKeyFile`), with `privateKeyPassphrase` for a key protected by one
    
-   Host key verification against the file in `knownHostsUri`, or else `~/.ssh/known_hosts` of the user that runs the integration
    

### Cross-Platform Support

Works across different operating systems and platforms, providing consistent secure file transfer capabilities regardless of the target system architecture.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Hello"
      steps:
        - setHeader:
            name: CamelFileName
            constant: "hello.txt"
        - to:
            uri: "kamelet:scp-sink"
            parameters:
              serverName: "files.example.com"
              serverPort: "22"
              username: "scpuser"
              password: "scppass"
              knownHostsUri: "/etc/scp/known_hosts"
              directoryName: "incoming/reports"
              chmod: "640"
```

This copies `hello.txt` to `incoming/reports` in the home directory of `scpuser`, with the permissions `640`. The umask of the server can take permissions away: with the usual umask 022, the default `664` gives `644`. A file that already exists keeps its permissions, and only its content is replaced.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/scp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/scp-sink.kamelet.yaml)