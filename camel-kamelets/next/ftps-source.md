# ![ftps source](_images/kamelets/ftps-source.svg) FTPS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory on an FTPS server (FTP with TLS encryption), one message per file, and by default leaves them on the server.

Use it to collect the files that a partner or a legacy system drops on an FTPS server, such as orders, invoices or exports. For a server without TLS use `ftp-source`, and for a server you reach with SSH use `sftp-source`.

Output: the body is the content of the file, as a stream. The `file` and `ce-file` headers hold the name of the file, with its path below `directoryName` when `recursive` is true, such as `2026/orders.csv`. `CamelFileName` holds the same name, and `CamelFileLength` the size of the file in bytes.

Good to know: files are not deleted or moved after they are read, unless `delete` is true or `move` is set. A file is read only once while the integration runs (`idempotent`), but the files left on the server are all read again after a restart; to read each file only once, also across restarts, set `move` to a directory such as `.done`, set `delete` to true, or keep the list of the files read in a file with `idempotentRepository`. It uses explicit TLS: it connects to the normal FTP port, usually 21, and then switches to TLS. A server that only accepts implicit TLS, usually on port 990, is not supported. Files are transferred in ASCII (text) mode unless `binary` is true.

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
| **delete** | Delete | If true, each file is deleted from the server once it has been read and handed on successfully. Use it to read each file only once, also across restarts. To keep the files, set `move` instead. | boolean | false |  |
| **idempotent** | Skip Files Already Read | If true, a file is read only once while the integration runs, even when it stays on the server. The list of the files read is kept in memory, so after a restart the files still on the server are read again, unless `move` or `delete` takes them away, or `idempotentRepository` keeps the list elsewhere. If false, and neither `delete` nor `move` is set, the same files are read again on every poll. | boolean | true |  |
| **idempotentRepository** | Files Read Store | The name of a bean that keeps the list of the files read, so that the files left on the server are not read again after a restart, such as a `FileIdempotentRepository` that keeps the list in a file. Declare the bean in the integration, for example under `beans` in YAML. Only used when `idempotent` is true. When it is not set, the list is kept in memory. | string |  | readFiles |
| **move** | Move After Read | Where to move each file on the server once it has been read and handed on successfully, so that it is not read again, also after a restart. A directory name, such as `.done`, is relative to the directory of the file. A path that ends with the name of the file, such as `done/$\\{date:now:yyyyMMdd}/$\\{file:name}`, is relative to `directoryName`, where `$\\{file:name}` is the name of the file and `$\\{date:now:yyyyMMdd}` today’s date. A directory whose name starts with a dot is never read, which matters when `recursive` is true. Missing directories are created, so `username` must be allowed to create directories and to rename files. When it is not set, files stay where they are. When `delete` is true too, the integration fails to start. | string |  | .done |
| **moveFailed** | Move Failed Files To | Where to move a file on the server when it could not be handed on, for example because the next step failed, so that it is not read over and over. The same format as `move`, such as `.error`. When it is not set, a file that fails stays where it is and is read again at every poll. It can be set together with `delete` or `move`. | string |  | .error |
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
    
-   Files are left on the server after they are read unless **Delete** is true or **Move** is set; with **Idempotent**, they are skipped while the integration runs but read again after a restart
    
-   **Passive Mode**: Use passive mode for FTPS connections (default: false)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false)
    
-   **Move**: Where to move each file on the server after it has been read, such as `.done`, so that it is not read again, also after a restart (not set by default). It cannot be combined with **Delete**
    
-   **Move Failed**: Where to move a file on the server when it could not be handed on, such as `.error` (not set by default). When not set, a file that fails is read again at every poll
    

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

### Example with Files Moved After Reading

```yaml
- route:
    from:
      uri: "kamelet:ftps-source"
      parameters:
        connectionHost: "ftps.example.com"
        username: "ftpsuser"
        password: "ftpspass"
        directoryName: "/incoming"
        move: ".done"
        moveFailed: ".error"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Each file is moved to the `.done` directory next to it once it has been read, and to `.error` when it could not be handed on, so a restart does not read the same files again while they are kept on the server. Directories whose names start with a dot are never read, also when **Recursive** is true. The user needs the right to create directories and rename files on the server.

### Example with Files Remembered Across Restarts

To keep the files on the server and still read each one only once, also across restarts, keep the list of the files read in a file. Declare a `FileIdempotentRepository` bean that writes the list to a file, and give its name in **idempotentRepository**:

```yaml
- beans:
    - name: readFiles
      type: "#class:org.apache.camel.support.processor.idempotent.FileIdempotentRepository"
      properties:
        fileStore: "#class:java.io.File('/var/data/read-files.dat')"
- route:
    from:
      uri: "kamelet:ftps-source"
      parameters:
        connectionHost: "ftps.example.com"
        username: "ftpsuser"
        password: "ftpspass"
        directoryName: "/incoming"
        idempotentRepository: "readFiles"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The file must be on storage that survives a restart of the integration, such as a persistent volume. A file that is put on the server again under the same name is not read again.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-source.kamelet.yaml)