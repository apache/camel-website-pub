# Camel Quarkus Examples

We offer several examples in [Camel Quarkus examples repository](https://github.com/apache/camel-quarkus-examples). To learn how to use them, please follow the [First steps](first-steps.md) chapter of the User guide.

Number of Examples: 33

 
| Example | Description |
| --- | --- |
| [AMQP](https://github.com/apache/camel-quarkus-examples/tree/main/amqp) | Shows how to produce and consume messages to an ActiveMQ Artemis broker using AMQP. |
| [Artemis to ElasticSearch](https://github.com/apache/camel-quarkus-examples/tree/main/artemis-elasticsearch) | Shows how the message is consumed from the Apache Artemis broker using MQTT protocol, transformed and loaded into ElasticSearch |
| [Camel Quarkus CXF SOAP example](https://github.com/apache/camel-quarkus-examples/tree/main/cxf-soap) | Shows how to use Camel CXF SOAP component. |
| [Communication with Netty over TCP](https://github.com/apache/camel-quarkus-examples/tree/main/netty-custom-correlation) | Shows how to use TCP communication with Netty using a custom codec to encode and decode the data over the wire. |
| [Custom `main()`](https://github.com/apache/camel-quarkus-examples/tree/main/timer-log-main) | Shows how to start Camel from a custom `main()` method |
| [Deploying a Camel Route in AWS Lambda](https://github.com/apache/camel-quarkus-examples/tree/main/aws-lambda) | Shows how to deploy a Camel Quarkus route as an AWS Lambda function |
| [Extract, Transform and Load between two databases](https://github.com/apache/camel-quarkus-examples/tree/main/jdbc-datasource) | Shows how to extract, transform and load between two databases |
| [FHIR](https://github.com/apache/camel-quarkus-examples/tree/main/fhir) | Shows how to use Camel FHIR with Quarkus. |
| [File consumer with Bindy & FTP](https://github.com/apache/camel-quarkus-examples/tree/main/file-bindy-ftp) | Shows how to consume CSV files, marshal & unmarshal the data and send it onwards via FTP |
| [HTTP with Post-Quantum Cryptography (PQC) (Java 17)](https://github.com/apache/camel-quarkus-examples/tree/main/http-pqc-j17) | Shows how to implement quantum-resistant authentication using hybrid certificates that combine RSA with post-quantum ML-DSA-65 signatures on Java 17 using application-level validation |
| [HTTP with Post-Quantum Cryptography (PQC) (Java 21)](https://github.com/apache/camel-quarkus-examples/tree/main/http-pqc-j21) | Shows how to implement quantum-resistant TLS using Java 21 with BouncyCastle JSSE provider for native PQC support with hybrid cipher suites |
| [HTTP with vanilla JAX-RS or with Camel `platform-http` component](https://github.com/apache/camel-quarkus-examples/tree/main/http-log) | Shows how to create HTTP endpoints using either the RESTEasy |
| [Health](https://github.com/apache/camel-quarkus-examples/tree/main/health) | Shows how to use Camel health-checks with Quarkus. |
| [JMS and JPA](https://github.com/apache/camel-quarkus-examples/tree/main/jms-jpa) | Shows how to run a Camel Quarkus application that supports JTA transactions on three external transactional resources: a database (MySQL), a messaging broker (Artemis) and a simulated XAResource which can demonstrate the commit, rollback and crash recovery. |
| [JPA idempotent repository](https://github.com/apache/camel-quarkus-examples/tree/main/jpa-idempotent-repository) | Shows how to consume a message only once, even when the message is delivered multiple times |
| [JTA and JPA](https://github.com/apache/camel-quarkus-examples/tree/main/jta-jpa) | Shows how to run a Camel Quarkus application that supports JTA transactions on two external transactional resources: a database (MySQL) and a simulate XAResource which can demonstrate the commit, rollback and crash recovery. |
| [Kafka example](https://github.com/apache/camel-quarkus-examples/tree/main/kafka) | Shows how to produce and consume messages in a Kafka topic, using Strimzi Operator |
| [Kamelet Chuck Norris](https://github.com/apache/camel-quarkus-examples/tree/main/kamelet-chucknorris) | Shows how you can build a simple Kamelet and use with your Camel applications. |
| [Leader election in Kubernetes: A Camel Quarkus Master example](https://github.com/apache/camel-quarkus-examples/tree/main/cluster-leader-election) | Shows how to use Camel master component. |
| [Message Bridge](https://github.com/apache/camel-quarkus-examples/tree/main/message-bridge) | Shows how to configure AMQ and IBM MQ clients to use the connection pooling and XA transactions. |
| [Observability](https://github.com/apache/camel-quarkus-examples/tree/main/observability) | Demonstrates how to add support for metrics, health checks and distributed tracing |
| [OpenAPI Contract First](https://github.com/apache/camel-quarkus-examples/tree/main/openapi-contract-first) | Shows how to run with Contract First OpenAPI. |
| [Platform HTTP security with Keycloak](https://github.com/apache/camel-quarkus-examples/tree/main/platform-http-security-keycloak) | Shows how to secure platform HTTP with Keycloak |
| [REST with Jackson](https://github.com/apache/camel-quarkus-examples/tree/main/rest-json) | Demonstrates how to create a REST service using the Camel REST DSL and Jackson. |
| [REST with Jackson: A Quarkus based example](https://github.com/apache/camel-quarkus-examples/tree/main/quarkus-rest-json) | Demonstrates how to use REST (Jackson) endpoints from a Quarkus project and invoke Camel routes. |
| [Saga and LRA](https://github.com/apache/camel-quarkus-examples/tree/main/saga) | Shows how to use saga and lra |
| [Send and receive messages from Redis](https://github.com/apache/camel-quarkus-examples/tree/main/spring-redis) | Shows how to produce and consume messages from Redis, using both basic operations and pub/sub messaging. |
| [Timer Hello World](https://github.com/apache/camel-quarkus-examples/tree/main/timer-log) | Uses the Camel timer component to output a Hello world message to the console |
| [Tokenize a CSV file](https://github.com/apache/camel-quarkus-examples/tree/main/file-split-log-xml) | Shows how to define a Camel route in XML for tokenizing a CSV a file. |
| [Unstructured Data Extraction with LangChain4j](https://github.com/apache/camel-quarkus-examples/tree/main/data-extract-langchain4j) | Shows how to convert unstructured text data to structured Java objects helped with a Large Language Model and LangChain4j |
| [Upload a file to an AWS S3 bucket](https://github.com/apache/camel-quarkus-examples/tree/main/aws2-s3) | Shows how to produce and consume messages to an aws2-s3 bucket. |
| [Variables](https://github.com/apache/camel-quarkus-examples/tree/main/variables) | Uses the Camel variables which can be configured from application.properties. |
| [Vertx-Websocket Chat](https://github.com/apache/camel-quarkus-examples/tree/main/vertx-websocket-chat) | Shows how to configure a WebSocket server and interact with connected peers. |