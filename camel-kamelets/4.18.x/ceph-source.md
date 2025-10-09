# ![ceph source](_images/kamelets/ceph-source.svg) Ceph Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an Ceph Bucket, managed by a Object Storage Gateway.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key. | string |  |  |
| **bucketName** | Bucket Name | **Required** The Ceph Bucket name. | string |  |  |
| **cephUrl** | Ceph Url Address | **Required** Set the Ceph Object Storage Address Url. | string |  | http://ceph-storage-address.com |
| **secretKey** | Secret Key | **Required** The secret key. | string |  |  |
| **zoneGroup** | Bucket Zone Group | **Required** The bucket zone group. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the bucket. | boolean | false |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected bucket. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Objects | Specifies to delete objects after consuming them. | boolean | true |  |
| **ignoreBody** | Ignore Body | If true, the Object body is ignored. Setting this to true overrides any behavior defined by the `includeBody` option. If false, the object is put in the body. | boolean | false |  |
| **includeBody** | Include Body | If true, the exchange is consumed and put into the body and closed. If false, the Object stream is put raw into the body and the headers are set with the object metadata. | boolean | true |  |
| **prefix** | Prefix | The bucket prefix to consider while searching. | string |  | folder/ |

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