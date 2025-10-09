# Component Starters

There are unused json files.

## Statistics

If this section appears in the (failed) website build, there is a mismatch between the camel spring boot starter json files, which are used to generate the spring-boot section of main camel component documentation, and the names used in those main camel component documentation pages. The names of the unused spring boot starter json files are listed below. Each of these needs to be used in a component doc page as the `camel-spring-boot-name` header attribute, like this:

```adoc
:camel-spring-boot-name: springdoc
```

There are 357 spring boot starter json files.

Of these 355 are used in components, dataformats, etc.

### Unused spring-boot-starter names

consul-cluster-service

file-cluster-service

infinispan-cluster-service

jgroups-raft-cluster-service

kubernetes-cluster-service

zookeeper-cluster-service

## Camel Spring Boot

Apache Camel Spring Boot supports the following Camel artifacts as Spring Boot Starters

## Camel Components

Number of Camel components: 351 in 288 JAR artifacts (5 deprecated)

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [ActiveMQ 5.x](../../components/4.14.x/activemq-component.md) | camel-activemq-starter | Stable | 1.0 | Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component. |
| [ActiveMQ 6.x](../../components/4.14.x/activemq6-component.md) | camel-activemq6-starter | Stable | 4.7 | Send messages to (or consume from) Apache ActiveMQ 6.x. This component extends the Camel JMS component. |
| [AMQP](../../components/4.14.x/amqp-component.md) | camel-amqp-starter | Stable | 1.2 | Messaging with AMQP protocol using Apache QPid Client. |
| [ArangoDb](../../components/4.14.x/arangodb-component.md) | camel-arangodb-starter | Stable | 3.5 | Perform operations on ArangoDb when used as a Document Database, or as a Graph Database |
| [AS2](../../components/4.14.x/as2-component.md) | camel-as2-starter | Stable | 2.22 | Transfer data securely and reliably using the AS2 protocol (RFC4130). |
| [Asterisk](../../components/4.14.x/asterisk-component.md) | camel-asterisk-starter | Stable | 2.18 | Interact with Asterisk PBX Server (VoIP). |
| [Atmosphere Websocket](../../components/4.14.x/atmosphere-websocket-component.md) | camel-atmosphere-websocket-starter | Stable | 2.14 | Expose WebSocket endpoints using the Atmosphere framework. |
| [Atom](../../components/4.14.x/atom-component.md) | camel-atom-starter | Stable | 1.2 | Poll Atom RSS feeds. |
| [Avro RPC](../../components/4.14.x/avro-component.md) | camel-avro-rpc-starter | Stable | 2.10 | Produce or consume Apache Avro RPC services. |
| [AWS Athena](../../components/4.14.x/aws2-athena-component.md) | camel-aws2-athena-starter | Stable | 3.4 | Access AWS Athena. |
| [AWS Bedrock](../../components/4.14.x/aws-bedrock-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Invoke Model of AWS Bedrock service. |
| [AWS Bedrock Agent](../../components/4.14.x/aws-bedrock-agent-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Operate on AWS Bedrock through its Agent. |
| [AWS Bedrock Agent Runtime](../../components/4.14.x/aws-bedrock-agent-runtime-component.md) | camel-aws-bedrock-starter | Stable | 4.5 | Invoke Model of AWS Bedrock Agent Runtime service. |
| [AWS Cloudtrail](../../components/4.14.x/aws-cloudtrail-component.md) | camel-aws-cloudtrail-starter | Stable | 3.19 | Consume events from Amazon Cloudtrail using AWS SDK version 2.x. |
| [AWS CloudWatch](../../components/4.14.x/aws2-cw-component.md) | camel-aws2-cw-starter | Stable | 3.1 | Sending metrics to AWS CloudWatch. |
| [AWS Config Service](../../components/4.14.x/aws-config-component.md) | camel-aws-config-starter | Stable | 4.3 | Manage AWS Config service. |
| [AWS DynamoDB](../../components/4.14.x/aws2-ddb-component.md) | camel-aws2-ddb-starter | Stable | 3.1 | Store and retrieve data from AWS DynamoDB. |
| [AWS DynamoDB Streams](../../components/4.14.x/aws2-ddbstream-component.md) | camel-aws2-ddb-starter | Stable | 3.1 | Receive messages from AWS DynamoDB Stream. |
| [AWS Elastic Compute Cloud (EC2)](../../components/4.14.x/aws2-ec2-component.md) | camel-aws2-ec2-starter | Stable | 3.1 | Manage AWS EC2 instances. |
| [AWS Elastic Container Service (ECS)](../../components/4.14.x/aws2-ecs-component.md) | camel-aws2-ecs-starter | Stable | 3.1 | Manage AWS ECS cluster instances. |
| [AWS Elastic Kubernetes Service (EKS)](../../components/4.14.x/aws2-eks-component.md) | camel-aws2-eks-starter | Stable | 3.1 | Manage AWS EKS cluster instances. |
| [AWS Eventbridge](../../components/4.14.x/aws2-eventbridge-component.md) | camel-aws2-eventbridge-starter | Stable | 3.6 | Send events to AWS Eventbridge cluster instances. |
| [AWS Identity and Access Management (IAM)](../../components/4.14.x/aws2-iam-component.md) | camel-aws2-iam-starter | Stable | 3.1 | Manage AWS IAM instances. |
| [AWS Key Management Service (KMS)](../../components/4.14.x/aws2-kms-component.md) | camel-aws2-kms-starter | Stable | 3.1 | Manage keys stored in AWS KMS instances. |
| [AWS Kinesis](../../components/4.14.x/aws2-kinesis-component.md) | camel-aws2-kinesis-starter | Stable | 3.2 | Consume and produce records from and to AWS Kinesis Streams. |
| [AWS Kinesis Firehose](../../components/4.14.x/aws2-kinesis-firehose-component.md) | camel-aws2-kinesis-starter | Stable | 3.2 | Produce data to AWS Kinesis Firehose streams. |
| [AWS Lambda](../../components/4.14.x/aws2-lambda-component.md) | camel-aws2-lambda-starter | Stable | 3.2 | Manage and invoke AWS Lambda functions. |
| [AWS Managed Streaming for Apache Kafka (MSK)](../../components/4.14.x/aws2-msk-component.md) | camel-aws2-msk-starter | Stable | 3.1 | Manage AWS MSK instances. |
| [AWS MQ](../../components/4.14.x/aws2-mq-component.md) | camel-aws2-mq-starter | Stable | 3.1 | Send messages to AWS MQ. |
| [AWS RedshiftData](../../components/4.14.x/aws2-redshift-data-component.md) | camel-aws2-redshift-starter | Stable | 4.1 | Perform operations on AWS Redshift using Redshift Data API. |
| [AWS S3 Storage Service](../../components/4.14.x/aws2-s3-component.md) | camel-aws2-s3-starter | Stable | 3.2 | Store and retrieve objects from AWS S3 Storage Service. |
| [AWS Secrets Manager](../../components/4.14.x/aws-secrets-manager-component.md) | camel-aws-secrets-manager-starter | Stable | 3.9 | Manage secrets using AWS Secrets Manager. |
| [AWS Security Token Service (STS)](../../components/4.14.x/aws2-sts-component.md) | camel-aws2-sts-starter | Stable | 3.5 | Manage AWS STS cluster instances. |
| [AWS Simple Email Service (SES)](../../components/4.14.x/aws2-ses-component.md) | camel-aws2-ses-starter | Stable | 3.1 | Send e-mails through AWS SES service. |
| [AWS Simple Notification System (SNS)](../../components/4.14.x/aws2-sns-component.md) | camel-aws2-sns-starter | Stable | 3.1 | Send messages to AWS Simple Notification Topic. |
| [AWS Simple Queue Service (SQS)](../../components/4.14.x/aws2-sqs-component.md) | camel-aws2-sqs-starter | Stable | 3.1 | Send and receive messages to/from AWS SQS. |
| [AWS StepFunctions](../../components/4.14.x/aws2-step-functions-component.md) | camel-aws2-step-functions-starter | Stable | 4.0 | Manage and invoke AWS Step functions. |
| [AWS Timestream](../../components/4.14.x/aws2-timestream-component.md) | camel-aws2-timestream-starter | Stable | 4.1 | Write records and execute queries on AWS time-series database |
| [AWS Translate](../../components/4.14.x/aws2-translate-component.md) | camel-aws2-translate-starter | Stable | 3.1 | Translate texts using AWS Translate and AWS SDK version 2.x. |
| [Azure CosmosDB](../../components/4.14.x/azure-cosmosdb-component.md) | camel-azure-cosmosdb-starter | Stable | 3.10 | To read and write records to the CosmosDB database on Azure cloud platform. |
| [Azure Event Hubs](../../components/4.14.x/azure-eventhubs-component.md) | camel-azure-eventhubs-starter | Stable | 3.5 | Send and receive events to/from Azure Event Hubs using AMQP protocol. |
| [Azure Files](../../components/4.14.x/azure-files-component.md) | camel-azure-files-starter | Preview | 3.22 | Send and receive files to Azure storage file share |
| [Azure Key Vault](../../components/4.14.x/azure-key-vault-component.md) | camel-azure-key-vault-starter | Stable | 3.17 | Manage secrets and keys in Azure Key Vault Service |
| [Azure ServiceBus](../../components/4.14.x/azure-servicebus-component.md) | camel-azure-servicebus-starter | Stable | 3.12 | Send and receive messages to/from Azure Service Bus. |
| [Azure Storage Blob Service](../../components/4.14.x/azure-storage-blob-component.md) | camel-azure-storage-blob-starter | Stable | 3.3 | Store and retrieve blobs from Azure Storage Blob Service. |
| [Azure Storage Data Lake Service](../../components/4.14.x/azure-storage-datalake-component.md) | camel-azure-storage-datalake-starter | Stable | 3.8 | Sends and receives files to/from Azure Data Lake Storage. |
| [Azure Storage Queue Service](../../components/4.14.x/azure-storage-queue-component.md) | camel-azure-storage-queue-starter | Stable | 3.3 | Stores and retrieves messages to/from Azure Storage Queue. |
| [Bean](../../components/4.14.x/bean-component.md) | camel-bean-starter | Stable | 1.0 | Invoke methods of Java beans stored in Camel registry. |
| [Bean Validator](../../components/4.14.x/bean-validator-component.md) | camel-bean-validator-starter | Stable | 2.3 | Validate the message body using the Java Bean Validation API. |
| [Bonita](../../components/4.14.x/bonita-component.md) | camel-bonita-starter | Stable | 2.19 | Communicate with a remote Bonita BPM process engine. |
| [Box](../../components/4.14.x/box-component.md) | camel-box-starter | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc. on box.com. |
| [Braintree](../../components/4.14.x/braintree-component.md) | camel-braintree-starter | Stable | 2.17 | Process payments using Braintree Payments. |
| [Browse](../../components/4.14.x/browse-component.md) | camel-browse-starter | Stable | 1.3 | Inspect the messages received on endpoints supporting BrowsableEndpoint. |
| [Caffeine Cache](../../components/4.14.x/caffeine-cache-component.md) | camel-caffeine-starter | Stable | 2.20 | Perform caching operations using Caffeine Cache. |
| [Caffeine LoadCache](../../components/4.14.x/caffeine-loadcache-component.md) | camel-caffeine-starter | Stable | 2.20 | Perform caching operations using Caffeine Cache with an attached CacheLoader. |
| [Cassandra CQL](../../components/4.14.x/cql-component.md) | camel-cassandraql-starter | Stable | 2.15 | Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax. |
| [ChatScript](../../components/4.14.x/chatscript-component.md) | camel-chatscript-starter | Stable | 3.0 | Chat with a ChatScript Server. |
| [Chunk](../../components/4.14.x/chunk-component.md) | camel-chunk-starter | Stable | 2.15 | Transform messages using Chunk templating engine. |
| [Class](../../components/4.14.x/class-component.md) | camel-bean-starter | Stable | 2.4 | Invoke methods of Java beans specified by class name. |
| [ClickUp](../../components/4.14.x/clickup-component.md) | camel-clickup-starter | Preview | 4.9 | Receives events from ClickUp |
| [CM SMS Gateway](../../components/4.14.x/cm-sms-component.md) | camel-cm-sms-starter | Stable | 2.18 | Send SMS messages via CM SMS Gateway. |
| [CoAP](../../components/4.14.x/coap-component.md) | camel-coap-starter | Stable | 2.16 | Send and receive messages to/from CoAP (Constrained Application Protocol) capable devices. |
| [CometD](../../components/4.14.x/cometd-component.md) | camel-cometd-starter | Stable | 2.0 | Offers publish/subscribe, peer-to-peer (via a server), and RPC style messaging using the CometD/Bayeux protocol. |
| [Consul](../../components/4.14.x/consul-component.md) | camel-consul-starter | Stable | 2.18 | Integrate with Consul service discovery and configuration store. |
| [Control Bus](../../components/4.14.x/controlbus-component.md) | camel-controlbus-starter | Stable | 2.11 | Manage and monitor Camel routes. |
| [Couchbase](../../components/4.14.x/couchbase-component.md) | camel-couchbase-starter | Stable | 2.19 | Query Couchbase Views with a poll strategy and/or perform various operations against Couchbase databases. |
| [CouchDB](../../components/4.14.x/couchdb-component.md) | camel-couchdb-starter | Stable | 2.11 | Consume changesets for inserts, updates and deletes in a CouchDB database, as well as get, save, update and delete documents from a CouchDB database. |
| [Cron](../../components/4.14.x/cron-component.md) | camel-cron-starter | Stable | 3.1 | A generic interface for triggering events at times specified through the Unix cron syntax. |
| [Crypto (JCE)](../../components/4.14.x/crypto-component.md) | camel-crypto-starter | Stable | 2.3 | Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE). |
| [CXF](../../components/4.14.x/cxf-component.md) | camel-cxf-soap-starter | Stable | 1.0 | Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client. |
| [CXF-RS](../../components/4.14.x/cxfrs-component.md) | camel-cxf-rest-starter | Stable | 2.0 | Expose JAX-RS REST services using Apache CXF or connect to external REST services using CXF REST client. |
| [Dapr](../../components/4.14.x/dapr-component.md) | camel-dapr-starter | Stable | 4.12 | Dapr component which interfaces with Dapr Building Blocks. |
| [Data Format](../../components/4.14.x/dataformat-component.md) | camel-dataformat-starter | Stable | 2.12 | Use a Camel Data Format as a regular Camel Component. |
| [Dataset](../../components/4.14.x/dataset-component.md) | camel-dataset-starter | Stable | 1.3 | Provide data for load and soak testing of your Camel application. |
| [DataSet Test](../../components/4.14.x/dataset-test-component.md) | camel-dataset-starter | Stable | 1.3 | Extends the mock component by pulling messages from another endpoint on startup to set the expected message bodies. |
| [Debezium DB2 Connector](../../components/4.14.x/debezium-db2-component.md) | camel-debezium-db2-starter | Stable | 3.17 | Capture changes from a DB2 database. |
| [Debezium MongoDB Connector](../../components/4.14.x/debezium-mongodb-component.md) | camel-debezium-mongodb-starter | Stable | 3.0 | Capture changes from a MongoDB database. |
| [Debezium MySQL Connector](../../components/4.14.x/debezium-mysql-component.md) | camel-debezium-mysql-starter | Stable | 3.0 | Capture changes from a MySQL database. |
| [Debezium Oracle Connector](../../components/4.14.x/debezium-oracle-component.md) | camel-debezium-oracle-starter | Stable | 3.17 | Capture changes from an Oracle database. |
| [Debezium PostgresSQL Connector](../../components/4.14.x/debezium-postgres-component.md) | camel-debezium-postgres-starter | Stable | 3.0 | Capture changes from a PostgresSQL database. |
| [Debezium SQL Server Connector](../../components/4.14.x/debezium-sqlserver-component.md) | camel-debezium-sqlserver-starter | Stable | 3.0 | Capture changes from an SQL Server database. |
| [Deep Java Library](../../components/4.14.x/djl-component.md) | camel-djl-starter | Stable | 3.3 | Infer Deep Learning models from message exchanges data using Deep Java Library (DJL). |
| [DFDL](../../components/4.14.x/dfdl-component.md) | camel-dfdl-starter | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [DHIS2](../../components/4.14.x/dhis2-component.md) | camel-dhis2-starter | Stable | 4.0 | Leverages the DHIS2 Java SDK to integrate Apache Camel with the DHIS2 Web API. |
| [DigitalOcean](../../components/4.14.x/digitalocean-component.md) | camel-digitalocean-starter | Stable | 2.19 | Manage Droplets and resources within the DigitalOcean cloud. |
| [Direct](../../components/4.14.x/direct-component.md) | camel-direct-starter | Stable | 1.0 | Call another endpoint from the same Camel Context synchronously. |
| [Disruptor](../../components/4.14.x/disruptor-component.md) | camel-disruptor-starter | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [Disruptor VM](../../components/4.14.x/disruptor-vm-component.md) | camel-disruptor-starter | Stable | 2.12 | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [DNS](../../components/4.14.x/dns-component.md) | camel-dns-starter | Stable | 2.7 | Perform DNS queries using DNSJava. |
| [Docker](../../components/4.14.x/docker-component.md) | camel-docker-starter | Stable | 2.15 | Manage Docker containers. |
| [Drill](../../components/4.14.x/drill-component.md) | camel-drill-starter | Stable | 2.19 | Perform queries against an Apache Drill cluster. |
| [Dropbox](../../components/4.14.x/dropbox-component.md) | camel-dropbox-starter | Stable | 2.14 | Upload, download and manage files, folders, groups, collaborations, etc on Dropbox. |
| [Dynamic Router](../../components/4.14.x/dynamic-router-component.md) | camel-dynamic-router-starter | Stable | 3.15 | The Dynamic Router component routes exchanges to recipients, and the recipients (and their rules) may change at runtime. |
| [Dynamic Router Control](../../components/4.14.x/dynamic-router-control-component.md) | camel-dynamic-router-starter | Stable | 4.4 | The Dynamic Router control endpoint for operations that allow routing participants to subscribe or unsubscribe to participate in dynamic message routing. |
| [Ehcache](../../components/4.14.x/ehcache-component.md) | camel-ehcache-starter | Stable | 2.18 | Perform caching operations using Ehcache. |
| [Elasticsearch](../../components/4.14.x/elasticsearch-component.md) | camel-elasticsearch-starter | Stable | 3.19 | Send requests to ElasticSearch via Java Client API. |
| [Elasticsearch Low level Rest Client](../../components/4.14.x/elasticsearch-rest-client-component.md) | camel-elasticsearch-rest-client-starter | Stable | 4.3 | Perform queries and other operations on Elasticsearch or OpenSearch (uses low-level client). |
| [Exec](../../components/4.14.x/exec-component.md) | camel-exec-starter | Stable | 2.3 | Execute commands on the underlying operating system. |
| [FHIR](../../components/4.14.x/fhir-component.md) | camel-fhir-starter | Stable | 2.23 | Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. |
| [File](../../components/4.14.x/file-component.md) | camel-file-starter | Stable | 1.0 | Read and write files. |
| [File Watch](../../components/4.14.x/file-watch-component.md) | camel-file-watch-starter | Stable | 3.0 | Get notified about file events in a directory using java.nio.file.WatchService. |
| [Flatpack](../../components/4.14.x/flatpack-component.md) | camel-flatpack-starter | Stable | 1.4 | Parse fixed width and delimited files using the FlatPack library. |
| [Flink](../../components/4.14.x/flink-component.md) | camel-flink-starter | Stable | 2.18 | Send DataSet jobs to an Apache Flink cluster. |
| [Flowable](../../components/4.14.x/flowable-component.md) | camel-flowable-starter | Preview | 4.9 | Send and receive messages from the Flowable BPMN and CMMN engines. |
| [FOP](../../components/4.14.x/fop-component.md) | camel-fop-starter | Stable | 2.10 | Render messages into PDF and other output formats supported by Apache FOP. |
| [Freemarker](../../components/4.14.x/freemarker-component.md) | camel-freemarker-starter | Stable | 2.10 | Transform messages using FreeMarker templates. |
| [FTP](../../components/4.14.x/ftp-component.md) | camel-ftp-starter | Stable | 1.1 | Upload and download files to/from FTP servers. |
| [FTPS](../../components/4.14.x/ftps-component.md) | camel-ftp-starter | Stable | 2.2 | Upload and download files to/from FTP servers supporting the FTPS protocol. |
| [Geocoder](../../components/4.14.x/geocoder-component.md) | camel-geocoder-starter | Stable | 2.12 | Find geocodes (latitude and longitude) for a given address or the other way round. |
| [Git](../../components/4.14.x/git-component.md) | camel-git-starter | Stable | 2.16 | Perform operations on git repositories. |
| [GitHub](../../components/4.14.x/github-component.md) | camel-github-starter | Stable | 2.15 | Interact with the GitHub API. |
| [Google BigQuery](../../components/4.14.x/google-bigquery-component.md) | camel-google-bigquery-starter | Stable | 2.20 | Google BigQuery data warehouse for analytics. |
| [Google BigQuery Standard SQL](../../components/4.14.x/google-bigquery-sql-component.md) | camel-google-bigquery-starter | Stable | 2.23 | Access Google Cloud BigQuery service using SQL queries. |
| [Google Calendar](../../components/4.14.x/google-calendar-component.md) | camel-google-calendar-starter | Stable | 2.15 | Perform various operations on a Google Calendar. |
| [Google Calendar Stream](../../components/4.14.x/google-calendar-stream-component.md) | camel-google-calendar-starter | Stable | 2.23 | Poll for changes in a Google Calendar. |
| [Google Cloud Functions](../../components/4.14.x/google-functions-component.md) | camel-google-functions-starter | Stable | 3.9 | Manage and invoke Google Cloud Functions |
| [Google Drive](../../components/4.14.x/google-drive-component.md) | camel-google-drive-starter | Stable | 2.14 | Manage files in Google Drive. |
| [Google Mail](../../components/4.14.x/google-mail-component.md) | camel-google-mail-starter | Stable | 2.15 | Manage messages in Google Mail. |
| [Google Mail Stream](../../components/4.14.x/google-mail-stream-component.md) | camel-google-mail-starter | Stable | 2.22 | Poll for incoming messages in Google Mail. |
| [Google Pubsub](../../components/4.14.x/google-pubsub-component.md) | camel-google-pubsub-starter | Stable | 2.19 | Send and receive messages to/from Google Cloud Platform PubSub Service. |
| [Google PubSub Lite](../../components/4.14.x/google-pubsub-lite-component.md) | camel-google-pubsub-lite-starter | Stable-deprecated | 4.6 | Send and receive messages to/from Google Cloud Platform PubSub Lite Service. |
| [Google Secret Manager](../../components/4.14.x/google-secret-manager-component.md) | camel-google-secret-manager-starter | Stable | 3.16 | Manage Google Secret Manager Secrets |
| [Google Sheets](../../components/4.14.x/google-sheets-component.md) | camel-google-sheets-starter | Stable | 2.23 | Manage spreadsheets in Google Sheets. |
| [Google Sheets Stream](../../components/4.14.x/google-sheets-stream-component.md) | camel-google-sheets-starter | Stable | 2.23 | Poll for changes in Google Sheets. |
| [Google Storage](../../components/4.14.x/google-storage-component.md) | camel-google-storage-starter | Stable | 3.9 | Store and retrieve objects from Google Cloud Storage Service using the google-cloud-storage library. |
| [Grape](../../components/4.14.x/grape-component.md) | camel-grape-starter | Stable-deprecated | 2.16 | Fetch, load and manage additional jars dynamically after Camel Context was started. |
| [GraphQL](../../components/4.14.x/graphql-component.md) | camel-graphql-starter | Stable | 3.0 | Send GraphQL queries and mutations to external systems. |
| [gRPC](../../components/4.14.x/grpc-component.md) | camel-grpc-starter | Stable | 2.19 | Expose gRPC endpoints and access external gRPC endpoints. |
| [Guava EventBus](../../components/4.14.x/guava-eventbus-component.md) | camel-guava-eventbus-starter | Stable-deprecated | 2.10 | Send and receive messages to/from Guava EventBus. |
| [Hashicorp Vault](../../components/4.14.x/hashicorp-vault-component.md) | camel-hashicorp-vault-starter | Stable | 3.18 | Manage secrets in Hashicorp Vault Service |
| [Hazelcast Atomic Number](../../components/4.14.x/hazelcast-atomicvalue-component.md) | camel-hazelcast-starter | Stable | 2.7 | Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number). |
| [Hazelcast Instance](../../components/4.14.x/hazelcast-instance-component.md) | camel-hazelcast-starter | Stable | 2.7 | Consume join/leave events of a cache instance in a Hazelcast cluster. |
| [Hazelcast List](../../components/4.14.x/hazelcast-list-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed list. |
| [Hazelcast Map](../../components/4.14.x/hazelcast-map-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed map. |
| [Hazelcast Multimap](../../components/4.14.x/hazelcast-multimap-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed multimap. |
| [Hazelcast Queue](../../components/4.14.x/hazelcast-queue-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed queue. |
| [Hazelcast Replicated Map](../../components/4.14.x/hazelcast-replicatedmap-component.md) | camel-hazelcast-starter | Stable | 2.16 | Perform operations on Hazelcast replicated map. |
| [Hazelcast Ringbuffer](../../components/4.14.x/hazelcast-ringbuffer-component.md) | camel-hazelcast-starter | Stable | 2.16 | Perform operations on Hazelcast distributed ringbuffer. |
| [Hazelcast SEDA](../../components/4.14.x/hazelcast-seda-component.md) | camel-hazelcast-starter | Stable | 2.7 | Asynchronously send/receive Exchanges between Camel routes running on potentially distinct JVMs/hosts backed by Hazelcast BlockingQueue. |
| [Hazelcast Set](../../components/4.14.x/hazelcast-set-component.md) | camel-hazelcast-starter | Stable | 2.7 | Perform operations on Hazelcast distributed set. |
| [Hazelcast Topic](../../components/4.14.x/hazelcast-topic-component.md) | camel-hazelcast-starter | Stable | 2.15 | Send and receive messages to/from Hazelcast distributed topic. |
| [HTTP](../../components/4.14.x/http-component.md) | camel-http-starter | Stable | 2.3 | Send requests to external HTTP servers using Apache HTTP Client 5.x. |
| [Huawei Cloud Face Recognition Service (FRS)](../../components/4.14.x/hwcloud-frs-component.md) | camel-huaweicloud-frs-starter | Stable | 3.15 | Face Recognition Service (FRS) is an intelligent service that uses computers to process, analyze, and understand facial images based on human facial features. |
| [Huawei Cloud Image Recognition](../../components/4.14.x/hwcloud-imagerecognition-component.md) | camel-huaweicloud-imagerecognition-starter | Stable | 3.12 | To identify objects, scenes, and concepts in images on Huawei Cloud |
| [Huawei Distributed Message Service (DMS)](../../components/4.14.x/hwcloud-dms-component.md) | camel-huaweicloud-dms-starter | Stable | 3.12 | To integrate with a fully managed, high-performance message queuing service on Huawei Cloud |
| [Huawei FunctionGraph](../../components/4.14.x/hwcloud-functiongraph-component.md) | camel-huaweicloud-functiongraph-starter | Stable | 3.11 | To call serverless functions on Huawei Cloud |
| [Huawei Identity and Access Management (IAM)](../../components/4.14.x/hwcloud-iam-component.md) | camel-huaweicloud-iam-starter | Stable | 3.11 | To securely manage users on Huawei Cloud |
| [Huawei Object Storage Service (OBS)](../../components/4.14.x/hwcloud-obs-component.md) | camel-huaweicloud-obs-starter | Stable | 3.12 | To provide stable, secure, efficient, and easy-to-use cloud storage service on Huawei Cloud |
| [Huawei Simple Message Notification (SMN)](../../components/4.14.x/hwcloud-smn-component.md) | camel-huaweicloud-smn-starter | Stable | 3.8 | To broadcast messages and connect cloud services through notifications on Huawei Cloud |
| [IBM Secrets Manager](../../components/4.14.x/ibm-secrets-manager-component.md) | camel-ibm-secrets-manager-starter | Stable | 4.11 | Manage secrets in IBM Secrets Manager Service |
| [IEC 60870 Client](../../components/4.14.x/iec60870-client-component.md) | camel-iec60870-starter | Stable | 2.20 | IEC 60870 supervisory control and data acquisition (SCADA) client using NeoSCADA implementation. |
| [IEC 60870 Server](../../components/4.14.x/iec60870-server-component.md) | camel-iec60870-starter | Stable | 2.20 | IEC 60870 supervisory control and data acquisition (SCADA) server using NeoSCADA implementation. |
| [Ignite Cache](../../components/4.14.x/ignite-cache-component.md) | camel-ignite-starter | Stable | 2.17 | Perform cache operations on an Ignite cache or consume changes from a continuous query. |
| [Ignite Compute](../../components/4.14.x/ignite-compute-component.md) | camel-ignite-starter | Stable | 2.17 | Run compute operations on an Ignite cluster. |
| [Ignite Events](../../components/4.14.x/ignite-events-component.md) | camel-ignite-starter | Stable | 2.17 | Receive events from an Ignite cluster by creating a local event listener. |
| [Ignite ID Generator](../../components/4.14.x/ignite-idgen-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Atomic Sequences and ID Generators . |
| [Ignite Messaging](../../components/4.14.x/ignite-messaging-component.md) | camel-ignite-starter | Stable | 2.17 | Send and receive messages from an Ignite topic. |
| [Ignite Queues](../../components/4.14.x/ignite-queue-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Queue data structures. |
| [Ignite Sets](../../components/4.14.x/ignite-set-component.md) | camel-ignite-starter | Stable | 2.17 | Interact with Ignite Set data structures. |
| [Infinispan](../../components/4.14.x/infinispan-component.md) | camel-infinispan-starter | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [Infinispan Embedded](../../components/4.14.x/infinispan-embedded-component.md) | camel-infinispan-embedded-starter | Stable | 2.13 | Read and write from/to Infinispan distributed key/value store and data grid. |
| [InfluxDB](../../components/4.14.x/influxdb-component.md) | camel-influxdb-starter | Stable | 2.18 | Interact with InfluxDB v1, a time series database. |
| [InfluxDB2](../../components/4.14.x/influxdb2-component.md) | camel-influxdb2-starter | Stable | 3.20 | Interact with InfluxDB v2, a time series database. |
| [IRC](../../components/4.14.x/irc-component.md) | camel-irc-starter | Stable | 1.1 | Send and receive messages to/from and IRC chat. |
| [IronMQ](../../components/4.14.x/ironmq-component.md) | camel-ironmq-starter | Stable | 2.17 | Send and receive messages to/from IronMQ an elastic and durable hosted message queue as a service. |
| [JCache](../../components/4.14.x/jcache-component.md) | camel-jcache-starter | Stable | 2.17 | Perform caching operations against JSR107/JCache. |
| [JCR](../../components/4.14.x/jcr-component.md) | camel-jcr-starter | Stable | 1.3 | Read and write nodes to/from a JCR compliant content repository. |
| [JDBC](../../components/4.14.x/jdbc-component.md) | camel-jdbc-starter | Stable | 1.2 | Access databases through SQL and JDBC. |
| [Jetty](../../components/4.14.x/jetty-component.md) | camel-jetty-starter | Stable | 1.2 | Expose HTTP endpoints using Jetty 12. |
| [JGroups](../../components/4.14.x/jgroups-component.md) | camel-jgroups-starter | Stable | 2.13 | Exchange messages with JGroups clusters. |
| [JGroups raft](../../components/4.14.x/jgroups-raft-component.md) | camel-jgroups-raft-starter | Stable | 2.24 | Exchange messages with JGroups-raft clusters. |
| [Jira](../../components/4.14.x/jira-component.md) | camel-jira-starter | Stable | 3.0 | Interact with JIRA issue tracker. |
| [JMS](../../components/4.14.x/jms-component.md) | camel-jms-starter | Stable | 1.0 | Send and receive messages to/from JMS message brokers. |
| [JMX](../../components/4.14.x/jmx-component.md) | camel-jmx-starter | Stable | 2.6 | Receive JMX notifications. |
| [JOLT](../../components/4.14.x/jolt-component.md) | camel-jolt-starter | Stable | 2.16 | JSON to JSON transformation using JOLT. |
| [JOOQ](../../components/4.14.x/jooq-component.md) | camel-jooq-starter | Stable | 3.0 | Store and retrieve Java objects from an SQL database using JOOQ. |
| [JPA](../../components/4.14.x/jpa-component.md) | camel-jpa-starter | Stable | 1.0 | Store and retrieve Java objects from databases using Java Persistence API (JPA). |
| [JSLT](../../components/4.14.x/jslt-component.md) | camel-jslt-starter | Stable | 3.1 | Query or transform JSON payloads using JSLT. |
| [JSON Schema Validator](../../components/4.14.x/json-validator-component.md) | camel-json-validator-starter | Stable | 2.20 | Validate JSON payloads using NetworkNT JSON Schema. |
| [JSONata](../../components/4.14.x/jsonata-component.md) | camel-jsonata-starter | Stable | 3.5 | Transforms JSON payload using JSONata transformation. |
| [JsonPatch](../../components/4.14.x/json-patch-component.md) | camel-json-patch-starter | Stable | 3.12 | Transforms JSON using JSON patch (RFC 6902). |
| [JT400](../../components/4.14.x/jt400-component.md) | camel-jt400-starter | Stable | 1.5 | Exchanges messages with an IBM i system using data queues, message queues, or program call. IBM i is the replacement for AS/400 and iSeries servers. |
| [JTE](../../components/4.14.x/jte-component.md) | camel-jte-starter | Stable | 4.4 | Transform messages using a Java based template engine (JTE). |
| [Kafka](../../components/4.14.x/kafka-component.md) | camel-kafka-starter | Stable | 2.13 | Send and receive messages to/from an Apache Kafka broker. |
| [Kamelet](../../components/4.14.x/kamelet-component.md) | camel-kamelet-starter | Stable | 3.8 | To call Kamelets |
| [Knative](../../components/4.14.x/knative-component.md) | camel-knative-starter | Stable | 3.15 | Send and receive events from Knative. |
| [Knative Http](../../components/4.14.x/knative-http-component.md) | camel-knative-http-starter | Stable | 3.15 | Camel Knative HTTP |
| [KServe](../../components/4.14.x/kserve-component.md) | camel-kserve-starter | Stable | 4.10 | Provide access to AI model servers with the KServe standard to run inference with remote models |
| [Kubernetes ConfigMap](../../components/4.14.x/kubernetes-config-maps-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes. |
| [Kubernetes Cronjob](../../components/4.14.x/kubernetes-cronjob-component.md) | camel-kubernetes-starter | Stable | 4.3 | Perform operations on Kubernetes CronJob. |
| [Kubernetes Custom Resources](../../components/4.14.x/kubernetes-custom-resources-component.md) | camel-kubernetes-starter | Stable | 3.7 | Perform operations on Kubernetes Custom Resources and get notified on Deployment changes. |
| [Kubernetes Deployments](../../components/4.14.x/kubernetes-deployments-component.md) | camel-kubernetes-starter | Stable | 2.20 | Perform operations on Kubernetes Deployments and get notified on Deployment changes. |
| [Kubernetes Event](../../components/4.14.x/kubernetes-events-component.md) | camel-kubernetes-starter | Stable | 3.20 | Perform operations on Kubernetes Events and get notified on Events changes. |
| [Kubernetes HPA](../../components/4.14.x/kubernetes-hpa-component.md) | camel-kubernetes-starter | Stable | 2.23 | Perform operations on Kubernetes Horizontal Pod Autoscalers (HPA) and get notified on HPA changes. |
| [Kubernetes Job](../../components/4.14.x/kubernetes-job-component.md) | camel-kubernetes-starter | Stable | 2.23 | Perform operations on Kubernetes Jobs. |
| [Kubernetes Namespaces](../../components/4.14.x/kubernetes-namespaces-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Namespaces and get notified on Namespace changes. |
| [Kubernetes Nodes](../../components/4.14.x/kubernetes-nodes-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Nodes and get notified on Node changes. |
| [Kubernetes Persistent Volume](../../components/4.14.x/kubernetes-persistent-volumes-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes and get notified on Persistent Volume changes. |
| [Kubernetes Persistent Volume Claim](../../components/4.14.x/kubernetes-persistent-volumes-claims-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Persistent Volumes Claims and get notified on Persistent Volumes Claim changes. |
| [Kubernetes Pods](../../components/4.14.x/kubernetes-pods-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Pods and get notified on Pod changes. |
| [Kubernetes Replication Controller](../../components/4.14.x/kubernetes-replication-controllers-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Replication Controllers and get notified on Replication Controllers changes. |
| [Kubernetes Resources Quota](../../components/4.14.x/kubernetes-resources-quota-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Resources Quotas. |
| [Kubernetes Secrets](../../components/4.14.x/kubernetes-secrets-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Secrets. |
| [Kubernetes Service Account](../../components/4.14.x/kubernetes-service-accounts-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Service Accounts. |
| [Kubernetes Services](../../components/4.14.x/kubernetes-services-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on Kubernetes Services and get notified on Service changes. |
| [Kudu](../../components/4.14.x/kudu-component.md) | camel-kudu-starter | Stable | 3.0 | Interact with Apache Kudu, a free and open source column-oriented data store of the Apache Hadoop ecosystem. |
| [LangChain4j Agent](../../components/4.14.x/langchain4j-agent-component.md) | camel-langchain4j-agent-starter | Preview | 4.14 | LangChain4j Agent component |
| [LangChain4j Chat](../../components/4.14.x/langchain4j-chat-component.md) | camel-langchain4j-chat-starter | Stable | 4.5 | LangChain4j Chat component |
| [LangChain4j Embeddings](../../components/4.14.x/langchain4j-embeddings-component.md) | camel-langchain4j-embeddings-starter | Stable | 4.5 | LangChain4j Embeddings |
| [LangChain4j Tools](../../components/4.14.x/langchain4j-tools-component.md) | camel-langchain4j-tools-starter | Preview | 4.8 | LangChain4j Tools and Function Calling Features |
| [LangChain4j Web Search](../../components/4.14.x/langchain4j-web-search-component.md) | camel-langchain4j-web-search-starter | Stable | 4.8 | LangChain4j Web Search Engine |
| [Language](../../components/4.14.x/language-component.md) | camel-language-starter | Stable | 2.5 | Execute scripts in any of the languages supported by Camel. |
| [LDAP](../../components/4.14.x/ldap-component.md) | camel-ldap-starter | Stable | 1.5 | Perform searches on LDAP servers. |
| [LDIF](../../components/4.14.x/ldif-component.md) | camel-ldif-starter | Stable | 2.20 | Perform updates on an LDAP server from an LDIF body content. |
| [Log Data](../../components/4.14.x/log-component.md) | camel-log-starter | Stable | 1.1 | Prints data form the routed message (such as body and headers) to the logger. |
| [Lucene](../../components/4.14.x/lucene-component.md) | camel-lucene-starter | Stable | 2.2 | Perform inserts or queries against Apache Lucene databases. |
| [Lumberjack](../../components/4.14.x/lumberjack-component.md) | camel-lumberjack-starter | Stable | 2.18 | Receive logs messages using the Lumberjack protocol. |
| [Mail](../../components/4.14.x/mail-component.md) | camel-mail-starter | Stable | 1.0 | Send and receive emails using imap, pop3 and smtp protocols. |
| [MapStruct](../../components/4.14.x/mapstruct-component.md) | camel-mapstruct-starter | Stable | 3.19 | Type Conversion using Mapstruct |
| [Master](../../components/4.14.x/master-component.md) | camel-master-starter | Stable | 2.20 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [Metrics](../../components/4.14.x/metrics-component.md) | camel-metrics-starter | Stable | 2.14 | Collect various metrics directly from Camel routes using the DropWizard metrics library. |
| [Micrometer](../../components/4.14.x/micrometer-component.md) | camel-micrometer-starter | Stable | 2.22 | Collect various metrics directly from Camel routes using the Micrometer library. |
| [Milvus](../../components/4.14.x/milvus-component.md) | camel-milvus-starter | Stable | 4.5 | Perform operations on the Milvus Vector Database. |
| [Mina](../../components/4.14.x/mina-component.md) | camel-mina-starter | Stable | 2.10 | Socket level networking using TCP or UDP with Apache Mina 2.x. |
| [Minio](../../components/4.14.x/minio-component.md) | camel-minio-starter | Stable | 3.5 | Store and retrieve objects from Minio Storage Service using Minio SDK. |
| [MLLP](../../components/4.14.x/mllp-component.md) | camel-mllp-starter | Stable | 2.17 | Communicate with external systems using the MLLP protocol. |
| [Mock](../../components/4.14.x/mock-component.md) | camel-mock-starter | Stable | 1.0 | Test routes and mediation rules using mocks. |
| [MongoDB](../../components/4.14.x/mongodb-component.md) | camel-mongodb-starter | Stable | 2.19 | Perform operations on MongoDB documents and collections. |
| [MongoDB GridFS](../../components/4.14.x/mongodb-gridfs-component.md) | camel-mongodb-gridfs-starter | Stable | 2.18 | Interact with MongoDB GridFS. |
| [Mustache](../../components/4.14.x/mustache-component.md) | camel-mustache-starter | Stable | 2.12 | Transform messages using a Mustache template. |
| [MVEL](../../components/4.14.x/mvel-component.md) | camel-mvel-starter | Stable | 2.12 | Transform messages using an MVEL template. |
| [MyBatis](../../components/4.14.x/mybatis-component.md) | camel-mybatis-starter | Stable | 2.7 | Performs a query, poll, insert, update or delete in a relational database using MyBatis. |
| [MyBatis Bean](../../components/4.14.x/mybatis-bean-component.md) | camel-mybatis-starter | Stable | 2.22 | Perform queries, inserts, updates or deletes in a relational database using MyBatis. |
| [Nats](../../components/4.14.x/nats-component.md) | camel-nats-starter | Stable | 2.17 | Send and receive messages from NATS messaging system. |
| [Neo4j](../../components/4.14.x/neo4j-component.md) | camel-neo4j-starter | Stable | 4.10 | Perform operations on the Neo4j Graph Database |
| [Netty](../../components/4.14.x/netty-component.md) | camel-netty-starter | Stable | 2.14 | Socket level networking using TCP or UDP with Netty 4.x. |
| [Netty HTTP](../../components/4.14.x/netty-http-component.md) | camel-netty-http-starter | Stable | 2.14 | Netty HTTP server and client using the Netty 4.x. |
| [Nitrite](../../components/4.14.x/nitrite-component.md) | camel-nitrite-starter | Stable-deprecated | 3.0 | Access Nitrite databases. |
| [OAI-PMH](../../components/4.14.x/oaipmh-component.md) | camel-oaipmh-starter | Stable | 3.5 | Harvest metadata using OAI-PMH protocol |
| [Olingo2](../../components/4.14.x/olingo2-component.md) | camel-olingo2-starter | Stable | 2.14 | Communicate with OData 2.0 services using Apache Olingo. |
| [Olingo4](../../components/4.14.x/olingo4-component.md) | camel-olingo4-starter | Stable | 2.19 | Communicate with OData 4.0 services using Apache Olingo OData API. |
| [OpenSearch](../../components/4.14.x/opensearch-component.md) | camel-opensearch-starter | Stable | 4.0 | Send requests to OpenSearch via Java Client API. |
| [OpenShift Build Config](../../components/4.14.x/openshift-build-configs-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on OpenShift Build Configs. |
| [OpenShift Builds](../../components/4.14.x/openshift-builds-component.md) | camel-kubernetes-starter | Stable | 2.17 | Perform operations on OpenShift Builds. |
| [OpenShift Deployment Configs](../../components/4.14.x/openshift-deploymentconfigs-component.md) | camel-kubernetes-starter | Stable | 3.18 | Perform operations on OpenShift Deployment Configs and get notified on Deployment Config changes. |
| [OpenStack Cinder](../../components/4.14.x/openstack-cinder-component.md) | camel-openstack-starter | Stable | 2.19 | Access data in OpenStack Cinder block storage. |
| [OpenStack Glance](../../components/4.14.x/openstack-glance-component.md) | camel-openstack-starter | Stable | 2.19 | Manage VM images and metadata definitions in OpenStack Glance. |
| [OpenStack Keystone](../../components/4.14.x/openstack-keystone-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Keystone for API client authentication, service discovery and distributed multi-tenant authorization. |
| [OpenStack Neutron](../../components/4.14.x/openstack-neutron-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Neutron for network services. |
| [OpenStack Nova](../../components/4.14.x/openstack-nova-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack to manage compute resources. |
| [OpenStack Swift](../../components/4.14.x/openstack-swift-component.md) | camel-openstack-starter | Stable | 2.19 | Access OpenStack Swift object/blob store. |
| [OptaPlanner](../../components/4.14.x/optaplanner-component.md) | camel-optaplanner-starter | Stable | 2.13 | Solve planning problems with OptaPlanner. |
| [Paho](../../components/4.14.x/paho-component.md) | camel-paho-starter | Stable | 2.16 | Communicate with MQTT message brokers using Eclipse Paho MQTT Client. |
| [Paho MQTT 5](../../components/4.14.x/paho-mqtt5-component.md) | camel-paho-mqtt5-starter | Stable | 3.8 | Communicate with MQTT message brokers using Eclipse Paho MQTT v5 Client. |
| [PDF](../../components/4.14.x/pdf-component.md) | camel-pdf-starter | Stable | 2.16 | Create, modify or extract content from PDF documents. |
| [Pinecone](../../components/4.14.x/pinecone-component.md) | camel-pinecone-starter | Stable | 4.6 | Perform operations on the Pinecone Vector Database. |
| [Platform HTTP](../../components/4.14.x/platform-http-component.md) | camel-platform-http-starter | Stable | 3.0 | Expose HTTP endpoints using the HTTP server available in the current platform. |
| [PLC4X](../../components/4.14.x/plc4x-component.md) | camel-plc4x-starter | Stable | 3.20 | Read and write to PLC devices |
| [PostgresSQL Event](../../components/4.14.x/pgevent-component.md) | camel-pgevent-starter | Stable | 2.15 | Send and receive PostgreSQL events via LISTEN and NOTIFY commands. |
| [PostgresSQL Replication Slot](../../components/4.14.x/pg-replication-slot-component.md) | camel-pg-replication-slot-starter | Stable | 3.0 | Poll for PostgreSQL Write-Ahead Log (WAL) records using Streaming Replication Slots. |
| [PQC Algorithms](../../components/4.14.x/pqc-component.md) | camel-pqc-starter | Stable | 4.12 | Post Quantum Cryptography Signature and Verification component. |
| [Printer](../../components/4.14.x/lpr-component.md) | camel-printer-starter | Stable | 2.1 | Send print jobs to printers. |
| [PubNub](../../components/4.14.x/pubnub-component.md) | camel-pubnub-starter | Stable | 2.19 | Send and receive messages to/from PubNub data stream network for connected devices. |
| [Pulsar](../../components/4.14.x/pulsar-component.md) | camel-pulsar-starter | Stable | 2.24 | Send and receive messages from/to Apache Pulsar messaging system. |
| [Qdrant](../../components/4.14.x/qdrant-component.md) | camel-qdrant-starter | Stable | 4.5 | Perform operations on the Qdrant Vector Database. |
| [Quartz](../../components/4.14.x/quartz-component.md) | camel-quartz-starter | Stable | 2.12 | Schedule sending of messages using the Quartz 2.x scheduler. |
| [QuickFix](../../components/4.14.x/quickfix-component.md) | camel-quickfix-starter | Stable | 2.1 | Open a Financial Interchange (FIX) session using an embedded QuickFix/J engine. |
| [Reactive Streams](../../components/4.14.x/reactive-streams-component.md) | camel-reactive-streams-starter | Stable | 2.19 | Exchange messages with reactive stream processing libraries compatible with the reactive streams standard. |
| [Ref](../../components/4.14.x/ref-component.md) | camel-ref-starter | Stable | 1.2 | Route messages to an endpoint looked up dynamically by name in the Camel Registry. |
| [REST](../../components/4.14.x/rest-component.md) | camel-rest-starter | Stable | 2.14 | Expose REST services or call external REST services. |
| [REST API](../../components/4.14.x/rest-api-component.md) | camel-rest-starter | Stable | 2.16 | Expose OpenAPI Specification of the REST services defined using Camel REST DSL. |
| [REST OpenApi](../../components/4.14.x/rest-openapi-component.md) | camel-rest-openapi-starter | Stable | 3.1 | To call REST services using OpenAPI specification as contract. |
| [Robot Framework](../../components/4.14.x/robotframework-component.md) | camel-robotframework-starter | Stable | 3.0 | Pass camel exchanges to acceptance test written in Robot DSL. |
| [RocketMQ](../../components/4.14.x/rocketmq-component.md) | camel-rocketmq-starter | Stable | 3.20 | Send and receive messages from RocketMQ cluster. |
| [RSS](../../components/4.14.x/rss-component.md) | camel-rss-starter | Stable | 2.0 | Poll RSS feeds. |
| [Saga](../../components/4.14.x/saga-component.md) | camel-saga-starter | Stable | 2.21 | Execute custom actions within a route using the Saga EIP. |
| [Salesforce](../../components/4.14.x/salesforce-component.md) | camel-salesforce-starter | Stable | 2.12 | Communicate with Salesforce using Java DTOs. |
| [SAP NetWeaver](../../components/4.14.x/sap-netweaver-component.md) | camel-sap-netweaver-starter | Stable | 2.12 | Send requests to SAP NetWeaver Gateway using HTTP. |
| [Scheduler](../../components/4.14.x/scheduler-component.md) | camel-scheduler-starter | Stable | 2.15 | Generate messages in specified intervals using java.util.concurrent.ScheduledExecutorService. |
| [Schematron](../../components/4.14.x/schematron-component.md) | camel-schematron-starter | Stable | 2.15 | Validate XML payload using the Schematron Library. |
| [SCP](../../components/4.14.x/scp-component.md) | camel-jsch-starter | Stable | 2.10 | Copy files to/from remote hosts using the secure copy protocol (SCP). |
| [SEDA](../../components/4.14.x/seda-component.md) | camel-seda-starter | Stable | 1.1 | Asynchronously call another endpoint from any Camel Context in the same JVM. |
| [Service](../../components/4.14.x/service-component.md) | camel-service-starter | Stable | 2.22 | Register a Camel endpoint to a Service Registry (such as Consul, Etcd) and delegate to it. |
| [ServiceNow](../../components/4.14.x/servicenow-component.md) | camel-servicenow-starter | Stable | 2.18 | Interact with ServiceNow via its REST API. |
| [Servlet](../../components/4.14.x/servlet-component.md) | camel-servlet-starter | Stable | 2.0 | Serve HTTP requests by a Servlet. |
| [SFTP](../../components/4.14.x/sftp-component.md) | camel-ftp-starter | Stable | 1.1 | Upload and download files to/from SFTP servers. |
| [Simple JMS](../../components/4.14.x/sjms-component.md) | camel-sjms-starter | Stable | 2.11 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 1.x API. |
| [Simple JMS2](../../components/4.14.x/sjms2-component.md) | camel-sjms2-starter | Stable | 2.19 | Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API. |
| [Slack](../../components/4.14.x/slack-component.md) | camel-slack-starter | Stable | 2.16 | Send and receive messages to/from Slack. |
| [SMB](../../components/4.14.x/smb-component.md) | camel-smb-starter | Stable | 4.3 | Read and write files to Server Message Block (SMB) file shares. |
| [Smooks](../../components/4.14.x/smooks-component.md) | camel-smooks-starter | Preview | 4.7 | Use Smooks to transform, route, and bind both XML and non-XML data, including EDI, CSV, JSON, and YAML. |
| [SMPP](../../components/4.14.x/smpp-component.md) | camel-smpp-starter | Stable | 2.2 | Send and receive SMS messages using a SMSC (Short Message Service Center). |
| [SNMP](../../components/4.14.x/snmp-component.md) | camel-snmp-starter | Stable | 2.1 | Receive traps and poll SNMP (Simple Network Management Protocol) capable devices. |
| [Solr](../../components/4.14.x/solr-component.md) | camel-solr-starter | Stable | 4.8 | Perform operations against Apache Lucene Solr. |
| [Splunk](../../components/4.14.x/splunk-component.md) | camel-splunk-starter | Stable | 2.13 | Publish or search for events in Splunk. |
| [Splunk HEC](../../components/4.14.x/splunk-hec-component.md) | camel-splunk-hec-starter | Stable | 3.3 | The splunk component allows publishing events in Splunk using the HTTP Event Collector. |
| [Spring Batch](../../components/4.14.x/spring-batch-component.md) | camel-spring-batch-starter | Stable | 2.10 | Send messages to Spring Batch for further processing. |
| [Spring Event](../../components/4.14.x/spring-event-component.md) | camel-spring-starter | Stable | 1.4 | Listen for Spring Application Events. |
| [Spring JDBC](../../components/4.14.x/spring-jdbc-component.md) | camel-spring-jdbc-starter | Stable | 3.10 | Access databases through SQL and JDBC with Spring Transaction support. |
| [Spring LDAP](../../components/4.14.x/spring-ldap-component.md) | camel-spring-ldap-starter | Stable | 2.11 | Perform searches in LDAP servers using filters as the message payload. |
| [Spring RabbitMQ](../../components/4.14.x/spring-rabbitmq-component.md) | camel-spring-rabbitmq-starter | Stable | 3.8 | Send and receive messages from RabbitMQ using the Spring RabbitMQ client. |
| [Spring Redis](../../components/4.14.x/spring-redis-component.md) | camel-spring-redis-starter | Stable | 2.11 | Send and receive messages from Redis. |
| [Spring WebService](../../components/4.14.x/spring-ws-component.md) | camel-spring-ws-starter | Stable | 2.6 | Access external web services as a client or expose your own web services. |
| [SQL](../../components/4.14.x/sql-component.md) | camel-sql-starter | Stable | 1.4 | Perform SQL queries using Spring JDBC. |
| [SQL Stored Procedure](../../components/4.14.x/sql-stored-component.md) | camel-sql-starter | Stable | 2.17 | Perform SQL queries as a JDBC Stored Procedures using Spring JDBC. |
| [SSH](../../components/4.14.x/ssh-component.md) | camel-ssh-starter | Stable | 2.10 | Execute commands on remote hosts using SSH. |
| [StAX](../../components/4.14.x/stax-component.md) | camel-stax-starter | Stable | 2.9 | Process XML payloads by a SAX ContentHandler. |
| [Stitch](../../components/4.14.x/stitch-component.md) | camel-stitch-starter | Stable | 3.8 | Stitch is a cloud ETL service that integrates various data sources into a central data warehouse through various integrations. |
| [Stomp](../../components/4.14.x/stomp-component.md) | camel-stomp-starter | Stable | 2.12 | Send and receive messages to/from STOMP (Simple Text Oriented Messaging Protocol) compliant message brokers. |
| [Stream](../../components/4.14.x/stream-component.md) | camel-stream-starter | Stable | 1.3 | Read from system-in and write to system-out and system-err streams. |
| [String Template](../../components/4.14.x/string-template-component.md) | camel-stringtemplate-starter | Stable | 1.2 | Transform messages using StringTemplate engine. |
| [Stub](../../components/4.14.x/stub-component.md) | camel-stub-starter | Stable | 2.10 | Stub out any physical endpoints while in development or testing. |
| [Tahu Edge Node / Device](../../components/4.14.x/tahu-edge-component.md) | camel-tahu-starter | Stable | 4.8 | Sparkplug B Edge Node and Device support over MQTT using Eclipse Tahu |
| [Tahu Host Application](../../components/4.14.x/tahu-host-component.md) | camel-tahu-starter | Stable | 4.8 | Sparkplug B Host Application support over MQTT using Eclipse Tahu |
| [Telegram](../../components/4.14.x/telegram-component.md) | camel-telegram-starter | Stable | 2.18 | Send and receive messages using the Telegram Bot API. |
| [TensorFlow Serving](../../components/4.14.x/tensorflow-serving-component.md) | camel-tensorflow-serving-starter | Stable | 4.10 | Provide access to TensorFlow Serving model servers to run inference with TensorFlow saved models remotely |
| [Thrift](../../components/4.14.x/thrift-component.md) | camel-thrift-starter | Stable | 2.20 | Call and expose remote procedures (RPC) with Apache Thrift data format and serialization mechanism. |
| [Thymeleaf](../../components/4.14.x/thymeleaf-component.md) | camel-thymeleaf-starter | Stable | 4.1 | Transform messages using a Thymeleaf template. |
| [Tika](../../components/4.14.x/tika-component.md) | camel-tika-starter | Stable | 2.19 | Parse documents and extract metadata and text using Apache Tika. |
| [Timer](../../components/4.14.x/timer-component.md) | camel-timer-starter | Stable | 1.0 | Generate messages in specified intervals using java.util.Timer. |
| [TorchServe](../../components/4.14.x/torchserve-component.md) | camel-torchserve-starter | Preview-deprecated | 4.9 | Provide access to PyTorch TorchServe servers to run inference with PyTorch models remotely |
| [Twilio](../../components/4.14.x/twilio-component.md) | camel-twilio-starter | Stable | 2.20 | Interact with Twilio REST APIs using Twilio Java SDK. |
| [Twitter Direct Message](../../components/4.14.x/twitter-directmessage-component.md) | camel-twitter-starter | Stable | 2.10 | Send and receive Twitter direct messages. |
| [Twitter Search](../../components/4.14.x/twitter-search-component.md) | camel-twitter-starter | Stable | 2.10 | Access Twitter Search. |
| [Twitter Timeline](../../components/4.14.x/twitter-timeline-component.md) | camel-twitter-starter | Stable | 2.10 | Send tweets and receive tweets from user’s timeline. |
| [Undertow](../../components/4.14.x/undertow-component.md) | camel-undertow-starter | Stable | 2.16 | Expose HTTP and WebSocket endpoints and access external HTTP/WebSocket servers. |
| [Validator](../../components/4.14.x/validator-component.md) | camel-validator-starter | Stable | 1.1 | Validate the payload using XML Schema and JAXP Validation. |
| [Velocity](../../components/4.14.x/velocity-component.md) | camel-velocity-starter | Stable | 1.2 | Transform messages using a Velocity template. |
| [Vert.x](../../components/4.14.x/vertx-component.md) | camel-vertx-starter | Stable | 2.12 | Send and receive messages to/from Vert.x Event Bus. |
| [Vert.x HTTP Client](../../components/4.14.x/vertx-http-component.md) | camel-vertx-http-starter | Stable | 3.5 | Send requests to external HTTP servers using Vert.x |
| [Vert.x WebSocket](../../components/4.14.x/vertx-websocket-component.md) | camel-vertx-websocket-starter | Stable | 3.5 | Expose WebSocket endpoints and connect to remote WebSocket servers using Vert.x |
| [Wasm](../../components/4.14.x/wasm-component.md) | camel-wasm-starter | Experimental | 4.4 | Invoke Wasm functions. |
| [Weather](../../components/4.14.x/weather-component.md) | camel-weather-starter | Stable | 2.12 | Poll the weather information from Open Weather Map. |
| [weaviate](../../components/4.14.x/weaviate-component.md) | camel-weaviate-starter | Stable | 4.12 | Perform operations on the Weaviate Vector Database. |
| [Web3j Ethereum Blockchain](../../components/4.14.x/web3j-component.md) | camel-web3j-starter | Stable | 2.22 | Interact with Ethereum nodes using web3j client API. |
| [Webhook](../../components/4.14.x/webhook-component.md) | camel-webhook-starter | Stable | 3.0 | Expose webhook endpoints to receive push notifications for other Camel components. |
| [WhatsApp](../../components/4.14.x/whatsapp-component.md) | camel-whatsapp-starter | Stable | 3.19 | Send messages to WhatsApp. |
| [WordPress](../../components/4.14.x/wordpress-component.md) | camel-wordpress-starter | Stable | 2.21 | Manage posts and users using the WordPress API. |
| [Workday](../../components/4.14.x/workday-component.md) | camel-workday-starter | Stable | 3.1 | Detect and parse documents using Workday. |
| [XChange](../../components/4.14.x/xchange-component.md) | camel-xchange-starter | Stable | 2.21 | Access market data and trade on Bitcoin and Altcoin exchanges. |
| [XJ](../../components/4.14.x/xj-component.md) | camel-xj-starter | Stable | 3.0 | Transform JSON and XML message using a XSLT. |
| [XML Security Sign](../../components/4.14.x/xmlsecurity-sign-component.md) | camel-xmlsecurity-starter | Stable | 2.12 | Sign XML payloads using the XML signature specification. |
| [XML Security Verify](../../components/4.14.x/xmlsecurity-verify-component.md) | camel-xmlsecurity-starter | Stable | 2.12 | Verify XML payloads using the XML signature specification. |
| [XMPP](../../components/4.14.x/xmpp-component.md) | camel-xmpp-starter | Stable | 1.0 | Send and receive messages to/from an XMPP chat server. |
| [XQuery](../../components/4.14.x/xquery-component.md) | camel-saxon-starter | Stable | 1.0 | Query and/or transform XML payloads using XQuery and Saxon. |
| [XSLT](../../components/4.14.x/xslt-component.md) | camel-xslt-starter | Stable | 1.3 | Transforms XML payload using an XSLT template. |
| [XSLT Saxon](../../components/4.14.x/xslt-saxon-component.md) | camel-xslt-saxon-starter | Stable | 3.0 | Transform XML payloads using an XSLT template using Saxon. |
| [Zeebe](../../components/4.14.x/zeebe-component.md) | camel-zeebe-starter | Preview | 3.21 | Zeebe component which integrates with Camunda Zeebe to interact with the API. |
| [Zendesk](../../components/4.14.x/zendesk-component.md) | camel-zendesk-starter | Stable | 2.19 | Manage Zendesk tickets, users, organizations, etc. |
| [ZooKeeper](../../components/4.14.x/zookeeper-component.md) | camel-zookeeper-starter | Stable | 2.9 | Manage ZooKeeper clusters. |
| [ZooKeeper Master](../../components/4.14.x/zookeeper-master-component.md) | camel-zookeeper-master-starter | Stable | 2.19 | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |

### Non-Spring-Boot Components

    
| Component | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [OAuth](../../components/4.14.x/oauth-component.md) | camel-oauth-starter | Preview | 4.12 | Socket level networking using TCP or UDP with Netty 4.x. |
| [Properties](../../components/4.14.x/properties-component.md) | camel-base-starter | Stable | 2.3 | The properties component is used for property placeholders in your Camel application, such as endpoint URIs. |

## Camel Data Formats

Number of Camel data formats: 48 in 43 JAR artifacts (0 deprecated)

    
| Data Format | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [ASN.1 File](../../components/4.14.x/dataformats/asn1-dataformat.md) | camel-asn1-starter | Stable | 2.20 | Encode and decode data structures using Abstract Syntax Notation One (ASN.1). |
| [Avro](../../components/4.14.x/dataformats/avro-dataformat.md) | camel-avro-starter | Stable | 2.14 | Serialize and deserialize messages using Apache Avro binary data format. |
| [Avro Jackson](../../components/4.14.x/dataformats/avroJackson-dataformat.md) | camel-jackson-avro-starter | Stable | 3.10 | Marshal POJOs to Avro and back using Jackson. |
| [Barcode](../../components/4.14.x/dataformats/barcode-dataformat.md) | camel-barcode-starter | Stable | 2.14 | Transform strings to various 1D/2D barcode bitmap formats and back. |
| [Base64](../../components/4.14.x/dataformats/base64-dataformat.md) | camel-base64-starter | Stable | 2.11 | Encode and decode data using Base64. |
| [BeanIO](../../components/4.14.x/dataformats/beanio-dataformat.md) | camel-beanio-starter | Stable | 2.10 | Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats). |
| [Bindy](../../components/4.14.x/dataformats/bindy-dataformat.md) | camel-bindy-starter | Stable | 2.0 | Marshal and unmarshal between POJOs and key-value pair (KVP) format using Camel Bindy |
| [CBOR](../../components/4.14.x/dataformats/cbor-dataformat.md) | camel-cbor-starter | Stable | 3.0 | Unmarshal a CBOR payload to POJO and back. |
| [Crypto (Java Cryptographic Extension)](../../components/4.14.x/dataformats/crypto-dataformat.md) | camel-crypto-starter | Stable | 2.3 | Encrypt and decrypt messages using Java Cryptography Extension (JCE). |
| [CSV](../../components/4.14.x/dataformats/csv-dataformat.md) | camel-csv-starter | Stable | 1.3 | Handle CSV (Comma Separated Values) payloads. |
| [DFDL](../../components/4.14.x/dataformats/dfdl-dataformat.md) | camel-dfdl-starter | Stable | 4.11 | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [FHIR JSon](../../components/4.14.x/dataformats/fhirJson-dataformat.md) | camel-fhir-starter | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from JSON. |
| [FHIR XML](../../components/4.14.x/dataformats/fhirXml-dataformat.md) | camel-fhir-starter | Stable | 2.21 | Marshall and unmarshall FHIR objects to/from XML. |
| [Flatpack](../../components/4.14.x/dataformats/flatpack-dataformat.md) | camel-flatpack-starter | Stable | 2.1 | Marshal and unmarshal Java lists and maps to/from flat files (such as CSV, delimited, or fixed length formats) using Flatpack library. |
| [Fory](../../components/4.14.x/dataformats/fory-dataformat.md) | camel-fory-starter | Preview | 4.9 | Serialize and deserialize messages using Apache Fory |
| [Grok](../../components/4.14.x/dataformats/grok-dataformat.md) | camel-grok-starter | Stable | 3.0 | Unmarshal unstructured data to objects using Logstash based Grok patterns. |
| [GZip Deflater](../../components/4.14.x/dataformats/gzipDeflater-dataformat.md) | camel-zip-deflater-starter | Stable | 2.0 | Compress and decompress messages using java.util.zip.GZIPStream. |
| [HL7](../../components/4.14.x/dataformats/hl7-dataformat.md) | camel-hl7-starter | Stable | 2.0 | Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec. |
| [iCal](../../components/4.14.x/dataformats/ical-dataformat.md) | camel-ical-starter | Stable | 2.12 | Marshal and unmarshal iCal (.ics) documents to/from model objects. |
| [ISO-8583](../../components/4.14.x/dataformats/iso8583-dataformat.md) | camel-iso8583-starter | Preview | 4.14 | Create, edit and read ISO-8583 messages. |
| [Jackson XML](../../components/4.14.x/dataformats/jacksonXml-dataformat.md) | camel-jacksonxml-starter | Stable | 2.16 | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson. |
| [JAXB](../../components/4.14.x/dataformats/jaxb-dataformat.md) | camel-jaxb-starter | Stable | 1.0 | Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard. |
| [JSON Fastjson](../../components/4.14.x/dataformats/fastjson-dataformat.md) | camel-fastjson-starter | Stable | 2.20 | Marshal POJOs to JSON and back using Fastjson |
| [JSON Gson](../../components/4.14.x/dataformats/gson-dataformat.md) | camel-gson-starter | Stable | 2.10 | Marshal POJOs to JSON and back using Gson |
| [JSON Jackson](../../components/4.14.x/dataformats/jackson-dataformat.md) | camel-jackson-starter | Stable | 2.0 | Marshal POJOs to JSON and back using Jackson. |
| [JSON JSON-B](../../components/4.14.x/dataformats/jsonb-dataformat.md) | camel-jsonb-starter | Stable | 3.7 | Marshal POJOs to JSON and back using JSON-B. |
| [JSonApi](../../components/4.14.x/dataformats/jsonApi-dataformat.md) | camel-jsonapi-starter | Stable | 3.0 | Marshal and unmarshal JSON:API resources using JSONAPI-Converter library. |
| [LZF Deflate Compression](../../components/4.14.x/dataformats/lzf-dataformat.md) | camel-lzf-starter | Stable | 2.17 | Compress and decompress streams using LZF deflate algorithm. |
| [MIME Multipart](../../components/4.14.x/dataformats/mimeMultipart-dataformat.md) | camel-mail-starter | Stable | 2.17 | Marshal Camel messages with attachments into MIME-Multipart messages and back. |
| [Parquet File](../../components/4.14.x/dataformats/parquetAvro-dataformat.md) | camel-parquet-avro-starter | Stable | 4.0 | Parquet Avro serialization and de-serialization. |
| [PGP](../../components/4.14.x/dataformats/pgp-dataformat.md) | camel-crypto-pgp-starter | Stable | 2.9 | Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP. |
| [Protobuf](../../components/4.14.x/dataformats/protobuf-dataformat.md) | camel-protobuf-starter | Stable | 2.2 | Serialize and deserialize Java objects using Google’s Protocol buffers. |
| [Protobuf Jackson](../../components/4.14.x/dataformats/protobufJackson-dataformat.md) | camel-jackson-protobuf-starter | Stable | 3.10 | Marshal POJOs to Protobuf and back using Jackson. |
| [RSS](../../components/4.14.x/dataformats/rss-dataformat.md) | camel-rss-starter | Stable | 2.1 | Transform from ROME SyndFeed Java Objects to XML and vice-versa. |
| [Smooks](../../components/4.14.x/dataformats/smooks-dataformat.md) | camel-smooks-starter | Preview | 4.9 | Transform and bind XML as well as non-XML data, including EDI, CSV, JSON, and YAML using Smooks. |
| [SOAP](../../components/4.14.x/dataformats/soap-dataformat.md) | camel-soap-starter | Stable | 2.3 | Marshal Java objects to SOAP messages and back. |
| [SWIFT MT](../../components/4.14.x/dataformats/swiftMt-dataformat.md) | camel-swift-starter | Stable | 3.20 | Encode and decode SWIFT MT messages. |
| [SWIFT MX](../../components/4.14.x/dataformats/swiftMx-dataformat.md) | camel-swift-starter | Stable | 3.20 | Encode and decode SWIFT MX messages. |
| [Syslog](../../components/4.14.x/dataformats/syslog-dataformat.md) | camel-syslog-starter | Stable | 2.6 | Marshall SyslogMessages to RFC3164 and RFC5424 messages and back. |
| [Tar File](../../components/4.14.x/dataformats/tarFile-dataformat.md) | camel-tarfile-starter | Stable | 2.16 | Archive files into tarballs or extract files from tarballs. |
| [Thrift](../../components/4.14.x/dataformats/thrift-dataformat.md) | camel-thrift-starter | Stable | 2.20 | Serialize and deserialize messages using Apache Thrift binary data format. |
| [uniVocity CSV](../../components/4.14.x/dataformats/univocityCsv-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to CSV (Comma Separated Values) using UniVocity Parsers. |
| [uniVocity Fixed Length](../../components/4.14.x/dataformats/univocityFixed-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to fixed length records using UniVocity Parsers. |
| [uniVocity TSV](../../components/4.14.x/dataformats/univocityTsv-dataformat.md) | camel-univocity-parsers-starter | Stable | 2.15 | Marshal and unmarshal Java objects from and to TSV (Tab-Separated Values) records using UniVocity Parsers. |
| [XML Security](../../components/4.14.x/dataformats/xmlSecurity-dataformat.md) | camel-xmlsecurity-starter | Stable | 2.0 | Encrypt and decrypt XML payloads using Apache Santuario. |
| [YAML SnakeYAML](../../components/4.14.x/dataformats/snakeYaml-dataformat.md) | camel-snakeyaml-starter | Stable | 2.17 | Marshal and unmarshal Java objects to and from YAML using SnakeYAML |
| [Zip Deflater](../../components/4.14.x/dataformats/zipDeflater-dataformat.md) | camel-zip-deflater-starter | Stable | 2.12 | Compress and decompress streams using java.util.zip.Deflater and java.util.zip.Inflater. |
| [Zip File](../../components/4.14.x/dataformats/zipFile-dataformat.md) | camel-zipfile-starter | Stable | 2.11 | Compression and decompress streams using java.util.zip.ZipStream. |

### Non-Spring-Boot Data Formats

    
| Data Format | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |

## Camel Languages

Number of Camel languages: 26 in 17 JAR artifacts (2 deprecated)

    
| Language | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Bean Method](../../components/4.14.x/languages/bean-language.md) | camel-bean-starter | Stable | 1.3 | Calls a Java bean method. |
| [Constant](../../components/4.14.x/languages/constant-language.md) | camel-core-starter | Stable | 1.5 | A fixed value set only once during the route startup. |
| [CSimple](../../components/4.14.x/languages/csimple-language.md) | camel-core-starter | Stable | 3.7 | Evaluate a compiled simple expression. |
| [DataSonnet](../../components/4.14.x/languages/datasonnet-language.md) | camel-datasonnet-starter | Stable | 3.7 | To use DataSonnet scripts for message transformations. |
| [ExchangeProperty](../../components/4.14.x/languages/exchangeProperty-language.md) | camel-core-starter | Stable | 2.0 | Gets a property from the Exchange. |
| [File](../../components/4.14.x/languages/file-language.md) | camel-core-starter | Stable | 1.1 | File related capabilities for the Simple language |
| [Groovy](../../components/4.14.x/languages/groovy-language.md) | camel-groovy-starter | Stable | 1.3 | Evaluates a Groovy script. |
| [Header](../../components/4.14.x/languages/header-language.md) | camel-core-starter | Stable | 1.5 | Gets a header from the Exchange. |
| [HL7 Terser](../../components/4.14.x/languages/hl7terser-language.md) | camel-hl7-starter | Stable | 2.11 | Get the value of a HL7 message field specified by terse location specification syntax. |
| [Java](../../components/4.14.x/languages/java-language.md) | camel-joor-starter | Stable | 4.3 | Evaluates a Java (Java compiled once at runtime) expression. |
| [JavaScript](../../components/4.14.x/languages/js-language.md) | camel-javascript-starter | Stable | 3.20 | Evaluates a JavaScript expression. |
| [jOOR](../../components/4.14.x/languages/joor-language.md) | camel-joor-starter | Stable-deprecated | 3.7 | Evaluates a jOOR (Java compiled once at runtime) expression. |
| [JQ](../../components/4.14.x/languages/jq-language.md) | camel-jq-starter | Stable | 3.18 | Evaluates a JQ expression against a JSON message body. |
| [JSONPath](../../components/4.14.x/languages/jsonpath-language.md) | camel-jsonpath-starter | Stable | 2.13 | Evaluates a JSONPath expression against a JSON message body. |
| [MVEL](../../components/4.14.x/languages/mvel-language.md) | camel-mvel-starter | Stable | 2.0 | Evaluates a MVEL template. |
| [OGNL](../../components/4.14.x/languages/ognl-language.md) | camel-ognl-starter | Stable-deprecated | 1.1 | Evaluates an OGNL expression (Apache Commons OGNL). |
| [Python](../../components/4.14.x/languages/python-language.md) | camel-python-starter | Experimental | 3.19 | Evaluates a Python expression. |
| [Ref](../../components/4.14.x/languages/ref-language.md) | camel-core-starter | Stable | 2.8 | Uses an existing expression from the registry. |
| [Simple](../../components/4.14.x/languages/simple-language.md) | camel-core-starter | Stable | 1.1 | Evaluates a Camel simple expression. |
| [SpEL](../../components/4.14.x/languages/spel-language.md) | camel-spring-starter | Stable | 2.7 | Evaluates a Spring expression (SpEL). |
| [Tokenize](../../components/4.14.x/languages/tokenize-language.md) | camel-core-starter | Stable | 2.0 | Tokenize text payloads using delimiter patterns. |
| [Variable](../../components/4.14.x/languages/variable-language.md) | camel-core-starter | Stable | 4.4 | Gets a variable |
| [Wasm](../../components/4.14.x/languages/wasm-language.md) | camel-wasm-starter | Experimental | 4.5 | Call a wasm (web assembly) function. |
| [XML Tokenize](../../components/4.14.x/languages/xtokenize-language.md) | camel-stax-starter | Stable | 2.14 | Tokenize XML payloads. |
| [XPath](../../components/4.14.x/languages/xpath-language.md) | camel-xpath-starter | Stable | 1.1 | Evaluates an XPath expression against an XML payload. |
| [XQuery](../../components/4.14.x/languages/xquery-language.md) | camel-saxon-starter | Stable | 1.0 | Evaluates an XQuery expressions against an XML payload. |

### Non-Spring-Boot Languages

    
| Language | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |

## Miscellaneous Extensions

Number of miscellaneous extensions: 22 in 22 JAR artifacts (0 deprecated)

    
| Extensions | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [AWS XRay](../../components/4.14.x/others/aws-xray.md) | camel-aws-xray-starter | Stable | 2.21 | Enable Distributed tracing using AWS XRay |
| [Cloudevents](../../components/4.14.x/others/cloudevents.md) | camel-cloudevents-starter | Stable | 3.15 | Camel support for the CloudEvents specification |
| [CSimple jOOR](../../components/4.14.x/others/csimple-joor.md) | camel-csimple-joor-starter | Stable | 3.7 | jOOR compiler for csimple language |
| [CXF Transport](../../components/4.14.x/others/cxf-transport.md) | camel-cxf-transport-starter | Stable | 2.8 | Camel Transport for Apache CXF |
| [Debug](../../components/4.14.x/others/debug.md) | camel-debug-starter | Stable | 3.15 | Enables Camel Route Debugging |
| [Jasypt](../../components/4.14.x/others/jasypt.md) | camel-jasypt-starter | Stable | 2.5 | Security using Jasypt |
| [JFR](../../components/4.14.x/others/jfr.md) | camel-jfr-starter | Stable | 3.8 | Diagnose Camel applications with Java Flight Recorder |
| [LangChain4j Tokenizer](../../components/4.14.x/others/langchain4j-tokenizer.md) | camel-langchain4j-tokenizer-starter | Preview | 4.8 | LangChain4j Tokenizer |
| [LevelDB](../../components/4.14.x/others/leveldb.md) | camel-leveldb-starter | Stable | 2.10 | Using LevelDB as persistent EIP store |
| [LRA](../../components/4.14.x/others/lra.md) | camel-lra-starter | Preview | 2.21 | Camel saga binding for Long-Running-Action framework |
| [Micrometer Observability](../../components/4.14.x/others/observation.md) | camel-observation-starter | Stable | 3.21 | Observability using Micrometer Observation |
| [Openapi Java](../../components/4.14.x/others/openapi-java.md) | camel-openapi-java-starter | Stable | 3.1 | Rest DSL support for using OpenApi doc |
| [OpenTelemetry](../../components/4.14.x/others/opentelemetry.md) | camel-opentelemetry-starter | Stable | 3.5 | Distributed tracing using OpenTelemetry |
| [Opentelemetry2](../../components/4.14.x/others/opentelemetry2.md) | camel-opentelemetry2-starter | Preview | 4.11 | Implementation of Camel Opentelemetry based on the Camel Telemetry spec |
| [Reactor](../../components/4.14.x/others/reactor.md) | camel-reactor-starter | Stable | 2.20 | Reactor based back-end for Camel’s reactive streams component |
| [Resilience4j](../../components/4.14.x/others/resilience4j.md) | camel-resilience4j-starter | Stable | 3.0 | Circuit Breaker EIP using Resilience4j |
| [RxJava](../../components/4.14.x/others/rxjava.md) | camel-rxjava-starter | Stable | 2.22 | RxJava based back-end for Camel’s reactive streams component |
| [Shiro](../../components/4.14.x/others/shiro.md) | camel-shiro-starter | Stable | 2.5 | Security using Shiro |
| [Spring Security](../../components/4.14.x/others/spring-security.md) | camel-spring-security-starter | Stable | 2.3 | Security using Spring Security |
| [Springdoc](../../components/4.14.x/others/springdoc.md) | camel-springdoc-starter |  | 3.14 | Springdoc Swagger UI for openapi-java in spring boot |
| [Telemetry Dev](../../components/4.14.x/others/telemetry-dev.md) | camel-telemetry-dev-starter | Preview | 4.11 | Basic implementation of Camel Telemetry useful for development purposes |
| [Undertow Spring Security](../../components/4.14.x/others/undertow-spring-security.md) | camel-undertow-spring-security-starter | Stable | 3.3 | Spring Security Provider for camel-undertow |

### Non-Spring-Boot Miscellaneous Extensions

    
| Extensions | Artifact | Support Level | Since | Description |
| --- | --- | --- | --- | --- |
| [Attachments](../../components/4.14.x/others/attachments.md) | camel-attachments-starter | Stable | 3.0 | Support for attachments on Camel messages |
| [Azure Schema Registry](../../components/4.14.x/others/azure-schema-registry.md) | camel-azure-schema-registry-starter | Stable | 4.2 | Azure Schema Registry Component for utilities to deal with authentication |
| [CLI Connector](../../components/4.14.x/others/cli-connector.md) | camel-cli-connector-starter | Stable | 3.19 | Runtime adapter connecting with Camel CLI |
| [DSL](../../components/4.14.x/others/dsl.md) | undefined-starter |  |  |  |
| [DSL Modeline](../../components/4.14.x/others/dsl-modeline.md) | camel-dsl-modeline-starter | Stable | 3.16 | Camel DSL modeline |
| [Elytron](../../components/4.14.x/others/elytron.md) | camel-elytron-starter | Stable-deprecated | 3.1 | Elytron Security Provider for camel-undertow |
| [Headersmap](../../components/4.14.x/others/headersmap.md) | camel-headersmap-starter | Stable | 2.20 | Fast case-insensitive headers map implementation |
| [Jandex](../../components/4.14.x/others/jandex.md) | camel-jandex-starter | Stable | 4.12 | Custom class and resource loader using jandex.idx |
| [Java DSL (runtime compiled)](../../components/4.14.x/others/java-joor-dsl.md) | camel-java-joor-dsl-starter | Stable | 3.9 | Camel Java DSL with jOOR |
| [Jaxb XML Dsl](../../components/4.14.x/others/java-xml-jaxb-dsl.md) | camel-xml-jaxb-dsl-starter | Stable | 3.9 | Camel DSL with YAML |
| [JTA](../../components/4.14.x/others/jta.md) | camel-jta-starter | Stable | 3.4 | Using Camel With JTA Transaction Manager |
| [Kamelet Main](../../components/4.14.x/others/kamelet-main.md) | camel-kamelet-main-starter | Preview | 3.11 | Main to run Kamelet standalone |
| [Mail Microsoft Oauth](../../components/4.14.x/others/mail-microsoft-oauth.md) | camel-mail-microsoft-oauth-starter | Stable | 3.18.4 | Camel Mail OAuth2 Authenticator for Microsoft Exchange Online |
| [Main](../../components/4.14.x/others/main.md) | camel-main-starter | Stable | 3.0 | Camel Main |
| [Micrometer Prometheus](../../components/4.14.x/others/micrometer-prometheus.md) | camel-micrometer-prometheus-starter | Stable | 4.3 | Camel Micrometer Prometheus for Camel Main |
| [Microprofile Config](../../components/4.14.x/others/microprofile-config.md) | camel-microprofile-config-starter | Stable | 3.0 | Bridging Eclipse MicroProfile Config with Camel properties |
| [Microprofile Fault Tolerance](../../components/4.14.x/others/microprofile-fault-tolerance.md) | camel-microprofile-fault-tolerance-starter | Stable | 3.3 | Circuit Breaker EIP using MicroProfile Fault Tolerance |
| [Microprofile Health](../../components/4.14.x/others/microprofile-health.md) | camel-microprofile-health-starter | Stable | 3.0 | Expose Camel health checks via MicroProfile Health |
| [Observability Services](../../components/4.14.x/others/observability-services.md) | camel-observability-services-starter | Preview | 4.9 | Camel Observability Services |
| [Openapi Validator](../../components/4.14.x/others/openapi-validator.md) | camel-openapi-validator-starter | Stable | 4.7 | OpenAPI validator for Camel Rest DSL |
| [Platform HTTP Jolokia](../../components/4.14.x/others/platform-http-jolokia.md) | camel-platform-http-jolokia-starter | Stable | 4.5 | Jolokia plugin for standalone Camel HTTP Platform |
| [Platform Http Main](../../components/4.14.x/others/platform-http-main.md) | camel-platform-http-main-starter | Stable | 4.0 | Platform HTTP for standalone Camel Main applications |
| [Platform Http Vertx](../../components/4.14.x/others/platform-http-vertx.md) | camel-platform-http-vertx-starter | Stable | 3.2 | Implementation of the Platform HTTP Engine based on Vert.x Web |
| [Reactive Executor Tomcat](../../components/4.14.x/others/reactive-executor-tomcat.md) | camel-reactive-executor-tomcat-starter | Experimental | 3.17 | Reactive Executor for camel-core using Apache Tomcat |
| [Reactive Executor Vert.x](../../components/4.14.x/others/reactive-executor-vertx.md) | camel-reactive-executor-vertx-starter | Experimental | 3.0 | Reactive Executor for camel-core using Vert.x |
| [Redis](../../components/4.14.x/others/redis.md) | camel-redis-starter | Preview | 3.5 | Aggregation repository using Redis as datastore |
| [Resourceresolver Github](../../components/4.14.x/others/resourceresolver-github.md) | camel-resourceresolver-github-starter | Stable | 3.11 | Resource resolver to load files from GitHub |
| [Spring Cloud Config](../../components/4.14.x/others/spring-cloud-config.md) | camel-spring-cloud-config-starter | Stable | 4.12 | Camel Spring Cloud Config support |
| [Spring Main](../../components/4.14.x/others/spring-main.md) | camel-spring-main-starter | Stable | 3.2 | Camel Spring Main support |
| [Spring XML](../../components/4.14.x/others/spring-xml.md) | camel-spring-xml-starter | Stable | 3.9 | Camel Spring with XML DSL |
| [Telemetry](../../components/4.14.x/others/telemetry.md) | camel-telemetry-starter | Preview | 4.11 | Distributed telemetry common interfaces |
| [Test JUnit5](../../components/4.14.x/others/test-junit5.md) | camel-test-junit5-starter | Stable | 3.0 | Camel unit testing with JUnit 5 |
| [Test Main JUnit5](../../components/4.14.x/others/test-main-junit5.md) | camel-test-main-junit5-starter | Stable | 3.16 | Camel unit testing with Main and JUnit 5 |
| [Test Spring JUnit5](../../components/4.14.x/others/test-spring-junit5.md) | camel-test-spring-junit5-starter | Stable | 3.0 | Camel unit testing with Spring and JUnit 5 |
| [ThreadPoolFactory Vert.x](../../components/4.14.x/others/threadpoolfactory-vertx.md) | camel-threadpoolfactory-vertx-starter | Experimental | 3.5 | ThreadPoolFactory for camel-core using Vert.x |
| [Tracing](../../components/4.14.x/others/tracing.md) | camel-tracing-starter | Stable | 3.5 | Distributed tracing common interfaces |
| [Write Ahead Log Strategy for Resume API](../../components/4.14.x/others/wal.md) | camel-wal-starter | Stable | 3.20 | Write Ahead Log Strategy for Resume API |
| [XML Io Dsl](../../components/4.14.x/others/java-xml-io-dsl.md) | camel-xml-io-dsl-starter | Stable | 3.9 | Camel DSL with XML |
| [YAML DSL](../../components/4.14.x/others/yaml-dsl.md) | camel-yaml-dsl-starter | Stable | 3.9 | Camel DSL with YAML |