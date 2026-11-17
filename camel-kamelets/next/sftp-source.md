# ![sftp source](_images/kamelets/sftp-source.svg) SFTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory on an SFTP server, over an encrypted SSH connection, one message per file, and by default leaves them on the server.

Use it to collect the files that a partner or another system drops on a server you reach with SSH, such as orders, invoices or exports. For an FTP server use `ftp-source` or `ftps-source`.

Output: the body is the content of the file, as bytes. The `file` and `ce-file` headers hold the name of the file, with its path below `directoryName` when `recursive` is true, such as `2026/orders.csv`. `CamelFileName` holds the same name, and `CamelFileLength` the size of the file in bytes.

Good to know: files are not deleted or moved after they are read, unless `delete` is true. A file is read only once while the integration runs (`idempotent`), but the files left on the server are all read again after a restart; set `delete` to true to read each file only once. Log in with `username` and either `password` or a private key. The key of the server must be in a known\_hosts file, `knownHostsUri` or else `~/.ssh/known_hosts` of the user that runs the integration, or the connection fails.

## Configuration Options

The following table summarizes the configuration options available for the `sftp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SFTP server, without `sftp://` and without a port. | string |  | sftp.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SFTP server, which is its SSH port, usually 22. | string | 22 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to read the files from. A path without a leading `/` is relative to the home directory of the user. | string |  | outgoing/orders |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName` is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | A setting of FTP that has no effect on SFTP, which always transfers files byte for byte. Leave it unset. | boolean | false |  |
| **delete** | Delete | If true, each file is deleted from the server once it has been read and handed on successfully. Use it to read each file only once, also across restarts. | boolean | false |  |
| **idempotent** | Skip Files Already Read | If true, a file is read only once while the integration runs, even when it stays on the server. The list of the files read is kept in memory, so after a restart the files still on the server are read again. If false, and `delete` is false, the same files are read again on every poll. | boolean | true |  |
| **ignoreFileNotFoundOrPermissionError** | Ignore Access Errors | If true, a directory or a file that does not exist, or that `username` may not read, is skipped. If false, it causes an error. | boolean | false |  |
| **knownHostsUri** | Known Hosts URI | The known\_hosts file that holds the key of the server, starting with `file://`, `classpath://`, `http://` or `https://`. Its lines can be made with `ssh-keyscan`. When it is not set, `~/.ssh/known_hosts` of the user that runs the integration is used, unless `useUserKnownHostsFile` is false; set it when that file does not exist, for example in a container. | string |  | file:///etc/sftp/known\_hosts |
| **passiveMode** | Passive Mode | A setting of FTP that has no effect on SFTP. Leave it unset. | boolean | false |  |
| **password** | Password | The password of `username`. Leave it empty to log in with a private key instead, set in `privateKeyFile` or `privateKeyUri`. | string |  |  |
| **privateKeyFile** | Private Key File | The path of a private key file on the machine that runs the integration, to log in with instead of a password. The matching public key must be in the `authorized_keys` of `username` on the server. | string |  | /etc/sftp/keys/id\_rsa |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the private key, when the key is protected with one. | string |  |  |
| **privateKeyUri** | Private Key URI | Where to load the private key from, instead of `privateKeyFile`. It starts with `file://` for a file, `classpath://` for a resource in the application, or `http://` or `https://`. | string |  | file:///etc/sftp/keys/id\_rsa |
| **recursive** | Recursive | If true, the files in the subdirectories of `directoryName` are read too. | boolean | false |  |
| **strictHostKeyChecking** | Strict Host Checking | Whether the key of the server must be found in a known\_hosts file. With `yes`, a server that is not in it is refused. With `no`, any server is accepted without checking its key, so someone in between could read the files and the password. `ask` is meant for interactive use. Enum values: \* yes \* no \* ask | string | yes |  |
| **useUserKnownHostsFile** | Use User Known Hosts File | If true and `knownHostsUri` is not set, the key of the server is looked up in `~/.ssh/known_hosts` of the user that runs the integration. | boolean | true |  |
| **username** | Username | The user to log in to the SFTP server as. | string |  |  |

## Dependencies

At runtime, the `sftp-source` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet supports SFTP authentication with a username and either a password or a private key (`privateKeyFile` or `privateKeyUri`). The key of the server must be in a known\_hosts file (`knownHostsUri`, or `~/.ssh/known_hosts` of the user that runs the integration). SFTP provides secure file transfer over SSH, ensuring encrypted communication.

### Configuration

The SFTP Source Kamelet supports the following configurations:

-   **Connection Host**: The hostname or IP address of the SFTP server (required)
    
-   **Connection Port**: The port number of the SFTP server (default: 22)
    
-   **Username**: Username for SFTP authentication
    
-   **Password**: Password for SFTP authentication, or use a private key
    
-   **Directory Name**: The starting directory path on the SFTP server (required)
    
-   **Recursive**: Process files in subdirectories (default: false)
    
-   **Idempotent**: Skip already-processed files (default: true)
    
-   **Binary**: Use binary transfer mode instead of ASCII (default: false)
    
-   **Auto Create**: Automatically create the starting directory if it doesn’t exist (default: true)
    
-   **Delete**: Delete files after successful processing (default: false). When false, files are left on the server; with **Idempotent**, they are skipped while the integration runs but read again after a restart
    

### Output Format

The Kamelet outputs the file content as bytes and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

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