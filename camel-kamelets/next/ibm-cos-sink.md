# ![ibm cos sink](_images/kamelets/ibm-cos-sink.svg) IBM Cloud Object Storage Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Upload data to an IBM Cloud Object Storage Bucket.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-cos-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** IBM Cloud API Key for authentication. | string |  |  |
| **bucketName** | Bucket Name | **Required** The IBM COS Bucket name. | string |  |  |
| **endpointUrl** | Endpoint URL | **Required** IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)). | string |  | https://s3.us-south.cloud-object-storage.appdomain.cloud |
| **serviceInstanceId** | Service Instance ID | **Required** IBM COS Service Instance ID (CRN). | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the IBM COS bucket. | boolean | false |  |
| **keyName** | Key Name | The key name for saving an element in the bucket. | string |  |  |
| **location** | Location | IBM COS Location/Region (e.g., us-south, eu-gb). | string |  | us-south |
| **multiPartUpload** | Multi-Part Upload | Use multi-part upload for large files. | boolean | false |  |
| **partSize** | Part Size | Part size for multi-part uploads (default 25MB). | integer | 26214400 |  |
| **storageClass** | Storage Class | The storage class to use when storing objects (e.g., STANDARD, VAULT, COLD, FLEX). | string |  |  |

## Dependencies

At runtime, the `ibm-cos-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
              location: "us-south"
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
              location: "us-south"
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
              location: "us-south"
              keyName: "data/myfile.txt"
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
              location: "us-south"
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
              location: "us-south"
              storageClass: "STANDARD"
```

Available storage classes include STANDARD, VAULT, COLD, and FLEX.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-sink.kamelet.yaml)