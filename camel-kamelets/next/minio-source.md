# ![minio source](_images/kamelets/minio-source.svg) Minio Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files (objects) in a MinIO bucket, one message per file, and by default deletes each file once it has been read.

Use it to process files that another system drops into a MinIO bucket, such as uploaded documents, exported reports or log files. For Amazon S3 use `aws-s3-source`, and for the S3 gateway of Ceph use `ceph-source`.

Output: the body is the content of the file, as bytes. The headers give the bucket name, the name of the file (`CamelMinioObjectName`), and its content type, size, ETag and last modified date.

Good to know: files are deleted from the bucket after they are read, unless `deleteAfterRead` is set to false; then the same files are read again on every poll, about twice a second. Only the files at the top of the bucket are read: a file in a folder, such as `reports/january.csv`, is not.

## Configuration Options

The following table summarizes the configuration options available for the `minio-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key to log in to MinIO with, such as the access key of a key pair created in the MinIO Console, or the name of a MinIO user. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to read the files from. | string |  | my-bucket |
| **endpoint** | Endpoint | **Required** The address of the MinIO server, as a URL with the port, such as `[http://localhost:9000](http://localhost:9000)`. Use `https://` when the server has TLS. | string |  | http://localhost:9000 |
| **secretKey** | Secret Key | **Required** The secret key that goes with `accessKey`, or the password of the MinIO user. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. If false, every poll fails while the bucket does not exist. | boolean | false |  |
| **deleteAfterRead** | Auto-delete Objects | If true, each file is deleted from the bucket after it has been read. Set it to false to keep the files; they are then read again on every poll. | boolean | true |  |

## Dependencies

At runtime, the `minio-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:minio-source"
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

## Minio Source Kamelet Description

### Authentication methods

This Kamelet connects to Minio using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet reads the files of a MinIO bucket, and produces one message per file, with the content of the file as bytes. It reads only the files at the top of the bucket, not the files in folders, and by default deletes each file after it has been read.

### Configuration

The Kamelet requires connection parameters specific to Minio:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: minio-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: minio-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/minio-source.kamelet.yaml)