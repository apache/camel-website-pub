# Kafka Share

**Since Camel 4.23**

**Only consumer is supported**

The Kafka Share component consumes the records of [Apache Kafka](http://kafka.apache.org/) topics through a [share group](https://cwiki.apache.org/confluence/display/KAFKA/KIP-932%3A+Queues+for+Kafka) (KIP-932, Queues for Kafka).

The consumers of a share group work through the records of a topic like a queue:

-   several consumers read the same partition, so the number of consumers is not limited by the number of partitions;
    
-   every record is acknowledged on its own: a failing record does not hold up the records after it;
    
-   the broker delivers a released record again, possibly to another consumer, and counts the deliveries of each record.
    

A share group has no offsets to commit or seek, no ordering guarantee, no transactions and no topic patterns. Use the [Kafka](kafka-component.md) component to produce records, and to consume them in order with a consumer group.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kafka-share</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

kafka-share:topic\[?options\]

The topic can be a comma-separated list of topics. The `groupId` option, the name of the share group, is required.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Kafka Share component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Sets additional properties for either kafka consumer or kafka producer in case they can’t be set directly on the camel configurations (e.g.: new Kafka properties that are not reflected yet in Camel configurations), the properties have to be prefixed with additionalProperties., e.g.: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. If the properties are set in the application.properties file, they must be prefixed with camel.component.kafka.additional-properties (camel.component.kafka-share.additional-properties for the Kafka Share component) followed by the property name enclosed in square brackets, for example the delivery.timeout.ms property in square brackets. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **brokers** (common) | URL of the Kafka brokers to use. The format is host1:port1,host2:port2, and the list can be a subset of brokers or a VIP pointing to a subset of brokers. This option is known as bootstrap.servers in the Kafka documentation. |  | String |
| **clientId** (common) | The client id is a user-specified string sent in each request to help trace calls. It should logically identify the application making the request. |  | String |
| **configuration** (consumer) | Allows to pre-configure the Kafka share component with common options that the endpoints will reuse. |  | KafkaShareConfiguration |
| **connectionMaxIdleMs** (common) | Close idle connections after the number of milliseconds specified by this config. | 540000 | Integer |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **metadataMaxAgeMs** (common) | The period of time in milliseconds after which we force a refresh of metadata even if we haven’t seen any partition leadership changes to proactively discover any new brokers or partitions. | 300000 | Integer |
| **metricReporters** (common) | A list of classes to use as metrics reporters. Implementing the MetricReporter interface allows plugging in classes that will be notified of new metric creation. The JmxReporter is always included to register JMX statistics. |  | String |
| **metricsSampleWindowMs** (common) | The window of time a metrics sample is computed over. | 30000 | Integer |
| **noOfMetricsSample** (common) | The number of samples maintained to compute metrics. | 2 | Integer |
| **receiveBufferBytes** (common) | The size of the TCP receive buffer (SO\_RCVBUF) to use when reading data. | 65536 | Integer |
| **reconnectBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when reconnecting to a broker that has repeatedly failed to connect. If provided, the backoff per host will increase exponentially for each consecutive connection failure, up to this maximum. After calculating the backoff increase, 20% random jitter is added to avoid connection storms. | 1000 | Integer |
| **reconnectBackoffMs** (common) | The amount of time to wait before attempting to reconnect to a given host. This avoids repeatedly connecting to a host in a tight loop. This backoff applies to all requests sent by the consumer to the broker. | 50 | Integer |
| **retryBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when retrying a request to the broker that has repeatedly failed. If provided, the backoff per client will increase exponentially for each failed request, up to this maximum. To prevent all clients from being synchronized upon retry, a randomized jitter with a factor of 0.2 will be applied to the backoff, resulting in the backoff falling within a range between 20% below and 20% above the computed value. If retry.backoff.ms is set to be higher than retry.backoff.max.ms, then retry.backoff.max.ms will be used as a constant backoff from the beginning without any exponential increase. | 1000 | Integer |
| **retryBackoffMs** (common) | The amount of time to wait before attempting to retry a failed request to a given topic partition. This avoids repeatedly sending requests in a tight loop under some failure scenarios. This value is the initial backoff value and will increase exponentially for each failed request, up to the retry.backoff.max.ms value. | 100 | Integer |
| **sendBufferBytes** (common) | Socket write buffer size. | 131072 | Integer |
| **shutdownTimeout** (common) | Timeout in milliseconds to wait gracefully for the consumer or producer to shut down and terminate its worker threads. | 30000 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **checkCrcs** (consumer) | Automatically check the CRC32 of the records consumed. This ensures no on-the-wire or on-disk corruption to the messages occurred. | true | Boolean |
| **commitMode** (consumer) | 
How the acknowledgements of a poll are committed to the broker. SYNC commits them after the records of the poll are processed, and waits for the result, so a failure to commit is reported to the exception handler. ASYNC commits them without waiting, and a failure to commit is logged.

Enum values:

-   SYNC
    
-   ASYNC
    





 | SYNC | KafkaShareCommitMode |
| **commitTimeoutMs** (consumer) | The maximum time to wait for the acknowledgements to be committed, when commitMode is SYNC. | 5000 | Long |
| **consumerRequestTimeoutMs** (consumer) | The configuration controls the maximum amount of time the client will wait for the response of a request. If the response is not received before the timeout elapses, the client will resend the request if necessary or fail the request if retries are exhausted. | 30000 | Integer |
| **consumersCount** (consumer) | The number of consumers that connect to the Kafka server. Each consumer runs on its own thread and receives records, as the records of a partition are shared by all the consumers of a share group. Unlike a consumer group, the number of consumers is not limited by the number of partitions. | 1 | int |
| **fetchMaxBytes** (consumer) | The maximum amount of data the server should return for a fetch request. This is not an absolute maximum: if the first record batch in the first non-empty partition of the fetch is larger than this value, the record batch will still be returned to ensure that the consumer can make progress. | 52428800 | Integer |
| **fetchMinBytes** (consumer) | The minimum amount of data the server should return for a fetch request. If insufficient data is available, the request will wait for that much data to accumulate before answering the request. | 1 | Integer |
| **fetchWaitMaxMs** (consumer) | The maximum amount of time the server will block before answering the fetch request if there isn’t enough data to immediately satisfy fetch.min.bytes. | 500 | Integer |
| **groupId** (consumer) | **Required** The name of the share group. All the consumers that use the same share group name share the records of the topics: each record is delivered to one of them. |  | String |
| **headerDeserializer** (consumer) | To use a custom KafkaHeaderDeserializer to deserialize kafka headers values. |  | KafkaHeaderDeserializer |
| **keyDeserializer** (consumer) | Deserializer class for the key that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **maxPartitionFetchBytes** (consumer) | The maximum amount of data per-partition the server will return. | 1048576 | Integer |
| **maxPollRecords** (consumer) | The maximum number of records returned in a single call to poll(). With the batch\_optimized acquire mode, a poll can return more records, to align with the batches of the topic. | 500 | Integer |
| **onFailure** (consumer) | 

How to acknowledge a record whose exchange failed or was rolled back. RELEASE makes the record available again, to this or another consumer, until the broker delivery count limit is reached. REJECT discards the record. ACCEPT marks the record as consumed.

Enum values:

-   ACCEPT
    
-   RELEASE
    
-   REJECT
    





 | RELEASE | KafkaShareAcknowledgeType |
| **pollOnError** (consumer) | 

What to do if the share consumer throws an exception while polling for new records. DISCARD and RETRY log the exception and poll again: unlike the kafka component, there is no record to skip or to retry, as the poll itself failed, and the records that fail in the route are handled with onFailure. ERROR\_HANDLER lets the exception handler of the consumer handle the exception, and polls again. RECONNECT closes the share consumer and creates a new one. STOP stops consuming. An authentication or authorization failure always stops consuming.

Enum values:

-   DISCARD
    
-   ERROR\_HANDLER
    
-   RECONNECT
    
-   RETRY
    
-   STOP
    





 | ERROR\_HANDLER | PollOnError |
| **pollTimeoutMs** (consumer) | The timeout used when polling the share consumer. | 5000 | Long |
| **preValidateHostAndPort** (consumer) | Whether to eager validate that broker host:port is valid and can be DNS resolved to known host during starting this consumer. If the validation fails, then an exception is thrown, which makes Camel fail fast. Disabling this will postpone the validation after the consumer is started, and Camel will keep re-connecting in case of validation or DNS resolution error. | true | boolean |
| **specificAvroReader** (consumer) | This enables the use of a specific Avro reader for use with the in multiple Schema registries documentation with Avro Deserializers implementation. This option is only available externally (not standard Apache Kafka). | false | boolean |
| **valueDeserializer** (consumer) | Deserializer class for value that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **acquireMode** (consumer (advanced)) | 

How the share consumer acquires records. With record\_limit, a poll() returns at most maxPollRecords records. With batch\_optimized, a poll() can return more records than maxPollRecords, to align with the batches of the topic.

Enum values:

-   batch\_optimized
    
-   record\_limit
    





 | batch\_optimized | String |
| **createConsumerBackoffInterval** (consumer (advanced)) | The delay in millis seconds to wait before trying again to create the kafka consumer (kafka-client). | 5000 | long |
| **createConsumerBackoffMaxAttempts** (consumer (advanced)) | Maximum attempts to create the kafka consumer (kafka-client), before eventually giving up and failing. Error during creating the consumer may be fatal due to invalid configuration and as such recovery is not possible. However, one part of the validation is DNS resolution of the bootstrap broker hostnames. This may be a temporary networking problem, and could potentially be recoverable. While other errors are fatal, such as some invalid kafka configurations. Unfortunately, kafka-client does not separate this kind of errors. Camel will by default retry forever, and therefore never give up. If you want to give up after many attempts then set this option and Camel will then when giving up terminate the consumer. To try again, you can manually restart the consumer by stopping, and starting the route. |  | int |
| **pollExceptionStrategy** (consumer (advanced)) | **Autowired** To use a custom strategy with the consumer to control how to handle exceptions thrown from the Kafka broker while polling messages. |  | PollExceptionStrategy |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **kafkaShareClientFactory** (advanced) | **Autowired** Factory to use for creating org.apache.kafka.clients.consumer.KafkaShareConsumer instances. This allows configuring a custom factory to create instances with logic that extends the vanilla Kafka clients. |  | KafkaShareClientFactory |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **schemaRegistryURL** (schema) | URL of the schema registry servers to use. The format is host1:port1,host2:port2. This is known as schema.registry.url in multiple Schema registries documentation. This option is only available externally (not standard Apache Kafka). |  | String |
| **kerberosBeforeReloginMinTime** (security) | Login thread sleep time between refresh attempts. | 60000 | Integer |
| **kerberosConfigLocation** (security) | Location of the kerberos config file. |  | String |
| **kerberosInitCmd** (security) | Kerberos kinit command path. Default is /usr/bin/kinit. | /usr/bin/kinit | String |
| **kerberosPrincipalToLocalRules** (security) | A list of rules for mapping from principal names to short names (typically operating system usernames). The rules are evaluated in order, and the first rule that matches a principal name is used to map it to a short name. Any later rules in the list are ignored. By default, principal names of the form {username}/{hostname}{REALM} are mapped to {username}. For more details on the format, please see the Security Authorization and ACLs documentation (at the Apache Kafka project website). Multiple values can be separated by comma. | DEFAULT | String |
| **kerberosRenewJitter** (security) | Percentage of random jitter added to the renewal time. | 0.05 | Double |
| **kerberosRenewWindowFactor** (security) | Login thread will sleep until the specified window factor of time from last refresh to ticket’s expiry has been reached, at which time it will try to renew the ticket. | 0.8 | Double |
| **oauthClientId** (security) | OAuth client ID. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthClientSecret** (security) | OAuth client secret. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthScope** (security) | OAuth scope. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthTokenEndpointUri** (security) | OAuth token endpoint URI. Used when saslAuthType is set to OAUTH. |  | String |
| **saslAuthType** (security) | 

Simplified authentication type to use. This provides an easier way to configure Kafka authentication without manually setting securityProtocol, saslMechanism, and saslJaasConfig. When set, the appropriate security settings are automatically derived. Note: This is optional. You can still use the traditional approach with explicit securityProtocol, saslMechanism, and saslJaasConfig properties.

Enum values:

-   NONE
    
-   PLAIN
    
-   SCRAM\_SHA\_256
    
-   SCRAM\_SHA\_512
    
-   SSL
    
-   OAUTH
    
-   AWS\_MSK\_IAM
    
-   KERBEROS
    





 |  | KafkaAuthType |
| **saslJaasConfig** (security) | Expose the kafka sasl.jaas.config parameter Example: org.apache.kafka.common.security.plain.PlainLoginModule required username=USERNAME password=PASSWORD;. |  | String |
| **saslKerberosServiceName** (security) | The Kerberos principal name that Kafka runs as. This can be defined either in Kafka’s JAAS config or in Kafka’s config. |  | String |
| **saslMechanism** (security) | The Simple Authentication and Security Layer (SASL) Mechanism used. For the valid values see [http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml](http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml). | GSSAPI | String |
| **saslPassword** (security) | Password for SASL authentication. Used when saslAuthType is set to PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | String |
| **saslUsername** (security) | Username for SASL authentication. Used when saslAuthType is set to PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | String |
| **securityProtocol** (security) | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | PLAINTEXT | String |
| **sslCipherSuites** (security) | A list of cipher suites. This is a named combination of authentication, encryption, MAC and key exchange algorithm used to negotiate the security settings for a network connection using TLS or SSL network protocol. By default, all the available cipher suites are supported. |  | String |
| **sslContextParameters** (security) | SSL configuration using a Camel SSLContextParameters object. If configured, it’s applied before the other SSL endpoint parameters. NOTE: Kafka only supports loading keystore from file locations, so prefix the location with file: in the KeyStoreParameters.resource option. |  | SSLContextParameters |
| **sslEnabledProtocols** (security) | The list of protocols enabled for SSL connections. The default is TLSv1.2,TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. With the default value for Java 11, clients and servers will prefer TLSv1.3 if both support it and fallback to TLSv1.2 otherwise (assuming both support at least TLSv1.2). This default should be fine for most cases. Also see the config documentation for SslProtocol. |  | String |
| **sslEndpointAlgorithm** (security) | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | https | String |
| **sslKeymanagerAlgorithm** (security) | The algorithm used by key manager factory for SSL connections. Default value is the key manager factory algorithm configured for the Java Virtual Machine. | SunX509 | String |
| **sslKeyPassword** (security) | The password of the private key in the key store file or the PEM key specified in sslKeystoreKey. This is required for clients only if two-way authentication is configured. |  | String |
| **sslKeystoreLocation** (security) | The location of the key store file. This is optional for the client and can be used for two-way authentication for the client. |  | String |
| **sslKeystorePassword** (security) | The store password for the key store file. This is optional for the client and only needed if sslKeystoreLocation is configured. Key store password is not supported for PEM format. |  | String |
| **sslKeystoreType** (security) | The file format of the key store file. This is optional for the client. The default value is JKS. | JKS | String |
| **sslProtocol** (security) | The SSL protocol used to generate the SSLContext. The default is TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. This value should be fine for most use cases. Allowed values in recent JVMs are TLSv1.2 and TLSv1.3. TLS, TLSv1.1, SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. With the default value for this config and sslEnabledProtocols, clients will downgrade to TLSv1.2 if the server does not support TLSv1.3. If this config is set to TLSv1.2, clients will not use TLSv1.3 even if it is one of the values in sslEnabledProtocols and the server only supports TLSv1.3. |  | String |
| **sslProvider** (security) | The name of the security provider used for SSL connections. Default value is the default security provider of the JVM. |  | String |
| **sslTrustmanagerAlgorithm** (security) | The algorithm used by trust manager factory for SSL connections. Default value is the trust manager factory algorithm configured for the Java Virtual Machine. | PKIX | String |
| **sslTruststoreLocation** (security) | The location of the trust store file. |  | String |
| **sslTruststorePassword** (security) | The password for the trust store file. If a password is not set, trust store file configured will still be used, but integrity checking is disabled. Trust store password is not supported for PEM format. |  | String |
| **sslTruststoreType** (security) | The file format of the trust store file. The default value is JKS. | JKS | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Kafka Share endpoint is configured using URI syntax:

kafka-share:topic

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** Name of the topic to consume from. Use comma to separate multiple topics. Topic patterns are not supported by share groups. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Sets additional properties for either kafka consumer or kafka producer in case they can’t be set directly on the camel configurations (e.g.: new Kafka properties that are not reflected yet in Camel configurations), the properties have to be prefixed with additionalProperties., e.g.: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. If the properties are set in the application.properties file, they must be prefixed with camel.component.kafka.additional-properties (camel.component.kafka-share.additional-properties for the Kafka Share component) followed by the property name enclosed in square brackets, for example the delivery.timeout.ms property in square brackets. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **brokers** (common) | URL of the Kafka brokers to use. The format is host1:port1,host2:port2, and the list can be a subset of brokers or a VIP pointing to a subset of brokers. This option is known as bootstrap.servers in the Kafka documentation. |  | String |
| **clientId** (common) | The client id is a user-specified string sent in each request to help trace calls. It should logically identify the application making the request. |  | String |
| **connectionMaxIdleMs** (common) | Close idle connections after the number of milliseconds specified by this config. | 540000 | Integer |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **metadataMaxAgeMs** (common) | The period of time in milliseconds after which we force a refresh of metadata even if we haven’t seen any partition leadership changes to proactively discover any new brokers or partitions. | 300000 | Integer |
| **metricReporters** (common) | A list of classes to use as metrics reporters. Implementing the MetricReporter interface allows plugging in classes that will be notified of new metric creation. The JmxReporter is always included to register JMX statistics. |  | String |
| **metricsSampleWindowMs** (common) | The window of time a metrics sample is computed over. | 30000 | Integer |
| **noOfMetricsSample** (common) | The number of samples maintained to compute metrics. | 2 | Integer |
| **receiveBufferBytes** (common) | The size of the TCP receive buffer (SO\_RCVBUF) to use when reading data. | 65536 | Integer |
| **reconnectBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when reconnecting to a broker that has repeatedly failed to connect. If provided, the backoff per host will increase exponentially for each consecutive connection failure, up to this maximum. After calculating the backoff increase, 20% random jitter is added to avoid connection storms. | 1000 | Integer |
| **reconnectBackoffMs** (common) | The amount of time to wait before attempting to reconnect to a given host. This avoids repeatedly connecting to a host in a tight loop. This backoff applies to all requests sent by the consumer to the broker. | 50 | Integer |
| **retryBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when retrying a request to the broker that has repeatedly failed. If provided, the backoff per client will increase exponentially for each failed request, up to this maximum. To prevent all clients from being synchronized upon retry, a randomized jitter with a factor of 0.2 will be applied to the backoff, resulting in the backoff falling within a range between 20% below and 20% above the computed value. If retry.backoff.ms is set to be higher than retry.backoff.max.ms, then retry.backoff.max.ms will be used as a constant backoff from the beginning without any exponential increase. | 1000 | Integer |
| **retryBackoffMs** (common) | The amount of time to wait before attempting to retry a failed request to a given topic partition. This avoids repeatedly sending requests in a tight loop under some failure scenarios. This value is the initial backoff value and will increase exponentially for each failed request, up to the retry.backoff.max.ms value. | 100 | Integer |
| **sendBufferBytes** (common) | Socket write buffer size. | 131072 | Integer |
| **shutdownTimeout** (common) | Timeout in milliseconds to wait gracefully for the consumer or producer to shut down and terminate its worker threads. | 30000 | int |
| **checkCrcs** (consumer) | Automatically check the CRC32 of the records consumed. This ensures no on-the-wire or on-disk corruption to the messages occurred. | true | Boolean |
| **commitMode** (consumer) | 
How the acknowledgements of a poll are committed to the broker. SYNC commits them after the records of the poll are processed, and waits for the result, so a failure to commit is reported to the exception handler. ASYNC commits them without waiting, and a failure to commit is logged.

Enum values:

-   SYNC
    
-   ASYNC
    





 | SYNC | KafkaShareCommitMode |
| **commitTimeoutMs** (consumer) | The maximum time to wait for the acknowledgements to be committed, when commitMode is SYNC. | 5000 | Long |
| **consumerRequestTimeoutMs** (consumer) | The configuration controls the maximum amount of time the client will wait for the response of a request. If the response is not received before the timeout elapses, the client will resend the request if necessary or fail the request if retries are exhausted. | 30000 | Integer |
| **consumersCount** (consumer) | The number of consumers that connect to the Kafka server. Each consumer runs on its own thread and receives records, as the records of a partition are shared by all the consumers of a share group. Unlike a consumer group, the number of consumers is not limited by the number of partitions. | 1 | int |
| **fetchMaxBytes** (consumer) | The maximum amount of data the server should return for a fetch request. This is not an absolute maximum: if the first record batch in the first non-empty partition of the fetch is larger than this value, the record batch will still be returned to ensure that the consumer can make progress. | 52428800 | Integer |
| **fetchMinBytes** (consumer) | The minimum amount of data the server should return for a fetch request. If insufficient data is available, the request will wait for that much data to accumulate before answering the request. | 1 | Integer |
| **fetchWaitMaxMs** (consumer) | The maximum amount of time the server will block before answering the fetch request if there isn’t enough data to immediately satisfy fetch.min.bytes. | 500 | Integer |
| **groupId** (consumer) | **Required** The name of the share group. All the consumers that use the same share group name share the records of the topics: each record is delivered to one of them. |  | String |
| **headerDeserializer** (consumer) | To use a custom KafkaHeaderDeserializer to deserialize kafka headers values. |  | KafkaHeaderDeserializer |
| **keyDeserializer** (consumer) | Deserializer class for the key that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **maxPartitionFetchBytes** (consumer) | The maximum amount of data per-partition the server will return. | 1048576 | Integer |
| **maxPollRecords** (consumer) | The maximum number of records returned in a single call to poll(). With the batch\_optimized acquire mode, a poll can return more records, to align with the batches of the topic. | 500 | Integer |
| **onFailure** (consumer) | 

How to acknowledge a record whose exchange failed or was rolled back. RELEASE makes the record available again, to this or another consumer, until the broker delivery count limit is reached. REJECT discards the record. ACCEPT marks the record as consumed.

Enum values:

-   ACCEPT
    
-   RELEASE
    
-   REJECT
    





 | RELEASE | KafkaShareAcknowledgeType |
| **pollOnError** (consumer) | 

What to do if the share consumer throws an exception while polling for new records. DISCARD and RETRY log the exception and poll again: unlike the kafka component, there is no record to skip or to retry, as the poll itself failed, and the records that fail in the route are handled with onFailure. ERROR\_HANDLER lets the exception handler of the consumer handle the exception, and polls again. RECONNECT closes the share consumer and creates a new one. STOP stops consuming. An authentication or authorization failure always stops consuming.

Enum values:

-   DISCARD
    
-   ERROR\_HANDLER
    
-   RECONNECT
    
-   RETRY
    
-   STOP
    





 | ERROR\_HANDLER | PollOnError |
| **pollTimeoutMs** (consumer) | The timeout used when polling the share consumer. | 5000 | Long |
| **preValidateHostAndPort** (consumer) | Whether to eager validate that broker host:port is valid and can be DNS resolved to known host during starting this consumer. If the validation fails, then an exception is thrown, which makes Camel fail fast. Disabling this will postpone the validation after the consumer is started, and Camel will keep re-connecting in case of validation or DNS resolution error. | true | boolean |
| **specificAvroReader** (consumer) | This enables the use of a specific Avro reader for use with the in multiple Schema registries documentation with Avro Deserializers implementation. This option is only available externally (not standard Apache Kafka). | false | boolean |
| **valueDeserializer** (consumer) | Deserializer class for value that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **acquireMode** (consumer (advanced)) | 

How the share consumer acquires records. With record\_limit, a poll() returns at most maxPollRecords records. With batch\_optimized, a poll() can return more records than maxPollRecords, to align with the batches of the topic.

Enum values:

-   batch\_optimized
    
-   record\_limit
    





 | batch\_optimized | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **kafkaShareClientFactory** (advanced) | Factory to use for creating org.apache.kafka.clients.consumer.KafkaShareConsumer instances. This allows configuring a custom factory to create instances with logic that extends the vanilla Kafka clients. |  | KafkaShareClientFactory |
| **schemaRegistryURL** (schema) | URL of the schema registry servers to use. The format is host1:port1,host2:port2. This is known as schema.registry.url in multiple Schema registries documentation. This option is only available externally (not standard Apache Kafka). |  | String |
| **kerberosBeforeReloginMinTime** (security) | Login thread sleep time between refresh attempts. | 60000 | Integer |
| **kerberosConfigLocation** (security) | Location of the kerberos config file. |  | String |
| **kerberosInitCmd** (security) | Kerberos kinit command path. Default is /usr/bin/kinit. | /usr/bin/kinit | String |
| **kerberosPrincipalToLocalRules** (security) | A list of rules for mapping from principal names to short names (typically operating system usernames). The rules are evaluated in order, and the first rule that matches a principal name is used to map it to a short name. Any later rules in the list are ignored. By default, principal names of the form {username}/{hostname}{REALM} are mapped to {username}. For more details on the format, please see the Security Authorization and ACLs documentation (at the Apache Kafka project website). Multiple values can be separated by comma. | DEFAULT | String |
| **kerberosRenewJitter** (security) | Percentage of random jitter added to the renewal time. | 0.05 | Double |
| **kerberosRenewWindowFactor** (security) | Login thread will sleep until the specified window factor of time from last refresh to ticket’s expiry has been reached, at which time it will try to renew the ticket. | 0.8 | Double |
| **oauthClientId** (security) | OAuth client ID. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthClientSecret** (security) | OAuth client secret. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthScope** (security) | OAuth scope. Used when saslAuthType is set to OAUTH. |  | String |
| **oauthTokenEndpointUri** (security) | OAuth token endpoint URI. Used when saslAuthType is set to OAUTH. |  | String |
| **saslAuthType** (security) | 

Simplified authentication type to use. This provides an easier way to configure Kafka authentication without manually setting securityProtocol, saslMechanism, and saslJaasConfig. When set, the appropriate security settings are automatically derived. Note: This is optional. You can still use the traditional approach with explicit securityProtocol, saslMechanism, and saslJaasConfig properties.

Enum values:

-   NONE
    
-   PLAIN
    
-   SCRAM\_SHA\_256
    
-   SCRAM\_SHA\_512
    
-   SSL
    
-   OAUTH
    
-   AWS\_MSK\_IAM
    
-   KERBEROS
    





 |  | KafkaAuthType |
| **saslJaasConfig** (security) | Expose the kafka sasl.jaas.config parameter Example: org.apache.kafka.common.security.plain.PlainLoginModule required username=USERNAME password=PASSWORD;. |  | String |
| **saslKerberosServiceName** (security) | The Kerberos principal name that Kafka runs as. This can be defined either in Kafka’s JAAS config or in Kafka’s config. |  | String |
| **saslMechanism** (security) | The Simple Authentication and Security Layer (SASL) Mechanism used. For the valid values see [http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml](http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml). | GSSAPI | String |
| **saslPassword** (security) | Password for SASL authentication. Used when saslAuthType is set to PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | String |
| **saslUsername** (security) | Username for SASL authentication. Used when saslAuthType is set to PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | String |
| **securityProtocol** (security) | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | PLAINTEXT | String |
| **sslCipherSuites** (security) | A list of cipher suites. This is a named combination of authentication, encryption, MAC and key exchange algorithm used to negotiate the security settings for a network connection using TLS or SSL network protocol. By default, all the available cipher suites are supported. |  | String |
| **sslContextParameters** (security) | SSL configuration using a Camel SSLContextParameters object. If configured, it’s applied before the other SSL endpoint parameters. NOTE: Kafka only supports loading keystore from file locations, so prefix the location with file: in the KeyStoreParameters.resource option. |  | SSLContextParameters |
| **sslEnabledProtocols** (security) | The list of protocols enabled for SSL connections. The default is TLSv1.2,TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. With the default value for Java 11, clients and servers will prefer TLSv1.3 if both support it and fallback to TLSv1.2 otherwise (assuming both support at least TLSv1.2). This default should be fine for most cases. Also see the config documentation for SslProtocol. |  | String |
| **sslEndpointAlgorithm** (security) | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | https | String |
| **sslKeymanagerAlgorithm** (security) | The algorithm used by key manager factory for SSL connections. Default value is the key manager factory algorithm configured for the Java Virtual Machine. | SunX509 | String |
| **sslKeyPassword** (security) | The password of the private key in the key store file or the PEM key specified in sslKeystoreKey. This is required for clients only if two-way authentication is configured. |  | String |
| **sslKeystoreLocation** (security) | The location of the key store file. This is optional for the client and can be used for two-way authentication for the client. |  | String |
| **sslKeystorePassword** (security) | The store password for the key store file. This is optional for the client and only needed if sslKeystoreLocation is configured. Key store password is not supported for PEM format. |  | String |
| **sslKeystoreType** (security) | The file format of the key store file. This is optional for the client. The default value is JKS. | JKS | String |
| **sslProtocol** (security) | The SSL protocol used to generate the SSLContext. The default is TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. This value should be fine for most use cases. Allowed values in recent JVMs are TLSv1.2 and TLSv1.3. TLS, TLSv1.1, SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. With the default value for this config and sslEnabledProtocols, clients will downgrade to TLSv1.2 if the server does not support TLSv1.3. If this config is set to TLSv1.2, clients will not use TLSv1.3 even if it is one of the values in sslEnabledProtocols and the server only supports TLSv1.3. |  | String |
| **sslProvider** (security) | The name of the security provider used for SSL connections. Default value is the default security provider of the JVM. |  | String |
| **sslTrustmanagerAlgorithm** (security) | The algorithm used by trust manager factory for SSL connections. Default value is the trust manager factory algorithm configured for the Java Virtual Machine. | PKIX | String |
| **sslTruststoreLocation** (security) | The location of the trust store file. |  | String |
| **sslTruststorePassword** (security) | The password for the trust store file. If a password is not set, trust store file configured will still be used, but integrity checking is disabled. Trust store password is not supported for PEM format. |  | String |
| **sslTruststoreType** (security) | The file format of the trust store file. The default value is JKS. | JKS | String |

## Message Headers

The Kafka Share component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKafkaTopic** (consumer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#TOPIC) | The topic from where the message originated. |  | String |
| **CamelKafkaPartition** (consumer) Constant: [`PARTITION`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#PARTITION) | The partition where the message was stored. |  | Integer |
| **CamelKafkaOffset** (consumer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#OFFSET) | The offset of the message. |  | Long |
| **CamelKafkaKey** (consumer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#KEY) | The key of the message if configured. |  | Object |
| **CamelKafkaTimestamp** (consumer) Constant: [`TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#TIMESTAMP) | The timestamp of the message. |  | Long |
| **CamelKafkaHeaders** (consumer) Constant: [`HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#HEADERS) | The record headers. |  | Headers |
| **CamelKafkaShareDeliveryCount** (consumer) Constant: [`DELIVERY_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#DELIVERY_COUNT) | How many times the record has been delivered, this delivery included. The header is not set when the broker does not count the deliveries. |  | Short |
| **CamelKafkaShareAcknowledge** (consumer) Constant: [`ACKNOWLEDGE`](https://javadoc.io/doc/org.apache.camel/camel-kafka-share/latest/org/apache/camel/component/kafka/share/KafkaShareConstants.html#ACKNOWLEDGE) | 
How to acknowledge the record (ACCEPT, RELEASE or REJECT), instead of deriving it from the outcome of the exchange. Set it in the route, for example to REJECT a record that was delivered too many times.

Enum values:

-   ACCEPT
    
-   RELEASE
    
-   REJECT
    





 |  | String |

## Usage

### Broker requirements

Share groups need the `share.version` feature of the cluster at level 1. It is enabled by default on a cluster created with Kafka 4.2 or newer; a cluster upgraded from an older version enables it with `kafka-features.sh --bootstrap-server <broker> upgrade --feature share.version=1`. On a single broker, also set `share.coordinator.state.topic.replication.factor=1` and `share.coordinator.state.topic.min.isr=1`, otherwise the broker cannot create the internal topic that holds the state of the share groups, and the consumers receive no records.

The broker setting `group.share.delivery.count.limit` (default 5) limits how many times a record is delivered, and `group.share.record.lock.duration.ms` (default 30 seconds) limits how long a consumer can hold a record before the broker makes it available to another consumer.

A new share group starts with the records produced after it is created. To consume the records already in the topic, set the group configuration `share.auto.offset.reset` to `earliest` before the group first consumes, for example with `kafka-configs.sh --entity-type groups --entity-name my-group --alter --add-config share.auto.offset.reset=earliest`.

### Acknowledgements

Each record is acknowledged after its exchange is processed, from the outcome of the exchange:

 
| Exchange outcome | Acknowledgement |
| --- | --- |
| The route set the `CamelKafkaShareAcknowledge` header (`ACCEPT`, `RELEASE` or `REJECT`) | The value of the header |
| Completed, or failed with an exception handled by the route (for example `onException(…​).handled(true)`) | `ACCEPT` |
| Failed, or rolled back | The `onFailure` option, `RELEASE` by default |
| Not processed because the consumer is stopping | `RELEASE` |

`ACCEPT`

The record was processed: it is not delivered again.

`RELEASE`

The record was not processed: the broker delivers it again, to this or another consumer, until the delivery count limit of the broker is reached.

`REJECT`

The record cannot be processed: it is discarded and not delivered again.

The acknowledgements of the records of a poll are committed to the broker after they are processed. With `commitMode=SYNC` (default) the consumer waits for the result, and a failure to commit is reported to the exception handler; with `commitMode=ASYNC` it does not wait, and a failure is logged. When the acknowledgements cannot be committed, the broker delivers the records again.

The `CamelKafkaShareAcknowledge` header starts with `Camel`, so a header with this name in a Kafka record is removed by the header filter strategy: only the route can set it.

### Delivery count and poison records

The `CamelKafkaShareDeliveryCount` header holds how many times the record has been delivered, this delivery included. As the broker delivers a released record again, a route can stop retrying a record that keeps failing, and move it elsewhere:

-   Java
    
-   YAML
    

```java
errorHandler(noErrorHandler()); // no local retries: the broker delivers the record again, possibly to another pod

onException(InvalidInvoiceException.class)
    .handled(true)                                       // handled -> ACCEPT
    .to("kafka:invoices-invalid?brokers={{kafka.brokers}}");

from("kafka-share:invoices?brokers={{kafka.brokers}}&groupId=invoice-ocr")
    .filter(header(KafkaShareConstants.DELIVERY_COUNT).isGreaterThanOrEqualTo(4))
        .setHeader(KafkaShareConstants.ACKNOWLEDGE, constant("REJECT"))
        .to("kafka:invoices-dlq?brokers={{kafka.brokers}}")
        .stop()
    .end()
    .to("http://ocr-service/extract")
    .to("kafka:invoices-extracted?brokers={{kafka.brokers}}");
```

```yaml
- route:
    from:
      uri: kafka-share:invoices
      parameters:
        brokers: "{{kafka.brokers}}"
        groupId: invoice-ocr
      steps:
        - filter:
            simple: "${header.CamelKafkaShareDeliveryCount} >= 4"
            steps:
              - setHeader:
                  name: CamelKafkaShareAcknowledge
                  constant: REJECT
              - to: "kafka:invoices-dlq?brokers={{kafka.brokers}}"
              - stop: {}
        - to: "http://ocr-service/extract"
        - to: "kafka:invoices-extracted?brokers={{kafka.brokers}}"
```

### Consumers count

Each consumer (`consumersCount`) runs on its own thread with its own share consumer, as the Kafka client is not thread safe. Unlike a consumer group, consumers beyond the number of partitions are not idle: all of them receive records.

-   Java
    
-   YAML
    

```java
// 20 concurrent consumers on a topic with 3 partitions: a slow ticket does not hold up the others
from("kafka-share:support-tickets?brokers={{kafka.brokers}}&groupId=ticket-triage&consumersCount=20")
    .to("langchain4j-chat:triage")
    .to("kafka:tickets-triaged?brokers={{kafka.brokers}}");
```

```yaml
- route:
    from:
      uri: kafka-share:support-tickets
      parameters:
        brokers: "{{kafka.brokers}}"
        groupId: ticket-triage
        consumersCount: 20
      steps:
        - to: "langchain4j-chat:triage"
        - to: "kafka:tickets-triaged?brokers={{kafka.brokers}}"
```

### Delivery semantics

Delivery is at-least-once. A record is processed again when:

-   its acquisition lock expires while the route processes it (see `group.share.record.lock.duration.ms`);
    
-   the JVM stops after the route’s side effects but before the acknowledgement reaches the broker;
    
-   the acknowledgements cannot be committed;
    
-   the route releases a record after a partial side effect.
    

Use the [Idempotent Consumer](eips/idempotentConsumer-eip.md) where duplicates matter.

### Differences from the Kafka component

The options of the Kafka component that are about offsets, consumer group membership and ordering do not apply to a share group: `seekTo`, `autoOffsetReset`, `autoCommitEnable`, `allowManualCommit`, `breakOnFirstError`, `partitionAssignor`, `groupProtocol`, `groupInstanceId`, `topicIsPattern`, `isolationLevel`, `offsetRepository` and `batching`. A share consumer cannot be paused, so suspending a route stops its consumer. The brokers, security, deserializer, header and additional properties options are the same as the Kafka component.

The client properties that a share consumer rejects (`auto.offset.reset`, `enable.auto.commit`, `group.instance.id`, `isolation.level`, `partition.assignment.strategy`, `interceptor.classes`, `session.timeout.ms`, `heartbeat.interval.ms`, `group.protocol` and `group.remote.assignor`) make the consumer fail to start, with an error naming them, when they are set as `additionalProperties`.

### Health check

The consumer is ready when all its share consumers are created and subscribed. When a share consumer cannot be created, the health check reports it as down, with the error and the `bootstrap.servers`, `group.id`, `client.id`, `route.id` and `topic` details.