# Camel Testing plugin

Write and run automated tests for Camel integrations using the [Citrus](https://citrusframework.org/) test framework.

Enable the plugin:

```bash
camel plugin add test
```

> **Tip**
> Run `camel test --help` to see all available subcommands.

## Initialize tests

Create an empty test file as a starting point:

```bash
camel test init route-test.yaml
```

The file extension determines the test language: YAML, Java, XML, or Cucumber (`.feature`).

> **Note**
> Tests are created in a `test` subfolder to separate them from runtime sources. You don’t need to navigate there — the plugin handles the working directory automatically.

## Run tests

Run tests locally with JUnit Jupiter — no project setup needed:

```bash
camel test run route-test.yaml
```

## Project export

When you export a project, the test plugin automatically includes test resources as test-scoped Maven dependencies in `src/test/java` and `src/test/resources`:

```bash
camel export route.yaml --dir my-export --runtime quarkus
cd my-export
./mvnw verify
```

> **Tip**
> The export creates a JUnit Jupiter test class in `src/test/java` that you can also run from your IDE.

## Dependency management

Basic Citrus dependencies are included out of the box. For additional modules (Kafka, Testcontainers, etc.), add them in a `jbang.properties` file next to the test source:

jbang.properties

```properties
run.deps=org.citrusframework:citrus-camel:4.7.0,\
org.citrusframework:citrus-kafka:4.7.0,\
org.citrusframework:citrus-testcontainers:4.7.0,\
org.apache.camel:camel-endpointdsl:4.13.0,\
org.apache.camel:camel-aws2-s3:4.13.0

run.D=citrus.camel.jbang.dump.integration.output=true
```

> **Tip**
> These dependencies are automatically added as test-scoped dependencies during project export.

## Writing tests with Citrus

The test plugin uses [Citrus](https://citrusframework.org/) as the underlying test framework. A typical test:

1.  Starts infrastructure (Kafka, database, etc.)
    
2.  Launches the Camel integration with test configuration
    
3.  Sends messages to trigger route logic
    
4.  Verifies the outcome
    

For full details, see the [Citrus documentation](https://citrusframework.org/citrus/reference/html/).

### Using infrastructure services

Start Camel infra services or Testcontainers as part of the test:

```yaml
actions:
  - camel:
      infra:
        run:
          service: postgres
  - testcontainers:
      start:
        kafka: {}
```

Connection settings are exposed as test variables (`CITRUS_CAMEL_INFRA_SERVICE_<NAME>_<PROP>` or `CITRUS_TESTCONTAINERS_<NAME>_<PROP>`) for use in `application.properties`:

```properties
camel.database.url=${CITRUS_CAMEL_INFRA_POSTGRES_SERVICE_ADDRESS}
camel.kafka.bootstrapServers=${CITRUS_TESTCONTAINERS_KAFKA_BOOTSTRAP_SERVERS}
```

See [Camel infra](https://citrusframework.org/citrus/reference/html/#camel-infra) and [Testcontainers](https://citrusframework.org/citrus/reference/html/#testcontainers) in the Citrus docs.

### Running the Camel integration

Launch a Camel integration as a separate process with test-specific configuration:

```yaml
actions:
  - camel:
      jbang:
        run:
          integration:
            file: "../route.yaml"
            systemProperties:
              file: "application.test.properties"
```

> **Tip**
> The path uses `../` because tests are in the `test` subfolder.

See [Camel CLI support in Citrus](https://citrusframework.org/citrus/reference/html/#apache-camel).

### Sending and receiving messages

Citrus supports Kafka, HTTP, SOAP, FTP, JMS, and many more transports:

Send to Kafka

```yaml
actions:
  - send:
      endpoint: "kafka:bookings"
      message:
        body:
          data: |
            { "client": "camel-batch", "product": "Orange", "amount": 200, "price": 1.0, "status": "APPROVAL_REQUIRED" }
        headers:
          - name: "citrus_kafka_messageKey"
            value: "bookings.csv_0"
```

Verify received message

```yaml
actions:
  - receive:
      endpoint: "kafka:reports"
      message:
        body:
          data: |
            { "bookings": { "completed": 1, "errors": 0 } }
```

You can also use any Camel endpoint URI directly (e.g., `camel:aws2-s3:my-bucket?amazonS3Client=#s3Client`). Bean references (`#beanName`) and Citrus test variables work in endpoint URIs.

See [send/receive actions](https://citrusframework.org/citrus/reference/html/#actions-send) and [message endpoints](https://citrusframework.org/citrus/reference/html/#endpoints) in the Citrus docs.