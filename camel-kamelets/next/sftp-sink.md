# ![sftp sink](_images/kamelets/sftp-sink.svg) SFTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an SFTP Server.

## Configuration Options

The following table summarizes the configuration options available for the `sftp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname of the FTP server. | string |  |  |
| **connectionPort** | Connection Port | **Required** The port of the FTP server. | string | 22 |  |
| **directoryName** | Directory Name | **Required** The starting directory. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | Automatically create the directory the files should be written to. | boolean | true |  |
| **binary** | Binary | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | boolean | false |  |
| **fileExist** | File Existence | How to behave in case of file already existent. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **passiveMode** | Passive Mode | Specifies to use passive mode connection. | boolean | false |  |
| **password** | Password | The password to access the FTP server. | string |  |  |
| **privateKeyFile** | Private Key File | Set the private key file so that the SFTP endpoint can do private key verification. | string |  |  |
| **privateKeyPassphrase** | Private Key Passphrase | Set the private key file passphrase so that the SFTP endpoint can do private key verification. | string |  |  |
| **privateKeyUri** | Private Key URI | Set the private key file (loaded from classpath by default) so that the SFTP endpoint can do private key verification. | string |  |  |
| **strictHostKeyChecking** | Strict Host Checking | Sets whether to use strict host key checking. | string | no |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | boolean | true |  |
| **username** | Username | The username to access the FTP server. | string |  |  |

## Dependencies

At runtime, the `sftp-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ftp
    
-   camel:core
    
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

### File Management Operations

Supports comprehensive file operations including:

-   File uploads and downloads
    
-   Directory creation and navigation
    
-   File and directory listing
    
-   Permission and attribute management
    

### Authentication Methods

Supports multiple authentication mechanisms:

-   Username and password authentication
    
-   Public key authentication
    
-   Interactive keyboard authentication
    
-   Host key verification
    

### Resume and Recovery

SFTP supports file transfer resume capabilities, allowing interrupted transfers to continue from where they left off, improving reliability for large file transfers.

### Cross-Platform Compatibility

Works seamlessly across different operating systems and platforms, providing consistent secure file transfer capabilities in heterogeneous environments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-sink.kamelet.yaml)