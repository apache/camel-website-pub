# ![azure storage files sink](_images/kamelets/azure-storage-files-sink.svg) Azure Storage Files Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file to a directory of a file share in Azure Files, named after the `file` header.

Use it to drop files where applications or people that mount the share can read them, such as reports or exports. For blob containers, use `azure-storage-blob-sink`.

Input: the body is the content of the file: text, bytes or a stream. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The optional `file` header (or `ce-file`) is the name of the file; only its last part is used, so `reports/2026/data.csv` is written as `data.csv` in `directoryName`. Without it, the file gets a generated unique name.

Output: the message is unchanged.

Good to know: a file with the same name is replaced, unless `fileExist` says otherwise. Missing directories are created. Headers that start with `CamelFile` or `CamelOverruleFile` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-files-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.file.core.windows.net](https://\<accountName\>.file.core.windows.net)`. | string |  | mystorageaccount |
| **shareName** | Share Name | **Required** The name of the file share in the storage account to write the files to. | string |  | documents |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, uses `sharedKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. The other values need settings that this Kamelet does not offer. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_SAS | string | SHARED\_ACCOUNT\_KEY |  |
| **directoryName** | Directory Name | The directory of the share to write the files to, such as `inbox/orders`. `.`, the default, is the top of the share. | string | . | inbox/orders |
| **fileExist** | If File Exists | What to do when a file with the same name is already in the directory. `Override` replaces it. `Fail` keeps it and fails the message. `Ignore` keeps it and drops the new content, without an error. When it is not set, `Override`. Enum values: \* Override \* Fail \* Ignore | string |  |  |
| **sharedKey** | Shared Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |

## Dependencies

At runtime, the `azure-storage-files-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:azure-storage-files-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Files Sink Kamelet Description

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

### Optional Headers

In the headers, you can set the `file` / `ce-file` property to specify the filename to upload. If you do not set it, the file gets a generated unique name.

The value is reduced to a single file name before use: any directory component is dropped, so `reports/2026/data.csv` is stored as `data.csv`. The file is always written inside the configured directory.

### Example that Never Replaces a File

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "report"
        period: 60000
      steps:
        - setHeader:
            name: file
            simple: "report-$\{date:now:yyyyMMdd}.txt"
        - to:
            uri: "kamelet:azure-storage-files-sink"
            parameters:
              accountName: "mystorageaccount"
              shareName: "documents"
              sharedKey: "the-access-key"
              directoryName: "reports"
              fileExist: "Fail"
```

The first message of the day writes `reports/report-20261118.txt`. The later messages of the same day fail, and the file is kept. With `Ignore` instead of `Fail`, they are dropped without an error.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-sink.kamelet.yaml)