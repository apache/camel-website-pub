# ![ibm cos source](_images/kamelets/ibm-cos-source.svg) IBM Cloud Object Storage Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Reads the files (objects) in a bucket of IBM Cloud Object Storage, one message per file, and by default deletes each file once it has been read.

Use it to process files that another system drops into a bucket, such as uploaded documents, exported reports or log files. To upload files to a bucket, use `ibm-cos-sink`.

Output: the body is the content of the file, as a stream. The headers give the bucket name (`CamelIBMCOSBucketName`), the key, that is the path of the file in the bucket (`CamelIBMCOSKey`), the content type, the size and the ETag of the file.

Good to know: files are deleted from the bucket after they are read, unless `deleteAfterRead` is set to false; then the same files are read again on every poll. `moveAfterRead` moves them to another bucket instead. To read one file only, set `fileName`. A file whose processing fails is kept, and read again on the next poll. It logs in with an IBM Cloud API key.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-cos-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** An IBM Cloud API key that may read (and delete) the files of the bucket. Create it in the IBM Cloud console under Manage > Access (IAM) > API keys, or use the `apikey` of a service credential of the Cloud Object Storage instance. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to read the files from. | string |  | my-bucket |
| **endpointUrl** | Endpoint URL | **Required** The address of Cloud Object Storage for the region of the bucket, starting with `https://`, as listed under Endpoints in the Cloud Object Storage instance. | string |  | https://s3.us-south.cloud-object-storage.appdomain.cloud |
| **serviceInstanceId** | Service Instance ID | **Required** The CRN (Cloud Resource Name) of the Cloud Object Storage instance, shown in the details of the instance in the IBM Cloud console. It starts with `crn:v1:bluemix:public:cloud-object-storage:`. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. | boolean | false |  |
| **delay** | Delay | How long to wait between two polls of the bucket, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **deleteAfterRead** | Auto-delete Objects | If true, each file is deleted from the bucket after it has been read. Set it to false to keep the files; they are then read again on every poll. | boolean | true |  |
| **delimiter** | Delimiter | The character that separates folders in the keys, usually `/`. When it is set, only the files directly in the folder of `prefix` are read, not those in its subfolders. | string |  | / |
| **destinationBucket** | Destination Bucket | The bucket to move the files to. Only used when `moveAfterRead` is true. | string |  | my-archive-bucket |
| **destinationBucketPrefix** | Destination Bucket Prefix | Text put before the name of each moved file in `destinationBucket`, such as a folder followed by `/`. Only used when `moveAfterRead` is true. | string |  | processed/ |
| **destinationBucketSuffix** | Destination Bucket Suffix | Text put after the name of each moved file in `destinationBucket`, such as `.done`. Only used when `moveAfterRead` is true. | string |  | .done |
| **fileName** | File Name | The key of one file to read, such as `inbox/orders.csv`, instead of all the files of the bucket; `prefix` and `delimiter` are then not used. With `deleteAfterRead` true, the default, the file is read once and deleted, and each later poll logs a warning that the key does not exist, until a file with that key is uploaded again. With `deleteAfterRead` false, the same file is read again on every poll. | string |  | inbox/orders.csv |
| **includeBody** | Include Body | If true, the body is the content of the file. If false, there is no body and only the headers describe the file. | boolean | true |  |
| **includeFolders** | Include Folders | If true, folder markers (empty objects whose key ends with `/`) are read as messages too. Set it to false to skip them. | boolean | true |  |
| **maxMessagesPerPoll** | Max Messages Per Poll | The most files to read at each poll. Use 0 or a negative number for no limit. | integer | 10 |  |
| **moveAfterRead** | Move Objects After Read | If true, each file is moved to `destinationBucket` after it has been read, that is copied there and deleted from this bucket, whatever `deleteAfterRead` says. | boolean | false |  |
| **prefix** | Prefix | Only read the files whose key starts with this text, such as a folder followed by `/`. | string |  | inbox/ |
| **region** | Region | The region of the bucket, such as `us-south` or `eu-gb`. It is information only, shown with the services the integration calls; the region used is the one of `endpointUrl`. | string |  | us-south |

## Dependencies

At runtime, the `ibm-cos-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:ibm-cos-source"
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

## IBM Cloud Object Storage Source Kamelet Description

### Authentication methods

This Kamelet requires authentication with IBM Cloud using an API Key and Service Instance ID (CRN - Cloud Resource Name).

To obtain these credentials:

-   API Key - Create an IBM Cloud API Key through the IBM Cloud console (Manage > Access (IAM) > API keys).
    
-   Service Instance ID - This is the Cloud Resource Name (CRN) of your IBM COS instance, found in your IBM COS service instance details.
    
-   Endpoint URL - The IBM COS endpoint URL for your region (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)).
    

For more information, see the [IBM Cloud Object Storage documentation](https://cloud.ibm.com/docs/cloud-object-storage)

### Usage examples

You can consume objects from an IBM COS bucket and delete them after processing:

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        region: "us-south"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The `deleteAfterRead` property is true by default, ensuring each object is consumed only once.

#### Consuming objects without deletion

To consume objects without deleting them, set `deleteAfterRead` to false:

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        region: "us-south"
        deleteAfterRead: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

#### Moving objects after reading

Instead of deleting objects, you can move them to another bucket:

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        region: "us-south"
        deleteAfterRead: false
        moveAfterRead: true
        destinationBucket: "archive-bucket"
        destinationBucketPrefix: "processed/"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

#### Consuming with a prefix filter

You can filter objects using a prefix:

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        region: "us-south"
        prefix: "inbox/"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This consumes only objects with keys starting with `inbox/`.

#### Reading one file

To read one file of the bucket instead of all of them, set `fileName` to its key. With `deleteAfterRead` false, the same file is read again on every poll; with the default `deleteAfterRead`, it is read once and deleted, and each later poll logs a warning that the key does not exist, until a file with that key is uploaded again.

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        fileName: "config/prices.csv"
        deleteAfterRead: false
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

#### Consuming only metadata

To consume only object metadata without the body, set `includeBody` to false:

```yaml
- route:
    from:
      uri: "kamelet:ibm-cos-source"
      parameters:
        bucketName: "my-bucket"
        apiKey: "{{ibm.api.key}}"
        serviceInstanceId: "{{ibm.service.instance.id}}"
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        region: "us-south"
        includeBody: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-source.kamelet.yaml)