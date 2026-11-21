# ![ceph sink](_images/kamelets/ceph-sink.svg) Ceph Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file (object) to a bucket of a Ceph Object Gateway, the S3-compatible storage of Ceph.

Use it to store data in Ceph, such as reports, exports, images or received messages to keep as an archive. For Amazon S3, or another S3-compatible storage such as MinIO, use `aws-s3-sink` (with `overrideEndpoint`, `uriEndpointOverride` and `forcePathStyle` for a storage other than AWS).

Input: the body is the content of the file, as text, bytes or a stream. Text is turned into bytes before the upload, and the `Content-Type` header is set to `application/octet-stream`. A file is passed on as it is, and so is a stream, unless stream caching is turned off. The key (the name of the file in the bucket) comes from the optional `file` header, or the `ce-file` header; when neither is set it is `keyName`, or a generated unique name when `keyName` is not set either.

Output: the body is the content of the file, as bytes when it was text, and the `Content-Type` header is `application/octet-stream`. The `CamelAwsS3ETag` header gives the ETag of the uploaded file.

Good to know: a file with the same key is overwritten, so with `keyName` set and no `file` header each message replaces the previous one. The bucket is addressed as part of the host name (such as `my-bucket.ceph.example.com`) unless `cephUrl` uses an IP address; set `forcePathStyle` to true when the DNS of the gateway has no wildcard name for its buckets. Headers that start with `CamelAwsS3` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The S3 access key of a Ceph Object Gateway user, as shown by `radosgw-admin user info`. | string |  |  |
| **bucketName** | Bucket Name | **Required** The name of the bucket to store the files in. | string |  | my-bucket |
| **cephUrl** | Ceph Url Address | **Required** The address of the Ceph Object Gateway (RGW), as a URL with the scheme and the port. | string |  | http://ceph-rgw.example.com:7480 |
| **secretKey** | Secret Key | **Required** The S3 secret key that goes with `accessKey`. | string |  |  |
| **zoneGroup** | Bucket Zone Group | **Required** The name of the zone group of the Ceph Object Gateway, used as the region of the requests. A Ceph cluster that was not set up with several zone groups uses `default`. | string |  | default |
| **autoCreateBucket** | Autocreate Bucket | If true, the bucket is created when it does not exist yet. If false, the bucket must already exist. | boolean | false |  |
| **forcePathStyle** | Force Path Style | If true, the bucket name is put in the path of the address (`[http://ceph-rgw.example.com:7480/my-bucket/key](http://ceph-rgw.example.com:7480/my-bucket/key)`) instead of in the host name (`[http://my-bucket.ceph-rgw.example.com:7480/key](http://my-bucket.ceph-rgw.example.com:7480/key)`). The Ceph Object Gateway always accepts the path style; the host name style works only when the gateway has a wildcard DNS name for its buckets. | boolean | false |  |
| **keyName** | Key Name | The key to store the files under, with its folder if any, used when a message has no `file` or `ce-file` header. When it is not set either, each file gets a generated unique name. | string |  | reports/latest.csv |

## Dependencies

At runtime, the `ceph-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:ceph-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## CEPH Sink Kamelet Description

### Authentication methods

In this Kamelet you need to use static credentials

### Optional Headers

In the header, you can optionally set the `file` / `ce-file` property to specify the name of the file to upload.

If you do not set the property in the header, the Kamelet uses the `keyName` option for the file name, or a generated unique name when `keyName` is not set.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-sink.kamelet.yaml)