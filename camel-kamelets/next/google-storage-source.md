# ![google storage source](_images/kamelets/google-storage-source.svg) Google Storage Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files (objects) in a Google Cloud Storage bucket, one message per file, and by default deletes each file once it has been read.

Use it to process files that another system drops into a bucket, such as uploaded documents, exported reports or log files. To react to new files through Pub/Sub notifications instead of reading the bucket over and over, use `google-storage-event-based-source`.

Output: the body is the content of the file, as a stream, and the `Content-Type` header is `application/octet-stream`. The headers give the bucket name (`CamelGoogleCloudStorageBucketName`), the object name, that is the path of the file in the bucket (`CamelGoogleCloudStorageObjectName`), the content type and the ETag of the file.

Good to know: files are deleted from the bucket after they are read, unless `deleteAfterRead` is set to false; then the same files are read again on every poll, about twice a second, or every `delay` milliseconds. With `moveAfterRead`, they are copied to `destinationBucket` first. A file whose processing fails is not deleted or moved, and is read again on the next poll. Without `serviceAccountKey`, it logs in with the Application Default Credentials of the environment where it runs, or with Workload Identity Federation when `useWorkloadIdentityFederation` is true.

## Configuration Options

The following table summarizes the configuration options available for the `google-storage-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket to read the files from, without `gs://`. | string |  | my-bucket |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. | boolean | false |  |
| **delay** | Delay | How long to wait between two reads of the bucket, in milliseconds. For example, 60000 is one minute. When it is not set, it is 500. | integer |  | 60000 |
| **deleteAfterRead** | Auto-delete Objects | If true, each file is deleted from the bucket after it has been read. Set it to false to keep the files; they are then read again on every poll. | boolean | true |  |
| **destinationBucket** | Destination Bucket | The name of the bucket to move the files to, without `gs://`. Only used when `moveAfterRead` is true. The bucket must exist; when it does not, a warning is logged and each file stays in its bucket, so it is read again on every poll. | string |  | my-archive-bucket |
| **filter** | Filter | A regular expression that the whole name of a file must match for the file to be read, such as `.*\.csv` for the CSV files only. The name includes the folders, as in `inbox/orders.csv`. | string |  | .\*\\.csv |
| **impersonatedServiceAccount** | Impersonated Service Account | The email of a service account to act as, with the credentials of Workload Identity Federation, so that the Kamelet gets the permissions of that service account. The federated identity needs the Service Account Token Creator role on it. Only used when `useWorkloadIdentityFederation` is true. | string |  | storage-reader@my-project-123.iam.gserviceaccount.com// |
| **includeBody** | Include Body | If true, the body is the content of the file. If false, the content is not downloaded, the body is empty, and only the headers describe the file, such as its size in `CamelGoogleCloudStorageContentLength`. When it is not set, it is true. | boolean |  |  |
| **includeFolders** | Include Folders | If true, folder markers, that is empty objects whose name ends with `/`, are read as files too. Set it to false to skip them. When it is not set, it is true. | boolean |  |  |
| **moveAfterRead** | Move Objects After Read | If true, each file is copied to `destinationBucket` after it has been read, under the same name, and then deleted from this bucket unless `deleteAfterRead` is false. A file whose processing fails is not moved. When it is not set, it is false. | boolean |  |  |
| **prefix** | Prefix | Only read the files whose name starts with this text, such as a folder followed by `/`. | string |  | inbox/ |
| **serviceAccountKey** | Service Account Key | The JSON key of a service account that may read (and delete) the files of the bucket, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. When it is not set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | binary |  |  |
| **useWorkloadIdentityFederation** | Use Workload Identity Federation | If true, it logs in with Workload Identity Federation instead of `serviceAccountKey`, which is then ignored. It uses the credential configuration file in `workloadIdentityConfig` or, when that is not set, the Application Default Credentials. When it is not set, it is false. | boolean |  |  |
| **workloadIdentityConfig** | Workload Identity Configuration | Where to load the Workload Identity Federation credential configuration file from: the JSON file of type `external_account` that `gcloud iam workload-identity-pools create-cred-config` creates, which tells how to exchange a token of another identity provider, such as AWS, Azure or Kubernetes, for Google credentials. Prefix the path with `file:`, `classpath:`, `http:` or `https:`. Only used when `useWorkloadIdentityFederation` is true. | string |  | file:/var/run/secrets/gcp/credential-config.json |

## Dependencies

At runtime, the `google-storage-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-storage
    
-   camel:jackson3
    

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
      uri: "kamelet:google-storage-source"
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

## Google Storage Source Kamelet Description

### Authentication methods

This Kamelet uses Service Account Key authentication to connect to Google Cloud Storage. You need to provide:

-   A service account key encoded in base64 format (optional, can use default credentials)
    
-   The name of the bucket from which to consume objects
    

### Output format

The Kamelet consumes objects from Google Cloud Storage and produces the object data.

### Configuration

The Kamelet requires the following parameters:

-   `bucketNameOrArn`: The name of the Google Cloud Storage bucket
    

Optional parameters: - `serviceAccountKey`: The service account key to use as credentials (must be base64 encoded) - `deleteAfterRead`: Specifies to delete objects after consuming them (default: true) - `autoCreateBucket`: Specifies to automatically create the Google Cloud Storage bucket (default: false) - `prefix`: The prefix which is used in the BlobListOptions to only consume objects we are interested in - `moveAfterRead` and `destinationBucket`: Move each file to another bucket after it has been read - `includeBody`: Set it to false to read only the description of each file, not its content (when not set: true) - `includeFolders`: Set it to false to skip the folder markers, the empty objects whose name ends with `/` (when not set: true) - `delay`: How long to wait between two reads of the bucket, in milliseconds (when not set: 500) - `useWorkloadIdentityFederation`, `workloadIdentityConfig` and `impersonatedServiceAccount`: Log in with Workload Identity Federation, see below

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:google-storage-source"
      parameters:
        bucketNameOrArn: "my-storage-bucket"
        serviceAccountKey: "{{service-account-key-base64}}"
        deleteAfterRead: false
        autoCreateBucket: false
        prefix: "data/"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Moving Files to Another Bucket

With `moveAfterRead`, each file that has been processed is copied to `destinationBucket`, under the same name, and then deleted from the bucket it was read from. A file whose processing fails stays where it is. To read a large bucket only once a minute, and to move the files without downloading their content:

```yaml
- route:
    from:
      uri: "kamelet:google-storage-source"
      parameters:
        bucketNameOrArn: "my-bucket"
        moveAfterRead: true
        destinationBucket: "my-archive-bucket"
        includeBody: false
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

With `includeBody: false`, the body is empty, and the headers describe the file, such as `CamelGoogleCloudStorageObjectName` and `CamelGoogleCloudStorageContentLength`. The destination bucket must exist: when it does not, a warning is logged, and the file stays in its bucket and is read again on every poll. With `deleteAfterRead: false`, the file is copied and kept, so it is read and copied again on every poll.

### Workload Identity Federation

To run without a service account key, outside Google Cloud, the Kamelet can exchange a token of another identity provider, such as AWS, Azure or a Kubernetes service account, for Google credentials. Create the credential configuration file with `gcloud iam workload-identity-pools create-cred-config`, and point `workloadIdentityConfig` at it:

```yaml
- route:
    from:
      uri: "kamelet:google-storage-source"
      parameters:
        bucketNameOrArn: "my-bucket"
        useWorkloadIdentityFederation: true
        workloadIdentityConfig: "file:/var/run/secrets/gcp/credential-config.json"
        impersonatedServiceAccount: "storage-reader@my-project-123.iam.gserviceaccount.com"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

With `impersonatedServiceAccount`, the Kamelet acts as that service account, which needs the Service Account Token Creator role granted to the federated identity. Without `workloadIdentityConfig`, the Application Default Credentials are used, which on GKE with Workload Identity need no setting at all.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-source.kamelet.yaml)