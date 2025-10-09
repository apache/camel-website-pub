# Camel Kamelets Documentation Index

Index of Camel Kamelets documentation pages.

# Kamelet Catalog

## Kamelet specification

Kamelets were originally born for Kubernetes and they have eventually moved to be used as Camel core resources. Its specification is a [Kubernetes CRD specification](apis/spec.md). You can use it in your project by using Maven dependency `org.apache.camel.kamelets:camel-kamelets-crds`.

## Development guide

Kamelets are extensible components. Look at the guide and learn [how to develop a new Kamelet](development.md).

## Compatibility Matrix

Compatibility between Kamelets catalog and Camel core    
| Camel-Kamelets Version | Using Camel Version | LTS Until | Branch |
| --- | --- | --- | --- |
| [Next (Pre-release)](index.md) | [4.8.0](../../components/next/index.md) |  | [main](https://github.com/apache/camel-kamelets) |
| [4.18.x (LTS)](../4.18.x/index.md) | [4.18.0](../../components/4.18.x/index.md) |  | [4.18.x](https://github.com/apache/camel-kamelets/tree/4.18.x) |
| [4.14.x (LTS)](../4.14.x/index.md) | [4.14.0](../../components/4.14.x/index.md) |  | [4.14.x](https://github.com/apache/camel-kamelets/tree/4.14.x) |

This page contains the default Apache Camel Kamelets catalog.

Consult the Kamelets User Guide for information about how to use these.

**We love contributions for this catalog**: you can follow the Kamelets Developer Guide for information on how to create new Kamelets and contribute them to the official [github.com/apache/camel-kamelets](https://github.com/apache/camel-kamelets/) repository.

[Camel Kamelets API](apis/spec.md)

[Camel Kamelets API](apis/spec.md)

 [![avro deserialize action](_images/kamelets/avro-deserialize-action.svg) Avro Deserialize Action](avro-deserialize-action.html)

 [![avro serialize action](_images/kamelets/avro-serialize-action.svg) Avro Serialize Action](avro-serialize-action.html)

 [![aws bedrock agent runtime sink](_images/kamelets/aws-bedrock-agent-runtime-sink.svg) AWS Bedrock Agent Runtime Sink](aws-bedrock-agent-runtime-sink.html)

 [![aws bedrock text sink](_images/kamelets/aws-bedrock-text-sink.svg) AWS Bedrock Text Sink](aws-bedrock-text-sink.html)

 [![aws cloudtrail source](_images/kamelets/aws-cloudtrail-source.svg) AWS Cloudtrail Source](aws-cloudtrail-source.html)

 [![aws cloudwatch sink](_images/kamelets/aws-cloudwatch-sink.svg) AWS CloudWatch Metrics Sink](aws-cloudwatch-sink.html)

 [![aws comprehend sink](_images/kamelets/aws-comprehend-sink.svg) AWS Comprehend Sink](aws-comprehend-sink.html)

 [![aws ddb sink](_images/kamelets/aws-ddb-sink.svg) AWS DynamoDB Sink](aws-ddb-sink.html)

 [![aws ddb streams source](_images/kamelets/aws-ddb-streams-source.svg) AWS DynamoDB Streams Source](aws-ddb-streams-source.html)

 [![aws ec2 sink](_images/kamelets/aws-ec2-sink.svg) AWS EC2 Sink](aws-ec2-sink.html)

 [![aws eventbridge sink](_images/kamelets/aws-eventbridge-sink.svg) AWS Eventbridge Sink](aws-eventbridge-sink.html)

 [![aws kinesis firehose sink](_images/kamelets/aws-kinesis-firehose-sink.svg) AWS Kinesis Firehose Sink](aws-kinesis-firehose-sink.html)

 [![aws kinesis sink](_images/kamelets/aws-kinesis-sink.svg) AWS Kinesis Sink](aws-kinesis-sink.html)

 [![aws kinesis source](_images/kamelets/aws-kinesis-source.svg) AWS Kinesis Source](aws-kinesis-source.html)

 [![aws lambda sink](_images/kamelets/aws-lambda-sink.svg) AWS Lambda Sink](aws-lambda-sink.html)

 [![aws polly sink](_images/kamelets/aws-polly-sink.svg) AWS Polly Sink](aws-polly-sink.html)

 [![aws redshift sink](_images/kamelets/aws-redshift-sink.svg) AWS Redshift Sink](aws-redshift-sink.html)

 [![aws redshift source](_images/kamelets/aws-redshift-source.svg) AWS Redshift Source](aws-redshift-source.html)

 [![aws s3 event based source](_images/kamelets/aws-s3-event-based-source.svg) AWS S3 Event Based Source](aws-s3-event-based-source.html)

 [![aws s3 sink](_images/kamelets/aws-s3-sink.svg) AWS S3 Sink](aws-s3-sink.html)

 [![aws s3 source](_images/kamelets/aws-s3-source.svg) AWS S3 Source](aws-s3-source.html)

 [![aws s3 streaming upload sink](_images/kamelets/aws-s3-streaming-upload-sink.svg) AWS S3 Streaming upload Sink](aws-s3-streaming-upload-sink.html)

 [![aws secrets manager sink](_images/kamelets/aws-secrets-manager-sink.svg) AWS Secrets Manager Sink](aws-secrets-manager-sink.html)

 [![aws ses sink](_images/kamelets/aws-ses-sink.svg) AWS SES Sink](aws-ses-sink.html)

 [![aws sns fifo sink](_images/kamelets/aws-sns-fifo-sink.svg) AWS SNS FIFO Sink](aws-sns-fifo-sink.html)

 [![aws sns sink](_images/kamelets/aws-sns-sink.svg) AWS SNS Sink](aws-sns-sink.html)

 [![aws sqs batch sink](_images/kamelets/aws-sqs-batch-sink.svg) AWS SQS Batch Sink](aws-sqs-batch-sink.html)

 [![aws sqs fifo sink](_images/kamelets/aws-sqs-fifo-sink.svg) AWS SQS FIFO Sink](aws-sqs-fifo-sink.html)

 [![aws sqs sink](_images/kamelets/aws-sqs-sink.svg) AWS SQS Sink](aws-sqs-sink.html)

 [![aws sqs source](_images/kamelets/aws-sqs-source.svg) AWS SQS Source](aws-sqs-source.html)

 [![aws sts assume role action](_images/kamelets/aws-sts-assume-role-action.svg) AWS STS Assume Role Action](aws-sts-assume-role-action.html)

 [![aws timestream query sink](_images/kamelets/aws-timestream-query-sink.svg) AWS Timestream Query Sink](aws-timestream-query-sink.html)

 [![aws translate action](_images/kamelets/aws-translate-action.svg) AWS Translate Action](aws-translate-action.html)

 [![azure cosmosdb sink](_images/kamelets/azure-cosmosdb-sink.svg) Azure CosmosDB Sink](azure-cosmosdb-sink.html)

 [![azure cosmosdb source](_images/kamelets/azure-cosmosdb-source.svg) Azure CosmosDB Source](azure-cosmosdb-source.html)

 [![azure eventhubs sink](_images/kamelets/azure-eventhubs-sink.svg) Azure Eventhubs Sink](azure-eventhubs-sink.html)

 [![azure eventhubs source](_images/kamelets/azure-eventhubs-source.svg) Azure Eventhubs Source](azure-eventhubs-source.html)

 [![azure functions sink](_images/kamelets/azure-functions-sink.svg) Azure Function Sink](azure-functions-sink.html)

 [![azure servicebus sink](_images/kamelets/azure-servicebus-sink.svg) Azure Servicebus Sink](azure-servicebus-sink.html)

 [![azure servicebus source](_images/kamelets/azure-servicebus-source.svg) Azure Servicebus Source](azure-servicebus-source.html)

 [![azure storage blob append sink](_images/kamelets/azure-storage-blob-append-sink.svg) Azure Storage Blob Append Sink](azure-storage-blob-append-sink.html)

 [![azure storage blob changefeed source](_images/kamelets/azure-storage-blob-changefeed-source.svg) Azure Storage Blob Changefeed Source](azure-storage-blob-changefeed-source.html)

 [![azure storage blob event based source](_images/kamelets/azure-storage-blob-event-based-source.svg) Azure Storage Blob Event-based Source](azure-storage-blob-event-based-source.html)

 [![azure storage blob sink](_images/kamelets/azure-storage-blob-sink.svg) Azure Storage Blob Sink](azure-storage-blob-sink.html)

 [![azure storage blob source](_images/kamelets/azure-storage-blob-source.svg) Azure Storage Blob Source](azure-storage-blob-source.html)

 [![azure storage datalake sink](_images/kamelets/azure-storage-datalake-sink.svg) Azure Storage Blob Data Lake Sink](azure-storage-datalake-sink.html)

 [![azure storage datalake source](_images/kamelets/azure-storage-datalake-source.svg) Azure Storage Blob Data Lake Source](azure-storage-datalake-source.html)

 [![azure storage files sink](_images/kamelets/azure-storage-files-sink.svg) Azure Storage Files Sink](azure-storage-files-sink.html)

 [![azure storage files source](_images/kamelets/azure-storage-files-source.svg) Azure Storage File Source](azure-storage-files-source.html)

 [![azure storage queue sink](_images/kamelets/azure-storage-queue-sink.svg) Azure Storage Queue Sink](azure-storage-queue-sink.html)

 [![azure storage queue source](_images/kamelets/azure-storage-queue-source.svg) Azure Storage Queue Source](azure-storage-queue-source.html)

 [![bitcoin source](_images/kamelets/bitcoin-source.svg) Bitcoin Source](bitcoin-source.html)

 [![caffeine action](_images/kamelets/caffeine-action.svg) Caffeine Action](caffeine-action.html)

 [![cassandra sink](_images/kamelets/cassandra-sink.svg) Cassandra Sink](cassandra-sink.html)

 [![cassandra source](_images/kamelets/cassandra-source.svg) Cassandra Source](cassandra-source.html)

 [![ceph sink](_images/kamelets/ceph-sink.svg) Ceph Sink](ceph-sink.html)

 [![ceph source](_images/kamelets/ceph-source.svg) Ceph Source](ceph-source.html)

 [![chuck norris source](_images/kamelets/chuck-norris-source.svg) Chuck Norris Source](chuck-norris-source.html)

 [![chunk template action](_images/kamelets/chunk-template-action.svg) Chunk Template Action](chunk-template-action.html)

 [![couchbase sink](_images/kamelets/couchbase-sink.svg) Couchbase Sink](couchbase-sink.html)

 [![counter source](_images/kamelets/counter-source.svg) Counter Source](counter-source.html)

 [![cron source](_images/kamelets/cron-source.svg) Cron Source](cron-source.html)

 [![crypto decrypt action](_images/kamelets/crypto-decrypt-action.svg) Crypto Decrypt Action](crypto-decrypt-action.html)

 [![crypto encrypt action](_images/kamelets/crypto-encrypt-action.svg) Crypto Encrypt Action](crypto-encrypt-action.html)

 [![data type action](_images/kamelets/data-type-action.svg) Data Type Action](data-type-action.html)

 [![databricks sink](_images/kamelets/databricks-sink.svg) Databricks Sink](databricks-sink.html)

 [![databricks source](_images/kamelets/databricks-source.svg) Databricks Source](databricks-source.html)

 [![delay action](_images/kamelets/delay-action.svg) Delay Action](delay-action.html)

 [![djl image to text action](_images/kamelets/djl-image-to-text-action.svg) Image-to-Text Action](djl-image-to-text-action.html)

 [![dns dig action](_images/kamelets/dns-dig-action.svg) DNS DIG Action](dns-dig-action.html)

 [![dns ip action](_images/kamelets/dns-ip-action.svg) DNS IP Action](dns-ip-action.html)

 [![dns lookup action](_images/kamelets/dns-lookup-action.svg) DNS Lookup Action](dns-lookup-action.html)

 [![drop field action](_images/kamelets/drop-field-action.svg) Drop Field Action](drop-field-action.html)

 [![drop header action](_images/kamelets/drop-header-action.svg) Drop Header Action](drop-header-action.html)

 [![drop headers action](_images/kamelets/drop-headers-action.svg) Drop Headers Action](drop-headers-action.html)

 [![dropbox sink](_images/kamelets/dropbox-sink.svg) Dropbox Sink](dropbox-sink.html)

 [![dropbox source](_images/kamelets/dropbox-source.svg) Dropbox Source](dropbox-source.html)

 [![earthquake source](_images/kamelets/earthquake-source.svg) Earthquake Source](earthquake-source.html)

 [![elasticsearch index sink](_images/kamelets/elasticsearch-index-sink.svg) ElasticSearch Index Sink](elasticsearch-index-sink.html)

 [![elasticsearch search source](_images/kamelets/elasticsearch-search-source.svg) ElasticSearch Search Source](elasticsearch-search-source.html)

 [![exec sink](_images/kamelets/exec-sink.svg) Exec Sink](exec-sink.html)

 [![extract field action](_images/kamelets/extract-field-action.svg) Extract Field Action](extract-field-action.html)

 [![fhir sink](_images/kamelets/fhir-sink.svg) FHIR Sink](fhir-sink.html)

 [![fhir source](_images/kamelets/fhir-source.svg) FHIR Source](fhir-source.html)

 [![file watch source](_images/kamelets/file-watch-source.svg) File Watch Source](file-watch-source.html)

 [![freemarker template action](_images/kamelets/freemarker-template-action.svg) Freemarker Template Action](freemarker-template-action.html)

 [![ftp sink](_images/kamelets/ftp-sink.svg) FTP Sink](ftp-sink.html)

 [![ftp source](_images/kamelets/ftp-source.svg) FTP Source](ftp-source.html)

 [![ftps sink](_images/kamelets/ftps-sink.svg) FTPS Sink](ftps-sink.html)

 [![ftps source](_images/kamelets/ftps-source.svg) FTPS Source](ftps-source.html)

 [![github commit source](_images/kamelets/github-commit-source.svg) GitHub Commit Source](github-commit-source.html)

 [![github event source](_images/kamelets/github-event-source.svg) GitHub Event Source](github-event-source.html)

 [![github pullrequest comment source](_images/kamelets/github-pullrequest-comment-source.svg) GitHub Pull Request Comments Source](github-pullrequest-comment-source.html)

 [![github pullrequest source](_images/kamelets/github-pullrequest-source.svg) GitHub Pull Request Source](github-pullrequest-source.html)

 [![github tag source](_images/kamelets/github-tag-source.svg) GitHub Tag Source](github-tag-source.html)

 [![google bigquery sink](_images/kamelets/google-bigquery-sink.svg) Google Big Query Sink](google-bigquery-sink.html)

 [![google calendar source](_images/kamelets/google-calendar-source.svg) Google Calendar Source](google-calendar-source.html)

 [![google functions sink](_images/kamelets/google-functions-sink.svg) Google Functions Sink](google-functions-sink.html)

 [![google mail source](_images/kamelets/google-mail-source.svg) Google Mail Source](google-mail-source.html)

 [![google pubsub sink](_images/kamelets/google-pubsub-sink.svg) Google Pubsub Sink](google-pubsub-sink.html)

 [![google pubsub source](_images/kamelets/google-pubsub-source.svg) Google Pubsub Source](google-pubsub-source.html)

 [![google sheets sink](_images/kamelets/google-sheets-sink.svg) Google Sheets Sink](google-sheets-sink.html)

 [![google sheets source](_images/kamelets/google-sheets-source.svg) Google Sheets Source](google-sheets-source.html)

 [![google storage event based source](_images/kamelets/google-storage-event-based-source.svg) Google Storage Event-based Source](google-storage-event-based-source.html)

 [![google storage sink](_images/kamelets/google-storage-sink.svg) Google Storage Sink](google-storage-sink.html)

 [![google storage source](_images/kamelets/google-storage-source.svg) Google Storage Source](google-storage-source.html)

 [![google vertexai sink](_images/kamelets/google-vertexai-sink.svg) Google Vertex AI Sink](google-vertexai-sink.html)

 [![graphql sink](_images/kamelets/graphql-sink.svg) GraphQL Sink](graphql-sink.html)

 [![has header filter action](_images/kamelets/has-header-filter-action.svg) Has Header Filter Action](has-header-filter-action.html)

 [![header matches filter action](_images/kamelets/header-matches-filter-action.svg) Header Matches Filter Action](header-matches-filter-action.html)

 [![hoist field action](_images/kamelets/hoist-field-action.svg) Hoist Field Action](hoist-field-action.html)

 [![http secured sink](_images/kamelets/http-secured-sink.svg) Secured HTTP Sink](http-secured-sink.html)

 [![http secured source](_images/kamelets/http-secured-source.svg) HTTP Secured Source](http-secured-source.html)

 [![http sink](_images/kamelets/http-sink.svg) HTTP Sink](http-sink.html)

 [![http source](_images/kamelets/http-source.svg) HTTP Source](http-source.html)

 [![ibm cos sink](_images/kamelets/ibm-cos-sink.svg) IBM Cloud Object Storage Sink](ibm-cos-sink.html)

 [![ibm cos source](_images/kamelets/ibm-cos-source.svg) IBM Cloud Object Storage Source](ibm-cos-source.html)

 [![ibm watson language sink](_images/kamelets/ibm-watson-language-sink.svg) IBM Watson Natural Language Understanding Sink](ibm-watson-language-sink.html)

 [![infinispan sink](_images/kamelets/infinispan-sink.svg) Infinispan Sink](infinispan-sink.html)

 [![infinispan source](_images/kamelets/infinispan-source.svg) Infinispan Source](infinispan-source.html)

 [![insert field action](_images/kamelets/insert-field-action.svg) Insert Field Action](insert-field-action.html)

 [![insert header action](_images/kamelets/insert-header-action.svg) Insert Header Action](insert-header-action.html)

 [![is tombstone filter action](_images/kamelets/is-tombstone-filter-action.svg) Is Tombstone Filter Action](is-tombstone-filter-action.html)

 [![jira add comment sink](_images/kamelets/jira-add-comment-sink.svg) Jira Add Comment Sink](jira-add-comment-sink.html)

 [![jira add issue sink](_images/kamelets/jira-add-issue-sink.svg) Jira Add Issue Sink](jira-add-issue-sink.html)

 [![jira oauth source](_images/kamelets/jira-oauth-source.svg) Jira oauth Source](jira-oauth-source.html)

 [![jira source](_images/kamelets/jira-source.svg) Jira Source](jira-source.html)

 [![jira transition issue sink](_images/kamelets/jira-transition-issue-sink.svg) Jira Transition Issue Sink](jira-transition-issue-sink.html)

 [![jira update issue sink](_images/kamelets/jira-update-issue-sink.svg) Jira Update Issue Sink](jira-update-issue-sink.html)

 [![jms amqp 10 sink](_images/kamelets/jms-amqp-10-sink.svg) JMS - AMQP 1.0 Sink](jms-amqp-10-sink.html)

 [![jms amqp 10 source](_images/kamelets/jms-amqp-10-source.svg) JMS - AMQP 1.0 Source](jms-amqp-10-source.html)

 [![jms amqp 10 ssl sink](_images/kamelets/jms-amqp-10-ssl-sink.svg) JMS - AMQP 1.0 SSL Sink](jms-amqp-10-ssl-sink.html)

 [![jms amqp 10 ssl source](_images/kamelets/jms-amqp-10-ssl-source.svg) JMS - AMQP 1.0 SSL Source](jms-amqp-10-ssl-source.html)

 [![jms apache artemis sink](_images/kamelets/jms-apache-artemis-sink.svg) JMS - Apache Artemis Sink](jms-apache-artemis-sink.html)

 [![jms apache artemis source](_images/kamelets/jms-apache-artemis-source.svg) JMS - Apache Artemis Source](jms-apache-artemis-source.html)

 [![jms ibm mq sink](_images/kamelets/jms-ibm-mq-sink.svg) JMS - IBM MQ Sink](jms-ibm-mq-sink.html)

 [![jms ibm mq source](_images/kamelets/jms-ibm-mq-source.svg) JMS - IBM MQ Source](jms-ibm-mq-source.html)

 [![jms pooled apache artemis sink](_images/kamelets/jms-pooled-apache-artemis-sink.svg) JMS Pooled - Apache Artemis Sink](jms-pooled-apache-artemis-sink.html)

 [![jms pooled apache artemis source](_images/kamelets/jms-pooled-apache-artemis-source.svg) JMS Pooled - Apache Artemis Source](jms-pooled-apache-artemis-source.html)

 [![jolt transformation action](_images/kamelets/jolt-transformation-action.svg) Jolt Transformation Action](jolt-transformation-action.html)

 [![jslt action](_images/kamelets/jslt-action.svg) JSLT Action](jslt-action.html)

 [![json deserialize action](_images/kamelets/json-deserialize-action.svg) Json Deserialize Action](json-deserialize-action.html)

 [![json patch action](_images/kamelets/json-patch-action.svg) Json Patch Action](json-patch-action.html)

 [![json schema validator action](_images/kamelets/json-schema-validator-action.svg) Json Schema Validator Action](json-schema-validator-action.html)

 [![json serialize action](_images/kamelets/json-serialize-action.svg) Json Serialize Action](json-serialize-action.html)

 [![jsonata action](_images/kamelets/jsonata-action.svg) Jsonata Action](jsonata-action.html)

 [![kafka apicurio registry not secured sink](_images/kamelets/kafka-apicurio-registry-not-secured-sink.svg) Kafka Not Secured with Apicurio Registry Sink](kafka-apicurio-registry-not-secured-sink.html)

 [![kafka apicurio registry not secured source](_images/kamelets/kafka-apicurio-registry-not-secured-source.svg) Kafka Not Secured with Apicurio Registry Source](kafka-apicurio-registry-not-secured-source.html)

 [![kafka azure schema registry sink](_images/kamelets/kafka-azure-schema-registry-sink.svg) Azure Kafka through Eventhubs with Azure Schema Registry Sink](kafka-azure-schema-registry-sink.html)

 [![kafka azure schema registry source](_images/kamelets/kafka-azure-schema-registry-source.svg) Azure Kafka through Eventhubs with Azure Schema Registry Source](kafka-azure-schema-registry-source.html)

 [![kafka batch apicurio registry not secured source](_images/kamelets/kafka-batch-apicurio-registry-not-secured-source.svg) Kafka Batch Not Secured with Apicurio Registry Source](kafka-batch-apicurio-registry-not-secured-source.html)

 [![kafka batch apicurio registry source](_images/kamelets/kafka-batch-apicurio-registry-source.svg) Kafka Batch with Apicurio Registry secured with Keycloak Source](kafka-batch-apicurio-registry-source.html)

 [![kafka batch azure schema registry source](_images/kamelets/kafka-batch-azure-schema-registry-source.svg) Azure Kafka Batch through Eventhubs with Azure Schema Registry Source](kafka-batch-azure-schema-registry-source.html)

 [![kafka batch manual commit action](_images/kamelets/kafka-batch-manual-commit-action.svg) Kafka Batch Manual Commit Action](kafka-batch-manual-commit-action.html)

 [![kafka batch source](_images/kamelets/kafka-batch-source.svg) Kafka Batch Source](kafka-batch-source.html)

 [![kafka manual commit action](_images/kamelets/kafka-manual-commit-action.svg) Kafka Manual Commit Action](kafka-manual-commit-action.html)

 [![kafka not secured apicurio registry json source](_images/kamelets/kafka-not-secured-apicurio-registry-json-source.svg) Kafka not secured with Apicurio Registry secured with Keycloak for JSON schema support Source](kafka-not-secured-apicurio-registry-json-source.html)

 [![kafka not secured apicurio registry sink](_images/kamelets/kafka-not-secured-apicurio-registry-sink.svg) Kafka Not Secured with Apicurio Registry secured with Keycloak Sink](kafka-not-secured-apicurio-registry-sink.html)

 [![kafka not secured apicurio registry source](_images/kamelets/kafka-not-secured-apicurio-registry-source.svg) Kafka not secured with Apicurio Registry secured with Keycloak Source](kafka-not-secured-apicurio-registry-source.html)

 [![kafka sink](_images/kamelets/kafka-sink.svg) Kafka Sink](kafka-sink.html)

 [![kafka source](_images/kamelets/kafka-source.svg) Kafka Source](kafka-source.html)

 [![kubernetes namespaces source](_images/kamelets/kubernetes-namespaces-source.svg) Kubernetes Namespaces Source](kubernetes-namespaces-source.html)

 [![kubernetes nodes source](_images/kamelets/kubernetes-nodes-source.svg) Kubernetes Nodes Source](kubernetes-nodes-source.html)

 [![kubernetes pods source](_images/kamelets/kubernetes-pods-source.svg) Kubernetes Pods Source](kubernetes-pods-source.html)

 [![log action](_images/kamelets/log-action.svg) Log Action](log-action.html)

 [![log sink](_images/kamelets/log-sink.svg) Log Sink](log-sink.html)

 [![mail imap source](_images/kamelets/mail-imap-source.svg) Mail IMAP Source](mail-imap-source.html)

 [![mail sink](_images/kamelets/mail-sink.svg) Mail Sink](mail-sink.html)

 [![mariadb sink](_images/kamelets/mariadb-sink.svg) MariaDB Sink](mariadb-sink.html)

 [![mariadb source](_images/kamelets/mariadb-source.svg) MariaDB Source](mariadb-source.html)

 [![mask field action](_images/kamelets/mask-field-action.svg) Mask Fields Action](mask-field-action.html)

 [![message timestamp router action](_images/kamelets/message-timestamp-router-action.svg) Message Timestamp Router Action](message-timestamp-router-action.html)

 [![minio sink](_images/kamelets/minio-sink.svg) Minio Sink](minio-sink.html)

 [![minio source](_images/kamelets/minio-source.svg) Minio Source](minio-source.html)

 [![mongodb changes stream source](_images/kamelets/mongodb-changes-stream-source.svg) MongoDB Changes Stream Source](mongodb-changes-stream-source.html)

 [![mongodb sink](_images/kamelets/mongodb-sink.svg) MongoDB Sink](mongodb-sink.html)

 [![mongodb source](_images/kamelets/mongodb-source.svg) MongoDB Source](mongodb-source.html)

 [![mqtt sink](_images/kamelets/mqtt-sink.svg) MQTT Sink](mqtt-sink.html)

 [![mqtt source](_images/kamelets/mqtt-source.svg) MQTT Source](mqtt-source.html)

 [![mqtt5 sink](_images/kamelets/mqtt5-sink.svg) MQTT v5 Sink](mqtt5-sink.html)

 [![mqtt5 source](_images/kamelets/mqtt5-source.svg) MQTT 5 Source](mqtt5-source.html)

 [![ms exchange online imap oauth source](_images/kamelets/ms-exchange-online-imap-oauth-source.svg) Microsoft Exchange IMAP OAuth2 Source](ms-exchange-online-imap-oauth-source.html)

 [![mustache template action](_images/kamelets/mustache-template-action.svg) Mustache Template Action](mustache-template-action.html)

 [![mvel template action](_images/kamelets/mvel-template-action.svg) Mvel Template Action](mvel-template-action.html)

 [![mysql sink](_images/kamelets/mysql-sink.svg) MySQL Sink](mysql-sink.html)

 [![mysql source](_images/kamelets/mysql-source.svg) MySQL Source](mysql-source.html)

 [![nats sink](_images/kamelets/nats-sink.svg) NATS Sink](nats-sink.html)

 [![nats source](_images/kamelets/nats-source.svg) NATS Source](nats-source.html)

 [![nominatim geocode action](_images/kamelets/nominatim-geocode-action.svg) Nominatim GeoCode Action](nominatim-geocode-action.html)

 [![ogcapi features action](_images/kamelets/ogcapi-features-action.svg) OGC Api Feature Get Item Action](ogcapi-features-action.html)

 [![opensearch index sink](_images/kamelets/opensearch-index-sink.svg) OpenSearch Index Sink](opensearch-index-sink.html)

 [![opensearch search source](_images/kamelets/opensearch-search-source.svg) OpenSearch Search Source](opensearch-search-source.html)

 [![oracle database sink](_images/kamelets/oracle-database-sink.svg) Oracle Database Sink](oracle-database-sink.html)

 [![oracle database source](_images/kamelets/oracle-database-source.svg) Oracle Database Source](oracle-database-source.html)

 [![pdf action](_images/kamelets/pdf-action.svg) PDF Action](pdf-action.html)

 [![postgresql sink](_images/kamelets/postgresql-sink.svg) PostgreSQL Sink](postgresql-sink.html)

 [![postgresql source](_images/kamelets/postgresql-source.svg) PostgreSQL Source](postgresql-source.html)

 [![pqc kem action](_images/kamelets/pqc-kem-action.svg) PQC Key Encapsulation/Decapsulation Action](pqc-kem-action.html)

 [![pqc signature action](_images/kamelets/pqc-signature-action.svg) PQC Signature Action](pqc-signature-action.html)

 [![predicate filter action](_images/kamelets/predicate-filter-action.svg) Predicate Filter Action](predicate-filter-action.html)

 [![protobuf deserialize action](_images/kamelets/protobuf-deserialize-action.svg) Protobuf Deserialize Action](protobuf-deserialize-action.html)

 [![protobuf serialize action](_images/kamelets/protobuf-serialize-action.svg) Protobuf Serialize Action](protobuf-serialize-action.html)

 [![pulsar sink](_images/kamelets/pulsar-sink.svg) Pulsar Sink](pulsar-sink.html)

 [![pulsar source](_images/kamelets/pulsar-source.svg) Pulsar Source](pulsar-source.html)

 [![redis sink](_images/kamelets/redis-sink.svg) Redis Sink](redis-sink.html)

 [![redis source](_images/kamelets/redis-source.svg) Redis Source](redis-source.html)

 [![regex router action](_images/kamelets/regex-router-action.svg) Regex Router Action](regex-router-action.html)

 [![replace field action](_images/kamelets/replace-field-action.svg) Replace Field Action](replace-field-action.html)

 [![resolve pojo schema action](_images/kamelets/resolve-pojo-schema-action.svg) Resolve Schema Action](resolve-pojo-schema-action.html)

 [![rest openapi sink](_images/kamelets/rest-openapi-sink.svg) REST OpenAPI Sink](rest-openapi-sink.html)

 [![salesforce composite upsert sink](_images/kamelets/salesforce-composite-upsert-sink.svg) Salesforce composite upsert Sink](salesforce-composite-upsert-sink.html)

 [![salesforce create sink](_images/kamelets/salesforce-create-sink.svg) Salesforce Create Sink](salesforce-create-sink.html)

 [![salesforce delete sink](_images/kamelets/salesforce-delete-sink.svg) Salesforce Delete Sink](salesforce-delete-sink.html)

 [![salesforce source](_images/kamelets/salesforce-source.svg) Salesforce Source](salesforce-source.html)

 [![salesforce update sink](_images/kamelets/salesforce-update-sink.svg) Salesforce Update Sink](salesforce-update-sink.html)

 [![scp sink](_images/kamelets/scp-sink.svg) SCP Sink](scp-sink.html)

 [![set body action](_images/kamelets/set-body-action.svg) Set Body Action](set-body-action.html)

 [![set kafka key action](_images/kamelets/set-kafka-key-action.svg) Set Kafka Key Action](set-kafka-key-action.html)

 [![sftp sink](_images/kamelets/sftp-sink.svg) SFTP Sink](sftp-sink.html)

 [![sftp source](_images/kamelets/sftp-source.svg) SFTP Source](sftp-source.html)

 [![simple filter action](_images/kamelets/simple-filter-action.svg) Simple Filter Action](simple-filter-action.html)

 [![slack sink](_images/kamelets/slack-sink.svg) Slack Sink](slack-sink.html)

 [![slack source](_images/kamelets/slack-source.svg) Slack Source](slack-source.html)

 [![snowflake sink](_images/kamelets/snowflake-sink.svg) Snowflake Sink](snowflake-sink.html)

 [![snowflake source](_images/kamelets/snowflake-source.svg) Snowflake Source](snowflake-source.html)

 [![solr sink](_images/kamelets/solr-sink.svg) Solr Sink](solr-sink.html)

 [![solr source](_images/kamelets/solr-source.svg) Solr Source](solr-source.html)

 [![splunk hec sink](_images/kamelets/splunk-hec-sink.svg) Splunk HEC Sink](splunk-hec-sink.html)

 [![splunk sink](_images/kamelets/splunk-sink.svg) Splunk Sink](splunk-sink.html)

 [![splunk source](_images/kamelets/splunk-source.svg) Splunk Source](splunk-source.html)

 [![spring rabbitmq sink](_images/kamelets/spring-rabbitmq-sink.svg) RabbitMQ Sink](spring-rabbitmq-sink.html)

 [![spring rabbitmq source](_images/kamelets/spring-rabbitmq-source.svg) RabbitMQ Source](spring-rabbitmq-source.html)

 [![sqlserver sink](_images/kamelets/sqlserver-sink.svg) Microsoft SQL Server Sink](sqlserver-sink.html)

 [![sqlserver source](_images/kamelets/sqlserver-source.svg) Microsoft SQL Server Source](sqlserver-source.html)

 [![ssh sink](_images/kamelets/ssh-sink.svg) SSH Sink](ssh-sink.html)

 [![ssh source](_images/kamelets/ssh-source.svg) SSH Source](ssh-source.html)

 [![string template action](_images/kamelets/string-template-action.svg) String Template Action](string-template-action.html)

 [![telegram sink](_images/kamelets/telegram-sink.svg) Telegram Sink](telegram-sink.html)

 [![telegram source](_images/kamelets/telegram-source.svg) Telegram Source](telegram-source.html)

 [![throttle action](_images/kamelets/throttle-action.svg) Throttle Action](throttle-action.html)

 [![timer source](_images/kamelets/timer-source.svg) Timer Source](timer-source.html)

 [![timestamp router action](_images/kamelets/timestamp-router-action.svg) Timestamp Router Action](timestamp-router-action.html)

 [![topic name matches filter action](_images/kamelets/topic-name-matches-filter-action.svg) Kafka Topic Name Matches Filter Action](topic-name-matches-filter-action.html)

 [![twitter directmessage source](_images/kamelets/twitter-directmessage-source.svg) Twitter Direct Message Source](twitter-directmessage-source.html)

 [![twitter search source](_images/kamelets/twitter-search-source.svg) Twitter Search Source](twitter-search-source.html)

 [![twitter timeline source](_images/kamelets/twitter-timeline-source.svg) Twitter Timeline Source](twitter-timeline-source.html)

 [![value to key action](_images/kamelets/value-to-key-action.svg) Value to Key Action](value-to-key-action.html)

 [![velocity template action](_images/kamelets/velocity-template-action.svg) Velocity Template Action](velocity-template-action.html)

 [![webhook source](_images/kamelets/webhook-source.svg) Webhook Source](webhook-source.html)

 [![wttrin source](_images/kamelets/wttrin-source.svg) wttr.in Source](wttrin-source.html)

 [![xj identity action](_images/kamelets/xj-identity-action.svg) XJ Identity Action](xj-identity-action.html)

 [![xj template action](_images/kamelets/xj-template-action.svg) XJ Template Action](xj-template-action.html)

[Kamelets Developer Guide](development.md)