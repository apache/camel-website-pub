# ![ftps source](_images/kamelets/ftps-source.svg) FTPS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an FTPS server.

## Configuration Options

The following table summarizes the configuration options available for the `ftps-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname of the FTPS server. | string |  |  |
| **connectionPort** | Connection Port | **Required** The port of the FTPS server. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The starting directory. | string |  |  |
| **password** | Password | **Required** The password to access the FTPS server. | string |  |  |
| **username** | Username | **Required** The username to access the FTPS server. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | Automatically create starting directory. | boolean | true |  |
| **binary** | Binary | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | boolean | false |  |
| **delete** | Delete | If true, the file is deleted after it is processed successfully. | boolean | false |  |
| **idempotent** | Idempotency | Skip already-processed files. | boolean | true |  |
| **passiveMode** | Passive Mode | Specifies to use passive mode connection. | boolean | false |  |
| **recursive** | Recursive | If a directory, look for files in all sub-directories as well. | boolean | false |  |

## Dependencies

At runtime, the `ftps-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:ftps-source"
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

## FTPS Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to access the FTPS server. FTPS provides FTP with SSL/TLS encryption for secure file transfer. The credentials are configured through the `username` and `password` properties.

### Configuration

The FTPS Source Kamelet supports the following configurations:

-   **Connection Host**: The hostname or IP address of the FTPS server (required)
    
-   **Connection Port**: The port number of the FTPS server (default: 21)
    
-   **Username**: Username for FTPS authentication (required)
    
-   **Password**: Password for FTPS authentication (required)
    
-   **Directory Name**: The starting directory path on the FTPS server (required)
    
-   **Passive Mode**: Use passive mode for FTPS connections (default: false)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false)
    

### Output Format

The Kamelet outputs file content as an `InputStream` and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

### Security

FTPS provides enhanced security over standard FTP by encrypting the connection using SSL/TLS. This ensures that credentials and data are transmitted securely.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:ftps-source"
      parameters:
        connectionHost: "ftps.example.com"
        connectionPort: "21"
        username: "ftpsuser"
        password: "ftpspass"
        directoryName: "/secure-incoming"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Passive Mode and Binary Transfer

```yaml
- route:
    from:
      uri: "kamelet:ftps-source"
      parameters:
        connectionHost: "ftps.example.com"
        connectionPort: "990"
        username: "ftpsuser"
        password: "ftpspass"
        directoryName: "/data"
        passiveMode: true
        binary: true
        recursive: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example uses port 990 (common for implicit FTPS), enables passive mode, binary transfer, and recursive directory processing.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml)