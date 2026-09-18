# ![minio sink](_images/kamelets/minio-sink.svg) Minio Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload data to MinIO.

## Configuration Options

The following table summarizes the configuration options available for the `minio-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key obtained from MinIO. | string |  |  |
| **bucketName** | Bucket Name | **Required** The Minio Bucket name. | string |  |  |
| **endpoint** | Endpoint | **Required** The MinIO Endpoint. You can specify an URL, domain name, IPv4 address, or IPv6 address. | string |  | http://localhost:9000 |
| **secretKey** | Secret Key | **Required** The secret key obtained from MinIO. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specify to automatically create the MinIO bucket. | boolean | false |  |
| **keyName** | Key Name | The key name for saving an element in the bucket. | string |  |  |

## Dependencies

At runtime, the `minio-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:minio
    
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
            uri: "kamelet:minio-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Minio Sink Kamelet Description

### Object Storage Integration

This Kamelet integrates with MinIO, an open-source object storage system that is compatible with Amazon S3 APIs. MinIO is ideal for cloud-native applications and data lake architectures.

### S3-Compatible API

MinIO provides S3-compatible APIs, making it easy to migrate from Amazon S3 or integrate with S3-compatible applications and tools.

### Authentication

Uses access key and secret key authentication for secure access to MinIO instances. These credentials should be properly managed and secured according to security best practices.

### Bucket Management

The Kamelet can optionally auto-create buckets if they don’t exist, providing flexibility for dynamic storage scenarios. Objects are stored with configurable key names.

### Object Naming

Object names can be specified through configuration or derived from message headers (`file` or `ce-file`). If no name is provided, the exchange ID is used as the object name.

### Deployment Flexibility

Supports various deployment scenarios including on-premises, cloud, and hybrid environments with configurable endpoint URLs.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-sink.kamelet.yaml)