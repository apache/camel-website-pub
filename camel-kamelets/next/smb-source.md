# ![smb source](_images/kamelets/smb-source.svg) SMB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory of a Windows or Samba file share (SMB), one message per file, and by default leaves them on the share.

Use it to collect the files that another system drops on a Windows file server or a NAS, such as orders, invoices or exports, from a share such as `\\fileserver\exports`. To write files to a share use `smb-sink`. For an FTP or SFTP server use `ftp-source` or `sftp-source`.

Output: the body is the content of the file, as bytes, or as a stream when `streamDownload` is true. `Content-Type` is `application/octet-stream`. The `file` and `ce-file` headers hold the name of the file, with its path below `directoryName` when `recursive` is true, such as `2026/orders.csv`. `CamelFileName` holds the same name, `CamelFileLength` the size of the file in bytes, `CamelFileLastModified` the time the file was last changed, in milliseconds since 1970, and `CamelSmbUncPath` the full Windows path of the file, such as `\\fileserver\exports\orders\orders.csv`.

Good to know: files are not deleted or moved after they are read, unless `delete` is true or `move` is set. A file is read only once while the integration runs (`idempotent`), but the files left on the share are all read again after a restart; to read each file only once, also across restarts, set `move` to a directory such as `.done`, set `delete` to true, or keep the list of the files read in a file with `idempotentRepository`. To read only some of the files, set `include`, `exclude` or `antInclude`. To leave a file alone while another program is still writing it, set `readLock`. Log in with `username` and `password`, or, on a share that allows guest access, with `username` set to `Guest` and no `password`. When the server cannot be reached or the login fails, the poll is skipped with a warning in the log, and tried again at the next poll. The content of the files is not encrypted on the network unless `encryptData` is true, and a share that requires encryption refuses the connection without it. When the application has a bean of the type `com.hierynomus.smbj.SmbConfig`, Camel uses it for the connection, and the Kamelet then fails to start when `encryptData` is true, or `connectTimeout`, `readTimeout` or `transactTimeout` is set: set them on that bean instead.

## Configuration Options

The following table summarizes the configuration options available for the `smb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SMB server, without `smb://`, without `\\` and without a port. | string |  | fileserver.example.com |
| **shareName** | Share Name | **Required** The name of the share, as the server shares it, such as `exports` for `\\fileserver\exports`. | string |  | exports |
| **username** | Username | **Required** The user to log in to the SMB server as, without the domain, such as `jdoe`. | string |  |  |
| **antInclude** | Include Files (Wildcards) | Wildcard patterns, separated by commas, that the path of a file must match to be read, such as `**.csv,**.xml`. The path is relative to `directoryName`, such as `2026/orders.csv` when `recursive` is true. **matches any part of a name and **any number of directories, so** `/`**`.csv` matches the CSV files in `directoryName` and in its subdirectories. Upper and lower case differ. When it is not set, all the files are read. | string |  | **\*/**.csv |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName` is created on the share when it does not exist. | boolean | true |  |
| **connectTimeout** | Connect Timeout | How long to wait for the connection to the server, in milliseconds. When it is not set, 5000 (5 seconds). | integer |  | 10000 |
| **connectionPort** | Connection Port | The port of the SMB server, usually 445. | integer | 445 |  |
| **delay** | Poll Interval | How long to wait between two polls of the directory, in milliseconds. For example, 60000 polls once a minute. When it is not set, 500. | integer |  | 60000 |
| **delete** | Delete | If true, each file is deleted from the share once it has been read and handed on successfully. Use it to read each file only once, also across restarts. To keep the files, set `move` instead. | boolean | false |  |
| **directoryName** | Directory Name | The directory within the share to read the files from, with `/` between its parts, such as `outgoing/orders`. When it is not set, the files at the top of the share are read. `/` reads them too, but the names in the file headers then start with `/`, such as `/orders.csv`. | string |  | outgoing/orders |
| **domain** | Domain | The Windows domain of `username`, such as `CORP` for the account `CORP\jdoe`. Leave it unset for a user of the server itself. | string |  | CORP |
| **encryptData** | Encrypt Data | If true, everything sent to and from the server, the content of the files included, is encrypted (SMB 3 encryption), also on a share that does not require it. A share that requires encryption, such as one with `smb encrypt = required` on Samba, refuses the connection unless it is true. The server must support SMB 3. | boolean | false |  |
| **exclude** | Exclude Files | A regular expression for the names of the files not to read, such as `.*\.(tmp|part)`. The whole name must match, upper and lower case count as the same, and only the name is matched, not its directory. A file it matches is not read, even when `include` or `antInclude` matches it too. | string |  | .\*\\.(tmp|part) |
| **idempotent** | Skip Files Already Read | If true, a file is read only once while the integration runs, even when it stays on the share. The list of the files read is kept in memory, so after a restart the files still on the share are read again, unless `move` or `delete` takes them away, or `idempotentRepository` keeps the list elsewhere. If false, and neither `delete` nor `move` is set, the same files are read again on every poll. | boolean | true |  |
| **idempotentRepository** | Files Read Store | The name of a bean that keeps the list of the files read, so that the files left on the share are not read again after a restart, such as a `FileIdempotentRepository` that keeps the list in a file. Declare the bean in the integration, for example under `beans` in YAML. Only used when `idempotent` is true. When it is not set, the list is kept in memory. | string |  | readFiles |
| **include** | Include Files | A regular expression that the name of a file must match to be read, such as `.*\.csv` for the CSV files. The whole name must match, upper and lower case count as the same, and only the name is matched, not its directory. The other files stay on the share. When it is not set, all the files are read. | string |  | .\*\\.csv |
| **maxMessagesPerPoll** | Max Files Per Poll | The largest number of files to read in one poll, such as 100. The other files are read at the next polls. The poll takes the first files the server lists, and `sortBy` sorts only these. When it is not set, or 0, all the files found are read. | integer |  | 100 |
| **move** | Move After Read | Where to move each file on the share once it has been read and handed on successfully, so that it is not read again, also after a restart. A directory name, such as `.done`, is relative to the directory of the file. A path that ends with the name of the file, such as `done/$\\{date:now:yyyyMMdd}/$\\{file:name}`, is relative to `directoryName`, where `$\\{file:name}` is the name of the file, with its path below `directoryName`, and `$\\{date:now:yyyyMMdd}` today’s date. A directory whose name starts with a dot is never read, which matters when `recursive` is true. Missing directories are created, so `username` must be allowed to create directories and to rename files. When it is not set, files stay where they are. When `delete` is true too, the Kamelet fails to start. | string |  | .done |
| **moveFailed** | Move Failed Files To | Where to move a file on the share when it could not be handed on, for example because the next step failed, so that it is not read over and over. The same format as `move`, such as `.error`. When it is not set, a file that fails stays where it is and is read again at every poll. It can be set together with `delete` or `move`. | string |  | .error |
| **password** | Password | The password of `username`. When it is not set, the Kamelet logs in with an empty password, which with `username` set to `Guest` is a guest login, on a share that allows guest access. | string |  |  |
| **preMove** | Move Before Read | Where to move each file on the share before it is read, so that another reader of the same directory does not take it too. The same format as `move`, such as `.inprogress`, a directory next to the file. `move`, `moveFailed` and `delete` then act on the file in its new place, so with `move` set to `.done` the file ends up in `.inprogress/.done`. When it is not set, a file is read where it is. | string |  | .inprogress |
| **readLock** | Wait Until Written | How to make sure that another program has finished writing a file before it is read. `changed` reads a file once its size and modification time have not changed between two checks 1 second apart, or, with `readLockMinAge`, once the file is that old. A file still changing after 10 seconds is skipped until the next poll, and while a file is checked the other files wait. `changed` never reads an empty file. `rename` reads a file once it can be renamed. `none` reads the files as they are. When it is not set, `none`. Enum values: \* none \* changed \* rename | string |  | changed |
| **readLockMinAge** | Minimum File Age | Only used when `readLock` is `changed`: how old a file must be, in milliseconds, before it is read, counted from its modification time on the share. For example, 60000 leaves a file alone until it has not been changed for one minute. A file that is not old enough is skipped until the next poll, after 10 seconds of checks. The clocks of the server and of the integration must agree. | integer |  | 60000 |
| **readTimeout** | Read Timeout | How long to wait for the server to answer a read of the content of a file, in milliseconds. When it is not set, 60000 (1 minute). | integer |  | 120000 |
| **recursive** | Recursive | If true, the files in the subdirectories of `directoryName` are read too. | boolean | false |  |
| **sortBy** | Sort By | The order in which the files of a poll are read. `file:name` sorts them by name, `file:modified` by modification time and `file:length` by size, from the smallest. Put `reverse:` in front for the reverse order, such as `reverse:file:modified` for the newest first, or `ignoreCase:` to sort names without case. Separate several orders with `;`, such as `file:modified;file:name`. When it is not set, the files are read in the order the server lists them. | string |  | reverse:file:modified |
| **streamDownload** | Stream Download | If true, each file is read from the share while it is handed on, instead of being read into memory first, and the body is a stream. Use it for files too large for memory. It saves memory only when the integration does not keep the stream in memory either: set `camel.main.streamCachingSpoolEnabled=true`, which writes large bodies to a temporary file, or turn stream caching off. When it is not set, false. | boolean |  |  |
| **transactTimeout** | Request Timeout | How long to wait for the server to answer the other requests, such as listing a directory, or opening, renaming or deleting a file, in milliseconds. When it is not set, 60000 (1 minute). | integer |  | 30000 |

## Dependencies

At runtime, the `smb-source` Kamelet relies upon the presence of the following dependencies:

-   camel:smb
    
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
      uri: "kamelet:smb-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smb-source.kamelet.yaml)