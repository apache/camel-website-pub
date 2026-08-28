# Components Index

Index of all Camel components.

# Components

## Core Components

Below is the list of core components that are provided by Apache Camel.

Number of Core Components: 29 in 26 JAR artifacts (0 deprecated)

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Bean](bean-component.md) | camel-bean | Stable | 1.0 | Invoke methods of Java beans stored in Camel registry. |
| [Browse](browse-component.md) | camel-browse | Stable | 1.3 | Inspect the messages received on endpoints supporting BrowsableEndpoint. |
| [Class](class-component.md) | camel-bean | Stable | 2.4 | Invoke methods of Java beans specified by class name. |
| [Control Bus](controlbus-component.md) | camel-controlbus | Stable | 2.11 | Manage and monitor Camel routes. |
| [Data Format](dataformat-component.md) | camel-dataformat | Stable | 2.12 | Use a Camel Data Format as a regular Camel Component. |
| [Dataset](dataset-component.md) | camel-dataset | Stable | 1.3 | Provide data for load and soak testing of your Camel application. |
| [DataSet Test](dataset-test-component.md) | camel-dataset | Stable | 1.3 | Extends the mock component by pulling messages from another endpoint on startup to set the expected message bodies. |
| [Direct](direct-component.md) | camel-direct | Stable | 1.0 | Call another endpoint from the same Camel Context synchronously. |
| [Dynamic Router](dynamic-router-component.md) | camel-dynamic-router | Stable | 3.15 | The Dynamic Router component routes exchanges to recipients, and the recipients (and their rules) may change at runtime. |
| [Event](event-component.md) | camel-event | Stable | 4.19 | Subscribe to Camel internal events such as route started/stopped and exchange completed/failed. |
| [Exec](exec-component.md) | camel-exec | Stable | 2.3 | Execute commands on the underlying operating system. |
| [File](file-component.md) | camel-file | Stable | 1.0 | Read and write files. |
| [Kamelet](kamelet-component.md) | camel-kamelet | Stable | 3.8 | To call Kamelets |
| [Language](language-component.md) | camel-language | Stable | 2.5 | Execute scripts in any of the languages supported by Camel. |
| [Log Data](log-component.md) | camel-log | Stable | 1.1 | Prints data from the routed message (such as body and headers) to the logger. |
| [Mock](mock-component.md) | camel-mock | Stable | 1.0 | Test routes and mediation rules using mocks. |
| [Once](once-component.md) | camel-once | Stable | 4.17 | Trigger a single message only once at startup (useful for development and testing purposes). |
| [Ref](ref-component.md) | camel-ref | Stable | 1.2 | Route messages to an endpoint looked up dynamically by name in the Camel Registry. |
| [REST](rest-component.md) | camel-rest | Stable | 2.14 | Expose REST services or call external REST services. |
| [REST API](rest-api-component.md) | camel-rest | Stable | 2.16 | Expose OpenAPI Specification of the REST services defined using Camel REST DSL. |
| [Scheduler](scheduler-component.md) | camel-scheduler | Stable | 2.15 | Generate messages in specified intervals using java.util.concurrent.ScheduledExecutorService. |
| [SEDA](seda-component.md) | camel-seda | Stable | 1.1 | Asynchronously call another endpoint from any Camel Context in the same JVM. |
| [Stream](stream-component.md) | camel-stream | Stable | 1.3 | Read from system-in and write to system-out and system-err streams. |
| [Stub](stub-component.md) | camel-stub | Stable | 2.10 | Stub out any physical endpoints while in development or testing. |
| [Timer](timer-component.md) | camel-timer | Stable | 1.0 | Generate messages in specified intervals using java.util.Timer. |
| [Validator](validator-component.md) | camel-validator | Stable | 1.1 | Validate the payload using XML Schema and JAXP Validation. |
| [Wasm](wasm-component.md) | camel-wasm | Experimental | 4.4 | Invoke Wasm functions. |
| [XSLT](xslt-component.md) | camel-xslt | Stable | 1.3 | Transforms XML payload using an XSLT template. |
| [XSLT Saxon](xslt-saxon-component.md) | camel-xslt-saxon | Stable | 3.0 | Transform XML payloads using an XSLT template using Saxon. |

## Components

Below is the list of non-core components that are provided by Apache Camel.

Number of Non-Core Components: 381 in 307 JAR artifacts (4 deprecated)

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [A2A](a2a-component.md) | camel-a2a | Preview | 4.21 | A2A endpoint for agent-to-agent communication. |
| [ActiveMQ 5.x](activemq-component.md) | camel-activemq | Stable | 1.0 | Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component. |
| [ActiveMQ 6.x](activemq6-component.md) | camel-activemq6 | Stable | 4.7 | Send messages to (or consume from) Apache ActiveMQ 6.x. This component extends the Camel JMS component. |
| [AI](ai-summary.md) |  |  |  |  |
| [AI Tool](ai-tool-component.md) | camel-ai-tool | Preview | 4.22 | Framework-agnostic consumer endpoint that registers a Camel route as an LLM tool in the shared AiToolRegistry. |
| [Alibaba EventBridge](alibaba-eventbridge-component.md) | camel-alibaba-eventbridge | Preview | 4.23 | Publish events to Alibaba Cloud EventBridge. |
| [Alibaba Function Compute (FC)](alibaba-fc-component.md) | camel-alibaba-fc | Preview | 4.23 | Invoke serverless functions on Alibaba Cloud Function Compute (FC). |
| [Alibaba Key Management Service (KMS)](alibaba-kms-component.md) | camel-alibaba-kms | Preview | 4.23 | Encrypt and decrypt data using Alibaba Cloud Key Management Service (KMS). |
| [Alibaba Message Service (MNS)](alibaba-mns-component.md) | camel-alibaba-mns | Preview | 4.23 | Send and receive messages to/from Alibaba Cloud Message Service (MNS). |
| [Alibaba Object Storage Service (OSS)](alibaba-oss-component.md) | camel-alibaba-oss | Preview | 4.23 | Alibaba Cloud Object Storage Service (OSS) component |
| [Alibaba Short Message Service (SMS)](alibaba-sms-component.md) | camel-alibaba-sms | Preview | 4.23 | Send SMS messages using Alibaba Cloud Short Message Service (SMS). |
| [Alibaba Simple Log Service (SLS)](alibaba-sls-component.md) | camel-alibaba-sls | Preview | 4.23 | Manage logs on Alibaba Cloud Simple Log Service (SLS). |
| [Alibaba Tablestore (OTS)](alibaba-ots-component.md) | camel-alibaba-ots | Preview | 4.23 | Perform row operations on Alibaba Cloud Tablestore (OTS). |
| [AMQP](amqp-component.md) | camel-amqp | Stable | 1.2 | Messaging with AMQP protocol using Apache Qpid Client. |
| [ArangoDb](arangodb-component.md) | camel-arangodb | Stable | 3.5 | Perform operations on ArangoDb when used as a Document Database, or as a Graph Database |
| [AS2](as2-component.md) | camel-as2 | Stable | 2.22 | Transfer data securely and reliably using the AS2 protocol (RFC4130). |
| [Asterisk](asterisk-component.md) | camel-asterisk | Stable | 2.18 | Interact with Asterisk PBX Server (VoIP). |
| [Atmosphere Websocket](atmosphere-websocket-component.md) | camel-atmosphere-websocket | Stable | 2.14 | Expose WebSocket endpoints using the Atmosphere framework. |
| [Atom](atom-component.md) | camel-atom | Stable | 1.2 | Poll Atom RSS feeds. |
| [Avro RPC](avro-component.md) | camel-avro-rpc | Stable | 2.10 | Produce or consume Apache Avro RPC services. |
| [AWS](aws-summary.md) |  |  |  |  |
| [AWS Athena](aws2-athena-component.md) | camel-aws2-athena | Stable | 3.4 | Access AWS Athena. |
| [AWS Bedrock](aws-bedrock-component.md) | camel-aws-bedrock | Stable | 4.5 | Invoke Model of AWS Bedrock service. |
| [AWS Bedrock Agent](aws-bedrock-agent-component.md) | camel-aws-bedrock | Stable | 4.5 | Operate on AWS Bedrock through its Agent. |
| [AWS Bedrock Agent Runtime](aws-bedrock-agent-runtime-component.md) | camel-aws-bedrock | Stable | 4.5 | Invoke Model of AWS Bedrock Agent Runtime service. |
| [AWS CloudTrail](aws-cloudtrail-component.md) | camel-aws-cloudtrail | Stable | 3.19 | Consume events from Amazon CloudTrail using AWS SDK version 2.x. |
| [AWS CloudWatch](aws2-cw-component.md) | camel-aws2-cw | Stable | 3.1 | Sending metrics to AWS CloudWatch. |
| [AWS Comprehend](aws2-comprehend-component.md) | camel-aws2-comprehend | Stable | 4.18 | Perform natural language processing using AWS Comprehend and AWS SDK version 2.x. |
| [AWS Config Service](aws-config-component.md) | camel-aws-config | Stable | 4.3 | Manage AWS Config service. |
| [AWS DynamoDB](aws2-ddb-component.md) | camel-aws2-ddb | Stable | 3.1 | Store and retrieve data from AWS DynamoDB. |
| [AWS DynamoDB Streams](aws2-ddbstream-component.md) | camel-aws2-ddb | Stable | 3.1 | Receive messages from AWS DynamoDB Stream. |
| [AWS Elastic Compute Cloud (EC2)](aws2-ec2-component.md) | camel-aws2-ec2 | Stable | 3.1 | Manage AWS EC2 instances. |
| [AWS Elastic Container Service (ECS)](aws2-ecs-component.md) | camel-aws2-ecs | Stable | 3.1 | Manage AWS ECS cluster instances. |
| [AWS Elastic Kubernetes Service (EKS)](aws2-eks-component.md) | camel-aws2-eks | Stable | 3.1 | Manage AWS EKS cluster instances. |
| [AWS Eventbridge](aws2-eventbridge-component.md) | camel-aws2-eventbridge | Stable | 3.6 | Manage AWS EventBridge cluster instances and consume events via SQS-backed polling. |
| [AWS Identity and Access Management (IAM)](aws2-iam-component.md) | camel-aws2-iam | Stable | 3.1 | Manage AWS IAM instances. |
| [AWS Key Management Service (KMS)](aws2-kms-component.md) | camel-aws2-kms | Stable | 3.1 | Manage keys stored in AWS KMS instances. |
| [AWS Kinesis](aws2-kinesis-component.md) | camel-aws2-kinesis | Stable | 3.2 | Consume and produce records from and to AWS Kinesis Streams. |
| [AWS Kinesis Firehose](aws2-kinesis-firehose-component.md) | camel-aws2-kinesis | Stable | 3.2 | Produce data to AWS Kinesis Firehose streams. |
| [AWS Lambda](aws2-lambda-component.md) | camel-aws2-lambda | Stable | 3.2 | Manage and invoke AWS Lambda functions. |
| [AWS Managed Streaming for Apache Kafka (MSK)](aws2-msk-component.md) | camel-aws2-msk | Stable | 3.1 | Manage AWS MSK instances. |
| [AWS MQ](aws2-mq-component.md) | camel-aws2-mq | Stable | 3.1 | Send messages to AWS MQ. |
| [AWS Parameter Store](aws-parameter-store-component.md) | camel-aws-parameter-store | Stable | 4.17 | Manage parameters using AWS Systems Manager (SSM) Parameter Store. |
| [AWS Polly](aws2-polly-component.md) | camel-aws2-polly | Stable | 4.18 | Synthesize speech using AWS Polly and AWS SDK version 2.x. |
| [AWS RedshiftData](aws2-redshift-data-component.md) | camel-aws2-redshift | Stable | 4.1 | Perform operations on AWS Redshift using Redshift Data API. |
| [AWS Rekognition](aws2-rekognition-component.md) | camel-aws2-rekognition | Stable | 4.17 | Manage and invoke AWS Rekognition. |
| [AWS S3 Storage Service](aws2-s3-component.md) | camel-aws2-s3 | Stable | 3.2 | Store and retrieve objects from AWS S3 Storage Service. |
| [AWS S3 Vectors](aws2-s3-vectors-component.md) | camel-aws2-s3-vectors | Stable | 4.17 | Store and query vector embeddings using AWS S3 Vectors with similarity search. |
| [AWS Secrets Manager](aws-secrets-manager-component.md) | camel-aws-secrets-manager | Stable | 3.9 | Manage secrets using AWS Secrets Manager. |
| [AWS Security Hub](aws-security-hub-component.md) | camel-aws-security-hub | Stable | 4.18 | Manage and interact with AWS Security Hub for security findings. |
| [AWS Security Token Service (STS)](aws2-sts-component.md) | camel-aws2-sts | Stable | 3.5 | Manage AWS STS cluster instances. |
| [AWS Simple Email Service (SES)](aws2-ses-component.md) | camel-aws2-ses | Stable | 3.1 | Send e-mails through AWS SES service. |
| [AWS Simple Notification System (SNS)](aws2-sns-component.md) | camel-aws2-sns | Stable | 3.1 | Send messages to AWS Simple Notification Topic. |
| [AWS Simple Queue Service (SQS)](aws2-sqs-component.md) | camel-aws2-sqs | Stable | 3.1 | Send and receive messages to/from AWS SQS. |
| [AWS StepFunctions](aws2-step-functions-component.md) | camel-aws2-step-functions | Stable | 4.0 | Manage and invoke AWS Step functions. |
| [AWS Textract](aws2-textract-component.md) | camel-aws2-textract | Stable | 4.15 | Extract text and data from documents using AWS Textract and AWS SDK version 2.x. |
| [AWS Timestream](aws2-timestream-component.md) | camel-aws2-timestream | Stable | 4.1 | Write records and execute queries on AWS time-series database |
| [AWS Transcribe](aws2-transcribe-component.md) | camel-aws2-transcribe | Stable | 4.15 | Automatically convert speech to text using AWS Transcribe service |
| [AWS Translate](aws2-translate-component.md) | camel-aws2-translate | Stable | 3.1 | Translate texts using AWS Translate and AWS SDK version 2.x. |
| [Azure](azure-summary.md) |  |  |  |  |
| [Azure CosmosDB](azure-cosmosdb-component.md) | camel-azure-cosmosdb | Stable | 3.10 | To read and write records to the CosmosDB database on Azure cloud platform. |
| [Azure Event Grid](azure-eventgrid-component.md) | camel-azure-eventgrid | Stable | 4.17 | Send events to Azure Event Grid topics. |
| [Azure Event Hubs](azure-eventhubs-component.md) | camel-azure-eventhubs | Stable | 3.5 | Send and receive events to/from Azure Event Hubs using AMQP protocol. |
| [Azure Files](azure-files-component.md) | camel-azure-files | Preview | 3.22 | Send and receive files to Azure storage file share |
| [Azure Functions](azure-functions-component.md) | camel-azure-functions | Stable | 4.19 | Invoke and manage Azure Functions. |
| [Azure Key Vault](azure-key-vault-component.md) | camel-azure-key-vault | Stable | 3.17 | Manage secrets and keys in Azure Key Vault Service |
| [Azure ServiceBus](azure-servicebus-component.md) | camel-azure-servicebus | Stable | 3.12 | Send and receive messages to/from Azure Service Bus. |
| [Azure Storage Blob Service](azure-storage-blob-component.md) | camel-azure-storage-blob | Stable | 3.3 | Store and retrieve blobs from Azure Storage Blob Service. |
| [Azure Storage Data Lake Service](azure-storage-datalake-component.md) | camel-azure-storage-datalake | Stable | 3.8 | Sends and receives files to/from Azure Data Lake Storage. |
| [Azure Storage Queue Service](azure-storage-queue-component.md) | camel-azure-storage-queue | Stable | 3.3 | Stores and retrieves messages to/from Azure Storage Queue. |
| [Bean Validator](bean-validator-component.md) | camel-bean-validator | Stable | 2.3 | Validate the message body using the Java Bean Validation API. |
| [Bonita](bonita-component.md) | camel-bonita | Stable | 2.19 | Communicate with a remote Bonita BPM process engine. |
| [Box](box-component.md) | camel-box | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc. on box.com. |
| [Braintree](braintree-component.md) | camel-braintree | Stable | 2.17 | Process payments using Braintree Payments. |
| [Caffeine Cache](caffeine-cache-component.md) | camel-caffeine | Stable | 2.20 | Perform caching operations using Caffeine Cache. |
| [Caffeine LoadCache](caffeine-loadcache-component.md) | camel-caffeine | Stable | 2.20 | Perform caching operations using Caffeine Cache with an attached CacheLoader. |
| [Camunda](camunda-component.md) | camel-camunda | Preview | 4.19 | Interact with Camunda 8 Orchestration Clusters using the Camunda Java Client. |
| [Cassandra CQL](cql-component.md) | camel-cassandraql | Stable | 2.15 | Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax. |
| [ChatScript](chatscript-component.md) | camel-chatscript | Stable | 3.0 | Chat with a ChatScript Server. |
| [Chunk](chunk-component.md) | camel-chunk | Stable | 2.15 | Transform messages using Chunk templating engine. |
| [ClickHouse](clickhouse-component.md) | camel-clickhouse | Preview | 4.22 | Interact with ClickHouse, the high-performance columnar OLAP database, for high-throughput ingestion and OLAP queries. |
| [ClickUp](clickup-component.md) | camel-clickup | Preview | 4.9 | Receives events from ClickUp |
| [CM SMS Gateway](cm-sms-component.md) | camel-cm-sms | Stable | 2.18 | Send SMS messages via CM SMS Gateway. |
| [CoAP](coap-component.md) | camel-coap | Stable | 2.16 | Send and receive messages to/from CoAP (Constrained Application Protocol) capable devices. |
| [CometD](cometd-component.md) | camel-cometd | Stable | 2.0 | Offers publish/subscribe, peer-to-peer (via a server), and RPC style messaging using the CometD/Bayeux protocol. |
| [Consul](consul-component.md) | camel-consul | Stable | 2.18 | Integrate with Consul service discovery and configuration store. |
| [Couchbase](couchbase-component.md) | camel-couchbase | Stable | 2.19 | Query Couchbase databases using SQL (N1QL) queries or MapReduce Views with a poll strategy and/or perform various operations against Couchbase databases. |
| [CouchDB](couchdb-component.md) | camel-couchdb | Stable | 2.11 | Consume changesets for inserts, updates and deletes in a CouchDB database, as well as get, save, update and delete documents from a CouchDB database. |
| [Cron](cron-component.md) | camel-cron | Stable | 3.1 | A generic interface for triggering events at times specified through the Unix cron syntax. |
| [Crypto (JCE)](crypto-component.md) | camel-crypto | Stable | 2.3 | Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE). |
| [CXF](cxf-component.md) | camel-cxf-soap | Stable | 1.0 | Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client. |
| [CXF-RS](cxfrs-component.md) | camel-cxf-rest | Stable | 2.0 | Expose JAX-RS REST services using Apache CXF or connect to external REST services using CXF REST client. |
| [CyberArk Vault](cyberark-vault-component.md) | camel-cyberark-vault | Stable | 4.17 | Retrieve secrets from CyberArk Conjur Vault. |
| [Dapr](dapr-component.md) | camel-dapr | Stable | 4.12 | Dapr component which interfaces with Dapr Building Blocks. |
| [Debezium](debezium-summary.md) |  |  |  |  |
| [Debezium DB2 Connector](debezium-db2-component.md) | camel-debezium-db2 | Stable | 3.17 | Capture changes from a DB2 database. |
| [Debezium MongoDB Connector](debezium-mongodb-component.md) | camel-debezium-mongodb | Stable | 3.0 | Capture changes from a MongoDB database. |
| [Debezium MySQL Connector](debezium-mysql-component.md) | camel-debezium-mysql | Stable | 3.0 | Capture changes from a MySQL database. |
| [Debezium Oracle Connector](debezium-oracle-component.md) | camel-debezium-oracle | Stable | 3.17 | Capture changes from an Oracle database. |
| [Debezium PostgreSQL Connector](debezium-postgres-component.md) | camel-debezium-postgres | Stable | 3.0 | Capture changes from a PostgreSQL database. |
| [Debezium SQL Server Connector](debezium-sqlserver-component.md) | camel-debezium-sqlserver | Stable | 3.0 | Capture changes from an SQL Server database. |
| [Deep Java Library](djl-component.md) | camel-djl | Stable | 3.3 | Infer Deep Learning models from message exchanges data using Deep Java Library (DJL). |
| [DFDL](dfdl-component.md) | camel-dfdl | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [DHIS2](dhis2-component.md) | camel-dhis2 | Stable | 4.0 | Leverages the DHIS2 Java SDK to integrate Apache Camel with the DHIS2 Web API. |
| [Disruptor](disruptor-component.md) | camel-disruptor | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [Disruptor VM](disruptor-vm-component.md) | camel-disruptor | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [DNS](dns-component.md) | camel-dns | Stable | 2.7 | Perform DNS queries using DNSJava. |
| [Docker](docker-component.md) | camel-docker | Stable | 2.15 | Manage Docker containers. |
| [Docling](docling-component.md) | camel-docling | Stable | 4.15 | Process documents using Docling library for parsing and conversion. |
| [Drill](drill-component.md) | camel-drill | Stable | 2.19 | Perform queries against an Apache Drill cluster. |
| [Dropbox](dropbox-component.md) | camel-dropbox | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc on Dropbox. |
| [DuckDB](duckdb-component.md) | camel-duckdb | Preview | 4.22 | Interact with DuckDB, the in-process analytical SQL database, for embedded analytics workloads. |
| [Dynamic Router Control](dynamic-router-control-component.md) | camel-dynamic-router | Stable | 4.4 | The Dynamic Router control endpoint for operations that allow routing participants to subscribe or unsubscribe to participate in dynamic message routing. |
| [Ehcache](ehcache-component.md) | camel-ehcache | Stable | 2.18 | Perform caching operations using Ehcache. |
| [Elasticsearch](elasticsearch-component.md) | camel-elasticsearch | Stable | 3.19 | Send requests to Elasticsearch via Java Client API. |
| [Elasticsearch Low level Rest Client](elasticsearch-rest-client-component.md) | camel-elasticsearch-rest-client | Stable | 4.3 | Perform queries and other operations on Elasticsearch or OpenSearch (uses low-level client). |
| [FHIR](fhir-component.md) | camel-fhir | Stable | 2.23 | Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. |
| [File Watch](file-watch-component.md) | camel-file-watch | Stable | 3.0 | Get notified about file events in a directory using java.nio.file.WatchService. |
| [Flatpack](flatpack-component.md) | camel-flatpack | Stable | 1.4 | Parse fixed width and delimited files using the FlatPack library. |
| [Flink](flink-component.md) | camel-flink | Stable | 2.18 | Send DataSet jobs to an Apache Flink cluster. |
| [Flowable](flowable-component.md) | camel-flowable | Stable | 4.9 | Send and receive messages from the Flowable BPMN and CMMN engines. |
| [FOP](fop-component.md) | camel-fop | Stable | 2.10 | Render messages into PDF and other output formats supported by Apache FOP. |
| [Freemarker](freemarker-component.md) | camel-freemarker | Stable | 2.10 | Transform messages using FreeMarker templates. |
| [FTP](ftp-component.md) | camel-ftp | Stable | 1.1 | Upload and download files to/from FTP servers. |
| [FTPS](ftps-component.md) | camel-ftp | Stable | 2.2 | Upload and download files to/from FTP servers supporting the FTPS protocol. |
| [Geocoder](geocoder-component.md) | camel-geocoder | Stable | 2.12 | Find geocodes (latitude and longitude) for a given address or the other way round. |
| [Git](git-component.md) | camel-git | Stable | 2.16 | Perform operations on git repositories. |
| [GitHub2](github2-component.md) | camel-github2 | Stable | 4.18 | Interact with the GitHub API. |
| [Google](google-summary.md) |  |  |  |  |
| [Google BigQuery](google-bigquery-component.md) | camel-google-bigquery | Stable | 2.20 | Google BigQuery data warehouse for analytics. |
| [Google BigQuery Standard SQL](google-bigquery-sql-component.md) | camel-google-bigquery | Stable | 2.23 | Access Google Cloud BigQuery service using SQL queries. |
| [Google Calendar](google-calendar-component.md) | camel-google-calendar | Stable | 2.15 | Perform various operations on a Google Calendar. |
| [Google Calendar Stream](google-calendar-stream-component.md) | camel-google-calendar | Stable | 2.23 | Poll for changes in a Google Calendar. |
| [Google Cloud Functions](google-functions-component.md) | camel-google-functions | Stable | 3.9 | Manage and invoke Google Cloud Functions |
| [Google Cloud Speech To Text](google-speech-to-text-component.md) | camel-google-speech-to-text | Stable | 4.19 | Transcribe audio to text using Google Cloud Speech-to-Text API |
| [Google Cloud Text To Speech](google-text-to-speech-component.md) | camel-google-text-to-speech | Stable | 4.19 | Synthesize speech from text using the Google Cloud Text-to-Speech API |
| [Google Cloud Vision](google-vision-component.md) | camel-google-vision | Stable | 4.19 | Detect labels, text, faces, logos and more on images through Google Cloud Vision API |
| [Google Drive](google-drive-component.md) | camel-google-drive | Stable | 2.14 | Manage files in Google Drive. |
| [Google Firestore](google-firestore-component.md) | camel-google-firestore | Stable | 4.19 | Store and retrieve data from Google Cloud Firestore NoSQL database. |
| [Google Mail](google-mail-component.md) | camel-google-mail | Stable | 2.15 | Manage messages in Google Mail. |
| [Google Mail Stream](google-mail-stream-component.md) | camel-google-mail | Stable | 2.22 | Poll for incoming messages in Google Mail. |
| [Google Pubsub](google-pubsub-component.md) | camel-google-pubsub | Stable | 2.19 | Send and receive messages to/from Google Cloud Platform PubSub Service. |
| [Google Secret Manager](google-secret-manager-component.md) | camel-google-secret-manager | Stable | 3.16 | Manage Google Secret Manager Secrets |
| [Google Sheets](google-sheets-component.md) | camel-google-sheets | Stable | 2.23 | Manage spreadsheets in Google Sheets. |
| [Google Sheets Stream](google-sheets-stream-component.md) | camel-google-sheets | Stable | 2.23 | Poll for changes in Google Sheets. |
| [Google Storage](google-storage-component.md) | camel-google-storage | Stable | 3.9 | Store and retrieve objects from Google Cloud Storage Service using the google-cloud-storage library. |
| [Google Vertex AI](google-vertexai-component.md) | camel-google-vertexai | Stable | 4.17 | Interact with Google Cloud Vertex AI generative models. |
| [GraphQL](graphql-component.md) | camel-graphql | Stable | 3.0 | Send GraphQL queries and mutations to external systems. |
| [gRPC](grpc-component.md) | camel-grpc | Stable | 2.19 | Expose gRPC endpoints and access external gRPC endpoints. |
| [HashiCorp Vault](hashicorp-vault-component.md) | camel-hashicorp-vault | Stable | 3.18 | Manage secrets in HashiCorp Vault Service |
| [Hazelcast](hazelcast-summary.md) | camel-hazelcast |  | 2.7 |  |
| [Hazelcast Atomic Number](hazelcast-atomicvalue-component.md) | camel-hazelcast | Stable-deprecated | 2.7 | Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number). |
| [Hazelcast Instance](hazelcast-instance-component.md) | camel-hazelcast | Stable | 2.7 | Consume join/leave events of a cache instance in a Hazelcast cluster. |
| [Hazelcast List](hazelcast-list-component.md) | camel-hazelcast | Stable | 2.7 | Perform operations on Hazelcast distributed list. |
| [Hazelcast Map](hazelcast-map-component.md) | camel-hazelcast | Stable | 2.7 | Perform operations on Hazelcast distributed map. |
| [Hazelcast Multimap](hazelcast-multimap-component.md) | camel-hazelcast | Stable | 2.7 | Perform operations on Hazelcast distributed multimap. |
| [Hazelcast PN Counter](hazelcast-pncounter-component.md) | camel-hazelcast | Stable | 4.19 | Increment, decrement, get, etc. operations on a Hazelcast PN Counter (CRDT counter). |
| [Hazelcast Queue](hazelcast-queue-component.md) | camel-hazelcast | Stable | 2.7 | Perform operations on Hazelcast distributed queue. |
| [Hazelcast Replicated Map](hazelcast-replicatedmap-component.md) | camel-hazelcast | Stable | 2.16 | Perform operations on Hazelcast replicated map. |
| [Hazelcast Ringbuffer](hazelcast-ringbuffer-component.md) | camel-hazelcast | Stable | 2.16 | Perform operations on Hazelcast distributed ringbuffer. |
| [Hazelcast SEDA](hazelcast-seda-component.md) | camel-hazelcast | Stable | 2.7 | Asynchronously send/receive Exchanges between Camel routes running on potentially distinct JVMs/hosts backed by Hazelcast BlockingQueue. |
| [Hazelcast Set](hazelcast-set-component.md) | camel-hazelcast | Stable | 2.7 | Perform operations on Hazelcast distributed set. |
| [Hazelcast Topic](hazelcast-topic-component.md) | camel-hazelcast | Stable | 2.15 | Send and receive messages to/from Hazelcast distributed topic. |
| [HTTP](http-component.md) | camel-http | Stable | 2.3 | Send requests to external HTTP servers using Apache HTTP Client 5.x. |
| [Huawei Cloud](hwcloud-summary.md) |  |  |  |  |
| [Huawei Cloud Face Recognition Service (FRS)](hwcloud-frs-component.md) | camel-huaweicloud-frs | Stable | 3.15 | Face Recognition Service (FRS) is an intelligent service that uses computers to process, analyze, and understand facial images based on human facial features. |
| [Huawei Cloud Image Recognition](hwcloud-imagerecognition-component.md) | camel-huaweicloud-imagerecognition | Stable | 3.12 | To identify objects, scenes, and concepts in images on Huawei Cloud |
| [Huawei Distributed Message Service (DMS)](hwcloud-dms-component.md) | camel-huaweicloud-dms | Stable | 3.12 | To integrate with a fully managed, high-performance message queuing service on Huawei Cloud |
| [Huawei FunctionGraph](hwcloud-functiongraph-component.md) | camel-huaweicloud-functiongraph | Stable | 3.11 | To call serverless functions on Huawei Cloud |
| [Huawei Identity and Access Management (IAM)](hwcloud-iam-component.md) | camel-huaweicloud-iam | Stable | 3.11 | To securely manage users on Huawei Cloud |
| [Huawei Object Storage Service (OBS)](hwcloud-obs-component.md) | camel-huaweicloud-obs | Stable | 3.12 | To provide stable, secure, efficient, and easy-to-use cloud storage service on Huawei Cloud |
| [Huawei Simple Message Notification (SMN)](hwcloud-smn-component.md) | camel-huaweicloud-smn | Stable | 3.8 | To broadcast messages and connect cloud services through notifications on Huawei Cloud |
| [Hugging Face](huggingface-component.md) | camel-huggingface | Stable | 4.19 | Integration with Hugging Face’s Model Hub by using the Deep Java Library (DJL) Python bridge |
| [IBM](ibm-summary.md) |  |  |  |  |
| [IBM Cloud Object Storage](ibm-cos-component.md) | camel-ibm-cos | Stable | 4.16 | Store and retrieve objects from IBM Cloud Object Storage. |
| [IBM Secrets Manager](ibm-secrets-manager-component.md) | camel-ibm-secrets-manager | Stable | 4.11 | Manage secrets in IBM Secrets Manager Service |
| [IBM Watson Discovery](ibm-watson-discovery-component.md) | camel-ibm-watson-discovery | Stable | 4.16 | Perform document understanding and search using IBM Watson Discovery |
| [IBM Watson Language](ibm-watson-language-component.md) | camel-ibm-watson-language | Stable | 4.16 | Perform natural language processing using IBM Watson Natural Language Understanding |
| [IBM Watson Speech to Text](ibm-watson-speech-to-text-component.md) | camel-ibm-watson-speech-to-text | Stable | 4.17 | Convert speech audio to text using IBM Watson Speech to Text |
| [IBM Watson Text to Speech](ibm-watson-text-to-speech-component.md) | camel-ibm-watson-text-to-speech | Stable | 4.17 | Convert text to natural-sounding speech using IBM Watson Text to Speech |
| [IBM watsonx.ai](ibm-watsonx-ai-component.md) | camel-ibm-watsonx-ai | Stable | 4.18 | Interact with IBM watsonx.ai foundation models for text generation, chat, embeddings, and more. |
| [IBM watsonx.data](ibm-watsonx-data-component.md) | camel-ibm-watsonx-data | Stable | 4.19 | Interact with IBM watsonx.data lakehouse for catalog, schema, table, and engine management. |
| [Iggy](iggy-component.md) | camel-iggy | Preview | 4.17 | Send and receive message to Apache Iggy streaming platform. |
| [Ignite](ignite-summary.md) | camel-ignite |  | 2.17 |  |
| [Ignite Cache](ignite-cache-component.md) | camel-ignite | Stable | 2.17 | Perform cache operations on an Ignite cache or consume changes from a continuous query. |
| [Ignite Compute](ignite-compute-component.md) | camel-ignite | Stable | 2.17 | Run compute operations on an Ignite cluster. |
| [Ignite Events](ignite-events-component.md) | camel-ignite | Stable | 2.17 | Receive events from an Ignite cluster by creating a local event listener. |
| [Ignite ID Generator](ignite-idgen-component.md) | camel-ignite | Stable | 2.17 | Interact with Ignite Atomic Sequences and ID Generators . |
| [Ignite Messaging](ignite-messaging-component.md) | camel-ignite | Stable | 2.17 | Send and receive messages from an Ignite topic. |
| [Ignite Queues](ignite-queue-component.md) | camel-ignite | Stable | 2.17 | Interact with Ignite Queue data structures. |
| [Ignite Sets](ignite-set-component.md) | camel-ignite | Stable | 2.17 | Interact with Ignite Set data structures. |
| [Infinispan](infinispan-component.md) | camel-infinispan | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [Infinispan Embedded](infinispan-embedded-component.md) | camel-infinispan-embedded | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [InfluxDB](influxdb-component.md) | camel-influxdb | Stable | 2.18 | Interact with InfluxDB v1, a time series database. |
| [InfluxDB2](influxdb2-component.md) | camel-influxdb2 | Stable | 3.20 | Interact with InfluxDB v2, a time series database. |
| [JCache](jcache-component.md) | camel-jcache | Stable | 2.17 | Perform caching operations against JSR107/JCache. |
| [JCR](jcr-component.md) | camel-jcr | Stable | 1.3 | Read and write nodes to/from a JCR compliant content repository. |
| [JDBC](jdbc-component.md) | camel-jdbc | Stable | 1.2 | Access databases through SQL and JDBC. |
| [Jetty](jetty-component.md) | camel-jetty | Stable | 1.2 | Expose HTTP endpoints using Jetty 12. |
| [JGroups](jgroups-component.md) | camel-jgroups | Stable | 2.13 | Exchange messages with JGroups clusters. |
| [JGroups raft](jgroups-raft-component.md) | camel-jgroups-raft | Stable | 2.24 | Exchange messages with JGroups-raft clusters. |
| [Jira](jira-component.md) | camel-jira | Stable | 3.0 | Interact with JIRA issue tracker. |
| [JMS](jms-component.md) | camel-jms | Stable | 1.0 | Send and receive messages to/from JMS message brokers. |
| [JMX](jmx-component.md) | camel-jmx | Stable | 2.6 | Receive JMX notifications. |
| [JOLT](jolt-component.md) | camel-jolt | Stable | 2.16 | JSON to JSON transformation using JOLT. |
| [JOOQ](jooq-component.md) | camel-jooq | Stable | 3.0 | Store and retrieve Java objects from an SQL database using JOOQ. |
| [JPA](jpa-component.md) | camel-jpa | Stable | 1.0 | Store and retrieve Java objects from databases using Java Persistence API (JPA). |
| [JSLT](jslt-component.md) | camel-jslt | Stable | 3.1 | Query or transform JSON payloads using JSLT. |
| [JSON Schema Validator](json-validator-component.md) | camel-json-validator | Stable | 2.20 | Validate JSON payloads using NetworkNT JSON Schema. |
| [JSONata](jsonata-component.md) | camel-jsonata | Stable | 3.5 | Transforms JSON payload using JSONata transformation. |
| [JT400](jt400-component.md) | camel-jt400 | Stable | 1.5 | Exchanges messages with an IBM i system using data queues, message queues, or program call. IBM i is the replacement for AS/400 and iSeries servers. |
| [JTE](jte-component.md) | camel-jte | Stable | 4.4 | Transform messages using a Java based template engine (JTE). |
| [Kafka](kafka-component.md) | camel-kafka | Stable | 2.13 | Send and receive messages to/from an Apache Kafka broker. |
| [Keycloak](keycloak-component.md) | camel-keycloak | Stable | 4.15 | Manage Keycloak instances via Admin API. |
| [Knative](knative-component.md) | camel-knative | Stable | 3.15 | Send and receive events from Knative. |
| [Knative Http](knative-http-component.md) | camel-knative-http | Stable | 3.15 | Camel Knative HTTP |
| [KServe](kserve-component.md) | camel-kserve | Stable | 4.10 | Provide access to AI model servers with the KServe standard to run inference with remote models |
| [Kubernetes](kubernetes-summary.md) | camel-kubernetes |  | 2.17 |  |
| [Kubernetes ConfigMap](kubernetes-config-maps-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes. |
| [Kubernetes Cronjob](kubernetes-cronjob-component.md) | camel-kubernetes | Stable | 4.3 | Perform operations on Kubernetes CronJob. |
| [Kubernetes Custom Resources](kubernetes-custom-resources-component.md) | camel-kubernetes | Stable | 3.7 | Perform operations on Kubernetes Custom Resources and get notified on Deployment changes. |
| [Kubernetes Deployments](kubernetes-deployments-component.md) | camel-kubernetes | Stable | 2.20 | Perform operations on Kubernetes Deployments and get notified on Deployment changes. |
| [Kubernetes Event](kubernetes-events-component.md) | camel-kubernetes | Stable | 3.20 | Perform operations on Kubernetes Events and get notified on Events changes. |
| [Kubernetes HPA](kubernetes-hpa-component.md) | camel-kubernetes | Stable | 2.23 | Perform operations on Kubernetes Horizontal Pod Autoscalers (HPA) and get notified on HPA changes. |
| [Kubernetes Job](kubernetes-job-component.md) | camel-kubernetes | Stable | 2.23 | Perform operations on Kubernetes Jobs. |
| [Kubernetes Namespaces](kubernetes-namespaces-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Namespaces and get notified on Namespace changes. |
| [Kubernetes Nodes](kubernetes-nodes-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Nodes and get notified on Node changes. |
| [Kubernetes Persistent Volume](kubernetes-persistent-volumes-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes and get notified on Persistent Volume changes. |
| [Kubernetes Persistent Volume Claim](kubernetes-persistent-volumes-claims-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes Claims and get notified on Persistent Volumes Claim changes. |
| [Kubernetes Pods](kubernetes-pods-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Pods and get notified on Pod changes. |
| [Kubernetes Replication Controller](kubernetes-replication-controllers-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Replication Controllers and get notified on Replication Controllers changes. |
| [Kubernetes Resources Quota](kubernetes-resources-quota-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Resources Quotas. |
| [Kubernetes Secrets](kubernetes-secrets-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Secrets. |
| [Kubernetes Service Account](kubernetes-service-accounts-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Service Accounts. |
| [Kubernetes Services](kubernetes-services-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on Kubernetes Services and get notified on Service changes. |
| [Kudu](kudu-component.md) | camel-kudu | Stable | 3.0 | Interact with Apache Kudu, a free and open source column-oriented data store of the Apache Hadoop ecosystem. |
| [LangChain4j Agent](langchain4j-agent-component.md) | camel-langchain4j-agent | Preview | 4.14 | LangChain4j Agent component |
| [LangChain4j Chat](langchain4j-chat-component.md) | camel-langchain4j-chat | Stable | 4.5 | LangChain4j Chat component |
| [LangChain4j Embedding Store](langchain4j-embeddingstore-component.md) | camel-langchain4j-embeddingstore | Stable | 4.14 | Perform operations on the LangChain4jEmbeddingStores. |
| [LangChain4j Embeddings](langchain4j-embeddings-component.md) | camel-langchain4j-embeddings | Stable | 4.5 | LangChain4j Embeddings |
| [LangChain4j Web Search](langchain4j-web-search-component.md) | camel-langchain4j-web-search | Stable | 4.8 | LangChain4j Web Search Engine |
| [LDAP](ldap-component.md) | camel-ldap | Stable | 1.5 | Perform searches on LDAP servers. |
| [LDIF](ldif-component.md) | camel-ldif | Stable | 2.20 | Perform updates on an LDAP server from an LDIF body content. |
| [LLM Integration Guide](ai-llm-integration-guide.md) |  |  |  |  |
| [Lucene](lucene-component.md) | camel-lucene | Stable | 2.2 | Perform inserts or queries against Apache Lucene databases. |
| [Lumberjack](lumberjack-component.md) | camel-lumberjack | Stable | 2.18 | Receive logs messages using the Lumberjack protocol. |
| [Mail](mail-component.md) | camel-mail | Stable | 1.0 | Send and receive emails using imap, pop3 and smtp protocols. |
| [MapStruct](mapstruct-component.md) | camel-mapstruct | Stable | 3.19 | Type Conversion using MapStruct |
| [Master](master-component.md) | camel-master | Stable | 2.20 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [Metrics](metrics-component.md) | camel-metrics | Stable | 2.14 | Collect various metrics directly from Camel routes using the DropWizard metrics library. |
| [Micrometer](micrometer-component.md) | camel-micrometer | Stable | 2.22 | Collect various metrics directly from Camel routes using the Micrometer library. |
| [Milvus](milvus-component.md) | camel-milvus | Stable | 4.5 | Perform operations on the Milvus Vector Database. |
| [Mina](mina-component.md) | camel-mina | Stable | 2.10 | Socket level networking using TCP or UDP with Apache Mina 2.x. |
| [MINA SFTP](mina-sftp-component.md) | camel-mina-sftp | Stable | 4.18 | Upload and download files to/from SFTP servers using Apache MINA SSHD. |
| [Minio](minio-component.md) | camel-minio | Stable | 3.5 | Store and retrieve objects from Minio Storage Service using Minio SDK. |
| [MLLP](mllp-component.md) | camel-mllp | Stable | 2.17 | Communicate with external systems using the MLLP protocol. |
| [MongoDB](mongodb-component.md) | camel-mongodb | Stable | 2.19 | Perform operations on MongoDB documents and collections. |
| [MongoDB GridFS](mongodb-gridfs-component.md) | camel-mongodb-gridfs | Stable | 2.18 | Interact with MongoDB GridFS. |
| [Mustache](mustache-component.md) | camel-mustache | Stable | 2.12 | Transform messages using a Mustache template. |
| [MVEL](mvel-component.md) | camel-mvel | Stable | 2.12 | Transform messages using an MVEL template. |
| [MyBatis](mybatis-component.md) | camel-mybatis | Stable | 2.7 | Performs a query, poll, insert, update or delete in a relational database using MyBatis. |
| [MyBatis Bean](mybatis-bean-component.md) | camel-mybatis | Stable | 2.22 | Perform queries, inserts, updates or deletes in a relational database using MyBatis. |
| [Nats](nats-component.md) | camel-nats | Stable | 2.17 | Send and receive messages from NATS messaging system. |
| [Neo4j](neo4j-component.md) | camel-neo4j | Stable | 4.10 | Perform operations on the Neo4j Graph Database |
| [Netty](netty-component.md) | camel-netty | Stable | 2.14 | Socket level networking using TCP or UDP with Netty 4.x. |
| [Netty HTTP](netty-http-component.md) | camel-netty-http | Stable | 2.14 | Netty HTTP server and client using the Netty 4.x. |
| [OAI-PMH](oaipmh-component.md) | camel-oaipmh | Stable | 3.5 | Harvest metadata using OAI-PMH protocol |
| [Olingo2](olingo2-component.md) | camel-olingo2 | Stable-deprecated | 2.14 | Communicate with OData 2.0 services using Apache Olingo. |
| [Olingo4](olingo4-component.md) | camel-olingo4 | Stable-deprecated | 2.19 | Communicate with OData 4.0 services using Apache Olingo OData API. |
| [OPC UA Browser](milo-browse-component.md) | camel-milo | Stable | 3.15 | Connect to OPC UA servers using the binary protocol for browsing the node tree. |
| [OPC UA Client](milo-client-component.md) | camel-milo | Stable | 2.19 | Connect to OPC UA servers using the binary protocol for acquiring telemetry data. |
| [OPC UA Server](milo-server-component.md) | camel-milo | Stable | 2.19 | Make telemetry data available as an OPC UA server. |
| [OpenAI](openai-component.md) | camel-openai | Stable | 4.17 | OpenAI endpoint for chat completion, Responses API, embeddings, audio transcription, audio translation, and text-to-speech. |
| [OpenSearch](opensearch-component.md) | camel-opensearch | Stable | 4.0 | Send requests to OpenSearch via Java Client API. |
| [OpenShift Build Config](openshift-build-configs-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on OpenShift Build Configs. |
| [OpenShift Builds](openshift-builds-component.md) | camel-kubernetes | Stable | 2.17 | Perform operations on OpenShift Builds. |
| [OpenShift Deployment Configs](openshift-deploymentconfigs-component.md) | camel-kubernetes | Stable | 3.18 | Perform operations on OpenShift Deployment Configs and get notified on Deployment Config changes. |
| [OpenStack](openstack-summary.md) | camel-openstack |  | 2.19 |  |
| [OpenStack Cinder](openstack-cinder-component.md) | camel-openstack | Stable | 2.19 | Access data in OpenStack Cinder block storage. |
| [OpenStack Glance](openstack-glance-component.md) | camel-openstack | Stable | 2.19 | Manage VM images and metadata definitions in OpenStack Glance. |
| [OpenStack Keystone](openstack-keystone-component.md) | camel-openstack | Stable | 2.19 | Access OpenStack Keystone for API client authentication, service discovery and distributed multi-tenant authorization. |
| [OpenStack Neutron](openstack-neutron-component.md) | camel-openstack | Stable | 2.19 | Access OpenStack Neutron for network services. |
| [OpenStack Nova](openstack-nova-component.md) | camel-openstack | Stable | 2.19 | Access OpenStack to manage compute resources. |
| [OpenStack Swift](openstack-swift-component.md) | camel-openstack | Stable | 2.19 | Access OpenStack Swift object/blob store. |
| [OpenTelemetry Metrics](opentelemetry-metrics-component.md) | camel-opentelemetry-metrics | Stable | 4.17 | Camel metrics based on the Camel Telemetry spec |
| [OptaPlanner](optaplanner-component.md) | camel-optaplanner | Stable | 2.13 | Solve planning problems with OptaPlanner. |
| [Paho](paho-component.md) | camel-paho | Stable-deprecated | 2.16 | Communicate with MQTT message brokers using Eclipse Paho MQTT Client. |
| [Paho MQTT 5](paho-mqtt5-component.md) | camel-paho-mqtt5 | Stable | 3.8 | Communicate with MQTT message brokers using Eclipse Paho MQTT v5 Client. |
| [PDF](pdf-component.md) | camel-pdf | Stable | 2.16 | Create, modify or extract content from PDF documents. |
| [PGVector](pgvector-component.md) | camel-pgvector | Stable | 4.19 | Perform operations on the PostgreSQL pgvector Vector Database. |
| [Pinecone](pinecone-component.md) | camel-pinecone | Stable | 4.6 | Perform operations on the Pinecone Vector Database. |
| [Platform HTTP](platform-http-component.md) | camel-platform-http | Stable | 3.0 | Expose HTTP endpoints using the HTTP server available in the current platform. |
| [PLC4X](plc4x-component.md) | camel-plc4x | Stable | 3.20 | Read and write to PLC devices |
| [PostgreSQL Event](pgevent-component.md) | camel-pgevent | Stable | 2.15 | Send and receive PostgreSQL events via LISTEN and NOTIFY commands. |
| [PostgreSQL Replication Slot](pg-replication-slot-component.md) | camel-pg-replication-slot | Stable | 3.0 | Poll for PostgreSQL Write-Ahead Log (WAL) records using Streaming Replication Slots. |
| [PQC Algorithms](pqc-component.md) | camel-pqc | Stable | 4.12 | Post Quantum Cryptography Signature and Verification component. |
| [Printer](lpr-component.md) | camel-printer | Stable | 2.1 | Send print jobs to printers. |
| [Properties](properties-component.md) | camel-base | Stable | 2.3 | The properties component is used for property placeholders in your Camel application, such as endpoint URIs. |
| [PubNub](pubnub-component.md) | camel-pubnub | Stable | 2.19 | Send and receive messages to/from PubNub data stream network for connected devices. |
| [Pulsar](pulsar-component.md) | camel-pulsar | Stable | 2.24 | Send and receive messages from/to Apache Pulsar messaging system. |
| [Qdrant](qdrant-component.md) | camel-qdrant | Stable | 4.5 | Perform operations on the Qdrant Vector Database. |
| [Quartz](quartz-component.md) | camel-quartz | Stable | 2.12 | Schedule sending of messages using the Quartz 2.x scheduler. |
| [QuickFix](quickfix-component.md) | camel-quickfix | Stable | 2.1 | Open a Financial Interchange (FIX) session using an embedded QuickFix/J engine. |
| [Reactive Streams](reactive-streams-component.md) | camel-reactive-streams | Stable | 2.19 | Exchange messages with reactive stream processing libraries compatible with the reactive streams standard. |
| [REST OpenApi](rest-openapi-component.md) | camel-rest-openapi | Stable | 3.1 | To call and expose REST services using OpenAPI specification as contract. |
| [REST Postman](rest-postman-component.md) | camel-rest-postman | Preview | 4.23 | To call and expose REST services using a Postman Collection as contract. |
| [Robot Framework](robotframework-component.md) | camel-robotframework | Stable | 3.0 | Pass camel exchanges to acceptance test written in Robot DSL. |
| [RocketMQ](rocketmq-component.md) | camel-rocketmq | Stable | 3.20 | Send and receive messages from RocketMQ cluster. |
| [RSS](rss-component.md) | camel-rss | Stable | 2.0 | Poll RSS feeds. |
| [Saga](saga-component.md) | camel-saga | Stable | 2.21 | Execute custom actions within a route using the Saga EIP. |
| [Salesforce](salesforce-component.md) | camel-salesforce | Stable | 2.12 | Communicate with Salesforce using Java DTOs. |
| [SAP NetWeaver](sap-netweaver-component.md) | camel-sap-netweaver | Stable | 2.12 | Send requests to SAP NetWeaver Gateway using HTTP. |
| [Schematron](schematron-component.md) | camel-schematron | Stable | 2.15 | Validate XML payload using the Schematron Library. |
| [SCP](scp-component.md) | camel-jsch | Stable | 2.10 | Copy files to/from remote hosts using the secure copy protocol (SCP). |
| [ServiceNow](servicenow-component.md) | camel-servicenow | Stable | 2.18 | Interact with ServiceNow via its REST API. |
| [Servlet](servlet-component.md) | camel-servlet | Stable | 2.0 | Serve HTTP requests by a Servlet. |
| [SFTP](sftp-component.md) | camel-ftp | Stable | 1.1 | Upload and download files to/from SFTP servers. |
| [Shell](shell-component.md) | camel-shell | Preview | 4.21 | Camel Shell component |
| [Simple JMS](sjms-component.md) | camel-sjms | Stable | 2.11 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 1.x API. |
| [Simple JMS2](sjms2-component.md) | camel-sjms2 | Stable | 2.19 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API. |
| [Slack](slack-component.md) | camel-slack | Stable | 2.16 | Send and receive messages to/from Slack. |
| [SMB](smb-component.md) | camel-smb | Stable | 4.3 | Read and write files to Server Message Block (SMB) file shares. |
| [Smooks](smooks-component.md) | camel-smooks | Stable | 4.7 | Use Smooks to transform, route, and bind both XML and non-XML data, including EDI, CSV, JSON, and YAML. |
| [SMPP](smpp-component.md) | camel-smpp | Stable | 2.2 | Send and receive SMS messages using a SMSC (Short Message Service Center). |
| [SNMP](snmp-component.md) | camel-snmp | Stable | 2.1 | Receive traps and poll SNMP (Simple Network Management Protocol) capable devices. |
| [Solr](solr-component.md) | camel-solr | Stable | 4.8 | Perform operations against Apache Lucene Solr. |
| [SPIFFE](spiffe-component.md) | camel-spiffe | Preview | 4.23 | Fetch and validate SPIFFE workload identity (X.509-SVID and JWT-SVID) from the SPIFFE Workload API. |
| [Splunk HEC](splunk-hec-component.md) | camel-splunk-hec | Stable | 3.3 | The splunk component allows publishing events in Splunk using the HTTP Event Collector. |
| [Spring](spring-summary.md) | camel-spring |  |  |  |
| [Spring AI Chat](spring-ai-chat-component.md) | camel-spring-ai-chat | Stable | 4.17 | Perform chat operations using Spring AI. |
| [Spring AI Embeddings](spring-ai-embeddings-component.md) | camel-spring-ai-embeddings | Stable | 4.17 | Spring AI Embeddings |
| [Spring AI Image](spring-ai-image-component.md) | camel-spring-ai-image | Stable | 4.19 | Spring AI Image Generation |
| [Spring AI Vector Store](spring-ai-vector-store-component.md) | camel-spring-ai-vector-store | Stable | 4.17 | Spring AI Vector Store |
| [Spring Batch](spring-batch-component.md) | camel-spring-batch | Stable | 2.10 | Send messages to Spring Batch for further processing. |
| [Spring Event](spring-event-component.md) | camel-spring | Stable | 1.4 | Listen for Spring Application Events. |
| [Spring JDBC](spring-jdbc-component.md) | camel-spring-jdbc | Stable | 3.10 | Access databases through SQL and JDBC with Spring Transaction support. |
| [Spring LDAP](spring-ldap-component.md) | camel-spring-ldap | Stable | 2.11 | Perform searches in LDAP servers using filters as the message payload. |
| [Spring RabbitMQ](spring-rabbitmq-component.md) | camel-spring-rabbitmq | Stable | 3.8 | Send and receive messages from RabbitMQ using the Spring RabbitMQ client. |
| [Spring Redis](spring-redis-component.md) | camel-spring-redis | Stable | 2.11 | Send and receive messages from Redis. |
| [Spring WebService](spring-ws-component.md) | camel-spring-ws | Stable | 2.6 | Access external web services as a client or expose your own web services. |
| [SQL](sql-component.md) | camel-sql | Stable | 1.4 | Perform SQL queries using Spring JDBC. |
| [SQL Stored Procedure](sql-stored-component.md) | camel-sql | Stable | 2.17 | Perform SQL queries as a JDBC Stored Procedures using Spring JDBC. |
| [SSH](ssh-component.md) | camel-ssh | Stable | 2.10 | Execute commands on remote hosts using SSH. |
| [State Store](state-store-component.md) | camel-state-store | Preview | 4.23 | Perform key-value operations against a pluggable KeyValueRepository backend. |
| [StAX](stax-component.md) | camel-stax | Stable | 2.9 | Process XML payloads by a SAX ContentHandler. |
| [Stitch](stitch-component.md) | camel-stitch | Stable | 3.8 | Stitch is a cloud ETL service that integrates various data sources into a central data warehouse through various integrations. |
| [String Template](string-template-component.md) | camel-stringtemplate | Stable | 1.2 | Transform messages using StringTemplate engine. |
| [Stripe](stripe-component.md) | camel-stripe | Preview | 4.17 | Interact with the Stripe payment platform. |
| [Tahu](tahu-summary.md) | camel-tahu | Preview | 4.8 | Sparkplug B Edge Node and Host Application support over MQTT using Eclipse Tahu |
| [Tahu Edge Node / Device](tahu-edge-component.md) | camel-tahu | Stable | 4.8 | Sparkplug B Edge Node and Device support over MQTT using Eclipse Tahu |
| [Tahu Host Application](tahu-host-component.md) | camel-tahu | Stable | 4.8 | Sparkplug B Host Application support over MQTT using Eclipse Tahu |
| [Telegram](telegram-component.md) | camel-telegram | Stable | 2.18 | Send and receive messages using the Telegram Bot API. |
| [TensorFlow Serving](tensorflow-serving-component.md) | camel-tensorflow-serving | Stable | 4.10 | Provide access to TensorFlow Serving model servers to run inference with TensorFlow saved models remotely |
| [Thrift](thrift-component.md) | camel-thrift | Stable | 2.20 | Call and expose remote procedures (RPC) with Apache Thrift data format and serialization mechanism. |
| [Thymeleaf](thymeleaf-component.md) | camel-thymeleaf | Stable | 4.1 | Transform messages using a Thymeleaf template. |
| [Tika](tika-component.md) | camel-tika | Stable | 2.19 | Parse documents and extract metadata and text using Apache Tika. |
| [Twilio](twilio-component.md) | camel-twilio | Stable | 2.20 | Interact with Twilio REST APIs using Twilio Java SDK. |
| [Twitter Direct Message](twitter-directmessage-component.md) | camel-twitter | Stable | 2.10 | Send and receive Twitter direct messages. |
| [Twitter Search](twitter-search-component.md) | camel-twitter | Stable | 2.10 | Access Twitter Search. |
| [Twitter Timeline](twitter-timeline-component.md) | camel-twitter | Stable | 2.10 | Send tweets and receive tweets from user’s timeline. |
| [Undertow](undertow-component.md) | camel-undertow | Stable | 2.16 | Expose HTTP and WebSocket endpoints and access external HTTP/WebSocket servers. |
| [Velocity](velocity-component.md) | camel-velocity | Stable | 1.2 | Transform messages using a Velocity template. |
| [Vert.x](vertx-component.md) | camel-vertx | Stable | 2.12 | Send and receive messages to/from Vert.x Event Bus. |
| [Vert.x HTTP Client](vertx-http-component.md) | camel-vertx-http | Stable | 3.5 | Send requests to external HTTP servers using Vert.x |
| [Vert.x WebSocket](vertx-websocket-component.md) | camel-vertx-websocket | Stable | 3.5 | Expose WebSocket endpoints and connect to remote WebSocket servers using Vert.x |
| [Weather](weather-component.md) | camel-weather | Stable | 2.12 | Poll the weather information from Open Weather Map. |
| [weaviate](weaviate-component.md) | camel-weaviate | Stable | 4.12 | Perform operations on the Weaviate Vector Database. |
| [Web3j Ethereum Blockchain](web3j-component.md) | camel-web3j | Stable | 2.22 | Interact with Ethereum nodes using web3j client API. |
| [Webhook](webhook-component.md) | camel-webhook | Stable | 3.0 | Expose webhook endpoints to receive push notifications for other Camel components. |
| [WhatsApp](whatsapp-component.md) | camel-whatsapp | Stable | 3.19 | Send messages to WhatsApp. |
| [WordPress](wordpress-component.md) | camel-wordpress | Stable | 2.21 | Manage posts and users using the WordPress API. |
| [Workday](workday-component.md) | camel-workday | Stable | 3.1 | Detect and parse documents using Workday. |
| [XChange](xchange-component.md) | camel-xchange | Stable | 2.21 | Access market data and trade on Bitcoin and Altcoin exchanges. |
| [XJ](xj-component.md) | camel-xj | Stable | 3.0 | Transform JSON and XML message using a XSLT. |
| [XML Security Sign](xmlsecurity-sign-component.md) | camel-xmlsecurity | Stable | 2.12 | Sign XML payloads using the XML signature specification. |
| [XML Security Verify](xmlsecurity-verify-component.md) | camel-xmlsecurity | Stable | 2.12 | Verify XML payloads using the XML signature specification. |
| [XMPP](xmpp-component.md) | camel-xmpp | Stable | 1.0 | Send and receive messages to/from an XMPP chat server. |
| [XQuery](xquery-component.md) | camel-saxon | Stable | 1.0 | Query and/or transform XML payloads using XQuery and Saxon. |
| [Zendesk](zendesk-component.md) | camel-zendesk | Stable | 2.19 | Manage Zendesk tickets, users, organizations, etc. |
| [ZooKeeper](zookeeper-component.md) | camel-zookeeper | Stable | 2.9 | Manage ZooKeeper clusters. |
| [ZooKeeper Master](zookeeper-master-component.md) | camel-zookeeper-master | Stable | 2.19 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |