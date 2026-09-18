# ![google storage sink](_images/kamelets/google-storage-sink.svg) Google Storage Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload objects to Google Cloud Storage.

## Configuration Options

The following table summarizes the configuration options available for the `google-storage-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucketNameOrArn** | Bucket Name Or ARN | **Required** The Google Cloud Storage bucket name or Bucket Amazon Resource Name (ARN). | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the Google Cloud Storage bucket. | boolean | false |  |
| **serviceAccountKey** | Service Account Key | The service account key to use as credentials for Google Cloud Storage access. You must encode this value in base64. | binary |  |  |

## Dependencies

At runtime, the `google-storage-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:google-storage
    
-   camel:jackson
    

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

-   **Bucket Name or ARN**: The Google Cloud Storage bucket name or Amazon Resource Name
    

### Optional Configuration

-   **Service Account Key**: Base64-encoded service account credentials
    
-   **Auto Create Bucket**: Automatically creates the bucket if it doesn’t exist (defaults to false)
    

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the object to upload.

If you do not set the property in the header, the Kamelet uses the exchange ID for the object name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-storage-sink.kamelet.yaml)