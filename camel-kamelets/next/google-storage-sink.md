# ![google storage sink](_images/kamelets/google-storage-sink.svg) Google Storage Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file (object) to a Google Cloud Storage bucket.

Use it to store data for later use or for other systems, such as exported reports, archived events or files received from another system. To read the files of a bucket, use `google-storage-source`.

Input: the body is the content of the file, as text, bytes, a stream or a file. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The optional `file` header (or `ce-file`) is the name of the file in the bucket, with its folders, such as `reports/2024-06-01.csv`; without it, the file gets a generated unique name.

Output: when it is used inside a route, the body afterwards describes the uploaded file (its bucket, name, size and generation), not its content, and the `CamelGoogleCloudStorageObjectName` header holds the name of the file.

Good to know: a file with the same name is overwritten. The bucket must exist, unless `autoCreateBucket` is true. Without `serviceAccountKey`, it logs in with the Application Default Credentials of the environment where it runs.

## Configuration Options

The following table summarizes the configuration options available for the `google-storage-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name | **Required** The name of the bucket to upload the files to, without `gs://`. | string |  | my-bucket |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. The service account then needs the permission to create buckets in the project. | boolean | false |  |
| **serviceAccountKey** | Service Account Key | The JSON key of a service account that may write to the bucket, encoded in Base64: create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys, then encode the downloaded file, for example with `base64 -w0 key.json`. When it is not set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | binary |  |  |

## Dependencies

At runtime, the `google-storage-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:google-storage-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Storage Sink Kamelet Description

### Authentication

This Kamelet supports Google Cloud service account authentication. The service account key is optional - if not provided, the Kamelet will use default credentials.

### Required Configuration

-   **Bucket Name**: The name of the Google Cloud Storage bucket
    

### Optional Configuration

-   **Service Account Key**: The JSON key file of a service account, encoded in Base64
    
-   **Auto Create Bucket**: Automatically creates the bucket if it doesn’t exist (defaults to false)
    

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the object to upload.

If you do not set the property in the header, the Kamelet uses a generated unique name for the object. An object with the same name is overwritten.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-sink.kamelet.yaml)