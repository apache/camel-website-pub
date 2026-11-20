# ![azure storage files source](_images/kamelets/azure-storage-files-source.svg) Azure Storage File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory of a file share in Azure Files, one message per file, and can delete each file once it has been read.

Use it to process files that people or applications put on a share, such as scanned documents or exports. For blob containers, use `azure-storage-blob-source`.

Output: the body is the file, which converts to text, bytes or a stream, and the `Content-Type` header is `application/octet-stream`. The `CamelFileName` header is the path of the file from `directoryName`, `CamelFileNameOnly` its name, and `CamelFileLength` and `CamelFileLastModified` its size and last-modified time.

Good to know: files are kept after they are read, so the same files are read again on every poll, every 500 milliseconds by default. To read each file only once, set `deleteAfterRead` to true to delete it, set `move` to a directory such as `.done` to move it, or set `noop` to true to leave it in place and remember the files read, in memory or, with `idempotentRepository`, across restarts. Subdirectories are read only when `recursive` is true. `include` and `antInclude` read only the files whose names match.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-files-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.file.core.windows.net](https://\<accountName\>.file.core.windows.net)`. | string |  | mystorageaccount |
| **shareName** | Share Name | **Required** The name of the file share in the storage account to read the files from. | string |  | documents |
| **antInclude** | Ant Include | Wildcard patterns, separated by commas, that the path of a file below `directoryName` must match to be read, such as `**/**.csv****`****.** matches any part of a name, and** any number of directories. When it is not set, all files are read. | string |  | **\*/**.csv |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, uses `sharedKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. The other values need settings that this Kamelet does not offer. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_SAS | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | How long to wait between two polls of the directory, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete File | If true, each file is deleted from the share once it has been processed. When false, the files stay and are read again on every poll, unless `move` or `noop` is set. When `move` is set too, the integration fails to start. | boolean | false |  |
| **directoryName** | Directory Name | The directory of the share to read the files from, such as `inbox/orders`. `.`, the default, is the top of the share. | string | . | inbox/orders |
| **idempotentRepository** | Files Read Store | The name of a bean that keeps the list of the files read, so that the files left on the share are not read again after a restart, such as a `FileIdempotentRepository` that keeps the list in a file. Declare the bean in the integration, for example under `beans` in YAML. Only used when `noop` is true. | string |  | readFiles |
| **include** | Include | A regular expression that the name of a file must match, as a whole and ignoring case, to be read, such as `.*\.(csv|txt)`. It is matched against the name of the file without its directory. When it is not set, all files are read. | string |  | .\*\\.csv |
| **maxMessagesPerPoll** | Max Files Per Poll | The most files to read at each poll, such as 100. The other files are read at the next polls. Use it to start slowly on a share that holds many files. When it is not set, all files are read at each poll. | integer |  | 100 |
| **move** | Move After Read | Where to move each file on the share once it has been read and handed on successfully, so that it is not read again, also after a restart. A directory name, such as `.done`, is relative to the directory of the file. A path that ends with the name of the file, such as `done/$\\{date:now:yyyyMMdd}/$\\{file:name}`, is relative to `directoryName`, where `$\\{file:name}` is the name of the file and `$\\{date:now:yyyyMMdd}` today’s date. A directory whose name starts with a dot is never read, which matters when `recursive` is true. Missing directories are created. When it is not set, files stay where they are. When `deleteAfterRead` is true too, the integration fails to start. | string |  | .done |
| **noop** | Leave Files Untouched | If true, the files are left where they are, and each file is read only once while the integration runs. The list of the files read is kept in memory, so the files are all read again after a restart, unless `idempotentRepository` keeps the list elsewhere. `move` is not used then. | boolean |  |  |
| **recursive** | Recursive Mode | If true, also reads the files in the subdirectories of `directoryName`. | boolean | false |  |
| **sharedKey** | Shared Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |

## Dependencies

At runtime, the `azure-storage-files-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-files
    
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
      uri: "kamelet:azure-storage-files-source"
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

## Azure Storage Files Source Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY` (default)
    
-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Shared key credentials: `SHARED_KEY_CREDENTIAL`
    
-   Azure SAS: `AZURE_SAS`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Example with Files Moved After Reading

```yaml
- route:
    from:
      uri: "kamelet:azure-storage-files-source"
      parameters:
        accountName: "mystorageaccount"
        shareName: "documents"
        sharedKey: "the-access-key"
        directoryName: "inbox"
        include: ".*\\.csv"
        move: ".done"
        maxMessagesPerPoll: 100
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Only the CSV files are read, at most 100 at each poll. Each file is moved to `inbox/.done` once it has been read, so it is not read again, also after a restart. Directories whose names start with a dot are never read, also when **recursive** is true. A path that ends with the name of the file, such as `done/$\{date:now:yyyyMMdd}/$\{file:name}`, moves the file to a directory of its own day below **directoryName**.

### Example with Files Remembered Across Restarts

To keep the files on the share and still read each one only once, also across restarts, set **noop** to true and keep the list of the files read in a file. Declare a `FileIdempotentRepository` bean that writes the list to a file, and give its name in **idempotentRepository**:

```yaml
- beans:
    - name: readFiles
      type: "#class:org.apache.camel.support.processor.idempotent.FileIdempotentRepository"
      properties:
        fileStore: "#class:java.io.File('/var/data/read-files.dat')"
- route:
    from:
      uri: "kamelet:azure-storage-files-source"
      parameters:
        accountName: "mystorageaccount"
        shareName: "documents"
        sharedKey: "the-access-key"
        directoryName: "inbox"
        noop: true
        idempotentRepository: "readFiles"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The file must be on storage that survives a restart of the integration, such as a persistent volume. Without **noop**, **idempotentRepository** is not used.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-source.kamelet.yaml)