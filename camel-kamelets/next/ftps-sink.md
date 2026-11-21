# ![ftps sink](_images/kamelets/ftps-sink.svg) FTPS Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file to a directory on an FTPS server, which is FTP with TLS encryption.

Use it to deliver exports, reports or data files to a partner or a legacy system that receives files over FTPS. For a server without TLS use `ftp-sink`, and for a server you reach with SSH use `sftp-sink`.

Input: the body is the content of the file, as text, bytes or a stream. The name of the file comes from the `file` header, or from `ce-file` when `file` is not set; any directory in it is dropped, so `reports/data.csv` is written as `data.csv`. Without these headers, `CamelFileName` is used as it is, subdirectories included, and without any of them a unique name is generated.

Output: the message is unchanged. The `CamelFileNameProduced` header is set to the path of the file on the server.

Good to know: a file with the same name is replaced, unless `fileExist` says otherwise. A file is uploaded under its real name from the start, so a reader that polls the directory can pick it up half-written. To prevent that, set `tempPrefix` to upload it under a temporary name and rename it once it is complete, or `doneFileName` to write an empty done file next to it once it is complete. By default it uses explicit TLS: it connects to the normal FTP port, usually 21, and then switches to TLS. For a server that uses implicit TLS, usually on port 990, set `implicit` to true. To keep the connection on TLS 1.2, set `securityProtocol` to `TLSv1.2`. The certificate of the server must be signed by a certificate authority (CA) that Java trusts. For a server with a self-signed certificate, or one signed by a private CA, set `trustStoreFile` and `trustStorePassword`: the Kamelet then trusts the certificates in that trust store, for this connection only. Do not use the `javax.net.ssl.trustStore` system property for this: it replaces the trust of the whole integration, so its other HTTPS connections, such as the downloads of its dependencies, then fail when the trust store does not hold their CAs too. A file name that points outside `directoryName` fails the message. Files are sent in ASCII (text) mode unless `binary` is true. Headers that start with `CamelFile` or `CamelOverruleFile`, except `CamelFileName`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `ftps-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionHost** | Connection Host | **Required** The host name or IP address of the FTPS server, without `ftps://` and without a port. | string |  | ftps.example.com |
| **connectionPort** | Connection Port | **Required** The port of the FTPS server, usually 21, or 990 when `implicit` is true. | string | 21 |  |
| **directoryName** | Directory Name | **Required** The directory on the server to write the files to. A path without a leading `/` is relative to the home directory of the user. It is created when it does not exist, unless `autoCreate` is false. | string |  | upload/orders |
| **password** | Password | **Required** The password of `username` on the FTPS server. | string |  |  |
| **username** | Username | **Required** The user to log in to the FTPS server as. | string |  |  |
| **autoCreate** | Autocreate Missing Directories | If true, `directoryName`, and any subdirectory in the `CamelFileName` header, is created on the server when it does not exist. | boolean | true |  |
| **binary** | Binary Mode | If true, files are transferred in binary mode, byte for byte. When false, they are transferred in ASCII mode, which is meant for text. Set it to true for files that are not text, such as images, archives or PDF files. | boolean | false |  |
| **doneFileName** | Done File Name | The name of an empty file to write next to each file once the file is complete, so that a reader knows the file can be read. `$\\{file:name}` stands for the name of the file and `$\\{file:name.noext}` for the name without its extension, so `$\\{file:name}.done` writes `orders.csv.done`, and `$\\{file:name.noext}.ready` writes `orders.ready`. A fixed name, such as `ready`, is written again after each file. No other `$\\{…​}` is allowed, and with one the file is uploaded but then the message fails. With `tempPrefix`, the done file is written after the file has its real name. When it is not set, no done file is written. | string |  | ${file:name}.done |
| **fileExist** | If File Exists | What to do when a file with the same name is already in the directory. `Override` replaces it, `Append` adds the new content at its end, `Fail` fails the message, and `Ignore` keeps the old file and drops the new content without an error. Enum values: \* Override \* Append \* Fail \* Ignore | string | Override |  |
| **implicit** | Implicit TLS | If true, the connection uses implicit TLS: it is encrypted from the start, usually on port 990. If false, it uses explicit TLS: it connects to the normal FTP port, usually 21, and then switches to TLS. Use the mode the server expects; the other one fails to connect. When it is not set, false. | boolean |  |  |
| **passiveMode** | Passive Mode | If true, the transfers use passive mode, in which the integration opens all the connections to the server. Set it to true when the integration or the server is behind a firewall or NAT, where the default active mode often fails. | boolean | false |  |
| **securityProtocol** | TLS Version | The newest TLS version that the connection offers, such as `TLSv1.3` or `TLSv1.2`. With `TLSv1.3`, a server that speaks only TLS 1.2 is reached too. With `TLSv1.2`, the connection never uses TLS 1.3. Set it for a server whose TLS 1.3 connections fail or hang. A server that speaks only TLS 1.3 then refuses the connection, with `protocol_version` in the error. When it is not set, `TLSv1.3`. | string |  | TLSv1.2 |
| **tempPrefix** | Temporary Name Prefix | A prefix for the name a file is uploaded under. Once the upload is complete, the file is renamed to its real name, so a reader that skips the names with this prefix never picks up a half-written file. `ftps-source`, like other readers built with Camel, skips the names that start with a dot, so a prefix such as `.tmp-`, which uploads `orders.csv` as `.tmp-orders.csv`, works with it as it is. A prefix that ends with `/`, such as `.inprogress/`, uploads the file into that subdirectory first, and the subdirectory is created when it does not exist, unless `autoCreate` is false. When it is not set, a file is uploaded under its real name from the start. With `fileExist` `Override`, a file of the same name is deleted when the upload starts, not when it ends. It cannot be combined with `fileExist` `Append`, and every message fails when both are set. `username` must be allowed to rename files. | string |  | .tmp- |
| **trustStoreFile** | Trust Store File | The path of a trust store file that holds the certificate of the FTPS server, or of the certificate authority (CA) that signed it, such as a PKCS12 or JKS file made with `keytool`. Set it for a server with a self-signed certificate, or one signed by a private CA. Set `trustStorePassword` with it, or every message fails. Only the certificates in this file are trusted for the server, not those that Java trusts, and only for this connection, so the rest of the integration keeps the trust of Java. When it is not set, the certificate of the server is checked against the certificate authorities that Java trusts. | string |  | /etc/ftps/truststore.p12 |
| **trustStorePassword** | Trust Store Password | The password of the trust store in `trustStoreFile`. It is needed with `trustStoreFile`; set without `trustStoreFile`, every message fails. | string |  |  |
| **trustStoreType** | Trust Store Type | The type of the trust store in `trustStoreFile`, such as `PKCS12` or `JKS`. Current Java versions read both PKCS12 and JKS files with either of these types, so it is needed only for other types. Set without `trustStoreFile`, every message fails. When it is not set, the default type of Java, `PKCS12` on current versions. | string |  | PKCS12 |

## Dependencies

At runtime, the `ftps-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:ftps-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## FTPS Sink Kamelet Description

### Authentication

This Kamelet uses username and password authentication to connect to FTPS (FTP over SSL/TLS) servers.

### Secure Connection

FTPS provides secure file transfer over encrypted connections using SSL/TLS protocols.

### Connection Configuration

Requires: - Connection host (FTPS server hostname) - Connection port (defaults to 21; usually 990 with implicit TLS) - Username and password credentials - Directory name for file operations

### File Transfer Options

-   **Transfer Mode**: ASCII (default) or Binary mode
    
-   **Passive Mode**: Can be enabled for firewall compatibility
    
-   **File Existence Handling**: Override (default), Append, Fail, or Ignore
    
-   **Auto-create Directories**: Automatically creates missing directories (enabled by default)
    
-   **Temporary Name Prefix**: Upload each file under a temporary name, such as `.tmp-orders.csv`, and rename it to its real name once it is complete (not set by default)
    
-   **Done File Name**: Write an empty done file next to each file once it is complete, such as `orders.csv.done` (not set by default)
    
-   **Implicit TLS**: Use implicit TLS, usually on port 990, instead of explicit TLS on the normal FTP port (default: false)
    

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses a default naming convention.

The value is reduced to a single file name before use: any directory component is dropped, so `reports/2026/data.csv` is stored as `data.csv`. The file is always written inside the configured directory.

### Example with a Temporary Name and a Done File

By default a file is uploaded under its real name from the start, so a reader that polls the directory can pick it up half-written. Set **tempPrefix**, **doneFileName**, or both, to prevent that:

```yaml
- route:
    from:
      uri: "timer:tick"
      parameters:
        period: 60000
      steps:
        - setBody:
            constant: "order-1,42"
        - setHeader:
            name: file
            constant: "orders.csv"
        - to:
            uri: "kamelet:ftps-sink"
            parameters:
              connectionHost: "ftps.example.com"
              username: "ftpuser"
              password: "ftppass"
              directoryName: "/incoming"
              tempPrefix: ".tmp-"
              doneFileName: "${file:name}.done"
```

Each file is uploaded as `.tmp-orders.csv` and renamed to `orders.csv` once the upload is complete, and then an empty `orders.csv.done` is written next to it. The FTPS Source Kamelet, like other readers built with Camel, skips the names that start with a dot, so it never reads a half-written file; another reader can wait for the `.done` file. In **doneFileName**, `${file:name}` stands for the name of the file and `${file:name.noext}` for the name without its extension; no other `${…​}` is allowed. The user needs the right to rename files on the server. **tempPrefix** cannot be combined with **fileExist** set to `Append`, and with `Override` a file of the same name is deleted when the upload starts.

### Example with Implicit TLS

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Hello"
      steps:
        - to:
            uri: "kamelet:ftps-sink"
            parameters:
              connectionHost: "ftps.example.com"
              connectionPort: "990"
              username: "ftpsuser"
              password: "ftpspass"
              directoryName: "/upload"
              implicit: true
              passiveMode: true
```

By default the Kamelet uses explicit TLS: it connects to the normal FTP port, usually 21, and then switches to TLS. A server that uses implicit TLS, usually on port 990, expects an encrypted connection from the start: set **Implicit TLS** for it.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ftps-sink.kamelet.yaml)