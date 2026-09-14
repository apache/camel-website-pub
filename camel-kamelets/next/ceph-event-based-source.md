Kamelet Catalog

# ![ceph event based source](_images/kamelets/ceph-event-based-source.svg) Ceph Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive Ceph RGW bucket notifications from a Kafka topic, and optionally fetch the object each notification refers to.

Ceph pushes bucket notifications to an endpoint configured on the topic; this Kamelet consumes the Kafka flavour of that. Configuring the notification and the topic on the Ceph side is done out of band with the S3 and topic APIs, not by this Kamelet.

Set getObject to true to fetch the object body from Ceph for ObjectCreated events. The notification JSON is emitted unchanged otherwise.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** A comma separated list of Kafka brokers to connect to. | string |  |  |
| **topic** | Topic Name | **Required** The Kafka topic Ceph pushes the bucket notifications to. | string |  | ceph-bucket-notifications |
| **accessKey** | Access Key | The access key to read objects from Ceph. Required when getObject is true. | string |  |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be latest, earliest or none. Enum values: \* latest \* earliest \* none | string | latest |  |
| **cephUrl** | Ceph URL | The URL of the Ceph RGW endpoint to fetch objects from. Required when getObject is true. | string |  | http://ceph-rgw:8080 |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers this source belongs to. | string |  | my-group-id |
| **getObject** | Get Object | Fetch the object body from Ceph for ObjectCreated events, instead of emitting only the notification. | boolean | false |  |
| **saslAuthType** | Authentication Type | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string | NONE |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **secretKey** | Secret Key | The secret key to read objects from Ceph. Required when getObject is true. | string |  |  |
| **zoneGroup** | Ceph Zone Group | The zone group the bucket belongs to, passed to the S3 client as its region. | string |  | zonegroup1 |

## Dependencies

At runtime, the `ceph-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:core
    
-   camel:jsonpath
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:aws2-s3
    

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
      uri: "kamelet:ceph-event-based-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-event-based-source.kamelet.yaml)