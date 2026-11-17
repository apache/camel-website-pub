# ![sftp sink](_images/kamelets/sftp-sink.svg) SFTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file to a directory on an SFTP server, which transfers files over an encrypted SSH connection.

Use it to deliver exports, reports or data files to a server you reach with SSH, such as the SFTP drop box of a partner. For an FTP server use `ftp-sink` or `ftps-sink`.

Input: the body is the content of the file, as text, bytes or a stream. The name of the file comes from the `file` header, or from `ce-file` when `file` is not set; any directory in it is dropped, so `reports/data.csv` is written as `data.csv`. Without these headers, `CamelFileName` is used as it is, subdirectories included, and without any of them a unique name is generated.

Output: the message is unchanged. The `CamelFileNameProduced` header is set to the path of the file on the server.

Good to know: a file with the same name is replaced, unless `fileExist` says otherwise. Log in with `username` and either `password` or a private key. The key of the server must be in a known\_hosts file, `knownHostsUri` or else `~/.ssh/known_hosts` of the user that runs the integration, or the connection fails. A file name that points outside `directoryName` fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `sftp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SFTP server, without `sftp://` and without a port. | string |  | sftp.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SFTP server, which is its SSH port, usually 22. | string | 22 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to write the files to. A path without a leading `/` is relative to the home directory of the user. It is created when it does not exist, unless `autoCreate` is false. | string |  | upload/orders |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName`, and any subdirectory in the `CamelFileName` header, is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | A setting of FTP that has no effect on SFTP, which always transfers files byte for byte. Leave it unset. | boolean | false |  |
| **fileExist** | If File Exists | What to do when a file with the same name is already in the directory. `Override` replaces it, `Append` adds the new content at its end, `Fail` fails the message, and `Ignore` keeps the old file and drops the new content without an error. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **knownHostsUri** | Known Hosts URI | The known\_hosts file that holds the key of the server, starting with `file://`, `classpath://`, `http://` or `https://`. Its lines can be made with `ssh-keyscan`. When it is not set, `~/.ssh/known_hosts` of the user that runs the integration is used, unless `useUserKnownHostsFile` is false; set it when that file does not exist, for example in a container. | string |  | file:///etc/sftp/known\_hosts |
| **passiveMode** | Passive Mode | A setting of FTP that has no effect on SFTP. Leave it unset. | boolean | false |  |
| **password** | Password | The password of `username`. Leave it empty to log in with a private key instead, set in `privateKeyFile` or `privateKeyUri`. | string |  |  |
| **privateKeyFile** | Private Key File | The path of a private key file on the machine that runs the integration, to log in with instead of a password. The matching public key must be in the `authorized_keys` of `username` on the server. | string |  | /etc/sftp/keys/id\_rsa |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the private key, when the key is protected with one. | string |  |  |
| **privateKeyUri** | Private Key URI | Where to load the private key from, instead of `privateKeyFile`. It starts with `file://` for a file, `classpath://` for a resource in the application, or `http://` or `https://`. | string |  | file:///etc/sftp/keys/id\_rsa |
| **strictHostKeyChecking** | Strict Host Checking | Whether the key of the server must be found in a known\_hosts file. With `yes`, a server that is not in it is refused. With `no`, any server is accepted without checking its key, so someone in between could read the files and the password. `ask` is meant for interactive use. Enum values: \* yes \* no \* ask | string | yes |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If true and `knownHostsUri` is not set, the key of the server is looked up in `~/.ssh/known_hosts` of the user that runs the integration. | boolean | true |  |
| **username** | Username | The user to log in to the SFTP server as. | string |  |  |

## Dependencies

At runtime, the `sftp-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ftp
    
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
            uri: "kamelet:sftp-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SFTP Sink Kamelet Description

### Secure File Transfer Protocol

This Kamelet provides secure file transfer capabilities using SFTP (SSH File Transfer Protocol). SFTP enables encrypted file transfers over SSH connections with comprehensive file management features.

### SSH-Based Security

Built on top of SSH protocol, SFTP provides strong authentication and encryption for all file transfer operations, ensuring data confidentiality and integrity.

### File Operations

The sink uploads each message as a file into `directoryName`, and creates missing directories when `autoCreate` is true. What happens when the file already exists is set by `fileExist` (`Override`, `Append`, `Fail` or `Ignore`). To read files from an SFTP server, use the SFTP Source Kamelet.

### Authentication Methods

Supports these authentication mechanisms:

-   Username and password authentication
    
-   Private key authentication (`privateKeyFile` or `privateKeyUri`, with `privateKeyPassphrase` for a protected key)
    
-   Host key verification against a known\_hosts file (`knownHostsUri`, or `~/.ssh/known_hosts` of the user that runs the integration); with the default `strictHostKeyChecking` of `yes`, a server that is not in it is refused
    

### Cross-Platform Compatibility

Works seamlessly across different operating systems and platforms, providing consistent secure file transfer capabilities in heterogeneous environments.

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses a default naming convention.

The value is reduced to a single file name before use: any directory component is dropped, so `reports/2026/data.csv` is stored as `data.csv`. The file is always written inside the configured directory.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-sink.kamelet.yaml)