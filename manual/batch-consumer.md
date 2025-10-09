# Batch Consumer

Batch Consumer is basically a [Polling Consumer](../components/4.18.x/eips/polling-consumer.md) that is capable of polling multiple Exchanges in a single pool.

To support batching the consumer must implement the `org.apache.camel.BatchConsumer` interface.

A range of Camel components support batching such as:

-   [AWS2 DDB](../components/4.18.x/aws2-ddb-component.md)
    
-   [AWS2 Kinesis](../components/4.18.x/aws2-kinesis-component.md)
    
-   [AWS2 S3](../components/4.18.x/aws2-s3-component.md)
    
-   [AWS2 SQS](../components/4.18.x/aws2-sqs-component.md)
    
-   [File](../components/4.18.x/file-component.md)
    
-   [FTP](../components/4.18.x/ftp-component.md)
    
-   [IronMQ](../components/4.18.x/ironmq-component.md)
    
-   [Jooq](../components/4.18.x/jooq-component.md)
    
-   [JPA](../components/4.18.x/jpa-component.md)
    
-   [Mail](../components/4.18.x/mail-component.md)
    
-   [Minio](../components/4.18.x/minio-component.md)
    
-   [MyBatis](../components/4.18.x/mybatis-component.md)
    
-   [Slack](../components/4.18.x/slack-component.md)
    
-   [Splunk](../components/4.18.x/splunk-component.md)
    
-   [SQL](../components/4.18.x/sql-component.md)
    

## Options

The `BatchConsumer` supports the following options:

 
| Option | Description |
| --- | --- |
| `maxMessagesPerPoll` | An integer to define a maximum messages to gather per poll. By default, no maximum is set. It can be used to set a limit of e.g., 1000 to avoid when starting up the server that there are thousands of files. Set a value of 0 or negative to disable it as unlimited. |

Very often a `BatchConsumer` is scheduled and is based of the `ScheduledBatchPollingConsumer` that has many options for configuring the scheduling. These options are listed with _(scheduler)_ as label in the endpoint options' in the [Components](../components/4.18.x/index.md) documentation.

## Exchange Properties

The following properties are set on the Exchange for each Exchange polled in the same batch.

 
| Property | Description |
| --- | --- |
| `CamelBatchSize` | The total number of Exchanges that was polled in this batch. |
| `CamelBatchIndex` | The current index of the batch. Starts from 0. |
| `CamelBatchComplete` | A boolean indicating the last Exchange in the batch. Is only `true` for the last entry. |