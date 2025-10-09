# Camel K Integration Scaling

## Manual Scaling

An Integration can be scaled using the `kubectl scale` command, e.g.:

```console
$ kubectl scale it <integration_name> --replicas <number_of_replicas>
```

This can also be achieved by editing the Integration resource directly, e.g.:

```console
$ kubectl patch it <integration_name> -p '{"spec":{"replicas":<number_of_replicas>}}'
```

The Integration also reports its number of replicas in the `.status.replicas` field, e.g.:

```console
$ kubectl get it <integration_name> -o jsonpath='{.status.replicas}'
```

## Autoscaling with Keda

If you have Keda operator you can leverage scaling (and serverless if you need to) on those services such as queues and databases which can be watched by Keda (see a list of [available scalers](https://keda.sh/docs/2.17/scalers/)). Each scaler has a different configuration, we will use here `kafka` as a reference. Let’s consider the following consumer:

```yaml
  - route:
      from:
        steps:
        - to: log:info
        uri: kafka:my-topic?brokers=my-cluster-kafka-bootstrap.strimzi.svc%3A9092&groupId=group-1
```

We can include a Keda trait configuration to scale it down to 0 when there is no traffic on the topic:

```yaml
apiVersion: camel.apache.org/v1
kind: Integration
metadata:
  name: keda-kafkatopic-to-log
  namespace: kafka
spec:
  flows:
  - route:
      from:
        steps:
        - to: log:info
        uri: kafka:my-topic?brokers=my-cluster-kafka-bootstrap.strimzi.svc%3A9092&groupId=group-1
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
            bootstrapServers: my-cluster-kafka-bootstrap.strimzi.svc:9092
            consumerGroup: group-1
            topic: my-topic
            lagThreshold: "10"
```

We have instructed the Integration to have max one replica running and 0 (serverless), when there are no events (`lagThreshold: "10"`) on the given topic.

## Autoscaling with Knative

An Integration that deploys as a Knative Service can automatically scale based on _incoming_ traffic, including scaling to zero.

The _incoming_ traffic measures either as:

-   The number of simultaneous requests, that are processed by each replica at any given time;
    
-   Or the number of requests that are processed per second, per replica.
    

That implies the Integration must expose a container port, that receives incoming requests, and complies with the [Knative runtime contract](https://github.com/knative/specs/blob/main/specs/serving/runtime-contract.md#protocols-and-ports). This is the case when the Integration either:

-   Exposes an HTTP endpoint, using the Camel HTTP component or the REST DSL, e.g.:
    
    ```javascript
    rest('/')
      .produces("text/plain")
      .get()
        .route()
        .transform().constant("Response");
    ```
    
-   Or consumes Knative events, from a Broker or a Channel, using the Knative component, e.g.:
    
    ```java
    from("knative:channel/events")
      .convertBodyTo(String.class)
      .to("log:info")
    ```
    

The Knative [_Autoscaler_](https://knative.dev/docs/serving/autoscaling/autoscaling-concepts/#supported-autoscaler-types) can be configured using the [Knative Service](../traits/knative-service.md) trait, e.g., to set the scaling upper bound (the maximum number of replicas):

```console
$ kamel run -t knative-service.max-scale=10
```

More information can be found in the Knative [Autoscaling](https://knative.dev/docs/serving/autoscaling/) documentation.

> **Note**
> When [manually scaling](#_manual_scaling) an Integration, that deploys as a Knative Service, both [scale bounds](https://knative.dev/docs/serving/autoscaling/scale-bounds/), i.e., `minScale` and `maxScale`, are set to the specified number of replicas. Scale bounds can be reset by removing the `.spec.replicas` field from the Integration, e.g., with:
>
> ```console
> $ kubectl patch it <integration_name> --type=json -p='[{"op": "remove", "path": "/spec/replicas"}]'
> ```

## Autoscaling with HPA

An Integration can automatically scale based on its CPU utilization and custom metrics using [horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/).

For example, executing the following command creates an _autoscaler_ for the Integration, with target CPU utilization set to 80%, and the number of replicas between 2 and 5:

```console
$ kubectl autoscale it <integration_name> --min=2 --max=5 --cpu-percent=80
```

[Integration metrics](../observability/monitoring/integration.md) can also be exported for horizontal pod autoscaling (HPA), using the [custom metrics Prometheus adapter](https://github.com/DirectXMan12/k8s-prometheus-adapter), so that the Integration can scale automatically based on its own metrics.

If you have an OpenShift cluster, you can follow [Exposing custom application metrics for autoscaling](https://docs.openshift.com/container-platform/4.4/monitoring/exposing-custom-application-metrics-for-autoscaling.md) to set it up.

Assuming you have the Prometheus adapter up and running, you can create a `HorizontalPodAutoscaler` resource based on a particular Integration metric, e.g.:

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: camel-k-autoscaler
spec:
  scaleTargetRef:
    apiVersion: camel.apache.org/v1
    kind: Integration
    name: example
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Pods
    pods:
      metric:
        name: application_camel_context_exchanges_inflight_count
      target:
        type: AverageValue
        averageValue: 1k
```

> **Warning**
> the HPA can work when the Integration replica field needs to be specified. You need to scale the Integration via `kubectl scale it my-it --replicas 1` or edit the `.spec.replicas` field of your Integration to 1. This is due to a [Kubernetes behavior which does not allow an empty value on the resource to scale](https://github.com/kubernetes/kubernetes/issues/111781).

More information can be found in [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) from the Kubernetes documentation.

> **Note**
> HPA can also be used with Knative, by installing the [HPA autoscaling Serving extension](https://knative.dev/docs/install/install-extensions/#install-optional-serving-extensions).