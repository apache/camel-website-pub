# ![minio source](_images/kamelets/minio-source.svg) Minio Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from MinIO.

## Configuration Options

The following table summarizes the configuration options available for the `minio-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The access key obtained from MinIO. | string |  |  |
| **bucketName** | Bucket Name | **Required** The MinIO Bucket name. | string |  |  |
| **endpoint** | Endpoint | **Required** The MinIO Endpoint. You can specify an URL, domain name, IPv4 address, or IPv6 address. | string |  | http://localhost:9000 |
| **secretKey** | Secret Key | **Required** The secret key obtained from MinIO. | string |  |  |
| **autoCreateBucket** | Autocreate Bucket | Specifies to automatically create the MinIO bucket. | boolean | false |  |
| **deleteAfterRead** | Auto-delete Objects | Delete objects after consuming them. | boolean | true |  |

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

The Kamelet consumes data from Minio and produces the data in JSON format.

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