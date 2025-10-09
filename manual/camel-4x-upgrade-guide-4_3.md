# Apache Camel 4.x Upgrade Guide

This document is for helping you upgrade your Apache Camel application from Camel 4.x to 4.y. For example, if you are upgrading Camel 4.0 to 4.2, then you should follow the guides from both 4.0 to 4.1 and 4.1 to 4.2.

> **Note**
> [The Camel Upgrade Recipes project](https://github.com/apache/camel-upgrade-recipes/) provides automated assistance for some common migration tasks. Note that manual migration is still required. See the [documentation](camel-upgrade-recipes-tool.md) page for details.

## Upgrading Camel 4.2 to 4.3

### camel-core

Moved class `org.apache.camel.impl.engine.MemoryStateRepository` from camel-base-engine to `org.apache.camel.support.processor.state.MemoryStateRepository` in camel-support.

Moved class `org.apache.camel.impl.engine.FileStateRepository` from camel-base-engine to `org.apache.camel.support.processor.state.FileStateRepository` in camel-support.

### Resequence EIP

The configuration for batch and stream has been renamed from `batch-config` to `batchConfig` and `stream-config` to `streamConfig`.

For example before:

```xml
<resequence>
    <stream-config timeout="1000" deliveryAttemptInterval="10"/>
    <simple>${header.seqnum}</simple>
    <to uri="mock:result" />
</resequence>
```

And now after:

```xml
<resequence>
    <streamConfig timeout="1000" deliveryAttemptInterval="10"/>
    <simple>${header.seqnum}</simple>
    <to uri="mock:result" />
</resequence>
```

### Throttle EIP

Throttle now uses the number of concurrent requests as the throttling measure instead of the number of requests per period.

Update throttle expressions configured with `maxRequestsPerPeriod` to use `maxConcurrentRequests` instead, and remove any `timePeriodMillis` option.

For example, update the following:

```java
long maxRequestsPerPeriod = 100L;

from("seda:a")
  .throttle(maxRequestsPerPeriod).timePeriodMillis(500)
  .to("seda:b")

// 1000 ms default time period
from("seda:c")
  .throttle(maxRequestsPerPeriod)
  .to("seda:d")
```

to use `maxConcurrentRequests`:

```java
long maxConcurrentRequests = 30L;

from("seda:a")
  .throttle(maxConcurrentRequests)
  .to("seda:b")

from("seda:c")
  .throttle(maxConcurrentRequests)
  .to("seda:d")
```

### Consumer health checks

The scheduled consumers have been improved to mark the consumer as _ready_ sooner, when possible. Previously a consumer would mark as ready after the first poll was completed. For example, an FTP consumer downloading a big file on the first poll could take so long time that the readiness check would timeout and fail during the startup of your Camel application.

The following components are now marking the consumer as ready sooner:

-   camel-aws
    
-   camel-azure
    
-   camel-box
    
-   camel-dhis2
    
-   camel-fhir
    
-   camel-couchbase
    
-   camel-ftp
    
-   camel-google
    
-   camel-ironmq
    
-   camel-jooq
    
-   camel-jpa
    
-   camel-mail
    
-   camel-minio
    
-   camel-mybatis
    
-   camel-olingo2
    
-   camel-olingo4
    
-   camel-slack
    
-   camel-splunk
    
-   camel-sql
    
-   camel-twilio
    
-   camel-zendesk
    

### camel-management

If the `nodeIdPrefix` has been configured on routes, then the MBeans for the processors will now use the prefix in their `ObjectName` also.

### camel-console

The context and route consoles have changed some values in their JSON output data for timestamp for created, completed and failed exchanges.

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Old Key</strong></td><td class="tableblock halign-left valign-top"><strong>New Key</strong></td></tr><tr><td class="tableblock halign-left valign-top"><code>sinceLastCreatedExchange</code></td><td class="tableblock halign-left valign-top"><code>lastCreatedExchangeTimestamp</code></td></tr><tr><td class="tableblock halign-left valign-top"><code>sinceLastCompletedExchange</code></td><td class="tableblock halign-left valign-top"><code>lastCompletedExchangeTimestamp</code></td></tr><tr><td class="tableblock halign-left valign-top"><code>sinceLastFailedExchange</code></td><td class="tableblock halign-left valign-top"><code>lastFailedExchangeTimestamp</code></td></tr></tbody></table>

The values are also changed from String ago to timestamp in millis.For example, old value `3m5s` is now `1701599263337`.

### camel-jbang

The `camel transform` command has been renamed to `camel transform route` as this command is used for transforming routes between DSLs such as XML to YAML.

There is a new `camel transform message` command to do message transformation.

### camel-jetty

Jetty has been upgraded from v11 to v12. End users may need to adjust to changes in Jetty.

### camel-kafka

The behavior for `breakOnFirstError` was altered as numerous issues were fixed. The behavior related to committing the offset is now determined by the `CommitManager` that is configured.

When the default `CommitManager` is used (`NoopCommitManager`) then no commit is performed. The route implementation will be responsible for managing the offset using `KafkaManualCommit` to manage the retrying of the payload.

When using the `SyncCommitManager` then the offset will be committed so that the payload is continually retried. This was the behavior described in the documentation.

When using the `AsyncCommitManager` then the offset will be committed so that the payload is continually retried. This was the behavior described in the documentation.

### camel-yaml-dsl

Using kebab-case in general has been deprecated, and you will see a WARN logs. Please migrate to camelCase.

The language for exchange property now only supports camelCase style, i.e. `exchange-property` is now `exchangeProperty`.

The `camelYamlDsl.json` Schema file has removed `inheritErrorHandler` option for all EIPs where it was not applicable. This option is only intended for the Load Balancer EIP. This makes the YAML schema in-line with the XML DSL schema.

### camel-hdfs

The HDFS component has been deprecated, and planned to be removed in 4.4 (see CAMEL-20196).

### camel-kafka

The header name for the `List<RecordMetadata>` metadata has changed from `org.apache.kafka.clients.producer.RecordMetadata` to `kafka.RECORD_META`, and the header constant from `KAFKA_RECORDMETA` to `KAFKA_RECORD_META`.