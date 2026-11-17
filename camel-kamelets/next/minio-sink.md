# ![minio sink](_images/kamelets/minio-sink.svg) Minio Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file (object) to a bucket in MinIO, the S3-compatible object storage.

Use it to store data in MinIO, such as reports, exports, images or received messages to keep as an archive. For Amazon S3 use `aws-s3-sink`, and for the S3 gateway of Ceph use `ceph-sink`.

Input: the body is the content of the file, as text, bytes or a stream. When `keyName` is set, every message is stored under that name. Otherwise the name of the file comes from the optional `file` header, or the `ce-file` header, and is a generated unique name when neither is set.

Output: the body is unchanged. The `CamelMinioObjectName` header holds the name the file was stored under, unless `keyName` is set.

Good to know: a file with the same name is overwritten, so with `keyName` set each message replaces the previous one. When `keyName` is set, the `file` and `ce-file` headers are ignored.

## Configuration Options

The following table summarizes the configuration options available for the `minio-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key to log in to MinIO with, such as the access key of a key pair created in the MinIO Console, or the name of a MinIO user. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to store the files in. | string |  | my-bucket |
| **endpoint** | Endpoint | **Required** The address of the MinIO server, as a URL with the port, such as `[http://localhost:9000](http://localhost:9000)`. Use `https://` when the server has TLS. | string |  | http://localhost:9000 |
| **secretKey** | Secret Key | **Required** The secret key that goes with `accessKey`, or the password of the MinIO user. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. If false, the bucket must already exist. | boolean | false |  |
| **keyName** | Key Name | The name to store every file under, with its folder if any. When it is not set, the name comes from the `file` or `ce-file` header of each message, or is generated. | string |  | reports/latest.csv |

## Dependencies

At runtime, the `minio-sink` Kamelet relies upon the presence of the following dependencies:

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

When the `keyName` option is set, every message is stored under that name, and the `file` and `ce-file` headers are ignored. Otherwise the object name comes from the `file` header, or the `ce-file` header, and is a generated unique name when neither is set.

### Deployment Flexibility

Supports various deployment scenarios including on-premises, cloud, and hybrid environments with configurable endpoint URLs.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-sink.kamelet.yaml)