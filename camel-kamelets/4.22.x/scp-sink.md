# ![scp sink](_images/kamelets/scp-sink.svg) SCP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send file to an FTP Server through Secure Copy Protocol

## Configuration Options

The following table summarizes the configuration options available for the `scp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **serverName** | Hostname | **Required** The hostname of the FTP server. | string |  |  |
| **serverPort** | Port | **Required** The port of the FTP server. | string |  |  |
| **password** | Password | Password for accessing FTP Server. | string |  |  |
| **privateKeyFile** | Private Key File | Set the private key file so that the SCP endpoint can do private key verification. | string |  |  |
| **privateKeyPassphrase** | Private Key Passphrase | Set the private key file passphrase so that the SCP endpoint can do private key verification. | string |  |  |
| **strictHostKeyChecking** | Strict Host Checking | Sets whether to use strict host key checking. | string | no |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | boolean | true |  |
| **username** | Username | Username for accessing FTP Server. | string |  |  |

## Dependencies

At runtime, the `scp-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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

Transfers files to remote servers and places them in specified directories with configurable file names and permissions.

### Network Efficiency

SCP provides efficient file transfer capabilities suitable for:

-   Automated file deployments
    
-   Backup operations
    
-   Data distribution across systems
    
-   Secure file archiving
    

### Authentication Methods

Supports multiple authentication methods:

-   Username and password authentication
    
-   Public key authentication
    
-   Host key verification for security
    

### Cross-Platform Support

Works across different operating systems and platforms, providing consistent secure file transfer capabilities regardless of the target system architecture.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/scp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/scp-sink.kamelet.yaml)