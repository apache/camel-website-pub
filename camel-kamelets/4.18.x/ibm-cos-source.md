# ![ibm cos source](_images/kamelets/ibm-cos-source.svg) IBM Cloud Object Storage Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from an IBM Cloud Object Storage Bucket.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-cos-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** IBM Cloud API Key for authentication. | string |  |  |
| **bucketName** | Bucket Name | **Required** The IBM COS Bucket name. | string |  |  |
| **endpointUrl** | Endpoint URL | **Required** IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)). | string |  | https://s3.us-south.cloud-object-storage.appdomain.cloud |
| **serviceInstanceId** | Service Instance ID | **Required** IBM COS Service Instance ID (CRN). | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the IBM COS bucket. | boolean | false |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected bucket. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Objects | Specifies to delete objects after consuming them. | boolean | true |  |
| **delimiter** | Delimiter | The delimiter to use for listing objects. | string |  |  |
| **destinationBucket** | Destination Bucket | Define the destination bucket where an object must be moved when moveAfterRead is set to true. | string |  |  |
| **destinationBucketPrefix** | Destination Bucket Prefix | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. | string |  |  |
| **destinationBucketSuffix** | Destination Bucket Suffix | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. | string |  |  |
| **includeBody** | Include Body | If true, the object body is included in the exchange. If false, only headers are set. | boolean | true |  |
| **includeFolders** | Include Folders | Include folders/directories when listing objects. | boolean | true |  |
| **location** | Location | IBM COS Location/Region (e.g., us-south, eu-gb). | string |  | us-south |
| **maxMessagesPerPoll** | Max Messages Per Poll | Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | integer | 10 |  |
| **moveAfterRead** | Move Objects After Read | Move objects from IBM COS bucket to a different bucket after they have been retrieved. | boolean | false |  |
| **prefix** | Prefix | The IBM COS bucket prefix to consider while searching. | string |  | folder/ |

## Dependencies

At runtime, the `ibm-cos-source` Kamelet relies upon the presence of the following dependencies:

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
        location: "us-south"
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
        location: "us-south"
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
        location: "us-south"
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
        location: "us-south"
        prefix: "inbox/"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This consumes only objects with keys starting with `inbox/`.

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
        location: "us-south"
        includeBody: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-cos-source.kamelet.yaml)