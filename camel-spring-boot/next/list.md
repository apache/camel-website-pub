# Component Starters

There are unused json files.

## Statistics

If this section appears in the (failed) website build, there is a mismatch between the camel spring boot starter json files, which are used to generate the spring-boot section of main camel component documentation, and the names used in those main camel component documentation pages. The names of the unused spring boot starter json files are listed below. Each of these needs to be used in a component doc page as the `camel-spring-boot-name` header attribute, like this:

```adoc
:camel-spring-boot-name: springdoc
```

There are 399 spring boot starter json files.

Of these 395 are used in components, dataformats, etc.

> **Note**
> Cluster service starters (consul, file, infinispan, jgroups-raft, kubernetes, zookeeper) are documented in the [Cluster Services](#_cluster_services) section below.

### Unused spring-boot-starter names

azure-eventgrid

consul-cluster-service

file-cluster-service

huggingface

infinispan-cluster-service

jackson3-avro

jackson3-protobuf

jackson3

jackson3xml

jgroups-raft-cluster-service

kubernetes-cluster-service

zookeeper-cluster-service

## Camel Spring Boot

Apache Camel Spring Boot supports the following Camel artifacts as Spring Boot Starters

## Camel Components

Number of Camel components: 390 in 324 JAR artifacts (10 deprecated)

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [ActiveMQ 5.x](../../components/next/activemq-component.md) | camel-activemq-starter | Stable | 1.0 | Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component. |
| [ActiveMQ 6.x](../../components/next/activemq6-component.md) | camel-activemq6-starter | Stable | 4.7 | Send messages to (or consume from) Apache ActiveMQ 6.x. This component extends the Camel JMS component. |
| [AMQP](../../components/next/amqp-component.md) | camel-amqp-starter | Stable | 1.2 | Messaging with AMQP protocol using Apache QPid Client. |
| [ArangoDb](../../components/next/arangodb-component.md) | camel-arangodb-starter | Stable | 3.5 | Perform operations on ArangoDb when used as a Document Database, or as a Graph Database |
| [AS2](../../components/next/as2-component.md) | camel-as2-starter | Stable | 2.22 | Transfer data securely and reliably using the AS2 protocol (RFC4130). |
| [Asterisk](../../components/next/asterisk-component.md) | camel-asterisk-starter | Stable | 2.18 | Interact with Asterisk PBX Server (VoIP). |
| [Atmosphere Websocket](../../components/next/atmosphere-websocket-component.md) | camel-atmosphere-websocket-starter | Stable | 2.14 | Expose WebSocket endpoints using the Atmosphere framework. |
| [Atom](../../components/next/atom-component.md) | camel-atom-starter | Stable | 1.2 | Poll Atom RSS feeds. |
| [Avro RPC](../../components/next/avro-component.md) | camel-avro-rpc-starter | Stable | 2.10 | Produce or consume Apache Avro RPC services. |
| [AWS Athena](../../components/next/aws2-athena-component.md) | camel-aws2-athena-starter | Stable | 3.4 | Access AWS Athena. |
| [AWS Bedrock](../../components/next/aws-bedrock-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Invoke Model of AWS Bedrock service. |
| [AWS Bedrock Agent](../../components/next/aws-bedrock-agent-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Operate on AWS Bedrock through its Agent. |
| [AWS Bedrock Agent Runtime](../../components/next/aws-bedrock-agent-runtime-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Invoke Model of AWS Bedrock Agent Runtime service. |
| [AWS Cloudtrail](../../components/next/aws-cloudtrail-component.md) | camel-aws-cloudtrail-starter | Stable | 3.19 | Consume events from Amazon Cloudtrail using AWS SDK version 2.x. |
| [AWS CloudWatch](../../components/next/aws2-cw-component.md) | camel-aws2-cw-starter | Stable | 3.1 | Sending metrics to AWS CloudWatch. |
| [AWS Comprehend](../../components/next/aws2-comprehend-component.md) | camel-aws2-comprehend-starter | Preview | 4.18 | Perform natural language processing using AWS Comprehend and AWS SDK version 2.x. |
| [AWS Config Service](../../components/next/aws-config-component.md) | camel-aws-config-starter | Stable | 4.3 | Manage AWS Config service. |
| [AWS DynamoDB](../../components/next/aws2-ddb-component.md) | camel-aws2-ddb-starter | Stable | 3.1 | Store and retrieve data from AWS DynamoDB. |
| [AWS DynamoDB Streams](../../components/next/aws2-ddbstream-component.md) | camel-aws2-ddb-starter | Stable | 3.1 | Receive messages from AWS DynamoDB Stream. |
| [AWS Elastic Compute Cloud (EC2)](../../components/next/aws2-ec2-component.md) | camel-aws2-ec2-starter | Stable | 3.1 | Manage AWS EC2 instances. |
| [AWS Elastic Container Service (ECS)](../../components/next/aws2-ecs-component.md) | camel-aws2-ecs-starter | Stable | 3.1 | Manage AWS ECS cluster instances. |
| [AWS Elastic Kubernetes Service (EKS)](../../components/next/aws2-eks-component.md) | camel-aws2-eks-starter | Stable | 3.1 | Manage AWS EKS cluster instances. |
| [AWS Eventbridge](../../components/next/aws2-eventbridge-component.md) | camel-aws2-eventbridge-starter | Stable | 3.6 | Manage AWS EventBridge cluster instances and consume events via SQS-backed polling. |
| [AWS Identity and Access Management (IAM)](../../components/next/aws2-iam-component.md) | camel-aws2-iam-starter | Stable | 3.1 | Manage AWS IAM instances. |
| [AWS Key Management Service (KMS)](../../components/next/aws2-kms-component.md) | camel-aws2-kms-starter | Stable | 3.1 | Manage keys stored in AWS KMS instances. |
| [AWS Kinesis](../../components/next/aws2-kinesis-component.md) | camel-aws2-kinesis-starter | Stable | 3.2 | Consume and produce records from and to AWS Kinesis Streams. |
| [AWS Kinesis Firehose](../../components/next/aws2-kinesis-firehose-component.md) | camel-aws2-kinesis-starter | Stable | 3.2 | Produce data to AWS Kinesis Firehose streams. |
| [AWS Lambda](../../components/next/aws2-lambda-component.md) | camel-aws2-lambda-starter | Stable | 3.2 | Manage and invoke AWS Lambda functions. |
| [AWS Managed Streaming for Apache Kafka (MSK)](../../components/next/aws2-msk-component.md) | camel-aws2-msk-starter | Stable | 3.1 | Manage AWS MSK instances. |
| [AWS MQ](../../components/next/aws2-mq-component.md) | camel-aws2-mq-starter | Stable | 3.1 | Send messages to AWS MQ. |
| [AWS Parameter Store](../../components/next/aws-parameter-store-component.md) | camel-aws-parameter-store-starter | Stable | 4.17 | Manage parameters using AWS Systems Manager (SSM) Parameter Store. |
| [AWS Polly](../../components/next/aws2-polly-component.md) | camel-aws2-polly-starter | Preview | 4.18 | Synthesize speech using AWS Polly and AWS SDK version 2.x. |
| [AWS RedshiftData](../../components/next/aws2-redshift-data-component.md) | camel-aws2-redshift-starter | Stable | 4.1 | Perform operations on AWS Redshift using Redshift Data API. |
| [AWS Rekognition](../../components/next/aws2-rekognition-component.md) | camel-aws2-rekognition-starter | Stable | 4.17 | Manage and invoke AWS Rekognition. |
| [AWS S3 Storage Service](../../components/next/aws2-s3-component.md) | camel-aws2-s3-starter | Stable | 3.2 | Store and retrieve objects from AWS S3 Storage Service. |
| [AWS S3 Vectors](../../components/next/aws2-s3-vectors-component.md) | camel-aws2-s3-vectors-starter | Stable | 4.17 | Store and query vector embeddings using AWS S3 Vectors with similarity search. |
| [AWS Secrets Manager](../../components/next/aws-secrets-manager-component.md) | camel-aws-secrets-manager-starter | Stable | 3.9 | Manage secrets using AWS Secrets Manager. |
| [AWS Security Hub](../../components/next/aws-security-hub-component.md) | camel-aws-security-hub-starter | Preview | 4.18 | Manage and interact with AWS Security Hub for security findings. |
| [AWS Security Token Service (STS)](../../components/next/aws2-sts-component.md) | camel-aws2-sts-starter | Stable | 3.5 | Manage AWS STS cluster instances. |
| [AWS Simple Email Service (SES)](../../components/next/aws2-ses-component.md) | camel-aws2-ses-starter | Stable | 3.1 | Send e-mails through AWS SES service. |
| [AWS Simple Notification System (SNS)](../../components/next/aws2-sns-component.md) | camel-aws2-sns-starter | Stable | 3.1 | Send messages to AWS Simple Notification Topic. |
| [AWS Simple Queue Service (SQS)](../../components/next/aws2-sqs-component.md) | camel-aws2-sqs-starter | Stable | 3.1 | Send and receive messages to/from AWS SQS. |
| [AWS StepFunctions](../../components/next/aws2-step-functions-component.md) | camel-aws2-step-functions-starter | Stable | 4.0 | Manage and invoke AWS Step functions. |
| [AWS Textract](../../components/next/aws2-textract-component.md) | camel-aws2-textract-starter | Stable | 4.15 | Extract text and data from documents using AWS Textract and AWS SDK version 2.x. |
| [AWS Timestream](../../components/next/aws2-timestream-component.md) | camel-aws2-timestream-starter | Stable | 4.1 | Write records and execute queries on AWS time-series database |
| [AWS Transcribe](../../components/next/aws2-transcribe-component.md) | camel-aws2-transcribe-starter | Stable | 4.15 | Automatically convert speech to text using AWS Transcribe service |
| [AWS Translate](../../components/next/aws2-translate-component.md) | camel-aws2-translate-starter | Stable | 3.1 | Translate texts using AWS Translate and AWS SDK version 2.x. |
| [Azure CosmosDB](../../components/next/azure-cosmosdb-component.md) | camel-azure-cosmosdb-starter | Stable | 3.10 | To read and write records to the CosmosDB database on Azure cloud platform. |
| [Azure Event Hubs](../../components/next/azure-eventhubs-component.md) | camel-azure-eventhubs-starter | Stable | 3.5 | Send and receive events to/from Azure Event Hubs using AMQP protocol. |
| [Azure Files](../../components/next/azure-files-component.md) | camel-azure-files-starter | Preview | 3.22 | Send and receive files to Azure storage file share |
| [Azure Functions](../../components/next/azure-functions-component.md) | camel-azure-functions-starter | Preview | 4.19 | Invoke and manage Azure Functions. |
| [Azure Key Vault](../../components/next/azure-key-vault-component.md) | camel-azure-key-vault-starter | Stable | 3.17 | Manage secrets and keys in Azure Key Vault Service |
| [Azure ServiceBus](../../components/next/azure-servicebus-component.md) | camel-azure-servicebus-starter | Stable | 3.12 | Send and receive messages to/from Azure Service Bus. |
| [Azure Storage Blob Service](../../components/next/azure-storage-blob-component.md) | camel-azure-storage-blob-starter | Stable | 3.3 | Store and retrieve blobs from Azure Storage Blob Service. |
| [Azure Storage Data Lake Service](../../components/next/azure-storage-datalake-component.md) | camel-azure-storage-datalake-starter | Stable | 3.8 | Sends and receives files to/from Azure Data Lake Storage. |
| [Azure Storage Queue Service](../../components/next/azure-storage-queue-component.md) | camel-azure-storage-queue-starter | Stable | 3.3 | Stores and retrieves messages to/from Azure Storage Queue. |
| [Bean](../../components/next/bean-component.md) | camel-bean-starter | Stable | 1.0 | Invoke methods of Java beans stored in Camel registry. |
| [Bean Validator](../../components/next/bean-validator-component.md) | camel-bean-validator-starter | Stable | 2.3 | Validate the message body using the Java Bean Validation API. |
| [Bonita](../../components/next/bonita-component.md) | camel-bonita-starter | Stable | 2.19 | Communicate with a remote Bonita BPM process engine. |
| [Box](../../components/next/box-component.md) | camel-box-starter | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc. on box.com. |
| [Braintree](../../components/next/braintree-component.md) | camel-braintree-starter | Stable | 2.17 | Process payments using Braintree Payments. |
| [Browse](../../components/next/browse-component.md) | camel-browse-starter | Stable | 1.3 | Inspect the messages received on endpoints supporting BrowsableEndpoint. |
| [Caffeine Cache](../../components/next/caffeine-cache-component.md) | camel-caffeine-starter | Stable | 2.20 | Perform caching operations using Caffeine Cache. |
| [Caffeine LoadCache](../../components/next/caffeine-loadcache-component.md) | camel-caffeine-starter | Stable | 2.20 | Perform caching operations using Caffeine Cache with an attached CacheLoader. |
| [Camunda](../../components/next/camunda-component.md) | camel-camunda-starter | Preview | 4.19 | Interact with Camunda 8 Orchestration Clusters using the Camunda Java Client. |
| [Cassandra CQL](../../components/next/cql-component.md) | camel-cassandraql-starter | Stable | 2.15 | Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax. |
| [ChatScript](../../components/next/chatscript-component.md) | camel-chatscript-starter | Stable | 3.0 | Chat with a ChatScript Server. |
| [Chunk](../../components/next/chunk-component.md) | camel-chunk-starter | Stable | 2.15 | Transform messages using Chunk templating engine. |
| [Class](../../components/next/class-component.md) | camel-bean-starter | Stable | 2.4 | Invoke methods of Java beans specified by class name. |
| [ClickUp](../../components/next/clickup-component.md) | camel-clickup-starter | Preview | 4.9 | Receives events from ClickUp |
| [CM SMS Gateway](../../components/next/cm-sms-component.md) | camel-cm-sms-starter | Stable | 2.18 | Send SMS messages via CM SMS Gateway. |
| [CoAP](../../components/next/coap-component.md) | camel-coap-starter | Stable | 2.16 | Send and receive messages to/from CoAP (Constrained Application Protocol) capable devices. |
| [CometD](../../components/next/cometd-component.md) | camel-cometd-starter | Stable | 2.0 | Offers publish/subscribe, peer-to-peer (via a server), and RPC style messaging using the CometD/Bayeux protocol. |
| [Consul](../../components/next/consul-component.md) | camel-consul-starter | Stable | 2.18 | Integrate with Consul service discovery and configuration store. |
| [Control Bus](../../components/next/controlbus-component.md) | camel-controlbus-starter | Stable | 2.11 | Manage and monitor Camel routes. |
| [Couchbase](../../components/next/couchbase-component.md) | camel-couchbase-starter | Stable | 2.19 | Query Couchbase databases using SQL (N1QL) queries or MapReduce Views with a poll strategy and/or perform various operations against Couchbase databases. |
| [CouchDB](../../components/next/couchdb-component.md) | camel-couchdb-starter | Stable | 2.11 | Consume changesets for inserts, updates and deletes in a CouchDB database, as well as get, save, update and delete documents from a CouchDB database. |
| [Cron](../../components/next/cron-component.md) | camel-cron-starter | Stable | 3.1 | A generic interface for triggering events at times specified through the Unix cron syntax. |
| [Crypto (JCE)](../../components/next/crypto-component.md) | camel-crypto-starter | Stable | 2.3 | Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE). |
| [CXF](../../components/next/cxf-component.md) | camel-cxf-soap-starter | Stable | 1.0 | Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client. |
| [CXF-RS](../../components/next/cxfrs-component.md) | camel-cxf-rest-starter | Stable | 2.0 | Expose JAX-RS REST services using Apache CXF or connect to external REST services using CXF REST client. |
| [CyberArk Vault](../../components/next/cyberark-vault-component.md) | camel-cyberark-vault-starter | Stable | 4.17 | Retrieve secrets from CyberArk Conjur Vault. |
| [Dapr](../../components/next/dapr-component.md) | camel-dapr-starter | Stable | 4.12 | Dapr component which interfaces with Dapr Building Blocks. |
| [Data Format](../../components/next/dataformat-component.md) | camel-dataformat-starter | Stable | 2.12 | Use a Camel Data Format as a regular Camel Component. |
| [Dataset](../../components/next/dataset-component.md) | camel-dataset-starter | Stable | 1.3 | Provide data for load and soak testing of your Camel application. |
| [DataSet Test](../../components/next/dataset-test-component.md) | camel-dataset-starter | Stable | 1.3 | Extends the mock component by pulling messages from another endpoint on startup to set the expected message bodies. |
| [Debezium DB2 Connector](../../components/next/debezium-db2-component.md) | camel-debezium-db2-starter | Stable | 3.17 | Capture changes from a DB2 database. |
| [Debezium MongoDB Connector](../../components/next/debezium-mongodb-component.md) | camel-debezium-mongodb-starter | Stable | 3.0 | Capture changes from a MongoDB database. |
| [Debezium MySQL Connector](../../components/next/debezium-mysql-component.md) | camel-debezium-mysql-starter | Stable | 3.0 | Capture changes from a MySQL database. |
| [Debezium Oracle Connector](../../components/next/debezium-oracle-component.md) | camel-debezium-oracle-starter | Stable | 3.17 | Capture changes from an Oracle database. |
| [Debezium PostgresSQL Connector](../../components/next/debezium-postgres-component.md) | camel-debezium-postgres-starter | Stable | 3.0 | Capture changes from a PostgresSQL database. |
| [Debezium SQL Server Connector](../../components/next/debezium-sqlserver-component.md) | camel-debezium-sqlserver-starter | Stable | 3.0 | Capture changes from an SQL Server database. |
| [Deep Java Library](../../components/next/djl-component.md) | camel-djl-starter | Stable | 3.3 | Infer Deep Learning models from message exchanges data using Deep Java Library (DJL). |
| [DFDL](../../components/next/dfdl-component.md) | camel-dfdl-starter | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [DHIS2](../../components/next/dhis2-component.md) | camel-dhis2-starter | Stable | 4.0 | Leverages the DHIS2 Java SDK to integrate Apache Camel with the DHIS2 Web API. |
| [DigitalOcean](../../components/next/digitalocean-component.md) | camel-digitalocean-starter | Stable | 2.19 | Manage Droplets and resources within the DigitalOcean cloud. |
| [Direct](../../components/next/direct-component.md) | camel-direct-starter | Stable | 1.0 | Call another endpoint from the same Camel Context synchronously. |
| [Disruptor](../../components/next/disruptor-component.md) | camel-disruptor-starter | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [Disruptor VM](../../components/next/disruptor-vm-component.md) | camel-disruptor-starter | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [DNS](../../components/next/dns-component.md) | camel-dns-starter | Stable | 2.7 | Perform DNS queries using DNSJava. |
| [Docker](../../components/next/docker-component.md) | camel-docker-starter | Stable | 2.15 | Manage Docker containers. |
| [Docling](../../components/next/docling-component.md) | camel-docling-starter | Stable | 4.15 | Process documents using Docling library for parsing and conversion. |
| [Drill](../../components/next/drill-component.md) | camel-drill-starter | Stable | 2.19 | Perform queries against an Apache Drill cluster. |
| [Dropbox](../../components/next/dropbox-component.md) | camel-dropbox-starter | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc on Dropbox. |
| [Dynamic Router](../../components/next/dynamic-router-component.md) | camel-dynamic-router-starter | Stable | 3.15 | The Dynamic Router component routes exchanges to recipients, and the recipients (and their rules) may change at runtime. |
| [Dynamic Router Control](../../components/next/dynamic-router-control-component.md) | camel-dynamic-router-starter | Stable | 4.4 | The Dynamic Router control endpoint for operations that allow routing participants to subscribe or unsubscribe to participate in dynamic message routing. |
| [Ehcache](../../components/next/ehcache-component.md) | camel-ehcache-starter | Stable | 2.18 | Perform caching operations using Ehcache. |
| [Elasticsearch](../../components/next/elasticsearch-component.md) | camel-elasticsearch-starter | Stable | 3.19 | Send requests to ElasticSearch via Java Client API. |
| [Elasticsearch Low level Rest Client](../../components/next/elasticsearch-rest-client-component.md) | camel-elasticsearch-rest-client-starter | Stable | 4.3 | Perform queries and other operations on Elasticsearch or OpenSearch (uses low-level client). |
| [Event](../../components/next/event-component.md) | camel-event-starter | Preview | 4.19 | Subscribe to Camel internal events such as route started/stopped and exchange completed/failed. |
| [Exec](../../components/next/exec-component.md) | camel-exec-starter | Stable | 2.3 | Execute commands on the underlying operating system. |
| [FHIR](../../components/next/fhir-component.md) | camel-fhir-starter | Stable | 2.23 | Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. |
| [File](../../components/next/file-component.md) | camel-file-starter | Stable | 1.0 | Read and write files. |
| [File Watch](../../components/next/file-watch-component.md) | camel-file-watch-starter | Stable | 3.0 | Get notified about file events in a directory using java.nio.file.WatchService. |
| [Flatpack](../../components/next/flatpack-component.md) | camel-flatpack-starter | Stable | 1.4 | Parse fixed width and delimited files using the FlatPack library. |
| [Flink](../../components/next/flink-component.md) | camel-flink-starter | Stable | 2.18 | Send DataSet jobs to an Apache Flink cluster. |
| [Flowable](../../components/next/flowable-component.md) | camel-flowable-starter | Stable | 4.9 | Send and receive messages from the Flowable BPMN and CMMN engines. |
| [FOP](../../components/next/fop-component.md) | camel-fop-starter | Stable | 2.10 | Render messages into PDF and other output formats supported by Apache FOP. |
| [Freemarker](../../components/next/freemarker-component.md) | camel-freemarker-starter | Stable | 2.10 | Transform messages using FreeMarker templates. |
| [FTP](../../components/next/ftp-component.md) | camel-ftp-starter | Stable | 1.1 | Upload and download files to/from FTP servers. |
| [FTPS](../../components/next/ftps-component.md) | camel-ftp-starter | Stable | 2.2 | Upload and download files to/from FTP servers supporting the FTPS protocol. |
| [Geocoder](../../components/next/geocoder-component.md) | camel-geocoder-starter | Stable | 2.12 | Find geocodes (latitude and longitude) for a given address or the other way round. |
| [Git](../../components/next/git-component.md) | camel-git-starter | Stable | 2.16 | Perform operations on git repositories. |
| [GitHub](../../components/next/github-component.md) | camel-github-starter | Stable-deprecated | 2.15 | Interact with the GitHub API. |
| [GitHub2](../../components/next/github2-component.md) | camel-github2-starter | Preview | 4.18 | Interact with the GitHub API. |
| [Google BigQuery](../../components/next/google-bigquery-component.md) | camel-google-bigquery-starter | Stable | 2.20 | Google BigQuery data warehouse for analytics. |
| [Google BigQuery Standard SQL](../../components/next/google-bigquery-sql-component.md) | camel-google-bigquery-starter | Stable | 2.23 | Access Google Cloud BigQuery service using SQL queries. |
| [Google Calendar](../../components/next/google-calendar-component.md) | camel-google-calendar-starter | Stable | 2.15 | Perform various operations on a Google Calendar. |
| [Google Calendar Stream](../../components/next/google-calendar-stream-component.md) | camel-google-calendar-starter | Stable | 2.23 | Poll for changes in a Google Calendar. |
| [Google Cloud Functions](../../components/next/google-functions-component.md) | camel-google-functions-starter | Stable | 3.9 | Manage and invoke Google Cloud Functions |
| [Google Cloud Speech To Text](../../components/next/google-speech-to-text-component.md) | camel-google-speech-to-text-starter | Preview | 4.19 | Transcribe audio to text using Google Cloud Speech-to-Text API |
| [Google Cloud Text To Speech](../../components/next/google-text-to-speech-component.md) | camel-google-text-to-speech-starter | Preview | 4.19 | Synthesize speech from text using the Google Cloud Text-to-Speech API |
| [Google Cloud Vision](../../components/next/google-vision-component.md) | camel-google-vision-starter | Preview | 4.19 | Detect labels, text, faces, logos and more on images through Google Cloud Vision API |
| [Google Drive](../../components/next/google-drive-component.md) | camel-google-drive-starter | Stable | 2.14 | Manage files in Google Drive. |
| [Google Firestore](../../components/next/google-firestore-component.md) | camel-google-firestore-starter | Preview | 4.19 | Store and retrieve data from Google Cloud Firestore NoSQL database. |
| [Google Mail](../../components/next/google-mail-component.md) | camel-google-mail-starter | Stable | 2.15 | Manage messages in Google Mail. |
| [Google Mail Stream](../../components/next/google-mail-stream-component.md) | camel-google-mail-starter | Stable | 2.22 | Poll for incoming messages in Google Mail. |
| [Google Pubsub](../../components/next/google-pubsub-component.md) | camel-google-pubsub-starter | Stable | 2.19 | Send and receive messages to/from Google Cloud Platform PubSub Service. |
| [Google Secret Manager](../../components/next/google-secret-manager-component.md) | camel-google-secret-manager-starter | Stable | 3.16 | Manage Google Secret Manager Secrets |
| [Google Sheets](../../components/next/google-sheets-component.md) | camel-google-sheets-starter | Stable | 2.23 | Manage spreadsheets in Google Sheets. |
| [Google Sheets Stream](../../components/next/google-sheets-stream-component.md) | camel-google-sheets-starter | Stable | 2.23 | Poll for changes in Google Sheets. |
| [Google Storage](../../components/next/google-storage-component.md) | camel-google-storage-starter | Stable | 3.9 | Store and retrieve objects from Google Cloud Storage Service using the google-cloud-storage library. |
| [Google Vertex AI](../../components/next/google-vertexai-component.md) | camel-google-vertexai-starter | Stable | 4.17 | Interact with Google Cloud Vertex AI generative models. |
| [Grape](../../components/next/grape-component.md) | camel-grape-starter | Stable-deprecated | 2.16 | Fetch, load and manage additional jars dynamically after Camel Context was started. |
| [GraphQL](../../components/next/graphql-component.md) | camel-graphql-starter | Stable | 3.0 | Send GraphQL queries and mutations to external systems. |
| [gRPC](../../components/next/grpc-component.md) | camel-grpc-starter | Stable | 2.19 | Expose gRPC endpoints and access external gRPC endpoints. |
| [Guava EventBus](../../components/next/guava-eventbus-component.md) | camel-guava-eventbus-starter | Stable-deprecated | 2.10 | Send and receive messages to/from Guava EventBus. |
| [Hashicorp Vault](../../components/next/hashicorp-vault-component.md) | camel-hashicorp-vault-starter | Stable | 3.18 | Manage secrets in Hashicorp Vault Service |
| [Hazelcast Atomic Number](../../components/next/hazelcast-atomicvalue-component.md) | camel-hazelcast-starter | Stable-deprecated | 2.7 | Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number). |
| [Hazelcast Instance](../../components/next/hazelcast-instance-component.md) | camel-hazelcast-starter | Stable | 2.7 | Consume join/leave events of a cache instance in a Hazelcast cluster. |
| [Hazelcast List](../../components/next/hazelcast-list-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed list. |
| [Hazelcast Map](../../components/next/hazelcast-map-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed map. |
| [Hazelcast Multimap](../../components/next/hazelcast-multimap-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed multimap. |
| [Hazelcast PN Counter](../../components/next/hazelcast-pncounter-component.md) | camel-hazelcast-starter | Preview | 4.19 | Increment, decrement, get, etc. operations on a Hazelcast PN Counter (CRDT counter). |
| [Hazelcast Queue](../../components/next/hazelcast-queue-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed queue. |
| [Hazelcast Replicated Map](../../components/next/hazelcast-replicatedmap-component.md) | camel-hazelcast-starter | Stable | 2.16 | Perform operations on Hazelcast replicated map. |
| [Hazelcast Ringbuffer](../../components/next/hazelcast-ringbuffer-component.md) | camel-hazelcast-starter | Stable | 2.16 | Perform operations on Hazelcast distributed ringbuffer. |
| [Hazelcast SEDA](../../components/next/hazelcast-seda-component.md) | camel-hazelcast-starter | Stable | 2.7 | Asynchronously send/receive Exchanges between Camel routes running on potentially distinct JVMs/hosts backed by Hazelcast BlockingQueue. |
| [Hazelcast Set](../../components/next/hazelcast-set-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed set. |
| [Hazelcast Topic](../../components/next/hazelcast-topic-component.md) | camel-hazelcast-starter | Stable | 2.15 | Send and receive messages to/from Hazelcast distributed topic. |
| [HTTP](../../components/next/http-component.md) | camel-http-starter | Stable | 2.3 | Send requests to external HTTP servers using Apache HTTP Client 5.x. |
| [Huawei Cloud Face Recognition Service (FRS)](../../components/next/hwcloud-frs-component.md) | camel-huaweicloud-frs-starter | Stable | 3.15 | Face Recognition Service (FRS) is an intelligent service that uses computers to process, analyze, and understand facial images based on human facial features. |
| [Huawei Cloud Image Recognition](../../components/next/hwcloud-imagerecognition-component.md) | camel-huaweicloud-imagerecognition-starter | Stable | 3.12 | To identify objects, scenes, and concepts in images on Huawei Cloud |
| [Huawei Distributed Message Service (DMS)](../../components/next/hwcloud-dms-component.md) | camel-huaweicloud-dms-starter | Stable | 3.12 | To integrate with a fully managed, high-performance message queuing service on Huawei Cloud |
| [Huawei FunctionGraph](../../components/next/hwcloud-functiongraph-component.md) | camel-huaweicloud-functiongraph-starter | Stable | 3.11 | To call serverless functions on Huawei Cloud |
| [Huawei Identity and Access Management (IAM)](../../components/next/hwcloud-iam-component.md) | camel-huaweicloud-iam-starter | Stable | 3.11 | To securely manage users on Huawei Cloud |
| [Huawei Object Storage Service (OBS)](../../components/next/hwcloud-obs-component.md) | camel-huaweicloud-obs-starter | Stable | 3.12 | To provide stable, secure, efficient, and easy-to-use cloud storage service on Huawei Cloud |
| [Huawei Simple Message Notification (SMN)](../../components/next/hwcloud-smn-component.md) | camel-huaweicloud-smn-starter | Stable | 3.8 | To broadcast messages and connect cloud services through notifications on Huawei Cloud |
| [IBM Cloud Object Storage](../../components/next/ibm-cos-component.md) | camel-ibm-cos-starter | Stable | 4.16 | Store and retrieve objects from IBM Cloud Object Storage. |
| [IBM Secrets Manager](../../components/next/ibm-secrets-manager-component.md) | camel-ibm-secrets-manager-starter | Stable | 4.11 | Manage secrets in IBM Secrets Manager Service |
| [IBM Watson Discovery](../../components/next/ibm-watson-discovery-component.md) | camel-ibm-watson-discovery-starter | Stable | 4.16 | Perform document understanding and search using IBM Watson Discovery |
| [IBM Watson Language](../../components/next/ibm-watson-language-component.md) | camel-ibm-watson-language-starter | Stable | 4.16 | Perform natural language processing using IBM Watson Natural Language Understanding |
| [IBM Watson Speech to Text](../../components/next/ibm-watson-speech-to-text-component.md) | camel-ibm-watson-speech-to-text-starter | Stable | 4.17 | Convert speech audio to text using IBM Watson Speech to Text |
| [IBM Watson Text to Speech](../../components/next/ibm-watson-text-to-speech-component.md) | camel-ibm-watson-text-to-speech-starter | Stable | 4.17 | Convert text to natural-sounding speech using IBM Watson Text to Speech |
| [IBM watsonx.ai](../../components/next/ibm-watsonx-ai-component.md) | camel-ibm-watsonx-ai-starter | Preview | 4.18 | Interact with IBM watsonx.ai foundation models for text generation, chat, embeddings, and more. |
| [IBM watsonx.data](../../components/next/ibm-watsonx-data-component.md) | camel-ibm-watsonx-data-starter | Preview | 4.19 | Interact with IBM watsonx.data lakehouse for catalog, schema, table, and engine management. |
| [IEC 60870 Client](../../components/next/iec60870-client-component.md) | camel-iec60870-starter | Stable | 2.20 | IEC 60870 supervisory control and data acquisition (SCADA) client using NeoSCADA implementation. |
| [IEC 60870 Server](../../components/next/iec60870-server-component.md) | camel-iec60870-starter | Stable | 2.20 | IEC 60870 supervisory control and data acquisition (SCADA) server using NeoSCADA implementation. |
| [Iggy](../../components/next/iggy-component.md) | camel-iggy-starter | Preview | 4.17 | Send and receive message to Apache Iggy streaming platform. |
| [Ignite Cache](../../components/next/ignite-cache-component.md) | camel-ignite-starter | Stable | 2.17 | Perform cache operations on an Ignite cache or consume changes from a continuous query. |
| [Ignite Compute](../../components/next/ignite-compute-component.md) | camel-ignite-starter | Stable | 2.17 | Run compute operations on an Ignite cluster. |
| [Ignite Events](../../components/next/ignite-events-component.md) | camel-ignite-starter | Stable | 2.17 | Receive events from an Ignite cluster by creating a local event listener. |
| [Ignite ID Generator](../../components/next/ignite-idgen-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Atomic Sequences and ID Generators . |
| [Ignite Messaging](../../components/next/ignite-messaging-component.md) | camel-ignite-starter | Stable | 2.17 | Send and receive messages from an Ignite topic. |
| [Ignite Queues](../../components/next/ignite-queue-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Queue data structures. |
| [Ignite Sets](../../components/next/ignite-set-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Set data structures. |
| [Infinispan](../../components/next/infinispan-component.md) | camel-infinispan-starter | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [Infinispan Embedded](../../components/next/infinispan-embedded-component.md) | camel-infinispan-embedded-starter | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [InfluxDB](../../components/next/influxdb-component.md) | camel-influxdb-starter | Stable | 2.18 | Interact with InfluxDB v1, a time series database. |
| [InfluxDB2](../../components/next/influxdb2-component.md) | camel-influxdb2-starter | Stable | 3.20 | Interact with InfluxDB v2, a time series database. |
| [IRC](../../components/next/irc-component.md) | camel-irc-starter | Stable | 1.1 | Send and receive messages to/from and IRC chat. |
| [IronMQ](../../components/next/ironmq-component.md) | camel-ironmq-starter | Stable | 2.17 | Send and receive messages to/from IronMQ an elastic and durable hosted message queue as a service. |
| [JCache](../../components/next/jcache-component.md) | camel-jcache-starter | Stable | 2.17 | Perform caching operations against JSR107/JCache. |
| [JCR](../../components/next/jcr-component.md) | camel-jcr-starter | Stable | 1.3 | Read and write nodes to/from a JCR compliant content repository. |
| [JDBC](../../components/next/jdbc-component.md) | camel-jdbc-starter | Stable | 1.2 | Access databases through SQL and JDBC. |
| [Jetty](../../components/next/jetty-component.md) | camel-jetty-starter | Stable | 1.2 | Expose HTTP endpoints using Jetty 12. |
| [JGroups](../../components/next/jgroups-component.md) | camel-jgroups-starter | Stable | 2.13 | Exchange messages with JGroups clusters. |
| [JGroups raft](../../components/next/jgroups-raft-component.md) | camel-jgroups-raft-starter | Stable | 2.24 | Exchange messages with JGroups-raft clusters. |
| [Jira](../../components/next/jira-component.md) | camel-jira-starter | Stable | 3.0 | Interact with JIRA issue tracker. |
| [JMS](../../components/next/jms-component.md) | camel-jms-starter | Stable | 1.0 | Send and receive messages to/from JMS message brokers. |
| [JMX](../../components/next/jmx-component.md) | camel-jmx-starter | Stable | 2.6 | Receive JMX notifications. |
| [JOLT](../../components/next/jolt-component.md) | camel-jolt-starter | Stable | 2.16 | JSON to JSON transformation using JOLT. |
| [JOOQ](../../components/next/jooq-component.md) | camel-jooq-starter | Stable | 3.0 | Store and retrieve Java objects from an SQL database using JOOQ. |
| [JPA](../../components/next/jpa-component.md) | camel-jpa-starter | Stable | 1.0 | Store and retrieve Java objects from databases using Java Persistence API (JPA). |
| [JSLT](../../components/next/jslt-component.md) | camel-jslt-starter | Stable | 3.1 | Query or transform JSON payloads using JSLT. |
| [JSON Schema Validator](../../components/next/json-validator-component.md) | camel-json-validator-starter | Stable | 2.20 | Validate JSON payloads using NetworkNT JSON Schema. |
| [JSONata](../../components/next/jsonata-component.md) | camel-jsonata-starter | Stable | 3.5 | Transforms JSON payload using JSONata transformation. |
| [JsonPatch](../../components/next/json-patch-component.md) | camel-json-patch-starter | Stable-deprecated | 3.12 | Transforms JSON using JSON patch (RFC 6902). |
| [JT400](../../components/next/jt400-component.md) | camel-jt400-starter | Stable | 1.5 | Exchanges messages with an IBM i system using data queues, message queues, or program call. IBM i is the replacement for AS/400 and iSeries servers. |
| [JTE](../../components/next/jte-component.md) | camel-jte-starter | Stable | 4.4 | Transform messages using a Java based template engine (JTE). |
| [Kafka](../../components/next/kafka-component.md) | camel-kafka-starter | Stable | 2.13 | Send and receive messages to/from an Apache Kafka broker. |
| [Kamelet](../../components/next/kamelet-component.md) | camel-kamelet-starter | Stable | 3.8 | To call Kamelets |
| [Keycloak](../../components/next/keycloak-component.md) | camel-keycloak-starter | Stable | 4.15 | Manage Keycloak instances via Admin API. |
| [Knative](../../components/next/knative-component.md) | camel-knative-starter | Stable | 3.15 | Send and receive events from Knative. |
| [Knative Http](../../components/next/knative-http-component.md) | camel-knative-http-starter | Stable | 3.15 | Camel Knative HTTP |
| [KServe](../../components/next/kserve-component.md) | camel-kserve-starter | Stable | 4.10 | Provide access to AI model servers with the KServe standard to run inference with remote models |
| [Kubernetes ConfigMap](../../components/next/kubernetes-config-maps-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes. |
| [Kubernetes Cronjob](../../components/next/kubernetes-cronjob-component.md) | camel-kubernetes-starter | Stable | 4.3 | Perform operations on Kubernetes CronJob. |
| [Kubernetes Custom Resources](../../components/next/kubernetes-custom-resources-component.md) | camel-kubernetes-starter | Stable | 3.7 | Perform operations on Kubernetes Custom Resources and get notified on Deployment changes. |
| [Kubernetes Deployments](../../components/next/kubernetes-deployments-component.md) | camel-kubernetes-starter | Stable | 2.20 | Perform operations on Kubernetes Deployments and get notified on Deployment changes. |
| [Kubernetes Event](../../components/next/kubernetes-events-component.md) | camel-kubernetes-starter | Stable | 3.20 | Perform operations on Kubernetes Events and get notified on Events changes. |
| [Kubernetes HPA](../../components/next/kubernetes-hpa-component.md) | camel-kubernetes-starter | Stable | 2.23 | Perform operations on Kubernetes Horizontal Pod Autoscalers (HPA) and get notified on HPA changes. |
| [Kubernetes Job](../../components/next/kubernetes-job-component.md) | camel-kubernetes-starter | Stable | 2.23 | Perform operations on Kubernetes Jobs. |
| [Kubernetes Namespaces](../../components/next/kubernetes-namespaces-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Namespaces and get notified on Namespace changes. |
| [Kubernetes Nodes](../../components/next/kubernetes-nodes-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Nodes and get notified on Node changes. |
| [Kubernetes Persistent Volume](../../components/next/kubernetes-persistent-volumes-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes and get notified on Persistent Volume changes. |
| [Kubernetes Persistent Volume Claim](../../components/next/kubernetes-persistent-volumes-claims-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes Claims and get notified on Persistent Volumes Claim changes. |
| [Kubernetes Pods](../../components/next/kubernetes-pods-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Pods and get notified on Pod changes. |
| [Kubernetes Replication Controller](../../components/next/kubernetes-replication-controllers-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Replication Controllers and get notified on Replication Controllers changes. |
| [Kubernetes Resources Quota](../../components/next/kubernetes-resources-quota-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Resources Quotas. |
| [Kubernetes Secrets](../../components/next/kubernetes-secrets-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Secrets. |
| [Kubernetes Service Account](../../components/next/kubernetes-service-accounts-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Service Accounts. |
| [Kubernetes Services](../../components/next/kubernetes-services-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Services and get notified on Service changes. |
| [Kudu](../../components/next/kudu-component.md) | camel-kudu-starter | Stable | 3.0 | Interact with Apache Kudu, a free and open source column-oriented data store of the Apache Hadoop ecosystem. |
| [LangChain4j Agent](../../components/next/langchain4j-agent-component.md) | camel-langchain4j-agent-starter | Preview | 4.14 | LangChain4j Agent component |
| [LangChain4j Chat](../../components/next/langchain4j-chat-component.md) | camel-langchain4j-chat-starter | Stable | 4.5 | LangChain4j Chat component |
| [LangChain4j Embedding Store](../../components/next/langchain4j-embeddingstore-component.md) | camel-langchain4j-embeddingstore-starter | Stable | 4.14 | Perform operations on the Langchain4jEmbeddingStores. |
| [LangChain4j Embeddings](../../components/next/langchain4j-embeddings-component.md) | camel-langchain4j-embeddings-starter | Stable | 4.5 | LangChain4j Embeddings |
| [LangChain4j Tools](../../components/next/langchain4j-tools-component.md) | camel-langchain4j-tools-starter | Preview | 4.8 | LangChain4j Tools and Function Calling Features |
| [LangChain4j Web Search](../../components/next/langchain4j-web-search-component.md) | camel-langchain4j-web-search-starter | Stable | 4.8 | LangChain4j Web Search Engine |
| [Language](../../components/next/language-component.md) | camel-language-starter | Stable | 2.5 | Execute scripts in any of the languages supported by Camel. |
| [LDAP](../../components/next/ldap-component.md) | camel-ldap-starter | Stable | 1.5 | Perform searches on LDAP servers. |
| [LDIF](../../components/next/ldif-component.md) | camel-ldif-starter | Stable | 2.20 | Perform updates on an LDAP server from an LDIF body content. |
| [Log Data](../../components/next/log-component.md) | camel-log-starter | Stable | 1.1 | Prints data form the routed message (such as body and headers) to the logger. |
| [Lucene](../../components/next/lucene-component.md) | camel-lucene-starter | Stable | 2.2 | Perform inserts or queries against Apache Lucene databases. |
| [Lumberjack](../../components/next/lumberjack-component.md) | camel-lumberjack-starter | Stable | 2.18 | Receive logs messages using the Lumberjack protocol. |
| [Mail](../../components/next/mail-component.md) | camel-mail-starter | Stable | 1.0 | Send and receive emails using imap, pop3 and smtp protocols. |
| [MapStruct](../../components/next/mapstruct-component.md) | camel-mapstruct-starter | Stable | 3.19 | Type Conversion using Mapstruct |
| [Master](../../components/next/master-component.md) | camel-master-starter | Stable | 2.20 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [Metrics](../../components/next/metrics-component.md) | camel-metrics-starter | Stable | 2.14 | Collect various metrics directly from Camel routes using the DropWizard metrics library. |
| [Micrometer](../../components/next/micrometer-component.md) | camel-micrometer-starter | Stable | 2.22 | Collect various metrics directly from Camel routes using the Micrometer library. |
| [Milvus](../../components/next/milvus-component.md) | camel-milvus-starter | Stable | 4.5 | Perform operations on the Milvus Vector Database. |
| [Mina](../../components/next/mina-component.md) | camel-mina-starter | Stable | 2.10 | Socket level networking using TCP or UDP with Apache Mina 2.x. |
| [MINA SFTP](../../components/next/mina-sftp-component.md) | camel-mina-sftp-starter | Preview | 4.18 | Upload and download files to/from SFTP servers using Apache MINA SSHD. |
| [Minio](../../components/next/minio-component.md) | camel-minio-starter | Stable | 3.5 | Store and retrieve objects from Minio Storage Service using Minio SDK. |
| [MLLP](../../components/next/mllp-component.md) | camel-mllp-starter | Stable | 2.17 | Communicate with external systems using the MLLP protocol. |
| [Mock](../../components/next/mock-component.md) | camel-mock-starter | Stable | 1.0 | Test routes and mediation rules using mocks. |
| [MongoDB](../../components/next/mongodb-component.md) | camel-mongodb-starter | Stable | 2.19 | Perform operations on MongoDB documents and collections. |
| [MongoDB GridFS](../../components/next/mongodb-gridfs-component.md) | camel-mongodb-gridfs-starter | Stable | 2.18 | Interact with MongoDB GridFS. |
| [Mustache](../../components/next/mustache-component.md) | camel-mustache-starter | Stable | 2.12 | Transform messages using a Mustache template. |
| [MVEL](../../components/next/mvel-component.md) | camel-mvel-starter | Stable | 2.12 | Transform messages using an MVEL template. |
| [MyBatis](../../components/next/mybatis-component.md) | camel-mybatis-starter | Stable | 2.7 | Performs a query, poll, insert, update or delete in a relational database using MyBatis. |
| [MyBatis Bean](../../components/next/mybatis-bean-component.md) | camel-mybatis-starter | Stable | 2.22 | Perform queries, inserts, updates or deletes in a relational database using MyBatis. |
| [Nats](../../components/next/nats-component.md) | camel-nats-starter | Stable | 2.17 | Send and receive messages from NATS messaging system. |
| [Neo4j](../../components/next/neo4j-component.md) | camel-neo4j-starter | Stable | 4.10 | Perform operations on the Neo4j Graph Database |
| [Netty](../../components/next/netty-component.md) | camel-netty-starter | Stable | 2.14 | Socket level networking using TCP or UDP with Netty 4.x. |
| [Netty HTTP](../../components/next/netty-http-component.md) | camel-netty-http-starter | Stable | 2.14 | Netty HTTP server and client using the Netty 4.x. |
| [OAI-PMH](../../components/next/oaipmh-component.md) | camel-oaipmh-starter | Stable | 3.5 | Harvest metadata using OAI-PMH protocol |
| [Olingo2](../../components/next/olingo2-component.md) | camel-olingo2-starter | Stable-deprecated | 2.14 | Communicate with OData 2.0 services using Apache Olingo. |
| [Olingo4](../../components/next/olingo4-component.md) | camel-olingo4-starter | Stable-deprecated | 2.19 | Communicate with OData 4.0 services using Apache Olingo OData API. |
| [Once](../../components/next/once-component.md) | camel-once-starter | Stable | 4.17 | Trigger a single message only once at startup (useful for development and testing purposes). |
| [OPC UA Browser](../../components/next/milo-browse-component.md) | camel-milo-starter | Stable | 3.15 | Connect to OPC UA servers using the binary protocol for browsing the node tree. |
| [OPC UA Client](../../components/next/milo-client-component.md) | camel-milo-starter | Stable | 2.19 | Connect to OPC UA servers using the binary protocol for acquiring telemetry data. |
| [OPC UA Server](../../components/next/milo-server-component.md) | camel-milo-starter | Stable | 2.19 | Make telemetry data available as an OPC UA server. |
| [OpenAI](../../components/next/openai-component.md) | camel-openai-starter | Stable | 4.17 | OpenAI endpoint for chat completion and embeddings. |
| [OpenSearch](../../components/next/opensearch-component.md) | camel-opensearch-starter | Stable | 4.0 | Send requests to OpenSearch via Java Client API. |
| [OpenShift Build Config](../../components/next/openshift-build-configs-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on OpenShift Build Configs. |
| [OpenShift Builds](../../components/next/openshift-builds-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on OpenShift Builds. |
| [OpenShift Deployment Configs](../../components/next/openshift-deploymentconfigs-component.md) | camel-kubernetes-starter | Stable | 3.18 | Perform operations on OpenShift Deployment Configs and get notified on Deployment Config changes. |
| [OpenStack Cinder](../../components/next/openstack-cinder-component.md) | camel-openstack-starter | Stable | 2.19 | Access data in OpenStack Cinder block storage. |
| [OpenStack Glance](../../components/next/openstack-glance-component.md) | camel-openstack-starter | Stable | 2.19 | Manage VM images and metadata definitions in OpenStack Glance. |
| [OpenStack Keystone](../../components/next/openstack-keystone-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Keystone for API client authentication, service discovery and distributed multi-tenant authorization. |
| [OpenStack Neutron](../../components/next/openstack-neutron-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Neutron for network services. |
| [OpenStack Nova](../../components/next/openstack-nova-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack to manage compute resources. |
| [OpenStack Swift](../../components/next/openstack-swift-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Swift object/blob store. |
| [OpenTelemetry Metrics](../../components/next/opentelemetry-metrics-component.md) | camel-opentelemetry-metrics-starter | Stable | 4.17 | Camel metrics based on the Camel Telemetry spec |
| [OptaPlanner](../../components/next/optaplanner-component.md) | camel-optaplanner-starter | Stable | 2.13 | Solve planning problems with OptaPlanner. |
| [Paho](../../components/next/paho-component.md) | camel-paho-starter | Stable | 2.16 | Communicate with MQTT message brokers using Eclipse Paho MQTT Client. |
| [Paho MQTT 5](../../components/next/paho-mqtt5-component.md) | camel-paho-mqtt5-starter | Stable | 3.8 | Communicate with MQTT message brokers using Eclipse Paho MQTT v5 Client. |
| [PDF](../../components/next/pdf-component.md) | camel-pdf-starter | Stable | 2.16 | Create, modify or extract content from PDF documents. |
| [Pinecone](../../components/next/pinecone-component.md) | camel-pinecone-starter | Stable | 4.6 | Perform operations on the Pinecone Vector Database. |
| [Platform HTTP](../../components/next/platform-http-component.md) | camel-platform-http-starter | Stable | 3.0 | Expose HTTP endpoints using the HTTP server available in the current platform. |
| [PLC4X](../../components/next/plc4x-component.md) | camel-plc4x-starter | Stable | 3.20 | Read and write to PLC devices |
| [PostgresSQL Event](../../components/next/pgevent-component.md) | camel-pgevent-starter | Stable | 2.15 | Send and receive PostgreSQL events via LISTEN and NOTIFY commands. |
| [PostgresSQL Replication Slot](../../components/next/pg-replication-slot-component.md) | camel-pg-replication-slot-starter | Stable | 3.0 | Poll for PostgreSQL Write-Ahead Log (WAL) records using Streaming Replication Slots. |
| [PQC Algorithms](../../components/next/pqc-component.md) | camel-pqc-starter | Stable | 4.12 | Post Quantum Cryptography Signature and Verification component. |
| [Printer](../../components/next/lpr-component.md) | camel-printer-starter | Stable | 2.1 | Send print jobs to printers. |
| [PubNub](../../components/next/pubnub-component.md) | camel-pubnub-starter | Stable | 2.19 | Send and receive messages to/from PubNub data stream network for connected devices. |
| [Pulsar](../../components/next/pulsar-component.md) | camel-pulsar-starter | Stable | 2.24 | Send and receive messages from/to Apache Pulsar messaging system. |
| [Qdrant](../../components/next/qdrant-component.md) | camel-qdrant-starter | Stable | 4.5 | Perform operations on the Qdrant Vector Database. |
| [Quartz](../../components/next/quartz-component.md) | camel-quartz-starter | Stable | 2.12 | Schedule sending of messages using the Quartz 2.x scheduler. |
| [QuickFix](../../components/next/quickfix-component.md) | camel-quickfix-starter | Stable | 2.1 | Open a Financial Interchange (FIX) session using an embedded QuickFix/J engine. |
| [Reactive Streams](../../components/next/reactive-streams-component.md) | camel-reactive-streams-starter | Stable | 2.19 | Exchange messages with reactive stream processing libraries compatible with the reactive streams standard. |
| [Ref](../../components/next/ref-component.md) | camel-ref-starter | Stable | 1.2 | Route messages to an endpoint looked up dynamically by name in the Camel Registry. |
| [REST](../../components/next/rest-component.md) | camel-rest-starter | Stable | 2.14 | Expose REST services or call external REST services. |
| [REST API](../../components/next/rest-api-component.md) | camel-rest-starter | Stable | 2.16 | Expose OpenAPI Specification of the REST services defined using Camel REST DSL. |
| [REST OpenApi](../../components/next/rest-openapi-component.md) | camel-rest-openapi-starter | Stable | 3.1 | To call and expose REST services using OpenAPI specification as contract. |
| [Robot Framework](../../components/next/robotframework-component.md) | camel-robotframework-starter | Stable | 3.0 | Pass camel exchanges to acceptance test written in Robot DSL. |
| [RocketMQ](../../components/next/rocketmq-component.md) | camel-rocketmq-starter | Stable | 3.20 | Send and receive messages from RocketMQ cluster. |
| [RSS](../../components/next/rss-component.md) | camel-rss-starter | Stable | 2.0 | Poll RSS feeds. |
| [Saga](../../components/next/saga-component.md) | camel-saga-starter | Stable | 2.21 | Execute custom actions within a route using the Saga EIP. |
| [Salesforce](../../components/next/salesforce-component.md) | camel-salesforce-starter | Stable | 2.12 | Communicate with Salesforce using Java DTOs. |
| [SAP NetWeaver](../../components/next/sap-netweaver-component.md) | camel-sap-netweaver-starter | Stable | 2.12 | Send requests to SAP NetWeaver Gateway using HTTP. |
| [Scheduler](../../components/next/scheduler-component.md) | camel-scheduler-starter | Stable | 2.15 | Generate messages in specified intervals using java.util.concurrent.ScheduledExecutorService. |
| [Schematron](../../components/next/schematron-component.md) | camel-schematron-starter | Stable | 2.15 | Validate XML payload using the Schematron Library. |
| [SCP](../../components/next/scp-component.md) | camel-jsch-starter | Stable | 2.10 | Copy files to/from remote hosts using the secure copy protocol (SCP). |
| [SEDA](../../components/next/seda-component.md) | camel-seda-starter | Stable | 1.1 | Asynchronously call another endpoint from any Camel Context in the same JVM. |
| [ServiceNow](../../components/next/servicenow-component.md) | camel-servicenow-starter | Stable | 2.18 | Interact with ServiceNow via its REST API. |
| [Servlet](../../components/next/servlet-component.md) | camel-servlet-starter | Stable | 2.0 | Serve HTTP requests by a Servlet. |
| [SFTP](../../components/next/sftp-component.md) | camel-ftp-starter | Stable | 1.1 | Upload and download files to/from SFTP servers. |
| [Simple JMS](../../components/next/sjms-component.md) | camel-sjms-starter | Stable | 2.11 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 1.x API. |
| [Simple JMS2](../../components/next/sjms2-component.md) | camel-sjms2-starter | Stable | 2.19 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API. |
| [Slack](../../components/next/slack-component.md) | camel-slack-starter | Stable | 2.16 | Send and receive messages to/from Slack. |
| [SMB](../../components/next/smb-component.md) | camel-smb-starter | Stable | 4.3 | Read and write files to Server Message Block (SMB) file shares. |
| [Smooks](../../components/next/smooks-component.md) | camel-smooks-starter | Stable | 4.7 | Use Smooks to transform, route, and bind both XML and non-XML data, including EDI, CSV, JSON, and YAML. |
| [SMPP](../../components/next/smpp-component.md) | camel-smpp-starter | Stable | 2.2 | Send and receive SMS messages using a SMSC (Short Message Service Center). |
| [SNMP](../../components/next/snmp-component.md) | camel-snmp-starter | Stable | 2.1 | Receive traps and poll SNMP (Simple Network Management Protocol) capable devices. |
| [Solr](../../components/next/solr-component.md) | camel-solr-starter | Stable | 4.8 | Perform operations against Apache Lucene Solr. |
| [Splunk](../../components/next/splunk-component.md) | camel-splunk-starter | Stable-deprecated | 2.13 | Publish or search for events in Splunk. |
| [Splunk HEC](../../components/next/splunk-hec-component.md) | camel-splunk-hec-starter | Stable | 3.3 | The splunk component allows publishing events in Splunk using the HTTP Event Collector. |
| [Spring AI Chat](../../components/next/spring-ai-chat-component.md) | camel-spring-ai-chat-starter | Stable | 4.17 | Perform chat operations using Spring AI. |
| [Spring AI Embeddings](../../components/next/spring-ai-embeddings-component.md) | camel-spring-ai-embeddings-starter | Stable | 4.17 | Spring AI Embeddings |
| [Spring AI Image](../../components/next/spring-ai-image-component.md) | camel-spring-ai-image-starter | Preview | 4.19 | Spring AI Image Generation |
| [Spring AI Tools](../../components/next/spring-ai-tools-component.md) | camel-spring-ai-tools-starter | Stable | 4.17 | Spring AI Tools and Function Calling Features |
| [Spring AI Vector Store](../../components/next/spring-ai-vector-store-component.md) | camel-spring-ai-vector-store-starter | Stable | 4.17 | Spring AI Vector Store |
| [Spring Batch](../../components/next/spring-batch-component.md) | camel-spring-batch-starter | Stable | 2.10 | Send messages to Spring Batch for further processing. |
| [Spring Event](../../components/next/spring-event-component.md) | camel-spring-starter | Stable | 1.4 | Listen for Spring Application Events. |
| [Spring JDBC](../../components/next/spring-jdbc-component.md) | camel-spring-jdbc-starter | Stable | 3.10 | Access databases through SQL and JDBC with Spring Transaction support. |
| [Spring LDAP](../../components/next/spring-ldap-component.md) | camel-spring-ldap-starter | Stable | 2.11 | Perform searches in LDAP servers using filters as the message payload. |
| [Spring RabbitMQ](../../components/next/spring-rabbitmq-component.md) | camel-spring-rabbitmq-starter | Stable | 3.8 | Send and receive messages from RabbitMQ using the Spring RabbitMQ client. |
| [Spring Redis](../../components/next/spring-redis-component.md) | camel-spring-redis-starter | Stable | 2.11 | Send and receive messages from Redis. |
| [Spring WebService](../../components/next/spring-ws-component.md) | camel-spring-ws-starter | Stable | 2.6 | Access external web services as a client or expose your own web services. |
| [SQL](../../components/next/sql-component.md) | camel-sql-starter | Stable | 1.4 | Perform SQL queries using Spring JDBC. |
| [SQL Stored Procedure](../../components/next/sql-stored-component.md) | camel-sql-starter | Stable | 2.17 | Perform SQL queries as a JDBC Stored Procedures using Spring JDBC. |
| [SSH](../../components/next/ssh-component.md) | camel-ssh-starter | Stable | 2.10 | Execute commands on remote hosts using SSH. |
| [StAX](../../components/next/stax-component.md) | camel-stax-starter | Stable | 2.9 | Process XML payloads by a SAX ContentHandler. |
| [Stitch](../../components/next/stitch-component.md) | camel-stitch-starter | Stable | 3.8 | Stitch is a cloud ETL service that integrates various data sources into a central data warehouse through various integrations. |
| [Stomp](../../components/next/stomp-component.md) | camel-stomp-starter | Stable-deprecated | 2.12 | Send and receive messages to/from STOMP (Simple Text Oriented Messaging Protocol) compliant message brokers. |
| [Stream](../../components/next/stream-component.md) | camel-stream-starter | Stable | 1.3 | Read from system-in and write to system-out and system-err streams. |
| [String Template](../../components/next/string-template-component.md) | camel-stringtemplate-starter | Stable | 1.2 | Transform messages using StringTemplate engine. |
| [Stripe](../../components/next/stripe-component.md) | camel-stripe-starter | Preview | 4.17 | Interact with the Stripe payment platform. |
| [Stub](../../components/next/stub-component.md) | camel-stub-starter | Stable | 2.10 | Stub out any physical endpoints while in development or testing. |
| [Tahu Edge Node / Device](../../components/next/tahu-edge-component.md) | camel-tahu-starter | Stable | 4.8 | Sparkplug B Edge Node and Device support over MQTT using Eclipse Tahu |
| [Tahu Host Application](../../components/next/tahu-host-component.md) | camel-tahu-starter | Stable | 4.8 | Sparkplug B Host Application support over MQTT using Eclipse Tahu |
| [Telegram](../../components/next/telegram-component.md) | camel-telegram-starter | Stable | 2.18 | Send and receive messages using the Telegram Bot API. |
| [TensorFlow Serving](../../components/next/tensorflow-serving-component.md) | camel-tensorflow-serving-starter | Stable | 4.10 | Provide access to TensorFlow Serving model servers to run inference with TensorFlow saved models remotely |
| [Thrift](../../components/next/thrift-component.md) | camel-thrift-starter | Stable | 2.20 | Call and expose remote procedures (RPC) with Apache Thrift data format and serialization mechanism. |
| [Thymeleaf](../../components/next/thymeleaf-component.md) | camel-thymeleaf-starter | Stable | 4.1 | Transform messages using a Thymeleaf template. |
| [Tika](../../components/next/tika-component.md) | camel-tika-starter | Stable | 2.19 | Parse documents and extract metadata and text using Apache Tika. |
| [Timer](../../components/next/timer-component.md) | camel-timer-starter | Stable | 1.0 | Generate messages in specified intervals using java.util.Timer. |
| [Twilio](../../components/next/twilio-component.md) | camel-twilio-starter | Stable | 2.20 | Interact with Twilio REST APIs using Twilio Java SDK. |
| [Twitter Direct Message](../../components/next/twitter-directmessage-component.md) | camel-twitter-starter | Stable | 2.10 | Send and receive Twitter direct messages. |
| [Twitter Search](../../components/next/twitter-search-component.md) | camel-twitter-starter | Stable | 2.10 | Access Twitter Search. |
| [Twitter Timeline](../../components/next/twitter-timeline-component.md) | camel-twitter-starter | Stable | 2.10 | Send tweets and receive tweets from user’s timeline. |
| [Undertow](../../components/next/undertow-component.md) | camel-undertow-starter | Stable | 2.16 | Expose HTTP and WebSocket endpoints and access external HTTP/WebSocket servers. |
| [Validator](../../components/next/validator-component.md) | camel-validator-starter | Stable | 1.1 | Validate the payload using XML Schema and JAXP Validation. |
| [Velocity](../../components/next/velocity-component.md) | camel-velocity-starter | Stable | 1.2 | Transform messages using a Velocity template. |
| [Vert.x](../../components/next/vertx-component.md) | camel-vertx-starter | Stable | 2.12 | Send and receive messages to/from Vert.x Event Bus. |
| [Vert.x HTTP Client](../../components/next/vertx-http-component.md) | camel-vertx-http-starter | Stable | 3.5 | Send requests to external HTTP servers using Vert.x |
| [Vert.x WebSocket](../../components/next/vertx-websocket-component.md) | camel-vertx-websocket-starter | Stable | 3.5 | Expose WebSocket endpoints and connect to remote WebSocket servers using Vert.x |
| [Wasm](../../components/next/wasm-component.md) | camel-wasm-starter | Experimental | 4.4 | Invoke Wasm functions. |
| [Weather](../../components/next/weather-component.md) | camel-weather-starter | Stable | 2.12 | Poll the weather information from Open Weather Map. |
| [weaviate](../../components/next/weaviate-component.md) | camel-weaviate-starter | Stable | 4.12 | Perform operations on the Weaviate Vector Database. |
| [Web3j Ethereum Blockchain](../../components/next/web3j-component.md) | camel-web3j-starter | Stable | 2.22 | Interact with Ethereum nodes using web3j client API. |
| [Webhook](../../components/next/webhook-component.md) | camel-webhook-starter | Stable | 3.0 | Expose webhook endpoints to receive push notifications for other Camel components. |
| [WhatsApp](../../components/next/whatsapp-component.md) | camel-whatsapp-starter | Stable | 3.19 | Send messages to WhatsApp. |
| [WordPress](../../components/next/wordpress-component.md) | camel-wordpress-starter | Stable | 2.21 | Manage posts and users using the WordPress API. |
| [Workday](../../components/next/workday-component.md) | camel-workday-starter | Stable | 3.1 | Detect and parse documents using Workday. |
| [XChange](../../components/next/xchange-component.md) | camel-xchange-starter | Stable | 2.21 | Access market data and trade on Bitcoin and Altcoin exchanges. |
| [XJ](../../components/next/xj-component.md) | camel-xj-starter | Stable | 3.0 | Transform JSON and XML message using a XSLT. |
| [XML Security Sign](../../components/next/xmlsecurity-sign-component.md) | camel-xmlsecurity-starter | Stable | 2.12 | Sign XML payloads using the XML signature specification. |
| [XML Security Verify](../../components/next/xmlsecurity-verify-component.md) | camel-xmlsecurity-starter | Stable | 2.12 | Verify XML payloads using the XML signature specification. |
| [XMPP](../../components/next/xmpp-component.md) | camel-xmpp-starter | Stable | 1.0 | Send and receive messages to/from an XMPP chat server. |
| [XQuery](../../components/next/xquery-component.md) | camel-saxon-starter | Stable | 1.0 | Query and/or transform XML payloads using XQuery and Saxon. |
| [XSLT](../../components/next/xslt-component.md) | camel-xslt-starter | Stable | 1.3 | Transforms XML payload using an XSLT template. |
| [XSLT Saxon](../../components/next/xslt-saxon-component.md) | camel-xslt-saxon-starter | Stable | 3.0 | Transform XML payloads using an XSLT template using Saxon. |
| [Zeebe](../../components/next/zeebe-component.md) | camel-zeebe-starter | Preview-deprecated | 3.21 | Zeebe component which integrates with Camunda Zeebe to interact with the API. |
| [Zendesk](../../components/next/zendesk-component.md) | camel-zendesk-starter | Stable | 2.19 | Manage Zendesk tickets, users, organizations, etc. |
| [ZooKeeper](../../components/next/zookeeper-component.md) | camel-zookeeper-starter | Stable | 2.9 | Manage ZooKeeper clusters. |
| [ZooKeeper Master](../../components/next/zookeeper-master-component.md) | camel-zookeeper-master-starter | Stable | 2.19 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |

### Non-Spring-Boot Components

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Hugging Face](../../components/next/huggingface-component.md) | camel-huggingface-starter | Preview | 4.19 | Integration with Hugging Face’s Model Hub by using the Deep Java Library (DJL) Python bridge |
| [PGVector](../../components/next/pgvector-component.md) | camel-pgvector-starter | Preview | 4.19 | Perform operations on the PostgreSQL pgvector Vector Database. |
| [Properties](../../components/next/properties-component.md) | camel-base-starter | Stable | 2.3 | The properties component is used for property placeholders in your Camel application, such as endpoint URIs. |

## Camel Data Formats

Number of Camel data formats: 52 in 46 JAR artifacts (0 deprecated)

    
| Data Format | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [ASN.1 File](../../components/next/dataformats/asn1-dataformat.md) | camel-asn1-starter | Stable | 2.20 | Encode and decode data structures using Abstract Syntax Notation One (ASN.1). |
| [Avro](../../components/next/dataformats/avro-dataformat.md) | camel-avro-starter | Stable | 2.14 | Serialize and deserialize messages using Apache Avro binary data format. |
| [Avro Jackson](../../components/next/dataformats/avroJackson-dataformat.md) | camel-jackson3-avro-starter | Preview | 4.19 | Marshal POJOs to Avro and back using Jackson. |
| [Barcode](../../components/next/dataformats/barcode-dataformat.md) | camel-barcode-starter | Stable | 2.14 | Transform strings to various 1D/2D barcode bitmap formats and back. |
| [Base64](../../components/next/dataformats/base64-dataformat.md) | camel-base64-starter | Stable | 2.11 | Encode and decode data using Base64. |
| [BeanIO](../../components/next/dataformats/beanio-dataformat.md) | camel-beanio-starter | Stable | 2.10 | Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats). |
| [Bindy](../../components/next/dataformats/bindy-dataformat.md) | camel-bindy-starter | Stable | 2.0 | Marshal and unmarshal between POJOs and key-value pair (KVP) format using Camel Bindy |
| [CBOR](../../components/next/dataformats/cbor-dataformat.md) | camel-cbor-starter | Stable | 3.0 | Unmarshal a CBOR payload to POJO and back. |
| [Crypto (Java Cryptographic Extension)](../../components/next/dataformats/crypto-dataformat.md) | camel-crypto-starter | Stable | 2.3 | Encrypt and decrypt messages using Java Cryptography Extension (JCE). |
| [CSV](../../components/next/dataformats/csv-dataformat.md) | camel-csv-starter | Stable | 1.3 | Handle CSV (Comma Separated Values) payloads. |
| [DFDL](../../components/next/dataformats/dfdl-dataformat.md) | camel-dfdl-starter | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [FHIR JSon](../../components/next/dataformats/fhirJson-dataformat.md) | camel-fhir-starter | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from JSON. |
| [FHIR XML](../../components/next/dataformats/fhirXml-dataformat.md) | camel-fhir-starter | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from XML. |
| [Flatpack](../../components/next/dataformats/flatpack-dataformat.md) | camel-flatpack-starter | Stable | 2.1 | Marshal and unmarshal Java lists and maps to/from flat files (such as CSV, delimited, or fixed length formats) using Flatpack library. |
| [Fory](../../components/next/dataformats/fory-dataformat.md) | camel-fory-starter | Stable | 4.9 | Serialize and deserialize messages using Apache Fory |
| [Grok](../../components/next/dataformats/grok-dataformat.md) | camel-grok-starter | Stable | 3.0 | Unmarshal unstructured data to objects using Logstash based Grok patterns. |
| [Groovy JSon](../../components/next/dataformats/groovyJson-dataformat.md) | camel-groovy-starter | Preview | 4.19 | Transform between JSon and java.util.Map or java.util.List objects. |
| [Groovy XML](../../components/next/dataformats/groovyXml-dataformat.md) | camel-groovy-starter | Stable | 4.15 | Transform between XML and Groovy Node (Map structure) objects. |
| [GZip Deflater](../../components/next/dataformats/gzipDeflater-dataformat.md) | camel-zip-deflater-starter | Stable | 2.0 | Compress and decompress messages using java.util.zip.GZIPStream. |
| [HL7](../../components/next/dataformats/hl7-dataformat.md) | camel-hl7-starter | Stable | 2.0 | Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec. |
| [iCal](../../components/next/dataformats/ical-dataformat.md) | camel-ical-starter | Stable | 2.12 | Marshal and unmarshal iCal (.ics) documents to/from model objects. |
| [ISO-8583](../../components/next/dataformats/iso8583-dataformat.md) | camel-iso8583-starter | Stable | 4.14 | Create, edit and read ISO-8583 messages. |
| [Jackson XML](../../components/next/dataformats/jacksonXml-dataformat.md) | camel-jacksonxml-starter | Stable | 2.16 | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson. |
| [JAXB](../../components/next/dataformats/jaxb-dataformat.md) | camel-jaxb-starter | Stable | 1.0 | Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard. |
| [JSON Fastjson](../../components/next/dataformats/fastjson-dataformat.md) | camel-fastjson-starter | Stable | 2.20 | Marshal POJOs to JSON and back using Fastjson |
| [JSON Gson](../../components/next/dataformats/gson-dataformat.md) | camel-gson-starter | Stable | 2.10 | Marshal POJOs to JSON and back using Gson |
| [JSON Jackson](../../components/next/dataformats/jackson-dataformat.md) | camel-jackson3-starter | Preview | 4.19 | Marshal POJOs to JSON and back using Jackson. |
| [JSON JSON-B](../../components/next/dataformats/jsonb-dataformat.md) | camel-jsonb-starter | Stable | 3.7 | Marshal POJOs to JSON and back using JSON-B. |
| [JSonApi](../../components/next/dataformats/jsonApi-dataformat.md) | camel-jsonapi-starter | Stable | 3.0 | Marshal and unmarshal JSON:API resources using JSONAPI-Converter library. |
| [LZF Deflate Compression](../../components/next/dataformats/lzf-dataformat.md) | camel-lzf-starter | Stable | 2.17 | Compress and decompress streams using LZF deflate algorithm. |
| [MIME Multipart](../../components/next/dataformats/mimeMultipart-dataformat.md) | camel-mail-starter | Stable | 2.17 | Marshal Camel messages with attachments into MIME-Multipart messages and back. |
| [OCSF](../../components/next/dataformats/ocsf-dataformat.md) | camel-ocsf-starter | Preview | 4.18 | Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON. |
| [Parquet File](../../components/next/dataformats/parquetAvro-dataformat.md) | camel-parquet-avro-starter | Stable | 4.0 | Parquet Avro serialization and de-serialization. |
| [PGP (Pretty Good Privacy Cryptographic)](../../components/next/dataformats/pgp-dataformat.md) | camel-crypto-pgp-starter | Stable | 2.9 | Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP. |
| [PQC (Post-Quantum Cryptography)](../../components/next/dataformats/pqc-dataformat.md) | camel-pqc-starter | Stable | 4.16 | Encrypt and decrypt messages using Post-Quantum Cryptography Key Encapsulation Mechanisms (KEM). |
| [Protobuf](../../components/next/dataformats/protobuf-dataformat.md) | camel-protobuf-starter | Stable | 2.2 | Serialize and deserialize Java objects using Google’s Protocol buffers. |
| [Protobuf Jackson](../../components/next/dataformats/protobufJackson-dataformat.md) | camel-jackson3-protobuf-starter | Preview | 4.19 | Marshal POJOs to Protobuf and back using Jackson. |
| [RSS](../../components/next/dataformats/rss-dataformat.md) | camel-rss-starter | Stable | 2.1 | Transform from ROME SyndFeed Java Objects to XML and vice-versa. |
| [Smooks](../../components/next/dataformats/smooks-dataformat.md) | camel-smooks-starter | Stable | 4.9 | Transform and bind XML as well as non-XML data, including EDI, CSV, JSON, and YAML using Smooks. |
| [SOAP](../../components/next/dataformats/soap-dataformat.md) | camel-soap-starter | Stable | 2.3 | Marshal Java objects to SOAP messages and back. |
| [SWIFT MT](../../components/next/dataformats/swiftMt-dataformat.md) | camel-swift-starter | Stable | 3.20 | Encode and decode SWIFT MT messages. |
| [SWIFT MX](../../components/next/dataformats/swiftMx-dataformat.md) | camel-swift-starter | Stable | 3.20 | Encode and decode SWIFT MX messages. |
| [Syslog](../../components/next/dataformats/syslog-dataformat.md) | camel-syslog-starter | Stable | 2.6 | Marshall SyslogMessages to RFC3164 and RFC5424 messages and back. |
| [Tar File](../../components/next/dataformats/tarFile-dataformat.md) | camel-tarfile-starter | Stable | 2.16 | Archive files into tarballs or extract files from tarballs. |
| [Thrift](../../components/next/dataformats/thrift-dataformat.md) | camel-thrift-starter | Stable | 2.20 | Serialize and deserialize messages using Apache Thrift binary data format. |
| [uniVocity CSV](../../components/next/dataformats/univocityCsv-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to CSV (Comma Separated Values) using UniVocity Parsers. |
| [uniVocity Fixed Length](../../components/next/dataformats/univocityFixed-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to fixed length records using UniVocity Parsers. |
| [uniVocity TSV](../../components/next/dataformats/univocityTsv-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to TSV (Tab-Separated Values) records using UniVocity Parsers. |
| [XML Security](../../components/next/dataformats/xmlSecurity-dataformat.md) | camel-xmlsecurity-starter | Stable | 2.0 | Encrypt and decrypt XML payloads using Apache Santuario. |
| [YAML SnakeYAML](../../components/next/dataformats/snakeYaml-dataformat.md) | camel-snakeyaml-starter | Stable | 2.17 | Marshal and unmarshal Java objects to and from YAML using SnakeYAML |
| [Zip Deflater](../../components/next/dataformats/zipDeflater-dataformat.md) | camel-zip-deflater-starter | Stable | 2.12 | Compress and decompress streams using java.util.zip.Deflater and java.util.zip.Inflater. |
| [Zip File](../../components/next/dataformats/zipFile-dataformat.md) | camel-zipfile-starter | Stable | 2.11 | Compression and decompress streams using java.util.zip.ZipStream. |

### Non-Spring-Boot Data Formats

    
| Data Format | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |

## Camel Languages

Number of Camel languages: 26 in 17 JAR artifacts (3 deprecated)

    
| Language | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Bean Method](../../components/next/languages/bean-language.md) | camel-bean-starter | Stable | 1.3 | Calls a Java bean method. |
| [Constant](../../components/next/languages/constant-language.md) | camel-core-starter | Stable | 1.5 | A fixed value set only once during the route startup. |
| [CSimple](../../components/next/languages/csimple-language.md) | camel-core-starter | Stable-deprecated | 3.7 | Evaluate a compiled simple expression. |
| [DataSonnet](../../components/next/languages/datasonnet-language.md) | camel-datasonnet-starter | Stable | 3.7 | To use DataSonnet scripts for message transformations. |
| [ExchangeProperty](../../components/next/languages/exchangeProperty-language.md) | camel-core-starter | Stable | 2.0 | Gets a property from the Exchange. |
| [File](../../components/next/languages/file-language.md) | camel-core-starter | Stable | 1.1 | File related capabilities for the Simple language |
| [Groovy](../../components/next/languages/groovy-language.md) | camel-groovy-starter | Stable | 1.3 | Evaluates a Groovy script. |
| [Header](../../components/next/languages/header-language.md) | camel-core-starter | Stable | 1.5 | Gets a header from the Exchange. |
| [HL7 Terser](../../components/next/languages/hl7terser-language.md) | camel-hl7-starter | Stable | 2.11 | Get the value of a HL7 message field specified by terse location specification syntax. |
| [Java](../../components/next/languages/java-language.md) | camel-joor-starter | Stable | 4.3 | Evaluates a Java (Java compiled once at runtime) expression. |
| [JavaScript](../../components/next/languages/js-language.md) | camel-javascript-starter | Stable | 3.20 | Evaluates a JavaScript expression. |
| [jOOR](../../components/next/languages/joor-language.md) | camel-joor-starter | Stable-deprecated | 3.7 | Evaluates a jOOR (Java compiled once at runtime) expression. |
| [JQ](../../components/next/languages/jq-language.md) | camel-jq-starter | Stable | 3.18 | Evaluates a JQ expression against a JSON message body. |
| [JSONPath](../../components/next/languages/jsonpath-language.md) | camel-jsonpath-starter | Stable | 2.13 | Evaluates a JSONPath expression against a JSON message body. |
| [MVEL](../../components/next/languages/mvel-language.md) | camel-mvel-starter | Stable | 2.0 | Evaluates a MVEL template. |
| [OGNL](../../components/next/languages/ognl-language.md) | camel-ognl-starter | Stable-deprecated | 1.1 | Evaluates an OGNL expression (Apache Commons OGNL). |
| [Python](../../components/next/languages/python-language.md) | camel-python-starter | Experimental | 3.19 | Evaluates a Python expression. |
| [Ref](../../components/next/languages/ref-language.md) | camel-core-starter | Stable | 2.8 | Uses an existing expression from the registry. |
| [Simple](../../components/next/languages/simple-language.md) | camel-core-starter | Stable | 1.1 | Evaluates a Camel simple expression. |
| [SpEL](../../components/next/languages/spel-language.md) | camel-spring-starter | Stable | 2.7 | Evaluates a Spring expression (SpEL). |
| [Tokenize](../../components/next/languages/tokenize-language.md) | camel-core-starter | Stable | 2.0 | Tokenize text payloads using delimiter patterns. |
| [Variable](../../components/next/languages/variable-language.md) | camel-core-starter | Stable | 4.4 | Gets a variable |
| [Wasm](../../components/next/languages/wasm-language.md) | camel-wasm-starter | Experimental | 4.5 | Call a wasm (web assembly) function. |
| [XML Tokenize](../../components/next/languages/xtokenize-language.md) | camel-stax-starter | Stable | 2.14 | Tokenize XML payloads. |
| [XPath](../../components/next/languages/xpath-language.md) | camel-xpath-starter | Stable | 1.1 | Evaluates an XPath expression against an XML payload. |
| [XQuery](../../components/next/languages/xquery-language.md) | camel-saxon-starter | Stable | 1.0 | Evaluates an XQuery expressions against an XML payload. |

### Non-Spring-Boot Languages

    
| Language | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |

## Miscellaneous Extensions

Number of miscellaneous extensions: 26 in 26 JAR artifacts (5 deprecated)

    
| Extensions | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [AWS XRay](../../components/next/others/aws-xray.md) | camel-aws-xray-starter | Stable-deprecated | 2.21 | Enable Distributed tracing using AWS XRay |
| [CLI Debug](../../components/next/others/cli-debug.md) | camel-cli-debug-starter | Stable | 4.17 | Remote CLI debugger |
| [Cloudevents](../../components/next/others/cloudevents.md) | camel-cloudevents-starter | Stable | 3.15 | Camel support for the CloudEvents specification |
| [CSimple jOOR](../../components/next/others/csimple-joor.md) | camel-csimple-joor-starter | Stable-deprecated | 3.7 | jOOR compiler for csimple language |
| [CXF Transport](../../components/next/others/cxf-transport.md) | camel-cxf-transport-starter | Stable | 2.8 | Camel Transport for Apache CXF |
| [Debug](../../components/next/others/debug.md) | camel-debug-starter | Stable | 3.15 | Enables Camel Route Debugging |
| [Jasypt](../../components/next/others/jasypt.md) | camel-jasypt-starter | Stable | 2.5 | Security using Jasypt |
| [JFR](../../components/next/others/jfr.md) | camel-jfr-starter | Stable | 3.8 | Diagnose Camel applications with Java Flight Recorder |
| [LangChain4j Tokenizer](../../components/next/others/langchain4j-tokenizer.md) | camel-langchain4j-tokenizer-starter | Preview | 4.8 | LangChain4j Tokenizer |
| [LevelDB](../../components/next/others/leveldb.md) | camel-leveldb-starter | Stable-deprecated | 2.10 | Using LevelDB as persistent EIP store |
| [LRA](../../components/next/others/lra.md) | camel-lra-starter | Preview | 2.21 | Camel saga binding for Long-Running-Action framework |
| [MDC Logging](../../components/next/others/mdc.md) | camel-mdc-starter | Preview | 4.15 | Logging MDC (Mapped Diagnostic Context) Service |
| [Micrometer Observability](../../components/next/others/observation.md) | camel-observation-starter | Stable-deprecated | 3.21 | Observability using Micrometer Observation |
| [Micrometer Observability 2](../../components/next/others/micrometer-observability.md) | camel-micrometer-observability-starter | Preview | 4.15 | Micrometer Observability implementation of Camel Telemetry |
| [Openapi Java](../../components/next/others/openapi-java.md) | camel-openapi-java-starter | Stable | 3.1 | Rest DSL support for using OpenApi doc |
| [OpenTelemetry](../../components/next/others/opentelemetry.md) | camel-opentelemetry-starter | Stable-deprecated | 3.5 | Distributed tracing using OpenTelemetry |
| [Opentelemetry2](../../components/next/others/opentelemetry2.md) | camel-opentelemetry2-starter | Stable | 4.11 | Implementation of Camel Opentelemetry based on the Camel Telemetry spec |
| [Reactor](../../components/next/others/reactor.md) | camel-reactor-starter | Stable | 2.20 | Reactor based back-end for Camel’s reactive streams component |
| [Resilience4j](../../components/next/others/resilience4j.md) | camel-resilience4j-starter | Stable | 3.0 | Circuit Breaker EIP using Resilience4j |
| [Resilience4j Micrometer](../../components/next/others/resilience4j-micrometer.md) | camel-resilience4j-micrometer-starter | Stable | 4.15 | Micrometer statistics for Resilience4j |
| [RxJava](../../components/next/others/rxjava.md) | camel-rxjava-starter | Stable | 2.22 | RxJava based back-end for Camel’s reactive streams component |
| [Shiro](../../components/next/others/shiro.md) | camel-shiro-starter | Stable | 2.5 | Security using Shiro |
| [Spring Security](../../components/next/others/spring-security.md) | camel-spring-security-starter | Stable | 2.3 | Security using Spring Security |
| [Springdoc](../../components/next/others/springdoc.md) | camel-springdoc-starter |  | 3.14 | Springdoc Swagger UI for openapi-java in spring boot |
| [Telemetry Dev](../../components/next/others/telemetry-dev.md) | camel-telemetry-dev-starter | Preview | 4.11 | Basic implementation of Camel Telemetry useful for development purposes |
| [Undertow Spring Security](../../components/next/others/undertow-spring-security.md) | camel-undertow-spring-security-starter | Stable | 3.3 | Spring Security Provider for camel-undertow |

### Non-Spring-Boot Miscellaneous Extensions

    
| Extensions | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Attachments](../../components/next/others/attachments.md) | camel-attachments-starter | Stable | 3.0 | Support for attachments on Camel messages |
| [Azure Schema Registry](../../components/next/others/azure-schema-registry.md) | camel-azure-schema-registry-starter | Stable | 4.2 | Azure Schema Registry Component for utilities to deal with authentication |
| [Camel YAML DSL Validator Maven Plugin](../../components/next/others/camel-yaml-dsl-validator-maven-plugin.md) | undefined-starter |  |  |  |
| [CLI Connector](../../components/next/others/cli-connector.md) | camel-cli-connector-starter | Stable | 3.19 | Runtime adapter connecting with Camel CLI |
| [DSL](../../components/next/others/dsl.md) | undefined-starter |  |  |  |
| [DSL Modeline](../../components/next/others/dsl-modeline.md) | camel-dsl-modeline-starter | Stable | 3.16 | Camel DSL modeline |
| [Elytron](../../components/next/others/elytron.md) | camel-elytron-starter | Stable-deprecated | 3.1 | Elytron Security Provider for camel-undertow |
| [Headersmap](../../components/next/others/headersmap.md) | camel-headersmap-starter | Stable | 2.20 | Fast case-insensitive headers map implementation |
| [Jandex](../../components/next/others/jandex.md) | camel-jandex-starter | Stable | 4.12 | Custom class and resource loader using jandex.idx |
| [Java DSL (runtime compiled)](../../components/next/others/java-joor-dsl.md) | camel-java-joor-dsl-starter | Stable | 3.9 | Camel Java DSL with jOOR |
| [Jaxb XML Dsl](../../components/next/others/java-xml-jaxb-dsl.md) | camel-xml-jaxb-dsl-starter | Stable | 3.9 | Camel DSL with XML using camel-jaxb |
| [JTA](../../components/next/others/jta.md) | camel-jta-starter | Stable | 3.4 | Using Camel With JTA Transaction Manager |
| [Kamelet Main](../../components/next/others/kamelet-main.md) | camel-kamelet-main-starter | Preview | 3.11 | Main to run Kamelet standalone |
| [Kamelet Main Support](../../components/next/others/kamelet-main-support.md) | camel-kamelet-main-support-starter | Preview | 4.19 | Support Module for Kamelet Main |
| [Mail Microsoft Oauth](../../components/next/others/mail-microsoft-oauth.md) | camel-mail-microsoft-oauth-starter | Stable | 3.18.4 | Camel Mail OAuth2 Authenticator for Microsoft Exchange Online |
| [Main](../../components/next/others/main.md) | camel-main-starter | Stable | 3.0 | Camel Main |
| [Micrometer Prometheus](../../components/next/others/micrometer-prometheus.md) | camel-micrometer-prometheus-starter | Stable | 4.3 | Camel Micrometer Prometheus for Camel Main |
| [Microprofile Config](../../components/next/others/microprofile-config.md) | camel-microprofile-config-starter | Stable | 3.0 | Bridging Eclipse MicroProfile Config with Camel properties |
| [Microprofile Fault Tolerance](../../components/next/others/microprofile-fault-tolerance.md) | camel-microprofile-fault-tolerance-starter | Stable | 3.3 | Circuit Breaker EIP using MicroProfile Fault Tolerance |
| [Microprofile Health](../../components/next/others/microprofile-health.md) | camel-microprofile-health-starter | Stable | 3.0 | Expose Camel health checks via MicroProfile Health |
| [Oauth](../../components/next/others/oauth.md) | camel-oauth-starter | Preview | 4.12 | Camel OAuth (Preview) |
| [Observability Services](../../components/next/others/observability-services.md) | camel-observability-services-starter | Preview | 4.9 | Camel Observability Services |
| [Openapi Validator](../../components/next/others/openapi-validator.md) | camel-openapi-validator-starter | Stable | 4.7 | OpenAPI validator for Camel Rest DSL |
| [Platform HTTP Jolokia](../../components/next/others/platform-http-jolokia.md) | camel-platform-http-jolokia-starter | Stable | 4.5 | Jolokia plugin for standalone Camel HTTP Platform |
| [Platform Http Main](../../components/next/others/platform-http-main.md) | camel-platform-http-main-starter | Stable | 4.0 | Platform HTTP for standalone Camel Main applications |
| [Platform Http Vertx](../../components/next/others/platform-http-vertx.md) | camel-platform-http-vertx-starter | Stable | 3.2 | Implementation of the Platform HTTP Engine based on Vert.x Web |
| [Reactive Executor Tomcat](../../components/next/others/reactive-executor-tomcat.md) | camel-reactive-executor-tomcat-starter | Experimental | 3.17 | Reactive Executor for camel-core using Apache Tomcat |
| [Reactive Executor Vert.x](../../components/next/others/reactive-executor-vertx.md) | camel-reactive-executor-vertx-starter | Experimental | 3.0 | Reactive Executor for camel-core using Vert.x |
| [Redis](../../components/next/others/redis.md) | camel-redis-starter | Stable | 3.5 | Aggregation repository using Redis as datastore |
| [Resourceresolver Github](../../components/next/others/resourceresolver-github.md) | camel-resourceresolver-github-starter | Stable | 3.11 | Resource resolver to load files from GitHub |
| [Spring Cloud Config](../../components/next/others/spring-cloud-config.md) | camel-spring-cloud-config-starter | Stable | 4.12 | Camel Spring Cloud Config support |
| [Spring Main](../../components/next/others/spring-main.md) | camel-spring-main-starter | Stable | 3.2 | Camel Spring Main support |
| [Spring XML](../../components/next/others/spring-xml.md) | camel-spring-xml-starter | Stable | 3.9 | Camel Spring with XML DSL |
| [Telemetry](../../components/next/others/telemetry.md) | camel-telemetry-starter | Preview | 4.11 | Distributed telemetry common interfaces |
| [Test JUnit5](../../components/next/others/test-junit5.md) | camel-test-junit5-starter | Stable | 3.0 | Camel unit testing with JUnit 5 |
| [Test JUnit6](../../components/next/others/test-junit6.md) | camel-test-junit6-starter | Stable | 4.17 | Camel unit testing with JUnit 6 |
| [Test Main JUnit5](../../components/next/others/test-main-junit5.md) | camel-test-main-junit5-starter | Stable | 3.16 | Camel unit testing with Main and JUnit 5 |
| [Test Main JUnit6](../../components/next/others/test-main-junit6.md) | camel-test-main-junit6-starter | Stable | 4.17 | Camel unit testing with Main and JUnit 6 |
| [Test Spring JUnit5](../../components/next/others/test-spring-junit5.md) | camel-test-spring-junit5-starter | Stable | 3.0 | Camel unit testing with Spring and JUnit 5 |
| [Test Spring JUnit6](../../components/next/others/test-spring-junit6.md) | camel-test-spring-junit6-starter | Stable | 4.17 | Camel unit testing with Spring and JUnit 6 |
| [ThreadPoolFactory Vert.x](../../components/next/others/threadpoolfactory-vertx.md) | camel-threadpoolfactory-vertx-starter | Experimental | 3.5 | ThreadPoolFactory for camel-core using Vert.x |
| [Tracing](../../components/next/others/tracing.md) | camel-tracing-starter | Stable-deprecated | 3.5 | Distributed tracing common interfaces |
| [Write Ahead Log Strategy for Resume API](../../components/next/others/wal.md) | camel-wal-starter | Stable | 3.20 | Write Ahead Log Strategy for Resume API |
| [XML Io Dsl](../../components/next/others/java-xml-io-dsl.md) | camel-xml-io-dsl-starter | Stable | 3.9 | Camel DSL with XML |
| [YAML DSL](../../components/next/others/yaml-dsl.md) | camel-yaml-dsl-starter | Stable | 3.9 | Camel YAML DSL |

## Cluster Services

The following cluster service starters provide high-availability clustering support for Camel applications. These are infrastructure starters that do not directly map to a Camel component but provide clustering capabilities.

  
| Cluster Service | Artifact | Description |
| --- | --- | --- |
| [Consul Cluster Service](consul-cluster-service.md) | camel-consul-cluster-service-starter | Cluster service implementation using HashiCorp Consul for distributed coordination and leader election. |
| [File Cluster Service](file-cluster-service.md) | camel-file-cluster-service-starter | Cluster service implementation using file-based locking for simple clustering scenarios. |
| [Infinispan Cluster Service](infinispan-cluster-service.md) | camel-infinispan-cluster-service-starter | Cluster service implementation using Infinispan distributed cache for clustering. |
| [JGroups Raft Cluster Service](jgroups-raft-cluster-service.md) | camel-jgroups-raft-cluster-service-starter | Cluster service implementation using JGroups with Raft consensus protocol. |
| [Kubernetes Cluster Service](kubernetes-cluster-service.md) | camel-kubernetes-cluster-service-starter | Cluster service implementation using Kubernetes native mechanisms for clustering. |
| [Zookeeper Cluster Service](zookeeper-cluster-service.md) | camel-zookeeper-cluster-service-starter | Cluster service implementation using Apache Zookeeper for distributed coordination. |