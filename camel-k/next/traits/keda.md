# Keda Trait

The KEDA trait allows you to configure KEDA autoscalers to scale up and down based of events.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait keda.[key]=[value] --trait keda.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `keda.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `keda.pollingInterval` | `int32` | Interval (seconds) to check each trigger on. |
| `keda.cooldownPeriod` | `int32` | The wait period between the last active trigger reported and scaling the resource back to 0. |
| `keda.idleReplicaCount` | `int32` | Enabling this property allows KEDA to scale the resource down to the specified number of replicas. |
| `keda.minReplicaCount` | `int32` | Minimum number of replicas. |
| `keda.maxReplicaCount` | `int32` | Maximum number of replicas. |
| `keda.triggers` | `[]github.com/apache/camel-k/v2/pkg/apis/camel/v1/trait.KedaTrigger` | Definition of triggers according to the KEDA format. Each trigger must contain `type` field corresponding to the name of a KEDA autoscaler and a key/value map named `metadata` containing specific trigger options and optionally a mapping of secrets, used by Keda operator to poll resources according to the autoscaler type. |
| `keda.auto` | `bool` | Automatically discover KEDA triggers from Camel component URIs. |
| `keda.autoMetadata` | `map[string]map[string]string` | Additional metadata to merge into auto-discovered triggers. Keys are trigger types (e.g., "kafka"), values are maps of metadata key-value pairs to merge (e.g., {"lagThreshold": "10"}). |
> **Note**
> the variable names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`

## Automatic scaler discovery

When `keda.auto` is enabled, Camel K inspects the consumer endpoints in an Integration and creates KEDA triggers for components with a registered scaler mapping. A scaler is the KEDA adapter that reads metrics from an external system and uses them to determine when a workload should scale. See the [KEDA scaler concepts](https://keda.sh/docs/latest/concepts/scaling-deployments/) documentation for more information.

Automatic discovery currently supports the following Camel components:

-   `activemq`: creates an Apache ActiveMQ trigger from destination and broker values in the endpoint URI. See the [KEDA Apache ActiveMQ scaler](https://keda.sh/docs/latest/scalers/activemq/) documentation for the available trigger metadata.
    
-   `kafka`: creates an Apache Kafka trigger from the topic, broker, and consumer-group values in the endpoint URI. See the [KEDA Apache Kafka scaler](https://keda.sh/docs/latest/scalers/apache-kafka/) documentation for the available trigger metadata.
    
-   `aws2-sqs`: creates an AWS SQS Queue trigger. `queueURL` comes from the `queueUrl` endpoint parameter, or is built from a queue ARN, or from the queue name with the `region` and `queueOwnerAWSAccountId` parameters. Otherwise the plain queue name is used, which KEDA accepts when it is unambiguous. `awsRegion` comes from `region` or the ARN, and `awsEndpoint` from `uriEndpointOverride` when `overrideEndpoint=true`. Set other metadata, such as `queueLength`, with `keda.autoMetadata`, and credentials with a KEDA `TriggerAuthentication`. See the [KEDA AWS SQS Queue scaler](https://keda.sh/docs/latest/scalers/aws-sqs/) documentation for the available trigger metadata.
    
-   `pulsar`: creates an Apache Pulsar trigger from the topic in the endpoint URI and the `subscriptionName` option (Camel’s default `subs` when it is not set). When the service URL (`serviceUrl` option or `camel.component.pulsar.service-url` property) uses the `pulsar://` scheme, `adminURL` is set to `[http://<host>:8080](http://\<host\>:8080)`; for TLS or a custom admin port, set it with `keda.autoMetadata`. See the [KEDA Apache Pulsar scaler](https://keda.sh/docs/latest/scalers/pulsar/) documentation for the available trigger metadata.
    
-   `spring-rabbitmq`: creates a RabbitMQ trigger whose `queueName` is the `queues` value of the endpoint URI, when it names a single queue. The broker address is not part of the URI: a `host` endpoint parameter, when present, is used as the trigger `host` as is; otherwise set `host`, together with `mode` and `value`, with `keda.autoMetadata`. See the [KEDA RabbitMQ Queue scaler](https://keda.sh/docs/latest/scalers/rabbitmq-queue/) documentation for the available trigger metadata.
    

Unsupported Camel components do not produce an automatically discovered trigger. You can still configure their KEDA triggers explicitly with `keda.triggers`.