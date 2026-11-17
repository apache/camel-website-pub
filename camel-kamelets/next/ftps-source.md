# ![ftps source](_images/kamelets/ftps-source.svg) FTPS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory on an FTPS server (FTP with TLS encryption), one message per file, and by default leaves them on the server.

Use it to collect the files that a partner or a legacy system drops on an FTPS server, such as orders, invoices or exports. For a server without TLS use `ftp-source`, and for a server you reach with SSH use `sftp-source`.

Output: the body is the content of the file, as a stream. The `file` and `ce-file` headers hold the name of the file, with its path below `directoryName` when `recursive` is true, such as `2026/orders.csv`. `CamelFileName` holds the same name, and `CamelFileLength` the size of the file in bytes.

Good to know: files are not deleted or moved after they are read, unless `delete` is true. A file is read only once while the integration runs (`idempotent`), but the files left on the server are all read again after a restart; set `delete` to true to read each file only once. It uses explicit TLS: it connects to the normal FTP port, usually 21, and then switches to TLS. A server that only accepts implicit TLS, usually on port 990, is not supported. Files are transferred in ASCII (text) mode unless `binary` is true.

## Configuration Options

The following table summarizes the configuration options available for the `ftps-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the FTPS server, without `ftps://` and without a port. | string |  | ftps.example.com |
| **connectionPort** | Connection Port | **Required** The port of the FTPS server, usually 21. The Kamelet connects with explicit TLS, so use the normal FTP port, not the implicit TLS port 990. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to read the files from. A path without a leading `/` is relative to the home directory of the user. | string |  | outgoing/orders |
| **password** | Password | **Required** The password of `username` on the FTPS server. | string |  |  |
| **username** | Username | **Required** The user to log in to the FTPS server as. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName` is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | If true, files are transferred in binary mode, byte for byte. When false, they are transferred in ASCII mode, which is meant for text. Set it to true for files that are not text, such as images, archives or PDF files. | boolean | false |  |
| **delete** | Delete | If true, each file is deleted from the server once it has been read and handed on successfully. Use it to read each file only once, also across restarts. | boolean | false |  |
| **idempotent** | Skip Files Already Read | If true, a file is read only once while the integration runs, even when it stays on the server. The list of the files read is kept in memory, so after a restart the files still on the server are read again. If false, and `delete` is false, the same files are read again on every poll. | boolean | true |  |
| **passiveMode** | Passive Mode | If true, the transfers use passive mode, in which the integration opens all the connections to the server. Set it to true when the integration or the server is behind a firewall or NAT, where the default active mode often fails. | boolean | false |  |
| **recursive** | Recursive | If true, the files in the subdirectories of `directoryName` are read too. | boolean | false |  |

## Dependencies

At runtime, the `ftps-source` Kamelet relies upon the presence of the following dependencies:

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
    
-   Files are left on the server after they are read unless **Delete** is true; with **Idempotent**, they are skipped while the integration runs but read again after a restart
    
-   **Passive Mode**: Use passive mode for FTPS connections (default: false)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false)
    

### Output Format

The Kamelet outputs file content as an `InputStream` and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

### Security

FTPS encrypts the connection of standard FTP with TLS. The Kamelet uses explicit FTPS (it switches to TLS on the normal FTP port).

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
        connectionPort: "21"
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

This example enables passive mode, binary transfer, and recursive directory processing. The Kamelet uses explicit FTPS: it connects to the normal FTP port and then switches to TLS. Servers that only accept implicit FTPS (usually on port 990) are not supported.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml)