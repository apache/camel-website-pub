# ![ceph event based source](_images/kamelets/ceph-event-based-source.svg) Ceph Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive Ceph RGW bucket notifications from a Kafka topic, and optionally fetch the object each notification refers to.

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

## Ceph Event Based Source Kamelet Description

### How Notifications Arrive

Ceph RGW pushes bucket notifications to an endpoint configured on the topic rather than being polled. This Kamelet consumes the Kafka flavour of that.

Configuring the notification and the topic on the Ceph side is done out of band, with the S3 and topic APIs, and is not something this Kamelet does.

### Fetching the Object

Set `getObject` to true to fetch the object body from Ceph for `ObjectCreated` events, using the same S3 compatible path that `ceph-source` and `ceph-sink` use. The notification JSON is emitted unchanged otherwise.

When `getObject` is enabled, `cephUrl`, `accessKey`, `secretKey` and `zoneGroup` are required so the object can be read back from the RGW endpoint.

### Ceph Extension Fields

The fields Ceph adds beyond the S3 notification specification are surfaced as headers, so a consumer does not have to re-parse the body for them. Each has a `ce-` prefixed CloudEvents counterpart as well.

-   `ceph-event-id` from `eventId` - identifies the event, for spotting duplicates after a transport retransmit. RGW populates it as `<timestamp>.<counter>.<etag>`, unique per event. The event structure in the Ceph documentation shows it empty, but that is a placeholder in the sample rather than what RGW emits.
    
-   `ceph-opaque-data` from `opaqueData` - free-form information attached to the topic by the user.
    
-   `ceph-object-metadata` from `s3.object.metadata` - user attributes on the object, sent as `x-amz-meta-` headers. Ceph can also filter notifications on these.
    
-   `ceph-object-tags` from `s3.object.tags` - object tags. Both this and the metadata arrive as a list of key/val entries rather than a flattened string.
    

`s3.bucket.id` is not surfaced. It is an internal Ceph identifier, useful for debugging but not for routing.

### Expected Payload

The topic is expected to carry only Ceph notifications. A message without a `Records` array fails the exchange rather than being passed through, so that a foreign message is not mistaken for an event with empty Ceph headers.

A Ceph notification always carries the extension fields, empty when nothing is set, so the headers above are always populated. A payload missing them is not a Ceph event and fails the same way.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ceph-event-based-source.kamelet.yaml)