# Camel K Pipe Scaling

## Manual Scaling

A Pipe can be scaled using the `kubectl scale` command, e.g.:

```console
$ kubectl scale pipe <pipe_name> --replicas <number_of_replicas>
```

This can also be achieved by editing the Pipe resource directly, e.g.:

```console
$ kubectl patch pipe <pipe_name> -p '{"spec":{"replicas":<number_of_replicas>}}'
```

The Pipe also reports its number of replicas in the `.status.replicas` field, e.g.:

```console
$ kubectl get pipe <pipe_name> -o jsonpath='{.status.replicas}'
```

## Autoscaling with Keda

If you have Keda operator you can leverage scaling (and serverless if you need to) on those services such as queues and databases which can be watched by Keda (see a list of [available scalers](https://keda.sh/docs/2.17/scalers/)). Each scaler has a different configuration, we will use here `kafka` as a reference. Let’s consider the following consumer:

```yaml
spec:
  sink:
    uri: log:info
  source:
    ref:
      kind: KafkaTopic
      apiVersion: kafka.strimzi.io/v1beta2
      name: my-topic
    properties:
      groupId: group-1
```

We can include a Keda trait configuration to scale it down to 0 when there is no traffic on the topic:

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: keda-kafkatopic-to-log
  namespace: kafka
spec:
  sink:
    uri: log:info
  source:
    ref:
      kind: KafkaTopic
      apiVersion: kafka.strimzi.io/v1beta2
      name: my-topic
    properties:
      groupId: group-1
  traits:
    keda:
      enabled: true
      minReplicaCount: 0
      maxReplicaCount: 1
      cooldownPeriod:  20
      pollingInterval: 10
      triggers:
        - type: kafka
          metadata:
            bootstrapServers: my-cluster-kafka-bootstrap.kafka.svc:9092
            consumerGroup: group-1
            topic: my-topic
            lagThreshold: "10"
```

We have instructed the Pipe to have max one replica running and 0 (serverless), when there are no events (`lagThreshold: "10"`) on the given topic.

## Autoscaling with Knative

A Pipe that binds an HTTP-based source Kamelet can automatically scale based on _incoming_ traffic when installed on a cluster with _Knative_ enabled, including scaling to zero.

The _incoming_ traffic measures either as:

-   The number of simultaneous requests, that are processed by each replica at any given time;
    
-   Or the number of requests that are processed per second, per replica.
    

The `webhook-source` Kamelet is one of the sources that enables auto-scaling when used in a Pipe:

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: webhook-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1
      name: webhook-source
  sink:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1
      name: log-sink
```

The Knative [_Autoscaler_](https://knative.dev/docs/serving/autoscaling/autoscaling-concepts/#supported-autoscaler-types) can be configured using the [Knative Service](../traits/knative-service.md) trait, e.g., to set the scaling upper bound (the maximum number of replicas):

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: webhook-binding
spec:
  integration:
      traits:
        knative-service:
          configuration:
            maxScale: 10
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1
      name: webhook-source
  sink:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1
      name: log-sink
```

More information can be found in the Knative [Autoscaling](https://knative.dev/docs/serving/autoscaling/) documentation.

> **Note**
> When [manually scaling](#_manual_scaling) a Pipe that deploys as a Knative Service, both [scale bounds](https://knative.dev/docs/serving/autoscaling/scale-bounds/), i.e., `minScale` and `maxScale`, are set to the specified number of replicas. Scale bounds can be reset by removing the `.spec.replicas` field from the Pipe, e.g., with:
>
> ```console
> $ kubectl patch pipe <pipe_name> --type=json -p='[{"op": "remove", "path": "/spec/replicas"}]'
> ```

## Autoscaling with HPA

A Pipe can automatically scale based on its CPU utilization and custom metrics using [horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/).

For example, executing the following command creates an _autoscaler_ for the Pipe, with target CPU utilization set to 80%, and the number of replicas between 2 and 5:

> **Warning**
> For the HPA to work, the Pipe replica field must be specified. You need to scale the Pipe via `kubectl scale pipe my-pipe --replicas 1` or edit the `.spec.replicas` field of your Pipe to 1. This is due to a [Kubernetes behavior which does not allow an empty value on the resource to scale](https://github.com/kubernetes/kubernetes/issues/111781).

```console
$ kubectl autoscale pipe <pipe_name> --min=2 --max=5 --cpu-percent=80
```

Refer to the [Integration scaling](integration.md) guide for information about using custom metrics.

> **Note**
> HPA can also be used with Knative, by installing the [HPA autoscaling Serving extension](https://knative.dev/docs/install/install-extensions/#install-optional-serving-extensions).