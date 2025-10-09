# Camel components supported on Quarkus

There are 310 components (6 deprecated, 63 JVM only)

     
| Component | Artifact | JVM  
since | Native  
since | Support  
level | Description |
| --- | --- | --- | --- | --- | --- |
| [ActiveMQ 5.x](extensions/activemq.md) | camel-quarkus-activemq | 1.0.0 | 1.0.0 | Stable | Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component. |
| [ActiveMQ 6.x](extensions/activemq6.md) | camel-quarkus-activemq6 | 3.30.0 | 3.30.0 | Stable | Send messages to (or consume from) Apache ActiveMQ 6.x. This component extends the Camel JMS component. |
| [AMQP](extensions/amqp.md) | camel-quarkus-amqp | 1.0.0 | 1.0.0 | Stable | Messaging with AMQP protocol using Apache QPid Client. |
| [ArangoDb](extensions/arangodb.md) | camel-quarkus-arangodb | 1.1.0 | 1.1.0 | Stable | Perform operations on ArangoDb when used as a Document Database, or as a Graph Database |
| [AS2](extensions/as2.md) | camel-quarkus-as2 | 1.0.0 | 1.0.0 | Stable | Transfer data securely and reliably using the AS2 protocol (RFC4130). |
| [Asterisk](extensions/asterisk.md) | camel-quarkus-asterisk | 1.1.0 | n/a | Preview | Interact with Asterisk PBX Server (VoIP). |
| [Atom](extensions/atom.md) | camel-quarkus-atom | 1.1.0 | 1.2.0 | Stable | Poll Atom RSS feeds. |
| [AWS Bedrock Agent Runtime](extensions/aws-bedrock.md) | camel-quarkus-aws-bedrock | 3.10.0 | 3.10.0 | Stable | Invoke Model of AWS Bedrock Agent Runtime service. |
| [AWS Bedrock Agent](extensions/aws-bedrock.md) | camel-quarkus-aws-bedrock | 3.10.0 | 3.10.0 | Stable | Operate on AWS Bedrock through its Agent. |
| [AWS Bedrock](extensions/aws-bedrock.md) | camel-quarkus-aws-bedrock | 3.10.0 | 3.10.0 | Stable | Invoke Model of AWS Bedrock service. |
| [AWS Secrets Manager](extensions/aws-secrets-manager.md) | camel-quarkus-aws-secrets-manager | 2.0.0 | 3.19.0 | Stable | Manage secrets using AWS Secrets Manager. |
| [AWS Athena](extensions/aws2-athena.md) | camel-quarkus-aws2-athena | 1.0.0 | 1.0.0 | Stable | Access AWS Athena. |
| [AWS CloudWatch](extensions/aws2-cw.md) | camel-quarkus-aws2-cw | 1.0.0 | 1.0.0 | Stable | Sending metrics to AWS CloudWatch. |
| [AWS DynamoDB](extensions/aws2-ddb.md) | camel-quarkus-aws2-ddb | 1.0.0 | 1.0.0 | Stable | Store and retrieve data from AWS DynamoDB. |
| [AWS DynamoDB Streams](extensions/aws2-ddb.md) | camel-quarkus-aws2-ddb | 1.0.0 | 1.0.0 | Stable | Receive messages from AWS DynamoDB Stream. |
| [AWS Elastic Compute Cloud (EC2)](extensions/aws2-ec2.md) | camel-quarkus-aws2-ec2 | 1.0.0 | 1.0.0 | Stable | Manage AWS EC2 instances. |
| [AWS Elastic Container Service (ECS)](extensions/aws2-ecs.md) | camel-quarkus-aws2-ecs | 1.0.0 | 1.0.0 | Stable | Manage AWS ECS cluster instances. |
| [AWS Elastic Kubernetes Service (EKS)](extensions/aws2-eks.md) | camel-quarkus-aws2-eks | 1.0.0 | 1.0.0 | Stable | Manage AWS EKS cluster instances. |
| [AWS Eventbridge](extensions/aws2-eventbridge.md) | camel-quarkus-aws2-eventbridge | 1.4.0 | 1.7.0 | Stable | Send events to AWS Eventbridge cluster instances. |
| [AWS Identity and Access Management (IAM)](extensions/aws2-iam.md) | camel-quarkus-aws2-iam | 1.0.0 | 1.0.0 | Stable | Manage AWS IAM instances. |
| [AWS Kinesis Firehose](extensions/aws2-kinesis.md) | camel-quarkus-aws2-kinesis | 1.1.0 | 1.7.0 | Stable | Produce data to AWS Kinesis Firehose streams. |
| [AWS Kinesis](extensions/aws2-kinesis.md) | camel-quarkus-aws2-kinesis | 1.1.0 | 1.7.0 | Stable | Consume and produce records from and to AWS Kinesis Streams. |
| [AWS Key Management Service (KMS)](extensions/aws2-kms.md) | camel-quarkus-aws2-kms | 1.0.0 | 1.0.0 | Stable | Manage keys stored in AWS KMS instances. |
| [AWS Lambda](extensions/aws2-lambda.md) | camel-quarkus-aws2-lambda | 1.1.0 | 1.1.0 | Stable | Manage and invoke AWS Lambda functions. |
| [AWS MQ](extensions/aws2-mq.md) | camel-quarkus-aws2-mq | 1.0.0 | 1.0.0 | Stable | Send messages to AWS MQ. |
| [AWS Managed Streaming for Apache Kafka (MSK)](extensions/aws2-msk.md) | camel-quarkus-aws2-msk | 1.0.0 | 1.0.0 | Stable | Manage AWS MSK instances. |
| [AWS S3 Storage Service](extensions/aws2-s3.md) | camel-quarkus-aws2-s3 | 1.0.0 | 1.0.0 | Stable | Store and retrieve objects from AWS S3 Storage Service. |
| [AWS Simple Email Service (SES)](extensions/aws2-ses.md) | camel-quarkus-aws2-ses | 1.0.0 | 1.0.0 | Stable | Send e-mails through AWS SES service. |
| [AWS Simple Notification System (SNS)](extensions/aws2-sns.md) | camel-quarkus-aws2-sns | 1.0.0 | 1.0.0 | Stable | Send messages to AWS Simple Notification Topic. |
| [AWS Simple Queue Service (SQS)](extensions/aws2-sqs.md) | camel-quarkus-aws2-sqs | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from AWS SQS. |
| [AWS Security Token Service (STS)](extensions/aws2-sts.md) | camel-quarkus-aws2-sts | 1.1.0 | 1.1.0 | Stable | Manage AWS STS cluster instances. |
| [AWS Translate](extensions/aws2-translate.md) | camel-quarkus-aws2-translate | 1.0.0 | 1.0.0 | Stable | Translate texts using AWS Translate and AWS SDK version 2.x. |
| [Azure CosmosDB](extensions/azure-cosmosdb.md) | camel-quarkus-azure-cosmosdb | 2.0.0 | n/a | Preview | To read and write records to the CosmosDB database on Azure cloud platform. |
| [Azure Event Hubs](extensions/azure-eventhubs.md) | camel-quarkus-azure-eventhubs | 1.7.0 | 1.7.0 | Stable | Send and receive events to/from Azure Event Hubs using AMQP protocol. |
| [Azure Files](extensions/azure-files.md) | camel-quarkus-azure-files | 3.22.0 | n/a | Preview | Send and receive files to Azure storage file share |
| [Azure Key Vault](extensions/azure-key-vault.md) | camel-quarkus-azure-key-vault | 2.10.0 | 3.13.0 | Stable | Manage secrets and keys in Azure Key Vault Service |
| [Azure ServiceBus](extensions/azure-servicebus.md) | camel-quarkus-azure-servicebus | 2.8.0 | 3.19.0 | Stable | Send and receive messages to/from Azure Service Bus. |
| [Azure Storage Blob Service](extensions/azure-storage-blob.md) | camel-quarkus-azure-storage-blob | 1.1.0 | 1.6.0 | Stable | Store and retrieve blobs from Azure Storage Blob Service. |
| [Azure Storage Data Lake Service](extensions/azure-storage-datalake.md) | camel-quarkus-azure-storage-datalake | 1.8.0 | 3.24.0 | Stable | Sends and receives files to/from Azure Data Lake Storage. |
| [Azure Storage Queue Service](extensions/azure-storage-queue.md) | camel-quarkus-azure-storage-queue | 1.1.0 | 1.7.0 | Stable | Stores and retrieves messages to/from Azure Storage Queue. |
| [Bean Validator](extensions/bean-validator.md) | camel-quarkus-bean-validator | 1.0.0 | 1.0.0 | Stable | Validate the message body using the Java Bean Validation API. |
| [Bean](extensions/bean.md) | camel-quarkus-bean | 0.1.0 | 0.1.0 | Stable | Invoke methods of Java beans stored in Camel registry. |
| [Bonita](extensions/bonita.md) | camel-quarkus-bonita | 1.1.0 | n/a | Preview | Communicate with a remote Bonita BPM process engine. |
| [Box](extensions/box.md) | camel-quarkus-box | 1.0.0 | 1.0.0 | Stable | Upload, download and manage files, folders, groups, collaborations, etc. on box.com. |
| [Braintree](extensions/braintree.md) | camel-quarkus-braintree | 1.0.0 | 1.0.0 | Stable | Process payments using Braintree Payments. |
| [Browse](extensions/browse.md) | camel-quarkus-browse | 1.1.0 | 1.2.0 | Stable | Inspect the messages received on endpoints supporting BrowsableEndpoint. |
| [Caffeine Cache](extensions/caffeine.md) | camel-quarkus-caffeine | 1.1.0 | 1.2.0 | Stable | Perform caching operations using Caffeine Cache. |
| [Caffeine LoadCache](extensions/caffeine.md) | camel-quarkus-caffeine | 1.1.0 | 1.2.0 | Stable | Perform caching operations using Caffeine Cache with an attached CacheLoader. |
| [ChatScript](extensions/chatscript.md) | camel-quarkus-chatscript | 1.1.0 | n/a | Preview | Chat with a ChatScript Server. |
| [Chunk](extensions/chunk.md) | camel-quarkus-chunk | 1.1.0 | n/a | Preview | Transform messages using Chunk templating engine. |
| [Class](extensions/bean.md) | camel-quarkus-bean | 0.1.0 | 0.1.0 | Stable | Invoke methods of Java beans specified by class name. |
| [CM SMS Gateway](extensions/cm-sms.md) | camel-quarkus-cm-sms | 1.1.0 | n/a | Preview | Send SMS messages via CM SMS Gateway. |
| [CoAP](extensions/coap.md) | camel-quarkus-coap | 1.1.0 | n/a | Preview | Send and receive messages to/from CoAP (Constrained Application Protocol) capable devices. |
| [CometD](extensions/cometd.md) | camel-quarkus-cometd | 1.1.0 | n/a | Preview | Offers publish/subscribe, peer-to-peer (via a server), and RPC style messaging using the CometD/Bayeux protocol. |
| [Consul](extensions/consul.md) | camel-quarkus-consul | 1.0.0 | 1.0.0 | Stable | Integrate with Consul service discovery and configuration store. |
| [Control Bus](extensions/controlbus.md) | camel-quarkus-controlbus | 0.4.0 | 0.4.0 | Stable | Manage and monitor Camel routes. |
| [Couchbase](extensions/couchbase.md) | camel-quarkus-couchbase | 1.0.0 | n/a | Preview | Query Couchbase Views with a poll strategy and/or perform various operations against Couchbase databases. |
| [CouchDB](extensions/couchdb.md) | camel-quarkus-couchdb | 1.0.0 | 1.0.0 | Stable | Consume changesets for inserts, updates and deletes in a CouchDB database, as well as get, save, update and delete documents from a CouchDB database. |
| [Cassandra CQL](extensions/cassandraql.md) | camel-quarkus-cassandraql | 1.0.0 | 1.7.0 | Stable | Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax. |
| [Cron](extensions/cron.md) | camel-quarkus-cron | 1.0.0 | 1.0.0 | Stable | A generic interface for triggering events at times specified through the Unix cron syntax. |
| [Crypto (JCE)](extensions/crypto.md) | camel-quarkus-crypto | 1.1.0 | 1.2.0 | Stable | Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE). |
| [CXF](extensions/cxf-soap.md) | camel-quarkus-cxf-soap | 2.12.0 | 2.12.0 | Stable | Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client. |
| [CyberArk Vault](extensions/cyberark-vault.md) | camel-quarkus-cyberark-vault | 3.31.0 | 3.31.0 | Stable | Retrieve secrets from CyberArk Conjur Vault. |
| [Data Format](extensions/dataformat.md) | camel-quarkus-dataformat | 0.4.0 | 0.4.0 | Stable | Use a Camel Data Format as a regular Camel Component. |
| [DataSet Test](extensions/dataset.md) | camel-quarkus-dataset | 2.11.0 | 2.11.0 | Stable | Extends the mock component by pulling messages from another endpoint on startup to set the expected message bodies. |
| [Dataset](extensions/dataset.md) | camel-quarkus-dataset | 2.11.0 | 2.11.0 | Stable | Provide data for load and soak testing of your Camel application. |
| [Debezium MongoDB Connector](extensions/debezium-mongodb.md) | camel-quarkus-debezium-mongodb | 1.0.0 | 1.6.0 | Stable | Capture changes from a MongoDB database. |
| [Debezium MySQL Connector](extensions/debezium-mysql.md) | camel-quarkus-debezium-mysql | 1.0.0 | 1.0.0 | Stable | Capture changes from a MySQL database. |
| [Debezium Oracle Connector](extensions/debezium-oracle.md) | camel-quarkus-debezium-oracle | 3.24.0 | 3.24.0 | Stable | Capture changes from an Oracle database. |
| [Debezium PostgresSQL Connector](extensions/debezium-postgres.md) | camel-quarkus-debezium-postgres | 1.0.0 | 1.0.0 | Stable | Capture changes from a PostgresSQL database. |
| [Debezium SQL Server Connector](extensions/debezium-sqlserver.md) | camel-quarkus-debezium-sqlserver | 1.0.0 | 1.0.0 | Stable | Capture changes from an SQL Server database. |
| [DFDL](extensions/dfdl.md) | camel-quarkus-dfdl | 3.22.0 | n/a | Preview | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [DigitalOcean](extensions/digitalocean.md) | camel-quarkus-digitalocean | 1.1.0 | 2.0.0 | Stable | Manage Droplets and resources within the DigitalOcean cloud. |
| [Direct](extensions/direct.md) | camel-quarkus-direct | 0.0.1 | 0.0.1 | Stable | Call another endpoint from the same Camel Context synchronously. |
| [Disruptor](extensions/disruptor.md) | camel-quarkus-disruptor | 1.1.0 | 1.2.0 | Stable | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [Deep Java Library](extensions/djl.md) | camel-quarkus-djl | 1.1.0 | n/a | Preview | Infer Deep Learning models from message exchanges data using Deep Java Library (DJL). |
| [DNS](extensions/dns.md) | camel-quarkus-dns | 1.1.0 | n/a | Preview | Perform DNS queries using DNSJava. |
| [Docling](extensions/docling.md) | camel-quarkus-docling | 3.29.0 | 3.31.0 | Stable | Process documents using Docling library for parsing and conversion. |
| [Drill](extensions/drill.md) | camel-quarkus-drill | 1.1.0 | n/a | Preview | Perform queries against an Apache Drill cluster. |
| [Dropbox](extensions/dropbox.md) | camel-quarkus-dropbox | 1.1.0 | 1.1.0 | Stable | Upload, download and manage files, folders, groups, collaborations, etc on Dropbox. |
| [Ehcache](extensions/ehcache.md) | camel-quarkus-ehcache | 1.1.0 | n/a | Preview | Perform caching operations using Ehcache. |
| [Elasticsearch Low level Rest Client](extensions/elasticsearch-rest-client.md) | camel-quarkus-elasticsearch-rest-client | 3.8.0 | 3.12.0 | Stable | Perform queries and other operations on Elasticsearch or OpenSearch (uses low-level client). |
| [Elasticsearch](extensions/elasticsearch.md) | camel-quarkus-elasticsearch | 3.2.0 | n/a | Preview | Send requests to ElasticSearch via Java Client API. |
| [Exec](extensions/exec.md) | camel-quarkus-exec | 0.4.0 | 0.4.0 | Stable | Execute commands on the underlying operating system. |
| [FHIR](extensions/fhir.md) | camel-quarkus-fhir | 0.3.0 | 0.3.0 | Stable | Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. |
| [File Watch](extensions/file-watch.md) | camel-quarkus-file-watch | 1.0.0 | 1.0.0 | Stable | Get notified about file events in a directory using java.nio.file.WatchService. |
| [File](extensions/file.md) | camel-quarkus-file | 0.4.0 | 0.4.0 | Stable | Read and write files. |
| [Flatpack](extensions/flatpack.md) | camel-quarkus-flatpack | 1.1.0 | 1.1.0 | Stable | Parse fixed width and delimited files using the FlatPack library. |
| [Flink](extensions/flink.md) | camel-quarkus-flink | 1.1.0 | n/a | Preview | Send DataSet jobs to an Apache Flink cluster. |
| [FOP](extensions/fop.md) | camel-quarkus-fop | 1.1.0 | 1.2.0 | Stable | Render messages into PDF and other output formats supported by Apache FOP. |
| [Freemarker](extensions/freemarker.md) | camel-quarkus-freemarker | 1.1.0 | 1.8.0 | Stable | Transform messages using FreeMarker templates. |
| [FTP](extensions/ftp.md) | camel-quarkus-ftp | 1.0.0 | 1.0.0 | Stable | Upload and download files to/from FTP servers. |
| [FTPS](extensions/ftp.md) | camel-quarkus-ftp | 1.0.0 | 1.0.0 | Stable | Upload and download files to/from FTP servers supporting the FTPS protocol. |
| [Geocoder](extensions/geocoder.md) | camel-quarkus-geocoder | 1.1.0 | 1.2.0 | Stable | Find geocodes (latitude and longitude) for a given address or the other way round. |
| [Git](extensions/git.md) | camel-quarkus-git | 1.1.0 | 1.1.0 | Stable | Perform operations on git repositories. |
| [GitHub](extensions/github.md) | camel-quarkus-github | 1.0.0 | 1.0.0 | Stable | Interact with the GitHub API. |
| [Google BigQuery Standard SQL](extensions/google-bigquery.md) | camel-quarkus-google-bigquery | 1.0.0 | 1.6.0 | Stable | Access Google Cloud BigQuery service using SQL queries. |
| [Google BigQuery](extensions/google-bigquery.md) | camel-quarkus-google-bigquery | 1.0.0 | 1.6.0 | Stable | Google BigQuery data warehouse for analytics. |
| [Google Calendar Stream](extensions/google-calendar.md) | camel-quarkus-google-calendar | 1.0.0 | 1.0.0 | Stable | Poll for changes in a Google Calendar. |
| [Google Calendar](extensions/google-calendar.md) | camel-quarkus-google-calendar | 1.0.0 | 1.0.0 | Stable | Perform various operations on a Google Calendar. |
| [Google Drive](extensions/google-drive.md) | camel-quarkus-google-drive | 1.0.0 | 1.0.0 | Stable | Manage files in Google Drive. |
| [Google Cloud Functions](extensions/google-functions.md) | camel-quarkus-google-functions | 2.0.0 | n/a | Preview | Manage and invoke Google Cloud Functions |
| [Google Mail Stream](extensions/google-mail.md) | camel-quarkus-google-mail | 1.0.0 | 1.0.0 | Stable | Poll for incoming messages in Google Mail. |
| [Google Mail](extensions/google-mail.md) | camel-quarkus-google-mail | 1.0.0 | 1.0.0 | Stable | Manage messages in Google Mail. |
| [Google Pubsub](extensions/google-pubsub.md) | camel-quarkus-google-pubsub | 1.0.0 | 1.5.0 | Stable | Send and receive messages to/from Google Cloud Platform PubSub Service. |
| [Google Secret Manager](extensions/google-secret-manager.md) | camel-quarkus-google-secret-manager | 2.8.0 | 3.19.0 | Stable | Manage Google Secret Manager Secrets |
| [Google Sheets Stream](extensions/google-sheets.md) | camel-quarkus-google-sheets | 1.0.0 | 1.0.0 | Stable | Poll for changes in Google Sheets. |
| [Google Sheets](extensions/google-sheets.md) | camel-quarkus-google-sheets | 1.0.0 | 1.0.0 | Stable | Manage spreadsheets in Google Sheets. |
| [Google Storage](extensions/google-storage.md) | camel-quarkus-google-storage | 2.0.0 | 2.0.0 | Stable | Store and retrieve objects from Google Cloud Storage Service using the google-cloud-storage library. |
| [GraphQL](extensions/graphql.md) | camel-quarkus-graphql | 1.0.0 | 1.0.0 | Stable | Send GraphQL queries and mutations to external systems. |
| [gRPC](extensions/grpc.md) | camel-quarkus-grpc | 1.0.0 | 1.0.0 | Stable | Expose gRPC endpoints and access external gRPC endpoints. |
| [Guava EventBus](extensions/guava-eventbus.md) | camel-quarkus-guava-eventbus | 1.1.0 | n/a | Preview | Send and receive messages to/from Guava EventBus. |
| [Hashicorp Vault](extensions/hashicorp-vault.md) | camel-quarkus-hashicorp-vault | 2.11.0 | 3.15.0 | Stable | Manage secrets in Hashicorp Vault Service |
| [Hazelcast Atomic Number](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number). |
| [Hazelcast Instance](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Consume join/leave events of a cache instance in a Hazelcast cluster. |
| [Hazelcast List](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed list. |
| [Hazelcast Map](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed map. |
| [Hazelcast Multimap](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed multimap. |
| [Hazelcast Queue](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed queue. |
| [Hazelcast Replicated Map](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast replicated map. |
| [Hazelcast Ringbuffer](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed ringbuffer. |
| [Hazelcast SEDA](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Asynchronously send/receive Exchanges between Camel routes running on potentially distinct JVMs/hosts backed by Hazelcast BlockingQueue. |
| [Hazelcast Set](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Perform operations on Hazelcast distributed set. |
| [Hazelcast Topic](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable | Send and receive messages to/from Hazelcast distributed topic. |
| [HTTP](extensions/http.md) | camel-quarkus-http | 1.0.0 | 1.0.0 | Stable | Send requests to external HTTP servers using Apache HTTP Client 5.x. |
| [Huawei Simple Message Notification (SMN)](extensions/huaweicloud-smn.md) | camel-quarkus-huaweicloud-smn | 1.8.0 | n/a | Preview | To broadcast messages and connect cloud services through notifications on Huawei Cloud |
| [IBM Cloud Object Storage](extensions/ibm-cos.md) | camel-quarkus-ibm-cos | 3.30.0 | 3.31.0 | Stable | Store and retrieve objects from IBM Cloud Object Storage. |
| [IBM Secrets Manager](extensions/ibm-secrets-manager.md) | camel-quarkus-ibm-secrets-manager | 3.22.0 | n/a | Preview | Manage secrets in IBM Secrets Manager Service |
| [IBM Watson Discovery](extensions/ibm-watson-discovery.md) | camel-quarkus-ibm-watson-discovery | 3.30.0 | n/a | Preview | Perform document understanding and search using IBM Watson Discovery |
| [IBM Watson Language](extensions/ibm-watson-language.md) | camel-quarkus-ibm-watson-language | 3.30.0 | n/a | Preview | Perform natural language processing using IBM Watson Natural Language Understanding |
| [IEC 60870 Client](extensions/iec60870.md) | camel-quarkus-iec60870 | 1.1.0 | n/a | Preview | IEC 60870 supervisory control and data acquisition (SCADA) client using NeoSCADA implementation. |
| [IEC 60870 Server](extensions/iec60870.md) | camel-quarkus-iec60870 | 1.1.0 | n/a | Preview | IEC 60870 supervisory control and data acquisition (SCADA) server using NeoSCADA implementation. |
| [Ignite Cache](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Perform cache operations on an Ignite cache or consume changes from a continuous query. |
| [Ignite Compute](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Run compute operations on an Ignite cluster. |
| [Ignite Events](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Receive events from an Ignite cluster by creating a local event listener. |
| [Ignite ID Generator](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Interact with Ignite Atomic Sequences and ID Generators . |
| [Ignite Messaging](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Send and receive messages from an Ignite topic. |
| [Ignite Queues](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Interact with Ignite Queue data structures. |
| [Ignite Sets](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Interact with Ignite Set data structures. |
| [Infinispan](extensions/infinispan.md) | camel-quarkus-infinispan | 0.0.1 | 0.0.1 | Stable | Read and write from/to Infinispan distributed key/value store and data grid. |
| [InfluxDB](extensions/influxdb.md) | camel-quarkus-influxdb | 1.0.0 | 1.0.0 | Stable | Interact with InfluxDB v1, a time series database. |
| [IRC](extensions/irc.md) | camel-quarkus-irc | 1.1.0 | n/a | Preview | Send and receive messages to/from and IRC chat. |
| [JCache](extensions/jcache.md) | camel-quarkus-jcache | 1.2.0 | 2.13.0 | Stable | Perform caching operations against JSR107/JCache. |
| [JCR](extensions/jcr.md) | camel-quarkus-jcr | 1.1.0 | n/a | Preview | Read and write nodes to/from a JCR compliant content repository. |
| [JDBC](extensions/jdbc.md) | camel-quarkus-jdbc | 0.0.1 | 0.0.1 | Stable | Access databases through SQL and JDBC. |
| [JGroups raft](extensions/jgroups-raft.md) | camel-quarkus-jgroups-raft | 1.1.0 | n/a | Preview | Exchange messages with JGroups-raft clusters. |
| [JGroups](extensions/jgroups.md) | camel-quarkus-jgroups | 1.1.0 | n/a | Preview | Exchange messages with JGroups clusters. |
| [Jira](extensions/jira.md) | camel-quarkus-jira | 1.0.0 | 1.0.0 | Stable | Interact with JIRA issue tracker. |
| [JMS](extensions/jms.md) | camel-quarkus-jms | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from JMS message brokers. |
| [JOLT](extensions/jolt.md) | camel-quarkus-jolt | 1.0.0 | 1.0.0 | Stable | JSON to JSON transformation using JOLT. |
| [JOOQ](extensions/jooq.md) | camel-quarkus-jooq | 1.1.0 | n/a | Preview | Store and retrieve Java objects from an SQL database using JOOQ. |
| [JPA](extensions/jpa.md) | camel-quarkus-jpa | 1.0.0 | 1.0.0 | Stable | Store and retrieve Java objects from databases using Java Persistence API (JPA). |
| [JSLT](extensions/jslt.md) | camel-quarkus-jslt | 1.1.0 | 1.4.0 | Stable | Query or transform JSON payloads using JSLT. |
| [JsonPatch](extensions/json-patch.md) | camel-quarkus-json-patch | 2.7.0 | n/a | Preview | Transforms JSON using JSON patch (RFC 6902). |
| [JSON Schema Validator](extensions/json-validator.md) | camel-quarkus-json-validator | 1.0.0 | 1.0.0 | Stable | Validate JSON payloads using NetworkNT JSON Schema. |
| [JSONata](extensions/jsonata.md) | camel-quarkus-jsonata | 1.6.0 | 1.6.0 | Stable | Transforms JSON payload using JSONata transformation. |
| [JT400](extensions/jt400.md) | camel-quarkus-jt400 | 1.1.0 | 3.8.0 | Stable | Exchanges messages with an IBM i system using data queues, message queues, or program call. IBM i is the replacement for AS/400 and iSeries servers. |
| [Kafka](extensions/kafka.md) | camel-quarkus-kafka | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from an Apache Kafka broker. |
| [Kamelet](extensions/kamelet.md) | camel-quarkus-kamelet | 1.7.0 | 1.7.0 | Stable | To call Kamelets |
| [Keycloak](extensions/keycloak.md) | camel-quarkus-keycloak | 3.29.0 | 3.31.0 | Stable | Manage Keycloak instances via Admin API. |
| [Knative](extensions/knative.md) | camel-quarkus-knative | 2.14.0 | 2.14.0 | Stable | Send and receive events from Knative. |
| [Kubernetes ConfigMap](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes ConfigMaps and get notified on ConfigMaps changes. |
| [Kubernetes Cronjob](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes CronJob. |
| [Kubernetes Custom Resources](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Custom Resources and get notified on Deployment changes. |
| [Kubernetes Deployments](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Deployments and get notified on Deployment changes. |
| [Kubernetes Event](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Events and get notified on Events changes. |
| [Kubernetes HPA](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Horizontal Pod Autoscalers (HPA) and get notified on HPA changes. |
| [Kubernetes Job](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Jobs. |
| [Kubernetes Namespaces](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Namespaces and get notified on Namespace changes. |
| [Kubernetes Nodes](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Nodes and get notified on Node changes. |
| [Kubernetes Persistent Volume Claim](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Persistent Volumes Claims and get notified on Persistent Volumes Claim changes. |
| [Kubernetes Persistent Volume](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Persistent Volumes and get notified on Persistent Volume changes. |
| [Kubernetes Pods](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Pods and get notified on Pod changes. |
| [Kubernetes Replication Controller](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Replication Controllers and get notified on Replication Controllers changes. |
| [Kubernetes Resources Quota](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Resources Quotas. |
| [Kubernetes Secrets](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Secrets. |
| [Kubernetes Service Account](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Service Accounts. |
| [Kubernetes Services](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on Kubernetes Services and get notified on Service changes. |
| [Kudu](extensions/kudu.md) | camel-quarkus-kudu | 1.0.0 | 1.0.0 | Stable | Interact with Apache Kudu, a free and open source column-oriented data store of the Apache Hadoop ecosystem. |
| [LangChain4j Agent](extensions/langchain4j-agent.md) | camel-quarkus-langchain4j-agent | 3.26.0 | 3.27.0 | Stable | LangChain4j Agent component |
| [LangChain4j Chat](extensions/langchain4j-chat.md) | camel-quarkus-langchain4j-chat | 3.11.0 | 3.12.0 | Stable | LangChain4j Chat component |
| [LangChain4j Embeddings](extensions/langchain4j-embeddings.md) | camel-quarkus-langchain4j-embeddings | 3.10.0 | 3.29.0 | Stable | LangChain4j Embeddings |
| [LangChain4j Embedding Store](extensions/langchain4j-embeddingstore.md) | camel-quarkus-langchain4j-embeddingstore | 3.29.0 | 3.29.0 | Stable | Perform operations on the Langchain4jEmbeddingStores. |
| [LangChain4j Tools](extensions/langchain4j-tools.md) | camel-quarkus-langchain4j-tools | 3.15.0 | 3.24.0 | Stable | LangChain4j Tools and Function Calling Features |
| [LangChain4j Web Search](extensions/langchain4j-web-search.md) | camel-quarkus-langchain4j-web-search | 3.15.0 | 3.24.0 | Stable | LangChain4j Web Search Engine |
| [Language](extensions/language.md) | camel-quarkus-language | 1.1.0 | 2.2.0 | Stable | Execute scripts in any of the languages supported by Camel. |
| [LDAP](extensions/ldap.md) | camel-quarkus-ldap | 1.1.0 | 3.2.0 | Stable | Perform searches on LDAP servers. |
| [LDIF](extensions/ldif.md) | camel-quarkus-ldif | 1.1.0 | n/a | Preview | Perform updates on an LDAP server from an LDIF body content. |
| [Log Data](extensions/log.md) | camel-quarkus-log | 0.0.1 | 0.0.1 | Stable | Prints data form the routed message (such as body and headers) to the logger. |
| [Printer](extensions/printer.md) | camel-quarkus-printer | 1.1.0 | n/a | Preview | Send print jobs to printers. |
| [Lucene](extensions/lucene.md) | camel-quarkus-lucene | 1.1.0 | n/a | Preview | Perform inserts or queries against Apache Lucene databases. |
| [Lumberjack](extensions/lumberjack.md) | camel-quarkus-lumberjack | 1.1.0 | 1.4.0 | Stable | Receive logs messages using the Lumberjack protocol. |
| [IMAP](extensions/mail.md) | camel-quarkus-mail | 0.2.0 | 0.2.0 | Stable | Send and receive emails using imap, pop3 and smtp protocols. |
| [MapStruct](extensions/mapstruct.md) | camel-quarkus-mapstruct | 3.2.0 | 3.2.0 | Stable | Type Conversion using Mapstruct |
| [Master](extensions/master.md) | camel-quarkus-master | 1.0.0 | 1.0.0 | Stable | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [Micrometer](extensions/micrometer.md) | camel-quarkus-micrometer | 1.5.0 | 1.5.0 | Stable | Collect various metrics directly from Camel routes using the Micrometer library. |
| [OPC UA Browser](extensions/milo.md) | camel-quarkus-milo | 3.31.0 | 3.31.0 | Stable | Connect to OPC UA servers using the binary protocol for browsing the node tree. |
| [OPC UA Client](extensions/milo.md) | camel-quarkus-milo | 3.31.0 | 3.31.0 | Stable | Connect to OPC UA servers using the binary protocol for acquiring telemetry data. |
| [OPC UA Server](extensions/milo.md) | camel-quarkus-milo | 3.31.0 | 3.31.0 | Stable | Make telemetry data available as an OPC UA server. |
| [Milvus](extensions/milvus.md) | camel-quarkus-milvus | 3.10.0 | 3.33.0 | Stable | Perform operations on the Milvus Vector Database. |
| [MINA SFTP](extensions/mina-sftp.md) | camel-quarkus-mina-sftp | 3.33.0 | 3.33.0 | Stable | Upload and download files to/from SFTP servers using Apache MINA SSHD. |
| [Minio](extensions/minio.md) | camel-quarkus-minio | 1.5.0 | 1.6.0 | Stable | Store and retrieve objects from Minio Storage Service using Minio SDK. |
| [MLLP](extensions/mllp.md) | camel-quarkus-mllp | 1.1.0 | 2.0.0 | Stable | Communicate with external systems using the MLLP protocol. |
| [Mock](extensions/mock.md) | camel-quarkus-mock | 1.0.0 | 1.0.0 | Stable | Test routes and mediation rules using mocks. |
| [MongoDB GridFS](extensions/mongodb-gridfs.md) | camel-quarkus-mongodb-gridfs | 1.0.0 | 1.0.0 | Stable | Interact with MongoDB GridFS. |
| [MongoDB](extensions/mongodb.md) | camel-quarkus-mongodb | 1.0.0 | 1.0.0 | Stable | Perform operations on MongoDB documents and collections. |
| [Mustache](extensions/mustache.md) | camel-quarkus-mustache | 1.0.0 | 1.0.0 | Stable | Transform messages using a Mustache template. |
| [MVEL](extensions/mvel.md) | camel-quarkus-mvel | 1.1.0 | n/a | Preview | Transform messages using an MVEL template. |
| [MyBatis Bean](extensions/mybatis.md) | camel-quarkus-mybatis | 1.1.0 | 2.8.0 | Stable | Perform queries, inserts, updates or deletes in a relational database using MyBatis. |
| [MyBatis](extensions/mybatis.md) | camel-quarkus-mybatis | 1.1.0 | 2.8.0 | Stable | Performs a query, poll, insert, update or delete in a relational database using MyBatis. |
| [Nats](extensions/nats.md) | camel-quarkus-nats | 1.1.0 | 1.1.0 | Stable | Send and receive messages from NATS messaging system. |
| [Netty HTTP](extensions/netty-http.md) | camel-quarkus-netty-http | 0.2.0 | 0.2.0 | Stable | Netty HTTP server and client using the Netty 4.x. |
| [Netty](extensions/netty.md) | camel-quarkus-netty | 0.4.0 | 0.4.0 | Stable | Socket level networking using TCP or UDP with Netty 4.x. |
| [Nitrite](extensions/nitrite.md) | camel-quarkus-nitrite | 1.0.0 | 1.8.0 | Stable | Access Nitrite databases. |
| [OAI-PMH](extensions/oaipmh.md) | camel-quarkus-oaipmh | 1.7.0 | 1.7.0 | Stable | Harvest metadata using OAI-PMH protocol |
| [Olingo4](extensions/olingo4.md) | camel-quarkus-olingo4 | 1.0.0 | 1.0.0 | Stable | Communicate with OData 4.0 services using Apache Olingo OData API. |
| [Once](extensions/once.md) | camel-quarkus-once | 3.31.0 | 3.31.0 | Stable | Trigger a single message only once at startup (useful for development and testing purposes). |
| [OpenAI](extensions/openai.md) | camel-quarkus-openai | 3.32.0 | 3.32.0 | Stable | OpenAI endpoint for chat completion and embeddings. |
| [OpenSearch](extensions/opensearch.md) | camel-quarkus-opensearch | 3.8.0 | n/a | Preview | Send requests to OpenSearch via Java Client API. |
| [OpenShift Build Config](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on OpenShift Build Configs. |
| [OpenShift Builds](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on OpenShift Builds. |
| [OpenShift Deployment Configs](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations on OpenShift Deployment Configs and get notified on Deployment Config changes. |
| [OpenStack Cinder](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Access data in OpenStack Cinder block storage. |
| [OpenStack Glance](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Manage VM images and metadata definitions in OpenStack Glance. |
| [OpenStack Keystone](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Access OpenStack Keystone for API client authentication, service discovery and distributed multi-tenant authorization. |
| [OpenStack Neutron](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Access OpenStack Neutron for network services. |
| [OpenStack Nova](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Access OpenStack to manage compute resources. |
| [OpenStack Swift](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Access OpenStack Swift object/blob store. |
| [OptaPlanner](extensions/optaplanner.md) | camel-quarkus-optaplanner | 1.1.0 | n/a | Preview | Solve planning problems with OptaPlanner. |
| [Paho MQTT 5](extensions/paho-mqtt5.md) | camel-quarkus-paho-mqtt5 | 1.8.0 | 1.8.0 | Stable | Communicate with MQTT message brokers using Eclipse Paho MQTT v5 Client. |
| [Paho](extensions/paho.md) | camel-quarkus-paho | 0.2.0 | 0.2.0 | Stable | Communicate with MQTT message brokers using Eclipse Paho MQTT Client. |
| [PDF](extensions/pdf.md) | camel-quarkus-pdf | 0.3.1 | 0.3.1 | Stable | Create, modify or extract content from PDF documents. |
| [PostgresSQL Replication Slot](extensions/pg-replication-slot.md) | camel-quarkus-pg-replication-slot | 1.1.0 | 1.2.0 | Stable | Poll for PostgreSQL Write-Ahead Log (WAL) records using Streaming Replication Slots. |
| [PostgresSQL Event](extensions/pgevent.md) | camel-quarkus-pgevent | 1.1.0 | 1.2.0 | Stable | Send and receive PostgreSQL events via LISTEN and NOTIFY commands. |
| [Pinecone](extensions/pinecone.md) | camel-quarkus-pinecone | 3.12.0 | 3.12.0 | Stable | Perform operations on the Pinecone Vector Database. |
| [Platform HTTP](extensions/platform-http.md) | camel-quarkus-platform-http | 0.3.0 | 0.3.0 | Stable | Expose HTTP endpoints using the HTTP server available in the current platform. |
| [PQC Algorithms](extensions/pqc.md) | camel-quarkus-pqc | 3.24.0 | n/a | Preview | Post Quantum Cryptography Signature and Verification component. |
| [PubNub](extensions/pubnub.md) | camel-quarkus-pubnub | 1.0.0 | 1.7.0 | Stable | Send and receive messages to/from PubNub data stream network for connected devices. |
| [Pulsar](extensions/pulsar.md) | camel-quarkus-pulsar | 1.1.0 | n/a | Preview | Send and receive messages from/to Apache Pulsar messaging system. |
| [Qdrant](extensions/qdrant.md) | camel-quarkus-qdrant | 3.10.0 | 3.10.0 | Stable | Perform operations on the Qdrant Vector Database. |
| [Quartz](extensions/quartz.md) | camel-quarkus-quartz | 1.0.0 | 1.0.0 | Stable | Schedule sending of messages using the Quartz 2.x scheduler. |
| [QuickFix](extensions/quickfix.md) | camel-quarkus-quickfix | 1.1.0 | n/a | Preview | Open a Financial Interchange (FIX) session using an embedded QuickFix/J engine. |
| [Reactive Streams](extensions/reactive-streams.md) | camel-quarkus-reactive-streams | 1.0.0 | 1.0.0 | Stable | Exchange messages with reactive stream processing libraries compatible with the reactive streams standard. |
| [Ref](extensions/ref.md) | camel-quarkus-ref | 1.0.0 | 1.0.0 | Stable | Route messages to an endpoint looked up dynamically by name in the Camel Registry. |
| [REST API](extensions/rest.md) | camel-quarkus-rest | 0.0.1 | 0.0.1 | Stable | Expose OpenAPI Specification of the REST services defined using Camel REST DSL. |
| [REST OpenApi](extensions/rest-openapi.md) | camel-quarkus-rest-openapi | 1.0.0 | 1.0.0 | Stable | To call REST services using OpenAPI specification as contract. |
| [REST](extensions/rest.md) | camel-quarkus-rest | 0.0.1 | 0.0.1 | Stable | Expose REST services or call external REST services. |
| [Robot Framework](extensions/robotframework.md) | camel-quarkus-robotframework | 1.1.0 | n/a | Preview | Pass camel exchanges to acceptance test written in Robot DSL. |
| [RSS](extensions/rss.md) | camel-quarkus-rss | 1.1.0 | 1.2.0 | Stable | Poll RSS feeds. |
| [Saga](extensions/saga.md) | camel-quarkus-saga | 1.1.0 | 1.4.0 | Stable | Execute custom actions within a route using the Saga EIP. |
| [Salesforce](extensions/salesforce.md) | camel-quarkus-salesforce | 0.2.0 | 0.0.2 | Stable | Communicate with Salesforce using Java DTOs. |
| [SAP NetWeaver](extensions/sap-netweaver.md) | camel-quarkus-sap-netweaver | 1.0.0 | 1.0.0 | Stable | Send requests to SAP NetWeaver Gateway using HTTP. |
| [Scheduler](extensions/scheduler.md) | camel-quarkus-scheduler | 0.4.0 | 0.4.0 | Stable | Generate messages in specified intervals using java.util.concurrent.ScheduledExecutorService. |
| [Schematron](extensions/schematron.md) | camel-quarkus-schematron | 1.1.0 | n/a | Preview | Validate XML payload using the Schematron Library. |
| [SCP](extensions/jsch.md) | camel-quarkus-jsch | 1.1.0 | 1.5.0 | Stable | Copy files to/from remote hosts using the secure copy protocol (SCP). |
| [SEDA](extensions/seda.md) | camel-quarkus-seda | 1.0.0 | 1.0.0 | Stable | Asynchronously call another endpoint from any Camel Context in the same JVM. |
| [ServiceNow](extensions/servicenow.md) | camel-quarkus-servicenow | 1.0.0 | 1.0.0 | Stable | Interact with ServiceNow via its REST API. |
| [Servlet](extensions/servlet.md) | camel-quarkus-servlet | 0.2.0 | 0.0.2 | Stable | Serve HTTP requests by a Servlet. |
| [SFTP](extensions/ftp.md) | camel-quarkus-ftp | 1.0.0 | 1.0.0 | Stable | Upload and download files to/from SFTP servers. |
| [Simple JMS](extensions/sjms.md) | camel-quarkus-sjms | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from a JMS Queue or Topic using plain JMS 1.x API. |
| [Simple JMS2](extensions/sjms2.md) | camel-quarkus-sjms2 | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API. |
| [Slack](extensions/slack.md) | camel-quarkus-slack | 0.3.0 | 0.3.0 | Stable | Send and receive messages to/from Slack. |
| [SMB](extensions/smb.md) | camel-quarkus-smb | 3.7.0 | 3.7.0 | Stable | Read and write files to Server Message Block (SMB) file shares. |
| [Smooks](extensions/smooks.md) | camel-quarkus-smooks | 3.18.0 | n/a | Preview | Use Smooks to transform, route, and bind both XML and non-XML data, including EDI, CSV, JSON, and YAML. |
| [SMPP](extensions/smpp.md) | camel-quarkus-smpp | 1.1.0 | n/a | Preview | Send and receive SMS messages using a SMSC (Short Message Service Center). |
| [SNMP](extensions/snmp.md) | camel-quarkus-snmp | 1.1.0 | n/a | Preview | Receive traps and poll SNMP (Simple Network Management Protocol) capable devices. |
| [Solr](extensions/solr.md) | camel-quarkus-solr | 3.19.0 | 3.19.0 | Stable | Perform operations against Apache Lucene Solr. |
| [Splunk HEC](extensions/splunk-hec.md) | camel-quarkus-splunk-hec | 1.1.0 | 3.8.0 | Stable | The splunk component allows publishing events in Splunk using the HTTP Event Collector. |
| [Splunk](extensions/splunk.md) | camel-quarkus-splunk | 1.8.0 | 1.8.0 | Stable | Publish or search for events in Splunk. |
| [Spring RabbitMQ](extensions/spring-rabbitmq.md) | camel-quarkus-spring-rabbitmq | 1.7.0 | 1.7.0 | Stable | Send and receive messages from RabbitMQ using the Spring RabbitMQ client. |
| [Spring Redis](extensions/spring-redis.md) | camel-quarkus-spring-redis | 3.6.0 | n/a | Preview | Send and receive messages from Redis. |
| [SQL Stored Procedure](extensions/sql.md) | camel-quarkus-sql | 1.0.0 | 1.0.0 | Stable | Perform SQL queries as a JDBC Stored Procedures using Spring JDBC. |
| [SQL](extensions/sql.md) | camel-quarkus-sql | 1.0.0 | 1.0.0 | Stable | Perform SQL queries using Spring JDBC. |
| [SSH](extensions/ssh.md) | camel-quarkus-ssh | 1.1.0 | 1.2.0 | Stable | Execute commands on remote hosts using SSH. |
| [StAX](extensions/stax.md) | camel-quarkus-stax | 1.1.0 | 1.7.0 | Stable | Process XML payloads by a SAX ContentHandler. |
| [Stitch](extensions/stitch.md) | camel-quarkus-stitch | 1.8.0 | n/a | Preview | Stitch is a cloud ETL service that integrates various data sources into a central data warehouse through various integrations. |
| [Stomp](extensions/stomp.md) | camel-quarkus-stomp | 1.1.0 | n/a | Preview | Send and receive messages to/from STOMP (Simple Text Oriented Messaging Protocol) compliant message brokers. |
| [Stream](extensions/stream.md) | camel-quarkus-stream | 1.0.0 | 1.0.0 | Stable | Read from system-in and write to system-out and system-err streams. |
| [String Template](extensions/stringtemplate.md) | camel-quarkus-stringtemplate | 1.1.0 | 1.2.0 | Stable | Transform messages using StringTemplate engine. |
| [Stub](extensions/stub.md) | camel-quarkus-stub | 1.1.0 | n/a | Preview | Stub out any physical endpoints while in development or testing. |
| [Telegram](extensions/telegram.md) | camel-quarkus-telegram | 1.0.0 | 1.0.0 | Stable | Send and receive messages using the Telegram Bot API. |
| [Thrift](extensions/thrift.md) | camel-quarkus-thrift | 1.1.0 | n/a | Preview | Call and expose remote procedures (RPC) with Apache Thrift data format and serialization mechanism. |
| [Tika](extensions/tika.md) | camel-quarkus-tika | 1.0.0 | 1.0.0 | Stable | Parse documents and extract metadata and text using Apache Tika. |
| [Timer](extensions/timer.md) | camel-quarkus-timer | 0.2.0 | 0.0.2 | Stable | Generate messages in specified intervals using java.util.Timer. |
| [Twilio](extensions/twilio.md) | camel-quarkus-twilio | 1.1.0 | 1.4.0 | Stable | Interact with Twilio REST APIs using Twilio Java SDK. |
| [Twitter Direct Message](extensions/twitter.md) | camel-quarkus-twitter | 0.2.0 | 0.1.0 | Stable | Send and receive Twitter direct messages. |
| [Twitter Search](extensions/twitter.md) | camel-quarkus-twitter | 0.2.0 | 0.1.0 | Stable | Access Twitter Search. |
| [Twitter Timeline](extensions/twitter.md) | camel-quarkus-twitter | 0.2.0 | 0.1.0 | Stable | Send tweets and receive tweets from user’s timeline. |
| [Validator](extensions/validator.md) | camel-quarkus-validator | 0.4.0 | 0.4.0 | Stable | Validate the payload using XML Schema and JAXP Validation. |
| [Velocity](extensions/velocity.md) | camel-quarkus-velocity | 1.1.0 | 1.2.0 | Stable | Transform messages using a Velocity template. |
| [Vert.x HTTP Client](extensions/vertx-http.md) | camel-quarkus-vertx-http | 1.1.0 | 1.1.0 | Stable | Send requests to external HTTP servers using Vert.x |
| [Vert.x WebSocket](extensions/vertx-websocket.md) | camel-quarkus-vertx-websocket | 1.1.0 | 1.1.0 | Stable | Expose WebSocket endpoints and connect to remote WebSocket servers using Vert.x |
| [Vert.x](extensions/vertx.md) | camel-quarkus-vertx | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from Vert.x Event Bus. |
| [Wasm](extensions/wasm.md) | camel-quarkus-wasm | 3.10.0 | 3.10.0 | Stable | Invoke Wasm functions. |
| [Weather](extensions/weather.md) | camel-quarkus-weather | 1.1.0 | 1.1.0 | Stable | Poll the weather information from Open Weather Map. |
| [weaviate](extensions/weaviate.md) | camel-quarkus-weaviate | 3.24.0 | 3.24.0 | Stable | Perform operations on the Weaviate Vector Database. |
| [Web3j Ethereum Blockchain](extensions/web3j.md) | camel-quarkus-web3j | 1.1.0 | n/a | Preview | Interact with Ethereum nodes using web3j client API. |
| [WordPress](extensions/wordpress.md) | camel-quarkus-wordpress | 1.1.0 | n/a | Preview | Manage posts and users using the WordPress API. |
| [Workday](extensions/workday.md) | camel-quarkus-workday | 1.1.0 | n/a | Preview | Detect and parse documents using Workday. |
| [XChange](extensions/xchange.md) | camel-quarkus-xchange | 1.1.0 | 2.0.0 | Stable | Access market data and trade on Bitcoin and Altcoin exchanges. |
| [XJ](extensions/xj.md) | camel-quarkus-xj | 1.1.0 | 3.7.0 | Stable | Transform JSON and XML message using a XSLT. |
| [XML Security Sign](extensions/xmlsecurity.md) | camel-quarkus-xmlsecurity | 1.1.0 | 1.7.0 | Stable | Sign XML payloads using the XML signature specification. |
| [XML Security Verify](extensions/xmlsecurity.md) | camel-quarkus-xmlsecurity | 1.1.0 | 1.7.0 | Stable | Verify XML payloads using the XML signature specification. |
| [XMPP](extensions/xmpp.md) | camel-quarkus-xmpp | 1.1.0 | n/a | Preview | Send and receive messages to/from an XMPP chat server. |
| [XQuery](extensions/saxon.md) | camel-quarkus-saxon | 1.1.0 | 2.0.0 | Stable | Query and/or transform XML payloads using XQuery and Saxon. |
| [XSLT Saxon](extensions/xslt-saxon.md) | camel-quarkus-xslt-saxon | 1.1.0 | 3.2.0 | Stable | Transform XML payloads using an XSLT template using Saxon. |
| [XSLT](extensions/xslt.md) | camel-quarkus-xslt | 0.4.0 | 0.4.0 | Stable | Transforms XML payload using an XSLT template. |
| [Zendesk](extensions/zendesk.md) | camel-quarkus-zendesk | 1.1.0 | 1.4.0 | Stable | Manage Zendesk tickets, users, organizations, etc. |
| [ZooKeeper Master](extensions/zookeeper-master.md) | camel-quarkus-zookeeper-master | 1.1.0 | n/a | Preview | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [ZooKeeper](extensions/zookeeper.md) | camel-quarkus-zookeeper | 1.1.0 | n/a | Preview | Manage ZooKeeper clusters. |