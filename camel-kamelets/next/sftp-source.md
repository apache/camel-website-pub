# ![sftp source](_images/kamelets/sftp-source.svg) SFTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory on an SFTP server, over an encrypted SSH connection, one message per file, and by default leaves them on the server.

Use it to collect the files that a partner or another system drops on a server you reach with SSH, such as orders, invoices or exports. For an FTP server use `ftp-source` or `ftps-source`.

Output: the body is the content of the file, as bytes, or as a stream when `streamDownload` is true. The `file` and `ce-file` headers hold the name of the file, with its path below `directoryName` when `recursive` is true, such as `2026/orders.csv`. `CamelFileName` holds the same name, and `CamelFileLength` the size of the file in bytes.

Good to know: files are not deleted or moved after they are read, unless `delete` is true or `move` is set. A file is read only once while the integration runs (`idempotent`), but the files left on the server are all read again after a restart; to read each file only once, also across restarts, set `move` to a directory such as `.done`, set `delete` to true, or keep the list of the files read in a file with `idempotentRepository`. To read only some of the files, set `include`, `exclude` or `antInclude`. To leave a file alone while another program is still writing it, set `readLock`. Log in with `username` and either `password` or a private key. The key of the server must be in a known\_hosts file, `knownHostsUri` or else `~/.ssh/known_hosts` of the user that runs the integration, or the connection fails.

## Configuration Options

The following table summarizes the configuration options available for the `sftp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SFTP server, without `sftp://` and without a port. | string |  | sftp.example.com |
| **connectionPort** | Connection Port | **Required** The port of the SFTP server, which is its SSH port, usually 22. | string | 22 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to read the files from. A path without a leading `/` is relative to the home directory of the user. | string |  | outgoing/orders |
| **antInclude** | Include Files (Wildcards) | Wildcard patterns, separated by commas, that the path of a file must match to be read, such as `**.csv,**.xml`. The path is relative to `directoryName`, such as `2026/orders.csv` when `recursive` is true. **matches any part of a name and **any number of directories, so** `.csv` matches the CSV files in `directoryName` only, and** `/*.csv` those in the subdirectories too. Upper and lower case differ. When it is not set, all the files are read. | string |  | **\*/**.csv |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName` is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | A setting of FTP that has no effect on SFTP, which always transfers files byte for byte. Leave it unset. | boolean | false |  |
| **connectTimeout** | Connect Timeout | How long to wait for the connection to the SFTP server, in milliseconds. A connection that fails is tried 3 times before the poll is skipped. When it is not set, 10000. | integer |  | 10000 |
| **delay** | Poll Interval | How long to wait between two polls of the directory, in milliseconds. For example, 60000 polls once a minute. When it is not set, 500. | integer |  | 60000 |
| **delete** | Delete | If true, each file is deleted from the server once it has been read and handed on successfully. Use it to read each file only once, also across restarts. To keep the files, set `move` instead. | boolean | false |  |
| **exclude** | Exclude Files | A regular expression for the names of the files not to read, such as `.*\.(tmp|part)`. The whole name must match, upper and lower case count as the same, and only the name is matched, not its directory. A file it matches is not read, even when `include` or `antInclude` matches it too. | string |  | .\*\\.(tmp|part) |
| **idempotent** | Skip Files Already Read | If true, a file is read only once while the integration runs, even when it stays on the server. The list of the files read is kept in memory, so after a restart the files still on the server are read again, unless `move` or `delete` takes them away, or `idempotentRepository` keeps the list elsewhere. If false, and neither `delete` nor `move` is set, the same files are read again on every poll. | boolean | true |  |
| **idempotentRepository** | Files Read Store | The name of a bean that keeps the list of the files read, so that the files left on the server are not read again after a restart, such as a `FileIdempotentRepository` that keeps the list in a file. Declare the bean in the integration, for example under `beans` in YAML. Only used when `idempotent` is true. When it is not set, the list is kept in memory. | string |  | readFiles |
| **ignoreFileNotFoundOrPermissionError** | Ignore Access Errors | If true, a directory or a file that does not exist, or that `username` may not read, is skipped. If false, it causes an error. | boolean | false |  |
| **include** | Include Files | A regular expression that the name of a file must match to be read, such as `.*\.csv` for the CSV files. The whole name must match, upper and lower case count as the same, and only the name is matched, not its directory. The other files stay on the server. When it is not set, all the files are read. | string |  | .\*\\.csv |
| **knownHostsUri** | Known Hosts URI | The known\_hosts file that holds the key of the server, starting with `file://`, `classpath://`, `http://` or `https://`. Its lines can be made with `ssh-keyscan`. When it is not set, `~/.ssh/known_hosts` of the user that runs the integration is used, unless `useUserKnownHostsFile` is false; set it when that file does not exist, for example in a container. | string |  | file:///etc/sftp/known\_hosts |
| **maxMessagesPerPoll** | Max Files Per Poll | The largest number of files to read in one poll, such as 100. The other files are read at the next polls. The poll takes the first files the server lists, and `sortBy` sorts only these. When it is not set, or 0, all the files found are read. | integer |  | 100 |
| **move** | Move After Read | Where to move each file on the server once it has been read and handed on successfully, so that it is not read again, also after a restart. A directory name, such as `.done`, is relative to the directory of the file. A path that ends with the name of the file, such as `done/$\\{date:now:yyyyMMdd}/$\\{file:name}`, is relative to `directoryName`, where `$\\{file:name}` is the name of the file and `$\\{date:now:yyyyMMdd}` today’s date. A directory whose name starts with a dot is never read, which matters when `recursive` is true. Missing directories are created, so `username` must be allowed to create directories and to rename files. When it is not set, files stay where they are. When `delete` is true too, the integration fails to start. | string |  | .done |
| **moveFailed** | Move Failed Files To | Where to move a file on the server when it could not be handed on, for example because the next step failed, so that it is not read over and over. The same format as `move`, such as `.error`. When it is not set, a file that fails stays where it is and is read again at every poll. It can be set together with `delete` or `move`. | string |  | .error |
| **passiveMode** | Passive Mode | A setting of FTP that has no effect on SFTP. Leave it unset. | boolean | false |  |
| **password** | Password | The password of `username`. Leave it empty to log in with a private key instead, set in `privateKeyFile` or `privateKeyUri`. | string |  |  |
| **preMove** | Move Before Read | Where to move each file on the server before it is read, so that another reader of the same directory does not take it too. The same format as `move`, such as `.inprogress`, a directory next to the file. `move`, `moveFailed` and `delete` then act on the file in its new place, so with `move` set to `.done` the file ends up in `.inprogress/.done`. When it is not set, a file is read where it is. | string |  | .inprogress |
| **privateKeyFile** | Private Key File | The path of a private key file on the machine that runs the integration, to log in with instead of a password. The matching public key must be in the `authorized_keys` of `username` on the server. | string |  | /etc/sftp/keys/id\_rsa |
| **privateKeyPassphrase** | Private Key Passphrase | The passphrase of the private key, when the key is protected with one. | string |  |  |
| **privateKeyUri** | Private Key URI | Where to load the private key from, instead of `privateKeyFile`. It starts with `file://` for a file, `classpath://` for a resource in the application, or `http://` or `https://`. | string |  | file:///etc/sftp/keys/id\_rsa |
| **readLock** | Wait Until Written | How to make sure that another program has finished writing a file before it is read. `changed` reads a file once its size and modification time have not changed between two checks 5 seconds apart, or, with `readLockMinAge`, once the file is that old. A file still changing after 20 seconds is skipped until the next poll, and while a file is checked the other files wait. `changed` never reads an empty file. `rename` reads a file once it can be renamed. `none` reads the files as they are. When it is not set, `none`. Enum values: \* none \* changed \* rename | string |  | changed |
| **readLockMinAge** | Minimum File Age | Only used when `readLock` is `changed`: how old a file must be, in milliseconds, before it is read, counted from its modification time on the server. For example, 60000 leaves a file alone until it has not been changed for one minute. A file that is not old enough is skipped until the next poll, after 20 seconds of checks. The clocks of the server and of the integration must agree. | integer |  | 60000 |
| **recursive** | Recursive | If true, the files in the subdirectories of `directoryName` are read too. | boolean | false |  |
| **serverAliveInterval** | Server Alive Interval | How often to check, in milliseconds, that the server still answers while no data comes from it. When the server misses a check, the connection is closed and the poll fails, and a new connection is made at the next poll. Use it to notice a lost connection soon, for example behind a firewall that drops idle connections. When it is set, `socketTimeout` is not used. When it is not set, no checks are made. | integer |  | 30000 |
| **socketTimeout** | Socket Timeout | How long the connection may stay without an answer from the server, in milliseconds, before it is closed and the poll fails. It is not used when `serverAliveInterval` is set. When it is not set, 300000 (5 minutes). | integer |  | 60000 |
| **sortBy** | Sort By | The order in which the files of a poll are read. `file:name` sorts them by name, `file:modified` by modification time and `file:length` by size. Put `reverse:` before it for the reverse order, such as `reverse:file:modified` for the newest first. Separate several sorts with `;`, such as `file:modified;file:name`. When it is not set, the files are read in the order the server lists them. | string |  | file:modified |
| **streamDownload** | Stream Download | If true, each file is read from the server while it is handed on, instead of being downloaded into memory first, and the body is a stream. Use it for files too large for memory. It saves memory only when the integration does not keep the stream in memory either: set `camel.main.streamCachingSpoolEnabled=true`, which writes large bodies to a temporary file, or turn stream caching off. When it is not set, false. | boolean |  |  |
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
    
-   **Delete**: Delete files after successful processing (default: false). When false, and **Move** is not set, files are left on the server; with **Idempotent**, they are skipped while the integration runs but read again after a restart
    
-   **Move**: Where to move each file on the server after it has been read, such as `.done`, so that it is not read again, also after a restart (not set by default). It cannot be combined with **Delete**
    
-   **Move Failed**: Where to move a file on the server when it could not be handed on, such as `.error` (not set by default). When not set, a file that fails is read again at every poll
    
-   **Include Files**: A regular expression that the name of a file must match to be read, such as `.*\.csv`; upper and lower case count as the same (not set by default)
    
-   **Exclude Files**: A regular expression for the names of the files not to read; it wins over **Include Files** and **Include Files (Wildcards)** (not set by default)
    
-   **Include Files (Wildcards)**: Wildcard patterns for the path below the directory, such as `**.csv**` **or** `*/*.csv`; upper and lower case differ (not set by default)
    
-   **Move Before Read**: Where to move each file before it is read, such as `.inprogress` (not set by default)
    
-   **Wait Until Written**: `changed` reads a file only once it has stopped changing, `rename` once it can be renamed (default: none)
    
-   **Minimum File Age**: With `changed`, how old a file must be before it is read, in milliseconds (not set by default)
    
-   **Poll Interval**: How long to wait between two polls, in milliseconds (default: 500)
    
-   **Max Files Per Poll**: The largest number of files read in one poll (not set by default: all)
    
-   **Sort By**: The order of the files in a poll, such as `file:modified` or `reverse:file:name` (not set by default: the order of the server)
    
-   **Stream Download**: Read each file from the server while it is handed on, instead of into memory first (default: false)
    
-   **Connect Timeout**: How long to wait for the connection, in milliseconds (default: 10000)
    
-   **Socket Timeout**: How long the connection may stay without an answer, in milliseconds (default: 300000)
    
-   **Server Alive Interval**: How often to check that the server still answers, in milliseconds (not set by default)
    

### Output Format

The Kamelet outputs the file content as bytes, or as a stream when **Stream Download** is true, and sets headers with file information: - `file`: The name of the processed file - `ce-file`: Cloud Events compatible file name header

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

### Example with Files Moved After Reading

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
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
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/incoming"
        idempotentRepository: "readFiles"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The file must be on storage that survives a restart of the integration, such as a persistent volume. A file that is put on the server again under the same name is not read again.

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

### Example with File Filters and Files Still Being Written

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/incoming"
        recursive: true
        antInclude: "**/*.csv"
        exclude: "draft-.*"
        readLock: "changed"
        sortBy: "file:modified"
        maxMessagesPerPoll: 100
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Once a minute, this reads the CSV files in `/incoming` and its subdirectories, except those whose names start with `draft-`, at most 100 of them in each poll, the oldest first. **Include Files (Wildcards)** matches the path below the directory, and upper and lower case differ: `*.csv` alone would match only the files directly in `/incoming`. **Include Files** and **Exclude Files** are regular expressions that match the name of the file alone, whatever the case. With **Max Files Per Poll**, a poll takes the first files the server lists and sorts only these.

`readLock: changed` reads a file only once its size and modification time have not changed for 5 seconds, so a file that another program is still uploading is left alone. It never reads an empty file, and while it checks a file the other files wait. With **Minimum File Age**, a file is read only once it is that old instead.

The files a poll reads can be moved out of the way first with **Move Before Read**, so that a second integration reading the same directory does not take them too:

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/incoming"
        preMove: ".inprogress"
        move: ".done"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Each file is moved to `.inprogress` before it is read, and from there to `.done` once it has been handed on, so it ends up in `/incoming/.inprogress/.done`.

### Example with Large Files

By default each file is downloaded into memory before it is handed on. For files too large for that, set **Stream Download**:

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/exports"
        streamDownload: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Camel keeps a message body that is a stream in memory too, unless told otherwise, so also set `camel.main.streamCachingSpoolEnabled=true` in the application properties: large bodies are then written to a temporary file. In a test with 256 MB of memory, a 400 MB file failed with an out of memory error without **Stream Download**, and with it but without spooling, and was read with both.

### Example with a Connection Check

```yaml
- route:
    from:
      uri: "kamelet:sftp-source"
      parameters:
        connectionHost: "sftp.example.com"
        username: "sftpuser"
        password: "sftppass"
        directoryName: "/incoming"
        connectTimeout: 5000
        serverAliveInterval: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Every 30 seconds without data from the server, the integration checks that the server still answers. When it does not, the connection is closed, the poll fails, and the next poll connects again. Without **Server Alive Interval**, a connection that no longer answers is closed after **Socket Timeout**, 5 minutes by default.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/sftp-source.kamelet.yaml)