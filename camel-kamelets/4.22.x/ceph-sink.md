# ![ceph sink](_images/kamelets/ceph-sink.svg) Ceph Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload data to an Ceph Bucket managed by a Object Storage Gateway.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key. | string |  |  |
| **bucketName** | Bucket Name | **Required** The Ceph Bucket name. | string |  |  |
| **cephUrl** | Ceph Url Address | **Required** Set the Ceph Object Storage Address Url. | string |  | http://ceph-storage-address.com |
| **secretKey** | Secret Key | **Required** The secret key. | string |  |  |
| **zoneGroup** | Bucket Zone Group | **Required** The bucket zone group. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the bucket. | boolean | false |  |
| **keyName** | Key Name | The key name for saving an element in the bucket. | string |  |  |

## Dependencies

At runtime, the `ceph-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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

If you do not set the property in the header, the Kamelet uses the exchange ID for the file name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-sink.kamelet.yaml)