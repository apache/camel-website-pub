# ![sftp source](_images/kamelets/sftp-source.svg) SFTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an SFTP server.

## Configuration Options

The following table summarizes the configuration options available for the `sftp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname of the SFTP server. | string |  |  |
| **connectionPort** | Connection Port | **Required** The port of the FTP server. | string | 22 |  |
| **directoryName** | Directory Name | **Required** The starting directory. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | Automatically create starting directory. | boolean | true |  |
| **binary** | Binary | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | boolean | false |  |
| **delete** | Delete | If true, the file is deleted after it is processed successfully. | boolean | false |  |
| **idempotent** | Idempotency | Skip already-processed files. | boolean | true |  |
| **ignoreFileNotFoundOrPermissionError** | Ignore File Not Found Or Permission Error | Whether to ignore when (trying to list files in directories or when downloading a file), which does not exist or due to permission error. By default when a directory or file does not exists or insufficient permission, then an exception is thrown. Setting this option to true allows to ignore that instead. | boolean | false |  |
| **passiveMode** | Passive Mode | Sets the passive mode connection. | boolean | false |  |
| **password** | Password | The password to access the SFTP server. | string |  |  |
| **privateKeyFile** | Private Key File | Set the private key file so that the SFTP endpoint can do private key verification. | string |  |  |
| **privateKeyPassphrase** | Private Key Passphrase | Set the private key file passphrase so that the SFTP endpoint can do private key verification. | string |  |  |
| **privateKeyUri** | Private Key URI | Set the private key file (loaded from classpath by default) so that the SFTP endpoint can do private key verification. | string |  |  |
| **recursive** | Recursive | If a directory, look for files in all sub-directories as well. | boolean | false |  |
| **strictHostKeyChecking** | Strict Host Checking | Sets whether to use strict host key checking. | string | no |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | boolean | true |  |
| **username** | Username | The username to access the SFTP server. | string |  |  |

## Dependencies

At runtime, the `sftp-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:sftp-source"
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

## SFTP Source Kamelet Description

### Authentication

This Kamelet supports SFTP authentication using username and password credentials. SFTP provides secure file transfer over SSH, ensuring encrypted communication.

### Configuration

The SFTP Source Kamelet supports the following configurations:

-   **Connection Host**: The hostname or IP address of the SFTP server (required)
    
-   **Connection Port**: The port number of the SFTP server (default: 22)
    
-   **Username**: Username for SFTP authentication (required)
    
-   **Password**: Password for SFTP authentication (required)
    
-   **Directory Name**: The starting directory path on the SFTP server (required)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false)
    

### Output Format

The Kamelet outputs file content as an `InputStream` and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

### Security

SFTP provides enhanced security over standard FTP by using SSH for authentication and encryption, ensuring that credentials and data are transmitted securely.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        connectionPort: "22"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/incoming"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Recursive Processing

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/data"
        recursive: true
        binary: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with File Deletion

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/processed"
        delete: true
        idempotent: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example deletes files after processing and disables idempotency to allow re-processing of files with the same name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-source.kamelet.yaml)