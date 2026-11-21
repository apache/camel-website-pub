# ![ceph source](_images/kamelets/ceph-source.svg) Ceph Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files (objects) in a bucket of a Ceph Object Gateway, one message per file, and by default deletes each file once it has been read.

Use it to process files that another system drops into a Ceph bucket, such as uploaded documents, exported reports or log files. To react to the bucket notifications of Ceph instead of reading the bucket over and over, use `ceph-event-based-source`.

Output: the body is the content of the file, as bytes, and the `Content-Type` header is `application/octet-stream`. The headers give the bucket name, the key (the path of the file in the bucket, `CamelAwsS3Key`), the content type and the ETag of the file.

Good to know: files are deleted from the bucket after they are read, unless `deleteAfterRead` is set to false; then the same files are read again on every poll. Files in folders are read too. The bucket is addressed as part of the host name (such as `my-bucket.ceph.example.com`) unless `cephUrl` uses an IP address; set `forcePathStyle` to true when the DNS of the gateway has no wildcard name for its buckets.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The S3 access key of a Ceph Object Gateway user, as shown by `radosgw-admin user info`. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to read the files from. | string |  | my-bucket |
| **cephUrl** | Ceph Url Address | **Required** The address of the Ceph Object Gateway (RGW), as a URL with the scheme and the port. | string |  | http://ceph-rgw.example.com:7480 |
| **secretKey** | Secret Key | **Required** The S3 secret key that goes with `accessKey`. | string |  |  |
| **zoneGroup** | Bucket Zone Group | **Required** The name of the zone group of the Ceph Object Gateway, used as the region of the requests. A Ceph cluster that was not set up with several zone groups uses `default`. | string |  | default |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. If false, every poll fails while the bucket does not exist. | boolean | false |  |
| **delay** | Delay | How long to wait between two polls of the bucket, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Objects | If true, each file is deleted from the bucket after it has been read. Set it to false to keep the files; they are then read again on every poll. | boolean | true |  |
| **forcePathStyle** | Force Path Style | If true, the bucket name is put in the path of the address (`[http://ceph-rgw.example.com:7480/my-bucket/key](http://ceph-rgw.example.com:7480/my-bucket/key)`) instead of in the host name (`[http://my-bucket.ceph-rgw.example.com:7480/key](http://my-bucket.ceph-rgw.example.com:7480/key)`). The Ceph Object Gateway always accepts the path style; the host name style works only when the gateway has a wildcard DNS name for its buckets. | boolean | false |  |
| **ignoreBody** | Ignore Body | If true, the content of the file is not read, and the body is empty; only the headers describe the file. It takes precedence over `includeBody`. | boolean | false |  |
| **includeBody** | Include Body | If true, the body is the content of the file, as bytes. If false, the body is a stream of the content, which suits large files. | boolean | true |  |
| **prefix** | Prefix | Read only the files whose key starts with this text, such as a folder name followed by `/`. When it is not set, all the files of the bucket are read. | string |  | folder/ |

## Dependencies

At runtime, the `ceph-source` Kamelet relies upon the presence of the following dependencies:

-   camel:aws2-s3
    
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
      uri: "kamelet:ceph-source"
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

## CEPH Source Kamelet Description

### Authentication methods

In this Kamelet you need to use static credentials

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-source.kamelet.yaml)