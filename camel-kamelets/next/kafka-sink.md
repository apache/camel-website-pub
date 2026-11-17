# ![kafka sink](_images/kamelets/kafka-sink.svg) Kafka Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as a record to a topic in Apache Kafka, or in a Kafka-compatible service such as Amazon MSK, Confluent Cloud or Redpanda.

Use it to publish events or data for other applications to read, such as orders, sensor readings or changes from a database. When the records must follow a schema kept in a schema registry, use one of the `kafka-**-registry-**` sinks instead.

Input: the body becomes the value of the record, as text. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The optional `key` header (or `kafka-key`, `ce-key`, `ce-kafkakey`) becomes the key of the record, and the optional `partition-key` header (or `ce-partitionkey`) is the number of the partition to write to. The other headers of the message, except the Camel ones, are sent as record headers.

Output: the message is unchanged.

Good to know: with the default `saslAuthType` of `NONE`, it connects with no login and no TLS, as a local Kafka expects. A managed Kafka service needs one of the other types.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **topic** | Topic Name | **Required** The name of the topic to write the records to. | string |  | orders |
| **oauthClientId** | OAuth Client ID | OAuth client ID. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | OAuth client secret. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthScope** | OAuth Scope | OAuth scope. Optional when saslAuthType is OAUTH. | string |  |  |
| **oauthTokenEndpointUri** | OAuth Token Endpoint | OAuth token endpoint URI. Required when saslAuthType is OAUTH. | string |  |  |
| **saslAuthType** | Authentication Type | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string | NONE |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. Used for mTLS authentication. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The password for the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | The password for the trust store file. | string |  |  |

## Dependencies

At runtime, the `kafka-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
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
            uri: "kamelet:kafka-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Sink Kamelet Description

### Authentication

The `saslAuthType` option chooses how the Kamelet logs in to Kafka. The options that each type needs are listed below; leave the others empty.

 
| `saslAuthType` | Options to set |
| --- | --- |
| `NONE` (default) | None. No login and no TLS, as a local Kafka expects. |
| `PLAIN`, `SCRAM_SHA_256`, `SCRAM_SHA_512` | `saslUsername` and `saslPassword`. |
| `SSL` | `sslTruststoreLocation` and `sslTruststorePassword`; for mutual TLS also `sslKeystoreLocation`, `sslKeystorePassword` and `sslKeyPassword`. |
| `OAUTH` | `oauthClientId`, `oauthClientSecret` and `oauthTokenEndpointUri`; `oauthScope` when the provider asks for one. |
| `AWS_MSK_IAM` | None in the Kamelet: the AWS credentials are taken from the environment the integration runs in. |
| `KERBEROS` | None in the Kamelet: Kerberos is configured in the environment the integration runs in. |

### Usage example

The route below sends a JSON order every ten seconds to the `orders` topic, with the order number as the record key.

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: '{"id": 42, "item": "book"}'
        contentType: application/json
      steps:
        - setHeader:
            name: key
            constant: "42"
        - to:
            uri: "kamelet:kafka-sink"
            parameters:
              bootstrapServers: "localhost:9092"
              topic: orders
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml)