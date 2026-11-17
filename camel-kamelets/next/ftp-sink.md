# ![ftp sink](_images/kamelets/ftp-sink.svg) FTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file to a directory on an FTP server.

Use it to deliver exports, reports or data files to a partner or a legacy system that receives files over FTP. For an encrypted connection use `ftps-sink`, and for a server you reach with SSH use `sftp-sink`.

Input: the body is the content of the file, as text, bytes or a stream. The name of the file comes from the `file` header, or from `ce-file` when `file` is not set; any directory in it is dropped, so `reports/data.csv` is written as `data.csv`. Without these headers, `CamelFileName` is used as it is, subdirectories included, and without any of them a unique name is generated.

Output: the message is unchanged. The `CamelFileNameProduced` header is set to the path of the file on the server.

Good to know: a file with the same name is replaced, unless `fileExist` says otherwise. The connection and the login are not encrypted. A file name that points outside `directoryName` fails the message. Files are sent in ASCII (text) mode unless `binary` is true.

## Configuration Options

The following table summarizes the configuration options available for the `ftp-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the FTP server, without `ftp://` and without a port. | string |  | ftp.example.com |
| **connectionPort** | Connection Port | **Required** The port of the FTP server. FTP servers usually listen on port 21. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to write the files to. A path without a leading `/` is relative to the home directory of the user. It is created when it does not exist, unless `autoCreate` is false. | string |  | upload/orders |
| **password** | Password | **Required** The password of `username` on the FTP server. | string |  |  |
| **username** | Username | **Required** The user to log in to the FTP server as. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName`, and any subdirectory in the `CamelFileName` header, is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | If true, files are transferred in binary mode, byte for byte. When false, they are transferred in ASCII mode, which is meant for text. Set it to true for files that are not text, such as images, archives or PDF files. | boolean | false |  |
| **fileExist** | If File Exists | What to do when a file with the same name is already in the directory. `Override` replaces it, `Append` adds the new content at its end, `Fail` fails the message, and `Ignore` keeps the old file and drops the new content without an error. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **passiveMode** | Passive Mode | If true, the transfers use passive mode, in which the integration opens all the connections to the server. Set it to true when the integration or the server is behind a firewall or NAT, where the default active mode often fails. | boolean | false |  |

## Dependencies

At runtime, the `ftp-sink` Kamelet relies upon the presence of the following dependencies:

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