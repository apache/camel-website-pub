# ![ftp source](_images/kamelets/ftp-source.svg) FTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an FTP server.

## Configuration Options

The following table summarizes the configuration options available for the `ftp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname of the FTP server. | string |  |  |
| **connectionPort** | Connection Port | **Required** The port of the FTP server. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The starting directory. | string |  |  |
| **password** | Password | **Required** The password to access the FTP server. | string |  |  |
| **username** | Username | **Required** The username to access the FTP server. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | Automatically create starting directory. | boolean | true |  |
| **binary** | Binary | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | boolean | false |  |
| **delete** | Delete | If true, the file is deleted after it is processed successfully. | boolean | false |  |
| **idempotent** | Idempotency | Skip already-processed files. | boolean | true |  |
| **passiveMode** | Passive Mode | Specifes to use passive mode connection. | boolean | false |  |
| **recursive** | Recursive | If a directory, look for files in all the sub-directories as well. | boolean | false |  |

## Dependencies

At runtime, the `ftp-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:ftp-source"
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

## FTP Source Kamelet Description

### Authentication

This Kamelet requires username and password authentication to access the FTP server. The credentials are configured through the `username` and `password` properties.

### Configuration

The FTP Source Kamelet supports the following configurations:

-   **Connection Host**: The hostname or IP address of the FTP server (required)
    
-   **Connection Port**: The port number of the FTP server (default: 21)
    
-   **Username**: Username for FTP authentication (required)
    
-   **Password**: Password for FTP authentication (required)
    
-   **Directory Name**: The starting directory path on the FTP server (required)
    
-   **Passive Mode**: Use passive mode for FTP connections (default: false)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false)
    

### Output Format

The Kamelet outputs file content as an `InputStream` and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:ftp-source"
      parameters:
        connectionHost: "ftp.example.com"
        connectionPort: "21"
        username: "ftpuser"
        password: "ftppass"
        directoryName: "/incoming"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Passive Mode and Recursive Processing

```yaml
- route:
    from:
      uri: "kamelet:ftp-source"
      parameters:
        connectionHost: "ftp.example.com"
        connectionPort: "21"
        username: "ftpuser"
        password: "ftppass"
        directoryName: "/data"
        passiveMode: true
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
      uri: "kamelet:ftp-source"
      parameters:
        connectionHost: "ftp.example.com"
        connectionPort: "21"
        username: "ftpuser"
        password: "ftppass"
        directoryName: "/processed"
        delete: true
        idempotent: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example deletes files after processing and disables idempotency to allow re-processing of files with the same name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftp-source.kamelet.yaml)