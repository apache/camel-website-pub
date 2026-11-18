# ![ceph event based source](_images/kamelets/ceph-event-based-source.svg) Ceph Event Based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the bucket notifications that a Ceph Object Gateway sends to a Kafka topic, one message per event, such as a file added to or deleted from a bucket.

Use it to react as soon as a file is uploaded to or removed from a Ceph bucket, without reading the bucket over and over. Set `getObject` to true to receive the content of each new file. To read and remove the files of a bucket instead, use `ceph-source`.

Output: the body is the notification as JSON text, unchanged: a `Records` array that gives the event name (such as `ObjectCreated:Put`), the bucket name and the key of the file. The headers `ceph-event-id`, `ceph-opaque-data`, `ceph-object-metadata` and `ceph-object-tags` give the fields Ceph adds to the event; metadata and tags are a List of entries with a `key` and a `val`. Each header is also set with a `ce-` name, such as `ce-cepheventid`. With `getObject` true, the body of an `ObjectCreated` event is the content of the file instead, as a stream, with its content type in `CamelAwsS3ContentType`, and the other events come out as parsed JSON (a Jackson `JsonNode`), not as text.

Good to know: the notification and its Kafka topic are set up on the Ceph side; this Kamelet only reads the topic. A record that is not a Ceph notification (without a `Records` array) fails. `saslAuthType` has no default and must be set; `NONE` connects to Kafka with no login and no TLS. Without `consumerGroup`, each start uses a new group, so with the default `autoOffsetReset` of `latest` the events sent while it was stopped are not read.

## Configuration Options

The following table summarizes the configuration options available for the `ceph-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. | string |  | broker1:9092,broker2:9092 |
| **saslAuthType** | Authentication Type | **Required** How to log in to Kafka. It has no default and must be set. `NONE` connects with no login and no TLS, as a local Kafka expects; `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` log in with `saslUsername` and `saslPassword`. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string |  |  |
| **topic** | Topic Name | **Required** The Kafka topic that the Ceph Object Gateway sends the bucket notifications to, as set in the push endpoint of the Ceph topic. | string |  | ceph-bucket-notifications |
| **accessKey** | Access Key | The S3 access key of a Ceph Object Gateway user that can read the bucket. Required when `getObject` is true. | string |  |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has not read the topic before. `latest` reads only the events sent from now on, `earliest` reads the topic from its start, and `none` fails. Enum values: \* latest \* earliest \* none | string | latest |  |
| **cephUrl** | Ceph URL | The address of the Ceph Object Gateway (RGW) to read the files from, as a URL with the scheme and the port. Required when `getObject` is true. | string |  | http://ceph-rgw:8080 |
| **consumerGroup** | Consumer Group | The name of the Kafka consumer group. Kafka remembers how far the group has read, so a restart continues where it stopped. When it is not set, a new group is used at each start. | string |  | my-group-id |
| **getObject** | Get Object | If true, for each `ObjectCreated` event the file is read from Ceph and becomes the body, instead of the notification. It needs `cephUrl`, `accessKey`, `secretKey` and `zoneGroup`. | boolean | false |  |
| **saslPassword** | Password | The password of `saslUsername`. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **saslUsername** | Username | The user to log in to Kafka as. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **secretKey** | Secret Key | The S3 secret key that goes with `accessKey`. Required when `getObject` is true. | string |  |  |
| **zoneGroup** | Ceph Zone Group | The name of the zone group of the Ceph Object Gateway, used as the region of the requests. Required when `getObject` is true. | string |  | zonegroup1 |

## Dependencies

At runtime, the `ceph-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:jsonpath
    
-   camel:jackson3
    
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

Set `getObject` to true to fetch the object body from Ceph for `ObjectCreated` events, using the same S3 compatible path that `ceph-source` and `ceph-sink` use. With `getObject` left false, the notification JSON is emitted unchanged, as text. With `getObject` true, the other events are emitted as parsed JSON (a Jackson `JsonNode`) rather than as text.

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