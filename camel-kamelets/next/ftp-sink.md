# ![ftp sink](_images/kamelets/ftp-sink.svg) FTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to an FTP server.

## Configuration Options

The following table summarizes the configuration options available for the `ftp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The hostname of the FTP server. | string |  |  |
| **connectionPort** | Connection Port | **Required** The port of the FTP server. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The starting directory. | string |  |  |
| **password** | Password | **Required** The password to access the FTP server. | string |  |  |
| **username** | Username | **Required** The username to access the FTP server. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | Automatically create the directory the files should be written to. | boolean | true |  |
| **binary** | Binary | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | boolean | false |  |
| **fileExist** | File Existence | How to behave in case of file already existent. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **passiveMode** | Passive Mode | Specifies to use passive mode connection. | boolean | false |  |

## Dependencies

At runtime, the `ftp-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:ftp-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## FTP Sink Kamelet Description

### Authentication

This Kamelet uses username and password authentication to connect to FTP servers.

### Connection Configuration

Requires: - Connection host (FTP server hostname) - Connection port (defaults to 21) - Username and password credentials - Directory name for file operations

### File Transfer Options

-   **Transfer Mode**: ASCII (default) or Binary mode
    
-   **Passive Mode**: Can be enabled for firewall compatibility
    
-   **File Existence Handling**: Override (default), Append, Fail, or Ignore
    
-   **Auto-create Directories**: Automatically creates missing directories (enabled by default)
    

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses a default naming convention.

The value is reduced to a single file name before use: any directory component is dropped, so `reports/2026/data.csv` is stored as `data.csv`. The file is always written inside the configured directory.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftp-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftp-sink.kamelet.yaml)