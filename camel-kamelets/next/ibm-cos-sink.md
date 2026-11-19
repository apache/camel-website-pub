# ![ibm cos sink](_images/kamelets/ibm-cos-sink.svg) IBM Cloud Object Storage Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Uploads each message as a file (object) to a bucket in IBM Cloud Object Storage.

Use it to store data for later use or for other systems, such as exported reports, archived events or files received from another system. To read the files of a bucket, use `ibm-cos-source`.

Input: the body is the content of the file, as text, bytes, a stream or a file. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The name of the file (its key) is `keyName` when it is set; otherwise the optional `file` header (or `ce-file`), with its folders, such as `reports/2024-06-01.csv`; otherwise a generated unique name.

Output: the message is unchanged, with the ETag of the uploaded file in the `CamelIBMCOSETag` header.

Good to know: a file with the same name is overwritten. With `deleteAfterWrite` set to true, a body that is a local file, such as the file of `file-watch-source`, is deleted from the local disk once it has been uploaded. The bucket must exist, unless `autoCreateBucket` is true. It logs in with an IBM Cloud API key. Headers that start with `CamelIBMCOS`, except `CamelIBMCOSKey`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-cos-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** An IBM Cloud API key that may write to the bucket. Create it in the IBM Cloud console under Manage > Access (IAM) > API keys, or use the `apikey` of a service credential of the Cloud Object Storage instance. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to upload the files to. | string |  | my-bucket |
| **endpointUrl** | Endpoint URL | **Required** The address of Cloud Object Storage for the region of the bucket, starting with `https://`, as listed under Endpoints in the Cloud Object Storage instance. | string |  | https://s3.us-south.cloud-object-storage.appdomain.cloud |
| **serviceInstanceId** | Service Instance ID | **Required** The CRN (Cloud Resource Name) of the Cloud Object Storage instance, shown in the details of the instance in the IBM Cloud console. It starts with `crn:v1:bluemix:public:cloud-object-storage:`. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. | boolean | false |  |
| **deleteAfterWrite** | Delete Local File | If true and the body is a local file, such as the file of `file-watch-source`, the file is deleted from the local disk once it has been uploaded. A body that is not a file, such as text or bytes, is uploaded and nothing is deleted. A reader that moves the file itself after the upload, such as the Camel file component by default, then logs a warning that it cannot move the file. When it is not set, it is false. | boolean |  |  |
| **keyName** | Key Name | The name of the file in the bucket, the same for every message, so each message overwrites the previous file. When it is not set, the name comes from the `file` or `ce-file` header, or is generated. A `CamelIBMCOSKey` header on the message, as `ibm-cos-source` sets, is used instead of it. | string |  | reports/latest.csv |
| **multiPartUpload** | Multi-Part Upload | If true, a file larger than `partSize` is uploaded in several parts, which suits large files. | boolean | false |  |
| **partSize** | Part Size | The size of each part of a multi-part upload, in bytes. For example, 26214400 is 25 MB. Only used when `multiPartUpload` is true. | integer | 26214400 |  |
| **region** | Region | The region of the bucket, such as `us-south` or `eu-gb`. It is information only, shown with the services the integration calls; the region used is the one of `endpointUrl`. | string |  | us-south |
| **storageClass** | Storage Class | The storage class to store the files with, such as `STANDARD`, `VAULT`, `COLD` or `FLEX`. | string |  | STANDARD |

## Dependencies

At runtime, the `ibm-cos-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ibm-cos
    
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
            uri: "kamelet:ibm-cos-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## IBM Cloud Object Storage Sink Kamelet Description

### Authentication methods

This Kamelet requires authentication with IBM Cloud using an API Key and Service Instance ID (CRN - Cloud Resource Name).

To obtain these credentials:

-   API Key - Create an IBM Cloud API Key through the IBM Cloud console (Manage > Access (IAM) > API keys).
    
-   Service Instance ID - This is the Cloud Resource Name (CRN) of your IBM COS instance, found in your IBM COS service instance details.
    
-   Endpoint URL - The IBM COS endpoint URL for your region (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)).
    

For more information, see the [IBM Cloud Object Storage documentation](https://cloud.ibm.com/docs/cloud-object-storage)

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the object to upload.

If you do not set the property in the header, the Kamelet uses the exchange ID for the object key name.

### Usage examples

Upload data to an IBM COS bucket:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      steps:
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              region: "us-south"
```

#### Auto-creating buckets

The Kamelet can automatically create the bucket if it doesn’t exist:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      steps:
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              region: "us-south"
              autoCreateBucket: true
```

#### Specifying a custom key name

You can specify a fixed key name for all uploaded objects:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      steps:
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              region: "us-south"
              keyName: "data/myfile.txt"
```

#### Deleting the local file after the upload

When the body is a local file, such as the file of `file-watch-source`, `deleteAfterWrite` deletes it from the local disk once it has been uploaded. A body that is not a file is uploaded, and nothing is deleted. This example uploads each new file of `/var/outbox` under its own name, and then deletes it.

```yaml
- route:
    from:
      uri: "kamelet:file-watch-source"
      parameters:
        filePath: "/var/outbox"
        events: "CREATE"
      steps:
        - to:
            uri: "kamelet:insert-header-action"
            parameters:
              name: "file"
              value: "$\{header.CamelFileName}"
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              deleteAfterWrite: true
```

#### Using multi-part upload for large files

For large files, you can enable multi-part upload:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      steps:
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              region: "us-south"
              multiPartUpload: true
              partSize: 52428800
```

The `partSize` is specified in bytes (default is 25MB = 26214400 bytes).

#### Specifying storage class

You can specify different storage classes for cost optimization:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      steps:
        - to:
            uri: "kamelet:ibm-cos-sink"
            parameters:
              bucketName: "my-bucket"
              apiKey: "{{ibm.api.key}}"
              serviceInstanceId: "{{ibm.service.instance.id}}"
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
              region: "us-south"
              storageClass: "STANDARD"
```

Available storage classes include STANDARD, VAULT, COLD, and FLEX.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-sink.kamelet.yaml)