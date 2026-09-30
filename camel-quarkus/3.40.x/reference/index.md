# Camel Quarkus extensions reference

> **Tip**
> In case you are missing some extension in the list:
>
> -   Upvote [an existing issue](https://github.com/apache/camel-quarkus/issues) or create [a new one](https://github.com/apache/camel-quarkus/issues/new) so that we can better prioritize our work.
>     
> -   You may also want to try to add the extension yourself following our [Contributor guide](../contributor-guide/index.md).
>     
> -   You may try your luck using the given camel component on Quarkus directly (without an extension). Most probably it will work in the JVM mode and fail in the native mode. Do not hesitate to [report](https://github.com/apache/camel-quarkus/issues) any issues you encounter.

There are 344 extensions (17 deprecated, 62 JVM only)

     
| Extension | Artifact | JVM  
since | Native  
since | Support  
level | Description |
| --- | --- | --- | --- | --- | --- |
| [A2A](extensions/a2a.md) | camel-quarkus-a2a | 3.38.0 | 3.38.0 | Preview | A2A endpoint for agent-to-agent communication. |
| [ActiveMQ](extensions/activemq.md) | camel-quarkus-activemq | 1.0.0 | 1.0.0 | Stable | Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component. |
| [ActiveMQ 6.x](extensions/activemq6.md) | camel-quarkus-activemq6 | 3.30.0 | 3.30.0 | Stable | Send messages to (or consume from) Apache ActiveMQ 6.x. This component extends the Camel JMS component. |
| [AI Tool](extensions/ai-tool.md) | camel-quarkus-ai-tool | 3.39.0 | 3.39.0 | Preview | Framework-agnostic consumer endpoint that registers a Camel route as an LLM tool in the shared AiToolRegistry. |
| [AMQP](extensions/amqp.md) | camel-quarkus-amqp | 1.0.0 | 1.0.0 | Stable | Messaging with AMQP protocol using Apache Qpid Client. |
| [ArangoDb](extensions/arangodb.md) | camel-quarkus-arangodb | 1.1.0 | 1.1.0 | Stable | Perform operations on ArangoDb when used as a Document Database, or as a Graph Database |
| [AS2](extensions/as2.md) | camel-quarkus-as2 | 1.0.0 | 1.0.0 | Stable | Transfer data securely and reliably using the AS2 protocol (RFC4130). |
| [ASN.1 File](extensions/asn1.md) | camel-quarkus-asn1 | 1.1.0 | n/a | Preview | Encode and decode data structures using Abstract Syntax Notation One (ASN.1) |
| [Asterisk](extensions/asterisk.md) | camel-quarkus-asterisk | 1.1.0 | n/a | Preview | Interact with Asterisk PBX Server (VoIP). |
| [Atom](extensions/atom.md) | camel-quarkus-atom | 1.1.0 | 1.2.0 | Stable | Poll Atom RSS feeds. |
| [Attachments](extensions/attachments.md) | camel-quarkus-attachments | 0.3.0 | 0.3.0 | Stable | Support for attachments on Camel messages |
| [Avro](extensions/avro.md) | camel-quarkus-avro | 1.0.0 | 1.0.0 | Stable | Serialize and deserialize messages using Apache Avro binary data format |
| [Avro Jackson](extensions/jackson-avro.md) | camel-quarkus-jackson-avro | 2.0.0 | 2.0.0 | Stable | Marshal POJOs to Avro and back using Jackson. |
| [AWS 2 Athena](extensions/aws2-athena.md) | camel-quarkus-aws2-athena | 1.0.0 | 1.0.0 | Stable | Access AWS Athena. |
| [AWS 2 CloudWatch](extensions/aws2-cw.md) | camel-quarkus-aws2-cw | 1.0.0 | 1.0.0 | Stable | Sending metrics to AWS CloudWatch. |
| [AWS 2 DynamoDB](extensions/aws2-ddb.md) | camel-quarkus-aws2-ddb | 1.0.0 | 1.0.0 | Stable | Store and retrieve data from AWS DynamoDB. Receive messages from AWS DynamoDB Stream. |
| [AWS 2 Elastic Compute Cloud (EC2)](extensions/aws2-ec2.md) | camel-quarkus-aws2-ec2 | 1.0.0 | 1.0.0 | Stable | Manage AWS EC2 instances. |
| [AWS 2 Elastic Container Service (ECS)](extensions/aws2-ecs.md) | camel-quarkus-aws2-ecs | 1.0.0 | 1.0.0 | Stable | Manage AWS ECS cluster instances. |
| [AWS 2 Elastic Kubernetes Service (EKS)](extensions/aws2-eks.md) | camel-quarkus-aws2-eks | 1.0.0 | 1.0.0 | Stable | Manage AWS EKS cluster instances. |
| [AWS 2 Eventbridge](extensions/aws2-eventbridge.md) | camel-quarkus-aws2-eventbridge | 1.4.0 | 1.7.0 | Stable | Manage AWS EventBridge cluster instances and consume events via SQS-backed polling. |
| [AWS 2 Identity and Access Management (IAM)](extensions/aws2-iam.md) | camel-quarkus-aws2-iam | 1.0.0 | 1.0.0 | Stable | Manage AWS IAM instances. |
| [AWS 2 Key Management Service (KMS)](extensions/aws2-kms.md) | camel-quarkus-aws2-kms | 1.0.0 | 1.0.0 | Stable | Manage keys stored in AWS KMS instances. |
| [AWS 2 Kinesis](extensions/aws2-kinesis.md) | camel-quarkus-aws2-kinesis | 1.1.0 | 1.7.0 | Stable | Consume and produce records from and to AWS Kinesis Streams. Produce data to AWS Kinesis Firehose streams. |
| [AWS 2 Lambda](extensions/aws2-lambda.md) | camel-quarkus-aws2-lambda | 1.1.0 | 1.1.0 | Stable | Manage and invoke AWS Lambda functions. |
| [AWS 2 Managed Streaming for Apache Kafka (MSK)](extensions/aws2-msk.md) | camel-quarkus-aws2-msk | 1.0.0 | 1.0.0 | Stable | Manage AWS MSK instances. |
| [AWS 2 MQ](extensions/aws2-mq.md) | camel-quarkus-aws2-mq | 1.0.0 | 1.0.0 | Stable | Send messages to AWS MQ. |
| [AWS 2 S3 Storage Service](extensions/aws2-s3.md) | camel-quarkus-aws2-s3 | 1.0.0 | 1.0.0 | Stable | Store and retrieve objects from AWS S3 Storage Service. |
| [AWS 2 Security Token Service (STS)](extensions/aws2-sts.md) | camel-quarkus-aws2-sts | 1.1.0 | 1.1.0 | Stable | Manage AWS STS cluster instances. |
| [AWS 2 Simple Email Service (SES)](extensions/aws2-ses.md) | camel-quarkus-aws2-ses | 1.0.0 | 1.0.0 | Stable | Send e-mails through AWS SES service. |
| [AWS 2 Simple Notification System (SNS)](extensions/aws2-sns.md) | camel-quarkus-aws2-sns | 1.0.0 | 1.0.0 | Stable | Send messages to AWS Simple Notification Topic. |
| [AWS 2 Simple Queue Service (SQS)](extensions/aws2-sqs.md) | camel-quarkus-aws2-sqs | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from AWS SQS. |
| [AWS 2 Translate](extensions/aws2-translate.md) | camel-quarkus-aws2-translate | 1.0.0 | 1.0.0 | Stable | Translate texts using AWS Translate and AWS SDK version 2.x. |
| [AWS Bedrock](extensions/aws-bedrock.md) | camel-quarkus-aws-bedrock | 3.10.0 | 3.10.0 | Stable | Invoke Model of AWS Bedrock service. |
| [AWS Cloudtrail](extensions/aws-cloudtrail.md) | camel-quarkus-aws-cloudtrail | 3.38.0 | 3.38.0 | Stable | Consume events from Amazon CloudTrail using AWS SDK version 2.x. |
| [AWS Secrets Manager](extensions/aws-secrets-manager.md) | camel-quarkus-aws-secrets-manager | 2.0.0 | 3.19.0 | Stable | Manage secrets using AWS Secrets Manager. |
| [Azure CosmosDB](extensions/azure-cosmosdb.md) | camel-quarkus-azure-cosmosdb | 2.0.0 | n/a | Preview | To read and write records to the CosmosDB database on Azure cloud platform. |
| [Azure Event Hubs](extensions/azure-eventhubs.md) | camel-quarkus-azure-eventhubs | 1.7.0 | 1.7.0 | Stable | Send and receive events to/from Azure Event Hubs using AMQP protocol. |
| [Azure Files](extensions/azure-files.md) | camel-quarkus-azure-files | 3.22.0 | n/a | Preview | Send and receive files to Azure storage file share |
| [Azure Key Vault](extensions/azure-key-vault.md) | camel-quarkus-azure-key-vault | 2.10.0 | 3.13.0 | Stable | Manage secrets and keys in Azure Key Vault Service |
| [Azure ServiceBus](extensions/azure-servicebus.md) | camel-quarkus-azure-servicebus | 2.8.0 | 3.19.0 | Stable | Send and receive messages to/from Azure Service Bus. |
| [Azure Storage Blob Service](extensions/azure-storage-blob.md) | camel-quarkus-azure-storage-blob | 1.1.0 | 1.6.0 | Stable | Store and retrieve blobs from Azure Storage Blob Service. |
| [Azure storage datalake service](extensions/azure-storage-datalake.md) | camel-quarkus-azure-storage-datalake | 1.8.0 | 3.24.0 | Stable | Sends and receives files to/from Azure Data Lake Storage. |
| [Azure Storage Queue Service](extensions/azure-storage-queue.md) | camel-quarkus-azure-storage-queue | 1.1.0 | 1.7.0 | Stable | Stores and retrieves messages to/from Azure Storage Queue. |
| [Barcode](extensions/barcode.md) | camel-quarkus-barcode | 1.1.0 | n/a | Preview | Transform strings to various 1D/2D barcode bitmap formats and back |
| [Base64](extensions/base64.md) | camel-quarkus-base64 | 1.0.0 | 1.0.0 | Stable | Encode and decode data using Base64 |
| [Bean](extensions/bean.md) | camel-quarkus-bean | 0.1.0 | 0.1.0 | Stable | Invoke methods of Java beans |
| [Bean Validator](extensions/bean-validator.md) | camel-quarkus-bean-validator | 1.0.0 | 1.0.0 | Stable | Validate the message body using the Java Bean Validation API. |
| [BeanIO](extensions/beanio.md) | camel-quarkus-beanio | 3.8.0 | 3.16.0 | Stable | Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats) |
| [Bindy](extensions/bindy.md) | camel-quarkus-bindy | 1.0.0 | 1.0.0 | Stable | Marshal and unmarshal between POJOs on one side and Comma separated values (CSV), fixed field length or key-value pair (KVP) formats on the other side using Camel Bindy |
| [Bonita](extensions/bonita.md) | camel-quarkus-bonita | 1.1.0 | n/a | Preview | Communicate with a remote Bonita BPM process engine. |
| [Box](extensions/box.md) | camel-quarkus-box | 1.0.0 | 1.0.0 | Stable | Upload, download and manage files, folders, groups, collaborations, etc. on box.com. |
| [Braintree](extensions/braintree.md) | camel-quarkus-braintree | 1.0.0 | 1.0.0 | Stable | Process payments using Braintree Payments. |
| [Browse](extensions/browse.md) | camel-quarkus-browse | 1.1.0 | 1.2.0 | Stable | Inspect the messages received on endpoints supporting BrowsableEndpoint. |
| [Caffeine Cache](extensions/caffeine.md) | camel-quarkus-caffeine | 1.1.0 | 1.2.0 | Stable | Perform caching operations using Caffeine Cache. |
| [Cassandra CQL](extensions/cassandraql.md) | camel-quarkus-cassandraql | 1.0.0 | 1.7.0 | Stable | Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax. |
| [CBOR](extensions/cbor.md) | camel-quarkus-cbor | 1.1.0 | 1.7.0 | Stable | Unmarshal a CBOR payload to POJO and back |
| [ChatScript](extensions/chatscript.md) | camel-quarkus-chatscript | 1.1.0 | n/a | Preview | Chat with a ChatScript Server. |
| [Chunk](extensions/chunk.md) | camel-quarkus-chunk | 1.1.0 | n/a | Preview | Transform messages using Chunk templating engine. |
| [CLI Connector](extensions/cli-connector.md) | camel-quarkus-cli-connector | 3.2.0 | n/a | Preview | Runtime adapter connecting with Camel CLI |
| [CLI Debug](extensions/cli-debug.md) | camel-quarkus-cli-debug | 3.31.0 | n/a | Preview | Remote CLI debugger |
| [Cloudevents](extensions/cloudevents.md) | camel-quarkus-cloudevents | 2.14.0 | 2.14.0 | Stable | Camel support for the CloudEvents specification |
| [CM SMS Gateway](extensions/cm-sms.md) | camel-quarkus-cm-sms | 1.1.0 | n/a | Preview | Send SMS messages via CM SMS Gateway. |
| [CoAP](extensions/coap.md) | camel-quarkus-coap | 1.1.0 | n/a | Preview | Send and receive messages to/from CoAP (Constrained Application Protocol) capable devices. |
| [CometD](extensions/cometd.md) | camel-quarkus-cometd | 1.1.0 | n/a | Preview | Offers publish/subscribe, peer-to-peer (via a server), and RPC style messaging using the CometD/Bayeux protocol. |
| [Console](extensions/console.md) | camel-quarkus-console | 2.16.0 | n/a | Preview | Camel Developer Console |
| [Consul](extensions/consul.md) | camel-quarkus-consul | 1.0.0 | 1.0.0 | Stable | Integrate with Consul service discovery and configuration store. |
| [Control Bus](extensions/controlbus.md) | camel-quarkus-controlbus | 0.4.0 | 0.4.0 | Stable | Manage and monitor Camel routes. |
| [Core](extensions/core.md) | camel-quarkus-core | 0.0.1 | 0.0.1 | Stable | Camel core functionality and basic Camel languages: Constant, ExchangeProperty, Header, Ref, Simple and Tokenize |
| [Couchbase](extensions/couchbase.md) | camel-quarkus-couchbase | 1.0.0 | n/a | Preview | Query Couchbase databases using SQL (N1QL) queries or MapReduce Views with a poll strategy and/or perform various operations against Couchbase databases. |
| [CouchDB](extensions/couchdb.md) | camel-quarkus-couchdb | 1.0.0 | 1.0.0 | Stable | Consume changesets for inserts, updates and deletes in a CouchDB database, as well as get, save, update and delete documents from a CouchDB database. |
| [Cron](extensions/cron.md) | camel-quarkus-cron | 1.0.0 | 1.0.0 | Stable | A generic interface for triggering events at times specified through the Unix cron syntax. |
| [Crypto (JCE)](extensions/crypto.md) | camel-quarkus-crypto | 1.1.0 | 1.2.0 | Stable | Sign and verify exchanges using the Signature Service of the Java Cryptographic Extension (JCE). |
| [CSimple](extensions/csimple.md) | camel-quarkus-csimple | 1.5.0 | 1.5.0 | Preview Deprecated | Compiled Simple language |
| [CSV](extensions/csv.md) | camel-quarkus-csv | 0.2.0 | 0.2.0 | Stable | Handle CSV (Comma Separated Values) payloads |
| [CXF](extensions/cxf-soap.md) | camel-quarkus-cxf-soap | 2.12.0 | 2.12.0 | Stable | Expose SOAP WebServices using Apache CXF or connect to external WebServices using CXF WS client. |
| [CyberArk Vault](extensions/cyberark-vault.md) | camel-quarkus-cyberark-vault | 3.31.0 | 3.31.0 | Stable | Retrieve secrets from CyberArk Conjur Vault. |
| [Data Format](extensions/dataformat.md) | camel-quarkus-dataformat | 0.4.0 | 0.4.0 | Stable | Use a Camel Data Format as a regular Camel Component. |
| [Dataset](extensions/dataset.md) | camel-quarkus-dataset | 2.11.0 | 2.11.0 | Stable | Provide data for load and soak testing of your Camel application. |
| [DataSonnet](extensions/datasonnet.md) | camel-quarkus-datasonnet | 2.10.0 | 2.10.0 | Stable | To use DataSonnet scripts for message transformations |
| [Debezium MongoDB Connector](extensions/debezium-mongodb.md) | camel-quarkus-debezium-mongodb | 1.0.0 | 1.6.0 | Stable | Capture changes from a MongoDB database. |
| [Debezium MySQL Connector](extensions/debezium-mysql.md) | camel-quarkus-debezium-mysql | 1.0.0 | 1.0.0 | Stable | Capture changes from a MySQL database. |
| [Debezium Oracle Connector](extensions/debezium-oracle.md) | camel-quarkus-debezium-oracle | 3.24.0 | 3.24.0 | Stable | Capture changes from an Oracle database. |
| [Debezium PostgresSQL Connector](extensions/debezium-postgres.md) | camel-quarkus-debezium-postgres | 1.0.0 | 1.0.0 | Stable | Capture changes from a PostgreSQL database. |
| [Debezium SQL Server Connector](extensions/debezium-sqlserver.md) | camel-quarkus-debezium-sqlserver | 1.0.0 | 1.0.0 | Stable | Capture changes from an SQL Server database. |
| [Debug](extensions/debug.md) | camel-quarkus-debug | 2.10.0 | 3.2.0 | Stable | Enables Camel Route Debugging |
| [Deep Java Library](extensions/djl.md) | camel-quarkus-djl | 1.1.0 | n/a | Preview | Infer Deep Learning models from message exchanges data using Deep Java Library (DJL). |
| [DFDL](extensions/dfdl.md) | camel-quarkus-dfdl | 3.22.0 | n/a | Preview | Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL). |
| [Diagram](extensions/diagram.md) | camel-quarkus-diagram | 3.38.0 | n/a | Preview | Camel Route Diagram rendering |
| [DigitalOcean](extensions/digitalocean.md) | camel-quarkus-digitalocean | 1.1.0 | 2.0.0 | Stable Deprecated | Manage Droplets and resources within the DigitalOcean cloud. |
| [Direct](extensions/direct.md) | camel-quarkus-direct | 0.0.1 | 0.0.1 | Stable | Call another endpoint from the same Camel Context synchronously. |
| [Disruptor](extensions/disruptor.md) | camel-quarkus-disruptor | 1.1.0 | 1.2.0 | Stable | Provides asynchronous SEDA behavior using LMAX Disruptor. |
| [DNS](extensions/dns.md) | camel-quarkus-dns | 1.1.0 | n/a | Preview | Perform DNS queries using DNSJava. |
| [Docling](extensions/docling.md) | camel-quarkus-docling | 3.29.0 | 3.31.0 | Stable | Process documents using Docling library for parsing and conversion. |
| [Drill](extensions/drill.md) | camel-quarkus-drill | 1.1.0 | n/a | Preview | Perform queries against an Apache Drill cluster. |
| [Dropbox](extensions/dropbox.md) | camel-quarkus-dropbox | 1.1.0 | 1.1.0 | Stable | Upload, download and manage files, folders, groups, collaborations, etc on Dropbox. |
| [DSL Modeline](extensions/dsl-modeline.md) | camel-quarkus-dsl-modeline | 2.14.0 | n/a | Preview | Camel DSL modeline |
| [Ehcache](extensions/ehcache.md) | camel-quarkus-ehcache | 1.1.0 | n/a | Preview | Perform caching operations using Ehcache. |
| [Elasticsearch](extensions/elasticsearch.md) | camel-quarkus-elasticsearch | 3.2.0 | 3.36.0 | Stable | Send requests to Elasticsearch via Java Client API. |
| [Elasticsearch Low level Rest Client](extensions/elasticsearch-rest-client.md) | camel-quarkus-elasticsearch-rest-client | 3.8.0 | 3.12.0 | Stable | Perform queries and other operations on Elasticsearch or OpenSearch (uses low-level client). |
| [Exec](extensions/exec.md) | camel-quarkus-exec | 0.4.0 | 0.4.0 | Stable | Execute commands on the underlying operating system. |
| [FHIR](extensions/fhir.md) | camel-quarkus-fhir | 0.3.0 | 0.3.0 | Stable | Exchange information in the healthcare domain using the FHIR (Fast Healthcare Interoperability Resources) standard. |
| [File](extensions/file.md) | camel-quarkus-file | 0.4.0 | 0.4.0 | Stable | Read and write files. |
| [File Cluster Service](extensions/file-cluster-service.md) | camel-quarkus-file-cluster-service | 3.10.0 | 3.10.0 | Stable | Provides a FileLock implementation of the Camel Cluster Service SPI |
| [File Watch](extensions/file-watch.md) | camel-quarkus-file-watch | 1.0.0 | 1.0.0 | Stable | Get notified about file events in a directory using java.nio.file.WatchService. |
| [Flatpack](extensions/flatpack.md) | camel-quarkus-flatpack | 1.1.0 | 1.1.0 | Stable | Parse fixed width and delimited files using the FlatPack library. |
| [Flink](extensions/flink.md) | camel-quarkus-flink | 1.1.0 | n/a | Preview | Send DataSet jobs to an Apache Flink cluster. |
| [FOP](extensions/fop.md) | camel-quarkus-fop | 1.1.0 | 1.2.0 | Stable | Render messages into PDF and other output formats supported by Apache FOP. |
| [Fory](extensions/fory.md) | camel-quarkus-fory | 3.18.0 | 3.18.0 | Stable | Serialize and deserialize messages using Apache Fory |
| [Freemarker](extensions/freemarker.md) | camel-quarkus-freemarker | 1.1.0 | 1.8.0 | Stable | Transform messages using FreeMarker templates. |
| [FTP](extensions/ftp.md) | camel-quarkus-ftp | 1.0.0 | 1.0.0 | Stable | Upload and download files to/from SFTP, FTP or SFTP servers |
| [Geocoder](extensions/geocoder.md) | camel-quarkus-geocoder | 1.1.0 | 1.2.0 | Stable | Find geocodes (latitude and longitude) for a given address or the other way round. |
| [Git](extensions/git.md) | camel-quarkus-git | 1.1.0 | 1.1.0 | Stable | Perform operations on git repositories. |
| [GitHub2](extensions/github2.md) | camel-quarkus-github2 | 3.38.0 | 3.38.0 | Stable | Interact with the GitHub API. |
| [Google BigQuery](extensions/google-bigquery.md) | camel-quarkus-google-bigquery | 1.0.0 | 1.6.0 | Stable | Access Google Cloud BigQuery service using SQL queries or Google Client Services API |
| [Google Calendar](extensions/google-calendar.md) | camel-quarkus-google-calendar | 1.0.0 | 1.0.0 | Stable | Perform various operations on a Google Calendar. |
| [Google Drive](extensions/google-drive.md) | camel-quarkus-google-drive | 1.0.0 | 1.0.0 | Stable | Manage files in Google Drive. |
| [Google Mail](extensions/google-mail.md) | camel-quarkus-google-mail | 1.0.0 | 1.0.0 | Stable | Manage messages in Google Mail. |
| [Google Pubsub](extensions/google-pubsub.md) | camel-quarkus-google-pubsub | 1.0.0 | 1.5.0 | Stable | Send and receive messages to/from Google Cloud Platform PubSub Service. |
| [Google Secret Manager](extensions/google-secret-manager.md) | camel-quarkus-google-secret-manager | 2.8.0 | 3.19.0 | Stable | Manage Google Secret Manager Secrets |
| [Google Sheets](extensions/google-sheets.md) | camel-quarkus-google-sheets | 1.0.0 | 1.0.0 | Stable | Manage spreadsheets in Google Sheets. |
| [Google Storage](extensions/google-storage.md) | camel-quarkus-google-storage | 2.0.0 | 2.0.0 | Stable | Store and retrieve objects from Google Cloud Storage Service using the google-cloud-storage library. |
| [GoogleCloudFunctions](extensions/google-functions.md) | camel-quarkus-google-functions | 2.0.0 | n/a | Preview | Manage and invoke Google Cloud Functions |
| [GraphQL](extensions/graphql.md) | camel-quarkus-graphql | 1.0.0 | 1.0.0 | Stable | Send GraphQL queries and mutations to external systems. |
| [Grok](extensions/grok.md) | camel-quarkus-grok | 1.0.0 | 1.0.0 | Stable | Unmarshal unstructured data to objects using Logstash based Grok patterns |
| [Groovy](extensions/groovy.md) | camel-quarkus-groovy | 1.0.0 | 3.2.0 | Stable | Evaluate a Groovy script |
| [gRPC](extensions/grpc.md) | camel-quarkus-grpc | 1.0.0 | 1.0.0 | Stable | Expose gRPC endpoints and access external gRPC endpoints. |
| [Gson](extensions/gson.md) | camel-quarkus-gson | 1.0.0 | 1.0.0 | Stable | Marshal POJOs to JSON and back using Gson |
| [Hashicorp Vault](extensions/hashicorp-vault.md) | camel-quarkus-hashicorp-vault | 2.11.0 | 3.15.0 | Stable | Manage secrets in HashiCorp Vault Service |
| [Hazelcast Atomic Number](extensions/hazelcast.md) | camel-quarkus-hazelcast | 1.1.0 | 1.6.0 | Stable Deprecated | Increment, decrement, set, etc. Hazelcast atomic number (a grid wide number). |
| [Headersmap](extensions/headersmap.md) | camel-quarkus-headersmap | 1.2.0 | 1.2.0 | Stable Deprecated | Fast case-insensitive headers map implementation |
| [HL7](extensions/hl7.md) | camel-quarkus-hl7 | 1.1.0 | 1.8.0 | Stable | Marshal and unmarshal HL7 (Health Care) model objects using the HL7 MLLP codec. |
| [HTTP](extensions/http.md) | camel-quarkus-http | 1.0.0 | 1.0.0 | Stable | Send requests to external HTTP servers using Apache HTTP Client 5.x. |
| [IBM Cloud Object Storage](extensions/ibm-cos.md) | camel-quarkus-ibm-cos | 3.30.0 | 3.31.0 | Stable | Store and retrieve objects from IBM Cloud Object Storage. |
| [IBM Secrets Manager](extensions/ibm-secrets-manager.md) | camel-quarkus-ibm-secrets-manager | 3.22.0 | n/a | Preview | Manage secrets in IBM Secrets Manager Service |
| [IBM Watson Discovery](extensions/ibm-watson-discovery.md) | camel-quarkus-ibm-watson-discovery | 3.30.0 | 3.35.0 | Stable | Perform document understanding and search using IBM Watson Discovery |
| [IBM Watson Language](extensions/ibm-watson-language.md) | camel-quarkus-ibm-watson-language | 3.30.0 | 3.35.0 | Stable | Perform natural language processing using IBM Watson Natural Language Understanding |
| [iCal](extensions/ical.md) | camel-quarkus-ical | 1.0.0 | 1.0.0 | Stable | Marshal and unmarshal iCal (\*.ics) documents to/from model objects |
| [IEC 60870 Client](extensions/iec60870.md) | camel-quarkus-iec60870 | 1.1.0 | n/a | Preview Deprecated | IEC 60870 supervisory control and data acquisition (SCADA) client using NeoSCADA implementation. |
| [Ignite Cache](extensions/ignite.md) | camel-quarkus-ignite | 1.1.0 | n/a | Preview | Perform cache operations on an Ignite cache or consume changes from a continuous query. |
| [Infinispan](extensions/infinispan.md) | camel-quarkus-infinispan | 0.0.1 | 0.0.1 | Stable | Read and write from/to Infinispan distributed key/value store and data grid. |
| [Infinispan Cluster Service](extensions/infinispan-cluster-service.md) | camel-quarkus-infinispan-cluster-service | 3.32.0 | 3.32.0 | Stable | Provides an Infinispan implementation of the Camel Cluster Service SPI |
| [InfluxDB](extensions/influxdb.md) | camel-quarkus-influxdb | 1.0.0 | 1.0.0 | Stable | Interact with InfluxDB v1, a time series database. |
| [IRC](extensions/irc.md) | camel-quarkus-irc | 1.1.0 | n/a | Preview Deprecated | Send and receive messages to/from an IRC chat. |
| [ISO-8583](extensions/iso8583.md) | camel-quarkus-iso8583 | 3.26.0 | 3.26.0 | Stable | Create, edit and read ISO-8583 messages |
| [Jackson](extensions/jackson.md) | camel-quarkus-jackson | 0.3.0 | 0.3.0 | Stable | Marshal POJOs to JSON and back using Jackson. |
| [JacksonXML](extensions/jacksonxml.md) | camel-quarkus-jacksonxml | 1.0.0 | 1.0.0 | Stable | Unmarshal an XML payloads to POJOs and back using XMLMapper extension of Jackson |
| [Jasypt](extensions/jasypt.md) | camel-quarkus-jasypt | 1.2.0 | 3.7.0 | Stable | Security using Jasypt |
| [Java jOOR DSL](extensions/java-joor-dsl.md) | camel-quarkus-java-joor-dsl | 1.8.0 | 2.16.0 | Stable | Camel Java DSL with jOOR |
| [JavaScript](extensions/javascript.md) | camel-quarkus-javascript | 3.14.0 | n/a | Preview | Evaluates a JavaScript expression |
| [JAXB](extensions/jaxb.md) | camel-quarkus-jaxb | 1.0.0 | 1.0.0 | Stable | Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard |
| [JCache](extensions/jcache.md) | camel-quarkus-jcache | 1.2.0 | 2.13.0 | Stable | Perform caching operations against JSR107/JCache. |
| [JCR](extensions/jcr.md) | camel-quarkus-jcr | 1.1.0 | n/a | Preview | Read and write nodes to/from a JCR compliant content repository. |
| [JDBC](extensions/jdbc.md) | camel-quarkus-jdbc | 0.0.1 | 0.0.1 | Stable | Access databases through SQL and JDBC. |
| [Jfr](extensions/jfr.md) | camel-quarkus-jfr | 1.7.0 | 2.6.0 | Stable | Diagnose Camel applications with Java Flight Recorder |
| [JGroups](extensions/jgroups.md) | camel-quarkus-jgroups | 1.1.0 | n/a | Preview | Exchange messages with JGroups clusters. |
| [JGroups raft](extensions/jgroups-raft.md) | camel-quarkus-jgroups-raft | 1.1.0 | n/a | Preview | Exchange messages with JGroups-raft clusters. |
| [Jira](extensions/jira.md) | camel-quarkus-jira | 1.0.0 | 1.0.0 | Stable | Interact with JIRA issue tracker. |
| [JMS](extensions/jms.md) | camel-quarkus-jms | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from JMS message brokers. |
| [Jolokia](extensions/jolokia.md) | camel-quarkus-jolokia | 3.19.0 | 3.20.0 | Stable | Expose runtime metrics and management operations via JMX with Jolokia |
| [JOLT](extensions/jolt.md) | camel-quarkus-jolt | 1.0.0 | 1.0.0 | Stable | JSON to JSON transformation using JOLT. |
| [JOOQ](extensions/jooq.md) | camel-quarkus-jooq | 1.1.0 | n/a | Preview | Store and retrieve Java objects from an SQL database using JOOQ. |
| [jOOR](extensions/joor.md) | camel-quarkus-joor | 2.0.0 | 3.2.0 | Stable Deprecated | Evaluate a jOOR (Java compiled once at runtime) expression language. |
| [JPA](extensions/jpa.md) | camel-quarkus-jpa | 1.0.0 | 1.0.0 | Stable | Store and retrieve Java objects from databases using Java Persistence API (JPA). |
| [JQ](extensions/jq.md) | camel-quarkus-jq | 2.11.0 | 2.11.0 | Stable | Evaluates a JQ expression against a JSON message body |
| [JSLT](extensions/jslt.md) | camel-quarkus-jslt | 1.1.0 | 1.4.0 | Stable | Query or transform JSON payloads using JSLT. |
| [JSON Fastjson](extensions/fastjson.md) | camel-quarkus-fastjson | 1.1.0 | n/a | Preview | Marshal POJOs to JSON and back using Fastjson |
| [JSON Path](extensions/jsonpath.md) | camel-quarkus-jsonpath | 1.0.0 | 1.0.0 | Stable | Evaluates a JSONPath expression against a JSON message body |
| [JSON Schema Validator](extensions/json-validator.md) | camel-quarkus-json-validator | 1.0.0 | 1.0.0 | Stable | Validate JSON payloads using NetworkNT JSON Schema. |
| [JSON-B](extensions/jsonb.md) | camel-quarkus-jsonb | 1.5.0 | 1.5.0 | Stable | Marshal POJOs to JSON and back using JSON-B. |
| [JSonApi](extensions/jsonapi.md) | camel-quarkus-jsonapi | 1.1.0 | n/a | Preview | Marshal and unmarshal JSON:API resources using JSONAPI-Converter library |
| [JSONATA](extensions/jsonata.md) | camel-quarkus-jsonata | 1.6.0 | 1.6.0 | Stable | Transforms JSON payload using JSONata transformation. |
| [JsonPatch](extensions/json-patch.md) | camel-quarkus-json-patch | 2.7.0 | n/a | Preview Deprecated | Transforms JSON using JSON patch (RFC 6902). |
| [Jsoup](extensions/jsoup.md) | camel-quarkus-jsoup | 3.38.0 | 3.38.0 | Stable | Cleanup HTML content |
| [JT400](extensions/jt400.md) | camel-quarkus-jt400 | 1.1.0 | 3.8.0 | Stable | Exchanges messages with an IBM i system using data queues, message queues, or program call. IBM i is the replacement for AS/400 and iSeries servers. |
| [JTA](extensions/jta.md) | camel-quarkus-jta | 1.0.0 | 1.0.0 | Stable | Using Camel With JTA Transaction Manager |
| [Kafka](extensions/kafka.md) | camel-quarkus-kafka | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from an Apache Kafka broker. |
| [Kamelet](extensions/kamelet.md) | camel-quarkus-kamelet | 1.7.0 | 1.7.0 | Stable | To call Kamelets |
| [Keycloak](extensions/keycloak.md) | camel-quarkus-keycloak | 3.29.0 | 3.31.0 | Preview | Manage Keycloak instances via Admin API. |
| [Knative](extensions/knative.md) | camel-quarkus-knative | 2.14.0 | 2.14.0 | Stable | Send and receive events from Knative. |
| [Knative Consumer](extensions/knative-consumer.md) | camel-quarkus-knative-consumer | 2.14.0 | 2.14.0 | Stable | Receives events from Knative |
| [Knative Producer](extensions/knative-producer.md) | camel-quarkus-knative-producer | 2.14.0 | 2.14.0 | Stable | Sends events to Knative |
| [Kubernetes](extensions/kubernetes.md) | camel-quarkus-kubernetes | 1.0.0 | 1.0.0 | Stable | Perform operations against Kubernetes API |
| [Kubernetes Cluster Service](extensions/kubernetes-cluster-service.md) | camel-quarkus-kubernetes-cluster-service | 3.10.0 | 3.10.0 | Stable | Provides a Kubernetes implementation of the Camel Cluster Service SPI |
| [Kudu](extensions/kudu.md) | camel-quarkus-kudu | 1.0.0 | 1.0.0 | Stable | Interact with Apache Kudu, a free and open source column-oriented data store of the Apache Hadoop ecosystem. |
| [LangChain4j Agent](extensions/langchain4j-agent.md) | camel-quarkus-langchain4j-agent | 3.26.0 | 3.27.0 | Preview | LangChain4j Agent component |
| [LangChain4j Chat](extensions/langchain4j-chat.md) | camel-quarkus-langchain4j-chat | 3.11.0 | 3.12.0 | Preview | LangChain4j Chat component |
| [LangChain4j Embedding Store](extensions/langchain4j-embeddingstore.md) | camel-quarkus-langchain4j-embeddingstore | 3.29.0 | 3.29.0 | Preview | Perform operations on the LangChain4jEmbeddingStores. |
| [LangChain4j Embeddings](extensions/langchain4j-embeddings.md) | camel-quarkus-langchain4j-embeddings | 3.10.0 | 3.29.0 | Preview | LangChain4j Embeddings |
| [LangChain4j Ingest](extensions/langchain4j-ingest.md) | camel-quarkus-langchain4j-ingest | 3.39.0 | 3.39.0 | Experimental | Declarative AI document ingestion: point a knowledge base at a folder via configuration; splitting, embedding and storing are handled under the hood |
| [LangChain4j Tokenizer](extensions/langchain4j-tokenizer.md) | camel-quarkus-langchain4j-tokenizer | 3.15.0 | 3.24.0 | Preview | LangChain4j Tokenizer |
| [LangChain4j Tools](extensions/langchain4j-tools.md) | camel-quarkus-langchain4j-tools | 3.15.0 | 3.24.0 | Preview Deprecated | LangChain4j Tools and Function Calling Features |
| [LangChain4j Web Search](extensions/langchain4j-web-search.md) | camel-quarkus-langchain4j-web-search | 3.15.0 | 3.24.0 | Preview | LangChain4j Web Search Engine |
| [Language](extensions/language.md) | camel-quarkus-language | 1.1.0 | 2.2.0 | Stable | Execute scripts in any of the languages supported by Camel. |
| [LDAP](extensions/ldap.md) | camel-quarkus-ldap | 1.1.0 | 3.2.0 | Stable | Perform searches on LDAP servers. |
| [LDIF](extensions/ldif.md) | camel-quarkus-ldif | 1.1.0 | n/a | Preview | Perform updates on an LDAP server from an LDIF body content. |
| [LevelDB](extensions/leveldb.md) | camel-quarkus-leveldb | 1.2.0 | 1.2.0 | Stable Deprecated | Using LevelDB as persistent EIP store |
| [Log](extensions/log.md) | camel-quarkus-log | 0.0.1 | 0.0.1 | Stable | Prints data from the routed message (such as body and headers) to the logger. |
| [LRA](extensions/lra.md) | camel-quarkus-lra | 1.2.0 | 1.8.0 | Stable | Camel saga binding for Long-Running-Action framework |
| [Lucene](extensions/lucene.md) | camel-quarkus-lucene | 1.1.0 | n/a | Preview | Perform inserts or queries against Apache Lucene databases. |
| [Lumberjack](extensions/lumberjack.md) | camel-quarkus-lumberjack | 1.1.0 | 1.4.0 | Stable | Receive logs messages using the Lumberjack protocol. |
| [LZF Deflate Compression](extensions/lzf.md) | camel-quarkus-lzf | 1.0.0 | 1.0.0 | Stable | Compress and decompress streams using LZF deflate algorithm |
| [Mail](extensions/mail.md) | camel-quarkus-mail | 0.2.0 | 0.2.0 | Stable | Send and receive emails using imap, pop3 and smtp protocols. |
| [Mail Microsoft Oauth](extensions/mail-microsoft-oauth.md) | camel-quarkus-mail-microsoft-oauth | 3.8.0 | 3.25.0 | Stable | Camel Mail OAuth2 Authenticator for Microsoft Exchange Online |
| [Management](extensions/management.md) | camel-quarkus-management | 1.1.0 | 3.2.0 | Stable | Camel Management |
| [MapStruct](extensions/mapstruct.md) | camel-quarkus-mapstruct | 3.2.0 | 3.2.0 | Stable | Type Conversion using MapStruct |
| [Master](extensions/master.md) | camel-quarkus-master | 1.0.0 | 1.0.0 | Stable | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |
| [MCP Server](extensions/mcp-server.md) | camel-quarkus-mcp-server | 3.39.0 | 3.39.0 | Preview | Expose ai-tool routes as MCP tools over streamable HTTP |
| [Mdc](extensions/mdc.md) | camel-quarkus-mdc | 3.29.0 | 3.29.0 | Stable | Logging MDC (Mapped Diagnostic Context) Service |
| [Micrometer](extensions/micrometer.md) | camel-quarkus-micrometer | 1.5.0 | 1.5.0 | Stable | Collect various metrics directly from Camel routes using the Micrometer library. |
| [Micrometer Observability 2](extensions/micrometer-observability.md) | camel-quarkus-micrometer-observability | 3.39.0 | 3.39.0 | Preview | Micrometer Observability implementation of Camel Telemetry |
| [Microprofile Fault Tolerance](extensions/microprofile-fault-tolerance.md) | camel-quarkus-microprofile-fault-tolerance | 1.0.0 | 1.0.0 | Stable | Circuit Breaker EIP using MicroProfile Fault Tolerance |
| [MicroProfile Health](extensions/microprofile-health.md) | camel-quarkus-microprofile-health | 0.3.0 | 0.3.0 | Stable | Expose Camel health checks via MicroProfile Health |
| [Milvus](extensions/milvus.md) | camel-quarkus-milvus | 3.10.0 | 3.33.0 | Stable | Perform operations on the Milvus Vector Database. |
| [MINA SFTP](extensions/mina-sftp.md) | camel-quarkus-mina-sftp | 3.33.0 | 3.33.0 | Stable | Upload and download files to/from SFTP servers using Apache MINA SSHD. |
| [Minio](extensions/minio.md) | camel-quarkus-minio | 1.5.0 | 1.6.0 | Stable | Store and retrieve objects from Minio Storage Service using Minio SDK. |
| [MLLP](extensions/mllp.md) | camel-quarkus-mllp | 1.1.0 | 2.0.0 | Stable | Communicate with external systems using the MLLP protocol. |
| [Mock](extensions/mock.md) | camel-quarkus-mock | 1.0.0 | 1.0.0 | Stable | Test routes and mediation rules using mocks. |
| [MongoDB](extensions/mongodb.md) | camel-quarkus-mongodb | 1.0.0 | 1.0.0 | Stable | Perform operations on MongoDB documents and collections. |
| [MongoDB GridFS](extensions/mongodb-gridfs.md) | camel-quarkus-mongodb-gridfs | 1.0.0 | 1.0.0 | Stable | Interact with MongoDB GridFS. |
| [Mustache](extensions/mustache.md) | camel-quarkus-mustache | 1.0.0 | 1.0.0 | Stable | Transform messages using a Mustache template. |
| [MVEL](extensions/mvel.md) | camel-quarkus-mvel | 1.1.0 | n/a | Preview | Transform messages using an MVEL template. |
| [MyBatis](extensions/mybatis.md) | camel-quarkus-mybatis | 1.1.0 | 2.8.0 | Stable | Performs a query, poll, insert, update or delete in a relational database using MyBatis. |
| [Nats](extensions/nats.md) | camel-quarkus-nats | 1.1.0 | 1.1.0 | Stable | Send and receive messages from NATS messaging system. |
| [Netty](extensions/netty.md) | camel-quarkus-netty | 0.4.0 | 0.4.0 | Stable | Socket level networking using TCP or UDP with Netty 4.x. |
| [Netty HTTP](extensions/netty-http.md) | camel-quarkus-netty-http | 0.2.0 | 0.2.0 | Stable | Netty HTTP server and client using the Netty 4.x. |
| [OAI-PMH](extensions/oaipmh.md) | camel-quarkus-oaipmh | 1.7.0 | 1.7.0 | Stable | Harvest metadata using OAI-PMH protocol |
| [Oauth](extensions/oauth.md) | camel-quarkus-oauth | 3.31.0 | 3.31.0 | Stable | Camel OAuth (Preview) |
| [Observability Services](extensions/observability-services.md) | camel-quarkus-observability-services | 3.19.0 | 3.19.0 | Stable | Camel Observability Services |
| [OCSF](extensions/ocsf.md) | camel-quarkus-ocsf | 3.38.0 | 3.38.0 | Stable | Marshal and unmarshal OCSF (Open Cybersecurity Schema Framework) security events to/from JSON |
| [OGNL](extensions/ognl.md) | camel-quarkus-ognl | 1.0.0 | 3.2.0 | Stable Deprecated | Evaluates an OGNL expression (Apache Commons OGNL) |
| [Olingo4](extensions/olingo4.md) | camel-quarkus-olingo4 | 1.0.0 | 1.0.0 | Stable Deprecated | Communicate with OData 4.0 services using Apache Olingo OData API. |
| [Once](extensions/once.md) | camel-quarkus-once | 3.31.0 | 3.31.0 | Stable | Trigger a single message only once at startup (useful for development and testing purposes). |
| [OPC UA Browser](extensions/milo.md) | camel-quarkus-milo | 3.31.0 | 3.31.0 | Stable | Connect to OPC UA servers using the binary protocol for browsing the node tree. |
| [OpenAI](extensions/openai.md) | camel-quarkus-openai | 3.32.0 | 3.32.0 | Stable | OpenAI endpoint for chat completion, Responses API, embeddings, audio transcription, audio translation, and text-to-speech. |
| [OpenAPI Java](extensions/openapi-java.md) | camel-quarkus-openapi-java | 1.0.0 | 1.0.0 | Stable | Rest DSL support for using OpenApi doc |
| [OpenAPI Validator](extensions/openapi-validator.md) | camel-quarkus-openapi-validator | 3.38.0 | 3.38.0 | Stable | OpenAPI validator for Camel Rest DSL |
| [OpenSearch](extensions/opensearch.md) | camel-quarkus-opensearch | 3.8.0 | n/a | Preview | Send requests to OpenSearch via Java Client API. |
| [OpenStack](extensions/openstack.md) | camel-quarkus-openstack | 1.0.0 | 2.0.0 | Stable | Interact with OpenStack APIs |
| [OpenTelemetry](extensions/opentelemetry.md) | camel-quarkus-opentelemetry | 2.1.0 | 2.1.0 | Stable Deprecated | Distributed tracing using OpenTelemetry |
| [Opentelemetry2](extensions/opentelemetry2.md) | camel-quarkus-opentelemetry2 | 3.22.0 | 3.22.0 | Stable | Implementation of Camel Opentelemetry based on the Camel Telemetry spec |
| [OptaPlanner](extensions/optaplanner.md) | camel-quarkus-optaplanner | 1.1.0 | n/a | Preview | Solve planning problems with OptaPlanner. |
| [Paho](extensions/paho.md) | camel-quarkus-paho | 0.2.0 | 0.2.0 | Stable Deprecated | Communicate with MQTT message brokers using Eclipse Paho MQTT Client. |
| [Paho MQTT5](extensions/paho-mqtt5.md) | camel-quarkus-paho-mqtt5 | 1.8.0 | 1.8.0 | Stable | Communicate with MQTT message brokers using Eclipse Paho MQTT v5 Client. |
| [PDF](extensions/pdf.md) | camel-quarkus-pdf | 0.3.1 | 0.3.1 | Stable | Create, modify or extract content from PDF documents. |
| [PGP](extensions/crypto-pgp.md) | camel-quarkus-crypto-pgp | 3.13.0 | 3.13.0 | Stable | Encrypt and decrypt messages using Java Cryptographic Extension (JCE) and PGP |
| [Pinecone](extensions/pinecone.md) | camel-quarkus-pinecone | 3.12.0 | 3.12.0 | Preview | Perform operations on the Pinecone Vector Database. |
| [Platform HTTP](extensions/platform-http.md) | camel-quarkus-platform-http | 0.3.0 | 0.3.0 | Stable | Expose HTTP endpoints using the HTTP server available in the current platform. |
| [PostgresSQL Event](extensions/pgevent.md) | camel-quarkus-pgevent | 1.1.0 | 1.2.0 | Stable | Send and receive PostgreSQL events via LISTEN and NOTIFY commands. |
| [PostgresSQL Replication Slot](extensions/pg-replication-slot.md) | camel-quarkus-pg-replication-slot | 1.1.0 | 1.2.0 | Stable | Poll for PostgreSQL Write-Ahead Log (WAL) records using Streaming Replication Slots. |
| [PQC Algorithms](extensions/pqc.md) | camel-quarkus-pqc | 3.24.0 | 3.35.0 | Stable | Post Quantum Computing Signature and Verification component. |
| [Printer](extensions/printer.md) | camel-quarkus-printer | 1.1.0 | n/a | Preview | Send print jobs to printers. |
| [Protobuf](extensions/protobuf.md) | camel-quarkus-protobuf | 1.0.0 | 1.5.0 | Stable | Serialize and deserialize Java objects using Google’s Protocol buffers |
| [Protobuf Jackson](extensions/jackson-protobuf.md) | camel-quarkus-jackson-protobuf | 2.0.0 | 2.0.0 | Stable | Marshal POJOs to Protobuf and back using Jackson. |
| [PubNub](extensions/pubnub.md) | camel-quarkus-pubnub | 1.0.0 | 1.7.0 | Stable | Send and receive messages to/from PubNub data stream network for connected devices. |
| [Pulsar](extensions/pulsar.md) | camel-quarkus-pulsar | 1.1.0 | n/a | Preview | Send and receive messages from/to Apache Pulsar messaging system. |
| [Python](extensions/python.md) | camel-quarkus-python | 3.24.0 | n/a | Preview | Evaluates a Python expression |
| [Qdrant](extensions/qdrant.md) | camel-quarkus-qdrant | 3.10.0 | 3.10.0 | Stable | Perform operations on the Qdrant Vector Database. |
| [Quartz](extensions/quartz.md) | camel-quarkus-quartz | 1.0.0 | 1.0.0 | Stable | Schedule sending of messages using the Quartz 2.x scheduler. |
| [QuickFix](extensions/quickfix.md) | camel-quarkus-quickfix | 1.1.0 | n/a | Preview | Open a Financial Interchange (FIX) session using an embedded QuickFix/J engine. |
| [Qute](extensions/qute.md) | camel-quarkus-qute | 1.0.0 | 1.0.0 | Stable | Transform messages using Quarkus Qute templating engine |
| [Reactive Executor](extensions/reactive-executor.md) | camel-quarkus-reactive-executor | 0.3.0 | 0.3.0 | Stable Deprecated | Reactive Executor for camel-core using Vert.x |
| [Reactive Streams](extensions/reactive-streams.md) | camel-quarkus-reactive-streams | 1.0.0 | 1.0.0 | Stable | Exchange messages with reactive stream processing libraries compatible with the reactive streams standard. |
| [Redis](extensions/redis.md) | camel-quarkus-redis | 1.6.0 | n/a | Preview | Aggregation repository using Redis as datastore |
| [Ref](extensions/ref.md) | camel-quarkus-ref | 1.0.0 | 1.0.0 | Stable | Route messages to an endpoint looked up dynamically by name in the Camel Registry. |
| [Rest](extensions/rest.md) | camel-quarkus-rest | 0.0.1 | 0.0.1 | Stable | Expose REST services and their OpenAPI Specification or call external REST services. |
| [REST OpenApi](extensions/rest-openapi.md) | camel-quarkus-rest-openapi | 1.0.0 | 1.0.0 | Stable | To call and expose REST services using OpenAPI specification as contract. |
| [Robot Framework](extensions/robotframework.md) | camel-quarkus-robotframework | 1.1.0 | n/a | Preview | Pass camel exchanges to acceptance test written in Robot DSL. |
| [RocketMQ](extensions/rocketmq.md) | camel-quarkus-rocketmq | 3.36.0 | 3.36.0 | Stable | Send and receive messages from RocketMQ cluster. |
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
| [Shiro](extensions/shiro.md) | camel-quarkus-shiro | 1.2.0 | 1.2.0 | Stable | Security using Shiro |
| [Simple JMS](extensions/sjms.md) | camel-quarkus-sjms | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from a JMS Queue or Topic using plain JMS 1.x API. |
| [Simple JMS2](extensions/sjms2.md) | camel-quarkus-sjms2 | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API. |
| [SimpleNotification](extensions/huaweicloud-smn.md) | camel-quarkus-huaweicloud-smn | 1.8.0 | n/a | Preview | To broadcast messages and connect cloud services through notifications on Huawei Cloud |
| [Slack](extensions/slack.md) | camel-quarkus-slack | 0.3.0 | 0.3.0 | Stable | Send and receive messages to/from Slack. |
| [SmallRye Reactive Messaging](extensions/smallrye-reactive-messaging.md) | camel-quarkus-smallrye-reactive-messaging | 1.0.0 | 1.0.0 | Stable | Camel integration with SmallRye Reactive Messaging |
| [SMB](extensions/smb.md) | camel-quarkus-smb | 3.7.0 | 3.7.0 | Stable | Read and write files to Server Message Block (SMB) file shares. |
| [Smooks](extensions/smooks.md) | camel-quarkus-smooks | 3.18.0 | n/a | Preview | Use Smooks to transform, route, and bind both XML and non-XML data, including EDI, CSV, JSON, and YAML. |
| [SMPP](extensions/smpp.md) | camel-quarkus-smpp | 1.1.0 | n/a | Preview | Send and receive SMS messages using a SMSC (Short Message Service Center). |
| [SnakeYAML](extensions/snakeyaml.md) | camel-quarkus-snakeyaml | 0.4.0 | 0.4.0 | Stable | Marshal and unmarshal Java objects to and from YAML using SnakeYAML |
| [SNMP](extensions/snmp.md) | camel-quarkus-snmp | 1.1.0 | n/a | Preview | Receive traps and poll SNMP (Simple Network Management Protocol) capable devices. |
| [SOAP dataformat](extensions/soap.md) | camel-quarkus-soap | 1.0.0 | 1.0.0 | Stable | Marshal Java objects to SOAP messages and back |
| [Solr](extensions/solr.md) | camel-quarkus-solr | 3.19.0 | 3.19.0 | Stable | Perform operations against Apache Lucene Solr. |
| [Splunk](extensions/splunk.md) | camel-quarkus-splunk | 1.8.0 | 1.8.0 | Stable Deprecated | Publish or search for events in Splunk. |
| [Splunk HEC](extensions/splunk-hec.md) | camel-quarkus-splunk-hec | 1.1.0 | 3.8.0 | Stable | The splunk component allows publishing events in Splunk using the HTTP Event Collector. |
| [Spring RabbitMQ](extensions/spring-rabbitmq.md) | camel-quarkus-spring-rabbitmq | 1.7.0 | 1.7.0 | Stable | Send and receive messages from RabbitMQ using the Spring RabbitMQ client. |
| [Spring Redis](extensions/spring-redis.md) | camel-quarkus-spring-redis | 3.6.0 | n/a | Preview | Send and receive messages from Redis. |
| [SQL](extensions/sql.md) | camel-quarkus-sql | 1.0.0 | 1.0.0 | Stable | Perform SQL queries. |
| [SSH](extensions/ssh.md) | camel-quarkus-ssh | 1.1.0 | 1.2.0 | Stable | Execute commands on remote hosts using SSH. |
| [StAX](extensions/stax.md) | camel-quarkus-stax | 1.1.0 | 1.7.0 | Stable | Process XML payloads by a SAX ContentHandler. |
| [Stitch](extensions/stitch.md) | camel-quarkus-stitch | 1.8.0 | n/a | Preview | Stitch is a cloud ETL service that integrates various data sources into a central data warehouse through various integrations. |
| [Stream](extensions/stream.md) | camel-quarkus-stream | 1.0.0 | 1.0.0 | Stable | Read from system-in and write to system-out and system-err streams. |
| [String Template](extensions/stringtemplate.md) | camel-quarkus-stringtemplate | 1.1.0 | 1.2.0 | Stable | Transform messages using StringTemplate engine. |
| [Stub](extensions/stub.md) | camel-quarkus-stub | 1.1.0 | n/a | Preview | Stub out any physical endpoints while in development or testing. |
| [SWIFT](extensions/swift.md) | camel-quarkus-swift | 3.2.0 | 3.2.0 | Stable | Encode and decode SWIFT messages. |
| [Syslog](extensions/syslog.md) | camel-quarkus-syslog | 1.1.0 | 1.7.0 | Stable | Marshall SyslogMessages to RFC3164 and RFC5424 messages and back |
| [Tar File](extensions/tarfile.md) | camel-quarkus-tarfile | 0.3.0 | 0.3.0 | Stable | Archive files into tarballs or extract files from tarballs |
| [Telegram](extensions/telegram.md) | camel-quarkus-telegram | 1.0.0 | 1.0.0 | Stable | Send and receive messages using the Telegram Bot API. |
| [Telemetry Dev](extensions/telemetry-dev.md) | camel-quarkus-telemetry-dev | 3.22.0 | 3.22.0 | Stable | Basic implementation of Camel Telemetry useful for development purposes |
| [ThreadPoolFactory Vert.x](extensions/threadpoolfactory-vertx.md) | camel-quarkus-threadpoolfactory-vertx | 1.0.0 | 1.0.0 | Stable Deprecated | ThreadPoolFactory for camel-core using Vert.x |
| [Thrift](extensions/thrift.md) | camel-quarkus-thrift | 1.1.0 | n/a | Preview | Call and expose remote procedures (RPC) with Apache Thrift data format and serialization mechanism. |
| [Tika](extensions/tika.md) | camel-quarkus-tika | 1.0.0 | 1.0.0 | Stable | Parse documents and extract metadata and text using Apache Tika. |
| [Timer](extensions/timer.md) | camel-quarkus-timer | 0.2.0 | 0.0.2 | Stable | Generate messages in specified intervals using java.util.Timer. |
| [TLS Registry](extensions/tls-registry.md) | camel-quarkus-tls-registry | 3.36.0 | 3.36.0 | Experimental | Configuration bridge for the Quarkus TLS registry and Camel SSLContextParameters |
| [Twilio](extensions/twilio.md) | camel-quarkus-twilio | 1.1.0 | 1.4.0 | Stable | Interact with Twilio REST APIs using Twilio Java SDK. |
| [Twitter](extensions/twitter.md) | camel-quarkus-twitter | 0.2.0 | 0.1.0 | Stable | Send tweets and receive tweets, direct messages and access Twitter Search |
| [uniVocity CSV](extensions/univocity-parsers.md) | camel-quarkus-univocity-parsers | 1.1.0 | 1.2.0 | Stable | Marshal and unmarshal Java objects from and to CSV (Comma Separated Values) using UniVocity Parsers. |
| [Validator](extensions/validator.md) | camel-quarkus-validator | 0.4.0 | 0.4.0 | Stable | Validate the payload using XML Schema and JAXP Validation. |
| [Velocity](extensions/velocity.md) | camel-quarkus-velocity | 1.1.0 | 1.2.0 | Stable | Transform messages using a Velocity template. |
| [Vert.x](extensions/vertx.md) | camel-quarkus-vertx | 1.0.0 | 1.0.0 | Stable | Send and receive messages to/from Vert.x Event Bus. |
| [Vert.x HTTP Client](extensions/vertx-http.md) | camel-quarkus-vertx-http | 1.1.0 | 1.1.0 | Stable | Send requests to external HTTP servers using Vert.x |
| [Vert.x WebSocket](extensions/vertx-websocket.md) | camel-quarkus-vertx-websocket | 1.1.0 | 1.1.0 | Stable | Expose WebSocket endpoints and connect to remote WebSocket servers using Vert.x |
| [Wasm](extensions/wasm.md) | camel-quarkus-wasm | 3.10.0 | 3.10.0 | Experimental | Invoke Wasm functions. |
| [Weather](extensions/weather.md) | camel-quarkus-weather | 1.1.0 | 1.1.0 | Stable | Poll the weather information from Open Weather Map. |
| [weaviate](extensions/weaviate.md) | camel-quarkus-weaviate | 3.24.0 | 3.24.0 | Stable | Perform operations on the Weaviate Vector Database. |
| [Web3j Ethereum Blockchain](extensions/web3j.md) | camel-quarkus-web3j | 1.1.0 | n/a | Preview | Interact with Ethereum nodes using web3j client API. |
| [Wordpress](extensions/wordpress.md) | camel-quarkus-wordpress | 1.1.0 | n/a | Preview | Manage posts and users using the WordPress API. |
| [Workday](extensions/workday.md) | camel-quarkus-workday | 1.1.0 | n/a | Preview | Detect and parse documents using Workday. |
| [XChange](extensions/xchange.md) | camel-quarkus-xchange | 1.1.0 | 2.0.0 | Stable | Access market data and trade on Bitcoin and Altcoin exchanges. |
| [XJ](extensions/xj.md) | camel-quarkus-xj | 1.1.0 | 3.7.0 | Stable | Transform JSON and XML message using a XSLT. |
| [XML IO DSL](extensions/xml-io-dsl.md) | camel-quarkus-xml-io-dsl | 1.8.0 | 1.8.0 | Stable | Camel XML DSL with camel-xml-io |
| [XML JAXB](extensions/xml-jaxb.md) | camel-quarkus-xml-jaxb | 1.0.0 | 1.0.0 | Stable | An XML stack for parsing XML route definitions. A legacy alternative to the fast an light weight camel-quarkus-xml-io-dsl |
| [XML JAXP](extensions/xml-jaxp.md) | camel-quarkus-xml-jaxp | 1.0.0 | 1.0.0 | Stable | XML JAXP type converters and parsers |
| [XML Security Sign](extensions/xmlsecurity.md) | camel-quarkus-xmlsecurity | 1.1.0 | 1.7.0 | Stable | Sign XML payloads using the XML signature specification. |
| [XMPP](extensions/xmpp.md) | camel-quarkus-xmpp | 1.1.0 | n/a | Preview | Send and receive messages to/from an XMPP chat server. |
| [XPath](extensions/xpath.md) | camel-quarkus-xpath | 1.0.0 | 1.0.0 | Stable | Evaluates an XPath expression against an XML payload |
| [XQuery](extensions/saxon.md) | camel-quarkus-saxon | 1.1.0 | 2.0.0 | Stable | Query and/or transform XML payloads using XQuery and Saxon. |
| [XSLT](extensions/xslt.md) | camel-quarkus-xslt | 0.4.0 | 0.4.0 | Stable | Transforms XML payload using an XSLT template. |
| [XSLT Saxon](extensions/xslt-saxon.md) | camel-quarkus-xslt-saxon | 1.1.0 | 3.2.0 | Stable | Transform XML payloads using an XSLT template using Saxon. |
| [YAML DSL](extensions/yaml-dsl.md) | camel-quarkus-yaml-dsl | 1.8.0 | 1.8.0 | Stable | Camel YAML DSL |
| [YAML IO](extensions/yaml-io.md) | camel-quarkus-yaml-io | 3.2.0 | 3.2.0 | Stable | Camel YAML IO |
| [Zendesk](extensions/zendesk.md) | camel-quarkus-zendesk | 1.1.0 | 1.4.0 | Stable | Manage Zendesk tickets, users, organizations, etc. |
| [Zip Deflate Compression](extensions/zip-deflater.md) | camel-quarkus-zip-deflater | 1.0.0 | 1.0.0 | Stable | Compress and decompress streams using java.util.zip.Deflater, java.util.zip.Inflater or java.util.zip.GZIPStream. |
| [Zip File](extensions/zipfile.md) | camel-quarkus-zipfile | 0.2.0 | 0.2.0 | Stable | Compression and decompress streams using java.util.zip.Zip\*Stream |
| [ZooKeeper](extensions/zookeeper.md) | camel-quarkus-zookeeper | 1.1.0 | n/a | Preview | Manage ZooKeeper clusters. |
| [ZooKeeper Master](extensions/zookeeper-master.md) | camel-quarkus-zookeeper-master | 1.1.0 | n/a | Preview | Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies. |