# ![smb sink](_images/kamelets/smb-sink.svg) SMB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes each message as a file to a directory of a Windows or Samba file share (SMB).

Use it to deliver exports, reports or data files to a Windows file server or a NAS, on a share such as `\\fileserver\imports`. To read files from a share use `smb-source`. For an FTP or SFTP server use `ftp-sink` or `sftp-sink`.

Input: the body is the content of the file, as text, bytes or a stream. The name of the file comes from the `file` header, or from `ce-file` when `file` is not set; any directory in it is dropped, so `reports/data.csv` and `reports\data.csv` are written as `data.csv`. Without these headers, `CamelFileName` is used as it is, subdirectories included, and without any of them a unique name is generated.

Output: the message is unchanged. The `CamelFileNameProduced` header is set to the path of the file within the share.

Good to know: a file with the same name is replaced, unless `fileExist` says otherwise. A file is written under its real name from the start, so a reader that polls the directory can pick it up half-written. To prevent that, set `tempPrefix` to write it under a temporary name and rename it once it is complete, or `doneFileName` to write an empty done file next to it once it is complete. Log in with `username` and `password`, or, on a share that allows guest access, with `username` set to `Guest` and no `password`. A message fails when the server cannot be reached or the login fails. The content of the files is not encrypted on the network unless `encryptData` is true, and a share that requires encryption refuses the connection without it. When the application has a bean of the type `com.hierynomus.smbj.SmbConfig`, Camel uses it for the connection, and the Kamelet then fails to start when `encryptData` is true, or `connectTimeout`, `writeTimeout` or `transactTimeout` is set: set them on that bean instead. A file name that points outside `directoryName`, such as `../orders.csv`, fails the message. Headers that start with `CamelFile`, `CamelOverruleFile` or `CamelSmb`, except `CamelFileName`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `smb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the SMB server, without `smb://`, without `\\` and without a port. | string |  | fileserver.example.com |
| **shareName** | Share Name | **Required** The name of the share, as the server shares it, such as `imports` for `\\fileserver\imports`. | string |  | imports |
| **username** | Username | **Required** The user to log in to the SMB server as, without the domain, such as `jdoe`. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName`, and any subdirectory in the `CamelFileName` header, is created on the share when it does not exist. If false, a message for a directory that does not exist fails. | boolean | true |  |
| **connectTimeout** | Connect Timeout | How long to wait for the connection to the server, in milliseconds. When it is not set, 5000 (5 seconds). | integer |  | 10000 |
| **connectionPort** | Connection Port | The port of the SMB server, usually 445. | integer | 445 |  |
| **directoryName** | Directory Name | The directory within the share to write the files to, with `/` between its parts, such as `incoming/orders`. When it is not set, the files are written at the top of the share. It is created when it does not exist, unless `autoCreate` is false. | string |  | incoming/orders |
| **domain** | Domain | The Windows domain of `username`, such as `CORP` for the account `CORP\jdoe`. Leave it unset for a user of the server itself. | string |  | CORP |
| **doneFileName** | Done File Name | The name of an empty file to write next to each file once the file is complete, so that a reader knows the file can be read. `$\\{file:name}` stands for the name of the file and `$\\{file:name.noext}` for the name without its extension, so `$\\{file:name}.done` writes `orders.csv.done`, and `$\\{file:name.noext}.ready` writes `orders.ready`. A fixed name, such as `ready`, is written again after each file. No other `$\\{…​}` is allowed, and with one the file is written but then the message fails. With `tempPrefix`, the done file is written after the file has its real name. When it is not set, no done file is written. | string |  | ${file:name}.done |
| **encryptData** | Encrypt Data | If true, everything sent to and from the server, the content of the files included, is encrypted (SMB 3 encryption), also on a share that does not require it. A share that requires encryption, such as one with `smb encrypt = required` on Samba, refuses the connection unless it is true. The server must support SMB 3. | boolean | false |  |
| **fileExist** | If File Exists | What to do when a file with the same name is already in the directory. `Override` replaces it, `Append` adds the new content at its end, `Fail` fails the message, and `Ignore` keeps the old file and drops the new content without an error. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **password** | Password | The password of `username`. When it is not set, the Kamelet logs in with an empty password, which with `username` set to `Guest` is a guest login, on a share that allows guest access. | string |  |  |
| **tempPrefix** | Temporary Name Prefix | A prefix for the name a file is written under. Once the file is complete, it is renamed to its real name, so a reader that skips the names with this prefix never picks up a half-written file. `smb-source`, like other readers built with Camel, skips the names that start with a dot, so a prefix such as `.tmp-`, which writes `orders.csv` as `.tmp-orders.csv`, works with it as it is. A prefix that ends with `/`, such as `.inprogress/`, writes the file into that subdirectory first, and the subdirectory is created when it does not exist. When it is not set, a file is written under its real name from the start. Do not combine it with `fileExist` `Append`, as a message for a file that already exists then fails and leaves the temporary file behind. `username` must be allowed to rename files. | string |  | .tmp- |
| **transactTimeout** | Request Timeout | How long to wait for the server to answer the other requests, such as listing a directory, or opening, renaming or deleting a file, in milliseconds. When it is not set, 60000 (1 minute). | integer |  | 30000 |
| **writeTimeout** | Write Timeout | How long to wait for the server to answer a write of the content of a file, in milliseconds. When it is not set, 60000 (1 minute). | integer |  | 120000 |

## Dependencies

At runtime, the `smb-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:smb-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/smb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/smb-sink.kamelet.yaml)